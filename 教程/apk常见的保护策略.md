## apk常见的一个保护策略

### 混淆

java层的混淆，ProGuard工具 



资源文件的混淆【MT 针对单个 smali 做修改】



SO 层的混淆 ollvm



签名校验

34

---

#### 模拟器检测Java层，SO很少

![image-20230908213244190](./assets/image-20230908213244190.png)

![image-20230908213346677](./assets/image-20230908213346677.png)



![image-20230908213442034](./assets/image-20230908213442034.png)



![image-20230908213526445](./assets/image-20230908213526445.png)



![image-20230908213702691](./assets/image-20230908213702691.png)



![image-20230908213755470](./assets/image-20230908213755470.png)



![image-20230908213821715](./assets/image-20230908213821715.png)



![image-20230908213849927](./assets/image-20230908213849927.png)



![image-20230908213938409](./assets/image-20230908213938409.png)



![image-20230908214043136](./assets/image-20230908214043136.png)



![image-20230908214213872](./assets/image-20230908214213872.png)

---

![image-20230908214303246](./assets/image-20230908214303246.png)

![image-20230908214320961](./assets/image-20230908214320961.png)



---

反调试



![image-20230908223154416](./assets/image-20230908223154416.png)

_start 

__libc_init

main



![image-20230908223901865](./assets/image-20230908223901865.png)



23946

![image-20230908224458739](./assets/image-20230908224458739.png)



检测 tracepid（？？？？？）

0 -> 1

​		

进程名称检测（？？？？）

