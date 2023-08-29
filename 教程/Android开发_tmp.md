## setClassName

`setClassName` 是 `Intent` 类中的一个方法，用于显式地设置 `Intent` 的组件名称。组件是一个应用内部的功能模块，例如一个 `Activity`、`Service`、`BroadcastReceiver` 或 `ContentProvider`。组件名称由应用的包名和组件的类名组成。

在 Android 开发中，`Intent` 是用于在不同组件之间传递消息的一种机制。当你想启动一个 `Activity`、`Service` 或发送一个广播时，通常都会创建一个 `Intent` 对象来指定你想要做什么。`Intent` 可以包含各种额外的数据，以键值对的形式保存。

`setClassName` 方法有两个参数：

1. 第一个参数是一个字符串，表示应用的包名。
2. 第二个参数也是一个字符串，表示组件的完全限定名（即包名 + 类名）。

## 示例 1：启动一个 Activity

假设我们有一个名为 `com.example.myapp` 的应用，其中有一个名为 `com.example.myapp.MainActivity` 的 `Activity` 类。以下是如何使用 `setClassName` 方法来创建一个 `Intent`，以启动这个 `Activity`：

```java
Intent intent = new Intent();
intent.setClassName("com.example.myapp", "com.example.myapp.MainActivity");
startActivity(intent);
```



## 示例 2：启动一个 Service

同样，假设我们有一个名为 `com.example.myapp.MyService` 的 `Service` 类。以下是如何使用 `setClassName` 方法来创建一个 `Intent`，以启动这个 `Service`：

```java
Intent intent = new Intent();
intent.setClassName("com.example.myapp", "com.example.myapp.MyService");
startService(intent);
```



## setClass

`setClass` 是 `Intent` 类中的一个方法。在 Android 中

`setClass` 方法有两个参数：

1. `Context`：当前上下文（通常是 `Activity` 或 `Application` 的实例）。
2. `Class<?>`：目标组件的 Class 对象。

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    public void goToSettings(View view) {
        Intent intent = new Intent();
        intent.setClass(MainActivity.this, SettingsActivity.class);
        startActivity(intent);
    }
}
```

---

## 直接使用 Intent 的构造函数

```java
Intent intent = new Intent(this, MathService.class);
bindService(intent, connection, Context.BIND_AUTO_CREATE);
```



## context.getCacheDir()

它返回一个表示应用的内部缓存目录的 `File` 对象

也就是  **/data/data/com.example.myapp/cache/**



## context.bindservice

## 1. **基本解释：**

- `context.bindService()` 是 Android 中用于绑定一个应用组件（通常是一个 Activity）到一个服务 (`Service`) 的方法。
- 它允许组件与 `Service` 建立一个持续的连接，并通过这个连接与 `Service` 进行交互。
- 与通过 `startService()` 启动的服务不同，绑定的服务与特定的组件关联，并且当所有客户端都与它解除绑定时，系统就会销毁它。



## 2. **比喻：**

想象 `Service` 是一个后台的员工（例如，一个专职的计算员工）。`Activity`（或其他组件）像是这个员工的经理。通过 `bindService()`，经理（`Activity`）可以直接与这个员工（`Service`）建立一个持续的联系，可以随时给他分派任务或获取工作的结果。

## 3. **参数解释：**

`context.bindService()` 通常接受三个参数：

1. **Intent**：这个 `Intent` 对象明确地指定了要绑定的 `Service`。
2. **ServiceConnection**：这是一个接口，组件（如 `Activity`）通过这个接口与 `Service` 互动。
3. **flags**：这是一个整型值，用于控制绑定选项。



## 4. **使用场景举例：**

- 假设我们正在开发一个音乐播放应用。我们可能有一个后台 `Service` 来控制音乐的播放，而界面上的 `Activity` 需要与这个 `Service` 交互，以更新播放状态、获取当前播放的歌曲等。



# **Instrumentation**

## 1. **什么是 Instrumentation？**

- **简单解释：** `Instrumentation` 是Android提供的一个用于监控应用和系统交互的工具。可以把它想象成一个手术室的监控仪器，它能够详细记录一个应用的行为和状态。

## 2. **Instrumentation 的主要用途：**

- **监控应用的交互和生命周期**：例如，它可以跟踪Activity的启动、服务的连接等。
- **执行和监控应用的测试**：例如，它可以模拟用户的点击事件，观察和验证应用的行为。

## 3. **如何使用 Instrumentation？**

- **基本使用**：要使用 `Instrumentation`，首先需要创建一个 `Instrumentation` 类的子类，并重写它的方法以插入你自己的逻辑。



```java
public class MyInstrumentation extends Instrumentation {

    @Override
    public void callActivityOnCreate(Activity activity, Bundle icicle) {
        super.callActivityOnCreate(activity, icicle);
        // 我们可以在这里插入自己的代码，比如记录日志
        Log.d("MyInstrumentation", "Activity " + activity.getLocalClassName() + " is created");
    }

}
```

这个 `MyInstrumentation` 类的主要功能是监控应用程序中 `Activity` 的创建过程。每当应用程序中的一个 `Activity` 被创建时，`MyInstrumentation` 的 `callActivityOnCreate` 方法都会被调用，然后它记录一条日志信息，告诉我们哪个 `Activity` 被创建了。



**如何启动 Instrumentation？**

通常，我们会通过一个独立的测试应用来启动 `Instrumentation`。我们需要在测试应用的 `AndroidManifest.xml` 文件中声明我们的 `Instrumentation` 类：

```java
<manifest ...>
    <instrumentation
        android:name=".MyInstrumentation"
        android:targetPackage="com.example.myapp" />
    ...
</manifest>
```

- `android:targetPackage` 指定了我们想要监控的目标应用。

- **如何运行 Instrumentation？**

  一般情况下，我们通过 `adb` 命令行工具来启动 `Instrumentation`：

```java
adb shell am instrument -w com.example.mytest/androidx.test.runner.AndroidJUnitRunner
```



## 5. **深入理解和高级用法**

- **模拟用户交互**：`Instrumentation` 可以模拟用户的交互事件，如点击、长按等。这对于自动化测试非常有用。
- **访问和修改内部状态**：通过 `Instrumentation`，我们可以访问应用的内部状态，甚至可以修改这些状态。这使得我们可以在不改变应用代码的情况下，测试应用在各种不同状态下的行为。

```java
public class MyInstrumentation extends Instrumentation {

    @Override
    public void onStart() {
        super.onStart();

        // 模拟一个点击事件
        sendPointerSync(MotionEvent.obtain(SystemClock.uptimeMillis(),SystemClock.uptimeMillis(),
                MotionEvent.ACTION_DOWN, 100, 100, 0));
    }
}
```



# getTargetContext 

```java
startService_AsukaProcess1Service(getTargetContext());
```

`getTargetContext()` 是 `Instrumentation` 类中的一个方法。这个方法用于获取被当前 `Instrumentation` 对象监控的应用程序的上下文（`Context`）。这个返回的上下文允许你访问和操作被测应用的资源、启动它的组件（如 `Activity`、`Service` 等）以及做其他与应用程序上下文相关的操作



# Context.BIND_AUTO_CREATE

在绑定到服务的时候，如果服务还没有运行，系统应该自动创建服务。换句话说，如果服务尚未运行，系统会调用服务的 `onCreate()` 方法，然后再调用 `onBind()` 方法。



# intentFilter.setPriority(1000)

设置广播的优先级

```java
IntentFilter intentFilter = new IntentFilter("com.android.jikealiveintent.action.MAIN_PROCESS_START");
intentFilter.setPriority(1000); // 设置优先级
context.registerReceiver(AsukaMainProcessStartReceiver_object, intentFilter);
```



假设有两个广播接收器`ReceiverA`和`ReceiverB`，我们为它们设置了不同的优先级：

```java
IntentFilter filterA = new IntentFilter("com.example.MY_ACTION");
filterA.setPriority(100);
registerReceiver(receiverA, filterA);

IntentFilter filterB = new IntentFilter("com.example.MY_ACTION");
filterB.setPriority(10);
registerReceiver(receiverB, filterB);
```

当一个匹配`"com.example.MY_ACTION"`动作的广播消息被发送时：

- 由于`ReceiverA`的优先级设置为100，它的优先级比`ReceiverB`（优先级为10）高，所以`ReceiverA`会首先接收到这个广播消息。
- 如果`ReceiverA`决定不终止这个广播，那么`ReceiverB`随后也会接收到这个广播消息。
- 如果`ReceiverA`决定终止这个广播（通过调用`abortBroadcast()`方法），那么`ReceiverB`将不会接收到这个广播消息。



## this.context.getPackageName()

它返回一个 `String`，这个 `String` 是当前应用程序的包名



## this.context.getDir("DaemonLog", 0)

**/data/data/com.example.myapp/app_DaemonLog**

创建或者访问这个目录



第二个参数是，表示私有的，也就是说，只能够被本项目访问



## this.context.getDir("DaemonLog", 0).getAbsolutePath();

获取绝对路径



## this.context.getPackageManager().getPackageInfo(this.context.getPackageName(), 0);

取应用的详细信息（如版本号、权限、签名等），查询可以处理特定类型的 Intent 的应用

你可以在这里设置

- `PackageManager.GET_ACTIVITIES`
- `PackageManager.GET_GIDS`
- `PackageManager.GET_CONFIGURATIONS`
- `PackageManager.GET_INSTRUMENTATION`
- `PackageManager.GET_PERMISSIONS`
- `PackageManager.GET_PROVIDERS`
- `PackageManager.GET_RECEIVERS`
- `PackageManager.GET_SERVICES`
- `PackageManager.GET_SIGNATURES`
- `PackageManager.GET_UNINSTALLED_PACKAGES`

分别是获取，对应的包的信息，并且这里可以，获取多个

like this

```java
PackageInfo packageInfo = context.getPackageManager().getPackageInfo(
    context.getPackageName(), 
    PackageManager.GET_ACTIVITIES | PackageManager.GET_SERVICES
);
```



0

表示的是基本的信息

- 应用的版本信息（如 `versionCode` 和 `versionName`）。
- 应用的包名（`packageName`）。



## packageInfo.applicationInfo.nativeLibraryDir

 native 库目录路径的字符串

## packageInfo.applicationInfo.publicSourceDir

它表示应用程序的 APK 文件的绝对路径



----

### equalsIgnoreCase

忽略大小写的比较



---

### ArrayList<String> arrayList = new ArrayList<>();和 数组 String[]



ArrayList<String> arrayList

列表是，灵活的 数组

列表能够改变数据的长度，能够查找，能够删除，

能够存储任意的数据类型，但是除了基本类型，也就是 int和char

但是可以，存储他们的包装类型，如 `Integer`, `Character`



String[]

- **数组**: 仅提供基本的读取和写入功能。没有上述方法。



他们能够互相的转化

```java
ArrayList<String> list = new ArrayList<>();
list.add("A");
list.add("B");
list.add("C");

String[] array = list.toArray(new String[0]);
```

其中这个部分 new String[0] ，只是为了告诉程序，数据类型

---

