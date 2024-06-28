# 原子操作和多线程


Rust 的原子操作主要通过标准库中的 `std::sync::atomic` 模块提供。原子操作允许在多线程环境中进行无锁并发编程，从而避免数据竞争和其它并发问题。

## 主要的原子类型

Rust 提供了几种常见的原子类型，这些类型都在 `std::sync::atomic` 模块中：

1. `AtomicBool`：原子布尔类型。
2. `AtomicIsize`：原子有符号整数类型。
3. `AtomicUsize`：原子无符号整数类型。
4. `AtomicI8`、`AtomicI16`、`AtomicI32`、`AtomicI64`、`AtomicI128`：原子有符号整数类型。
5. `AtomicU8`、`AtomicU16`、`AtomicU32`、`AtomicU64`、`AtomicU128`：原子无符号整数类型。

这些原子类型支持一些基本操作，如加载、存储、交换和比较并交换。

## 常用操作

以下是一些常用的原子操作及其用法：

### 1. `load` 和 `store`

`load` 和 `store` 操作用于读取和写入原子变量的值。这些操作可以指定内存排序（Memory Ordering），如 `Relaxed`、`Acquire`、`Release`、`AcqRel` 和 `SeqCst`。

```rust
use std::sync::atomic::{AtomicI32, Ordering};

fn main() {
    let atomic_val = AtomicI32::new(5);
  
    // 读取原子变量的值
    let val = atomic_val.load(Ordering::SeqCst);
    println!("Value: {}", val);

    // 写入原子变量
    atomic_val.store(10, Ordering::SeqCst);
    let new_val = atomic_val.load(Ordering::SeqCst);
    println!("New Value: {}", new_val);
}
```

### 2. `swap`

`swap` 操作用于交换原子变量的值。

```rust
use std::sync::atomic::{AtomicI32, Ordering};

fn main() {
    let atomic_val = AtomicI32::new(5);
  
    // 交换值
    let old_val = atomic_val.swap(10, Ordering::SeqCst);
    println!("Old Value: {}", old_val);
    let new_val = atomic_val.load(Ordering::SeqCst);
    println!("New Value: {}", new_val);
}
```

### 3. `compare_and_swap` 和 `compare_exchange`

`compare_and_swap` 和 `compare_exchange` 操作用于进行原子的比较并交换操作。如果当前值等于期望值，则将其交换为新的值。

```rust
use std::sync::atomic::{AtomicI32, Ordering};

fn main() {
    let atomic_val = AtomicI32::new(5);
  
    // 比较并交换
    let old_val = atomic_val.compare_and_swap(5, 10, Ordering::SeqCst);
    println!("Old Value: {}", old_val);
    let new_val = atomic_val.load(Ordering::SeqCst);
    println!("New Value: {}", new_val);

    // 使用 compare_exchange
    let result = atomic_val.compare_exchange(10, 15, Ordering::Acquire, Ordering::Relaxed);
    match result {
        Ok(val) => println!("Exchanged Value: {}", val),
        Err(val) => println!("Failed to Exchange, Current Value: {}", val),
    }
}
```

### 4. `fetch_add` 和 `fetch_sub`

`fetch_add` 和 `fetch_sub` 操作用于原子地增加或减少变量的值。

```rust
use std::sync::atomic::{AtomicI32, Ordering};

fn main() {
    let atomic_val = AtomicI32::new(5);
  
    // 原子增加
    let old_val = atomic_val.fetch_add(10, Ordering::SeqCst);
    println!("Old Value: {}", old_val);
    let new_val = atomic_val.load(Ordering::SeqCst);
    println!("New Value: {}", new_val);

    // 原子减少
    let old_val = atomic_val.fetch_sub(3, Ordering::SeqCst);
    println!("Old Value: {}", old_val);
    let new_val = atomic_val.load(Ordering::SeqCst);
    println!("New Value: {}", new_val);
}
```

## 内存排序

内存排序（Memory Ordering）定义了原子操作在多线程环境中的可见性和顺序。Rust 提供了几种内存排序选项：

- `Ordering::Relaxed`：不做任何同步保证，只保证操作的原子性。
- `Ordering::Acquire`：操作之前的所有读写不会被重排序到该操作之后。
- `Ordering::Release`：操作之后的所有读写不会被重排序到该操作之前。
- `Ordering::AcqRel`：结合 `Acquire` 和 `Release` 的效果。
- `Ordering::SeqCst`：顺序一致性，确保所有操作按程序顺序执行。

选择合适的内存排序非常重要，可以根据具体的并发需求来选择。

## 总结

Rust 的原子操作为开发高效且安全的多线程应用提供了基础。通过 `std::sync::atomic` 模块，您可以执行各种原子操作，以确保多线程环境下的数据一致性和安全性。在使用原子操作时，了解内存排序以及如何正确使用这些操作是关键。
