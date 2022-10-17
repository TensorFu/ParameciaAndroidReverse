「保活」基本上是两条路：

- 提升自己进程的优先级，让系统不要轻易弄死自己；
- App 之间互相结盟，一个兄弟死了其他兄弟把它拉起来。



一般来说，系统杀进程有两种方法，这两个方法都通过 ActivityManagerService 提供：

- killBackgroundProcesses（系统一般是用的）
- forceStopPackage（用户一般用这个）但是国内的厂商和三星也是用的这个方式杀的进程，更加稳定和彻底



