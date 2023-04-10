- [Android 体系结构](#android-体系结构)
- [四大组件](#四大组件)
- [活动](#活动)
- [服务](#服务)
  - [服务的两种启动方式](#服务的两种启动方式)
- [广播接受者](#广播接受者)
- [内容提供者](#内容提供者)
- [创建一个activity之activity\_main](#创建一个activity之activity_main)
- [用户交互\_响应用户操作和更新应用界面](#用户交互_响应用户操作和更新应用界面)
- [@Override](#override)
- [关于注解](#关于注解)
- [如何使用 Intents 在 Android 应用中进行页面跳转](#如何使用-intents-在-android-应用中进行页面跳转)
- [如何在 Android 应用中保存和读取数据](#如何在-android-应用中保存和读取数据)
- [Fragments](#fragments)
- [Fragment 的交互](#fragment-的交互)
- [Fragment 的交互\_调用activity当中的函数](#fragment-的交互_调用activity当中的函数)
- [使用 Fragment 与 Activity 之间的接口通信](#使用-fragment-与-activity-之间的接口通信)
- [Fragment 的生命周期](#fragment-的生命周期)






### Android 体系结构
Android系统采用分层架构，从高到低分为四层，分别是
1. 应用程序层
     提供一些核心应用程序包，如短信客户端程序、电话拨号程序，Web浏览器、日历、闹钟，安装在上面的程序

2. 应用程序框架层
     主要提供构建应用程序时用到的各种API。例如，活动管理器、窗体管理器、内容提供者、资源管理器等。

3. 系统库与Android运行层

     1. 系统库

          是应用程序框架的支撑，主要通过C/C++库来为Android系统提供主要的特性支持。例如包含有SQLite嵌人式数据库引擎，WebKit提供浏览器内核的支持，Media Framework多媒体库，支持多种常用的音频、视频格式的录制和回放

       2. Android运行时层

          包含核心库和虚拟机，核心库兼容了大多数JAVA语言所需要调用的功能函数，还包含了Android的核心API

4. Linux内核层
    作为硬件和软件之间的抽象层，为Android设备上的各种硬件提供底层驱动，如品示驱动、音频驱动、蓝牙驱动等



1. 我们使用Android最主要的就是使用应用，我们所使用的应用，就是应用层
2. 但是开发应用需要用到一些 API 这些 API 就是应用程序框架层
3. API 也不是凭空来的，他也需要支持，比方说数据库，多媒体等等，这个就是 Android 的系统库
4. 与此同时，还有一个 Android 系统的虚拟机 ，Android 的程序就是运行在这个地方。
5. 系统库也不是凭空来的，还需要 Linux 的内核，这个内核就是和硬件进行交流的驱动程序

-----



### 四大组件

### 活动
Android 中，Activity是所有程序的根本，所有程序的流程都运行在Activity 之中，Activity可以算是开发者遇到的最频繁，也是Android 当中最基本的模块之一。在Android的程序当中，Activity 一般代表手机屏幕的一屏。如果把手机比作一个浏览器，那么Activity就相当于一个网页。在Activity 当中可以添加一些Button、Check box 等控件。可以看到Activity 概念和网页的概念相当类似。一般一个Android 应用是由多个Activity 组成的。这多个Activity 之间可以进行相互跳转，例如，按下一个Button按钮后，可能会跳转到其他的Activity。和网页跳转稍微有些不一样的是，Activity 之间的跳转有可能返回值，例如，从Activity A 跳转到Activity B，那么当Activity B 运行结束的时候，有可能会给Activity A 一个返回值。这样做在很多时候是相当方便的。当打开一个新的屏幕时，之前一个屏幕会被置为暂停状态，并且压入历史堆栈中。用户可以通过回退操作返回到以前打开过的屏幕。可以选择性的移除一些没有必要保留的屏幕，因为Android会把每个应用的开始到当前的每个屏幕保存在堆栈中

​			

### 服务

Service 是android 系统中的一种组件，它跟Activity 的级别差不多，但是他不能自己运行，只能后台运行，并且可以和其他组件进行交互。Service 是没有界面的长生命周期的代码。Service是一种程序，它可以运行很长时间，但是它却没有用户界面。这么说有点枯燥，来看个例子。打开一个音乐播放器的程序，这个时候若想上网了，那么，打开Android浏览器，这个时候虽然已经进入了浏览器这个程序，但是，歌曲播放并没有停止，而是在后台继续一首接着一首的播放。其实这个播放就是由播放音乐的Service进行控制。当然这个播放音乐的Service也可以停止，例如，当播放列表里边的歌曲都结束，或者用户按下了停止音乐播放的快捷键等。Service 可以在和多场合的应用中使用，比如播放多媒体的时候用户启动了其他Activity这个时候程序要在后台继续播放，比如检测SD 卡上文件的变化，再或者在后台记录地理信息位置的改变等等，总之服务嘛，总是藏在后头的。

#### 服务的两种启动方式
Context.startService()：
	Service会经历onCreate -> onStart（如果Service还没有运行，则android先调用onCreate（）然后调用onStart()；如果Service已经运行，则只调用onStart（），所以一个Service的onStart方法可能会重复调用多次 ）

StopService 的时候直接 onDestroy 
	如果是调用者自己直接退出而没有调用 StopService 的话，Service会 一直在后台运行。该 Service 的调用者再启动起来后可以通过 stopService 关闭 Service 。 注意，多次调用 Context.startservice() 不会嵌套（即使会有相应的onStart()方法被调用），所以无论同一个服务被启动了多少次，一旦调用 Context.stopService() 或者 StopSelf() ，他都会被停止。
补充说明：传递给StartService（0的Intent对象会传递给onStart()方法。调用顺序为：onCreate --> onStart（可多次调用) --> onDestroy

Context.bindService()：
	Service会经历onCreate()-->onBind()，onBind将返回给客户端一个IBind接口实例，IBind允许客户端回调服务的方法，比如得到Service运行的状态或其他操作。这个时候把调用者（Context，例如Activity）会和Service绑定在一起，Context退出了，Service就会调用onUnbind --> onDestroyed相应退出，所谓绑定在一起就共存亡了。

​			

### 广播接受者
在Android 中，Broadcast是一种广泛运用的在应用程序之间传输信息的机制。而BroadcastReceiver 是对发送出来的Broadcast进行过滤接受并响应的一类组件。可以使用BroadcastReceiver 来让应用对一个外部的事件做出响应。这是非常有意思的，例如，当电话呼入这个外部事件到来的时候，可以利用BroadcastReceiver 进行处理。例如，当下载一个程序成功完成的时候，仍然可以利用BroadcastReceiver 进行处理。BroadcastReceiver不能生成UI，也就是说对于用户来说不是透明的，用户是看不到的。BroadcastReceiver通过NotificationManager 来通知用户这些事情发生了。BroadcastReceiver 既可以在AndroidManifest.xml 中注册，也可以在运行时的代码中使用Context.registerReceiver（)进行注册。只要是注册了，当事件来临的时候，即使程序没有启动，系统也在需要的时候启动程序。各种应用还可以通过使用 Context.sendBroadcast() 将它们自己的Intent Broadcasts广播给其他应用程序。

​		

### 内容提供者
Content Provider 是Android提供的第三方应用数据的访问方案。
在Android 中，对数据的保护是很严密的，除了放在SD卡中的数据，一个应用所持有的数据库、文件等内容，都是不允许其他直接访问的。Android当然不会真的把每个应用都做成一座孤岛，它为所有应用都准备了一扇窗，这就是Content Provider。应用想对外提供的数据，可以通过派生Content Provider类， 封装成一枚Content Provider，每个Content Provider都用一个uri作为独立的标识，形如：content://com.xxxxx。所有东西看着像REST的样子，但实际上，它比REST 更为灵活。和REST类似，uri也可以有两种类型，一种是带id的，另一种是列表的，但实现者不需要按照这个模式来做，给id的uri也可以返回列表类型的数据，只要调用者明白，就无妨，不用苛求所谓的REST。

-------

### 创建一个activity之activity_main

路径 app/res/layout

注意这个布局文件的文件名，只能够小写字母组成的

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello, World!"
        android:textSize="24sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>

```

详细解读这个文件

`<?xml version="1.0" encoding="utf-8"?>` 表示的是，xml 的版本还有就是编码格式

​		

```xml
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">
```

`ConstraintLayout` 表示的是 容器

`xmlns` 是命名空间，让我们可以使用 Android、app和tools命名空间的属性

`layout_width`和`layout_height`属性设置为`match_parent`，这意味着`ConstraintLayout`将填充其父容器的整个空间

`tools:context`属性指定了与此布局相关联的Activity类



翻译

ConstraintLayout 约束_布局

widget 小部件

​		

```xml
<TextView
    android:id="@+id/textView"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Hello, World!"
    android:textSize="24sp"
    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toTopOf="parent" />
```

- `android:id="@+id/textView"`为`TextView`指定了一个唯一的ID，我们可以在代码中引用它
- `android:layout_width="wrap_content"`和`android:layout_height="wrap_content"`表示`TextView`的宽度和高度将根据其内容自适应。
- `android:text="Hello, World!"`设置`TextView`显示的文本为 "Hello, World!"
- `android:textSize="24sp"`设置文本的大小为24sp（尺寸独立像素，适合用于设置字体大小）

这个主要是设置 TextView 的自己的属性

​						

* `app:layout_constraintBottom_toBottomOf="parent"`：将`TextView`的底部与父容器的底部对齐。
* `app:layout_constraintEnd_toEndOf="parent"`：将`TextView`的末端（在英语环境中为右侧）与父容器的末端对齐。
* `app:layout_constraintStart_toStartOf="parent"`：将`TextView`的起始端（在英语环境中为左侧）与父容器的起始端对齐。
* `app:layout_constraintTop_toTopOf="parent"`：将`TextView`的顶部与父容器的顶部对齐

定义了`TextView`相对于其父容器`ConstraintLayout`的约束关系

​					

翻译

wrap 包裹

wrap_content 自适应内容

​			

`</androidx.constraintlayout.widget.ConstraintLayout>` 这是根元素`ConstraintLayout`的结束标签

父容器（也称为父视图或父元素）是一个包含其他视图（称为子视图或子元素）的视图。父容器负责组织、定位和管理其子视图。在我们刚才讨论的布局示例中，`ConstraintLayout`是一个父容器，它包含了一个`TextView`子视图			

父容器可以是任何类型的布局视图，例如`LinearLayout`、`RelativeLayout`或`ConstraintLayout`等。每种父容器都有其特定的布局规则和属性，用于控制子视图的位置和行为。

​				

```java
package com.example.helloworldapp;

import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}
```







----

### 用户交互_响应用户操作和更新应用界面

```xml
    <Button
        android:id="@id/my_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="一个按钮"
        tools:layout_editor_absoluteX="16dp"
        tools:layout_editor_absoluteY="149dp"
        tools:ignore="MissingConstraints" />
```

`tools:ignore="MissingConstraints"` 添加这个属性是因为，在这个按钮当中，有一个属性是比较重要的但是没有添加，`ignore="MissingConstraints"`忽略缺少约束条件

​						

```java
public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button myButton = findViewById(R.id.my_button);
        myButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // 在这里处理点击事件
                Toast.makeText(MainActivity.this, "Button clicked!", Toast.LENGTH_SHORT).show();
            }
        });
    }
}
```

这里面主要是三个函数

`OnClickListener()` 他的作用是给 button 做一个监听器，他的作用是监听 button 的按键事件

`setOnClickListener()` 他的作用就是将我们的 监听器 附加到我们的按键，他接受一个参数就是 `OnClickListener()` 这个接口实现的类

`onClick()` 这个就是点击了 button 之后的一些操作，比方说在里面打开打一个 activity 或者是显示一个提示等等 ... 

​			

这个代码，我们能够知道，先是从布局信息当中找到我们想要操作的控件（by id）这个按键就有一个对象

对象.setOnClickListener 就能够关联上OnClickListener

OnClickListener就能够执行 onClick 里面的代码

​			

如果将这个拆分来写可以是这个样子

```java
public class MainActivity extends AppCompatActivity {
    // 创建一个实现了OnClickListener接口的类
    private class MyButtonClickListener implements View.OnClickListener {
        @Override
        public void onClick(View v) {
            // 在这里处理点击事件
            Toast.makeText(MainActivity.this, "Button clicked!", Toast.LENGTH_SHORT).show();
        }
    }

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // 找到按钮
        Button myButton = findViewById(R.id.my_button);

        // 创建一个MyButtonClickListener实例
        MyButtonClickListener listener = new MyButtonClickListener();

        // 使用setOnClickListener方法将监听器附加到按钮上
        myButton.setOnClickListener(listener);
    }
}
```

1. `Toast.makeText()`: 这是一个静态方法，用于创建一个 Toast 对象。Toast 是 Android 中一种用于显示短暂消息的小型弹出窗口。它在屏幕上持续显示几秒钟，然后自动消失，不干扰用户操作。
2. `MainActivity.this`: 这是一个对当前 `MainActivity` 实例的引用。因为我们在 `MyButtonClickListener` 类中使用了这段代码，所以需要明确地引用外部类（即 `MainActivity`）的实例。`MainActivity.this` 表示我们希望使用 `MainActivity` 的当前实例作为上下文（Context）参数。上下文是一个抽象类，代表应用程序环境的信息，通常用于访问与应用程序相关的资源和操作。
3. `Toast.LENGTH_SHORT`: 这是一个预定义的常量，表示 Toast 消息显示的持续时间。`Toast.LENGTH_SHORT`表示 Toast 消息显示的时间较短。另一个可选值是`Toast.LENGTH_LONG`，表示 Toast 消息显示的时间较长。`
4. `show()`: 这是一个 Toast 对象的方法，用于将 Toast 消息显示在屏幕上。在使用 `makeText()` 创建 Toast 对象后，必须调用 `show()` 方法才能将其显示给用户。



```java
package com.fu.tt;
import android.widget.Button;
import android.view.View;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button firstButton = findViewById(R.id.first_button);
        firstButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Toast.makeText(MainActivity.this,"o1111111",Toast.LENGTH_LONG).show();
            }
        });
        Toast.makeText(this,"o1111111",Toast.LENGTH_LONG).show();
    }
}
```

这个代码，就是使用的匿名内部类的方式进行的，也是内部类，所以要通过 `MainActivity.this` 的方式对当前实例 context 引用

如果不是在里面，就可以直接使用 this 进行引用，比方说这样 `Toast.makeText(this,"o1111111",Toast.LENGTH_LONG).show();` 

​		

下面两个代码增加，对 MainAcitivity.this 的理解

```java
public class MainActivity extends AppCompatActivity implements View.OnClickListener {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button firstButton = findViewById(R.id.first_button);
        firstButton.setOnClickListener(this);
    }

    @Override
    public void onClick(View v) {
        Toast.makeText(this, "o1111111", Toast.LENGTH_LONG).show();
    }
}
```

​				

```java
package com.fu.tt;
import android.widget.Button;
import android.view.View;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button firstButton = findViewById(R.id.first_button);
        firstButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
              ##
                Toast.makeText(v.getContext(),"o1111111",Toast.LENGTH_LONG).show();
              ##
            }
        });

        Toast.makeText(this,"？？、、、",Toast.LENGTH_LONG).show();
    }

}
```

​			

### @Override

@Override 是一个 Java 注解，用于表示一个方法是重写了父类或接口中的方法。当你在一个子类或实现了某个接口的类中编写一个方法时，如果该方法是重写父类或接口中已有的方法，建议使用 `@Override` 注解 

​			

### 关于注解

android 当中有一些直接调用的注解，比方说 @Override 他表示这个函数是一个重写

* @Override

注 解 用 于 标 记 一 个 方 法 ， 该 方 法 覆 盖 了 其 父 类 中 的 方 法 ，如果你的覆盖了一个，父类当中不存在的方法，就会报错

```java
@Override
public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
}
```

​			

*  @Nullable 和  @NonNull

  `@Nullable` 和  `@NonNull` 注 解 用 于 标 记 一 个 方 法 的 参 数 、 返 回 值 或 字 段 的 可 空 性 。 如 果 你 使 用  `@Nullable` 注 解 标 记 了 一 个 参 数 、 返 回 值 或 字 段 ， 那 么 它 可 以 为  null。 如 果 你 使 用  `@NonNull`注 解 标 记 了 一 个 参 数 、 返 回 值 或 字 段 ， 那 么 它 不 可 以 为  null。  

```java
@Nullable
public void setName(@Nullable String name) {
    this.name = name;
}

@NonNull
public String getName() {
    return name;
}

@NonNull
private String name;
```

​				

* @SuppressLint

解 用 于 禁 用  Lint 检 查 器 中 的 某 些 警 告 或 错 误 。 如 果 你 使 用  `@SuppressLint` 注 解 标 记 了 一 个 类 、 方 法 或 字 段 ， 那 么  Lint 检 查 器 将 不 会 对 该 类 、 方 法 或 字 段 进 行 检 查 

```java
@SuppressLint("SetTextI18n")
private void initUI() {
    // Set the text of the button
    Button firstButton = findViewById(R.id.first_button);
    firstButton.setText("Click me!");
}
```

Lint 检 查 器 是  Android 开 发 工 具 中 的 一 个 静 态 代 码 分 析 工 具 ， 它 可 以 帮 助 开 发 者 发 现 代 码 中 的 潜 在 问 题 		

`@SuppressLint("SetTextI18n")` 是 一 个 注 解 ， 它 用 于 禁 止  Lint 检 查 器 中 的  `SetTextI18n` 警 告 。 这 个 警 告 是 关 于  Android 应 用 程 序 中 的 国 际 化 问 题 ， 它 表 示 应 该 使 用 字 符 串 资 源 来 设 置  UI 元 素 

的 文 本 ， 而 不 是 直 接 在 代 码 中 设 置 文 本 。 		

​		

类似的还有很多

`@SuppressLint("UnusedCode")` 

该 警 告 表 示 应 用 程 序 中 存 在 未 使 用 的 代 码 ， 例 如 未 使 用 的 方 法 、 变 量 等 等 

​			

`@SuppressLint("UnusedreSources")` 

警 告 表 示 应 用 程 序 中 存 在 未 使 用 的 资 源 ， 例 如 布 局 文 件 、 字 符 串 资 源 等 等 



翻译		

Suppress 本身就是抑制，压制的意思，还通常指的是针对错误的抑制，让一些错误不出现。

---

### 如何使用 Intents 在 Android 应用中进行页面跳转

Intents 是 Android 系统中用于描述应用间或应用内组件间通信的一种机制，Intents 可以用于启动 `Activity`、服务或发送广播等

以下是一个简单的示例，我们将创建两个 Activity，`MainActivity` 和 `SecondActivity`，并在 `MainActivity` 中添加一个按钮，用于跳转到 `SecondActivity`

* 首先在 app/res/layout 当中新建一个 secondactivity 的布局界面，activity_second.xml

 ```xml
 <?xml version="1.0" encoding="utf-8"?>
 <androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
     xmlns:app="http://schemas.android.com/apk/res-auto"
     xmlns:tools="http://schemas.android.com/tools"
     android:layout_width="match_parent"
     android:layout_height="match_parent"
     tools:context=".SecondActivity">
 
     <TextView
         android:id="@+id/textView2"
         android:layout_width="wrap_content"
         android:layout_height="wrap_content"
         android:text="Welcome to Second Activity!"
         android:textSize="24sp"
         app:layout_constraintBottom_toBottomOf="parent"
         app:layout_constraintEnd_toEndOf="parent"
         app:layout_constraintStart_toStartOf="parent"
         app:layout_constraintTop_toTopOf="parent" />
 
 </androidx.constraintlayout.widget.ConstraintLayout>
 ```

​			

* 在代码当中新建一个 SecondActicity.java 的类文件

```java
package com.fu.tt;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;

public class SecondActivity extends AppCompatActivity{
    @Override
    protected  void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_second);
    }
}

```

继承自 `AppCompatActivity`，并在 `onCreate` 方法中设置 `activity_second.xml` 为其布局

​				

* 还需要将这个 activity 的这个类注册到 androidmanifest.xml 当中让系统知道

```xml
<manifest ...>
    ...
    <application ...>
        ...
        <activity android:name=".SecondActivity" />
    </application>
</manifest>

```

​				

* 添加按钮，然后跳转

需要在 `MainActivity` 的布局文件 `activity_main.xml` 中添加一个按钮，用于跳转到 `SecondActivity`。添加如下代码：

```xml
    <Button
        android:id="@+id/go_to_second_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Go to Second Activity"
        app:layout_constraintBottom_toTopOf="@+id/textView"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.764" />
```

​			

* 最后，在 `MainActivity` 类中，为按钮设置一个 `OnClickListener`，并使用 `Intent` 跳转到 `SecondActivity`

```java
        Button goToSecondActivityBUtton = findViewById(R.id.go_to_second_button);
        goToSecondActivityBUtton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(MainActivity.this,SecondActivity.class);
                startActivity(intent);
            }
        });
```

1. `new Intent(MainActivity.this, SecondActivity.class)`: 这是创建一个新的 `Intent` 对象的构造函数。它需要两个参数：
2. `MainActivity.this`: 这是当前 `Activity` 的上下文（Context）。因为我们在 `MainActivity` 的内部类（`OnClickListener`）中创建了 `Intent`，所以需要使用 `MainActivity.this` 来引用外部类的实例。
3. `SecondActivity.class`: 这是我们要跳转到的目标 `Activity` 的类名。这里我们传递了 `SecondActivity` 的类对象（`SecondActivity.class`），告诉 `Intent` 我们希望启动这个 `Activity`。

---

### 如何在 Android 应用中保存和读取数据

翻译

Share_Preferences 共享偏好设置

​		

可以在用户更改设置或输入内容时调用 `saveData` 方法，并在 `Activity` 启动或恢复时调用 `loadData` 方法来显示先前保存的数据

```java
private void saveData(String key, String value) {
    SharedPreferences sharedPreferences = getSharedPreferences("MySharedPreferences", MODE_PRIVATE);
    SharedPreferences.Editor editor = sharedPreferences.edit();
    editor.putString(key, value);
    editor.apply();
}
```

```java
    private String loadData(String key) {
        SharedPreferences sharedPreferences = getSharedPreferences("MySharedPreferences", MODE_PRIVATE);
        return sharedPreferences.getString(key, "default_value");
    }
```

这两个函数，一个写入，一个读取

`SharedPreferences`，这是一种轻量级的数据存储方式，适用于存储少量简单的数据

* `getSharedPreferences` 方法获取 `SharedPreferences` 实例
* `SharedPreferences.Editor` 对象并使用 `putString` 方法将键值对添加到编辑器中
* 最后，调用 `apply` 方法将更改保存到 `SharedPreferences` 文件

可以在用户更改设置或输入内容时调用 `saveData` 方法，并在 `Activity` 启动或恢复时调用 `loadData` 方法来显示先前保存的数据。直到卸载软件或者是，手动删除，这些数据才会消失。

​		

`SharedPreferences sharedPreferences = getSharedPreferences("MySharedPreferences", MODE_PRIVATE);` 这里是打开/创建一个 SharedPreferences 的对象，并且设置这个文件的名字MySharedPreferences，和他的访问属性`MODE_PRIVATE` 这个表示，只能够本程序的代码能够访问这个存储的数据。进程间的通信多是使用 `ContentProvider` 

​		

`SharedPreferences.Editor editor = sharedPreferences.edit();` 创建 SharedPreferences 对象的编辑器

`editor.putString(key, value); ` 就是写入键值对		

还有 `putInt` `putBoolean` ...



`editor.apply();` 

保存写入数据

当你调用 `apply()` 方法时，应用程序可以继续执行其他任务，而不需要等待数据保存操作完成。由于 `apply()` 方法是异步的，通常推荐使用它而不是 `commit()` 方法，后者是同步的并可能阻塞当前线程



我们可以看到，在访问的时候，和创建的时候，都设置了属性但是实际上，大多数的情况，MODE_PRIVATE，直接设置这个属性就行，无论是在读取的时候还是在

​		

`sharedPreferences.getString(key, "default_value");` 这个函数在执行的时候，如果没有找到对应的键值对，就会弹出 default_value（这个是自定的）		

----

### Fragments

翻译 

Fragments 分段，块

​			

在大屏的手机上，特别是平板上，我们竖着拿平板，和横着拿平板，我们的显示布局是不一样的		

Fragments的作用就是将一个 activity 的界面，分为好几段，方便管理，他依附于 activity 而存在

1. **灵活性**：Fragments 可以在不同的 Activity 之间重用，这意味着可以在不同的屏幕和场景下共享相同的 UI 逻辑。
2. **适应性**：Fragments 支持动态调整布局，可以根据屏幕尺寸和方向更好地适应不同的设备。例如，在手机上，您可以使用一个 Fragment 显示列表，然后在用户选择列表项时，启动另一个 Activity 并使用另一个 Fragment 显示详细信息。而在平板电脑上，您可以在同一个 Activity 中并排显示这两个 Fragment。
3. **生命周期管理**：Fragments 有自己的生命周期，与宿主 Activity 相互关联但又独立于它。这使得在处理与 Fragment 相关的操作时更加灵活，例如在 Activity 运行时动态添加、删除或替换 Fragment。Fragments 的生命周期管理也有助于实现更高效的资源管理。



* 首先新建一个 fragments 的类

```java
package com.fu.tt;

import androidx.fragment.app.Fragment;
import android.os.Bundle;
import android.view.LayoutInflater;
import android.view.ViewGroup;

import androidx.annotation.NonNull;
import androidx.annotation.Nullable;
import android.view.View;

public class OneFragment extends Fragment {

    @Override
    public void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        // 在这里执行您需要在视图创建之前的操作，例如初始化成员变量或设置监听器
      	// 但是大部分的时候是不需要 Oncreate 函数的，因为大部分的初始化的代码可以在 onCreateView 当中实现，只有如果您需要在视图创建之前执行某些操作
    }

    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
        return inflater.inflate(R.layout.onefragment, container, false);
    }
}

```



`LayoutInflater inflater`：用于将 XML 布局文件转换为实际的 View 对象，onCreateView 这个函数一定会返回一个 View 类型的对象，所以需要转换一下

​			

`inflater.inflate` 里面有三个参数

`R.layout.onefragment` 指定我的 fragment 的布局内容

`ViewGroup container`：承载 Fragment 视图的父容器。在将 Fragment 添加到 Activity 时，这通常是一个 FrameLayout 或其他容器，每个 Fragment 都必须要有一个父容器，即它的视图必须要嵌入到另一个视图中。这个父容器在 Fragment 被添加到 Activity 中时被指定	

`Bundle savedInstanceState`：如果 Fragment 在之前的配置更改（如屏幕旋转）中被销毁并重新创建，此参数将包含之前保存的 Fragment 状态。			

`return inflater.inflate(R.layout.fragment_example, container, false);` 		

这行代码使用传入的 `LayoutInflater` 对象将 XML 布局文件（这里是 `R.layout.fragment_example`）转换为一个 View 对象。这个 View 对象随后被添加到 `ViewGroup container` 

​			

重点关注一下这个 container ，他的类型是 ViewGroup 

他就是，Activity_main.xml 当中添加的容器

​			

还有就是关注一下 false 这个参数（通常情况之下，只需要，默认false就行了）

```java
public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
    if (container != null) {
        inflater.inflate(R.layout.onefragment, container, true);
        return container.findViewById(R.id.onefragment_root_view);
    } else {
        return inflater.inflate(R.layout.onefragment, container, false);
    }
}
```

注意添加了一个 onefragment_root_view 这个是 OneFragment.xml 的根布局的 id 

就是如果你的这个第三个参数设置为 true ，那么还需要添加一步，就是根视图的引用，但是设置为false 这个步骤是自动的，


给 OneFragment.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/onefragment_root_view"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello from One Fragment!"
        android:textSize="24sp" />
</LinearLayout>
```

​			

OneFragment.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello from One Fragment!"
        android:textSize="24sp" />
</LinearLayout>
```

​		

Activity_main.xml 当中添加

```xml
    <androidx.fragment.app.FragmentContainerView
        android:id="@+id/fragment_container"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />
```

​			

```java
public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        OneFragment exampleFragment = new OneFragment();
        FragmentManager fragmentManager = getSupportFragmentManager();
        FragmentTransaction fragmentTransaction = fragmentManager.beginTransaction();
        fragmentTransaction.add(R.id.fragment_container, exampleFragment);
        fragmentTransaction.commit();
    }
}
```

1. `OneFragment exampleFragment = new OneFragment();` 创建一个 `OneFragment` 类型的对象 `exampleFragment`，它是我们要添加到 Activity 中的 Fragment 实例。
2. `FragmentManager fragmentManager = getSupportFragmentManager();` 通过调用 `getSupportFragmentManager()` 方法来获取与当前 Activity 关联的 `FragmentManager` 实例。`FragmentManager` 是一个类，用于管理 Activity 中的 Fragments。
3. `FragmentTransaction fragmentTransaction = fragmentManager.beginTransaction();` 通过 `FragmentManager` 的 `beginTransaction()` 方法，开启一个新的 Fragment 事务。`FragmentTransaction` 类用于执行与 Fragments 相关的一系列操作（如添加、删除、替换等）。
4. `fragmentTransaction.add(R.id.fragment_container, exampleFragment);` 使用 `add()` 方法将 `exampleFragment` 添加到 `fragment_container` 中。`R.id.fragment_container` 是一个容器（通常是一个 FrameLayout），用于承载 Fragments。这行代码的作用是将 `exampleFragment` 放入指定的容器中。
5. `fragmentTransaction.commit();` 调用 `commit()` 方法以提交 Fragment 事务。这个方法告诉 `FragmentManager`，我们已完成所有的 Fragment 操作并希望执行这些操作。`FragmentManager` 会在合适的时机将 Fragment 添加到 Activity 中。

翻译

Transaction

事务通常由一系列的操作组成，如果其中任何一个操作失败，则整个事务都将回滚，即撤销之前的所有操作。



----

### Fragment 的交互

* 首先在 fragment 里面添加按钮

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello from One Fragment!"
        android:textSize="24sp" />

    <Button
        android:id="@+id/button_fragment"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Click me!" />

</LinearLayout>
```

翻译	

Linear_Layout 线性布局

​		

* class OneFragment

```java
package com.fu.tt;

import androidx.fragment.app.Fragment;
import android.os.Bundle;
import android.view.LayoutInflater;
import android.view.ViewGroup;

import androidx.annotation.NonNull;
import androidx.annotation.Nullable;
import android.view.View;
import android.widget.Button;
import android.widget.Toast;

public class OneFragment extends Fragment {

    @Override
    public void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        // 在这里执行您需要在视图创建之前的操作，例如初始化成员变量或设置监听器
    }

    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
        View view = inflater.inflate(R.layout.onefragment, container, false);
        Button button = view.findViewById(R.id.button_fragment);
        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Toast.makeText(getActivity(),"我的fragment",Toast.LENGTH_SHORT).show();
            }
        });
        return view;
    }
}
```

​		

* MainActivity.class

```java
package com.fu.tt;
import android.content.Intent;
import android.widget.Button;
import android.view.View;

import androidx.appcompat.app.AppCompatActivity;
import androidx.fragment.app.FragmentManager;
import androidx.fragment.app.FragmentTransaction;

import android.os.Bundle;
import android.widget.Toast;
import android.content.SharedPreferences;

public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        OneFragment exampleFragment = new OneFragment();
        FragmentManager fragmentManager = getSupportFragmentManager();
        FragmentTransaction fragmentTransaction = fragmentManager.beginTransaction();
        fragmentTransaction.add(R.id.fragment_container, exampleFragment);
        fragmentTransaction.commit();
    }
    }
}
```



需要注意的是，我们知道

```java
        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Toast.makeText(getActivity(),"我的fragment",Toast.LENGTH_SHORT).show();
            }
        });
```

这一段的代码，我们是通过匿名的内部类的方式实现的

`Toast.makeText(getActivity(),"我的fragment",Toast.LENGTH_SHORT).show();` 		

所以我们要通过这样的方式，指定 context 

在前面的MainActivity我们有三种方式进行指定

1. MainActivity.this

2. v.getContext()

   或者是第三种，通过直接继承的方式

   ```java
   public class MainActivity extends AppCompatActivity implements View.OnClickListener {
   
       @Override
       public void onClick(View v)
       {
           Toast.makeText(this, "o1111111", Toast.LENGTH_LONG).show();
       }
     	@Override
       protected void onCreate(Bundle savedInstanceState) {
           super.onCreate(savedInstanceState);
           setContentView(R.layout.activity_main);
   
           Button firstButton = findViewById(R.id.first_button);
           firstButton.setOnClickListener(this);
       }
   
   ```

​		

那在这个地方能够使用 OneFragment.this 嘛，能够使用，第三种方式嘛？（可以使用 v.getContext() ，getActivity（））

都不行，这是因为 `Toast.makeText()` 方法的第一个参数需要一个 `Context` 对象，而不是 `OneFragment` 类的实例。由于 `OneFragment` 类扩展了 `Fragment` 类，Fragment 不是 Context 的子类

而由于 `MainActivity` 类继承自 `AppCompatActivity`，它本身就是一个 `Context` 类的子类。因此，在这种情况下，您可以将 `MainActivity.this` 作为 `Toast.makeText()` 方法的第一个参数

​			

那在 MainActivity 当中能够使用 `getActivity()` 嘛？		

不能因为在 `MainActivity` 类中，您不能使用 `getActivity()` 方法来获取上下文（`Context` 对象）。`getActivity()` 方法只能在 `Fragment` 类中使用，因为它用于获取与 Fragment 关联的 Activity 实例。

​			

### Fragment 的交互_调用activity当中的函数

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello from One Fragment!"
        android:textSize="24sp" />

    <Button
        android:id="@+id/button_fragment"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Click me!" />

</LinearLayout>
```

​			

```java
public class MainActivity extends AppCompatActivity {
    // ...
    
    public void onFragmentButtonClicked() {
        Toast.makeText(this, "Button clicked in Fragment!", Toast.LENGTH_SHORT).show();
    }
}
```

​		

```java
public class ExampleFragment extends Fragment {
    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
        View view = inflater.inflate(R.layout.fragment_example, container, false);

        Button button = view.findViewById(R.id.button_fragment);
        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
              ## 
                if (getActivity() instanceof MainActivity) {
                    ((MainActivity) getActivity()).onFragmentButtonClicked();
                }
              ##
            }
        });
        return view;
    }
}
```

​			

### 使用 Fragment 与 Activity 之间的接口通信

假设我们有一个名为 `MainActivity` 的 Activity，它包含一个名为 `ExampleFragment` 的 Fragment。我们希望在 Fragment 中的按钮被点击时，能够在 Activity 中执行一些操作。

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello from One Fragment!"
        android:textSize="24sp" />

    <Button
        android:id="@+id/button_fragment"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Click me!" />

</LinearLayout>
```

​			

```java
public class MainActivity extends AppCompatActivity implements OneFragment.OnFragmentButtonClickListener {
    // ...
    
    public void onFragmentButtonClicked() {
        Toast.makeText(this, "在 Fragment 中的按钮被点击时，在 Activity 中执行的操作", Toast.LENGTH_SHORT).show();
    }
}
```

​			

一个名为 `listener` 的变量，以及重写 `onAttach` 和 `onDetach` 方法

在 `onAttach` 方法中检查是否实现了 `OnFragmentButtonClickListener` 接口，如果实现了，我们将其赋值给 `listener`。当 Fragment 脱离 Activity 时，我们将 `listener` 置为 null，以避免内存泄漏。

```java
public class ExampleFragment extends Fragment {
    public interface OnFragmentButtonClickListener {
        void onFragmentButtonClicked();
    }

    private OnFragmentButtonClickListener listener;

    @Override
    public void onAttach(@NonNull Context context) {
        super.onAttach(context);
        if (context instanceof OnFragmentButtonClickListener) {
            listener = (OnFragmentButtonClickListener) context;
        } else {
            throw new RuntimeException(context.toString() + " must implement OnFragmentButtonClickListener");
        }
    }

    @Override
    public void onDetach() {
        super.onDetach();
        listener = null;
    }

    // ...
}
```

​		

最后，修改 `ExampleFragment` 类中的按钮点击监听器，以调用 `listener.onFragmentButtonClicked()`：

```java
package com.fu.tt;

import androidx.fragment.app.Fragment;
import android.os.Bundle;
import android.view.LayoutInflater;
import android.view.ViewGroup;

import androidx.annotation.NonNull;
import androidx.annotation.Nullable;
import android.view.View;
import android.widget.Button;
import android.widget.Toast;
import android.content.Context;

public class OneFragment extends Fragment {
    private OnFragmentButtonClickListener listener;

    public interface OnFragmentButtonClickListener {
        void onFragmentButtonClicked();
    }

    @Override
    public void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        // 在这里执行您需要在视图创建之前的操作，例如初始化成员变量或设置监听器
    }

    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
        View view = inflater.inflate(R.layout.onefragment, container, false);
        Button button = view.findViewById(R.id.button_fragment);
        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (listener != null) {
                    listener.onFragmentButtonClicked();
                }
            }
        });
        return view;
    }

    @Override
    public void onAttach(@NonNull Context context) {
        super.onAttach(context);
        if (context instanceof OnFragmentButtonClickListener) {
            listener = (OnFragmentButtonClickListener) context;
        } else {
            throw new RuntimeException(context.toString() + " must implement OnFragmentButtonClickListener");
        }
    }

    @Override
    public void onDetach() {
        super.onDetach();
        listener = null;
    }
}
```

​			

需要注意的是，context 其实就是所属的 activity 的实例（MainActivity.this）

```java
    public void onAttach(@NonNull Context context) {
        super.onAttach(context);
        if (context instanceof OnFragmentButtonClickListener) {
            listener = (OnFragmentButtonClickListener) context;
        } else {
            throw new RuntimeException(context.toString() + " must implement OnFragmentButtonClickListener");
        }
    }
```





---

### Fragment 的生命周期	

1. **onAttach()**: 当 Fragment 与 Activity 关联时，此方法被调用。在这里，您可以获取宿主 Activity 的引用并执行与之相关的初始化操作。
2. **onCreate()**: 当 Fragment 的实例被创建时，此方法被调用。您可以在这里进行非视图相关的初始化操作，例如初始化变量。
3. **onCreateView()**: 当 Fragment 需要创建其视图时，此方法被调用。您需要在这里加载 Fragment 的布局并返回视图对象。
4. **onViewCreated()**: 当 Fragment 的视图被创建后，此方法被调用。在这里，您可以执行与视图相关的初始化操作，如设置监听器和更新视图内容。
5. **onActivityCreated()**: 当宿主 Activity 的 `onCreate()` 方法执行完成后，此方法被调用。您可以在这里进行与 Activity 相关的初始化操作。
6. **onStart()**: 当 Fragment 变得可见时，此方法被调用。您可以在这里执行与界面展示相关的操作。
7. **onResume()**: 当 Fragment 变得可以与用户交互时，此方法被调用。这是 Fragment 生命周期中的最后一个阶段。

从这个阶段开始，Fragment 可能会进入暂停状态。当这种情况发生时，以下方法将被调用：

1. **onPause()**: 当 Fragment 不再与用户交互时，此方法被调用。您可以在这里保存数据和执行其他与暂停状态相关的操作。
2. **onStop()**: 当 Fragment 变得不可见时，此方法被调用。您可以在这里执行与界面隐藏相关的操作。

接下来，Fragment 可能会重新进入活动状态，或者它可能会被销毁。如果 Fragment 被销毁，以下方法将被调用：

1. **onDestroyView()**: 当 Fragment 的视图被销毁时，此方法被调用。您可以在这里释放与视图相关的资源。
2. **onDestroy()**: 当 Fragment 的实例被销毁时，此方法被调用。您可以在这里释放与 Fragment 相关的资源。
3. **onDetach()**: 当 Fragment 与宿主 Activity 分离时，此方法被调用。您可以在这里执行与解除关联相关的操作。





1. **onAttach()**: Fragment 和 Activity 建立关联时调用。可以获取 Activity 的引用。
2. **onCreate()**: Fragment 创建时调用。进行非视图相关的初始化。
3. **onCreateView()**: Fragment 需要创建视图时调用。加载布局并返回视图对象。
4. **onViewCreated()**: 视图创建后调用。执行视图相关的初始化操作。
5. **onActivityCreated()**: Activity 完成创建后调用。进行 Activity 相关的初始化操作。
6. **onStart()**: Fragment 变得可见时调用。执行与展示相关的操作。
7. **onResume()**: Fragment 可以与用户交互时调用。此时 Fragment 处于活动状态。

接下来，Fragment 可能暂停、停止或销毁。相应的方法依次为：

1. **onPause()**: 当暂停时调用。保存数据，执行与暂停相关的操作。
2. **onStop()**: 当不可见时调用。执行与界面隐藏相关的操作。
3. **onDestroyView()**: 视图销毁时调用。释放视图资源。
4. **onDestroy()**: 实例销毁时调用。释放 Fragment 资源。
5. **onDetach()**: 与 Activity 分离时调用。执行与解除关联相关的操作。

---

### 广播接受者（BroadcastReceiver）

广播接收器（BroadcastReceiver）是 Android 系统中一种用于在应用程序之间发送和接收全局消息的组件。它允许你响应系统级事件，例如设备启动、网络状态变化、电池电量变化等。广播接收器还可以用于在应用程序内部发送和接收消息，以实现不同组件之间的通信

* 设置接收到之后的操作

```java
public class MyBroadcastReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        // 在这里处理接收到的广播
    }
}
```

​			

* 注册广播

```xml
<application ...>
    ...
    <receiver android:name=".MyBroadcastReceiver">
        <intent-filter>
            <action android:name="com.example.MY_BROADCAST" />
        </intent-filter>
    </receiver>
    ...
</application>
```

​			

* 发送广播

```java
Intent intent = new Intent("com.example.MY_BROADCAST");
sendBroadcast(intent);
```



### 普通广播和有序广播

1. 普通广播（Normal Broadcasts）：

普通广播是异步发送的，这意味着广播的接收者几乎同时收到广播。这种广播无法被中止，因此所有注册了的接收器都会收到该广播。普通广播使用 `sendBroadcast()` 方法发送。

```java
Intent intent = new Intent("com.example.MY_BROADCAST");
sendBroadcast(intent);
```

​		

2. 有序广播（Ordered Broadcasts）：

有序广播是同步发送的。这意味着在发送广播时，接收器按照优先级顺序依次处理广播。优先级较高的接收器可以拦截广播，阻止优先级较低的接收器接收到广播。有序广播使用 `sendOrderedBroadcast()` 方法发送。

```java
Intent intent = new Intent("com.example.MY_ORDERED_BROADCAST");
sendOrderedBroadcast(intent, null);
```

在发送有序广播时，你可以通过调用 `abortBroadcast()` 方法来阻止后续接收器接收广播。但请注意，这仅适用于具有相同或更低优先级的接收器。

```java
public class MyHighPriorityReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        // 处理广播
        abortBroadcast(); // 阻止后续接收器接收广播
    }
}
```

​			

在 AndroidManifest.xml 文件中，你可以使用 `android:priority` 属性为广播接收器设置优先级。优先级的范围为 -1000 到 1000，数值越高，优先级越高。

```java
<receiver android:name=".MyHighPriorityReceiver">
    <intent-filter android:priority="1000">
        <action android:name="com.example.MY_ORDERED_BROADCAST" />
    </intent-filter>
</receiver>
```

​			

### 关于广播的案例_通过监听充电断电广播显示提示（动态注册）

* 继承一个广播接收器的类 PowerConnectionReceiver

```java
package com.fu.tt;

import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.widget.Toast;

public class PowerConnectionReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent)
    {
        String action = intent.getAction();
        if (action != null) {
            if (action.equals(Intent.ACTION_POWER_CONNECTED)) {
                Toast.makeText(context, "充电器已连接", Toast.LENGTH_SHORT).show();
            } else if (action.equals(Intent.ACTION_POWER_DISCONNECTED)) {
                Toast.makeText(context, "充电器已断开", Toast.LENGTH_SHORT).show();
            }
        }
    }
}
```

​			

* 在您的 `MainActivity` 中，创建一个 `PowerConnectionReceiver` 的实例：

```java
private PowerConnectionReceiver powerConnectionReceiver;
```

注意，这里的 PowerConnectionReceiver 就是广播接收器的类

​			

* 在 `onCreate` 方法中初始化并注册广播接收器：

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    powerConnectionReceiver = new PowerConnectionReceiver();
    IntentFilter filter = new IntentFilter();
    filter.addAction(Intent.ACTION_POWER_CONNECTED);
    filter.addAction(Intent.ACTION_POWER_DISCONNECTED);
    registerReceiver(powerConnectionReceiver, filter);
}
```

1. `IntentFilter filter = new IntentFilter();`

   这里创建了一个 `IntentFilter` 实例。`IntentFilter` 类是用于指定广播接收器需要接收哪些类型的广播事件的工具。在创建 `IntentFilter` 之后，可以通过 `addAction()` 方法添加要监听的广播事件。

2. `filter.addAction(Intent.ACTION_POWER_CONNECTED);`这一行将 `ACTION_POWER_CONNECTED` 动作添加到了 `filter` 中。`ACTION_POWER_CONNECTED` 是一个系统广播，当设备连接到电源时触发。这意味着 `PowerConnectionReceiver` 将会在设备开始充电时收到广播。

​			

* 在 `onDestroy` 方法中注销广播接收器：

```java
@Override
protected void onDestroy() {
    super.onDestroy();
    unregisterReceiver(powerConnectionReceiver);
}
```

​			

### 关于广播的案例_（静态注册）

有的广播是不能够进行静态广播的注册的

比方说。。。

1. `android.intent.action.SCREEN_ON`
2. `android.intent.action.SCREEN_OFF`
3. `android.intent.action.USER_PRESENT`
4. `android.intent.action.TIME_TICK`
5. `android.intent.action.PACKAGE_ADDED`
6. `android.intent.action.PACKAGE_REMOVED`
7. `android.intent.action.BATTERY_CHANGED`
8. `android.intent.action.ACTION_POWER_CONNECTED`
9. `android.intent.action.ACTION_POWER_DISCONNECTED`
10. `android.intent.action.ACTION_SHUTDOWN`
11. `android.intent.action.ACTION_PACKAGE_NEEDS_VERIFICATION`
12. `android.intent.action.ACTION_PACKAGE_VERIFIED`
13. `android.intent.action.ACTION_PACKAGE_FIRST_LAUNCH`
14. `android.intent.action.ACTION_PACKAGE_FULLY_REMOVED`
15. `android.intent.action.ACTION_PACKAGE_INSTALL`
16. `android.intent.action.ACTION_PACKAGE_REPLACED`
17. `android.intent.action.ACTION_PACKAGE_RESTARTED`
18. `android.intent.action.ACTION_PACKAGE_DATA_CLEARED`
19. `android.intent.action.ACTION_PACKAGE_CHANGED`
20. `android.intent.action.ACTION_PACKAGE_REMOVED`
21. `android.intent.action.ACTION_PACKAGE_ADDED`
22. `android.intent.action.ACTION_PACKAGE_SUSPENDED`
23. `android.intent.action.ACTION_PACKAGE_UNSUSPENDED`
24. `android.intent.action.ACTION_MY_PACKAGE_SUSPENDED`
25. `android.intent.action.ACTION_MY_PACKAGE_UNSUSPENDED`
26. `android.intent.action.ACTION_MANAGE_APP_PERMISSION`
27. `android.intent.action.ACTION_MANAGE_APP_PERMISSIONS`
28. `android.intent.action.ACTION_LOCATION_SOURCE_SETTINGS`
29. `android.intent.action.ACTION_BUG_REPORT`

.....

1. 可以静态注册的广播：
   - 显式广播（即指定了特定组件的广播）。
   - 部分隐式广播（没有指定特定组件，而是基于 Intent Filter 的广播），这些广播通常与系统启动、设备启动、网络状态变化等事件有关。官方文档中会明确说明哪些广播可以静态注册。
2. 只能动态注册的广播：
   - 隐式广播，从 Android 8.0（API 级别 26）开始，许多系统广播事件不能使用静态注册。这类广播主要是那些频繁发生且与应用程序的实时状态相关的广播，例如电池状态、Wi-Fi状态、屏幕状态等。

​			



```xml
<application
    ...
    >
    ...
    <receiver
        android:name=".TimeZoneChangeReceiver"
        android:exported="false">
        <intent-filter>
            <action android:name="android.intent.action.TIMEZONE_CHANGED" />
        </intent-filter>
    </receiver>
</application>

```

​				

```java
package com.example.yourapp;

import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.widget.Toast;

public class TimeZoneChangeReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        if (intent.getAction() != null && intent.getAction().equals(Intent.ACTION_TIMEZONE_CHANGED)) {
            Toast.makeText(context, "时区已更改", Toast.LENGTH_SHORT).show();
        }
    }
}
```







---

### 广播的生命周期

播接收器（BroadcastReceiver）没有像 Activity、Service 或 Fragment 那样的典型生命周期。广播接收器的生命周期非常简短，因为它们的主要目的是接收应用程序之间或系统组件之间发送的广播消息，并对其进行响应。

当广播接收器接收到匹配的 Intent 时，系统会调用其 `onReceive()` 方法。在 `onReceive()` 方法内，可以处理接收到的 Intent，例如，检查 Intent 的操作、读取携带的数据等。在处理完广播后，广播接收器的实例会被销毁。

广播接收器的生命周期可以总结为以下步骤：

1. 注册：通过在 AndroidManifest.xml 中静态注册或在代码中动态注册，订阅特定的广播事件。
2. 接收：当广播事件发生时，系统会创建广播接收器的实例，并调用其 `onReceive()` 方法。
3. 处理：在 `onReceive()` 方法内处理接收到的 Intent。
4. 销毁：处理完广播后，广播接收器实例会被销毁。

需要注意的是，广播接收器不应执行耗时操作，因为在 `onReceive()` 方法中，有一个很短的执行时间限制（约 10 秒）。如果需要执行耗时操作，可以考虑在广播接收器内启动一个 Service 来处理。







