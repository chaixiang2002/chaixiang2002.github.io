以下是 Android 12 (AOSP) 应用权限设计的整体框架解析，重点围绕**运行时权限**和**安装时权限**的设计逻辑和实现机制：

---

### 一、权限分类与设计原则
Android 的权限模型旨在通过分层控制保护用户隐私和系统安全。在 AOSP 12 中，权限主要分为以下两类：

#### 1. **安装时权限（Install-Time Permissions）**
- **定义**：在应用安装时自动授予的权限，无需用户主动确认。
- **子类**：
  - **普通权限（Normal Permissions）**：低风险权限（如 `SET_WALLPAPER`），仅需在 `AndroidManifest` 中声明即可自动授予。
  - **签名权限（Signature Permissions）**：仅当应用与声明权限的组件（如系统或同一签名应用）匹配时自动授予。
- **适用场景**：用于访问对系统或其他应用影响较小的功能（如网络状态查询）。

#### 2. **运行时权限（Runtime Permissions）**
- **定义**：需要用户在应用运行时动态授权的危险权限（如 `CAMERA`、`LOCATION`），涉及用户隐私或敏感数据。
- **特点**：
  - **动态请求**：通过 `requestPermissions()` 触发系统弹窗，用户可选择“始终允许”“仅使用时允许”或“拒绝”。
  - **按需申请**：推荐在用户触发相关功能时请求（如点击拍照按钮时请求相机权限）。
- **权限组**：权限按逻辑分组（如 `STORAGE` 组包含读写权限），用户授予组内任一权限后，同组其他权限可自动授予（但此行为可能随版本变化）。

---

### 二、权限框架实现机制
#### 1. **权限声明与检查**
- **声明**：所有权限需在 `AndroidManifest.xml` 中声明，否则系统会忽略请求。
- **检查**：通过 `checkSelfPermission()` 验证权限是否已授予，返回 `PERMISSION_GRANTED` 或 `PERMISSION_DENIED`。

#### 2. **权限授予策略**
- **默认处理程序**：系统核心功能（如默认拨号应用）可通过 `DefaultPermissionGrantPolicy` 预授予权限，确保基本功能可用。
- **特权应用**：预装系统应用（如 `priv-app`）默认拥有所有权限，但用户仍可手动撤销。

#### 3. **运行时权限的兼容性处理**
- **目标 SDK 版本**：
  - **targetSdkVersion < 23**：危险权限在安装时自动授予（兼容旧版本）。
  - **targetSdkVersion ≥ 23**：强制使用运行时权限模型。
- **用户撤销权限**：用户可在系统设置中随时撤销已授予的权限，应用需处理 `SecurityException` 等异常。

---

### 三、AOSP 权限管理的核心组件
#### 1. **PackageManagerService**
- **职责**：管理应用安装、权限授予及状态持久化（如写入 `packages.xml`）。
- **关键流程**：
  - **安装阶段**：解析 `AndroidManifest` 中的权限声明，根据类型（普通/签名）自动授予。
  - **运行时授权**：处理用户动态授权的请求，更新权限状态。

#### 2. **PermissionController**
- **作用**：独立的系统应用，负责显示权限弹窗、管理权限设置界面。
- **自定义限制**：支持通过 `DefaultPermissionGrantPolicy` 配置例外（如预装应用的默认权限）。

#### 3. **权限策略文件**
- **default-permissions.xml**：定义系统预装应用的默认权限（如默认相机应用的 `CAMERA` 权限）。
- **permissions.xml**：声明系统级权限及其保护级别（如 `signature` 或 `dangerous`）。

---

### 四、特殊权限与限制
#### 1. **硬性限制（Hard Restrictions）**
- **定义**：某些权限（如 `SMS`）必须通过系统许可名单（Allowlist）授予，否则无法使用。
- **适用场景**：仅限预装应用或特定系统组件（如默认短信应用）。

#### 2. **软性限制（Soft Restrictions）**
- **定义**：未列入许可名单的应用仍可请求权限，但需遵循更严格的审核策略。

---

### 五、开发者最佳实践
1. **最小权限原则**：仅请求功能必需的权限，避免过度申请。
2. **延迟请求**：在用户触发相关操作时再请求权限（如点击按钮时请求相机权限）。
3. **透明解释**：通过 `shouldShowRequestPermissionRationale()` 向用户说明权限用途。
4. **兼容性测试**：覆盖所有可能的权限状态（如已授予、拒绝、永久拒绝）。

---

### 六、权限模型演进与 AOSP 12 特性
- **Android 10+ 变更**：
  - **后台位置权限**：需单独申请，用户可选择“仅在使用时允许”。
  - **动态权限组**：权限分组可能随版本变化，开发者需避免依赖固定分组。

---

### 参考资料
- [Android 权限概览（官方文档）](https://developer.android.google.cn/guide/topics/permissions/overview)  
- [AOSP 权限默认授予策略](https://blog.csdn.net/tq501501/article/details/109203318)  
- [运行时权限适配指南](https://www.jb51.net/article/98092.htm)  

如需进一步了解具体代码实现（如 `DefaultPermissionGrantPolicy` 的权限预授予逻辑），可参考 AOSP 源码中的 `frameworks/base/services/core/java/com/android/server/pm/` 目录。



---

---

在 Android 权限管理框架中，`PermissionManagerService.java` 和 `PackageManagerService.java` 是两个核心组件，分别负责权限管理和包管理。以下是这两个方法的具体作用和对应框架中的角色：

---

### **1. `restorePermissionState` 方法**
#### **位置**：
`frameworks/base/services/core/java/com/android/server/pm/permission/PermissionManagerService.java`

#### **作用**：
- **权限状态恢复**：在应用安装、更新或系统启动时，恢复应用的权限状态。
- **关键逻辑**：
  - 根据应用的 `AndroidManifest.xml` 中声明的权限，结合系统策略（如默认权限授予、用户设置），确定最终权限状态。
  - 处理运行时权限和安装时权限的转换（如从旧版本升级时，将安装时权限转换为运行时权限）。
  - 更新权限状态到 `PermissionState` 对象中，并持久化到 `packages.xml`。

#### **对应框架中的角色**：
- **权限管理核心**：`PermissionManagerService` 是权限管理的核心服务，负责权限的授予、撤销和状态维护。
- **与 `PackageManagerService` 协作**：在应用安装或更新时，`PackageManagerService` 调用 `restorePermissionState` 来恢复权限状态。

#### **关键流程**：
1. **权限解析**：从 `AndroidPackage` 对象中提取权限声明。
2. **权限授予**：
   - 普通权限和签名权限在安装时自动授予。
   - 运行时权限根据用户设置和系统策略决定是否授予。
3. **状态更新**：将权限状态更新到 `PermissionState` 对象中，并持久化到 `packages.xml`。

---

### **2. `applyPolicy` 方法**
#### **位置**：
`frameworks/base/services/core/java/com/android/server/pm/PackageManagerService.java`

#### **作用**：
- **包安装策略应用**：在应用安装或更新时，应用系统策略（如默认权限授予、签名验证、系统应用特权等）。
- **关键逻辑**：
  - 根据应用的 `AndroidManifest.xml` 和系统策略，确定应用的安装行为（如是否为系统应用、是否需要更新权限）。
  - 调用 `PermissionManagerService` 的 `restorePermissionState` 方法恢复权限状态。

#### **对应框架中的角色**：
- **包管理核心**：`PackageManagerService` 是包管理的核心服务，负责应用的安装、更新和卸载。
- **与 `PermissionManagerService` 协作**：在安装或更新应用时，调用 `PermissionManagerService` 处理权限相关逻辑。

#### **关键流程**：
1. **包解析**：解析应用的 `AndroidManifest.xml`，提取包名、版本号、权限声明等信息。
2. **策略应用**：
   - 验证应用签名和系统策略（如是否为系统应用）。
   - 调用 `restorePermissionState` 恢复权限状态。
3. **安装完成**：将应用信息写入 `packages.xml`，完成安装或更新。

---

### **两者关系与协作**
1. **权限管理与包管理的分工**：
   - `PackageManagerService` 负责包的生命周期管理（安装、更新、卸载）。
   - `PermissionManagerService` 负责权限的生命周期管理（授予、撤销、状态维护）。

2. **协作流程**：
   - 在应用安装或更新时，`PackageManagerService` 调用 `PermissionManagerService` 的 `restorePermissionState` 方法恢复权限状态。
   - `PermissionManagerService` 根据系统策略和用户设置，确定最终权限状态，并更新到 `PermissionState` 对象中。

3. **数据持久化**：
   - 权限状态最终会写入 `packages.xml`，确保系统重启后权限状态一致。

---

### **示例场景**
#### **场景 1：应用安装**
1. `PackageManagerService` 解析应用的 `AndroidManifest.xml`。
2. 调用 `PermissionManagerService` 的 `restorePermissionState` 方法恢复权限状态。
3. 根据系统策略（如默认权限授予）和用户设置，确定最终权限状态。
4. 将应用信息和权限状态写入 `packages.xml`。

#### **场景 2：应用更新**
1. `PackageManagerService` 解析新版本的 `AndroidManifest.xml`。
2. 调用 `PermissionManagerService` 的 `restorePermissionState` 方法恢复权限状态。
3. 处理权限变更（如新增权限、移除权限）。
4. 更新 `packages.xml` 中的权限状态。

---

### **总结**
| **方法**                 | **所属服务**               | **作用**                       | **协作关系**                                      |
| ------------------------ | -------------------------- | ------------------------------ | ------------------------------------------------- |
| `restorePermissionState` | `PermissionManagerService` | 恢复应用的权限状态             | 被 `PackageManagerService` 调用，处理权限相关逻辑 |
| `applyPolicy`            | `PackageManagerService`    | 应用系统策略，完成包安装或更新 | 调用 `PermissionManagerService` 恢复权限状态      |

通过这两个方法的协作，Android 实现了权限管理与包管理的无缝集成，确保应用权限的正确授予和状态维护。



---

---

在 Android 应用权限框架中，`MANAGE_USERS` 和 `CREATE_USERS` 是两个与**用户管理**相关的系统权限，主要用于控制应用对设备用户（User Profile）的管理能力。以下是它们的详细说明：

---

### **1. `MANAGE_USERS` 权限**
- **权限名称**：`android.permission.MANAGE_USERS`
- **保护级别**：`signature|privileged|development`
- **作用**：
  - 允许应用管理设备上的用户（User Profile），包括创建、删除、修改用户信息。
  - 允许应用查询用户列表、切换用户、设置用户限制等。
- **适用场景**：
  - 系统设置应用（如用户管理界面）。
  - 企业设备管理应用（如 MDM 解决方案）。
- **权限声明**：
  ```xml
  <uses-permission android:name="android.permission.MANAGE_USERS" />
  ```

---

### **2. `CREATE_USERS` 权限**
- **权限名称**：`android.permission.CREATE_USERS`
- **保护级别**：`signature|privileged|development`
- **作用**：
  - 允许应用创建新的用户（User Profile）。
  - 通常与 `MANAGE_USERS` 配合使用。
- **适用场景**：
  - 多用户设备管理应用。
  - 企业设备管理应用（如创建受限用户）。
- **权限声明**：
  ```xml
  <uses-permission android:name="android.permission.CREATE_USERS" />
  ```

---

### **3. `checkManageOrCreateUsersPermission` 方法**
- **位置**：`UserManagerService.java`
- **作用**：
  - 检查调用者是否具有 `MANAGE_USERS` 或 `CREATE_USERS` 权限。
  - 如果没有权限，抛出 `SecurityException`。
- **实现逻辑**：
  ```java
  private void checkManageOrCreateUsersPermission(String message) {
      if (mContext.checkCallingOrSelfPermission(android.Manifest.permission.MANAGE_USERS)
              != PackageManager.PERMISSION_GRANTED
              && mContext.checkCallingOrSelfPermission(android.Manifest.permission.CREATE_USERS)
              != PackageManager.PERMISSION_GRANTED) {
          throw new SecurityException("You either need MANAGE_USERS or CREATE_USERS permission to: "
                  + message);
      }
  }
  ```

---

### **4. 权限框架中的角色**
- **系统权限**：`MANAGE_USERS` 和 `CREATE_USERS` 属于系统级权限，普通应用无法声明或使用。
- **保护级别**：
  - `signature`：仅系统签名应用可使用。
  - `privileged`：仅预装在系统分区的应用可使用。
  - `development`：仅调试版本可用。
- **权限检查**：通过 `UserManagerService` 的 `checkManageOrCreateUsersPermission` 方法强制执行。

---

### **5. 应用场景**
#### **场景 1：多用户设备管理**
- **功能**：创建、删除、切换用户。
- **权限**：`MANAGE_USERS` 和 `CREATE_USERS`。
- **示例**：系统设置中的“用户和账户”功能。

#### **场景 2：企业设备管理**
- **功能**：创建受限用户、设置用户策略。
- **权限**：`MANAGE_USERS` 和 `CREATE_USERS`。
- **示例**：企业 MDM 解决方案。

---

### **6. 权限授予与限制**
- **默认授予**：仅系统签名应用和预装应用可自动获得权限。
- **用户控制**：普通用户无法通过设置界面授予或撤销这些权限。
- **安全性**：通过 `signature` 和 `privileged` 保护级别，确保只有受信任的应用可管理用户。

---

### **7. 相关 API**
- **UserManager**：
  - `createUser()`：创建新用户（需 `CREATE_USERS` 权限）。
  - `getUsers()`：查询用户列表（需 `MANAGE_USERS` 权限）。
  - `removeUser()`：删除用户（需 `MANAGE_USERS` 权限）。
- **UserHandle**：表示用户的唯一标识。

---

### **8. 错误分析**
根据日志，`com.android.vending`（Google Play 商店）因缺少 `MANAGE_USERS` 或 `CREATE_USERS` 权限，导致 `SecurityException`。可能原因：
1. **权限未声明**：Google Play 商店未在 `AndroidManifest.xml` 中声明权限。
2. **权限未授予**：系统未授予 Google Play 商店权限（需系统签名或预装）。
3. **权限检查逻辑变更**：AOSP 12 可能加强了权限检查逻辑。

---

### **解决方案**
1. **检查权限声明**：
   - 确保 `AndroidManifest.xml` 中声明了 `MANAGE_USERS` 或 `CREATE_USERS`。
   ```xml
   <uses-permission android:name="android.permission.MANAGE_USERS" />
   <uses-permission android:name="android.permission.CREATE_USERS" />
   ```

2. **调整权限检查逻辑**：
   - 如果应用无需管理用户，移除相关代码。
   - 如果应用需管理用户，确保其具有系统签名或预装在系统分区。

3. **调试与测试**：
   - 使用 `adb shell pm list permissions -g -d` 查看权限状态。
   - 使用 `adb shell dumpsys package <package-name>` 检查权限授予情况。

---

### **总结**
- `MANAGE_USERS` 和 `CREATE_USERS` 是 Android 用户管理的核心权限，仅系统级应用可使用。
- 通过 `checkManageOrCreateUsersPermission` 方法强制执行权限检查，确保系统安全。
- 开发者需根据应用场景合理声明和使用权限，避免 `SecurityException`。

---

---



