# ParameciaAndroidReverse
草履虫的Android逆向教程 [欢迎大家在issue当中指出更正的地方，或者是通过下面的联系方式联系我]

联系方式：[telegram账号](https://t.me/GitFub)

在本教程当中所使用到的用例 APK 大部分来自网络下载，如若已经侵犯你的利益，请联系删除

在本教程当中所使用到的软件版本和设备信息列表

* 设备：小米10  虚拟机
* 手机系统：MIUI 13（基于Android 11-12）
* PC系统：Windows10专业版    macOS12.3
* Java：1.8.0_202  Java17
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
  - [APK 文件结构](#apk-文件结构)
  - [APK 的打包流程](#apk-的打包流程)
  - [Android逆向当中的常用命令](#android逆向当中的常用命令)
  - [Android 相关的基础知识](#android-相关的基础知识)
  - [Android开发流程简介](#android开发流程简介)
  - [android的保活](#android的保活)
  - [java 代码基础](#java-代码基础)
  - [smali 语法](#smali-语法)
  - [smali 代码阅读](#smali-代码阅读)
  - [汇编](#汇编)
  - [汇编代码阅读](#汇编代码阅读)
  - [APKtool 工具反编译 apk](#apktool-工具反编译-apk)
  - [frida环境的安装](#frida环境的安装)
  - [frida使用](#frida使用)
  - [JEB 静态分析动态调试Java层破解登录过程实例](#jeb-静态分析动态调试java层破解登录过程实例)
  - [IDA 动态调试流程](#ida-动态调试流程)
  - [IDAso层动态调试破解登录过程实例](#idaso层动态调试破解登录过程实例)
  - [工具脱壳实操](#工具脱壳实操)
  - [apk文件加壳的常用so文件命名方式](#apk文件加壳的常用so文件命名方式)

---

## Android开发

[android开发](教程/android开发.md)

在这个文档当中，我们细致的讨论，如何进行Android开发，包括

* Android系统的体系结构
* Android当中的四大组件
* 开发环境的搭建
* Android项目的文件结构
* 新建一个Android项目
* 编写一个Android项目

[通知](教程/通知.md)

> 介绍什么是通知，怎么搭建，什么是通知的渠道，以及怎么发送一个通知
> Build.builder 可以添加哪些属性
> 全屏通知的使用



目前我们所使用的语言是 Java 语言，在后续的完善当中我们会跟进kotlin语言的Android开发

---

### NDK 开发

[NDK开发](教程/NDK开发.md)

---

### CPP 文件的编译以及 OLLVM 的混淆

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

## Android 相关的基础知识

[android相关的基础知识](教程/Android相关的基础知识.md)

简介 Android 系统的框架，和四大组件

---

## Android的生命周期

[android的生命周期](教程/android的生命周期.md)

---

## Android开发流程

[Android 开发流程](教程/Android开发流程.md)

从新建工程了解 Android 开发的流程

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

[frida环境的安装](教程/frida环境的安装.md)

---

## frida使用

[frida使用](教程/frida使用.md)

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

### fart 脱壳机的理解

[fart 脱壳机的理解](教程/fart 脱壳机的理解)

> 本文章是对 fart 脱壳机的学习，分析和理解

----

### unidbg 使用教程

[unidbg 使用教程](教程/unidbg使用教程.md)

