```yml

12-16 03:02:01.107 23660 23660 I Watchdog: Resuming HandlerChecker: main thread for reason: packagemanagermain. Pause count: 0
12-16 03:02:01.107 23660 23660 E System  : ******************************************
12-16 03:02:01.107 23660 23660 E System  : ************ Failure starting system services
12-16 03:02:01.107 23660 23660 E System  : java.lang.NullPointerException: Attempt to read from field 'java.lang.String android.content.pm.PackageParser$Package.codePath' on a null object reference
12-16 03:02:01.107 23660 23660 E System  :      at com.android.server.pm.PackageManagerService.executeDeletePackageLIF(PackageManagerService.java:20194)
12-16 03:02:01.107 23660 23660 E System  :      at com.android.server.pm.PackageManagerService.deletePackageLIF(PackageManagerService.java:20063)
12-16 03:02:01.107 23660 23660 E System  :      at com.android.server.pm.PackageManagerService.addForInitLI(PackageManagerService.java:9822)
12-16 03:02:01.107 23660 23660 E System  :      at com.android.server.pm.PackageManagerService.scanPackageChildLI(PackageManagerService.java:9537)
12-16 03:02:01.107 23660 23660 E System  :      at com.android.server.pm.PackageManagerService.scanDirLI(PackageManagerService.java:9353)
12-16 03:02:01.107 23660 23660 E System  :      at com.android.server.pm.PackageManagerService.scanDirTracedLI(PackageManagerService.java:9282)
12-16 03:02:01.107 23660 23660 E System  :      at com.android.server.pm.PackageManagerService.<init>(PackageManagerService.java:2772)
12-16 03:02:01.107 23660 23660 E System  :      at com.android.server.pm.PackageManagerService.main(PackageManagerService.java:2369)
12-16 03:02:01.107 23660 23660 E System  :      at com.android.server.SystemServer.startBootstrapServices(SystemServer.java:738)
12-16 03:02:01.107 23660 23660 E System  :      at com.android.server.SystemServer.run(SystemServer.java:512)
12-16 03:02:01.107 23660 23660 E System  :      at com.android.server.SystemServer.main(SystemServer.java:351)
12-16 03:02:01.107 23660 23660 E System  :      at java.lang.reflect.Method.invoke(Native Method)
12-16 03:02:01.107 23660 23660 E System  :      at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:492)
12-16 03:02:01.107 23660 23660 E System  :      at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:908)
12-16 03:02:01.107 23660 23660 E System  :      Suppressed: java.lang.IllegalStateException: Not all tasks finished before calling close: [java.util.concurrent.FutureTask@3057dfa, java.util.concurrent.FutureTask@f14ffab, java.util.concurrent.FutureTask@b192608, java.util.concurrent.FutureTask@57bd1a1, java.util.concurrent.FutureTask@31d7fc6, java.util.concurrent.FutureTask@9a1eb87, java.util.concurrent.FutureTask@11e9ab4, java.util.concurrent.FutureTask@862e6dd, java.util.concurrent.FutureTask@61d252, java.util.concurrent.FutureTask@527b923, java.util.concurrent.FutureTask@64ae20, java.util.concurrent.FutureTask@4ac13d9, java.util.concurrent.FutureTask@e26c19e, java.util.concurrent.FutureTask@3b2c47f]
12-16 03:02:01.107 23660 23660 E System  :              at com.android.server.pm.ParallelPackageParser.close(ParallelPackageParser.java:145)
12-16 03:02:01.107 23660 23660 E System  :              at com.android.server.pm.PackageManagerService.$closeResource(PackageManagerService.java:3583)
12-16 03:02:01.107 23660 23660 E System  :              at com.android.server.pm.PackageManagerService.scanDirLI(PackageManagerService.java:9387)
12-16 03:02:01.107 23660 23660 E System  :              ... 9 more
12-16 03:02:01.107 23660 23660 E Zygote  : System zygote died with exception
12-16 03:02:01.107 23660 23660 E Zygote  : java.lang.NullPointerException: Attempt to read from field 'java.lang.String android.content.pm.PackageParser$Package.codePath' on a null object reference
12-16 03:02:01.107 23660 23660 E Zygote  :      at com.android.server.pm.PackageManagerService.executeDeletePackageLIF(PackageManagerService.java:20194)
12-16 03:02:01.107 23660 23660 E Zygote  :      at com.android.server.pm.PackageManagerService.deletePackageLIF(PackageManagerService.java:20063)
12-16 03:02:01.107 23660 23660 E Zygote  :      at com.android.server.pm.PackageManagerService.addForInitLI(PackageManagerService.java:9822)
12-16 03:02:01.107 23660 23660 E Zygote  :      at com.android.server.pm.PackageManagerService.scanPackageChildLI(PackageManagerService.java:9537)
12-16 03:02:01.107 23660 23660 E Zygote  :      at com.android.server.pm.PackageManagerService.scanDirLI(PackageManagerService.java:9353)
12-16 03:02:01.107 23660 23660 E Zygote  :      at com.android.server.pm.PackageManagerService.scanDirTracedLI(PackageManagerService.java:9282)
12-16 03:02:01.107 23660 23660 E Zygote  :      at com.android.server.pm.PackageManagerService.<init>(PackageManagerService.java:2772)
12-16 03:02:01.107 23660 23660 E Zygote  :      at com.android.server.pm.PackageManagerService.main(PackageManagerService.java:2369)
12-16 03:02:01.107 23660 23660 E Zygote  :      at com.android.server.SystemServer.startBootstrapServices(SystemServer.java:738)
12-16 03:02:01.107 23660 23660 E Zygote  :      at com.android.server.SystemServer.run(SystemServer.java:512)
12-16 03:02:01.107 23660 23660 E Zygote  :      at com.android.server.SystemServer.main(SystemServer.java:351)
12-16 03:02:01.107 23660 23660 E Zygote  :      at java.lang.reflect.Method.invoke(Native Method)
12-16 03:02:01.107 23660 23660 E Zygote  :      at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:492)
12-16 03:02:01.107 23660 23660 E Zygote  :      at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:908)
12-16 03:02:01.107 23660 23660 E Zygote  :      Suppressed: java.lang.IllegalStateException: Not all tasks finished before calling close: [java.util.concurrent.FutureTask@3057dfa, java.util.concurrent.FutureTask@f14ffab, java.util.concurrent.FutureTask@b192608, java.util.concurrent.FutureTask@57bd1a1, java.util.concurrent.FutureTask@31d7fc6, java.util.concurrent.FutureTask@9a1eb87, java.util.concurrent.FutureTask@11e9ab4, java.util.concurrent.FutureTask@862e6dd, java.util.concurrent.FutureTask@61d252, java.util.concurrent.FutureTask@527b923, java.util.concurrent.FutureTask@64ae20, java.util.concurrent.FutureTask@4ac13d9, java.util.concurrent.FutureTask@e26c19e, java.util.concurrent.FutureTask@3b2c47f]
12-16 03:02:01.107 23660 23660 E Zygote  :              at com.android.server.pm.ParallelPackageParser.close(ParallelPackageParser.java:145)
12-16 03:02:01.107 23660 23660 E Zygote  :              at com.android.server.pm.PackageManagerService.$closeResource(PackageManagerService.java:3583)
12-16 03:02:01.107 23660 23660 E Zygote  :              at com.android.server.pm.PackageManagerService.scanDirLI(PackageManagerService.java:9387)
12-16 03:02:01.107 23660 23660 E Zygote  :              ... 9 more
12-16 03:02:01.107 23660 23660 D AndroidRuntime: Shutting down VM
12-16 03:02:01.107 23660 23660 E AndroidRuntime: *** FATAL EXCEPTION IN SYSTEM PROCESS: main
12-16 03:02:01.107 23660 23660 E AndroidRuntime: java.lang.NullPointerException: Attempt to read from field 'java.lang.String android.content.pm.PackageParser$Package.codePath' on a null object reference
12-16 03:02:01.107 23660 23660 E AndroidRuntime:        at com.android.server.pm.PackageManagerService.executeDeletePackageLIF(PackageManagerService.java:20194)
12-16 03:02:01.107 23660 23660 E AndroidRuntime:        at com.android.server.pm.PackageManagerService.deletePackageLIF(PackageManagerService.java:20063)
12-16 03:02:01.107 23660 23660 E AndroidRuntime:        at com.android.server.pm.PackageManagerService.addForInitLI(PackageManagerService.java:9822)
12-16 03:02:01.107 23660 23660 E AndroidRuntime:        at com.android.server.pm.PackageManagerService.scanPackageChildLI(PackageManagerService.java:9537)
12-16 03:02:01.107 23660 23660 E AndroidRuntime:        at com.android.server.pm.PackageManagerService.scanDirLI(PackageManagerService.java:9353)
12-16 03:02:01.107 23660 23660 E AndroidRuntime:        at com.android.server.pm.PackageManagerService.scanDirTracedLI(PackageManagerService.java:9282)
12-16 03:02:01.107 23660 23660 E AndroidRuntime:        at com.android.server.pm.PackageManagerService.<init>(PackageManagerService.java:2772)
12-16 03:02:01.107 23660 23660 E AndroidRuntime:        at com.android.server.pm.PackageManagerService.main(PackageManagerService.java:2369)
12-16 03:02:01.107 23660 23660 E AndroidRuntime:        at com.android.server.SystemServer.startBootstrapServices(SystemServer.java:738)
12-16 03:02:01.107 23660 23660 E AndroidRuntime:        at com.android.server.SystemServer.run(SystemServer.java:512)
12-16 03:02:01.107 23660 23660 E AndroidRuntime:        at com.android.server.SystemServer.main(SystemServer.java:351)
12-16 03:02:01.107 23660 23660 E AndroidRuntime:        at java.lang.reflect.Method.invoke(Native Method)
12-16 03:02:01.107 23660 23660 E AndroidRuntime:        at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:492)
12-16 03:02:01.107 23660 23660 E AndroidRuntime:        at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:908)
12-16 03:02:01.107 23660 23660 E AndroidRuntime:        Suppressed: java.lang.IllegalStateException: Not all tasks finished before calling close: [java.util.concurrent.FutureTask@3057dfa, java.util.concurrent.FutureTask@f14ffab, java.util.concurrent.FutureTask@b192608, java.util.concurrent.FutureTask@57bd1a1, java.util.concurrent.FutureTask@31d7fc6, java.util.concurrent.FutureTask@9a1eb87, java.util.concurrent.FutureTask@11e9ab4, java.util.concurrent.FutureTask@862e6dd, java.util.concurrent.FutureTask@61d252, java.util.concurrent.FutureTask@527b923, java.util.concurrent.FutureTask@64ae20, java.util.concurrent.FutureTask@4ac13d9, java.util.concurrent.FutureTask@e26c19e, java.util.concurrent.FutureTask@3b2c47f]
12-16 03:02:01.107 23660 23660 E AndroidRuntime:                at com.android.server.pm.ParallelPackageParser.close(ParallelPackageParser.java:145)
12-16 03:02:01.107 23660 23660 E AndroidRuntime:                at com.android.server.pm.PackageManagerService.$closeResource(PackageManagerService.java:3583)
12-16 03:02:01.107 23660 23660 E AndroidRuntime:                at com.android.server.pm.PackageManagerService.scanDirLI(PackageManagerService.java:9387)
12-16 03:02:01.107 23660 23660 E AndroidRuntime:                ... 9 more
12-16 03:02:01.108 23660 23660 E AndroidRuntime: Error reporting crash
12-16 03:02:01.108 23660 23660 E AndroidRuntime: java.lang.NullPointerException: Attempt to invoke interface method 'void android.app.IActivityManager.handleApplicationCrash(android.os.IBinder, android.app.ApplicationErrorReport$ParcelableCrashInfo)' on a null object reference
12-16 03:02:01.108 23660 23660 E AndroidRuntime:        at com.android.internal.os.RuntimeInit$KillApplicationHandler.uncaughtException(RuntimeInit.java:145)
12-16 03:02:01.108 23660 23660 E AndroidRuntime:        at java.lang.ThreadGroup.uncaughtException(ThreadGroup.java:1073)
12-16 03:02:01.108 23660 23660 E AndroidRuntime:        at java.lang.ThreadGroup.uncaughtException(ThreadGroup.java:1068)
12-16 03:02:01.108 23660 23660 E AndroidRuntime:        at java.lang.Thread.dispatchUncaughtException(Thread.java:2187)
12-16 03:02:01.108 23660 23660 I Process : Sending signal. PID: 23660 SIG: 9
```



