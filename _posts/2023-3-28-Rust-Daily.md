---
layout: post
title: Rust Daily Learning - Day 2 - Variables and Data Types
categories: Rust
description: Exploring variables, data types, and mutability in Rust
keywords: Rust, Programming, Daily Learning, Variables, Data Types, Mutability
---
# Rust Daily Learning - Day 2

- [Overview](#overview)
- [Variables and Mutability](#variables-and-mutability)
- [Data Types](#data-types)

## Overview

Welcome back to the Rust daily learning series! Today, we will dive into variables, data types, and mutability in Rust. Understanding these fundamentals will help you become proficient in Rust programming.

## Variables and Mutability

By default, variables in Rust are immutable, meaning their values cannot be changed once assigned. To create a mutable variable, use the `mut` keyword:

```rust
fn main() {
    let mut x = 5;
    println!("The value of x is: {}", x);
    x = 6;
    println!("The value of x is: {}", x);
}
```

In this example, we create a mutable variable `x`, set its value to 5, and then change its value to 6.

## Data Types

Rust is a statically-typed language, which means that the data type of a variable must be known at compile time. Rust has two categories of data types: scalar and compound.

### Scalar Types

Scalar types represent a single value. There are four primary scalar types in Rust:

1. Integers - signed (`i8`, `i16`, `i32`, `i64`, `i128`) and unsigned (`u8`, `u16`, `u32`, `u64`, `u128`). The default integer type is `i32`.
2. Floating-point numbers - `f32` and `f64`. The default is `f64`.
3. Booleans - `bool`. The values can be `true` or `false`.
4. Characters - `char`. Single Unicode scalar values enclosed in single quotes, e.g., `'A'`, `'ß'`, `'🤖'`.

### Compound Types

Compound types group multiple values into one type. Rust has two compound types:

1. Tuples - A fixed-size collection of values with different types. Example:

```rust
fn main() {
    let tup: (i32, f64, u8) = (500, 6.4, 1);
    let (x, y, z) = tup;
    println!("The value of y is: {}", y);
}
```

1. Arrays - A collection of values with the same type and fixed length. Example:

```rust
fn main() {
    let arr: [i32; 5] = [1, 2, 3, 4, 5];
    let first = arr[0];
    let second = arr[1];
    println!("The values are: {} and {}", first, second);
}
```

That's all for today! In the next installment, we will learn about control flow in Rust, including conditionals and loops. Stay tuned and keep learning!