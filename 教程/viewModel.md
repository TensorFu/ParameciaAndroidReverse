## viewModel

其本质是一个数据持有类，他是一个持有存储一个 View 的数据的一个类

### 一个案例

> 这是一个可以直接贴进 android studio 当中直接运行的代码

CounterViewModel.java

```java
package com.open.ok;

import androidx.lifecycle.ViewModel;

public class CounterViewModel extends ViewModel {
    private int counter = 0;

    public int getCounter() {
        return counter;
    }

    public void incrementCounter() {
        this.counter++;
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

        viewModel = new ViewModelProvider(this).get(CounterViewModel.class);

        final TextView counterTextView = findViewById(R.id.tv_counter);
        Button incrementButton = findViewById(R.id.btn_increment);

        // 设置初始值
        counterTextView.setText("Counter: " + viewModel.getCounter());

        incrementButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                viewModel.incrementCounter();
                counterTextView.setText("Counter: " + viewModel.getCounter());
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

最关键的就是

`viewModel = new ViewModelProvider(this).get(CounterViewModel.class);` 			

通过这一行代码得到这个数据持有类			

​				

布局文件 activity_main.xml

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
        android:id="@+id/tv_counter"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerHorizontal="true"
        android:text="Counter: 0"
        android:textSize="24sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.521"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.648"
        tools:ignore="MissingConstraints" />

    <Button
        android:id="@+id/btn_increment"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/tv_counter"
        android:layout_centerHorizontal="true"
        android:text="Increment"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.498"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.36"
        tools:ignore="MissingConstraints" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

​			



