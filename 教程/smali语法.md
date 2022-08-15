## smali语法

- [smali语法](#smali语法)
  - [数据类型](#数据类型)
  - [语法关键字](#语法关键字)
    - [关于 .class .super .source 的补充](#关于-class-super-source-的补充)
    - [关于 .field 的补充](#关于-field-的补充)
    - [关于 .local 关键字的补充](#关于-local-关键字的补充)
    - [类方法的声明](#类方法的声明)
    - [关于 .parameter  的补充](#关于-parameter--的补充)
  - [关于赋值](#关于赋值)
    - [变量间的赋值 const](#变量间的赋值-const)
    - [对象赋值](#对象赋值)
  - [判断语句](#判断语句)
  - [函数的调用 invoke](#函数的调用-invoke)
  - [smali 代码阅读](#smali-代码阅读)
    - [例子1](#例子1)
    - [例子2](#例子2)
    - [例子3](#例子3)
    - [例子4 for 循环](#例子4-for-循环)
    - [例子5 switch-case（两种【零散，有组织的】）](#例子5-switch-case两种零散有组织的)



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
| .field              | 定义字段（就是成员变量名的声明，成员变量定义在类中，整个类都可以访问）<br />.field <访问权限><修饰关键字 static/final...> <变量名>:<变量类型><br />.field actionBar:Landroid/app/ActionBar; <br /><=><br />ActionBar actionBar; |
| .method             | 方法的开始                                                   |
| .end method         | 方法的结束                                                   |
| .annotation         | 注解的开始                                                   |
| .end annotation     | 注解的结束                                                   |
| .implements         | 定义接口指令                                                 |
| .parameter / .param | 指定了方法的参数<br />有多少个方法参数就有多少个.parameter   |
| .line N关键字       | line N代表其下代码还原成java代码在源文件第N行 <br />.line 3<br />const/4 v0 0x01<br />iput v0,p0,LTest;->a:I<br />表示的是这个方法在 Java 当中的第三行 |
| .prologue           | 表示函数的代码逻辑从这一行开始<br />.method public Test()V<br/>    .registers N<br/>    .prologue<br/>    #do-something<br/>    return-void<br/>.end method |
| .registers          | 表明方法当中使用寄存器的总数，并且包括参数寄存器，下面的 .locals  这个不包括参数寄存器 |
| .locals             | 表明是申请了多少个本地寄存器（不包含参数寄存器）<br />注意：在修改了 smali 代码之后记得修改这个值 |
| .local              | 声明一个本地的变量<br />例如：.local v0, wait:Landroid/os/Message; |

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

#### 关于 .field 的补充

.field <访问权限 protect/private/public ><修饰关键字 static/final...> <变量名>:<变量类型>

例子1：

```assembly
.field private static final TAG:Ljava/lang/String; = "MainActivity"
```

```java
private  static final String TAG = "MainActivity";
```

​    

例子2：

```assembly
.field private mButton:Landroid/widget/Button;
```

```java
private Button mButton
```

---

#### 关于 .local 关键字的补充

`.local v0, args:Landroid/os/Message;`

表明申请一个本地变量

1. $V_0$ 寄存器当中的内容作为初始值
2.  args 变量名
3. Landroid/os/Message 数据类型（Message 的数据类型）



例子1：

```assembly
.local v0, "ans":Ljava/lang/String;
```

```java
String ans="";  
```

​     

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

---

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

---

### 判断语句

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

---

### 函数的调用 invoke

1. private：invoke-direct 
2. public    |    protected： invoke-virtual 
3. static：invoke-static 
4. parent:  invoke-super



基本调用形式：invoke-xxx {参数},类;->函数(参数原型)   



例子：

```assembly
invoke-super {p0, p1}, Landroid/support/v4/app/FragmentActivity;->onCreate(Landroid/os/Bundle;)V
```

```java
super.onCreate(savedInstanceState);  // 其中p0是this，其父类是FragmentActivity，p1,是savedInstanceState，其原型是Bundle；即调用p0->onCreate(p1)
```



```assembly
const-string v0, "NDKLIB"
invoke-static {v0}, Ljava/lang/System;->loadLibrary(Ljava/lang/String;)V
```

```java
System.loadLibrary("NDKLIB")
```





---

### smali 代码阅读

#### 例子1

```assembly
.method private ifRegistered()Z
    .locals 2            // 本地寄存器的个数
    .prologue
    const/4 v0, 0x1      //v0赋值为1
    if-eqz v0, :cond_0   //判断v0是否等于0，等于0则跳到cond_0执行
    const/4 v1, 0x1      //符合条件分支
    :goto_0              //标签
    return v1            //返回v1的值
    :cond_0              //标签
    const/4 v1, 0x0      //cond_0分支
    goto :goto_0         //跳到goto_0执行
.end method
```



#### 例子2

```assembly
.local v0, args:Landroid/os/Message;
const/4 v1, 0x12
iput v1,v0,Landroid/os/Message;->what:I
```

```java
args.what = 18
```



#### 例子3

```assembly
const-string v0, "Eric"
invoke-static {v0}, Lcmb/pbi;->t(Ljava/lang/String;)Ljava/lang/String;
move-result-object v2
```

表示将方法t返回的String对象保存到 $V_2$ 中，并且返回出去

move-result / move-result-object 有相同的效果



#### 例子4 for 循环

```java
public void encrypt(String str) {
    String ans = "";
    for (int i = 0 ; i < str.length();i++){
        ans += str.charAt(i);
    }
    Log.e("ans:",ans);
}
```

```assembly
# public void encrypt(String str) {
.method public encrypt(Ljava/lang/String;)V 
.locals 4  # 使用了四个局部变量 
.param p1, "str"# Ljava/lang/String;  # 类型 string str 的参数 就是传进来的这个 String str
.prologue  # 代码开始

# String ans = "";
const-string v0, ""  # 给v0 空的字符串
.local v0, "ans":Ljava/lang/String;  # ans = ""

# for (int i  0 ; i < str.length();i++){
# int i=0 =>v1
const/4 v1, 0x0 # v1 = 0
.local v1, "i":I # int i = 0

:goto_0         # 标签 第一次遇到是可以直接进入的，如果后面再次遇到，就会回到这里
# str.length()=>v2
invoke-virtual {p1}, Ljava/lang/String;->length()I # str(p1).length()
move-result v2 # 通过 v2 返回上面的 结果 v2 = str.length()

# i<str.length() 
if-ge v1, v2, :cond_0 # 如果v1 >= v2 跳转到 cond_0

# ans += str.charAt(i); 
# str.charAt(i) => v2
new-instance v2, Ljava/lang/StringBuilder;  # 新建一个 StringBuilder 的对象，并且放进 v2 寄存器
invoke-direct {v2}, Ljava/lang/StringBuilder;-><init>()V # 就是一个初始化常常和上面的一起出现
invoke-virtual {v2, v0}, Ljava/lang/StringBuilder;->append(Ljava/lang/String;)Ljava/lang/StringBuilder; # StringBuilder(v2).append(string v0->ans变量)
move-result-object v2  # 第一次执行的时候就是一个 空的字符串 v2->ans = ""

#str.charAt(i) => v3
invoke-virtual {p1, v1}, Ljava/lang/String;->charAt(I)C # string(p1->string str).charAt(int v1->i)
move-result v3 # char v3 = string.charAt(int i)

# ans += v3 =>v0
invoke-virtual {v2, v3}, Ljava/lang/StringBuilder;->append(C)Ljava/lang/StringBuilder; # StringBuilder(v2->ans).append(char v3)
move-result-object v2 # 将结果覆盖 v2 
invoke-virtual {v2}, Ljava/lang/StringBuilder;->toString()Ljava/lang/String; # StringBuilder(v2).toString()
move-result-object v0 # 结果放在 v0

# i++
add-int/lit8 v1, v1, 0x1 # i++ 
goto :goto_0

# Log.e("ans:",ans);
:cond_0
const-string v2, "ans:" 
invoke-static {v2, v0}, Landroid/util/Log;->e(Ljava/lang/String;Ljava/lang/String;)I # log.e(v2("ans:"),v0(变量ans))
return-void  
.end method
```





#### 例子5 switch-case（两种【零散，有组织的】）

java 当中的 switch-case 每一个 case 里面都应该有一个break，如果没有，就算找到了，后面还是会继续执行

```java
public void encrypt(int flag) {
        String ans = null;
        switch (flag){
            case 0:
                ans = "ans is 0";
                break;
            default:
                ans = "noans";
                break;
        }
        Log.v("ans:",ans);
    }
```

```assembly
#public void encrypt(int flag) {
.method public encrypt(I)V  # void encrypt(int flag)
    .locals 2 # 两个本地寄存器，两个局部变量
    .param p1, "flag"    # I 传进来的int flag
    .prologue
#String ans = null;
    const/4 v0, 0x0 # v0 = 0
    .local v0, "ans":Ljava/lang/String; # string ans = 0
#switch (flag){
    packed-switch p1, :pswitch_data_0 # pswitch_data_0指定case区域的开头及结尾

#default: ans="noans"
    const-string v0, "noans" # v0 = "noans"
#Log.v("ans:",ans)
    :goto_0
    const-string v1, "ans:" # v1 = "ans"
    invoke-static {v1, v0}, Landroid/util/Log;->v(Ljava/lang/String;Ljava/lang/String;)I # int log.v(v1,v0)
    return-void
#case 0: ans="ans is 0"
    :pswitch_0      #pswitch_<case的值>
    const-string v0, "ans is 0" # v0 = "ans is 0"
    goto :goto_0  # break 
    nop

    :pswitch_data_0 # case区域的结束
    .packed-switch 0x0   #定义case的情况
        :pswitch_0   #case 0
    .end packed-switch

.end method
```

packed-switch 指令。p1为传递进来的 int 类型的数值

pswitch_data_0  为case 区域

第一条指令“.packed-switch”指定了比较的初始值为0 也就是从哪一个开始

pswitch_0~ pswitch_3分别是比较结果为“case 0 ”到“case 3 ”时要跳转到的地址

可以发现，标号的命名采用 **pswitch_ 开关**，后面的数值为 case 分支需要判断的值，并且它的值依次递增

再来看看这些标号处的代码，每个标号处都使用v0 寄存器初始化一个字符串

然后跳转到了goto_0 标号处，可见goto_0 是所有的 case 分支的出口



**零散的**

```java
private String sparseSwitch(int age) {
    String str = null;
    switch (age) {
        case 5:
            str = "he is a baby";
            break;
        case 15:
            str = "he is a student";
            break;
        case 35:
            str = "he is a father";
            break;
        case 65:
            str = "he is a grandpa";
            break;
        default:
            str = "he is a person";
            break;
    }
    return str;
}
```

```assembly
.method private sparseSwitch(I)Ljava/lang/String;
    .locals 1
    .parameter "age"
    .prologue
    .line 43
    const/4 v0, 0x0
    .line 44
    .local v0, str:Ljava/lang/String;
    sparse-switch p1, :sswitch_data_0  # sparse-switch分支，sswitch_data_0指定case区域 # 看到sparse-switch 表示的这是零散的 switch 并且直接跳转到 sswitch_data_0 这个位置  
    .line 58
    const-string v0, "he is a person"  #case default

    .line 61
    :goto_0    #case 出口
    return-object v0  #返回字符串

    .line 46
    :sswitch_0    #case 5
    const-string v0, "he is a baby"
    .line 47
    goto :goto_0 #跳转到goto_0标号处

    .line 49
    :sswitch_1    #case 15
    const-string v0, "he is a student"
    .line 50
    goto :goto_0 #跳转到goto_0标号处
    .line 52
    :sswitch_2    #case 35
    const-string v0, "he is a father"
    .line 53
    goto :goto_0 #跳转到goto_0标号处

    .line 55
    :sswitch_3    #case 65
    const-string v0, "he is a grandpa"
    .line 56
    goto :goto_0 #跳转到goto_0标号处
    .line 44
    nop
    :sswitch_data_0
    .sparse-switch            #case 区域
        0x5 -> :sswitch_0     #case 5(0x5)
        0xf -> :sswitch_1     #case 15(0xf)
        0x23 -> :sswitch_2    #case 35(0x23)
        0x41 -> :sswitch_3    #case 65(0x41)
    .end sparse-switch
.end method
```

在 发现了 sparse-switch 之后直接跳到

sswitch_data_0 的代码区块，但是这里的并没有给出 case 的初始值

```
    0x5 -> :sswitch_0     #case 5(0x5)
    0xf -> :sswitch_1     #case 15(0xf)
    0x23 -> :sswitch_2    #case 35(0x23)
    0x41 -> :sswitch_3    #case 65(0x41)
```

不同的 p1 的值对应不同的 sswitch_x

---

```assembly
sget-object v0, Lcom/aaa;->ID:Ljava/lang/String;
```

sget-object就是用来获取变量值并保存到紧接着的参数的寄存器中，在这里，把上面出现的ID这个String成员变量获取并放到v0这个寄存器中,因为只指出了该类的所属的类型,可以看出这是个静态的(static fields)



```assembly
sget-object v0, Lcom/disney/Class1;->PREFS_INSTALLATION_ID:Ljava/lang/String;
```

上句中sget-object指令把PREFS_INSTALLATION_ID这个String成员变量获取并放到v0寄存器中。



```assembly
iget-object v0, p0, Lcom/disney/Class1;->_view:Lcom/disney/Class2;
```

上句iget-object指令比sget-object多了一个参数p0，就是该变量所在类的实例，在这里就是p0即“this”。



```assembly
const/4 v3, 0x0
sput-object v3, Lcom/disney/Class1;->globalIapHandler:Lcom/disney/config/GlobalPurchaseHandler;
```

Class1.globalIapHandler = null;



