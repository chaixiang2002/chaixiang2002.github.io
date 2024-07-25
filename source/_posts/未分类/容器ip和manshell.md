地址：192.168.168.147:/root/manage-shell

ip:

启动参数：./android_ctl.sh start 0 --images=xxx

macvlan

/userdata/init-in-arm/sh/build_image.sh

./build_image.sh /userdata/snow/rk3588_docker-android10-user-super.img-20240511.0228.tgz

/userdata/arm-agent/bin/manage-shell

./android_ctl.sh restart 0 --image=latest

修改容器名

root@AntDock:/data/arm-agent/bin/manage-shell# vim android_common.env

cd /userdata/snow/manage-shell
  519  clear
  520  ls
  521  cd ..
  522  rm -rf manage-shell/
  523  scp -r 192.168.168.147:/root/manage-shell .
  524  cd manage-shell/
  525  ls
  526  rm -rf .git
  527  ls
  528  rm -rf docker-net-test/
  529  ls
  530  docker images
  531  cd ..
  532  ls
  533  cd ..
  534  ls
  535  ps -ef
  536  ps -ef
  537  ps -ef |grep arm-agent
  538  cd -
  539  ls
  540  docker ps
  541  cd ..
  542  cd arm-agent/bin/manage-shell/
  543  ls
  544  docker images
  545  cd ~
  546  ls
  547  ls
  548  cd /userdata/
  549  ls
  550  ssh 192.168.168.147 ls /root/arm-init-shell/init-in-linx
  551  ssh 192.168.168.147 ls /root/arm-init-shell/
  552  scp -r 192.168.168.147:/root/arm-init-shell/init-in-arm .
  553  cd init-
  554  cd init-in-arm/
  555  ls
  556  cd sh/
  557  ./build_image.sh /userdata/snow/rk3588_docker-android10-user-super.img-20240511.0228.tgz
  558  ls
  559  cd ../../
  560  cd arm-agent/bin/manage-shell/
  561  ./android_ctl.sh restart 0 --image=latest
  562  docker exec -it android_0 /system/bin/sh
  563  history



./android_ctl.sh start 0 --mac=7c:2a:14:3b:35:da --ip=192.168.30.35 --cpu=0 --gpu=0 --ram=0 --rom=0 --imei=863935410512281 --androidId=46af8b6feb561edc --serialNo=01MM0Q99SUN9 --wifiMac=04:6d:1c:01:12:9d --brand=Google --model=Pixel 2 --gateway=192.168.30.1 --subnet=192.168.30.0/24 --instanceId=92870289188257794

--image=latest
