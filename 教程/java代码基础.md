## java代码基础

- [java代码基础](#java代码基础)
  - [static关键字](#static关键字)
    - [static关键字修饰方法](#static关键字修饰方法)
    - [static关键字修饰变量](#static关键字修饰变量)
    - [static静态代码块](#static静态代码块)
  - [构造函数](#构造函数)
  - [方法重写与方法重载](#方法重写与方法重载)
  - [接口](#接口)

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

