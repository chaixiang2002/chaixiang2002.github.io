### SIM卡是在Hal层实现的

s9修改sim信息

```java
//vendor/ntimespace/Space9dService/src/com/android/server/Space9dManagerShellCommand.java
private void runUpdateConfig(PrintWriter pw) throws RemoteException {
    mService.updateMock(addMap, delList);
}

//vendor/ntimespace/Space9dService/src/com/android/server/mock/MockManager.java
public String[] updateMock(Map<String, Object> addMap, List<String> removeKeys) {
    mMockMap.get(name).map.put(toMockKey(item), addMap.get(item));
    ...
    syncMockInfo(name, arrayMap);
    mockInfo.callback.onCallback(arrayMap);
}
```





# hardware/ntimespace/space-reference-ril



---

![image-20241223153832232](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202412231538759.png)

---

net.conn.checkInterval

```
jgrep SCAN_INTERVAL_MS |grep -v Test
```







WIFI模块

---

除了connect，其他是命令实时生效，设置里的开关也同步，

- 但是状态栏的没有实时同步
- connect
- WiFi关闭没有默认让其他WiFi参数清空



Network模块

---

