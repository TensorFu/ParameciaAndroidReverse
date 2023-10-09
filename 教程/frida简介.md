## Frida的简介以及安装

[Frida的Github官网](https://github.com/frida/frida)

在这个官网当中，我们知道

是一种动态插桩工具，可以插入一些代码到原生`app`的内存空间去，（动态地监视和修改其行为）

也就是说能够，将我们的 app 当中的代码，劫持住，并且获取这个函数的，输入，已经输出。		

并且，我们能够修改输入的函数，得到不一样的输出，比方说，当我们接收到，下发下来的VIP:true，的字段，我们才会开启会员的服务，我们可以直接修改这里的，判断函数，将我们的 app ，无论何时，接收到的，会员判定函数的输入都是 true ，那么就能够实现，破解会员功能的目的。			

同样的，我们还能够，直接修改返回值，也就是说，无论我们接收到什么参数，中间经过何种的计算，和判断，我们直接将这个，会员的判定函数，返回值设置为 true ，那么也能够实现相似的功能。

​					

### 安装

* 安装frida-tools 和 firda （整个过程比较的缓慢，可以使用 jnettop 查看下载的进度）

`pip3 install frida-tools ` 			

`pip3 install frida` 				

​		

* 下载 frida-server [下载链接](https://github.com/frida/frida/releases)  		

需要注意的是，这个 firda-server 一定要跟你的 firda 的版本是一样的。并且，注意你的设备的 cpu 是64位的还是32位的，通过 `getprop ro.product.cpu.abi` 这个指令就能够看得到你的设备的位数，		

![image-20220926201451519](./assets/image-20220926201451519.png)

​							

* 将这个 firda-server 文件解压之后，通过 push 指令，发送到 /data/local/tmp 文件夹下面
* 并且将这个文件的权限通过 chmod 指令设置为最高

![image-20220926203544585](./assets/image-20220926203544585.png)



### 