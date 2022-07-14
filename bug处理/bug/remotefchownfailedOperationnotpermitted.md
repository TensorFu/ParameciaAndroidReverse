## remote fchown failed: Operation not permitted

### 问题描述

![11](media/11.png)

---

### 问题解决:

正确的指令应该是：

`adb push C:\\Users\\user\\Desktop\\JEBDebugger_so\\classes.dex /data/local/tmp`  



而不是 

`adb push C:\\Users\\user\\Desktop\\JEBDebugger_so\\classes.dex data/local/tmp` 



问题解决

![12](media/12.png)

