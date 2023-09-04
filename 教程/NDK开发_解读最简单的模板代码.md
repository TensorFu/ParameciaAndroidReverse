###  NDK 开发简介

1. 为了安全（C++ 反编译出来的代码狗都不想看，加了混淆，狗看了都摇头）
2. 为了运行速度
3. 他能够获取 Java 层的返回值，或者能够给 Java 层递返回值

### 创建项目

1. 首先是我们要选择，我们的项目，注意不是任何的项目都可以，只能是 Native C++ 的项目

![image-20230707165049807](./assets/image-20230707165049807.png)

​					

2. 设置你的项目的名称

   ![image-20230707165242306](./assets/image-20230707165242306.png)

​			

3. 最后是选择 C++ 

![image-20230707165341461](./assets/image-20230707165341461.png)

​				

### 认识你的项目文件结构

![image-20230707170729993](./assets/image-20230707170729993.png)

你会看到相较于以前的新建的项目，我们的项目多了 CPP 的这个文件夹				

这个目录下存放的是你的 C++ 源代码文件和 `CMakeLists.txt` 文件，用于编译你的 C++ 代码				



我们来看看 MainActivity.java 这个文件有什么不同

```java
package com.my.myc_plus;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.widget.TextView;

import com.my.myc_plus.databinding.ActivityMainBinding;

public class MainActivity extends AppCompatActivity {

    static {
        System.loadLibrary("myc_plus");
    }

    private ActivityMainBinding binding;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        binding = ActivityMainBinding.inflate(getLayoutInflater());
        setContentView(binding.getRoot());

        TextView tv = binding.sampleText;
        tv.setText(stringFromJNI());
    }

    public native String stringFromJNI();
}
```

​			

这里我们发现他导入了 libmyc_plus.so 的这个文件（但是我们没有 myc_plus.cpp 的这个文件啊，这个我们后面解释）

```java
    static {
        System.loadLibrary("myc_plus");
    }
```

​			

这是一个被 native 修饰的一个函数，说明这个函数的实现在 so 文件当中，也就是上面我们看到的那个 so 文件，看这个函数的类型就知道返回的是一个字符串，并且这个字符串在后面的展示当中被当做展示的文本

```java
public native String stringFromJNI();
```

​			

注意：如果你的一个 项目或者说一个类当中被加入了多个 so 文件，那么你应该要确保，每一个 so 层的函数的函数名没有重复，因为你重复以后，他不会报错，但是他的执行是按照，谁先加载执行谁的函数，所以可能会出现执行的函数和你想象当中不一样的情况

​			

**对应的 C++ 的代码**

```C++
#include <jni.h>
#include <string>

extern "C" JNIEXPORT jstring JNICALL
Java_com_my_myc_1plus_MainActivity_stringFromJNI(
        JNIEnv* env,
        jobject /* this */) {
    std::string hello = "Hello from C++";
    return env->NewStringUTF(hello.c_str());
}
```

注意：通过观察这个 ，Java_com_my_myc_1plus_MainActivity_stringFromJNI 这个路径，我们会发现，为什么多了一个 1 			

为什么不是 ： Java_com_my_myc_plus_MainActivity_stringFromJNI，那是因为在原来的路径当中 com.my.myc_plus.MainActivity.stringFromJNI()，有一个下划线，这个下划线没有办法直接转，不然就成了两个下划线，看起来很怪，而且下划线一多，也不知道连在一起到底多少个下划线。所以下划线就转换成了 1 

​				

**加载 so 文件的方式有两种(一般都是 System.loadLibrary )**

1. `System.loadLibrary(String libName)`: 这个函数接受一个库名（不包括 "lib" 前缀和 ".so" 后缀）作为参数。它会搜索系统的库路径（例如，在 Android 设备上的 `/lib` 目录）和应用的私有库路径（例如，你的 APK 包里的 `lib` 目录）来查找并加载这个库。
2. `System.load(String absolutePath)`: 这个函数接受一个 `.so` 文件的绝对路径作为参数。它不会搜索任何路径，而是直接加载这个路径下的 `.so` 文件。

​				

**为什么 C++ 的文件名和 .so 的文件名不一样**

原因是编译文件决定的

```tex
# For more information about using CMake with Android Studio, read the
# documentation: https://d.android.com/studio/projects/add-native-code.html

# Sets the minimum version of CMake required to build the native library.

cmake_minimum_required(VERSION 3.22.1)

# Declares and names the project.

project("myc_plus")

# Creates and names a library, sets it as either STATIC
# or SHARED, and provides the relative paths to its source code.
# You can define multiple libraries, and CMake builds them for you.
# Gradle automatically packages shared libraries with your APK.

add_library( # Sets the name of the library.
        myc_plus

        # Sets the library as a shared library.
        SHARED

        # Provides a relative path to your source file(s).
        native-lib.cpp)

# Searches for a specified prebuilt library and stores the path as a
# variable. Because CMake includes system libraries in the search path by
# default, you only need to specify the name of the public NDK library
# you want to add. CMake verifies that the library exists before
# completing its build.

find_library( # Sets the name of the path variable.
        log-lib

        # Specifies the name of the NDK library that
        # you want CMake to locate.
        log)

# Specifies libraries CMake should link to your target library. You
# can link multiple libraries, such as libraries you define in this
# build script, prebuilt third-party libraries, or system libraries.

target_link_libraries( # Specifies the target library.
        myc_plus

        # Links the target library to the log library
        # included in the NDK.
        ${log-lib})
```

​			

### C++ 代码

```C++
extern "C"
JNIEXPORT jstring JNICALL
Java_com_example_myapp_MyActivity_stringFromJNI(
    JNIEnv* env,
    jobject /* this */) {
  std::string hello = "Hello from C++";
  return env->NewStringUTF(hello.c_str());
}
```

**extern "C"**

当你在代码中看到 `extern` ，可以把它理解为"这个函数/变量的定义存在于别的地方"。`extern`关键字告诉编译器，即使在当前文件中没有找到该函数或变量的定义，也不要报错，因为定义在其他地方。



这是一个链接说明符，用于告诉C++编译器按照C语言的方式来处理函数。C++支持函数重载，即函数名可以相同但参数不同，如果不加上这个关键词，那么编译的时候他就会按照 C++  的规则进行编译，那么这个时候，函数的名字就发生了改变了，而C 不会做出这样的改变，编译了以后能够保持函数的名字不变。C++在编译时会通过名字修饰（name mangling）来保持函数的唯一性。`extern "C"`使得该函数在编译时不进行名字修饰，从而可以在C代码或者其他C++代码中被找到和调用。

那么为什么要这样做呢？

因为：当Java通过Java Native Interface (JNI)调用C/C++代码时，需要的是具有特定名称的函数。这个名称在Java中是作为字符串硬编码的，因此，在这种情况下，对于Java来说，C/C++函数的名称必须是唯一的，就是在做 ndk 开发的时候，是不支持函数的重载的。



**JNIEXPORT jstring JNICALL**

`JNIEXPORT`: 这是一个导出标志，用于告诉编译器这个函数将被导出，因此其他代码（例如Java代码）可以调用它。

​			

`jstring` 这个就是，告诉系统，`Java_com_example_myapp_MyActivity_stringFromJNI` 这个函数的返回值的类型

​				

`JNICALL` 就是告诉编译器，这个函数应该使用JNI调用约定。也就是要使用 JNI 函数的调用规范来使用这个函数



#### JNI 函数的两个参数 JNIEnv* env , jobject obj (jclass obj)

```C++
Java_com_my_myc_1plus_MainActivity_stringFromJNI(
        JNIEnv* env,
        jobject /* this */) {
    std::string hello = "Hello from C++";
    return env->NewStringUTF(hello.c_str());
}
```

这里面有两个参数

第一个参数是 **JNIEnv* env：**		

```java
jclass cls = env->FindClass("com/example/myapp/MyClass");
```

`env`是一个指向`JNIEnv`结构体的指针，`JNIEnv`中有一个名为`FindClass`的成员（在这种情况下，`FindClass`是一个函数指针）。所以`env->FindClass`就是通过`env`指针访问`JNIEnv`结构体中的`FindClass`函数

他的作用主要就是一个，调用 JNI 的函数，指向哪一个，就调用哪一个的函数

​			

第二个参数 **jclass obj** / **jobject obj**

第二个参数是，不定的，主要是看你的 native 方法是不是静态的			

如果是静态方法，那么就是 **jclass** 

如果是实例方法，那么就是 **jobject**



当我们的方法是静态方法的时候，我们应该使用 jclass 			

比方说我有一个类  Mainclass 并且在里面申请了 native 方法，并且是静态的方式申请的。

jclass obj 的 obj 代表的就是`Mainclass`这个Java类。你可以通过这个`obj`参数，调用该类的其他静态方法，或者访问该类的静态字段。			

当然你也是可以访问，实例方法的，这个随后介绍

​					

当我们的实例方法的时候，我们应该使用 jobject

jobject obj 的 obj 表示调用该 JNI 函数的Java对象。例如，如果你在一个Java实例方法中调用了一个native方法，那么这个`obj`就代表了那个Java实例 ，比方说我有一个类  Mainclass 并且在里面申请了 native 方法，并且是实例方法申请的			

那么

```java
Mainclass mainclass  = new Mainclass();
mainclass.native_function();
```

我们的 obj 就是表示的 mainclass 这个实例			

同样的，我们还是可以调用他们的静态函数，静态变量，或者是，实例方法，或者实例变量。



现在我们来看看第二个参数的使用

1. 首先，如果我们的 native 的函数是一个静态的函数

   1. 那么我们的第二个参数就应该是 jclass 
   2. 通过 jclass 获取静态的变量和静态的方法

   























