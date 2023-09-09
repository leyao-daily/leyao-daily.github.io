---
layout: post
title: Rust Daily Learning - Day 19 - Channels for Thread Communication
categories: Rust
description: Learn about channels for thread communication in Rust
keywords: Rust, Programming, Channels, Concurrency, Threads
---
# Rust Daily Learning - Day 19

## Channels for Thread Communication

Channels in Rust are a way to send data between threads, allowing them to communicate with each other. The standard library provides the `std::sync::mpsc` module, which stands for "multiple producer, single consumer". It offers a multiple-producer, single-consumer channel that you can use to send messages between threads.

### Creating a Channel

To create a channel, use the `mpsc::channel` function, which returns a tuple with a transmitter and a receiver:

```rust
use std::sync::mpsc;
use std::thread;
use std::time::Duration;

fn main() {
    let (tx, rx) = mpsc::channel();

    thread::spawn(move || {
        let val = String::from("Hello, Rust!");
        tx.send(val).unwrap();
    });

    let received = rx.recv().unwrap();
    println!("Received: {}", received);
}
```

In this example, we create a channel with a transmitter `tx` and a receiver `rx`. We spawn a new thread, sending a `String` value through the channel by calling `tx.send(val).unwrap()`. The main thread waits to receive the value with `rx.recv().unwrap()` and prints it.

### Sending Multiple Messages

You can use channels to send multiple messages between threads:

```rust
use std::sync::mpsc;
use std::thread;
use std::time::Duration;

fn main() {
    let (tx, rx) = mpsc::channel();
    let tx1 = mpsc::Sender::clone(&tx);

    thread::spawn(move || {
        let messages = vec![
            String::from("Hello"),
            String::from("from"),
            String::from("the"),
            String::from("thread"),
        ];

        for msg in messages {
            tx1.send(msg).unwrap();
            thread::sleep(Duration::from_secs(1));
        }
    });

    thread::spawn(move || {
        let messages = vec![
            String::from("more"),
            String::from("messages"),
            String::from("for"),
            String::from("you"),
        ];

        for msg in messages {
            tx.send(msg).unwrap();
            thread::sleep(Duration::from_secs(1));
        }
    });

    for received in rx {
        println!("Received: {}", received);
    }
}
```

In this example, we clone the transmitter to have two different transmitters for two different threads. Each thread sends a series of messages through the channel. The main thread receives messages from both threads and prints them as they arrive.