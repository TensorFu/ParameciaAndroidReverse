## frida使用

### 通过frida输出Hello I'm here

* 新建 .js 文档

```javascript
setTimeout
(
    function()
    {  
        Java.perform(function()
        {      
            console.log("hello world!");    
        });
    }
);
```

首先我们把一个匿名函数作 为参数传给了setTimeout()函数，在这个匿名函数体中调用了Frida 的API函数Java.perform()，这个API函数本身又接受了一个匿名函数 作为参数，该匿名函数最终调用console.log()函数来打印一个"Hello world!"字符串。这里需要调用setTimeout()方法是因为该方法将函 数注册到JavaScript运行库中，然后在JavaScript运行库中调用 Java.perform()方法将函数注册到App的Java运行库中并在其中执行 该函数(本范例打印输出了一条log)			

* 将手机/虚拟机里面的 frida-server 运行起来

`./fs`  通过这样的方式就能够运行 frida-server ，fs 是我已经对frida-server 改名，这里以你实际的 frida-server 的名字为准			

​			

* 检查是否已经运行了frida-server

`frida-ps -U`  **-U** 表示的是 USB 连接的设备，如果连接成功，就会显示，已经在手机/虚拟机上面运行的，进程，反之就不会显示正在运行的进程

​			

* 通过附加模式注入到指定的进程

`frida -U -l /Users/faker/Documents/hello_world.js "Max cleaner" ` 

**-U** 表示的是 USB 连接的设备			

**-l** 表示的是引入插件

"Max cleaner" 表示的是，想要附加的进程，这里的进程一般来说，是包名，但是主要是以 `firda-ps -U`  显示的结果为主，比方说，max cleaner 这一款软件，的包名是 `com.lpstu.max.junk.clean` 但是在 frida-ps -U 当中显示的是 Max cleaner 那么，注入进程的时候，就写 Max cleaner ，并且注意，这个名字中间有空格，所以两侧要加上双引号，如果，没有空格，那么可以不加			

----

### frida Hook Java层 普通函数

* 新建一个工程，MainActivity.java 如下

```java
package com.example.demo2;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.util.Log;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        while(true)
        {
            try{
                Thread.sleep(1000);
            }
            catch (InterruptedException e)
            {
                e.printStackTrace();
            }
            fun(50,30);
        }
    }
    void fun (int x,int y){
        Log.d("demo2.1",String.valueOf(x+y));
    }
}
```



Hook_java.js

```javascript
function main()
{
    console.log("脚本已经加载好...")
    Java.perform(function()
    {
        console.log("注入 Java perform 函数")
        var MainActivity = Java.use("com.example.demo2.MainActivity") //定位类
        console.log("Java.use 执行成功")
        MainActivity.fun.implementation = function(x,y)
        {
            console.log("x=>",x,"y=>",y)
            var ret_value = this.fun(x,y)
            return ret_value
        }
    })
}
setImmediate(main);
```

脚本中使用function关键字定义了一个main()函数，用于存放 Hook脚本，然后调用Frida的API函数Java.perform()将脚本中的内 容注入到Java运行库，这个API的参数是一个匿名函数，函数内容是 监控和修改Java函数逻辑的主体内容			

​			

在Java.perform()函数包裹的匿名函数中，首先调用了Frida的 API函数Java.use()，这个函数的参数是Hook的函数所在类的类名， 参数的类型是一个字符串类型，比如Hook的fun()函数所在类的全名，此处是 `com.example.demo2.MainActivity ` 

​			

这个函数的返回值动态 地为相应Java类获取一个JavaScript Wrapper，可以通俗地理解为 一个JavaScript对象。

在获取到对应的JavaScript对象后，通过“.”符号连接fun这个 对 应 的 函 数 名 ， 然 后 加 上 implementation 关 键 词 表 示 实 现 MainActivity对象的fun()函数		

​			

最后通过“=”这个符号连接一个匿 名函数，参数内容和原Java的内容一致。不同的是，JavaScript是一 个弱类型的语言，不需要指明参数类型。此时一个针对MainActivity 类的fun()函数的Hook框架就完成了。		

​				

这个匿名函数的内容取决于逆向开发和分析人员想修改这个被 Hook的函数的哪些运行逻辑。比如调用console.log()函数把参数内容 打印出来				

通过this.fun()函数再次调用原函数，并把原本的参数传递 给这个fun()函数。简而言之，就是重新执行原函数的内容，最后将这 个函数的返回值直接通过return指令返回。				

在Hook一个函数时，还有一个地方需要注意，那就是最好不要 修改被Hook的函数的返回值类型，否则可能会引起程序崩溃等问 题，比如直接通过调用原函数将原函数的返回值返回（如果不返回，原来的程序，该函数的后续操作就会错乱）			

​				

`setImmediate` (Frida的API函数)函数传递的参数是要被执行 的函数，比如传入main参数，表示当Frida注入App后立即执行 main()函数。				

这个函数和`setTimeout()` 函数类似，都是用于指定要执 行的函数，不同的是`setTimeout` 可以用于指定Frida注入App多长时间后执行函数，往往用于延时注入。				

如果传递的第二个参数为0或者 压根没有第二个参数，就和setImmediate()函数的作用一样

​			

### Hook Java层 重载函数

* 新建一个工程，Mainactivity 的内容如下

```java
package com.example.demo2;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.util.Log;

import java.util.Locale;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        while(true)
        {
            try{
                Thread.sleep(1000);
            }
            catch (InterruptedException e)
            {
                e.printStackTrace();
            }
            fun(50,30);
            Log.d("chongzai",fun("重载部分"));
        }
    }
    void fun (int x,int y){
        Log.d("chongzai",String.valueOf(x+y));
    }
    String fun(String x){
        return x.toLowerCase();
    }
}
```

​			

Hook_java.js

```javascript
function main()
{
    console.log("脚本加载成功...")
    Java.perform(function()
    {
        console.log("注入函数成功...")
        var MainActivity = Java.use("com.example.demo2.MainActivity")
        console.log("java.use 执行成功...")
        MainActivity.fun.overload("int","int").implementation = function(x,y)
        {
            console.log("x=>",x,"y=>",y)
            var result_value = this.fun(30,40)
            return result_value
        }
        
    })
}
setTimeout(main)
```

​				

```javascript
function main()
{
    console.log("脚本加载成功...")
    Java.perform(function()
    {
        console.log("注入函数成功...")
        var MainActivity = Java.use("com.example.demo2.MainActivity")
        console.log("java.use 执行成功...")
        MainActivity.fun.overload("java.lang.String").implementation = function(x)
        {
            console.log("x=>",x)
            var result_value = this.fun("hook string")
            return result_value
        }
        
    })
}
setTimeout(main)
```

​				

---

### 主动调用

主动调用就是强制调用一个函数去执行

如果不想分析详细的算法逻辑，可以直接通过主动传递 参数来调用关键算法函数，忽略方法函数的实现过程直接得到密文或 者明文，可以说这是各种算法调用的“克星”

在Java中，类中的函数可分为两种:类函数和实例方法。通俗地 讲，就是静态的方法和动态的方法。				

类函数使用关键字static修饰， 和对应类是绑定的，如果类函数还被public关键词修饰着，在外部就 可以直接通过类去调用			

如果是类函数的主动调用，直接 使用Java.use()函数找到类进行调用即可			

​				

实例方法则没有关键字static修饰，在外部 只能通过创建对应类的实例再通过这个实例去调用。在Frida中主动 调用的类型会根据方法类型区分开

如果是实例方法的主动调 用，则需要在找到对应的实例后对方法进行调用。这里用到了Frida 中非常重要的一个API函数Java.choose()，这个函数可以在Java的堆 中寻找指定类的实例。



* 新建一个工程，Mainactivity如下

```java
package com.example.demo2;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.util.Log;

import java.util.Locale;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        while(true)
        {
            try{
                Thread.sleep(1000);
            }
            catch (InterruptedException e)
            {
                e.printStackTrace();
            }
            fun(50,30);
            Log.d("chongzai",fun("重载部分"));
            //secret();
            //staticsecret();z
        }
    }
    void fun (int x,int y){
        Log.d("chongzai",String.valueOf(x+y));
    }
    String fun(String x){
        return x.toLowerCase();
    }
    String secret()
    {
        Log.d("sss","这是一个动态方法");
        return "动态方法被hook";
    }
    static String staticsecret()
    {
        Log.d("sss","这是一个静态方法");
        return "静态方法被hook";
    }
}
```



* 主动调用和被动调用的代码如下

```javascript
function main()
{
    console.log("脚本加载成功...")
    Java.perform(function()
    {
        console.log("注入函数成功...")
        var MainActivity = Java.use("com.example.demo2.MainActivity")
        console.log("java.use 执行成功...")
        MainActivity.fun.overload("java.lang.String").implementation = function(x)
        {
            console.log("x=>11",x)
            var result_value = this.fun("hook string")
            return result_value
        }
        
    })
}

function hook_java()
{
    console.log("脚本记载已经OK。。。")
    Java.perform(function()
    {
        var MainActivity = Java.use("com.example.demo2.MainActivity")
        console.log("脚本已经注入...")
        MainActivity.secret.implementation = function()
        {
            console.log(this.secret())
            return "";
        }
    })
}

function Djava()
{
    console.log("脚本交在成功...")
    Java.perform(function()
    {
        console.log("开始注入脚本...")

        // 主动调用静态函数
        var MainActivity = Java.use("com.example.demo2.MainActivity")
        console.log("脚本注入成功...")
        MainActivity.staticsecret()

        // 主动调用动态函数
        Java.choose(
            "com.example.demo2.MainActivity",
        {
            onMatch:function(instance)
            {
                console.log("instance found",instance)
                instance.secret()
            },
            onComplete:function()
            {
                console.log("调用完成...")
            }
        })
    })
}

 
setTimeout(Djava)
```

调用之后发现，在代码当中没有被调用的两个函数，在 `adb catlog | grep sss` 显示打印的结果

​			

可以发现静态的staticSecret()函数 和Hook时使用的方式大同小异，都是使用Java.use这个API去获取，MainActivity类，在获取对应的类对象后通过“.”连接符连接 staticSecret方法名，最终以和Java中一样的方式直接调用静态方法 staticSecret()函数			

​				

动态方法secret需要先通过Java.choose这个 API从内存中获取相应类的实例对象，然后才能通过这个实例对象去 调用动态的secret()函数，如果需要主动调用动态函数，必须确保存在相应类的对象，否则 无法进入Java.choose这个API的回调onMatch逻辑中，比如 MainActivity类对象。由于App在打开后确实运行在MainActivity界 面上，那么这个对象就一定会存在，这就是所谓的“所见即所得”思想				

---

## 自动化之RPC

就是使用Python对JavaScript脚本进行操作
