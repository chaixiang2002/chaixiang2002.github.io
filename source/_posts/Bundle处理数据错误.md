```java
NineDSpaceManager mSpaceManager = (NineDSpaceManager) mContext.getSystemService(Context.SPACE_SERVICE);
mSpaceManager.sendTracking("gpsData", dataPacket);



dataPacket.putDoubleArray("data", locationData); //放入double[]数组
```

### JSONObject添加数组失败

```java
JSONObject message = new JSONObject();
if (val instanceof double[]) {
    // 如果 val 是 double[]，将其转换为 JSONArray
    JSONArray jsonArray = new JSONArray();
    for (double d : (double[]) val) {
        jsonArray.put(d);  // 将每个 double 值添加到 JSONArray
    }
    message.put(key, jsonArray);  // 将 JSONArray 添加到 message
} 
```



红手指

```

$ sudo df -h
Filesystem          Size Used Avail Use% Mounted on
tmpfs               7.7G  41M  7.7G   1% /
none                 10M 1.1M  8.8M  12% /dev
/dev/mapper/vg-vm_1  88G  14G   74G  16% /data
overlay_super_1      35G  12G   23G  34% /system
tmpfs               7.7G    0  7.7G   0% /mnt
tmpfs               7.7G 8.0K  7.7G   1% /apex
tmpfs               7.7G 564K  7.7G   1% /linkerconfig
tmpfs               7.7G    0  7.7G   0% /data_mirror
/dev/fuse            88G  14G   74G  16% /mnt/user/0/emulated
```

/data

/system

/mnt/user/0/emulated



我们的

```
77751364438d:/ # df -h
Filesystem                   Size  Used Avail Use% Mounted on
overlay                      216G  113G  102G  53% /
tmpfs                         64M  636K   63M   1% /dev
tmpfs                        7.7G     0  7.7G   0% /sys/fs/cgroup
shm                           64M     0   64M   0% /dev/shm
/dev/mapper/vg_data-userdata 216G  113G  102G  53% /data
tmpfs                        7.7G     0  7.7G   0% /mnt
tmpfs                        7.7G     0  7.7G   0% /apex
/dev/fuse                    216G  113G  102G  53% /mnt/runtime/default/emulated
/dev/fuse                    216G  113G  102G  53% /mnt/runtime/read/emulated
/dev/fuse                    216G  113G  102G  53% /mnt/runtime/write/emulated
77751364438d:/ # 
```

/                v

/data        v







huawei

```

$ df -h
Filesystem                   Size  Used Avail Use% Mounted on
/dev/block/dm-7              1.8G  1.8G     0 100% /
tmpfs                        3.6G  2.2M  3.6G   1% /dev
tmpfs                        3.6G     0  3.6G   0% /mnt
none                         3.6G     0  3.6G   0% /mnt/update_engine
/data/misc_ce/0/kdfs/storage 112G   98G   14G  88% /mnt/mdfs/.hmdfs
/data/media/0                112G   98G   14G  88% /mnt/mdfs/sdcard
/mnt/media_rw                3.6G     0  3.6G   0% /mnt/mdfs/external_storage
mdfs                          14G     0   14G   0% /mnt/mdfs/groups
tmpfs                        3.6G     0  3.6G   0% /apex
/dev/block/loop3             232K   36K  192K  16% /apex/com.android.apex.cts.shim@1
/dev/block/loop4             4.9M  4.9M     0 100% /apex/com.android.conscrypt@300000000
/dev/block/loop5             5.6M  5.6M     0 100% /apex/com.android.media@300000000
/dev/block/loop6              22M   22M     0 100% /apex/com.android.media.swcodec@300000000
/dev/block/loop7             1.7M  1.6M     0 100% /apex/com.android.resolv@300000000
/dev/block/loop8             102M  102M     0 100% /apex/com.android.runtime@1
/dev/block/loop9             792K  764K   12K  99% /apex/com.android.tzdata@300000000
/dev/block/dm-5               36M   36M     0 100% /patch_hw
/dev/block/dm-8              6.9M  6.9M     0 100% /cust
/dev/block/dm-9              1.3G  1.3G     0 100% /hw_product
/dev/block/dm-10              65M   65M     0 100% /odm
/dev/block/dm-11             110M  110M     0 100% /preas
/dev/block/dm-12             998M  998M     0 100% /preload
/dev/block/dm-13             394M  394M     0 100% /vendor
/dev/block/dm-14             1.1M  1.1M     0 100% /vendor/preavs
/dev/block/dm-15             128K  128K     0 100% /version
overlay                       36M   36M     0 100% /system/lib64
/dev/block/by-name/userdata  112G   98G   14G  88% /data
/dev/block/by-name/cache      93M   88K   90M   1% /cache
overlay                      110M  110M     0 100% /system/product/priv-app
overlay                      110M  110M     0 100% /system/product/app
overlay                      110M  110M     0 100% /system/product/etc/permissions
/data/media                  112G   98G   14G  88% /storage/emulated
```

