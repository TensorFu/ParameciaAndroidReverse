[TOC]

```java
import com.appsflyer.AppsFlyerConversionListener;
import com.appsflyer.AppsFlyerLib;
/**
  * 创建人：SCC
  * 功能描述：AppsFlyer接入
  */
public class MyApp extends Application {
    private static MyApp singleton;

    @Override
    public void onCreate() {
        super.onCreate();
        AppsFlyerConversionListener conversionListener = new AppsFlyerConversionListener() {
            @Override
            public void onConversionDataSuccess(Map<String, Object> conversionData) {
                for (String attrName : conversionData.keySet()) {
                    MLog.e("attribute: " + attrName + " = " + conversionData.get(attrName));
                }
            }
            @Override
            public void onConversionDataFail(String errorMessage) {
                MLog.e( "error getting conversion data: " + errorMessage);
            }
            @Override
            public void onAppOpenAttribution(Map<String, String> conversionData) {
                for (String attrName : conversionData.keySet()) {
                    MLog.e("attribute: " + attrName + " = " + conversionData.get(attrName));
                }
            }
            @Override
            public void onAttributionFailure(String errorMessage) {
                MLog.e("error onAttributionFailure : " + errorMessage);
            }
        };
        AppsFlyerLib.getInstance().init("你的开发密钥", conversionListener, getApplicationContext());
        AppsFlyerLib.getInstance().start(this);
    }
}
```



### 权限配置

#### 【必选】权限列表

```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
```

#### 【可选】硬件信息访问权限

```xml
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
```

#### installreferrer 依赖所需权限

```xml
<uses-permission android:name="com.google.android.finsky.permission.BIND_GET_INSTALL_REFERRER_SERVICE" />
```



### Appsflyer App ID 配置

```xml
<meta-data android:name="IMSDK_APPSFLYER_KEY" android:value="{APPSFLYER_KEY}" />
```

`{APPSFLYER_KEY}` 需要修改为业务 App Key 就是 ==devkey？==



### Receiver 配置

如果 AndroidManifest.xml 中没有 `com.android.vending.INSTALL_REFERRER` 配置，添加如下 Receiver 配置

```xml
<receiver android:name="com.appsflyer.SingleInstallBroadcastReceiver" android:exported="true">
   <intent-filter>
       <action android:name="com.android.vending.INSTALL_REFERRER" />
   </intent-filter>
</receiver>
```

​			

如果 AndroidManifest.xml 已经存在 `com.android.vending.INSTALL_REFERRER` 配置，添加如下 Receiver 配置

```xml
<receiver android:name="com.appsflyer.MultipleInstallBroadcastReceiver" android:exported="true">
 <intent-filter>
    <action android:name="com.android.vending.INSTALL_REFERRER" />
 </intent-filter>
</receiver>
```

​			

### GMS 依赖版本配置

```xml
<meta-data android:name="com.google.android.gms.version" android:value="@integer/google_play_services_version" />
```



```java
package com.appsflyer.onelink.appsflyeronelinkbasicapp;

import com.appsflyer.AppsFlyerLib;
import com.appsflyer.deeplink.DeepLink;
import com.appsflyer.deeplink.DeepLinkListener;
import com.appsflyer.deeplink.DeepLinkResult;
import com.appsflyer.AppsFlyerConversionListener;

import android.app.Application;
import android.content.Intent;
import android.util.Log;
import com.google.gson.Gson;
import androidx.annotation.NonNull;
import java.util.Map;
import java.util.Objects;

public class AppsflyerBasicApp extends Application {
    public static final String LOG_TAG = "AppsFlyerOneLinkSimApp";
    public static final String DL_ATTRS = "dl_attrs";
    Map<String, Object> conversionData = null;

    @Override
    public void onCreate() {
        super.onCreate();
        String afDevKey = AppsFlyerConstants.afDevKey;
        AppsFlyerLib appsflyer = AppsFlyerLib.getInstance();
        // Make sure you remove the following line when building to production
        appsflyer.setDebugLog(true);
        appsflyer.setMinTimeBetweenSessions(0);

        appsflyer.subscribeForDeepLink(new DeepLinkListener(){
            @Override
            public void onDeepLinking(@NonNull DeepLinkResult deepLinkResult) {
                DeepLinkResult.Status dlStatus = deepLinkResult.getStatus();
                if (dlStatus == DeepLinkResult.Status.FOUND) {
                    Log.d(LOG_TAG, "Deep link found");
                } else if (dlStatus == DeepLinkResult.Status.NOT_FOUND) {
                    Log.d(LOG_TAG, "Deep link not found");
                    return;
                } else {
                    // dlStatus == DeepLinkResult.Status.ERROR
                    DeepLinkResult.Error dlError = deepLinkResult.getError();
                    Log.d(LOG_TAG, "There was an error getting Deep Link data: " + dlError.toString());
                    return;
                }
                DeepLink deepLinkObj = deepLinkResult.getDeepLink();
                try {
                    Log.d(LOG_TAG, "The DeepLink data is: " + deepLinkObj.toString());
                } catch (Exception e) {
                    Log.d(LOG_TAG, "DeepLink data came back null");
                    return;
                }
                // An example for using is_deferred
                if (deepLinkObj.isDeferred()) {
                    Log.d(LOG_TAG, "This is a deferred deep link");
                } else {
                    Log.d(LOG_TAG, "This is a direct deep link");
                }
                // An example for getting deep_link_value
                String fruitName = "";
                try {
                    fruitName = deepLinkObj.getDeepLinkValue();
                    if (fruitName == null){
                        Log.d(LOG_TAG, "Deeplink value returned null");
                        return;
                    }
                    Log.d(LOG_TAG, "The DeepLink will route to: " + fruitName);
                } catch (Exception e) {
                    Log.d(LOG_TAG, "Custom param fruit_name was not found in DeepLink data");
                    return;
                }
                goToFruit(fruitName, deepLinkObj);
            }
        });

        AppsFlyerConversionListener conversionListener =  new AppsFlyerConversionListener() {
            @Override
            public void onConversionDataSuccess(Map<String, Object> conversionDataMap) {
                for (String attrName : conversionDataMap.keySet())
                    Log.d(LOG_TAG, "Conversion attribute: " + attrName + " = " + conversionDataMap.get(attrName));
                String status = Objects.requireNonNull(conversionDataMap.get("af_status")).toString();
                if(status.equals("Non-organic")){
                    if( Objects.requireNonNull(conversionDataMap.get("is_first_launch")).toString().equals("true")){
                        Log.d(LOG_TAG,"Conversion: First Launch");
                    } else {
                        Log.d(LOG_TAG,"Conversion: Not First Launch");
                    }
                } else {
                    Log.d(LOG_TAG, "Conversion: This is an organic install.");
                }
                conversionData = conversionDataMap;
            }

            @Override
            public void onConversionDataFail(String errorMessage) {
                Log.d(LOG_TAG, "error getting conversion data: " + errorMessage);
            }

            @Override
            public void onAppOpenAttribution(Map<String, String> attributionData) {
                Log.d(LOG_TAG, "onAppOpenAttribution: This is fake call.");
            }

            @Override
            public void onAttributionFailure(String errorMessage) {
                Log.d(LOG_TAG, "error onAttributionFailure : " + errorMessage);
            }
        };
        appsflyer.init(afDevKey, conversionListener, this);
        appsflyer.start(this);
    }

    private void goToFruit(String fruitName, DeepLink dlData) {
        String fruitClassName = (fruitName.substring(0, 1).toUpperCase() + fruitName.substring(1)).concat("Activity");
        try {
            Class fruitClass = Class.forName(this.getPackageName().concat(".").concat(fruitClassName));
            Log.d(LOG_TAG, "Looking for class " + fruitClass);
            Intent intent = new Intent(getApplicationContext(), fruitClass);
            if (dlData != null) {
                // TODO - make DeepLink Parcelable
                String objToStr = new Gson().toJson(dlData);
                intent.putExtra(DL_ATTRS, objToStr);
            }
            intent.setFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
            startActivity(intent);
        } catch (ClassNotFoundException e) {
            Log.d(LOG_TAG, "Deep linking failed looking for " + fruitName);
            e.printStackTrace();
        }
    }
}
```

---

```java
AppsFlyerLib.getInstance().start(getApplicationContext(), <YOUR_DEV_KEY>, new AppsFlyerRequestListener() {
  @Override
  public void onSuccess() {
    Log.d(LOG_TAG, "Launch sent successfully, got 200 response code from server");
  }
  
  @Override
  public void onError(int i, @NonNull String s) {
    Log.d(LOG_TAG, "Launch failed to be sent:\n" +
          "Error code: " + i + "\n"
          + "Error description: " + s);
  }
});
```



```java
import android.app.Application;
import com.appsflyer.AppsFlyerLib;
// ...
public class AFApplication extends Application {
    // ...
    @Override
    public void onCreate() {
        super.onCreate();
        // ...
        AppsFlyerLib.getInstance().init(<AF_DEV_KEY>, null, this);
        AppsFlyerLib.getInstance().start(this);
        // ...
    }
    // ...
}
```







