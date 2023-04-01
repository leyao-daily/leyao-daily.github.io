---
layout: post
title: Rust Daily Learning - Day 7 - Enums
categories: Rust
description: Learn how to define and work with enums in Rust
keywords: Rust, Programming, Daily Learning, Enums, Custom Data Types, Pattern Matching
---
# Rust Daily Learning - Day 7

- [Overview](#overview)
- [Defining Enums](#defining-enums)
- [Enum Variants](#enum-variants)
- [Pattern Matching](#pattern-matching)

## Overview

Welcome to Day 7 of the Rust daily learning series! Today, we'll introduce enums, another powerful way to define custom data types in Rust. Enums, short for enumerations, allow you to define a type that can have several different values, each with its own variant.

## Defining Enums

To define an enum, use the `enum` keyword followed by the name of the enum and its variants, enclosed in curly braces `{}`. Here's an example:

```rust
enum IpAddrKind {
    V4,
    V6,
}
```

## Enum Variants

Each variant of an enum can store different data types. You can specify the data types for each variant by adding them in parentheses after the variant name. Here's an example:

```rust
enum IpAddr {
    V4(u8, u8, u8, u8),
    V6(String),
}

fn main() {
    let home = IpAddr::V4(127, 0, 0, 1);
    let loopback = IpAddr::V6(String::from("::1"));
}
```

## Pattern Matching

Pattern matching is a powerful feature in Rust that allows you to destructure enums and perform operations based on their variants. The `match` keyword is used for pattern matching, and each arm of the match expression specifies a pattern and the code to run when the pattern is matched.

```rust
enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter,
}

fn value_in_cents(coin: Coin) -> u32 {
    match coin {
        Coin::Penny => 1,
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter => 25,
    }
}

fn main() {
    let coin = Coin::Dime;
    println!("The value of the coin is: {} cents", value_in_cents(coin));
}
```

That's it for today's lesson on enums in Rust. Enums are a versatile way to define custom data types with different variants and associated data. Keep learning and see you in the next installment!