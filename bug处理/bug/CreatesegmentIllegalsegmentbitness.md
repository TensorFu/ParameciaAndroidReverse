## Create segment (12C00000-32C00000, sel 00000000):Illegal segment bitness.

### 问题描述

![17](media/17.png)

---

### 问题解决

出现这个错误是因为android_server与调试设备位数不一样   

例如64位的手机使用32位的android_server。  

