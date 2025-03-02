

systemctl stop docker

一定要关闭docker服务

```json
先vi编辑文件再    :%!python3 -m json.tool


antdock:/userdata/ant/containers/bef0fbd771d1fd663d6ff371b07dd256ae627274cc4a3659d6f3ce2e20acfcae# vim hostconfig.json 


    "Binds": [
        "/userdata/container/android_data/data_3:/data:rw",
        "/var/lib/lxcfs/proc/meminfo:/proc/meminfo:rw",
        "/userdata/arm-agent/mount/default/vendor/etc/container/container_common.conf:/vendor/etc/container/container_common.conf:rw",
        "/userdata/arm-agent/mount/3/vendor/etc/container/container.conf:/vendor/etc/container/container.conf:rw",
        "/userdata/arm-agent/mount/3/system/etc/default_mock.prop:/system/etc/default_mock.prop:rw",
        "/userdata/arm-agent/mount/3/system/etc/default_radio.conf:/system/etc/default_radio.conf:rw",
        "/userdata/arm-agent/mount/3/system/etc/Launcher3:/system/etc/Launcher3:rw",
        "/userdata/arm-agent/mount/3/vendor/app:/vendor/app:rw"
    ],
      

antdock:/userdata/ant/containers/bef0fbd771d1fd663d6ff371b07dd256ae627274cc4a3659d6f3ce2e20acfcae# vim config.v2.json
    "MountPoints": {
        "/vendor/app": {
            "Source": "/userdata/arm-agent/mount/3/vendor/app",
            "Destination": "/vendor/app",
            "RW": true,
            "Name": "",
            "Driver": "",
            "Type": "bind",
            "Propagation": "rprivate",
            "Spec": {
                "Type": "bind",
                "Source": "/userdata/arm-agent/mount/3/vendor/app",
                "Target": "/vendor/app"
            },
            "SkipMountpointCreation": false
        },


```

