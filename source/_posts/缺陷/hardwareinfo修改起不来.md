a2debc10e5d4:/ # logcat
--------- beginning of system
08-30 03:40:02.815    36    36 I vold    : Vold 3.0 (the awakening) firing up
08-30 03:40:02.815    36    36 D vold    : Detected support for: ext4 f2fs vfat
08-30 03:40:02.815    36    36 E vold    : Failed open: No such file or directory
08-30 03:40:02.816    36    36 D vold    : VoldNativeService::start() completed OK
--------- beginning of main
08-30 03:40:02.828    28    28 I hwservicemanager: hwservicemanager is ready now.
08-30 03:40:02.841    42    42 I android.hardware.keymaster@3.0-impl: Fetching keymaster device name default
08-30 03:40:02.841    42    42 I android.hardware.keymaster@3.0-impl: Could not find any keystore module, using software-only implementation.
08-30 03:40:02.842    42    42 I ServiceManagement: Registered android.hardware.keymaster@3.0::IKeymasterDevice/default (start delay of 17ms)
08-30 03:40:02.842    42    42 I ServiceManagement: Removing namespace from process name android.hardware.keymaster@3.0-service to keymaster@3.0-service.
08-30 03:40:02.842    42    42 I android.hardware.keymaster@3.0-service: Registration complete for android.hardware.keymaster@3.0::IKeymasterDevice/default.
08-30 03:40:02.851    36    36 I Checkpoint: cp_prepareCheckpoint called
08-30 03:40:02.866    48    48 E fsverity_init: Failed to load /product/etc/security/fsverity/*.der
08-30 03:40:02.868    28    28 I hwservicemanager: getTransport: Cannot find entry android.hardware.configstore@1.0::ISurfaceFlingerConfigs/default in either framework or device manifest.
08-30 03:40:02.868    43    43 I SurfaceFlinger: Using HWComposer service: 'default'
08-30 03:40:02.868    43    43 I SurfaceFlinger: SurfaceFlinger is starting
08-30 03:40:02.868    28    28 I hwservicemanager: getTransport: Cannot find entry android.hardware.configstore@1.1::ISurfaceFlingerConfigs/default in either framework or device manifest.
08-30 03:40:02.868    43    43 I SurfaceFlinger: Treble testing override: 'false'
08-30 03:40:02.869    43    43 I SurfaceFlinger: SurfaceFlinger's main thread ready to run. Initializing graphics H/W...
08-30 03:40:02.869    43    43 I SurfaceFlinger: Phase offset NS: 1000000
08-30 03:40:02.869    43    43 D RenderEngine: RenderEngine GLES Backend
08-30 03:40:02.877    49    49 E /system/bin/mini-keyctl: Cannot find keyring id
08-30 03:40:02.877    43    43 D libEGL  : loaded /vendor/lib64/egl/libGLES_mali.so
08-30 03:40:02.884    43    43 I mali_so : [File] : hardware/arm/maliT760/driver/product/base/src/mali_base_kbase.c; [Line] : 1292; [Func] : base_context_deal_with_version_affairs_rk_ext;
08-30 03:40:02.884    43    43 I mali_so : arm_release_ver of this mali_so is 'g12p0-01eac0', rk_so_ver is '5'.
08-30 03:40:02.884    43    43 I mali_so : [File] : hardware/arm/maliT760/driver/product/base/src/mali_base_kbase.c; [Line] : 1308; [Func] : base_context_deal_with_version_affairs_rk_ext;
08-30 03:40:02.884    43    43 I mali_so : arm_release_vers are match. to set the full mali_ver 'g12p0-01eac0-5' as value of 'sys.gmali.version'.
08-30 03:40:02.886    28    28 I hwservicemanager: getTransport: Cannot find entry android.hardware.configstore@1.0::ISurfaceFlingerConfigs/default in either framework or device manifest.
08-30 03:40:02.891    52    52 E fsverity_init: Failed to restrict .fs-verity keyring
08-30 03:40:02.893    43    43 E RenderEngine: Couldn't set SCHED_FIFO for ImageManager
08-30 03:40:02.893    43    43 I RenderEngine: OpenGL ES informations:
08-30 03:40:02.893    43    43 I RenderEngine: vendor    : ARM
08-30 03:40:02.893    43    43 I RenderEngine: renderer  : Mali-G610
08-30 03:40:02.893    43    43 I RenderEngine: version   : OpenGL ES 3.2 v1.g12p0-01eac0.d80164e2f5b37cc3667103831c67a8c0
08-30 03:40:02.893    43    43 I RenderEngine: extensions: GL_EXT_debug_marker GL_ARM_rgba8 GL_ARM_mali_shader_binary GL_OES_depth24 GL_OES_depth_texture GL_OES_depth_texture_cube_map GL_OES_packed_depth_stencil GL_OES_rgb8_rgba8 GL_EXT_read_format_bgra GL_OES_compressed_paletted_texture GL_OES_compressed_ETC1_RGB8_texture GL_OES_standard_derivatives GL_OES_EGL_image GL_OES_EGL_image_external GL_OES_EGL_image_external_essl3 GL_OES_EGL_sync GL_OES_texture_npot GL_OES_vertex_half_float GL_OES_required_internalformat GL_OES_vertex_array_object GL_OES_mapbuffer GL_EXT_texture_format_BGRA8888 GL_EXT_texture_rg GL_EXT_texture_type_2_10_10_10_REV GL_OES_fbo_render_mipmap GL_OES_element_index_uint GL_EXT_shadow_samplers GL_OES_texture_compression_astc GL_KHR_texture_compression_astc_ldr GL_KHR_texture_compression_astc_hdr GL_KHR_texture_compression_astc_sliced_3d GL_EXT_texture_compression_astc_decode_mode GL_EXT_texture_compression_astc_decode_mode_rgb9e5 GL_KHR_debug GL_EXT_occlusion_query_boolean GL_EXT_disjoint_timer_query GL_EXT_blend_minmax GL_EXT_discard_
08-30 03:40:02.893    43    43 I RenderEngine: GL_MAX_TEXTURE_SIZE = 16383
08-30 03:40:02.893    43    43 I RenderEngine: GL_MAX_VIEWPORT_DIMS = 16383
08-30 03:40:02.894    43    43 I ServiceManagement: getService: Trying again for android.hardware.graphics.composer@2.1::IComposer/default...
08-30 03:40:02.904    58    58 I apexd   : Marking APEXd as starting
08-30 03:40:02.905    58    58 I apexd   : Scanning /system/apex for embedded keys
08-30 03:40:02.905    58    58 I apexd   : Scanning /product/apex for embedded keys
08-30 03:40:02.905    58    58 I apexd   : ... does not exist. Skipping
08-30 03:40:02.905    58    58 I apexd   : Populating APEX database from mounts...
08-30 03:40:02.905    58    58 E apexd   : Failed to walk /product/apex : Can't open /product/apex for reading : No such file or directory
08-30 03:40:02.905    58    58 I apexd   : Found "/apex/com.android.tzdata@299900000"
08-30 03:40:02.905    58    58 I apexd   : Found "/apex/com.android.runtime@1"
08-30 03:40:02.905    58    58 I apexd   : 2 packages restored.
08-30 03:40:02.905    58    58 I apexd   : Scanning /data/apex/sessions looking for sessions to be activated.
08-30 03:40:02.905    58    58 I apexd   : Scanning /data/apex/active looking for APEX packages.
08-30 03:40:02.905    58    58 I apexd   : Activated 0 packages. Skipped: 0
08-30 03:40:02.906    58    58 I apexd   : Scanning /system/apex looking for APEX packages.
08-30 03:40:02.906    58    58 I apexd   : Found /system/apex/com.android.conscrypt
08-30 03:40:02.906    58    58 V apexd   : Creating mount point: /apex/com.android.conscrypt@299900000
08-30 03:40:02.906    58    58 I apexd   : Successfully bind-mounted flattened package /system/apex/com.android.conscrypt on /apex/com.android.conscrypt@299900000
08-30 03:40:02.906    58    58 V apexd   : Creating bind-mount for /apex/com.android.conscrypt for /apex/com.android.conscrypt@299900000
08-30 03:40:02.906    58    58 V apexd   : Creating mountpoint /apex/com.android.conscrypt
08-30 03:40:02.906    58    58 V apexd   : Bind-mounting /apex/com.android.conscrypt@299900000 to /apex/com.android.conscrypt
08-30 03:40:02.906    58    58 D apexd   : Successfully activated /system/apex/com.android.conscrypt package_name: com.android.conscrypt version: 299900000
08-30 03:40:02.906    58    58 I apexd   : Found /system/apex/com.android.media
08-30 03:40:02.906    58    58 V apexd   : Creating mount point: /apex/com.android.media@290000000
08-30 03:40:02.906    58    58 I apexd   : Successfully bind-mounted flattened package /system/apex/com.android.media on /apex/com.android.media@290000000
08-30 03:40:02.906    58    58 V apexd   : Creating bind-mount for /apex/com.android.media for /apex/com.android.media@290000000
08-30 03:40:02.906    58    58 V apexd   : Creating mountpoint /apex/com.android.media
08-30 03:40:02.906    58    58 V apexd   : Bind-mounting /apex/com.android.media@290000000 to /apex/com.android.media
08-30 03:40:02.906    58    58 D apexd   : Successfully activated /system/apex/com.android.media package_name: com.android.media version: 290000000
08-30 03:40:02.906    58    58 I apexd   : Found /system/apex/com.android.tzdata
08-30 03:40:02.906    58    58 I apexd   : Skipping activation of /system/apex/com.android.tzdata same package with higher version 299900000 is already active
08-30 03:40:02.906    58    58 I apexd   : Found /system/apex/com.android.resolv
08-30 03:40:02.906    58    58 V apexd   : Creating mount point: /apex/com.android.resolv@290000000
08-30 03:40:02.906    58    58 I apexd   : Successfully bind-mounted flattened package /system/apex/com.android.resolv on /apex/com.android.resolv@290000000
08-30 03:40:02.906    58    58 V apexd   : Creating bind-mount for /apex/com.android.resolv for /apex/com.android.resolv@290000000
08-30 03:40:02.906    58    58 V apexd   : Creating mountpoint /apex/com.android.resolv
08-30 03:40:02.906    58    58 V apexd   : Bind-mounting /apex/com.android.resolv@290000000 to /apex/com.android.resolv
08-30 03:40:02.906    58    58 D apexd   : Successfully activated /system/apex/com.android.resolv package_name: com.android.resolv version: 290000000
08-30 03:40:02.906    58    58 I apexd   : Found /system/apex/com.android.media.swcodec
08-30 03:40:02.906    58    58 V apexd   : Creating mount point: /apex/com.android.media.swcodec@290000000
08-30 03:40:02.906    58    58 I apexd   : Successfully bind-mounted flattened package /system/apex/com.android.media.swcodec on /apex/com.android.media.swcodec@290000000
08-30 03:40:02.906    58    58 V apexd   : Creating bind-mount for /apex/com.android.media.swcodec for /apex/com.android.media.swcodec@290000000
08-30 03:40:02.906    58    58 V apexd   : Creating mountpoint /apex/com.android.media.swcodec
08-30 03:40:02.906    58    58 V apexd   : Bind-mounting /apex/com.android.media.swcodec@290000000 to /apex/com.android.media.swcodec
08-30 03:40:02.906    58    58 D apexd   : Successfully activated /system/apex/com.android.media.swcodec package_name: com.android.media.swcodec version: 290000000
08-30 03:40:02.906    58    58 I apexd   : Found /system/apex/com.android.runtime.release
08-30 03:40:02.906    58    58 I apexd   : Skipping activation of /system/apex/com.android.runtime.release same package with higher version 1 is already active
08-30 03:40:02.906    58    58 I apexd   : Activated 4 packages. Skipped: 2
08-30 03:40:02.906    58    58 I apexd   : Scanning /product/apex looking for APEX packages.
08-30 03:40:02.906    58    58 E apexd   : Failed to activate packages from /product/apex : Failed to scan /product/apex : Can't open /product/apex for reading : No such file or directory
08-30 03:40:02.906    58    58 I apexd   : Marking APEXd as ready
08-30 03:40:02.915    44    44 I ServiceManager: Waiting for service 'SurfaceFlinger' on '/dev/binder'...
08-30 03:40:02.916    36    36 D vold    : fscrypt_init_user0
08-30 03:40:02.916    36    36 D vold    : fscrypt_prepare_user_storage for volume null, user 0, serial 0, flags 1
08-30 03:40:02.916    36    36 D vold    : Preparing: /data/system/users/0
08-30 03:40:02.916    36    36 D vold    : Preparing: /data/misc/profiles/cur/0
08-30 03:40:02.916    36    36 D vold    : Preparing: /data/system_de/0
08-30 03:40:02.916    36    36 D vold    : Preparing: /data/misc_de/0
08-30 03:40:02.916    36    36 D vold    : Preparing: /data/vendor_de/0
08-30 03:40:02.916    36    36 D vold    : Preparing: /data/user_de/0
08-30 03:40:02.916    36    36 D vold    : /system/bin/vold_prepare_subdirs
08-30 03:40:02.916    36    36 D vold    :     prepare
08-30 03:40:02.916    36    36 D vold    :     
08-30 03:40:02.916    36    36 D vold    :     0
08-30 03:40:02.916    36    36 D vold    :     1
08-30 03:40:02.922    66    66 D vold_prepare_subdirs: Setting up mode 700 uid 0 gid 0 context null on path: /data/misc_de/0/vold
08-30 03:40:02.922    66    66 D vold_prepare_subdirs: Setting up mode 700 uid 0 gid 0 context null on path: /data/misc_de/0/storaged
08-30 03:40:02.922    66    66 D vold_prepare_subdirs: Setting up mode 700 uid 0 gid 0 context null on path: /data/misc_de/0/rollback
08-30 03:40:02.922    66    66 D vold_prepare_subdirs: Setting up mode 700 uid 1000 gid 1000 context null on path: /data/vendor_de/0/fpdata
08-30 03:40:02.922    66    66 D vold_prepare_subdirs: Setting up mode 700 uid 1000 gid 1000 context null on path: /data/vendor_de/0/facedata
08-30 03:40:02.922    36    36 D vold    : fscrypt_unlock_user_key 0 serial=0 token_present=0
08-30 03:40:02.922    36    36 E vold    : Failed to chmod /data/system_ce/0: No such file or directory
08-30 03:40:02.922    36    36 E vold    : Failed to chmod /data/misc_ce/0: No such file or directory
08-30 03:40:02.922    36    36 E vold    : Failed to chmod /data/media/0: No such file or directory
08-30 03:40:02.932    68    68 I /system/bin/tzdatacheck: timezone distro dir /data/misc/zoneinfo/current does not exist. No action required.
08-30 03:40:02.943    70    70 I art_apex: === ART pre-boot integrity checks ===
08-30 03:40:02.962    72    72 F art_apex: Device is not fsverity-enabled.
08-30 03:40:02.990    77    77 I /system/bin/flags_health_check: ServerConfigurableFlagsReset reset_mode value: 0
08-30 03:40:02.990    77    77 I /system/bin/flags_health_check: ServerConfigurableFlagsReset attempted boot count is under threshold, skipping reset.
08-30 03:40:03.008    78    78 I netdClient: Skipping libnetd_client init since *we* are netd
08-30 03:40:03.009    78    78 I netd    : netd 1.0 starting
08-30 03:40:03.010    78    78 I Netd    : Loaded resolver library from /apex/com.android.resolv/lib64/libnetd_resolv.so
08-30 03:40:03.015    44    44 I ServiceManager: Waiting for service 'SurfaceFlinger' on '/dev/binder'...
08-30 03:40:03.019    85    85 I ServiceManagement: Registered android.hardware.cas@1.1::IMediaCasService/default (start delay of 24ms)
08-30 03:40:03.019    85    85 I ServiceManagement: Removing namespace from process name android.hardware.cas@1.1-service to cas@1.1-service.
08-30 03:40:03.023   102   102 I lowmemorykiller: Using psi monitors for memory pressure detection
08-30 03:40:03.023   102   102 W lowmemorykiller: set SCHED_FIFO failed Operation not permitted
08-30 03:40:03.026    86    86 I ServiceManagement: Registered android.hardware.drm@1.0::IDrmFactory/default (start delay of 32ms)
08-30 03:40:03.026    86    86 I ServiceManagement: Removing namespace from process name android.hardware.drm@1.0-service to drm@1.0-service.
08-30 03:40:03.027    86    86 I         : Registration complete for android.hardware.drm@1.0::IDrmFactory/default.
08-30 03:40:03.028    86    86 I ServiceManagement: Registered android.hardware.drm@1.0::ICryptoFactory/default (start delay of 33ms)
08-30 03:40:03.031    86    86 I ServiceManagement: Removing namespace from process name android.hardware.drm@1.0-service to drm@1.0-service.
08-30 03:40:03.031    86    86 I         : Registration complete for android.hardware.drm@1.0::ICryptoFactory/default.
08-30 03:40:03.046    98    98 D RockitHwService: rockit.hardware.rockit.hw@1.0-service starting...
08-30 03:40:03.046    98    98 W /vendor/bin/hw/rockchip.hardware.rockit.hw@1.0-service: No seccomp policy defined for this architecture.
08-30 03:40:03.046    98    98 D RockitHwService: Instantiating rockit hw service....
08-30 03:40:03.046    98    98 D RockitHwService: RockitHwService
08-30 03:40:03.056    98    98 I ServiceManagement: Registered rockchip.hardware.rockit.hw@1.0::IRockitHwService/default (start delay of 51ms)
08-30 03:40:03.056    98    98 I ServiceManagement: Removing namespace from process name rockchip.hardware.rockit.hw@1.0-service to hw@1.0-service.
08-30 03:40:03.056    98    98 I RockitHwService: rockit hw service created
08-30 03:40:03.062    91    91 I health@2.0/: health@2.0/default: Hal starting main loop...
08-30 03:40:03.062    91    91 I health@2.0/: health@2.0/default Hal is starting up...
08-30 03:40:03.069    84    84 I ServiceManagement: Registered android.hardware.audio@5.0::IDevicesFactory/default (start delay of 75ms)
08-30 03:40:03.069    84    84 I ServiceManagement: Removing namespace from process name android.hardware.audio@2.0-service to audio@2.0-service.
08-30 03:40:03.069    84    84 I audiohalservice: Registration complete for android.hardware.audio@5.0::IDevicesFactory/default.
08-30 03:40:03.070    90    90 E android.hardware.graphics.composer@2.1-service: Couldn't set SCHED_FIFO: 1
08-30 03:40:03.070    91    91 I ServiceManagement: Registered android.hardware.health@2.0::IHealth/default (start delay of 66ms)
08-30 03:40:03.071    91    91 I ServiceManagement: Removing namespace from process name android.hardware.health@2.0-service to health@2.0-service.
08-30 03:40:03.071    91    91 I health@2.0/: health@2.0/default: Hal init done
08-30 03:40:03.086    92    92 E light   : light_open lights backlight failed: -38
08-30 03:40:03.086    92    92 E light   : Light passthrough failed to load legacy HAL.
08-30 03:40:03.086    92    92 E light   : light_open lights keyboard failed: -38
08-30 03:40:03.086    92    92 E light   : Light passthrough failed to load legacy HAL.
08-30 03:40:03.087    92    92 E light   : light_open lights buttons failed: -38
08-30 03:40:03.087    92    92 E light   : Light passthrough failed to load legacy HAL.
08-30 03:40:03.087    92    92 E light   : light_open lights battery failed: -38
08-30 03:40:03.087    92    92 E light   : Light passthrough failed to load legacy HAL.
08-30 03:40:03.087    92    92 E light   : light_open lights notifications failed: -38
08-30 03:40:03.087    92    92 E light   : Light passthrough failed to load legacy HAL.
08-30 03:40:03.087    92    92 E light   : light_open lights attention failed: -38
08-30 03:40:03.087    92    92 E light   : Light passthrough failed to load legacy HAL.
08-30 03:40:03.087    92    92 E light   : light_open lights bluetooth failed: -38
08-30 03:40:03.087    92    92 E light   : Light passthrough failed to load legacy HAL.
08-30 03:40:03.087    92    92 E light   : light_open lights wifi failed: -38
08-30 03:40:03.087    92    92 E light   : Light passthrough failed to load legacy HAL.
08-30 03:40:03.087    92    92 I light   : Could not open any lights.
08-30 03:40:03.087    94    94 I ServiceManagement: Registered android.hardware.radio.config@1.0::IRadioConfig/default (start delay of 81ms)
08-30 03:40:03.087    94    94 I ServiceManagement: Removing namespace from process name android.hardware.radio.config@1.0-service to config@1.0-service.
08-30 03:40:03.087    94    94 D android.hardware.radio.config@1.0-service: Default service is ready.
08-30 03:40:03.087    90    90 D hwc-drm-debug: DrmHwcTwo version : HWC2-1.4.10-Android-10-Patch2-Container
08-30 03:40:03.088    90    90 I hwc-drm-device: InitEnvFromXml,line=158 Load /vendor/etc/HwComposerEnv.xml success.
08-30 03:40:03.088    90    90 I hwc-drm-device: InitEnvFromXml,line=193 Version=1.1.1 Mode=0 FbWidth=11520 FbHeight=1080 ConnectorCnt=4
08-30 03:40:03.088    90    90 I hwc-drm-device: InitEnvFromXml,line=245 Connector[0] type=HDMI-A-1 [0,0,3840,1080]=>[0,0,0,0]
08-30 03:40:03.088    90    90 I hwc-drm-device: InitEnvFromXml,line=245 Connector[1] type=HDMI-A-2 [3840,0,1920,1080]=>[0,0,0,0]
08-30 03:40:03.088    90    90 I hwc-drm-device: InitEnvFromXml,line=245 Connector[2] type=HDMI-A-3 [5760,0,1920,1080]=>[0,0,0,0]
08-30 03:40:03.088    90    90 I hwc-drm-device: InitEnvFromXml,line=245 Connector[3] type=DP-1 [7680,0,3840,1080]=>[0,0,0,0]
08-30 03:40:03.088    96    96 I android.hardware.wifi@1.0-service: Wifi Hal is booting up...
08-30 03:40:03.090    96    96 I ServiceManagement: Registered android.hardware.wifi@1.3::IWifi/default (start delay of 85ms)
08-30 03:40:03.090    96    96 I ServiceManagement: Removing namespace from process name android.hardware.wifi@1.0-service to wifi@1.0-service.
08-30 03:40:03.090    92    92 I ServiceManagement: Registered android.hardware.light@2.0::ILight/default (start delay of 86ms)
08-30 03:40:03.090    92    92 I ServiceManagement: Removing namespace from process name android.hardware.light@2.0-service to light@2.0-service.
08-30 03:40:03.090    92    92 I         : Registration complete for android.hardware.light@2.0::ILight/default.
08-30 03:40:03.093    84    84 I ServiceManagement: Registered android.hardware.audio.effect@5.0::IEffectsFactory/default (start delay of 99ms)
08-30 03:40:03.093    84    84 I audiohalservice: Registration complete for android.hardware.audio.effect@5.0::IEffectsFactory/default.
08-30 03:40:03.094    28    28 I hwservicemanager: getTransport: Cannot find entry android.hardware.soundtrigger@2.2::ISoundTriggerHw/default in either framework or device manifest.
08-30 03:40:03.094    84    84 E audiohalservice: Could not get passthrough implementation for android.hardware.soundtrigger@2.2::ISoundTriggerHw/default.
08-30 03:40:03.094    28    28 I hwservicemanager: getTransport: Cannot find entry android.hardware.soundtrigger@2.1::ISoundTriggerHw/default in either framework or device manifest.
08-30 03:40:03.094    88    88 I ServiceManagement: Registered android.hardware.gnss@1.0::IGnss/default (start delay of 100ms)
08-30 03:40:03.095    88    88 I ServiceManagement: Removing namespace from process name android.hardware.gnss@1.0-service to gnss@1.0-service.
08-30 03:40:03.095    88    88 I android.hardware.gnss@1.0-service: Registration complete for android.hardware.gnss@1.0::IGnss/default.
08-30 03:40:03.095    84    84 E audiohalservice: Could not get passthrough implementation for android.hardware.soundtrigger@2.1::ISoundTriggerHw/default.
08-30 03:40:03.097    84    84 E SoundTriggerHalImpl: couldn't load sound trigger module sound_trigger.primary (No such file or directory)
08-30 03:40:03.100    89    89 I ServiceManagement: Registered android.hardware.graphics.allocator@3.0::IAllocator/default (start delay of 105ms)
08-30 03:40:03.100    89    89 I ServiceManagement: Removing namespace from process name android.hardware.graphics.allocator@3.0-service to allocator@3.0-service.
08-30 03:40:03.100    89    89 I android.hardware.graphics.allocator@3.0-service: Registration complete for android.hardware.graphics.allocator@3.0::IAllocator/default.
08-30 03:40:03.101    97    97 D rockchip.hardware.outputmanager@1.0-service: ***************defaultPassthroughServiceImplementation IRkOutputManager ******
08-30 03:40:03.101    97    97 E rockchip.hardware.outputmanager@1.0-service: Couldn't set SCHED_FIFO: 1
08-30 03:40:03.101    84    84 I ServiceManagement: Registered android.hardware.soundtrigger@2.0::ISoundTriggerHw/default (start delay of 107ms)
08-30 03:40:03.101    84    84 I audiohalservice: Registration complete for android.hardware.soundtrigger@2.0::ISoundTriggerHw/default.
08-30 03:40:03.101    81    81 I bootstat: Service started: /system/bin/bootstat --set_system_boot_reason 
08-30 03:40:03.101    81    81 I bootstat: Canonical boot reason: reboot,shell
08-30 03:40:03.101    81    81 I bootstat: Canonical boot reason: reboot,shell
08-30 03:40:03.102    28    28 I hwservicemanager: getTransport: Cannot find entry android.hardware.bluetooth.audio@2.0::IBluetoothAudioProvidersFactory/default in either framework or device manifest.
08-30 03:40:03.103    84    84 E audiohalservice: Could not get passthrough implementation for android.hardware.bluetooth.audio@2.0::IBluetoothAudioProvidersFactory/default.
08-30 03:40:03.103    84    84 W audiohalservice: Could not register Bluetooth Audio API 2.0
08-30 03:40:03.103    28    28 I hwservicemanager: getTransport: Cannot find entry android.hardware.bluetooth.a2dp@1.0::IBluetoothAudioOffload/default in either framework or device manifest.
08-30 03:40:03.103    97    97 I ServiceManagement: Registered rockchip.hardware.outputmanager@1.0::IRkOutputManager/default (start delay of 99ms)
08-30 03:40:03.103    97    97 I ServiceManagement: Removing namespace from process name rockchip.hardware.outputmanager@1.0-service to outputmanager@1.0-service.
08-30 03:40:03.104    97    97 I rockchip.hardware.outputmanager@1.0-service: Registration complete for rockchip.hardware.outputmanager@1.0::IRkOutputManager/default.
08-30 03:40:03.104    84    84 E audiohalservice: Could not get passthrough implementation for android.hardware.bluetooth.a2dp@1.0::IBluetoothAudioOffload/default.
08-30 03:40:03.104    84    84 W audiohalservice: Could not register Bluetooth audio offload 1.0
08-30 03:40:03.113    83    83 I ServiceManagement: Registered android.system.suspend@1.0::ISystemSuspend/default (start delay of 119ms)
08-30 03:40:03.113    83    83 I ServiceManagement: Removing namespace from process name android.system.suspend@1.0-service to suspend@1.0-service.
08-30 03:40:03.114    90    90 I hwc-drm-baseparameter: DrmBaseparameter validate fail!
08-30 03:40:03.114    90    90 I hwc-drm-device: DrmVersion=3.0.0
08-30 03:40:03.114    90    90 D hwc-drm-device: ro.container.primary_type is 
08-30 03:40:03.114    90    90 D hwc-drm-device: ro.container.primary_type is not set, use normal mode
08-30 03:40:03.114    90    90 E hwc-drm-crtc: Failed to get left margin property
08-30 03:40:03.114    90    90 E hwc-drm-crtc: Failed to get right margin property
08-30 03:40:03.114    90    90 E hwc-drm-crtc: Failed to get top margin property
08-30 03:40:03.114    90    90 E hwc-drm-crtc: Failed to get bottom margin property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get PORT_ID property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get PORT_ID value
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get ACLK property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get plane_mask property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get GAMMA_LUT property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get GAMMA_LUT_SIZE property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get CUBIC_LUT property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get CUBIC_LUT_SIZE property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Could not get FEATURE property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Could not get variable_refresh_rate property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Could not get max_refresh_rate property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Could not get min_refresh_rate_ property
08-30 03:40:03.115    90    90 I hwc-drm-crtc: Init,line=278 crtc-id=58 vrr=0, maxrr=0 minrr=0
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get left margin property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get right margin property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get top margin property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get bottom margin property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get PORT_ID property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get PORT_ID value
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get ACLK property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get plane_mask property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get GAMMA_LUT property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get GAMMA_LUT_SIZE property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get CUBIC_LUT property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get CUBIC_LUT_SIZE property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Could not get FEATURE property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Could not get variable_refresh_rate property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Could not get max_refresh_rate property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Could not get min_refresh_rate_ property
08-30 03:40:03.115    90    90 I hwc-drm-crtc: Init,line=278 crtc-id=64 vrr=0, maxrr=0 minrr=0
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get left margin property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get right margin property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get top margin property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get bottom margin property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get PORT_ID property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get PORT_ID value
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get ACLK property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get plane_mask property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get GAMMA_LUT property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get GAMMA_LUT_SIZE property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get CUBIC_LUT property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get CUBIC_LUT_SIZE property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Could not get FEATURE property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Could not get variable_refresh_rate property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Could not get max_refresh_rate property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Could not get min_refresh_rate_ property
08-30 03:40:03.115    90    90 I hwc-drm-crtc: Init,line=278 crtc-id=70 vrr=0, maxrr=0 minrr=0
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get left margin property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get right margin property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get top margin property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get bottom margin property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get PORT_ID property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get PORT_ID value
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get ACLK property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get plane_mask property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get GAMMA_LUT property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get GAMMA_LUT_SIZE property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get CUBIC_LUT property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get CUBIC_LUT_SIZE property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Could not get FEATURE property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Could not get variable_refresh_rate property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Could not get max_refresh_rate property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Could not get min_refresh_rate_ property
08-30 03:40:03.115    90    90 I hwc-drm-crtc: Init,line=278 crtc-id=76 vrr=0, maxrr=0 minrr=0
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get left margin property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get right margin property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get top margin property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get bottom margin property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get PORT_ID property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get PORT_ID value
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get ACLK property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get plane_mask property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get GAMMA_LUT property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get GAMMA_LUT_SIZE property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get CUBIC_LUT property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get CUBIC_LUT_SIZE property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Could not get FEATURE property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Could not get variable_refresh_rate property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Could not get max_refresh_rate property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Could not get min_refresh_rate_ property
08-30 03:40:03.115    90    90 I hwc-drm-crtc: Init,line=278 crtc-id=82 vrr=0, maxrr=0 minrr=0
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get left margin property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get right margin property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get top margin property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get bottom margin property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get PORT_ID property
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get PORT_ID value
08-30 03:40:03.115    90    90 E hwc-drm-crtc: Failed to get ACLK property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Failed to get plane_mask property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Failed to get GAMMA_LUT property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Failed to get GAMMA_LUT_SIZE property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Failed to get CUBIC_LUT property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Failed to get CUBIC_LUT_SIZE property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Could not get FEATURE property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Could not get variable_refresh_rate property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Could not get max_refresh_rate property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Could not get min_refresh_rate_ property
08-30 03:40:03.116    90    90 I hwc-drm-crtc: Init,line=278 crtc-id=88 vrr=0, maxrr=0 minrr=0
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Failed to get left margin property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Failed to get right margin property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Failed to get top margin property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Failed to get bottom margin property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Failed to get PORT_ID property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Failed to get PORT_ID value
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Failed to get ACLK property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Failed to get plane_mask property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Failed to get GAMMA_LUT property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Failed to get GAMMA_LUT_SIZE property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Failed to get CUBIC_LUT property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Failed to get CUBIC_LUT_SIZE property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Could not get FEATURE property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Could not get variable_refresh_rate property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Could not get max_refresh_rate property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Could not get min_refresh_rate_ property
08-30 03:40:03.116    90    90 I hwc-drm-crtc: Init,line=278 crtc-id=94 vrr=0, maxrr=0 minrr=0
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Failed to get left margin property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Failed to get right margin property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Failed to get top margin property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Failed to get bottom margin property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Failed to get PORT_ID property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Failed to get PORT_ID value
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Failed to get ACLK property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Failed to get plane_mask property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Failed to get GAMMA_LUT property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Failed to get GAMMA_LUT_SIZE property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Failed to get CUBIC_LUT property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Failed to get CUBIC_LUT_SIZE property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Could not get FEATURE property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Could not get variable_refresh_rate property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Could not get max_refresh_rate property
08-30 03:40:03.116    90    90 E hwc-drm-crtc: Could not get min_refresh_rate_ property
08-30 03:40:03.116    90    90 I hwc-drm-crtc: Init,line=278 crtc-id=100 vrr=0, maxrr=0 minrr=0
08-30 03:40:03.116    90    90 E hwc-drm-device: DONE probing crtc
08-30 03:40:03.117    90    90 W hwc-drm-connector: Could not get hdr output metadata property
08-30 03:40:03.117    90    90 W hwc-drm-connector: Could not get hdr panel metadata property
08-30 03:40:03.117    90    90 W hwc-drm-connector: Could not get Colorspace property, try to get hdmi_output_colorimetry property.
08-30 03:40:03.117    90    90 W hwc-drm-connector: Could not get hdmi_output_colorimetry property.
08-30 03:40:03.117    90    90 W hwc-drm-connector: Could not get color_format property, try to get hdmi_output_format property.
08-30 03:40:03.117    90    90 W hwc-drm-connector: Could not get hdmi_output_format property.
08-30 03:40:03.117    90    90 W hwc-drm-connector: Could not get color_depth property, try to get hdmi_output_depth
08-30 03:40:03.117    90    90 W hwc-drm-connector: Could not get hdmi_output_depth property
08-30 03:40:03.117    90    90 W hwc-drm-connector: Could not get hdmi_output_format property
08-30 03:40:03.117    90    90 W hwc-drm-connector: Could not get hdmi_output_depth property
08-30 03:40:03.117    90    90 W hwc-drm-connector: Could not get CONNECTOR_ID property
08-30 03:40:03.117    90    90 I hwc-drm-connector: UpdateConnectorBaseInfo fail, the device may not have a baseparameter.
08-30 03:40:03.117    90    90 W hwc-drm-connector: Could not get USER_SPLIT_MODE property
08-30 03:40:03.117    44    44 I ServiceManager: Waiting for service 'SurfaceFlinger' on '/dev/binder'...
08-30 03:40:03.118    82    82 I ServiceManagement: Registered android.hidl.allocator@1.0::IAllocator/ashmem (start delay of 120ms)
08-30 03:40:03.118    82    82 I ServiceManagement: Removing namespace from process name android.hidl.allocator@1.0-service to allocator@1.0-service.
08-30 03:40:03.118    90    90 W hwc-drm-connector: Could not get hdr output metadata property
08-30 03:40:03.118    90    90 W hwc-drm-connector: Could not get hdr panel metadata property
08-30 03:40:03.118    90    90 W hwc-drm-connector: Could not get Colorspace property, try to get hdmi_output_colorimetry property.
08-30 03:40:03.118    90    90 W hwc-drm-connector: Could not get hdmi_output_colorimetry property.
08-30 03:40:03.118    90    90 W hwc-drm-connector: Could not get color_format property, try to get hdmi_output_format property.
08-30 03:40:03.118    90    90 W hwc-drm-connector: Could not get hdmi_output_format property.
08-30 03:40:03.118    90    90 W hwc-drm-connector: Could not get color_depth property, try to get hdmi_output_depth
08-30 03:40:03.118    90    90 W hwc-drm-connector: Could not get hdmi_output_depth property
08-30 03:40:03.118    90    90 W hwc-drm-connector: Could not get hdmi_output_format property
08-30 03:40:03.118    90    90 W hwc-drm-connector: Could not get hdmi_output_depth property
08-30 03:40:03.118    90    90 W hwc-drm-connector: Could not get CONNECTOR_ID property
08-30 03:40:03.118    90    90 I hwc-drm-connector: UpdateConnectorBaseInfo fail, the device may not have a baseparameter.
08-30 03:40:03.118    90    90 W hwc-drm-connector: Could not get USER_SPLIT_MODE property
08-30 03:40:03.119    90    90 W hwc-drm-connector: Could not get hdr output metadata property
08-30 03:40:03.119    90    90 W hwc-drm-connector: Could not get hdr panel metadata property
08-30 03:40:03.119    90    90 W hwc-drm-connector: Could not get Colorspace property, try to get hdmi_output_colorimetry property.
08-30 03:40:03.119    90    90 W hwc-drm-connector: Could not get hdmi_output_colorimetry property.
08-30 03:40:03.119    90    90 W hwc-drm-connector: Could not get color_format property, try to get hdmi_output_format property.
08-30 03:40:03.119    90    90 W hwc-drm-connector: Could not get hdmi_output_format property.
08-30 03:40:03.119    90    90 W hwc-drm-connector: Could not get color_depth property, try to get hdmi_output_depth
08-30 03:40:03.119    90    90 W hwc-drm-connector: Could not get hdmi_output_depth property
08-30 03:40:03.119    90    90 W hwc-drm-connector: Could not get hdmi_output_format property
08-30 03:40:03.119    90    90 W hwc-drm-connector: Could not get hdmi_output_depth property
08-30 03:40:03.119    90    90 W hwc-drm-connector: Could not get CONNECTOR_ID property
08-30 03:40:03.119    90    90 I hwc-drm-connector: UpdateConnectorBaseInfo fail, the device may not have a baseparameter.
08-30 03:40:03.119    90    90 W hwc-drm-connector: Could not get USER_SPLIT_MODE property
08-30 03:40:03.120    90    90 W hwc-drm-connector: Could not get hdr output metadata property
08-30 03:40:03.120    90    90 W hwc-drm-connector: Could not get hdr panel metadata property
08-30 03:40:03.120    90    90 W hwc-drm-connector: Could not get Colorspace property, try to get hdmi_output_colorimetry property.
08-30 03:40:03.120    90    90 W hwc-drm-connector: Could not get hdmi_output_colorimetry property.
08-30 03:40:03.120    90    90 W hwc-drm-connector: Could not get color_format property, try to get hdmi_output_format property.
08-30 03:40:03.120    90    90 W hwc-drm-connector: Could not get hdmi_output_format property.
08-30 03:40:03.120    90    90 W hwc-drm-connector: Could not get color_depth property, try to get hdmi_output_depth
08-30 03:40:03.120    90    90 W hwc-drm-connector: Could not get hdmi_output_depth property
08-30 03:40:03.120    90    90 W hwc-drm-connector: Could not get hdmi_output_format property
08-30 03:40:03.121    90    90 W hwc-drm-connector: Could not get hdmi_output_depth property
08-30 03:40:03.121    90    90 W hwc-drm-connector: Could not get CONNECTOR_ID property
08-30 03:40:03.121    90    90 I hwc-drm-connector: UpdateConnectorBaseInfo fail, the device may not have a baseparameter.
08-30 03:40:03.121    90    90 W hwc-drm-connector: Could not get USER_SPLIT_MODE property
08-30 03:40:03.122    90    90 W hwc-drm-connector: Could not get hdr output metadata property
08-30 03:40:03.122    90    90 W hwc-drm-connector: Could not get hdr panel metadata property
08-30 03:40:03.122    90    90 W hwc-drm-connector: Could not get Colorspace property, try to get hdmi_output_colorimetry property.
08-30 03:40:03.122    90    90 W hwc-drm-connector: Could not get hdmi_output_colorimetry property.
08-30 03:40:03.122    90    90 W hwc-drm-connector: Could not get color_format property, try to get hdmi_output_format property.
08-30 03:40:03.122    90    90 W hwc-drm-connector: Could not get hdmi_output_format property.
08-30 03:40:03.122    90    90 W hwc-drm-connector: Could not get color_depth property, try to get hdmi_output_depth
08-30 03:40:03.122    90    90 W hwc-drm-connector: Could not get hdmi_output_depth property
08-30 03:40:03.122    90    90 W hwc-drm-connector: Could not get hdmi_output_format property
08-30 03:40:03.122    90    90 W hwc-drm-connector: Could not get hdmi_output_depth property
08-30 03:40:03.122    90    90 W hwc-drm-connector: Could not get CONNECTOR_ID property
08-30 03:40:03.122    90    90 I hwc-drm-connector: UpdateConnectorBaseInfo fail, the device may not have a baseparameter.
08-30 03:40:03.122    90    90 W hwc-drm-connector: Could not get USER_SPLIT_MODE property
08-30 03:40:03.123    90    90 W hwc-drm-connector: Could not get hdr output metadata property
08-30 03:40:03.123    90    90 W hwc-drm-connector: Could not get hdr panel metadata property
08-30 03:40:03.123    90    90 W hwc-drm-connector: Could not get Colorspace property, try to get hdmi_output_colorimetry property.
08-30 03:40:03.123    90    90 W hwc-drm-connector: Could not get hdmi_output_colorimetry property.
08-30 03:40:03.123    90    90 W hwc-drm-connector: Could not get color_format property, try to get hdmi_output_format property.
08-30 03:40:03.123    90    90 W hwc-drm-connector: Could not get hdmi_output_format property.
08-30 03:40:03.123    90    90 W hwc-drm-connector: Could not get color_depth property, try to get hdmi_output_depth
08-30 03:40:03.123    90    90 W hwc-drm-connector: Could not get hdmi_output_depth property
08-30 03:40:03.123    90    90 W hwc-drm-connector: Could not get hdmi_output_format property
08-30 03:40:03.123    90    90 W hwc-drm-connector: Could not get hdmi_output_depth property
08-30 03:40:03.123    90    90 W hwc-drm-connector: Could not get CONNECTOR_ID property
08-30 03:40:03.123    90    90 I hwc-drm-connector: UpdateConnectorBaseInfo fail, the device may not have a baseparameter.
08-30 03:40:03.123    90    90 W hwc-drm-connector: Could not get USER_SPLIT_MODE property
08-30 03:40:03.124    90    90 W hwc-drm-connector: Could not get hdr output metadata property
08-30 03:40:03.124    90    90 W hwc-drm-connector: Could not get hdr panel metadata property
08-30 03:40:03.124    90    90 W hwc-drm-connector: Could not get Colorspace property, try to get hdmi_output_colorimetry property.
08-30 03:40:03.124    90    90 W hwc-drm-connector: Could not get hdmi_output_colorimetry property.
08-30 03:40:03.124    90    90 W hwc-drm-connector: Could not get color_format property, try to get hdmi_output_format property.
08-30 03:40:03.124    90    90 W hwc-drm-connector: Could not get hdmi_output_format property.
08-30 03:40:03.124    90    90 W hwc-drm-connector: Could not get color_depth property, try to get hdmi_output_depth
08-30 03:40:03.124    90    90 W hwc-drm-connector: Could not get hdmi_output_depth property
08-30 03:40:03.124    90    90 W hwc-drm-connector: Could not get hdmi_output_format property
08-30 03:40:03.124    90    90 W hwc-drm-connector: Could not get hdmi_output_depth property
08-30 03:40:03.124    90    90 W hwc-drm-connector: Could not get CONNECTOR_ID property
08-30 03:40:03.124    90    90 I hwc-drm-connector: UpdateConnectorBaseInfo fail, the device may not have a baseparameter.
08-30 03:40:03.124    90    90 W hwc-drm-connector: Could not get USER_SPLIT_MODE property
08-30 03:40:03.124   100   100 I FastMixerState: sMaxFastTracks = 8
08-30 03:40:03.125    90    90 W hwc-drm-connector: Could not get hdr output metadata property
08-30 03:40:03.125    90    90 W hwc-drm-connector: Could not get hdr panel metadata property
08-30 03:40:03.125    90    90 W hwc-drm-connector: Could not get Colorspace property, try to get hdmi_output_colorimetry property.
08-30 03:40:03.125    90    90 W hwc-drm-connector: Could not get hdmi_output_colorimetry property.
08-30 03:40:03.125    90    90 W hwc-drm-connector: Could not get color_format property, try to get hdmi_output_format property.
08-30 03:40:03.125    90    90 W hwc-drm-connector: Could not get hdmi_output_format property.
08-30 03:40:03.125    90    90 W hwc-drm-connector: Could not get color_depth property, try to get hdmi_output_depth
08-30 03:40:03.125    90    90 W hwc-drm-connector: Could not get hdmi_output_depth property
08-30 03:40:03.125    90    90 W hwc-drm-connector: Could not get hdmi_output_format property
08-30 03:40:03.125    90    90 W hwc-drm-connector: Could not get hdmi_output_depth property
08-30 03:40:03.125    90    90 W hwc-drm-connector: Could not get CONNECTOR_ID property
08-30 03:40:03.125   100   100 V MediaUtils: physMem: 16703926272
08-30 03:40:03.125    90    90 I hwc-drm-connector: UpdateConnectorBaseInfo fail, the device may not have a baseparameter.
08-30 03:40:03.125   100   100 V MediaUtils: requested limit: 536870912
08-30 03:40:03.125    90    90 W hwc-drm-connector: Could not get USER_SPLIT_MODE property
08-30 03:40:03.125   100   100 I libc    : malloc_limit: Allocation limit enabled, max size 536870912 bytes
08-30 03:40:03.125   100   100 I audioserver: ServiceManager: 0x73e85c3dc0
08-30 03:40:03.125   100   100 W BatteryNotifier: batterystats service unavailable!
08-30 03:40:03.125    90    90 I hwc-drm-device: UpdateInfoFromXml,line=261 DmXml_.Mode = 0 
08-30 03:40:03.126    90    90 I hwc-drm-plane: Could not get eotf property
08-30 03:40:03.126    90    90 I hwc-drm-plane: Could not get colorspace property
08-30 03:40:03.126    90    90 E hwc-drm-plane: Could not get ZPOS property, try to get zpos property
08-30 03:40:03.126    90    90 E hwc-drm-plane: Could not get zpos property
08-30 03:40:03.126    90    90 E hwc-drm-plane: Could not get AREA_ID property
08-30 03:40:03.126    90    90 E hwc-drm-plane: Could not get SHARE_ID property
08-30 03:40:03.126    90    90 E hwc-drm-plane: Could not get FEATURE property
08-30 03:40:03.126    90    90 I hwc-drm-plane: Could not get alpha property
08-30 03:40:03.126    90    90 I hwc-drm-plane: Could not get pixel blend mode property
08-30 03:40:03.126    90    90 E hwc-drm-plane: Could not get FEATURE property
08-30 03:40:03.126    90    90 E hwc-drm-plane: Could not get NAME property
08-30 03:40:03.126    90    90 E hwc-drm-plane: Could not get INPUT_WIDTH property
08-30 03:40:03.126    90    90 E hwc-drm-plane: Could not get INPUT_HEIGHT property
08-30 03:40:03.126    90    90 E hwc-drm-plane: Could not get OUTPUT_WIDTH property
08-30 03:40:03.126    90    90 E hwc-drm-plane: Could not get OUTPUT_HEIGHT property
08-30 03:40:03.126    90    90 E hwc-drm-plane: Could not get SCALE_RATE property
08-30 03:40:03.126    90    90 E hwc-drm-plane: Could not get ASYNC_COMMIT property
08-30 03:40:03.126    90    90 I hwc-drm-plane: Could not get eotf property
08-30 03:40:03.126    90    90 I hwc-drm-plane: Could not get colorspace property
08-30 03:40:03.126    28    28 I hwservicemanager: getTransport: Cannot find entry android.hardware.audio@5.0::IDevicesFactory/msd in either framework or device manifest.
08-30 03:40:03.126    90    90 E hwc-drm-plane: Could not get ZPOS property, try to get zpos property
08-30 03:40:03.126    90    90 E hwc-drm-plane: Could not get zpos property
08-30 03:40:03.126    90    90 E hwc-drm-plane: Could not get AREA_ID property
08-30 03:40:03.126    90    90 E hwc-drm-plane: Could not get SHARE_ID property
08-30 03:40:03.126    90    90 E hwc-drm-plane: Could not get FEATURE property
08-30 03:40:03.126    90    90 I hwc-drm-plane: Could not get alpha property
08-30 03:40:03.126    90    90 I hwc-drm-plane: Could not get pixel blend mode property
08-30 03:40:03.126    90    90 E hwc-drm-plane: Could not get FEATURE property
08-30 03:40:03.126    90    90 E hwc-drm-plane: Could not get NAME property
08-30 03:40:03.126    90    90 E hwc-drm-plane: Could not get INPUT_WIDTH property
08-30 03:40:03.126    90    90 E hwc-drm-plane: Could not get INPUT_HEIGHT property
08-30 03:40:03.126    90    90 E hwc-drm-plane: Could not get OUTPUT_WIDTH property
08-30 03:40:03.126    90    90 E hwc-drm-plane: Could not get OUTPUT_HEIGHT property
08-30 03:40:03.126    90    90 E hwc-drm-plane: Could not get SCALE_RATE property
08-30 03:40:03.126    90    90 E hwc-drm-plane: Could not get ASYNC_COMMIT property
08-30 03:40:03.126    90    90 I hwc-drm-plane: Could not get eotf property
08-30 03:40:03.126    90    90 I hwc-drm-plane: Could not get colorspace property
08-30 03:40:03.126    90    90 E hwc-drm-plane: Could not get ZPOS property, try to get zpos property
08-30 03:40:03.127    90    90 E hwc-drm-plane: Could not get zpos property
08-30 03:40:03.127    90    90 E hwc-drm-plane: Could not get AREA_ID property
08-30 03:40:03.127    90    90 E hwc-drm-plane: Could not get SHARE_ID property
08-30 03:40:03.127    90    90 E hwc-drm-plane: Could not get FEATURE property
08-30 03:40:03.127    90    90 I hwc-drm-plane: Could not get alpha property
08-30 03:40:03.127    90    90 I hwc-drm-plane: Could not get pixel blend mode property
08-30 03:40:03.127    90    90 E hwc-drm-plane: Could not get FEATURE property
08-30 03:40:03.127    90    90 E hwc-drm-plane: Could not get NAME property
08-30 03:40:03.127    90    90 E hwc-drm-plane: Could not get INPUT_WIDTH property
08-30 03:40:03.127    90    90 E hwc-drm-plane: Could not get INPUT_HEIGHT property
08-30 03:40:03.127    90    90 E hwc-drm-plane: Could not get OUTPUT_WIDTH property
08-30 03:40:03.127   100   100 I AudioFlinger: Using default 3000 mSec as standby time.
08-30 03:40:03.127    90    90 E hwc-drm-plane: Could not get OUTPUT_HEIGHT property
08-30 03:40:03.127    90    90 E hwc-drm-plane: Could not get SCALE_RATE property
08-30 03:40:03.127    90    90 E hwc-drm-plane: Could not get ASYNC_COMMIT property
08-30 03:40:03.127    90    90 I hwc-drm-plane: Could not get eotf property
08-30 03:40:03.127    90    90 I hwc-drm-plane: Could not get colorspace property
08-30 03:40:03.127    90    90 E hwc-drm-plane: Could not get ZPOS property, try to get zpos property
08-30 03:40:03.127    90    90 E hwc-drm-plane: Could not get zpos property
08-30 03:40:03.127    90    90 E hwc-drm-plane: Could not get AREA_ID property
08-30 03:40:03.127    90    90 E hwc-drm-plane: Could not get SHARE_ID property
08-30 03:40:03.127    90    90 E hwc-drm-plane: Could not get FEATURE property
08-30 03:40:03.127    90    90 I hwc-drm-plane: Could not get alpha property
08-30 03:40:03.127    90    90 I hwc-drm-plane: Could not get pixel blend mode property
08-30 03:40:03.127   100   100 E APM::Serializer: deserialize: Could not parse /odm/etc/audio_policy_configuration.xml document.
08-30 03:40:03.127    90    90 E hwc-drm-plane: Could not get FEATURE property
08-30 03:40:03.127    90    90 E hwc-drm-plane: Could not get NAME property
08-30 03:40:03.127    90    90 E hwc-drm-plane: Could not get INPUT_WIDTH property
08-30 03:40:03.127    90    90 E hwc-drm-plane: Could not get INPUT_HEIGHT property
08-30 03:40:03.127    90    90 E hwc-drm-plane: Could not get OUTPUT_WIDTH property
08-30 03:40:03.127    90    90 E hwc-drm-plane: Could not get OUTPUT_HEIGHT property
08-30 03:40:03.127    90    90 E hwc-drm-plane: Could not get SCALE_RATE property
08-30 03:40:03.128    90    90 E hwc-drm-plane: Could not get ASYNC_COMMIT property
08-30 03:40:03.128    90    90 I hwc-drm-plane: Could not get eotf property
08-30 03:40:03.128    90    90 I hwc-drm-plane: Could not get colorspace property
08-30 03:40:03.128    90    90 E hwc-drm-plane: Could not get ZPOS property, try to get zpos property
08-30 03:40:03.128    90    90 E hwc-drm-plane: Could not get zpos property
08-30 03:40:03.128    90    90 E hwc-drm-plane: Could not get AREA_ID property
08-30 03:40:03.128    90    90 E hwc-drm-plane: Could not get SHARE_ID property
08-30 03:40:03.128    90    90 E hwc-drm-plane: Could not get FEATURE property
08-30 03:40:03.128    90    90 I hwc-drm-plane: Could not get alpha property
08-30 03:40:03.128    90    90 I hwc-drm-plane: Could not get pixel blend mode property
08-30 03:40:03.128    90    90 E hwc-drm-plane: Could not get FEATURE property
08-30 03:40:03.128    90    90 E hwc-drm-plane: Could not get NAME property
08-30 03:40:03.128    90    90 E hwc-drm-plane: Could not get INPUT_WIDTH property
08-30 03:40:03.128    90    90 E hwc-drm-plane: Could not get INPUT_HEIGHT property
08-30 03:40:03.128    90    90 E hwc-drm-plane: Could not get OUTPUT_WIDTH property
08-30 03:40:03.128    90    90 E hwc-drm-plane: Could not get OUTPUT_HEIGHT property
08-30 03:40:03.128    90    90 E hwc-drm-plane: Could not get SCALE_RATE property
08-30 03:40:03.128    90    90 E hwc-drm-plane: Could not get ASYNC_COMMIT property
08-30 03:40:03.128    90    90 I hwc-drm-plane: Could not get eotf property
08-30 03:40:03.128    90    90 I hwc-drm-plane: Could not get colorspace property
08-30 03:40:03.128    90    90 E hwc-drm-plane: Could not get ZPOS property, try to get zpos property
08-30 03:40:03.128    90    90 E hwc-drm-plane: Could not get zpos property
08-30 03:40:03.128    90    90 E hwc-drm-plane: Could not get AREA_ID property
08-30 03:40:03.128    90    90 E hwc-drm-plane: Could not get SHARE_ID property
08-30 03:40:03.128    90    90 E hwc-drm-plane: Could not get FEATURE property
08-30 03:40:03.128    90    90 I hwc-drm-plane: Could not get alpha property
08-30 03:40:03.128    90    90 I hwc-drm-plane: Could not get pixel blend mode property
08-30 03:40:03.128    90    90 E hwc-drm-plane: Could not get FEATURE property
08-30 03:40:03.128    90    90 E hwc-drm-plane: Could not get NAME property
08-30 03:40:03.128    90    90 E hwc-drm-plane: Could not get INPUT_WIDTH property
08-30 03:40:03.128    90    90 E hwc-drm-plane: Could not get INPUT_HEIGHT property
08-30 03:40:03.128    90    90 E hwc-drm-plane: Could not get OUTPUT_WIDTH property
08-30 03:40:03.128    90    90 E hwc-drm-plane: Could not get OUTPUT_HEIGHT property
08-30 03:40:03.128    90    90 E hwc-drm-plane: Could not get SCALE_RATE property
08-30 03:40:03.128    90    90 E hwc-drm-plane: Could not get ASYNC_COMMIT property
08-30 03:40:03.128    90    90 I hwc-drm-plane: Could not get eotf property
08-30 03:40:03.128    90    90 I hwc-drm-plane: Could not get colorspace property
08-30 03:40:03.129    90    90 E hwc-drm-plane: Could not get ZPOS property, try to get zpos property
08-30 03:40:03.129    90    90 E hwc-drm-plane: Could not get zpos property
08-30 03:40:03.129    90    90 E hwc-drm-plane: Could not get AREA_ID property
08-30 03:40:03.129    90    90 E hwc-drm-plane: Could not get SHARE_ID property
08-30 03:40:03.129    90    90 E hwc-drm-plane: Could not get FEATURE property
08-30 03:40:03.129    90    90 I hwc-drm-plane: Could not get alpha property
08-30 03:40:03.129    90    90 I hwc-drm-plane: Could not get pixel blend mode property
08-30 03:40:03.129    90    90 E hwc-drm-plane: Could not get FEATURE property
08-30 03:40:03.129    90    90 E hwc-drm-plane: Could not get NAME property
08-30 03:40:03.129    90    90 E hwc-drm-plane: Could not get INPUT_WIDTH property
08-30 03:40:03.129    90    90 E hwc-drm-plane: Could not get INPUT_HEIGHT property
08-30 03:40:03.129    90    90 E hwc-drm-plane: Could not get OUTPUT_WIDTH property
08-30 03:40:03.129    90    90 E hwc-drm-plane: Could not get OUTPUT_HEIGHT property
08-30 03:40:03.129    90    90 E hwc-drm-plane: Could not get SCALE_RATE property
08-30 03:40:03.129    90    90 E hwc-drm-plane: Could not get ASYNC_COMMIT property
08-30 03:40:03.129    90    90 I hwc-drm-plane: Could not get eotf property
08-30 03:40:03.129    90    90 I hwc-drm-plane: Could not get colorspace property
08-30 03:40:03.129    90    90 E hwc-drm-plane: Could not get ZPOS property, try to get zpos property
08-30 03:40:03.129    90    90 E hwc-drm-plane: Could not get zpos property
08-30 03:40:03.129    90    90 E hwc-drm-plane: Could not get AREA_ID property
08-30 03:40:03.129    90    90 E hwc-drm-plane: Could not get SHARE_ID property
08-30 03:40:03.129    90    90 E hwc-drm-plane: Could not get FEATURE property
08-30 03:40:03.129    90    90 I hwc-drm-plane: Could not get alpha property
08-30 03:40:03.129    90    90 I hwc-drm-plane: Could not get pixel blend mode property
08-30 03:40:03.129    90    90 E hwc-drm-plane: Could not get FEATURE property
08-30 03:40:03.129    90    90 E hwc-drm-plane: Could not get NAME property
08-30 03:40:03.129    90    90 E hwc-drm-plane: Could not get INPUT_WIDTH property
08-30 03:40:03.129    90    90 E hwc-drm-plane: Could not get INPUT_HEIGHT property
08-30 03:40:03.129    90    90 E hwc-drm-plane: Could not get OUTPUT_WIDTH property
08-30 03:40:03.129    90    90 E hwc-drm-plane: Could not get OUTPUT_HEIGHT property
08-30 03:40:03.129    90    90 E hwc-drm-plane: Could not get SCALE_RATE property
08-30 03:40:03.129    90    90 E hwc-drm-plane: Could not get ASYNC_COMMIT property
08-30 03:40:03.129    90    90 E hwc-resource-manager: Open fb0 fail in Init
08-30 03:40:03.129    90    90 I hwc-resource-manager: Init,line=93 Create DrmDisplayCompositor crtc=58
08-30 03:40:03.129    90    90 I hwc-resource-manager: Init,line=93 Create DrmDisplayCompositor crtc=64
08-30 03:40:03.129    90    90 I hwc-resource-manager: Init,line=93 Create DrmDisplayCompositor crtc=70
08-30 03:40:03.129    90    90 I hwc-resource-manager: Init,line=93 Create DrmDisplayCompositor crtc=76
08-30 03:40:03.129    90    90 I hwc-resource-manager: Init,line=93 Create DrmDisplayCompositor crtc=82
08-30 03:40:03.129    90    90 I hwc-resource-manager: Init,line=93 Create DrmDisplayCompositor crtc=88
08-30 03:40:03.129    90    90 I hwc-resource-manager: Init,line=93 Create DrmDisplayCompositor crtc=94
08-30 03:40:03.129    90    90 I hwc-resource-manager: Init,line=93 Create DrmDisplayCompositor crtc=100
08-30 03:40:03.129    90    90 E hwc-drm-two: Init::CreateDisplay
08-30 03:40:03.129    90    90 E hwc-drm-two: CreateDisplay type=1
08-30 03:40:03.129   100   100 E APM::AudioPolicyEngine/Config: parse: Could not parse document /vendor/etc/audio_policy_engine_configuration.xml
08-30 03:40:03.129   100   100 W APM::AudioPolicyEngine/Base: loadAudioPolicyEngineConfig: No configuration found, using default matching phone experience.
08-30 03:40:03.130   100   100 E APM::AudioPolicyEngine/Config: parseLegacyVolumeFile: Could not parse document /odm/etc/audio_policy_configuration.xml
08-30 03:40:03.130    90    90 E hwc-drm-two: display-id=0
08-30 03:40:03.130    90    90 I hwc-drm-connector: UpdateDisplayMode,line=440, display=0 persist.vendor.resolution.Virtual-0=Unkonw
08-30 03:40:03.130    90    90 I hwc-drm-connector: UpdateDisplayMode,line=448, display=0 persist.vendor.resolution.main=Unkonw
08-30 03:40:03.130    90    90 I hwc-drm-connector: UpdateDisplayMode,line=534, Find best mode-id=1 : 1024x768p60.000000
08-30 03:40:03.130    90    90 E hwc-drm-two: ClearDisplay,line=333 init_success_=0 skip.
08-30 03:40:03.130    90    90 I hwc-drm-device: FindAvailableCrtcByFirst,line=1452 Find display-id=0 with conn[61] crtc=58 success!
08-30 03:40:03.130    90    90 I hwc-drm-device: BindConnectorAndCrtc,line=1640 current_mode id=1 , w=1024,h=768,fps=60.000000 
08-30 03:40:03.132    84    84 I JWAudioHAL: adev_open: audio_hw_if pid:84
08-30 03:40:03.132    84    84 I JWAudioHAL: audio_out: samplerate=44100 buf_size=4096
08-30 03:40:03.132    84    84 I JWAudioHAL: audio_in: samplerate=8000 buf_size=4096
08-30 03:40:03.132    84    84 W DeviceHAL: Error from HAL Device in function get_master_volume: Function not implemented
08-30 03:40:03.132    84    84 W DeviceHAL: Error from HAL Device in function get_master_mute: Function not implemented
08-30 03:40:03.133   100   100 I AudioFlinger: loadHwModule() Loaded primary audio interface, handle 10
08-30 03:40:03.133   100   100 I AudioFlinger: openOutput() this 0x73e85ce600, module 10 Device 0x2, SamplingRate 48000, Format 0x000001, Channels 0x3, flags 0x2
08-30 03:40:03.133   100   100 I AudioFlinger: HAL output buffer size 1024 frames, normal sink buffer size 1024 frames
08-30 03:40:03.134    84   140 I JWAudioHAL: connecter thread init pid:84, tid:140
08-30 03:40:03.134    84   140 I JWAudioHAL: connect to /data/misc/audioserver/audio_out success
08-30 03:40:03.134    84   141 I JWAudioHAL: recv thread init pid:84, tid:141
08-30 03:40:03.135    95    95 I JWSensorsHal: sensors : open sensors called and name: p
08-30 03:40:03.135    95    95 I JWSensorsHal: JWSensor Func Called and DEVICE_NAME:accelerometer
08-30 03:40:03.135    95    95 I JWSensorsHal: JWSensor Func Called and DEVICE_NAME:magnetic
08-30 03:40:03.135    95    95 I JWSensorsHal: JWSensor Func Called and DEVICE_NAME:compass
08-30 03:40:03.135    95    95 I JWSensorsHal: JWSensor Func Called and DEVICE_NAME:gravity
08-30 03:40:03.135    95    95 I JWSensorsHal: JWSensor Func Called and DEVICE_NAME:stepcounter
08-30 03:40:03.135    95    95 I JWSensorsHal: JWSensor Func Called and DEVICE_NAME:stepdetector
08-30 03:40:03.135    95    95 I JWSensorsHal: JWSensor Func Called and DEVICE_NAME:gyroscope
08-30 03:40:03.135    95    95 I JWSensorsHal: JWSensor Func Called and DEVICE_NAME:light
08-30 03:40:03.135    95    95 I JWSensorsHal: JWSensor Func Called and DEVICE_NAME:proximity
08-30 03:40:03.135    95    95 I JWSensorsHal: JWSensor Func Called and DEVICE_NAME:pressure
08-30 03:40:03.135    95    95 I JWSensorsHal: JWSensor Func Called and DEVICE_NAME:temperature
08-30 03:40:03.135   100   100 I BufferProvider: found effect "Multichannel Downmix To Stereo" from The Android Open Source Project
08-30 03:40:03.135    95   143 I JWSensorsHal: connecter thread init pid:95, tid:143
08-30 03:40:03.135    95   143 I JWSensorsHal: connect to /data/misc/sensor/sensor_ctrl success
08-30 03:40:03.135    95   143 V JWSensorsHal: sending type:0xfff40000 to /data/misc/sensor/sensor_ctrl
08-30 03:40:03.136   100   100 I AudioFlinger: Using module 10 as the primary audio interface
08-30 03:40:03.136    90    90 I hwc-drm-device: BindConnectorAndCrtc,line=1665 display-id=0 Bind Connector-id=61 Crtc-id=58 success!.
08-30 03:40:03.136    90    90 E hwc-drm-two: TryAssignPlane,line=168 display 1 crtc is NULL.
08-30 03:40:03.136    90    90 E hwc-drm-two: TryAssignPlane,line=168 display 2 crtc is NULL.
08-30 03:40:03.136    90    90 E hwc-drm-two: TryAssignPlane,line=168 display 3 crtc is NULL.
08-30 03:40:03.136    90    90 E hwc-drm-two: TryAssignPlane,line=168 display 4 crtc is NULL.
08-30 03:40:03.136    90    90 E hwc-drm-two: TryAssignPlane,line=168 display 5 crtc is NULL.
08-30 03:40:03.136    90    90 E hwc-drm-two: TryAssignPlane,line=168 display 6 crtc is NULL.
08-30 03:40:03.136    90    90 E hwc-drm-two: TryAssignPlane,line=168 display 7 crtc is NULL.
08-30 03:40:03.136    90    90 W hwc-drm-two: assignPlaneByHWC,line=56 Crtc PlaneMask not set, have to use HwcPlaneMask, please check Crtc::PlaneMask info.
08-30 03:40:03.136    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=58 mask=0x1 ,plane_mask=0xf03
08-30 03:40:03.136    90    90 E hwc-drm-two: assignPlaneByHWC,line=66 display=1 crtc is NULL.
08-30 03:40:03.136    90    90 E hwc-platform: TryAssignPlane,line=113 Failed provision stage with ret -1
08-30 03:40:03.136    90    90 W hwc-drm-device: BindDpyRes,line=1855 TryAssignPlane fail, ret = -1
08-30 03:40:03.136    90    90 E hwc-drm-two: Init,line=380 Failed to BindDpyRes for display=0 -1
08-30 03:40:03.136    90    90 E hwc-drm-two: Init::CreateDisplay
08-30 03:40:03.136    90    90 E hwc-drm-two: CreateDisplay type=1
08-30 03:40:03.136    90    90 E hwc-drm-two: display-id=1
08-30 03:40:03.136    90    90 I hwc-drm-connector: UpdateDisplayMode,line=440, display=1 persist.vendor.resolution.Virtual-0=Unkonw
08-30 03:40:03.136    90    90 I hwc-drm-connector: UpdateDisplayMode,line=448, display=1 persist.vendor.resolution.aux=Unkonw
08-30 03:40:03.136    90    90 I hwc-drm-connector: UpdateDisplayMode,line=534, Find best mode-id=83 : 1024x768p60.000000
08-30 03:40:03.136    90    90 E hwc-drm-two: ClearDisplay,line=333 init_success_=0 skip.
08-30 03:40:03.136    90    90 I hwc-drm-device: FindAvailableCrtcByFirst,line=1452 Find display-id=1 with conn[67] crtc=64 success!
08-30 03:40:03.136    87    87 I ServiceManagement: Registered android.hardware.drm@1.2::IDrmFactory/clearkey (start delay of 142ms)
08-30 03:40:03.136    87    87 I ServiceManagement: Removing namespace from process name android.hardware.drm@1.2-service.clearkey to drm@1.2-service.clearkey.
08-30 03:40:03.136    95    95 I ServiceManagement: Registered android.hardware.sensors@1.0::ISensors/default (start delay of 132ms)
08-30 03:40:03.136    95    95 I ServiceManagement: Removing namespace from process name android.hardware.sensors@1.0-service to sensors@1.0-service.
08-30 03:40:03.136    90    90 I hwc-drm-device: BindConnectorAndCrtc,line=1640 current_mode id=83 , w=1024,h=768,fps=60.000000 
08-30 03:40:03.136    95    95 I android.hardware.sensors@1.0-service: Registration complete for android.hardware.sensors@1.0::ISensors/default.
08-30 03:40:03.137    87    87 I ServiceManagement: Registered android.hardware.drm@1.2::ICryptoFactory/clearkey (start delay of 142ms)
08-30 03:40:03.137    87    87 I ServiceManagement: Removing namespace from process name android.hardware.drm@1.2-service.clearkey to drm@1.2-service.clearkey.
08-30 03:40:03.137   100   100 V APM_AudioPolicyManager: checkAndSetVolume cannot set volume group 3 volume with force use = 0 for comm
08-30 03:40:03.138    84    84 W DeviceHAL: Error from HAL Device in function set_voice_volume: Function not implemented
08-30 03:40:03.138   100   100 W AudioFlinger: moveEffects() bad srcOutput 0
08-30 03:40:03.138   100   100 V APM_AudioPolicyManager: selectOutputForMusicEffects selected output 13
08-30 03:40:03.138   100   100 V APM_AudioPolicyManager: setOutputDevices device {type:0x2,@:} delayMs 0
08-30 03:40:03.138   100   100 V APM_AudioPolicyManager: setOutputDevices() prevDevice {type:0x2,@:}
08-30 03:40:03.138   100   100 V APM_AudioPolicyManager: setOutputDevices changing device to {type:0x2,@:}
08-30 03:40:03.139   100   145 I AudioFlinger: AudioFlinger's thread 0x73e8674e00 tid=145 ready to run
08-30 03:40:03.139   100   145 W AudioFlinger: no wake lock to update, system not ready yet
08-30 03:40:03.139    95   144 I JWSensorsHal: recv thread init pid:95, tid:144
08-30 03:40:03.142    93    93 I ServiceManagement: Registered android.hardware.power@1.0::IPower/default (start delay of 138ms)
08-30 03:40:03.142    93    93 I ServiceManagement: Removing namespace from process name android.hardware.power@1.0-service to power@1.0-service.
08-30 03:40:03.143    93    93 I android.hardware.power@1.0-service: Registration complete for android.hardware.power@1.0::IPower/default.
08-30 03:40:03.147    79    79 D AndroidRuntime: >>>>>> START com.android.internal.os.ZygoteInit uid 0 <<<<<<
08-30 03:40:03.149    79    79 I AndroidRuntime: Using default boot image
08-30 03:40:03.149    79    79 I AndroidRuntime: Leaving lock profiling enabled
08-30 03:40:03.150    79    79 I zygote64: option[0]=-Xzygote
08-30 03:40:03.150    79    79 I zygote64: option[1]=exit
08-30 03:40:03.150    79    79 I zygote64: option[2]=vfprintf
08-30 03:40:03.150    79    79 I zygote64: option[3]=sensitiveThread
08-30 03:40:03.150    79    79 I zygote64: option[4]=-verbose:gc
08-30 03:40:03.150    79    79 I zygote64: option[5]=-Xms16m
08-30 03:40:03.150    79    79 I zygote64: option[6]=-Xmx512m
08-30 03:40:03.150    79    79 I zygote64: option[7]=-XX:HeapGrowthLimit=192m
08-30 03:40:03.150    79    79 I zygote64: option[8]=-XX:HeapMinFree=512k
08-30 03:40:03.150    79    79 I zygote64: option[9]=-XX:HeapMaxFree=8m
08-30 03:40:03.150    79    79 I zygote64: option[10]=-XX:HeapTargetUtilization=0.75
08-30 03:40:03.150    79    79 I zygote64: option[11]=-Xusejit:true
08-30 03:40:03.150    79    79 I zygote64: option[12]=-Xjitsaveprofilinginfo
08-30 03:40:03.150    79    79 I zygote64: option[13]=-XjdwpOptions:suspend=n,server=y
08-30 03:40:03.150    79    79 I zygote64: option[14]=-XjdwpProvider:default
08-30 03:40:03.150    79    79 I zygote64: option[15]=-Ximage-compiler-option
08-30 03:40:03.150    79    79 I zygote64: option[16]=--runtime-arg
08-30 03:40:03.150    79    79 I zygote64: option[17]=-Ximage-compiler-option
08-30 03:40:03.150    79    79 I zygote64: option[18]=-Xms64m
08-30 03:40:03.150    79    79 I zygote64: option[19]=-Ximage-compiler-option
08-30 03:40:03.150    79    79 I zygote64: option[20]=--runtime-arg
08-30 03:40:03.150    79    79 I zygote64: option[21]=-Ximage-compiler-option
08-30 03:40:03.150    79    79 I zygote64: option[22]=-Xmx64m
08-30 03:40:03.150    79    79 I zygote64: option[23]=-Ximage-compiler-option
08-30 03:40:03.150    79    79 I zygote64: option[24]=--profile-file=/system/etc/boot-image.prof
08-30 03:40:03.150    79    79 I zygote64: option[25]=-Ximage-compiler-option
08-30 03:40:03.150    79    79 I zygote64: option[26]=--compiler-filter=speed-profile
08-30 03:40:03.150    79    79 I zygote64: option[27]=-Xcompiler-option
08-30 03:40:03.150    79    79 I zygote64: option[28]=--runtime-arg
08-30 03:40:03.150    79    79 I zygote64: option[29]=-Xcompiler-option
08-30 03:40:03.150    79    79 I zygote64: option[30]=-Xms64m
08-30 03:40:03.150    79    79 I zygote64: option[31]=-Xcompiler-option
08-30 03:40:03.150    79    79 I zygote64: option[32]=--runtime-arg
08-30 03:40:03.150    79    79 I zygote64: option[33]=-Xcompiler-option
08-30 03:40:03.150    79    79 I zygote64: option[34]=-Xmx512m
08-30 03:40:03.150    79    79 I zygote64: option[35]=-Ximage-compiler-option
08-30 03:40:03.150    79    79 I zygote64: option[36]=--instruction-set-variant=cortex-a76
08-30 03:40:03.150    79    79 I zygote64: option[37]=-Xcompiler-option
08-30 03:40:03.150    79    79 I zygote64: option[38]=--instruction-set-variant=cortex-a76
08-30 03:40:03.150    79    79 I zygote64: option[39]=-Ximage-compiler-option
08-30 03:40:03.150    79    79 I zygote64: option[40]=--instruction-set-features=default
08-30 03:40:03.150    79    79 I zygote64: option[41]=-Xcompiler-option
08-30 03:40:03.150    79    79 I zygote64: option[42]=--instruction-set-features=default
08-30 03:40:03.150    79    79 I zygote64: option[43]=-Duser.locale=zh-CN
08-30 03:40:03.150    79    79 I zygote64: option[44]=--cpu-abilist=arm64-v8a
08-30 03:40:03.150    79    79 I zygote64: option[45]=-Xcompiler-option
08-30 03:40:03.150    79    79 I zygote64: option[46]=--generate-mini-debug-info
08-30 03:40:03.150    79    79 I zygote64: option[47]=-Xfingerprint:samsung/GT-P7500/GT-P7500:3.2/HTJ85B/XWKL1:user/release-keys
08-30 03:40:03.153    90    90 I hwc-drm-device: BindConnectorAndCrtc,line=1665 display-id=1 Bind Connector-id=67 Crtc-id=64 success!.
08-30 03:40:03.153    90    90 E hwc-drm-two: TryAssignPlane,line=168 display 2 crtc is NULL.
08-30 03:40:03.153    90    90 E hwc-drm-two: TryAssignPlane,line=168 display 3 crtc is NULL.
08-30 03:40:03.153    90    90 E hwc-drm-two: TryAssignPlane,line=168 display 4 crtc is NULL.
08-30 03:40:03.153    90    90 E hwc-drm-two: TryAssignPlane,line=168 display 5 crtc is NULL.
08-30 03:40:03.153    90    90 E hwc-drm-two: TryAssignPlane,line=168 display 6 crtc is NULL.
08-30 03:40:03.153    90    90 E hwc-drm-two: TryAssignPlane,line=168 display 7 crtc is NULL.
08-30 03:40:03.153    90    90 W hwc-drm-two: assignPlaneByHWC,line=56 Crtc PlaneMask not set, have to use HwcPlaneMask, please check Crtc::PlaneMask info.
08-30 03:40:03.153    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=58 mask=0x1 ,plane_mask=0xf03
08-30 03:40:03.153    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=64 mask=0x2 ,plane_mask=0xf00c
08-30 03:40:03.153    90    90 E hwc-drm-two: assignPlaneByHWC,line=66 display=2 crtc is NULL.
08-30 03:40:03.153    90    90 E hwc-platform: TryAssignPlane,line=113 Failed provision stage with ret -1
08-30 03:40:03.153    90    90 W hwc-drm-device: BindDpyRes,line=1855 TryAssignPlane fail, ret = -1
08-30 03:40:03.153    90    90 E hwc-drm-two: Init,line=380 Failed to BindDpyRes for display=1 -1
08-30 03:40:03.153    90    90 E hwc-drm-two: Init::CreateDisplay
08-30 03:40:03.153    90    90 E hwc-drm-two: CreateDisplay type=1
08-30 03:40:03.153    90    90 E hwc-drm-two: display-id=2
08-30 03:40:03.153    90    90 I hwc-drm-connector: UpdateDisplayMode,line=440, display=2 persist.vendor.resolution.Virtual-0=Unkonw
08-30 03:40:03.153    90    90 I hwc-drm-connector: UpdateDisplayMode,line=448, display=2 persist.vendor.resolution.aux=Unkonw
08-30 03:40:03.153    90    90 I hwc-drm-connector: UpdateDisplayMode,line=534, Find best mode-id=165 : 1024x768p60.000000
08-30 03:40:03.153    90    90 E hwc-drm-two: ClearDisplay,line=333 init_success_=0 skip.
08-30 03:40:03.153    90    90 I hwc-drm-device: FindAvailableCrtcByFirst,line=1452 Find display-id=2 with conn[73] crtc=70 success!
08-30 03:40:03.153    90    90 I hwc-drm-device: BindConnectorAndCrtc,line=1640 current_mode id=165 , w=1024,h=768,fps=60.000000 
08-30 03:40:03.170    90    90 I hwc-drm-device: BindConnectorAndCrtc,line=1665 display-id=2 Bind Connector-id=73 Crtc-id=70 success!.
08-30 03:40:03.170    90    90 E hwc-drm-two: TryAssignPlane,line=168 display 3 crtc is NULL.
08-30 03:40:03.170    90    90 E hwc-drm-two: TryAssignPlane,line=168 display 4 crtc is NULL.
08-30 03:40:03.170    90    90 E hwc-drm-two: TryAssignPlane,line=168 display 5 crtc is NULL.
08-30 03:40:03.170    90    90 E hwc-drm-two: TryAssignPlane,line=168 display 6 crtc is NULL.
08-30 03:40:03.170    90    90 E hwc-drm-two: TryAssignPlane,line=168 display 7 crtc is NULL.
08-30 03:40:03.170    90    90 W hwc-drm-two: assignPlaneByHWC,line=56 Crtc PlaneMask not set, have to use HwcPlaneMask, please check Crtc::PlaneMask info.
08-30 03:40:03.170    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=58 mask=0x1 ,plane_mask=0xf03
08-30 03:40:03.170    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=64 mask=0x2 ,plane_mask=0xf00c
08-30 03:40:03.170    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=70 mask=0x4 ,plane_mask=0xf0030
08-30 03:40:03.170    90    90 E hwc-drm-two: assignPlaneByHWC,line=66 display=3 crtc is NULL.
08-30 03:40:03.170    90    90 E hwc-platform: TryAssignPlane,line=113 Failed provision stage with ret -1
08-30 03:40:03.170    90    90 W hwc-drm-device: BindDpyRes,line=1855 TryAssignPlane fail, ret = -1
08-30 03:40:03.170    90    90 E hwc-drm-two: Init,line=380 Failed to BindDpyRes for display=2 -1
08-30 03:40:03.170    90    90 E hwc-drm-two: Init::CreateDisplay
08-30 03:40:03.170    90    90 E hwc-drm-two: CreateDisplay type=1
08-30 03:40:03.170    90    90 E hwc-drm-two: display-id=3
08-30 03:40:03.170    90    90 I hwc-drm-connector: UpdateDisplayMode,line=440, display=3 persist.vendor.resolution.Virtual-0=Unkonw
08-30 03:40:03.170    90    90 I hwc-drm-connector: UpdateDisplayMode,line=448, display=3 persist.vendor.resolution.aux=Unkonw
08-30 03:40:03.170    90    90 I hwc-drm-connector: UpdateDisplayMode,line=534, Find best mode-id=247 : 1024x768p60.000000
08-30 03:40:03.170    90    90 E hwc-drm-two: ClearDisplay,line=333 init_success_=0 skip.
08-30 03:40:03.170    90    90 I hwc-drm-device: FindAvailableCrtcByFirst,line=1452 Find display-id=3 with conn[79] crtc=76 success!
08-30 03:40:03.171    90    90 I hwc-drm-device: BindConnectorAndCrtc,line=1640 current_mode id=247 , w=1024,h=768,fps=60.000000 
08-30 03:40:03.184   100   145 W AudioFlinger: no wake lock to update, system not ready yet
08-30 03:40:03.185   100   100 V APM_AudioPolicyManager: setOutputDevices() AF::createAudioPatch returned 0 patchHandle 12 num_sources 1 num_sinks 1
08-30 03:40:03.185   100   100 V APM_AudioPolicyManager: checkAndSetVolume cannot set volume group 3 volume with force use = 0 for comm
08-30 03:40:03.187   100   156 I AudioFlinger: AudioFlinger's thread 0x73e8704240 tid=156 ready to run
08-30 03:40:03.187   100   156 W AudioFlinger: no wake lock to update, system not ready yet
08-30 03:40:03.187   100   156 W AudioFlinger: no wake lock to update, system not ready yet
08-30 03:40:03.187    90    90 I hwc-drm-device: BindConnectorAndCrtc,line=1665 display-id=3 Bind Connector-id=79 Crtc-id=76 success!.
08-30 03:40:03.187    90    90 E hwc-drm-two: TryAssignPlane,line=168 display 4 crtc is NULL.
08-30 03:40:03.187    90    90 E hwc-drm-two: TryAssignPlane,line=168 display 5 crtc is NULL.
08-30 03:40:03.187    90    90 E hwc-drm-two: TryAssignPlane,line=168 display 6 crtc is NULL.
08-30 03:40:03.187    90    90 E hwc-drm-two: TryAssignPlane,line=168 display 7 crtc is NULL.
08-30 03:40:03.187    90    90 W hwc-drm-two: assignPlaneByHWC,line=56 Crtc PlaneMask not set, have to use HwcPlaneMask, please check Crtc::PlaneMask info.
08-30 03:40:03.187    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=58 mask=0x1 ,plane_mask=0xf03
08-30 03:40:03.187    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=64 mask=0x2 ,plane_mask=0xf00c
08-30 03:40:03.187    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=70 mask=0x4 ,plane_mask=0xf0030
08-30 03:40:03.187    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=76 mask=0x8 ,plane_mask=0xf000c0
08-30 03:40:03.187    90    90 E hwc-drm-two: assignPlaneByHWC,line=66 display=4 crtc is NULL.
08-30 03:40:03.187    90    90 E hwc-platform: TryAssignPlane,line=113 Failed provision stage with ret -1
08-30 03:40:03.187    90    90 W hwc-drm-device: BindDpyRes,line=1855 TryAssignPlane fail, ret = -1
08-30 03:40:03.187    90    90 E hwc-drm-two: Init,line=380 Failed to BindDpyRes for display=3 -1
08-30 03:40:03.187    90    90 E hwc-drm-two: Init::CreateDisplay
08-30 03:40:03.187    90    90 E hwc-drm-two: CreateDisplay type=1
08-30 03:40:03.187    90    90 E hwc-drm-two: display-id=4
08-30 03:40:03.188    90    90 I hwc-drm-connector: UpdateDisplayMode,line=440, display=4 persist.vendor.resolution.Virtual-0=Unkonw
08-30 03:40:03.188    90    90 I hwc-drm-connector: UpdateDisplayMode,line=448, display=4 persist.vendor.resolution.aux=Unkonw
08-30 03:40:03.188    90    90 I hwc-drm-connector: UpdateDisplayMode,line=534, Find best mode-id=329 : 1024x768p60.000000
08-30 03:40:03.188    90    90 E hwc-drm-two: ClearDisplay,line=333 init_success_=0 skip.
08-30 03:40:03.188    90    90 I hwc-drm-device: FindAvailableCrtcByFirst,line=1452 Find display-id=4 with conn[85] crtc=82 success!
08-30 03:40:03.188    90    90 I hwc-drm-device: BindConnectorAndCrtc,line=1640 current_mode id=329 , w=1024,h=768,fps=60.000000 
08-30 03:40:03.189   100   100 I bt_a2dp_hw: adev_open:  adev_open in A2dp_hw module
08-30 03:40:03.190   100   100 I AudioFlinger: loadHwModule() Loaded a2dp audio interface, handle 18
08-30 03:40:03.190   100   100 E APM_AudioPolicyManager: initialize: Input device list is empty!
08-30 03:40:03.192    84    84 W DeviceHAL: Error from HAL Device in function set_master_volume: Function not implemented
08-30 03:40:03.192   100   100 I AudioFlinger: loadHwModule() Loaded usb audio interface, handle 26
08-30 03:40:03.192   100   100 E APM_AudioPolicyManager: initialize: Input device list is empty!
08-30 03:40:03.193    84    84 I r_submix: adev_open(name=audio_hw_if)
08-30 03:40:03.194    84    84 I r_submix: adev_init_check()
08-30 03:40:03.194    84    84 W DeviceHAL: Error from HAL Device in function set_master_volume: Function not implemented
08-30 03:40:03.195    84    84 W DeviceHAL: Error from HAL Device in function set_master_mute: Function not implemented
08-30 03:40:03.195   100   100 I AudioFlinger: loadHwModule() Loaded r_submix audio interface, handle 34
08-30 03:40:03.195    84    84 D r_submix: adev_open_input_stream(addr=0)
08-30 03:40:03.195    84    84 D r_submix: submix_audio_device_create_pipe_l(addr=0, idx=9)
08-30 03:40:03.195    84    84 D r_submix:   now using address 0 for route 9
08-30 03:40:03.195   100   161 I AudioFlinger: AudioFlinger's thread 0x735b02c500 tid=161 ready to run
08-30 03:40:03.195    84    84 I r_submix: in_standby()
08-30 03:40:03.195   100   161 W AudioFlinger: no wake lock to update, system not ready yet
08-30 03:40:03.195    84   118 I r_submix: in_standby()
08-30 03:40:03.196   100   161 W AudioFlinger: no wake lock to update, system not ready yet
08-30 03:40:03.197    84   118 D r_submix: adev_close_input_stream()
08-30 03:40:03.197    84   118 D r_submix: submix_audio_device_release_pipe_l(idx=9) addr=0
08-30 03:40:03.197    84   118 D r_submix: submix_audio_device_destroy_pipe_l(): pipe destroyed
08-30 03:40:03.197   100   100 I         : Waiting for activity service
08-30 03:40:03.198    80    80 D AndroidRuntime: >>>>>> START com.android.internal.os.ZygoteInit uid 0 <<<<<<
08-30 03:40:03.200    80    80 I AndroidRuntime: Using default boot image
08-30 03:40:03.200    80    80 I AndroidRuntime: Leaving lock profiling enabled
08-30 03:40:03.200    79    79 D ICU     : Time zone APEX file found: /apex/com.android.tzdata/etc/icu/icu_tzdata.dat
08-30 03:40:03.201    80    80 I zygote  : option[0]=-Xzygote
08-30 03:40:03.201    80    80 I zygote  : option[1]=exit
08-30 03:40:03.201    80    80 I zygote  : option[2]=vfprintf
08-30 03:40:03.201    80    80 I zygote  : option[3]=sensitiveThread
08-30 03:40:03.201    80    80 I zygote  : option[4]=-verbose:gc
08-30 03:40:03.201    80    80 I zygote  : option[5]=-Xms16m
08-30 03:40:03.201    80    80 I zygote  : option[6]=-Xmx512m
08-30 03:40:03.201    80    80 I zygote  : option[7]=-XX:HeapGrowthLimit=192m
08-30 03:40:03.201    80    80 I zygote  : option[8]=-XX:HeapMinFree=512k
08-30 03:40:03.201    80    80 I zygote  : option[9]=-XX:HeapMaxFree=8m
08-30 03:40:03.201    80    80 I zygote  : option[10]=-XX:HeapTargetUtilization=0.75
08-30 03:40:03.201    80    80 I zygote  : option[11]=-Xusejit:true
08-30 03:40:03.201    80    80 I zygote  : option[12]=-Xjitsaveprofilinginfo
08-30 03:40:03.201    80    80 I zygote  : option[13]=-XjdwpOptions:suspend=n,server=y
08-30 03:40:03.201    80    80 I zygote  : option[14]=-XjdwpProvider:default
08-30 03:40:03.201    80    80 I zygote  : option[15]=-Ximage-compiler-option
08-30 03:40:03.201    80    80 I zygote  : option[16]=--runtime-arg
08-30 03:40:03.201    80    80 I zygote  : option[17]=-Ximage-compiler-option
08-30 03:40:03.201    80    80 I zygote  : option[18]=-Xms64m
08-30 03:40:03.201    80    80 I zygote  : option[19]=-Ximage-compiler-option
08-30 03:40:03.201    80    80 I zygote  : option[20]=--runtime-arg
08-30 03:40:03.201    80    80 I zygote  : option[21]=-Ximage-compiler-option
08-30 03:40:03.201    80    80 I zygote  : option[22]=-Xmx64m
08-30 03:40:03.201    80    80 I zygote  : option[23]=-Ximage-compiler-option
08-30 03:40:03.201    80    80 I zygote  : option[24]=--profile-file=/system/etc/boot-image.prof
08-30 03:40:03.201    80    80 I zygote  : option[25]=-Ximage-compiler-option
08-30 03:40:03.201    80    80 I zygote  : option[26]=--compiler-filter=speed-profile
08-30 03:40:03.201    80    80 I zygote  : option[27]=-Xcompiler-option
08-30 03:40:03.201    80    80 I zygote  : option[28]=--runtime-arg
08-30 03:40:03.201    80    80 I zygote  : option[29]=-Xcompiler-option
08-30 03:40:03.201    80    80 I zygote  : option[30]=-Xms64m
08-30 03:40:03.201    80    80 I zygote  : option[31]=-Xcompiler-option
08-30 03:40:03.201    80    80 I zygote  : option[32]=--runtime-arg
08-30 03:40:03.201    80    80 I zygote  : option[33]=-Xcompiler-option
08-30 03:40:03.201    80    80 I zygote  : option[34]=-Xmx512m
08-30 03:40:03.201    80    80 I zygote  : option[35]=-Ximage-compiler-option
08-30 03:40:03.201    80    80 I zygote  : option[36]=--instruction-set-variant=cortex-a76
08-30 03:40:03.201    80    80 I zygote  : option[37]=-Xcompiler-option
08-30 03:40:03.201    80    80 I zygote  : option[38]=--instruction-set-variant=cortex-a76
08-30 03:40:03.201    80    80 I zygote  : option[39]=-Ximage-compiler-option
08-30 03:40:03.201    80    80 I zygote  : option[40]=--instruction-set-features=default
08-30 03:40:03.201    80    80 I zygote  : option[41]=-Xcompiler-option
08-30 03:40:03.201    80    80 I zygote  : option[42]=--instruction-set-features=default
08-30 03:40:03.201    80    80 I zygote  : option[43]=-Duser.locale=zh-CN
08-30 03:40:03.201    80    80 I zygote  : option[44]=--cpu-abilist=armeabi-v7a,armeabi
08-30 03:40:03.201    80    80 I zygote  : option[45]=-Xcompiler-option
08-30 03:40:03.201    80    80 I zygote  : option[46]=--generate-mini-debug-info
08-30 03:40:03.201    80    80 I zygote  : option[47]=-Xfingerprint:samsung/GT-P7500/GT-P7500:3.2/HTJ85B/XWKL1:user/release-keys
08-30 03:40:03.204    90    90 I hwc-drm-device: BindConnectorAndCrtc,line=1665 display-id=4 Bind Connector-id=85 Crtc-id=82 success!.
08-30 03:40:03.204    90    90 E hwc-drm-two: TryAssignPlane,line=168 display 5 crtc is NULL.
08-30 03:40:03.204    90    90 E hwc-drm-two: TryAssignPlane,line=168 display 6 crtc is NULL.
08-30 03:40:03.204    90    90 E hwc-drm-two: TryAssignPlane,line=168 display 7 crtc is NULL.
08-30 03:40:03.204    90    90 W hwc-drm-two: assignPlaneByHWC,line=56 Crtc PlaneMask not set, have to use HwcPlaneMask, please check Crtc::PlaneMask info.
08-30 03:40:03.204    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=58 mask=0x1 ,plane_mask=0xf03
08-30 03:40:03.204    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=64 mask=0x2 ,plane_mask=0xf00c
08-30 03:40:03.204    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=70 mask=0x4 ,plane_mask=0xf0030
08-30 03:40:03.204    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=76 mask=0x8 ,plane_mask=0xf000c0
08-30 03:40:03.204    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=82 mask=0x10 ,plane_mask=0x0
08-30 03:40:03.204    90    90 E hwc-drm-two: assignPlaneByHWC,line=66 display=5 crtc is NULL.
08-30 03:40:03.205    90    90 E hwc-platform: TryAssignPlane,line=113 Failed provision stage with ret -1
08-30 03:40:03.205    90    90 W hwc-drm-device: BindDpyRes,line=1855 TryAssignPlane fail, ret = -1
08-30 03:40:03.205    90    90 E hwc-drm-two: Init,line=380 Failed to BindDpyRes for display=4 -1
08-30 03:40:03.205    90    90 E hwc-drm-two: Init::CreateDisplay
08-30 03:40:03.205    90    90 E hwc-drm-two: CreateDisplay type=1
08-30 03:40:03.205    90    90 E hwc-drm-two: display-id=5
08-30 03:40:03.205    90    90 I hwc-drm-connector: UpdateDisplayMode,line=440, display=5 persist.vendor.resolution.Virtual-0=Unkonw
08-30 03:40:03.205    90    90 I hwc-drm-connector: UpdateDisplayMode,line=448, display=5 persist.vendor.resolution.aux=Unkonw
08-30 03:40:03.205    90    90 I hwc-drm-connector: UpdateDisplayMode,line=534, Find best mode-id=411 : 1024x768p60.000000
08-30 03:40:03.205    90    90 E hwc-drm-two: ClearDisplay,line=333 init_success_=0 skip.
08-30 03:40:03.205    90    90 I hwc-drm-device: FindAvailableCrtcByFirst,line=1452 Find display-id=5 with conn[91] crtc=88 success!
08-30 03:40:03.205    90    90 I hwc-drm-device: BindConnectorAndCrtc,line=1640 current_mode id=411 , w=1024,h=768,fps=60.000000 
08-30 03:40:03.214    79    79 W zygote64: JNI RegisterNativeMethods: attempt to register 0 native methods for android.media.AudioAttributes
08-30 03:40:03.216    79    79 W zygote64: Landroid/util/S9Helper; failed initialization: java.lang.InternalError: Cannot create threads in zygote
08-30 03:40:03.216    79    79 W zygote64:   at void java.lang.Thread.nativeCreate(java.lang.Thread, long, boolean) (Thread.java:-2)
08-30 03:40:03.216    79    79 W zygote64:   at void java.lang.Thread.start() (Thread.java:883)
08-30 03:40:03.216    79    79 W zygote64:   at java.lang.Object sun.nio.fs.AbstractPoller$1.run() (AbstractPoller.java:64)
08-30 03:40:03.216    79    79 W zygote64:   at java.lang.Object java.security.AccessController.doPrivileged(java.security.PrivilegedAction) (AccessController.java:43)
08-30 03:40:03.216    79    79 W zygote64:   at void sun.nio.fs.AbstractPoller.start() (AbstractPoller.java:59)
08-30 03:40:03.216    79    79 W zygote64:   at void sun.nio.fs.LinuxWatchService.<init>(sun.nio.fs.UnixFileSystem) (LinuxWatchService.java:83)
08-30 03:40:03.216    79    79 W zygote64:   at java.nio.file.WatchService sun.nio.fs.LinuxFileSystem.newWatchService() (LinuxFileSystem.java:47)
08-30 03:40:03.216    79    79 W zygote64:   at void android.util.S9Helper.<clinit>() (S9Helper.java:18)
08-30 03:40:03.216    79    79 W zygote64:   at java.lang.String android.os.SystemProperties.get(java.lang.String) (SystemProperties.java:114)
08-30 03:40:03.216    79    79 W zygote64:   at void com.android.internal.os.ZygoteInit.main(java.lang.String[]) (ZygoteInit.java:836)
08-30 03:40:03.216    79    79 W zygote64: 
08-30 03:40:03.216    79    79 E Zygote  : System zygote died with exception
08-30 03:40:03.216    79    79 E Zygote  : java.lang.InternalError: Cannot create threads in zygote
08-30 03:40:03.216    79    79 E Zygote  :      at java.lang.Thread.nativeCreate(Native Method)
08-30 03:40:03.216    79    79 E Zygote  :      at java.lang.Thread.start(Thread.java:883)
08-30 03:40:03.216    79    79 E Zygote  :      at sun.nio.fs.AbstractPoller$1.run(AbstractPoller.java:64)
08-30 03:40:03.216    79    79 E Zygote  :      at java.security.AccessController.doPrivileged(AccessController.java:43)
08-30 03:40:03.216    79    79 E Zygote  :      at sun.nio.fs.AbstractPoller.start(AbstractPoller.java:59)
08-30 03:40:03.216    79    79 E Zygote  :      at sun.nio.fs.LinuxWatchService.<init>(LinuxWatchService.java:83)
08-30 03:40:03.216    79    79 E Zygote  :      at sun.nio.fs.LinuxFileSystem.newWatchService(LinuxFileSystem.java:47)
08-30 03:40:03.216    79    79 E Zygote  :      at android.util.S9Helper.<clinit>(S9Helper.java:18)
08-30 03:40:03.216    79    79 E Zygote  :      at android.os.SystemProperties.get(SystemProperties.java:114)
08-30 03:40:03.216    79    79 E Zygote  :      at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:836)
08-30 03:40:03.216    79    79 D AndroidRuntime: Shutting down VM
08-30 03:40:03.217    44    44 I ServiceManager: Waiting for service 'SurfaceFlinger' on '/dev/binder'...
08-30 03:40:03.222    90    90 I hwc-drm-device: BindConnectorAndCrtc,line=1665 display-id=5 Bind Connector-id=91 Crtc-id=88 success!.
08-30 03:40:03.222    90    90 E hwc-drm-two: TryAssignPlane,line=168 display 6 crtc is NULL.
08-30 03:40:03.222    90    90 E hwc-drm-two: TryAssignPlane,line=168 display 7 crtc is NULL.
08-30 03:40:03.222    90    90 W hwc-drm-two: assignPlaneByHWC,line=56 Crtc PlaneMask not set, have to use HwcPlaneMask, please check Crtc::PlaneMask info.
08-30 03:40:03.222    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=58 mask=0x1 ,plane_mask=0xf03
08-30 03:40:03.222    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=64 mask=0x2 ,plane_mask=0xf00c
08-30 03:40:03.222    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=70 mask=0x4 ,plane_mask=0xf0030
08-30 03:40:03.222    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=76 mask=0x8 ,plane_mask=0xf000c0
08-30 03:40:03.222    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=82 mask=0x10 ,plane_mask=0x0
08-30 03:40:03.222    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=88 mask=0x20 ,plane_mask=0x0
08-30 03:40:03.222    90    90 E hwc-drm-two: assignPlaneByHWC,line=66 display=6 crtc is NULL.
08-30 03:40:03.222    90    90 E hwc-platform: TryAssignPlane,line=113 Failed provision stage with ret -1
08-30 03:40:03.222    90    90 W hwc-drm-device: BindDpyRes,line=1855 TryAssignPlane fail, ret = -1
08-30 03:40:03.222    90    90 E hwc-drm-two: Init,line=380 Failed to BindDpyRes for display=5 -1
08-30 03:40:03.222    90    90 E hwc-drm-two: Init::CreateDisplay
08-30 03:40:03.222    90    90 E hwc-drm-two: CreateDisplay type=1
08-30 03:40:03.222    90    90 E hwc-drm-two: display-id=6
08-30 03:40:03.222    90    90 I hwc-drm-connector: UpdateDisplayMode,line=440, display=6 persist.vendor.resolution.Virtual-0=Unkonw
08-30 03:40:03.222    90    90 I hwc-drm-connector: UpdateDisplayMode,line=448, display=6 persist.vendor.resolution.aux=Unkonw
08-30 03:40:03.222    90    90 I hwc-drm-connector: UpdateDisplayMode,line=534, Find best mode-id=493 : 1024x768p60.000000
08-30 03:40:03.222    90    90 E hwc-drm-two: ClearDisplay,line=333 init_success_=0 skip.
08-30 03:40:03.222    90    90 I hwc-drm-device: FindAvailableCrtcByFirst,line=1452 Find display-id=6 with conn[97] crtc=94 success!
08-30 03:40:03.222    90    90 I hwc-drm-device: BindConnectorAndCrtc,line=1640 current_mode id=493 , w=1024,h=768,fps=60.000000 
08-30 03:40:03.231    27    27 I ServiceManager: service 'media.audio_flinger' died
08-30 03:40:03.231    84    84 I r_submix: adev_close()
08-30 03:40:03.239    90    90 I hwc-drm-device: BindConnectorAndCrtc,line=1665 display-id=6 Bind Connector-id=97 Crtc-id=94 success!.
08-30 03:40:03.239    90    90 E hwc-drm-two: TryAssignPlane,line=168 display 7 crtc is NULL.
08-30 03:40:03.239    90    90 W hwc-drm-two: assignPlaneByHWC,line=56 Crtc PlaneMask not set, have to use HwcPlaneMask, please check Crtc::PlaneMask info.
08-30 03:40:03.239    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=58 mask=0x1 ,plane_mask=0xf03
08-30 03:40:03.239    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=64 mask=0x2 ,plane_mask=0xf00c
08-30 03:40:03.239    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=70 mask=0x4 ,plane_mask=0xf0030
08-30 03:40:03.239    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=76 mask=0x8 ,plane_mask=0xf000c0
08-30 03:40:03.239    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=82 mask=0x10 ,plane_mask=0x0
08-30 03:40:03.239    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=88 mask=0x20 ,plane_mask=0x0
08-30 03:40:03.239    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=94 mask=0x40 ,plane_mask=0x0
08-30 03:40:03.239    90    90 E hwc-drm-two: assignPlaneByHWC,line=66 display=7 crtc is NULL.
08-30 03:40:03.239    90    90 E hwc-platform: TryAssignPlane,line=113 Failed provision stage with ret -1
08-30 03:40:03.239    90    90 W hwc-drm-device: BindDpyRes,line=1855 TryAssignPlane fail, ret = -1
08-30 03:40:03.239    90    90 E hwc-drm-two: Init,line=380 Failed to BindDpyRes for display=6 -1
08-30 03:40:03.239    90    90 E hwc-drm-two: Init::CreateDisplay
08-30 03:40:03.239    90    90 E hwc-drm-two: CreateDisplay type=1
08-30 03:40:03.239    90    90 E hwc-drm-two: display-id=7
08-30 03:40:03.239    90    90 I hwc-drm-connector: UpdateDisplayMode,line=440, display=7 persist.vendor.resolution.Virtual-0=Unkonw
08-30 03:40:03.239    90    90 I hwc-drm-connector: UpdateDisplayMode,line=448, display=7 persist.vendor.resolution.aux=Unkonw
08-30 03:40:03.239    90    90 I hwc-drm-connector: UpdateDisplayMode,line=534, Find best mode-id=575 : 1024x768p60.000000
08-30 03:40:03.239    90    90 E hwc-drm-two: ClearDisplay,line=333 init_success_=0 skip.
08-30 03:40:03.239    90    90 I hwc-drm-device: FindAvailableCrtcByFirst,line=1452 Find display-id=7 with conn[103] crtc=100 success!
08-30 03:40:03.253   181   181 I wificond: wificond is starting up...
08-30 03:40:03.259    90    90 I hwc-drm-device: BindConnectorAndCrtc,line=1640 current_mode id=575 , w=1024,h=768,fps=60.000000 
08-30 03:40:03.276    90    90 I hwc-drm-device: BindConnectorAndCrtc,line=1665 display-id=7 Bind Connector-id=103 Crtc-id=100 success!.
08-30 03:40:03.276    90    90 W hwc-drm-two: assignPlaneByHWC,line=56 Crtc PlaneMask not set, have to use HwcPlaneMask, please check Crtc::PlaneMask info.
08-30 03:40:03.276    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=58 mask=0x1 ,plane_mask=0xf03
08-30 03:40:03.276    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=64 mask=0x2 ,plane_mask=0xf00c
08-30 03:40:03.276    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=70 mask=0x4 ,plane_mask=0xf0030
08-30 03:40:03.276    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=76 mask=0x8 ,plane_mask=0xf000c0
08-30 03:40:03.276    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=82 mask=0x10 ,plane_mask=0x0
08-30 03:40:03.276    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=88 mask=0x20 ,plane_mask=0x0
08-30 03:40:03.276    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=94 mask=0x40 ,plane_mask=0x0
08-30 03:40:03.276    90    90 I hwc-drm-two: assignPlaneByHWC,line=90, crtc-id=100 mask=0x80 ,plane_mask=0x0
08-30 03:40:03.276    90    90 I hwc-drm-two: assignPlaneByHWC,line=101, name=(null) cur_crtcs_mask=0x1
08-30 03:40:03.276    90    90 I hwc-drm-device: UpdateDisplayGamma,line=1161 Virtual crtc-id=100 not support gamma.
08-30 03:40:03.276    90    90 I hwc-drm-device: UpdateDisplay3DLut,line=1208 Virtual crtc-id=100 not support cubic lut.
08-30 03:40:03.286    90    90 I hwc-drm-connector: GetFramebufferInfo,line=853, display=7 persist.vendor.framebuffer.Virtual-0=Unkonw
08-30 03:40:03.286    90    90 I hwc-drm-connector: GetFramebufferInfo,line=861, display=7 persist.vendor.framebuffer.aux=Unkonw
08-30 03:40:03.286    90    90 E hwc-drm-two: hello30:0:0
08-30 03:40:03.314   209   209 I /system/bin/tombstoned: tombstoned successfully initialized
08-30 03:40:03.317    44    44 I ServiceManager: Waiting for service 'SurfaceFlinger' on '/dev/binder'...
08-30 03:40:03.328   201   201 I ServiceManagement: Registered android.frameworks.stats@1.0::IStats/default (start delay of 44ms)
08-30 03:40:03.329   201   201 W statsd  : statscompanion service unavailable!
08-30 03:40:03.329   201   201 I statsd  : Statsd starts to listen to socket.
08-30 03:40:03.339   206   206 I ServiceManagement: Registered android.hardware.radio@1.1::IRadio/slot1 (start delay of 54ms)
08-30 03:40:03.339   206   206 I ServiceManagement: Registered android.hardware.radio.deprecated@1.0::IOemHook/slot1 (start delay of 55ms)
08-30 03:40:03.345   188   188 D LibBpfLoader: Loading ELF object /system/etc/bpf/netd.o with license Apache 2.0
08-30 03:40:03.345   188   188 D LibBpfLoader: Loaded code section 3 (cgroupskb_ingress_stats)
08-30 03:40:03.345   188   188 D LibBpfLoader: Loaded relo section 3 (.relcgroupskb/ingress/stats)
08-30 03:40:03.345   188   188 D LibBpfLoader: Adding section 3 to cs list
08-30 03:40:03.345   188   188 D LibBpfLoader: Loaded code section 5 (cgroupskb_egress_stats)
08-30 03:40:03.345   188   188 D LibBpfLoader: Loaded relo section 5 (.relcgroupskb/egress/stats)
08-30 03:40:03.345   188   188 D LibBpfLoader: Adding section 5 to cs list
08-30 03:40:03.345   188   188 D LibBpfLoader: Loaded code section 7 (skfilter_egress_xtbpf)
08-30 03:40:03.345   188   188 D LibBpfLoader: Loaded relo section 7 (.relskfilter/egress/xtbpf)
08-30 03:40:03.345   188   188 D LibBpfLoader: Adding section 7 to cs list
08-30 03:40:03.345   188   188 D LibBpfLoader: Loaded code section 9 (skfilter_ingress_xtbpf)
08-30 03:40:03.345   188   188 D LibBpfLoader: Loaded relo section 9 (.relskfilter/ingress/xtbpf)
08-30 03:40:03.345   188   188 D LibBpfLoader: Adding section 9 to cs list
08-30 03:40:03.345   188   188 D LibBpfLoader: Loaded code section 11 (skfilter_whitelist_xtbpf)
08-30 03:40:03.345   188   188 D LibBpfLoader: Loaded relo section 11 (.relskfilter/whitelist/xtbpf)
08-30 03:40:03.345   188   188 D LibBpfLoader: Adding section 11 to cs list
08-30 03:40:03.345   188   188 D LibBpfLoader: Loaded code section 13 (skfilter_blacklist_xtbpf)
08-30 03:40:03.345   188   188 D LibBpfLoader: Loaded relo section 13 (.relskfilter/blacklist/xtbpf)
08-30 03:40:03.345   188   188 D LibBpfLoader: Adding section 13 to cs list
08-30 03:40:03.345   188   188 D LibBpfLoader: Loaded code section 15 (cgroupsock_inet_create)
08-30 03:40:03.345   188   188 D LibBpfLoader: Loaded relo section 15 (.relcgroupsock/inet/create)
08-30 03:40:03.345   188   188 D LibBpfLoader: Adding section 15 to cs list
08-30 03:40:03.346   188   188 D LibBpfLoader: bpf_create_map name cookie_tag_map, ret: 6
08-30 03:40:03.346   188   188 D LibBpfLoader: bpf_create_map name uid_counterset_map, ret: 7
08-30 03:40:03.347   188   188 D LibBpfLoader: bpf_create_map name app_uid_stats_map, ret: 8
08-30 03:40:03.347   188   188 D LibBpfLoader: bpf_create_map name stats_map_A, ret: 9
08-30 03:40:03.347   188   188 D LibBpfLoader: bpf_create_map name stats_map_B, ret: 10
08-30 03:40:03.347   188   188 D LibBpfLoader: bpf_create_map name iface_stats_map, ret: 11
08-30 03:40:03.347   188   188 D LibBpfLoader: bpf_create_map name configuration_map, ret: 12
08-30 03:40:03.347   188   188 D LibBpfLoader: bpf_create_map name uid_owner_map, ret: 13
08-30 03:40:03.349   188   188 D LibBpfLoader: bpf_create_map name iface_index_name_map, ret: 14
08-30 03:40:03.349   188   188 D LibBpfLoader: bpf_create_map name uid_permission_map, ret: 15
08-30 03:40:03.349   188   188 D LibBpfLoader: map_fd found at 0 is 6 in /system/etc/bpf/netd.o
08-30 03:40:03.349   188   188 D LibBpfLoader: map_fd found at 1 is 7 in /system/etc/bpf/netd.o
08-30 03:40:03.349   188   188 D LibBpfLoader: map_fd found at 2 is 8 in /system/etc/bpf/netd.o
08-30 03:40:03.349   188   188 D LibBpfLoader: map_fd found at 3 is 9 in /system/etc/bpf/netd.o
08-30 03:40:03.349   188   188 D LibBpfLoader: map_fd found at 4 is 10 in /system/etc/bpf/netd.o
08-30 03:40:03.349   188   188 D LibBpfLoader: map_fd found at 5 is 11 in /system/etc/bpf/netd.o
08-30 03:40:03.349   188   188 D LibBpfLoader: map_fd found at 6 is 12 in /system/etc/bpf/netd.o
08-30 03:40:03.349   188   188 D LibBpfLoader: map_fd found at 7 is 13 in /system/etc/bpf/netd.o
08-30 03:40:03.349   188   188 D LibBpfLoader: map_fd found at 8 is 14 in /system/etc/bpf/netd.o
08-30 03:40:03.349   188   188 D LibBpfLoader: map_fd found at 9 is 15 in /system/etc/bpf/netd.o
08-30 03:40:03.349   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 616,               insn offset 77 , insn 118
08-30 03:40:03.349   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 688,               insn offset 86 , insn 118
08-30 03:40:03.349   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 1040,              insn offset 130 , insn 118
08-30 03:40:03.349   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 1184,              insn offset 148 , insn 118
08-30 03:40:03.349   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 1264,              insn offset 158 , insn 118
08-30 03:40:03.349   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 1368,              insn offset 171 , insn 118
08-30 03:40:03.349   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 1472,              insn offset 184 , insn 118
08-30 03:40:03.349   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 1512,              insn offset 189 , insn 118
08-30 03:40:03.349   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 1576,              insn offset 197 , insn 118
08-30 03:40:03.349   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 1680,              insn offset 210 , insn 118
08-30 03:40:03.349   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 1720,              insn offset 215 , insn 118
08-30 03:40:03.349   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 1848,              insn offset 231 , insn 118
08-30 03:40:03.349   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 1952,              insn offset 244 , insn 118
08-30 03:40:03.349   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 1992,              insn offset 249 , insn 118
08-30 03:40:03.349   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 2056,              insn offset 257 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 2160,              insn offset 270 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 2200,              insn offset 275 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 2288,              insn offset 286 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 2392,              insn offset 299 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 2432,              insn offset 304 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 608,               insn offset 76 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 680,               insn offset 85 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 904,               insn offset 113 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 1048,              insn offset 131 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 1128,              insn offset 141 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 1232,              insn offset 154 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 1336,              insn offset 167 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 1376,              insn offset 172 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 1440,              insn offset 180 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 1544,              insn offset 193 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 1584,              insn offset 198 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 1712,              insn offset 214 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 1816,              insn offset 227 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 1856,              insn offset 232 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 1920,              insn offset 240 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 2024,              insn offset 253 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 2064,              insn offset 258 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 2152,              insn offset 269 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 2256,              insn offset 282 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 2296,              insn offset 287 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 40,                insn offset 5 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 144,               insn offset 18 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 184,               insn offset 23 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 40,                insn offset 5 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 144,               insn offset 18 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 184,               insn offset 23 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 136,               insn offset 17 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 32,                insn offset 4 , insn 118
08-30 03:40:03.350   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 80,                insn offset 10 , insn 118
08-30 03:40:03.353   188   188 D LibBpfLoader: New bpf core prog_load for /system/etc/bpf/netd.o (cgroupskb_ingress_stats) returned: 16
08-30 03:40:03.353   188   188 D LibBpfLoader: New bpf core prog_load for /system/etc/bpf/netd.o (cgroupskb_egress_stats) returned: 17
08-30 03:40:03.353   188   188 D LibBpfLoader: New bpf core prog_load for /system/etc/bpf/netd.o (skfilter_egress_xtbpf) returned: 18
08-30 03:40:03.353   188   188 D LibBpfLoader: New bpf core prog_load for /system/etc/bpf/netd.o (skfilter_ingress_xtbpf) returned: 19
08-30 03:40:03.354   188   188 D LibBpfLoader: New bpf core prog_load for /system/etc/bpf/netd.o (skfilter_whitelist_xtbpf) returned: 20
08-30 03:40:03.354   188   188 D LibBpfLoader: New bpf core prog_load for /system/etc/bpf/netd.o (skfilter_blacklist_xtbpf) returned: 21
08-30 03:40:03.354   188   188 D LibBpfLoader: New bpf core prog_load for /system/etc/bpf/netd.o (cgroupsock_inet_create) returned: 22
08-30 03:40:03.354   188   188 I bpfloader: Attempted load object: /system/etc/bpf/netd.o, ret: Success
08-30 03:40:03.354   188   188 D LibBpfLoader: Loading ELF object /system/etc/bpf/clatd.o with license Apache 2.0
08-30 03:40:03.354   188   188 D LibBpfLoader: Loaded code section 3 (schedcls_ingress_clat_ether)
08-30 03:40:03.354   188   188 D LibBpfLoader: Loaded relo section 3 (.relschedcls/ingress/clat_ether)
08-30 03:40:03.354   188   188 D LibBpfLoader: Adding section 3 to cs list
08-30 03:40:03.354   188   188 D LibBpfLoader: Loaded code section 5 (schedcls_ingress_clat_rawip)
08-30 03:40:03.354   188   188 D LibBpfLoader: Loaded relo section 5 (.relschedcls/ingress/clat_rawip)
08-30 03:40:03.354   188   188 D LibBpfLoader: Adding section 5 to cs list
08-30 03:40:03.354   188   188 D LibBpfLoader: bpf_create_map name clat_ingress_map, ret: 23
08-30 03:40:03.354   188   188 D LibBpfLoader: map_fd found at 0 is 23 in /system/etc/bpf/clatd.o
08-30 03:40:03.355    90    90 I ServiceManagement: Registered android.hardware.graphics.composer@2.1::IComposer/default (start delay of 350ms)
08-30 03:40:03.355    90    90 I ServiceManagement: Removing namespace from process name android.hardware.graphics.composer@2.1-service to composer@2.1-service.
08-30 03:40:03.356    90    90 I android.hardware.graphics.composer@2.1-service: Registration complete for android.hardware.graphics.composer@2.1::IComposer/default.
08-30 03:40:03.358   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 400,               insn offset 50 , insn 118
08-30 03:40:03.358   188   188 D LibBpfLoader: applying relo to instruction at byte offset: 360,               insn offset 45 , insn 118
08-30 03:40:03.358   188   188 D LibBpfLoader: New bpf core prog_load for /system/etc/bpf/clatd.o (schedcls_ingress_clat_ether) returned: 24
08-30 03:40:03.358   188   188 D LibBpfLoader: New bpf core prog_load for /system/etc/bpf/clatd.o (schedcls_ingress_clat_rawip) returned: 25
08-30 03:40:03.364   188   188 I bpfloader: Attempted load object: /system/etc/bpf/clatd.o, ret: Success
08-30 03:40:03.371    90    90 I hwc-drm-two: GetMaxVirtualDisplayCount,line=238 
08-30 03:40:03.371    43    43 I HWComposer: Switching to legacy multi-display mode
08-30 03:40:03.372    90    90 I hwc-drm-connector: GetFramebufferInfo,line=853, display=0 persist.vendor.framebuffer.Virtual-0=Unkonw
08-30 03:40:03.372    90    90 I hwc-drm-connector: GetFramebufferInfo,line=861, display=0 persist.vendor.framebuffer.main=720x1280@60
08-30 03:40:03.372    90    90 E hwc-drm-two: hello30:720:1280
08-30 03:40:03.372    90    90 I hwc-drm-connector: GetFramebufferInfo,line=853, display=0 persist.vendor.framebuffer.Virtual-0=Unkonw
08-30 03:40:03.372    90    90 I hwc-drm-connector: GetFramebufferInfo,line=861, display=0 persist.vendor.framebuffer.main=720x1280@60
08-30 03:40:03.372    90    90 E hwc-drm-two: hello30:720:1280
08-30 03:40:03.372    43    43 E DispSync: Couldn't set SCHED_FIFO for DispSyncThread
08-30 03:40:03.372    43    43 E SurfaceFlinger: Couldn't set SCHED_FIFO for EventThread
08-30 03:40:03.372    43    43 E SurfaceFlinger: Couldn't set SCHED_FIFO for EventThread
08-30 03:40:03.373    43    43 D FramebufferSurface: Creating for display 0
08-30 03:40:03.373    43   227 W SurfaceFlinger: Ignoring VSYNC request while display is disconnected
08-30 03:40:03.374    43   228 W SurfaceFlinger: Ignoring VSYNC request while display is disconnected
08-30 03:40:03.378   208   208 I gatekeeperd: Starting gatekeeperd...
08-30 03:40:03.379    28    28 I hwservicemanager: getTransport: Cannot find entry android.hardware.gatekeeper@1.0::IGatekeeper/default in either framework or device manifest.
08-30 03:40:03.386   208   208 W gatekeeperd: falling back to software GateKeeper
08-30 03:40:03.386   204   204 I media.codec: mediacodecservice starting
08-30 03:40:03.387   204   204 W media.codec: libminijail[204]: failed to get path of fd 4: No such file or directory
08-30 03:40:03.387   204   204 W media.codec: libminijail[204]: allowing syscall: clock_gettime
08-30 03:40:03.387   204   204 W media.codec: libminijail[204]: allowing syscall: connect
08-30 03:40:03.387   204   204 W media.codec: libminijail[204]: allowing syscall: fcntl64
08-30 03:40:03.387   204   204 W media.codec: libminijail[204]: allowing syscall: socket
08-30 03:40:03.387   204   204 W media.codec: libminijail[204]: allowing syscall: writev
08-30 03:40:03.387   204   204 W media.codec: libminijail[204]: logging seccomp filter failures
08-30 03:40:03.388    89    89 E ion     : ioctl c0044901 failed with code -1: Not a typewriter
08-30 03:40:03.389    90    90 I hwc-drm-two: HWC2 Init: SF register connector 67 type=Virtual, type_id=2 
08-30 03:40:03.389    90    90 I hwc-drm-connector: GetFramebufferInfo,line=853, display=1 persist.vendor.framebuffer.Virtual-0=Unkonw
08-30 03:40:03.389    90    90 I hwc-drm-connector: GetFramebufferInfo,line=861, display=1 persist.vendor.framebuffer.aux=Unkonw
08-30 03:40:03.389    90    90 E hwc-drm-two: hello30:0:0
08-30 03:40:03.389    90    90 I hwc-drm-connector: GetFramebufferInfo,line=853, display=1 persist.vendor.framebuffer.Virtual-0=Unkonw
08-30 03:40:03.389    90    90 I hwc-drm-connector: GetFramebufferInfo,line=861, display=1 persist.vendor.framebuffer.aux=Unkonw
08-30 03:40:03.389    90    90 E hwc-drm-two: hello30:0:0
08-30 03:40:03.390    43    43 D FramebufferSurface: Creating for display 1
08-30 03:40:03.390   204   204 E omx_comp_regs: Rockchip_OMX_Component_Register(59): in
08-30 03:40:03.390   204   204 E omx_comp_regs: Rockchip_OMX_Component_Register(73): in
08-30 03:40:03.391    90    90 I hwc-drm-two: HWC2 Init: SF register connector 73 type=Virtual, type_id=3 
08-30 03:40:03.391   204   204 I vpu_api : dlopen vpu lib /vendor/lib/librk_vpuapi.so success
08-30 03:40:03.391   204   204 E omx_comp_regs: Rockchip_OMX_Component_Register(75): in so name: libomxvpu_dec.so
08-30 03:40:03.391   204   204 E omx_comp_regs: Rockchip_OMX_Component_Register(81): in num: 12
08-30 03:40:03.392   204   204 E omx_log : Rockchip_OMX_COMPONENT_Library_Register(50): in
08-30 03:40:03.392   204   204 I chatty  : uid=1046(mediacodec) omx@1.0-service identical 10 lines
08-30 03:40:03.392   204   204 E omx_log : Rockchip_OMX_COMPONENT_Library_Register(50): in
08-30 03:40:03.392   204   204 E omx_comp_regs: Rockchip_OMX_Component_Register(110): Rockchip_OSAL_dlerror: (null)
08-30 03:40:03.392   204   204 E omx_comp_regs: Rockchip_OMX_Component_Register(73): in
08-30 03:40:03.392    43    43 E HWComposer: Ignoring connection of tertiary display 2
08-30 03:40:03.392    90    90 I hwc-drm-two: HWC2 Init: SF register connector 79 type=Virtual, type_id=4 
08-30 03:40:03.392    43    43 E HWComposer: Ignoring connection of tertiary display 3
08-30 03:40:03.392    90    90 I hwc-drm-two: HWC2 Init: SF register connector 85 type=Virtual, type_id=5 
08-30 03:40:03.392    43    43 E HWComposer: Ignoring connection of tertiary display 4
08-30 03:40:03.392    90    90 I hwc-drm-two: HWC2 Init: SF register connector 91 type=Virtual, type_id=6 
08-30 03:40:03.392    43    43 E HWComposer: Ignoring connection of tertiary display 5
08-30 03:40:03.392    90    90 I hwc-drm-two: HWC2 Init: SF register connector 97 type=Virtual, type_id=7 
08-30 03:40:03.392    43    43 E HWComposer: Ignoring connection of tertiary display 6
08-30 03:40:03.392   204   204 E omx_comp_regs: Rockchip_OMX_Component_Register(75): in so name: libomxvpu_enc.so
08-30 03:40:03.392   204   204 E omx_comp_regs: Rockchip_OMX_Component_Register(81): in num: 3
08-30 03:40:03.392   204   204 E omx_comp_regs: Rockchip_OMX_Component_Register(110): Rockchip_OSAL_dlerror: (null)
08-30 03:40:03.392   204   204 I libstagefrighthw: OMX IL core libOMX_Core.so: declares component OMX.rk.video_decoder.avc
08-30 03:40:03.392   204   204 I libstagefrighthw: OMX IL core libOMX_Core.so: declares component OMX.rk.video_decoder.m4v
08-30 03:40:03.392   204   204 I libstagefrighthw: OMX IL core libOMX_Core.so: declares component OMX.rk.video_decoder.h263
08-30 03:40:03.392   204   204 I libstagefrighthw: OMX IL core libOMX_Core.so: declares component OMX.rk.video_decoder.flv1
08-30 03:40:03.392   204   204 I libstagefrighthw: OMX IL core libOMX_Core.so: declares component OMX.rk.video_decoder.m2v
08-30 03:40:03.392   204   204 I libstagefrighthw: OMX IL core libOMX_Core.so: declares component OMX.rk.video_decoder.vp8
08-30 03:40:03.392   204   204 I libstagefrighthw: OMX IL core libOMX_Core.so: declares component OMX.rk.video_decoder.vp9
08-30 03:40:03.392   204   204 I libstagefrighthw: OMX IL core libOMX_Core.so: declares component OMX.rk.video_decoder.vc1
08-30 03:40:03.392   204   204 I libstagefrighthw: OMX IL core libOMX_Core.so: declares component OMX.rk.video_decoder.wmv3
08-30 03:40:03.392   204   204 I libstagefrighthw: OMX IL core libOMX_Core.so: declares component OMX.rk.video_decoder.hevc
08-30 03:40:03.392   204   204 I libstagefrighthw: OMX IL core libOMX_Core.so: declares component OMX.rk.video_decoder.mjpeg
08-30 03:40:03.392   204   204 I libstagefrighthw: OMX IL core libOMX_Core.so: declares component OMX.rk.video_decoder.av1
08-30 03:40:03.392   204   204 I libstagefrighthw: OMX IL core libOMX_Core.so: declares component OMX.rk.video_encoder.avc
08-30 03:40:03.392   204   204 I libstagefrighthw: OMX IL core libOMX_Core.so: declares component OMX.rk.video_encoder.hevc
08-30 03:40:03.392   204   204 I libstagefrighthw: OMX IL core libOMX_Core.so: declares component OMX.rk.video_encoder.vp8
08-30 03:40:03.392   204   204 I libstagefrighthw: OMX IL core libOMX_Core.so: contains 15 components
08-30 03:40:03.393   204   204 I SoftOMXPlugin: createOMXPlugin
08-30 03:40:03.393    90    90 I hwc-drm-two: HWC2 Init: SF register connector 103 type=Virtual, type_id=8 
08-30 03:40:03.393    43    43 E HWComposer: Ignoring connection of tertiary display 7
08-30 03:40:03.393   204   204 D MediaCodecsXmlParser: parsing /vendor/etc/media_codecs.xml...
08-30 03:40:03.393   204   204 D MediaCodecsXmlParser: parsing /vendor/etc/media_codecs_google_audio.xml...
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: max-channel-count = 2
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: sample-rate-ranges = 8000,11025,12000,16000,22050,24000,32000,44100,48000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 8000-320000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: max-channel-count = 1
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: sample-rate-ranges = 8000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 4750-12200
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: max-channel-count = 1
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: sample-rate-ranges = 16000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 6600-23850
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: max-channel-count = 8
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: sample-rate-ranges = 7350,8000,11025,12000,16000,22050,24000,32000,44100,48000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 8000-960000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: max-channel-count = 1
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: sample-rate-ranges = 8000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 64000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: max-channel-count = 1
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: sample-rate-ranges = 8000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 64000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: max-channel-count = 8
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: sample-rate-ranges = 8000-96000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 32000-500000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: max-channel-count = 8
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: sample-rate-ranges = 48000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 6000-510000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: max-channel-count = 8
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: sample-rate-ranges = 8000-96000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-10000000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: max-channel-count = 8
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: sample-rate-ranges = 8000-96000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-10000000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: max-channel-count = 6
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: sample-rate-ranges = 8000,11025,12000,16000,22050,24000,32000,44100,48000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 8000-960000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: max-channel-count = 1
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: sample-rate-ranges = 8000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 4750-12200
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: feature-bitrate-modes = CBR
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: max-channel-count = 1
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: sample-rate-ranges = 16000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 6600-23850
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: feature-bitrate-modes = CBR
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: max-channel-count = 2
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: sample-rate-ranges = 1-655350
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-21000000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: complexity-default = 5
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: complexity-range = 0-8
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: feature-bitrate-modes = CQ
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: size-range = 96x96-4096x2160
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: alignment = 4x4
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: block-size = 16x16
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: blocks-per-second-range = 1-489600
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-10000000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: feature-adaptive-playback = 0
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: max-concurrent-instances = 6
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: performance-point-3840x2160-range = 60-60
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: size-range = 176x144-1920x1088
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: alignment = 8x8
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: block-size = 16x16
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: blocks-per-second-range = 1-244800
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-10000000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: feature-adaptive-playback = 0
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: max-concurrent-instances = 6
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: performance-point-1920x1088-range = 60-60
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: size-range = 176x144-1920x1088
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: alignment = 8x8
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: block-size = 16x16
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: blocks-per-second-range = 1-244800
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-10000000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: feature-adaptive-playback = 0
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: max-concurrent-instances = 6
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: performance-point-1920x1088-range = 60-60
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: size-range = 176x144-1920x1088
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: alignment = 8x8
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: block-size = 16x16
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: blocks-per-second-range = 1-244800
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-10000000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: feature-adaptive-playback = 0
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: max-concurrent-instances = 6
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: performance-point-1920x1088-range = 60-60
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: size-range = 176x144-1920x1088
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: alignment = 8x8
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: block-size = 16x16
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: blocks-per-second-range = 1-244800
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-10000000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: feature-adaptive-playback = 0
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: max-concurrent-instances = 6
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: performance-point-1920x1088-range = 60-60
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: size-range = 176x144-1920x1088
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: alignment = 8x8
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: block-size = 16x16
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: blocks-per-second-range = 1-244800
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-10000000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: feature-adaptive-playback = 0
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: max-concurrent-instances = 6
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: performance-point-1920x1088-range = 60-60
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: size-range = 400x400-4096x2160
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: alignment = 2x2
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: block-size = 16x16
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: blocks-per-second-range = 1-244800
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-10000000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: feature-adaptive-playback = 0
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: max-concurrent-instances = 6
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: performance-point-3840x2160-range = 60-60
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: size-range = 176x144-1920x1088
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: alignment = 16x8
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-10000000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: feature-bitrate-modes = VBR,CBR
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: max-concurrent-instances = 4
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: performance-point-1920x1088-range = 60-60
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: size-range = 176x144-1920x1088
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: alignment = 16x8
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-10000000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: feature-bitrate-modes = VBR,CBR
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: max-concurrent-instances = 4
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: performance-point-1920x1088-range = 60-60
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: size-range = 176x144-1920x1088
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: alignment = 16x8
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-10000000
08-30 03:40:03.393   204   204 I MediaCodecsXmlParser: limit: feature-bitrate-modes = VBR,CBR
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: max-concurrent-instances = 4
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: performance-point-1920x1088-range = 60-60
08-30 03:40:03.394   204   204 D MediaCodecsXmlParser: parsing /vendor/etc/media_codecs_google_video.xml...
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: size-range = 2x2-1280x720
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: alignment = 8x8
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: block-size = 16x16
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: blocks-per-second-range = 1-983040
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-40000000
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: feature-adaptive-playback = 0
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: size-range = 64x64-1280x720
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: alignment = 8x8
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: block-size = 16x16
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: blocks-per-second-range = 1-244800
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-10000000
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: feature-adaptive-playback = 0
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: max-concurrent-instances = 32
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: size-range = 64x64-1280x720
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: alignment = 2x2
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: block-size = 16x16
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: blocks-per-second-range = 1-244800
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-10000000
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: feature-adaptive-playback = 0
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: max-concurrent-instances = 32
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: size-range = 2x2-1280x720
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: alignment = 8x8
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: block-size = 16x16
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: blocks-per-second-range = 1-983040
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-40000000
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: feature-adaptive-playback = 0
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: size-range = 176x144-176x144
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: alignment = 16x16
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-128000
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: size-range = 16x16-176x144
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: alignment = 16x16
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: block-size = 16x16
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: blocks-per-second-range = 12-1485
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-64000
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: size-range = 176x144-1280x720
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: alignment = 2x2
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-40000000
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: feature-bitrate-modes = VBR,CBR
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: size-range = 176x144-1280x720
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: alignment = 2x2
08-30 03:40:03.394   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-40000000
08-30 03:40:03.397    28    28 I hwservicemanager: getTransport: Cannot find entry android.hardware.usb.gadget@1.0::IUsbGadget/default in either framework or device manifest.
08-30 03:40:03.404   204   204 I MediaCodecsXmlParser: limit: feature-bitrate-modes = VBR,CBR
08-30 03:40:03.405   204   204 D MediaCodecsXmlParser: parsing /vendor/etc/media_codecs_performance.xml...
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-320x240-range = 165-165
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-720x480-range = 149-149
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1280x720-range = 73-73
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1920x1080-range = 18-18
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-320x240-range = 165-165
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-720x480-range = 149-149
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1280x720-range = 73-73
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1920x1080-range = 18-18
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-320x240-range = 165-165
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-720x480-range = 149-149
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1280x720-range = 73-73
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1920x1080-range = 18-18
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-320x240-range = 306-306
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-720x480-range = 54-54
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1280x720-range = 58-58
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-176x144-range = 619-619
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-176x144-range = 619-619
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-320x180-range = 55-55
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-640x360-range = 35-35
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1280x720-range = 28-28
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1920x1080-range = 32-32
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-320x240-range = 617-617
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-720x480-range = 559-559
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1280x720-range = 276-276
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1920x1080-range = 164-164
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-3840x2160-range = 130-130
08-30 03:40:03.405   204   204 D MediaCodecsXmlParser: MediaCodec: cannot update non-existing codec at line 63 of /vendor/etc/media_codecs_performance.xml
08-30 03:40:03.405   204   204 D MediaCodecsXmlParser: MediaCodec: cannot update non-existing codec at line 70 of /vendor/etc/media_codecs_performance.xml
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-320x180-range = 500-500
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-640x360-range = 387-387
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1280x720-range = 112-112
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1920x1080-range = 77-77
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-176x144-range = 600-600
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-352x288-range = 600-600
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-176x144-range = 600-600
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-352x288-range = 700-700
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-640x360-range = 164-286
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-720x480-range = 245-261
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1280x720-range = 181-189
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1920x1080-range = 130-130
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-3840x2160-range = 130-130
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-320x240-range = 230-230
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-720x480-range = 132-132
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1280x720-range = 38-38
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1920x1080-range = 51-51
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-352x288-range = 253-253
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-640x360-range = 128-128
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-720x480-range = 104-104
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1280x720-range = 91-91
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-320x180-range = 432-432
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-640x360-range = 320-320
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1280x720-range = 48-48
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1920x1080-range = 24-24
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-320x180-range = 432-432
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-640x360-range = 320-320
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1280x720-range = 38-42
08-30 03:40:03.405   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1920x1080-range = 94-94
08-30 03:40:03.405   204   204 D MediaCodecsXmlParser: MediaCodec: cannot update non-existing codec at line 122 of /vendor/etc/media_codecs_performance.xml
08-30 03:40:03.405   204   204 D MediaCodecsXmlParser: Cannot find /data/misc/media/media_codecs_profiling_results.xml
08-30 03:40:03.411   204   204 I ServiceManagement: Registered android.hardware.media.omx@1.0::IOmx/default (start delay of 126ms)
08-30 03:40:03.411   204   204 I ServiceManagement: Removing namespace from process name android.hardware.media.omx@1.0-service to omx@1.0-service.
08-30 03:40:03.411   204   204 I media.codec: IOmx HAL service created.
08-30 03:40:03.411   204   204 D MediaCodecsXmlParser: parsing /vendor/etc/media_codecs.xml...
08-30 03:40:03.411   204   204 D MediaCodecsXmlParser: parsing /vendor/etc/media_codecs_google_audio.xml...
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: max-channel-count = 2
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: sample-rate-ranges = 8000,11025,12000,16000,22050,24000,32000,44100,48000
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 8000-320000
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: max-channel-count = 1
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: sample-rate-ranges = 8000
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 4750-12200
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: max-channel-count = 1
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: sample-rate-ranges = 16000
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 6600-23850
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: max-channel-count = 8
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: sample-rate-ranges = 7350,8000,11025,12000,16000,22050,24000,32000,44100,48000
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 8000-960000
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: max-channel-count = 1
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: sample-rate-ranges = 8000
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 64000
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: max-channel-count = 1
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: sample-rate-ranges = 8000
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 64000
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: max-channel-count = 8
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: sample-rate-ranges = 8000-96000
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 32000-500000
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: max-channel-count = 8
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: sample-rate-ranges = 48000
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 6000-510000
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: max-channel-count = 8
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: sample-rate-ranges = 8000-96000
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-10000000
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: max-channel-count = 8
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: sample-rate-ranges = 8000-96000
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-10000000
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: max-channel-count = 6
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: sample-rate-ranges = 8000,11025,12000,16000,22050,24000,32000,44100,48000
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 8000-960000
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: max-channel-count = 1
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: sample-rate-ranges = 8000
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 4750-12200
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: feature-bitrate-modes = CBR
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: max-channel-count = 1
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: sample-rate-ranges = 16000
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 6600-23850
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: feature-bitrate-modes = CBR
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: max-channel-count = 2
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: sample-rate-ranges = 1-655350
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-21000000
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: complexity-default = 5
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: complexity-range = 0-8
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: feature-bitrate-modes = CQ
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: size-range = 96x96-4096x2160
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: alignment = 4x4
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: block-size = 16x16
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: blocks-per-second-range = 1-489600
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-10000000
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: feature-adaptive-playback = 0
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: max-concurrent-instances = 6
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: performance-point-3840x2160-range = 60-60
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: size-range = 176x144-1920x1088
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: alignment = 8x8
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: block-size = 16x16
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: blocks-per-second-range = 1-244800
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-10000000
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: feature-adaptive-playback = 0
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: max-concurrent-instances = 6
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: performance-point-1920x1088-range = 60-60
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: size-range = 176x144-1920x1088
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: alignment = 8x8
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: block-size = 16x16
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: blocks-per-second-range = 1-244800
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-10000000
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: feature-adaptive-playback = 0
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: max-concurrent-instances = 6
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: performance-point-1920x1088-range = 60-60
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: size-range = 176x144-1920x1088
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: alignment = 8x8
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: block-size = 16x16
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: blocks-per-second-range = 1-244800
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-10000000
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: feature-adaptive-playback = 0
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: max-concurrent-instances = 6
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: performance-point-1920x1088-range = 60-60
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: size-range = 176x144-1920x1088
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: alignment = 8x8
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: block-size = 16x16
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: blocks-per-second-range = 1-244800
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-10000000
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: feature-adaptive-playback = 0
08-30 03:40:03.411   204   204 I MediaCodecsXmlParser: limit: max-concurrent-instances = 6
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: performance-point-1920x1088-range = 60-60
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: size-range = 176x144-1920x1088
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: alignment = 8x8
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: block-size = 16x16
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: blocks-per-second-range = 1-244800
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-10000000
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: feature-adaptive-playback = 0
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: max-concurrent-instances = 6
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: performance-point-1920x1088-range = 60-60
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: size-range = 400x400-4096x2160
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: alignment = 2x2
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: block-size = 16x16
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: blocks-per-second-range = 1-244800
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-10000000
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: feature-adaptive-playback = 0
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: max-concurrent-instances = 6
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: performance-point-3840x2160-range = 60-60
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: size-range = 176x144-1920x1088
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: alignment = 16x8
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-10000000
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: feature-bitrate-modes = VBR,CBR
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: max-concurrent-instances = 4
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: performance-point-1920x1088-range = 60-60
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: size-range = 176x144-1920x1088
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: alignment = 16x8
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-10000000
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: feature-bitrate-modes = VBR,CBR
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: max-concurrent-instances = 4
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: performance-point-1920x1088-range = 60-60
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: size-range = 176x144-1920x1088
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: alignment = 16x8
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-10000000
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: feature-bitrate-modes = VBR,CBR
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: max-concurrent-instances = 4
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: performance-point-1920x1088-range = 60-60
08-30 03:40:03.412   204   204 D MediaCodecsXmlParser: parsing /vendor/etc/media_codecs_google_video.xml...
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: size-range = 2x2-1280x720
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: alignment = 8x8
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: block-size = 16x16
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: blocks-per-second-range = 1-983040
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-40000000
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: feature-adaptive-playback = 0
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: size-range = 64x64-1280x720
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: alignment = 8x8
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: block-size = 16x16
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: blocks-per-second-range = 1-244800
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-10000000
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: feature-adaptive-playback = 0
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: max-concurrent-instances = 32
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: size-range = 64x64-1280x720
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: alignment = 2x2
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: block-size = 16x16
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: blocks-per-second-range = 1-244800
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-10000000
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: feature-adaptive-playback = 0
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: max-concurrent-instances = 32
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: size-range = 2x2-1280x720
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: alignment = 8x8
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: block-size = 16x16
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: blocks-per-second-range = 1-983040
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-40000000
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: feature-adaptive-playback = 0
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: size-range = 176x144-176x144
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: alignment = 16x16
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-128000
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: size-range = 16x16-176x144
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: alignment = 16x16
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: block-size = 16x16
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: blocks-per-second-range = 12-1485
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-64000
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: size-range = 176x144-1280x720
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: alignment = 2x2
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-40000000
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: feature-bitrate-modes = VBR,CBR
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: size-range = 176x144-1280x720
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: alignment = 2x2
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: bitrate-range = 1-40000000
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: feature-bitrate-modes = VBR,CBR
08-30 03:40:03.412   204   204 D MediaCodecsXmlParser: parsing /vendor/etc/media_codecs_performance.xml...
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-320x240-range = 165-165
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-720x480-range = 149-149
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1280x720-range = 73-73
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1920x1080-range = 18-18
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-320x240-range = 165-165
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-720x480-range = 149-149
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1280x720-range = 73-73
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1920x1080-range = 18-18
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-320x240-range = 165-165
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-720x480-range = 149-149
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1280x720-range = 73-73
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1920x1080-range = 18-18
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-320x240-range = 306-306
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-720x480-range = 54-54
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1280x720-range = 58-58
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-176x144-range = 619-619
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-176x144-range = 619-619
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-320x180-range = 55-55
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-640x360-range = 35-35
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1280x720-range = 28-28
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1920x1080-range = 32-32
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-320x240-range = 617-617
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-720x480-range = 559-559
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1280x720-range = 276-276
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1920x1080-range = 164-164
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-3840x2160-range = 130-130
08-30 03:40:03.412   204   204 D MediaCodecsXmlParser: MediaCodec: cannot update non-existing codec at line 63 of /vendor/etc/media_codecs_performance.xml
08-30 03:40:03.412   204   204 D MediaCodecsXmlParser: MediaCodec: cannot update non-existing codec at line 70 of /vendor/etc/media_codecs_performance.xml
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-320x180-range = 500-500
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-640x360-range = 387-387
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1280x720-range = 112-112
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1920x1080-range = 77-77
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-176x144-range = 600-600
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-352x288-range = 600-600
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-176x144-range = 600-600
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-352x288-range = 700-700
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-640x360-range = 164-286
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-720x480-range = 245-261
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1280x720-range = 181-189
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1920x1080-range = 130-130
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-3840x2160-range = 130-130
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-320x240-range = 230-230
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-720x480-range = 132-132
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1280x720-range = 38-38
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1920x1080-range = 51-51
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-352x288-range = 253-253
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-640x360-range = 128-128
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-720x480-range = 104-104
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1280x720-range = 91-91
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-320x180-range = 432-432
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-640x360-range = 320-320
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1280x720-range = 48-48
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1920x1080-range = 24-24
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-320x180-range = 432-432
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-640x360-range = 320-320
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1280x720-range = 38-42
08-30 03:40:03.412   204   204 I MediaCodecsXmlParser: limit: measured-frame-rate-1920x1080-range = 94-94
08-30 03:40:03.412   204   204 D MediaCodecsXmlParser: MediaCodec: cannot update non-existing codec at line 122 of /vendor/etc/media_codecs_performance.xml
08-30 03:40:03.412   204   204 D MediaCodecsXmlParser: Cannot find /data/misc/media/media_codecs_profiling_results.xml
08-30 03:40:03.412   204   204 E MediaCodecsXmlParser: Cannot find the role for a decoder of type video/flv
08-30 03:40:03.412   204   204 E MediaCodecsXmlParser: Cannot find the role for a decoder of type video/mjpeg
08-30 03:40:03.415   207   207 I /apex/com.android.media.swcodec/bin/mediaswcodec: media swcodec service starting
08-30 03:40:03.415   207   207 W /apex/com.android.media.swcodec/bin/mediaswcodec: Could not read additional policy file '/vendor/etc/seccomp_policy/mediaswcodec.policy'
08-30 03:40:03.415   207   207 W /apex/com.android.media.swcodec/bin/mediaswcodec: libminijail[207]: failed to get path of fd 4: No such file or directory
08-30 03:40:03.415   207   207 W /apex/com.android.media.swcodec/bin/mediaswcodec: libminijail[207]: allowing syscall: connect
08-30 03:40:03.415   207   207 W /apex/com.android.media.swcodec/bin/mediaswcodec: libminijail[207]: allowing syscall: fcntl
08-30 03:40:03.415   207   207 W /apex/com.android.media.swcodec/bin/mediaswcodec: libminijail[207]: allowing syscall: sendto
08-30 03:40:03.415   207   207 W /apex/com.android.media.swcodec/bin/mediaswcodec: libminijail[207]: allowing syscall: socket
08-30 03:40:03.415   207   207 W /apex/com.android.media.swcodec/bin/mediaswcodec: libminijail[207]: allowing syscall: writev
08-30 03:40:03.415   207   207 W /apex/com.android.media.swcodec/bin/mediaswcodec: libminijail[207]: logging seccomp filter failures
08-30 03:40:03.415   207   207 I CodecServiceRegistrant: Creating software Codec2 service...
08-30 03:40:03.416   211   211 I usbd    : Usb HAL not found
08-30 03:40:03.416   204   204 I ServiceManagement: Registered android.hardware.media.omx@1.0::IOmxStore/default (start delay of 132ms)
08-30 03:40:03.416   204   204 I ServiceManagement: Removing namespace from process name android.hardware.media.omx@1.0-service to omx@1.0-service.
08-30 03:40:03.419    44    44 I ServiceManager: Waiting for service 'SurfaceFlinger' on '/dev/binder'...
08-30 03:40:03.423   177   177 I mediaserver: ServiceManager: 0xf19232a0
08-30 03:40:03.423   177   177 W BatteryNotifier: batterystats service unavailable!
08-30 03:40:03.423   177   177 W BatteryNotifier: batterystats service unavailable!
08-30 03:40:03.424   207   207 I ServiceManagement: Registered android.hardware.media.c2@1.0::IComponentStore/software (start delay of 129ms)
08-30 03:40:03.424   207   207 I CodecServiceRegistrant: Software Codec2 service created.
08-30 03:40:03.436   195   195 I installd: installd firing up
08-30 03:40:03.446   200   200 I netdClient: Skipping libnetd_client init since *we* are netd
08-30 03:40:03.448    28    28 I hwservicemanager: getTransport: Cannot find entry android.hardware.keymaster@4.0::IKeymasterDevice/default in either framework or device manifest.
08-30 03:40:03.451   202   244 I storaged: storaged: Start
08-30 03:40:03.454   205   205 D DrmService: ----------------running drmservice---------------
08-30 03:40:03.454   205   205 E DrmService: rknand_sys_storage open fail
08-30 03:40:03.454   205   205 D DrmService: Get HID data:
08-30 03:40:03.454   196   196 I keystore: found android.hardware.keymaster@3.0::IKeymasterDevice with interface name default and seclevel SOFTWARE
08-30 03:40:03.454   196   196 W keystore: No secure Keymaster implementation found, but device offers insecure Keymaster HAL. Using as default.
08-30 03:40:03.458   200   200 I netd    : netd 1.0 starting
08-30 03:40:03.461   200   200 I Netd    : Loaded resolver library from /apex/com.android.resolv/lib64/libnetd_resolv.so
08-30 03:40:03.462   200   200 D TetherController: Setting IP forward enable = 0
08-30 03:40:03.467   196   196 I ServiceManagement: Registered android.system.wifi.keystore@1.0::IKeystore/default (start delay of 193ms)
08-30 03:40:03.467   199   199 I mediametrics: ServiceManager: 0x772d28f280
08-30 03:40:03.467   199   199 D MediaAnalyticsService: MediaAnalyticsService created
08-30 03:40:03.472   205   205 E DrmService: ----vendor read sn error,try drmboot----
08-30 03:40:03.472   205   205 E DrmService: rknand_sys_storage open fail
08-30 03:40:03.472   205   205 D DrmService: verify: save serialno:  (0)
08-30 03:40:03.484   187   187 D AndroidRuntime: >>>>>> START com.android.internal.os.ZygoteInit uid 0 <<<<<<
08-30 03:40:03.487   187   187 I AndroidRuntime: Using default boot image
08-30 03:40:03.487   187   187 I AndroidRuntime: Leaving lock profiling enabled
08-30 03:40:03.491   200   200 I netd    : Creating child chains: 27.7ms
08-30 03:40:03.491   200   200 I netd    : Setting up OEM hooks: 0.1ms
08-30 03:40:03.491   200   200 I netd    : Setting up FirewallController hooks: 0.0ms
08-30 03:40:03.491   186   186 D AndroidRuntime: >>>>>> START com.android.internal.os.ZygoteInit uid 0 <<<<<<
08-30 03:40:03.491   200   200 I netd    : Setting up TetherController hooks: 0.7ms
08-30 03:40:03.492   200   200 I netd    : Setting up BandwidthController hooks: 0.5ms
08-30 03:40:03.492   200   200 I netd    : Setting up IdletimerController hooks: 0.0ms
08-30 03:40:03.493   187   187 I zygote  : option[0]=-Xzygote
08-30 03:40:03.493   187   187 I zygote  : option[1]=exit
08-30 03:40:03.493   187   187 I zygote  : option[2]=vfprintf
08-30 03:40:03.493   187   187 I zygote  : option[3]=sensitiveThread
08-30 03:40:03.493   187   187 I zygote  : option[4]=-verbose:gc
08-30 03:40:03.493   187   187 I zygote  : option[5]=-Xms16m
08-30 03:40:03.493   187   187 I zygote  : option[6]=-Xmx512m
08-30 03:40:03.493   187   187 I zygote  : option[7]=-XX:HeapGrowthLimit=192m
08-30 03:40:03.493   187   187 I zygote  : option[8]=-XX:HeapMinFree=512k
08-30 03:40:03.493   187   187 I zygote  : option[9]=-XX:HeapMaxFree=8m
08-30 03:40:03.493   187   187 I zygote  : option[10]=-XX:HeapTargetUtilization=0.75
08-30 03:40:03.493   187   187 I zygote  : option[11]=-Xusejit:true
08-30 03:40:03.493   187   187 I zygote  : option[12]=-Xjitsaveprofilinginfo
08-30 03:40:03.493   187   187 I zygote  : option[13]=-XjdwpOptions:suspend=n,server=y
08-30 03:40:03.493   187   187 I zygote  : option[14]=-XjdwpProvider:default
08-30 03:40:03.493   187   187 I zygote  : option[15]=-Ximage-compiler-option
08-30 03:40:03.493   187   187 I zygote  : option[16]=--runtime-arg
08-30 03:40:03.493   187   187 I zygote  : option[17]=-Ximage-compiler-option
08-30 03:40:03.493   187   187 I zygote  : option[18]=-Xms64m
08-30 03:40:03.493   187   187 I zygote  : option[19]=-Ximage-compiler-option
08-30 03:40:03.493   187   187 I zygote  : option[20]=--runtime-arg
08-30 03:40:03.493   187   187 I zygote  : option[21]=-Ximage-compiler-option
08-30 03:40:03.493   187   187 I zygote  : option[22]=-Xmx64m
08-30 03:40:03.493   187   187 I zygote  : option[23]=-Ximage-compiler-option
08-30 03:40:03.493   187   187 I zygote  : option[24]=--profile-file=/system/etc/boot-image.prof
08-30 03:40:03.493   187   187 I zygote  : option[25]=-Ximage-compiler-option
08-30 03:40:03.493   187   187 I zygote  : option[26]=--compiler-filter=speed-profile
08-30 03:40:03.493   187   187 I zygote  : option[27]=-Xcompiler-option
08-30 03:40:03.493   187   187 I zygote  : option[28]=--runtime-arg
08-30 03:40:03.493   187   187 I zygote  : option[29]=-Xcompiler-option
08-30 03:40:03.493   187   187 I zygote  : option[30]=-Xms64m
08-30 03:40:03.493   187   187 I zygote  : option[31]=-Xcompiler-option
08-30 03:40:03.493   187   187 I zygote  : option[32]=--runtime-arg
08-30 03:40:03.493   187   187 I zygote  : option[33]=-Xcompiler-option
08-30 03:40:03.493   187   187 I zygote  : option[34]=-Xmx512m
08-30 03:40:03.493   187   187 I zygote  : option[35]=-Ximage-compiler-option
08-30 03:40:03.493   187   187 I zygote  : option[36]=--instruction-set-variant=cortex-a76
08-30 03:40:03.493   187   187 I zygote  : option[37]=-Xcompiler-option
08-30 03:40:03.493   187   187 I zygote  : option[38]=--instruction-set-variant=cortex-a76
08-30 03:40:03.493   187   187 I zygote  : option[39]=-Ximage-compiler-option
08-30 03:40:03.493   187   187 I zygote  : option[40]=--instruction-set-features=default
08-30 03:40:03.493   187   187 I zygote  : option[41]=-Xcompiler-option
08-30 03:40:03.493   187   187 I zygote  : option[42]=--instruction-set-features=default
08-30 03:40:03.493   187   187 I zygote  : option[43]=-Duser.locale=zh-CN
08-30 03:40:03.493   187   187 I zygote  : option[44]=--cpu-abilist=armeabi-v7a,armeabi
08-30 03:40:03.493   187   187 I zygote  : option[45]=-Xcompiler-option
08-30 03:40:03.493   187   187 I zygote  : option[46]=--generate-mini-debug-info
08-30 03:40:03.493   187   187 I zygote  : option[47]=-Xfingerprint:samsung/GT-P7500/GT-P7500:3.2/HTJ85B/XWKL1:user/release-keys
08-30 03:40:03.494   186   186 I AndroidRuntime: Using default boot image
08-30 03:40:03.494   186   186 I AndroidRuntime: Leaving lock profiling enabled
08-30 03:40:03.494   186   186 I zygote64: option[0]=-Xzygote
08-30 03:40:03.494   186   186 I zygote64: option[1]=exit
08-30 03:40:03.494   186   186 I zygote64: option[2]=vfprintf
08-30 03:40:03.494   186   186 I zygote64: option[3]=sensitiveThread
08-30 03:40:03.494   186   186 I zygote64: option[4]=-verbose:gc
08-30 03:40:03.494   186   186 I zygote64: option[5]=-Xms16m
08-30 03:40:03.494   186   186 I zygote64: option[6]=-Xmx512m
08-30 03:40:03.494   186   186 I zygote64: option[7]=-XX:HeapGrowthLimit=192m
08-30 03:40:03.494   186   186 I zygote64: option[8]=-XX:HeapMinFree=512k
08-30 03:40:03.494   186   186 I zygote64: option[9]=-XX:HeapMaxFree=8m
08-30 03:40:03.494   186   186 I zygote64: option[10]=-XX:HeapTargetUtilization=0.75
08-30 03:40:03.494   186   186 I zygote64: option[11]=-Xusejit:true
08-30 03:40:03.494   186   186 I zygote64: option[12]=-Xjitsaveprofilinginfo
08-30 03:40:03.494   186   186 I zygote64: option[13]=-XjdwpOptions:suspend=n,server=y
08-30 03:40:03.494   186   186 I zygote64: option[14]=-XjdwpProvider:default
08-30 03:40:03.494   186   186 I zygote64: option[15]=-Ximage-compiler-option
08-30 03:40:03.494   186   186 I zygote64: option[16]=--runtime-arg
08-30 03:40:03.494   186   186 I zygote64: option[17]=-Ximage-compiler-option
08-30 03:40:03.494   186   186 I zygote64: option[18]=-Xms64m
08-30 03:40:03.494   186   186 I zygote64: option[19]=-Ximage-compiler-option
08-30 03:40:03.494   186   186 I zygote64: option[20]=--runtime-arg
08-30 03:40:03.494   186   186 I zygote64: option[21]=-Ximage-compiler-option
08-30 03:40:03.494   186   186 I zygote64: option[22]=-Xmx64m
08-30 03:40:03.494   186   186 I zygote64: option[23]=-Ximage-compiler-option
08-30 03:40:03.494   186   186 I zygote64: option[24]=--profile-file=/system/etc/boot-image.prof
08-30 03:40:03.494   186   186 I zygote64: option[25]=-Ximage-compiler-option
08-30 03:40:03.494   186   186 I zygote64: option[26]=--compiler-filter=speed-profile
08-30 03:40:03.494   186   186 I zygote64: option[27]=-Xcompiler-option
08-30 03:40:03.494   186   186 I zygote64: option[28]=--runtime-arg
08-30 03:40:03.494   186   186 I zygote64: option[29]=-Xcompiler-option
08-30 03:40:03.494   186   186 I zygote64: option[30]=-Xms64m
08-30 03:40:03.494   186   186 I zygote64: option[31]=-Xcompiler-option
08-30 03:40:03.494   186   186 I zygote64: option[32]=--runtime-arg
08-30 03:40:03.494   186   186 I zygote64: option[33]=-Xcompiler-option
08-30 03:40:03.494   186   186 I zygote64: option[34]=-Xmx512m
08-30 03:40:03.494   186   186 I zygote64: option[35]=-Ximage-compiler-option
08-30 03:40:03.495   186   186 I zygote64: option[36]=--instruction-set-variant=cortex-a76
08-30 03:40:03.495   186   186 I zygote64: option[37]=-Xcompiler-option
08-30 03:40:03.495   186   186 I zygote64: option[38]=--instruction-set-variant=cortex-a76
08-30 03:40:03.495   186   186 I zygote64: option[39]=-Ximage-compiler-option
08-30 03:40:03.495   186   186 I zygote64: option[40]=--instruction-set-features=default
08-30 03:40:03.495   186   186 I zygote64: option[41]=-Xcompiler-option
08-30 03:40:03.495   186   186 I zygote64: option[42]=--instruction-set-features=default
08-30 03:40:03.495   186   186 I zygote64: option[43]=-Duser.locale=zh-CN
08-30 03:40:03.495   186   186 I zygote64: option[44]=--cpu-abilist=arm64-v8a
08-30 03:40:03.495   186   186 I zygote64: option[45]=-Xcompiler-option
08-30 03:40:03.495   186   186 I zygote64: option[46]=--generate-mini-debug-info
08-30 03:40:03.495   186   186 I zygote64: option[47]=-Xfingerprint:samsung/GT-P7500/GT-P7500:3.2/HTJ85B/XWKL1:user/release-keys
08-30 03:40:03.497   200   200 I netd    : Setting up StrictController hooks: 5.3ms
08-30 03:40:03.497   200   200 I ClatdController: 4.9+ kernel and device shipped with Q+ - clat ebpf should work.
08-30 03:40:03.497   200   200 I netd    : Initializing ClatdController: 0.1ms
08-30 03:40:03.516   200   200 I netd    : Initializing traffic control: 18.4ms
08-30 03:40:03.516   205   205 E DrmService: Unable to open path (/sys/class/android_usb/android0/iSerial),error is(No such file or directory)
08-30 03:40:03.516   205   205 E DrmService: try /config/usb_gadget/g1/strings/0x409/serialnumber
08-30 03:40:03.516   205   205 E DrmService: Unable to open path (/config/usb_gadget/g1/strings/0x409/serialnumber),error is(No such file or directory)
08-30 03:40:03.518   200   200 I netd    : Enabling bandwidth control: 2.0ms
08-30 03:40:03.520    44    44 I ServiceManager: Waiting for service 'SurfaceFlinger' on '/dev/binder'...
08-30 03:40:03.531   252   252 I adbd    : adbd listening on port 5555
08-30 03:40:03.532   200   200 E Netd    : cannot find interface dummy0
08-30 03:40:03.533   200   200 I netd    : Initializing RouteController: 14.8ms
08-30 03:40:03.533   200   200 D XfrmController: XfrmController::ipSecAddXfrmInterface, line=1379
08-30 03:40:03.536   200   200 D XfrmController: XfrmController::ipSecRemoveTunnelInterface, line=1592
08-30 03:40:03.536   200   200 D XfrmController: deviceName=ipsec_test
08-30 03:40:03.536   200   200 D XfrmController: Sending Netlink XFRM Message: XFRM_MSG_FLUSHSA
08-30 03:40:03.536   200   200 D XfrmController: Sending Netlink XFRM Message: XFRM_MSG_FLUSHPOLICY
08-30 03:40:03.536   200   200 I netd    : Initializing XfrmController: 3.4ms
08-30 03:40:03.536   200   200 I libnetd_resolv: resolv_init: Initializing resolver
08-30 03:40:03.541   200   200 D MDnsDS  : MDnsSdListener::Hander starting up
08-30 03:40:03.541   200   264 D MDnsDS  : MDnsSdListener starting to monitor
08-30 03:40:03.541   200   264 D MDnsDS  : Going to poll with pollCount 1
08-30 03:40:03.542   200   200 I netd    : Registering NetdNativeService: 1.2ms
08-30 03:40:03.547   200   200 I ServiceManagement: Registered android.system.net.netd@1.1::INetd/default (start delay of 263ms)
08-30 03:40:03.548   200   200 I netd    : Registering NetdHwService: 5.5ms
08-30 03:40:03.548   200   200 I netd    : Netd started in 100ms
08-30 03:40:03.558   193   193 I ScriptGuard: Server is listening for connections.
08-30 03:40:03.571   186   186 D ICU     : Time zone APEX file found: /apex/com.android.tzdata/etc/icu/icu_tzdata.dat
08-30 03:40:03.573   187   187 D ICU     : Time zone APEX file found: /apex/com.android.tzdata/etc/icu/icu_tzdata.dat
08-30 03:40:03.588   186   186 W zygote64: JNI RegisterNativeMethods: attempt to register 0 native methods for android.media.AudioAttributes
08-30 03:40:03.590   186   186 W zygote64: Landroid/util/S9Helper; failed initialization: java.lang.InternalError: Cannot create threads in zygote
08-30 03:40:03.590   186   186 W zygote64:   at void java.lang.Thread.nativeCreate(java.lang.Thread, long, boolean) (Thread.java:-2)
08-30 03:40:03.590   186   186 W zygote64:   at void java.lang.Thread.start() (Thread.java:883)
08-30 03:40:03.590   186   186 W zygote64:   at java.lang.Object sun.nio.fs.AbstractPoller$1.run() (AbstractPoller.java:64)
08-30 03:40:03.590   186   186 W zygote64:   at java.lang.Object java.security.AccessController.doPrivileged(java.security.PrivilegedAction) (AccessController.java:43)
08-30 03:40:03.590   186   186 W zygote64:   at void sun.nio.fs.AbstractPoller.start() (AbstractPoller.java:59)
08-30 03:40:03.590   186   186 W zygote64:   at void sun.nio.fs.LinuxWatchService.<init>(sun.nio.fs.UnixFileSystem) (LinuxWatchService.java:83)
08-30 03:40:03.590   186   186 W zygote64:   at java.nio.file.WatchService sun.nio.fs.LinuxFileSystem.newWatchService() (LinuxFileSystem.java:47)
08-30 03:40:03.590   186   186 W zygote64:   at void android.util.S9Helper.<clinit>() (S9Helper.java:18)
08-30 03:40:03.590   186   186 W zygote64:   at java.lang.String android.os.SystemProperties.get(java.lang.String) (SystemProperties.java:114)
08-30 03:40:03.590   186   186 W zygote64:   at void com.android.internal.os.ZygoteInit.main(java.lang.String[]) (ZygoteInit.java:836)
08-30 03:40:03.590   186   186 W zygote64: 
08-30 03:40:03.591   186   186 E Zygote  : System zygote died with exception
08-30 03:40:03.591   186   186 E Zygote  : java.lang.InternalError: Cannot create threads in zygote
08-30 03:40:03.591   186   186 E Zygote  :      at java.lang.Thread.nativeCreate(Native Method)
08-30 03:40:03.591   186   186 E Zygote  :      at java.lang.Thread.start(Thread.java:883)
08-30 03:40:03.591   186   186 E Zygote  :      at sun.nio.fs.AbstractPoller$1.run(AbstractPoller.java:64)
08-30 03:40:03.591   186   186 E Zygote  :      at java.security.AccessController.doPrivileged(AccessController.java:43)
08-30 03:40:03.591   186   186 E Zygote  :      at sun.nio.fs.AbstractPoller.start(AbstractPoller.java:59)
08-30 03:40:03.591   186   186 E Zygote  :      at sun.nio.fs.LinuxWatchService.<init>(LinuxWatchService.java:83)
08-30 03:40:03.591   186   186 E Zygote  :      at sun.nio.fs.LinuxFileSystem.newWatchService(LinuxFileSystem.java:47)
08-30 03:40:03.591   186   186 E Zygote  :      at android.util.S9Helper.<clinit>(S9Helper.java:18)
08-30 03:40:03.591   186   186 E Zygote  :      at android.os.SystemProperties.get(SystemProperties.java:114)
08-30 03:40:03.591   186   186 E Zygote  :      at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:836)
08-30 03:40:03.591   186   186 D AndroidRuntime: Shutting down VM
08-30 03:40:03.595   187   187 W zygote  : JNI RegisterNativeMethods: attempt to register 0 native methods for android.media.AudioAttributes
08-30 03:40:03.599   187   187 W zygote  : Landroid/util/S9Helper; failed initialization: java.lang.InternalError: Cannot create threads in zygote
08-30 03:40:03.599   187   187 W zygote  :   at void java.lang.Thread.nativeCreate(java.lang.Thread, long, boolean) (Thread.java:-2)
08-30 03:40:03.599   187   187 W zygote  :   at void java.lang.Thread.start() (Thread.java:883)
08-30 03:40:03.599   187   187 W zygote  :   at java.lang.Object sun.nio.fs.AbstractPoller$1.run() (AbstractPoller.java:64)
08-30 03:40:03.599   187   187 W zygote  :   at java.lang.Object java.security.AccessController.doPrivileged(java.security.PrivilegedAction) (AccessController.java:43)
08-30 03:40:03.599   187   187 W zygote  :   at void sun.nio.fs.AbstractPoller.start() (AbstractPoller.java:59)
08-30 03:40:03.599   187   187 W zygote  :   at void sun.nio.fs.LinuxWatchService.<init>(sun.nio.fs.UnixFileSystem) (LinuxWatchService.java:83)
08-30 03:40:03.599   187   187 W zygote  :   at java.nio.file.WatchService sun.nio.fs.LinuxFileSystem.newWatchService() (LinuxFileSystem.java:47)
08-30 03:40:03.599   187   187 W zygote  :   at void android.util.S9Helper.<clinit>() (S9Helper.java:18)
08-30 03:40:03.599   187   187 W zygote  :   at java.lang.String android.os.SystemProperties.get(java.lang.String) (SystemProperties.java:114)
08-30 03:40:03.599   187   187 W zygote  :   at void com.android.internal.os.ZygoteInit.main(java.lang.String[]) (ZygoteInit.java:836)
08-30 03:40:03.599   187   187 W zygote  : 
08-30 03:40:03.599   187   187 E Zygote  : System zygote died with exception
08-30 03:40:03.599   187   187 E Zygote  : java.lang.InternalError: Cannot create threads in zygote
08-30 03:40:03.599   187   187 E Zygote  :      at java.lang.Thread.nativeCreate(Native Method)
08-30 03:40:03.599   187   187 E Zygote  :      at java.lang.Thread.start(Thread.java:883)
08-30 03:40:03.599   187   187 E Zygote  :      at sun.nio.fs.AbstractPoller$1.run(AbstractPoller.java:64)
08-30 03:40:03.599   187   187 E Zygote  :      at java.security.AccessController.doPrivileged(AccessController.java:43)
08-30 03:40:03.599   187   187 E Zygote  :      at sun.nio.fs.AbstractPoller.start(AbstractPoller.java:59)
08-30 03:40:03.599   187   187 E Zygote  :      at sun.nio.fs.LinuxWatchService.<init>(LinuxWatchService.java:83)
08-30 03:40:03.599   187   187 E Zygote  :      at sun.nio.fs.LinuxFileSystem.newWatchService(LinuxFileSystem.java:47)
08-30 03:40:03.599   187   187 E Zygote  :      at android.util.S9Helper.<clinit>(S9Helper.java:18)
08-30 03:40:03.599   187   187 E Zygote  :      at android.os.SystemProperties.get(SystemProperties.java:114)
08-30 03:40:03.599   187   187 E Zygote  :      at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:836)
08-30 03:40:03.599   187   187 D AndroidRuntime: Shutting down VM
08-30 03:40:03.607   197   197 I mediaserver: ServiceManager: 0xf4283120
08-30 03:40:03.613    27    27 I ServiceManager: service 'media.player' died
08-30 03:40:03.613    27    27 I ServiceManager: service 'media.resource_manager' died
08-30 03:40:03.618    27    27 I ServiceManager: service 'dnsresolver' died
08-30 03:40:03.618    27    27 I ServiceManager: service 'netd' died
08-30 03:40:03.620    44    44 I ServiceManager: Waiting for service 'SurfaceFlinger' on '/dev/binder'...
08-30 03:40:03.636   198   198 V MediaUtils: physMem: 16703926272
08-30 03:40:03.636   198   198 V MediaUtils: requested limit: 3340785240
08-30 03:40:03.636   198   198 I libc    : malloc_limit: Allocation limit enabled, max size 3340785240 bytes
08-30 03:40:03.638   198   198 W /system/bin/mediaextractor: Could not read additional policy file '/vendor/etc/seccomp_policy/mediaextractor.policy'
08-30 03:40:03.638   198   198 W /system/bin/mediaextractor: libminijail[198]: failed to get path of fd 4: No such file or directory
08-30 03:40:03.638   198   198 W /system/bin/mediaextractor: libminijail[198]: allowing syscall: connect
08-30 03:40:03.638   198   198 W /system/bin/mediaextractor: libminijail[198]: allowing syscall: fcntl
08-30 03:40:03.638   198   198 W /system/bin/mediaextractor: libminijail[198]: allowing syscall: sendto
08-30 03:40:03.638   198   198 W /system/bin/mediaextractor: libminijail[198]: allowing syscall: socket
08-30 03:40:03.638   198   198 W /system/bin/mediaextractor: libminijail[198]: allowing syscall: writev
08-30 03:40:03.638   198   198 W /system/bin/mediaextractor: libminijail[198]: logging seccomp filter failures
08-30 03:40:03.663   198   198 E MediaExtractorFactory: couldn't opendir(/system/lib64/extractors)
08-30 03:40:03.667   296   296 I /system/bin/sshd: Server listening on :: port 22.
08-30 03:40:03.667   296   296 I /system/bin/sshd: Server listening on 0.0.0.0 port 22.
08-30 03:40:03.667   296   296 E /system/bin/sshd: error: Couldn't create pid file "/var/run/sshd.pid": Read-only file system
08-30 03:40:03.681    27    27 I ServiceManager: service 'wificond' died
08-30 03:40:03.720    44    44 I ServiceManager: Waiting for service 'SurfaceFlinger' on '/dev/binder'...
08-30 03:40:03.761    43    43 D RenderEngine: shader cache generated - 48 shaders in 366.929688 ms
08-30 03:40:03.762    43    43 I ServiceManagement: Registered android.frameworks.displayservice@1.0::IDisplayService/default (start delay of 937ms)
08-30 03:40:03.762    43    43 E SurfaceFlinger: Couldn't set SCHED_FIFO
08-30 03:40:03.762    43    43 D SurfaceFlinger: Setting power mode 2 on display 0
08-30 03:40:03.762    90    90 E hwc-drm-two: SetPowerMode,line=2050 init_success_=0 skip.
08-30 03:40:03.762    43    43 E HWComposer: setPowerMode: setPowerMode(On) failed for display 0: BadDisplay (2)
08-30 03:40:03.762    43    43 W SurfaceFlinger: Couldn't set SCHED_FIFO on display on
08-30 03:40:03.762    43    43 D SurfaceFlinger: Finished setting power mode 2 on display 0
08-30 03:40:03.821    44    44 D BootAnimation: BootAnimationStartTiming start time: 67887776ms
08-30 03:40:03.821    44    44 D BootAnimation: BootAnimationPreloadTiming start time: 67887776ms
08-30 03:40:03.821    44    44 D BootAnimation: bootvideo:No boot video animation,EXIT_VIDEO_NAME:false,bootvideo.showtime:-1
08-30 03:40:03.821    44    44 D BootAnimation: BootAnimationPreloadStopTiming start time: 67887776ms
08-30 03:40:03.829    44   312 D libEGL  : loaded /vendor/lib64/egl/libGLES_mali.so
08-30 03:40:03.834    44   312 I mali_so : [File] : hardware/arm/maliT760/driver/product/base/src/mali_base_kbase.c; [Line] : 1292; [Func] : base_context_deal_with_version_affairs_rk_ext;
08-30 03:40:03.834    44   312 I mali_so : arm_release_ver of this mali_so is 'g12p0-01eac0', rk_so_ver is '5'.
08-30 03:40:03.834    44   312 I mali_so : [File] : hardware/arm/maliT760/driver/product/base/src/mali_base_kbase.c; [Line] : 1308; [Func] : base_context_deal_with_version_affairs_rk_ext;
08-30 03:40:03.834    44   312 I mali_so : arm_release_vers are match. to set the full mali_ver 'g12p0-01eac0-5' as value of 'sys.gmali.version'.
08-30 03:40:03.936    28    28 I hwservicemanager: getTransport: Cannot find entry android.hardware.configstore@1.0::ISurfaceFlingerConfigs/default in either framework or device manifest.
08-30 03:40:03.943    44   312 D BootAnimation: BootAnimationShownTiming start time: 67887898ms
08-30 03:40:03.970    43    43 I SurfaceFlinger: Enter boot animation
08-30 03:40:03.971    90    90 E drm_hwc2_gralloc: hwc_get_handle_name:cann't get value from gralloc
08-30 03:40:03.971    90   224 E drm_hwc2_gralloc: hwc_get_handle_name:cann't get value from gralloc
08-30 03:40:03.971    90   224 E hwc-drm-two: hello:socket:29
08-30 03:40:03.987    90   224 E drm_hwc2_gralloc: hwc_get_handle_name:cann't get value from gralloc
08-30 03:40:03.987    90   224 I chatty  : uid=1000(system) HwBinder:90_2 identical 1 line
08-30 03:40:04.054    90   224 E drm_hwc2_gralloc: hwc_get_handle_name:cann't get value from gralloc
08-30 03:40:08.021   326   326 D RockitHwService: rockit.hardware.rockit.hw@1.0-service starting...
08-30 03:40:08.021   326   326 W /vendor/bin/hw/rockchip.hardware.rockit.hw@1.0-service: No seccomp policy defined for this architecture.
08-30 03:40:08.021   326   326 D RockitHwService: Instantiating rockit hw service....
08-30 03:40:08.021   326   326 D RockitHwService: RockitHwService
08-30 03:40:08.021   326   326 I ServiceManagement: Registered rockchip.hardware.rockit.hw@1.0::IRockitHwService/default (start delay of 17ms)
08-30 03:40:08.021   326   326 I ServiceManagement: Removing namespace from process name rockchip.hardware.rockit.hw@1.0-service to hw@1.0-service.
08-30 03:40:08.021   326   326 I RockitHwService: rockit hw service created
08-30 03:40:08.045   325   325 I ServiceManagement: Registered android.hardware.audio@5.0::IDevicesFactory/default (start delay of 40ms)
08-30 03:40:08.045   325   325 I ServiceManagement: Removing namespace from process name android.hardware.audio@2.0-service to audio@2.0-service.
08-30 03:40:08.045   325   325 I audiohalservice: Registration complete for android.hardware.audio@5.0::IDevicesFactory/default.
08-30 03:40:08.048   325   325 I ServiceManagement: Registered android.hardware.audio.effect@5.0::IEffectsFactory/default (start delay of 44ms)
08-30 03:40:08.048   325   325 I audiohalservice: Registration complete for android.hardware.audio.effect@5.0::IEffectsFactory/default.
08-30 03:40:08.048    28    28 I hwservicemanager: getTransport: Cannot find entry android.hardware.soundtrigger@2.2::ISoundTriggerHw/default in either framework or device manifest.
08-30 03:40:08.049   325   325 E audiohalservice: Could not get passthrough implementation for android.hardware.soundtrigger@2.2::ISoundTriggerHw/default.
08-30 03:40:08.049    28    28 I hwservicemanager: getTransport: Cannot find entry android.hardware.soundtrigger@2.1::ISoundTriggerHw/default in either framework or device manifest.
08-30 03:40:08.049   325   325 E audiohalservice: Could not get passthrough implementation for android.hardware.soundtrigger@2.1::ISoundTriggerHw/default.
08-30 03:40:08.050   325   325 E SoundTriggerHalImpl: couldn't load sound trigger module sound_trigger.primary (No such file or directory)
08-30 03:40:08.051   325   325 I ServiceManagement: Registered android.hardware.soundtrigger@2.0::ISoundTriggerHw/default (start delay of 46ms)
08-30 03:40:08.051   325   325 I audiohalservice: Registration complete for android.hardware.soundtrigger@2.0::ISoundTriggerHw/default.
08-30 03:40:08.051    28    28 I hwservicemanager: getTransport: Cannot find entry android.hardware.bluetooth.audio@2.0::IBluetoothAudioProvidersFactory/default in either framework or device manifest.
08-30 03:40:08.051   325   325 E audiohalservice: Could not get passthrough implementation for android.hardware.bluetooth.audio@2.0::IBluetoothAudioProvidersFactory/default.
08-30 03:40:08.051   325   325 W audiohalservice: Could not register Bluetooth Audio API 2.0
08-30 03:40:08.051    28    28 I hwservicemanager: getTransport: Cannot find entry android.hardware.bluetooth.a2dp@1.0::IBluetoothAudioOffload/default in either framework or device manifest.
08-30 03:40:08.051   325   325 E audiohalservice: Could not get passthrough implementation for android.hardware.bluetooth.a2dp@1.0::IBluetoothAudioOffload/default.
08-30 03:40:08.051   325   325 W audiohalservice: Could not register Bluetooth audio offload 1.0
08-30 03:40:08.092   327   327 I FastMixerState: sMaxFastTracks = 8
08-30 03:40:08.093   327   327 V MediaUtils: physMem: 16703926272
08-30 03:40:08.093   327   327 V MediaUtils: requested limit: 536870912
08-30 03:40:08.093   327   327 I libc    : malloc_limit: Allocation limit enabled, max size 536870912 bytes
08-30 03:40:08.093   327   327 I audioserver: ServiceManager: 0x7b71d49dc0
08-30 03:40:08.093   327   327 W BatteryNotifier: batterystats service unavailable!
08-30 03:40:08.094    28    28 I hwservicemanager: getTransport: Cannot find entry android.hardware.audio@5.0::IDevicesFactory/msd in either framework or device manifest.
08-30 03:40:08.095   327   327 I AudioFlinger: Using default 3000 mSec as standby time.
08-30 03:40:08.095   327   327 E APM::Serializer: deserialize: Could not parse /odm/etc/audio_policy_configuration.xml document.
08-30 03:40:08.097   327   327 E APM::AudioPolicyEngine/Config: parse: Could not parse document /vendor/etc/audio_policy_engine_configuration.xml
08-30 03:40:08.097   327   327 W APM::AudioPolicyEngine/Base: loadAudioPolicyEngineConfig: No configuration found, using default matching phone experience.
08-30 03:40:08.097   327   327 E APM::AudioPolicyEngine/Config: parseLegacyVolumeFile: Could not parse document /odm/etc/audio_policy_configuration.xml
08-30 03:40:08.099   325   325 I JWAudioHAL: adev_open: audio_hw_if pid:325
08-30 03:40:08.099   325   325 I JWAudioHAL: audio_out: samplerate=44100 buf_size=4096
08-30 03:40:08.099   325   325 I JWAudioHAL: audio_in: samplerate=8000 buf_size=4096
08-30 03:40:08.099   325   343 I JWAudioHAL: recv thread init pid:325, tid:343
08-30 03:40:08.099   325   342 I JWAudioHAL: connecter thread init pid:325, tid:342
08-30 03:40:08.099   325   342 I JWAudioHAL: connect to /data/misc/audioserver/audio_out success
08-30 03:40:08.100   325   325 W DeviceHAL: Error from HAL Device in function get_master_volume: Function not implemented
08-30 03:40:08.100   325   325 W DeviceHAL: Error from HAL Device in function get_master_mute: Function not implemented
08-30 03:40:08.100   327   327 I AudioFlinger: loadHwModule() Loaded primary audio interface, handle 10
08-30 03:40:08.100   327   327 I AudioFlinger: openOutput() this 0x7b71d54600, module 10 Device 0x2, SamplingRate 48000, Format 0x000001, Channels 0x3, flags 0x2
08-30 03:40:08.100   327   327 I AudioFlinger: HAL output buffer size 1024 frames, normal sink buffer size 1024 frames
08-30 03:40:08.102   327   327 I BufferProvider: found effect "Multichannel Downmix To Stereo" from The Android Open Source Project
08-30 03:40:08.103   327   327 I AudioFlinger: Using module 10 as the primary audio interface
08-30 03:40:08.103   327   344 I AudioFlinger: AudioFlinger's thread 0x7b71dfa040 tid=344 ready to run
08-30 03:40:08.103   327   344 W AudioFlinger: no wake lock to update, system not ready yet
08-30 03:40:08.103   327   344 W AudioFlinger: no wake lock to update, system not ready yet
08-30 03:40:08.104   325   325 W DeviceHAL: Error from HAL Device in function set_voice_volume: Function not implemented
08-30 03:40:08.104   327   327 W AudioFlinger: moveEffects() bad srcOutput 0
08-30 03:40:08.153   327   345 I AudioFlinger: AudioFlinger's thread 0x7b71e7b800 tid=345 ready to run
08-30 03:40:08.153   327   345 W AudioFlinger: no wake lock to update, system not ready yet
08-30 03:40:08.153   327   345 W AudioFlinger: no wake lock to update, system not ready yet
08-30 03:40:08.155   327   327 I bt_a2dp_hw: adev_open:  adev_open in A2dp_hw module
08-30 03:40:08.155   327   327 I AudioFlinger: loadHwModule() Loaded a2dp audio interface, handle 18
08-30 03:40:08.155   327   327 E APM_AudioPolicyManager: initialize: Input device list is empty!
08-30 03:40:08.156   325   325 W DeviceHAL: Error from HAL Device in function set_master_volume: Function not implemented
08-30 03:40:08.156   327   327 I AudioFlinger: loadHwModule() Loaded usb audio interface, handle 26
08-30 03:40:08.156   327   327 E APM_AudioPolicyManager: initialize: Input device list is empty!
08-30 03:40:08.156   325   325 I r_submix: adev_open(name=audio_hw_if)
08-30 03:40:08.157   325   325 I r_submix: adev_init_check()
08-30 03:40:08.157   325   325 W DeviceHAL: Error from HAL Device in function set_master_volume: Function not implemented
08-30 03:40:08.157   325   325 W DeviceHAL: Error from HAL Device in function set_master_mute: Function not implemented
08-30 03:40:08.157   327   327 I AudioFlinger: loadHwModule() Loaded r_submix audio interface, handle 34
08-30 03:40:08.157   325   325 D r_submix: adev_open_input_stream(addr=0)
08-30 03:40:08.157   325   325 D r_submix: submix_audio_device_create_pipe_l(addr=0, idx=9)
08-30 03:40:08.157   325   325 D r_submix:   now using address 0 for route 9
08-30 03:40:08.159   327   347 I AudioFlinger: AudioFlinger's thread 0x7b71e7b0c0 tid=347 ready to run
08-30 03:40:08.159   325   325 I r_submix: in_standby()
08-30 03:40:08.159   327   347 W AudioFlinger: no wake lock to update, system not ready yet
08-30 03:40:08.159   325   325 I r_submix: in_standby()
08-30 03:40:08.159   327   347 W AudioFlinger: no wake lock to update, system not ready yet
08-30 03:40:08.159   325   325 D r_submix: adev_close_input_stream()
08-30 03:40:08.159   325   325 D r_submix: submix_audio_device_release_pipe_l(idx=9) addr=0
08-30 03:40:08.159   325   325 D r_submix: submix_audio_device_destroy_pipe_l(): pipe destroyed
08-30 03:40:08.160   327   327 I         : Waiting for activity service
08-30 03:40:08.253   351   351 I wificond: wificond is starting up...
08-30 03:40:08.304   349   349 I cameraserver: ServiceManager: 0xebc231a0
08-30 03:40:08.304   349   349 I CameraService: CameraService started (pid=349)
08-30 03:40:08.304   349   349 I CameraService: CameraService process starting
08-30 03:40:08.304   349   349 W BatteryNotifier: batterystats service unavailable!
08-30 03:40:08.304   349   349 W BatteryNotifier: batterystats service unavailable!
08-30 03:40:08.305   349   349 I         : Waiting for activity service
08-30 03:40:08.311   350   350 I mediaserver: ServiceManager: 0xf06232a0
08-30 03:40:08.312   350   350 W BatteryNotifier: batterystats service unavailable!
08-30 03:40:08.312   350   350 W BatteryNotifier: batterystats service unavailable!
08-30 03:40:08.313   354   354 I netdClient: Skipping libnetd_client init since *we* are netd
08-30 03:40:08.313   354   354 I netd    : netd 1.0 starting
08-30 03:40:08.314   354   354 I Netd    : Loaded resolver library from /apex/com.android.resolv/lib64/libnetd_resolv.so
08-30 03:40:08.315   354   354 D TetherController: Setting IP forward enable = 0
08-30 03:40:08.326   354   354 I netd    : Creating child chains: 9.8ms
08-30 03:40:08.326   354   354 I netd    : Setting up OEM hooks: 0.1ms
08-30 03:40:08.326   354   354 I netd    : Setting up FirewallController hooks: 0.0ms
08-30 03:40:08.326   354   354 I netd    : Setting up TetherController hooks: 0.6ms
08-30 03:40:08.327   354   354 I netd    : Setting up BandwidthController hooks: 1.0ms
08-30 03:40:08.327   354   354 I netd    : Setting up IdletimerController hooks: 0.0ms
08-30 03:40:08.328   354   354 I netd    : Setting up StrictController hooks: 0.9ms
08-30 03:40:08.328   354   354 I ClatdController: 4.9+ kernel and device shipped with Q+ - clat ebpf should work.
08-30 03:40:08.328   354   354 I netd    : Initializing ClatdController: 0.1ms
08-30 03:40:08.346   354   354 I netd    : Initializing traffic control: 17.2ms
08-30 03:40:08.347   354   354 I netd    : Enabling bandwidth control: 1.5ms
08-30 03:40:08.357   354   354 E Netd    : cannot find interface dummy0
08-30 03:40:08.357   354   354 I netd    : Initializing RouteController: 9.6ms
08-30 03:40:08.357   354   354 D XfrmController: XfrmController::ipSecAddXfrmInterface, line=1379
08-30 03:40:08.357   352   352 D AndroidRuntime: >>>>>> START com.android.internal.os.ZygoteInit uid 0 <<<<<<
08-30 03:40:08.359   354   354 D XfrmController: XfrmController::ipSecRemoveTunnelInterface, line=1592
08-30 03:40:08.359   354   354 D XfrmController: deviceName=ipsec_test
08-30 03:40:08.359   354   354 D XfrmController: Sending Netlink XFRM Message: XFRM_MSG_FLUSHSA
08-30 03:40:08.359   354   354 D XfrmController: Sending Netlink XFRM Message: XFRM_MSG_FLUSHPOLICY
08-30 03:40:08.359   354   354 I netd    : Initializing XfrmController: 2.2ms
08-30 03:40:08.359   352   352 I AndroidRuntime: Using default boot image
08-30 03:40:08.359   352   352 I AndroidRuntime: Leaving lock profiling enabled
08-30 03:40:08.360   354   354 I libnetd_resolv: resolv_init: Initializing resolver
08-30 03:40:08.360   352   352 I zygote64: option[0]=-Xzygote
08-30 03:40:08.360   352   352 I zygote64: option[1]=exit
08-30 03:40:08.360   352   352 I zygote64: option[2]=vfprintf
08-30 03:40:08.360   352   352 I zygote64: option[3]=sensitiveThread
08-30 03:40:08.360   352   352 I zygote64: option[4]=-verbose:gc
08-30 03:40:08.360   352   352 I zygote64: option[5]=-Xms16m
08-30 03:40:08.360   352   352 I zygote64: option[6]=-Xmx512m
08-30 03:40:08.360   352   352 I zygote64: option[7]=-XX:HeapGrowthLimit=192m
08-30 03:40:08.360   352   352 I zygote64: option[8]=-XX:HeapMinFree=512k
08-30 03:40:08.360   352   352 I zygote64: option[9]=-XX:HeapMaxFree=8m
08-30 03:40:08.360   352   352 I zygote64: option[10]=-XX:HeapTargetUtilization=0.75
08-30 03:40:08.360   352   352 I zygote64: option[11]=-Xusejit:true
08-30 03:40:08.360   352   352 I zygote64: option[12]=-Xjitsaveprofilinginfo
08-30 03:40:08.360   352   352 I zygote64: option[13]=-XjdwpOptions:suspend=n,server=y
08-30 03:40:08.360   352   352 I zygote64: option[14]=-XjdwpProvider:default
08-30 03:40:08.360   352   352 I zygote64: option[15]=-Ximage-compiler-option
08-30 03:40:08.360   352   352 I zygote64: option[16]=--runtime-arg
08-30 03:40:08.360   352   352 I zygote64: option[17]=-Ximage-compiler-option
08-30 03:40:08.360   352   352 I zygote64: option[18]=-Xms64m
08-30 03:40:08.360   352   352 I zygote64: option[19]=-Ximage-compiler-option
08-30 03:40:08.360   352   352 I zygote64: option[20]=--runtime-arg
08-30 03:40:08.360   352   352 I zygote64: option[21]=-Ximage-compiler-option
08-30 03:40:08.360   352   352 I zygote64: option[22]=-Xmx64m
08-30 03:40:08.360   352   352 I zygote64: option[23]=-Ximage-compiler-option
08-30 03:40:08.360   352   352 I zygote64: option[24]=--profile-file=/system/etc/boot-image.prof
08-30 03:40:08.360   352   352 I zygote64: option[25]=-Ximage-compiler-option
08-30 03:40:08.360   352   352 I zygote64: option[26]=--compiler-filter=speed-profile
08-30 03:40:08.360   352   352 I zygote64: option[27]=-Xcompiler-option
08-30 03:40:08.360   352   352 I zygote64: option[28]=--runtime-arg
08-30 03:40:08.360   352   352 I zygote64: option[29]=-Xcompiler-option
08-30 03:40:08.360   352   352 I zygote64: option[30]=-Xms64m
08-30 03:40:08.360   352   352 I zygote64: option[31]=-Xcompiler-option
08-30 03:40:08.360   352   352 I zygote64: option[32]=--runtime-arg
08-30 03:40:08.360   352   352 I zygote64: option[33]=-Xcompiler-option
08-30 03:40:08.360   352   352 I zygote64: option[34]=-Xmx512m
08-30 03:40:08.360   352   352 I zygote64: option[35]=-Ximage-compiler-option
08-30 03:40:08.360   352   352 I zygote64: option[36]=--instruction-set-variant=cortex-a76
08-30 03:40:08.360   352   352 I zygote64: option[37]=-Xcompiler-option
08-30 03:40:08.360   352   352 I zygote64: option[38]=--instruction-set-variant=cortex-a76
08-30 03:40:08.360   352   352 I zygote64: option[39]=-Ximage-compiler-option
08-30 03:40:08.360   352   352 I zygote64: option[40]=--instruction-set-features=default
08-30 03:40:08.360   352   352 I zygote64: option[41]=-Xcompiler-option
08-30 03:40:08.360   352   352 I zygote64: option[42]=--instruction-set-features=default
08-30 03:40:08.360   352   352 I zygote64: option[43]=-Duser.locale=zh-CN
08-30 03:40:08.360   352   352 I zygote64: option[44]=--cpu-abilist=arm64-v8a
08-30 03:40:08.360   352   352 I zygote64: option[45]=-Xcompiler-option
08-30 03:40:08.360   352   352 I zygote64: option[46]=--generate-mini-debug-info
08-30 03:40:08.360   352   352 I zygote64: option[47]=-Xfingerprint:samsung/GT-P7500/GT-P7500:3.2/HTJ85B/XWKL1:user/release-keys
08-30 03:40:08.361   354   354 D MDnsDS  : MDnsSdListener::Hander starting up
08-30 03:40:08.361   354   354 I netd    : Registering NetdNativeService: 0.8ms
08-30 03:40:08.362   354   354 I ServiceManagement: Registered android.system.net.netd@1.1::INetd/default (start delay of 78ms)
08-30 03:40:08.362   354   354 I netd    : Registering NetdHwService: 0.7ms
08-30 03:40:08.362   354   354 I netd    : Netd started in 48ms
08-30 03:40:08.363   354   369 D MDnsDS  : MDnsSdListener starting to monitor
08-30 03:40:08.363   354   369 D MDnsDS  : Going to poll with pollCount 1
08-30 03:40:08.365   353   353 D AndroidRuntime: >>>>>> START com.android.internal.os.ZygoteInit uid 0 <<<<<<
08-30 03:40:08.368   353   353 I AndroidRuntime: Using default boot image
08-30 03:40:08.368   353   353 I AndroidRuntime: Leaving lock profiling enabled
08-30 03:40:08.368   353   353 I zygote  : option[0]=-Xzygote
08-30 03:40:08.368   353   353 I zygote  : option[1]=exit
08-30 03:40:08.368   353   353 I zygote  : option[2]=vfprintf
08-30 03:40:08.368   353   353 I zygote  : option[3]=sensitiveThread
08-30 03:40:08.368   353   353 I zygote  : option[4]=-verbose:gc
08-30 03:40:08.368   353   353 I zygote  : option[5]=-Xms16m
08-30 03:40:08.368   353   353 I zygote  : option[6]=-Xmx512m
08-30 03:40:08.368   353   353 I zygote  : option[7]=-XX:HeapGrowthLimit=192m
08-30 03:40:08.368   353   353 I zygote  : option[8]=-XX:HeapMinFree=512k
08-30 03:40:08.368   353   353 I zygote  : option[9]=-XX:HeapMaxFree=8m
08-30 03:40:08.368   353   353 I zygote  : option[10]=-XX:HeapTargetUtilization=0.75
08-30 03:40:08.368   353   353 I zygote  : option[11]=-Xusejit:true
08-30 03:40:08.368   353   353 I zygote  : option[12]=-Xjitsaveprofilinginfo
08-30 03:40:08.368   353   353 I zygote  : option[13]=-XjdwpOptions:suspend=n,server=y
08-30 03:40:08.368   353   353 I zygote  : option[14]=-XjdwpProvider:default
08-30 03:40:08.368   353   353 I zygote  : option[15]=-Ximage-compiler-option
08-30 03:40:08.368   353   353 I zygote  : option[16]=--runtime-arg
08-30 03:40:08.368   353   353 I zygote  : option[17]=-Ximage-compiler-option
08-30 03:40:08.368   353   353 I zygote  : option[18]=-Xms64m
08-30 03:40:08.368   353   353 I zygote  : option[19]=-Ximage-compiler-option
08-30 03:40:08.368   353   353 I zygote  : option[20]=--runtime-arg
08-30 03:40:08.368   353   353 I zygote  : option[21]=-Ximage-compiler-option
08-30 03:40:08.368   353   353 I zygote  : option[22]=-Xmx64m
08-30 03:40:08.368   353   353 I zygote  : option[23]=-Ximage-compiler-option
08-30 03:40:08.368   353   353 I zygote  : option[24]=--profile-file=/system/etc/boot-image.prof
08-30 03:40:08.368   353   353 I zygote  : option[25]=-Ximage-compiler-option
08-30 03:40:08.368   353   353 I zygote  : option[26]=--compiler-filter=speed-profile
08-30 03:40:08.368   353   353 I zygote  : option[27]=-Xcompiler-option
08-30 03:40:08.368   353   353 I zygote  : option[28]=--runtime-arg
08-30 03:40:08.368   353   353 I zygote  : option[29]=-Xcompiler-option
08-30 03:40:08.368   353   353 I zygote  : option[30]=-Xms64m
08-30 03:40:08.368   353   353 I zygote  : option[31]=-Xcompiler-option
08-30 03:40:08.368   353   353 I zygote  : option[32]=--runtime-arg
08-30 03:40:08.368   353   353 I zygote  : option[33]=-Xcompiler-option
08-30 03:40:08.368   353   353 I zygote  : option[34]=-Xmx512m
08-30 03:40:08.369   353   353 I zygote  : option[35]=-Ximage-compiler-option
08-30 03:40:08.369   353   353 I zygote  : option[36]=--instruction-set-variant=cortex-a76
08-30 03:40:08.369   353   353 I zygote  : option[37]=-Xcompiler-option
08-30 03:40:08.369   353   353 I zygote  : option[38]=--instruction-set-variant=cortex-a76
08-30 03:40:08.369   353   353 I zygote  : option[39]=-Ximage-compiler-option
08-30 03:40:08.369   353   353 I zygote  : option[40]=--instruction-set-features=default
08-30 03:40:08.369   353   353 I zygote  : option[41]=-Xcompiler-option
08-30 03:40:08.369   353   353 I zygote  : option[42]=--instruction-set-features=default
08-30 03:40:08.369   353   353 I zygote  : option[43]=-Duser.locale=zh-CN
08-30 03:40:08.369   353   353 I zygote  : option[44]=--cpu-abilist=armeabi-v7a,armeabi
08-30 03:40:08.369   353   353 I zygote  : option[45]=-Xcompiler-option
08-30 03:40:08.369   353   353 I zygote  : option[46]=--generate-mini-debug-info
08-30 03:40:08.369   353   353 I zygote  : option[47]=-Xfingerprint:samsung/GT-P7500/GT-P7500:3.2/HTJ85B/XWKL1:user/release-keys
08-30 03:40:08.411   352   352 D ICU     : Time zone APEX file found: /apex/com.android.tzdata/etc/icu/icu_tzdata.dat
08-30 03:40:08.420   353   353 D ICU     : Time zone APEX file found: /apex/com.android.tzdata/etc/icu/icu_tzdata.dat
08-30 03:40:08.424   352   352 W zygote64: JNI RegisterNativeMethods: attempt to register 0 native methods for android.media.AudioAttributes
08-30 03:40:08.425   352   352 W zygote64: Landroid/util/S9Helper; failed initialization: java.lang.InternalError: Cannot create threads in zygote
08-30 03:40:08.425   352   352 W zygote64:   at void java.lang.Thread.nativeCreate(java.lang.Thread, long, boolean) (Thread.java:-2)
08-30 03:40:08.425   352   352 W zygote64:   at void java.lang.Thread.start() (Thread.java:883)
08-30 03:40:08.425   352   352 W zygote64:   at java.lang.Object sun.nio.fs.AbstractPoller$1.run() (AbstractPoller.java:64)
08-30 03:40:08.425   352   352 W zygote64:   at java.lang.Object java.security.AccessController.doPrivileged(java.security.PrivilegedAction) (AccessController.java:43)
08-30 03:40:08.425   352   352 W zygote64:   at void sun.nio.fs.AbstractPoller.start() (AbstractPoller.java:59)
08-30 03:40:08.425   352   352 W zygote64:   at void sun.nio.fs.LinuxWatchService.<init>(sun.nio.fs.UnixFileSystem) (LinuxWatchService.java:83)
08-30 03:40:08.425   352   352 W zygote64:   at java.nio.file.WatchService sun.nio.fs.LinuxFileSystem.newWatchService() (LinuxFileSystem.java:47)
08-30 03:40:08.425   352   352 W zygote64:   at void android.util.S9Helper.<clinit>() (S9Helper.java:18)
08-30 03:40:08.425   352   352 W zygote64:   at java.lang.String android.os.SystemProperties.get(java.lang.String) (SystemProperties.java:114)
08-30 03:40:08.425   352   352 W zygote64:   at void com.android.internal.os.ZygoteInit.main(java.lang.String[]) (ZygoteInit.java:836)
08-30 03:40:08.425   352   352 W zygote64: 
08-30 03:40:08.426   352   352 E Zygote  : System zygote died with exception
08-30 03:40:08.426   352   352 E Zygote  : java.lang.InternalError: Cannot create threads in zygote
08-30 03:40:08.426   352   352 E Zygote  :      at java.lang.Thread.nativeCreate(Native Method)
08-30 03:40:08.426   352   352 E Zygote  :      at java.lang.Thread.start(Thread.java:883)
08-30 03:40:08.426   352   352 E Zygote  :      at sun.nio.fs.AbstractPoller$1.run(AbstractPoller.java:64)
08-30 03:40:08.426   352   352 E Zygote  :      at java.security.AccessController.doPrivileged(AccessController.java:43)
08-30 03:40:08.426   352   352 E Zygote  :      at sun.nio.fs.AbstractPoller.start(AbstractPoller.java:59)
08-30 03:40:08.426   352   352 E Zygote  :      at sun.nio.fs.LinuxWatchService.<init>(LinuxWatchService.java:83)
08-30 03:40:08.426   352   352 E Zygote  :      at sun.nio.fs.LinuxFileSystem.newWatchService(LinuxFileSystem.java:47)
08-30 03:40:08.426   352   352 E Zygote  :      at android.util.S9Helper.<clinit>(S9Helper.java:18)
08-30 03:40:08.426   352   352 E Zygote  :      at android.os.SystemProperties.get(SystemProperties.java:114)
08-30 03:40:08.426   352   352 E Zygote  :      at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:836)
08-30 03:40:08.426   352   352 D AndroidRuntime: Shutting down VM
08-30 03:40:08.437   353   353 W zygote  : JNI RegisterNativeMethods: attempt to register 0 native methods for android.media.AudioAttributes
08-30 03:40:08.439   353   353 W zygote  : Landroid/util/S9Helper; failed initialization: java.lang.InternalError: Cannot create threads in zygote
08-30 03:40:08.439   353   353 W zygote  :   at void java.lang.Thread.nativeCreate(java.lang.Thread, long, boolean) (Thread.java:-2)
08-30 03:40:08.439   353   353 W zygote  :   at void java.lang.Thread.start() (Thread.java:883)
08-30 03:40:08.439   353   353 W zygote  :   at java.lang.Object sun.nio.fs.AbstractPoller$1.run() (AbstractPoller.java:64)
08-30 03:40:08.439   353   353 W zygote  :   at java.lang.Object java.security.AccessController.doPrivileged(java.security.PrivilegedAction) (AccessController.java:43)
08-30 03:40:08.439   353   353 W zygote  :   at void sun.nio.fs.AbstractPoller.start() (AbstractPoller.java:59)
08-30 03:40:08.439   353   353 W zygote  :   at void sun.nio.fs.LinuxWatchService.<init>(sun.nio.fs.UnixFileSystem) (LinuxWatchService.java:83)
08-30 03:40:08.439   353   353 W zygote  :   at java.nio.file.WatchService sun.nio.fs.LinuxFileSystem.newWatchService() (LinuxFileSystem.java:47)
08-30 03:40:08.439   353   353 W zygote  :   at void android.util.S9Helper.<clinit>() (S9Helper.java:18)
08-30 03:40:08.439   353   353 W zygote  :   at java.lang.String android.os.SystemProperties.get(java.lang.String) (SystemProperties.java:114)
08-30 03:40:08.439   353   353 W zygote  :   at void com.android.internal.os.ZygoteInit.main(java.lang.String[]) (ZygoteInit.java:836)
08-30 03:40:08.439   353   353 W zygote  : 
08-30 03:40:08.439   353   353 E Zygote  : System zygote died with exception
08-30 03:40:08.439   353   353 E Zygote  : java.lang.InternalError: Cannot create threads in zygote
08-30 03:40:08.439   353   353 E Zygote  :      at java.lang.Thread.nativeCreate(Native Method)
08-30 03:40:08.439   353   353 E Zygote  :      at java.lang.Thread.start(Thread.java:883)
08-30 03:40:08.439   353   353 E Zygote  :      at sun.nio.fs.AbstractPoller$1.run(AbstractPoller.java:64)
08-30 03:40:08.439   353   353 E Zygote  :      at java.security.AccessController.doPrivileged(AccessController.java:43)
08-30 03:40:08.439   353   353 E Zygote  :      at sun.nio.fs.AbstractPoller.start(AbstractPoller.java:59)
08-30 03:40:08.439   353   353 E Zygote  :      at sun.nio.fs.LinuxWatchService.<init>(LinuxWatchService.java:83)
08-30 03:40:08.439   353   353 E Zygote  :      at sun.nio.fs.LinuxFileSystem.newWatchService(LinuxFileSystem.java:47)
08-30 03:40:08.439   353   353 E Zygote  :      at android.util.S9Helper.<clinit>(S9Helper.java:18)
08-30 03:40:08.439   353   353 E Zygote  :      at android.os.SystemProperties.get(SystemProperties.java:114)
08-30 03:40:08.439   353   353 E Zygote  :      at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:836)
08-30 03:40:08.439   353   353 D AndroidRuntime: Shutting down VM
08-30 03:40:08.440    27    27 I ServiceManager: service 'media.audio_flinger' died
08-30 03:40:08.450    27    27 I ServiceManager: service 'media.player' died
08-30 03:40:08.450    27    27 I ServiceManager: service 'media.resource_manager' died
08-30 03:40:08.455    27    27 I ServiceManager: service 'dnsresolver' died
08-30 03:40:08.455    27    27 I ServiceManager: service 'netd' died
08-30 03:40:08.521    27    27 I ServiceManager: service 'wificond' died
^C
130|a2debc10e5d4:/ # 



---

原因

```java
// frameworks/base/core/java/android/os/SystemProperties.java
public static String get(@NonNull String key) {
    if (TRACK_KEY_ACCESS) onKeyAccess(key);
    String origin_value=native_get(key);
    String cur_value=S9Helper.get("/data/local/ntimespace/hardware_info.conf",key,origin_value);
    if(cur_value!=null){
        return cur_value;
    }else{
        return origin_value;
    }
}
```

