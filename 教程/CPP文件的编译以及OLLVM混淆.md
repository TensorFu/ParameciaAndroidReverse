### CPP的编译以及OLLVM混淆

开发工具：android studio			

开发的平台：MacOS				

​			

1. 安装 NDK 和 CMake

首先确定你的设备已经安装了上述的内容

在Android Studio中，你可以通过SDK Manager来安装NDK和CMake。这可以通过点击“Android Studio” -> “Preferences(Settings)” -> “Appearance & Behavior” -> “System Settings” -> “Android SDK” -> “SDK Tools”，然后选择NDK和CMake进行安装。

​				

2. 创建CMakeLists.txt文件

在你的项目的main/CPP目录下（也就是 .cpp 文件同一个目录），创建一个新的文件并命名为CMakeLists.txt。在这个文件中，你将定义你的本地库（native library）以及它的源文件。下面是一个基本的CMakeLists.txt文件例子：

```txt
# For more information about using CMake with Android Studio, read the
# documentation: https://d.android.com/studio/projects/add-native-code.html

# Sets the minimum version of CMake required to build the native library.

cmake_minimum_required(VERSION 3.10.2)

# Declares and names the project.

project("tctest")

# Creates and names a library, sets it as either STATIC
# or SHARED, and provides the relative paths to its source code.
# You can define multiple libraries, and CMake builds them for you.
# Gradle automatically packages shared libraries with your APK.

add_library( # Sets the name of the library.
        testok

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
        testok

        # Links the target library to the log library
        # included in the NDK.
        ${log-lib})
```

现在我们就来分析一下这个 txt 的文件

​					

```txt
cmake_minimum_required(VERSION 3.10.2)
```

这行代码是用来指定构建本地库所需要的CMake的最小版本号。每个版本都可能带有一些新特性或者对已有特性的改进。因此，如果你的CMake脚本中使用了某个版本特有的特性，你需要指定这个最小版本号，以确保CMake能正确地理解和执行你的脚本。



```txt
project("tctest")
```

就是表示你的项目，你的项目所属的名称就是这个

​			

```txt
add_library( # Sets the name of the library.
        testok

        # Sets the library as a shared library.
        SHARED

        # Provides a relative path to your source file(s).
        native-lib.cpp)
```

add_library：创建一个库

testok：表示这个库的名字叫做，testok 

SHARED：这个库也是一个动态的链接库（也就是生成一个so文件），如果这个地方的内容是 STATIC 那么这个就是一个静态的库，静态库和动态库的区别就是，静态库就是在你编译程序的时候，所有的代码都已经被包含在程序里，你的程序就像是一个可以独立工作的机器，不依赖其他文件。而动态库则是在程序运行的时候才被加载，这就意味着多个程序可以共享同一个库，节省空间，但是如果库丢失或者版本不对，程序可能无法运行。并且 JNI 仅仅支持 动态库，如果你要是用静态库，在编译的时候也会被合并到 动态的链接库当中

native-lib.cpp：源文件的相对路径和名称

​			

```txt
find_library( # Sets the name of the path variable.
        log-lib

        # Specifies the name of the NDK library that
        # you want CMake to locate.
        log)

# Specifies libraries CMake should link to your target library. You
# can link multiple libraries, such as libraries you define in this
# build script, prebuilt third-party libraries, or system libraries.

target_link_libraries( # Specifies the target library.
        astatic

        # Links the target library to the log library
        # included in the NDK.
        ${log-lib})
```

这个就是在链接库

​				

```txt
find_library( # Sets the name of the path variable.
        log-lib

        # Specifies the name of the NDK library that
        # you want CMake to locate.
        log)
```

找到了 log 这个库，并且将这个路径存储在  log-lib 变量当中

​			

```txt 
 target_link_libraries( # Specifies the target library.
        astatic

        # Links the target library to the log library
        # included in the NDK.
        ${log-lib})
```

这个就是把什么（log-lib） 库链接到 目标库当中（astatic）

​			

如果要链接多个怎么办？

```txt
# 查找 log 库
find_library( # Sets the name of the path variable.
        log-lib

        # Specifies the name of the NDK library that
        # you want CMake to locate.
        log)

# 查找 m 库
find_library( # Sets the name of the path variable.
        m-lib

        # Specifies the name of the NDK library that
        # you want CMake to locate.
        m)

# 链接找到的库
target_link_libraries( # Specifies the target library.
        your-target-library

        # Links the target library to the log library
        # and m library included in the NDK.
        ${log-lib}
        ${m-lib})
```



3. 修改 build.gradle 文件

```buid.gradle
android {
    ...
    defaultConfig {
        ...
        externalNativeBuild {
            cmake {
                cppFlags ""
            }
        }
    }

    externalNativeBuild {
        cmake {
            path file('src/main/cpp/CMakeLists.txt')
            version '3.22.1'
        }
    }
    }
}
```

`cmake_minimum_required(VERSION 3.10.2)` 是在 `CMakeLists.txt` 文件中指定的，它表示你的CMake脚本需要至少3.10.2版本的CMake才能正确解析和执行。这是因为CMake的某些功能在不同版本之间可能会有变化，所以你需要指定一个最低版本来保证你的CMake脚本能正确运行。

另一方面，`version '3.22.1'` 是在你的 `build.gradle` 文件中指定的，它告诉Android Studio应该使用哪个版本的CMake来编译你的C++代码。在大多数情况下，你应该使用最新的CMake版本来获取最新的功能和错误修复。			

​				

如果我们想，一次性编译多个so ，也就是 32位的，64位的

那我们需要再 build.gradle 当中添加

```build.gradle
        ndk {
            abiFilters 'armeabi-v7a', 'arm64-v8a', 'x86', 'x86_64'
        }
```

到 defaultConfig 当中

​					

```build.gradle
android {
    namespace 'com.jni.astatic'
    compileSdk 33

    defaultConfig {
        applicationId "com.jni.astatic"
        minSdk 24
        targetSdk 33
        versionCode 1
        versionName "1.0"

        testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
        externalNativeBuild {
            cmake {
                cppFlags '-std=c++17'
            }
        }
        ndk {
            abiFilters 'armeabi-v7a', 'arm64-v8a', 'x86', 'x86_64'
        }
    }

    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
    }
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
    externalNativeBuild {
        cmake {
            path file('src/main/cpp/CMakeLists.txt')
            version '3.22.1'
        }
    }
    buildFeatures {
        viewBinding true
    }
}
```

​				

---

### LLVM简介

[LLVM官网](https://llvm.org)

LLVM 本身是一个模块化的编译器

他能够将任何的语言都，转化为 IR 语言，这个 IR 同时也不针对任何一个硬件平台，能够转化为任意硬件平台的汇编语言



### CLang



























