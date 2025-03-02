现象：

- 云机黑屏，重启，删容器，杀stream都无法恢复



报错：

```log

02-24 16:08:56.484   263   263 I SettingsState: No settings state /data/system/users/0/settings_ssaid.xml
02-24 16:08:56.484   263   263 I SettingsState: directory info for directory/file /data/system/users/0/settings_ssaid.xml with stacktrace
02-24 16:08:56.484   263   263 I SettingsState: java.lang.Exception
02-24 16:08:56.484   263   263 I SettingsState:         at com.android.providers.settings.SettingsState.logSettingsDirectoryInformation(SettingsState.java:753)
02-24 16:08:56.484   263   263 I SettingsState:         at com.android.providers.settings.SettingsState.readStateSyncLocked(SettingsState.java:852)
02-24 16:08:56.484   263   263 I SettingsState:         at com.android.providers.settings.SettingsState.<init>(SettingsState.java:277)
02-24 16:08:56.484   263   263 I SettingsState:         at com.android.providers.settings.SettingsProvider$SettingsRegistry.ensureSettingsStateLocked(SettingsProvider.java:2631)
02-24 16:08:56.484   263   263 I SettingsState:         at com.android.providers.settings.SettingsProvider$SettingsRegistry.ensureSettingsForUserLocked(SettingsProvider.java:2619)
02-24 16:08:56.484   263   263 I SettingsState:         at com.android.providers.settings.SettingsProvider$SettingsRegistry.peekSettingsStateLocked(SettingsProvider.java:2909)
02-24 16:08:56.484   263   263 I SettingsState:         at com.android.providers.settings.SettingsProvider$SettingsRegistry.getSettingsNamesLocked(SettingsProvider.java:2561)
02-24 16:08:56.484   263   263 I SettingsState:         at com.android.providers.settings.SettingsProvider$SettingsRegistry.syncSsaidTableOnStart(SettingsProvider.java:2543)
02-24 16:08:56.484   263   263 I SettingsState:         at com.android.providers.settings.SettingsProvider$SettingsRegistry.<init>(SettingsProvider.java:2439)
02-24 16:08:56.484   263   263 I SettingsState:         at com.android.providers.settings.SettingsProvider.onCreate(SettingsProvider.java:333)
02-24 16:08:56.484   263   263 I SettingsState:         at android.content.ContentProvider.attachInfo(ContentProvider.java:2092)
02-24 16:08:56.484   263   263 I SettingsState:         at android.content.ContentProvider.attachInfo(ContentProvider.java:2066)
02-24 16:08:56.484   263   263 I SettingsState:         at android.app.ActivityThread.installProvider(ActivityThread.java:7065)
02-24 16:08:56.484   263   263 I SettingsState:         at android.app.ActivityThread.installContentProviders(ActivityThread.java:6610)
02-24 16:08:56.484   263   263 I SettingsState:         at android.app.ActivityThread.installSystemProviders(ActivityThread.java:7251)
02-24 16:08:56.484   263   263 I SettingsState:         at com.android.server.am.ActivityManagerService.installSystemProviders(ActivityManagerService.java:7659)
02-24 16:08:56.484   263   263 I SettingsState:         at com.android.server.SystemServer.startOtherServices(SystemServer.java:984)
02-24 16:08:56.484   263   263 I SettingsState:         at com.android.server.SystemServer.run(SystemServer.java:514)
02-24 16:08:56.484   263   263 I SettingsState:         at com.android.server.SystemServer.main(SystemServer.java:351)
02-24 16:08:56.484   263   263 I SettingsState:         at java.lang.reflect.Method.invoke(Native Method)
02-24 16:08:56.484   263   263 I SettingsState:         at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:492)
02-24 16:08:56.484   263   263 I SettingsState:         at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:908)
02-24 16:08:56.484   263   263 I SettingsState: ancestor directory /data/system/users/0 exists
02-24 16:08:56.484   263   263 I SettingsState: ancestor directory /data/system/users/0 permissions: r: true w: true x: true
02-24 16:08:56.484   263   263 I SettingsState: ancestor's parent directory /data/system/users permissions: r: true w: true x: true
02-24 16:08:56.486   263   263 W NineDSpaceManager: warning: no space9d service
02-24 16:08:56.490   263   263 I chatty  : uid=1000 system_server identical 42 lines
02-24 16:08:56.490   263   263 W NineDSpaceManager: warning: no space9d service
02-24 16:08:56.491   263   263 I SystemServer: StartDropBoxManager
02-24 16:08:56.491   263   263 I SystemServiceManager: Starting com.android.server.DropBoxManagerService
02-24 16:08:56.491   263   263 I SystemServer: StartVibratorService
```





解决方法：

```
rm -rf /data/system/users/0/settings_*.xml  

reboot重启
```



造成原因大概率是bin/manage-shell/sh/update_android_id.sh写文件的时候出错了