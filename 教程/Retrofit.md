## Retrofit

[TOC]

简单来说 Retrofit  就是一个高级的 OKHttp 			

Retrofit 是一种在 Android 和 Java 应用程序中处理 HTTP 客户端的类型安全的库。这是由 Square, Inc. 开发的。Retrofit 被设计成简洁和高效，特别适合用于移动应用。通过 Retrofit，开发者可以很容易地将 HTTP API 转换成 Java 接口。			

​			

### 主要特点：

1. **类型安全**：Retrofit 使用注解来描述 HTTP 请求参数、路径和查询参数，这使得库能够确保类型的安全性。
2. **高性能**：Retrofit 基于 OkHttp 库，因此它继承了 OkHttp 的性能优势，如连接池、缓存和 HTTP/2 支持。
3. **灵活性**：Retrofit 支持同步和异步调用，允许开发者根据需要选择。
4. **支持多种数据格式**：Retrofit 支持多种数据格式，如 JSON、XML，以及 Protocol Buffers。
5. **简洁的 API**：Retrofit 提供了一种简洁、直观的 API，使得创建和管理网络请求变得简单。

​						



### 一个实战的案例

我们现在是想，通过 Retrofit 访问一个天气的服务器，然后拿到一个地区的，温度的信息			

首先要非常的感谢，有能够让我们随便访问的服务器				

[openweathermap注册的地址	](https://openweathermap.org)			

现在你在这个网站当中注册一个账号			

注册成功之后，就能够获得一个 APIKEY ，你也可以使用我的这里的现成的 key [ 544a1d9a2925e59467b8c59d1f59c29f ]				

​				

[openweathermap的API响应格式](https://openweathermap.org/current#current_JSON)		

通过上面的这个文档我们知道以下的内容

#### 请求的格式

```makefile
https://api.openweathermap.org/data/2.5/weather?lat={lat}&lon={lon}&appid={API key}
```

也就是说，我们想要一个，天气的信息，那么我就需要，发送一个坐标（经度和维度），还有就是 key ，这个 key 就是前面，我们注册的时候，网站送给我们的 key 			

​			

#### 响应的格式

这个是官方告诉我们，他们大概会按照专业的形式，下发数据

```json
{
  "coord": {
    "lon": 10.99,
    "lat": 44.34
  },
  "weather": [
    {
      "id": 501,
      "main": "Rain",
      "description": "moderate rain",
      "icon": "10d"
    }
  ],
  "base": "stations",
  "main": {
    "temp": 298.48,
    "feels_like": 298.74,
    "temp_min": 297.56,
    "temp_max": 300.05,
    "pressure": 1015,
    "humidity": 64,
    "sea_level": 1015,
    "grnd_level": 933
  },
  "visibility": 10000,
  "wind": {
    "speed": 0.62,
    "deg": 349,
    "gust": 1.18
  },
  "rain": {
    "1h": 3.16
  },
  "clouds": {
    "all": 100
  },
  "dt": 1661870592,
  "sys": {
    "type": 2,
    "id": 2075663,
    "country": "IT",
    "sunrise": 1661834187,
    "sunset": 1661882248
  },
  "timezone": 7200,
  "id": 3163858,
  "name": "Zocca",
  "cod": 200
}                        
```

​				

#### 开始写代码

了解了上面的信息之后，我们开始写代码

最开始，你应该添加依赖

```build.gradle
    implementation 'com.squareup.retrofit2:retrofit:2.9.0'
    implementation 'com.squareup.retrofit2:converter-gson:2.9.0'
```

​						

##### WeatherResponse

这个主要就是根据，服务器的下发数据，进行编写，所谓是一个萝卜一个坑，如果这个部分不是很理解的，我也不知道怎么解释，大概的意思就是，你需要，写一个类，来对应下发的 JSON 的数据，这里的嵌套就是通过，静态的内部类实现的，这里的嵌套的深度是，两层，如果你还有更加深度的掐套，那么，就需要，在静态内部类当中再加上一个静态的内部类，我相信，你懂我的意思，我也会在后面，提供一个案例

```java
package com.open.OPENretrofit2;

import java.util.List;

public class WeatherResponse {
    public Coord coord;
    public List<Weather> weather;
    public String base;
    public Main main;
    public int visibility;
    public Wind wind;
    public Rain rain;
    public Clouds clouds;
    public long dt;
    public Sys sys;
    public int timezone;
    public int id;
    public String name;
    public int cod;

    public static class Coord {
        public double lon;
        public double lat;
    }

    public static class Weather {
        public int id;
        public String main;
        public String description;
        public String icon;
    }

    public static class Main {
        public float temp;
        public float feels_like;
        public float temp_min;
        public float temp_max;
        public int pressure;
        public int humidity;
        public int sea_level;
        public int grnd_level;
    }

    public static class Wind {
        public float speed;
        public int deg;
        public float gust;
    }

    public static class Rain {
        public float _1h;
    }

    public static class Clouds {
        public int all;
    }

    public static class Sys {
        public int type;
        public int id;
        public String country;
        public long sunrise;
        public long sunset;
    }
}
```

​			

```json
{
  "coord": {
    "lon": 10.99,
    "lat": 44.34
  },
  "weather": [
    {
      "id": 501,
      "main": "Rain",
      "description": "moderate rain",
      "icon": "10d"
    }
  ],
  "base": "stations",
  "main": {
    "temp": 298.48,
    "feels_like": 298.74,
    "temp_min": 297.56,
    "temp_max": 300.05,
    "pressure": 1015,
    "humidity": 64,
    "sea_level": 1015,
    "grnd_level": 933
  },
  "visibility": 10000,
  "wind": {
    "speed": 0.62,
    "deg": 349,
    "gust": 1.18
  },
  "rain": {
    "1h": 3.16
  },
  "clouds": {
    "all": 100
  },
  "dt": 1661870592,
  "sys": {
    "type": 2,
    "id": 2075663,
    "country": "IT",
    "sunrise": 1661834187,
    "sunset": 1661882248
  },
  "timezone": 7200,
  "id": 3163858,
  "name": "Zocca",
  "cod": 200
}                        
```

​			

###### 如果有更加深的JSON

JSON	

```json
{
  "outer": {
    "inner": {
      "field": "value"
    }
  }
}
```

​				

Java

```java
public class Response {
    public Outer outer;
    
    public static class Outer {
        public Inner inner;
        
        public static class Inner {
            public String field;
        }
    }
}
```

​					

##### 编写接口 OpenWeatherMapApi 

```java
import retrofit2.Call;
import retrofit2.http.GET;
import retrofit2.http.Query;

public interface OpenWeatherMapApi {
    @GET("weather")
    Call<WeatherResponse> getCurrentWeatherData(@Query("lat") String lat, @Query("lon") String lon, @Query("appid") String appid);
}
```

这里就是相当于在设置，请求头和设置 URL 

​					

```java
@GET("weather")
```

`@GET`这个部分的作用是，将这个请求设置为 **GET** 类型					

`"weather"` 表示的是 API 请求的相对 URL 路径					

所谓的相当路径，就是相比较于我们之前说的，基础路径				

​				

这是我们之前看到的，URL 

```makefile
https://api.openweathermap.org/data/2.5/weather?lat={lat}&lon={lon}&appid={API key}
```

​			

这个就是基础路径（怎么设置基础路径后面介绍）		

```makefile
https://api.openweathermap.org/data/2.5
```

​				

后面的 weather 就是相对的路径（相对路径是放在最后的）

```
https://api.openweathermap.org/data/2.5/weather
```

​				

```java
Call<WeatherResponse> getCurrentWeatherData(@Query("lat") String lat, @Query("lon") String lon, @Query("appid") String appid);
}
```

这是一个 Retrofit 接口方法，它定义了一个 HTTP GET 请求，用于从 OpenWeatherMap API 获取当前天气数据	

​							

方法返回类型： `Call<WeatherResponse>`

- `Call<T>`：这是 Retrofit 的一个类，代表一个尚未执行的 HTTP 请求。你可以通过这个 `Call` 对象来执行请求。
- `WeatherResponse`：这是一个 Java 类，用于存储 API 响应的数据。Retrofit 将会把 HTTP 响应自动转换为这个类的一个对象。

​						

方法名： `getCurrentWeatherData`

这是你为这个方法定义的名字。你将通过这个名字来调用这个方法。

方法参数： `@Query("lat") String lat, @Query("lon") String lon, @Query("appid") String appid`

这些是你在调用此方法时需要传递的参数。每个参数前都有一个 `@Query` 注解，这表示这些参数将会被添加到请求的 URL 中作为查询参数。

- `@Query("lat") String lat`：这将会把传递的 `lat` 参数值添加到 URL 中，形成一个查询参数，例如：`...?lat=value`.
- `@Query("lon") String lon` 和 `@Query("appid") String appid` 同理。

​				

当我们调用的时候（怎么调用，我们后面介绍）

```java
call = apiInterface.getCurrentWeatherData("35.6895", "139.6917", "YOUR_API_KEY");
```

就会得到这样的 URL 

```java
GET http://api.openweathermap.org/data/2.5/weather?lat=35.6895&lon=139.6917&appid=YOUR_API_KEY
```

​				

#### 发起请求

这是一个点击一个按钮就能够发送一个请求，并且处理一个响应的一个函数，将获取到的响应当中的温度打印在，日志当中

```java
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

import com.open.OPENretrofit2.databinding.ActivityMainBinding;

import retrofit2.Call;
import retrofit2.Callback;
import retrofit2.Response;
import retrofit2.Retrofit;
import retrofit2.converter.gson.GsonConverterFactory;

public class MainActivity extends AppCompatActivity {
    private Button buttonLoad;

    // Used to load the 'OPENretrofit2' library on application startup.
    static {
        System.loadLibrary("OPENretrofit2");
    }

    private ActivityMainBinding binding;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        binding = ActivityMainBinding.inflate(getLayoutInflater());
        setContentView(binding.getRoot());

        // Example of a call to a native method
        TextView tv = binding.sampleText;
        tv.setText(stringFromJNI());

        Retrofit retrofit = new Retrofit.Builder()
                .baseUrl("https://api.openweathermap.org/data/2.5/")
                .addConverterFactory(GsonConverterFactory.create())
                .build();

        OpenWeatherMapApi api = retrofit.create(OpenWeatherMapApi.class);


        buttonLoad = findViewById(R.id.buttonLoad);

        buttonLoad.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // 在这里发起网络请求
                Call<WeatherResponse> call = api.getCurrentWeatherData("35.6895", "139.6917", "544a1d9a2925e59467b8c59d1f59c29f");
                call.enqueue(new Callback<WeatherResponse>() {
                    @Override
                    public void onResponse(Call<WeatherResponse> call, Response<WeatherResponse> response) {
                        float temperature = response.body().main.temp;
                        Log.i("天气", "Temperature: " + temperature); // 在这里打印温度
                        Log.i("天气","获取成功");
                    }

                    @Override
                    public void onFailure(Call<WeatherResponse> call, Throwable t) {
                        // 处理错误
                        Log.i("天气","获取失败");
                    }
                });
            }
        });
    }

    /**
     * A native method that is implemented by the 'OPENretrofit2' native library,
     * which is packaged with this application.
     */
    public native String stringFromJNI();
}
```



##### 请求的主体

```java
        Retrofit retrofit = new Retrofit.Builder()
                .baseUrl("https://api.openweathermap.org/data/2.5/")
                .addConverterFactory(GsonConverterFactory.create())
                .build();

        OpenWeatherMapApi api = retrofit.create(OpenWeatherMapApi.class);


                // 在这里发起网络请求
                Call<WeatherResponse> call = api.getCurrentWeatherData("35.6895", "139.6917", "544a1d9a2925e59467b8c59d1f59c29f");
                call.enqueue(new Callback<WeatherResponse>() {
                    @Override
                    public void onResponse(Call<WeatherResponse> call, Response<WeatherResponse> response) {
                        float temperature = response.body().main.temp;
                        Log.i("天气", "Temperature: " + temperature); // 在这里打印温度
                        Log.i("天气","获取成功");
                    }

                    @Override
                    public void onFailure(Call<WeatherResponse> call, Throwable t) {
                        // 处理错误
                        Log.i("天气","获取失败");
                    }
                });
```

​					

**创建 Retrofit Builder**

```java
        Retrofit retrofit = new Retrofit.Builder()
                .baseUrl("https://api.openweathermap.org/data/2.5/")
                .addConverterFactory(GsonConverterFactory.create())
                .build();
```

**设置基础 URL**

```java
baseUrl("https://api.openweathermap.org/data/2.5/")
```

**添加转换工厂**

```java
addConverterFactory(GsonConverterFactory.create())
```

这个工厂负责将 HTTP 响应体转换成 Java 对象，以及将 Java 对象转换成请求体			

`GsonConverterFactory.create()` 使用 Gson 库来解析 JSON 响应			

​					

