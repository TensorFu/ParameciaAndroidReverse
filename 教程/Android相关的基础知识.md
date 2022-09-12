# Android相关的基础知识

- [Android相关的基础知识](#android相关的基础知识)
  - [系统框架](#系统框架)
    - [Linux内核层](#linux内核层)
    - [Android四大组件](#android四大组件)

## 系统框架

### Linux内核层

![img](C:\Users\86480\Desktop\ParameciaAndroidReverse\教程\assets\1620.jpeg)

根据这一张图的描述，一共分为下面的五个部分 

Linux内核、HAL硬件抽象层（是我们最不关心的一个层）、系统Native库和Android运行时环境（这两个也被称之为系统运行库层）、Java框架层（应用框架层）以及应用层这5层架构

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