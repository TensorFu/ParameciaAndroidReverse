## java代码基础

- [java代码基础](#java代码基础)
  - [static关键字](#static关键字)
    - [static关键字修饰方法](#static关键字修饰方法)
    - [static关键字修饰变量](#static关键字修饰变量)
    - [static静态代码块](#static静态代码块)
  - [构造函数](#构造函数)
  - [方法重写与方法重载](#方法重写与方法重载)
  - [接口](#接口)
  - [startsWith()](#startswith)
  - [TextUtils.isEmpty](#textutilsisempty)
  - [Bundle](#bundle)
  - [Context](#context)
  - [synchronized](#synchronized)
  - [volatile](#volatile)

### static关键字

可以修饰 变量 函数    

方便在没有创建对象的情况下来进行调用，并且全局通用，各个对象的关键字变量之间互相影响   

static 可以修饰 类 ，变量 ，方法     

下面介绍后面两种    

​     

#### static关键字修饰方法

```java
public class StaticMethod {
    public static void test() {
        System.out.println("============= 静态方法=============");
    };
    public static void main(String[] args) {
        //方式一：直接通过类名
        StaticMethod.test(); // 直接调用 类.方法 就能够直接使用，是静态方法的特点
        //方式二：
        StaticMethod fdd=new StaticMethod(); // 传统的先实例化对象，再通过实例化的对象调用方法
        fdd.test();
    }
}
```

​    

#### static关键字修饰变量    

被static修饰的成员变量叫做静态变量，也叫做类变量，说明这个变量是属于这个类的，而不是属于是对象，没有被static修饰的成员变量叫做实例变量，说明这个变量是属于某个具体的对象的   

```java
public class StaticVar {
    private static String name="java的架构师技术栈"；
    public static void main(String[] args) {
        //直接通过类名
        StaticVar.name;
    }
}
```

​    

#### static静态代码块

它是**随着类的加载而执行，只执行一次，并优先于主函数**。具体说，**静态代码块是由类调用**的。类调用时，先执行静态代码块，然后才执行主函数的。

**静态代码块其实就是给类初始化的，而构造代码块是给对象初始化的**

```java
public class MainActivity extends Activity implements View.OnClickListener {
    Button P;
    Button S;
    int cnt;
    int flag;
    private final Handler handler;
    int m;
    int n;
    Button r;
    private final Runnable showMessageTask;

    static {
        System.loadLibrary("calc"); // 静态代码块
    }

    public MainActivity() {
        this.cnt = 0;
        this.handler = new Handler();
        this.showMessageTask = new Runnable() {
        };
    }

    public native int calc() {
    }
```

---

### 构造函数

就是初始化实例    

由于构造方法是如此特殊，所以构造方法的名称就是类名。构造方法的参数没有限制，在方法内部，也可以编写任意语句。但是，和普通方法相比，构造方法没有返回值（也没有`void`），调用构造方法，必须用`new`操作符

```java
public class Main {
    public static void main(String[] args) {
        Person p = new Person("Xiao Ming", 15);
        System.out.println(p.getName());
        System.out.println(p.getAge());
    }
}

class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public String getName() {
        return this.name;
    }

    public int getAge() {
        return this.age;
    }
}
```

---

### 方法重写与方法重载

@Override	方法重写

重写是子类对父类的允许访问的方法的实现过程进行重新编写, 返回值和形参都不能改变。**即外壳不变，核心重写！**    

重写的好处在于子类可以根据需要，定义特定于自己的行为。 也就是说子类能够根据需要实现父类的方法。

```java
    public MainActivity() {
        this.cnt = 0;
        this.handler = new Handler();
        this.showMessageTask = new Runnable() {
            @Override //方法重载的标志
            public void run() {
                TextView tv3 = (TextView)MainActivity.this.findViewById(0x7F0C0052);  // id:textView3
                if(MainActivity.this.n - MainActivity.this.m == 1) {
                    ++MainActivity.this.cnt;
                    tv3.setText("WIN! +" + String.valueOf(MainActivity.this.cnt));
                }
                else if(MainActivity.this.m - MainActivity.this.n == 1) {
                    MainActivity.this.cnt = 0;
                    tv3.setText("LOSE +0");
                }
                else if(MainActivity.this.m == MainActivity.this.n) {
                    tv3.setText("DRAW +" + String.valueOf(MainActivity.this.cnt));
                }
                else if(MainActivity.this.m < MainActivity.this.n) {
                    MainActivity.this.cnt = 0;
                    tv3.setText("LOSE +0");
                }
                else {
                    ++MainActivity.this.cnt;
                    tv3.setText("WIN! +" + String.valueOf(MainActivity.this.cnt));
                }

                if(1000 == MainActivity.this.cnt) {
                    tv3.setText("SECCON{" + String.valueOf((MainActivity.this.cnt + MainActivity.this.calc()) * 107) + "}");
                }

                MainActivity.this.flag = 0;
            }
        };
    }

    public native int calc() {
    }
```

​		



重载(overloading)		没有关键字

是在一个类里面，方法名字相同，而参数不同。返回类型可以相同也可以不同。		

每个重载的方法（或者构造函数）都必须有一个独一无二的参数类型列表。		

简而言之就是新的方法名字相同但是参数不同，实现的功能也不同		

最常用的地方就是构造器的重载。

```java
public class Overloading {
    public int test(){
        System.out.println("test1");
        return 1;
    }
 
    public void test(int a){
        System.out.println("test2");
    }   
 
    //以下两个参数类型顺序不同
    public String test(int a,String s){
        System.out.println("test3");
        return "returntest3";
    }   
 
    public String test(String s,int a){
        System.out.println("test4");
        return "returntest4";
    }   
 
    public static void main(String[] args){
        Overloading o = new Overloading();
        System.out.println(o.test());
        o.test(1);
        System.out.println(o.test(1,"test3"));
        System.out.println(o.test("test4",1));
    }
}
```

---

### 接口

首先接口通过 inerface 进行定义		

通过 implements 进行实现		

接口之间的继承还是通过 extends 进行实现的		

因为Java当中不支持多继承，但是接口支持多继承		

所以可以多个接口共同实现一个		

可以把它理解成，支持多继承的一个类		

但是接口是不支持直接实现类，它更像是父类的一个补充		

```java
public inerface Runner
{
  int ID = 1;
  void run ();
}
interface Animal extends Runner
{
  void breathe ();
}
class Fish implements Animal
{
  public void run ()
{
   System.out.println("fish is swimming");
}
public void breather()
{
   System.out.println("fish is bubbing");   
}
}
abstract LandAnimal implements Animal
{
  public void breather ()
{
   System.out.println("LandAnimal is breathing");
}
}
class Student extends Person implements Runner
{
   ......
   public void run ()
    {
         System.out.println("the student is running");
    }
   ......
}

interface Flyer
{
  void fly ();
}
class Bird implements Runner , Flyer
{
  public void run ()
   {
       System.out.println("the bird is running");
   }
  public void fly ()
   {
       System.out.println("the bird is flying");
   }
}
class TestFish
{
  public static void main (String args[])
   {
      Fish f = new Fish();
      int j = 0;
      j = Runner.ID;
      j = f.ID;
   }
}
```

----

### startsWith()

startsWith() 方法用于检测字符串是否以指定的前缀开始

---

### TextUtils.isEmpty

用来判断字符串是不是为空

```java

public static boolean isEmpty(CharSequence str) {  
    if (str == null || str.length() == 0)  
        return true;  
    else  
        return false;  
```

在字符串为null或者""的情况下，都是可以用 TextUtils.isEmpty() 来进行判断的，因为当""情况下，str.length()==0，所以同样也会返回true

---

### TextUtils.isDigitsOnly

用来判断字符串是不是全部都是数字

---

### Bundle

这个类似于 Python 当中的字典

Bundle主要用于传递数据；它保存的数据，是以key-value(键值对)的形式存在的。

我们经常使用Bundle在Activity之间传递数据，传递的数据可以是boolean、byte、int、long、float、double、string等基本类型或它们对应的数组，也可以是对象或对象数组。当Bundle传递的是对象或对象数组时，必须实现Serializable 或 Parcelable接口。下面分别介绍Activity之间如何传递基本类型、传递对象

​		

Bundle提供了各种常用类型的putXxx()/getXxx()方法

---

### Context

Context的中文翻译为：语境; 上下文; 背景; 环境，在开发中我们经常说称之为“上下文”，那么这个“上下文”到底是指什么意思呢？在语文中，我们可以理解为语境，在程序中，我们可以理解为当前对象在程序中所处的一个环境，一个与系统交互的过程。比如微信聊天，此时的“环境”是指聊天的界面以及相关的数据请求与传输，Context在加载资源、启动Activity、获取系统服务、创建View等操作都要参与。

​							

那Context到底是什么呢？一个Activity就是一个Context，一个Service也是一个Context。Android程序员把“场景”抽象为Context类，他们认为用户和操作系统的每一次交互都是一个场景，比如打电话、发短信，这些都是一个有界面的场景，还有一些没有界面的场景，比如后台运行的服务（Service）。一个应用程序可以认为是一个工作环境，用户在这个环境中会切换到不同的场景，这就像一个前台秘书，她可能需要接待客人，可能要打印文件，还可能要接听客户电话，而这些就称之为不同的场景，前台秘书可以称之为一个应用程序。

​			

Context一共有三种类型，分别是Application、Activity和Service。这三个类虽然分别各种承担着不同的作用，但它们都属于Context的一种，而它们具体Context的功能则是由ContextImpl类去实现的

​			

就像它的名字(上下文)一样，他是项目当前的状态的一个标识，他可以让新创建出来，新加入进来的对象或组件知道当前项目的进度，处于一个什么状态，这样我们就可以容易理解上下文的意思了把，上文就是自己知道了之前项目已经处于一个什么样的状态，下文就是告诉后来的对象或者组件当前项目处于一个什么状态。
你可以通过getApplication()、getContext()、getBaseContext()或者this(在当前的Activity中时)来获取context上下文。

​			

---

### synchronized

synchronized可以保证方法或者代码块在运行时，同一时刻只有一个方法可以进入到临界区			

一个线程访问一个对象中的synchronized(this)同步代码块时，其它线程试图访问该对象的线程将被阻塞			

---

### volatile

**变量修改对其他线程立即可见**			

就是我在一个线程对一个变量进行了修改，那么其他线程马上就可以知道我修改了他	

---

### getString()

**getString**表示以 Java 编程语言中String的形式获取此 ResultSet 对象的当前行中指定列的值。			

```java
Connection conn = ……  //省略部分代码
String sql = "SELECT username,pwd FROM myTable";
Statement st = conn.createStatement();
ResultSet rs = st.executeQuery(sql);
while(rs.next()){
    System.out.println(rs.getString("username"));  //获取username列的列值
    System.out.println(rs.getString("pwd"));  //获取pwd列的列值
}
```

​							

```java
Connection conn = ……  //省略部分代码
String sql = "SELECT username,pwd FROM myTable";  //定义查询SQL语句
Statement st = conn.createStatement();
ResultSet rs = st.executeQuery(sql);
while(rs.next()){
    System.out.println(rs.getString(1));  //获取数据表中第一列数据值
    System.out.println(rs.getString(2));  //获取数据表中第二列数据值
}
```

---

### System.currentTimeMillis()

生产一个当前的毫秒数，一个从1970年1月1日开始的毫秒数

---

### MMKV

是一种支持多进程的字典

MMKV 是基于 mmap 内存映射的 key-value 组件

MMKV 的使用非常简单，所有变更立马生效，无需调用 sync、apply。

​			

MMKV 提供一个全局的实例，可以直接使用

```java
import com.tencent.mmkv.MMKV;
//……

//1. 获取默认全局实例 (一般就使用这个就行)
MMKV kv = MMKV.defaultMMKV();

//2. 也可以自定义MMKV对象，设置自定ID  (根据业务区分的存取实例)
MMKV kv = MMKV.mmkvWithID("ID");

//3. MMKV默认是支持单进程的，如果业务需要多进程访问，需要在初始化的时候添加多进程模式参数
MMKV kv = MMKV.mmkvWithID("ID", MMKV.MULTI_PROCESS_MODE); //多进程同步支持
```

​				

```java
/** 添加/更新数据 **/
//存boolean类型
kv.encode("bool", true);
//存int类型
kv.encode("int", Integer.MIN_VALUE);
//存string类型
kv.encode("string", "MyiSMMKV");


/** 获取数据 **/
//获取boolean类型数据
boolean bValue = kv.decodeBool("bool");
//获取int类型数据
int iValue = kv.decodeInt("int");
//获取string类型数据
String str = kv.decodeString("string");
//...等类型的获取

// 删除数据
mmkv.removeValueForKey(key);
```

---

### parseInt()

```java
int I = Integer.parseInt("123456");
```

把字符串转变成整形

---

### Build. VERSION. SDK_INT

代表的操作系统的版本号，谷歌的解释大致翻译如下当前在此硬件上运行的软件的SDK

---

### CharSequence

简单理解成，这就是一个 String 

CharSequence与String都能用于定义字符串，但CharSequence的值是可读可写序列，而String的值是只读序列。

---

### System.currentTimeMillis()

获取一个当前系统时间的时间戳

---

### ArrayList

ArrayList 类是一个可以动态修改的数组，与普通数组的区别就是它是没有固定大小的限制，我们可以添加或删除元素，类似于Python当中的列表

---

### Android中的RemoteViews

RemoteViews翻译过来就是远程视图.顾名思义,RemoteViews不是当前进程的View,是属于SystemServer进程

RemoteViews在Android中的使用场景有两种：通知栏和桌面小部件。

```java
private void showDefaultNotification() {
    NotificationCompat.Builder builder = new NotificationCompat.Builder(this);

    // 设置通知的基本信息：icon、标题、内容
    builder.setSmallIcon(R.mipmap.ic_launcher);
    builder.setContentTitle("My notification");
    builder.setContentText("Hello World!");
    builder.setAutoCancel(true);

    // 设置通知的点击行为：这里启动一个 Activity
    Intent intent = new Intent(this, SecondActivity.class);
    PendingIntent pendingIntent = PendingIntent.getActivity(this, 0, intent, PendingIntent.FLAG_UPDATE_CURRENT);
    builder.setContentIntent(pendingIntent);

    // 发送通知 id 需要在应用内唯一
    NotificationManager notificationManager = (NotificationManager) getSystemService(Context.NOTIFICATION_SERVICE);
    notificationManager.notify(id, builder.build());
}
```



自定义通知

```java
private void showCustomNotification() {

    RemoteViews remoteView;

    // 构建 remoteView
    remoteView = new RemoteViews(getPackageName(), R.layout.layout_notification);
    remoteView.setTextViewText(R.id.tvMsg, "哈shenhuniurou");
    remoteView.setImageViewResource(R.id.ivIcon, R.mipmap.ic_launcher_round);

    NotificationCompat.Builder builder = new NotificationCompat.Builder(this);

    // 设置自定义 RemoteViews
    builder.setContent(remoteView).setSmallIcon(R.mipmap.ic_launcher);

    // 设置通知的优先级(悬浮通知)
    builder.setPriority(NotificationCompat.PRIORITY_MAX);
    Uri alarmSound = RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION);
    // 设置通知的提示音
    builder.setSound(alarmSound);


    // 设置通知的点击行为：这里启动一个 Activity
    Intent intent = new Intent(this, SecondActivity.class);
    PendingIntent pendingIntent = PendingIntent.getActivity(this, 0, intent, PendingIntent.FLAG_UPDATE_CURRENT);
    builder.setContentIntent(pendingIntent);
    builder.setAutoCancel(true);
    Notification notification = builder.build();

    NotificationManager notificationManager = (NotificationManager) getSystemService(Context.NOTIFICATION_SERVICE);
    notificationManager.notify(1001, notification);
}
```





* setTextViewText(viewId, text) 设置文本
* setTextColor(viewId, color)           设置文本颜色
* setTextViewTextSize(viewId, units, size)     设置文本大小
* setImageViewBitmap(viewId, bitmap)        设置图片
* setImageViewResource(viewId, srcId)       根据图片资源设置图片
* setViewPadding(viewId,left, top,right, bottom) 设置Padding间距
* setOnClickPendingIntent(viewId, pendingIntent)  设置点击事件，表示的是点击 viewId 这标签的按钮，会触发后面的 pendingIntent 

---

### Intent

Intent 是 Android 非常常用的一个用于组件间互相通信的信息对象，常用于启动组件和传递数据

Intent传送数据是以键值对的形式，主要通过`putExtra()`方法，该方法接收两个参数，第一个是数据的键,第二个是数据的值

​		

向目标Activity传递数据：

```java
Intent intent=new Intent(this,Main2Activity.class);
//可传递多种类型的数据
intent.putExtra("name","张三");
intent.putExtra("age",12);
startActivity(intent);
```

​			

在目标Activity中取出数据

```java
Intent intent=getIntent();
//用getXxxExtra()取出对应类型的数据。取出String只需要指定key
String name=intent.getStringExtra("name");
//取出int要指定key，还要设置默认值，当intent中没有该key对应的value时，返回设置的默认值
int age=intent.getIntExtra("age",0);
```

​		

Intent 的包含信息与构造

![5064136-90a90f76a05437fa](./assets/5064136-90a90f76a05437fa.png)

| 代码                                         | 描述                                                         |
| -------------------------------------------- | ------------------------------------------------------------ |
| Intent()                                     | 构造一个空 Intent                                            |
| Intent(String action)                        | 构造一个指定 action 的 Intent                                |
| Intent(String action，Uri uri)               | 构造一个指定 action 和 uri（相当于同时设定了 data）的 Intent |
| Intent(Context packageContext，Class<?> cls) | 构造一个指定目标组件的 Intent，显式 Intent 的主要构造方法    |

​			

| 代码                                            | 描述                                                        |
| ----------------------------------------------- | ----------------------------------------------------------- |
| setAction(String action)                        | 指定 action                                                 |
| setClass(Context packageContext, Class<?> cls)  | 制定目标组件类名                                            |
| setData(Uri data)                               | 设置 Data 的 uri                                            |
| setType(String type)                            | 设置 Data 的 MIME 类型                                      |
| setDataAndType(Uri data, String type)           | 同时设置 Data 的 uri 与 MIME 类型                           |
| addCategory(String category)                    | 添加一项 Category，Intent 可有多个 Category                 |
| addFlags(int flags)                             | 设置 Flag，决定目标组件的启动方式                           |
| putExtra(String name, 基本类型和序列化类 value) | 放入附加数据，参 2 可以是各种基本类型，及序列化后的自定义类 |
| putExtras(Bundle extras)                        | 把封装了数据信息的 Bundle 对象放入 Intent                   |

​			

#### Action

指 Intent 发向的组件的主要动作，比如：图片应用中主要动作为查看图片的组件、地图应用中主要动作为查看地址的组件。另外，对于广播（Broadcast）组件而言，Intent 的 action 则是指广播具体的值。当 Broadcast Receiver 接收到该值时代表了某事件已经发生。
通常使用的主要是 Android 系统内置 action，这些 action 实际上是保存在 Intent 类中的静态常量，系统的默认组件（如：默认浏览器、图片浏览器、拨号页面等）都可以响应相应的 action。下面给出几个比较常见内置 action。

**ACTION_VIEW**
向用户展示某信息，比如使用浏览器打开网址，用图片应用显示图片等

**ACTION_SEND**
用于发送数据，比如电子邮件应用或者一些社交应用。

**ACTION_DIAL**
显示带拨号盘的页面，让用户可以进行拨号动作。



**自定义action**， 供 Intent 在自己的应用内使用（或者供其他应用在自己的应用中调用组件）。如果定义自己的操作，请确保将应用的软件包名称作为前缀。 例如：

```java
static final String ACTION_TIMETRAVEL = "com.example.action.TIMETRAVEL";
```

​				

​				

#### Data

包含了 URI 对象和 memitype 两个部分，分别是待操作数据的引用 uri，以及待操作数据的数据类型。两部分均为可选，但是要注意同时设置时应该使用 `setDataAndType()`方法，防止互相抵消。
Data 内容一般由 action 决定，比如 action 为 ACTION_VIEW，那么 Data 就可以是一个网址，也可以是图片之类的数据 uri。
同时指定 Uri 和 MIME 类型有助于 Android 系统找到接收 Intent 的最佳组件，例如可以响应 ACTION_VIEW 的组件可能有非常多，浏览器、播放器、图片应用等等。此时设置`mimeType`为`"image/jpeg"`或者`video/mp4`，则系统可以筛选出更合适的响应组件。



#### Category

目标组件的类型信息字符串，一个 Intent 可以添加多个 Category 。以下是比较常见的 Category：

**CATEGORY_BROWSABLE**
目标 Activity 允许本身通过网络浏览器启动，以显示链接引用的数据，如图像或电子邮件。

**CATEGORY_LAUNCHER**
该 Activity 是任务的初始 Activity，在系统的应用启动器中列出。

需要注意的是大部分 Intent 虽然不需要设置 Category，但是在调用使用 Intent 的方法（如`starActivity（）`等）的时候，会默认为该 Intent 添加 CATEGORY_DEFAULT，相应目标组件的Intent过滤器应该添加该类别，具体会在下文 **2、Intent的用法** 中详述。

**以上 4 种（组件类名、Action、Data、Category）是会影响系统对 Intent 的解析从而决定最终启动那个组件的信息，以下两种（Extra、Flag）属于附加的信息，不影响系统解析启动那个组件**

​				

#### Extra

Intent 携带附加数据，也是组件间互相传递信息比较常见的做法。使用各种 `putExtra()`方法添加 extra 数据，每种方法均接受两个参数：键名和值。还可以创建一个包含所有 extra 数据的 Bundle 对象，然后使用 `putExtras()`将 Bundle 插入 Intent 中。
具体用法在下文 **3、数据传送** 中详述。

​					

#### Flag

指示 Android 系统如何启动 Activity，例如，Activity 应属于哪个任务，以及启动之后如何处理（例如，它是否属于最近的 Activity 列表）。

​					

#### Intent 构造示例：

```java
    Intent intent = new Intent(this,TagerActivity.class);//显式 Intent 构造示例

    //隐式Intent构造示例
    Intent intent=new Intent(Intent.ACTION_VIEW);//设定 action 为展示内容
    intent.setData(Uri.parse("http://www.baidu.com"));//设置 data 的 uri 为一个网址
    intent.addCategory(Intent.CATEGORY_LAUNCHER);//目标组件为某个应用的首页面
    intent.setFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);//目标 Activity 的启动方式为 single top
    intent.putExtra("extra_my","Tom");//附加 String 数据
```



---

### PendingIntent

PendingIntent可以看作是对Intent的一个封装，但它不是立刻执行某个行为，

而是满足某些条件或触发某些事件后才执行指定的行为。
