解决方法【已验证】

```diff

diff --git a/system/vold/VolumeManager.cpp b/system/vold/VolumeManager.cpp
index 44bff5a978..4d629667e6 100644
--- a/system/vold/VolumeManager.cpp
+++ b/system/vold/VolumeManager.cpp
@@ -224,6 +224,7 @@ void VolumeManager::handleBlockEvent(NetlinkEvent* evt) {
                         flags |= android::vold::Disk::Flags::kSd;
                     } else {
                         flags |= android::vold::Disk::Flags::kUsb;
+                        return;
                     }
 
                     auto disk =

```

