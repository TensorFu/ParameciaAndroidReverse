## LiveData



### LiveData 简介

（简而言之就是，一个能够在 activity之间，Fragment之间，ViewModel之间，或者他们相互之间，实时更新，实时共享的数据，类似于多线程的，共享数据）

LiveData 是 Android Jetpack 构件库中的一个核心组件，它是一个**可观察的数据持有者类**，可用于在应用程序的不同组件（如 Activity、Fragment 或 ViewModel）之间共享和观察数据。LiveData 遵循观察者模式，使 UI 组件（如 Activity 或 Fragment）能够在数据更改时自动更新。这有助于实现更简洁、可维护和可测试的代码。



**可观察的数据持有者类** 是什么意思？
我们首先看，数据持有类，所谓的数据持有类，意思就是，他是一个存放数据的类，不是用来处理逻辑的类						

可观察是什么意思？简单理解就是，这个数据持有类他是一个可以被监控的，他里面的数据的变动，会影响其他的组件						

​					

**LiveData 的特点**

1. **确保 UI 与数据状态一致**：因为 LiveData 遵循观察者模式，所以当数据更改时，所有订阅的 UI 组件都会自动更新。
2. **生命周期感知**：LiveData 是生命周期感知的，这意味着它会自动管理观察者的订阅，确保只在活跃的生命周期（如 Activity 处于 started 或 resumed 状态）时更新 UI。这样可以避免在不活跃的生命周期（如 Activity 处于 paused 或 stopped 状态）中进行不必要的 UI 更新，从而提高性能。
3. **无内存泄漏**：由于 LiveData 会自动管理订阅，所以在组件（如 Activity 或 Fragment）销毁时不会造成内存泄漏。
4. **数据共享**：LiveData 可以在不同组件之间轻松共享数据，特别是与 ViewModel 一起使用时，可以实现 UI 逻辑与数据处理逻辑的解耦。

​			

可以了解到 **LiveData** 的最主要的作用是，共享数据，并且是共享实时数据，但是我们在前面的学习当中就已经学习了，通过多线程的数据共享的方式进行共享数据，为什么还需要这个东西？				

而 **LiveData 提供的数据共享是指在应用程序的不同组件**（如 Activity、Fragment 或 ViewModel）之间共享和观察数据。LiveData 的数据共享关注的是组件间的数据传递，以及在数据变化时自动更新 UI。LiveData 的优势在于生命周期感知、自动管理观察者订阅、避免内存泄漏等。

​					



### 实例代码_观察单个变量的变化

这是一个完整的实例，可以直接贴在你的 android studio 当中执行

User.java

```java
package com.open.ok;

public class User {
    private String name;

    public User(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
```

这就是一个数据持有类，他的作用就是持有一个数据，用来存储一个数据

在这里我们存放一个，用户的信息，这个用户信息只包含一项，那就是用户的姓名			

​			

UserRepository.java	

```java
package com.open.ok;

import java.util.concurrent.Executor;
import java.util.concurrent.Executors;

// UserRepository.java
public class UserRepository {
    private static UserRepository instance;
    private final Executor executor = Executors.newSingleThreadExecutor(); // 模拟后台线程

    public static UserRepository getInstance() {
        if (instance == null) {
            instance = new UserRepository();
        }
        return instance;
    }

    public void getUser(final UserDataCallback callback) {
        // 模拟异步获取数据
        executor.execute(new Runnable() {
            @Override
            public void run() {
                try {
                    Thread.sleep(2000);  // 模拟网络延迟
                    User user = new User("John Doe");
                    callback.onDataLoaded(user);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });
    }

    public interface UserDataCallback {
        void onDataLoaded(User user);
    }
}
```

- `UserRepository`模拟了一个数据源。在真实的应用程序中，这可能是从网络或数据库获取数据。
- `getUser()`方法是调用后台任务以异步获取用户数据的地方。这里，我们只是模拟了这个操作。
- `executor.execute()`用于异步运行代码块。
- 在此代码块中，我们模拟了网络延迟，然后创建了一个新的`User`对象并通过回调返回

​				

UserViewModel.java

```java
package com.open.ok;

import androidx.lifecycle.LiveData;
import androidx.lifecycle.ViewModel;

// UserViewModel.java
public class UserViewModel extends ViewModel {
    private final UserNameLiveData userNameLiveData = new UserNameLiveData();

    public LiveData<String> getUserName() {
        return userNameLiveData;
    }

    public void loadUserData() {
        UserRepository.getInstance().getUser(new UserRepository.UserDataCallback() {
            @Override
            public void onDataLoaded(User user) {
                userNameLiveData.updateData(user.getName());
            }
        });
    }

    static class UserNameLiveData extends LiveData<String> {
        public void updateData(String data) {
            postValue(data); // 此处调用是合法的，因为我们在 LiveData 的子类中
        }
    }
}
```

注意：这里的 LiveData 传进去的数据有两种方式，第一种方式是，setValue() 的方式，这种方式其实几乎可以忽略，因为他只能在主线程当中使用，而我们的 postValue 是一个可以再任何

​			

MainActivity.java

```java
package com.open.ok;

import androidx.appcompat.app.AppCompatActivity;
import androidx.lifecycle.ViewModelProvider;

import android.os.Bundle;
import android.widget.Button;
import android.widget.TextView;

import com.open.ok.databinding.ActivityMainBinding;

public class MainActivity extends AppCompatActivity {
    private UserViewModel viewModel;

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

        final TextView userNameTextView = findViewById(R.id.userNameTextView);
        Button loadDataButton = findViewById(R.id.loadDataButton);

        viewModel = new ViewModelProvider(this).get(UserViewModel.class);
        viewModel.getUserName().observe(this, new androidx.lifecycle.Observer<String>() {
            @Override
            public void onChanged(String userName) {
                userNameTextView.setText(userName);
            }
        });

        loadDataButton.setOnClickListener(new android.view.View.OnClickListener() {
            @Override
            public void onClick(android.view.View v) {
                viewModel.loadUserData(); // 模拟数据加载
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

