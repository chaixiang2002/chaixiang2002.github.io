[Android 性能优化 五 性能分析工具dumpsys的使用_android dumpsys-CSDN博客](https://blog.csdn.net/androiddevelop/article/details/37689339?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-37689339-blog-119522548.235%5Ev43%5Epc_blog_bottom_relevance_base7&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-37689339-blog-119522548.235%5Ev43%5Epc_blog_bottom_relevance_base7&utm_relevant_index=2)











`dumpsys package` 是一个 Android 调试命令，可以用来获取设备上包管理器 (Package Manager) 的详细信息。这个命令输出的信息非常详尽，包括应用程序包的信息、权限、用户、活动、服务、广播

接收器等。以下是一些常见的使用方法和示例：

### 基本用法

```sh
adb shell dumpsys package
```

这个命令会输出所有安装在设备上的包的信息。由于输出信息量很大，可以使用 `grep` 或 `find` 命令来筛选特定信息。

### 查看特定应用包的信息

```sh
adb shell dumpsys package <package-name>
```

例如，查看 `com.android.settings` 包的信息：

```sh
adb shell dumpsys package com.android.settings
```

### 过滤输出信息

1. **查看已安装的包列表：**

```sh
adb shell dumpsys package packages
```

2. **查看特定应用的权限：**

```sh
adb shell dumpsys package <package-name> | grep granted=true
```

3. **查看正在运行的服务：**

```sh
adb shell dumpsys package services
```

4. **查看特定应用的活动（activities）：**

```sh
adb shell dumpsys package <package-name> | grep Activity
```

### 示例

假设我们要查看 `com.android.chrome` 的详细信息：

```sh
adb shell dumpsys package com.android.chrome
```

输出可能包括：

- **包名 (Package name)：** com.android.chrome
- **版本信息 (Version)：** 版本代码和版本名称
- **安装位置 (Install location)：** 内部存储或外部存储
- **用户信息 (User information)：** 哪些用户安装了该应用
- **权限信息 (Permissions)：** 应用申请的权限及其状态
- **活动 (Activities)：** 应用中的活动列表
- **服务 (Services)：** 应用中的服务列表
- **广播接收器 (Broadcast Receivers)：** 应用中的广播接收器
- **提供者 (Providers)：** 应用中的内容提供者

### 高级用法

1. **查看权限被授予的应用列表：**

```sh
adb shell dumpsys package | grep granted=true
```

2. **查看应用安装位置：**

```sh
adb shell dumpsys package | grep -A 1 'Package \['
```

3. **查看特定用户的应用列表：**

```sh
adb shell dumpsys package --user <user-id>
```

例如，查看用户0的应用列表：

```sh
adb shell dumpsys package --user 0
```

### 过滤输出

由于 `dumpsys package` 的输出信息非常多，可以将输出重定向到文件，方便后续查看和分析：

```sh
adb shell dumpsys package > package_info.txt
```

然后在本地机器上使用文本编辑器或命令行工具进行查看和分析。

### 总结

`dumpsys package` 是一个非常强大的命令，可以帮助开发者和调试人员详细了解设备上应用包的各种信息。通过不同的过滤和筛选方式，可以快速获取所需的特定信息。希望这些示例和用法对你有所帮助！
