## smali代码阅读

### 例子一

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
        System.loadLibrary("calc");
    }

    public MainActivity() {
        this.cnt = 0;
        this.handler = new Handler();
        this.showMessageTask = new Runnable() {
            @Override
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

    @Override  // android.view.View$OnClickListener
    public void onClick(View arg11) {
        if(this.flag == 1) {
            return;
        }

        this.flag = 1;
        ((TextView)this.findViewById(0x7F0C0052)).setText("");  // id:textView3
        TextView tv = (TextView)this.findViewById(0x7F0C0050);  // id:textView
        TextView tv2 = (TextView)this.findViewById(0x7F0C0051);  // id:textView2
        this.m = 0;
        this.n = new Random().nextInt(3);
        tv2.setText(new String[]{"CPU: Paper", "CPU: Rock", "CPU: Scissors"}[this.n]);
        if(arg11 == this.P) {
            tv.setText("YOU: Paper");
            this.m = 0;
        }

        if(arg11 == this.r) {
            tv.setText("YOU: Rock");
            this.m = 1;
        }

        if(arg11 == this.S) {
            tv.setText("YOU: Scissors");
            this.m = 2;
        }

        this.handler.postDelayed(this.showMessageTask, 1000L);
    }

    @Override  // android.app.Activity
    protected void onCreate(Bundle arg2) {
        super.onCreate(arg2);
        this.setContentView(0x7F040018);  // layout:activity_main
        this.P = (Button)this.findViewById(0x7F0C004D);  // id:button
        this.S = (Button)this.findViewById(0x7F0C004F);  // id:button3
        this.r = (Button)this.findViewById(0x7F0C004E);  // id:buttonR
        this.P.setOnClickListener(this);
        this.r.setOnClickListener(this);
        this.S.setOnClickListener(this);
        this.flag = 0;
    }
}
```

​      

```assembly
.class public MainActivity
.super Activity

.implements View$OnClickListener
```

`public class MainActivity extends Activity implements View.OnClickListener`      

格式：**.class 权限 关键字 类名**    

.class 表示的是声明类    public 表示的类的权限    MainActivity 表示的类名    

.super 表示的继承于 Activity    

.implements 表示的继承于 View.OnClickListener 这个接口    



```assembly
.field P:Button

.field S:Button

.field cnt:I

.field flag:I

.field private final handler:Handler

.field m:I

.field n:I

.field r:Button

.field private final showMessageTask:Runnable
```

```java
    Button P;
    Button S;
    int cnt;
    int flag;
    private final Handler handler;
    int m;
    int n;
    Button r;
    private final Runnable showMessageTask;
```

格式：**.field 权限 关键字 类属性名：数据类型 **   

.field 表示的是定义类属性     

`.field private final showMessageTask:Runnable` == ` private final Runnable showMessageTask;`     

​    

```smali
.method static constructor <clinit>()V
          .registers 1
00000000  const-string        v0, "calc"
00000004  invoke-static       System->loadLibrary(String)V, v0
0000000A  return-void
.end method.method static constructor <clinit>()V
          .registers 1
00000000  const-string        v0, "calc"
00000004  invoke-static       System->loadLibrary(String)V, v0
0000000A  return-void
.end method
```

```java
    static {
        System.loadLibrary("calc");
    }
```

`.method static constructor <clinit>()V`  表示的是静态代码块    

`.registers 1` 使用寄存器的个数     

`const-string        v0, "calc"` 给 $V_0$ 寄存器赋值 “calc”    

`invoke-static       System->loadLibrary(String)V, v0` 调用静态函数     

`.end method.method static constructor <clinit>()V` 静态代码块结束    

​    

```
.method public constructor <init>()V 
          .registers 2
00000000  invoke-direct       Activity-><init>()V, p0
00000006  const/4             v0, 0
00000008  iput                v0, p0, MainActivity->cnt:I
0000000C  new-instance        v0, Handler
00000010  invoke-direct       Handler-><init>()V, v0
00000016  iput-object         v0, p0, MainActivity->handler:Handler
0000001A  new-instance        v0, MainActivity$1
0000001E  invoke-direct       MainActivity$1-><init>(MainActivity)V, v0, p0
00000024  iput-object         v0, p0, MainActivity->showMessageTask:Runnable
00000028  return-void
.end method
```

```java
     public MainActivity() {
        this.cnt = 0;
        this.handler = new Handler();
        this.showMessageTask = new Runnable() {
            @Override
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

`.method public constructor <init>()V` 表示的是定义一个构造函数，构造函数和类名同名

`          .registers 2` 申请两个寄存器		

`invoke-direct       Activity-><init>()V, p0` 这个是和构造函数一起配对使用的，它和`.method public constructor <init>()V` 共同构成构造函数		

`const/4             v0, 0` 给 $V_0$ 寄存器一个值（0）		

`iput                v0, p0, MainActivity->cnt:I` iput 赋值操作，用于将 int 类型的数据赋值给后面的对象 P0.cnt 也就是this.cnt 		

`new-instance        v0, Handler` 新建一个对象，Handler 并且存入 $V_0$ 急促请你当中		

`invoke-direct       Handler-><init>()V, v0` 初始化该对象的构造函数，

```assembly
0000001A  new-instance        v0, MainActivity$1
0000001E  invoke-direct       MainActivity$1-><init>(MainActivity)V, v0, p0
00000024  iput-object         v0, p0, MainActivity->showMessageTask:Runnable
```

`MainActivity$1` 表示的是一个内部类，新建一个内部类的对象，并且将它存储在 $V_0$ 寄存器当中，`new MainActivity.1()`  			

并且利用这个构造函数对他进行初始化，最后将这个赋值给 Runnable 类型的 `this.showMessageTask` 			

所以完整应该是，`Runnable this.showMessageTask = new  MainActivity.1()`  			

`return-void`  函数返回 void 

​				

```assembly
.end method

.method public native calc()I
.end method
```

`public native int calc(){}`			

​			

```assembly
.method public onClick(View)V
          .registers 12
00000000  const/4             v9, 3
00000002  const/4             v8, 2
00000004  const/4             v7, 0
00000006  const/4             v6, 1
00000008  iget                v5, p0, MainActivity->flag:I
0000000C  if-ne               v5, v6, :12
:10
00000010  return-void
:12
00000012  iput                v6, p0, MainActivity->flag:I
00000016  const               v5, 0x7F0C0052  # id:textView3
0000001C  invoke-virtual      MainActivity->findViewById(I)View, p0, v5
00000022  move-result-object  v4
00000024  check-cast          v4, TextView
00000028  const-string        v5, ""
0000002C  invoke-virtual      TextView->setText(CharSequence)V, v4, v5
00000032  const               v5, 0x7F0C0050  # id:textView
00000038  invoke-virtual      MainActivity->findViewById(I)View, p0, v5
0000003E  move-result-object  v2
00000040  check-cast          v2, TextView
00000044  const               v5, 0x7F0C0051  # id:textView2
0000004A  invoke-virtual      MainActivity->findViewById(I)View, p0, v5
00000050  move-result-object  v3
00000052  check-cast          v3, TextView
00000056  iput                v7, p0, MainActivity->m:I
0000005A  new-instance        v0, Random
0000005E  invoke-direct       Random-><init>()V, v0
00000064  invoke-virtual      Random->nextInt(I)I, v0, v9
0000006A  move-result         v5
0000006C  iput                v5, p0, MainActivity->n:I
00000070  new-array           v1, v9, [String
00000074  const-string        v5, "CPU: Paper"
00000078  aput-object         v5, v1, v7
0000007C  const-string        v5, "CPU: Rock"
00000080  aput-object         v5, v1, v6
00000084  const-string        v5, "CPU: Scissors"
00000088  aput-object         v5, v1, v8
0000008C  iget                v5, p0, MainActivity->n:I
00000090  aget-object         v5, v1, v5
00000094  invoke-virtual      TextView->setText(CharSequence)V, v3, v5
0000009A  iget-object         v5, p0, MainActivity->P:Button
0000009E  if-ne               p1, v5, :B0
:A2
000000A2  const-string        v5, "YOU: Paper"
000000A6  invoke-virtual      TextView->setText(CharSequence)V, v2, v5
000000AC  iput                v7, p0, MainActivity->m:I
:B0
000000B0  iget-object         v5, p0, MainActivity->r:Button
000000B4  if-ne               p1, v5, :C6
:B8
000000B8  const-string        v5, "YOU: Rock"
000000BC  invoke-virtual      TextView->setText(CharSequence)V, v2, v5
000000C2  iput                v6, p0, MainActivity->m:I
:C6
000000C6  iget-object         v5, p0, MainActivity->S:Button
000000CA  if-ne               p1, v5, :DC
:CE
000000CE  const-string        v5, "YOU: Scissors"
000000D2  invoke-virtual      TextView->setText(CharSequence)V, v2, v5
000000D8  iput                v8, p0, MainActivity->m:I
:DC
000000DC  iget-object         v5, p0, MainActivity->handler:Handler
000000E0  iget-object         v6, p0, MainActivity->showMessageTask:Runnable
000000E4  const-wide/16       v8, 1000
000000E8  invoke-virtual      Handler->postDelayed(Runnable, J)Z, v5, v6, v8, v9
000000EE  goto                :10
.end method
```

```java
    @Override  // android.view.View$OnClickListener
    public void onClick(View arg11) {
        if(this.flag == 1) {
            return;
        }

        this.flag = 1;
        ((TextView)this.findViewById(0x7F0C0052)).setText("");  // id:textView3
        TextView tv = (TextView)this.findViewById(0x7F0C0050);  // id:textView
        TextView tv2 = (TextView)this.findViewById(0x7F0C0051);  // id:textView2
        this.m = 0;
        this.n = new Random().nextInt(3);
        tv2.setText(new String[]{"CPU: Paper", "CPU: Rock", "CPU: Scissors"}[this.n]);
        if(arg11 == this.P) {
            tv.setText("YOU: Paper");
            this.m = 0;
        }

        if(arg11 == this.r) {
            tv.setText("YOU: Rock");
            this.m = 1;
        }

        if(arg11 == this.S) {
            tv.setText("YOU: Scissors");
            this.m = 2;
        }

        this.handler.postDelayed(this.showMessageTask, 1000L);
    }
```

​		

---

### 例子二

```java
    public void onClick(View arg11) {
        if(this.flag == 1) {
            return;
        }

        this.flag = 1;
        ((TextView)this.findViewById(0x7F0C0052)).setText("");  // id:textView3
        TextView tv = (TextView)this.findViewById(0x7F0C0050);  // id:textView
        TextView tv2 = (TextView)this.findViewById(0x7F0C0051);  // id:textView2
        this.m = 0;
        this.n = new Random().nextInt(3);
        tv2.setText(new String[]{"CPU: Paper", "CPU: Rock", "CPU: Scissors"}[this.n]);
        if(arg11 == this.P) {
            tv.setText("YOU: Paper");
            this.m = 0;
        }

        if(arg11 == this.r) {
            tv.setText("YOU: Rock");
            this.m = 1;
        }

        if(arg11 == this.S) {
            tv.setText("YOU: Scissors");
            this.m = 2;
        }

        this.handler.postDelayed(this.showMessageTask, 1000L);
    }
```

```assembly
.method public onClick(View)V
          .registers 12
00000000  const/4             v9, 3
00000002  const/4             v8, 2
00000004  const/4             v7, 0
00000006  const/4             v6, 1
00000008  iget                v5, p0, MainActivity->flag:I
0000000C  if-ne               v5, v6, :12
:10
00000010  return-void
:12
00000012  iput                v6, p0, MainActivity->flag:I
00000016  const               v5, 0x7F0C0052  # id:textView3
0000001C  invoke-virtual      MainActivity->findViewById(I)View, p0, v5
00000022  move-result-object  v4
00000024  check-cast          v4, TextView
00000028  const-string        v5, ""
0000002C  invoke-virtual      TextView->setText(CharSequence)V, v4, v5
00000032  const               v5, 0x7F0C0050  # id:textView
00000038  invoke-virtual      MainActivity->findViewById(I)View, p0, v5
0000003E  move-result-object  v2
00000040  check-cast          v2, TextView
00000044  const               v5, 0x7F0C0051  # id:textView2
0000004A  invoke-virtual      MainActivity->findViewById(I)View, p0, v5
00000050  move-result-object  v3
00000052  check-cast          v3, TextView
00000056  iput                v7, p0, MainActivity->m:I
0000005A  new-instance        v0, Random
0000005E  invoke-direct       Random-><init>()V, v0
00000064  invoke-virtual      Random->nextInt(I)I, v0, v9
0000006A  move-result         v5
0000006C  iput                v5, p0, MainActivity->n:I
00000070  new-array           v1, v9, [String
00000074  const-string        v5, "CPU: Paper"
00000078  aput-object         v5, v1, v7
0000007C  const-string        v5, "CPU: Rock"
00000080  aput-object         v5, v1, v6
00000084  const-string        v5, "CPU: Scissors"
00000088  aput-object         v5, v1, v8
0000008C  iget                v5, p0, MainActivity->n:I
00000090  aget-object         v5, v1, v5
00000094  invoke-virtual      TextView->setText(CharSequence)V, v3, v5
0000009A  iget-object         v5, p0, MainActivity->P:Button
0000009E  if-ne               p1, v5, :B0
:A2
000000A2  const-string        v5, "YOU: Paper"
000000A6  invoke-virtual      TextView->setText(CharSequence)V, v2, v5
000000AC  iput                v7, p0, MainActivity->m:I
:B0
000000B0  iget-object         v5, p0, MainActivity->r:Button
000000B4  if-ne               p1, v5, :C6
:B8
000000B8  const-string        v5, "YOU: Rock"
000000BC  invoke-virtual      TextView->setText(CharSequence)V, v2, v5
000000C2  iput                v6, p0, MainActivity->m:I
:C6
000000C6  iget-object         v5, p0, MainActivity->S:Button
000000CA  if-ne               p1, v5, :DC
:CE
000000CE  const-string        v5, "YOU: Scissors"
000000D2  invoke-virtual      TextView->setText(CharSequence)V, v2, v5
000000D8  iput                v8, p0, MainActivity->m:I
:DC
000000DC  iget-object         v5, p0, MainActivity->handler:Handler
000000E0  iget-object         v6, p0, MainActivity->showMessageTask:Runnable
000000E4  const-wide/16       v8, 1000
000000E8  invoke-virtual      Handler->postDelayed(Runnable, J)Z, v5, v6, v8, v9
000000EE  goto                :10
.end method
```



```assembly
.method public onClick(View)V
          .registers 12
00000000  const/4             v9, 3
00000002  const/4             v8, 2
00000004  const/4             v7, 0
00000006  const/4             v6, 1
00000008  iget                v5, p0, MainActivity->flag:I
0000000C  if-ne               v5, v6, :12
```

```java
public void onClick(view arg1){
    if(this.flag != 1)
    {
        goto:12
    }
    else
    {
        ...
    }
}
```

将数字 3 赋值给 $V_9$ 寄存器		

将数字 2 赋值给 $V_8$ 寄存器		

将数字 0 赋值给 $V_7$ 寄存器		

将数字 1 赋值给 $V_6$ 寄存器		

将 this.flag 存放在 $V_5$ 寄存器当中		

如果 $V_5$ 和 $V_6$ 寄存器不相等，则跳转到 标号为 12 的代码块			

​			

```assembly
00000012  iput                v6, p0, MainActivity->flag:I
```

```java
this.flag = 1
```

将 $V_6$ 寄存器的值给到 $P_0$.flag（this.flag） 中		



```assembly
00000016  const               v5, 0x7F0C0052  # id:textView3
0000001C  invoke-virtual      MainActivity->findViewById(I)View, p0, v5 
00000022  move-result-object  v4
00000024  check-cast          v4, TextView 
00000028  const-string        v5, ""
0000002C  invoke-virtual      TextView->setText(CharSequence)V, v4, v5
```



将 0x7F0C0052 内容存储在 $V_5$ 寄存器当中				

`this.findViewById(0x7F0C0052)` 并且将这个结果存放在 $V_4$ 寄存器当中，将这个结果强制类型转换成 TextView，写作 `(TextView)this.findViewById(0x7F0C0052)`			

将 `“”` 内容赋值给 $V_5$ 			

`((TextView)this.findViewById(0x7F0C0052)).setText(“”)` 并且他的返回值是 void 所以就写成这个样子		

```assembly
00000032  const               v5, 0x7F0C0050  # id:textView
00000038  invoke-virtual      MainActivity->findViewById(I)View, p0, v5
0000003E  move-result-object  v2
00000040  check-cast          v2, TextView
```

`TextView v2 = (TextView)this.findViewById(0x7F0C0050)` 

​			

```assembly
00000044  const               v5, 0x7F0C0051  # id:textView2
0000004A  invoke-virtual      MainActivity->findViewById(I)View, p0, v5
00000050  move-result-object  v3
00000052  check-cast          v3, TextView
```

```java
TextView v3 = (TextView)this.findViewById(0x7F0C0051)
```

​			

```assembly
00000056  iput                v7, p0, MainActivity->m:I
```

```java
this.m = 0
```

​			

```assembly
0000005A  new-instance        v0, Random
0000005E  invoke-direct       Random-><init>()V, v0
00000064  invoke-virtual      Random->nextInt(I)I, v0, v9
0000006A  move-result         v5
0000006C  iput                v5, p0, MainActivity->n:I
```

```java
this.n = new random.nextInt(3)
```

新建一个对象，`new random` 并且存储在 $V_5$ 寄存器当中，调用该对象的构造函数，对该对象进行初始化			

`this.n = new random.nextInt(3)` 		

​			

```assembly
00000070  new-array           v1, v9, [String
00000074  const-string        v5, "CPU: Paper"
00000078  aput-object         v5, v1, v7
0000007C  const-string        v5, "CPU: Rock"
00000080  aput-object         v5, v1, v6
00000084  const-string        v5, "CPU: Scissors"
00000088  aput-object         v5, v1, v8
0000008C  iget                v5, p0, MainActivity->n:I
00000090  aget-object         v5, v1, v5
```

```java
new String[]{"CPU: Paper", "CPU: Rock", "CPU: Scissors"}[this.n]
```

新建一个列表，类型是 string 长度是 $V_9$ ，列表存放在寄存器 $V_1$ 当中

将 $V_5$ 寄存器的内容放在  $V_1$ 当中，并且地址是 $V_7$ 			

`iget                v5, p0, MainActivity->n:I` 将 `this.n` 的内容赋值给 $V_5$ 寄存器			

`aget-object         v5, v1, v5` 取 $V_1$ 列表当中的，地址为 `this.n`  的元素，并将他赋值给 $V_5$

​			

```assembly
00000094  invoke-virtual      TextView->setText(CharSequence)V, v3, v5
```

```java
tv2.setText(new String[]{"CPU: Paper", "CPU: Rock", "CPU: Scissors"}[this.n]);
```

​		

```assembly
0000009A  iget-object         v5, p0, MainActivity->P:Button
0000009E  if-ne               p1, v5, :B0
```

```JAVA
if(this.p != arg)
{
    goto:B0
}
else
{
    ...
}
```

​		

```assembly
000000A2  const-string        v5, "YOU: Paper"
000000A6  invoke-virtual      TextView->setText(CharSequence)V, v2, v5
000000AC  iput                v7, p0, MainActivity->m:I
```

```java
v	2.setText("YOU: Paper");
this.m = 0;
```

​		

```assembly
000000B0  iget-object         v5, p0, MainActivity->r:Button
000000B4  if-ne               p1, v5, :C6
```

```java
if(arg11 != this.r){
    goto:C6
}
else
{
    ...
}
```

​			

```assembly
000000B8  const-string        v5, "YOU: Rock"
000000BC  invoke-virtual      TextView->setText(CharSequence)V, v2, v5
000000C2  iput                v6, p0, MainActivity->m:I
```

```java
v2.setText("YOU: Rock");
this.m = 1;
```

​		

```assembly
000000C6  iget-object         v5, p0, MainActivity->S:Button
000000CA  if-ne               p1, v5, :DC
```

```java
if(arg11 != this.S)
{
    goto:DC
}
else
{
    ...
}
```

​		

```assembly
000000CE  const-string        v5, "YOU: Scissors"
000000D2  invoke-virtual      TextView->setText(CharSequence)V, v2, v5
000000D8  iput                v8, p0, MainActivity->m:I
```

```java
tv.setText("YOU: Scissors");
this.m = 2;
```

​			

```assembly
000000DC  iget-object         v5, p0, MainActivity->handler:Handler
000000E0  iget-object         v6, p0, MainActivity->showMessageTask:Runnable
000000E4  const-wide/16       v8, 1000
000000E8  invoke-virtual      Handler->postDelayed(Runnable, J)Z, v5, v6, v8, v9
000000EE  goto                :10
```

```java
this.handler.postDelayed(this.showMessageTask, 1000L);
```

因为这里的第二个参数是 long 数据类型，所以，是两个寄存器存储数据

