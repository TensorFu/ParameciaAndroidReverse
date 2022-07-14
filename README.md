# ParameciaAndroidReverse
草履虫的Android逆向教程 [欢迎大家在issue当中指出更正的地方，或者是通过下面的联系方式联系我]

联系方式：[telegram账号](https://t.me/GitFub)

在本教程当中所使用到的用例 APK 大部分来自网络下载，如若已经侵犯你的利益，请联系删除

在本教程当中所使用到的软件版本和设备信息列表

* 设备：小米10
* 手机系统：MIUI 13（基于Android 11-12）
* PC系统：Windows10专业版
* Java：1.8.0_202
* IDA：IDA 7.5 pro
* jadx-gui：jadx-gui-1.4.2-no-jre-win.exe
* JEB：JEB 3.19.1.202005071620

---

[面试](/面试/面试题.md)

> 在这里整理了Android 逆向面试当中常见的问题以及简述答案

---

[bug处理](/bug处理/README.md)

> 在这里记录了一些笔者在实践当中出现的一些错误以及解决办法

---

- [ParameciaAndroidReverse](#parameciaandroidreverse)
  - [JEB 静态分析动态调试Java层破解登录过程实例](#jeb-静态分析动态调试java层破解登录过程实例)
  - [IDA 动态调试流程](#ida-动态调试流程)
  - [IDAso层动态调试破解登录过程实例](#idaso层动态调试破解登录过程实例)
  - [工具脱壳实操](#工具脱壳实操)

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

