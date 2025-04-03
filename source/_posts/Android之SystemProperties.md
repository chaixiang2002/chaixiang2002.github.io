### Java工具类的实现

```
frameworks/base/core/java/android/os/
  - SystemProperties.java
frameworks/base/core/jni/
  - android_os_SystemProperties.cpp
```

## C/C++ 层实现

```yml
system/core/init/
  - property_service.cpp   # 属性服务主逻辑
  - properties/           # 属性相关实现
bionic/
  - libc/bionic/          # 系统属性相关
    - system_properties.cpp
frameworks/native/
  - libs/system_properties/ # 属性系统核心
```

共享内存实现跨进程访问，关键数据结构

```cpp
struct prop_area {
    uint32_t bytes_used;
    atomic_uint_least32_t serial;
    uint32_t magic;
    uint32_t version;
    uint32_t reserved[28];
    char data[0];
};

struct prop_bt {
    uint32_t namelen;
    atomic_uint_least32_t prop;
    atomic_uint_least32_t left;
    atomic_uint_least32_t right;
    atomic_uint_least32_t children;
    char name[0];
};

struct prop_info {
    atomic_uint_least32_t serial;
    char value[PROP_VALUE_MAX];
    char name[0];
};
```

### 关键流程

1. **初始化**：
   - `__system_properties_init()` 初始化共享内存区域
   - `property_init()` 在 init 进程中调用
2. **属性读取**：
   - `__system_property_find()` 查找属性
   - `__system_property_read()` 读取属性值
3. **属性设置**：
   - `__system_property_set()` 设置属性值
   - 通过 socket 通知 init 进程处理持久化属性

---

```
frameworks/base/core/java/android/os/SystemProperties.java
    private static native String native_get(String key, String def);
frameworks/base/core/jni/android_os_SystemProperties.cpp   
    SystemProperties_getSS

```

```
frameworks/base/core/java/android/os/SystemProperties.java
    private static native void native_set(String key, String def);
frameworks/base/core/jni/android_os_SystemProperties.cpp
	SystemProperties_set
	
system/libbase/include/android-base/properties.h（走的是）
```

### SystemProperties 底层实现的双重机制解析

```cpp
void SystemProperties_set(JNIEnv *env, jobject clazz, jstring keyJ,
                          jstring valJ)
{
... 
    bool success;
#if defined(__BIONIC__)
    success = !__system_property_set(key.c_str(), value ? value->c_str() : "");
#else
    success = android::base::SetProperty(key.c_str(), value ? value->c_str() : "");
#endif
...
}
```

| 特性       | Bionic 实现 (`__system_property_set`) | 基础库实现 (`android::base::SetProperty`) |
| :--------- | :------------------------------------ | :---------------------------------------- |
| 性能       | 更高（共享内存直接访问）              | 较低（可能需要进程间通信）                |
| 持久化支持 | 完整支持                              | 可能有限                                  |
| 运行环境   | 仅限 Android 系统                     | 可在非 Android 环境使用                   |
| 实现复杂度 | 更复杂                                | 更简单                                    |
| 同步机制   | 原子操作+共享内存                     | 可能使用文件锁等机制                      |
| 权限控制   | 完整 SELinux 集成                     | 可能缺少                                  |

![image-20250331114622147](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202503311146333.png)

使用的是libc的实现







### Libc的实现

bionic/libc/bionic/system_property_set.cpp

```cpp

__BIONIC_WEAK_FOR_NATIVE_BRIDGE
int __system_property_set(const char* key, const char* value) {
  if (key == nullptr) return -1;
  if (value == nullptr) value = "";

  if (g_propservice_protocol_version == 0) {
    detect_protocol_version();
  }

  if (g_propservice_protocol_version == kProtocolVersion1) {
    // Old protocol does not support long names or values
    if (strlen(key) >= PROP_NAME_MAX) return -1;
    if (strlen(value) >= PROP_VALUE_MAX) return -1;

    prop_msg msg;
    memset(&msg, 0, sizeof msg);
    msg.cmd = PROP_MSG_SETPROP;
    strlcpy(msg.name, key, sizeof msg.name);
    strlcpy(msg.value, value, sizeof msg.value);

    return send_prop_msg(&msg);
  } else {
    // New protocol only allows long values for ro. properties only.
    if (strlen(value) >= PROP_VALUE_MAX && strncmp(key, "ro.", 3) != 0) return -1;
    // Use proper protocol
    PropertyServiceConnection connection;
    if (!connection.IsValid()) {
      errno = connection.GetLastError();
      async_safe_format_log(
          ANDROID_LOG_WARN, "libc",
          "Unable to set property \"%s\" to \"%s\": connection failed; errno=%d (%s)", key, value,
          errno, strerror(errno));
      return -1;
    }

    SocketWriter writer(&connection);
    if (!writer.WriteUint32(PROP_MSG_SETPROP2).WriteString(key).WriteString(value).Send()) {
      errno = connection.GetLastError();
      async_safe_format_log(ANDROID_LOG_WARN, "libc",
                            "Unable to set property \"%s\" to \"%s\": write failed; errno=%d (%s)",
                            key, value, errno, strerror(errno));
      return -1;
    }

    int result = -1;
    if (!connection.RecvInt32(&result)) {
      errno = connection.GetLastError();
      async_safe_format_log(ANDROID_LOG_WARN, "libc",
                            "Unable to set property \"%s\" to \"%s\": recv failed; errno=%d (%s)",
                            key, value, errno, strerror(errno));
      return -1;
    }

    if (result != PROP_SUCCESS) {
      async_safe_format_log(ANDROID_LOG_WARN, "libc",
                            "Unable to set property \"%s\" to \"%s\": error code: 0x%x", key, value,
                            result);
      return -1;
    }

    return 0;
  }
}

```

取决于 `g_propservice_protocol_version` 的值，即 **旧协议 (`kProtocolVersion1`)** 和 **新协议**。我们分别分析这两种情况的行为。

| **特性**            | **旧协议 (`kProtocolVersion1`)**  | **新协议 (`kProtocolVersion2`)**         |
| ------------------- | --------------------------------- | ---------------------------------------- |
| **最大 Key 长度**   | 受 `PROP_NAME_MAX` 限制           | 受 `PROP_NAME_MAX` 限制                  |
| **最大 Value 长度** | 受 `PROP_VALUE_MAX` 限制          | 仅 `ro.*` 属性支持更长值                 |
| **通信方式**        | **消息队列**（`send_prop_msg()`） | **Socket** (`PropertyServiceConnection`) |
| **协议版本**        | `PROP_MSG_SETPROP`                | `PROP_MSG_SETPROP2`                      |
| **失败处理**        | 返回 `-1`                         | 记录日志，返回 `-1`                      |
| **日志记录**        | 无日志                            | 使用 `async_safe_format_log()` 记录日志  |

![image-20250331145156692](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202503311451011.png)

用的新协议