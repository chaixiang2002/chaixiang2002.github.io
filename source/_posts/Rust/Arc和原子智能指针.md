经常看到类似let receiver=Arc::new(Mutex::new(receiver));的代码 Mutex可以理解为给东西上锁 Arc是什么？

---

`Arc` 代表 **Atomic Reference Counting**，是 Rust 中提供的一种**原子引用计数智能指针**。它允许多个线程共享同一个值，并确保当最后一个引用被丢弃时，值会被正确释放。`Arc` 是多线程环境中的常用工具，能够在线程之间安全地共享数据。

### 1. 什么是 `Arc`？
`Arc<T>` 提供的是一个**线程安全的引用计数**，可以在多个线程中同时拥有对同一块数据的引用，而不需要担心并发问题。与 `Rc<T>` 不同的是，`Rc<T>` 只能用于单线程中，`Arc<T>` 通过原子操作保证引用计数的更新在多线程环境下也是安全的。

`Arc` 是不可变的，但你可以和其他类型（如 `Mutex`）结合，来实现对共享数据的可变性。

### 2. 作用
在多线程环境中，每个线程都会有自己独立的堆栈空间，当多个线程需要访问同一块数据时，必须通过某种形式共享内存。这时，`Arc<T>` 就可以用来保证内存安全，并允许多个线程共享同一个值。

### 3. 示例
以你的代码为例：
```rust
let receiver = Arc::new(Mutex::new(receiver));
```
这里，`receiver` 是一个 `mpsc::Receiver<Job>`，你希望多个线程（即多个 `Worker`）能够共享这个 `receiver`，同时又保证线程安全。

- `Mutex::new(receiver)`：将 `receiver` 放入 `Mutex`，保证线程之间互斥访问该数据。因为多个线程不能同时解锁同一个 `Mutex`，这样可以避免并发问题。
- `Arc::new(...)`：将 `Mutex<Receiver<Job>>` 包裹在 `Arc` 中，允许多个线程共享对同一数据的所有权。

**简而言之：**
- `Mutex` 用来**上锁**，确保同一时间只有一个线程可以修改数据。
- `Arc` 用来**共享所有权**，允许多个线程共享数据，并且自动管理数据的生命周期。

### 4. `Arc` 的工作机制
`Arc` 在内部维护了一个原子引用计数，每次克隆 `Arc` 时，这个计数会增加。当某个 `Arc` 实例被丢弃时，计数减少。只有当计数降为 0 时，数据才会被释放。这种机制可以防止在多线程环境中，多个线程尝试同时释放同一块内存时发生的问题。

### 5. `Arc` 的常见用法
`Arc` 经常与 `Mutex` 结合使用，以实现对数据的并发访问控制：
```rust
use std::sync::{Arc, Mutex};
use std::thread;

fn main() {
    let data = Arc::new(Mutex::new(0));

    let mut handles = vec![];

    for _ in 0..10 {
        let data = Arc::clone(&data);
        let handle = thread::spawn(move || {
            let mut num = data.lock().unwrap();
            *num += 1;
        });
        handles.push(handle);
    }

    for handle in handles {
        handle.join().unwrap();
    }

    println!("Result: {}", *data.lock().unwrap());
}
```
在这个例子中：
- `Arc::clone(&data)`：每个线程获取 `Arc` 的克隆，所有线程共享同一个 `Mutex` 包裹的数据。
- `data.lock()`：每个线程在访问 `data` 时需要先获取锁，确保安全访问。

### 总结
- **`Arc<T>`**：是一个线程安全的引用计数智能指针，用于共享所有权。
- **`Mutex<T>`**：用于在线程间互斥地访问数据。
- 这两者结合可以让多个线程安全地共享和修改同一块数据。

如果你有多个线程需要访问同一块数据并且需要保证线程安全，`Arc<Mutex<T>>` 是一个常用的组合方式。

---

### mpsc多生产者单消费者

其实在 Rust 的 `mpsc`（multiple producer, single consumer，即“多生产者，单消费者”）通道模型中，`mpsc::Receiver` 本身并**不支持多个接收者**同时存在并从通道中接收数据。`mpsc` 的设计是允许**多个生产者（发送者）**，但只允许**一个消费者（接收者）**，这就是为什么它叫做 "single consumer"。

### 那为什么我们需要加锁和 `Arc`？

你提到的代码中，将 `mpsc::Receiver` 包装在 `Arc<Mutex<Receiver<T>>>` 中的原因是，你需要多个线程（`Worker`）共享**一个接收者**，并且通过互斥锁来确保在同一时刻只有一个线程能够从这个接收者中读取任务。

- **`Receiver` 不支持多消费者**：如果你尝试简单地克隆 `Receiver` 并在多个线程中使用，那么 Rust 不会允许这样做，因为 `Receiver` 的设计不支持多消费者。你可以克隆 `Sender`，但不能克隆 `Receiver`。
- **通过加锁实现线程安全**：将 `Receiver` 放在 `Mutex` 中，意味着在每次线程想要从 `Receiver` 中接收任务时，必须先获取锁。这样就能保证同一时刻只有一个线程能访问 `Receiver`，并消费任务。
- **`Arc` 允许多线程共享**：由于多个线程需要共享同一个 `Receiver`，你需要用 `Arc`（原子引用计数）来管理共享所有权，这样可以确保多线程同时安全地持有 `Receiver` 的所有权。

### 举个例子说明：

```rust
let (sender, receiver) = mpsc::channel();
let receiver = Arc::new(Mutex::new(receiver));

for _ in 0..num_workers {
    let receiver = Arc::clone(&receiver);

    thread::spawn(move || {
        loop {
            let task = receiver.lock().unwrap().recv();

            match task {
                Ok(job) => {
                    println!("Received a job; executing it.");
                    job();
                }
                Err(_) => {
                    println!("Channel closed; shutting down worker.");
                    break;
                }
            }
        }
    });
}
```

在这个例子中：
- `mpsc::Receiver` 只能有一个实例，因此你使用 `Arc` 和 `Mutex` 让多个线程能安全地共享同一个 `Receiver`。
- 当线程获取任务时，它会先锁住 `Mutex`，然后调用 `recv()` 从通道中获取任务。在锁住期间，其他线程无法获取这个锁，也就不能同时消费任务。

### 总结：
- **`mpsc::Receiver` 本身只支持一个消费者**：它设计为单消费者模型，不支持多个接收者同时从同一通道中消费任务。
- **`Arc<Mutex<Receiver>>` 的作用**：通过 `Arc` 和 `Mutex` 允许多个线程安全地共享同一个接收者，并确保任务不会被多个线程同时消费。

如果你不使用 `Mutex`，则在多个线程尝试使用同一个 `Receiver` 时会出现数据竞争，导致并发问题。因此，`Mutex` 是用来防止多个线程同时访问 `Receiver` 并造成冲突的。

---

### 哪rust有没有多生产者多消费者通道模型？

是的，Rust 提供了**多生产者多消费者（multiple producer, multiple consumer，MPMC）**的通道模型。在标准库中，虽然 `mpsc` 模型只支持**单消费者**，但是可以通过第三方库如 **`crossbeam`** 来实现 MPMC 通道模型。

`crossbeam-channel` 是一个非常流行的库，它提供了更强大的通道功能，包括多生产者、多消费者的支持。你可以使用 `crossbeam` 实现多个生产者和多个消费者同时发送和接收消息的场景。

### 使用 `crossbeam-channel` 实现 MPMC

首先，你需要在 `Cargo.toml` 中添加 `crossbeam-channel` 依赖：

```toml
[dependencies]
crossbeam-channel = "0.5"
```

然后你可以这样使用它：

```rust
use crossbeam_channel::unbounded;
use std::thread;

fn main() {
    let (sender, receiver) = unbounded();

    // 创建多个生产者线程
    let sender1 = sender.clone();
    let sender2 = sender.clone();

    thread::spawn(move || {
        sender1.send("Message from producer 1").unwrap();
    });

    thread::spawn(move || {
        sender2.send("Message from producer 2").unwrap();
    });

    // 创建多个消费者线程
    let receiver1 = receiver.clone();
    thread::spawn(move || {
        while let Ok(message) = receiver1.recv() {
            println!("Consumer 1 received: {}", message);
        }
    });

    thread::spawn(move || {
        while let Ok(message) = receiver.recv() {
            println!("Consumer 2 received: {}", message);
        }
    });

    // 主线程休眠等待所有线程完成
    thread::sleep(std::time::Duration::from_secs(1));
}
```

### 解释：

1. **通道创建**：`unbounded()` 创建了一个无界通道，返回了一个发送者 (`sender`) 和一个接收者 (`receiver`)。
2. **生产者线程**：
   - 通过 `sender.clone()`，我们创建了多个生产者（`sender1` 和 `sender2`），每个生产者都能发送消息到同一个通道。
   - 两个线程分别发送消息。
3. **消费者线程**：
   - 通过 `receiver.clone()`，我们创建了多个消费者（`receiver1` 和 `receiver2`），每个消费者都能从同一个通道接收消息。
   - 消费者线程会一直尝试从通道中接收消息，直到通道关闭或所有消息都处理完。
4. **多消费者支持**：在 `crossbeam-channel` 中，每个消费者都会从通道中按顺序获取消息，确保同一条消息只会被一个消费者消费。

### `crossbeam-channel` 的特点

- **多生产者多消费者**：你可以在多个线程中使用同一个通道来进行并发的生产和消费，通道支持多个生产者和多个消费者。
- **无界和有界通道**：`crossbeam-channel` 提供了 `unbounded()` 无界通道和 `bounded(capacity)` 有界通道，允许你根据需要选择不同的通道类型。
- **性能优化**：`crossbeam-channel` 在性能方面比标准库的 `mpsc` 要更高效，尤其是在高并发场景下。

### 总结

虽然 Rust 标准库的 `mpsc` 只支持单消费者模型，但通过 `crossbeam-channel` 库，你可以轻松实现多生产者多消费者的通道模型。如果你需要高效的 MPMC 通道，这是一个非常适合的选择。

---

### Rust官方还要哪些通道模型

Rust 官方标准库中除了 `mpsc`（multiple producer, single consumer，多生产者单消费者）之外，还提供了一个基于 **`std::sync::mpsc`** 的多种通道模型变体。虽然这些变体是基于单消费者设计的，但它们可以通过不同的方式来支持各种并发模型。主要包括：

### 1. `std::sync::mpsc::channel()`
- **模型**：多生产者，单消费者
- **特点**：Rust 标准库中最常见的通道模型，支持多个生产者（通过克隆 `Sender`），但只允许一个消费者（`Receiver`）。
- **使用场景**：适用于生产者比较多，但消费者只需要一个的场景，比如任务调度、事件驱动系统。

### 2. `std::sync::mpsc::sync_channel()`
- **模型**：多生产者，单消费者（带容量限制）
- **特点**：与 `channel` 不同，`sync_channel` 创建的是**有界通道**。你需要指定通道的容量，即允许缓冲的消息数量。当通道满时，发送者会被阻塞，直到有消息被消费。
- **使用场景**：适用于需要控制并发流量的场景，比如实现工作队列，或者希望有流量控制的任务调度。

#### 示例：
```rust
use std::sync::mpsc;
use std::thread;
use std::time::Duration;

fn main() {
    let (sender, receiver) = mpsc::sync_channel(2); // 缓冲区大小为2

    thread::spawn(move || {
        for i in 0..5 {
            sender.send(i).unwrap();
            println!("Sent {}", i);
        }
    });

    thread::sleep(Duration::from_secs(1)); // 模拟接收延迟
    for received in receiver {
        println!("Received {}", received);
    }
}
```

### 3. `std::sync::mpsc::Sender` 和 `std::sync::mpsc::Receiver`
- `Sender` 是用来发送消息的通道发送端，它可以被克隆，因此你可以有多个生产者。
- `Receiver` 是接收消息的通道接收端，它不允许克隆，因此只能有一个消费者。

### Rust 官方标准库没有直接提供 MPMC（多生产者多消费者）的通道模型，标准库中的 `mpsc` 是为单消费者设计的。但是，可以通过下面两种方式间接实现：

1. **通过 `Arc<Mutex<Receiver<T>>>`**：
   - 通过将单个接收者共享给多个线程（消费者），并且通过 `Arc` 和 `Mutex` 进行同步访问，能够实现类似多消费者的行为，但本质上仍然是多个线程共享一个 `Receiver`，并且通过互斥锁来确保线程安全。

2. **通过 `crossbeam` 等第三方库**：
   - Rust 标准库之外，`crossbeam-channel` 是一个流行的第三方库，它提供了真正的多生产者多消费者通道模型。`crossbeam-channel` 具备高效的无锁并发特性，适合高并发场景。

### 其他 Rust 标准库支持的通道类型

虽然 Rust 标准库主要提供的是 `mpsc` 相关的通道模型，但它还有一些相关的并发原语，可以结合通道模型使用：

### 1. `std::sync::Mutex` 和 `std::sync::RwLock`
- **`Mutex`**：在多线程中提供互斥访问共享数据的机制，只有一个线程能访问数据，其它线程则需要等待锁的释放。
- **`RwLock`**：提供了多读单写的访问方式，多个线程可以同时读，但写操作需要独占访问。

### 2. `std::sync::Arc`（原子引用计数）
- **`Arc`**（Atomic Reference Counting）：是多线程环境下用于共享数据的智能指针。它允许多个线程共享所有权，并保证线程安全。常用于需要多线程共享一个资源（如 `Mutex` 或 `Receiver`）的场景。

### 总结

Rust 标准库中的并发通道模型主要是基于 **`std::sync::mpsc`** 提供的多生产者单消费者模型（MPMC 通道需要通过第三方库实现）。同时，Rust 标准库还提供了如 `Mutex`、`Arc` 等工具，允许你在多线程中安全地共享数据。

如果需要多生产者多消费者模型，建议使用 **`crossbeam-channel`** 或其他第三方库来实现高效并发。

---

## [上一章节的遗留问题](https://course.rs/advance-practice1/graceful-shutdown.html#上一章节的遗留问题)

在上一章节的末尾，我们提到将 `let` 替换为 `while let` 后，多线程的优势将荡然无存，原因藏的很隐蔽：

1. `Mutex` 结构体没有提供显式的 `unlock`，要依赖作用域结束后的 `drop` 来自动释放
2. `let job = receiver.lock().unwrap().recv().unwrap();` 在这行代码中，由于使用了 `let`，右边的任何临时变量会在 `let` 语句结束后立即被 `drop`，因此锁会自动释放
3. 然而 `while let` (还包括 `if let` 和 `match`) 直到最后一个花括号后，才触发 `drop`

```rust
impl Worker {
    fn new(id: usize, receiver: Arc<Mutex<mpsc::Receiver<Job>>>) -> Worker {
        let thread = thread::spawn(move || {
            while let Ok(job) = receiver.lock().unwrap().recv() {
                println!("Worker {id} got a job; executing.");

                job();
            }
        });

        Worker { id, thread }
    }
}
```

根据之前的分析，上面的代码直到 `job()` 任务执行结束后，才会释放锁，去执行另一个请求，最终造成请求排队。