# ParameciaAndroidReverse
草履虫的Android逆向教程 [欢迎大家在issue当中指出更正的地方，或者是通过下面的联系方式联系我]

联系方式：[telegram账号](https://t.me/GitFub)

在本教程当中所使用到的用例 APK 大部分来自网络下载，如若已经侵犯你的利益，请联系删除

在本教程当中所使用到的软件版本和设备信息列表

* 设备：小米10  || 虚拟机
* 手机系统：MIUI 13（基于Android 11-12）
* PC系统：Windows10专业版    ||  macOS12.3
* Java：1.8.0_202  || Java17
* IDA：IDA 7.5 pro 
* jadx-gui：jadx-gui-1.4.2-no-jre-win.exe
* JEB：JEB 3.19.1.202005071620
* 参考书籍《安卓Frida逆向与抓包实战》
* 参考书籍《安卓Frida逆向与协议分析》

---

[面试](面试/面试题.md)

> 在这里整理了Android 逆向面试当中常见的问题以及简述答案

---

[bug处理](bug处理/README.md)

> 在这里记录了一些笔者在实践当中出现的一些错误以及解决办法

---

- [ParameciaAndroidReverse](#parameciaandroidreverse)
  - [Android开发](#android开发)
    - [Android 体系结构](#android-体系结构)
    - [广播接受者](#广播接受者)
    - [intent以及PendingIntent](#intent以及pendingintent)
    - [UI](#ui)
      - [viewModel](#viewmodel)
    - [响应式编程](#响应式编程)
      - [LiveData](#livedata)
      - [MutableLiveData](#mutablelivedata)
      - [RxJava](#rxjava)
    - [通知](#通知)
    - [多线程](#多线程)
      - [Thread 类实现多线程开发](#thread-类实现多线程开发)
    - [网络编程](#网络编程)
      - [android的网络编程\_HttpURLConnection框架](#android的网络编程_httpurlconnection框架)
      - [Retrofit](#retrofit)
      - [OKHttp](#okhttp)
  - [NDK 开发](#ndk-开发)
  - [CPP 文件的编译以及 OLLVM 的混淆](#cpp-文件的编译以及-ollvm-的混淆)
  - [Android项目的文件结构](#android项目的文件结构)
  - [APK 文件结构](#apk-文件结构)
  - [APK 的打包流程](#apk-的打包流程)
  - [Android逆向当中的常用命令](#android逆向当中的常用命令)
  - [Charles抓包的配置](#charles抓包的配置)
  - [Android 相关的基础知识](#android-相关的基础知识)
  - [Android 开发教程](#android-开发教程)
  - [android的保活](#android的保活)
  - [java 代码基础](#java-代码基础)
  - [smali 语法](#smali-语法)
  - [smali 代码阅读](#smali-代码阅读)
  - [汇编](#汇编)
  - [汇编代码阅读](#汇编代码阅读)
  - [APKtool 工具反编译 apk](#apktool-工具反编译-apk)
  - [frida环境的安装](#frida环境的安装)
  - [frida](#frida)
  - [objection](#objection)
  - [apk 的保护策略](#apk-的保护策略)
  - [JEB 静态分析动态调试Java层破解登录过程实例](#jeb-静态分析动态调试java层破解登录过程实例)
  - [IDA 动态调试流程](#ida-动态调试流程)
  - [IDAso层动态调试破解登录过程实例](#idaso层动态调试破解登录过程实例)
  - [工具脱壳实操](#工具脱壳实操)
  - [apk文件加壳的常用so文件命名方式](#apk文件加壳的常用so文件命名方式)
  - [fart 脱壳机的理解](#fart-脱壳机的理解)
  - [unidbg 使用教程](#unidbg-使用教程)
  - [JNItrace](#jnitrace)
  - [奇怪的知识增加了](#奇怪的知识增加了)

---

## Android开发
### Android 体系结构

[Android_体系结构](教程/Android_体系结构.md)

> 在这里我们介绍，android 的系统分为哪些层级
>
> 以及，什么是：
>
> 【应用程序层】【应用程序框架层】【系统库与Android运行层】【Linux内核层】
>
> 以及他们之间的关系

​								

### 广播接受者

[广播接受者](教程/广播接受者.md)

> 全面的介绍和理解，广播接受者这个组件
>
> 什么是，静态注册和动态注册，以及不同版本的 android ，对于广播接受者的权限的变化

​				

### intent以及PendingIntent

[intent以及PendingIntent](教程/intent.md)

> 介绍什么是 intent，以及什么是PendingIntent

​				

### 数据持有类

> 所谓的数据持有类，本质上是一个管理数据的类，一个 activity 可能有很多的数据，一个 view 可能也有很多的数据，我们讲将这些信息豆放在一个类当中统一管理，这个类就叫做，数据持有类。跟我们的数据持有类高度相关的，就是，响应式编程，当这个数据持有类的一个数据发生改变了，那么就会如同广播一样，通知所有的关心这个数据的其他的组件

#### viewModel

[viewModel](教程/viewModel.md)

> 我们在，编写代码的时候，一个界面，会有很多的数据信息，或者是状态的信息，那么怎么管理这些数据信息，用到的就是我们的 viewModel 
>
> 1. **Model**：代表数据和业务逻辑。它直接处理数据、数据库或服务器交互等。
> 2. **View**：代表UI。视图通常是轻量级的，并且只是表示用户界面的元素。
> 3. **ViewModel**：是View和Model之间的桥梁。它保留视图的状态和数据，并响应视图的行为请求，处理数据（来自模型）以适应视图的需要。

​									

### 响应式编程

> 当我们的设备的某一些数据发生改变，我们需要快速的通知到其他的，组件，让其他的组件发生改变，比较常见的就是，时钟的显示，每一秒钟都会有数据发生改变，我需要设置一个观察者，一直盯着这个数据，当我们的这个秒数走动一次，我们就通知UI组件开始显示最新的时间。而这个观察者就是我们的响应式编程的核心概念

#### LiveData

[LiveData](教程/LiveData.md)

> 介绍了什么是 LiveData ，LiveData 设计为只读版本。它的设计目标是允许数据的读取，但不推荐外部直接更改它的值，什么意思呢？简单来说就是，他不希望这个被持有的数据是，用户能够点点戳戳就能够改变的值，要改变他的值，可以是通过系统自然的运行发送出来的数据，或者是服务器下发下来的数据，这就是为什么，当我们想要改变他的值，需要新建一个子类，然后在里面设置一个 postValue() 的方法，通过这复杂的方式。
>
> 一个可以直接运行的真实的案例

#### MutableLiveData

[MutableLiveData](教程/MutableLiveData.md)

> 介绍 MutableLiveData ，MutableLiveData设计为可读写版本的`LiveData`。当你需要从外部更改数据值时，你会使用`MutableLiveData` ，这个更加贴近于你的直觉理解到的，可观察的数据

#### RxJava

[RxJava](教程/RxJava.md)

> 介绍 RxJava 的基本的知识，RxJava 的 Observable 可以看作是一个更复杂、更灵活的 LiveData
>
> 分析一个实际的真实的案例

​						

### 通知

[通知](教程/通知.md)

> 介绍什么是通知
>
> 怎么搭建通知
>
> 什么是通知的渠道
>
> 以及怎么发送一个通知
> Build.builder 可以添加哪些属性



​				

### 多线程

#### Thread 类实现多线程开发

[Thread 类实现多线程开发](教程/Thread_类实现多线程开发.md)

> 介绍了传统的 Java 实现多线程的方法
>
> 介绍了 Runnable接口 
>
> 通过代码解释了 Runnable接口的优点

​					

### 网络编程

#### android的网络编程_HttpURLConnection框架

[android的网络编程_HttpURLConnection框架](教程/android的网络编程.md)

> 从最基本的什么是网络编程开始
>
> 介绍了什么是IP，以及私有IP和公有IP，端口，HTTP/HTTPS协议的区别和特点
>
> 介绍了URL，以及如何解析URL
>
> 介绍了请求和响应，以及如何发送请求，处理响应（基于  HttpURLConnection ）

#### Retrofit

[Retrofit](教程/Retrofit.md)

> 介绍了如果使用 Retrofit 进行发送请求

[Retrofit和RxJava的结合使用](教程/Retrofit和RxJava的结合使用.md)

> 在真实的开发当中，我们经常，用 Retrofit 和 RxJava 结合使用，一个负责请求网络数据，一个负责对响应的数据数据做出反应

#### OKHttp

[OKHttp](教程/OKHttp.md)

> 





目前我们所使用的语言是 Java 语言，在后续的完善当中我们会跟进kotlin语言的Android开发

---

## NDK 开发

[NDK开发_解读最简单的模板代码](教程/NDK开发_解读最简单的模板代码.md)

> 创建一个 NDK 的项目
>
> 逐行分析这个android studio 生成的 NDK 版本的 hello world 版的 demo 
>
> 了解最基本的，编译文件，加载 SO 文件，静态注册函数的命名规则，C++ 文件的几个字段



### virtualAPP

[virtualAPP](教程/virtualAPP.md)

> 



## CPP 文件的编译以及 OLLVM 的混淆

[CPP文件的编译以及OLLVM混淆](教程/CPP文件的编译以及OLLVM混淆.md)

> 所谓的 CPP 的文件的编译，就是将 C++ 的代码，生成 so 文件
>
> 在这个过程当中会使用到 OLLVM 的混淆

---

## Android项目的文件结构

[Android项目的文件结构](教程/Android项目的文件结构.md)



## APK 文件结构

[APK文件结构](教程/APK文件结构.md)

APK文件 就是 Android 的安装包，它本身也是一个压缩包，我们可以通过解压软件对 APK 文件直接进行解压

---

## APK 的打包流程

[APK打包的流程](教程/APK打包的流程.md)

简介程序从 Java 代码到安装包的过程

---

## Android逆向当中的常用命令

[Android逆向当中的常用命令](教程/Android逆向当中的常用命令.md)

---

## Charles抓包的配置

[Charles抓包的配置](教程/Charles抓包的配置.md)

> 介绍了 Charles 的安装
>
> Mac 端的抓包，iOS 端的抓包，android 端的抓包的证书的配置

----

## Android 相关的基础知识

[android相关的基础知识](教程/Android相关的基础知识.md)

简介 Android 系统的框架，和四大组件

---

## Android 开发教程

[android开发教程](教程/android开发.md)

---

## android的保活

[android的保活](教程/android的保活.md)



---

## java 代码基础

[Java代码基础](教程/java代码基础.md)

static关键字[static关键字的修饰方法，static关键字修饰变量，static静态代码块]，构造函数，方法重写与方法重载，接口

---

## smali 语法

[smali语法](教程/smali语法.md)

静态分析当中常见的 smali 代码

---

## smali 代码阅读

[smali代码阅读](教程/smali代码阅读.md)

## 汇编

[汇编](教程/arm汇编.md)

简单arm汇编语法

---

## 汇编代码阅读

[汇编代码阅读](教程/汇编代码阅读.md)

静态分析当中常见的比较，比较长的汇编指令

---

## APKtool 工具反编译 apk

[APKtool工具反编译apk](教程/Apktool工具反编译apk.md)

我们将 apk 解压之后会看到很多的 .dex 的文件，在反编译之后，就会生成一个一个 smali 的文件，通过这些文件，我们就能够了解应用的运行逻辑，以及动态调试，当然使用 Androidkiller 也能够直接进行反编译

---

## frida环境的安装



---

## frida

[Frida简介以及安装](教程/frida简介.md)

> 介绍 Frida 的这一款工具
>
> 介绍如何在你的设备上安装 Frida



[frida环境的安装](教程/frida环境的安装.md)

[Frida的两种启动方式](教程/Frida的两种启动方式.md)



[frida使用](教程/frida使用.md)

> Frida 的简介
>

---

## objection

[objection](教程/objection.md)



---

## apk 的保护策略

[apk常见的保护策略](教程/apk常见的保护策略.md)

> 在这里，我们介绍了什么是混淆
>
> 以及，关于 ProGuard混淆工具 怎么使用
>
> 推荐了一款笔者比较喜欢的混淆工具
>
> 介绍了如何编译 OLLVM的C++ 的混淆工具





---

## JEB 静态分析动态调试Java层破解登录过程实例

[JEB动态调试获取注册码_java层](/教程/JEB动态调试获取注册码_java层.md)

通过 JEB 静态分析和动态调试，获取一个软件的注册码。将 apk 放在 JEB 软件当中，分析反编译之后的代码，发现 Java 层的 checkSN() 函数的位置最有可能是在处理验证码的校验函数，通过分析，得到 chechSN() 是通过不断的获取MD5 值得到的，通过分析 smali 代码，获得的单个字符存储在 v8 寄存器当中，完整的验证码存储在 v5 寄存器当中

> 例子当中所涉及到的 APK 在 release 仓库当中

---

## IDA 动态调试流程





---

## IDAso层动态调试破解登录过程实例

[IDAso层动态调试破解登录过程实例](教程/IDAso层动态调试破解登录过程实例.md)

通过 JEB 分析出这个 APK 的登录校验在 so 层当中，通过 IDA 的 so层 静态分析，得到 APK 的登录校验的逻辑，通过修改动态调试的方式，修改寄存器的值，直接返回 True 或者是通过修改参数寄存器，使之匹配成功。达到无论输入什么账号和密码都能够登录的目的。

> 例子当中所涉及到的 APK 在 release 仓库当中

---

## 工具脱壳实操

[工具脱壳实操](/教程/工具脱壳实操.md)

这个实操是通过 frida_dexdump 工具进行脱壳的操作过程，脱壳的目标 apk 是迅雷app

> 例子当中所涉及到的工具在 release 仓库当中，原下载链接在文章当中

---

## apk文件加壳的常用so文件命名方式

[apk文件加壳的常用so文件命名方式](教程/apk文件加壳的常用so文件命名方式.md)

---

## fart 脱壳机的理解

[fart 脱壳机的理解](教程/fart 脱壳机的理解)

> 本文章是对 fart 脱壳机的学习，分析和理解

----

## unidbg 使用教程

[unidbg 使用教程之自带案例 kanxue.test2 分析](教程/unidbg使用教程1.md)

> 在这一篇文章当中，了解 kanxue.test2 的这一个 demo 所涉及到的一些代码
>
> 1. 什么是构造虚拟机，以及虚拟机的选择
>
> 2. 什么是后端工厂的引擎以及，怎么选择后端工厂的引擎
> 3. 如何设置模拟器的解析器
> 4. 如何初始化 android 库
> 5. 如何调用 SO 文件当中的函数



---

## JNItrace

[JNItrace使用教程](教程/JNItrace使用教程.md)

----

## 奇怪的知识增加了

[jadx-gui不能够解析dex的文件](教程/jadxgui不能够解析dex的文件.md)

[jadx-gui还原代码错误](教程/jadx-gui还原代码错误.md)

[Httpcanary证书的安装](教程/Httpcanary证书的安装.md)

[不用设置路由器翻墙的抓包外网APP的方法](教程/不用设置路由器翻墙的抓包外网APP的方法.md)

