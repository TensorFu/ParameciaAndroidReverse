# IDAso层动态调试破解登录过程实例


- [IDAso层动态调试破解登录过程实例](#idaso层动态调试破解登录过程实例)
    - [检查是否可以调试](#检查是否可以调试)
    - [静态分析 APK](#静态分析-apk)
    - [进行附加进程调试](#进行附加进程调试)


***此教程当中所用的 APK 在 release 当中的  IDADebugger_so.zip 压缩包当中***



### 检查是否可以调试

查看 Manifest.xml 的文件的 debuggerable 如果是 True 那么就是可以进行调试的，如果是 false 就说明不能够进行调试（将他放在 Androidkiller 当中改好了以后，回编译，打包进行调试）

![29](media/29.png)



### 静态分析 APK 

找到了整个程序的入口

![31](media/31.png)



通过这个程序的入口分析这个程序，找到了验证账号和密码的位置在 chech() 函数这个地方

![32](media/32.png)



双击进去查看这个函数发现这是一个被 native 修饰的函数，说明函数的实现是通过 C语言实现的，也就是 so 层

![33](media/33.png)



将你的对应的 apk 文件解压，发现这个文件夹下面还 x86 和 armeabi-v7a 的文件夹，说明这个 apk 是 32位 的 apk 对应的，需要打开 32位 的 IDA pro ，并且将 \JEBDebugger_so\lib\armeabi\libJniTest.so 文件放在 IDA pro 当中（因为 JEB 不能够查看 so 层的信息）

![34](media/34.png)



直接选择 **ok** 

![35](media/35.png)



打开 Exports 表格，查找我们需要分析的函数

![36](media/36.png)



因为我们的函数叫做 check() 函数所以它的名字叫做 Java_demo2_jni_com_myapplication_myJNI_check

![38](media/38.png)



双击刚刚的那个函数，就能够看得到这个界面，在这个界面按下 F5 能够将汇编代码转变成 C 代码

![40](media/40.png)



鼠标右键选择 Hide casts 选择隐藏数据类型（目的是为了查看代码方便）

![41](media/41.png)



类似这样的就是 IDA pro 没有识别到，需要手动识别

![42](media/42.png)



双击进入按下 A（进行手动识别字符串）/P（进行手动识别函数）->  Esc（返回）-> tab / F5 （切换到 C 代码） -> F5（刷新）

![43](media/43.png)

![44](media/44.png)

![45](media/45.png)

![46](media/46.png)

![47](media/47.png)



修改 check() 函数的数据类型，我们知道这个函数的前面的两个参数 分别是 JNIEnv *env 和 jobject obj ，按 Y 键进行数据类型的修改

![49](media/49.png)



修改 check() 函数的参数，按 N 键，进行参数的重命名

![50](media/50.png)



通过 JEB 的静态分析，我们知道 Check() 一共有三个参数

MainActivity.this.ct

MainActivity.this.User_Name.getText().toString().trim()

MainActivity.this.User_Pass.getText().toString().trim()

第一个是什么我们不用管

第二个是用户名

第三个是密码

分别对应了 int a4, int a5，a4 参数在后面转换成了 $V_9$ ，a5 参数在后面转换成了 $V_{13}$

![51](media/51.png)

![52](media/51.png)



通过分析参数，找到了账号和密码的判断函数

![53](media/53.png)



### 进行附加进程调试

* 将 Android_server（如果是64位的软件就需要使用 Android_server64 ） push 到 data/local/tmp 文件夹当中 `adb push android_server /data/local/tmp`

* 给一个 root 的权限 `su` 

* 给他一个 777 的最高权限 `chmod 777 android_server` 

* 最好将 Android_server 改名，防止关键文件检测 `mv android_server as32` 

* 将 Android_server 运行起来最好同时改一个端口，防止端口检测 `./as -p31928` 

  ![55](media/55.png)



进行端口的转换

![56](media/56.png)



打开你的软件让他出运行的状态

打开 IDA pro （需要打开对应的 IDA pro 在刚刚的分析当中我们已经知道这个 APP 是 32位 的 APP 所以 使用 IDA pro 如果是 64 位的 APP 那么就使用 IDA pro 64）

选择 Debugger -> Attach -> Remote ...

![54](media/54.png)



hostname 就选择 127.0.0.1

port 就选择 Android_server 的端口 23946

![57](media/57.png)



选择你要调试的进程

![58](media/58.png)

![59](media/59.png)



在 modules 当中搜索 libJniTest.so（在 JEBDebugger_so\lib\armeabi 路径下）

![60](media/60.png)

![61](media/61.png)



双击进入找到，我们调试的 check() 函数，双击进入

![62](media/62.png)



F5 将汇编代码转换成 C 代码，通过上面介绍的方法，将没有识别的部分转换成代码，隐藏数据类型

![63](media/63.png)



根据静态分析的数据，这个位置在进行账号的比对，在这个位置 tab 转换成汇编代码

![64](media/64.png)



会发现这个函数在汇编当中对应的位置，在这个位置 F2 下断点，F9 运行程序（或者是运行到下一个断点的位置），并在手机上点击登录

![65](media/65.png)



会发现程序停在了断点的位置

![66.png](media/66.png)



可以发现在这个函数的前面有两个寄存器，那分别是判断函数的两个参数，并且最后判断是否跳转的依据是 $V_0$ 是不是等于 0 ，说明结果存放在 $V_0$ 当中

![67](media/67.png)



下面的思路就是修改 $V_0$ 寄存器的值，让他直接返回 0 实现跳转，或者是，直接修改两个寄存器的值，让他们比对成功

1. 直接修改返回值 $V_0$ 的值，让他直接判断成功

![68](media/70.png)

选择将寄存器的内容全部置 0 下面的密码校验也是如此

![](media/71.png)

![72](media/72.png)

通过了密码检测之后，直接 F9 就能够看到手机上显示登陆成功

2. 通过修改参数，强行比对成功

先点二进制显示区域

![73](media/73.png)

再进入 $R_1$ 寄存器查看他的内容，并且记录下他的值

![75](media/75.png)

再进入 $R_0$ 寄存器，查看他的值，并且通过 F2 修改他的值（就是 $R_1$ 的值），然后 F2 保存，密码的校验是一样的

![76](media/76.png)

等到密码校验的寄存器也修改了以后， F9 运行，在手机上看到登陆成功，就说明，成功了





