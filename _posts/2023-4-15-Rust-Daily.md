---
layout: post
title: Rust Daily Learning - Day 20 - Async Programming in Rust
categories: Rust
description: Introduction to async programming in Rust
keywords: Rust, Programming, Async, Concurrency, Futures
---
# Rust Daily Learning - Day 20

- [Introduction](#introduction)
- [Futures](#futures)
- [Async/Await](#async-await)
- [Tokio Runtime](#tokio-runtime)

## Introduction

Asynchronous programming allows you to write non-blocking code, which can greatly improve the efficiency and performance of your application. In Rust, async programming is supported through the use of Futures, async/await syntax, and runtimes like Tokio.

## Futures

A Future is a value that represents a computation that may not have completed yet. In Rust, the `std::future::Future` trait defines the behavior of a future. You can create a future by implementing the `Future` trait or using async functions.

Here's an example of a simple future that immediately returns a value:

```rust
use std::future::Future;
use std::pin::Pin;
use std::task::{Context, Poll};

struct ImmediateValue(i32);

impl Future for ImmediateValue {
    type Output = i32;

    fn poll(self: Pin<&mut Self>, _cx: &mut Context<'_>) -> Poll<Self::Output> {
        Poll::Ready(self.0)
    }
}
```

## Async/Await

Rust provides the `async` and `await` keywords to make working with futures easier. An `async` function returns a future, and you can use `await` within an `async` function to wait for the completion of another future.

Here's an example of an async function that sleeps for a given duration:

```rust
use std::time::Duration;
use tokio::time::sleep;

async fn sleep_for(duration: Duration) {
    sleep(duration).await;
}
```

## Tokio Runtime

Tokio is a popular async runtime for Rust, providing an event-driven platform for executing asynchronous tasks. To use Tokio, add it to your `Cargo.toml`:

```toml
[dependencies]
tokio = { version = "1", features = ["full"] }
```

Here's an example of using Tokio to execute an async function:

```rust
use std::time::Duration;
use tokio::runtime::Runtime;

fn main() {
    let rt = Runtime::new().unwrap();
    rt.block_on(async {
        let duration = Duration::from_secs(2);
        println!("Starting to sleep");
        sleep_for(duration).await;
        println!("Finished sleeping");
    });
}
```

With this knowledge, you can now start exploring async programming in Rust!