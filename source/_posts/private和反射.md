[面试官：private 可以通过反射访问，那么 private 的意义是什么？-腾讯云开发者社区-腾讯云](https://cloud.tencent.com/developer/article/1949972)

- private修饰的成员和方法不能被外部访问
- 反射是为了外部可以调用对象的私有方法和成员



意义：

- 食堂厨房门前的“闲人免进”的牌子，Java的private修饰符不是为了绝对安全设计的，而是对用户常规使用Java的一种约束





[**Constructor：**](https://cloud.tencent.com/developer/tools/blog-entry?target=http%3A%2F%2Fmp.weixin.qq.com%2Fs%3F__biz%3DMzI3ODcxMzQzMw%3D%3D%26mid%3D2247546398%26idx%3D2%26sn%3D57f74b2c88499238e85d4fd1399e3edc%26chksm%3Deb50b328dc273a3ec6090897af40ccf10a1bd0fcfdea046efd306c77dc2c12f6482ac639cfe4%26scene%3D21%23wechat_redirect&objectId=1949972&objectType=1&isNewArticle=undefined)

[代表类的单个构造方法，通过Constructor我们可执行一个类的某个构造方法（有参或者无参）来创建对象时。](https://cloud.tencent.com/developer/tools/blog-entry?target=http%3A%2F%2Fmp.weixin.qq.com%2Fs%3F__biz%3DMzI3ODcxMzQzMw%3D%3D%26mid%3D2247546398%26idx%3D2%26sn%3D57f74b2c88499238e85d4fd1399e3edc%26chksm%3Deb50b328dc273a3ec6090897af40ccf10a1bd0fcfdea046efd306c77dc2c12f6482ac639cfe4%26scene%3D21%23wechat_redirect&objectId=1949972&objectType=1&isNewArticle=undefined)

[**Method：**](https://cloud.tencent.com/developer/tools/blog-entry?target=http%3A%2F%2Fmp.weixin.qq.com%2Fs%3F__biz%3DMzI3ODcxMzQzMw%3D%3D%26mid%3D2247546398%26idx%3D2%26sn%3D57f74b2c88499238e85d4fd1399e3edc%26chksm%3Deb50b328dc273a3ec6090897af40ccf10a1bd0fcfdea046efd306c77dc2c12f6482ac639cfe4%26scene%3D21%23wechat_redirect&objectId=1949972&objectType=1&isNewArticle=undefined)

[代表类中的单个方法，可以用于执行类的某个普通方法，有参或无参，并可以接收返回值。](https://cloud.tencent.com/developer/tools/blog-entry?target=http%3A%2F%2Fmp.weixin.qq.com%2Fs%3F__biz%3DMzI3ODcxMzQzMw%3D%3D%26mid%3D2247546398%26idx%3D2%26sn%3D57f74b2c88499238e85d4fd1399e3edc%26chksm%3Deb50b328dc273a3ec6090897af40ccf10a1bd0fcfdea046efd306c77dc2c12f6482ac639cfe4%26scene%3D21%23wechat_redirect&objectId=1949972&objectType=1&isNewArticle=undefined)

[**Field：**](https://cloud.tencent.com/developer/tools/blog-entry?target=http%3A%2F%2Fmp.weixin.qq.com%2Fs%3F__biz%3DMzI3ODcxMzQzMw%3D%3D%26mid%3D2247546398%26idx%3D2%26sn%3D57f74b2c88499238e85d4fd1399e3edc%26chksm%3Deb50b328dc273a3ec6090897af40ccf10a1bd0fcfdea046efd306c77dc2c12f6482ac639cfe4%26scene%3D21%23wechat_redirect&objectId=1949972&objectType=1&isNewArticle=undefined)

[代表类中的单个属性，用于set或get属性](https://cloud.tencent.com/developer/tools/blog-entry?target=http%3A%2F%2Fmp.weixin.qq.com%2Fs%3F__biz%3DMzI3ODcxMzQzMw%3D%3D%26mid%3D2247546398%26idx%3D2%26sn%3D57f74b2c88499238e85d4fd1399e3edc%26chksm%3Deb50b328dc273a3ec6090897af40ccf10a1bd0fcfdea046efd306c77dc2c12f6482ac639cfe4%26scene%3D21%23wechat_redirect&objectId=1949972&objectType=1&isNewArticle=undefined)

```java
public static void main(String[] args)  throws Exception {

    Reflect reflect = new Reflect("a");

    Method[] methods = Reflect.class.getMethods();
    Field[] fields = Reflect.class.getDeclaredFields();

    for (int i = 0; i < fields.length; i ++) {
        fields[i].setAccessible(true);
        System.out.println(fields[i].getName());
    }

    for (int j = 0; j < methods.length; j ++) {
        methods[j].setAccessible(true);
        System.out.println(methods[j].getName());

        methods[j].invoke(reflect);
        System.out.println(methods[j].getName());
    }
}
```

