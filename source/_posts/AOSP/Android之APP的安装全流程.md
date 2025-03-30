PM的架构

应用层：PackageInstaller 负责用户界面和安装会话管理的app

框架层：

- PackageManagerService：核心服务
- PackageParser   ：解析APK文件的Manifest文件，提取应用信息。
- ApplicationPackageManager：提供应用层与PMS的接口

HAL层：无

内核层：installd：负责APK文件的实际安装操作，如解压、复制、权限设置（Linux）



