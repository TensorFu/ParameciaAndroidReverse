## java代码基础



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

