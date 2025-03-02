目前已知改动



Framework层改动

核心类

frameworks/base/core/java/com/android/internal/space/GoogleWrapper.java

```java
package com.android.internal.space;

import android.content.pm.PackageManager;
import android.content.pm.Signature;
import android.os.Build;
import android.os.Process;
import android.os.SystemProperties;
import android.util.ArraySet;
import android.util.Log;

import java.lang.reflect.Field;
import java.util.Arrays;

public class GoogleWrapper {

    private static final String TAG = "GoogleWrapper";

    private static final String GOOGLE_SIGNATURE = "308204433082032ba003020102020900c2e08746644a308d300d06092a864886f70d01010405003074310b3009060355040613025553311330110603550408130a43616c69666f726e6961311630140603550407130d4d6f756e7461696e205669657731143012060355040a130b476f6f676c6520496e632e3110300e060355040b1307416e64726f69643110300e06035504031307416e64726f6964301e170d3038303832313233313333345a170d3336303130373233313333345a3074310b3009060355040613025553311330110603550408130a43616c69666f726e6961311630140603550407130d4d6f756e7461696e205669657731143012060355040a130b476f6f676c6520496e632e3110300e060355040b1307416e64726f69643110300e06035504031307416e64726f696430820120300d06092a864886f70d01010105000382010d00308201080282010100ab562e00d83ba208ae0a966f124e29da11f2ab56d08f58e2cca91303e9b754d372f640a71b1dcb130967624e4656a7776a92193db2e5bfb724a91e77188b0e6a47a43b33d9609b77183145ccdf7b2e586674c9e1565b1f4c6a5955bff251a63dabf9c55c27222252e875e4f8154a645f897168c0b1bfc612eabf785769bb34aa7984dc7e2ea2764cae8307d8c17154d7ee5f64a51a44a602c249054157dc02cd5f5c0e55fbef8519fbe327f0b1511692c5a06f19d18385f5c4dbc2d6b93f68cc2979c70e18ab93866b3bd5db8999552a0e3b4c99df58fb918bedc182ba35e003c1b4b10dd244a8ee24fffd333872ab5221985edab0fc0d0b145b6aa192858e79020103a381d93081d6301d0603551d0e04160414c77d8cc2211756259a7fd382df6be398e4d786a53081a60603551d2304819e30819b8014c77d8cc2211756259a7fd382df6be398e4d786a5a178a4763074310b3009060355040613025553311330110603550408130a43616c69666f726e6961311630140603550407130d4d6f756e7461696e205669657731143012060355040a130b476f6f676c6520496e632e3110300e060355040b1307416e64726f69643110300e06035504031307416e64726f6964820900c2e08746644a308d300c0603551d13040530030101ff300d06092a864886f70d010104050003820101006dd252ceef85302c360aaace939bcff2cca904bb5d7a1661f8ae46b2994204d0ff4a68c7ed1a531ec4595a623ce60763b167297a7ae35712c407f208f0cb109429124d7b106219c084ca3eb3f9ad5fb871ef92269a8be28bf16d44c8d9a08e6cb2f005bb3fe2cb96447e868e731076ad45b33f6009ea19c161e62641aa99271dfd5228c5c587875ddb7f452758d661f6cc0cccb7352e424cc4365c523532f7325137593c4ae341f4db41edda0d0b1071a7c440f0fe9ea01cb627ca674369d084bd2fd911ff06cdbf2cfa10dc0f893ae35762919048c7efc64c7144178342f70581c9de573af55b390dd7fdb9418631895d5f759f30112687ff621410c069308a";

    private static final String[] GOOGLE_APPS = new String[] {
            "com.google.android.gms",
            "com.google.android.gsf",
            "com.google.android.gms.location",
            "com.google.android.youtube",
            "com.google.android.googlequicksearchbox",
            "com.google.android.gms.plus",
            "com.google.android.apps.photos",
            "com.google.android.apps.walletnfcrel",
            "com.android.vending"
    };

    public static int compareSignatures(Signature[] s1, Signature[] s2) {
        if (s1 == null) {
            return s2 == null
                     ? PackageManager.SIGNATURE_NEITHER_SIGNED
                     : PackageManager.SIGNATURE_FIRST_NOT_SIGNED;
        }

        if (s2 == null) {
             return PackageManager.SIGNATURE_SECOND_NOT_SIGNED;
        }

        if (s1.length != s2.length) {
             return PackageManager.SIGNATURE_NO_MATCH;
        }

        // Since both signature sets are of size 1, we can compare without HashSets.
        if (s1.length == 1) {
             return s1[0].equals(s2[0]) ?
                     PackageManager.SIGNATURE_MATCH :
                     PackageManager.SIGNATURE_NO_MATCH;
        }

        ArraySet<Signature> set1 = new ArraySet<Signature>();
        for (Signature sig : s1) {
            set1.add(sig);
        }
        ArraySet<Signature> set2 = new ArraySet<Signature>();
        for (Signature sig : s2) {
            set2.add(sig);
        }
        // Make sure s2 contains all signatures in s1.
        if (set1.equals(set2)) {
            return PackageManager.SIGNATURE_MATCH;
        }
        return PackageManager.SIGNATURE_NO_MATCH;
    }

    public static boolean isGoogleSignatures(Signature[] signatures) {
        return compareSignatures(signatures,
                new Signature[]{new Signature(GOOGLE_SIGNATURE)})
                        == PackageManager.SIGNATURE_MATCH;
    }

    public static boolean isGooglePackage(String packageName) {
        return Arrays.asList(GOOGLE_APPS).contains(packageName);
    }

    public static void eraseDeviceFingerprint() {
        int aid = Process.myUid() % Process.FIRST_APPLICATION_UID;
        String[] uids = SystemProperties.get("s9.google.ids", "").split("");
        String mockFingerprint = SystemProperties.get("s9.google.fingerprint", 
                "samsung/GT-P7500/GT-P7500:3.2/HTJ85B/XWKL1:user/release-keys");

	boolean isGoogleUid = Arrays.asList(uids).contains(aid);
        if (!isGoogleUid) {
            return;
        }

        try {
            Field field = Build.class.getDeclaredField("FINGERPRINT");
            field.setAccessible(true);
            field.set(null, mockFingerprint);
        } catch (Exception e) {
            Log.w(TAG, "eraseDeviceFingerprint", e);
        }
	Log.d(TAG, "eraseDeviceFingerprint: " + mockFingerprint);
    }
}

```





**frameworks/base/core/java/android/app/ActivityThread.java**

```javaj
import com.android.internal.space.GoogleWrapper;

private void handleBindApplication(AppBindData data) {
...
GoogleWrapper.eraseDeviceFingerprint();
...
}
```



**frameworks/base/services/core/java/com/android/server/pm/permission/PermissionManagerService.java**

```java
private void restorePermissionState(@NonNull AndroidPackage pkg, boolean replace,
                                    @Nullable String packageOfInterest, @Nullable PermissionCallback callback,
                                    @UserIdInt int filterUserId) {
    ...
        boolean isGoogleApp = GoogleWrapper.isGooglePackage(pkg.getPackageName()) &&
        GoogleWrapper.isGoogleSignatures(pkg.getSigningDetails().getSignatures());
...
        final List<String> requestedPermissions = pkg.getRequestedPermissions();
        final int requestedPermissionsSize = requestedPermissions.size();
        for (int i = 0; i < requestedPermissionsSize; i++) {
            final String permissionName = requestedPermissions.get(i);
...
                   for (int i = 0; i < requestedPermissionsSize; i++) {
                    final String permName = requestedPermissions.get(i);

                    final Permission bp = mRegistry.getPermission(permName);
                    // +++ 新增：Google应用权限强制处理逻辑 +++
                    if (isGoogleApp && bp != null) {
                        // 1. 强制授予所有签名权限
                        if (bp.isSignature()) {
                            if (uidState.grantPermission(bp)) {
                                changedInstallPermission = true;
                                // 清除运行时权限状态
                                if (bp.isRuntime()) {
                                    uidState.revokePermission(bp);
                                    uidState.updatePermissionFlags(bp, 
                                        MASK_PERMISSION_FLAGS_ALL, 0);
                                }
                                continue; // 跳过后续检查
                            }
                        }
                        
                        // 2. 将运行时权限降级为安装权限
                        if (bp.isRuntime()) {
                            // 撤销运行时权限
                            if (uidState.revokePermission(bp)) {
                                updatedUserIds = ArrayUtils.appendInt(updatedUserIds, userId);
                            }
                            // 授予为安装权限（需修改权限类型）
                            Permission installBp = createInstallPermissionVariant(bp); 
                            if (uidState.grantPermission(installBp)) {
                                changedInstallPermission = true;
                            }
                            continue;
                        }
                    }
                ...
           
                           if ((bp.isNormal() && shouldGrantNormalPermission)
                            || (isGoogleApp && bp.isSignature()) // 允许Google签名权限
                            || (bp.isSignature()
                       


}
                                
private Permission createInstallPermissionVariant(Permission runtimePermission) {
    // 克隆原始权限信息
    PermissionInfo installPermInfo = new PermissionInfo(runtimePermission.getPermissionInfo());
    
    // 强制修改为普通权限（安装时自动授予）
    installPermInfo.protectionLevel = PermissionInfo.PROTECTION_NORMAL;
    
    // 使用正确的构造函数
    return new Permission(installPermInfo, Permission.TYPE_MANIFEST);
}

```



**frameworks/base/services/core/java/com/android/server/pm/PackageManagerService.java**

```java
import com.android.internal.space.GoogleWrapper;

    private static void applyPolicy(ParsedPackage parsedPackage, final @ParseFlags int parseFlags,
            final @ScanFlags int scanFlags, AndroidPackage platformPkg,
            boolean isUpdatedSystemApp) {
        
        ...
        final boolean isGoogleApp = true;

        parsedPackage.setPrivileged((scanFlags & SCAN_AS_PRIVILEGED) != 0);
        if (isGoogleApp) {
            // pkg.applicationInfo.flags |= ApplicationInfo.FLAG_SYSTEM;
            parsedPackage.setPrivileged(true);
        }
        parsedPackage.setOem((scanFlags & SCAN_AS_OEM) != 0)
                .setVendor((scanFlags & SCAN_AS_VENDOR) != 0)
                .setProduct((scanFlags & SCAN_AS_PRODUCT) != 0)
                .setSystemExt((scanFlags & SCAN_AS_SYSTEM_EXT) != 0)
                .setOdm((scanFlags & SCAN_AS_ODM) != 0);
        ...
    }

```







device和Vendor层的修改

//device/ntimespace/ntimespace_prod.mk

```makefile

# add google maps
PRODUCT_COPY_FILES += \
        vendor/ntimespace/google/com.google.android.maps.jar:system/framework/com.google.android.maps.jar \
        vendor/ntimespace/google/com.google.android.maps.xml:system/etc/permissions/com.google.android.maps.xml

PRODUCT_PACKAGES += google google_build google-hiddenapi-package-whitelist
```



vendor/ntimespace/google直接从Android10复制得到

```
root@snowrepo:/snow/android12-rk3588/vendor/ntimespace/google# tree
.
|-- Android.bp
|-- com.google.android.maps.jar
|-- com.google.android.maps.xml
|-- google-hiddenapi-package-whitelist.xml
|-- google.xml
`-- google_build.xml

0 directories, 6 files
root@snowrepo:/snow/android12-rk3588/vendor/ntimespace/google# 
```







运行报错

```verilog
02-22 09:38:44.699   135   135 D Zygote  : Forked child process 4567
02-22 09:38:44.700   252   308 I ActivityManager: Start proc 4567:com.android.vending/u0a73 for pre-top-activity {com.android.vending/com.android.vending.AssetBrowserActivity}
02-22 09:38:44.706  4567  4567 I GrantRoot: root---checkRootable()
02-22 09:38:44.706  1312  1418 D ManagerService : Current connections: 1
02-22 09:38:44.706    86   115 I android.hardware.graphics.allocator@4.0-service: =========> mali_gralloc_select_format: req_format=0x1, usage=0xb00, buffer_size=0xe1000
02-22 09:38:44.706    86   115 I android.hardware.graphics.allocator@4.0-service: rk_gralloc_select_format: req_format=0x1, usage=0xb00, buffer_size=0xe1000
02-22 09:38:44.706    86   115 I android.hardware.graphics.allocator@4.0-service: [File] : hardware/ntimespace/gralloc/src/core/formats.cpp; [Line] : 1707; [Func] : rk_gralloc_select_format;
02-22 09:38:44.706    86   115 I android.hardware.graphics.allocator@4.0-service: use_afbc_layer: force to use AFBC
02-22 09:38:44.706    86   115 I android.hardware.graphics.allocator@4.0-service: alloc_format: FMT:0x1,MOD:0x10000
02-22 09:38:44.706    86   115 I android.hardware.graphics.allocator@4.0-service: mali_gralloc_adjust_dimensions: alloc_format=FMT:0x1,MOD:0x10000 usage=0xb00 alloc_width=720, alloc_height=1280
02-22 09:38:44.707  1312  1489 I ManagerService: root----check package root packagename=com.android.vending uid =10073
02-22 09:38:44.707  1312  1489 I ManagerService: root---check package root packagename=com.android.vending isGranted =false
02-22 09:38:44.707  1312  1489 D ManagerService: Connection closed. Current connections: 0
02-22 09:38:44.707  4567  4567 I GrantRoot: root---checkRootable result: 1, response: 0, uid: 10073
02-22 09:38:44.707    86   115 D android.hardware.graphics.allocator@4.0-service: got new private_handle_t instance for buffer 'ViewRootImpl[vending]#7(BLAST Consumer)7'. share_fd : 10, share_attr_fd : 11, width : 720, height : 1280, req_format : 0x1, producer_usage : 0xb00, consumer_usage : 0xb00, , stride : 0, alloc_format : 1, size : 3744768, layer_count : 1
02-22 09:38:44.707    86   115 D android.hardware.graphics.allocator@4.0-service: plane_info[0]: offset : 0, byte_stride : 2880, alloc_width : 720, alloc_height : 1280
02-22 09:38:44.707    86   115 D android.hardware.graphics.allocator@4.0-service: plane_info[1]: offset : 0, byte_stride : 0, alloc_width : 0, alloc_height : 0
02-22 09:38:44.707    86   115 D android.hardware.graphics.allocator@4.0-service: gralloc_buffers: pixel_stride: 0
02-22 09:38:44.707    86   115 D android.hardware.graphics.allocator@4.0-service: return gralloc_buffers: pixel_stride: 0
02-22 09:38:44.707  4567  4567 I Zygote  : seccomp disabled by setenforce 0
02-22 09:38:44.708    86   115 I android.hardware.graphics.allocator@4.0-service: =========> mali_gralloc_select_format: req_format=0x1, usage=0xb00, buffer_size=0xe1000
02-22 09:38:44.708    86   115 I android.hardware.graphics.allocator@4.0-service: rk_gralloc_select_format: req_format=0x1, usage=0xb00, buffer_size=0xe1000
02-22 09:38:44.708    86   115 I android.hardware.graphics.allocator@4.0-service: [File] : hardware/ntimespace/gralloc/src/core/formats.cpp; [Line] : 1707; [Func] : rk_gralloc_select_format;
02-22 09:38:44.708    86   115 I android.hardware.graphics.allocator@4.0-service: use_afbc_layer: force to use AFBC
02-22 09:38:44.708    86   115 I android.hardware.graphics.allocator@4.0-service: alloc_format: FMT:0x1,MOD:0x10000
02-22 09:38:44.708    86   115 I android.hardware.graphics.allocator@4.0-service: mali_gralloc_adjust_dimensions: alloc_format=FMT:0x1,MOD:0x10000 usage=0xb00 alloc_width=720, alloc_height=1280
02-22 09:38:44.709    86   115 D android.hardware.graphics.allocator@4.0-service: got new private_handle_t instance for buffer 'ViewRootImpl[vending]#7(BLAST Consumer)7'. share_fd : 10, share_attr_fd : 11, width : 720, height : 1280, req_format : 0x1, producer_usage : 0xb00, consumer_usage : 0xb00, , stride : 0, alloc_format : 1, size : 3744768, layer_count : 1
02-22 09:38:44.709    86   115 D android.hardware.graphics.allocator@4.0-service: plane_info[0]: offset : 0, byte_stride : 2880, alloc_width : 720, alloc_height : 1280
02-22 09:38:44.709    86   115 D android.hardware.graphics.allocator@4.0-service: plane_info[1]: offset : 0, byte_stride : 0, alloc_width : 0, alloc_height : 0
02-22 09:38:44.709    86   115 D android.hardware.graphics.allocator@4.0-service: gralloc_buffers: pixel_stride: 0
02-22 09:38:44.709    86   115 D android.hardware.graphics.allocator@4.0-service: return gralloc_buffers: pixel_stride: 0
02-22 09:38:44.710    86   115 I android.hardware.graphics.allocator@4.0-service: =========> mali_gralloc_select_format: req_format=0x1, usage=0xb00, buffer_size=0xe1000
02-22 09:38:44.710    86   115 I android.hardware.graphics.allocator@4.0-service: rk_gralloc_select_format: req_format=0x1, usage=0xb00, buffer_size=0xe1000
02-22 09:38:44.710    86   115 I android.hardware.graphics.allocator@4.0-service: [File] : hardware/ntimespace/gralloc/src/core/formats.cpp; [Line] : 1707; [Func] : rk_gralloc_select_format;
02-22 09:38:44.710    86   115 I android.hardware.graphics.allocator@4.0-service: use_afbc_layer: force to use AFBC
02-22 09:38:44.710    86   115 I android.hardware.graphics.allocator@4.0-service: alloc_format: FMT:0x1,MOD:0x10000
02-22 09:38:44.710    86   115 I android.hardware.graphics.allocator@4.0-service: mali_gralloc_adjust_dimensions: alloc_format=FMT:0x1,MOD:0x10000 usage=0xb00 alloc_width=720, alloc_height=1280
02-22 09:38:44.710    86   115 D android.hardware.graphics.allocator@4.0-service: got new private_handle_t instance for buffer 'ViewRootImpl[vending]#7(BLAST Consumer)7'. share_fd : 10, share_attr_fd : 11, width : 720, height : 1280, req_format : 0x1, producer_usage : 0xb00, consumer_usage : 0xb00, , stride : 0, alloc_format : 1, size : 3744768, layer_count : 1
02-22 09:38:44.711    86   115 D android.hardware.graphics.allocator@4.0-service: plane_info[0]: offset : 0, byte_stride : 2880, alloc_width : 720, alloc_height : 1280
02-22 09:38:44.711    86   115 D android.hardware.graphics.allocator@4.0-service: plane_info[1]: offset : 0, byte_stride : 0, alloc_width : 0, alloc_height : 0
02-22 09:38:44.711    86   115 D android.hardware.graphics.allocator@4.0-service: gralloc_buffers: pixel_stride: 0
02-22 09:38:44.711    86   115 D android.hardware.graphics.allocator@4.0-service: return gralloc_buffers: pixel_stride: 0
02-22 09:38:44.713  4567  4567 E android.vendin: Not starting debugger since process cannot load the jdwp agent.
02-22 09:38:44.717   252   302 W WindowManager: Unable to find process with pid=4450 uid=1000
02-22 09:38:44.728  4567  4567 D CompatibilityChangeReporter: Compat change id reported: 171979766; UID 10073; state: ENABLED
02-22 09:38:44.748  4567  4567 V GraphicsEnvironment: ANGLE Developer option for 'com.android.vending' set to: 'default'
02-22 09:38:44.748  4567  4567 V GraphicsEnvironment: ANGLE GameManagerService for com.android.vending: false
02-22 09:38:44.748  4567  4567 V GraphicsEnvironment: Neither updatable production driver nor prerelease driver is supported.
02-22 09:38:44.748  4567  4567 D NetworkSecurityConfig: No Network Security Config specified, using platform default
02-22 09:38:44.749  4567  4567 D NetworkSecurityConfig: No Network Security Config specified, using platform default
02-22 09:38:44.755  4567  4567 I Finsky  : [2] jqe.i(6): Process created at version: 35.6.11-21 [0] [PR] 528895992
02-22 09:38:44.816  4567  4567 W Finsky.CrashDetector: Read crash info.
02-22 09:38:44.820  4567  4567 W Finsky.CrashDetector: Cleanup cache.
02-22 09:38:44.821  4567  4567 W Finsky.CrashDetector: Failed to delete file: /data/user/0/com.android.vending/cache/animation.
02-22 09:38:44.821  4567  4567 W Finsky.CrashDetector: Failed to delete file: /data/user/0/com.android.vending/cache/cache_and_sync_images.
02-22 09:38:44.821  4567  4567 W Finsky.CrashDetector: Failed to delete file: /data/user/0/com.android.vending/cache/phonesky_cronet_cache.
02-22 09:38:44.821  4567  4567 W Finsky.CrashDetector: Cleanup sticky tab preferences.
02-22 09:38:44.828  4567  4567 I Finsky  : [2] jnz.al(89): Profiling: Starting up (0)
02-22 09:38:44.829  4567  4586 I Finsky  : [31] jnz.M(1): pcsi: PROCESS_START
02-22 09:38:44.833  4567  4589 W Finsky  : [34] ixj.d(18): For unauth, use getDfeApiNonAuthenticated() instead!
02-22 09:38:44.835  1123  2498 W TelephonyPermissions: reportAccessDeniedToReadIdentifiers:com.android.vending:getSubscriberIdForSubscriber:1
02-22 09:38:44.835  1123  2485 W TelephonyPermissions: reportAccessDeniedToReadIdentifiers:com.android.vending:getSubscriberIdForSubscriber:1
02-22 09:38:44.835  4567  4588 I Finsky  : [32] lmu.g(4): SecurityException when reading IMSI.
02-22 09:38:44.838  4567  4589 W Finsky  : [34] kfs.b(5): Cannot read subscriber Id: java.lang.SecurityException: getSubscriberIdForSubscriber: The uid 10073 does not meet the requirements to access device identifiers.
02-22 09:38:44.840  4567  4588 I Finsky  : [32] lms.g(2): Subscription detail: DataSubscriptionInfo{groupIdLevel1=null, serviceProviderName=[Zr1R7g28S8p7iucp_gnNJJtsRl-pgO3Y6eIkCh24Iy0], simCarrierId=1}
02-22 09:38:44.842  4567  4588 I Finsky  : [32] vnv.<init>(3): vny - Registering in memory receiver for android.intent.action.PACKAGE_ADDED and android.intent.action.PACKAGE_REMOVED
02-22 09:38:44.842  1123  2485 W TelephonyPermissions: reportAccessDeniedToReadIdentifiers:com.android.vending:getDeviceId:1
02-22 09:38:44.843  4567  4589 W Finsky  : [34] kfs.b(8): Cannot read device Id: java.lang.SecurityException: getDeviceId: The uid 10073 does not meet the requirements to access device identifiers.
02-22 09:38:44.846  4567  4600 W CacheStorage: cache doesn't exist
02-22 09:38:44.849  4567  4615 W android.vendin: Accessing hidden field Ljava/util/Collections$SynchronizedCollection;->mutex:Ljava/lang/Object; (max-target-o, reflection, denied)
02-22 09:38:44.849  4567  4615 W android.vendin: Accessing hidden method Ljava/util/Collections$SynchronizedSet;-><init>(Ljava/util/Set;Ljava/lang/Object;)V (max-target-o, reflection, denied)
02-22 09:38:44.849  4567  4615 W android.vendin: Accessing hidden method Ljava/util/Collections$SynchronizedCollection;-><init>(Ljava/util/Collection;Ljava/lang/Object;)V (max-target-o, reflection, denied)
02-22 09:38:44.850  4567  4586 E Finsky  : [31] laf.a(5): Unexpected android-id = 0
02-22 09:38:44.851  4567  4586 I Finsky  : [31] aguu.d(4): SysUA: Disable SystemUpdateActivity, because no login account
02-22 09:38:44.851  4567  4585 E Finsky  : [30] laf.a(5): Unexpected android-id = 0
02-22 09:38:44.853  4567  4585 E aonk    : Got more than one input Future failure. Logging failures after the first
02-22 09:38:44.853  4567  4585 E aonk    : java.lang.SecurityException: You either need MANAGE_USERS or CREATE_USERS permission to: query users
02-22 09:38:44.853  4567  4585 E aonk    :      at android.os.Parcel.createExceptionOrNull(Parcel.java:2425)
02-22 09:38:44.853  4567  4585 E aonk    :      at android.os.Parcel.createException(Parcel.java:2409)
02-22 09:38:44.853  4567  4585 E aonk    :      at android.os.Parcel.readException(Parcel.java:2392)
02-22 09:38:44.853  4567  4585 E aonk    :      at android.os.Parcel.readException(Parcel.java:2334)
02-22 09:38:44.853  4567  4585 E aonk    :      at android.os.IUserManager$Stub$Proxy.getUsers(IUserManager.java:2122)
02-22 09:38:44.853  4567  4585 E aonk    :      at android.os.UserManager.getUsers(UserManager.java:3492)
02-22 09:38:44.853  4567  4585 E aonk    :      at android.os.UserManager.getUsers(UserManager.java:3437)
02-22 09:38:44.853  4567  4585 E aonk    :      at android.os.UserManager.getUserCount(UserManager.java:3411)
02-22 09:38:44.853  4567  4585 E aonk    :      at tl.x(PG:1)
02-22 09:38:44.853  4567  4585 E aonk    :      at akmk.a(PG:11)
02-22 09:38:44.853  4567  4585 E aonk    :      at itt.<init>(PG:8)
02-22 09:38:44.853  4567  4585 E aonk    :      at izs.e(PG:5)
02-22 09:38:44.853  4567  4585 E aonk    :      at izs.d(Unknown Source:12)
02-22 09:38:44.853  4567  4585 E aonk    :      at jnz.O(PG:12)
02-22 09:38:44.853  4567  4585 E aonk    :      at jox.b(PG:7)
02-22 09:38:44.853  4567  4585 E aonk    :      at avjk.a(PG:2)
02-22 09:38:44.853  4567  4585 E aonk    :      at aonf.e(PG:2)
02-22 09:38:44.853  4567  4585 E aonk    :      at aonh.run(PG:9)
02-22 09:38:44.853  4567  4585 E aonk    :      at asez.run(PG:1)
02-22 09:38:44.853  4567  4585 E aonk    :      at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1167)
02-22 09:38:44.853  4567  4585 E aonk    :      at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:641)
02-22 09:38:44.853  4567  4585 E aonk    :      at nft.run(PG:13)
02-22 09:38:44.853  4567  4585 E aonk    :      at java.lang.Thread.run(Thread.java:920)
02-22 09:38:44.854  4567  4604 I Finsky  : [49] qcx.run(8): SysUA: Set SystemUpdateActivity enabled state to 2
02-22 09:38:44.855  4567  4586 W Settings: Setting download_manager_max_bytes_over_mobile has moved from android.provider.Settings.Secure to android.provider.Settings.Global.
02-22 09:38:44.855  4567  4600 I Finsky  : [45] pg.run(5): Set UnhibernateActivity enabled state to 0
02-22 09:38:44.858  4567  4585 I Finsky  : [30] svb.r(6): Enqueuing libraries load for 0
02-22 09:38:44.859  4567  4588 I Finsky  : [32] ageq.<init>(4): VerifyApps: Setup app restrictions monitor
02-22 09:38:44.859  4567  4603 I Finsky  : [48] svb.s(1): Starting libraries load for 0
02-22 09:38:44.860  4567  4588 I Finsky  : [32] agkr.a(3): VerifyApps: Device wide unknown source restriction updated
02-22 09:38:44.861  3689  3689 D BoundBrokerSvc: onBind: Intent { act=com.google.android.gms.safetynet.service.START pkg=com.google.android.gms }
02-22 09:38:44.861  3689  3689 D BoundBrokerSvc: Loading bound service for intent: Intent { act=com.google.android.gms.safetynet.service.START pkg=com.google.android.gms }
02-22 09:38:44.870  4567  4586 I Finsky  : [31] uum.i(3): SettingNotFoundException, fall through to G.downloadBytesOverMobileMaximum
02-22 09:38:44.870  4567  4586 W Settings: Setting download_manager_recommended_max_bytes_over_mobile has moved from android.provider.Settings.Secure to android.provider.Settings.Global.
02-22 09:38:44.871  4567  4587 E aonk    : Got more than one input Future failure. Logging failures after the first
02-22 09:38:44.871  4567  4587 E aonk    : java.lang.SecurityException: Calling identity is not authorized
02-22 09:38:44.871  4567  4587 E aonk    :      at android.os.Parcel.createExceptionOrNull(Parcel.java:2425)
02-22 09:38:44.871  4567  4587 E aonk    :      at android.os.Parcel.createException(Parcel.java:2409)
02-22 09:38:44.871  4567  4587 E aonk    :      at android.os.Parcel.readException(Parcel.java:2392)
02-22 09:38:44.871  4567  4587 E aonk    :      at android.os.Parcel.readException(Parcel.java:2334)
02-22 09:38:44.871  4567  4587 E aonk    :      at android.app.admin.IDevicePolicyManager$Stub$Proxy.getDeviceOwnerComponent(IDevicePolicyManager.java:9170)
02-22 09:38:44.871  4567  4587 E aonk    :      at android.app.admin.DevicePolicyManager.getDeviceOwnerComponentInner(DevicePolicyManager.java:7921)
02-22 09:38:44.871  4567  4587 E aonk    :      at android.app.admin.DevicePolicyManager.getDeviceOwnerComponentOnAnyUser(DevicePolicyManager.java:7904)
02-22 09:38:44.871  4567  4587 E aonk    :      at adch.c(PG:5)
02-22 09:38:44.871  4567  4587 E aonk    :      at jnz.T(PG:2)
02-22 09:38:44.871  4567  4587 E aonk    :      at jpd.b(PG:3)
02-22 09:38:44.871  4567  4587 E aonk    :      at avjk.a(PG:2)
02-22 09:38:44.871  4567  4587 E aonk    :      at aonf.e(PG:2)
02-22 09:38:44.871  4567  4587 E aonk    :      at aonh.run(PG:9)
02-22 09:38:44.871  4567  4587 E aonk    :      at asez.run(PG:1)
02-22 09:38:44.871  4567  4587 E aonk    :      at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1167)
02-22 09:38:44.871  4567  4587 E aonk    :      at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:641)
02-22 09:38:44.871  4567  4587 E aonk    :      at nft.run(PG:13)
02-22 09:38:44.871  4567  4587 E aonk    :      at java.lang.Thread.run(Thread.java:920)
02-22 09:38:44.872  4567  4586 I Finsky  : [31] uum.h(3): SettingNotFoundException, fall through to G.downloadBytesOverMobileRecommended
02-22 09:38:44.873  4567  4603 I Finsky  : [48] svb.s(23): Finished loading 0 libraries.
02-22 09:38:44.873  4567  4586 I Finsky  : [31] alvu.d(2): registerListener
02-22 09:38:44.875  4567  4586 I Finsky  : [31] alvu.d(2): registerListener
02-22 09:38:44.876  4567  4567 D AndroidRuntime: Shutting down VM
02-22 09:38:44.876  4567  4616 E Finsky  : [61] laf.a(5): Unexpected android-id = 0
02-22 09:38:44.876  4567  4567 E AndroidRuntime: FATAL EXCEPTION: main
02-22 09:38:44.876  4567  4567 E AndroidRuntime: Process: com.android.vending, PID: 4567
02-22 09:38:44.876  4567  4567 E AndroidRuntime: java.lang.RuntimeException: Unable to create application com.google.android.finsky.application.classic.ClassicApplication: java.lang.IllegalStateException: Failed to initialize FinskyApp
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at android.app.ActivityThread.handleBindApplication(ActivityThread.java:6849)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at android.app.ActivityThread.access$1500(ActivityThread.java:266)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at android.app.ActivityThread$H.handleMessage(ActivityThread.java:2101)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at android.os.Handler.dispatchMessage(Handler.java:106)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at android.os.Looper.loopOnce(Looper.java:201)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at android.os.Looper.loop(Looper.java:288)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at android.app.ActivityThread.main(ActivityThread.java:7952)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at java.lang.reflect.Method.invoke(Native Method)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:548)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:1003)
02-22 09:38:44.876  4567  4567 E AndroidRuntime: Caused by: java.lang.IllegalStateException: Failed to initialize FinskyApp
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at jnz.aw(PG:9)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at jqe.i(PG:66)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at jqe.onCreate(PG:3)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at android.app.Instrumentation.callApplicationOnCreate(Instrumentation.java:1223)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at android.app.ActivityThread.handleBindApplication(ActivityThread.java:6844)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        ... 9 more
02-22 09:38:44.876  4567  4567 E AndroidRuntime: Caused by: java.util.concurrent.ExecutionException: java.lang.SecurityException: You either need MANAGE_USERS or CREATE_USERS permission to: query users
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at aond.r(PG:3)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at aond.get(PG:7)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at oq.i(Unknown Source:1)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at jnz.aw(PG:2)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        ... 13 more
02-22 09:38:44.876  4567  4567 E AndroidRuntime: Caused by: java.lang.SecurityException: You either need MANAGE_USERS or CREATE_USERS permission to: query users
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at android.os.Parcel.createExceptionOrNull(Parcel.java:2425)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at android.os.Parcel.createException(Parcel.java:2409)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at android.os.Parcel.readException(Parcel.java:2392)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at android.os.Parcel.readException(Parcel.java:2334)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at android.os.IUserManager$Stub$Proxy.getUsers(IUserManager.java:2122)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at android.os.UserManager.getUsers(UserManager.java:3492)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at android.os.UserManager.getUsers(UserManager.java:3437)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at android.os.UserManager.getUserCount(UserManager.java:3411)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at tl.x(PG:1)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at akmk.a(PG:11)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at itt.<init>(PG:8)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at izs.e(PG:5)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at izs.d(Unknown Source:12)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at jnz.N(PG:1)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at jom.b(PG:5)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at avjk.a(PG:2)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at aonf.e(PG:2)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at aonh.run(PG:9)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at asez.run(PG:1)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1167)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:641)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at nft.run(PG:13)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at java.lang.Thread.run(Thread.java:920)
02-22 09:38:44.876  4567  4567 E AndroidRuntime: Caused by: android.os.RemoteException: Remote stack trace:
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at com.android.server.pm.UserManagerService.checkManageOrCreateUsersPermission(UserManagerService.java:2508)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at com.android.server.pm.UserManagerService.getUsers(UserManagerService.java:837)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at android.os.IUserManager$Stub.onTransact(IUserManager.java:929)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at android.os.Binder.execTransactInternal(Binder.java:1179)
02-22 09:38:44.876  4567  4567 E AndroidRuntime:        at android.os.Binder.execTransact(Binder.java:1143)
02-22 09:38:44.876  4567  4567 E AndroidRuntime: 
02-22 09:38:44.877  4567  4567 W Finsky.CrashDetector: Crash at version: 35.6.11-21 [0] [PR] 528895992.
02-22 09:38:44.878  4567  4589 I Finsky  : [34] row.<init>(4): Item store provider started.
02-22 09:38:44.879  4567  4616 E aond    : RuntimeException while executing runnable aooj{qty@e2fdee6} with executor qq@c302c27
02-22 09:38:44.879  4567  4616 E aond    : java.lang.SecurityException: You either need MANAGE_USERS or CREATE_USERS permission to: query users
02-22 09:38:44.879  4567  4616 E aond    :      at android.os.Parcel.createExceptionOrNull(Parcel.java:2425)
02-22 09:38:44.879  4567  4616 E aond    :      at android.os.Parcel.createException(Parcel.java:2409)
02-22 09:38:44.879  4567  4616 E aond    :      at android.os.Parcel.readException(Parcel.java:2392)
02-22 09:38:44.879  4567  4616 E aond    :      at android.os.Parcel.readException(Parcel.java:2334)
02-22 09:38:44.879  4567  4616 E aond    :      at android.os.IUserManager$Stub$Proxy.getUsers(IUserManager.java:2122)
02-22 09:38:44.879  4567  4616 E aond    :      at android.os.UserManager.getUsers(UserManager.java:3492)
02-22 09:38:44.879  4567  4616 E aond    :      at android.os.UserManager.getUsers(UserManager.java:3437)
02-22 09:38:44.879  4567  4616 E aond    :      at android.os.UserManager.getUserCount(UserManager.java:3411)
02-22 09:38:44.879  4567  4616 E aond    :      at tl.x(PG:1)
02-22 09:38:44.879  4567  4616 E aond    :      at akmk.a(PG:11)
02-22 09:38:44.879  4567  4616 E aond    :      at itt.<init>(PG:8)
02-22 09:38:44.879  4567  4616 E aond    :      at izs.e(PG:5)
02-22 09:38:44.879  4567  4616 E aond    :      at izs.d(Unknown Source:12)
02-22 09:38:44.879  4567  4616 E aond    :      at itp.a(Unknown Source:2)
02-22 09:38:44.879  4567  4616 E aond    :      at lcu.b(Unknown Source:10)
02-22 09:38:44.879  4567  4616 E aond    :      at lcu.h(PG:1)
02-22 09:38:44.879  4567  4616 E aond    :      at itz.R(PG:4)
02-22 09:38:44.879  4567  4616 E aond    :      at itz.E(PG:3)
02-22 09:38:44.879  4567  4616 E aond    :      at itz.G(Unknown Source:1)
02-22 09:38:44.879  4567  4616 E aond    :      at qty.c(PG:2)
02-22 09:38:44.879  4567  4616 E aond    :      at qty.b(PG:9)
02-22 09:38:44.879  4567  4616 E aond    :      at aooj.run(PG:6)
02-22 09:38:44.879  4567  4616 E aond    :      at qq.execute(PG:17)
02-22 09:38:44.879  4567  4616 E aond    :      at aond.h(PG:1)
02-22 09:38:44.879  4567  4616 E aond    :      at aond.agu(PG:6)
02-22 09:38:44.879  4567  4616 E aond    :      at apbe.ao(PG:3)
02-22 09:38:44.879  4567  4616 E aond    :      at agto.c(PG:16)
02-22 09:38:44.879  4567  4616 E aond    :      at hzq.run(PG:2)
02-22 09:38:44.880   252   976 W ActivityTaskManager:   Force finishing activity com.android.vending/.AssetBrowserActivity

```

