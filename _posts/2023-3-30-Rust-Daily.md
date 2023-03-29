---
layout: post
title: Rust Daily Learning - Day 4 - Functions
categories: Rust
description: Explore functions and their usage in Rust programs
keywords: Rust, Programming, Daily Learning, Functions, Parameters, Return Values
---
# Rust Daily Learning - Day 4

- [Overview](#overview)
- [Defining Functions](#defining-functions)
- [Function Parameters](#function-parameters)
- [Return Values](#return-values)

## Overview

Welcome to Day 4 of the Rust daily learning series! Today, we will dive into functions, an essential building block of any Rust program. Functions allow you to organize your code into reusable and modular components, making it more efficient and maintainable.

## Defining Functions

In Rust, you define functions using the `fn` keyword followed by the function name, a parenthesized list of input parameters, and a code block wrapped in braces. The following example demonstrates a simple function definition:

```rust
fn main() {
    print_hello();
}

fn print_hello() {
    println!("Hello, world!");
}
```

## Function Parameters

To pass values to a function, you can define input parameters. In Rust, you need to specify the type of each parameter. Here's an example:

```rust
fn main() {
    print_sum(5, 6);
}

fn print_sum(a: i32, b: i32) {
    let sum = a + b;
    println!("The sum is: {}", sum);
}
```

## Return Values

Functions can also return values. To specify the return type, add an arrow (`->`) followed by the type after the input parameters. To return a value, use the `return` keyword, or simply end the function with an expression without a semicolon. Here's an example:

```rust
main() {
    let result = multiply(3, 4);
    println!("The product is: {}", result);
}

fn multiply(x: i32, y: i32) -> i32 {
    x * y
}
```

That's it for today's lesson on functions in Rust. In the next installment, we'll explore ownership, a key concept in Rust's memory management system. Keep learning and see you soon!

