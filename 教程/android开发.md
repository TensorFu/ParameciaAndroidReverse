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
- [广播接受者（BroadcastReceiver）](#广播接受者broadcastreceiver)
- [普通广播和有序广播](#普通广播和有序广播)
- [关于广播的案例\_通过监听充电断电广播显示提示（动态注册）](#关于广播的案例_通过监听充电断电广播显示提示动态注册)
- [关于广播的案例\_时区更改（静态注册）](#关于广播的案例_时区更改静态注册)
- [关于广播的案例\_Intent.ACTION\_BATTERY\_CHANGED显示电量（动态注册）](#关于广播的案例_intentaction_battery_changed显示电量动态注册)
- [动态注册的广播再来一个例子](#动态注册的广播再来一个例子)
- [隐式广播和显式广播](#隐式广播和显式广播)
- [显式\_静态注册广播的例子](#显式_静态注册广播的例子)
- [显式\_动态注册的案例](#显式_动态注册的案例)
- [隐式\_静态广播](#隐式_静态广播)
- [隐式\_动态广播](#隐式_动态广播)
- [Activity 间通信广播：](#activity-间通信广播)
- [SecondActivity 通过广播修改 MainActivity 的展示效果](#secondactivity-通过广播修改-mainactivity-的展示效果)
- [一个最简单的有序广播（动态注册\_隐式）](#一个最简单的有序广播动态注册_隐式)
- [一个最简单的有序广播（静态注册\_显式）](#一个最简单的有序广播静态注册_显式)
- [阻断有序广播](#阻断有序广播)
- [有序广播（修改广播单条信息\_修改广播结果）](#有序广播修改广播单条信息_修改广播结果)
- [有序广播（修改广播多条信息\_修改广播额外信息）](#有序广播修改广播多条信息_修改广播额外信息)
- [setResultExtras 和 setResultData](#setresultextras-和-setresultdata)
- [普通广播的数据传递（Bundle\&intent）](#普通广播的数据传递bundleintent)
- [有序广播（带最终接受者）](#有序广播带最终接受者)
- [有序广播\_指定finalReceiver的运行线程（第四个参数）](#有序广播_指定finalreceiver的运行线程第四个参数)
- [带权限的广播](#带权限的广播)
  - [权限的申请](#权限的申请)
  - [一个关于权限的code案例](#一个关于权限的code案例)
- [有序广播（结果码）](#有序广播结果码)
- [有序广播（最后三个参数）](#有序广播最后三个参数)
- [普通广播（将任务分发到其他线程执行）](#普通广播将任务分发到其他线程执行)
- [Activity之间的通信startActivityForResult\_onActivityResult](#activity之间的通信startactivityforresult_onactivityresult)
- [广播的生命周期](#广播的生命周期)
- [Activity 的生命周期](#activity-的生命周期)
- [多线程开发](#多线程开发)
- [多线程开发（Thread 类）](#多线程开发thread-类)
- [多线程开发（Thread 类\_Runnabled的继承优势）](#多线程开发thread-类_runnabled的继承优势)
- [多线程开发（Thread 类\_Runnabled的资源共享优势）](#多线程开发thread-类_runnabled的资源共享优势)
  - [runOnUiThread()](#runonuithread)
  - [使用 Lambda 表达式简化 Runnable](#使用-lambda-表达式简化-runnable)
  - [使用线程池执行 Runnable 任务\_FixedThreadPool](#使用线程池执行-runnable-任务_fixedthreadpool)
  - [使用线程池执行 Runnable 任务\_CachedThreadPool](#使用线程池执行-runnable-任务_cachedthreadpool)
  - [使用线程池执行 Runnable 任务\_ScheduledThreadPool](#使用线程池执行-runnable-任务_scheduledthreadpool)
  - [使用线程池执行 Runnable 任务\_SingleThreadExecutor](#使用线程池执行-runnable-任务_singlethreadexecutor)
- [多线程\_Android 中与其他组件配合使用 Runnable](#多线程_android-中与其他组件配合使用-runnable)
- [多线程 AsyncTask](#多线程-asynctask)
- [Handler\_通信](#handler_通信)
- [在其他的线程当中创建 looper](#在其他的线程当中创建-looper)
- [import android.os.Message](#import-androidosmessage)
- [import android.os.Message\_arg1和arg2](#import-androidosmessage_arg1和arg2)
- [import android.os.Message\_obj](#import-androidosmessage_obj)
- [import android.os.Message\_在message当中存放多个数据](#import-androidosmessage_在message当中存放多个数据)
- [import android.os.Message\_msg.when](#import-androidosmessage_msgwhen)
- [Handle的线程之间的通信](#handle的线程之间的通信)






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

### 关于广播的案例_时区更改（静态注册）

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

下面的这个

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

​			

### 关于广播的案例_Intent.ACTION_BATTERY_CHANGED显示电量（动态注册）

`ACTION_BATTERY_CHANGED` 是一个系统广播，当设备的电池状态、电量、充电方式等发生变化时，它会被触发。这个广播会提供一系列有关电池信息的额外数据，包括电池状态、充电方式、电池剩余电量等。

​			

```java
public class MainActivity extends AppCompatActivity {
    private BatteryStatusReceiver batteryStatusReceiver;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        batteryStatusReceiver = new BatteryStatusReceiver();
        IntentFilter filter = new IntentFilter(Intent.ACTION_BATTERY_CHANGED);
        registerReceiver(batteryStatusReceiver, filter);
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        if (batteryStatusReceiver != null) {
            unregisterReceiver(batteryStatusReceiver);
        }
    }
}
```

​				

```java
package com.example.yourapp;

import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.os.BatteryManager;
import android.widget.Toast;

public class BatteryStatusReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        String action = intent.getAction();
        if (action != null && action.equals(Intent.ACTION_BATTERY_CHANGED)) {
            int status = intent.getIntExtra(BatteryManager.EXTRA_STATUS, -1);
            int level = intent.getIntExtra(BatteryManager.EXTRA_LEVEL, -1);
            int scale = intent.getIntExtra(BatteryManager.EXTRA_SCALE, -1);

            Toast.makeText(context, "电池电量：" + level + "，最大电量：" + scale, Toast.LENGTH_SHORT).show();
        }
    }
}
```

`status` 变量用于存储电池的当前状态。`BatteryManager.EXTRA_STATUS` 是从 `Intent` 中获取电池状态的键。`-1` 是默认值，当获取失败时返回。

- BatteryManager.BATTERY_STATUS_UNKNOWN：表示电池状态未知（值为1）。
- BatteryManager.BATTERY_STATUS_CHARGING：表示电池正在充电（值为2）。
- BatteryManager.BATTERY_STATUS_DISCHARGING：表示电池正在放电（值为3）。
- BatteryManager.BATTERY_STATUS_NOT_CHARGING：表示电池未充电（值为4）。
- BatteryManager.BATTERY_STATUS_FULL：表示电池已充满（值为5）。



### 动态注册的广播再来一个例子

在Activity中注册广播，可以正常监听电量状态，但随着Activity生命周期变化，不能持续监听电量

常见的不能静态注册的

　　android.intent.action.SCREEN_ON

　　android.intent.action.SCREEN_OFF

　　android.intent.action.BATTERY_CHANGED

　　android.intent.action.CONFIGURATION_CHANGED 	

​			`android.intent.action.CONFIGURATION_CHANGED` 是一个系统广播，它在设备的配置发生变化时触发。例如，当屏幕方向发生变化、用户切换语言、更改系统字体大小等情况下，此广播会被触发。

　　android.intent.action.TIME_TICK （每一分钟发送一次，类似于打点计时器）

​			

动态注册不能放到activity中，因为动态注册必须要在activity消亡的时候调用unregisterReceiver，会随着activity的解锁消失而不能再接收广播。一般的办法是在activity起来后马上start一个service,这个service里动态注册一个broadcastreceiver，service必须常驻在系统内，我在切换时区的广播当中添加，打开服务的代码

```java
package com.fu.tt;

import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.os.BatteryManager;
import android.widget.Toast;

public class BootBroadcastReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        String timeZone_action = "android.intent.action.TIMEZONE_CHANGED";
        if(timeZone_action.equals(intent.getAction())){
            Toast.makeText(context,"BOOT_COMPLETED",Toast.LENGTH_SHORT).show();
            Intent batteryServiceIntent = new Intent(context, BatteryService.class);
            context.startService(batteryServiceIntent);
        }
    }
}
```

​		

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.TT"
        tools:targetApi="31">
...

        <receiver
            android:name=".BootBroadcastReceiver"
            android:exported="false">
            <intent-filter>
                <action android:name="android.intent.action.TIMEZONE_CHANGED" />
            </intent-filter>
        </receiver>

        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>

            <meta-data
                android:name="android.app.lib_name"
                android:value="" />
        </activity>
      ...
        <service android:name=".BatteryService" />
    </application>
</manifest>
```





```java
package com.fu.tt;

import android.app.Service;
import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.content.IntentFilter;
import android.os.BatteryManager;
import android.os.Environment;
import android.os.IBinder;
import android.util.Log;
import android.widget.Toast;
import android.os.Handler;
import android.os.Looper;

import java.io.BufferedWriter;
import java.io.File;
import java.io.FileWriter;
import java.io.IOException;
import java.text.SimpleDateFormat;
import java.util.Date;


public class BatteryService extends Service {

    private static final String TAG = "BatteryReceiver";
    private static final long LOG_INTERVAL = 5000; // 5秒
    private Handler logHandler;

    private Runnable logRunnable = new Runnable() {
        @Override
        public void run() {
            Log.i(TAG, "Service is running");
            logHandler.postDelayed(this, LOG_INTERVAL);
        }
    };

    @Override
    public IBinder onBind(Intent intent) {
        return null;
    }

    @Override
    public void onCreate() {
        super.onCreate();
        Log.i(TAG, "onCreate--------------");
        IntentFilter batteryfilter = new IntentFilter();
        batteryfilter.addAction(Intent.ACTION_BATTERY_CHANGED);
        registerReceiver(batteryReceiver, batteryfilter);
    }

    @Override
    public void onStart(Intent intent, int startId) {
        super.onStart(intent, startId);
    }

    @Override
    public int onStartCommand(Intent intent, int flags, int startId) {
        Log.i(TAG, "onStartCommand--------------");
        logHandler = new Handler(Looper.getMainLooper());
        logHandler.post(logRunnable);
        return Service.START_STICKY; //
    }

    @Override
    public void onDestroy() {
        Log.i(TAG, "onDestroy--------------");
        super.onDestroy();
        logHandler.removeCallbacks(logRunnable);
        this.unregisterReceiver(batteryReceiver);
    }

    // 接收电池信息更新的广播
    private BroadcastReceiver batteryReceiver = new BroadcastReceiver()
    {
        @Override
        public void onReceive(Context context, Intent intent)
        {
            Toast.makeText(context,"执行了",Toast.LENGTH_SHORT).show();
            Log.i(TAG, "BatteryReceiver--------------");
            String action = intent.getAction();
            Log.i(TAG, " 0 action:"+ action);
            Log.i(TAG, "ACTION_BATTERY_CHANGED");
            int status = intent.getIntExtra("status", 0);
            int health = intent.getIntExtra("health", 0);
            boolean present = intent.getBooleanExtra("present", false);
            int level = intent.getIntExtra("level", 0);
            int scale = intent.getIntExtra("scale", 0);
            int icon_small = intent.getIntExtra("icon-small", 0);
            int plugged = intent.getIntExtra("plugged", 0);
            int voltage = intent.getIntExtra("voltage", 0);
            int temperature = intent.getIntExtra("temperature", 0);
            String technology = intent.getStringExtra("technology");

            String statusString = "";
            switch (status)
            {
                case BatteryManager.BATTERY_STATUS_UNKNOWN:
                    statusString = "unknown";
                    break;
                case BatteryManager.BATTERY_STATUS_CHARGING:
                    statusString = "charging";
                    break;
                case BatteryManager.BATTERY_STATUS_DISCHARGING:
                    statusString = "discharging";
                    break;
                case BatteryManager.BATTERY_STATUS_NOT_CHARGING:
                    statusString = "not charging";
                    break;
                case BatteryManager.BATTERY_STATUS_FULL:
                    statusString = "full";
                    break;
            }
            String acString = "";

            switch (plugged)
            {
                case BatteryManager.BATTERY_PLUGGED_AC:
                    acString = "plugged ac";
                    break;
                case BatteryManager.BATTERY_PLUGGED_USB:
                    acString = "plugged usb";
                    break;
            }

            SimpleDateFormat sDateFormat = new SimpleDateFormat("yyyy-MM-dd hh:mm:ss:SSS ");
            String date = sDateFormat.format(new java.util.Date());

            Log.i(TAG, "battery: date=" + date + ",status " + statusString
                    + ",level=" + level +",scale=" + scale
                    + ",voltage=" + voltage +",acString=" + acString );
        }
    };
    private static void writeLogtoFile(String logTypename, String mylogtype,
                                       String tag, String text) {// 新建或打开日志文件
        Log.i("zjq", "mylog----------");
        File path = Environment.getExternalStorageDirectory();
        Date nowtime = new Date();
        String needWriteMessage = text;
        File file = new File(path, "needWriteFiel" + logTypename);
        try {
            FileWriter filerWriter = new FileWriter(file, true);// 后面这个参数代表是不是要接上文件中原来的数据，不进行覆盖
            BufferedWriter bufWriter = new BufferedWriter(filerWriter);
            bufWriter.write(needWriteMessage);
            bufWriter.newLine();
            bufWriter.close();
            filerWriter.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

​			

### 隐式广播和显式广播

在前面的广播当中，我们发现，发送的时候，都是系统的行为，我们在接受的时候，只能够匹配上就能够接受这个广播，需要注意的是，有些系统的广播，不单单要注册，还需要你的权限 `<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />` 比方说这样。这种在发送的时候没有指定接受的类的时候

但是我们可以主动的发送广播。发送广播的时候，如果我们指定了接受的 class ，那么就是显式广播

如果我们发送的时候没有指定接受的 class 就是隐式的广播

​			

### 显式_静态注册广播的例子

```java
package com.fu.tt;

import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.widget.Toast;

public class CustomBroadcastReceiver extends BroadcastReceiver {

    @Override
    public void onReceive(Context context, Intent intent)
    {
        Toast.makeText(context,"显式广播",Toast.LENGTH_SHORT).show();
    }
}
```



```xml
        <receiver android:name=".CustomBroadcastReceiver"
            android:exported="false">
            <intent-filter>
                <action android:name="com.example.CUSTOM_BROADCAST"/>
            </intent-filter>
        </receiver>

```

​			

```java
package com.fu.tt;
import android.content.Intent;
import android.content.IntentFilter;
import android.widget.Button;
import android.view.View;

import androidx.appcompat.app.AppCompatActivity;
import androidx.fragment.app.FragmentManager;
import androidx.fragment.app.FragmentTransaction;

import android.os.Bundle;
import android.widget.Toast;
import android.content.SharedPreferences;

public class MainActivity extends AppCompatActivity implements OneFragment.OnFragmentButtonClickListener  {

    private BatteryStatusReceiver batteryStatusReceiver;


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // 发送广播
        Button btnSendBroadcast = findViewById(R.id.btn_send_broadcast);
        btnSendBroadcast.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                sendCustomBroadcast();
            }
        });
    }

    @Override
    protected void onDestroy()
    {
        super.onDestroy();
//        unregisterReceiver(powerConnectionReceiver);
        if (batteryStatusReceiver != null) {
            unregisterReceiver(batteryStatusReceiver);
        }
    }


    private void sendCustomBroadcast() {
        Intent customBroadcast = new Intent(this, CustomBroadcastReceiver.class);
        customBroadcast.setAction("com.example.CUSTOM_BROADCAST");
        sendBroadcast(customBroadcast);
    }
}
```



### 显式_动态注册的案例

我们将创建两个 Activity：`MainActivity` 和 `SecondActivity`。`MainActivity` 将动态注册一个广播接收器，而 `SecondActivity` 将发送一个显式广播，通知 `MainActivity` 更新 UI

BroadcastReceiver.java

```java
package com.fu.tt;
import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.widget.Toast;

public class MyBroadcastReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        String message = intent.getStringExtra("message");
        if (context instanceof MainActivity) {
            ((MainActivity) context).updateUI(message);
        }
    }
}
```

在这个方法中，我们需要更新 `MainActivity` 的 UI，但是我们需要首先确保 `context` 是一个 `MainActivity` 实例。

1. 首先，我们将 `context` 强制转换为 `MainActivity` 类型。这是因为 `context` 是一个更通用的类型，而我们需要访问 `MainActivity` 中的 `updateUI` 方法。强制转换确保我们可以调用这个特定的方法。
2. 接下来，我们调用 `updateUI(message)` 方法。这个方法是在 `MainActivity` 类中定义的，并且接收一个字符串作为参数。在这个例子中，`message` 参数是从广播的 `Intent` 中获取的。



MainActivity.java 并且定义 updateUI 

```java
public class MainActivity extends AppCompatActivity {
    private MyBroadcastReceiver myBroadcastReceiver;
    private TextView textView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        textView = findViewById(R.id.textView);
        myBroadcastReceiver = new MyBroadcastReceiver();
      
      	IntentFilter filter = new IntentFilter("com.example.UPDATE_UI");
        registerReceiver(myBroadcastReceiver, filter);
    }

    @Override
    protected void onResume() {
        super.onResume();
        
    }

    @Override
    protected void onPause() {
        super.onPause();
        unregisterReceiver(myBroadcastReceiver);
    }

    public void updateUI(String message) {
        textView.setText(message);
    }

    public void goToSecondActivity(View view) {
        Intent intent = new Intent(this, SecondActivity.class);
        startActivity(intent);
    }
}
```



SecondActivity.java

```java
public class SecondActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_second);
    }

    public void sendMessageToMainActivity(View view) {
        Intent intent = new Intent("com.example.UPDATE_UI");
        intent.setPackage(getPackageName());
        intent.putExtra("message", "Hello from SecondActivity!");
        sendBroadcast(intent);
    }
}
```

`intent.setPackage(getPackageName());` 这行代码设置了 Intent 的目标包名。这意味着，只有这个包名下的应用程序才能接收到这个 Intent。在这个例子中，`getPackageName()` 返回当前应用的包名。

这一行代码的主要目的是将 Intent 的范围限制在当前应用程序内。这样，你可以确保 Intent 只会发送给你自己的应用，而不会泄露到其他应用中。

​			

SecondActivity.xml

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

    <Button
        android:id="@+id/button_send_broadcast"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:onClick="sendBroadcast"
        android:text="send2 Broadcast"
        app:layout_constraintBottom_toTopOf="@+id/textView2"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.498"
        app:layout_constraintStart_toStartOf="parent" />

    <Button
        android:id="@+id/button2_send_broadcast"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="60dp"
        android:onClick="sendMessageToMainActivity"
        android:text="send Broadcast"
        app:layout_constraintBottom_toTopOf="@+id/textView2"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.497"
        app:layout_constraintStart_toStartOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

​			

### 隐式_静态广播

已经关闭大部分这样的操作，能够写，不报错，但是不发送。

少量的系统广播，主要就是触发比较少的 比方说，开机广播，还有就是切换时区广播



AndroidManifest.xml

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.timezonechange">

    <application
        ...>
        
        <receiver android:name=".TimeZoneChangeReceiver">
            <intent-filter>
                <action android:name="android.intent.action.TIMEZONE_CHANGED" />
            </intent-filter>
        </receiver>
        
    </application>

</manifest>
```

​			

MyBroadcastReceiverYin.java

```java
package com.fu.tt;
import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.widget.Toast;

public class MyBroadcastReceiverYin extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        if ("android.intent.action.TIMEZONE_CHANGED".equals(intent.getAction())) {
            String message = "收到切换时区的，隐式静态广播";
            Toast.makeText(context, message, Toast.LENGTH_SHORT).show();
        }
    }
}
```



### 隐式_动态广播

Activity_main.xml

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


    <Button
        android:id="@+id/send_broadcast_yin_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="420dp"
        android:text=" 隐式静态广播 "
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.498"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <Button
        android:id="@+id/broadcast_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="500dp"
        android:text=" 隐式动态广播 "
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.498"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />


</androidx.constraintlayout.widget.ConstraintLayout>

```

​			

Mainactivity.java

```java
private CustomBroadcastReceiver customBroadcastReceiver;

@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
  
  	Button broadcastButton = findViewById(R.id.broadcast_button);
    broadcastButton.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View view) {
            Intent intent = new Intent("com.example.CUSTOM_ACTION");
            intent.putExtra("message", "Hello from MainActivity!");
            sendBroadcast(intent);
        }
    });


    customBroadcastReceiver = new CustomBroadcastReceiver();
    IntentFilter intentFilter = new IntentFilter("com.example.CUSTOM_ACTION"); // 如果想添加广播就用 intentFilter.addAction("com.example.CUSTOM_ACTION"); 
    registerReceiver(customBroadcastReceiver, intentFilter);
}

@Override
protected void onDestroy() {
    super.onDestroy();
    unregisterReceiver(customBroadcastReceiver);
}

```

​			

CustomBroadcastReceiver.java

```java
package com.fu.tt;

import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.widget.Toast;

public class CustomBroadcastReceiver extends BroadcastReceiver {

    @Override
    public void onReceive(Context context, Intent intent)
    {
        if (intent.getAction().equals("com.example.CUSTOM_ACTION"))
        {
            Toast.makeText(context, "收到隐式动态广播： " , Toast.LENGTH_SHORT).show();
        }
        else
        {
            Toast.makeText(context, "收到广播： " , Toast.LENGTH_SHORT).show();
        }
    }
}
```



### Activity 间通信广播：

简单来说就是一个 activity 进行注册（一般来说注册在前，至少同时），另一个 activity 进行发送，然后激活广播接收器。显示内容



```java
package com.fu.tt;
import android.content.Intent;
import android.content.IntentFilter;
import android.widget.Button;
import android.view.View;

import androidx.appcompat.app.AppCompatActivity;
import androidx.fragment.app.FragmentManager;
import androidx.fragment.app.FragmentTransaction;

import android.os.Bundle;
import android.widget.Toast;
import android.content.SharedPreferences;

public class MainActivity extends AppCompatActivity implements OneFragment.OnFragmentButtonClickListener  {

  	// 客制化广播接收器
    private CustomBroadcastReceiver customBroadcastReceiver;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // 通信，广播注册
        customBroadcastReceiver = new CustomBroadcastReceiver();
        IntentFilter intentFilter = new IntentFilter("com.out.CUSTOM_BROADCAST");
        registerReceiver(customBroadcastReceiver, intentFilter);

    }

    @Override
    protected void onDestroy() {
        Toast.makeText(MainActivity.this,"已经执行了onDestory",Toast.LENGTH_SHORT).show();
        super.onDestroy();
        unregisterReceiver(customBroadcastReceiver);
    }
}
```

​			

```java
package com.fu.tt;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.content.IntentFilter;
import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.Toast;

public class SecondActivity extends AppCompatActivity{
    @Override
    protected  void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_second);
        
        // 发送广播
        Button btnSendBroadcast = findViewById(R.id.btn_send_broadcast);
        btnSendBroadcast.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                sendCustomBroadcast();
            }
        });
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
    }

  // 附带一个信息，发送了一个广播 com.out.CUSTOM_BROADCAST
    private void sendCustomBroadcast() {
        Intent customBroadcast = new Intent("com.out.CUSTOM_BROADCAST");
        customBroadcast.putExtra("message", "来自MainActivity的消息");
        sendBroadcast(customBroadcast);
    }
}
```

​				

```java
package com.fu.tt;

import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.widget.Toast;

public class CustomBroadcastReceiver extends BroadcastReceiver {

    @Override
    public void onReceive(Context context, Intent intent)
    {
        String message = intent.getStringExtra("message");
        Toast.makeText(context, "收到广播： " + message , Toast.LENGTH_SHORT).show();
    }
}
```



### SecondActivity 通过广播修改 MainActivity 的展示效果

1. MainActivity对应的（activity_main.xml）：

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
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <Button
        android:id="@+id/go_to_second_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:onClick="goToSecondActivity" <! 设置了这个，就不用设置按钮监听器，也不需要，将监听器的内容附加到按钮上，按下这个按钮之后，就会自动的执行 goToSecondActivity 这个函数>
        android:text="Go to Second Activity"
        app:layout_constraintBottom_toTopOf="@+id/textView"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />
</androidx.constraintlayout.widget.ConstraintLayout>

```

​			

MainActivity.java：

```java
import androidx.appcompat.app.AppCompatActivity;
import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.content.IntentFilter;
import android.os.Bundle;
import android.view.View;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {

    private TextView textView; // 全局变量，获得更新的数据
  
  // 声明在 MainActivity 当中的广播接收器，在里面能够接受来自 intent 的携带信息
    private BroadcastReceiver updateUIReceiver = new BroadcastReceiver() {
        @Override
        public void onReceive(Context context, Intent intent) {
            String newText = intent.getStringExtra("new_text");
            textView.setText(newText); // 这个就是用来设置  textView = findViewById(R.id.textView); 的文本信息
        }
    };

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        textView = findViewById(R.id.textView);
    }

    @Override
    protected void onResume() {
        super.onResume();
        IntentFilter filter = new IntentFilter("com.example.UPDATE_UI");
        registerReceiver(updateUIReceiver, filter);
    }

		@Override
    protected void onDestroy() {
        super.onDestroy();
        unregisterReceiver(updateUIReceiver);
    }

    public void goToSecondActivity(View view) {
        Intent intent = new Intent(this, SecondActivity.class);
        startActivity(intent);
    }
}

```

​			

SecondActivity（activity_second.xml）

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".SecondActivity">

    <Button
        android:id="@+id/button_send_broadcast"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:onClick="sendBroadcast"
        android:text="Send Broadcast"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />
</androidx.constraintlayout.widget.ConstraintLayout>
```

​			

SecondActivity.java：

```java
import androidx.appcompat.app.AppCompatActivity;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;

public class SecondActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_second);
    }

  // 发送一条广播，并且携带一条信息
    public void sendBroadcast(View view) {
        Intent intent = new Intent("com.example.UPDATE_UI");
        intent.putExtra("new_text", "Text updated from Second Activity!");
        sendBroadcast(intent);
    }
}
```

​			



### 一个最简单的有序广播（动态注册_隐式）

有序广播（Ordered Broadcast）是一种特殊类型的广播，允许多个广播接收器按照优先级顺序接收和处理广播。在传统的广播中，所有注册的广播接收器几乎是同时收到广播，但在有序广播中，系统会按照接收器的优先级顺序依次发送广播。每个接收器在处理完广播后，可以决定是否传递给下一个接收器，还可以修改广播数据。



如果我们没有写优先级，那么这个优先级就是 0 。

如果大家都是 0 那么顺序就是注册的顺序，接近同步 。 



翻译

priority ： 优先权



MainActivity.java

```java
package com.fu.tt;
import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.content.IntentFilter;
import android.util.Log;
import android.widget.Button;
import android.view.View;

import androidx.appcompat.app.AppCompatActivity;
import androidx.fragment.app.FragmentManager;
import androidx.fragment.app.FragmentTransaction;

import android.os.Bundle;
import android.widget.TextView;
import android.widget.Toast;
import android.content.SharedPreferences;

public class MainActivity extends AppCompatActivity   {


    private HighPriorityReceiver highPriorityReceiver;
    private LowPriorityReceiver lowPriorityReceiver;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

      // 按钮调用我发送广播
        Button broadcastButton = findViewById(R.id.broadcast_button);
        broadcastButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                sendOrderedBroadcast();
            }
        });

      // 调用注册广播
        highPriorityReceiver = new HighPriorityReceiver();
        lowPriorityReceiver = new LowPriorityReceiver();
        registerOrderedReceivers();
    }

  // 注销广播
    @Override
    protected void onDestroy() {
        super.onDestroy();

        unregisterReceiver(highPriorityReceiver);
        unregisterReceiver(lowPriorityReceiver);
    }

    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause() {
        super.onPause();
    }

  // 注册广播，设置优先级
    private void registerOrderedReceivers() {
        IntentFilter highPriorityFilter = new IntentFilter("com.example.ORDERED_BROADCAST");
        highPriorityFilter.setPriority(100);
        registerReceiver(highPriorityReceiver, highPriorityFilter);

        IntentFilter lowPriorityFilter = new IntentFilter("com.example.ORDERED_BROADCAST");
        lowPriorityFilter.setPriority(999);
        registerReceiver(lowPriorityReceiver, lowPriorityFilter);
    }

  // 发送广播
    private void sendOrderedBroadcast() {
        Intent intent = new Intent("com.example.ORDERED_BROADCAST");
        sendOrderedBroadcast(intent, null);
    }
}
```

​			

LowPriorityReceiver.java

```java
package com.fu.tt;

import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.util.Log;
import android.widget.Toast;

public class LowPriorityReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        Toast.makeText(context, "LowPriorityReceiver 接收到广播", Toast.LENGTH_SHORT).show();
    }
}

```

​				

HighPriorityReceiver.java

```java
package com.fu.tt;


import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.util.Log;
import android.widget.Toast;

public class HighPriorityReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        Toast.makeText(context, "HighPriorityReceiver 接收到广播", Toast.LENGTH_SHORT).show();
    }
}

```

​			

### 一个最简单的有序广播（静态注册_显式）

AndroidManifest.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />

    <uses-permission android:name="com.example.permission.MODULE_A" />
    <uses-permission android:name="com.example.permission.MODULE_B" />


    <permission
        android:name="com.example.permission.MY_BROADCAST_PERMISSION"
        android:protectionLevel="normal" />

    <uses-permission android:name="com.example.permission.MY_BROADCAST_PERMISSION" />

    <uses-permission android:name="android.permission.READ_CONTACTS" />

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.TT"
        tools:targetApi="31">

        <receiver android:name=".MyOrderedBroadcastReceiver"
            android:exported="false">
            <intent-filter android:priority="100">  <!-- 设置权限 -->
                <action android:name="com.example.ORDERED_EXPLICIT_ACTION" />
            </intent-filter>
        </receiver>



        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>

            <meta-data
                android:name="android.app.lib_name"
                android:value="" />
        </activity>

    </application>
</manifest>
```

​			

MyOrderedBroadcastReceiver.java

```java
package com.fu.tt;
import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.util.Log;
import android.widget.Toast;

public class MyOrderedBroadcastReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        String action = intent.getAction();
        if ("com.example.ORDERED_EXPLICIT_ACTION".equals(action)) {
            Toast.makeText(context, "接收到静态注册有序显式广播", Toast.LENGTH_SHORT).show();
        }
    }
}
```

​				

MainActivity.java

```java
package com.fu.tt;
import android.app.Activity;
import android.content.BroadcastReceiver;
import android.content.ComponentName;
import android.content.Context;
import android.content.Intent;
import android.content.IntentFilter;
import android.content.pm.PackageManager;
import android.os.Handler;
import android.os.HandlerThread;
import android.util.Log;
import android.widget.Button;
import android.view.View;
import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;
import android.os.Bundle;
import android.widget.Toast;
import android.os.HandlerThread;


import android.Manifest;


public class MainActivity extends AppCompatActivity   {

    private ReceiverA receiverA;
    private ReceiverB receiverB;
    private BroadcastReceiver finalReceiver;
    private Handler handler;
    private HandlerThread handlerThread;



    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        HandlerThread handlerThread = new HandlerThread("FinalReceiverThread");
        handlerThread.start();
        handler = new Handler(handlerThread.getLooper());

        // 发送有序广播
        findViewById(R.id.send_ordered_broadcast_button).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Log.i("guangbo","发送按钮点击");
                Toast.makeText(MainActivity.this, "发送广播", Toast.LENGTH_SHORT).show();
                sendOrderedExplicitBroadcast();
            }
        });
    }

    private void registerReceivers() {
        receiverA = new ReceiverA();
        IntentFilter filterA = new IntentFilter("com.example.orderedbroadcast.ACTION");
        filterA.setPriority(100);
        registerReceiver(receiverA, filterA);

        receiverB = new ReceiverB();
        IntentFilter filterB = new IntentFilter("com.example.orderedbroadcast.ACTION");
        filterB.setPriority(99);
        registerReceiver(receiverB, filterB);
    }

    private void sendOrderedBroadcastWithFinalReceiver() {
        Intent intent = new Intent("com.example.orderedbroadcast.ACTION");
        finalReceiver = new FinalReceiver();
        // 发送有序广播，添加最终接收者
        sendOrderedBroadcast(intent, null, finalReceiver, handler, Activity.RESULT_OK, null, null);
    }


    @Override
    protected void onDestroy() {
        super.onDestroy();
        unregisterReceiver(finalReceiver);
    }

    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause() {
        super.onPause();
    }

    private void sendOrderedExplicitBroadcast() {
        Intent intent = new Intent();
        intent.setComponent(new ComponentName(getPackageName(), MyOrderedBroadcastReceiver.class.getName()));
        intent.setAction("com.example.ORDERED_EXPLICIT_ACTION");
        sendOrderedBroadcast(intent, null);
    }
}
```



这个代码

```java
    private void sendOrderedExplicitBroadcast() {
        Intent intent = new Intent();
        intent.setComponent(new ComponentName(getPackageName(), MyOrderedBroadcastReceiver.class.getName()));
        intent.setAction("com.example.ORDERED_EXPLICIT_ACTION");
        sendOrderedBroadcast(intent, null);
    }
```

跟这个代码

```java
    private void sendOrderedExplicitBroadcast() {
        Intent intent = new Intent(this,MyOrderedBroadcastReceiver.class);
        intent.setAction("com.example.ORDERED_EXPLICIT_ACTION");
        sendOrderedBroadcast(intent, null);
    }
```

作用是一样的



### 阻断有序广播

`abortBroadcast();` // 阻断广播



ReceiverA.java

```java
package com.fu.tt;

import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.util.Log;


public class ReceiverA extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        if ("com.example.orderedbroadcast.ACTION".equals(intent.getAction())) {
            Log.d("Receiver", "收到有序广播，并且已经阻断了广播的传播");
            abortBroadcast(); // 阻断广播
        }
    }
}
```

​			

ReceiverB.java

```java
package com.fu.tt;

import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.util.Log;

public class ReceiverB extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        if ("com.example.orderedbroadcast.ACTION".equals(intent.getAction())) {
            Log.d("Receiver", "收到有序广播B");
        }
    }
}
```

​				

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">


  。。。。。
  

    <Button
        android:id="@+id/send_ordered_broadcast_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="发送有序广播"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.501"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.622" />


</androidx.constraintlayout.widget.ConstraintLayout>
```

​			

MainActivity.java

```java
package com.fu.tt;
import android.content.Intent;
import android.content.IntentFilter;
import android.content.pm.PackageManager;
import android.util.Log;
import android.widget.Button;
import android.view.View;
import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;
import android.os.Bundle;
import android.widget.Toast;

import android.Manifest;



public class MainActivity extends AppCompatActivity   {

    private ReceiverA receiverA;
    private ReceiverB receiverB;



    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // 动态注册广播接收器
        registerReceivers();


        // 发送有序广播
        findViewById(R.id.send_ordered_broadcast_button).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Log.i("guangbo","发送按钮点击");
                sendOrderedBroadcast();
            }
        });
    }

    private void registerReceivers() {
        receiverA = new ReceiverA();
        IntentFilter filterA = new IntentFilter("com.example.orderedbroadcast.ACTION");
        filterA.setPriority(100);
        registerReceiver(receiverA, filterA);

        receiverB = new ReceiverB();
        IntentFilter filterB = new IntentFilter("com.example.orderedbroadcast.ACTION");
        filterB.setPriority(999);
        registerReceiver(receiverB, filterB);
    }

    private void sendOrderedBroadcast() {
        Intent intent = new Intent("com.example.orderedbroadcast.ACTION");
        sendOrderedBroadcast(intent, null);
        Log.i("guangbo","发送函数执行完成");
    }


    @Override
    protected void onDestroy() {
        super.onDestroy();
        unregisterReceiver(receiverA);
        unregisterReceiver(receiverB);
    }

    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause() {
        super.onPause();
    }
}
```

​				

### 有序广播（修改广播单条信息_修改广播结果）

MainActivity.java

```java
package com.fu.tt;
import android.app.Activity;
import android.content.BroadcastReceiver;
import android.content.ComponentName;
import android.content.Context;
import android.content.Intent;
import android.content.IntentFilter;
import android.content.pm.PackageManager;
import android.os.Handler;
import android.os.HandlerThread;
import android.util.Log;
import android.widget.Button;
import android.view.View;
import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;
import android.os.Bundle;
import android.widget.Toast;
import android.os.HandlerThread;


import android.Manifest;



public class MainActivity extends AppCompatActivity   {

    private BroadcastReceiver myOrderedBroadcastReceiver1;
    private BroadcastReceiver myOrderedBroadcastReceiver2;



    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // 注册广播
        registerOrderedReceivers();



        // 发送有序广播
        findViewById(R.id.send_ordered_broadcast_button).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Log.i("guangbo","发送按钮点击");
                Toast.makeText(MainActivity.this, "发送广播", Toast.LENGTH_SHORT).show();
                    sendOrderedBroadcastWithModifiedData();
            }
        });
    }

    // 注册广播
    private void registerOrderedReceivers() {
        IntentFilter filter = new IntentFilter("com.example.ORDERED_ACTION");
        filter.setPriority(100);
        myOrderedBroadcastReceiver1 = new MyOrderedBroadcastReceiver1();
        registerReceiver(myOrderedBroadcastReceiver1, filter);

        filter.setPriority(50);
        myOrderedBroadcastReceiver2 = new MyOrderedBroadcastReceiver2();
        registerReceiver(myOrderedBroadcastReceiver2, filter);
    }




// 注销广播
    @Override
    protected void onDestroy() {
        super.onDestroy();
        unregisterReceiver(myOrderedBroadcastReceiver1);
        unregisterReceiver(myOrderedBroadcastReceiver2);
    }

  // 发送广播，并且附带信息
    private void sendOrderedBroadcastWithModifiedData() {
        Intent intent = new Intent("com.example.ORDERED_ACTION");
        intent.putExtra("message", "Hello, this is a message from the sender.");

        // 发送有序广播
        sendOrderedBroadcast(intent, null);
    }


    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause() {
        super.onPause();
    }
}
```

​			

MyOrderedBroadcastReceiver1.java

```java
package com.fu.tt;

import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.util.Log;
import android.widget.Toast;

public class MyOrderedBroadcastReceiver1 extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        String originalMessage = intent.getStringExtra("message");
        String newMessage = originalMessage + " (Modified by Receiver1)";

        Log.d("Receiver1", "Original Message: " + originalMessage);
        Log.d("Receiver1", "New Message: " + newMessage);

        // 修改广播信息
        setResultData(newMessage);
    }
}
```

​			

MyOrderedBroadcastReceiver2

```java
package com.fu.tt;

import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.util.Log;
import android.widget.Toast;

public class MyOrderedBroadcastReceiver2 extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        String modifiedMessage = getResultData();
        Log.d("Receiver2", "Modified Message: " + modifiedMessage);
    }
}

```



### 有序广播（修改广播多条信息_修改广播额外信息）

MainActivity.java

```java
package com.fu.tt;
import android.app.Activity;
import android.content.BroadcastReceiver;
import android.content.ComponentName;
import android.content.Context;
import android.content.Intent;
import android.content.IntentFilter;
import android.content.pm.PackageManager;
import android.os.Handler;
import android.os.HandlerThread;
import android.util.Log;
import android.widget.Button;
import android.view.View;
import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;
import android.os.Bundle;
import android.widget.Toast;
import android.os.HandlerThread;


import android.Manifest;



public class MainActivity extends AppCompatActivity   {

    private BroadcastReceiver myOrderedBroadcastReceiver1;
    private BroadcastReceiver myOrderedBroadcastReceiver2;



    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // 注册广播
        registerOrderedReceivers();

        // 发送有序广播
        findViewById(R.id.send_ordered_broadcast_button).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Log.i("guangbo","发送按钮点击");
                Toast.makeText(MainActivity.this, "发送广播", Toast.LENGTH_SHORT).show();
                    sendOrderedBroadcastWithModifiedData();
            }
        });
    }

    // 注册广播
    private void registerOrderedReceivers() {
        IntentFilter filter = new IntentFilter("com.example.ORDERED_ACTION");
        filter.setPriority(100);
        myOrderedBroadcastReceiver1 = new MyOrderedBroadcastReceiver1();
        registerReceiver(myOrderedBroadcastReceiver1, filter);

        filter.setPriority(50);
        myOrderedBroadcastReceiver2 = new MyOrderedBroadcastReceiver2();
        registerReceiver(myOrderedBroadcastReceiver2, filter);
    }



// 注销广播
    @Override
    protected void onDestroy() {
        super.onDestroy();
        unregisterReceiver(myOrderedBroadcastReceiver1);
        unregisterReceiver(myOrderedBroadcastReceiver2);
    }

  // 给我们的广播写入两条数据，两个键值对
    private void sendOrderedBroadcastWithModifiedData() {
        Intent intent = new Intent("com.example.ORDERED_ACTION");
        intent.putExtra("message1", "Hello, this is message1 from the sender.");
        intent.putExtra("message2", "Hello, this is message2 from the sender.");

        // 发送有序广播
        sendOrderedBroadcast(intent, null);
    }


    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause() {
        super.onPause();
    }

}
```

​			

MyOrderedBroadcastReceiver1.java

```java
package com.fu.tt;

import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.os.Bundle;
import android.util.Log;
import android.widget.Toast;

public class MyOrderedBroadcastReceiver1 extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        String originalMessage1 = intent.getStringExtra("message1");
        String newMessage1 = originalMessage1 + " (Modified by Receiver1)";
        Log.d("Receiver1", "Original Message1: " + originalMessage1);
        Log.d("Receiver1", "New Message1: " + newMessage1);

        String originalMessage2 = intent.getStringExtra("message2");
        String newMessage2 = originalMessage2 + " (Modified by Receiver1)";
        Log.d("Receiver1", "Original Message2: " + originalMessage2);
        Log.d("Receiver1", "New Message2: " + newMessage2);


        // 获取当前的额外数据
        Bundle extras = getResultExtras(true);

        // 修改多个键值对的信息
        extras.putString("message1", "newValue1");
        extras.putString("message2", "newValue2");


        // 将修改后的 Bundle 设置为结果额外数据
        setResultExtras(extras);
    }
}
```

​			

MyOrderedBroadcastReceiver2.java

```java
package com.fu.tt;

import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.os.Bundle;
import android.util.Log;
import android.widget.Toast;

public class MyOrderedBroadcastReceiver2 extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        Bundle extras = getResultExtras(false);
        String modifiedMessage1 = extras.getString("message1");
        String modifiedMessage2 = extras.getString("message2");
        Log.d("Receiver2", "Modified Message1: " + modifiedMessage1);
        Log.d("Receiver2", "Modified Message2: " + modifiedMessage2);
    }
}
```



### setResultExtras 和 setResultData

有序广播当中的数据传递

`setResultExtras(Bundle)` 和 `setResultData(String)` 是在 BroadcastReceiver 的 `onReceive()` 方法中使用的两个方法，它们分别用于修改广播中的额外数据（键值对）和结果数据（字符串）。这两个方法通常在有序广播中使用，因为有序广播允许接收者之间传递修改后的数据。

1. `setResultExtras(Bundle)`：

这个方法用于设置或修改广播中的额外数据。额外数据包含在一个 Bundle 对象中，可以在广播中附带任意数量的键值对。你可以使用 `getResultExtras(boolean)` 获取当前的额外数据，然后对其进行修改，最后使用 `setResultExtras(Bundle)` 设置回广播。

```java
@Override
public void onReceive(Context context, Intent intent) {
    // 获取当前的额外数据
    Bundle extras = getResultExtras(true);

    // 修改键值对的信息
    extras.putString("key1", "new value 1");
    extras.putString("key2", "new value 2");

    // 将修改后的 Bundle 设置为结果额外数据
    setResultExtras(extras);
}
```

​			

2. `setResultData(String)`：

这个方法用于设置或修改广播中的结果数据。结果数据是一个字符串，它可以在广播中传递单个值。你可以使用 `getResultData()` 获取当前的结果数据，然后使用 `setResultData(String)` 设置回广播。

```java
@Override
public void onReceive(Context context, Intent intent) {
    // 获取当前的结果数据
    String currentData = getResultData();

    // 修改结果数据
    String newData = currentData + " modified by Receiver";

    // 将修改后的数据设置为结果数据
    setResultData(newData);
}
```

​			

要获取额外数据（键值对）和结果数据（字符串），你可以在 BroadcastReceiver 的 `onReceive()` 方法中使用 `getResultExtras(boolean)` 和 `getResultData()` 方法。

​				

1. 获取额外数据（键值对）：

你可以使用 `getResultExtras(boolean)` 方法获取广播中的额外数据。这个方法返回一个 Bundle 对象，其中包含所有键值对。`boolean` 参数表示如果当前没有额外数据，是否创建一个新的空 Bundle 对象。

```java
@Override
public void onReceive(Context context, Intent intent) {
    // 获取额外数据
    Bundle extras = getResultExtras(true);

    // 从额外数据中获取特定的键值对
    String value1 = extras.getString("key1");
    String value2 = extras.getString("key2");

    // 对获取到的数据进行操作
    // ...
}
```

​			

2. 获取结果数据（字符串）：

你可以使用 `getResultData()` 方法获取广播中的结果数据。这个方法返回一个字符串，表示结果数据。

```java
@Override
public void onReceive(Context context, Intent intent) {
    // 获取结果数据
    String resultData = getResultData();

    // 对获取到的结果数据进行操作
    // ...
}
```

​			

### 普通广播的数据传递（Bundle&intent）

​			

**intent	**				

MainActivity.java

```java
Intent intent = new Intent("com.example.myaction");
intent.putExtra("key_string", "Hello World!");
intent.putExtra("key_int", 42);
intent.putExtra("key_bool", true);
sendBroadcast(intent);
```

​			

MyBroadcastReceiver.java

```java
public class MyBroadcastReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        String valueString = intent.getStringExtra("key_string");
        int valueInt = intent.getIntExtra("key_int", 0);
        boolean valueBool = intent.getBooleanExtra("key_bool", false);

        // 在这里使用获取到的值进行相应的操作
    }
}
```

1. `getStringExtra(String key)` - 获取字符串值
2. `getIntExtra(String key, int defaultValue)` - 获取整数值
3. `getBooleanExtra(String key, boolean defaultValue)` - 获取布尔值
4. `getLongExtra(String key, long defaultValue)` - 获取长整数值
5. `getFloatExtra(String key, float defaultValue)` - 获取浮点数值
6. `getDoubleExtra(String key, double defaultValue)` - 获取双精度浮点数值
7. `getByteExtra(String key, byte defaultValue)` - 获取字节值
8. `getShortExtra(String key, short defaultValue)` - 获取短整数值
9. `getCharExtra(String key, char defaultValue)` - 获取字符值
10. `getParcelableExtra(String key)` - 获取实现了 `Parcelable` 接口的对象
11. `getSerializableExtra(String key)` - 获取实现了 `Serializable` 接口的对象
12. `getBundleExtra(String key)` - 获取 `Bundle` 对象

注意：对于基本数据类型（如整数、布尔值、浮点数等），`getXXXExtra` 方法需要一个默认值参数，以便在找不到指定键的情况下返回默认值。对于引用类型（如字符串、`Parcelable`、`Serializable` 等），当找不到指定键时，方法会返回 `null`。

​			

```java
int intValue = intent.getIntExtra("key", 0); // 如果找不到 "key"，则返回 0
boolean boolValue = intent.getBooleanExtra("key", false); // 如果找不到 "key"，则返回 false
float floatValue = intent.getFloatExtra("key", 0.0f); // 如果找不到 "key"，则返回 0.0f
```

​				

**Bundle**

MainActivity.java

```java
// 创建一个 Intent 对象
Intent intent = new Intent("com.example.MY_BROADCAST_ACTION");

// 将数据添加到 Intent 对象
intent.putExtra("key1", "value1");
intent.putExtra("key2", "value2");

// 发送广播
sendBroadcast(intent);
```

​				

MyBroadcastReceiver.java

```java
public class MyBroadcastReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        // 从 Intent 对象中获取包含所有额外数据的 Bundle 对象
        Bundle extras = intent.getExtras();

        // 从 Bundle 对象中提取特定数据
        String value1 = extras.getString("key1");
        String value2 = extras.getString("key2");

        // 对获取到的数据进行操作
        // ...
    }
}
```

​			

多种数据类型的数据

MainActivity.java

```java
private void sendCustomBroadcast() {
    Intent intent = new Intent("com.example.CUSTOM_ACTION");

    Bundle extras = new Bundle();
    extras.putInt("key_int", 42);
    extras.putBoolean("key_boolean", true);
    extras.putString("key_string", "Hello, Bundle!");
    // ... 添加其他类型的值

    intent.putExtras(extras);

    sendBroadcast(intent);
}
```

​			

MyBroadcastReceiver.java

```java
public class MyBroadcastReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        Bundle extras = intent.getExtras();
        if (extras != null) {
            int intValue = extras.getInt("key_int", 0);
            boolean boolValue = extras.getBoolean("key_boolean", false);
            String strValue = extras.getString("key_string");
            // ... 获取其他类型的值

            Log.d("MyBroadcastReceiver", "Received int: " + intValue);
            Log.d("MyBroadcastReceiver", "Received boolean: " + boolValue);
            Log.d("MyBroadcastReceiver", "Received string: " + strValue);
            // ... 打印其他类型的值
        }
    }
}
```

extras.getInt 这个的，默认值是可有可无的。如果有的话，就是指定默认值，没有的话，就是默认的默认值



### 有序广播（带最终接受者）

FinalReceiver.java

```java
import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.util.Log;

public class FinalReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        Log.d("FinalReceiver", "收到有序广播");
    }
}
```

​			

MainActivity.java

```java
package com.fu.tt;
import android.app.Activity;
import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.content.IntentFilter;
import android.content.pm.PackageManager;
import android.util.Log;
import android.widget.Button;
import android.view.View;
import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;
import android.os.Bundle;
import android.widget.Toast;

import android.Manifest;


public class MainActivity extends AppCompatActivity   {

    private ReceiverA receiverA;
    private ReceiverB receiverB;
    private BroadcastReceiver finalReceiver;


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // 创建一个最终接收者
        finalReceiver = new FinalReceiver();

        // 动态注册广播接收器
        registerReceivers();


        // 发送有序广播
        findViewById(R.id.send_ordered_broadcast_button).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Log.i("guangbo","发送按钮点击");
                sendOrderedBroadcastWithFinalReceiver();
            }
        });
    }

    private void registerReceivers() {
        receiverA = new ReceiverA();
        IntentFilter filterA = new IntentFilter("com.example.orderedbroadcast.ACTION");
        filterA.setPriority(100);
        registerReceiver(receiverA, filterA);

        receiverB = new ReceiverB();
        IntentFilter filterB = new IntentFilter("com.example.orderedbroadcast.ACTION");
        filterB.setPriority(99);
        registerReceiver(receiverB, filterB);
    }

    private void sendOrderedBroadcastWithFinalReceiver() {
        Intent intent = new Intent("com.example.orderedbroadcast.ACTION");

        // 发送有序广播，添加最终接收者
        sendOrderedBroadcast(intent, null, finalReceiver, null, Activity.RESULT_OK, null, null);
    }


    @Override
    protected void onDestroy() {
        super.onDestroy();
        unregisterReceiver(receiverA);
        unregisterReceiver(receiverB);
    }

    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause() {
        super.onPause();
    }
}
```

注意这个注销对于 finalReceiver 是不需要的

​			

详细分析 `sendOrderedBroadcast(intent, null, finalReceiver, null, Activity.RESULT_OK, null, null);` 这一行代码

1. `intent` - 要发送的广播的 `Intent`。它包含了广播的 action、数据、类别等信息。

2. `null` - 一个字符串，用于指定发送广播所需的权限。在这个例子中，我们使用 `null` 表示发送广播不需要任何特定权限。

3. `finalReceiver` - 最终的广播接收者，它是一个 `BroadcastReceiver` 实例。当有序广播完成时，这个接收者的 `onReceive()` 方法将被调用。在这个例子中，我们创建了一个匿名的 `BroadcastReceiver` 实例作为最终接收者。

4. `null` - 一个 `Handler`，用于指定哪个线程应该处理最终接收者的 `onReceive()` 方法。在这个例子中，我们使用 `null` 表示使用默认的线程。当你发送一个有序广播时，广播接收者会按顺序处理广播。这个 `Handler` 参数可以指定最终接收者的 `onReceive()` 方法应该在哪个线程上运行。如果你设置为 `null`，那么默认情况下，接收者的 `onReceive()` 方法将在主线程（UI线程）上运行。例如，如果你想让最终接收者在子线程上运行，你可以创建一个 `HandlerThread` 和一个与之关联的 `Handler`，然后将这个 `Handler` 传递给 `sendOrderedBroadcast()` 方法，在大多数情况下，您可以将此参数设置为`null`，这意味着最终接收者将在当前线程（通常是主线程）中执行`onReceive()`方法。这对于大多数简单的场景已经足够了，因为广播接收者的处理通常不会耗费太多时间。

   然而，在某些情况下，您可能希望最终接收者在一个不同的线程中处理广播，以避免阻塞主线程。例如，如果您的应用程序需要在收到广播时执行一些耗时的操作（如文件读写、网络请求等），那么在主线程中执行这些操作可能会导致应用程序界面卡顿或不响应。

5. `Activity.RESULT_OK` - 一个整数，表示广播的初始结果代码。接收者可以根据需要修改这个结果代码。

6. `null` - 一个字符串，表示广播的初始结果数据。接收者可以根据需要修改这个结果数据。

7. `null` - 一个 `Bundle`，用于传递广播的初始额外数据。接收者可以根据需要修改这个额外数据。（4~7都是用来广播之间进行通信的）

注意这些参数只存在有序广播当中



### 有序广播_指定finalReceiver的运行线程（第四个参数）

我们知道第四个参数的作用是，用于指定哪个线程应该处理最终接收者的 `onReceive()` 方法。



FinalReceiver.java

```java
package com.fu.tt;
import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.util.Log;

public class FinalReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        Log.d("FinalReceiver", "开始处理耗时操作");

        // 模拟耗时操作，比如网络请求或者文件操作
        try {
            Thread.sleep(5000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        Log.d("FinalReceiver", "耗时操作完成");
    }
}
```

​				

MainActivity.java

```java
package com.fu.tt;
import android.app.Activity;
import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.content.IntentFilter;
import android.content.pm.PackageManager;
import android.os.Handler;
import android.os.HandlerThread;
import android.util.Log;
import android.widget.Button;
import android.view.View;
import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;
import android.os.Bundle;
import android.widget.Toast;
import android.os.HandlerThread;


import android.Manifest;


public class MainActivity extends AppCompatActivity   {

    private BroadcastReceiver finalReceiver;
    private Handler handler;
    private HandlerThread handlerThread;



    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        HandlerThread handlerThread = new HandlerThread("FinalReceiverThread");
        handlerThread.start();
        handler = new Handler(handlerThread.getLooper());


        // 动态注册广播接收器
        registerReceivers();


        // 发送有序广播
        findViewById(R.id.send_ordered_broadcast_button).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Log.i("guangbo","发送按钮点击");
                sendOrderedBroadcastWithFinalReceiver();
            }
        });
    }

    private void registerReceivers() {
        receiverA = new ReceiverA();
        IntentFilter filterA = new IntentFilter("com.example.orderedbroadcast.ACTION");
        filterA.setPriority(100);
        registerReceiver(receiverA, filterA);

        receiverB = new ReceiverB();
        IntentFilter filterB = new IntentFilter("com.example.orderedbroadcast.ACTION");
        filterB.setPriority(99);
        registerReceiver(receiverB, filterB);
    }

    private void sendOrderedBroadcastWithFinalReceiver() {
        Intent intent = new Intent("com.example.orderedbroadcast.ACTION");
        finalReceiver = new FinalReceiver();

        // 发送有序广播，添加最终接收者
        sendOrderedBroadcast(intent, null, finalReceiver, handler, Activity.RESULT_OK, null, null);
    }

  
// 注销广播，关闭线程，并且是安全关闭（也就是说，他会在关闭之前，将没有处理完的任务处理完才关闭）
  // 如果使用的 handlerThread.quit(); 就是直接关闭线程
    @Override
    protected void onDestroy() {
        super.onDestroy();
        handlerThread.quitSafely();
        unregisterReceiver(finalReceiver);
    }

    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause() {
        super.onPause();
    }
}
```



分析代码

```java
        HandlerThread handlerThread = new HandlerThread("FinalReceiverThread");
        handlerThread.start();
        handler = new Handler(handlerThread.getLooper());
```

1. `HandlerThread handlerThread = new HandlerThread("FinalReceiverThread");`
   1. 这行代码创建了一个名为 "FinalReceiverThread" 的新 `HandlerThread` 实例。`HandlerThread` 是一个特殊的线程，它可以处理和执行任务。
2. `handlerThread.start();`
   1. 这行代码启动了我们创建的 `HandlerThread`。当线程启动后，它会准备好处理任务
3. `handler = new Handler(handlerThread.getLooper());`
   1. 这行代码创建了一个 `Handler` 实例，它是用来将任务发送到 `HandlerThread` 上执行的工具。我们需要让 `Handler` 知道它应该将任务发送到哪个线程上，所以我们将刚刚创建的 `handlerThread` 的 `Looper` 传递给新的 `Handler`。`Looper` 是一个处理消息队列（任务队列）的组件，它将任务分发到关联的线程上。



```java
// 发送有序广播，添加最终接收者
        sendOrderedBroadcast(intent, null, finalReceiver, handler, Activity.RESULT_OK, null, null);
```

通过这样的方式，将 finalReceiver 的任务队列添加进 handlerThread 线程当中			

（一般来说，`Handler` 的 `post()` 和 `postDelayed()` 方法用于将任务发送到与之关联的 `HandlerThread` 上。这个我们后面介绍）				

​			









### 带权限的广播

首先我们要知道，我们的某一次的广播并不是想每一个都收到，在之前，我们的做法是显示广播，但是显式管理起来，在比较多的情况之下，就很难维护了

给我们的广播上加上权限也是为了安全。特别是比较高的权限，需要签名才能够执行广播接收器。

他能够限制广播发送者，我给广播接收器设置了权限，只有发送者跟我有一样的权限，才能够执行广播接收器

他能够限制广播接受者，我给广播发送这设置了权限，只有接受者跟我一样的权限才能够，接受我发送的广播

​				

#### 权限的申请

```xml
<permission
    android:name="com.example.permission.MY_BROADCAST_PERMISSION"
    android:protectionLevel="normal" />

<uses-permission android:name="com.example.permission.MY_BROADCAST_PERMISSION" />
```

`<permission>`：用于声明自定义权限。当您想创建一个自己的权限，以便其他应用程序使用时，您需要在 Manifest 文件中声明 `<permission>`。这里您可以设置权限的名称、保护级别等属性

​			

`<uses-permission>`：用于声明您的应用程序需要使用的权限。当您的应用程序需要使用某个权限（无论是 Android 系统权限还是其他应用程序提供的自定义权限）时，需要在 Manifest 文件中使用 `<uses-permission>` 标签，标签用于告诉系统您的应用程序需要使用某个权限。这可以是您自己定义的权限（通过 `<permission>` 标签声明的权限），也可以是 Android 系统中的预定义权限（如访问网络、访问存储等）				

​		

`<permission>` 用于声明您的应用程序提供的自定义权限，而 `<uses-permission>` 用于声明您的应用程序要要用哪些权限			

​			

```xml
android:protectionLevel="normal"
```

`android:protectionLevel` 是用于定义一个自定义权限的安全级别。它决定了其他应用程序在请求使用该权限时需要满足的条件。对于 `android:protectionLevel="normal"`，这是最低的安全级别，表示任何应用程序只需在其 AndroidManifest.xml 文件中使用 `<uses-permission>` 标签请求这个权限，就可以获得这个权限。

除了 "normal" 之外，还有其他几种 protectionLevel：

1. `dangerous`：表示权限可能会影响用户隐私或设备操作。请求此类权限的应用程序需要在运行时向用户请求权限，用户可以选择允许或拒绝。
2. `signature`：表示只有与声明此权限的应用程序具有相同签名的应用程序才能获得此权限。这意味着只有由相同开发者签名的应用程序才能共享这个权限。
3. `signatureOrSystem`：表示只有具有相同签名的应用程序或系统级应用程序才能获得此权限。这意味着只有由相同开发者签名的应用程序或者已经预安装在设备上的系统应用才能使用这个权限。



简而言之，`android:protectionLevel="normal"` 意味着这个自定义权限相对容易获得，任何应用程序只要在其 manifest 文件中声明对该权限的需求



AndroidManifest.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

  <! 声明一个权限 >
  <! 使用权限 >
    <permission
        android:name="com.example.permission.MY_BROADCAST_PERMISSION"
        android:protectionLevel="normal" />

    <uses-permission android:name="com.example.permission.MY_BROADCAST_PERMISSION" />


    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.TT"
        tools:targetApi="31">

      
      ....
      
      
     

    </application>
</manifest>
```





MainActivity.java

```java
package com.fu.tt;
import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.content.IntentFilter;
import android.util.Log;
import android.widget.Button;
import android.view.View;

import androidx.appcompat.app.AppCompatActivity;
import androidx.fragment.app.FragmentManager;
import androidx.fragment.app.FragmentTransaction;

import android.os.Bundle;
import android.widget.TextView;
import android.widget.Toast;
import android.content.SharedPreferences;

import android.content.ComponentName;

public class MainActivity extends AppCompatActivity   {

    private CustomBroadcastReceiver customBroadcastReceiver;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

      // 注册广播，设置权限
        customBroadcastReceiver = new CustomBroadcastReceiver();
        IntentFilter filter = new IntentFilter("com.example.CUSTOM_ACTION");
        registerReceiver(customBroadcastReceiver, filter,"com.example.permission.MY_BROADCAST_PERMISSION",null);


        Button broadcastButton = findViewById(R.id.broadcast_button);
        broadcastButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                sendCustomBroadcast();
            }
        });
    }

  // 发送广播，设置权限
    private void sendCustomBroadcast() {
        Intent intent = new Intent("com.example.CUSTOM_ACTION");
        sendBroadcast(intent,"com.example.permission.MY_BROADCAST_PERMISSION");
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        unregisterReceiver(customBroadcastReceiver);
    }

    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause() {
        super.onPause();
    }
}
```

​			

CustomBroadcastReceiver.java

```java
package com.fu.tt;

import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.util.Log;
import android.widget.Toast;

public class CustomBroadcastReceiver extends BroadcastReceiver {
    private static final String TAG = "CustomBroadcastReceiver";

    @Override
    public void onReceive(Context context, Intent intent) {
        Toast.makeText(context, "接受到权限广播", Toast.LENGTH_SHORT).show();
        Log.i(TAG, "Received custom broadcast.");
    }
}
```

​			

#### 一个关于权限的code案例

这是一个请求联系人权限的demo

Androidmanifest.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

<!-- 这就是我们想要申请的权限 -->
    <uses-permission android:name="android.permission.READ_CONTACTS" />

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.TT"
        tools:targetApi="31">

      
      
。。。
      
      
     

    </application>
</manifest>
```

​			

```java
package com.fu.tt;
import android.content.pm.PackageManager;
import android.widget.Button;
import android.view.View;
import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;
import android.os.Bundle;
import android.widget.Toast;

// Manifest.permission.READ_CONTACTS 这个需要的import
import android.Manifest;



public class MainActivity extends AppCompatActivity   {

    private static final int PERMISSION_REQUEST_READ_CONTACTS = 100; 

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button requestPermissionButton = findViewById(R.id.request_permission_button);
        requestPermissionButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                requestReadContactsPermission();
            }
        });
    }

    private void requestReadContactsPermission() {
        // 检查是不是已经拥有了读取联系人的权限
        if (ContextCompat.checkSelfPermission(this, Manifest.permission.READ_CONTACTS)
                != PackageManager.PERMISSION_GRANTED) {

            if (ActivityCompat.shouldShowRequestPermissionRationale(this, Manifest.permission.READ_CONTACTS)) {
                Toast.makeText(this, "需要读取联系人权限来显示联系人列表", Toast.LENGTH_SHORT).show();
            }

            ActivityCompat.requestPermissions(this, new String[]{Manifest.permission.READ_CONTACTS},
                    PERMISSION_REQUEST_READ_CONTACTS);
        } else {
            displayContacts();
        }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);
        if (requestCode == PERMISSION_REQUEST_READ_CONTACTS) {
            if (grantResults.length > 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                displayContacts();
            } else {
                Toast.makeText(this, "权限被拒绝，无法显示联系人列表", Toast.LENGTH_SHORT).show();
            }
        }
    }

    private void displayContacts() {
        Toast.makeText(this, "读取并显示联系人列表...", Toast.LENGTH_SHORT).show();
        // 实际应用中，在这里实现读取联系人并显示的逻辑
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
    }

    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause() {
        super.onPause();
    }
}
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

    <Button
        android:id="@+id/request_permission_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="请求联系人权限"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
```



现在来逐句分析一下这个代码

1. `<uses-permission android:name="android.permission.READ_CONTACTS" />` 
   1. 这个是我们申请的权限，不是我们声明的权限。所以是 uses-permission 		

2. `android:allowBackup="true"` 

   1. `<application>`标签里设置。它的作用是指示应用的数据是否可以进行备份和恢复。值为`true`表示允许备份，值为`false`表示不允许备份。 然后在用户更换设备或重新安装应用时恢复。这可以帮助用户保留应用的设置、数据等信息

3. `android:dataExtractionRules="@xml/data_extraction_rules"` 

   1. 它指定了一个XML资源文件，该文件包含了应用数据提取规则（备份，数据转移，一键换机这样的功能）。这些规则决定了哪些应用数据应该被包含在设备的全局备份和恢复过程中，`@xml/data_extraction_rules`表示规则文件位于应用的`res/xml`目录下，文件名为`data_extraction_rules.xml`。在这个文件中，通过 `<include>` 和 `<exclude>` 来包含和排除一些文件夹

   2. ```xml
      <data-extraction-rules>
          <include domain="file" path="shared_prefs" />
          <exclude domain="file" path="shared_prefs/excluded_prefs.xml" />
          <include domain="file" path="databases" />
          <include domain="file" path="app_webview" />
          <include domain="file" path="app_textures" />
      </data-extraction-rules>
      ```

4. `android:fullBackupContent="@xml/backup_rules"` （Android 12 开始就已经弃用，改用 dataExtractionRules 属性）

   1. 全量备份是指将应用程序的所有数据备份到云端（例如，Google Drive），以便在需要时进行恢复。全量备份可以在用户更换设备或者重置设备后，帮助用户恢复应用程序的数据，文件在 xml/backup_rules.xml 。所以这两个属性，一个是负责数据转移，也就是一键换机的时候，使用，另一个是，负责云端备份，至于本地备份是开发者自己的行为。在新的Android当中的（12及其以上），这个属性已经删掉了，全部变成了 dataExtractionRules 这个属性

5. `android:label="@string/app_name" ` 

   1. 个例子中，它表示应用程序的名称将从 `res/values/strings.xml` 资源文件中引用的字符串值中获取，该字符串的名称是 `app_name`

6. ` android:roundIcon="@mipmap/ic_launcher_round"` 

   1. 是一个属性，用于指定应用程序的圆形图标。在这个例子中，它表示应用程序的圆形图标将从 `mipmap` 资源文件夹中引用的图像文件中获取，该图像的名称是 `res/values/ic_launcher_round` 注意这不是一个文件，而是一个文件夹，下面放了各种分辨率下的，图标的文件。

7. `android:supportsRtl="true"` 

   1. 是一个属性，表示您的应用程序支持从右到左（RTL）的布局方向。这主要用于支持阿拉伯语、希伯来语等从右到左书写的语言

8. `tools:targetApi="31" ` 这个属性用于指定当前应用的目标 API 级别，在这个例子中是 31。API 级别表示应用程序所针对的 Android 平台版本。 这个只显示信息，不参与编译



先是检测是不是已经获取到了读取联系人的权限，如果没有就请求联系人的权限

```java
    private void requestReadContactsPermission() {
        // 检查是不是已经拥有了读取联系人的权限
        if (ContextCompat.checkSelfPermission(this, Manifest.permission.READ_CONTACTS)
                != PackageManager.PERMISSION_GRANTED) {

            if (ActivityCompat.shouldShowRequestPermissionRationale(this, Manifest.permission.READ_CONTACTS)) {
                Toast.makeText(this, "需要读取联系人权限来显示联系人列表", Toast.LENGTH_SHORT).show();
            }

            ActivityCompat.requestPermissions(this, new String[]{Manifest.permission.READ_CONTACTS},
                    PERMISSION_REQUEST_READ_CONTACTS);
        } else {
            displayContacts();
        }
    }
```

翻译

GRANTED ：已授予

​				

```java
if (ContextCompat.checkSelfPermission(this, Manifest.permission.READ_CONTACTS)
                != PackageManager.PERMISSION_GRANTED)
```

`ContextCompat.checkSelfPermission(this, Manifest.permission.READ_CONTACTS` 是用来检查是不是已经获取了权限，获取与否会返回一个值，如果这个值 等于 `PackageManager.PERMISSION_GRANTED` 就说明已经获取了权限，如果不等于就说明没有获取权限		

​		

```java
            if (ActivityCompat.shouldShowRequestPermissionRationale(this, Manifest.permission.READ_CONTACTS)) {
                Toast.makeText(this, "需要读取联系人权限来显示联系人列表", Toast.LENGTH_SHORT).show();
            }
```

翻译

Rationale : 原因

​		

这个是，是否应该显示请求权限的原因

这个时候就应该有人奇怪，为什么我之前就已经判断是是不是有权限，有权限就获取权限，没有权限，就说明用户拒绝了，为什么还要是否应该显示请求权限的原因

因为有一种情况，当用户第一次安装并运行应用时，应用可能会请求某些权限。对于用户来说，可能会觉得突然弹出权限请求不明所以。如果直接请求权限，用户可能会对此感到困惑，并拒绝授予权限。这对应用的功能和用户体验可能会产生负面影响。`shouldShowRequestPermissionRationale()` 方法的作用在于，当用户之前已经拒绝过权限请求时，这个方法会返回 `true`。这时，开发者可以在再次请求权限之前，向用户展示解释，阐述为什么应用需要这个权限。这样可以提高用户对权限请求的理解，增加用户同意授权的可能性。		

需要注意的是，`shouldShowRequestPermissionRationale()` 方法仅在用户已经拒绝过权限请求的情况下返回 `true`。对于首次请求权限，或者用户在拒绝权限请求时勾选了 "不再询问" 选项，这个方法会返回 `false`。这就是为什么我们需要在请求权限之前，额外判断是否需要向用户展示解释的原因。				

`ActivityCompat.shouldShowRequestPermissionRationale()` 方法返回值如下：

- 返回 `true`：当用户之前已经拒绝过权限请求，但没有勾选 "不再询问" 选项。在这种情况下，应用应当在请求权限之前向用户提供解释，让用户了解为什么应用需要这个权限。
- 返回 `false`：在以下情况下，该方法会返回 false
  1. 用户首次安装应用，还没有请求过权限。
  2. 用户在拒绝权限请求时勾选了 "不再询问" 选项。
  3. 应用已经获得了相应权限。

​				



```java
            ActivityCompat.requestPermissions(this, new String[]{Manifest.permission.READ_CONTACTS},
                    PERMISSION_REQUEST_READ_CONTACTS);
```

这段代码的作用是请求 READ_CONTACTS 权限。当应用调用这个方法时，系统会弹出一个对话框，询问用户是否允许应用访问联系人信息。用户做出决定后，系统会调用 `onRequestPermissionsResult()` 方法，通知应用请求的结果。			

`new String[]{Manifest.permission.READ_CONTACTS}`：一个包含要请求的权限的字符串数组。在这个例子中，我们只请求一个权限：`Manifest.permission.READ_CONTACTS`，用于读取联系人信息。

`PERMISSION_REQUEST_READ_CONTACTS` 是我们的自定义的标识符，用于区别不同的权限。

​			

```java
   public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);
        if (requestCode == PERMISSION_REQUEST_READ_CONTACTS) {
            if (grantResults.length > 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                displayContacts();
            } else {
                Toast.makeText(this, "权限被拒绝，无法显示联系人列表", Toast.LENGTH_SHORT).show();
            }
        }
    }
```

这个代码的作用是显示我我们的联系人，但是我们的权限授予是异步的，所以，我们使用这个权限的时候，不能够确定就已经赋予上了。所以需要检查一下

​			

### 有序广播（结果码）

Activity.RESULT_OK 这个就是一个常量他就是 -1，然后传进去

在广播接收器当中的结束的位置，通过 setResultCode(200) ；类似于这样的操作。

我们在任何一个位置，比方说原来的Activity，或者是下一个 OnReceive 的方法当中就能够通过 `getResultCode()` 的函数获取到，当前的 结果码，如果，我们获取到的结果码是 200 ，就说明，我们的这个已经执行完毕了



MainActivity.java

```java
package com.fu.tt;
import android.app.Activity;
import android.content.BroadcastReceiver;
import android.content.ComponentName;
import android.content.Context;
import android.content.Intent;
import android.content.IntentFilter;
import android.content.pm.PackageManager;
import android.os.Handler;
import android.os.HandlerThread;
import android.util.Log;
import android.widget.Button;
import android.view.View;
import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;
import android.os.Bundle;
import android.widget.Toast;
import android.os.HandlerThread;


import android.Manifest;


public class MainActivity extends AppCompatActivity   {


    private BroadcastReceiver finalReceiver;
    private MyOrderedBroadcastReceiver1 myOrderedBroadcastReceiver1;
    private MyOrderedBroadcastReceiver2 myOrderedBroadcastReceiver2;



    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // 注册广播
        registerOrderedReceivers();



        // 发送有序广播
        findViewById(R.id.send_ordered_broadcast_button).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Log.i("guangbo","发送按钮点击");
                Toast.makeText(MainActivity.this, "发送广播", Toast.LENGTH_SHORT).show();
                sendOrderedBroadcast();
            }
        });
    }

    // 注册广播
    private void registerOrderedReceivers() {
        IntentFilter filter = new IntentFilter("com.example.ORDERED_ACTION");
        filter.setPriority(100);
        myOrderedBroadcastReceiver1 = new MyOrderedBroadcastReceiver1();
        registerReceiver(myOrderedBroadcastReceiver1, filter);

        filter.setPriority(50);
        myOrderedBroadcastReceiver2 = new MyOrderedBroadcastReceiver2();
        registerReceiver(myOrderedBroadcastReceiver2, filter);
    }





    @Override
    protected void onDestroy() {
        super.onDestroy();
        unregisterReceiver(myOrderedBroadcastReceiver1);
        unregisterReceiver(myOrderedBroadcastReceiver2);
    }



    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause() {
        super.onPause();
    }

    private void sendOrderedBroadcast() {
        Intent intent = new Intent("com.example.ORDERED_ACTION");
        intent.setPackage(getPackageName());
        sendOrderedBroadcast(intent, null, new BroadcastReceiver() {
            @Override
            public void onReceive(Context context, Intent intent) {
                int resultCode = getResultCode();
                Log.d("OrderedBroadcast", "Final Receiver: Result code = " + resultCode);
            }
        }, null, Activity.RESULT_OK, null, null);
    }
}
```

​			

OrderedBroadcastReceiver1.java

```java
package com.fu.tt;

import android.app.Activity;
import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.util.Log;

public class OrderedBroadcastReceiver1 extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        int resultCode = getResultCode(); // 他没有什么作用，他的作用就是获取上一次的赋予的结果码
        if (resultCode == Activity.RESULT_OK) {
            Log.d("OrderedBroadcast", "Receiver 1: Result code = " + resultCode);
            setResultCode(100); // 设置结果码
        }
    }
}
```

​			

OrderedBroadcastReceiver2.java

```java
package com.fu.tt;

import android.app.Activity;
import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.util.Log;

public class OrderedBroadcastReceiver2 extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        int resultCode = getResultCode();
        if (resultCode == 100) {
            Log.d("OrderedBroadcast", "Receiver 2: Result code = " + resultCode);
            setResultCode(200);
        }
    }
}
```

在普通广播（非有序广播）中，广播接收者是异步执行的，且接收者之间没有先后顺序，因此也没有结果代码。普通广播通常用于通知多个接收者某个事件发生，而不关心接收者处理的结果或顺序。

​				

### 有序广播（最后三个参数）

最后三个参数分别是

1. 结果码（Result Code）： 结果码是一个整数值，用于表示广播处理的状态或结果。你可以通过 `setResultCode(int)` 方法在 BroadcastReceiver 中设置结果码，然后在后续的接收者或最终接收者中使用 `getResultCode()` 方法获取这个值。结果码主要用于表示广播处理过程中的某种状态，例如表示操作成功、失败或其他状态。
2. 结果数据（Result Data）： 结果数据是一个字符串值，用于在广播接收者之间传递简单的文本信息。你可以通过 `setResultData(String)` 方法在 BroadcastReceiver 中设置结果数据，然后在后续的接收者或最终接收者中使用 `getResultData()` 方法获取这个值。结果数据适用于传递较简单的文本信息，例如修改后的文本消息等。
3. 额外数据（Extras）： 额外数据是一个 Bundle 对象，其中可以包含多种数据类型（如字符串、整数、布尔值等）。你可以在发送广播时将数据存储在 Intent 的 Extras 中，然后在 BroadcastReceiver 中使用 `intent.getExtras()` 方法获取这些数据。如果需要在广播接收者之间修改或添加额外数据，可以通过 `setResultExtras(Bundle)` 方法设置新的 Bundle 对象，然后在后续的接收者或最终接收者中使用 `getResultExtras(boolean)` 方法获取这个 Bundle。额外数据适用于传递复杂的数据结构，例如包含多个键值对的 Bundle 对象。

这三个参数的存在意义主要是为了在广播接收者之间传递不同类型和复杂度的数据。结果码用于传递状态信息，结果数据用于传递简单的文本信息，而额外数据用于传递更复杂的数据结构。它们在一定程度上具有互补性，可以根据你的需求选择使用哪个参数来传递数据。需要注意的是，这些参数在有序广播中才能发挥作用，因为有序广播允许接收者之间传递修改后的数据。在普通广播中，你需要使用 Intent 对象中的 getExtras() 和其他类似方法获取相应的数据。				

​					

### 普通广播（将任务分发到其他线程执行）

普通广播中指定运行的线程：默认情况下，广播接收者的 `onReceive()` 方法在主线程中执行。如果您需要在其他线程中执行广播接收者的代码，可以在 `onReceive()` 方法中使用 `Handler`、`HandlerThread` 或其他并发工具将代码分发到其他线程。然而，这种方式并不会影响广播接收者的执行顺序，仅仅是将接收者的处理逻辑移到其他线程执行。

​				

BackgroundTaskManager.java

```java
package com.fu.tt;

import android.os.Handler;
import android.os.HandlerThread;

public class BackgroundTaskManager {
    private static BackgroundTaskManager instance;
    private HandlerThread handlerThread;
    private Handler handler;

    private BackgroundTaskManager() {
        handlerThread = new HandlerThread("BackgroundTaskManagerThread");
        handlerThread.start();
        handler = new Handler(handlerThread.getLooper());
    }

    public static BackgroundTaskManager getInstance() {
        if (instance == null) {
            instance = new BackgroundTaskManager();
        }
        return instance;
    }

    public void postTask(Runnable task) {
        handler.post(task);
    }
}
```

​					

MyBroadcastReceiver.java

```java
package com.fu.tt;
import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.os.Handler;
import android.os.HandlerThread;
import android.util.Log;
import android.widget.Toast;

public class MyBroadcastReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(final Context context, final Intent intent) {
        Log.i("MyBroadcastReceiver", "收到广播");

        BackgroundTaskManager.getInstance().postTask(new Runnable() {
            @Override
            public void run() {
                // 在这里执行后台任务
                Log.d("MyBroadcastReceiver", "后台任务执行中...");

                // 模拟耗时任务
                try {
                    Thread.sleep(2000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                Log.d("MyBroadcastReceiver", "后台任务完成");
            }
        });
    }
}
```

​				

```java
package com.fu.tt;
import android.app.Activity;
import android.content.BroadcastReceiver;
import android.content.ComponentName;
import android.content.Context;
import android.content.Intent;
import android.content.IntentFilter;
import android.content.pm.PackageManager;
import android.os.Handler;
import android.os.HandlerThread;
import android.util.Log;
import android.widget.Button;
import android.view.View;
import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;
import android.os.Bundle;
import android.widget.Toast;
import android.os.HandlerThread;


import android.Manifest;



public class MainActivity extends AppCompatActivity   {

    private MyBroadcastReceiver myBroadcastReceiver;



    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        myBroadcastReceiver = new MyBroadcastReceiver();
        IntentFilter intentFilter = new IntentFilter("com.example.BACKGROUND_TASK_ACTION");
        registerReceiver(myBroadcastReceiver, intentFilter);


        // 发送有序广播
        findViewById(R.id.send_ordered_broadcast_button).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Log.i("guangbo","发送按钮点击");
                Toast.makeText(MainActivity.this, "发送广播", Toast.LENGTH_SHORT).show();
                Intent intent = new Intent("com.example.BACKGROUND_TASK_ACTION");
                sendBroadcast(intent);
            }
        });
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        unregisterReceiver(myBroadcastReceiver);
        BackgroundTaskManager.getInstance().quitSafely();
    }

    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause()
    {
        super.onPause();
    }
}
```

​				

分析代码			

```java
    public static BackgroundTaskManager getInstance() {
        if (instance == null) {
            instance = new BackgroundTaskManager();
        }
        return instance;
    }
```

这个 `getInstance()` 方法是一个典型的单例模式的实现。单例模式（Singleton Pattern）是一种设计模式，它确保一个类只有一个实例，并提供一个全局访问点。在这个例子中，`BackgroundTaskManager` 类是一个单例类。			

可以把MyBroadcastReceiver.java这个类拆开写，方便理解

```java
package com.fu.tt;
import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.os.Handler;
import android.os.HandlerThread;
import android.util.Log;
import android.widget.Toast;

public class MyBroadcastReceiver extends BroadcastReceiver {
    // 接收到广播
    @Override
    public void onReceive(final Context context, final Intent intent) {
        handleBroadcast(context, intent);
    }


    private void handleBroadcast(Context context, Intent intent) {
        Log.i("MyBroadcastReceiver", "收到广播");

        // 生成多线程的任务
        Runnable task = createBackgroundTask();
        // 将多线程的任务添加给线程
        BackgroundTaskManager backgroundTaskManager = BackgroundTaskManager.getInstance();
        backgroundTaskManager.postTask(task);
    }

    // 返回一个 Runnable 的任务，任务加在重写的 run 函数当中
    private Runnable createBackgroundTask() {
        return new Runnable() {
            @Override
            public void run() {
                performBackgroundTask();
            }
        };
    }

    private void performBackgroundTask() {
        Log.d("MyBroadcastReceiver", "后台任务执行中...");
        // 当前运行在哪一个线程当中
        Log.d("MyBroadcastReceiver","正在 ：" + Thread.currentThread().getName() + " 线程上执行 ... ")

        // 模拟耗时任务
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        Log.d("MyBroadcastReceiver", "后台任务完成");
    }
}
```

​				

### Activity之间的通信startActivityForResult_onActivityResult

在前面的介绍当中，我们知道，广播能够做到两个Activity之间的通信，onActivityResult和startActivityForResult 同样的能够做到。















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



---

### Activity 的生命周期

1. 创建（onCreate）：当 Activity 实例被创建时调用。在这个阶段，您可以初始化组件、设置布局、注册事件监听器等。
2. 启动（onStart）：当 Activity 变为可见时调用。此时，Activity 还不能与用户进行交互，但可以执行准备工作。
3. 恢复（onResume）：当 Activity 准备好与用户进行交互时调用。此时，Activity 处于前台并获取到焦点。
4. 暂停（onPause）：当 Activity 失去焦点时调用。此时，Activity 仍然可见，但无法与用户进行交互。
5. 停止（onStop）：当 Activity 完全不可见时调用。例如，用户切换
6. 重启（onRestart）：当 Activity 从完全不可见状态重新变为可见时调用。在 onStop 之后，onRestart 会被触发，然后是 onStart。

1. 销毁（onDestroy）：当 Activity 实例被销毁时调用。此时，您应该释放资源、注销广播接收器等。在 Activity 结束或系统回收资源时，onDestroy 会被触发。



以一个简单的应用为例，该应用包含两个 Activity：Activity1 和 Activity2。我们将详细描述用户在这个应用中执行的操作以及对应的 Activity 生命周期阶段。

1. 用户打开应用：这时，Activity1 的 onCreate、onStart 和 onResume 方法依次被调用。Activity1 处于运行状态。
2. 用户点击按钮跳转到 Activity2：此时，Activity1 的 onPause 方法被调用，因为它失去了焦点。接着，Activity2 的 onCreate、onStart 和 onResume 方法被调用，进入运行状态。此外，Activity1 的 onStop 方法会被调用，因为它已完全不可见。
3. 用户点击返回按钮，返回到 Activity1：这时，Activity2 的 onPause 方法被调用。然后，Activity1 的 onRestart、onStart 和 onResume 方法被调用，重新回到运行状态。接下来，Activity2 的 onStop 和 onDestroy 方法被调用，因为用户已经离开了 Activity2。
4. 用户按下 Home 键，将应用放到后台：此时，Activity1 的 onPause 和 onStop 方法被调用，因为它失去了焦点并完全不可见。
5. 用户通过最近应用列表重新打开应用：这时，Activity1 的 onRestart、onStart 和 onResume 方法被调用，重新回到运行状态。
6. 用户按下返回键或通过其他方式退出应用：此时，Activity1 的 onPause、onStop 和 onDestroy 方法被调用，完成整个生命周期。



---

### 多线程开发

在 Android 中，有以下几种常用的多线程编程方法：

1. **Thread 类**：直接使用 Java 中的 `Thread` 类创建一个新的线程。你可以通过继承 `Thread` 类并重写 `run()` 方法，或者通过传递一个 `Runnable` 对象来实现。这是一种基本的多线程编程方法，但需要注意线程间的同步和通信问题。
2. **AsyncTask 类**：`AsyncTask` 是一个 Android 提供的轻量级异步任务类，适用于执行较短时间的后台任务。`AsyncTask` 可以让你在后台线程上执行任务，然后在主线程上更新 UI。需要注意的是，`AsyncTask` 自 Android 11（API 级别 30）开始已被弃用，建议使用其他替代方案。
3. **HandlerThread 类**：`HandlerThread` 是一个可以在新线程中运行 `Handler` 的预定义类。它创建了一个新的线程，其中包含一个与其关联的 `Looper`。这个 `Looper` 可以用于创建 `Handler` 对象，从而实现在子线程中处理消息和运行任务。`HandlerThread` 非常适合于需要执行周期性任务或需要处理消息队列的场景。
4. **IntentService 类**：`IntentService` 是一个用于处理异步请求的服务类。通过发送 `Intent` 来启动服务，`IntentService` 会在一个工作线程上执行该请求，然后在完成后自动停止服务。`IntentService` 适用于执行一次性的后台任务，例如文件下载。
5. **ThreadPoolExecutor 类**：`ThreadPoolExecutor` 是 Java 并发库中的一个类，用于创建和管理线程池。它可以用于执行大量的短时间任务，这些任务可以在一个固定数量的线程上并发执行。线程池可以减少线程创建和销毁的开销，提高系统性能。
6. **RxJava**：RxJava 是一个响应式编程库，它可以让你使用观察者模式来处理异步任务。RxJava 提供了一系列操作符，让你可以方便地管理多线程、数据流和回调。
7. **Kotlin 协程**：如果你使用 Kotlin 进行 Android 开发，可以使用 Kotlin 协程来处理异步任务。协程是一种轻量级的线程管理方式，它可以让你编写简洁的异步代码，同时提供了结构化的并发。

​				

### 多线程开发（Thread 类）

Thread 类是 Java 提供的基本多线程编程工具。使用 Thread 类创建线程有两种方法：

1. 继承 Thread 类并重写 `run()` 方法；
2. 实现 Runnable 接口并将 Runnable 对象传递给 Thread 构造函数。

​			

**方法一：继承 Thread 类**

1. 创建一个新类，继承自 Thread 类，并重写 `run()` 方法。

```java
public class MyThread extends Thread {
    @Override
    public void run() {
        // 在这里执行线程任务
        for (int i = 0; i < 5; i++) {
            System.out.println("MyThread: " + i);
            try {
                Thread.sleep(1000); // 休眠 1 秒
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

​			

2. 在需要创建线程的地方创建 `MyThread` 实例，并调用 `start()` 方法启动线程。

```java
MyThread myThread = new MyThread();
myThread.start();
```

​				

完整的代码

```java
package com.fu.tt;
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.util.Log;


public class MainActivity extends AppCompatActivity   {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        MyThread myThread = new MyThread();
        myThread.start();
    }

    // 自定义线程类，继承自 Thread 类
    private static class MyThread extends Thread {
        @Override
        public void run() {
            super.run();

            // 在这里执行线程任务
            for (int i = 0; i < 5; i++) {
                Log.d("MyThread", "线程运行中：" + i);

                try {
                    // 模拟耗时任务，线程休眠1秒
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
    }

    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause()
    {
        super.onPause();
    }
}
```

在这个例子中，线程会在 `run()` 方法中的任务执行完毕后自动退出。你可以看到 `run()` 方法里有一个循环，循环执行5次打印日志和休眠操作。当循环执行完毕后，`run()` 方法结束，线程自然就退出了。			

​			

​			

**方法二：实现 Runnable 接口**（更加推荐）

1. 创建一个新类，实现 Runnable 接口，并重写 `run()` 方法。			

```java
public class MyRunnable implements Runnable {
    @Override
    public void run() {
        // 在这里执行线程任务
        for (int i = 0; i < 5; i++) {
            System.out.println("MyRunnable: " + i);
            try {
                Thread.sleep(1000); // 休眠 1 秒
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

​				

2. 在需要创建线程的地方创建 Thread 实例，将 `MyRunnable` 对象传递给 Thread 构造函数，并调用 `start()` 方法启动线程。

```java
MyRunnable myRunnable = new MyRunnable();
Thread thread = new Thread(myRunnable);
thread.start();
```

​			

完整的代码（比较不正常的写法）

```java
package com.fu.tt;
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.util.Log;


public class MainActivity extends AppCompatActivity implements Runnable  {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);


        Thread myThread = new Thread(this);
        myThread.start();
    }

    // 自定义线程类，继承自 Thread 类
    private static class MyThread extends Thread {
        @Override
        public void run() {
            super.run();

            // 在这里执行线程任务
            for (int i = 0; i < 5; i++) {
                Log.d("MyThread", "线程运行中：" + i);

                try {
                    // 模拟耗时任务，线程休眠1秒
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
    }

    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause()
    {
        super.onPause();
    }

    @Override
    public void run() {
        for (int i = 0; i < 100; i++) {
            Log.d("MyRunnable", "MyRunnable is running: " + i);
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

​			

完整的代码（比较正常的写法）

MainActivity.java

```java
package com.fu.tt;
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.util.Log;


public class MainActivity extends AppCompatActivity   {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        MyRunnable myRunnable = new MyRunnable();
        Thread myThread = new Thread(myRunnable);
        myThread.start();
    }

    // 自定义线程类，继承自 Thread 类
    private static class MyThread extends Thread {
        @Override
        public void run() {
            super.run();

            // 在这里执行线程任务
            for (int i = 0; i < 5; i++) {
                Log.d("MyThread", "线程运行中：" + i);

                try {
                    // 模拟耗时任务，线程休眠1秒
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
    }

    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause()
    {
        super.onPause();
    }
}
```

​					

MyRunnable.java

```java
package com.fu.tt;

import android.util.Log;

public class MyRunnable implements Runnable {
    @Override
    public void run() {
        for (int i = 0; i < 100; i++) {
            Log.d("MyRunnable", "MyRunnable is running: " + i);
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

```

​			

**这两种方式有什么区别，为什么要大费周章的使用第二种方式?**

**1. 继承关系**

方法一是通过继承 Thread 类来实现多线程，方法二是通过实现 Runnable 接口来实现多线程。Java 语言不支持多重继承，因此，如果一个类已经继承了其他类，就无法再继承 Thread 类。在这种情况下，实现 Runnable 接口就成了实现多线程的唯一选择。

**2. 资源共享**

当使用继承 Thread 类的方法创建线程时，每个线程都拥有自己的实例变量。这意味着，每个线程之间是相互独立的，它们不共享实例变量。而使用 Runnable 接口的方法，由于多个线程共享同一个 Runnable 实例，因此，它们可以共享实例变量，更容易实现资源共享。

**3. 代码复用**

实现 Runnable 接口的方式更具代码复用性。当一个类实现了 Runnable 接口，它可以作为一个线程任务，也可以作为一个普通的类被其他类调用。而继承 Thread 类的方式则限制了代码复用性，因为它是一个线程类，只能用于线程任务。

**4. 灵活性**

实现 Runnable 接口允许您更灵活地组织代码。例如，可以创建一个工作类，实现 Runnable 接口，并在该类中实现多个任务。然后，可以通过创建多个线程，为每个线程分配一个任务，以实现并发执行。这样的代码组织更加清晰和灵活。

总结起来，使用实现 Runnable 接口的方式更具灵活性、代码复用性和资源共享性。在实际开发中，实现 Runnable 接口的方式比继承 Thread 类更受推荐。当然，根据具体需求和场景，您可以选择适合您的方法。

接下来，我们通过代码一一来看他的优势

​				

### 多线程开发（Thread 类_Runnabled的继承优势）

以下是一个使用 `Runnable` 的例子，该例子展示了当一个类已经继承了另一个类时，为什么需要实现 `Runnable` 接口以实现多线程			

​				

首先，创建一个名为 `BaseClass.java` 的新文件，并定义 `BaseClass` 类：

```java
public class BaseClass {
    public void baseMethod() {
        Log.d("BaseClass", "This is a method in the base class.");
    }
}
```

​			

然后创建一个名为 `MyExtendedClass.java` 的新文件，继承 `BaseClass` 类并实现 `Runnable` 接口：

```java
public class MyExtendedClass extends BaseClass implements Runnable {
    @Override
    public void run() {
        Log.d("MyExtendedClass", "MyExtendedClass is running.");
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

​				

接下来，在你的主要活动或其他类中，你可以创建一个 `MyExtendedClass` 实例，启动一个新线程并调用 `baseMethod()`：

```java
public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        MyExtendedClass myExtendedClass = new MyExtendedClass();
        Thread myThread = new Thread(myExtendedClass);
        myThread.start();
        myExtendedClass.baseMethod();
    }
}
```

在这个例子中，`MyExtendedClass` 类继承了 `BaseClass` 并实现了 `Runnable` 接口。由于 Java 不支持多重继承，我们不能同时继承 `BaseClass` 和 `Thread`。但是，我们可以实现 `Runnable` 接口，从而让 `MyExtendedClass` 具有多线程功能，同时保留对 `BaseClass` 的继承。这使得 `MyExtendedClass` 可以访问 `BaseClass` 中的方法，如 `baseMethod()`。

​				

### 多线程开发（Thread 类_Runnabled的资源共享优势）

MainActivity.java

```java
package com.fu.tt;
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.util.Log;
import android.widget.TextView;


public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

      // 他们对于同一个 sharedCounter 的counter 数值进行增加，一个增加100，如果两者互不通信，那么最后显示结果肯定是 100 ，如果两个都对同一个 sharedCounter 操作，也就是尽心了通信，那么最后就是200
        Counter sharedCounter = new Counter(0);

        Thread thread1 = new Thread(new IncrementTask(sharedCounter));
        Thread thread2 = new Thread(new IncrementTask(sharedCounter));

        thread1.start();
        thread2.start();

      // 他的作用是阻塞当前的主线程，也就是，UI线程，目的是，等待我们的加数线程都运行结束以后，才更新UI
      // 如果阻塞，可能两边线程各自加了50，总数就是100。还以为没有进行通信呢
        try {
            thread1.join();
            thread2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
// 这个作用是更新UI，加上这个的目的是确保我们的更新，UI的工作是在主线程上面运行的，在我们的例子当中，不是那么的必要
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                TextView textView = findViewById(R.id.textView);
                textView.setText("Counter value: " + sharedCounter.getValue());
            }
        });
    }



    @Override
    protected void onDestroy() {
        super.onDestroy();
    }

    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause()
    {
        super.onPause();
    }
}
```

​			

Counter.java

```java
package com.fu.tt;

public class Counter {
    private int value;

    public Counter(int initialValue) {
        value = initialValue;
    }

    public void increment() {
        value++;
    }

    public int getValue() {
        return value;
    }
}

```

​			

IncrementTask.java

```java
package com.fu.tt;

public class IncrementTask implements Runnable {
    private Counter counter;

    public IncrementTask(Counter counter) {
        this.counter = counter;
    }

    @Override
    public void run() {
        for (int i = 0; i < 100; i++) {
            counter.increment();
        }
    }
}
```

​			

#### runOnUiThread()

这个是保证我们的更改 UI 的代码一定执行在 UI 主线程上面					

MainActivity.java				

```java
package com.fu.tt;
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;


public class MainActivity extends AppCompatActivity {
    private TextView textView;
    private Button button;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        button = findViewById(R.id.button);
        textView = findViewById(R.id.textView);

        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                performLongRunningTaskAndUpdateTextView();
            }
        });
    }


    @Override
    protected void onDestroy() {
        super.onDestroy();
    }

    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause()
    {
        super.onPause();
    }

    private void performLongRunningTask() {
        new Thread(new Runnable() {
            @Override
            public void run() {
                simulateLongRunningTask();
                updateUIAfterTaskCompletion();
                runOnUiThread(new Runnable() {
                    @Override
                    public void run() {

                    }
                });
            }
        }).start();
    }

    private void simulateLongRunningTask() {
        // 模拟耗时任务（如网络请求）
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    private void updateUIAfterTaskCompletion() {

        textView.setText("Task completed");
    }

    private void performLongRunningTaskAndUpdateTextView() {
        new Thread(new Runnable() {
            @Override
            public void run() {
                // 模拟耗时操作
                try {
                    Thread.sleep(2000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }

                // 耗时操作完成，更新 TextView
                runOnUiThread(new Runnable() {
                    @Override
                    public void run() {
                        textView.setText("Task completed!");
                    }
                });
            }
        }).start();
    }
}
```

在这个案例当中，我们把更新UI 的操作移步到了，一个线程当中，但是，在执行的时候，又通过 runOnUiThread  这样的方式，对我们的，更新代码强制在 主线程当中运行 （但是你会发现，即便是将 runOnUiThread 这个部分的代码删掉，程序依然会成功的运行，并且没有任何的错误，这个错误，在不同的设备上的是否触发，有随机性）

​			

#### 使用 Lambda 表达式简化 Runnable

```java
Runnable runnable = () -> {
    System.out.println("Hello from the Runnable implemented with a Lambda expression!");
};
```

​			

```java
new Thread(() -> {
    // 这里执行任务
}).start();
```

​			

其实就是省掉了

```java
                    @Override
                    public void run() {
                        ...
                    }
```

变成了

```java
() -> textView.setText("Task completed!")
```

​					

对比下面的两个代码

```java
package com.fu.tt;
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;


public class MainActivity extends AppCompatActivity {
    private TextView textView;
    private Button button;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        button = findViewById(R.id.button);
        textView = findViewById(R.id.textView);

        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                performLongRunningTaskAndUpdateTextView();
            }
        });
    }


    @Override
    protected void onDestroy() {
        super.onDestroy();
    }

    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause()
    {
        super.onPause();
    }

    private void performLongRunningTask() {
        new Thread(new Runnable() {
            @Override
            public void run() {
                simulateLongRunningTask();
                updateUIAfterTaskCompletion();
                runOnUiThread(new Runnable() {
                    @Override
                    public void run() {

                    }
                });
            }
        }).start();
    }

    private void simulateLongRunningTask() {
        // 模拟耗时任务（如网络请求）
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    private void updateUIAfterTaskCompletion() {

        textView.setText("Task completed");
    }

    private void performLongRunningTaskAndUpdateTextView() {
        new Thread(new Runnable() {
            @Override
            public void run() {
                // 模拟耗时操作
                try {
                    Thread.sleep(2000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }

                // 耗时操作完成，更新 TextView
                runOnUiThread(new Runnable() {
                    @Override
                    public void run() {
                        textView.setText("Task completed!");
                    }
                });
            }
        }).start();
    }
}
```

​			

```java
import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button button = findViewById(R.id.button);
        TextView textView = findViewById(R.id.textView);

        button.setOnClickListener(view -> {
            // 使用 Lambda 表达式实现 Runnable
            Runnable task = () -> {
                try {
                    // 模拟一个耗时任务
                    Thread.sleep(3000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }

                // 更新 UI 必须在 UI 线程中进行
                runOnUiThread(() -> textView.setText("Task completed!"));
            };

            // 创建并启动一个新线程来执行任务
            new Thread(task).start();
        });
    }
}
```





#### 使用线程池执行 Runnable 任务_FixedThreadPool

线程池是一种管理线程的机制，它允许您事先创建多个线程并将它们保存在一个池中。当需要执行任务时，线程池会从池中获取一个空闲的线程来执行任务。任务完成后，线程返回池中，等待下一个任务。线程池的好处在于减少了线程的创建和销毁开销，同时能更有效地管理系统资源。

​				

FixedThreadPool：这是一个拥有固定数量线程的线程池。任务提交时，如果线程池中有空闲线程，它将被用于执行任务。如果没有空闲线程，任务将被排队等待。

​			

```java
package com.fu.tt;
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;



public class MainActivity extends AppCompatActivity {
    private TextView textView;
    private Button button;
    private ExecutorService executorService;

    private static final String TAG = "ThreadPoolExample";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button button = findViewById(R.id.button);
        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                executeTasks();
            }
        });
    }

    private void executeTasks() {
        ExecutorService  = Executors.newFixedThreadPool(4);

        Runnable task1 = new Runnable() {
            @Override
            public void run() {
                for (int i = 0; i < 10; i++) {
                    Log.d(TAG, "Task 1 - Number: " + i);
                }
            }
        };

        Runnable task2 = new Runnable() {
            @Override
            public void run() {
                for (int i = 0; i < 10; i++) {
                    Log.d(TAG, "Task 2 - Number: " + i);
                }
            }
        };

        Runnable task3 = new Runnable() {
            @Override
            public void run() {
                for (int i = 0; i < 10; i++) {
                    Log.d(TAG, "Task 3 - Number: " + i);
                }
            }
        };

        Runnable task4 = new Runnable() {
            @Override
            public void run() {
                for (int i = 0; i < 10; i++) {
                    Log.d(TAG, "Task 4 - Number: " + i);
                }
            }
        };

        // 提交任务到线程池
        executorService.execute(task1);
        executorService.execute(task2);
        executorService.execute(task3);
        executorService.execute(task4);

        // 关闭线程池（在完成所有任务后）
        executorService.shutdown();
    }


    @Override
    protected void onDestroy() {
        super.onDestroy();
        // 关闭线程池，释放资源
        executorService.shutdown();
    }


    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause()
    {
        super.onPause();
    }
}
```

​				

#### 使用线程池执行 Runnable 任务_CachedThreadPool

`CachedThreadPool` 是 Java 提供的一种线程池实现，它具有动态调整线程数量的特点。当需要执行新任务时，`CachedThreadPool` 会尝试重用之前创建的空闲线程。如果没有空闲线程可用，`CachedThreadPool` 会创建一个新线程来执行任务。当线程完成任务并变为空闲时，如果在一定时间内（默认为 60 秒）没有新任务分配给该线程，线程将被终止并从线程池中移除。这种特性使得 `CachedThreadPool` 在执行大量短时任务时表现出较高的性能。			



MainActivity.java

```java
package com.fu.tt;
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;


public class MainActivity extends AppCompatActivity {
    private TextView textView;
    private Button button;
    private ExecutorService executorService;

    private static final String TAG = "CachedThreadPoolExample";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        executorService = Executors.newFixedThreadPool(4);

        Button button = findViewById(R.id.button);
        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                executeTasks();
            }
        });
    }

    private void executeTasks() {
        // 创建线程池
        ExecutorService executorService = Executors.newCachedThreadPool();

        // 创建任务
        Runnable task1 = () -> {
            for (int i = 0; i < 10; i++) {
                Log.d(TAG, "Task 1 - Number: " + i);
            }
        };

        Runnable task2 = () -> {
            for (int i = 0; i < 10; i++) {
                Log.d(TAG, "Task 2 - Number: " + i);
            }
        };

        Runnable task3 = () -> {
            for (int i = 0; i < 10; i++) {
                Log.d(TAG, "Task 3 - Number: " + i);
            }
        };

        // 提交任务到线程池
        executorService.execute(task1);
        executorService.execute(task2);
        executorService.execute(task3);

        // 关闭线程池（在完成所有任务后）
        executorService.shutdown();
    }


    @Override
    protected void onDestroy() {
        super.onDestroy();
        // 关闭线程池，释放资源
        executorService.shutdown();
    }


    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause()
    {
        super.onPause();
    }
}
```

​				

#### 使用线程池执行 Runnable 任务_ScheduledThreadPool

`ScheduledThreadPool` 是 Java 提供的一种线程池实现，它允许您在指定的延迟后执行任务，或者按照固定的时间间隔定期执行任务。

```java
import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.widget.Button;

import java.util.concurrent.Executors;
import java.util.concurrent.ScheduledExecutorService;
import java.util.concurrent.TimeUnit;

public class MainActivity extends AppCompatActivity {

    private static final String TAG = "ScheduledThreadPoolExample";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button button = findViewById(R.id.button);
        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                scheduleTasks();
            }
        });
    }

    private void scheduleTasks() {
        ScheduledExecutorService scheduledExecutorService = Executors.newScheduledThreadPool(2);

        // 延迟任务
        Runnable delayedTask = () -> Log.d(TAG, "Delayed task executed");
        scheduledExecutorService.schedule(delayedTask, 3, TimeUnit.SECONDS);

        // 定期任务
        Runnable periodicTask = () -> Log.d(TAG, "Periodic task executed");
        scheduledExecutorService.scheduleAtFixedRate(periodicTask, 5, 2, TimeUnit.SECONDS);
    }
}
```

翻译

scheduled ： 计划中的

Fixed ：固定的

Rate ：频率

period ：周期



​			

```java
        Runnable delayedTask = () -> Log.d(TAG, "Delayed task executed");
        scheduledExecutorService.schedule(delayedTask, 3, TimeUnit.SECONDS);
```

delayedTask : 任务

3 TimeUnit.SECONDS ： 延迟 3 秒钟

​			

```java
        // 定期任务
        Runnable periodicTask = () -> Log.d(TAG, "Periodic task executed");
        scheduledExecutorService.scheduleAtFixedRate(periodicTask, 5, 2, TimeUnit.SECONDS);
```

1. `periodicTask`：这是要执行的任务，它实现了 `Runnable` 接口。
2. `5`：这是一个整数值，表示任务的**初始延迟**。这意味着任务将在 5 秒后开始执行。
3. `2`：这是一个整数值，表示任务执行之间的**固定周期**。这意味着任务开始执行后，每隔 2 秒将再次执行一次。
4. `TimeUnit.SECONDS`：这是一个枚举值，表示时间单位。在这个例子中，它表示初始延迟和固定周期的时间单位都是秒。

​				

如果我们延迟 3 小时，但是每隔秒钟执行一次，应该怎么办呢？也就是说，延迟时间和固定周期的时间单位不一样				

​				

```java
ScheduledExecutorService scheduledExecutorService = Executors.newScheduledThreadPool(1);
Runnable periodicTask = new Runnable() {
    @Override
    public void run() {
        // 你的任务代码
    }
};

long initialDelay = TimeUnit.HOURS.toSeconds(3); // 将 3 小时转换为秒
scheduledExecutorService.scheduleAtFixedRate(periodicTask, initialDelay, 2, TimeUnit.SECONDS);

```

​				

#### 使用线程池执行 Runnable 任务_SingleThreadExecutor

`SingleThreadExecutor` 是一个线程池实现，它只使用一个工作线程来执行任务。这个线程池的主要特点是任务会按照提交顺序依次执行。因为它只有一个线程，所以能保证任务之间的顺序性，不会出现多线程执行时的竞争问题。这种线程池适用于需要顺序执行的任务场景。

​			

MainActivity.java

```java
package com.fu.tt;
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;


public class MainActivity extends AppCompatActivity {
    private TextView textView;
    private Button button;
    private ExecutorService executorService;


    private ExecutorService singleThreadExecutor;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        singleThreadExecutor = Executors.newSingleThreadExecutor();

        Button button = findViewById(R.id.button);
        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                singleThreadExecutorTasks();
            }
        });
    }

    private void singleThreadExecutorTasks() {
        Runnable task1 = new Runnable() {
            @Override
            public void run() {
                Log.i("SingleThreadExecutor", "Task 1 is running");
            }
        };

        Runnable task2 = new Runnable() {
            @Override
            public void run() {
                Log.i("SingleThreadExecutor", "Task 2 is running");
            }
        };

        Runnable task3 = new Runnable() {
            @Override
            public void run() {
                Log.i("SingleThreadExecutor", "Task 3 is running");
            }
        };

        singleThreadExecutor.execute(task1);
        singleThreadExecutor.execute(task2);
        singleThreadExecutor.execute(task3);
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        // 关闭线程池，释放资源
        singleThreadExecutor.shutdown();
    }

    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause()
    {
        super.onPause();
    }
}
```

这个是依次执行的

​			

### 多线程_Android 中与其他组件配合使用 Runnable









### 多线程 AsyncTask

**自 Android 11（API 级别 30）开始已被弃用**				

AsyncTask 类是 Android 提供的一个便捷的类，用于在后台线程上执行异步任务，同时在 UI 线程上更新用户界面。AsyncTask 通常用于执行较短时间的后台任务，如从网络加载数据、文件操作或者数据库查询等。

AsyncTask 的工作原理是在后台线程上执行任务，然后在任务完成时，通知 UI 线程进行界面更新。这样可以确保用户界面保持响应，避免因为耗时操作而卡住。			



&&&







-------

### Handler_通信

Handler 的作用是将任务投递到指定的线程中执行。它并不负责创建或管理线程，而是在已有的线程（如主线程或子线程）中调度任务。同时，Handler 可以携带一些信息，以便在任务执行过程中使用

Handler 是 Android 中一个非常有用的组件，它允许您在不同线程之间进行**通信和任务调度**。Handler 主要用于在后台线程执行任务并将结果传递回主线程（UI线程）。

​				

翻译

Handler ：处理程序

Looper ：循环器

​			

下面这个代码演示如何在后台线程执行任务并更新 UI。在这个示例中，我们将创建一个简单的计时器，在后台线程中每隔一秒更新计数器，并将其显示在 TextView 中			

activity_layout.xml			

```xml
<TextView
    android:id="@+id/textView"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Count: 0" />
```

​						

Mainacttivity.java

```java
package com.fu.tt;
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.os.Handler;
import android.os.Looper;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

import java.util.concurrent.ExecutorService;

public class MainActivity extends AppCompatActivity {
    private TextView textView;
    private Button button;
    private Handler handler;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        handler = new Handler(Looper.getMainLooper());


        Button button = findViewById(R.id.button);
        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                startCounter();
            }
        });
    }
    private void startCounter() {
        new Thread(new Runnable() {
            @Override
            public void run() {
                for (int i = 1; i <= 1000; i++) {
                    // 模拟耗时任务（例如计算或网络请求）
                    try {
                        Thread.sleep(100);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }

                    // 将计数值传递给主线程以更新 UI
                    int finalI = i;
                    handler.post(new Runnable() {
                        @Override
                        public void run() {
                            TextView textView = findViewById(R.id.textView);
                            textView.setText("Count: " + finalI);
                        }
                    });
                }
            }
        }).start();
    }



    @Override
    protected void onDestroy() {
        super.onDestroy();
    }


    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause()
    {
        super.onPause();
    }
}
```

​				

分析代码

```java
handler = new Handler(Looper.getMainLooper());
```

 `Handler` 对象，它关联到主线程（UI线程）的 `Looper`			

​			

`Looper.getMainLooper()`：`Looper` 是一个消息循环处理器，它在一个线程中管理一个消息队列。每个线程只能有一个 `Looper`。`getMainLooper()` 是一个静态方法，用于获取主线程（UI线程）的 `Looper` 对象。		

​		

```java
                    handler.post(new Runnable() {
                        @Override
                        public void run() {
                            TextView textView = findViewById(R.id.textView);
                            textView.setText("Count: " + finalI);
                        }
                    });
```

下面是 `handler.post()` 方法的简要说明：

- 参数：一个实现了 `Runnable` 接口的对象。这个对象的 `run()` 方法将在与 `Handler` 关联的线程中执行。
- 返回值：一个布尔值，表示 `Runnable` 对象是否成功添加到消息队列。如果成功添加，返回 `true`；否则返回 `false`

​			

将代码改成 runOnUiThread 也是可以的，能够保证修改 UI线程 的代码，运行在，UI线程上

```java
package com.fu.tt;
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.os.Handler;
import android.os.Looper;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

import java.util.concurrent.ExecutorService;

public class MainActivity extends AppCompatActivity {
    private TextView textView;
    private Button button;
    private Handler handler;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        handler = new Handler(Looper.getMainLooper());


        Button button = findViewById(R.id.button);
        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                startCounter();
            }
        });
    }
    private void startCounter() {
        new Thread(new Runnable() {
            @Override
            public void run() {
                for (int i = 1; i <= 1000; i++) {
                    // 模拟耗时任务（例如计算或网络请求）
                    try {
                        Thread.sleep(100);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }

                    // 将计数值传递给主线程以更新 UI
                    int finalI = i;
                    runOnUiThread(new Runnable() {
                        @Override
                        public void run() {
                            TextView textView = findViewById(R.id.textView);
                            textView.setText("Count: " + finalI);
                        }
                    });
                }
            }
        }).start();
    }


    @Override
    protected void onDestroy() {
        super.onDestroy();
    }


    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause()
    {
        super.onPause();
    }
}
```

​			

### 在其他的线程当中创建 looper

在刚刚的代码当中，我们知道

```java
handler = new Handler(Looper.getMainLooper());
```

1. `Handler`：`Handler` 是 Android 系统提供的一个组件，用于在不同线程之间传递和处理消息。通常，它用于将后台线程的计算结果传递给主线程以更新 UI。`Handler` 的主要功能是将 `Runnable` 对象或 `Message` 对象发送到关联的 `Looper` 的消息队列中。
2. `Looper.getMainLooper()`：`Looper` 是一个消息循环处理器，它在一个线程中管理一个消息队列。每个线程只能有一个 `Looper`。`getMainLooper()` 是一个静态方法，用于获取主线程（UI线程）的 `Looper` 对象。
3. `new Handler(Looper.getMainLooper())`：这个构造函数创建一个新的 `Handler` 实例，并将其关联到传入的 `Looper` 对象。在这个例子中，我们传入了主线程的 `Looper`，这意味着我们创建的 `Handler` 对象与主线程关联。

​			

那么 `Looper.getMainLooper() ` `getMainLooper()` 是一个静态方法，用于获取主线程（UI线程）的 `Looper` 对象，那我们如何获取，其他线程的 looper 呢？			

​						

以下是一个完整的例子，演示了如何在一个新的线程中创建一个 `Looper`，并通过 `Handler` 在主线程和新线程之间发送消息。在这个例子中，我们将在新线程中计算斐波那契数列的第 n 项，并将结果显示在主线程的 `TextView` 上。			

​				

```java
package com.fu.tt;
import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.os.Handler;
import android.os.Looper;
import android.os.Message;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

import java.util.concurrent.ExecutorService;

public class MainActivity extends AppCompatActivity {
    private TextView textView;
    private Handler mainHandler;
    private Handler workerHandler;

    private static final int MESSAGE_TYPE_FIBONACCI_RESULT = 1;


    @Override
    protected void onCreate(Bundle savedInstanceState) {

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        textView = findViewById(R.id.textView);

        mainHandler = new Handler(Looper.getMainLooper()) {
            @Override
            public void handleMessage(Message msg)
            {
                if (msg.what == MESSAGE_TYPE_FIBONACCI_RESULT) {
                    int result = msg.arg1;
                    textView.setText("Fibonacci result: " + result);
                }
            }
        };

        MyLooperThread myLooperThread = new MyLooperThread();
        myLooperThread.start();

        // 等待 workerHandler 初始化完成
        while ((workerHandler = myLooperThread.getHandler()) == null) {
            try {
                Thread.sleep(100);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

        // 计算斐波那契数列的第 10 项
        Message workerMessage = Message.obtain(workerHandler, 10);
        workerHandler.sendMessage(workerMessage);
    }

    private class MyLooperThread extends Thread {
        private Handler handler;

        @Override
        public void run() {
            Looper.prepare();
            handler = new Handler(Looper.myLooper()) {
                @Override
                public void handleMessage(Message msg) {
                    int n = msg.what;
                    int result = fibonacci(n);

                    Message mainMessage = Message.obtain(mainHandler, MESSAGE_TYPE_FIBONACCI_RESULT);
                    mainMessage.arg1 = result;
                    mainHandler.sendMessage(mainMessage);
                }
            };
            Looper.loop();
        }

      // 用于判断，是不是已经新建成功
        public Handler getHandler() {
            return handler;
        }

        private int fibonacci(int n) {
            if (n <= 1) {
                return n;
            }
            return fibonacci(n - 1) + fibonacci(n - 2);
        }
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
    }

    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause()
    {
        super.onPause();
    }
}
```

​			

这个示例中，我们创建了一个名为 `MyLooperThread` 的子类，它从 `Thread` 继承。在该线程的 `run` 方法中，我们调用 `Looper.prepare()` 和 `Looper.loop()` 以在新线程中创建一个 `Looper`。我们还创建了一个 `Handler` 对象，它用于处理从主线程发送过来的消息。

在 `MainActivity` 的 `onCreate` 方法中，我们启动了 `MyLooperThread`，等待它的 `Handler` 初始化完成。然后，我们通过发送一个消息来请求计算斐波那契数列的第 10 项。`MyLooperThread` 的 `Handler` 接收到消息后，计算结果并将其发送回主线程，主线程的 `Handler` 更新 `TextView` 以显示结果					

​				

`Looper.prepare()` 和 `Looper.loop()` 是 `Looper` 类的方法，它们用于在新线程中创建一个消息循环。下面是对这两个方法的详细解释：

1. `Looper.prepare()`: 这个方法会在当前线程中初始化一个新的 `Looper` 实例。每个线程只能有一个 `Looper` 实例，所以 `prepare()` 方法只能在一个线程中调用一次。调用 `Looper.prepare()` 会为当前线程创建一个与之关联的消息队列。
2. `Looper.loop()`: 这个方法会启动消息循环。它从与当前线程关联的消息队列中获取消息，并将它们分发给相应的 `Handler`。`Looper.loop()` 会一直运行，直到消息队列为空且没有活动的 `Handler` 时才会退出。当一个线程调用了 `Looper.loop()`，它会一直处理消息，直到循环结束。这就是为什么称之为消息循环。

当您想要在一个新线程中创建一个 `Looper` 时，您需要调用 `Looper.prepare()` 和 `Looper.loop()`。首先，调用 `Looper.prepare()` 来创建一个新的 `Looper` 实例并设置与当前线程关联的消息队列。接下来，创建一个或多个 `Handler`，它们将负责处理消息。最后，调用 `Looper.loop()` 启动消息循环。

​				

### import android.os.Message

`Message` 是 Android 中用于在线程之间传递信息的一个轻量级的数据结构。`Message` 通常与 `Handler` 一起使用，用于在线程之间发送消息，实现线程间通信。

以下是 `Message` 的一些关键概念和属性：

1. `what`：一个整型字段，用于表示消息的类型。您可以在发送和处理消息时使用这个字段来区分不同类型的消息。
2. `arg1` 和 `arg2`：这是两个整型字段，您可以用它们携带一些整数数据。这对于携带简单的数据非常有用，但是对于更复杂的数据结构，您可能需要使用下面提到的 `obj` 字段。
3. `obj`：一个 `Object` 字段，您可以用它携带任何类型的对象数据。请注意，您需要确保在发送和接收消息时正确地处理这个字段中的对象类型。
4. `when`：一个长整型字段，表示消息何时应该被处理。当您通过 `Handler` 发送延时消息时，`when` 字段会自动设置为系统时间加上延迟的毫秒数。

​				

```java
package com.fu.tt;
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.os.Handler;
import android.os.Looper;
import android.os.Message;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

import java.util.concurrent.ExecutorService;

public class MainActivity extends AppCompatActivity {
    private TextView textView;
    private MyLooperThread myLooperThread;
    private Handler mainHandler;
    private Handler handler;

    private static final int MESSAGE_TYPE_UPDATE_TEXT = 1;

    @Override
    protected void onCreate(Bundle savedInstanceState) {

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        textView = findViewById(R.id.textView);

        handler = new Handler(Looper.getMainLooper()) {
            @Override
            public void handleMessage(Message msg) {
                if (msg.what == MESSAGE_TYPE_UPDATE_TEXT) {
                    String text = (String) msg.obj;
                    textView.setText(text);
                }
            }
        };


        new Thread(new Runnable() {
            @Override
            public void run() {
                String newText = "Hello from background thread!";
                Message message = Message.obtain(handler, MESSAGE_TYPE_UPDATE_TEXT);
                message.obj = newText;
                handler.sendMessage(message);
            }
        }).start();
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
    }


    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause()
    {
        super.onPause();
    }
}
```

​			

```java
        new Thread(new Runnable() {
            @Override
            public void run() {
                String newText = "Hello from background thread!";
                Message message = Message.obtain(handler, MESSAGE_TYPE_UPDATE_TEXT);
                message.obj = newText;
                handler.sendMessage(message);
            }
        }).start();
```

1. `new Thread(new Runnable() {...}).start();`：这里创建了一个新的线程，并传入一个 `Runnable` 对象，这个对象包含了线程要执行的代码。然后调用 `start()` 方法启动这个线程。
2. `@Override public void run() {...}`：这是 `Runnable` 接口的 `run()` 方法。这个方法包含了在线程中要执行的代码。当线程启动时，它将自动调用这个方法。
3. `String newText = "Hello from background thread!";`：这是一个简单的字符串变量，我们将在后续的代码中将其作为消息发送给主线程。
4. `Message message = Message.obtain(handler, MESSAGE_TYPE_UPDATE_TEXT);`：这里我们使用 `Message.obtain()` 方法创建一个新的 `Message` 实例。我们传入一个 `Handler` 对象（在本例中是主线程的 `handler`）和一个整数 `MESSAGE_TYPE_UPDATE_TEXT`（用于表示消息类型）。这样我们可以在 `handleMessage()` 方法中根据 `what` 字段区分消息类型。
5. `message.obj = newText;`：这里我们将 `newText` 字符串赋值给 `Message` 的 `obj` 字段。这允许我们将字符串作为消息内容发送给主线程。
6. `handler.sendMessage(message);`：这里我们使用 `handler` 的 `sendMessage()` 方法将 `Message` 实例发送给主线程。当主线程收到这个消息时，它将在 `handleMessage()` 方法中处理消息，并根据 `what` 字段更新 UI。

​			

```java
        handler = new Handler(Looper.getMainLooper()) {
            @Override
            public void handleMessage(Message msg) {
                if (msg.what == MESSAGE_TYPE_UPDATE_TEXT) {
                    String text = (String) msg.obj;
                    textView.setText(text);
                }
            }
        };
```

1. `handler = new Handler(Looper.getMainLooper())`：这行代码创建了一个`Handler`对象，并将其与主线程的`Looper`对象关联起来。通过将`Looper.getMainLooper()`作为参数传递给`Handler`构造函数，我们告诉这个`Handler`处理来自主线程`Looper`的消息队列。因此，这个`Handler`可以在主线程中处理从其他线程发送过来的消息。
2. `public void handleMessage(Message msg)`：这个方法是`Handler`类的一个重要方法，需要我们重写以处理消息。这个方法会在主线程中被调用，以处理从其他线程发送过来的消息。
3. `if (msg.what == MESSAGE_TYPE_UPDATE_TEXT)`：`msg.what`是一个整数值，用于区分不同类型的消息。在这个例子中，我们检查`msg.what`是否等于预先定义的`MESSAGE_TYPE_UPDATE_TEXT`常量，以确定是否需要处理这条消息。
4. `String text = (String) msg.obj`：如果消息的类型是`MESSAGE_TYPE_UPDATE_TEXT`，我们将`msg.obj`转换为`String`类型。在这个例子中，`msg.obj`包含了我们要在`TextView`中显示的文本。
5. `textView.setText(text)`：最后，我们使用`setText()`方法将`TextView`的文本设置为从`msg.obj`获取的字符串。这样，主线程就可以根据从其他线程发送过来的消息更新UI。

​				

### import android.os.Message_arg1和arg2

`Message`对象中的`arg1`和`arg2`是两个整型字段（**如果是其他的数据类型，就用 message.obj** ），它们可以用于携带整数类型的数据。这对于在消息中传递简单的整数数据非常有用。它们可以作为额外的信息与`msg.what`字段一起使用，以帮助接收方根据这些参数执行相应的操作。

```java
package com.fu.tt;
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.os.Handler;
import android.os.Looper;
import android.os.Message;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

import java.util.concurrent.ExecutorService;

public class MainActivity extends AppCompatActivity {
    private TextView textView;
    private Handler handler;

    public static final int OPERATION_ADD = 1;
    public static final int OPERATION_SUBTRACT = 2;


    @Override
    protected void onCreate(Bundle savedInstanceState) {

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        textView = findViewById(R.id.textView);

        handler = new Handler(Looper.getMainLooper()) {
            @Override
            public void handleMessage(Message msg) {
                int result = -1;
                if (msg.what == OPERATION_ADD) {
                    result = msg.arg1 + msg.arg2;
                } else if (msg.what == OPERATION_SUBTRACT) {
                    result = msg.arg1 - msg.arg2;
                }
                // 更新UI，例如显示结果
                textView.setText(String.valueOf(result));
            }
        };

        Message message = Message.obtain();
        message.what = OPERATION_SUBTRACT;
        message.arg1 = 3;
        message.arg2 = 5;
        handler.sendMessage(message);
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
    }


    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause()
    {
        super.onPause();
    }
}
```

我将`Message`对象的创建和发送移到了`onCreate()`方法的末尾。这样在创建`Handler`对象后，才会发送`Message`对象。否则，`Handler`对象可能尚未创建，而`Message`对象已经发送，这将导致无法处理消息

​			

在这次的创建 message 的时候，我们使用的是

```java
Message message = Message.obtain();
```

​			

而不是使用的

```java
Message message = Message.obtain(handler, MESSAGE_TYPE_UPDATE_TEXT);
```

​			

这是因为

```java
        Message message = Message.obtain();
        message.what = OPERATION_SUBTRACT;
        message.arg1 = 3;
        message.arg2 = 5;
        handler.sendMessage(message);
```

在后续的操作当中已经单独指定了 `message.what = OPERATION_SUBTRACT;`			

至于 handler ，在发送广播的时候 `handler.sendMessage(message);` 就已经指定了，在创建的时候指定，其实是有点画蛇添足的			

​			

### import android.os.Message_obj

`Message.obj` 是一个用于携带任意类型对象数据的字段。在使用 `Message` 传递数据时，您可以将需要传递的对象赋值给 `obj` 字段。然后，在接收消息时，您需要根据发送的对象类型进行相应的处理。		

Person.java

```java
public class Person {
    public String name;
    public int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

​				

MainActivity.java

```java
public class MainActivity extends AppCompatActivity {
    private TextView textView;
    private Handler handler;

    public static final int MESSAGE_TYPE_PERSON = 1;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        textView = findViewById(R.id.textView);

        handler = new Handler(Looper.getMainLooper()) {
            @Override
            public void handleMessage(Message msg) {
                if (msg.what == MESSAGE_TYPE_PERSON) {
                    Person person = (Person) msg.obj;
                    String text = "Name: " + person.name + ", Age: " + person.age;
                    textView.setText(text);
                }
            }
        };

        new Thread(new Runnable() {
            @Override
            public void run() {
                Person person = new Person("Alice", 30);
                Message message = Message.obtain();
                message.what = MESSAGE_TYPE_PERSON;
                message.obj = person;
                handler.sendMessage(message);
            }
        }).start();
    }
}
```

在这个例子中，我们创建了一个 `Person` 对象并将其发送给主线程的 `Handler`。`Handler` 根据 `message.what` 判断消息类型，并将 `message.obj` 转换为 `Person` 类型，然后在 UI 上显示其属性。

需要注意的是，在使用 `Message.obj` 传递对象时，要确保发送和接收时正确处理对象类型，避免类型转换异常。

​				

### import android.os.Message_在message当中存放多个数据

可以发现，无论是， arg1_arg2 还是 obj 都只能存放一个数据，想要发送多个信息，可以考虑 Bundle 的数据（或者是在 msg.obj 当中传入一个 Bundle ）

```java
package com.fu.tt;
import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.os.Handler;
import android.os.Looper;
import android.os.Message;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

import java.util.concurrent.ExecutorService;

public class MainActivity extends AppCompatActivity {
    private TextView textView;
    private Handler handler;

    public static final int MESSAGE_TYPE_UPDATE_TEXT = 1;


    @Override
    protected void onCreate(Bundle savedInstanceState) {

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        textView = findViewById(R.id.textView);

        handler = new Handler(Looper.getMainLooper()) {
            @Override
            public void handleMessage(@NonNull Message msg) {
                if (msg.what == MESSAGE_TYPE_UPDATE_TEXT) {
                    Bundle data = msg.getData();
                    String newText = data.getString("newTextKey");
                    int someInt = data.getInt("someIntKey");
                    double someDouble = data.getDouble("someDoubleKey");

                    // 使用获取到的数据执行操作
                    textView.setText(newText);
                    // ...
                }
            }

        };

        new Thread(new Runnable() {
            @Override
            public void run() {
                String newText = "Hello from background thread!";
                int someInt = 42;
                double someDouble = 3.14;

                Message message = Message.obtain(handler, MESSAGE_TYPE_UPDATE_TEXT);

                // 创建一个 Bundle 对象，并将多个数据放入其中
                Bundle data = new Bundle();
                data.putString("newTextKey", newText);
                data.putInt("someIntKey", someInt);
                data.putDouble("someDoubleKey", someDouble);

                // 将 Bundle 对象与 Message 关联
                message.setData(data);

                handler.sendMessage(message);
            }
        }).start();

    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
    }


    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause()
    {
        super.onPause();
    }
}
```

​					

```java
package com.fu.tt;
import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.os.Handler;
import android.os.Looper;
import android.os.Message;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

import java.util.concurrent.ExecutorService;

public class MainActivity extends AppCompatActivity {
    private TextView textView;
    private Handler handler;

    public static final int MESSAGE_TYPE_UPDATE_TEXT = 1;


    @Override
    protected void onCreate(Bundle savedInstanceState) {

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        textView = findViewById(R.id.textView);

        handler = new Handler(Looper.getMainLooper()) {
            @Override
            public void handleMessage(@NonNull Message msg) {
                if (msg.what == MESSAGE_TYPE_UPDATE_TEXT) {
                    Bundle data = (Bundle) msg.obj;
                    String newText = data.getString("newTextKey");
                    int someInt = data.getInt("someIntKey");
                    double someDouble = data.getDouble("someDoubleKey");

                    // 使用获取到的数据执行操作
                    textView.setText(String.valueOf(someInt));
                    // ...
                }
            }

        };

        new Thread(new Runnable() {
            @Override
            public void run() {
                String newText = "Hello from background thread!";
                int someInt = 42;
                double someDouble = 3.14;

                Message message = Message.obtain(handler, MESSAGE_TYPE_UPDATE_TEXT);

                // 创建一个 Bundle 对象，并将多个数据放入其中
                Bundle data = new Bundle();
                data.putString("newTextKey", newText);
                data.putInt("someIntKey", someInt);
                data.putDouble("someDoubleKey", someDouble);

                // 将 Bundle 对象与 Message 关联
                message.obj = data;

                handler.sendMessage(message);
            }
        }).start();
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
    }


    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause()
    {
        super.onPause();
    }
}
```

​				

### import android.os.Message_msg.when

`Message.when` 是一个长整型字段，用于表示消息应该在何时被处理。在使用 `Handler` 发送延时消息时，`when` 字段会自动设置为当前系统时间加上延迟的毫秒数。`Handler` 内部会根据这个值进行消息调度和处理。

当您需要在一定时间后处理某个消息时，您可以使用 `Handler` 的 `sendMessageDelayed()` 方法，该方法需要指定一个延迟时间。例如，假设我们想要在 5 秒后更新 `TextView` 的文本：			

​				

handler.sendMessageDelayed(message, 5000);

```java
public class MainActivity extends AppCompatActivity {
    private TextView textView;
    private Handler handler;

    public static final int MESSAGE_TYPE_UPDATE_TEXT = 1;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        textView = findViewById(R.id.textView);

        handler = new Handler(Looper.getMainLooper()) {
            @Override
            public void handleMessage(Message msg) {
                if (msg.what == MESSAGE_TYPE_UPDATE_TEXT) {
                    textView.setText("Text updated after 5 seconds");
                }
            }
        };

        // 创建一个 Message 对象并设置其类型
        Message message = Message.obtain();
        message.what = MESSAGE_TYPE_UPDATE_TEXT;

        // 使用 sendMessageDelayed() 方法发送延时消息
        handler.sendMessageDelayed(message, 5000); // 延迟 5 秒
    }
}
```

​				

或者是				

sendMessageAtTime				

```java
public class MainActivity extends AppCompatActivity {
    private TextView textView;
    private Handler handler;

    public static final int MESSAGE_TYPE_UPDATE_TEXT = 1;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        textView = findViewById(R.id.textView);

        handler = new Handler(Looper.getMainLooper()) {
            @Override
            public void handleMessage(Message msg) {
                if (msg.what == MESSAGE_TYPE_UPDATE_TEXT) {
                    textView.setText("Text updated after 5 seconds");
                }
            }
        };

        // 创建一个 Message 对象并设置其类型
        Message message = Message.obtain();
        message.what = MESSAGE_TYPE_UPDATE_TEXT;

        // 设置 Message.when 字段为当前系统时间加上延迟的毫秒数
        long currentTimeMillis = SystemClock.uptimeMillis();
        long delayMillis = 5000;
        message.when = currentTimeMillis + delayMillis;

        // 使用 sendMessageAtTime() 方法发送延迟消息
        handler.sendMessageAtTime(message, message.when);
    }
}
```

​						

### Handle的线程之间的通信

在之前，我们已经讲解了如何做到，线程之间的通信，现在我们再看看，如何做到，线程之间的通信



```java
package com.fu.tt;
import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;

import android.content.pm.PackageManager;
import android.os.Bundle;
import android.os.Handler;
import android.os.Looper;
import android.os.Message;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.Manifest;

import java.util.concurrent.ExecutorService;

public class MainActivity extends AppCompatActivity {

    private static final int UPDATE_UI = 1;
    private Button button;
    private TextView textView;

    private Handler handler = new Handler(Looper.getMainLooper()) {
        @Override
        public void handleMessage(Message msg) {
            if (msg.what == UPDATE_UI) {
                textView.setText("耗时操作已完成");
            }
        }
    };

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        button = findViewById(R.id.button);
        textView = findViewById(R.id.textView);

        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                performTask();
            }
        });
    }


    // 在另一个线程，执行的耗时任务
    private void performTask() {
        new Thread(new Runnable() {
            @Override
            public void run() {
                try {
                    Thread.sleep(2000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }

                Message message = handler.obtainMessage(UPDATE_UI);
                handler.sendMessage(message);
            }
        }).start();
    }


    @Override
    protected void onDestroy() {
        super.onDestroy();
    }

    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause()
    {
        super.onPause();
    }
}
```



### Handler looper 还有 Runnable  这三个东西的关系

#### Handler

**作用与功能：**

1. 通信：`Handler` 用于在不同线程之间发送和处理消息。它可以将消息从一个线程发送到另一个线程，例如从后台线程发送消息到主线程（UI线程）。
2. 任务调度：`Handler` 还可以用于任务调度，即在指定的时间或时间间隔后执行特定任务。它提供了一系列方法（如 `post()`、`postDelayed()` 和 `postAtTime()`）来安排任务。

​			

#### Looper

**作用与功能：**

1. 消息循环：`Looper` 是一个运行在特定线程的消息循环，负责从与其关联的消息队列中取出并处理消息。每个线程只能有一个关联的 `Looper`，默认情况下，仅主线程（UI线程）有一个 `Looper`。
2. 管理消息队列：`Looper` 管理一个消息队列，它将接收到的消息和 `Runnable` 对象按照优先级和预定执行时间排序。当执行完一个任务后，`Looper` 将继续从队列中取出并执行下一个任务。		

​			

#### Runnable

**作用与功能：**

1. 封装任务：`Runnable` 是一个接口，用于封装要在特定线程上执行的任务。您可以通过实现 `Runnable` 接口的 `run()` 方法来定义任务内容。
2. 灵活调度：`Runnable` 对象可以直接传递给 `Handler` 的 `post()` 方法或作为消息的一部分发送。这为在不同线程之间调度任务提供了灵活性。

​		

简单来说，Runnable 的作用是，封装任务，Looper 的作用是，管理消息和任务，Handler 的作用是发送消息和任务

但是处理消息是在			

```java
    private Handler handler = new Handler(Looper.getMainLooper()) {
        @Override
        public void handleMessage(Message msg) {
            if (msg.what == UPDATE_UI) {
                textView.setText("耗时操作已完成");
            }
        }
    };
```

当中实现的			

​			

### Handle的任务调度

`Handler` 除了用于线程间通信外，还可以用于任务调度。任务调度是指在某个特定的时间或时间间隔后执行特定的任务。`Handler` 提供了 `post()`, `postDelayed()`, `postAtTime()` 等方法来实现任务调度。

1. `post(Runnable r)`: 将一个 `Runnable` 对象加入到消息队列中，该队列会被关联到 `Handler` 的 `Looper`。`Runnable` 会在下一个空闲时间执行。			

```java
handler.post(new Runnable() {
    @Override
    public void run() {
        // 在主线程执行的代码
    }
});
```

​				

2. `postDelayed(Runnable r, long delayMillis)`: 将一个 `Runnable` 对象加入到消息队列中，该队列会被关联到 `Handler` 的 `Looper`。`Runnable` 会在指定的延迟时间（以毫秒为单位）后执行。

```java
handler.postDelayed(new Runnable() {
    @Override
    public void run() {
        // 在主线程执行的代码
    }
}, 3000); // 延迟 3 秒执行
```

​			

3. `postAtTime(Runnable r, long uptimeMillis)`: 将一个 `Runnable` 对象加入到消息队列中，该队列会被关联到 `Handler` 的 `Looper`。`Runnable` 会在指定的系统运行时间（以毫秒为单位）后执行。

```java
long targetTime = SystemClock.uptimeMillis() + 5000; // 当前系统运行时间 + 5 秒
handler.postAtTime(new Runnable() {
    @Override
    public void run() {
        // 在主线程执行的代码
    }
}, targetTime);
```

​					

#### post(Runnable r)

`post(Runnable r)` 是 `Handler` 类中的一个方法，它用于将一个 `Runnable` 对象添加到与 `Handler` 关联的 `Looper` 的消息队列中。`Runnable` 对象中的任务将在 `Looper` 所关联的线程中执行。		

这里是 `post(Runnable r)` 方法的详细解释：

**功能：** 将一个 `Runnable` 对象添加到消息队列中，以便在 `Looper` 关联的线程上执行。

**参数：** `r` - 要执行的 `Runnable` 对象。

**返回值：** 如果成功将 `Runnable` 对象添加到消息队列，则返回 `true`；否则返回 `false`。



```java
package com.fu.tt;
import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;

import android.content.pm.PackageManager;
import android.os.Bundle;
import android.os.Handler;
import android.os.Looper;
import android.os.Message;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.Manifest;

import java.util.concurrent.ExecutorService;

public class MainActivity extends AppCompatActivity {

    private static final int UPDATE_UI = 1;
    private Button button;
    private TextView textView;

    private Handler mainThreadHandler = new Handler(Looper.getMainLooper());

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        button = findViewById(R.id.button);
        textView = findViewById(R.id.textView);

        mainThreadHandler = new Handler(Looper.getMainLooper());

        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                updateUI();
            }
        });
    }


    private void updateUI() {
        mainThreadHandler.post(new Runnable() {
            @Override
            public void run() {
                textView.setText("UI has been updated!");
            }
        });
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
    }

    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause()
    {
        super.onPause();
    }
}
```

​			

#### postDelayed(Runnable r, long delayMillis) 

**参数：**

- `r` - 要执行的 `Runnable` 对象。
- `delayMillis` - 延迟执行 `Runnable` 对象的时间，以毫秒为单位。

**返回值：** 如果成功将 `Runnable` 对象添加到消息队列，则返回 `true`；否则返回 `false`。

​			

```java
package com.fu.tt;
import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;

import android.content.pm.PackageManager;
import android.os.Bundle;
import android.os.Handler;
import android.os.Looper;
import android.os.Message;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.Manifest;

import java.util.concurrent.ExecutorService;

public class MainActivity extends AppCompatActivity {

    private static final int UPDATE_UI = 1;
    private Button button;
    private TextView textView;

    private Handler mainThreadHandler = new Handler(Looper.getMainLooper());

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        button = findViewById(R.id.button);
        textView = findViewById(R.id.textView);

        mainThreadHandler = new Handler(Looper.getMainLooper());

        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                updateUI();
            }
        });
    }


    private void updateUI() {
        mainThreadHandler.postDelayed(new Runnable() {
            @Override
            public void run() {
                textView.setText("UI has been updated!");
            }
        },3000); //3秒钟
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
    }

    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause()
    {
        super.onPause();
    }
}
```

​				

#### postAtTime(Runnable r, long uptimeMillis)

`postAtTime(Runnable r, long uptimeMillis)` 是 `Handler` 类中的一个方法，它用于将一个 `Runnable` 对象添加到与 `Handler` 关联的 `Looper` 的消息队列中，并在指定的系统运行时间（uptimeMillis）时执行。与 `post(Runnable r)` 和 `postDelayed(Runnable r, long delayMillis)` 类似，`Runnable` 对象中的任务将在 `Looper` 所关联的线程中执行。

​					

**功能：** 将一个 `Runnable` 对象添加到消息队列中，在指定的系统运行时间（uptimeMillis）时在 `Looper` 关联的线程上执行。

**参数：**

- `r` - 要执行的 `Runnable` 对象。
- `uptimeMillis` - 指定的系统运行时间，以毫秒为单位。这个值是从系统启动开始计算的，不包括深度睡眠时间。

**返回值：** 如果成功将 `Runnable` 对象添加到消息队列，则返回 `true`；否则返回 `false`。

​			

```java
package com.fu.tt;
import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;

import android.content.pm.PackageManager;
import android.os.Bundle;
import android.os.Handler;
import android.os.Looper;
import android.os.Message;
import android.os.SystemClock;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.Manifest;

import java.util.concurrent.ExecutorService;

public class MainActivity extends AppCompatActivity {

    private static final int UPDATE_UI = 1;
    private Button button;
    private TextView textView;

    private Handler mainThreadHandler = new Handler(Looper.getMainLooper());

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        button = findViewById(R.id.button);
        textView = findViewById(R.id.textView);

        mainThreadHandler = new Handler(Looper.getMainLooper());

        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                updateUI();
            }
        });
    }


    private void updateUI() {
        long currentTime = SystemClock.uptimeMillis();
        long targetTime = currentTime + 3000; // 在当前时间的基础上增加 3000 毫秒（3 秒）
        mainThreadHandler.postAtTime(new Runnable() {
            @Override
            public void run() {
                // 在主线程（UI线程）中执行的代码，例如更新 UI
                textView.setText("定时更新的内容");
            }
        }, targetTime);
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
    }

    protected void onResume()
    {
        super.onResume();
    }

    @Override
    protected void onPause()
    {
        super.onPause();
    }
}
```



#### SystemClock 的几种方法

`SystemClock.uptimeMillis()` 是 Android 中 `SystemClock` 类的一个方法，它返回自系统启动以来的时间（不包括设备处于深度睡眠状态的时间），单位为毫秒。这个方法在计算延迟、设定定时任务或者测量时间间隔等场景下非常有用。

`SystemClock.uptimeMillis()` 的返回值表示设备从启动到现在经过的时间，但不包括设备进入深度睡眠（如 CPU 休眠）的时间。这意味着在设备处于活跃状态时，这个值会持续增加，但在设备进入睡眠状态时，这个值会暂停。

`SystemClock` 类中还有其他几个与时间相关的方法，例如：

- `SystemClock.elapsedRealtime()`：返回自系统启动以来的时间，包括设备处于深度睡眠状态的时间，单位为毫秒。
- `SystemClock.currentThreadTimeMillis()`：返回当前线程已运行的时间，单位为毫秒。
- `SystemClock.sleep(long ms)`：使当前线程睡眠指定的毫秒数。

​			

### Handler.Callback

`mainThreadHandler = new Handler(Looper.getMainLooper())` 的方式并没有完全被淘汰，但是在某些场景下，使用 `Handler.Callback` 接口来处理消息更加推荐，因为这样可以更好地管理和组织代码。		

​				

`Handler.Callback` 接口允许您更加灵活地处理 `Handler` 收到的消息。当您在创建 `Handler` 对象时提供一个实现了 `Handler.Callback` 接口的对象，`Handler` 会将接收到的消息传递给该 `Callback` 对象的 `handleMessage(Message msg)` 方法处理。这样，**您可以将消息处理逻辑与 `Handler` 对象的创建分离**，使代码更加模块化和易于维护。**也就是说，可以在类里面重写消息/任务处理函数 handleMessage ，而不是，在创建的时候，一起写 handleMessage** 

​					

不使用 Handler.Callback

```java
package com.fu.tt;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.os.Handler;
import android.os.Looper;
import android.os.Message;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    private static final int MESSAGE_TYPE_1 = 1;
    private static final int MESSAGE_TYPE_2 = 2;

    private Button buttonType1;
    private Button buttonType2;

    private Handler mainThreadHandler;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        buttonType1 = findViewById(R.id.buttonType1);
        buttonType2 = findViewById(R.id.buttonType2);

        mainThreadHandler = new Handler(Looper.getMainLooper()) {
            @Override
            public void handleMessage(Message msg) {
                switch (msg.what) {
                    case MESSAGE_TYPE_1:
                        Toast.makeText(MainActivity.this, "Message type 1 received", Toast.LENGTH_SHORT).show();
                        break;
                    case MESSAGE_TYPE_2:
                        Toast.makeText(MainActivity.this, "Message type 2 received", Toast.LENGTH_SHORT).show();
                        break;
                    default:
                        super.handleMessage(msg);
                }
            }
        };

        buttonType1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                mainThreadHandler.sendEmptyMessage(MESSAGE_TYPE_1);
            }
        });

        buttonType2.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                mainThreadHandler.sendEmptyMessage(MESSAGE_TYPE_2);
            }
        });
    }
}
```

​				

加了Handler.Callback

```java
package com.fu.tt;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.os.Handler;
import android.os.Looper;
import android.os.Message;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity implements Handler.Callback {

    private static final int MESSAGE_TYPE_1 = 1;
    private static final int MESSAGE_TYPE_2 = 2;

    private Button buttonType1;
    private Button buttonType2;

    private Handler mainThreadHandler;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        buttonType1 = findViewById(R.id.buttonType1);
        buttonType2 = findViewById(R.id.buttonType2);

        mainThreadHandler = new Handler(Looper.getMainLooper(), this);

        buttonType1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                mainThreadHandler.sendEmptyMessage(MESSAGE_TYPE_1);
            }
        });

        buttonType2.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                mainThreadHandler.sendEmptyMessage(MESSAGE_TYPE_2);
            }
        });
    }

    @Override
    public boolean handleMessage(Message msg) {
        // 根据 msg.what 的值处理不同的消息
        switch (msg.what) {
            case MESSAGE_TYPE_1:
                // 处理类型为 MESSAGE_TYPE_1 的消息
                Toast.makeText(this, "Message type 1 received", Toast.LENGTH_SHORT).show();
                break;
            case MESSAGE_TYPE_2:
                Toast.makeText(this, "Message type 2 received", Toast.LENGTH_SHORT).show();
                // 处理类型为 MESSAGE_TYPE_2 的消息
                break;
            default:
                // 对于未知的消息类型，返回 false，表示消息未被处理
                return false;
        }
        // 返回 true，表示消息已被处理
        return true;
    }
}
```

​				

通过Lambda表达式

```java
package com.fu.tt;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.os.Handler;
import android.os.Looper;
import android.os.Message;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    private static final int MESSAGE_TYPE_1 = 1;
    private static final int MESSAGE_TYPE_2 = 2;

    private Button buttonType1;
    private Button buttonType2;

    private Handler mainThreadHandler;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        buttonType1 = findViewById(R.id.buttonType1);
        buttonType2 = findViewById(R.id.buttonType2);

        mainThreadHandler = new Handler(Looper.getMainLooper(), msg -> {
            switch (msg.what) {
                case MESSAGE_TYPE_1:
                    Toast.makeText(MainActivity.this, "Message type 1 received", Toast.LENGTH_SHORT).show();
                    break;
                case MESSAGE_TYPE_2:
                    Toast.makeText(MainActivity.this, "Message type 2 received", Toast.LENGTH_SHORT).show();
                    break;
                default:
                    return false;
            }
            return true;
        });

        buttonType1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                mainThreadHandler.sendEmptyMessage(MESSAGE_TYPE_1);
            }
        });

        buttonType2.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                mainThreadHandler.sendEmptyMessage(MESSAGE_TYPE_2);
            }
        });
    }
}
```

​				

将lambda表达式展开			

```java
package com.fu.tt;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.os.Handler;
import android.os.Looper;
import android.os.Message;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    private static final int MESSAGE_TYPE_1 = 1;
    private static final int MESSAGE_TYPE_2 = 2;

    private Button buttonType1;
    private Button buttonType2;

    private Handler mainThreadHandler;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        buttonType1 = findViewById(R.id.buttonType1);
        buttonType2 = findViewById(R.id.buttonType2);


        mainThreadHandler = new Handler(Looper.getMainLooper(), new Handler.Callback() {
            @Override
            public boolean handleMessage(Message msg) {
                switch (msg.what) {
                    case MESSAGE_TYPE_1:
                        Toast.makeText(MainActivity.this, "Message type 1 received", Toast.LENGTH_SHORT).show();
                        break;
                    case MESSAGE_TYPE_2:
                        Toast.makeText(MainActivity.this, "Message type 2 received", Toast.LENGTH_SHORT).show();
                        break;
                    default:
                        return false;
                }
                return true;
            }
        });


        buttonType1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                mainThreadHandler.sendEmptyMessage(MESSAGE_TYPE_1);
            }
        });

        buttonType2.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                mainThreadHandler.sendEmptyMessage(MESSAGE_TYPE_2);
            }
        });
    }
}
```

​				

加了Handler.Callback

```java
package com.fu.tt;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.os.Handler;
import android.os.Looper;
import android.os.Message;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    private static final int MESSAGE_TYPE_1 = 1;
    private static final int MESSAGE_TYPE_2 = 2;

    private Button buttonType1;
    private Button buttonType2;

    private Handler mainThreadHandler;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        buttonType1 = findViewById(R.id.buttonType1);
        buttonType2 = findViewById(R.id.buttonType2);

        Handler.Callback callback = new Handler.Callback() {
            @Override
            public boolean handleMessage(Message msg) {
                switch (msg.what) {
                    case MESSAGE_TYPE_1:
                        Toast.makeText(MainActivity.this, "Message type 1 received", Toast.LENGTH_SHORT).show();
                        break;
                    case MESSAGE_TYPE_2:
                        Toast.makeText(MainActivity.this, "Message type 2 received", Toast.LENGTH_SHORT).show();
                        break;
                    default:
                        return false;
                }
                return true;
            }
        };

        mainThreadHandler = new Handler(Looper.getMainLooper(), callback);

        buttonType1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                mainThreadHandler.sendEmptyMessage(MESSAGE_TYPE_1);
            }
        });

        buttonType2.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                mainThreadHandler.sendEmptyMessage(MESSAGE_TYPE_2);
            }
        });
    }
}
```

​				

### Lambda表达式

ambda 表达式是 Java 8 中引入的一种新特性，它提供了一种简洁、函数式的方法来表示只有一个方法的接口（也称为**函数式接口**）的实例。Lambda 表达式可以使代码更简洁、易读。

```java
(parameters) -> { body }
```

1. 参数列表 (parameters)：它定义了 Lambda 表达式所需要的输入参数。参数列表可以为空，有一个参数或多个参数。如果参数列表为空，您需要使用一对空括号 `()`。如果只有一个参数，可以选择省略括号。如果有多个参数，需要用逗号分隔，用括号括起来。
2. 箭头符号 (->)：它用于分隔参数列表和 Lambda 表达式的主体部分。
3. 主体 (body)：它包含了 Lambda 表达式需要执行的代码。主体可以是一个表达式或一个代码块。如果主体是一个表达式，那么结果将被隐式返回。如果主体是一个代码块，您需要使用大括号 `{}` 将其括起来，并且可能需要显式使用 `return` 语句返回结果。      

如果一个接口里只有一个抽象方法（不包括默认方法和静态方法），那么这个接口就被称为函数式接口（Functional Interface）。只有函数式接口才能使用 Lambda 表达式。

​					

```java
package com.fu.tt;

interface MyFunctionalInterface {
    void doSomething(String input);
}
```



```java
package com.fu.tt;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.os.Handler;
import android.os.Looper;
import android.os.Message;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    private static final int MESSAGE_TYPE_1 = 1;
    private static final int MESSAGE_TYPE_2 = 2;

    private Button buttonType1;
    private Button buttonType2;

    private Handler mainThreadHandler;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        MyFunctionalInterface myInstance1 = input -> Log.i("tag","Hello, " + input);;


        MyFunctionalInterface myInstance2 = new MyFunctionalInterface() {
            @Override
            public void doSomething(String input) {
                Log.i("tag","Hello, " + input);
            }
        };

        myInstance1.doSomething("heisenberg");
        myInstance2.doSomething("heisenberg");
    }
}
```

​				

**一个案例**

Greeting.java		

```java
package com.fu.tt;

@FunctionalInterface
public interface Greeting {
    void sayHello(String name);
}
```

`@FunctionalInterface` 是一个注解，用于表示一个接口是一个函数式接口。函数式接口是一个具有单一抽象方法（SAM）的接口。由于它们只包含一个方法，它们可以用于 Lambda 表达式和方法引用。			

请注意，`@FunctionalInterface` 注解不是强制性的。如果一个接口只包含一个抽象方法，它在语义上仍然是一个函数式接口，即使没有使用 `@FunctionalInterface` 注解。然而，建议使用这个注解来明确表示接口的用途并提高代码的可读性。				

​					

LambdaDemo.java

```java
public class LambdaDemo {
    public static void main(String[] args) {
        // 使用带有大括号的 Lambda 表达式实现 Greeting 接口
        Greeting greeting = (name) -> {
            String greetingMessage = "Hello, " + name + "!";
            System.out.println(greetingMessage);
            return greetingMessage;
        };

        // 调用 sayHello 方法
        String result = greeting.sayHello("Alice");
        System.out.println("Greeting result: " + result);
    }
}
```

或者是，当只有一个的函数的时候，就可以不用 { }

```java
package com.fu.tt;

import android.util.Log;

public class LambdaDemo {
    public static void main(String[] args) {
        // 使用 Lambda 表达式实现 Greeting 接口
        Greeting greeting = (name) -> Log.i("tag","Hello " + name + "!");

        // 调用 sayHello 方法
        greeting.sayHello("Alice");
    }
}
```

​					

#### 接口当中的默认方法

接口可以包含默认方法（Default Method）。默认方法是一种特殊类型的方法，它在接口中提供了具体的实现，而不是一个抽象方法。默认方法允许接口的设计者在不破坏已有实现的情况下，向接口添加新的方法		

​			

默认方法使用 `default` 关键字修饰，并提供方法体。这样，实现接口的类可以选择覆盖默认方法，也可以直接使用默认实现。以下是一个带有默认方法的接口示例：			

```java
public interface MyInterface {
    void abstractMethod(String input);

    default void defaultMethod() {
        System.out.println("This is a default method in the interface.");
    }
}
```

​				

### View.post() 和 View.postDelayed()

`View.post()` 和 `View.postDelayed()` 是 Android View 类的方法，它们允许你将一个 Runnable 对象排队到 UI 线程的消息队列中。这对于更新 UI 或执行与 UI 相关的操作非常有用，因为这些操作必须在 UI 线程上执行。这两个方法都可以确保 Runnable 对象在 UI 线程上运行。

1. `View.post(Runnable action)`：这个方法将 Runnable 对象添加到 View 的消息队列中。当 View 的 UI 线程准备好执行 Runnable 时，它会执行。**这是在不使用 Handler 的情况下**，在 UI 线程上执行代码的简便方法

​					

**View.post()**	

```java
textView.post(new Runnable() {
    @Override
    public void run() {
        textView.setText("Text updated on the UI thread");
    }
});
```



**View.postDelayed()**				

```java
textView.postDelayed(new Runnable() {
    @Override
    public void run() {
        textView.setText("Text updated after 2 seconds");
    }
}, 2000); // 更新文本将在 2 秒后发生
```

​			

完整的demo

activity_main.xml

```xml
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">


    <Button
        android:id="@+id/updateButton"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Update Text"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Initial Text"
        app:layout_constraintBottom_toTopOf="@+id/updateButton"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />


</androidx.constraintlayout.widget.ConstraintLayout>
```

​				

MainActivity.java

```java
package com.fu.tt;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.os.Handler;
import android.os.Looper;
import android.os.Message;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    private Button updateButton;
    private TextView textView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        updateButton = findViewById(R.id.updateButton);
        textView = findViewById(R.id.textView);

        updateButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                textView.post(new Runnable() {
                    @Override
                    public void run() {
                        textView.setText("Updating...");
                    }
                });

                textView.postDelayed(new Runnable() {
                    @Override
                    public void run() {
                        textView.setText("Updated!");
                    }
                }, 2000);
            }
        });
    }
}
```

​			

### Timer 和 TimerTask

1. Timer 类

   `Timer` 类是 Java 提供的一个实用工具类，用于在将来的某个时间点调度任务。您可以使用 `schedule()` 方法指定要执行的任务（`TimerTask` 类型）以及任务的执行时间。这里有一个简单的示例：

```java
import java.util.Timer;

public class TimerExample {
    public static void main(String[] args) {
        Timer timer = new Timer();
        timer.schedule(new MyTimerTask(), 3000);
    }
}

```

​			

2. TimerTask 类

`TimerTask` 是一个实现了 `Runnable` 接口的抽象类，它定义了一个 `run()` 方法，该方法将在指定时间由 `Timer` 类执行。以下是一个简单的 `MyTimerTask` 示例：

MyTimerTask.java

```java
package com.fu.tt;

import android.util.Log;

import java.util.TimerTask;

public class MyTimerTask extends TimerTask {
    @Override
    public void run() {
        Log.i("MyTimerTask","Task executed!");
    }
}
```

​			

要让任务定期执行，可以使用 `Timer` 类的 `scheduleAtFixedRate()` 方法。以下是一个简单的示例

```java
import java.util.Timer;

public class TimerExample {
    public static void main(String[] args) {
        Timer timer = new Timer();
        timer.scheduleAtFixedRate(new MyTimerTask(), 0, 3000);
    }
}
```

在这个示例中，我们使用 `scheduleAtFixedRate()` 方法让 `MyTimerTask` 每隔 3 秒执行一次。首次执行任务将在 0 毫秒后开始，即立即开始。

将这两个类放在一个项目中，运行 `TimerExample` 类，您会看到控制台每隔 3 秒输出一次 "Task executed!"。

​			

一个案例				

如何在 `TimerTask` 中更新 UI 线程的 UI			

```java
package com.fu.tt;

import java.util.TimerTask;

public class MyTimerTask extends TimerTask {

    private MainActivity mainActivity;

    public MyTimerTask(MainActivity mainActivity) {
        this.mainActivity = mainActivity;
    }

    @Override
    public void run() {
        mainActivity.runOnUiThread(new Runnable() {
            @Override
            public void run() {
                mainActivity.updateTextView();
            }
        });
    }
}
```

​			

```java
package com.fu.tt;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.os.Handler;
import android.os.Looper;
import android.os.Message;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;
import java.util.Timer;

public class MainActivity extends AppCompatActivity {

    private Button updateButton;
    private TextView textView;
    private int counter = 0;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        updateButton = findViewById(R.id.updateButton);
        textView = findViewById(R.id.textView);

        Timer timer = new Timer();


        updateButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Timer timer = new Timer();
                timer.scheduleAtFixedRate(new MyTimerTask(MainActivity.this), 0, 1000);
            }
        });
    }

    public void updateTextView() {
        counter++;
        textView.setText("Counter: " + counter);
    }
}
```

​				

或者是写在一起

```java
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.os.Handler;
import android.widget.TextView;

import java.util.Timer;
import java.util.TimerTask;

public class MainActivity extends AppCompatActivity {

    private TextView textView;
    private int counter = 0;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        textView = findViewById(R.id.textView);

        Timer timer = new Timer();
        timer.scheduleAtFixedRate(new MyTimerTask(), 0, 1000);
    }

    class MyTimerTask extends TimerTask {
        @Override
        public void run() {
            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    counter++;
                    textView.setText("Counter: " + counter);
                }
            });
        }
    }
}
```

​					

### 线程池

`java.util.concurrent.ExecutorService` 是一个 Java 接口，它表示一个可以执行提交的 `Runnable` 和 `Callable` 任务的线程池。

它提供了一些方法，如 `execute(Runnable)`、`submit(Callable)`、`submit(Runnable)` 等，用于提交任务，并提供了如 `shutdown()` 和 `awaitTermination(long, TimeUnit)` 等方法来关闭线程池。这个接口是 Java 并发框架的核心组件之一，它的实现类为 `ThreadPoolExecutor`。			

​							

`java.util.concurrent.Executors` 是一个 Java 类，提供了一些静态工厂方法，用于创建不同类型的 `ExecutorService` 实例。这些方法包括：

- `newFixedThreadPool(int nThreads)`: 创建一个固定线程数量的线程池。
- `newCachedThreadPool()`: 创建一个缓存线程池，根据需要自动增加线程数量。
- `newSingleThreadExecutor()`: 创建一个单线程执行器。
- `newScheduledThreadPool(int corePoolSize)`: 创建一个调度线程池，用于在给定延迟后执行任务或定期执行任务。

通过使用 `Executors` 类提供的工厂方法，你可以轻松地创建各种类型的线程池，而不需要自己手动实例化 `ThreadPoolExecutor` 类并配置各种参数。这大大简化了线程池的创建过程。

总结一下，`ExecutorService` 是一个接口，表示一个线程池，而 `Executors` 是一个类，提供了创建 `ExecutorService` 实例的工厂方法。这两者结合起来，使得在 Java 中创建和使用线程池变得简单和方便。



在 Android 开发中，线程池是一种有效管理多个线程的方法，以便更高效地处理并发任务。线程池可以重用已经创建的线程，从而减少了创建和销毁线程的开销。在 Java 和 Android 中，`ExecutorService` 是管理线程池的主要类。

以下是关于线程池的一些关键知识点，以及与之相关的代码示例：

1. 创建线程池

   使用 `Executors` 类创建线程池。以下是创建不同类型线程池的方法：

   - 固定线程池（Fixed Thread Pool）：拥有固定数量的线程。

     ```java
     javaCopy code
     int numberOfThreads = 4;
     ExecutorService fixedThreadPool = Executors.newFixedThreadPool(numberOfThreads);
     ```

   - 单线程执行器（Single Thread Executor）：仅有一个线程的线程池。

     ```java
     javaCopy code
     ExecutorService singleThreadExecutor = Executors.newSingleThreadExecutor();
     ```

   - 缓存线程池（Cached Thread Pool）：根据需要创建新线程的线程池，但会在可能的情况下重用之前构造的线程。

     ```java
     javaCopy code
     ExecutorService cachedThreadPool = Executors.newCachedThreadPool();
     ```

   - 定时线程池（Scheduled Thread Pool）：用于执行定时任务的线程池。

     ```java
     javaCopy code
     int numberOfThreads = 4;
     ScheduledExecutorService scheduledThreadPool = Executors.newScheduledThreadPool(numberOfThreads);
     ```

2. 提交任务

   使用 `ExecutorService` 的 `submit()` 方法提交任务。任务通常是实现了 `Runnable` 接口的类。

   ```java
   javaCopy code
   class MyTask implements Runnable {
       @Override
       public void run() {
           // 任务逻辑
       }
   }
   
   MyTask task = new MyTask();
   fixedThreadPool.submit(task);
   ```

   也可以使用 Lambda 表达式创建任务：

   ```java
   javaCopy code
   fixedThreadPool.submit(() -> {
       // 任务逻辑
   });
   ```

3. 关闭线程池

   在不再需要线程池时，使用 `shutdown()` 方法关闭线程池。这将启动有序的关闭，在关闭之前允许提交的任务完成。可以使用 `awaitTermination()` 方法等待线程池关闭。

   ```java
   javaCopy code
   fixedThreadPool.shutdown();
   
   try {
       if (!fixedThreadPool.awaitTermination(60, TimeUnit.SECONDS)) {
           fixedThreadPool.shutdownNow();
       }
   } catch (InterruptedException e) {
       fixedThreadPool.shutdownNow();
   }
   ```

4. 定时任务

   对于定时任务，使用 `ScheduledExecutorService`。以下是如何使用 `schedule()`、`scheduleAtFixedRate()` 和 `scheduleWithFixedDelay()` 方法执行定时任务：

   - `schedule()`：在指定的延迟之后运行一次任务。

     ```
     javaCopy code
     Runnable task = () -> {
         // 任务逻辑
     };
     long delay = 5;
     TimeUnit timeUnit = TimeUnit.SECONDS;
     scheduledThreadPool.schedule(task, delay, timeUnit);
     ```

   - `scheduleAtFixedRate()`：在指定的初始延迟之后开始运行任务，并以固定的速率连续执行任务。如果任务的执行时间超过指定的周期，则下一个任务将在当前任务完成后立即开始。

     ```java
     javaCopy code
     Runnable task = () -> {
         // 任务逻辑
     };
     long initialDelay = 1;
     long period = 5;
     TimeUnit timeUnit = TimeUnit.SECONDS;
     scheduledThreadPool.scheduleAtFixedRate(task, initialDelay, period, timeUnit);
     ```

   - `scheduleWithFixedDelay()`：在指定的初始延迟之后开始运行任务，并在每次任务完成后以固定的延迟执行下一个任务。

     ```java
     javaCopy code
     Runnable task = () -> {
         // 任务逻辑
     };
     long initialDelay = 1;
     long delay = 5;
     TimeUnit timeUnit = TimeUnit.SECONDS;
     scheduledThreadPool.scheduleWithFixedDelay(task, initialDelay, delay, timeUnit);
     ```

5. 自定义线程池

在某些情况下，您可能需要自定义线程池，以便更好地控制线程的创建、管理和回收。可以使用 `ThreadPoolExecutor` 类创建自定义线程池。

```
javaCopy code
int corePoolSize = 2;
int maximumPoolSize = 4;
long keepAliveTime = 60;
TimeUnit timeUnit = TimeUnit.SECONDS;
BlockingQueue<Runnable> workQueue = new LinkedBlockingQueue<>();
ThreadFactory threadFactory = Executors.defaultThreadFactory();
RejectedExecutionHandler handler = new ThreadPoolExecutor.AbortPolicy();

ThreadPoolExecutor customThreadPool = new ThreadPoolExecutor(
    corePoolSize, maximumPoolSize, keepAliveTime, timeUnit, workQueue, threadFactory, handler
);
```

这些参数的含义如下：

- `corePoolSize`：线程池维护的核心线程数。
- `maximumPoolSize`：线程池允许的最大线程数。
- `keepAliveTime`：非核心线程空闲等待新任务的最长时间。超过这个时间，非核心线程将被终止。
- `timeUnit`：`keepAliveTime` 参数的时间单位。
- `workQueue`：用于存储等待执行的任务的阻塞队列。
- `threadFactory`：用于创建新线程的工厂。
- `handler`：当线程池已满且队列已满时，拒绝处理新任务的处理程序。

​				

#### 线程池_fixedThreadPool（固定线程池）

ExecutorService 是一个可管理线程池的接口，提供了线程管理和任务执行的方法。FixedThreadPool 是 ExecutorService 的一种实现，它创建了一个具有固定线程数的线程池。

​			

```java
package com.fu.tt;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.os.Handler;
import android.os.Looper;
import android.os.Message;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;
import java.util.Timer;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class MainActivity extends AppCompatActivity {
    private static final String TAG = "MainActivity";
    private ExecutorService fixedThreadPool;


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button button = findViewById(R.id.start_button);
        fixedThreadPool = Executors.newFixedThreadPool(3);

        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                for (int i = 0; i < 100; i++) {
                    final int taskNumber = i;
                    fixedThreadPool.execute(new Runnable() {
                        @Override
                        public void run() {
                            try {
                                Thread.sleep(2000);
                            } catch (InterruptedException e) {
                                e.printStackTrace();
                            }
                            Log.d(TAG, "Task " + taskNumber + " is executed by thread: " + Thread.currentThread().getName());
                        }
                    });
                }
            }
        });
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        if (fixedThreadPool != null) {
          // 关闭线程池
            fixedThreadPool.shutdown();
        }
    }
}
```

​				

1. 线程复用：线程池中的线程在完成任务后不会立即销毁，而是等待新的任务分配给它。这种复用机制避免了频繁创建和销毁线程带来的性能开销。
2. 任务调度：线程池负责管理任务队列，根据线程的可用性来调度任务。在这个例子中，FixedThreadPool 的线程数量为3，因此线程池会并发执行3个任务。当一个任务完成时，空闲的线程会开始执行下一个任务。任务将在队列中等待，直到有可用的线程来执行它们。（一次性打印三个日志）
3. 资源控制：线程池可以控制同时运行的线程数量，从而避免过多的线程消耗系统资源。在这个例子中，我们创建了一个具有3个线程的 FixedThreadPool，这意味着在任何时候，最多只会有3个线程同时执行任务。这有助于提高应用程序的性能，特别是在资源受限的设备上。

​			

#### 线程池_SingleThreadExecutor（单线程执行器）

单线程执行器（Single Thread Executor）是一种特殊类型的线程池，它只有一个工作线程。这意味着它同时只能执行一个任务，而其他任务将排队等待。单线程执行器的一个主要优点是它可以保证任务按照提交的顺序依次执行。这在某些场景下非常有用，比如你需要按顺序执行一系列任务，而不希望它们在多个线程中并发执行

```java
package com.fu.tt;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.os.Handler;
import android.os.Looper;
import android.os.Message;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;
import java.util.Timer;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class MainActivity extends AppCompatActivity {
    private static final String TAG = "MainActivity";
    private ExecutorService executorService;


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button button = findViewById(R.id.start_button);

        // 创建一个单线程执行器
        executorService = Executors.newSingleThreadExecutor();

        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                for (int i = 0; i < 10; i++) {
                    final int taskNumber = i;
                    executorService.execute(new Runnable() {
                        @Override
                        public void run() {
                            try {
                                Thread.sleep(2000);
                            } catch (InterruptedException e) {
                                e.printStackTrace();
                            }
                            Log.d(TAG, "Task " + taskNumber + " is executed by thread: " + Thread.currentThread().getName());
                        }
                    });
                }
            }
        });
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        if (executorService != null) {
            executorService.shutdown();
        }
    }
}
```

​				

#### 线程池_cachedThreadPool（缓存线程池）

缓存线程池（Cached Thread Pool）是一种特殊类型的线程池，它的工作线程数量可以根据需要动态调整。当有新任务提交到缓存线程池时，如果有空闲的工作线程，那么这个任务将立即被这个工作线程执行；如果没有空闲的工作线程，线程池会创建一个新的工作线程来执行这个任务。此外，当工作线程空闲一段时间后（默认为60秒），它将被自动销毁以减少资源占用。

缓存线程池适用于执行大量短时任务的场景，因为它可以根据任务数量动态调整线程数量，从而提高系统资源的利用率。				

​				

```java
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.widget.TextView;

import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class MainActivity extends AppCompatActivity {

    private TextView textView;
    private ExecutorService cachedThreadPool;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        textView = findViewById(R.id.textView);

        // 创建一个缓存线程池
        cachedThreadPool = Executors.newCachedThreadPool();

        // 提交任务
        for (int i = 0; i < 10; i++) {
            int taskNumber = i + 1;
            cachedThreadPool.execute(() -> {
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }

                // 更新 UI
                runOnUiThread(() -> textView.append("Task " + taskNumber + " completed on thread: " + Thread.currentThread().getName() + "\n"));
            });
        }
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        // 关闭线程池
        if (cachedThreadPool != null) {
            cachedThreadPool.shutdown();
        }
    }
}
```

​				

#### 线程池_ScheduledThreadPool（定时任务）

定时线程池（Scheduled Thread Pool）允许您在指定延迟之后运行任务，或者定期执行任务。在 Android 开发中，您可以使用 `java.util.concurrent.ScheduledThreadPoolExecutor` 类来创建和管理定时线程池。

​					

**scheduleAtFixedRate（周期）**

```java
import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import java.util.concurrent.Executors;
import java.util.concurrent.ScheduledExecutorService;
import java.util.concurrent.TimeUnit;

public class MainActivity extends AppCompatActivity {

    private TextView textView;
    private Button startButton;
    private int counter = 0;
    private ScheduledExecutorService scheduledExecutorService;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        textView = findViewById(R.id.textView);
        startButton = findViewById(R.id.startButton);

        scheduledExecutorService = Executors.newScheduledThreadPool(1);

        startButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                scheduledExecutorService.scheduleAtFixedRate(new Runnable() {
                    @Override
                    public void run() {
                        runOnUiThread(new Runnable() {
                            @Override
                            public void run() {
                                counter++;
                                textView.setText("Counter: " + counter);
                            }
                        });
                    }
                }, 0, 1, TimeUnit.SECONDS);
            }
        });
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        scheduledExecutorService.shutdown();
    }
}
```

 `Executors.newScheduledThreadPool(1)` 创建一个包含一个线程的定时线程池，然后，当用户点击 `startButton` 时，我们使用 `scheduleAtFixedRate` 方法安排一个定期运行的任务，注意：**每次点击按钮时，你都会向线程池中提交一个新的定时任务。这些任务会在同一个线程中依次执行。因此，在你的示例中，你会有多个定时任务在同一个线程中同时运行，导致计数器加速。	并不是因为点击一次 START 就新增一个线程，多个线程同时运行，导致的计时速度加快**			

​							

```java
scheduleAtFixedRate(new Runnable,0,1,TimeUnit.SECONDS)
```

1. `Runnable command`: 要执行的任务。这是一个实现了 `Runnable` 接口的对象，表示要执行的代码。
2. `long initialDelay`: 初始延迟。这是任务首次执行前的等待时间。这个值的单位是由第 4 个参数指定的。
3. `long period`: 任务执行的间隔。这是连续任务执行之间的时间间隔。这个值的单位是由第 4 个参数指定的。
4. `TimeUnit unit`: 时间单位。这是一个枚举类型，用于指定初始延迟和执行间隔的时间单位。可用的单位包括 `NANOSECONDS`（纳秒）、`MICROSECONDS`（微秒）、`MILLISECONDS`（毫秒）、`SECONDS`（秒）、`MINUTES`（分钟）、`HOURS`（小时）和 `DAYS`（天）。

​			

```java
scheduledExecutorService.scheduleAtFixedRate(new Runnable() {
    @Override
    public void run() {
        // ... 更新 UI ...
    }
}, 0, 1, TimeUnit.SECONDS);
```

这意味着：

1. 我们创建了一个新的 `Runnable` 对象，该对象包含要执行的任务（在本例中为更新 UI）。
2. 初始延迟为 0，任务将立即开始执行。
3. 任务执行间隔为 1 秒，即每隔 1 秒执行一次任务。
4. 时间单位为 `TimeUnit.SECONDS`，表示初始延迟和执行间隔都以秒为单位。

​					

如果你想将十个任务分配给十个线程，你只需要创建一个拥有十个线程的线程池，每一次 `scheduledExecutorService.scheduleAtFixedRate` 都会将新的任务分配空闲的线程，如果，你的没有空闲的，就会加在一个线程上面添加多个任务				
通过点按按钮的方式，给十个线程分配任务

```java
package com.fu.tt;

import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import java.util.concurrent.Executors;
import java.util.concurrent.ScheduledExecutorService;
import java.util.concurrent.TimeUnit;

public class MainActivity extends AppCompatActivity {

    private TextView textView;
    private Button startButton;
    private int counter = 0;
    private ScheduledExecutorService scheduledExecutorService;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        textView = findViewById(R.id.textView);
        startButton = findViewById(R.id.startButton);

        scheduledExecutorService = Executors.newScheduledThreadPool(100);

        startButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                scheduledExecutorService.scheduleAtFixedRate(new Runnable() {
                    @Override
                    public void run() {
                        runOnUiThread(new Runnable() {
                            @Override
                            public void run() {
                                counter++;
                                textView.setText("Counter: " + counter);
                            }
                        });
                    }
                }, 0, 1, TimeUnit.SECONDS);
            }
        });
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        scheduledExecutorService.shutdown();
    }
}
```

​					

一次性就执行十次，让我们的线程池满负荷运行

```java
package com.fu.tt;

import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import java.util.concurrent.Executors;
import java.util.concurrent.ScheduledExecutorService;
import java.util.concurrent.TimeUnit;

public class MainActivity extends AppCompatActivity {

    private TextView textView;
    private Button startButton;
    private int counter = 0;
    private ScheduledExecutorService scheduledExecutorService;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        textView = findViewById(R.id.textView);
        startButton = findViewById(R.id.startButton);

        scheduledExecutorService = Executors.newScheduledThreadPool(10);

        startButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                for (int i = 0; i < 10; i++) {
                    scheduledExecutorService.scheduleAtFixedRate(new Runnable() {
                        @Override
                        public void run() {
                            runOnUiThread(new Runnable() {
                                @Override
                                public void run() {
                                    counter++;
                                    textView.setText("Counter: " + counter);
                                }
                            });
                        }
                    }, 0, 1, TimeUnit.SECONDS);
                }
            }
        });
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        scheduledExecutorService.shutdown();
    }
}
```

​					

​				

**schedule（延迟）**	

`ScheduledExecutorService` 的 `schedule` 方法允许你在指定的延迟后执行一个一次性任务。

```java
package com.fu.tt;

import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

import java.util.concurrent.Executors;
import java.util.concurrent.ScheduledExecutorService;
import java.util.concurrent.TimeUnit;

public class MainActivity extends AppCompatActivity {

    private TextView textView;
    private Button startButton;
    private ScheduledExecutorService scheduledExecutorService;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        textView = findViewById(R.id.textView);
        startButton = findViewById(R.id.startButton);

        scheduledExecutorService = Executors.newScheduledThreadPool(1);

        startButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                scheduledExecutorService.schedule(new Runnable() {
                    @Override
                    public void run() {
                        runOnUiThread(new Runnable() {
                            @Override
                            public void run() {
                                textView.setText("Task executed after 3 seconds");
                            }
                        });
                    }
                }, 3, TimeUnit.SECONDS);
            }
        });
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        scheduledExecutorService.shutdown();
    }
}
```

​				

在这个例子中，我们有一个 `TextView` 和一个 `Button`。当用户点击按钮时，将在延迟 3 秒后执行一个任务，该任务将更新 `TextView` 的文本。请注意，这个任务只会执行一次，不会周期性地重复。

`scheduledExecutorService.schedule()` 方法有三个参数：

1. `Runnable`：要执行的任务。
2. `long delay`：任务开始执行前的延迟时间。
3. `TimeUnit unit`：延迟时间的单位（如 `TimeUnit.SECONDS`、`TimeUnit.MILLISECONDS` 等）。

​				

### 自创建线程池

`ThreadPoolExecutor` 是 `java.util.concurrent` 包中的一个类，它允许你创建自定义的线程池。与 `Executors` 类提供的预定义线程池不同，使用 `ThreadPoolExecutor`，你可以更好地控制线程池的行为，例如核心线程数、最大线程数、线程空闲时间等。				



```java
package com.fu.tt;


import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

import java.util.concurrent.LinkedBlockingQueue;
import java.util.concurrent.ThreadPoolExecutor;
import java.util.concurrent.TimeUnit;

public class MainActivity extends AppCompatActivity {

    private TextView textView;
    private Button startButton;
    private ThreadPoolExecutor threadPoolExecutor;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        textView = findViewById(R.id.textView);
        startButton = findViewById(R.id.startButton);

        int corePoolSize = 2;
        int maximumPoolSize = 4;
        long keepAliveTime = 10;
        TimeUnit unit = TimeUnit.SECONDS;
        LinkedBlockingQueue<Runnable> workQueue = new LinkedBlockingQueue<>();

        threadPoolExecutor = new ThreadPoolExecutor(corePoolSize, maximumPoolSize, keepAliveTime, unit, workQueue);

        startButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                threadPoolExecutor.execute(new Runnable() {
                    @Override
                    public void run() {
                        try {
                            Thread.sleep(3000);
                        } catch (InterruptedException e) {
                            e.printStackTrace();
                        }
                        runOnUiThread(new Runnable() {
                            @Override
                            public void run() {
                                textView.setText("Task executed by custom ThreadPoolExecutor");
                            }
                        });
                    }
                });
            }
        });
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        threadPoolExecutor.shutdown();
    }
}
```

1. `corePoolSize`：线程池中的核心线程数。即使线程空闲，线程池也会保持这些核心线程。
2. `maximumPoolSize`：线程池中允许的最大线程数。当工作队列已满时，线程池会创建新线程，直到达到最大线程数。
3. `keepAliveTime`：非核心线程空闲时的最长保持时间。超过这个时间，非核心线程将被终止。
4. `unit`：`keepAliveTime` 的时间单位。
5. `workQueue`：用于存储等待执行的任务的阻塞队列。

当用户点击按钮时，我们将一个任务提交给线程池。这个任务会模拟耗时操作（通过 `Thread.sleep(3000)`），然后在主线程上更新 `TextView` 的文本。				

​					

```java
LinkedBlockingQueue<Runnable> workQueue = new LinkedBlockingQueue<>();
```

`LinkedBlockingQueue` 是 `java.util.concurrent` 包中的一个类，它实现了一个**线程安全的阻塞队列**。这个队列用于存储等待执行的任务。它是 `ThreadPoolExecutor` 构造函数的一个参数。

​				

阻塞队列（BlockingQueue）是一种特殊的队列，它支持在多线程环境下的插入和提取操作。其中，"阻塞" 的含义是指，当队列为空时，从队列中获取元素的操作会被阻塞，直到队列中有元素为止。同样，当队列已满时，向队列中添加元素的操作也会被阻塞，直到队列中有空位置为止。

`LinkedBlockingQueue` 是一种实现了阻塞队列接口的类，它使用链表作为底层数据结构。它是线程安全的，意味着在多线程环境下，你不需要担心多个线程同时访问队列时的同步问题。

在线程池中，`LinkedBlockingQueue` 用于存储等待执行的任务。当你向线程池提交任务时，任务会被添加到 `LinkedBlockingQueue` 中。线程池中的线程会从队列中获取任务并执行它们。如果队列为空，线程会等待，直到有新任务提交到队列为止。

举个例子，假设你有一个线程池，它有3个线程。同时，你向线程池提交了5个任务。线程池中的3个线程将立即开始执行前3个任务。而剩下的2个任务会被添加到 `LinkedBlockingQueue` 中等待执行。当线程池中的一个线程完成了它的任务，它将从队列中获取下一个任务并执行。这样，队列中的任务会按照先进先出（FIFO）的顺序被处理。

总之，`LinkedBlockingQueue` 是一种线程安全的、基于链表的阻塞队列。在线程池中，它用于存储等待执行的任务，并且支持多线程环境下的安全操作。

​				

### 泛型（Generics）

泛型（Generics）是 Java 编程语言中的一个重要特性，它允许在类、接口和方法中使用类型参数。泛型的主要目的是提高代码的可重用性，减少代码重复，并增加类型安全性。			

**就是不在意数据的类型	**				

​				

#### 泛型类和泛型接口

泛型类和泛型接口是带有一个或多个类型参数的类和接口。例如，Java 集合框架中的 `List<E>` 和 `Map<K, V>` 都是泛型接口。在这些接口中，`E`、`K` 和 `V` 分别表示元素类型、键类型和值类型。

一个例子			

1. 首先，创建一个名为 `Storage` 的泛型接口，包含 `add`、`get` 和 `size` 方法。

```java
public interface Storage<T> {
    void add(T item);
    T get(int index);
    int size();
}
```

在这个泛型接口中，我们使用了泛型参数 `T`，表示要存储的元素类型				

​				

创建一个实现了 `Storage` 接口的泛型类 `ArrayStorage`，用于将元素存储在一个数组中。

```java
import java.util.Arrays;

public class ArrayStorage<T> implements Storage<T> {
    private Object[] items;
    private int size;

    public ArrayStorage() {
        items = new Object[10];
        size = 0;
    }

    @Override
    public void add(T item) {
        if (size == items.length) {
            items = Arrays.copyOf(items, size * 2);
        }
        items[size++] = item;
    }

    @SuppressWarnings("unchecked")
    @Override
    public T get(int index) {
        if (index < 0 || index >= size) {
            throw new IndexOutOfBoundsException("Index: " + index + ", Size: " + size);
        }
        return (T) items[index];
    }

    @Override
    public int size() {
        return size;
    }
}
```

在这个泛型类中，我们使用了与 `Storage` 接口相同的泛型参数 `T`。注意，我们在 `ArrayStorage` 类中使用了一个 `Object[]` 数组来存储元素，并在获取元素时进行了类型转换。					

​										

在你的 `MainActivity` 类中，测试 `ArrayStorage` 类的使用

```java
import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {

    private TextView textView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        textView = findViewById(R.id.textView);

        // 使用泛型类 ArrayStorage 存储 String 类型的元素
        Storage<String> stringStorage = new ArrayStorage<>();
        stringStorage.add("Hello");
        stringStorage.add("World");

        // 使用泛型类 ArrayStorage 存储 Integer 类型的元素
        Storage<Integer> integerStorage = new ArrayStorage<>();
        integerStorage.add(1);
        integerStorage.add(2);
        integerStorage.add(3);

        StringBuilder sb = new StringBuilder();
        sb.append("String Storage: ").append(stringStorage.get(0)).append(", ").append(stringStorage.get(1)).append("\n");
        sb.append("Integer Storage: ").append(integerStorage.get(0)).append(", ").append(integerStorage.get(1)).append(", ").append(integerStorage.get(2));

        textView.setText(sb.toString());
    }
}
```

