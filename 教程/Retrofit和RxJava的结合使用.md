## Retrofit和RxJava的结合使用

### 一个真实的案例

我们这里想要实现的是，从网络上获取一个图片，并且显示在手机上

​					

我们这里要感谢，能够免费的公开的获取一个图片的网站 [pixabay.com](https://pixabay.com/zh/)			

#### 获取APIkey

首先我们需要打开这个网站，[pixabay.com](https://pixabay.com/zh/) 并且注册一个账号，在网站的右上方的位置找到 explore（或者叫做探索）点击这个按钮，就能够看得到， API 的选项。这个时候，就能够看得到我们的 key （或者是你可以用我现成的 key ：24788540-83d8e58f3038faa4869c3adbe ） 

同时我们还知道，他的请求的 URL 的格式，和下发的数据的格式 [文档](https://pixabay.com/api/docs/)   

​			

根据他的例子我们知道

https://pixabay.com/api/?key=24788540-83d8e58f3038faa4869c3adbe&q=yellow+flowers&image_type=photo

这个URL主要分为以下的几个部分

1. pixabay.com
2. api/
3. ?key=24788540-83d8e58f3038faa4869c3adbe&q=yellow+flowers&image_type=photo



我们就知道，我们主要关心的就是，key 和 我们的搜索条件，这里搜索的是 黄+花，图片的类型是 photo

​				

### 开始写代码

根据返回的响应，我们知道，我们的想要的图片的链接的位置，所以我们设置，相应数据的接受的格式

ResponseData.java

```java
package com.open.ok;

import java.util.List;

class ResponseData {
    public int total;
    public List<ImageData> hits;

    static class ImageData {
        public String webformatURL;
    }
}
```

​			

PixabayApi.java

```java
package com.open.ok;


import io.reactivex.rxjava3.core.Observable;
import retrofit2.http.GET;
import retrofit2.http.Query;


public interface PixabayApi {
    @GET("api/")
    Observable<ResponseData> getImages(@Query("key") String apiKey,
                                       @Query("q") String query,
                                       @Query("image_type") String imageType);
}
```

​				

MainActivity.java

```java
package com.open.ok;

import androidx.appcompat.app.AppCompatActivity;
import androidx.lifecycle.ViewModelProvider;

import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.ImageView;
import android.widget.TextView;

import com.bumptech.glide.Glide;
import com.open.ok.databinding.ActivityMainBinding;

import io.reactivex.rxjava3.android.schedulers.AndroidSchedulers;
import io.reactivex.rxjava3.core.Observer;
import io.reactivex.rxjava3.disposables.Disposable;
import io.reactivex.rxjava3.schedulers.Schedulers;
import okhttp3.OkHttpClient;
import okhttp3.logging.HttpLoggingInterceptor;
import retrofit2.Retrofit;
import retrofit2.adapter.rxjava3.RxJava3CallAdapterFactory;
import retrofit2.converter.gson.GsonConverterFactory;

public class MainActivity extends AppCompatActivity {
    private ImageView imageView;
    private final String PIXABAY_API_KEY = "24788540-83d8e58f3038faa4869c3adbe";
    private final String BASE_URL = "https://pixabay.com/";

    // Used to load the 'ok' library on application startup.
    static {
        System.loadLibrary("ok");
    }

    private ActivityMainBinding binding;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        binding = ActivityMainBinding.inflate(getLayoutInflater());
        setContentView(binding.getRoot());

        TextView tv = binding.sampleText;
        tv.setText(stringFromJNI());

        // 用来打印日志
        HttpLoggingInterceptor logging = new HttpLoggingInterceptor();
        logging.setLevel(HttpLoggingInterceptor.Level.BODY);
        OkHttpClient.Builder httpClient = new OkHttpClient.Builder();
        httpClient.addInterceptor(logging);

        imageView = findViewById(R.id.imageView);
        Retrofit retrofit = new Retrofit.Builder()
                .baseUrl(BASE_URL)
                .addConverterFactory(GsonConverterFactory.create())
                .addCallAdapterFactory(RxJava3CallAdapterFactory.create()) // 注意这个是必须的，这样才能够保证这两种框架能够结合起来使用
                .client(httpClient.build())
                .build();

        PixabayApi api = retrofit.create(PixabayApi.class);

        api.getImages(PIXABAY_API_KEY, "yellow+flower", "photo")
                .subscribeOn(Schedulers.io())
                .observeOn(AndroidSchedulers.mainThread())
                .subscribe(new Observer<ResponseData>() {
                    @Override
                    public void onSubscribe(Disposable d) {
                    }

                    @Override
                    public void onNext(ResponseData responseData) {
                        if (responseData.total > 0) {
                            loadImage(responseData.hits.get(0).webformatURL);
                        }
                    }

                    @Override
                    public void onError(Throwable e) {
                        e.printStackTrace();
                    }

                    @Override
                    public void onComplete() {
                        // Handle completion if needed
                    }
                });
    }

    private void loadImage(String url) {
        Log.i("okk",url);
        Glide.with(this)
                .load(url)
                .into(imageView);
    }

    /**
     * A native method that is implemented by the 'ok' native library,
     * which is packaged with this application.
     */
    public native String stringFromJNI();
}
```

​			

1. **`addCallAdapterFactory(RxJava3CallAdapterFactory.create())`**

   这是Retrofit的一个功能，允许您将Retrofit的网络请求与RxJava结合使用。RxJava是一个Java库，用于实现响应式编程。

   `RxJava3CallAdapterFactory`是一个工厂，它能让Retrofit返回RxJava 3的`Observable`, `Single`, `Completable`等对象，而不是常规的Call对象。这意味着您可以将Retrofit网络请求与RxJava操作符结合使用，进行更复杂的异步操作。

2. **`.subscribeOn(Schedulers.io())`**

   这是一个RxJava的操作符。它告诉RxJava在哪个线程上执行这个`Observable`的工作。在这里，您选择了`Schedulers.io()`，这是一个为I/O操作（例如网络请求或磁盘读写）优化的调度器。

3. **`.observeOn(AndroidSchedulers.mainThread())`**

   这又是一个RxJava的操作符。它指定当`Observable`发出项目或完成时应在哪个线程上调用`Observer`的方法。在这里，您选择了`AndroidSchedulers.mainThread()`，这意味着`Observer`的方法（如`onNext`, `onError`, `onComplete`）将在Android的主线程上执行，这对于更新UI是必要的。

4. **`.subscribe(new Observer<ResponseData>() {...})`**

   这是您订阅`Observable`的地方，以便在`Observable`发出项目、出错或完成时接收通知。`Observer`有三个主要的方法：

   - `onNext(T item)`: 每当`Observable`发出项目时，都会调用此方法。在这里，您检查响应是否有图像，并尝试加载第一张图像。
   - `onError(Throwable e)`: 如果在处理`Observable`期间发生错误，将调用此方法。您在此打印了堆栈跟踪。
   - `onComplete()`: 当`Observable`成功完成其发射的项目并不会再发出任何其他项目时，将调用此方法。





