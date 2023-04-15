---
layout: post
title: Rust Daily Learning - Day 21 - Unsafe Rust
categories: Rust
description: Exploring Unsafe Rust for more control over low-level details
keywords: Rust, Programming, Unsafe, Low-level
---
# Rust Daily Learning - Day 21

- [Introduction](#introduction)
- [Unsafe Code](#unsafe-code)
- [Unsafe Functions](#unsafe-functions)
- [Unsafe Traits](#unsafe-traits)
- [Unsafe Blocks](#unsafe-blocks)

## Introduction

Rust is designed to provide strong guarantees about memory safety and prevent data races. However, in some cases, you may need more control over the low-level details of your code or interact with unsafe external code. This is where unsafe Rust comes in.

## Unsafe Code

Unsafe code allows you to perform actions that would normally be disallowed by the Rust compiler due to potential memory safety issues. When writing unsafe code, you take on the responsibility of ensuring memory safety.

Common use cases for unsafe code include:

- Interfacing with C libraries
- Performance-critical sections
- Implementing low-level data structures

## Unsafe Functions

An unsafe function is a function that contains unsafe code. To declare an unsafe function, you need to add the `unsafe` keyword before the `fn` keyword:

```rust
unsafe fn my_unsafe_function() {
    // unsafe code
}
```

To call an unsafe function, you need to use an unsafe block (see below).

## Unsafe Traits

An unsafe trait is a trait that requires the implementor to uphold certain invariants. To declare an unsafe trait, you need to add the `unsafe` keyword before the `trait` keyword:

```rust
unsafe trait MyUnsafeTrait {
    fn some_method(&self);
}
```

When implementing an unsafe trait, you also need to use the `unsafe` keyword:

```rust
struct MyStruct;

unsafe impl MyUnsafeTrait for MyStruct {
    fn some_method(&self) {
        // unsafe code
    }
}
```

## Unsafe Blocks

An unsafe block is a block of code where you explicitly assert that the code inside the block is memory-safe. To create an unsafe block, you need to use the `unsafe` keyword followed by a pair of curly braces:

```rust
unsafe {
    // unsafe code
}
```

When you call an unsafe function or perform an unsafe operation, you need to use an unsafe block:

```rust
fn main() {
    unsafe {
        my_unsafe_function();
    }
}
```

Remember, when writing unsafe code, you take on the responsibility of ensuring memory safety. Always be cautious when using unsafe code and only use it when absolutely necessary.