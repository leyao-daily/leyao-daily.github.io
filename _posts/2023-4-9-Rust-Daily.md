---
layout: post
title: Rust Daily Learning - Day 14 - Closures
categories: Rust
description: Learn about closures in Rust
keywords: Rust, Programming, Daily Learning, Closures, Functions, Anonymous Functions
---
# Rust Daily Learning - Day 14

- [Overview](#overview)
- [Closures](#closures)

## Overview

Welcome to Day 14 of the Rust daily learning series! Today, we'll learn about closures in Rust, which are anonymous functions that can capture their surrounding environment.

## Closures

Closures are functions that can capture values from the scope in which they are defined. They are also known as anonymous functions, as they don't have a name. Closures are a powerful feature in Rust, allowing you to create flexible and reusable code.

Here's a basic example of a closure:

```rust
fn main() {
    let add_one = |x: i32| x + 1;
    let result = add_one(5);
    println!("The result is: {}", result);
}
```

In this example, we define a closure `add_one` that takes a single argument `x` of type `i32` and returns `x + 1`. We then call this closure with the argument `5`, which returns `6`.

Closures can also capture variables from their surrounding environment. Here's an example of a closure capturing a variable:

```rust
fn main() {
    let x = 5;
    let add_x = |y: i32| y + x;
    let result = add_x(3);
    println!("The result is: {}", result);
}
```

In this example, the closure `add_x` captures the variable `x` from its environment, allowing it to use `x` inside the closure. When we call `add_x(3)`, it returns `8`.

Rust has three different closure types, each with its own set of rules for capturing variables:

1. `Fn` - Borrows the captured variables immutably.
2. `FnMut` - Borrows the captured variables mutably.
3. `FnOnce` - Takes ownership of the captured variables.

Understanding closures and their various types will help you write more flexible and concise code in Rust.