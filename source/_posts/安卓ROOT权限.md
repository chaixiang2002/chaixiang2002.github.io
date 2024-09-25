![image-20240919171604104](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202409191716783.png)

基于aosp10的二次定制开发的系统， 项目需求是在设置应用中加一个root权限的选项，在这个页面中，可以选择给某个应用root权限 我想问问这个需求中，给某个应用root权限是怎么实现的？核心原理是什么？

在 AOSP 10 的二次定制开发中，要在设置应用中添加一个选项来授予特定应用 root 权限，需要深刻理解 Android 系统的安全模型和权限管理机制。默认情况下，Android 系统严格限制应用获得 root 权限，因为这会对系统的安全性造成严重威胁。实现给特定应用 root 权限的需求涉及到修改系统的安全策略和权限管理逻辑。

### 实现给应用 root 权限的核心原理
1. **理解 root 权限**：在 Android 中，root 权限意味着对系统的最高权限，可以执行任何操作，包括访问系统级 API、修改系统文件和设置。这种权限一般只授予系统级进程和应用。

2. **修改权限管理机制**：
   - **su 二进制文件**：传统的授予应用 root 权限的方法是通过 `su` 命令。在常见的 Android root 方案中，`su` 二进制文件被安装在 `/system/bin/` 或 `/system/xbin/` 中，通过它可以临时将进程的用户权限提升为 root 用户权限。
   - **修改 su 权限验证逻辑**：在授予应用 root 权限时，需要修改 `su` 的权限验证逻辑，使其能够根据你的设置应用中的配置，判断某个应用是否被允许执行 `su` 命令。
   - **System Server 修改**：为了在系统级别控制对 root 权限的授予，需要修改 System Server（如 `PackageManagerService`）以便它能够识别和处理应用的 root 权限请求。

3. **实现步骤**：
   - **添加 su 二进制文件**：确保在你的定制系统中，`su` 二进制文件已安装，并且可供特定的应用调用。
   - **修改 su 源码**：修改 `su` 的源码，使其能够根据一个配置文件或数据库（由设置应用管理）来判断某个应用是否被授予 root 权限。例如，可以在 `su` 代码中添加一段逻辑，检查某个配置文件中列出的允许使用 root 权限的应用列表。
   - **设置应用界面**：在设置应用中添加一个页面，列出当前系统中安装的应用，并提供选项让用户选择是否给予某个应用 root 权限。
   - **存储和管理权限列表**：设置应用将用户的选择存储在一个文件或数据库中，这个文件需要被 `su` 进程读取以决定是否授予 root 权限。
   - **授予权限的流程**：
     1. 应用请求 root 权限时，调用 `Runtime.getRuntime().exec("su")`。
     2. 系统中的 `su` 二进制文件被执行，它检查当前应用的包名。
     3. `su` 读取之前设置的配置文件或数据库，判断这个应用是否在允许列表中。
     4. 如果在列表中，`su` 提升进程权限为 root；否则拒绝并返回错误。

4. **注意事项**：
   - **安全风险**：赋予应用 root 权限会带来严重的安全风险，需要确保只有经过严格验证的应用才能获得此权限，并且需要明确告知用户。
   - **系统完整性**：确保对 `su` 及其权限验证逻辑的修改不影响系统的完整性，避免引入漏洞。
   - **用户提示**：在设置中授予 root 权限时，应该提供明确的用户提示，警告用户可能的风险。

### 总结
给应用 root 权限的核心原理是通过修改 `su` 二进制文件和系统权限管理机制，使其能够根据用户在设置应用中配置的权限列表，决定是否授予某个应用 root 权限。这涉及到系统级代码的修改，需要非常谨慎地处理，以避免安全问题。





我想问问，在没有root权限的时候，我们调用一些系统api或修改系统文件，会报权限错误 请问这个权限管理在aosp10页面的哪里，改模块的源码在哪？，他是属于linux的模块还是安卓的模块 我看到别人的实现大概是自己集成su程序，用它来获取root权限，这个核心原理是什么？

在 Android 系统中，权限管理是由多个组件共同协作完成的，涵盖了 Linux 内核级别的安全模型以及 Android 自身的权限机制。

### Android 权限管理的原理
1. **Linux 内核级别权限**：
   - Android 是基于 Linux 内核构建的，所以它继承了 Linux 的用户和权限模型。每个应用在安装时都会被分配一个唯一的用户 ID（UID）。文件系统和进程间的权限控制由 Linux 内核管理。默认情况下，应用只能访问由其 UID 所拥有的文件和资源，无法访问其他应用的数据。
   - **SELinux（Security-Enhanced Linux）**：Android 引入了 SELinux 来加强安全性，通过强制访问控制（MAC）来限制进程的权限。SELinux 策略配置位于 `system/sepolicy`，主要控制系统进程的访问权限。

2. **Android Framework 权限**：
   - Android 应用层的权限由 `AndroidManifest.xml` 中声明的权限控制，如 `READ_EXTERNAL_STORAGE`、`WRITE_EXTERNAL_STORAGE` 等。这些权限由系统在应用安装时授予，并由系统服务在运行时检查。
   - 系统服务如 `PackageManagerService` 和 `ActivityManagerService` 负责在运行时检查应用是否拥有特定权限。权限管理的核心代码位于 `frameworks/base/services/core/java/com/android/server/pm/PackageManagerService.java`。
   - **权限检查点**：在 Android 系统中，关键的权限检查点位于调用系统 API 时。例如，访问摄像头、位置服务、文件系统等操作，都会在系统服务中检查调用者的权限。

### 权限管理源码位置
- **系统 API 调用权限检查**：`frameworks/base/core/java/android/os/Binder.java` 中的 `checkPermission` 方法是很多系统 API 的权限检查入口。
- **PackageManagerService**：位于 `frameworks/base/services/core/java/com/android/server/pm/PackageManagerService.java`，负责管理应用的安装、卸载以及权限授予。
- **SELinux 策略**：`system/sepolicy` 目录包含了 Android 的 SELinux 策略配置，通过这些策略来限制系统进程和应用的权限。

### `su` 程序获取 root 权限的核心原理
1. **`su` 程序简介**：
   - `su` 是一个在类 Unix 系统上使用的工具，用于在当前会话中以其他用户身份（通常是超级用户 root）执行命令。在 Android 上，`su` 通常用于在应用中获得 root 权限。
   - 在 Android 系统中，由于安全模型的限制，普通应用进程无法直接获得 root 权限。而 `su` 程序通过在设备上安装一个具有 setuid 属性的二进制文件，使得特定进程可以在运行时获得 root 权限。

2. **`su` 获取 root 权限的流程**：
   - **Setuid 位**：`su` 程序的二进制文件通常具有 setuid 位，这意味着无论哪个用户运行它，它都会以文件所有者的身份运行。在 Android 中，这通常是 root 用户。因此，当应用调用 `su` 时，它实际上是以 root 身份运行 `su`。
   - **权限提升**：`su` 进程启动后，它会检查请求者的权限和参数，然后根据自身的逻辑决定是否授予 root 权限。通常，这个过程会涉及到用户授权的机制，如弹出对话框请求用户确认。
   - **执行命令**：如果 `su` 授予了权限，它会以 root 权限执行指定的命令，或者启动一个具有 root 权限的 shell 会话。

3. **自定义 `su` 实现**：
   - **自定义权限验证**：一些定制系统会替换或自定义 `su`，在其中增加权限验证逻辑。例如，通过读取某个配置文件或数据库，判断某个应用是否被授予了 root 权限。
   - **集成 `su`**：在自定义 ROM 或系统中，开发者可以将 `su` 程序作为系统应用或者放置在 `/system/bin/` 或 `/system/xbin/` 目录下，这样当应用请求 root 权限时，系统中已经存在的 `su` 程序可以处理这些请求。

### 总结
- **权限管理模块**：Android 的权限管理是由 Linux 内核、SELinux 和 Android Framework 共同实现的。核心源码包括 `PackageManagerService`、`Binder` 和 SELinux 策略配置等。
- **`su` 程序的原理**：`su` 程序利用 Linux 的 setuid 特性，允许指定进程以 root 权限运行。自定义 `su` 程序可以通过增加权限验证逻辑，实现更灵活的权限管理。



我可以理解为，获取root权限的应用和没有获取root权限的应用主要差别是uid吗？获取root权限的应用其进程uid是root su程序的作用就是可以改变应用的uid是吗？ 我还有疑问： su本身也是程序，他怎么能修改其他进程的uid？ 另外现在的安卓系统都没有su程序了吗？为什么各种想要root的用户，都要自己集成su程序？

你的理解部分正确，但还需要进一步澄清一些关键概念：

1. **获取 root 权限的应用与 UID 的关系**：
   - 是的，Android 中每个应用都有一个唯一的用户 ID（UID），普通应用运行在其独立的 UID 下，并受到 Linux 内核的权限限制。只有系统进程或特定的系统应用拥有更高的权限，包括 root 权限（UID 为 0）。
   - 获取 root 权限的应用可以执行一些系统级操作，这是因为它们的进程在执行时被临时提升为 root 用户身份（UID 为 0），从而拥有了更高的权限。

2. **`su` 程序的作用**：
   - `su` 程序的主要作用是让调用它的进程临时以 root 权限运行。通常情况下，普通应用没有直接访问 root 权限的能力。而 `su` 程序是一种中介，允许用户通过它将某个进程的权限提升为 root 权限。
   - 具体来说，`su` 通过 Linux 的 `setuid` 机制实现权限提升。`su` 程序本身的二进制文件具有 `setuid` 位（`s` 位）权限，这意味着无论哪个用户执行它，它都会以文件所有者（通常是 root）的身份运行。

3. **`su` 如何修改其他进程的 UID**：
   - `su` 不直接修改其他进程的 UID，而是创建一个新的进程，以 root 权限运行这个新进程。流程如下：
     1. 应用调用 `su` 时，请求提升权限。
     2. `su` 程序根据内置逻辑（或用户授权）决定是否允许权限提升。
     3. 如果允许，`su` 创建一个新的子进程，并将这个子进程的 UID 设置为 0（root）。然后执行指定的命令或启动一个 shell 会话。
   - `su` 进程本身在执行时就已经运行在 root 权限下，这使得它有能力创建一个以 root 身份运行的子进程。

4. **Android 系统和 `su` 程序**：
   - 现代的 Android 设备出厂时通常不包含 `su` 程序，原因如下：
     - **安全性**：默认情况下，Android 设备没有 root 访问权限，以保护系统和用户数据的安全。允许任意应用获得 root 权限会极大增加恶意软件攻击的风险。
     - **官方策略**：Google 和设备制造商一般不鼓励用户获取 root 权限，因为这会破坏系统的安全模型和应用沙箱机制。
   - 因此，如果用户想要在他们的设备上获得 root 权限，他们需要自己集成 `su` 程序，这通常涉及解锁设备的引导加载程序（bootloader）、安装自定义恢复（如 TWRP），并刷入一个包含 `su` 程序的 ZIP 包。

### 总结
- **UID 和权限**：获取 root 权限的关键在于进程以 root 用户身份（UID 为 0）运行。`su` 程序提供了一个机制来临时提升某个进程的 UID 为 0，使其能够以 root 权限运行。
- **`su` 的作用**：`su` 并不直接修改已有进程的 UID，而是启动一个新的子进程，并将这个子进程的 UID 设置为 root，从而实现权限提升。
- **Android 默认没有 `su`**：为了安全和稳定，出厂的 Android 设备不包含 `su`，需要 root 的用户只能自己集成 `su`，这也是很多用户需要自行刷机获取 root 权限的原因。









u0_a93       11565  2436 7 36:07 ?        00:00:00 ru.andr7e.deviceinfohw.pro  u0_a93       11597 11565 0 36:07 ?        00:00:00 sh  u0_a93       11618 11565 0 36:07 ?        00:00:00 su u0_a93       11619 11565 0 36:07 ?        00:00:00 su  u0_a93       11622 11618 0 36:07 ?        00:00:00 su  root         11624     1 0 36:07 ?        00:00:00 s9su --master  root         11625 11624 0 36:07 ?        00:00:00 s9su --master root         11626 11625 0 36:07 ?        00:00:00 s9su --master u0_a93       11627 11619 0 36:07 ?        00:00:00 su root         11629 11626 0 36:07 ?        00:00:00 sh root         11630     1 0 36:07 ?        00:00:00 s9su --master root         11631 11630 0 36:07 ?        00:00:00 s9su --master root         11632 11631 0 36:07 ?        00:00:00 s9su --master root         11633 11632 0 36:07 ?        00:00:00 sh root         11676    23 4 36:17 pts/0    00:00:00 ps -ef 我给ru.andr7e.deviceinfohw.pro这个应用root权限了，他也通过root获取了更多系统的信息 不过为什么这个进程不是root而是u0_a93？他是怎么利用su获取这些系统信息的？

在这个过程中，虽然 `ru.andr7e.deviceinfohw.pro` 应用（UID 为 `u0_a93`）本身的进程 UID 并没有被提升为 `root`，但它通过 `su` 命令启动了新的子进程，并在这些子进程中执行了以 `root` 权限运行的操作。这个过程可以分解为以下几个步骤：

1. **应用请求 root 权限**：`ru.andr7e.deviceinfohw.pro` 应用使用 `su` 命令尝试获得 root 权限。它的目的是执行某些需要更高权限的操作，而这些操作无法在其自身的 UID 下完成。

2. **启动 `su` 进程**：应用通过执行 `su` 命令启动一个 `su` 进程。这个 `su` 进程的 UID 仍然是 `u0_a93`，它只是一个中间步骤。

3. **`su` 提权**：
   - `su` 程序会根据预先配置的策略或者用户交互，决定是否允许应用获得 root 权限。
   - 如果允许，`su` 程序会启动新的子进程，并将这些子进程的 UID 设置为 `root`（UID 为 0）。
   
4. **以 root 运行**：
   - 你可以看到 `s9su --master` 进程，它们是以 `root` 身份运行的。这些进程是 `su` 启动的，并且具备 root 权限。
   - 这些 `root` 进程可以执行各种需要 root 权限的操作，例如读取系统信息、修改系统文件等。
   - 最终的操作结果可以通过进程间通信（如 `stdout`）传递回原应用 `ru.andr7e.deviceinfohw.pro`。

5. **进程间通信**：
   - 虽然原始应用进程 `ru.andr7e.deviceinfohw.pro` 仍然以 `u0_a93` 运行，但它通过 `su` 提升了子进程的权限，并通过这些子进程执行高权限操作。
   - 应用可以通过这些子进程来获取系统信息，然后将结果传回给自身，从而实现其功能。

### 为什么原应用进程 UID 没有变化？
- 原应用进程并没有直接成为 `root`，因为 Android 系统对进程的 UID 和权限有严格的管理。即使获得了 root 权限，`su` 也只是启动了一个新的子进程，并没有改变原应用进程的 UID。
- 这样做是为了隔离安全风险，即使应用的某部分被赋予了 root 权限，整个应用的其他部分仍然在原有的权限范围内运行，降低了潜在的安全隐患。

### 总结
- `ru.andr7e.deviceinfohw.pro` 应用通过 `su` 命令启动了新的 `root` 子进程（例如 `s9su --master`），这些子进程拥有 root 权限，执行所需的高权限操作。
- 原始应用进程的 UID 仍然是 `u0_a93`，通过与 `su` 子进程的通信，应用可以获取所需的系统信息。
- `su` 通过 `setuid` 机制创建新的子进程，使这些子进程在 root 权限下运行，而不会直接改变原始应用进程的 UID。





可能有用

[给 Android ROM（AOSP）集成 SuperSU 的方法 | SickWorm的博客](https://sickworm.com/?p=367)

[AOSP Android 10定制su名字隐藏root (sunofbeach.net)](https://www.sunofbeach.net/a/1627299344324681730)

比较有用

[将Android10编译成真正的具有root权限的系统_安卓10能root吗-CSDN博客](https://blog.csdn.net/chlbd/article/details/107065810)

神珍

[Android系统权限和root权限 - 巽曌 - 博客园 (cnblogs.com)](https://www.cnblogs.com/xun99/archive/2013/01/17/2865208.html)





### 集成su

---

位置：system/extras/su/su.cpp

注释main函数的开始两行：

```c
uid_t current_uid = getuid();
if (current_uid != AID_ROOT && current_uid != AID_SHELL) error(1, 0, "not allowed");
```

如果当前进程的uid不是shell或root，就报错

---

位置：system/core/libcutils/fs_config.cpp

文件中搜索修改为如下内容。

```c
static const struct fs_path_config android_dirs[] = {
        // clang-format off
    { 00770, AID_SYSTEM,       AID_CACHE,        0, "cache" },
    { 00555, AID_ROOT,         AID_ROOT,         0, "config" },
    { 00771, AID_SYSTEM,       AID_SYSTEM,       0, "data/app" },
    { 00771, AID_SYSTEM,       AID_SYSTEM,       0, "data/app-private" },
    { 00771, AID_SYSTEM,       AID_SYSTEM,       0, "data/app-ephemeral" },
    { 00771, AID_ROOT,         AID_ROOT,         0, "data/dalvik-cache" },
    { 00771, AID_SYSTEM,       AID_SYSTEM,       0, "data/data" },
    { 00771, AID_SHELL,        AID_SHELL,        0, "data/local/tmp" },
    { 00771, AID_SHELL,        AID_SHELL,        0, "data/local" },
    { 00770, AID_DHCP,         AID_DHCP,         0, "data/misc/dhcp" },
    { 00771, AID_SHARED_RELRO, AID_SHARED_RELRO, 0, "data/misc/shared_relro" },
    { 01771, AID_SYSTEM,       AID_MISC,         0, "data/misc" },
    { 00775, AID_MEDIA_RW,     AID_MEDIA_RW,     0, "data/media/Music" },
    { 00775, AID_MEDIA_RW,     AID_MEDIA_RW,     0, "data/media" },
    { 00750, AID_ROOT,         AID_SHELL,        0, "data/nativetest" },
    { 00750, AID_ROOT,         AID_SHELL,        0, "data/nativetest64" },
    { 00775, AID_ROOT,         AID_ROOT,         0, "data/preloads" },
    { 00771, AID_SYSTEM,       AID_SYSTEM,       0, "data" },
    { 00755, AID_ROOT,         AID_SYSTEM,       0, "mnt" },
    { 00751, AID_ROOT,         AID_SHELL,        0, "product/bin" },
    { 00750, AID_ROOT,         AID_SHELL,        0, "sbin" },
    { 00777, AID_ROOT,         AID_ROOT,         0, "sdcard" },
    { 00751, AID_ROOT,         AID_SDCARD_R,     0, "storage" },
    { 00751, AID_ROOT,         AID_SHELL,        0, "system/bin" },
    { 00755, AID_ROOT,         AID_ROOT,         0, "system/etc/ppp" },
    { 00755, AID_ROOT,         AID_SHELL,        0, "system/vendor" },
    { 00751, AID_ROOT,         AID_SHELL,        0, "system/xbin" },
    { 00755, AID_ROOT,         AID_SHELL,        0, "system/apex/*/bin" },
    { 00751, AID_ROOT,         AID_SHELL,        0, "vendor/bin" },
    { 00755, AID_ROOT,         AID_SHELL,        0, "vendor" },
    { 00755, AID_ROOT,         AID_ROOT,         0, 0 },
        // clang-format on
};
```

这段代码定义了一个结构体数组 `android_dirs`，用于指定不同目录的权限和所有者信息。这些信息在 Android 系统中用于管理目录的访问权限和所有权。以下是详细解释：

### 结构体定义

`fs_path_config` 是一个结构体，描述了一个目录的配置。结构体的定义可能如下：

```cpp
struct fs_path_config {
    mode_t mode;       // 目录的权限
    uid_t owner;       // 目录的所有者的 UID
    gid_t group;       // 目录的组的 GID
    unsigned flags;    // 可能的标志位
    const char* path;  // 目录路径
};
```

### 数组中的每一项

每一项都是一个 `fs_path_config` 结构体的实例，用于描述一个目录的配置。字段解释如下：

1. **`mode`**: 目录的权限位。这个值是八进制的文件权限模式，例如 `00770` 表示目录的权限是 `rwxrwx---`。

2. **`owner`**: 目录的所有者的 UID（用户 ID）。`AID_ROOT` 通常是 0，表示 root 用户。`AID_SHELL` 是一个特定的 shell 用户的 UID。

3. **`group`**: 目录的组的 GID（组 ID）。它指定了哪些用户组有权限访问这个目录。

4. **`flags`**: 可能的标志位。这个字段在这里未被使用，所以它是 0。

5. **`path`**: 目录的路径。这是相对于根文件系统的路径。

### 详细解释

- **`{ 00770, AID_SYSTEM, AID_CACHE, 0, "cache" }`**:
  - 权限 `00770`：所有者和组具有读取、写入和执行权限（`rwxrwx---`），其他人没有权限。
  - 所有者是 `AID_SYSTEM`，组是 `AID_CACHE`。这表示 `cache` 目录由 `system` 用户拥有，并且属于 `cache` 组。

- **`{ 00755, AID_ROOT, AID_SYSTEM, 0, "mnt" }`**:
  - 权限 `00755`：所有者有读取、写入和执行权限（`rwxr-xr-x`），组和其他人只有读取和执行权限。
  - 所有者是 `AID_ROOT`，组是 `AID_SYSTEM`。这表示 `mnt` 目录由 `root` 用户拥有，并且属于 `system` 组。

- **`{ 00777, AID_ROOT, AID_ROOT, 0, "sdcard" }`**:
  - 权限 `00777`：所有人都具有读取、写入和执行权限（`rwxrwxrwx`），通常用于公共访问目录。
  - 所有者和组都是 `AID_ROOT`。这表示 `sdcard` 目录由 `root` 用户拥有，并且属于 `root` 组。

### 作用

这个配置数组在 Android 系统中用于：

- **文件系统初始化**：在系统启动时，设置这些目录的权限和所有者，以确保系统能够正确地管理访问权限。
- **安全性管理**：通过正确配置权限和所有者，系统能够限制对敏感目录的访问，确保只有授权的用户或进程可以访问或修改这些目录。

### 总结

`fs_path_config` 数组定义了多个目录的权限和所有者配置。这些配置对于确保系统的安全性和正确性至关重要，特别是在涉及到系统文件和数据目录时。

---

![image-20240918182602735](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202409181826030.png)

根据你提供的图片，这些是 `su.c` 文件中的函数。以下是每个函数的可能作用解释，基于常见的 `su` 命令实现：

1. **is_daemon**: 检查当前进程是否是守护进程。`su` 命令有时会作为后台服务（守护进程）运行，这个函数用于判断。

2. **daemon_from_uid**: 根据用户 ID (`UID`) 启动或判断守护进程。可能用于通过 UID 来判断是否应运行守护进程。

3. **daemon_from_pid**: 根据进程 ID (`PID`) 来操作守护进程，类似于 `daemon_from_uid`，但这里是通过进程 ID 进行操作。

4. **fork_zero_fucks**: 这个名称较为随意，可能是执行特定任务的 `fork()` 函数。`fork()` 是创建子进程的系统调用，可能为了某些任务（不太关心错误处理，故名称中包含 "zero fucks"）。

5. **from_init**: 这个函数可能用于初始化上下文，特别是从系统初始化进程 (`init`) 中获取某些信息或进行操作。

6. **populate_environment**: 用于设置环境变量。在执行 `su` 时，可能需要根据特定的上下文设置一组新的环境变量。

7. **set_identity**: 用于设置用户或进程的身份（UID/GID），以确保执行操作时具有正确的权限。

8. **usage**: 显示程序的用法信息，通常在用户输入不正确或请求帮助时显示。

9. **deny**: 拒绝某些权限请求。`su` 程序可能需要判断某些上下文或请求并拒绝执行。

10. **allow**: 允许某些权限请求，与 `deny` 函数相反，允许在某些条件下的权限切换。

11. **access_disabled**: 判断或设置某些访问功能是否被禁用。可能是用于判断当前上下文是否禁止了某些功能。

12. **fork_for_samsung**: 特定于三星设备的 `fork()` 实现，可能是为了处理三星设备上的特定需求。

13. **main**: 主函数，程序的入口点，负责处理命令行输入并启动相应操作。

14. **su_main**: 类似 `main` 函数，但可能是 `su` 功能的核心处理逻辑，通常用于处理实际的权限提升。

这些函数的具体实现细节依赖于代码的具体内容，但从命名和常见 `su` 实现的角度来看，它们基本与权限管理、环境设置和守护进程相关。如果你有进一步的代码细节或上下文信息，可以更准确地说明这些函数的作用。



---

```c++
int su_main(int argc, char *argv[], int need_client) {}
```

这段代码是一个 `su`（Super User）命令的实现，它允许应用程序以 root 权限执行任务。`su` 命令的核心功能是切换用户身份，尤其是提升到 root 权限。下面详细解释它是如何让应用程序获取 root 权限的：

### 1. **权限检查与主函数调用**

```c
int main(int argc, char *argv[]) {
    if (getuid() != geteuid()) {
        ALOGE("must not be a setuid binary");
        return 1;
    }

    return su_main(argc, argv, 1);
}
```

- `getuid()` 和 `geteuid()` 用于获取当前用户的实际用户 ID 和有效用户 ID。
- 在通常情况下，`su` 程序会被设置为 `setuid` 二进制文件，使得即使普通用户运行，它也可以以 root 权限执行。该段代码确保程序不能以 `setuid` 方式被调用，否则报错。
- `su_main` 是实际处理权限提升的函数，`main` 函数直接调用 `su_main`，并传递命令行参数。

### 2. **`su_main` 函数**

```c
int su_main(int argc, char *argv[], int need_client) {
    // start up in daemon mode if prompted
    if (argc == 2 && strcmp(argv[1], "--master") == 0) {
        return run_daemon();
    }
```

- 如果传递了 `--master` 参数，`su` 将以守护进程模式运行，执行 `run_daemon()` 函数。这允许 `su` 以后台服务的方式持续运行，处理后续的权限请求。

```c
    int ppid = getppid();
    fork_for_samsung();
```

- 通过 `getppid()` 获取父进程 ID（PPID），并调用 `fork_for_samsung()`，这可能是针对三星设备的特定处理。

### 3. **环境变量清理**

```c
    static const char* const unsec_vars[] = { ... };
    const char* const* cp   = unsec_vars;
    const char* const* endp = cp + sizeof(unsec_vars)/sizeof(unsec_vars[0]);
    while (cp < endp) {
        unsetenv(*cp);
        cp++;
    }
```

- 这里清理了所有不安全的环境变量，防止恶意进程通过特定的环境变量来提升权限或影响系统行为。

### 4. **权限上下文设置**

```c
    struct su_context ctx = {
        .from = {
            .pid = -1,
            .uid = 0,
            .bin = "",
            .args = "",
            .name = "",
        },
        .to = {
            .uid = AID_ROOT,
            .login = 0,
            .keepenv = 0,
            .shell = NULL,
            .command = NULL,
            .argv = argv,
            .argc = argc,
            .optind = 0,
            .name = "",
        },
    };
```

- 定义了一个 `su_context` 结构体，保存了当前的权限请求的上下文信息。`ctx.from` 包含了发起请求的用户或进程的信息，而 `ctx.to` 则是目标用户信息，这里将目标 UID 设定为 `AID_ROOT`（root 权限）。

### 5. **命令行选项解析**

```c
    while ((c = getopt_long(argc, argv, "+c:hlmps:Vv", long_opts, NULL)) != -1) {
        // 处理命令行参数，设置目标 shell、命令或环境保持选项等。
    }
```

- 这里解析了命令行参数，通过 `-c` 可以指定要执行的命令，通过 `-s` 指定 shell，`-l` 切换登录模式，`-p` 保留环境变量等。

### 6. **尝试连接守护进程**

```c
    if (need_client) {
        // attempt to connect to daemon...
        ALOGD("starting daemon client %d %d", getuid(), geteuid());
        return connect_daemon(argc, argv, ppid);
    }
```

- 如果 `need_client` 被设置，程序将尝试连接到守护进程。守护进程用于统一管理 root 权限请求。

### 7. **处理用户和 UID**

```c
    /* username or uid */
    if (optind < argc && strcmp(argv[optind], "--")) {
        struct passwd *pw;
        pw = getpwnam(argv[optind]);
        if (!pw) {
            ctx.to.uid = strtoul(argv[optind], &endptr, 10);
        } else {
            ctx.to.uid = pw->pw_uid;
        }
    }
```

- 如果提供了用户名或 UID 参数，`su` 将尝试获取目标用户的 UID，并设置为上下文中的目标 UID（即需要切换到的身份）。

### 8. **权限请求处理**

```c
    if (from_init(&ctx.from) < 0) {
        deny(&ctx);
    }

    // Check if the user is root, and if so, grant permissions.
    if (ctx.from.uid == AID_ROOT) {
        ALOGD("Allowing root/system/radio.");
        allow(&ctx, NULL);
    }

    // Check if access is disabled
    if (access_disabled(&ctx.from)) {
        ALOGD("access_disabled");
        deny(&ctx);
    }

    // Autogrant shell
    if (ctx.from.uid == AID_SHELL) {
        ALOGD("Allowing shell.");
        allow(&ctx, NULL);
    }
```

- 调用 `from_init()` 获取请求发起者的详细信息。如果初始化失败，调用 `deny()` 函数拒绝权限请求。
- 如果发起请求的 UID 是 `AID_ROOT`（即 root 用户），将自动调用 `allow()` 函数直接授予权限。
- 检查是否完全禁用了 superuser 访问（通过 `access_disabled()` 函数）。如果禁用了，则调用 `deny()` 拒绝请求。
- 如果请求来自 shell 用户（`AID_SHELL`），则直接授予权限。

### 9. **最终授权**

```c
    allow(&ctx, NULL);
```

- 最后，调用 `allow()` 函数授予权限。这是程序最终的授权步骤。如果所有的条件都通过了，那么请求将被允许，权限被提升。

### 总结

这段代码的基本流程是：
1. 检查权限、解析命令行参数，并清理不安全的环境变量。
2. 根据请求发起者的 UID 判断是否允许权限提升。
3. 如果符合条件（如是 root 用户或 shell 用户），将执行 `allow()` 函数授予权限。
4. 如果有必要，它将尝试连接守护进程来处理权限请求。

通过这样的流程，它能够让应用程序（尤其是 Android 应用）在符合条件的情况下获取 root 权限。



---

### 获取ROOT的全过程

一个应用程序要获取 root 权限，通常需要通过以下步骤与系统交互，以实现权限提升。以下是详细的过程，结合了你提供的 `GrantRoot` 代码的工作原理来进行讲解。

### 1. 应用程序请求 root 权限

- 当应用程序需要执行某些高权限操作时，会向用户发起 root 权限请求，通常会通过弹窗或者请求框询问用户是否允许该操作。
- 在请求权限的同时，应用会尝试与系统中的 su 二进制文件或与 root 提权管理器（如 Magisk、SuperSU 等）通信。

### 2. 与 su 管理器交互

- 应用程序通过执行 `su` 命令来请求提权。系统中典型的 su 管理器会捕获这个请求并验证来源（例如包名、UID）。
- su 管理器会将请求传递给对应的 su 守护进程进行进一步处理。

### 3. su 守护进程验证请求

- su 守护进程会检查当前应用的身份（UID、包名）并判断是否应该授予 root 权限。这可能涉及用户之前的设置（例如记住该应用的权限请求）。
- 如果请求被允许，守护进程会切换到 root 用户并执行相应的命令。

### 4. 提权过程（结合 `GrantRoot` 中的实现）

#### 4.1 后台服务验证（`checkRootable()` 方法）

- `checkRootable()` 方法是提权的第一步，通过与后台 socket 服务通信，验证当前 UID 是否被允许提权。
- 这个服务通常会在系统的某个特殊路径（如 `/data/system/root_sock`）监听请求，根据接收的数据（如 `root:<uid>`）来判断请求的合法性。
- 如果返回 `'1'` 表示允许提权，否则表示拒绝。

#### 4.2 准备提权环境（`startGrantRoot()` 方法）

- 如果验证通过，`GrantRoot` 类中的 `startGrantRoot()` 方法会创建必要的目录和文件结构（如 `/data/overlay_misc`），并设置适当的权限。
- 然后，它会在 `/system/bin` 上执行一个叠加挂载操作，将 `su` 二进制文件放置在可访问的路径中。通过这种方式，可以将 su 命令插入系统路径。

#### 4.3 创建符号链接并挂载（`startGrantRoot()` 方法）

- `startGrantRoot()` 方法会创建一个指向真正 su 守护进程（如 `/system/xbin/s9su`）的符号链接，保证后续所有 su 请求都能找到正确的二进制文件执行。
- 挂载完成后，应用程序或 su 守护进程可以以 root 身份执行指定的命令。

### 5. 执行高权限命令

- 一旦挂载和符号链接完成，应用程序的请求就被转发给 su 守护进程。守护进程以 root 身份执行应用的请求，并将执行结果返回给应用。
- 应用程序可以通过这种方式获得访问系统敏感文件、修改系统设置或执行其他需要高权限的操作。

### 6. 收尾与安全措施

- 完成提权操作后，su 管理器会记录操作日志或向用户报告，以便用户可以追踪哪些应用请求了 root 权限。
- 一些 su 管理器可能会有超时机制，在一段时间后自动撤销权限，保证安全性。

### 总结

- 整个提权过程依赖于 su 管理器、su 守护进程和系统内的文件结构调整。
- `GrantRoot` 实现中，通过动态创建和挂载 su 命令来绕过系统的安全限制，让应用能够访问 root 级别的功能。
- 提权的核心是权限验证（防止滥用）和权限执行（通过 su 守护进程），确保应用能在用户授权的情况下安全获得 root 权限。

希望这能帮你全面理解应用如何在 Android 中获取 root 权限以及其中涉及的各个步骤！





### su程序的可见性

这是一个非常重要的安全问题。你提到的疑问的确涉及到了挂载和链接 `su` 程序后所产生的权限控制和可见性问题。

在 `startGrantRoot()` 方法中，确实通过挂载和符号链接将 `su` 程序暴露在 `/system/bin` 或者其他关键路径中，这样的操作可能会带来系统级别的权限暴露风险。然而，是否所有应用程序都可以访问 `su` 程序取决于挂载的实现方式和环境隔离的控制。

### 1. 挂载和符号链接的权限控制

`startGrantRoot()` 方法的关键操作包括：
- 在 `/system/bin` 或其他路径执行一个叠加挂载操作 (`mount` overlay)，将 `su` 程序暴露出来。
- 创建符号链接指向 su 二进制文件。

这两步确实将 `su` 文件放置在一个所有应用都可能访问的路径中，从表面上看，似乎所有应用都可以使用 `su` 程序获取 root 权限。但是否真的可行，取决于以下几方面的控制。

### 2. 可见性与挂载命名空间

挂载操作的可见性取决于使用的命名空间（Namespace）。在现代 Linux（包括 Android）的实现中，有以下几个关键点：

- **私有挂载命名空间**：如果挂载操作是在私有命名空间中进行的，那么这个挂载变更仅对当前进程和它的子进程可见。这意味着，只有调用 `startGrantRoot()` 方法的进程（以及其子进程）能看到 `su` 程序，而其他进程无法访问这些变更。这种隔离大大提高了系统的安全性。

- **共享挂载命名空间**：如果挂载是在一个共享的命名空间中进行的，那么挂载的变更将会被系统中的所有进程所看到，这会导致安全性问题，因为任何进程都可以访问挂载路径上的 `su` 程序。

#### 检查代码中的命名空间使用

从你提供的代码片段来看，`startGrantRoot()` 并没有显式地展示出命名空间控制的细节。如果 `startGrantRoot()` 的挂载操作是在私有挂载命名空间中进行的（例如使用 `unshare(CLONE_NEWNS)` 创建新的挂载命名空间），那么这个变更只会影响当前的进程空间。

### 3. 系统挂载策略和 SELinux

- **SELinux (Security-Enhanced Linux)**：Android 系统通常启用 SELinux 作为额外的安全层。即便 `su` 程序被挂载并暴露出来，SELinux 策略可以进一步限制哪些应用有权访问 `su`，从而防止未经授权的应用执行 `su`。

- **系统权限设置**：挂载目录的权限和 su 文件本身的权限也会限制对 su 的访问。通常情况下，`su` 文件会被设置为仅允许特定的用户或进程组（如 root、system、shell）访问。

### 4. 总结

- 如果 `startGrantRoot()` 中的挂载是私有命名空间，那么 `su` 程序的暴露仅对当前调用的进程有效，其他应用是看不到的。
- 如果没有使用私有命名空间，那么 su 程序对所有应用都可见，这确实是一个重大的安全风险。
- SELinux 和文件权限可以进一步控制对 su 的访问，即便挂载可见，也会有额外的限制。

因此，最安全的实现方式是确保挂载操作在一个私有的命名空间中进行，结合 SELinux 和严格的权限控制，确保只有受信任的应用和进程能够调用 `su` 程序。



### su程序的挂载和链接

### `su` 程序的链接和挂载步骤详解

从你提供的代码中，`GrantRoot` 类通过 `startGrantRoot()` 方法实现提权，其核心在于对 `su` 程序的链接和挂载操作。下面我将详细描述这些步骤、链接和挂载的具体操作，以及最终的挂载位置和可见性。

#### 1. 目录的创建和权限设置

首先，`startGrantRoot()` 函数执行了一系列目录创建操作，以确保用于挂载和链接的工作环境准备就绪：

- **创建工作目录和上层目录：**
  
  代码中创建了以下三个目录：

  1. **`/data/overlay_misc/`：**  
     用于存放 overlay 文件系统相关的数据。
     
  2. **`/data/overlay_misc/workdir`：**  
     用作 overlay 挂载的工作目录。

  3. **`/data/overlay_misc/upper`：**  
     用作 overlay 挂载的上层目录，存放文件变更数据。

这些目录的权限分别为 `0750` 和 `0751`，限制了非 root、system、shell 用户的访问权限。

#### 2. 创建 `su` 的符号链接

接下来是符号链接的创建步骤：

- **链接路径：** `/data/overlay_misc/upper/su`
- **链接目标：** `/system/xbin/s9su`

如果 `su` 的链接路径 `/data/overlay_misc/upper/su` 不存在，或者存在但不是一个符号链接，代码会执行以下步骤：

1. **删除旧的 `su` 文件（如果存在且不是符号链接）。**
2. **创建新的符号链接，将 `su` 链接到 `/system/xbin/s9su`。**

**创建这个链接的意义在于：** 通过这个符号链接，`su` 程序的位置被虚拟映射到 overlay 文件系统中，从而实现了对 `su` 程序的间接调用。

#### 3. 叠加挂载 `overlay` 文件系统

接下来是关键的挂载步骤，通过叠加挂载（overlay mount）将 `/system/bin` 与 `upper` 和 `workdir` 目录结合：

- **挂载参数：** 
  ```c
  sprintf(data, "lowerdir=%s,upperdir=%s,workdir=%s", "/system/bin", OVERLAY_MISC_UPPERDIR, OVERLAY_MISC_WORKDIR);
  ```
  其中：
  - `lowerdir=/system/bin`：系统的可执行文件目录，作为底层目录。
  - `upperdir=/data/overlay_misc/upper`：包含变更文件（如 `su` 符号链接）的上层目录。
  - `workdir=/data/overlay_misc/workdir`：用于挂载操作的工作目录。

- **挂载命令：**
  ```c
  mount("overlay", "/system/bin", "overlay", MS_RDONLY, data);
  ```
  这条命令的效果是将 `upperdir` 和 `workdir` 叠加在 `lowerdir` 上，挂载点为 `/system/bin`，并且设置为只读 (`MS_RDONLY`)。

**最终效果：** 

- 这个挂载操作使得 `upperdir` 中的变更（如 `/data/overlay_misc/upper/su` 的符号链接）对 `/system/bin` 目录内的进程可见。
- 由于 overlay 挂载，所有调用 `/system/bin/su` 的操作都会指向 `/data/overlay_misc/upper/su` 的符号链接，进而执行实际的 `/system/xbin/s9su` 程序。

#### 4. 可见性和权限控制

**命名空间的控制：** 

- 如果挂载操作发生在一个私有挂载命名空间中（如通过 `unshare(CLONE_NEWNS)` 创建），这个挂载变更仅对当前的进程和子进程有效。
- 其他应用或系统进程无法看到这些变更，从而限制了 `su` 程序的使用权限。

**安全措施：**

- 通过使用私有命名空间以及 SELinux 策略来进一步控制哪些用户或进程能够访问挂载的 `su` 符号链接，避免未授权的访问。

#### 总结

1. **符号链接** 将 `/system/xbin/s9su` 映射为 `/data/overlay_misc/upper/su`。
2. **挂载 overlay 文件系统** 将 `upperdir` 与 `/system/bin` 叠加，使得 `su` 程序在 `/system/bin` 可见。
3. **挂载点为 `/system/bin`**，变更只对当前命名空间内的进程有效。
4. **安全性依赖于命名空间隔离和 SELinux 策略**，确保 `su` 程序不会被未经授权的应用访问。

这个过程通过叠加文件系统和命名空间控制，实现了对 `su` 程序的安全使用和访问权限管理。







### proc_watcher程序理解

这个程序是一个 Android 系统中的进程监控和提权工具，主要由几个关键部分组成，包括 `GrantRoot`、`BuildModifier`、`SocketConnection` 等。这些部分配合在一起，通过监控应用的创建并在特定条件下授予 root 权限，同时还会修改系统属性以实现某些系统行为的调整。下面是对程序各部分的详细讲解：

### 整体功能
- **程序的核心功能**是监听应用进程的创建事件，并在满足特定条件时，授予应用 root 权限，同时可以通过 `BuildModifier` 修改系统属性。
- 这些功能通常用于系统工具、性能调优工具或其他需要访问系统底层权限的应用。

### 程序的组成部分及每部分的功能

1. **Android.bp（构建脚本）**
   - 定义了名为 `libandroidpw` 的共享库。
   - 依赖的源文件包括 `AppWatcher.cpp`、`SocketConnection.cpp`、`BuildModifier.cpp` 和 `GrantRoot.cpp`。
   - 依赖的库有 `libcutils` 和 `liblog`，用于系统日志输出和属性操作。
   - 使用的编译标志包括对一些编译警告的启用和禁用。

2. **`AppWatcher.cpp`（应用监控）**
   - 主要负责监听和响应 Android 系统进程的创建事件。
   - 包含两个核心函数：
     1. **`onZygoteFork()`：**  
        在 Zygote 进程分叉前执行，用于在系统启动应用程序之前进行一些环境设置操作，通过 `BuildModifier` 修改系统属性。
     2. **`onAppCreate()`：**  
        在应用创建后执行，通过 `GrantRoot` 类尝试对应用进行提权操作，根据 UID 判断是否可以授予 root 权限。
   
3. **`GrantRoot.h` 和 `GrantRoot.cpp`（权限提升）**
   - `GrantRoot` 类负责具体的提权操作，根据用户 UID 来判断是否允许执行提权。
   - 主要方法：
     1. **`handleRoot()`：**  
        检查 UID 是否是 root、system 或 shell 用户，如果是，则尝试执行提权。
     2. **`startGrantRoot()`：**  
        执行提权的核心逻辑，包括创建符号链接 `/data/overlay_misc/upper/su` 指向 `/system/xbin/s9su`，然后通过 overlay 文件系统将其挂载到 `/system/bin`，使得 `su` 程序可用。
     3. **`checkRootable()`：**  
        通过 socket 连接 `/data/system/root_sock`，与后台服务通信来验证当前用户是否具备提权资格，确保提权过程的安全性。

4. **`BuildModifier.h` 和 `BuildModifier.cpp`（系统属性修改）**
   - `BuildModifier` 类用于修改 Android 系统的属性和版本信息。
   - 主要方法：
     1. **`getApplyproperties()`：**  
        通过 socket 连接 `/data/system/s9_sock`，从后台获取需要修改的属性集合。
     2. **`apply()`：**  
        遍历属性集合，根据每个属性的键值对来修改系统的属性字段。调用多个设置函数（如 `setStringValue()`、`setBooleanValue()` 等），修改 `Build` 类和 `Version` 类中的属性。

5. **具体的属性修改方法**
   - **`setStringValue()`：** 修改系统类的字符串属性。
   - **`setStringArrayValue()`：** 修改字符串数组属性。
   - **`setLongValue()`：** 修改长整型属性。
   - **`setBooleanValue()`：** 修改布尔型属性。
   - **`setIntegerValue()`：** 修改整型属性。

### 详细工作流程

1. **进程创建监听：**
   - 当系统的 Zygote 进程分叉创建新的应用进程时，会调用 `onZygoteFork()` 和 `onAppCreate()`。
   - `onZygoteFork()` 调用 `BuildModifier` 类的 `apply()` 方法，调整系统属性。
   
2. **应用提权：**
   - `onAppCreate()` 调用 `GrantRoot` 类的 `handleRoot()` 方法，尝试根据 UID 对应用进行提权。
   - 如果用户 UID 符合条件或通过了权限检查，则执行提权，挂载 `su` 程序，使其可用。

3. **提权实现：**
   - `startGrantRoot()` 方法执行一系列挂载和链接操作，确保 `su` 程序链接到 `/system/bin`，使得有权限的进程可以执行提权命令。

4. **系统属性修改：**
   - `BuildModifier` 通过 socket 获取需要修改的系统属性。
   - 使用获取到的键值对来动态调整系统 `Build` 和 `Version` 类的相关字段。

### 总结

- 这个程序通过监听应用的创建过程，动态调整系统属性，并在满足特定条件时授予应用 root 权限。
- 各个组件之间通过 socket 通信和共享库的方式紧密集成，完成提权和系统行为修改的任务。
- 整体设计结合了 C++ 的系统接口、JNI 和 Android 系统底层功能，适合用于开发需要高度权限管理和系统行为控制的应用工具。



### 应用程序调用su程序如何获得结果的

在 Android 系统中，应用程序想要通过 `su` 程序获取 root 权限并执行操作的过程大致如下：

1. **启动 `su` 进程**：应用程序会通过某种方式（如 Java 的 `Runtime.exec()`、`ProcessBuilder` 或 C/C++ 的 `fork/exec` 等）执行 `su` 命令，并将所需执行的命令作为参数传给 `su`。例如，应用程序可能会执行以下命令：
   ```bash
   su -c "cat /path/to/protected/file"
   ```
   这意味着应用程序请求 `su` 以 root 权限执行 `cat /path/to/protected/file` 命令。

2. **`su` 的运行逻辑**：在 `su` 程序的 `main` 函数中，`su_main` 会处理应用程序传入的参数，并确定是否以 root 权限执行命令。在 `su_main` 函数中，程序会处理命令行参数，如 `-c`、`-l`、`-p`、`-s` 等。

3. **`allow` 函数执行命令**：
   - `allow()` 函数是 `su` 程序授权执行命令的核心部分。当 `su` 判断应用程序具有执行权限时，它会在 `allow()` 函数中实际执行该命令。
   - 在 `allow()` 中，`su` 通过 `execvp` 调用目标命令（如 `cat`）。在调用 `execvp` 时，`su` 会用 fork 创建子进程，并在子进程中执行指定命令。父进程则会等待子进程执行完成。

4. **获取执行结果**：
   - 在 `allow()` 函数中，父进程使用 `waitpid` 等待子进程完成执行。这时，子进程执行的命令的标准输出和错误输出会传递给父进程。
   - 如果应用程序通过 `Runtime.exec()` 启动 `su`，则应用程序可以通过获取 `Process` 对象来捕获子进程的输出流（`getInputStream()`）和错误流（`getErrorStream()`）。应用程序可以读取这些流以获得命令的执行结果。

5. **处理和返回结果**：
   - `su` 会将执行结果通过标准输出（stdout）或标准错误（stderr）返回给应用程序。
   - 应用程序可以通过读取 `Process` 的输出流来获取命令的执行结果。例如，如果应用程序执行了 `cat /path/to/protected/file`，结果会通过 `Process.getInputStream()` 读取。
   

**代码流程的举例**：
假设应用程序执行了如下代码来读取一个文件：

```java
Process process = Runtime.getRuntime().exec(new String[]{"su", "-c", "cat /path/to/protected/file"});
BufferedReader reader = new BufferedReader(new InputStreamReader(process.getInputStream()));
String line;
while ((line = reader.readLine()) != null) {
    System.out.println(line);
}
process.waitFor();
```

在这个例子中，`Runtime.getRuntime().exec()` 执行 `su`，并将 `cat /path/to/protected/file` 作为参数传入。`su` 程序在确认权限后，使用 `allow()` 函数中的 `execvp` 执行 `cat` 命令。`cat` 的输出会通过管道传回应用程序，应用程序读取并处理这些输出。

### 总结
应用程序通过执行 `su` 命令并传入需要 root 权限执行的命令，`su` 会根据权限控制和执行逻辑来实际执行命令。执行结果通过标准输出或标准错误返回给应用程序，应用程序则通过进程的输入流读取结果。





### root授权关键日志

```verilog
I ManagerService: root----check package root packagename=ru.andr7e.deviceinfohw.pro uid =10093
I ManagerService: root---check package root packagename=ru.andr7e.deviceinfohw.pro isGranted =true // 拓展功能root应用 打勾
I GrantRoot: root---checkRootable result: 1, response: 1 ,uid:10093 // response: 1 满足root权限
I GrantRoot: root---startGrantRoot, uid:10093 ,ret: 0 // GrantRoot挂载成功
    
D su      : su invoked.// 进入su程序
D su      : Waiting for pid 21556//执行完了，等待下一个指令
```

