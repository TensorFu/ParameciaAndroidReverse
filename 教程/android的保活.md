「保活」基本上是两条路：

- 提升自己进程的优先级，让系统不要轻易弄死自己；
- App 之间互相结盟，一个兄弟死了其他兄弟把它拉起来。



一般来说，系统杀进程有两种方法，这两个方法都通过 ActivityManagerService 提供：

- killBackgroundProcesses（系统一般是用的）
- forceStopPackage（用户一般用这个）但是国内的厂商和三星也是用的这个方式杀的进程，更加稳定和彻底



https://juejin.cn/post/7003992225575075876

https://cloud.tencent.com/developer/article/1784046

http://www.520monkey.com/archives/1303



开启前台Service（效果好，推荐） 

Service中循环播放一段无声音频（效果较好，但耗电量高，谨慎使用） 

双进程守护（Android 5.0前有效） 

JobScheduler（Android 5.0后引入，8.0后失效）

1 像素activity保活方案（不推荐） 

广播锁屏、自定义锁屏（不推荐） 

第三方推送SDK唤醒（效果好，缺点是第三方接入）

---

[双进程守护+Jobshcedule 保活](https://developer.aliyun.com/article/863811?spm=a2c6h.14164896.0.0.4dbe59bb5PyOhA)

[保活方案-知乎](https://zhuanlan.zhihu.com/p/79324310)

[NDK 轮询实现保活](https://cloud.tencent.com/developer/article/1655131)

---

### 【Android 进程保活】应用进程拉活-账户同步拉活

账户同步的作用 : 如果应用的数据发生了改变 , 可以通过账户进行同步 , 进而与服务器进行数据同步操作 , 执行同步时 , 系统会拉活对应的应用进程 ;			

进程拉活只是账户同步的附带作用 ;			

账户同步需要在 账户同步服务 Service 中进行 , 定义一个 Service 进行账户同步 , 其 onBind 方法必须返回 AbstractThreadedSyncAdapter 的 getSyncAdapterBinder() 值 ;				

账户同步需要自定义一个 AbstractThreadedSyncAdapter 类 , 并在 Service 中维护一个该类对象 ;

```java
class ThreadSyncAdapter extends AbstractThreadedSyncAdapter{
        public ThreadSyncAdapter(Context context, boolean autoInitialize) {
            super(context, autoInitialize);
        }
        public ThreadSyncAdapter(Context context, boolean autoInitialize,
                                 boolean allowParallelSyncs) {
            super(context, autoInitialize, allowParallelSyncs);
        }
        @Override
        public void onPerformSync(Account account, Bundle extras, String authority,
                                  ContentProviderClient provider, SyncResult syncResult) {
            // 账户同步操作
            // 与数据库 , 服务器同步操作 , 这里只是为了应用进程拉活 , 不实现具体的逻辑
        }
    }
```

---

## 应用拉活进程-账户同步拉活

[【Android 进程保活】应用进程拉活 ( 账户同步拉活 | 账户同步 | 源码资源 )（一）](https://developer.aliyun.com/article/863808?spm=a2c6h.14164896.0.0.84c859bbFaVtRy)

[【Android 进程保活】应用进程拉活 ( 账户同步拉活 | 账户同步 | 源码资源 )（二）](https://developer.aliyun.com/article/863809?spm=a2c6h.14164896.0.0.19056252WOIdUn)

这是通过，账户同步数据的方式进行，拉起，然后实现保活

找到了 AbstractThreadedSyncAdapter 类 的子类，

有 onPerformSync 函数 是系统在执行同步时执行的函数

```java
public class InfoService extends Service {

    /* renamed from: designated  reason: collision with root package name */
    public dating f11620designated;

    /* loaded from: classes3.dex */
    public class dating extends AbstractThreadedSyncAdapter {
        public dating(Context context) {
            super(context, true);
        }

        @Override // android.content.AbstractThreadedSyncAdapter
        public final void onPerformSync(Account account, Bundle bundle, String str, ContentProviderClient contentProviderClient, SyncResult syncResult) {
            uni.dating datingVar = acre.f13524tied;
            if (datingVar != null) {
                datingVar.f14580dating.startKeepService();
            }
        }
    }

    @Override // android.app.Service
    public final IBinder onBind(Intent intent) {
        return this.f11620designated.getSyncAdapterBinder();
    }

    @Override // android.app.Service
    public final void onCreate() {
        super.onCreate();
        this.f11620designated = new dating(getApplicationContext());
    }
}
```





在 xml 文件当中找到了 注册的该 Service 的区块				

还有 meta-data  -> ContentProvider 与 同步 Service 进行关联 			

账户同步的相关资源数据   up			

```xml
 <service android:name="io.github.crius.dae.auth.InfoService" android:enabled="true" android:exported="true">
            <intent-filter>
                <action android:name="android.content.SyncAdapter"/>
            </intent-filter>
            <meta-data android:name="android.content.SyncAdapter" android:resource="@xml/up"/>
        </service>
```



在 xml/up.xml 文件当中

```xml
<?xml version="1.0" encoding="utf-8"?>
<sync-adapter xmlns:android="http://schemas.android.com/apk/res/android" android:accountType="com.superclean.booster.accounttype" android:contentAuthority="com.superclean.booster_provider" android:userVisible="true" android:supportsUploading="false" android:allowParallelSyncs="false" android:isAlwaysSyncable="true"/>
```

android:contentAuthority 属性就是指定的该 ContentProvider ："com.superclean.booster_provider"			

android:accountType 就是账户类型

android:isAlwaysSyncable 属性 , 表示该账户同步操作 , 是否总是同步 , 这里设置 true , 账户拉活 , 越频繁越好	

android:userVisible 属性 , 表示是否在 " 设置 -> 账号 " 界面 , 展示一个账户同步开关 , 这里选择 false , 不给用户展示 , 万一用户给关了 , 就无法进行账户拉活应用进程操作（但是ultra cleaner 设置的 可见）			

​			

创建 ContentProvider , 然后在清单文件中注册			

其中 provider 标签的 android:authorities 就是上述 sync-adapter 标签中的 android:contentAuthority 属性值：com.superclean.booster_provider			

```xml
<provider android:name="io.github.crius.dae.auth.FreshInfoProvicer" android:exported="false" android:authorities="com.superclean.booster_provider" android:syncable="true"/>
```

​			

根据教程最后

通过 调用 ContentResolver 的 setIsSyncable 方法 , 设置账户同步开启 

调用 ContentResolver 的 setSyncAutomatically 方法 , 设置账户自动同步 , 注意 : 该操作需要权限 android.permission.WRITE_SYNC_SETTINGS （这个权限在 manifest.xml 当中找到了）

调用 ContentResolver 的 setSyncAutomatically 方法 , 设置账户自动同步 , 最后一个参数是同步周期 , 这个值只是参考值

​		

但是在代码部分 **没有找到**

setIsSyncable 函数

setSyncAutomatically 函数

addPeriodicSync 函数

---

## Android 进程保活】应用进程拉活 ( 应用进程拉活简介 | 广播拉活 | 显示广播与隐式广播 | 全家桶拉活 )

[【Android 进程保活】应用进程拉活 ( 应用进程拉活简介 | 广播拉活 | 显示广播与隐式广播 | 全家桶拉活 )](https://developer.aliyun.com/article/863802?spm=a2c6h.14164896.0.0.763962521zPATr)

只要进行进程拉活 , 都会或多或少占用系统的资源 , 尤其是内存资源 , 因此 Android 官方对这种操作进行了各种限制 , 从 Android 7.0 开始限制 , 到 Android 8.0 之后 , 基本无法进行应用拉活操作 ;			

二、 广播拉活

监听系统的广播事件 , 系统在发生特定事件时 , 发出对应事件广播 ;			

在 AndroidManifest.xml 中 静态注册 的广播接收者可以接受系统发出的广播 , 监听这些广播 , 然后由系统自动拉活广播接收者所在的应用进程 ;			

Android 8.0 ( API Level 26 ) 限制更严格 , 基本就禁止了这种做法 ; 在该版本及以后的版本中无法在 AndroidManifest.xml 清单文件中注册接收隐式广播的广播接收者			

特例：

ACTION_LOCKED_BOOT_COMPLETED

ACTION_BOOT_COMPLETED 开机广播 , ACTION_USER_INITIALIZE 用户账户添加广播 , ACTION_LOCALE_CHANGED 时间区域改变广播 				

这些隐式广播发出来的情况很特殊 , 有可能一天也发不出一条广播 , 用于拉活应用进程不太合适 

---

## 应用进程拉活 ( 双进程守护保活 )

[【Android 进程保活】应用进程拉活 ( 双进程守护保活 )](https://blog.csdn.net/shulianghan/article/details/115604667)					

" 远程前台进程 " 与 " 本地前台进程 " 实现了相同的功能 , 代码基本一致 , 这两个进程都是前台进程 , 都进行了提权 , 并且互相绑定 , 当监听到绑定的另外一个进程突然断开连接 , 则本进程再次开启前台进程提权 , 并且重新绑定对方进程 , 以达到拉活对方进程的目的 ;
					

这两个进程之间需要绑定，每个服务中都需要定义继承 IMyAidlInterface.Stub 的 Binder 类

但是		

没有找到 IMyAidlInterface.Stub，搜索的方式：IMyAidlInterface.Stub				



未完 。。。。





---

## 应用进程拉活 双进程守护+JobScheduler

[【Android 进程保活】应用进程拉活 ( 双进程守护 + JobScheduler 保活 | 成功率最高 | 推荐使用 )（一)](https://developer.aliyun.com/article/863811?spm=a2c6h.14164896.0.0.3513403aUKWlu5)    

[【Android 进程保活】应用进程拉活 ( 双进程守护 + JobScheduler 保活 | 成功率最高 | 推荐使用 )（二) ](https://developer.aliyun.com/article/863812?spm=a2c6h.14164896.0.0.3513403aUKWlu5)    

[【Android 进程保活】应用进程拉活 ( 双进程守护 + JobScheduler 保活 | 成功率最高 | 推荐使用 )（三)](https://developer.aliyun.com/article/863813?spm=a2c6h.14164896.0.0.3513403aUKWlu5)    

​			

在 JobService 的 onStartJob 方法中 , 判定 " 双进程守护保活 " 中的双进程是否挂了 , 如果这两个进程挂了 , 就重新将挂掉的进程重启 ;

​			



未完 。。。

---

提高进程优先级

开机之后能够自启动软件，oom_adj 的值是 3

当打开的时候软件的 oom_adj = 0 

切换后台的时候，oom_adj 3

手动关闭软件之后还是 3

可能是通过 3 的优先级，进行保活（但是感觉这个优先级也不是很高）也可能没有用优先级保活，

分析：没有采用 一个像素 activity 的保活策略			

​				

----

## 提升进程优先级（1 像素 Activity 提高进程优先级）

[【Android 进程保活】提升进程优先级 ( 1 像素 Activity 提高进程优先级 | taskAffinity 亲和性说明 | 运行效果 | 源码资源 )	](https://hanshuliang.blog.csdn.net/article/details/115482010)	

实现原理：

使用 Activity 可以提升进程的 oom_adj 值

APP 进入后台后 , 使用 BroadcastReceiver 广播接收者 , 监听 Android 系统的锁屏广播事件		

屏幕锁定 : 启动只有 1 像素的透明 Activity 界面 ;
屏幕解锁 : 退出上述 1 像素的透明 Activity 界面 ;

​		

实现步骤：

1. 注册一个 广播接受者
2. 设置成一个像素的 activity 
3. 监听 android.intent.action.SCREEN_ON 和 android.intent.action.SCREEN_OFF , 两个广播 , 再锁屏时启动 1 像素 Activity , 在解除锁屏时 , 关闭 1 像素 Activity 
4. 新建管理类，该管理类负责 Activity 组件与 BroadcastReceiver 组件的耦合，在里面实现，注册广播和接触注册广播，开启activity 界面和关闭activity界面。
5. Androidmanifest.xml 文件配置，配置 1 像素 Activity 的亲和性设置 , 不要把这个 Activity 放在与主 Activity 相同的任务栈中 , 否则在解除锁定时 , 会拉起后台的无关任务栈 ，不要把 1 像素 Activity 展示到用户眼前 , 对用户透明即可
   1. 通过 android:excludeFromRecents="true" 将该 activity 组件在最近任务当中不可见
   2. 通过 android:taskAffinity="kim.hsl.keep_progress_alive.onepixel" />  设置 Activity 亲和性，让该界面在一个独立的任务栈中 , 不要与本应用的其它任务栈放在一起避免解除锁屏后 , 关闭 1 像素界面 , 将整个任务栈都唤醒
   3. 设置透明主题，保证一个像素的 activity 是完全透明的

​			

分析：

1. 准备通过 android.intent.action.SCREEN_ON 找到，app 在关屏之后，打开一个 activity 的代码，但是，在代码当中，接受了关屏广播之后没有发现，有通过 startActivity() 打开Activity 的代码。
2. 在 Androidmanifest.xml 文件当中找到 android:excludeFromRecents="true" 其对应的，Activity ：io.github.crius.dae.HoActivity

io.github.crius.dae.HoActivity 代码

```java
public class HoActivity extends AppCompatActivity {
    @Override // android.app.Activity
    public void onCreate(Bundle bundle, PersistableBundle persistableBundle) {
        super.onCreate(bundle, persistableBundle);
        Window window = getWindow();
        window.setGravity(8388659);
        WindowManager.LayoutParams attributes = window.getAttributes();
        attributes.x = 0;
        attributes.y = 0;
        attributes.height = 1;
        attributes.width = 1;
        window.setAttributes(attributes);
    }

    @Override // androidx.fragment.app.FragmentActivity, android.app.Activity
    public void onResume() {
        super.onResume();
        try {
            if (((PowerManager) getApplicationContext().getSystemService("power")).isScreenOn()) {
                finish();
                return;
            }
            dating datingVar = acre.f13524tied;
            if (datingVar == null) {
                return;
            }
            datingVar.f14580dating.startKeepService();
        } catch (Exception unused) {
            finish();
        }
    }
}
```

​			

开启这个 Activity 的管理类，在 com.superclean.booster.notification.services.BackupWorker 

run 函数代码

```java
public final void run() {
            try {
                Intent intent = new Intent(BackupWorker.this.f9074dating, HoActivity.class);
                intent.addFlags(268435456);
                BackupWorker.this.f9074dating.startActivity(intent);
              
                Intent intent2 = new Intent(BackupWorker.this.f9074dating, KeepService.class);
                if (Build.VERSION.SDK_INT >= 26) {
                    BackupWorker.this.f9074dating.startForegroundService(intent2);
                } else {
                    BackupWorker.this.f9074dating.startService(intent2);
                }
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
```

BackupWorker.this.f9074dating.startActivity(intent); 打开一个像素的保活			

​		

---

## 提升进程优先级-使用前台 Service

[【Android 进程保活】提升进程优先级 ( 使用前台 Service 提高应用进程优先级 | 效果展示 | 源码资源 )（一）](https://developer.aliyun.com/article/863800)

实现原理：

前台进程中除了前台显示的 Activity 之外 , 还有前台服务 , 即调用 startForeground 方法启动的服务 ;

按下 Home 键后 , 通过前台服务 , 让后台进程仍然是前台进程 ;			

​			



















