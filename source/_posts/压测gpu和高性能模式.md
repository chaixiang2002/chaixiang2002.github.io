```sh
antdock:/snow# cat /sys/devices/platform/fb000000.gpu/devfreq/fb000000.gpu/load
94@800000000Hz          #前面是gpu占用，后面是频率

# 开启gpu和cpu的高性能模式
antdock:/snow# echo performance > /sys/devices/system/cpu/cpufreq/policy0/scaling_governor 
echo performance > /sys/devices/system/cpu/cpufreq/policy4/scaling_governor 
echo performance > /sys/devices/system/cpu/cpufreq/policy6/scaling_governor 
echo performance > /sys/devices/platform/fb000000.gpu/devfreq/fb000000.gpu/governor 
antdock:/snow# cat /sys/devices/platform/fb000000.gpu/devfreq/fb000000.gpu/load
100@700000000Hz      
```

gpu压测网站：https://cznull.github.io/vsbm