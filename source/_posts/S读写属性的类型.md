###  WiFiMock获取Map
**frameworks/base/core/java/com/android/internal/space/api/WiFiMock.java**

 int netType = (int) mMap.getOrDefault("active_network", ConnectivityManager.TYPE_WIFI);

- public void onCallback(Map map) 
  - this.mMap = map;
- mMap = mSpaceService.addMockCallback(NAME, this)

**vendor/ntimespace/Space9dService/src/com/android/server/Space9dManagerService.java**

  public Map addMockCallback(String name, IMockCallback callback) throws RemoteException

- return mMockManager.addMockCallback(name, callback);

**vendor/ntimespace/Space9dService/src/com/android/server/mock/MockManager.java**

public Map<String, Object> addMockCallback(String name, IMockCallback callback)

- mockInfo = mMockMap.get(name);

private void loadMockInfo()

- mockInfo.map.putAll(CommonHelper.readMapFile(path));





### s9命令写入mock

**vendor/ntimespace/Space9dService/src/com/android/server/Space9dManagerShellCommand.java**

private void runUpdateConfig(PrintWriter pw) throws RemoteException

- String[] mockModules = mService.updateMock(addMap, delList);

vendor/ntimespace/Space9dService/src/com/android/server/mock/MockManager.java

public String[] updateMock(Map<String, Object> addMap, List<String> removeKeys)

- mMockMap.get(name).map.put(toMockKey(item), addMap.get(item));





---

**vendor/ntimespace/Space9dService/src/com/android/server/mock/MockManager.java**

public String[] updateMock(Map<String, Object> addMap, List<String> removeKeys)

-  syncMockInfo(name, arrayMap);

- private void syncMockInfo(String name, Map<String, Object> map)
  -  CommonHelper.writeMapToFile(path, map);

**vendor/ntimespace/Space9dService/src/com/android/server/comm/CommonHelper.java**

```java
    public static void writeMapToFile(String filePath, Map<String, Object> map) {
        try (BufferedWriter bw = new BufferedWriter(new FileWriter(filePath))) {
            Object val;
            String type;
            for (Map.Entry<String, Object> entry : map.entrySet()) {
                val = entry.getValue();
                if (val instanceof Integer) {
                    type = "int";
                } else if (val instanceof Float) {
                    type = "float";
                } else if (val instanceof Double) {
                    type = "double";
                } else if (val instanceof Long) {
                    type = "long";
                } else if (val instanceof Boolean) {
                    type = "boolean";
                } else {
                    type = "string";
                }
                String line = type + ":" + entry.getKey() + "=" + val;
                bw.write(line);
                bw.newLine();
            }
        } catch (IOException e) {
            Slog.w(TAG, "writeMapToFile: " + e.getMessage());
        }
    }
```

