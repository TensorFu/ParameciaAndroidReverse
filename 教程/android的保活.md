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



---

## 应用进程拉活 双进程守护+JobScheduler

[【Android 进程保活】应用进程拉活 ( 双进程守护 + JobScheduler 保活 | 成功率最高 | 推荐使用 )（一)](https://developer.aliyun.com/article/863811?spm=a2c6h.14164896.0.0.3513403aUKWlu5)    

[【Android 进程保活】应用进程拉活 ( 双进程守护 + JobScheduler 保活 | 成功率最高 | 推荐使用 )（二) ](https://developer.aliyun.com/article/863812?spm=a2c6h.14164896.0.0.3513403aUKWlu5)    

[【Android 进程保活】应用进程拉活 ( 双进程守护 + JobScheduler 保活 | 成功率最高 | 推荐使用 )（三)](https://developer.aliyun.com/article/863813?spm=a2c6h.14164896.0.0.3513403aUKWlu5)    

​			

在 JobService 的 onStartJob 方法中 , 判定 " 双进程守护保活 " 中的双进程是否挂了 , 如果这两个进程挂了 , 就重新将挂掉的进程重启 ;





















