---
layout: post
title: Rust Daily Learning - Day 6 - Structs
categories: Rust
description: Learn how to define and work with structs in Rust
keywords: Rust, Programming, Daily Learning, Structs, Custom Data Types
---
# Rust Daily Learning - Day 6

- [Overview](#overview)
- [Defining Structs](#defining-structs)
- [Instantiating Structs](#instantiating-structs)
- [Accessing and Modifying Fields](#accessing-and-modifying-fields)
- [Tuple Structs](#tuple-structs)

## Overview

Welcome to Day 6 of the Rust daily learning series! Today, we'll introduce structs, a powerful way to define custom data types in Rust. Structs are particularly useful when you want to group related pieces of data together.

## Defining Structs

To define a struct, use the `struct` keyword followed by the name of the struct and its fields, enclosed in curly braces `{}`. Here's an example:

```rust
struct User {
    username: String,
    email: String,
    sign_in_count: u64,
    active: bool,
}
```

## Instantiating Structs

To create an instance of a struct, specify the name of the struct followed by the values for each field, enclosed in curly braces `{}`. Here's an example:

```rust
let user1 = User {
    email: String::from("someone@example.com"),
    username: String::from("someusername123"),
    active: true,
    sign_in_count: 1,
};
```

## Accessing and Modifying Fields

You can access the fields of a struct using dot notation. To modify a field, you must make the struct instance mutable. Here's an example:

```rust
fn main() {
    let mut user1 = User {
        email: String::from("someone@example.com"),
        username: String::from("someusername123"),
        active: true,
        sign_in_count: 1,
    };

    user1.email = String::from("anotheremail@example.com");

    println!("User email: {}", user1.email);
}
```

## Tuple Structs

Rust also supports tuple structs, which are structs with named fields but no field names. Tuple structs are useful when you want to give a tuple a name for better readability. To define a tuple struct, use the `struct` keyword followed by the name of the tuple struct and its field types, enclosed in parentheses `()`.

```rust
struct Color(i32, i32, i32);
struct Point(i32, i32, i32);

fn main() {
    let black = Color(0, 0, 0);
    let origin = Point(0, 0, 0);
}
```

That's it for today's lesson on structs in Rust. In the next installment, we'll explore enums, another powerful way to define custom data types in Rust. Keep learning and see you soon!