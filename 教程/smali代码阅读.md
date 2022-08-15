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
```



