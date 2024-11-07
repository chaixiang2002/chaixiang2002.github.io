[JNI 编程上手指南之 HelloWorld 实战 - 掘金 (juejin.cn)](https://juejin.cn/post/7243016090818068539)

development/samples/SimpleJNI

##### HelloJNI.java

```
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
