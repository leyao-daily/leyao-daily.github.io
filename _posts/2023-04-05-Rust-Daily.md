---
layout: post
title: Rust Daily Learning - Day 10 - Multithreading and Concurrency
categories: Rust
description: Learn about multithreading and concurrency in Rust
keywords: Rust, Programming, Daily Learning, Multithreading, Concurrency
---
# Rust Daily Learning - Day 10

- [Overview](#overview)
- [Threads in Rust](#threads-in-rust)
- [Sharing Data between Threads](#sharing-data-between-threads)
- [Atomic Operations and Mutexes](#atomic-operations-and-mutexes)

## Overview

Welcome to Day 10 of the Rust daily learning series! Today, we'll explore multithreading and concurrency in Rust, and learn how to create and manage threads, share data between them, and ensure safe access to shared resources.

## Threads in Rust

Rust provides built-in support for creating and managing threads. To create a new thread, you can use the `std::thread::spawn` function, which takes a closure as its argument. The closure contains the code that the new thread will execute.

```rust
use std::thread;
use std::time::Duration;

fn main() {
    let handle = thread::spawn(|| {
        for i in 1..10 {
            println!("Hi number {} from the spawned thread!", i);
            thread::sleep(Duration::from_millis(1));
        }
    });

    for i in 1..5 {
        println!("Hi number {} from the main thread!", i);
        thread::sleep(Duration::from_millis(1));
    }

    handle.join().unwrap();
}
```

## Sharing Data between Threads

In Rust, you can share data between threads using `Arc` (Atomic Reference Counting) and `Mutex` (Mutual Exclusion). `Arc` allows multiple threads to have read-only access to the same data, while `Mutex` ensures that only one thread at a time can access the data.

```rust
use std::sync::{Arc, Mutex};
use std::thread;

fn main() {
    let counter = Arc::new(Mutex::new(0));
    let mut handles = vec![];

    for _ in 0..10 {
        let counter = Arc::clone(&counter);
        let handle = thread::spawn(move || {
            let mut num = counter.lock().unwrap();
            *num += 1;
        });
        handles.push(handle);
    }

    for handle in handles {
        handle.join().unwrap();
    }

    println!("Result: {}", *counter.lock().unwrap());
}
```

## Atomic Operations and Mutexes

For simple atomic operations, you can use the `Atomic` types provided by the `std::sync::atomic` module. These types allow you to perform atomic operations, such as `fetch_add`, `compare_and_swap`, and others, without the need for a Mutex.

```rust
use std::sync::atomic::{AtomicUsize, Ordering};
use std::thread;

static COUNTER: AtomicUsize = AtomicUsize::new(0);

fn main() {
    let mut handles = vec![];

    for _ in 0..10 {
        let handle = thread::spawn(|| {
            for _ in 0..1000 {
                COUNTER.fetch_add(1, Ordering::SeqCst);
            }
        });
        handles.push(handle);
    }

    for handle in handles {
        handle.join().unwrap();
    }

    println!("Result: {}", COUNTER.load(Ordering::SeqCst));
}
```

In this example, we use an `AtomicUsize` to perform atomic addition without the need for a Mutex. This can provide better performance in some cases, as it avoids the overhead of locking and unlocking a Mutex.