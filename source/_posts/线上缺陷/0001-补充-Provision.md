[Android首次启动流程解析：Provision.apk与SetupWizard交互 - CSDN文库](https://wenku.csdn.net/doc/3zsip7e2u7?spm=1001.2101.3001.6650.6&utm_medium=distribute.pc_relevant.none-task-c_download-2~default~OPENSEARCH~Rate-6-3zsip7e2u7-blog-138052846.235^v43^pc_blog_bottom_relevance_base7&depth_1-utm_source=distribute.pc_relevant.none-task-c_download-2~default~OPENSEARCH~Rate-6-3zsip7e2u7-blog-138052846.235^v43^pc_blog_bottom_relevance_base7&utm_relevant_index=12)



[android provision apk 分析 - 点点爱梦 - 博客园](https://www.cnblogs.com/liulaolaiu/p/11744495.html)

[[Android\][Framework]Provision-腾讯云开发者社区-腾讯云](https://cloud.tencent.com/developer/article/1341563)

**packages/apps/Provision/src/com/android/provision/DefaultActivity.java**

provision这个唯一的作用就是

这是Android系统内置的一个应用，它的主要任务是在设备第一次启动时设置`DeviceProvisioned`标志。由于`Provision.apk`具有与`Launcher`相同的HOME属性，但优先级更高，因此在开机时首先运行。这个应用没有用户界面，它的目的是确保设备的基本配置完成。在完成设置`DeviceProvisioned`标志后，`Provision.apk`会自我禁用并退出，以便后续的HOME属性应用可以接手。

[Android 自定义开机引导最强篇 provision_android provision-CSDN博客](https://blog.csdn.net/qq_27061049/article/details/131921166)

```xml
            <intent-filter android:priority="1">
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.HOME" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.SETUP_WIZARD" />
            </intent-filter>
```

android:priority代表触发事件的优先级
如果不在pri-app中，这个优先级会被重置0，（-1000，1000）越大越优先，例如这里android.intent.category.HOME让自己成为一个Launcher

android.intent.category.SETUP_WIZARD则是代表系统引导