# android数据库的逆向（Line）

Android数据库：SQLite

但是它不支持加密



所以 apk 在处理的时候有两种加密的方式

1. 写进数据库的数据进行加密
2. 对整个数据库的文件进行加密（通过 SQLiteCipher 这个开源的框架）

---

1. 选在 Line 解压
2. 得到 dex 放进 jadx 得到 Java的代码
3. 反编译之后就是 smali
4. 用 Android studio 导入反编译之后的项目，准备动态调试
5. 在 Android studio 当中 [add New Configuration] 当中选择 remote 
6. 端口号改为手机应用对应的端口号



1. 分析手机的设置选项，找到一张数据库当中的数据，有一张表格记录了，允许他人通过ID添加，的选择
2. 所以我们分析这个打钩的过程，应该是打钩后将false改为true，然后对true进行加密写入数据库（更新数据库字段）
3. 使用 DDMS method profiling
4. method profiling后的结果，先使用文本编辑器将这个trace文件打开
5. 搜索文本update 分析可知，这是对数据库的更新
6. 在DDMS中查找update方法（G:\SDKplatforms\tools\lib\monitor-x86_64）
7. 看到调用这个update方法的是iec.a方法
8. 在jadx中打开iec类，查看iec.a(SQliteDatabase,cc,String)Z方法：
9. 在该方法前设置断点进行动态调试
10. 在 Android studio 里面找到这个函数，进行断点，运行动态调试
11. his.k.containsKey(ccVar)的ccVar参数，也就是key值
12. String str2 = (String) this.k.get(ccVar) 就是获取加密之后的值（str2）查看 str2 的值
13. 同时this.k便是存储要写入到数据库的数据的key-value键值对：（为啥？？？）
14. 所以需要进行代码跟踪，查找this.k的key == PROFILE_ALLOW_SEARCH_BY_ID的value值的生成的地方，也就是加密的地方。
15. 在iqc.a(iqf)这个方法里面找到了value值生成的地方：
16. 通过iqa.a(String)方法对字符串进行加密：
17. iqa.a(String)方法可以看到其调用了am.a(long,String)方法，其中传入了一个long型常量15485863L，可以考虑这个long型常量可能为了生成对称加密的秘钥而传入的。
18. 继续跟踪am.a(long,String)方法，hph.a()方法：可以很明显的看到hph.a方法使用的是AES对称加密算法对传入的str进行加密，在最后的将加密后的密文作为参数传入hxf.a()方法中
19. hxf.a()方法：很明显是将最后加密的结果进行了Base64编码，然后返回给程序
20. 到这里再回到am.a中就可以很明显的知道在调用hph.a(a(l),str)方法时传入的参数a(l)就是AES加密算法的密码，通过这个密码，在hph.a方法中生成AES加密的秘钥。
    来看AES加密算法的密码是如何生成的，进入am.a(long)方法：





* 导入项目的时候可能不是正确的方式
  * 导入的最后的时候，显示这个可能是有问题的
    * ![image-20220728165026555](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20220728165026555.png)





* 在连接远程调试的时候，教程当中是 remote ，但是实际当中只看到了 remote JVM debug（我选的这个）

* 这个地方进行了更改，端口本来是应该使用手机对应，应用的app的端口号，但是我没有查到。没有改，jdk的版本教程当中使用的是1.4，Android studio默认给我的是 jdk9 and later ，但是我电脑当中一般都是1.8，所以我选择 jdk5~8
* ![image-20220728172447096](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20220728172447096.png)

一切结束以后并没有任何的反应







