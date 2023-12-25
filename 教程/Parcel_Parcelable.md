## Parcel 和 Parcelable

```java
public class Person implements Parcelable {
    private String name;
    private int age;

    // 构造函数
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Parcelable构造函数，也就是从 parcel 数据当中拿到这个数据
    protected Person(Parcel in) {
        name = in.readString();
        age = in.readInt();
    }

  // 将我们的数据写进  parcel 数据对象当中
    @Override
    public void writeToParcel(Parcel parcel, int i) {
        parcel.writeString(name);
        parcel.writeInt(age);
    }
  
    public static final Parcelable.Creator<Person> CREATOR = new Parcelable.Creator<Person>() {
      @Override
      public Person createFromParcel(Parcel in) {
          return new Person(in);
      }

      @Override
      public Person[] newArray(int size) {
          return new Person[size];
      }
  };
}
```



### 一个案例

定义 `Person` 类，它实现了 `Parcelable` 接口。

```java
import android.os.Parcel;
import android.os.Parcelable;

public class Person implements Parcelable {
    private String name;
    private int age;

    // 构造函数
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // 从Parcel中读取数据的构造函数
    protected Person(Parcel in) {
        name = in.readString();
        age = in.readInt();
    }

  // 这里的 flag 一般来说都是 0 ，绝大部分都是 0 。他只是将我们的数据写进去的，附加信息
    @Override
    public void writeToParcel(Parcel parcel, int flags) {
        parcel.writeString(name);
        parcel.writeInt(age);
    }

    public static final Parcelable.Creator<Person> CREATOR = new Parcelable.Creator<Person>() {
        @Override
        public Person createFromParcel(Parcel in) {
            return new Person(in);
        }

        @Override
        public Person[] newArray(int size) {
            return new Person[size];
        }
    };

}
```

​				

`ActivityA` 中发送 `Person` 对象

我们创建一个 `Person` 对象，并通过 `Intent` 将其发送到 `ActivityB`。

```java
import android.content.Intent;
import android.os.Bundle;
import androidx.appcompat.app.AppCompatActivity;

public class ActivityA extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_a);

        Person person = new Person("John Doe", 30);
        Intent intent = new Intent(ActivityA.this, ActivityB.class);
        intent.putExtra("person_data", person);
        startActivity(intent);
    }
}
```

​					

在 `ActivityB` 中，我们从接收到的 `Intent` 中提取 `Person` 对象。

```java
import android.content.Intent;
import android.os.Bundle;
import androidx.appcompat.app.AppCompatActivity;

public class ActivityB extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_b);

        Intent intent = getIntent();
        Person person = intent.getParcelableExtra("person_data");
        if (person != null) {
            // 使用person对象的数据
            String name = person.getName();
            int age = person.getAge();
            // 处理获取的数据，比如更新UI
        }
    }
}
```





























