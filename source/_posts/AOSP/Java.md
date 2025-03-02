 **Java Lambda**

```java
// 使用 Lambda 表达式计算两个数的和
MathOperation addition = (a, b) -> a + b;

// 调用 Lambda 表达式
int result = addition.operation(5, 3);
System.out.println("5 + 3 = " + result);
```



```java
// 传统的匿名内部类
Runnable runnable1 = new Runnable() {
    @Override
    public void run() {
        System.out.println("Hello World!");
    }
};

// 使用 Lambda 表达式
Runnable runnable2 = () -> System.out.println("Hello World!");
```

