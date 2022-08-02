## 在使用JEB进行动态调试的时候一直卡在 Attaching To Target

### 问题描述



---

### 问题解决

JEB 会自动完成端口转发，不用 Device Monitor 实现端口转发；若已打开 Monitor，要关闭

如果你还打开了 Android studio 或者是其他的监视器，也一定并关闭