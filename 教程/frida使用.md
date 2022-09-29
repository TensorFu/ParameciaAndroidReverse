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
```







