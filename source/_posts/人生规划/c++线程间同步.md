## promise 和 future

```c++
promise<void> readyFoo;
future<void> futureFoo;

//Worker线程
void foo(function<void()> printFoo) {
    // 等待readyFoo
    futureFoo.get(); 
    printFoo();
}

//main线程
int main(){
    futureFoo = readyFoo.get_future();//连接readyFoo和futureFoo
    
    pre();//做好其他工作
    readyFoo.set_value();//通知准备好了，设置readyFoo
}
```



**无锁同步**：

- 与传统的条件变量和信号量相比，`promise` 和 `future` 提供了一种无锁的方式来传递值或通知线程。这对于减少锁竞争、避免死锁和提高程序性能非常有利。



## 信号量sem

```c++
sem_t foo_done;

//Worker线程
void foo(function<void()> printFoo) {
    // 等待readyFoo
	sem_wait(&foo_done);
    printFoo();
}
//main线程
int main(){
    pre();//做好其他工作
    sem_init(&foo_done,0,1);//通知准备好了，设置readyFoo
}
```

**灵活性**：

- **`promise/future`**：专注于一次性的事件通知（例如：线程完成任务）。它适用于某个操作的同步或传递一个结果。
- **信号量**：信号量的灵活性更高，可以用来控制多个线程的访问权限，特别适用于生产者/消费者模型、资源池等场景。

## 互斥锁

## 条件变量

[1117. H2O 生成 - 力扣（LeetCode）](https://leetcode.cn/problems/building-h2o/)

```c++
class H2O {
public:
    int sumh=2;
    condition_variable cv;
    mutex mt;
    H2O() {

    }

    void hydrogen(function<void()> releaseHydrogen) {
        unique_lock<mutex> lock(mt);
        cv.wait(lock,[this]{return sumh>0;});//h>1s时连续2次
        releaseHydrogen();
        sumh--;
        cv.notify_all();
    }

    void oxygen(function<void()> releaseOxygen) {
        unique_lock<mutex> lock(mt);
        cv.wait(lock,[this]{return sumh<1;});
        releaseOxygen();
        sumh=2;
        cv.notify_all();
    }
};
```



## 原子操作

基本的生产者-消费者问题

```c++
std::atomic<bool> ready(false);
std::atomic<int> data(0);

void producer() {
    data.store(42, std::memory_order_relaxed); 
    ready.store(true, std::memory_order_release);
}

void consumer() {
    while (!ready.load(std::memory_order_acquire)); // 等待 ready=true
    std::cout << "Data: " << data.load(std::memory_order_relaxed) << std::endl;
}

```



```c++
class FizzBuzz {
private:
    int n;
    atomic<bool> waitfizz;
    atomic<int> waitbuzz;
    atomic<int> waitfb;
    atomic<int> waitnumber;

public:
    FizzBuzz(int n) {
        this->n = n;
    }

    // printFizz() outputs "fizz".
    void fizz(function<void()> printFizz) {
        int i=3;
        for(i=3;i<=n;i+=3){
            if(i%5!=0){
                //----
                while(!waitfizz.load(std::memory_order_acquire)){
                    this_thread::yield();
                }
                // cout<< i<<endl;
                printFizz();
                waitfizz.store(false,memory_order_release);
                waitnumber.store(true,memory_order_release);
                //----
            }
        }
    }

    // printBuzz() outputs "buzz".
    void buzz(function<void()> printBuzz) {
        for(int i=5;i<=n;i+=5){
            if(i%3!=0){
                //----
                while(!waitbuzz.load(std::memory_order_acquire)){
                    this_thread::yield();
                }
                // cout<< i<<endl;
                printBuzz();
                waitbuzz.store(false,memory_order_release);
                waitnumber.store(true,memory_order_release);
                //----
            }
        }
    }

    // printFizzBuzz() outputs "fizzbuzz".
	void fizzbuzz(function<void()> printFizzBuzz) {
        for(int i=15;i<=n;i+=15){
            //----
            while(!waitfb.load(std::memory_order_acquire)){
                this_thread::yield();
            }
                // cout<< i<<endl;
            printFizzBuzz();
            waitfb.store(false,memory_order_release);
            waitnumber.store(true,memory_order_release);
            //----
        }
    }

    // printNumber(x) outputs "x", where x is an integer.
    void number(function<void(int)> printNumber) {
        for(int i=1;i<=n;i++){
            if(i%3==0){
                if(i%5==0){
                    //---
                    waitnumber.store(false,memory_order_release);//
                    waitfb.store(true,memory_order_release);
                    while(!waitnumber.load(std::memory_order_acquire)){
                        this_thread::yield();
                    }
                    //---  
                }else{
                    //---
                    waitnumber.store(false,memory_order_release);//
                    waitfizz.store(true,memory_order_release);
                    while(!waitnumber.load(std::memory_order_acquire)){
                        this_thread::yield();
                    }
                }                
            }else if(i%5==0){
                //---
                waitnumber.store(false,memory_order_release);//
                waitbuzz.store(true,memory_order_release);
                while(!waitnumber.load(std::memory_order_acquire)){
                    this_thread::yield();
                }
                //---
            }else{
                //---
                // cout<< i<<endl;
                printNumber(i);
                //---
            }
        }
    }
};
```





在多线程编程中，**`promise/future`**、**信号量 (`sem_t`)**、**互斥锁**、**条件变量**、**原子操作**等同步原语有各自的优缺点，并适用于不同的场景。以下是对这些同步原语的性能比较、适应场景及其区别的详细分析：

### 1. **性能比较（高频任务切换触发场景）**

在高频任务切换和频繁的线程间通信或同步场景下，不同的同步机制有不同的性能特性。

- **原子操作**（Atomic Operations）：
  - **性能最高**：原子操作是最低层次的同步机制，不涉及任何线程阻塞或上下文切换。它通过 CPU 指令直接保证操作的原子性，无需额外的锁或调度，因此在高频任务切换时性能非常高。
  - **适用场景**：适用于需要低延迟、并发度非常高的场景，比如计数器、标志位等简单的同步需求。
- **互斥锁**（Mutex）：
  - **性能次之**：互斥锁会引入线程阻塞和上下文切换，尤其是在竞争激烈时（例如多个线程竞争同一资源），性能较差。不过，相比于条件变量和信号量，它的实现更简单，适用于较为简单的互斥需求。
  - **适用场景**：适用于需要在多个线程间保护共享资源的场景，特别是在数据修改时。如果共享资源访问并不频繁，互斥锁性能相对较好。
- **条件变量**（Condition Variable）：
  - **性能较低**：条件变量依赖于互斥锁来保护共享资源，并且会使线程在等待条件时进入阻塞状态，这会涉及到上下文切换，因此性能较低。
  - **适用场景**：适用于生产者/消费者模式、事件通知等场景，其中一个线程需要等待另一个线程的某个条件满足。高频切换时，条件变量的性能通常较差。
- **信号量**（Semaphore）：
  - **性能较低**：信号量也会导致线程阻塞和上下文切换，尤其是在高竞争情况下，性能会比原子操作差一些，但比条件变量稍好。
  - **适用场景**：适用于需要管理多个线程访问共享资源的场景，如资源池、线程池、限制访问的场景（例如限制最大并发数）。
- **`promise/future`**：
  - **性能较低**：`promise` 和 `future` 会涉及线程阻塞和唤醒机制，通常用于线程间传递结果或通知，虽然实现简单且易于理解，但由于需要线程间的通信，它们在高频任务切换时的性能相对较差。
  - **适用场景**：适用于任务完成的通知、线程间结果传递的场景。它们本质上是一种同步原语，适合需要传递某个事件或结果的场景。

### 2. **适应场景区别**

- **原子操作（Atomic Operations）**：

  - 使用场景

    ：

    - 高频度的并发访问。
    - 不涉及复杂的资源管理和条件判断，仅需对简单数据（如计数器、状态标志等）进行操作。
    - 优点是高效和无阻塞，适用于对性能要求极高的场景。

  - 限制

    ：

    - 适用于非常简单的同步任务，不适合复杂的资源访问或依赖关系的同步。

- **互斥锁（Mutex）**：

  - 使用场景

    ：

    - 用于保护共享资源，如修改共享变量、管理文件访问等。
    - 适合单一线程对共享资源的独占访问。

  - 限制

    ：

    - 如果在高竞争的情况下频繁进行加锁和解锁，性能可能会受到影响，尤其是在没有适当优化的情况下（例如，过多的上下文切换）。

- **条件变量（Condition Variable）**：

  - 使用场景

    ：

    - 适用于生产者/消费者模式，需要线程间同步的场景。
    - 适合等待某些条件满足时再执行任务的场景，如等待缓冲区非空、等待特定信号等。

  - 限制

    ：

    - 需要互斥锁配合使用，在高频任务切换的场景下，阻塞等待可能带来性能瓶颈。

- **信号量（Semaphore）**：

  - 使用场景

    ：

    - 用于控制多个线程对共享资源的访问，通常是对资源进行计数控制的场景。
    - 适合线程池、资源池等场景，尤其是在有限资源的情况下。

  - 限制

    ：

    - 比条件变量稍微高效，但依然涉及线程阻塞和上下文切换。在竞争激烈的场景下，性能可能会受到影响。

- **`promise/future`**：

  - 使用场景

    ：

    - 适合在一个线程执行某个操作后，通知另一个线程继续执行的场景。
    - 适合需要线程间传递任务结果、事件通知等场景。

  - 限制

    ：

    - 由于涉及到阻塞、唤醒机制，性能相对较差，尤其是在高频任务切换的场景下。

### 3. **总结：**

| 同步原语             | 性能特性           | 适用场景                                 | 限制                                       |
| -------------------- | ------------------ | ---------------------------------------- | ------------------------------------------ |
| **原子操作**         | 性能最优，无阻塞   | 高频度并发操作，简单的计数器、标志位等   | 适用于简单的同步，无法解决复杂依赖关系     |
| **互斥锁**           | 中等（阻塞、竞争） | 保护共享资源，线程独占访问               | 高竞争时性能较差，易导致死锁               |
| **条件变量**         | 性能较低（阻塞）   | 生产者/消费者模式，等待某些条件的发生    | 高频切换时性能较差，依赖互斥锁             |
| **信号量**           | 性能较低（阻塞）   | 控制多个线程访问共享资源，线程池、资源池 | 高频任务切换时性能较差                     |
| **`promise/future`** | 性能较低（阻塞）   | 线程间事件通知、传递任务结果             | 高频切换时性能较差，适用于通知而非高频任务 |

- **高频任务切换场景**：对于非常高频的任务切换，**原子操作**是最优的选择。它避免了线程阻塞和上下文切换，提供了极高的性能。
- **复杂资源同步**：当需要线程间独占共享资源时，**互斥锁**是常见的选择。对于需要更复杂的同步机制（如生产者/消费者），可以使用**条件变量**。
- **资源管理与线程池**：当涉及多个线程访问有限资源时，**信号量**是一个很好的选择。
- **线程间通知与结果传递**：对于线程间的任务通知或结果传递，**`promise/future`** 是适合的工具。

每种同步原语的性能和适应场景都各有优缺点，选择合适的同步机制可以帮助提高程序的效率和稳定性。

你的问题非常好，涉及到了**无锁同步**的本质、它的优势以及为什么在某些情况下它的性能可能反而更差。

### 1. **`promise/future` 的无锁机制为什么性能较差？**

`promise/future` 机制本身并不是“完全无锁”的，它的性能劣化是由于它内部还是依赖于线程的**阻塞**和**唤醒**机制。在这种情况下，**无锁**并不意味着没有任何线程调度或阻塞，而是指避免了传统的锁竞争（如互斥锁）的情况。

`promise/future` 主要用于线程间同步和传递事件，虽然它避免了传统的互斥锁（mutex）竞争，但它依然会涉及到以下几个性能瓶颈：

- **线程阻塞与唤醒**：
  - 在 `future.get()` 调用时，如果 `promise.set_value()` 没有被调用，当前线程会被阻塞，等待另一个线程设置值。这种阻塞和唤醒机制可能导致线程上下文切换，而上下文切换本身会引入开销。
  - 阻塞操作本身就涉及到线程的挂起、恢复等，这些操作会导致CPU周期的浪费，尤其是在高频切换的场景下。
- **内存屏障和同步机制**：
  - `promise/future` 内部需要保证多线程之间的同步正确性，因此需要一些同步原语来防止竞争条件，这些同步操作（如原子操作、内存屏障等）可能导致额外的性能开销。
- **高频场景的开销**：
  - 在高频任务切换场景中，`promise/future` 机制的每次阻塞和唤醒都需要执行线程调度，这导致了性能的下降。相比之下，原子操作（atomic operations）由于直接在CPU级别进行同步，不涉及阻塞和唤醒，因此性能更高。

### 2. **为什么人们追求无锁同步？**

追求无锁同步的主要目的是**减少线程间的竞争和上下文切换**，提高多线程程序的性能。**无锁**的同步原语能够在多线程并发访问共享资源时避免显式的锁竞争，从而带来几个显著的优势：

#### **减少上下文切换**：

- 当一个线程在等待锁（例如互斥锁）时，通常会进入阻塞状态，操作系统会将它从CPU中移除，并调度其他线程运行。这会导致**上下文切换**（context switching），是一个相对昂贵的操作。上下文切换不仅需要保存和恢复线程的状态，还需要花费时间进行调度。
- 无锁同步避免了这种显式的阻塞和唤醒，减少了上下文切换的次数，能够显著提升程序的响应速度和吞吐量。

#### **提高并发度**：

- 在锁竞争严重的情况下（多个线程争夺同一个锁），锁的开销可能会非常大，导致程序性能下降。而无锁同步能够允许更多线程并行工作，而不会由于锁的争夺而产生性能瓶颈。
- 特别是对于高并发环境（如多核处理器），无锁同步可以使得多个线程并行执行，从而充分利用系统资源。

#### **避免死锁**：

- 在传统的锁（如互斥锁）中，可能会出现死锁问题（两个或多个线程互相等待对方释放锁，导致无法继续执行）。无锁算法通过避免显式的锁操作，可以减少死锁的风险。
- 无锁同步避免了传统锁的死锁和优先级反转问题，使得程序更可靠。

#### **减少资源消耗**：

- 使用锁时，系统会为每个线程管理锁的状态，在高频访问时，可能会消耗大量的内存和CPU资源。
- 无锁同步不需要这种锁状态的管理，因此在高并发场景下，能有效减少资源消耗。

### 3. **无锁同步的挑战与适用场景**

虽然无锁同步有很多优势，但它并不是在所有场景下都是最优选择。无锁同步的挑战包括：

- **复杂的实现**：无锁同步通常需要使用低级的原子操作（如CAS，Compare and Swap），这些操作在某些情况下会非常复杂。设计和实现无锁算法需要更多的考虑和细致的设计，否则可能会导致潜在的错误或性能问题。
- **适用场景有限**：无锁同步更适合于简单的计数器、标志位等共享资源的访问，而对于复杂的数据结构（例如链表、哈希表等），实现无锁操作会更加困难，而且可能不如传统锁方案可靠。
- **可能的性能退化**：虽然无锁同步避免了传统锁的竞争，但在一些场景下，频繁的原子操作、内存屏障和复杂的同步逻辑可能导致性能问题。例如，在高竞争的情况下，如果线程数量非常大，无锁算法可能会因为高频的CAS失败导致“自旋”（spin）时间过长，反而影响性能。

### 4. **总结：**

- **`promise/future` 的性能差**：`promise/future` 是一个无锁的同步机制，但它会引起线程阻塞和唤醒，这导致了上下文切换和线程调度的开销，尤其是在高频任务切换时，性能较差。它的设计目标是简单易用的线程间通信和同步，而不是针对极端性能优化的场景。
- **无锁同步的优势**：
  - 减少上下文切换，提高并发度。
  - 避免死锁。
  - 减少资源消耗。
- **无锁的挑战**：
  - 复杂的实现和使用场景的限制。
  - 在某些高竞争场景下，无锁的算法可能比传统锁的实现性能更差。

**追求无锁同步**的意义在于尽量减少线程之间的竞争、上下文切换和资源消耗，从而在高并发和低延迟的场景中提高性能，但并不是所有场景都适合无锁同步。在选择同步原语时，需要根据具体的应用场景来权衡性能、可靠性和复杂性。