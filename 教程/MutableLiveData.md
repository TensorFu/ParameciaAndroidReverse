## MutableLiveData

### 一个可以直接运行的案例

​			

CounterViewModel.java

```java
package com.open.ok;
import androidx.lifecycle.MutableLiveData;
import androidx.lifecycle.ViewModel;

public class CounterViewModel extends ViewModel {
    private final MutableLiveData<Integer> counter = new MutableLiveData<>(0);

    public MutableLiveData<Integer> getCounter() {
        return counter;
    }

    public void incrementCounter() {
        Integer currentCounter = counter.getValue();
        if (currentCounter != null) {
            counter.setValue(currentCounter + 1);
        }
    }
}

```

​			

MainActivity.java

```java
package com.open.ok;

import androidx.appcompat.app.AppCompatActivity;
import androidx.lifecycle.ViewModelProvider;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

import com.open.ok.databinding.ActivityMainBinding;

public class MainActivity extends AppCompatActivity {
    private CounterViewModel viewModel;

    // Used to load the 'ok' library on application startup.
    static {
        System.loadLibrary("ok");
    }

    private ActivityMainBinding binding;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        binding = ActivityMainBinding.inflate(getLayoutInflater());
        setContentView(binding.getRoot());

        // Example of a call to a native method
        TextView tv = binding.sampleText;
        tv.setText(stringFromJNI());

        TextView counterText = findViewById(R.id.counterText);  // 假设你的布局中有一个ID为counterText的TextView
        Button incrementButton = findViewById(R.id.incrementButton);  // 假设你的布局中有一个ID为incrementButton的Button

        viewModel = new ViewModelProvider(this).get(CounterViewModel.class);

        // 观察计数器的变化
        viewModel.getCounter().observe(this, counterValue -> {
            counterText.setText(String.valueOf(counterValue));
        });

        // 按钮点击事件
        incrementButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                viewModel.incrementCounter();
            }
        });
    }

    /**
     * A native method that is implemented by the 'ok' native library,
     * which is packaged with this application.
     */
    public native String stringFromJNI();
}
```

​			

不使用 lambda 表达式的写法

```Java
        viewModel = new ViewModelProvider(this).get(CounterViewModel.class);

        // 观察计数器的变化
        viewModel.getCounter().observe(this, new Observer<Integer>() {
            @Override
            public void onChanged(Integer counterValue) {
                counterText.setText(String.valueOf(counterValue));
            }
        });
```

​				

activity_main.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/sample_text"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello World!"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <TextView
        android:id="@+id/counterText"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="100dp"
        android:text="0"
        android:textSize="24sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"/>

    <Button
        android:id="@+id/incrementButton"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/counterText"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="50dp"
        android:text="Increment Counter"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.497"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.287" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

​				

