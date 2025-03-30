

改动观察

```
vendor/ntimespace/Space9dService/AndroidManifest.xml
vendor/ntimespace/Space9dService/src/com/android/server/Space9dManagerService.java
vendor/ntimespace/Space9dService/src/com/android/server/comm/HttpHelper.java


frameworks/base/core/res/res/values-zh-rCN/strings.xml
frameworks/base/core/res/res/values-zh-rHK/strings.xml
frameworks/base/services/core/java/com/android/server/pm/PackageManagerService.java
```



```java
frameworks/base/services/core/java/com/android/server/pm/PackageManagerService.java
public ParceledListSlice<PackageInfo> getInstalledPackages(int flags, int userId) {
    return mComputer.getInstalledPackages(flags, userId);
}

private static class ComputerTracker implements Computer {
    public final ParceledListSlice<PackageInfo> getInstalledPackages(int flags, int userId) {
        ThreadComputer current = snapshot();
        try {
            return current.mComputer.getInstalledPackages(flags, userId);
        } finally {
            current.release();
        }
    }
}

protected static class ComputerEngine implements Computer {
    public final ParceledListSlice<PackageInfo> getInstalledPackages(int flags, int userId) {
        final int callingUid = Binder.getCallingUid();
        if (getInstantAppPackageName(callingUid) != null) {
            return ParceledListSlice.emptyList();
        }
        if (!mUserManager.exists(userId)) return ParceledListSlice.emptyList();
        flags = updateFlagsForPackage(flags, userId);

        enforceCrossUserPermission(callingUid, userId, false /* requireFullPermission */,
                                   false /* checkShell */, "get installed packages");

        return getInstalledPackagesBody(flags, userId, callingUid);
    }
    protected ParceledListSlice<PackageInfo> getInstalledPackagesBody(int flags, int userId,
                                                                      int callingUid) {
        // writer
        final boolean listUninstalled = (flags & MATCH_KNOWN_PACKAGES) != 0;
        final boolean listApex = (flags & MATCH_APEX) != 0;
        final boolean listFactory = (flags & MATCH_FACTORY_ONLY) != 0;

        ArrayList<PackageInfo> list;
        if (listUninstalled) {
            list = new ArrayList<>(mSettings.getPackagesLocked().size());
            for (PackageSetting ps : mSettings.getPackagesLocked().values()) {
                if (listFactory) {
                    if (!ps.isSystem()) {
                        continue;
                    }
                    PackageSetting psDisabled = mSettings.getDisabledSystemPkgLPr(ps);
                    if (psDisabled != null) {
                        ps = psDisabled;
                    }
                }
                if (filterSharedLibPackageLPr(ps, callingUid, userId, flags)) {
                    continue;
                }
                if (shouldFilterApplicationLocked(ps, callingUid, userId)) {
                    continue;
                }
                final PackageInfo pi = generatePackageInfo(ps, flags, userId);
                if (pi != null) {
                    list.add(pi);
                }
            }
        } else {
            list = new ArrayList<>(mPackages.size());
            for (AndroidPackage p : mPackages.values()) {
                PackageSetting ps = getPackageSetting(p.getPackageName());
                if (listFactory) {
                    if (!p.isSystem()) {
                        continue;
                    }
                    PackageSetting psDisabled = mSettings.getDisabledSystemPkgLPr(ps);
                    if (psDisabled != null) {
                        ps = psDisabled;
                    }
                }
                if (filterSharedLibPackageLPr(ps, callingUid, userId, flags)) {
                    continue;
                }
                if (shouldFilterApplicationLocked(ps, callingUid, userId)) {
                    continue;
                }
                final PackageInfo pi = generatePackageInfo(ps, flags, userId);
                if (pi != null) {
                    list.add(pi);
                }
            }
        }
        if (listApex) {
            if (listFactory) {
                list.addAll(mApexManager.getFactoryPackages());
            } else {
                list.addAll(mApexManager.getActivePackages());
            }
            if (listUninstalled) {
                list.addAll(mApexManager.getInactivePackages());
            }
        }
        return new ParceledListSlice<>(list);
    }
}
```



```
return new ParceledListSlice<>(SystemTracking.get(mContext)
                    .getAppFilter().onPackageFilter(ArrayList<PackageInfo> list));
```





---

源码追踪

frameworks/base/services/core/java/com/android/server/pm/PackageManagerService.java

​	ApplicationInfo ai = SystemTracking.get(mContext).getAppFilter().onAppFilter(raw.applicationInfo);

frameworks/base/services/core/java/com/android/server/space/AppFilter.java

​	public List<ApplicationInfo> onAppFilter(List<ApplicationInfo> ais)

​		if (!mHiddenList.contains(ai.packageName) || callingUid == ai.uid)



private void updateHiddenApps() 

​	    NineDSpaceManager manager = (NineDSpaceManager) mContext.getSystemService(Context.SPACE_SERVICE);

​    	mPrivileges = manager.getHiddenPackages(mHiddenList);

vendor/ntimespace/Space9dService/src/com/android/server/Space9dManagerService.java

​	public int[] getHiddenPackages(List<String> hiddenList) throws RemoteException

​	    IModule module = mModuleManager.getModule(BusinessModule.NAME);

​    BusinessModule bm = (BusinessModule) module;

​    BusinessModule.AppUpdater updater = bm.getUpdater();

vendor/ntimespace/Space9dService/src/com/android/server/module/BusinessModule.java

​	  public AppUpdater getUpdater() { return mUpdater;}

​		mUpdater = new AppUpdater(context, hideCp.combValue, privList);



public void startUpdate() 

HttpHelper.HttpResult result = HttpHelper.doPost(server, body);

mSpecialApps.add(hidedApps.getString(i));

public int[] onUpdateHiddenApps(List<String> hiddenList)

hiddenList.addAll(mSpecialApps);



[2025-03-10 14:06:38] INFO Executing command: ./sh/modify_service_config.sh 0 install_verify https://testcgwdebug.ntimespace.com/cpPis/app/apkList/allow_install

[2025-03-10 14:06:38] INFO Command output:

generating tmp service config with template

Update service config of model: 'install_verify' as enable='true', value='https://testcgwdebug.ntimespace.com/cpPis/app/apkList/allow_install' success





vendor/ntimespace/Space9dService/src/com/android/server/module/BusinessModule.java

HttpHelper.HttpResult result = HttpHelper.doPost(server, body);

server：

/userdata/container/android_data/data_1/misc/s9/service_config.xml 

 <comb name="install_verify" enable="false"></comb>

new AppUpdater(context, hideCp.combValue, privList);

​	AppUpdater(Context context, String server

​		this.server = server;









------------

frameworks/base/services/core/java/com/android/server/pm/PackageManagerService.java

private void installPackagesLI(List<InstallRequest> requests) {



private PrepareResult preparePackageLI(InstallArgs args, PackageInstalledInfo res)

boolean isNotInstallSpecificApp = SystemTracking.get(mContext).getProxy().isNotInstallSpecificApp(args.origin.resolvedPath);



frameworks/base/services/core/java/com/android/server/space/SystemTracking.java

  public ActionProxy getProxy() {

​    return new ActionProxy();

  }

//



vendor/ntimespace/Space9dService/src/com/android/server/Space9dManagerService.java

  public boolean isNotInstallSpecificApp(String apkPath) 

​	 IModule module = mModuleManager.getModule(BusinessModule.NAME);

​    ConfigProperty cp = (ConfigProperty) module.getProp(BusinessModule.NOT_INSTALL_SPECIFIC_APP);





  public boolean installVerify(String apkPath, String packageName) {























---------------------------

frameworks/base/services/core/java/com/android/server/pm/PackageManagerService.java

private PrepareResult preparePackageLI(InstallArgs args, PackageInstalledInfo res)

boolean allow = SystemTracking.get(mContext).getProxy().installVerify(args.origin.resolvedPath,pkgName);

./base/core/java/com/android/internal/space/NineDSpaceManager.java:97:    public boolean installVerify(String apkPath, String packageName) {
./base/core/java/com/android/internal/space/NineDSpaceManager.java:101:                return mService.installVerify(apkPath, packageName);
./base/services/core/java/com/android/server/space/SystemTracking.java:46:        public boolean installVerify(String apkPath, String packageName) {
./base/services/core/java/com/android/server/space/SystemTracking.java:47:            return mSpaceManager.installVerify(apkPath, packageName);
./base/services/core/java/com/android/server/pm/PackageManagerService.java:17926:        boolean allow = SystemTracking.get(mContext).getProxy().installVerify(args.origin.resolvedPath,



code /userdata/container/android_data/data_1/misc/s9/service_config.xml 

<comb name="install_verify" enable="true">https://idc.palmderive.com/cpPis/app/apkList/allow_install</comb>