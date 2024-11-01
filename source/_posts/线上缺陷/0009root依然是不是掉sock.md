发送端

// vendor/ntimespace/proc_watcher/GrantRoot.cpp

```c++
bool GrantRoot::checkRootable() {
  ALOGI("root---checkRootable(");

  char buffer[64];
  char data[48];

  int length;
  char response = 0;
  bool result;

  SocketConnection socket;
  if (!socket.doOpen("/data/system/root_sock")) {
    ALOGE("root---socket.doOpen(),failed!");
    return false;//!
  }

  memset(buffer, 0, sizeof(buffer));

  memset(data, 0, sizeof(data));
  length = snprintf(data, sizeof(data), "root:%d", mUid);
  snprintf(buffer, sizeof(buffer), "%02d|%s", length, data);

  result = socket.request(buffer, &response, sizeof(response));
  socket.doClose();
  ALOGI("root---checkRootable result: %d, response: %c ,uid:%d", result, response,mUid);
  if (!result) {
    ALOGE("root---result:%d",result);
    return false;
  }
  return response == '1';
}

```



接受端

// vendor/ntimespace/ExtProvider/src/com/android/ext/root/ManagerService.java

```java
public class ClientHandler implements Runnable {
        private final LocalSocket clientSocket;

        ClientHandler(LocalSocket clientSocket) {
            this.clientSocket = clientSocket;
        }

        @Override
        public void run() {
            try {
                InputStream inputStream = clientSocket.getInputStream();
                OutputStream outputStream = clientSocket.getOutputStream();

                byte[] sizeBytes = new byte[2];
                inputStream.read(sizeBytes);
                int length = Integer.valueOf(new String(sizeBytes));
                // ingore |
                inputStream.read();
                byte[] dataBytes = new byte[length];
                inputStream.read(dataBytes);

                String data = new String(dataBytes);
                int uid = 0;
                if (data.startsWith("root:")) {
                    uid = Integer.parseInt(data.split(":")[1]);
                }

                if (uid < Process.FIRST_APPLICATION_UID) {
                    outputStream.write("1".getBytes());
                } else if (uid >= Process.FIRST_APPLICATION_UID
                        && uid <= Process.LAST_APPLICATION_UID) {
                    String packageName = Package.getPackageNameByUid(mContext, uid);
                    Log.i("ManagerService","root----check package root packagename="+ packageName +" uid =" + uid);
                    if (packageName != null) {
                        boolean isGranted = mController.isRootApp(packageName);//!
                        Log.i("ManagerService","root---check package root packagename="+ packageName +" isGranted =" + isGranted);
                        outputStream.write((isGranted ? "1" : "0").getBytes());
                    } else {
                        outputStream.write("0".getBytes());
                    }
                } else {
                    outputStream.write("0".getBytes());
                }
                outputStream.flush();

                inputStream.close();
                outputStream.close();
                clientSocket.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
```



二者之间通讯

在这段代码中，`Grant::checkRootable` 函数和 `ClientHandler` 类之间通过 Unix socket 交换数据，具体流程如下：

### 发送数据（C++ 端）

1. **构建请求数据**：
   - `data` 字符串格式为 `"root:<mUid>"`，其中 `<mUid>` 是用户的 UID。
   - 计算长度并格式化为 `buffer`，格式为 `"<length>|<data>"`，如 `05|root:1234`（假设 UID 是 1234）。

2. **发送**：
   - 将 `buffer` 发送到 socket。

### 接收数据（Java 端）

1. **读取请求**：
   - 首先读取 2 字节，获取消息长度。
   - 跳过分隔符 `|`，然后读取实际的数据 `dataBytes`。

2. **解析数据**：
   - 将读取到的数据转换为字符串，并解析 UID。
   - 如果 UID 小于 `Process.FIRST_APPLICATION_UID`，则返回 `"1"`，表示允许根访问。
   - 如果 UID 在合法范围内，检查该 UID 对应的包名是否有根权限，返回 `"1"` 或 `"0"`。

### 交换的数据

- **C++ 端发送**：
  - 格式为 `"<length>|root:<mUid>"`，如 `05|root:1234`。
  
- **Java 端返回**：
  - 返回结果为 `"1"` 或 `"0"`，表示根权限的状态。

### ALOGD 打印

如果要使用 `ALOGD` 打印发送的数据，你可以在 C++ 中的 `checkRootable` 函数中添加如下代码：

```cpp
ALOGD("Sending data: %s", buffer);
```

这将打印出发送到 socket 的完整数据。

---

![image-20241023140359732](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202410231404496.png)

![image-20241023140415495](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202410231404311.png)

不是chmod的问题

---

线上缺陷

目前有一个线上缺陷，是安卓2个应用程序之间通过sock域通讯远程调用。

服务端

//vendor/ntimespace/ExtProvider/src/com/android/ext/root/ManagerService.java

```java
private void startListen() {
    isStart = true;

    if (mSockFd != null && mSockFd.valid()) {
        try {
            mServerSocket = new LocalServerSocket(mSockFd);
            Log.i("ManagerService", "Server socket listening...");

            mThreadPool = new ThreadPoolExecutor(
                6, // corePoolSize: Minimum number of threads to keep in the pool (0 here)
                12, // maximumPoolSize: Maximum number of threads (no upper limit here)
                10L, // keepAliveTime: Threads idle for 60 seconds are terminated
                TimeUnit.SECONDS, // keepAliveTime unit
                new SynchronousQueue<>() // Work queue: SynchronousQueue for short-lived tasks
            );

            LocalSocket socket;
            while (isStart) {
                try {
                    socket = mServerSocket.accept();
                    Log.i("ManagerService", "Client connected: " + socket.getRemoteSocketAddress());
                    mThreadPool.execute(new ClientHandler(socket));
                } catch (IOException e) {
                    Log.e("ManagerService", "Error accepting client connection: " + e.getMessage());
                }
            }

        } catch (IOException e) {
            Log.e("ManagerService", "Server socket creation failed: " + e.getMessage());
        }
    }
}

public class ClientHandler implements Runnable {
    private final LocalSocket clientSocket;

    ClientHandler(LocalSocket clientSocket) {
        this.clientSocket = clientSocket;
    }

    @Override
    public void run() {
        try {
            Log.i("ManagerService", "Handling client: " + clientSocket.getRemoteSocketAddress());
            InputStream inputStream = clientSocket.getInputStream();
            OutputStream outputStream = clientSocket.getOutputStream();

            byte[] sizeBytes = new byte[2];
            inputStream.read(sizeBytes);
            int length = Integer.valueOf(new String(sizeBytes));
            // ingore |
            inputStream.read();
            byte[] dataBytes = new byte[length];
            inputStream.read(dataBytes);

            String data = new String(dataBytes);
            int uid = 0;
            if (data.startsWith("root:")) {
                uid = Integer.parseInt(data.split(":")[1]);
            }

            if (uid < Process.FIRST_APPLICATION_UID) {
                outputStream.write("1".getBytes());
            } else if (uid >= Process.FIRST_APPLICATION_UID
                       && uid <= Process.LAST_APPLICATION_UID) {
                String packageName = Package.getPackageNameByUid(mContext, uid);
                Log.i("ManagerService", "Checking package: " + packageName + " (UID: " + uid + ")");
                if (packageName != null) {
                    boolean isGranted = mController.isRootApp(packageName);
                    Log.i("ManagerService", "Package " + packageName + " granted: " + isGranted);
                    outputStream.write((isGranted ? "1" : "0").getBytes());
                } else {
                    outputStream.write("0".getBytes());
                }
            } else {
                outputStream.write("0".getBytes());
            }
            outputStream.flush();

            inputStream.close();
            outputStream.close();
            clientSocket.close();
        } catch (IOException e) {
            Log.e("ManagerService", "Error handling client: " + e.getMessage());
        }
    }
}
```





// vendor/ntimespace/ExtProvider/jni/UnixSocket.cpp

```cpp
int createServerSocket(JNIEnv *env, jobject thiz, jstring path) {
    struct sockaddr_un server_socket;

    int sock = socket(AF_UNIX, SOCK_STREAM, 0);
    if (sock < 0) {
        return -1;
    }

    int opt = 1;
    setsockopt(sock, SOL_SOCKET, SO_REUSEADDR, &opt, sizeof(opt));

    memset(&server_socket, 0, sizeof(server_socket));
    server_socket.sun_family = AF_LOCAL;

    const char* path_c = env->GetStringUTFChars(path, NULL);
    strcpy(server_socket.sun_path, path_c);
    socklen_t socklen = strlen(path_c) + offsetof(struct sockaddr_un, sun_path);

    env->ReleaseStringUTFChars(path, path_c);

    if (bind(sock, (struct sockaddr *) &server_socket, socklen) < 0) {
        close(sock);
        return -1;
    }
    return sock;
}
```



客户端

// vendor/ntimespace/proc_watcher/GrantRoot.cpp

```cpp
bool GrantRoot::checkRootable() {
  ALOGI("root---checkRootable(");

  char buffer[64];
  char data[48];

  int length;
  char response = 0;
  bool result;

  SocketConnection socket;
  if (!socket.doOpen("/data/system/root_sock")) {
    ALOGE("root---socket.doOpen(),failed!");
    return false;
  }

  memset(buffer, 0, sizeof(buffer));

  memset(data, 0, sizeof(data));
  length = snprintf(data, sizeof(data), "root:%d", mUid);
  snprintf(buffer, sizeof(buffer), "%02d|%s", length, data);

  result = socket.request(buffer, &response, sizeof(response));
  socket.doClose();
  ALOGI("root---checkRootable result: %d, response: %c ,uid:%d", result, response,mUid);
  if (!result) {
    ALOGE("root---result:%d",result);
    return false;
  }
  return response == '1';
}

```





// vendor/ntimespace/proc_watcher/SocketConnection.cpp

```cpp
#include "SocketConnection.h"

bool SocketConnection::doOpen(const char* sock_path) {
  struct sockaddr_un un;
  struct timeval tv;
  int ret;

  if (sock_path == nullptr) {
    ALOGW("Socket path is nullptr");
    return false;
  }

  if (access(sock_path, F_OK) != 0) {
    ALOGW("Access socket err: %s", strerror(errno));
    return false;
  }

  un.sun_family = AF_UNIX;
  strcpy(un.sun_path, sock_path);

  mFd = socket(AF_UNIX, SOCK_STREAM, 0);
  if (mFd < 0) {
    ALOGW("Create socket err: %s", strerror(errno));
    return false;
  }

  tv.tv_sec  = 1;
  tv.tv_usec = 0;
  setsockopt(mFd, SOL_SOCKET, SO_SNDTIMEO, &tv, sizeof(tv));
  setsockopt(mFd, SOL_SOCKET, SO_RCVTIMEO, &tv, sizeof(tv));

  ret = connect(mFd, (struct sockaddr *)&un, sizeof(un));
  if (ret < 0) {
    doClose();
    ALOGW("Connect socket err: %s", strerror(errno));
    return false;
  }
  return true;
}

bool SocketConnection::request(const char* message, char* result, int result_size) {
  int ret = write(mFd, message, strlen(message));
  if (ret < 0) {
    ALOGW("Write socket err: %s", strerror(errno));
    return false;
  }

  ret = read(mFd, result, result_size);
  if (ret < 0) {
    ALOGW("Read socket err: %s", strerror(errno));
    return false;
  }
  return true;
}

void SocketConnection::doClose() {
  if (mFd > 0) {
    close(mFd);
  }
}

```





线上报错，这个远程调用偶尔会出现socket连接失败,前后都有socket连接成功的，就是偶尔失败

```
10-23 02:44:56.480029  1478  1478 I GrantRoot: root---checkRootable(                                                                                                                                                     
10-23 02:44:56.480063  1478  1478 W         : Connect socket err: Connection refused                                                                                                                                     
10-23 02:44:56.480084  1478  1478 I chatty  : uid=0(root) main identical 4 lines                                                                                                                                         
10-23 02:44:56.480088  1478  1478 W         : Connect socket err: Connection refused                                                                                                                                     
10-23 02:44:56.480095  1478  1478 E GrantRoot: root---socket.doOpen(),failed!  
```

\2. 获取特定应用的 UID
adb shell pm list packages -U | grep <package_name>

----

查看应用正在起来错误进程

>  Start proc 1746:com.lsjejwn.clw/u0a96 for activity {com.lsjejwn.clw/com.nx.main.activity.SplashActivity}