## smali语法

- [smali语法](#smali语法)
  - [数据类型](#数据类型)
  - [语法关键字](#语法关键字)
    - [关于 .class .super .source 的补充](#关于-class-super-source-的补充)
    - [关于 .local 关键字的补充](#关于-local-关键字的补充)
    - [类方法的声明](#类方法的声明)
    - [关于 .parameter  的补充](#关于-parameter--的补充)
  - [关于赋值](#关于赋值)
    - [变量间的赋值 const](#变量间的赋值-const)
    - [对象赋值](#对象赋值)



### 数据类型

| smali          | Java                                                         |
| -------------- | ------------------------------------------------------------ |
| V              | void（返回值的数据类型）                                     |
| Z              | Boolean                                                      |
| B              | Byte                                                         |
| S              | short                                                        |
| C              | Char                                                         |
| I              | int                                                          |
| J              | long                                                         |
| F              | float                                                        |
| D              | double                                                       |
| [类型          | 数组 <br />[I表示一个int型数据<br />[Ljava/lang/String 表示一个String的对象数组 |
| Lpackage/name; | 对象类型 L表示这是一个对象类型<br />package表示该对象所在的包<br />；表示对象名称的结束 |



### 语法关键字

| 关键词              | 说明                                                         |
| ------------------- | ------------------------------------------------------------ |
| .class              | 定义Java类的权限和类的名字                                   |
| .super              | 定义父类类名                                                 |
| .source             | 定义Java源文件<br />.source "ccccc.java"<br />这是一个由ccccc.java编译得到的smali文件 |
| .field              | 定义字段（就是局部变量名的声明）<br />.field <访问权限> <变量名>:<变量类型><br />.field actionBar:Landroid/app/ActionBar; <br /><=><br />ActionBar actionBar; |
| .method             | 方法的开始                                                   |
| .end method         | 方法的结束                                                   |
| .annotation         | 注释的开始                                                   |
| .end annotation     | 注释的结束                                                   |
| .implements         | 定义接口指令                                                 |
| .parameter / .param | 指定了方法的参数<br />有多少个方法参数就有多少个.parameter   |
| .line N关键字       | line N代表其下代码还原成java代码在源文件第N行 <br />.line 3<br />const/4 v0 0x01<br />iput v0,p0,LTest;->a:I<br />表示的是这个方法在 Java 当中的第三行 |
| .prologue           | 表示函数的代码逻辑从这一行开始<br />.method public Test()V<br/>    .registers N<br/>    .prologue<br/>    #do-something<br/>    return-void<br/>.end method |
| .registers          | 表明方法当中使用寄存器的总数，并且包括参数寄存器，下面的 .locals  这个不包括参数寄存器 |
| .locals             | 表明是申请了多少个本地寄存器                                 |
| .local              | 声明一个本地的变量<br />例如：.local v0, wait:Landroid/os/Message; |
| .locals             | 表明这一个方法内使用了多少本地寄存器<br />注意：在修改了 smali 代码之后记得修改这个值 |
| .prologue           | 表示java源文件中指定行                                       |

---

#### 关于 .class .super .source 的补充

```assembly
.class public Lcom/lvf/simplestdemo/MainActivity; # 有这么一个类，叫做 MainActivity，并且权限是 public
.super Landroid/support/v7/app/AppCompatActuvuty; # 这个类继承于 AppCompatActuvuty
.source "MainActivity.java"; # 这个类所在的文件是 MainActivity.java
```

```java
public class MainActivity extends AppCompatActivity
```





---

#### 关于 .local 关键字的补充

`.local v0, args:Landroid/os/Message;`

表明申请一个本地变量

1. $V_0$ 寄存器当中的内容作为初始值
2.  args 变量名
3. Landroid/os/Message 数据类型（Message 的数据类型）



例子1：

`.local v0, "ans":Ljava/lang/String;` <=对应源码=> `String ans=""`;  



例子2:

```assembly
.local v0, wait:Landroid/os/Message;  
const/4 v1, 0x2  
iput v1, v0, Landroid/os/Message;->what:I
```

```java
wait.what = 0x2;（wait是Message的实例）
```

---

#### 类方法的声明

```assembly
.method <访问权限> <方法名>(参数原型) <方法原型>
    [.prologue]    // 指定代码开始位置
    [.param]       // 指定方法参数
    [.line]        // 指定代码在源代码中的行数，混淆后可能不存在
    [.locals]  // 使用的局部变量个数（本地寄存器的个数）
    <代码体>
.end method
```



例子：

```assembly
.method public onTabReselected(Landroid/app/ActionBar$Tab;Landroid/app/FragmentTransaction;)V 
    .locals 0
    .param p1, "tab"    # Landroid/app/ActionBar$Tab; 
    .param p2, "fragmentTransaction"    # Landroid/app/FragmentTransaction;   
    .prologue 
    .line 55     //可能经过混淆后不存在
    return-void
.end method
```

```java
public void onTabReselected(ActionBar$Tab tab, FragmentTransaction fragmentTransaction){
}
```

---









---

#### 关于 .parameter  的补充

有多少个方法的参数就有多少个 .parameter 

并且后面就是，这个参数的名字

```java
private String packedSwitch(int i) {  
    String str = null;  
    switch (i) {  
        case 0:  
            str = "she is a baby";  
            break;  
        case 1:  
            str = "she is a girl";  
            break;  
        case 2:  
            str = "she is a woman";  
            break;  
        case 3:  
            str = "she is an obasan";  
            break;  
        default:  
            str = "she is a person";  
            break;  
    }  
    return str;  
}  
```

```assembly
.method private packedSwitch(I)Ljava/lang/String;  
    .locals 1  
    .parameter "i"  
    .prologue  
    .line 21  
    const/4 v0, 0x0  
    .line 22  
    .local v0, str:Ljava/lang/String;  #v0为字符串，0表示null  
    packed-switch p1, :pswitch_data_0  #packed-switch分支，pswitch_data_0指定case区域  
    .line 36  
    const-string v0, "she is a person"  #default分支  
    .line 39  
    :goto_0      #所有case的出口  
    return-object v0 #返回字符串v0  
    .line 24  
    :pswitch_0    #case 0  
    const-string v0, "she is a baby"  
    .line 25  
    goto :goto_0  #跳转到goto_0标号处  
    .line 27  
    :pswitch_1    #case 1  
    const-string v0, "she is a girl"  
    .line 28  
    goto :goto_0  #跳转到goto_0标号处  
    .line 30  
    :pswitch_2    #case 2  
    const-string v0, "she is a woman"  
    .line 31  
    goto :goto_0  #跳转到goto_0标号处  
    .line 33  
    :pswitch_3    #case 3  
    const-string v0, "she is an obasan"  
    .line 34  
    goto :goto_0  #跳转到goto_0标号处  
    .line 22  
    nop  
    :pswitch_data_0  
    .packed-switch 0x0    #case  区域，从0开始，依次递增  
        :pswitch_0  #case 0  
        :pswitch_1  #case 1  
        :pswitch_2  #case 2  
        :pswitch_3  #case 3  
    .end packed-switch  
.end method
```





```java 
.class public Lcom/aaaaa;     
.super Lcom/bbbbb;
.source "ccccc.java"

它是com.aaaaa这个package下的一个类（第1行）
继承自com.bbbbb这个类（第2行）
这是一个由ccccc.java编译得到的smali文件（第3行）
```



### 关于赋值

#### 变量间的赋值 const

```assembly
const                   v0, 0x7F030018  # R.layout.activity_challenge   #从R中取出静态值
const/4                 v3, 0x2   #4也可以换成16或者high16，表示取整数值
const-string            v2, "Challenge"  # 取字符串
const-class             v2, Context    #把类对象取出
```



#### 对象赋值

```assembly
iput-object             a,(this),b   将a的值给b，一般用于b的初始化
iget-object             a,(this),b   将b的值给a，一般用于获取b的地址，接着调用它
# eg.
iput-object             v0, p0, ChallengeActivity->actionBar:ActionBar
iget-object             v0, p0, ChallengeActivity->actionBar:ActionBar
```





```java
1. hello ()V --> void hello()

2. hello (III)Z --> boolean hello(int, int, int)

3. hello (Z[I[ILjava/lang/String;J)Ljava/lang/String;

-->String hello (boolean, int[], int[], String, long) 
```



判断语句

```assembly
if-eq vA, vB, :cond_X   如果vA等于vB则跳转到:cond_X     equal
if-ne vA, vB, :cond_X   如果vA不等于vB则跳转到:cond_X    not equal     
if-lt vA, vB, :cond_X   如果vA小于vB则跳转到:cond_X    less than
if-ge vA, vB, :cond_X   如果vA大于等于vB则跳转到:cond_X    great than or equal
if-gt vA, vB, :cond_X   如果vA大于vB则跳转到:cond_X    great than
if-le vA, vB, :cond_X   如果vA小于等于vB则跳转到:cond_X    less than or equal
if-eqz vA, :cond_X      如果vA等于0则跳转到:cond_X
if-nez vA, :cond_X      如果vA不等于0则跳转到:cond_X
if-ltz vA, :cond_X      如果vA小于0则跳转到:cond_X
if-gez vA, :cond_X      如果vA大于等于0则跳转到:cond_X
if-gtz vA, :cond_X      如果vA大于0则跳转到:cond_X
if-lez vA, :cond_X      如果vA小于等于0则跳转到:cond_X
```



