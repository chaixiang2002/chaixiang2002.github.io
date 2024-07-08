在AOSP 10项目中，`StorageManagerService` 是负责管理设备存储的服务。它处理存储卷（如SD卡和USB驱动器）的挂载、卸载和格式化等操作。以下是 `StorageManagerService`的架构以及从应用层到底层的相关目录、文件和核心函数。

### 1. 应用层

应用层通常通过 `StorageManager`类与存储管理服务交互。

- **目录**: `frameworks/base/core/java/android/os/storage/`
- **文件**: `StorageManager.java`

```java
public class StorageManager {
    // 核心函数
    public VolumeInfo findVolumeById(String id) {
        // 查找指定ID的卷
    }

    public List<VolumeInfo> getVolumes() {
        // 获取所有存储卷信息
    }

    public List<DiskInfo> getDisks() {
        // 获取所有磁盘信息
    }

    public void mount(String volId) {
        // 挂载指定卷
    }

    public void unmount(String volId) {
        // 卸载指定卷
    }
}
```

### 2. 系统服务层

系统服务层中的 `StorageManagerService`负责处理来自应用层的请求，并执行相应的存储操作。

- **目录**: `frameworks/base/services/core/java/com/android/server/storage/`
- **文件**: `StorageManagerService.java`

```java
public class StorageManagerService extends IStorageManager.Stub {
    // 核心函数
    private void mount(String volId, int mountFlags, int mountUserId) {
        // 挂载指定卷
    }

    private void unmount(String volId) {
        // 卸载指定卷
    }

    private void format(String volId) {
        // 格式化指定卷
    }

    private void onUserAdded(int userId) {
        // 处理新用户添加
    }

    private void onUserRemoved(int userId) {
        // 处理用户删除
    }
}
```

### 3. JNI层

JNI层通过JNI接口与底层的原生代码进行交互，执行具体的存储操作。

- **目录**: `frameworks/base/services/core/jni/`
- **文件**: `com_android_server_storage_StorageManagerService.cpp`

```cpp
static void android_server_storage_StorageManagerService_mount(JNIEnv* env, jobject clazz, jstring volId, jint mountFlags, jint mountUserId) {
    // 调用底层C++函数挂载卷
}

static void android_server_storage_StorageManagerService_unmount(JNIEnv* env, jobject clazz, jstring volId) {
    // 调用底层C++函数卸载卷
}

static void android_server_storage_StorageManagerService_format(JNIEnv* env, jobject clazz, jstring volId) {
    // 调用底层C++函数格式化卷
}
```

### 4. 底层服务层

底层服务层通常由 `Vold`（Volume Daemon）守护进程负责，处理实际的存储设备管理操作。

- **目录**: `system/vold/`
- **文件**: `VolumeManager.cpp`, `VolumeManager.h`, `Volume.cpp`, `Volume.h`

```cpp
class VolumeManager {
public:
    // 核心函数
    int mountVolume(const std::string& volId, int mountFlags) {
        // 挂载卷
    }

    int unmountVolume(const std::string& volId) {
        // 卸载卷
    }

    int formatVolume(const std::string& volId) {
        // 格式化卷
    }

    // 其他管理函数
};
```

### 5. 文件系统层

文件系统层由Linux内核提供支持，处理具体的文件系统操作。

- **目录**: 位于内核源码中，与文件系统相关的代码分散在多个子目录中，如 `fs/`, `block/` 等。

### 6. HAL层

硬件抽象层（HAL）提供标准接口，供上层服务调用实际硬件操作。

- **目录**: `hardware/interfaces/storage/`
- **文件**: 例如 `IStorage.hal`

```hal
interface IStorage {
    // 核心函数
    mountVolume(string volId, int mountFlags);
    unmountVolume(string volId);
    formatVolume(string volId);
}
```

### 总结

`StorageManagerService`的架构从上至下包括应用层、系统服务层、JNI层、底层服务层、文件系统层和HAL层。每一层通过接口和服务调用实现存储管理操作，确保整个存储系统的稳定和高效运行。





---






在AOSP 10中，负责搜索和管理所有存储设备的主要组件是 `Vold`（Volume Daemon）。`Vold`处理对存储设备的检测和管理。具体来说，`Vold`中的 `VolumeManager`类负责管理和跟踪系统中的所有存储设备。

在 `VolumeManager`类中，主要负责搜索和管理所有存储设备的函数是 `VolumeManager::start`和 `VolumeManager::addDisk`。

### 1. `VolumeManager::start` 函数

`VolumeManager::start`函数会初始化存储管理系统，并启动对存储设备的检测。

- **目录**: `system/vold/`
- **文件**: `VolumeManager.cpp`

```cpp
int VolumeManager::start() {
    // 初始化并启动存储管理系统
    mBroadcaster = new NetlinkHandler();
    mBroadcaster->start();

    // 扫描现有的设备
    processConfig();

    // 启动Uevent处理器以监视存储设备的变化
    mUeventHandler = new UeventHandler();
    mUeventHandler->start();

    return 0;
}
```

### 2. `VolumeManager::addDisk` 函数

`VolumeManager::addDisk`函数会处理新检测到的磁盘设备，并将其添加到管理列表中。

- **目录**: `system/vold/`
- **文件**: `VolumeManager.cpp`

```cpp
void VolumeManager::addDisk(const std::shared_ptr<Disk>& disk) {
    // 添加新检测到的磁盘设备到管理列表中
    mDisks[disk->getId()] = disk;
    disk->create();
}
```

### 3. UeventHandler 类

`UeventHandler`类负责处理来自内核的Uevent消息，当系统检测到新的存储设备时，会触发相应的处理函数。

- **目录**: `system/vold/`
- **文件**: `UeventHandler.cpp`

```cpp
void UeventHandler::handleBlockEvent(NetlinkEvent* evt) {
    // 处理块设备事件，如添加、移除存储设备
    if (evt->getAction() == NetlinkEvent::NlActionAdd) {
        // 添加设备
        VolumeManager::Instance()->handleBlockAdd(evt);
    } else if (evt->getAction() == NetlinkEvent::NlActionRemove) {
        // 移除设备
        VolumeManager::Instance()->handleBlockRemove(evt);
    }
}
```

### 核心流程

1. **初始化和启动**: 在 `VolumeManager::start`函数中，系统会初始化并启动存储管理系统，开始扫描现有设备和启动Uevent处理器以监视设备变化。
2. **处理设备添加事件**: 当有新的存储设备连接到系统时，`UeventHandler`类会处理来自内核的设备添加事件，并调用 `VolumeManager::handleBlockAdd`函数。
3. **添加设备到管理列表**: 在 `VolumeManager::handleBlockAdd`函数中，会创建新的 `Disk`对象，并调用 `VolumeManager::addDisk`将其添加到管理列表中。

通过上述流程，`Vold`可以动态地检测和管理系统中的所有存储设备。具体的代码实现集中在 `VolumeManager`和 `UeventHandler`类中，这些类位于 `system/vold/`目录下。

































从你提供的日志来看，`StorageManagerService`在执行过程中发生了 `android.os.ServiceSpecificException`错误，这主要发生在尝试挂载存储设备时。

### 代码位置分析

1. **`IVold`接口**：
   `IVold` 是一个与存储管理相关的接口，定义了各种与Vold守护进程（Volume Daemon）通信的方法。该错误显示在 `IVold$Stub$Proxy.mount(IVold.java:1565)`处，表示在Vold的挂载方法中出现了问题。
2. **`StorageManagerService`类**：
   `StorageManagerService`负责管理设备的存储相关任务，包括挂载、卸载、格式化等操作。

### 具体代码位置

根据错误日志，可以确定调用链如下：

- `IVold$Stub$Proxy.mount(IVold.java:1565)`
- `StorageManagerService.mount(StorageManagerService.java:1816)`

在AOSP源码中找到相关代码：

1. **`StorageManagerService`类**：

   该类位于：

   ```
   frameworks/base/services/core/java/com/android/server/StorageManagerService.java
   ```
2. **`mount`方法**：

   打开 `StorageManagerService.java`文件，找到以下代码段：

   ```java
   public void mount(String volId, int mountFlags, int mountUserId) {
       try {
           mVold.mount(volId, mountFlags, mountUserId);
       } catch (Exception e) {
           throw new RuntimeException("Failed to mount volume " + volId, e);
       }
   }
   ```
3. **`IVold`接口**：

   该接口位于：

   ```
   frameworks/base/core/java/android/os/IVold.aidl
   ```

   在这个文件中定义了各种存储相关操作的方法，其中包括 `mount`方法。

### 问题分析

从日志来看，问题出在 `mount`方法调用上。具体的错误代码为 `android.os.ServiceSpecificException: (code -5)`。通常，这类错误可能是由于权限、文件系统损坏、设备不支持或设备不可用等原因引起的。

### 调试建议

1. **检查设备状态**：确认设备是否连接正常且支持被挂载。
2. **检查权限**：确保应用和进程有足够的权限执行挂载操作。
3. **查看详细日志**：进一步查看系统日志，找到更多与 `Vold`相关的信息，以便更好地定位问题。
4. **代码审查**：查看 `StorageManagerService`和 `IVold`相关代码，确保逻辑正确无误。

希望这些信息能帮到你解决问题。如果需要进一步调试或分析具体问题，建议深入查看与存储管理相关的代码和文档。
