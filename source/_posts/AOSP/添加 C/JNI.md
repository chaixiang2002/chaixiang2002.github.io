[JNI 编程上手指南之 HelloWorld 实战 - 掘金 (juejin.cn)](https://juejin.cn/post/7243016090818068539)

development/samples/SimpleJNI

##### HelloJNI.java

```java
public class HelloJNI {
    static {
        System.loadLibrary("hello");
    }

    private native String Hellocx();

    public static void main(String[] args) {
       String a= new HelloJNI().Hellocx();
       System.out.println(a);
    }
}

```

### 生成.h

/snow/android10/prebuilts/jdk/jdk9/linux-x86/bin/javac -h .  HelloJNI.java

##### HelloJNI.c

```
#include "HelloJNI.h"
#include <stdio.h>
#include <jni.h>

//方法名要和 Java 层包名对应上
JNIEXPORT jstring JNICALL Java_HelloJNI_Hellocx(JNIEnv *env, jobject obj)
{
    return (*env)->NewStringUTF(env,"Hello i am chaixiang ,leaning JNI !");
}

```

### 编译

gcc -fpic -I"/snow/android10/prebuilts/jdk/jdk9/linux-x86/include/" -I"/snow/android10/prebuilts/jdk/jdk9/linux-x86/include/linux/" -shared -o libhello.so HelloJNI.c

### 测试demo

/snow/android10/prebuilts/jdk/jdk9/linux-x86/bin/java -Djava.library.path=. HelloJNI

**目前属于静态注册**



### `LOCAL_MODULE_TAGS` 变量

`LOCAL_MODULE_TAGS` 是一个标识模块标签的变量。它通常用于描述模块的使用场景和发布级别。这个变量可以接受多个标签，如 `tests`、`debug`、`eng`、`samples` 等。每个标签有特定的用途和含义。

### `samples` 标签

在这个语句中，`samples` 是 `LOCAL_MODULE_TAGS` 的值，表示该模块属于示例模块。通常情况下，`samples` 标签用于标识一些示例程序或演示模块。这些模块通常不是核心系统的一部分，而是提供给开发者作为参考或学习资源。


---

1. src
   有一个JNI类，

   ```java
       static {
           System.loadLibrary("snowjni");
       }

       static native String hello(int a, int b);
   ```
2. jni





---

# JNI静态注册和动态注册

在 Android 系统开发中，JNI（Java Native Interface）用于在 Java 层和 C/C++ 层之间进行交互。JNI 注册机制主要分为 **动态注册** 和 **静态注册**，两者有各自不同的使用场景和原理。

### 1. 静态注册（Static Registration）

静态注册是通过 Java 层的类加载机制在应用启动时进行注册。C/C++ 代码中会提前指定好要映射到 Java 方法的名称和签名，然后通过 JNI 提供的 API (`RegisterNatives`) 注册原生方法。

#### 实现方式：

静态注册需要通过 `JNI_OnLoad` 函数进行注册。在这个函数中，你需要用 `RegisterNatives` 函数明确指定 Java 类与 C/C++ 方法的映射关系。代码结构如下：

```cpp
#include <jni.h>

static JNINativeMethod gMethods[] = {
    {"nativeMethod", "()V", (void *)nativeMethod}
};

JNIEXPORT jint JNICALL JNI_OnLoad(JavaVM *vm, void *reserved) {
    JNIEnv *env;
    jint result = JNI_ERR;

    if (vm->GetEnv((void **) &env, JNI_VERSION_1_6) != JNI_OK) {
        return JNI_ERR;
    }

    jclass clazz = env->FindClass("com/example/MyClass");
    if (clazz == NULL) {
        return JNI_ERR;
    }

    result = env->RegisterNatives(clazz, gMethods, sizeof(gMethods) / sizeof(gMethods[0]));
    if (result < 0) {
        return JNI_ERR;
    }

    return JNI_VERSION_1_6;
}
```

#### 使用场景：

- **启动时注册**：静态注册一般用于那些在应用启动时就需要初始化并且映射关系已知的原生方法。
- **性能优化**：静态注册由于是在应用启动时完成的注册，性能上较为稳定，不需要在运行时动态查找方法签名。
- **代码稳定性**：如果你能够确保所有的原生方法都是在编译时就确定的，静态注册非常适合。

### 2. 动态注册（Dynamic Registration）

动态注册则是通过在 Java 层加载类后，在运行时根据实际情况注册原生方法。你可以在任何时刻通过 JNI 动态加载并注册方法。这意味着，原生方法的注册可以延迟到实际调用时才发生。

#### 实现方式：

动态注册不依赖于 `JNI_OnLoad`，而是在代码中手动调用 `RegisterNatives` 方法。其注册过程类似于静态注册，但是可以灵活地控制何时注册原生方法。

```cpp
#include <jni.h>

extern "C" JNIEXPORT void JNICALL
Java_com_example_MyClass_registerNative(JNIEnv *env, jclass clazz) {
    static JNINativeMethod gMethods[] = {
        {"nativeMethod", "()V", (void *)nativeMethod}
    };

    env->RegisterNatives(clazz, gMethods, sizeof(gMethods) / sizeof(gMethods[0]));
}
```

#### 使用场景：

- **运行时灵活性**：动态注册通常用于需要按需加载原生方法的场景，例如插件化架构或动态生成的方法映射。
- **动态库加载**：当原生库在运行时才加载时，动态注册可以按需注册本地方法，而不是在启动时就完成。
- **模块化和扩展性**：如果你需要根据不同的情况或条件注册不同的原生方法，可以使用动态注册，便于实现模块化和可扩展性。

### 总结：

- **静态注册**：在应用启动时完成注册，适用于映射关系已知且不需要变化的场景，性能稳定，启动时有一定的初始化成本。
- **动态注册**：注册时机灵活，可以根据运行时的需求按需进行注册，适合插件化、模块化或动态库加载等需求。

两者的选择主要依赖于应用的需求和架构设计，静态注册适用于大多数常规场景，而动态注册则适用于更复杂或需要灵活性的场景。

我们接下来看个动态注册的例子吧

java层： com/example/ndk/NativeTest.java

```java
package com.example.ndk;

public class NativeTest {
    static {
      System.loadLibrary("nativetest"); 
    }
    public native void init();

    public native void init(int age);

    public native boolean init(String name);

    public native void update();
}
```

C 层的实现主要有三步：

- 实现 java 层本地方法
- 构建一个 JNINativeMethod 类型的数组
- 注册本地函数

NativeTest.c :

```c++
#include <jni.h>
#include <stdio.h>

#ifdef __cplusplus
extern "C" {
#endif

//1 实现 java 层本地方法
JNIEXPORT void JNICALL
c_init1(JNIEnv *env, jobject thiz) {
     printf("c_init1\n");
}
  
JNIEXPORT void JNICALL
c_init2(JNIEnv *env, jobject thiz, jint age) {
    printf("c_init2\n");
}
  
JNIEXPORT jboolean JNICALL
c_init3(JNIEnv *env, jobject thiz, jstring name) {
    printf("c_init3\n");
}
 
JNIEXPORT void JNICALL
c_update(JNIEnv *env, jobject thiz) {
    printf("c_update\n");
}

#ifdef __cplusplus
}
#endif


// typedef struct {
// 	//Java层native方法名称
//    const char* name;
// 	//方法签名
//    const char* signature;
// 	//native层方法指针
//    void*       fnPtr;
// } JNINativeMethod;

//2 构建 JNINativeMethod 数组
//中间的方法签名看上去有点怪异，后面我们来讲它的命名规则
static JNINativeMethod methods[] = {
        {"init", "()V", (void *)c_init1},
        {"init", "(I)V", (void *)c_init2},
        {"init", "(Ljava/lang/String;)Z", (void *)c_init3},
        {"update", "()V", (void *)c_update},
};

/**
 * 3 完成动态注册的入口函数
 *  其内容基本固定
 */ 
JNIEXPORT jint JNICALL
JNI_OnLoad(JavaVM *vm, void *reserved) {
    JNIEnv *env = NULL;
    jint result = -1;
 
    // 获取JNI env变量
    if (vm->GetEnv((void**) &env, JNI_VERSION_1_6) != JNI_OK) {
        // 失败返回-1
        return result;
    }
 
    // 获取native方法所在类
    const char* className = "com/example/ndk/NativeTest";
    jclass clazz = env->FindClass(className);
    if (clazz == NULL) {
        return result;
    }
 
    // 动态注册native方法
    if (env->RegisterNatives(clazz, methods, sizeof(methods) / sizeof(methods[0])) < 0) {
        return result;
    }
 
    // 返回成功
    result = JNI_VERSION_1_6;
    return result;
}
```

JNINativeMethod 第二个成员变量是方法签名

# 为何要使用动态注册

[JNI静态注册与动态注册：概念、优缺点与使用场景](https://cloud.baidu.com/article/2715590)

- 静态注册需要在编译时确定本地方法的名称和签名，因此很难在运行时动态地添加或修改本地方法。

- 静态注册会导致本地代码与Java类紧密耦合，不利于代码的模块化和复用。

- 动态注册是指在运行时根据Java类和本地方法的描述信息动态地创建本地方法表。这种方式不需要在编译时确定本地方法的名称和签名，而是在运行时动态地添加或修改本地方法。
- 性能开销：动态注册需要额外的运行时开销，因为需要在运行时创建本地方法表