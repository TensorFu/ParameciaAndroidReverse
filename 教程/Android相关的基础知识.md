# Android相关的基础知识

- [Android相关的基础知识](#android相关的基础知识)
  - [系统框架](#系统框架)
    - [Linux内核层](#linux内核层)
    - [Android四大组件](#android四大组件)

## 系统框架

### Linux内核层

![img](assets/1620.jpg)

根据这一张图的描述，一共分为下面的五个部分 

Linux内核、HAL硬件抽象层（是我们最不关心的一个层）、系统Native库和Android运行时环 境（这两个也被称之为系统运行库层）、Java框架层（应用框架层）以及应用层这5层架构

1. Linux内核层，Android在某种程度上就是一个Linux，那么Linux存在的内核漏洞，在Android上面也是存在的，Linux上面的一些命令，理论上也是可以在Android上面执行的，但是，因为缺少硬件环境，所以没有办法实现。
2. 运行库层，一部分是Linux里面的原生库文件，比方说多媒体支持的库文件，libopengl.so 和数据库存储功能的 libsqlite.so 文件，林一部分是 Android 特有的一些库文件，他其实就是一个虚拟机，（Dalvik/Art）
3. 应用框架层，就是给Android开发提供一些API支持
4. 应用层，就是我们的进行Android开发的部分，也是我们最关心的一层，这里面包含了自带应用和下载的应用



## Android四大组件

四大组件就是

1. 活动（Activity）
2. 服务（Service）
3. 广播接收器（Broadcast Receiver）
4. 内容提供者（Content Provider）

activity 就是一个界面，一个界面就可以理解成是一个Activity

Service 就是一个后台

Broadcast Receiver 就是相应其他应用程序（包括系统） 的广播消息

Content Provider 用于进程之间的交互，通常就是从一个应用程序像其他的应用程序提供数据

---

### 广播

想想三体当中叶文杰，罗辑通过太阳向宇宙当中发送的一个安全声明，公布了地球的位置，Android当中的广播与之类似，就是发送一个消息让整个手机都接到消息，比方说，你的屏幕点亮了，比方说你的电量很低了，比方说你的某一个软件卸载了，或者是安装了，这个时候都会有一些软件会突然跳起来（特别是清理类的软件）他是怎么知道的呢，就是通过系统广播知道的，当然，还有一些广播是通过软件自己发送出去的，比方说，你的微信想要拉起某一个浏览器，也是通过广播这样的方式进行的。

广播分为静态注册和动态注册两种

​				

* 动态注册

编写一个继承BroadcastReceiver的广播接收器的类

```java
   class DynamicReceiver extends BroadcastReceiver {

        @Override
        public void onReceive(Context context, Intent intent) {
            Toast.makeText(context,intent.getStringExtra("dynamicInfo"), Toast.LENGTH_SHORT).show();
        }
    }
```

  			

设置广播接收器参数并注册

```java
	@Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
//        实例化动态广播所需IntertFilter
        IntentFilter intentFilter = new IntentFilter();
        intentFilter.addAction("dynamic");
        dynamicReceiver = new DynamicReceiver();
//        动态注册广播
        registerReceiver(dynamicReceiver, intentFilter);
    }

```

​			

发送广播

```java
    Intent intent = new Intent();
    intent.setAction("dynamic");
    intent.putExtra("dynamicInfo", "动态广播");
    sendBroadcast(intent);
```

​					

* 静态注册

通过这样的方式生成一个 MyStaticReceiver.java 

![image-20221010135606819](./assets/image-20221010135606819.png)

​			

编写接收到广播之后操作

```java
public class MyStaticReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        Toast.makeText(context,intent.getStringExtra("staticInfo"), Toast.LENGTH_SHORT).show();
    }
}
```

​			

发送广播

```java
	Intent intent = new Intent(this, MyStaticReceiver.class);
//        Android 8.0及以上静态注册广播需要使用显示Intent
//        Intent intent = new Intent();
//        intent.setAction("static");
    intent.putExtra("staticInfo", "静态广播");
    sendBroadcast(intent);
```



**动态注册广播不是常驻型广播**，也就是说广播跟随Activity的生命周期。注意在Activity结束前，移除广播接收器。**静态注册是常驻型**，也就是说当应用程序关闭后，如果有信息广播来，程序也会被系统调用自动运行

​				

* 有序广播和无序广播

1.Normalbroadcasts：默认广播

默认广播即普通广播，发送一个普通广播使用Context.sendBroadcast方法，普通广播对于多个接收者来说是完全异步的，通常每个接收者都无需等待即可以接收到广播，接收者相互之间不会有影响。对于这种广播，接收者无法终止广播，即无法阻止其他接收者的接收动作。

2.orderedbroadcasts：有序广播

发送一个有序广播使用Context.sendorderedBroadcast方法，有序广播比较特殊，它每次只发送到优先级较高的接收者那里，然后由优先级高的接受者再传播到优先级低的接收者那里，优先级高的接收者有能力终止这个广播。
			

1. 当广播为默认广播时：无视优先级，优先接收动态广播。
2. 当广播为有序广播时：优先级高的先接收（不分静态和动态）。同优先级的广播接收器，优先接收动态广播。