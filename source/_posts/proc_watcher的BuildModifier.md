这个代码实现了在 Android 系统中修改 `Build` 和 `Build.VERSION` 类静态字段的功能。具体来说，它通过 JNI 操作，动态修改系统属性（如 `ro.build.*`、`ro.product.*` 等），这些属性通常在设备启动时由 Android 系统读取，并作为设备信息的一部分。它的主要功能是根据外部的配置信息，动态地更新这些字段，通常用于某些定制化的需求或调试目的。

### 主要功能解析：

1. **`BuildModifier` 类**：
   - 该类主要用于修改 `android.os.Build` 和 `android.os.Build.VERSION` 类的静态字段。它通过 JNI 获取到这些类的字段（如 `ro.build.id`、`ro.build.version.release` 等），并根据需要修改这些字段的值。
   - 它通过 `apply()` 方法读取配置文件或外部数据源，解析并应用配置更新。
2. **`getApplyproperties()` 方法**：
   - 这个方法通过与 `/data/system/s9_sock` 的套接字连接，获取配置数据（key-value 键值对），这些配置决定了将要更新的 `Build` 和 `Build.VERSION` 字段。
   - 然后，`apply()` 方法会遍历这些配置并根据配置更新相应的字段。
3. **静态字段的修改**：
   - 通过 JNI，`setStringValue`、`setStringArrayValue`、`setLongValue` 等方法分别针对不同类型的字段（字符串、布尔值、长整型等）进行设置。
   - 根据字段类型（如 `[Ljava/lang/String;`、`Ljava/lang/String;`、`I` 等），不同的 setter 函数会被调用来更新静态字段的值。
4. **`lookupSignBuild()` 和 `lookupSignVersion()` 方法**：
   - 这两个方法会根据输入的 `key`（如 `ro.build.id`）查找相应的字段名、常量名和类型，确保正确找到要更新的字段。
   - 如果找到了匹配的字段，就会通过 JNI 设置新的值。
5. **socket 通信**：
   - 通过一个自定义的 `SocketConnection` 类与一个 socket (`/data/system/s9_sock`) 通信，获取到配置信息。这种方式通常用于某些需要动态更新系统信息的场景，比如从外部应用或模块获取动态的配置信息。

### 这个功能可能的应用场景：

- **系统定制化**：某些定制 Android 系统的场景，可能需要动态修改 `Build` 或 `Build.VERSION` 中的一些字段。例如，修改 `ro.build.fingerprint` 来模拟不同的设备或不同的版本号。
- **调试和测试**：开发人员可能需要修改这些字段来模拟不同的设备状态或者版本信息，用于调试、测试或兼容性验证。
- **设备虚拟化或模拟**：例如在某些虚拟化环境中，通过修改这些字段来伪装成不同型号的设备。
- **设备信息伪造**：一些应用可能需要在设备信息上进行伪造，修改设备的型号、制造商、硬件版本等信息。

### 总结：

该代码实现了在应用启动后，通过 JNI 修改 Android 系统中 `Build` 和 `Build.VERSION` 类的静态字段，通常用于动态更新系统属性、模拟不同的设备状态或版本，或者在定制 Android 系统时进行修改。它通过套接字与外部数据源进行通信，获取配置信息，并应用到系统属性中。



























-----

信息发送端

```

12-05 15:55:21.565    80    80 W         : 0001| Read socket err: Try again
12-05 15:55:21.565    80    80 W         : 0001| Write socket message: 0006!prop:0
12-05 15:55:21.565    80    80 W         : 0001|  BuildModifier.cpp socket.request err:
12-05 15:55:21.581  2536  2536 W         : 0001| Write socket message succeeful: 10|root:10093
```



vendor/ntimespace/Space9dService/src/com/android/server/MessageHandler.java

```java
    private boolean onInternalMessage(LocalSocket socket, String data) {
        if (data.startsWith("prop:")) {
            Properties properties = mService.getModuleManager().getSysProp(false);
            StringBuffer buffer = new StringBuffer();
            Set<String> keys = properties.stringPropertyNames();
            if (keys.size() > 0) {
                for (String key : keys) {
                    buffer.append(key).append('=').append(properties.getProperty(key).toString());
                }
                buffer.deleteCharAt(buffer.length() - 1);
            }
            getServer().send(socket, buffer.toString());
            return true;
        }
        return false;
    }
```

public void onMessageReceive(LocalSocket socket, String data) {



vendor/ntimespace/Space9dService/src/com/android/server/ServerSocket.java

private void handleClient(LocalSocket socket) {

```
                    //! 处理特殊的 "CNCT" 消息，将新客户端添加到客户端列表。
                    // 握手逻辑
                    if ("CNCT".equals(message)) {
                        if (!mClients.contains(socket)) {
                            mClients.add(socket);
                        } else {
                            Slog.w(TAG, "link has been established.");
                        }
                    } else {
                    //! 读取消息内容，并将其传递给 MessageListener
                        mListener.onMessageReceive(socket, message);
                    }
```





![image-20241205173828414](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20241205173828414.png)



![image-20241205173916692](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20241205173916692.png)



没有回应的原因
mClients.contains(socket)   没有包含整个socket