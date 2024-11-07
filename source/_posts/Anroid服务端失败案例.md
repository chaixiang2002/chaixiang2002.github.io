```kotlin
   override fun onStartCommand(intent: Intent?, flags: Int, startId: Int): Int {
        Log.d("BrightnessService", "Service started")
        CoroutineScope(Dispatchers.IO).launch {
            try {
                val serverSocket = ServerSocket(port, 50, InetAddress.getByName("0.0.0.0"))
                Log.d("BrightnessService", "ServerSocket listening on port $port")
                while (true) {
                    val socket: Socket = serverSocket.accept()
                    Log.d("BrightnessService", "New connection accepted")
                    // 使用协程处理每个连接
                    launch { handleClient(socket) }
                }
            } catch (e: Exception) {
                Log.e("BrightnessService", "Error: ${e.message}")
                e.printStackTrace()
            }
        }
        return START_STICKY
    }

    private suspend fun handleClient(socket: Socket) {
        Log.d("BrightnessService", "Handling new client")

        val input = socket.getInputStream().bufferedReader()
        Log.d("BrightnessService", "11111111111111")
        val message = input.readLine() ?: return
        Log.d("BrightnessService", "Received message: $message")

        if (message.startsWith("LightsService|setBrightness|")) {
            val brightness = message.split("|")[2].toIntOrNull()
            brightness?.let {
                if (it in 0..255) {
                    setBrightness(it)
                    socket.getOutputStream().write("$it\n".toByteArray())
                    socket.getOutputStream().flush()
                }
            }
        } else {
            socket.getOutputStream().write("asd".toByteArray())
            socket.getOutputStream().flush()
        }

        socket.close()
    } 
```

问题情况：
  val message = input.readLine() ?: return
这一句每次要等到客户端关闭时才执行完，导致客户端根本得不到响应



问题原因和解决方法

### 解释：`readLine()` 阻塞行为

`readLine()` 是基于字符流的，它会一直等待直到接收到一个换行符 `\n`，作为一行的结束标志。如果客户端在连接建立后发送了数据，但没有发送换行符，服务端的 `readLine()` 会一直阻塞，直到：

1. **客户端发送换行符**（`'\n'`）。
2. **客户端主动关闭连接**，此时 `readLine()` 会返回 `null`，表示输入流已结束。

如何解决这个问题？

```kotlin
val buffer = ByteArray(1024)
val bytesRead = socket.getInputStream().read(buffer)
if (bytesRead != -1) {
    val message = String(buffer, 0, bytesRead)
    Log.d("BrightnessService", "Received message: $message")
}

```

