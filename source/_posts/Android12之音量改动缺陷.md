#### 错误日志分析

```verilog
安卓系统中VolumeDialogImpl是什么？
03-11 07:59:56.336   102   205 E APM::VolumeCurve: Invalid device category 1 for Volume Curve
```

`VolumeDialogImpl` 是 Android 系统中用于管理和显示音量调节对话框的一个实现类。它属于 Android 系统 UI 的一部分，通常与音量控制逻辑紧密相关。

------

#### **`VolumeDialogImpl` 的作用**

1. **音量调节对话框的显示**：
   - 当用户按下音量键时，系统会显示一个音量调节对话框，允许用户调整媒体音量、铃声音量、通知音量等。
   - `VolumeDialogImpl` 负责管理这个对话框的显示、布局和交互逻辑。
2. **音量控制逻辑**：
   - `VolumeDialogImpl` 与 `AudioService` 和 `AudioManager` 交互，将用户的音量调节操作传递给系统音频服务。
3. **多音量流的支持**：
   - Android 支持多种音量流（如媒体、铃声、通知、通话等），`VolumeDialogImpl` 负责根据当前上下文显示正确的音量流调节界面。
4. **UI 定制**：
   - `VolumeDialogImpl` 是 Android 系统 UI 的一部分，设备制造商（OEM）可以对其进行定制，以适配不同的设备外观和交互风格。

------

### `VolumeDialogImpl` 的调用链

1. **用户按下音量键**：
   - 物理音量键或软件音量键触发事件。
2. **`PhoneWindowManager` 处理事件**：
   - `PhoneWindowManager` 是 Android 系统中处理硬件按键事件的核心类。
   - 当音量键被按下时，`PhoneWindowManager` 会调用 `AudioService` 来调整音量。
3. **`AudioService` 处理音量逻辑**：
   - `AudioService` 是 Android 音频系统的核心服务，负责管理音量、音频路由等。
   - `AudioService` 会根据当前音频流类型（如媒体、铃声等）调整音量，并通知 `VolumeDialogImpl` 更新 UI。
4. **`VolumeDialogImpl` 显示对话框**：
   - `VolumeDialogImpl` 根据 `AudioService` 的通知，显示音量调节对话框，并更新音量条和图标。
5. **用户交互**：
   - 用户可以通过对话框进一步调整音量或切换音量流。

------

### 关于日志中的错误：`Invalid device category 1 for Volume Curve`

日志中的错误信息：

复制

```
03-11 07:59:56.336   102   205 E APM::VolumeCurve: Invalid device category 1 for Volume Curve
```

#### **错误原因**

1. **无效的设备类别**：
   - 日志表明，系统尝试为设备类别 `1` 设置音量曲线（Volume Curve），但该类别无效。
   - 设备类别通常用于区分不同的音频设备（如扬声器、耳机、蓝牙设备等）。
2. **音量曲线（Volume Curve）**：
   - 音量曲线定义了音量级别与设备输出之间的关系。
   - 每个设备类别可能有不同的音量曲线，以确保音量调节的平滑性和一致性。
3. **可能的原因**：
   - 设备类别 `1` 未在系统的音频策略配置文件（如 `audio_policy_configuration.xml`）中正确定义。
   - 音频策略配置文件中缺少对该设备类别的支持。



```verilog
03-11 08:00:03.175   102   102 E APM::VolumeCurve: Invalid device category 1 for Volume Curve
03-11 08:00:03.176   491   738 I vol.Events: writeEvent level_changed STREAM_MUSIC 51
03-11 08:00:03.177   491   738 I vol.Events: writeEvent key STREAM_MUSIC 51
03-11 08:00:03.195   491   491 I vol.Events: writeEvent show_dialog volume_changed keyguard=false
03-11 08:00:03.197   491   491 W ConstraintSet: id unknown center_vertical_guideline
03-11 08:00:03.197   491   491 W ConstraintSet: id unknown center_horizontal_guideline
03-11 08:00:03.197   491   491 W ConstraintSet: id unknown media_action_barrier
03-11 08:00:03.197   491   491 W ConstraintSet: id unknown remove_text
03-11 08:00:03.197   491   491 W ConstraintSet: id unknown settings
03-11 08:00:03.197   491   491 W ConstraintSet: id unknown cancel
03-11 08:00:03.197   491   491 W ConstraintSet: id unknown dismiss
03-11 08:00:03.214   491   491 W ConstraintSet: id unknown center_vertical_guideline
03-11 08:00:03.214   491   491 W ConstraintSet: id unknown center_horizontal_guideline
03-11 08:00:03.214   491   491 W ConstraintSet: id unknown media_action_barrier
03-11 08:00:03.214   491   491 W ConstraintSet: id unknown remove_text
03-11 08:00:03.214   491   491 W ConstraintSet: id unknown settings
03-11 08:00:03.214   491   491 W ConstraintSet: id unknown cancel
03-11 08:00:03.214   491   491 W ConstraintSet: id unknown dismiss

再解释一下，这个确实是我调整音量大小时的日志
```

#### 1. **`APM::VolumeCurve` 错误**

复制

```
03-11 08:00:03.175   102   102 E APM::VolumeCurve: Invalid device category 1 for Volume Curve
```

- **解释**：
  - `APM` 是 `Audio Policy Manager` 的缩写，负责管理音频策略。
  - `VolumeCurve` 是音量曲线，用于定义音量级别与设备输出之间的关系。
  - 错误表明系统尝试为设备类别 `1` 设置音量曲线，但该类别无效。
- **可能原因**：
  - 设备类别 `1` 未在音频策略配置文件（如 `audio_policy_configuration.xml`）中正确定义。
  - 音量曲线配置文件中缺少对该设备类别的支持。

------

#### 2. **音量调整事件**

复制

```
03-11 08:00:03.176   491   738 I vol.Events: writeEvent level_changed STREAM_MUSIC 51
03-11 08:00:03.177   491   738 I vol.Events: writeEvent key STREAM_MUSIC 51
```

- **解释**：
  - `vol.Events` 是音量相关的事件日志。
  - `level_changed` 表示音量级别发生了变化。
  - `STREAM_MUSIC` 表示当前调整的是媒体音量流。
  - `51` 是调整后的音量值。
- **说明**：
  - 用户调整了媒体音量，系统记录了音量变化事件。

------

#### 3. **显示音量对话框**

复制

```
03-11 08:00:03.195   491   491 I vol.Events: writeEvent show_dialog volume_changed keyguard=false
```

- **解释**：
  - `show_dialog` 表示系统正在显示音量调节对话框。
  - `volume_changed` 表示音量发生了变化。
  - `keyguard=false` 表示当前设备未处于锁屏状态。
- **说明**：
  - 系统在音量调整时显示了音量调节对话框。

------

#### 4. **`ConstraintSet` 警告**

复制

```
03-11 08:00:03.197   491   491 W ConstraintSet: id unknown center_vertical_guideline
03-11 08:00:03.197   491   491 W ConstraintSet: id unknown center_horizontal_guideline
03-11 08:00:03.197   491   491 W ConstraintSet: id unknown media_action_barrier
03-11 08:00:03.197   491   491 W ConstraintSet: id unknown remove_text
03-11 08:00:03.197   491   491 W ConstraintSet: id unknown settings
03-11 08:00:03.197   491   491 W ConstraintSet: id unknown cancel
03-11 08:00:03.197   491   491 W ConstraintSet: id unknown dismiss
```

- **解释**：
  - `ConstraintSet` 是 Android 布局约束系统的一部分，用于定义 UI 元素的布局规则。
  - 这些日志表明系统在加载音量对话框的布局时，未能找到某些 UI 元素的 ID。
- **可能原因**：
  - 音量对话框的布局文件中缺少某些 UI 元素的定义。
  - 布局文件中的 ID 与代码中的引用不匹配。
- **说明**：
  - 这些警告通常不会影响功能，但可能会导致 UI 显示异常。

------

### 调用链总结

1. **用户按下音量键**：
   - 物理音量键或软件音量键触发事件。
2. **`PhoneWindowManager` 处理事件**：
   - `PhoneWindowManager` 检测到音量键事件，并通知 `AudioService` 调整音量。
3. **`AudioService` 调整音量**：
   - `AudioService` 根据当前音频流类型（如 `STREAM_MUSIC`）调整音量。
   - 如果音量发生变化，`AudioService` 会通知 `VolumeDialogImpl` 更新 UI。
4. **`VolumeDialogImpl` 显示对话框**：
   - `VolumeDialogImpl` 显示音量调节对话框，并更新音量条和图标。
   - 如果布局文件中存在 ID 不匹配的问题，会触发 `ConstraintSet` 警告。
5. **记录事件日志**：
   - 系统记录音量调整事件（如 `level_changed` 和 `show_dialog`）。

------

### 问题定位与解决

#### 1. **`APM::VolumeCurve` 错误**

- **解决方法**：
  - 检查音频策略配置文件（如 `audio_policy_configuration.xml`），确保设备类别 `1` 正确定义。
  - 确保音量曲线配置文件（如 `audio_volume_curves.xml`）中包含对设备类别 `1` 的支持。

#### 2. **`ConstraintSet` 警告**

- **解决方法**：
  - 检查音量对话框的布局文件（如 `volume_dialog.xml`），确保所有 UI 元素的 ID 正确定义。
  - 确保布局文件中的 ID 与代码中的引用一致。

















​    Log.d(TAG, "setSystemAudioVolume(int oldVolume, int newVolume, int maxVolume, int flags)");





frameworks/av/services/audiopolicy/engine/common/include/VolumeCurve.h

​	virtual float volIndexToDb(device_category deviceCat, int indexInUi) const

frameworks/av/services/audiopolicy/managerdefault/AudioPolicyManager.cpp

​	float AudioPolicyManager::computeVolume(IVolumeCurves &curves,

​	status_t AudioPolicyManager::checkAndSetVolume(IVolumeCurves &curves,

void AudioPolicyManager::setVolumeSourceMute(VolumeSource volumeSource,





outputDesc->setVolume(

​      volumeDb, volumeSource, curves.getStreamTypes(), deviceTypes, delayMs, force);







出错的逻辑

```cpp
frameworks/av/services/audiopolicy/managerdefault/AudioPolicyManager.cpp
status_t AudioPolicyManager::checkAndSetVolume(IVolumeCurves &curves,
	float volumeDb = computeVolume(curves, volumeSource, index, deviceTypes);

float AudioPolicyManager::computeVolume(IVolumeCurves &curves,
	curves.volIndexToDb(Volume::getDeviceCategory(deviceTypes), index);
                                        
frameworks/av/services/audiopolicy/common/include/Volume.h
      static device_category getDeviceCategory(const android::DeviceTypeSet& deviceTypes)
    {
        switch(getDeviceForVolume(deviceTypes)) {
        case AUDIO_DEVICE_OUT_EARPIECE:
            return DEVICE_CATEGORY_EARPIECE;
        case AUDIO_DEVICE_OUT_WIRED_HEADSET:
  ...
        default:
            return DEVICE_CATEGORY_SPEAKER;
        }
    }                                      
frameworks/av/services/audiopolicy/engine/common/include/VolumeCurve.h
    virtual float volIndexToDb(device_category deviceCat, int indexInUi) const
    {
        sp<VolumeCurve> vc = getCurvesFor(deviceCat);
        if (vc != 0) {
            return vc->volIndexToDb(indexInUi, mIndexMin, mIndexMax);
        } else {
            ALOGE("Invalid device category %d for Volume Curve", deviceCat);//!
            return 0.0f;
        }
    }
    sp<VolumeCurve> getCurvesFor(device_category device) const
    {
        if (indexOfKey(device) < 0) {
            return 0;
        }
        return valueFor(device);
    }
```







```
frameworks/base/services/core/java/com/android/server/audio/AudioService.java
private void adjustSuggestedStreamVolume(int direction, int suggestedStreamType, int flags,

protected void adjustStreamVolume(int streamType, int direction, int flags,
    final int device = getDeviceForStream(streamTypeAlias);
    sendMsg(mAudioHandler, MSG_UNMUTE_STREAM, SENDMSG_QUEUE,streamTypeAlias, flags, null, UNMUTE_STREAM_DELAY);
private static void sendMsg(Handler handler, int msg,
            int existingMsgPolicy, int arg1, int arg2, Object obj, int delay) {
    	handler.sendMessageAtTime(handler.obtainMessage(msg, arg1, arg2, obj), time);	
                                    


private class AudioHandler extends Handler {

}
```



```java
    private static final int MSG_UNMUTE_STREAM = 18;
    private static final int MSG_SET_DEVICE_VOLUME = 0;

sendMsg(mAudioHandler, MSG_UNMUTE_STREAM, SENDMSG_QUEUE, streamTypeAlias, flags, null, UNMUTE_STREAM_DELAY);
sendMsg(mAudioHandler, MSG_SET_DEVICE_VOLUME,SENDMSG_QUEUE,device, 0,streamState,0);

public void handleMessage(Message msg) {
    switch (msg.what) {
            ...
        case MSG_SET_DEVICE_VOLUME:
            setDeviceVolume((VolumeStreamState) msg.obj, msg.arg1);
            break;
		case MSG_UNMUTE_STREAM:
            onUnmuteStream(msg.arg1, msg.arg2);
            break;   
            ...
    }
}

/*package*/ void setDeviceVolume(VolumeStreamState streamState, int device) {

    synchronized (VolumeStreamState.class) {
        // Apply volume
        streamState.applyDeviceVolume_syncVSS(device);

        // Apply change to all streams using this one as alias
        int numStreamTypes = AudioSystem.getNumStreamTypes();
        for (int streamType = numStreamTypes - 1; streamType >= 0; streamType--) {
            if (streamType != streamState.mStreamType &&
                mStreamVolumeAlias[streamType] == streamState.mStreamType) {
                // Make sure volume is also maxed out on A2DP device for aliased stream
                // that may have a different device selected
                int streamDevice = getDeviceForStream(streamType);
                if ((device != streamDevice) && mAvrcpAbsVolSupported
                    && AudioSystem.DEVICE_OUT_ALL_A2DP_SET.contains(device)) {
                    mStreamStates[streamType].applyDeviceVolume_syncVSS(device);
                }
                mStreamStates[streamType].applyDeviceVolume_syncVSS(streamDevice);
            }
        }
    }
    // Post a persist volume msg
    sendMsg(mAudioHandler,
            MSG_PERSIST_VOLUME,
            SENDMSG_QUEUE,
            device,
            0,
            streamState,
            PERSIST_DELAY);

}

private void onUnmuteStream(int stream, int flags) {
    boolean wasMuted;
    synchronized (VolumeStreamState.class) {
        final VolumeStreamState streamState = mStreamStates[stream];
        wasMuted = streamState.mute(false); // if unmuting causes a change, it was muted

        final int device = getDeviceForStream(stream);
        final int index = streamState.getIndex(device);
        sendVolumeUpdate(stream, index, index, flags, device);
    }
    if (stream == AudioSystem.STREAM_MUSIC && wasMuted) {
        synchronized (mHdmiClientLock) {
            maybeSendSystemAudioStatusCommand(true);
        }
    }
}
    
```

 

---

### 自底而上

   "AudioOutPath":"/userdata/container/android_data/data_%d/misc/audioserver/audio_out",

​    "AudioInPath":"/userdata/container/android_data/data_%d/misc/audioserver/audio_in",



#### audio.primary.rk3588

hardware/ntimespace/audio/Android.mk

路径的设置

hardware/ntimespace/audio/audio_hw.c

​	\#define AUDIO_OUT_PATH "/data/misc/audioserver/audio_out"  //g_serverAddr

​	static int adev_open(const hw_module_t* module, const char* name    ，hw_device_t** device) 

​		property_get("ro.audio_out.path", g_audio_out_path, AUDIO_OUT_PATH);

​		strncpy(g_serverAddr.sun_path, g_audio_out_path, sizeof(g_serverAddr.sun_path) - 1);



往out写入音频

hardware/ntimespace/audio/audio_hw.c

​	static ssize_t out_write(struct audio_stream_out *stream, const void* buffer,size_t bytes)

​		send_msg(g_sockfd, JWAUDIO_PCM_BLOCK, buffer, bytes); //



device中集成audio lib

device/ntimespace/modules/audio/audio.mk

device/ntimespace/modules/audio/rt_audio_config.xml

```makefile
# audio lib
PRODUCT_PACKAGES += \
    audio_policy.rk3588 \
    audio.primary.rk3588 \
    audio.a2dp.default \
    audio.r_submix.default \
    libaudioroute \
    audio.usb.default 

PRODUCT_PACKAGES += \
    android.hardware.soundtrigger@2.0-impl

# audio lib
PRODUCT_PACKAGES += \
    libtinyalsa \

PRODUCT_COPY_FILES += \
    $(LOCAL_PATH)/rt_audio_config.xml:/system/etc/rt_audio_config.xml
```



#### 底层方法的层层传递

```cpp
hardware/ntimespace/audio/audio_hw.c

static int adev_open_output_stream(struct audio_hw_device *dev,

                  audio_io_handle_t handle,

                  audio_devices_t devices,

                  audio_output_flags_t flags,

                  struct audio_config *config,

                  struct audio_stream_out **stream_out,

                  const char *address __unused)

		out->stream.write = out_write;//!!!!!!!!!!

static int adev_open(const hw_module_t* module, const char* name, hw_device_t** device)

	  adev->device.open_output_stream = adev_open_output_stream;//!!!!!!!!!!

static struct hw_module_methods_t hal_module_methods = {
    .open = adev_open,
};

struct audio_module HAL_MODULE_INFO_SYM = {
    .common = {
        .tag = HARDWARE_MODULE_TAG,
        .module_api_version = AUDIO_MODULE_API_VERSION_0_1,
        .hal_api_version = HARDWARE_HAL_API_VERSION,
        .id = AUDIO_HARDWARE_MODULE_ID,
        .name = "JW audio HW HAL",
        .author = "JW SpaceTime",
        .methods = &hal_module_methods,
    },
};
```



#### AudioFlinger导入hw模块

frameworks/av/services/audioflinger/AudioFlinger.cpp

```cpp
static const char * const audio_interfaces[] = {
    AUDIO_HARDWARE_MODULE_ID_PRIMARY,
    AUDIO_HARDWARE_MODULE_ID_A2DP,
    AUDIO_HARDWARE_MODULE_ID_USB,
};
AudioHwDevice* AudioFlinger::findSuitableHwDev_l(
        audio_module_handle_t module,
        audio_devices_t deviceType){
    for (size_t i = 0; i < arraysize(audio_interfaces); i++) {
        loadHwModule_l(audio_interfaces[i]);
    }
    sp<DeviceHalInterface> dev;//!!!!!!!!!!!!!!!!!!!!!!!!!

    int rc = mDevicesFactoryHal->openDevice(name, &dev);//!!!!!!!!!!!!!
    rc = dev->initCheck();
}
```



#### AUDIO_HARDWARE_MODULE_ID_PRIMARY

```cpp
hardware/interfaces/audio/core/all-versions/default/DevicesFactory.cpp
Return<void> DevicesFactory::openDevice(const hidl_string& moduleName, openDevice_cb _hidl_cb) {
    if (moduleName == AUDIO_HARDWARE_MODULE_ID_PRIMARY) {
        return openDevice<PrimaryDevice>(moduleName.c_str(), _hidl_cb);
    }
    return openDevice(moduleName.c_str(), _hidl_cb);
}
```



# 

[Android 音频子系统--05：AudioFlinger启动分析1.概述   在《Android 音频子系统--03 - 掘金](https://juejin.cn/post/7423403181995180042)AudioFlinger启动分析!!!!!!!!!!!

audioserver

*// frameworks/av/media/audioserver/main_audioserver.cpp*

*// frameworks/native/include/binder/BinderService.h*

*// frameworks/av/services/audioflinger/AudioFlinger.cpp*

AudioFlinger::AudioFlinger()

**void** **AudioFlinger::onFirstRef**()

**audio_module_handle_t** **AudioFlinger::loadHwModule**(**const** **char** *name)

**audio_module_handle_t** **AudioFlinger::loadHwModule_l**(**const** **char** *name)

*// frameworks/av/media/libaudiohal/DevicesFactoryHalHybrid.cpp*

**status_t** **DevicesFactoryHalHybrid::openDevice**(**const** **char** *name, sp<DeviceHalInterface> *device)

*// frameworks/av/media/libaudiohal/DevicesFactoryHalLocal.cpp*

**status_t** **DevicesFactoryHalLocal::openDevice**(**const** **char** *name, sp<DeviceHalInterface> *device)

*// frameworks/av/media/libaudiohal/DevicesFactoryHalLocal.cpp*

**static** **status_t** **load_audio_interface**(**const** **char** *if_name, **audio_hw_device_t** **dev)

*// hardware/libhardware/include/hardware/audio.h*

static inline int audio_hw_device_open(const struct hw_module_t* module,   struct audio_hw_device** device)

*// hardware/libhardware_legacy/audio/audio_hw_hal.cpp*

**static** **int** **legacy_adev_open**(**const** **hw_module_t*** **module**, **const** **char*** name, **hw_device_t**** device)

这里总结下 loadHwModule对硬件的封装:

- **AudioFlinger：** AudioHwDevice (放入mAudioHwDevs数组中)；
- **audio_hw_hal.cpp**：audio_hw_device；
- **厂家：** AudioHardware (派生自: AudioHardwareInterface)；
- **AudioHwDevice：** 对audio_hw_device的封装；
- **audio_hw_device：** 函数的实现要通过AudioHardware类对象。

*// frameworks/av/services/audioflinger/AudioFlinger.cpp*

```cpp
status_t AudioFlinger::openOutput(audio_module_handle_t module,
                                  audio_io_handle_t *output,
                                  audio_config_t *config,
                                  audio_devices_t *devices,
                                  const String8& address,
                                  uint32_t *latencyMs,
                                  audio_output_flags_t flags)


sp<AudioFlinger::ThreadBase> AudioFlinger::openOutput_l(audio_module_handle_t module,
                                                            audio_io_handle_t *output,
                                                            audio_config_t *config,
                                                            audio_devices_t devices,
                                                            const String8& address,
                                                            audio_output_flags_t flags)


```

  ALOGD("0011 AudioFlinger::setStreamVolume value%f ", value);





```log
03-13 09:54:25.369   279  1152 D AS.AudioService: 0011 setStreamVolume(int streamType, int index, int flags, String callingPackage)
03-13 09:54:25.369   279  1152 D AS.AudioService: 0011 void setStreamVolume(int streamType, int index, int flags, String callingPackage,...
03-13 09:54:25.369   279  1152 D AS.AudioService: 0011 setSystemAudioVolume(int oldVolume, int newVolume, int maxVolume, int flags)
03-13 09:54:25.369   279  1152 D AS.AudioService: 0011 onSetStreamVolume(int streamType, int index, int flags, int device,
03-13 09:54:25.369   279  1152 D AS.AudioService: 0011 setStreamVolumeInt(int streamType,
03-13 09:54:25.371   279  1152 D AS.AudioService: 0011 handler.sendMessageAtTime0
03-13 09:54:25.372   279   484 D AS.AudioService: 0011 setDeviceVolume(VolumeStreamState streamState, int device)2
03-13 09:54:25.372   279   484 D AS.AudioService: 0011 applyDeviceVolume_syncVSS(int device) 
03-13 09:54:25.372   279   484 D AS.AudioService: 0011 setStreamVolumeIndex(int index, int device) 
03-13 09:54:25.373   279   484 D AS.AudioService: 0011 applyDeviceVolume_syncVSS(int device) 
03-13 09:54:25.374   279   484 D AS.AudioService: 0011 setStreamVolumeIndex(int index, int device) 
03-13 09:54:25.375   279   484 D AS.AudioService: 0011 applyDeviceVolume_syncVSS(int device) 
03-13 09:54:25.375   279   484 D AS.AudioService: 0011 setStreamVolumeIndex(int index, int device) 
03-13 09:54:25.376   279   484 D AS.AudioService: 0011 applyDeviceVolume_syncVSS(int device) 
03-13 09:54:25.376   279   484 D AS.AudioService: 0011 setStreamVolumeIndex(int index, int device) 
03-13 09:54:25.378   279   484 D AS.AudioService: 0011 handler.sendMessageAtTime1
03-13 09:54:25.398   279   622 D AS.AudioService: 0011 handler.sendMessageAtTime29
03-13 09:54:25.418   279  1152 D AS.AudioService: 0011 handler.sendMessageAtTime29
03-13 09:54:25.453   279  1152 D AS.AudioService: 0011 handler.sendMessageAtTime29
03-13 09:54:25.948   279   622 D AS.AudioService: 0011 handler.sendMessageAtTime29
03-13 09:54:27.381   279  1152 D AS.AudioService: 0011 handler.sendMessageAtTime29
```

- **调用链**：应用层 → `AudioManager` → `AudioSystem` (Java) → `AudioSystem` (Native) → `AudioFlinger` → `PlaybackThread` → HAL 层。
- **关键模块**：
  - `AudioManager`：提供音量调节的 Java API。
  - `AudioSystem`：Java 层与 Native 层的桥梁。
  - `AudioFlinger`：Android 音频系统的核心服务。
  - `PlaybackThread`：管理音频播放线程。
  - HAL 层：将音量设置传递给底层硬件。





frameworks/av/media/libaudioclient/AudioSystem.cpp

status_t AudioSystem::setStreamVolumeIndex(audio_stream_type_t stream,

​                      int index,

​                      audio_devices_t device) {

  		return statusTFromBinderStatus(

​      aps->setStreamVolumeIndex(streamAidl, deviceAidl, indexAidl));/!!!!!!!!!!!!!

const sp<IAudioPolicyService>& aps = AudioSystem::get_audio_policy_service();

const sp<IAudioPolicyService> AudioSystem::get_audio_policy_service() {

​	gAudioPolicyService = interface_cast<IAudioPolicyService>(binder);!!!!!!!!!!!!!!!!!!!!!!!!!!!

​	ap = gAudioPolicyService;

​	return ap;



frameworks/av/services/audiopolicy/service/AudioPolicyInterfaceImpl.cpp

Status AudioPolicyService::setStreamVolumeIndex(media::AudioStreamType streamAidl,

​	mAudioPolicyManager->setStreamVolumeIndex(stream,

​                                       index,

​                                       device)

frameworks/av/services/audiopolicy/managerdefault/AudioPolicyManager.cpp

status_t AudioPolicyManager::setStreamVolumeIndex(audio_stream_type_t stream,

​                         int index,

​                         audio_devices_t device)

​		return setVolumeIndexForAttributes(attributes, index, device);

status_t AudioPolicyManager::setVolumeIndexForAttributes(const audio_attributes_t &attributes,

​                             int index,

​                             audio_devices_t device)

  	ALOGD("0011 AudioPolicyManager::setVolumeIndexForAttributes0 %d",index);

​	  ALOGD("0011 AudioPolicyManager::setVolumeIndexForAttributes1 1 ");

​	status = setVolumeCurveIndex(index, device, curves);

-----

```
/vendor/etc/audio_policy_configuration.xml
/vendor/etc/r_submix_audio_policy_configuration.xml

/vendor/etc/media_codecs_google_audio.xml
/vendor/etc/a2dp_audio_policy_configuration_7_0.xml
/vendor/etc/usb_audio_policy_configuration.xml




------------
PRODUCT_SOONG_NAMESPACES += frameworks/av/services/audiopolicy/config

# audio policy
PRODUCT_PACKAGES += \
    audio_policy_configuration.xml \
    r_submix_audio_policy_configuration.xml \
    audio_policy_volumes.xml \
    default_volume_tables.xml \
    primary_audio_policy_configuration.xml \
    surround_sound_configuration_5_0.xml \
    frameworks/av/media/libeffects/data/audio_effects.xml:$(TARGET_COPY_OUT_VENDOR)/etc/audio_effects.xml \
    usb_audio_policy_configuration.xml \
    frameworks/av/media/libstagefright/data/media_codecs_google_audio.xml:$(TARGET_COPY_OUT_VENDOR)/etc/media_codecs_google_audio.xml \
    frameworks/av/services/audiopolicy/config/a2dp_audio_policy_configuration_7_0.xml:$(TARGET_COPY_OUT_VENDOR)/etc/a2dp_audio_policy_configuration_7_0.xml


```

