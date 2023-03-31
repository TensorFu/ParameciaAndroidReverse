- [Android 体系结构](#android-体系结构)
- [四大组件](#四大组件)
  - [活动](#活动)
  - [服务](#服务)
    - [服务的两种启动方式](#服务的两种启动方式)
  - [广播接受者](#广播接受者)
  - [内容提供者](#内容提供者)






## Android 体系结构
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



## 四大组件

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

### activity_main

路径 app/res/layout

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

`setOnClickListener()` 他的作用就是将我们的 监听器 附加到我们的按键

`onClick()` 这个就是点击了 button 之后的一些操作，比方说在里面打开打一个 activity 或者是显示一个提示等等 ... 

​			

这个代码，我们能够知道，先是从布局信息当中找到我们想要操作的控件（by id）这个按键就有一个对象

对象.setOnClickListener 就能够关联上OnClickListener

OnClickListener就能够执行 onClick 里面的代码

​			

















