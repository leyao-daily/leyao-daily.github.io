---
layout: post
title: Rust Daily Learning - Day 5 - Ownership
categories: Rust
description: Discover the concept of ownership in Rust and its role in memory management
keywords: Rust, Programming, Daily Learning, Ownership, Memory Management, Borrowing, References
---
# Rust Daily Learning - Day 5

- [Overview](#overview)
- [Understanding Ownership](#understanding-ownership)
- [Borrowing](#borrowing)
- [References](#references)

## Overview

Welcome to Day 5 of the Rust daily learning series! Today, we'll delve into the concept of ownership, a core principle of Rust's memory management system. Understanding ownership is crucial for writing efficient, safe, and error-free Rust programs.

## Understanding Ownership

In Rust, memory is managed through a system of ownership with a set of rules that the compiler checks at compile time. Ownership rules ensure memory safety without the need for a garbage collector. Here are the three key rules:

1. Each value in Rust has a variable that's called its owner.
2. There can only be one owner at a time.
3. When the owner goes out of scope, the value will be dropped.

Consider the following example:

```rust
fn main() {
    let s = String::from("hello");
    takes_ownership(s);
    // println!("{}", s); // This line would cause a compilation error
}

fn takes_ownership(some_string: String) {
    println!("{}", some_string);
}
```

## Borrowing

Instead of transferring ownership, Rust allows you to create references to a value, which is called borrowing. Borrowing enables you to use a value in a function without taking ownership of it. Here's an example:

```rust
fn main() {
    let s = String::from("hello");
    calculate_length(&s);
    println!("The length of '{}' is {}.", s, calculate_length(&s));
}

fn calculate_length(s: &String) -> usize {
    s.len()
}
```

## References

References allow you to access a value without taking ownership. There are two types of references:

1. Immutable References: These references allow read-only access to a value.
2. Mutable References: These references allow read-write access to a value.

To create a mutable reference, use the `&mut` keyword:

```rust
fn main() {
    let mut s = String::from("hello");
    change(&mut s);
    println!("The new string is: {}", s);
}

fn change(s: &mut String) {
    s.push_str(", world!");
}
```

That's it for today's lesson on ownership in Rust. In the next installment, we'll explore structs, a powerful way to define custom data types. Keep learning and see you soon!