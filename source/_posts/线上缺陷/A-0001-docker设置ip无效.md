```
IMAGE_0=rk3588:user-adb-lyt-root12041358
MEM_UPPER_LIMIT_0=0
MEM_LOWER_LIMIT_0=0
CPUS_0=0
CPUSET_0=1-7
MAC_0=6c:4a:e0:c5:ab:ce
IP_0=192.168.168.50
QUOTA_LIMIT_0=0



services:
  "android_0":
    container_name: ${CONTAINER_NAME_PRE}0
    image: ${IMAGE_0}
    stdin_open: true
    restart: unless-stopped
    privileged: true
    cpuset: ${CPUSET_0}
    volumes:
      - ${ANDROID_DATA_DIR}/data_0:/data:rw
      - /var/lib/lxcfs/proc/meminfo:/proc/meminfo:rw
      - /userdata/arm-agent/mount/0/system/etc/scripts/init:/system/etc/scripts/init:rw
      - /userdata/arm-agent/mount/default/business_script:/data/local/business_script:rwx
    environment:
      - SELF_ID=0
    ports:
      - "1100:5555"
    deploy:
      resources:
        limits:
          memory: ${MEM_UPPER_LIMIT_0}
          cpus: '${CPUS_0}'
        reservations:
          memory: ${MEM_LOWER_LIMIT_0}
    networks:
      android-mac:
        ipv4_address: 192.168.168.50
        mac_address: ${MAC_0}
```





```shell
[2024-12-04 14:26:16] INFO Instruction snapshot: /userdata/arm-agent/bin/manage-shell/android_ctl.sh reset 0 --image=latest
[2024-12-04 14:26:16] INFO Android_0 is resetting.
[2024-12-04 14:26:16] INFO android_0 is running
[2024-12-04 14:26:16] INFO Executing command: docker compose -f docker-compose.yml -f /userdata/arm-agent/mount/metadata/0.yml down android_0
[2024-12-04 14:26:23] INFO Instruction snapshot: manage-shell/android_ctl.sh status 0
[2024-12-04 14:26:23] INFO Start acquiring Android_0 status.
[2024-12-04 14:26:23] INFO android_0 is running
[2024-12-04 14:26:27] INFO Command output:
 Container android_0  Stopping
 Container android_0  Stopped
 Container android_0  Removing
 Container android_0  Removed
 Network android-mac  Removing
 Network android-mac  Resource is still in use
[2024-12-04 14:26:27] INFO Command succeeded.
[2024-12-04 14:26:27] INFO Remove container android_0 success
[2024-12-04 14:26:27] INFO Executing command: rm -rf /userdata/container/android_data/data_0/*
[2024-12-04 14:26:27] INFO Command output:

[2024-12-04 14:26:27] INFO Command succeeded.
[2024-12-04 14:26:27] INFO Executing command: rm -f ./parmater_history/0.conf
[2024-12-04 14:26:27] INFO Command output:

[2024-12-04 14:26:27] INFO Command succeeded.
[2024-12-04 14:26:27] INFO get start lock for android_0 success
[2024-12-04 14:26:27] INFO android_0 is not exist
[2024-12-04 14:26:28] INFO Parmater [image] changed [] -> [rk3588:RK_ANDROID10-RKR14-huangkb11271143]
[2024-12-04 14:26:28] INFO Parmater [image] changed [] -> [rk3588:user-adb-lyt-root12041358]
[2024-12-04 14:26:28] INFO Configing for parameter: image
[2024-12-04 14:26:28] INFO Executing command: ./sh/set_image.sh 0 rk3588:user-adb-lyt-root12041358
[2024-12-04 14:26:28] INFO Command output:
image not changed, container id: 0, image: rk3588:user-adb-lyt-root12041358
[2024-12-04 14:26:28] INFO Command succeeded.
[2024-12-04 14:26:28] INFO Executing command: docker compose -f docker-compose.yml -f /userdata/arm-agent/mount/metadata/0.yml up android_0 -d
[2024-12-04 14:26:28] INFO Command output:
time="2024-12-04T14:26:28+08:00" level=warning msg="Found orphan containers ([android_3 android_2 android_1]) for this project. If you removed or renamed this service in your compose file, you can run this command with the --remove-orphans flag to clean it up."
 Container android_0  Creating
 Container android_0  Created
 Container android_0  Starting
 Container android_0  Started
[2024-12-04 14:26:28] INFO Command succeeded.
[2024-12-04 14:26:58] INFO Instruction snapshot: manage-shell/android_ctl.sh status 0
[2024-12-04 14:26:58] INFO Start acquiring Android_0 status.
[2024-12-04 14:26:58] INFO android_0 is running
[2024-12-04 14:27:33] INFO Instruction snapshot: manage-shell/android_ctl.sh status 0
[2024-12-04 14:27:33] INFO Start acquiring Android_0 status.
[2024-12-04 14:27:33] INFO android_0 is running
[2024-12-04 14:28:08] INFO Instruction snapshot: manage-shell/android_ctl.sh status 0
[2024-12-04 14:28:08] INFO Start acquiring Android_0 status.
[2024-12-04 14:28:08] INFO android_0 is running
[2024-12-04 14:28:43] INFO Instruction snapshot: manage-shell/android_ctl.sh status 0
[2024-12-04 14:28:43] INFO Start acquiring Android_0 status.
[2024-12-04 14:28:43] INFO android_0 is running
[2024-12-04 14:29:18] INFO Instruction snapshot: manage-shell/android_ctl.sh status 0
[2024-12-04 14:29:18] INFO Start acquiring Android_0 status.
[2024-12-04 14:29:18] INFO android_0 is running
[2024-12-04 14:29:53] INFO Instruction snapshot: manage-shell/android_ctl.sh status 0
[2024-12-04 14:29:53] INFO Start acquiring Android_0 status.
[2024-12-04 14:29:53] INFO android_0 is running
[2024-12-04 14:30:28] INFO Instruction snapshot: manage-shell/android_ctl.sh status 0
[2024-12-04 14:30:28] INFO Start acquiring Android_0 status.
[2024-12-04 14:30:28] INFO android_0 is running

```

