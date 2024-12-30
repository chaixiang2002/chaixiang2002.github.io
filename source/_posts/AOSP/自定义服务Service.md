    在Android系统中，如果你想创建一个名为"space"的服务，让其他程序可以通过`ServiceManager.getService("space")`获取到你的服务，你可以按照以下步骤进行：

1. 在目录 `frameworks/base/core/java/android/os`中增加自己的AIDL文件用来声明服务。例如，你可以创建一个名为 `SpaceService.aidl`的文件，内容可能如下：

```java
package android.os;
interface ISpaceService {
    // 在这里声明你的方法
}
```

2. 在 `frameworks/base/Android.mk`添加aidl的声明，例如：

```makefile
core/java/android/os/ISpaceService.aidl \\
```

3. 在目录 `frameworks/base/services/java/com/android/server`增加service的实现文件，例如 `SpaceService.java`，内容可能如下：

```java
package com.android.server;
import android.content.Context;
import android.os.ISpaceService;
public class SpaceService extends ISpaceService.Stub {
    public SpaceService(Context context) {
        super();
    }
    // 在这里实现你的方法
}
```

4. 将Java服务添加到ServiceManager中。在文件 `frameworks/base/services/java/com/android/server/SystemServer.java`添加：

```java
SpaceService ss = new SpaceService(context);
ServiceManager.addService("space", ss);
```

5. 重新编译Android并运行，你所创建的服务即可访问。在任意应用中，调用服务的方法如下：

```java
import android.os.ServiceManager;
import android.os.ISpaceService;
ISpaceService ss = ISpaceService.Stub.asInterface(ServiceManager.getService("space"));
```

[以上步骤是一个基本的流程，你可能需要根据你的具体需求进行修改](https://blog.csdn.net/sdkdlwk/article/details/90548491)[^1^](https://blog.csdn.net/sdkdlwk/article/details/90548491)。希望这个答案对你有所帮助！





----

报错

```java
henryInterface service = henryInterface.Stub.asInterface(ServiceManager.getService(henryManager.SERVICE));
if (service != null) {
    try {
        service.registerCallback(new Callback() {
            @Override
            public void onMessageReceived(int type, String value) {
                Slog.d("HenryService", "Received message: " + value);
            }
        });
        service.sendMessage(1, "Hello from client");
    } catch (RemoteException e) {
        e.printStackTrace();
    }
}


frameworks/base/services/core/java/com/android/server/lights/LightsService.java:107: error: <anonymous com.android.server.lights.LightsService$LightImpl$1> is not abstract and does not override abstract method asBinder() in IInterface
                    service.registerCallback(new Callback() {
                                                            ^
1 error
FAILED: [W][2024-12-27T11:15:08+0800][19724] void cmdline::logParams(nsjconf_t *)():250 Process will be UID/EUID=0 in the global user namespace, and will have user root-level access to files
[W][2024-12-27T11:15:08+0800][19724] void cmdline::logParams(nsjconf_t *)():260 Process will be GID/EGID=0 in the global user namespace, and will have group root-level access to files
11:17:13 ninja failed with: exit status 1

#### failed to build some targets (02:13 (mm:ss)) ####

Build android failed!
```



# Stub类

在 Java 中，`Stub` 类通常与 **远程方法调用**（Remote Method Invocation, RMI）和 **Android 的 AIDL**（Android Interface Definition Language）相关。它是一个设计模式，通常用于 **代理模式** 或 **接口的实现**，特别是跨进程通信（IPC）时使用。

在 Android 中，`Stub` 类主要用于 **Binder** 机制，它是通过 **AIDL** 生成的，主要目的是在不同进程间传递接口的实现。

### 1. **什么是 Stub？**

**Stub** 是一个代理对象，通常用于提供对远程对象或接口的访问。它的作用是：

- **接口的代理**：Stub 实现了接口，并在接口方法中提供远程调用的功能。在调用方看来，Stub 就像是一个普通对象，实际上它的操作是在远程服务端执行的。
- **跨进程通信（IPC）**：在 Android 中，`Stub` 类通常用于进程间的通信。客户端和服务端运行在不同的进程中，客户端通过 `Stub` 调用服务端的方法，系统自动处理进程间的通信细节。

### 2. **`Stub` 在 AIDL 中的作用**

在 AIDL（Android Interface Definition Language）中，`Stub` 是由 AIDL 编译器自动生成的一个类，通常用来实现跨进程的接口。它充当 **服务端接口的实现**，并且在后台负责处理客户端的请求。

- **客户端**：通过 `Binder`（或者 `Stub` 类）与服务端通信，实际上是向 `Stub` 对象发送请求。
- **服务端**：`Stub` 类会在服务端接收来自客户端的请求，并调用相应的方法。

### 3. **`Stub` 类的结构**

AIDL 编译器根据定义的接口（`.aidl` 文件）自动生成 `Stub` 类。它实现了 `IInterface` 接口，并重写了 `asBinder()` 方法，用于将 `Stub` 类转化为 `Binder` 对象，供客户端使用。

### 4. **`Stub` 的工作方式**

- **客户端调用**：客户端通过 `Stub` 向服务端发送请求，`Stub` 会将请求封装成 IPC 消息并发送到服务端。
- **服务端响应**：服务端的 `Stub` 会接收客户端的请求，然后调用实际的实现方法。

### 5. **示例：AIDL 和 Stub 的使用**

假设我们有一个简单的 AIDL 接口，表示一个计算服务。客户端通过 `Stub` 发送请求到服务端，让服务端计算两个数的和。

#### 1) 定义 AIDL 接口：`ICalculator.aidl`

```aidl
package com.example.aidl;

interface ICalculator {
    int add(int a, int b);
}
```

#### 2) 编译生成的 `Stub` 类（服务端）：

```java
package com.example.aidl;

import android.os.Binder;
import android.os.IBinder;

public abstract class ICalculatorStub extends Binder implements ICalculator {
    public static ICalculator asInterface(IBinder obj) {
        // 将 Binder 对象转换为 ICalculator 接口
        if (obj == null) {
            return null;
        }
        ICalculator in = (ICalculator) obj.queryLocalInterface(DESCRIPTOR);
        if (in != null) {
            return in;
        }
        return new ICalculatorProxy(obj);
    }

    @Override
    public IBinder asBinder() {
        return this;
    }

    // 这里会包含对接口方法的实际实现，比如 add()
    public static final String DESCRIPTOR = "com.example.aidl.ICalculator";

    @Override
    public int add(int a, int b) {
        // 实际的加法实现
        return a + b;
    }
}
```

#### 3) 服务端实现：

```java
package com.example.aidl;

import android.os.RemoteException;

public class CalculatorService extends ICalculatorStub {

    @Override
    public int add(int a, int b) throws RemoteException {
        return a + b;
    }
}
```

#### 4) 客户端调用：

```java
package com.example.aidlclient;

import android.os.Bundle;
import android.os.IBinder;
import android.os.RemoteException;
import androidx.appcompat.app.AppCompatActivity;
import com.example.aidl.ICalculator;

public class MainActivity extends AppCompatActivity {

    private ICalculator mCalculator;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        // 获取服务端的 Binder 对象（通常是通过 AIDL 的服务绑定）
        IBinder binder = ServiceManager.getService("calculator"); // 假设已经绑定了服务
        mCalculator = ICalculator.Stub.asInterface(binder);

        try {
            int result = mCalculator.add(3, 4);
            System.out.println("Result: " + result);
        } catch (RemoteException e) {
            e.printStackTrace();
        }
    }
}
```

### 6. **问题解决：为什么需要 `Stub`？**

`Stub` 类的主要作用是 **解决跨进程调用** 问题。具体来说，它：

- **隐藏远程调用细节**：客户端可以像调用本地方法一样调用远程方法。`Stub` 负责将调用请求通过 Binder 传递到服务端。
- **管理进程间通信**：在不同进程间传递数据时，`Stub` 充当了中介，它将数据封装为 IPC 消息并转发。
- **实现接口**：`Stub` 类实现了接口的方法，并通过 `asBinder()` 方法将自己转换为 `Binder` 对象，这样就可以与客户端进行交互。

### 总结

`Stub` 类是 Android 进程间通信（IPC）中的关键组件，它充当客户端与服务端之间的桥梁，使得不同进程之间能够透明地进行方法调用。通过 AIDL，Android 自动为你生成 `Stub` 类，它负责将远程方法调用转化为 IPC 请求，从而简化了跨进程调用的实现。

# 回调

`Stub` 和 `Callback` 的结合主要出现在 **回调机制** 中，特别是在 Android 的 **跨进程通信**（IPC）中，使用 AIDL 定义接口时，可以通过 `Callback` 接口来实现 **异步通知** 或 **事件通知**。这种方式通常用于服务端需要将一些事件或结果异步通知到客户端。

### 1. **回调机制的背景**

在 Android 的 Binder IPC 中，通常服务端处理一些操作后会返回结果。然而，有时候服务端可能需要异步地将结果或通知推送给客户端。为了实现这一功能，客户端需要实现一个 `Callback` 接口，服务端则可以通过 `Callback` 向客户端发送异步消息。

AIDL 的回调机制就是这样一种模式，它允许服务端通过 `Callback` 接口通知客户端一些事件或数据变化。客户端通过 `registerCallback` 方法注册回调，服务端通过这个回调将事件异步发送给客户端。

### 2. **如何结合 `Stub` 和 `Callback`？**

`Stub` 和 `Callback` 通常结合使用，`Stub` 负责在服务端接收来自客户端的请求，而 `Callback` 负责让服务端能够异步地通知客户端。

- **客户端**：客户端通过 `Stub` 绑定服务并注册回调接口 (`Callback`)。
- **服务端**：服务端使用 `Stub` 类实现接口，在执行一些操作时，通过 `Callback` 将结果异步回调到客户端。

### 3. **具体示例**

假设我们有一个服务端提供计算功能，客户端请求计算并需要获取结果，而服务端在计算完成后通过回调通知客户端。

#### 1. **定义回调接口 `Callback.aidl`**

首先，定义一个 `Callback` 接口，让服务端能够向客户端发送消息：

```aidl
// Callback.aidl
package com.example.callback;

// 回调接口，用于通知客户端事件
interface Callback {
    // 远程方法：接收到计算结果时回调
    oneway void onMessageReceived(int type, String value);
}
```

#### 2. **定义计算服务接口 `ICalculator.aidl`**

接下来，定义计算接口，服务端通过这个接口向客户端提供计算功能，并通过回调将结果返回：

```aidl
// ICalculator.aidl
package com.example.callback;

// 计算服务接口
interface ICalculator {
    // 注册回调接口
    void registerCallback(in Callback callback);

    // 执行加法运算
    int add(int a, int b);
}
```

#### 3. **服务端实现 `ICalculator` 接口（包含回调）**

在服务端实现 `ICalculator.Stub`，它负责执行计算，并通过回调向客户端发送结果。

```java
// CalculatorService.java (服务端)
package com.example.callback;

import android.os.RemoteCallbackList;
import android.os.RemoteException;
import android.util.Log;

public class CalculatorService extends ICalculator.Stub {

    private static final String TAG = "CalculatorService";

    // 存储客户端的回调列表
    private RemoteCallbackList<Callback> mCallbackList = new RemoteCallbackList<>();

    @Override
    public void registerCallback(Callback callback) throws RemoteException {
        mCallbackList.register(callback);
        Log.d(TAG, "Callback registered");
    }

    @Override
    public int add(int a, int b) throws RemoteException {
        // 模拟加法操作
        int result = a + b;

        // 将结果通过回调通知客户端
        sendMessageToClients(result);
        return result;
    }

    private void sendMessageToClients(int result) {
        int count = mCallbackList.getRegisteredCallbackCount();
        if (count > 0) {
            // 使用 RemoteCallbackList 进行回调
            final int size = mCallbackList.beginBroadcast();
            for (int i = 0; i < size; i++) {
                Callback cb = mCallbackList.getBroadcastItem(i);
                try {
                    if (cb != null) {
                        cb.onMessageReceived(1, "Result: " + result); // 回调给客户端
                    }
                } catch (RemoteException e) {
                    e.printStackTrace();
                    Log.d(TAG, "Remote exception: " + e.getMessage());
                }
            }
            mCallbackList.finishBroadcast();
        }
    }
}
```

#### 4. **客户端实现回调并注册**

客户端通过 `Stub` 调用服务，并注册回调接口，以便服务端在计算完成后通知客户端。

```java
// MainActivity.java (客户端)
package com.example.callbackclient;

import android.os.Bundle;
import android.os.RemoteException;
import androidx.appcompat.app.AppCompatActivity;
import com.example.callback.ICalculator;
import com.example.callback.Callback;

public class MainActivity extends AppCompatActivity {

    private ICalculator mCalculator;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        // 获取服务端的 ICalculator 对象（通过 AIDL 绑定服务）
        mCalculator = ICalculator.Stub.asInterface(ServiceManager.getService("calculator_service"));

        try {
            // 注册回调接口
            mCalculator.registerCallback(new Callback.Stub() {
                @Override
                public void onMessageReceived(int type, String value) {
                    // 接收到服务端的回调消息
                    System.out.println("Received from service: " + value);
                }
            });

            // 请求加法计算
            int result = mCalculator.add(3, 5);
            System.out.println("Add result: " + result);
        } catch (RemoteException e) {
            e.printStackTrace();
        }
    }
}
```

### 4. **工作流程**

1. **客户端**：通过 `Stub.asInterface()` 获取 `ICalculator` 的代理对象，并调用 `registerCallback()` 方法注册回调接口。
2. **服务端**：服务端接收到客户端请求后执行加法操作，然后通过回调接口 `sendMessageToClients()` 将计算结果通知客户端。
3. **回调**：客户端实现了 `Callback` 接口，并在 `onMessageReceived()` 方法中处理服务端的消息。

### 5. **总结**

在 Android 中，结合使用 `Stub` 和 `Callback` 可以实现异步的跨进程通信。`Stub` 类提供了服务端接口的实现，而 `Callback` 则允许服务端在处理完请求后，通过回调异步地将结果通知到客户端。具体的步骤包括：

- **客户端**通过 `Stub` 获取远程服务并注册回调。
- **服务端**执行相关操作（如计算），然后通过 `Callback` 异步地通知客户端。

这种模式常用于服务端需要异步通知客户端的场景，如更新UI、事件通知等。

----

周总的服务

frameworks/base/api/current.txt

frameworks/base/core/java/android/content/Context.java

frameworks/base/core/java/android/app/SystemServiceRegistry.java



frameworks/base/core/java/com/android/internal/space/NineDSpaceManager.java

frameworks/base/core/java/com/android/internal/space/api/BluetoothMock.java

frameworks/base/core/jni/com_android_internal_os_Zygote.cpp

frameworks/base/services/core/java/com/android/server/space/AppFilter.java

frameworks/base/Android.bp

我的服务

---

[Android Java 系统服务框架与第三方 App 使用自定义 Java 系统服务Android Java 系统服务 - 掘金](https://juejin.cn/post/7264920202864640059?searchId=20241227175833842A5ABB92EB9837653B)

[添加 Java 系统服务 | Android Framework](https://yuandaimaahao.github.io/AndroidFrameworkTutorialPages/003.学穿Binder篇/021.添加 Java 系统服务.html)





# 如何创建一个Java系统服务

1. 创建服务的AIDL，对外提供接口frameworks/base/core/java/com/android/henryservice/henryInterface.aidl
2. 创建服务的实现Binder 服务端类 Stub类，frameworks/base/services/core/java/com/android/server/henryservice/henryservice.java
3. 创建服务的Manager管理类，frameworks/base/core/java/com/android/henryservice/henryManager.java
4. 构建文件中添加AIDL的路径，frameworks/base/Android.bp
5. SystemServer添加服务到ServiceManager，其他组件可以通过 `ServiceManager.getService` 获取到你的服务实例frameworks/base/services/java/com/android/server/SystemServer.java
6. 注册并指定服务实例的创建，确保系统能够通过 `getSystemService` 方法访问你的服务。frameworks/base/core/java/android/app/SystemServiceRegistry.java



# 2种系统服务的区别

[添加 Java 系统服务 | Android Framework](https://yuandaimaahao.github.io/AndroidFrameworkTutorialPages/003.学穿Binder篇/021.添加 Java 系统服务.html)

[Android 添加系统服务的完整流程SystemService(史上最全)-CSDN博客](https://blog.csdn.net/qq_45649553/article/details/138523625)

这两种方法的主要区别在于 **服务的管理** 和 **系统服务的注册方式**。具体来说，第2种方法通过引入 **Manager 类** 和 **SystemServiceRegistry** 注册机制，提供了更加灵活、模块化和标准化的方式来处理系统服务。我们来详细分析一下这两种方式的区别，以及第2种方式的设计目的。

### 第一种方式：直接通过 `ServiceManager` 注册

步骤：

1. 创建服务的 **AIDL** 文件，定义服务的接口。
2. 实现服务端的 **Binder** 服务类（即继承 `Binder` 的类，通常是 `Stub` 实现）。
3. 在 **构建文件（Android.bp）** 中添加 AIDL 的路径。
4. 在 **SystemServer** 中通过 `ServiceManager.addService` 注册服务，其他组件可以通过 `ServiceManager.getService` 获取该服务实例。

这种方式比较简单，适用于一些简单的服务，尤其是当你的服务不需要复杂的生命周期管理或者对外接口不需要经过复杂的访问控制时，采用这种方式注册服务是足够的。

**缺点**：

- 直接通过 `ServiceManager` 注册服务的方式并没有很好地集成到 Android 的服务管理框架中。这使得服务的管理（如生命周期管理、服务访问权限控制等）相对麻烦。
- 这种方式会让服务的创建和管理变得不够灵活，尤其当你需要对服务进行更细粒度的控制（例如配置参数、依赖注入等）时，可能不太方便。

### 第二种方式：引入 **Manager 类** 和 **`SystemServiceRegistry`** 注册

步骤：

1. 创建服务的 **AIDL** 文件，定义服务的接口。
2. 编写 **Manager** 类，用来封装服务的创建和管理逻辑。
3. 创建服务的 **Binder** 服务类（即 `Stub` 实现类）。
4. 在 **构建文件（Android.bp）** 中添加 AIDL 的路径。
5. 在 **SystemServer** 中通过 `ServiceManager.addService` 注册服务。
6. 使用 **`SystemServiceRegistry`** 注册服务，确保通过 `getSystemService` 获取服务时，系统会知道如何实例化该服务。

### 关键区别

- **Manager 类的引入**：
   第二种方式通过引入 **Manager 类**，将服务的创建和管理从具体的服务实现中分离出来。**Manager** 类通常负责：
  - 创建服务实例。
  - 管理服务的生命周期。
  - 实现服务的初始化、依赖注入和其它额外功能。 这样做的好处是将服务的管理逻辑与服务本身的实现解耦，从而提高代码的可维护性和扩展性。
- **`SystemServiceRegistry` 的注册**： 第二种方式通过 **`SystemServiceRegistry`** 完成服务的注册。这样做的目的在于：
  1. **统一管理系统服务**：`SystemServiceRegistry` 是 Android 系统中用于管理所有系统服务的地方，它确保所有服务的注册都遵循统一的流程，提供了更好的可维护性。
  2. **标准化服务的创建和获取**：通过注册到 `SystemServiceRegistry`，服务能够通过 `Context.getSystemService()` 进行访问，而不是直接调用 `ServiceManager.getService()`。这样可以使系统服务的获取更加符合 Android 的架构设计。
  3. **生命周期管理**：使用 `SystemServiceRegistry` 可以更容易地实现服务的生命周期管理，例如服务的延迟加载、懒加载等。这使得服务的管理变得更加灵活。

### 设计目的和优势

引入 **Manager 类** 和 **`SystemServiceRegistry`** 进行服务注册，主要有以下几个设计目的和优势：

1. **增强模块化**：通过 Manager 类来管理服务的创建和生命周期，能够使服务的逻辑更加独立，降低服务之间的耦合度。这样做能够让系统服务的创建和管理更加清晰，有助于后续的维护和扩展。
2. **遵循 Android 架构规范**：`SystemServiceRegistry` 使得服务的管理更加标准化和一致化。所有服务都通过相同的机制进行注册和获取，使得 Android 的服务架构更加规范，容易进行扩展和改进。
3. **提高可维护性**：通过将服务的创建和管理逻辑从服务本身中分离出来，**Manager 类** 可以专注于服务的初始化、配置和生命周期管理，而服务类本身则专注于实现具体的业务逻辑。这样，服务类更加简洁，代码可维护性和可扩展性提高。
4. **灵活性**：`SystemServiceRegistry` 提供了更加灵活的服务管理方式，比如延迟加载服务、按需实例化服务等。它允许更复杂的服务管理逻辑，如依赖注入、初始化延迟等，这些都是直接使用 `ServiceManager.addService` 方式难以实现的。
5. **服务的依赖管理**：通过 Manager 类和 `SystemServiceRegistry` 的结合，系统服务之间的依赖关系可以更加清晰和规范。如果有多个服务相互依赖，Manager 类可以提供更好的管理和协调机制。

### 总结

- **第一种方式**：适合简单的服务，直接通过 `ServiceManager` 注册服务，便捷快速，但缺乏灵活性和标准化管理，容易导致服务管理混乱。
- **第二种方式**：通过引入 **Manager 类** 和 **`SystemServiceRegistry`** 进行服务的注册和管理，提供了更强的灵活性、可维护性和标准化，适用于需要更复杂管理的系统服务，尤其是在大型和复杂的系统中，这种方式能够提供更好的可扩展性和服务的生命周期管理。

总体来说，第二种方式设计更为完善和灵活，尤其适用于复杂的系统服务管理，遵循了 Android 的架构设计原则。



# 为什么引入 `Manager` 和 `SystemServiceRegistry` 设计？

确实，**第2种方式**的优势主要体现在复杂业务场景下，尤其是需要管理多个依赖、服务生命周期、懒加载、或者服务之间有复杂交互的情况下。我们可以通过一个具体的复杂业务场景来更好地理解 **引入 `Manager` 类** 和 **`SystemServiceRegistry`** 的设计如何解决实际问题。

### 场景背景：设备管理服务

假设我们正在为一个设备管理平台（类似于 Android 的 **Device Policy Manager**）构建一个 **设备监控服务**，它需要处理多个系统服务并协调它们的工作。我们的服务需要与 **Wi-Fi**、**蓝牙**、**网络状态**、**设备电池状态** 等多个服务进行交互。这个服务不仅要定期检查硬件设备的状态，还要根据设备的状态来调整一些系统配置，比如连接 Wi-Fi、关闭蓝牙、设置电池节能模式等。

在这种场景下，我们面临的问题是：

1. 各种硬件服务的状态更新频繁。
2. 不同服务之间的依赖和协作：例如，Wi-Fi 状态变化时可能需要根据蓝牙的连接状态进行某些调整。
3. 各种硬件服务可能需要在不同的生命周期中动态加载（懒加载），而且它们之间可能会有复杂的依赖关系。
4. 设备管理服务本身可能需要在整个系统中以单例的方式进行管理。

如果使用 **第一种方式**（直接通过 `ServiceManager` 注册服务）来管理这些服务，代码的复杂性和维护难度会迅速增加。具体问题包括：

### 复杂业务场景：设备监控服务（没有 `Manager` 和 `SystemServiceRegistry`）

#### 1. 复杂的依赖关系管理

- 我们的设备监控服务需要依赖 Wi-Fi、蓝牙、网络状态等多个系统服务。如果直接通过 `ServiceManager` 注册这些服务，代码会非常臃肿且重复。每个服务都需要手动处理其生命周期，并且每次获取服务实例时都需要通过 `ServiceManager.getService()` 来进行调用。
- **问题**：这些服务可能需要在某些条件下懒加载（例如，只有当 Wi-Fi 启动时，才加载 Wi-Fi 相关的服务）。如果通过 `ServiceManager` 直接管理服务实例，无法优雅地处理懒加载。

#### 2. 服务的初始化和生命周期管理

- 假设 **Wi-Fi** 和 **蓝牙** 服务是独立的，它们的初始化是由设备管理服务来控制的。例如，Wi-Fi 服务需要在设备启动时初始化，而蓝牙服务可能需要在设备的某些场景下才初始化。
- **问题**：通过 `ServiceManager` 添加服务时，无法灵活地控制服务的初始化时机。如果想要推迟初始化或者需要为服务注入一些额外的配置，就需要在 `SystemServer` 中编写大量的额外代码来实现这些控制。

#### 3. 服务间的协调和依赖注入

- 假设 **Wi-Fi** 服务和 **蓝牙** 服务需要互相协调。例如，当设备连接到 Wi-Fi 时，蓝牙可能需要断开；或者当电池电量低时，需要关闭 Wi-Fi 和蓝牙节能。
- **问题**：直接通过 `ServiceManager` 获取这些服务会导致每次调用都需要通过 `getService` 进行，且没有标准化的方式来协调服务之间的交互。这些服务的协调代码会变得非常混乱，并且难以维护。

#### 4. 重复的代码和硬编码

- 在没有 `Manager` 类的情况下，管理每个服务的代码会相对重复。例如，Wi-Fi 服务需要检测是否启用了 Wi-Fi，然后获取 Wi-Fi 状态；蓝牙服务需要检查蓝牙是否启用，然后获取设备的蓝牙状态等。
- **问题**：每次访问服务时，都需要写重复的代码来初始化和管理服务实例，造成冗余和硬编码。这样的代码不易扩展，增加新服务时，需要修改很多地方。

------

### 使用 **第二种方式**（引入 Manager 类 和 SystemServiceRegistry）

引入 **Manager 类** 和 **`SystemServiceRegistry`** 后，整个服务管理框架变得更加清晰、可维护和可扩展。

#### 1. 统一的服务管理：**Manager 类**

- **Manager 类** 可以封装所有服务的创建和管理逻辑，处理服务的初始化、生命周期和依赖管理。例如，Wi-Fi 服务和蓝牙服务的管理可以通过 `DeviceManager` 这样的类来集中管理。`DeviceManager` 类不仅可以负责服务的初始化，还可以管理它们之间的协调。

  ```kotlin
  class DeviceManager(context: Context) {
      private val connectivityManager = context.getSystemService(ConnectivityManager::class.java)
      private val wifiManager = context.getSystemService(WifiManager::class.java)
      private val bluetoothManager = context.getSystemService(BluetoothManager::class.java)
  
      fun initializeServices() {
          if (wifiManager.isWifiEnabled) {
              // 初始化 Wi-Fi 相关服务
          }
  
          if (bluetoothManager.isBluetoothEnabled) {
              // 初始化蓝牙相关服务
          }
      }
  
      fun handleLowBatteryMode() {
          // 根据电池状态调整 Wi-Fi 和蓝牙状态
      }
  }
  ```

- **优点**：`DeviceManager` 类将所有与硬件相关的服务的创建、初始化和生命周期管理封装在一起，减少了冗余的代码，也使得服务间的依赖关系更加明确。

#### 2. 延迟加载和懒加载：`SystemServiceRegistry`

- 通过 `SystemServiceRegistry`，我们可以在需要时动态加载服务，而不是在启动时一开始就加载所有服务。假设我们的设备管理服务只有在用户需要操作 Wi-Fi 或蓝牙时才加载相应的服务。
- **优点**：通过 `SystemServiceRegistry` 统一管理服务实例，系统可以根据实际需要懒加载服务，避免不必要的资源浪费。例如，Wi-Fi 服务只会在用户需要连接 Wi-Fi 时才会被加载和初始化。

#### 3. 服务的协调与依赖注入

- 如果 Wi-Fi 服务和蓝牙服务有依赖关系，`DeviceManager` 类可以提供更加灵活的服务协调。比如当 Wi-Fi 连接成功时，可以自动断开蓝牙连接。

  ```kotlin
  class DeviceManager(context: Context) {
      private val wifiManager = context.getSystemService(WifiManager::class.java)
      private val bluetoothManager = context.getSystemService(BluetoothManager::class.java)
  
      fun connectToWifiAndDisableBluetooth(wifiSSID: String) {
          wifiManager.connect(wifiSSID)
          bluetoothManager.disable()  // 禁用蓝牙
      }
  }
  ```

- **优点**：这种方式可以避免在每次访问服务时手动管理服务之间的协调逻辑，使得服务间的依赖更加容易管理和扩展。

#### 4. 更加模块化和可扩展的设计

- 当我们需要增加新的硬件服务时，比如添加一个 **电池管理服务**，我们只需要在 `DeviceManager` 中进行扩展，而不需要修改 `SystemServer` 中的注册逻辑或者修改每个具体服务的代码。

------

### 总结：为什么引入 `Manager` 和 `SystemServiceRegistry` 设计重要？

- **复杂服务的管理**：引入 **Manager 类** 和 **`SystemServiceRegistry`** 后，服务的初始化、生命周期管理和服务间协调变得更加清晰。`Manager` 类帮助我们集中管理各个服务，并确保服务能够以合理的时机初始化和启动。
- **避免冗余和硬编码**：通过统一的管理方式，我们避免了重复代码和硬编码，尤其是服务之间的协调代码可以集中管理，易于维护。
- **懒加载和依赖注入**：通过 `SystemServiceRegistry`，我们可以实现服务的懒加载，使得系统在必要时才加载服务，提升系统性能并节省资源。
- **服务扩展性**：通过 `Manager` 类和 `SystemServiceRegistry` 的设计，增加新服务和修改现有服务的逻辑变得更加简单，避免了在 `SystemServer` 中手动管理多个服务实例的麻烦。

总之，当服务变得复杂，需要协调和管理多个系统服务时，直接使用 `ServiceManager` 注册服务的方式会显得比较繁琐和难以维护。通过引入 **Manager 类** 和 **`SystemServiceRegistry`**，能够使得服务的管理更加灵活、可扩展和规范，适用于复杂的系统服务场景。