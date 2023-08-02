C++ 当中重定义的一些数据类型

```C++
typedef uint8_t  jboolean; /* unsigned 8 bits */
typedef int8_t   jbyte;    /* signed 8 bits */
typedef uint16_t jchar;    /* unsigned 16 bits */
typedef int16_t  jshort;   /* signed 16 bits */
typedef int32_t  jint;     /* signed 32 bits */
typedef int64_t  jlong;    /* signed 64 bits */
typedef float    jfloat;   /* 32-bit IEEE 754 */
typedef double   jdouble;  /* 64-bit IEEE 754 */
```

​			

call 调用一个方法

```C++
    jobject     (*CallObjectMethod)(JNIEnv*, jobject, jmethodID, ...);
```

* 调用一个方法，返回值是一个 object 

* 第一个参数是 JNIEnv 指针

* 第二个参数是，指向当前的类

* 第三个参数是 jmethodID （需要先获取 methodID）

  * ```java
    jmethodID   (*GetMethodID)(JNIEnv*, jclass, const char*, const char*);
    ```

  * 第一个参数是 JNIEnv 指针 

  * 第二个参数是 jclass 

    * ```C++
      jclass      (*FindClass)(JNIEnv*, const char*);
      ```

    * 第一个参数是 JNIEnv 指针 

    *  第二个参数，是类的路径 

  * 第三个参数是，函数的名字

  * 第四个参数是，函数的签名（是不包含函数的名字）

* 第四个参数是（函数的参数）

get

set



获取一个 Java 的字段

```C++
jobject     (*GetObjectField)(JNIEnv*, jobject, jfieldID);
```

* ```C++
  jfieldID    (*GetFieldID)(JNIEnv*, jclass, const char*, const char*);
  ```

  * 第一个参数是 JNIEnv 指针 

  * ```java
    jclass      (*FindClass)(JNIEnv*, const char*);
    ```

    * 第二个参数是类的路径

  * 字段的名字

  * 字段的签名（包括名字吗？？）

设置一个 Java 的字段

```java
    void        (*SetObjectField)(JNIEnv*, jobject, jfieldID, jobject);
```

第二个参数和第四个参数 ？？



### 静态注册

```
extern "C"
JNIEXPORT void JNICALL
Java_com_ui_home_Mainacitivity(JNIEnv *env, jclass obj)
```





```C++
jstring     (*NewStringUTF)(JNIEnv*, const char*);
```

​		



```C++
jstring     (*NewString)(JNIEnv*, const jchar*, jsize);
```

​				

编译 so 文件

---

获取 Java 层的实例字符串的内容

```C++
jobject     (*GetObjectField)(JNIEnv*, jobject, jfieldID);
```



```C++
jfieldID    (*GetFieldID)(JNIEnv*, jclass, const char*, const char*);
```

第二个参数是，字段的变量名

第三个参数是，数据类型的签名



```C++
jclass      (*FindClass)(JNIEnv*, const char*);
```

第二个参数是，类的路径







获取静态变量的内容

```C++
jobject     (*GetStaticObjectField)(JNIEnv*, jclass, jfieldID);
```



第二个参数

```C++
jclass      (*FindClass)(JNIEnv*, const char*);
```



第三个参数

```C++
jfieldID    (*GetStaticFieldID)(JNIEnv*, jclass, const char*,
                    const char*);
```

第二个参数是 变量的内容

第三个参数的内容是 变量的签名

----

so层调用实例方法和静态方法



---

动态注册

 

```C++
typedef struct {
    const char* name;
    const char* signature;
    void*       fnPtr;
} JNINativeMethod;
```



```C++
JINativeMethod nativeMethod[]= {
{"add", " (FF) F", a (void*) addch},
{"sub", " (FF) F" (void*) subc},
{"mul", " (FF) F", (void*)mulc} 
{"div", " (FF)F", ....
(void*) dovI
```









