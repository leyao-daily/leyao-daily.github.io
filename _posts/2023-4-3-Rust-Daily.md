---
layout: post
title: Rust Daily Learning - Day 8 - Error Handling
categories: Rust
description: Learn how to handle errors effectively in Rust
keywords: Rust, Programming, Daily Learning, Error Handling, Result, Option, unwrap, expect
---
# Rust Daily Learning - Day 8

- [Overview](#overview)
- [Result and Option Enums](#result-and-option-enums)
- [Unwrap and Expect](#unwrap-and-expect)
- [The ? Operator](#the-question-mark-operator)

## Overview

Welcome to Day 8 of the Rust daily learning series! Today, we'll dive into error handling in Rust. Error handling is an essential aspect of programming, as it helps you deal with unexpected situations and ensure your program runs smoothly.

## Result and Option Enums

Rust uses enums to represent the possibility of success or failure in a function. The `Result` and `Option` enums are commonly used for this purpose.

- `Result`: Represents a successful or failed computation. It has two variants: `Ok` for success and `Err` for failure.
- `Option`: Represents a value that might be present or absent. It has two variants: `Some` for a present value and `None` for an absent value.

Here's an example of using the `Result` enum:

```rust
use std::fs::File;

fn main() {
    let f = File::open("hello.txt");

    let f = match f {
        Ok(file) => file,
        Err(error) => panic!("Problem opening the file: {:?}", error),
    };
}
```

## Unwrap and Expect

The `unwrap` and `expect` methods are helpful shortcuts for working with `Result` and `Option` enums. They automatically handle the `Ok` or `Some` variant and return the value inside. If the `Err` or `None` variant is encountered, they will panic and terminate the program.

- `unwrap`: Returns the value if `Ok` or `Some`, otherwise panics.
- `expect`: Similar to `unwrap`, but allows you to provide a custom panic message.

```rust
let f = File::open("hello.txt").unwrap(); // Will panic if the file cannot be opened.

let f = File::open("hello.txt").expect("Failed to open hello.txt"); // Will panic with a custom message if the file cannot be opened.
```

## The ? Operator

The `?` operator is another convenient way to handle errors in Rust. When placed after a function that returns a `Result`, it will automatically return the `Err` variant if it's encountered, or continue executing the code with the value inside the `Ok` variant.

```rust
use std::io;
use std::io::Read;
use std::fs::File;

fn read_username_from_file() -> Result<String, io::Error> {
    let mut f = File::open("hello.txt")?;
    let mut s = String::new();
    f.read_to_string(&mut s)?;
    Ok(s)
}
```

That's it for today's lesson on error handling in Rust. By using the `Result` and `Option` enums, as well as the `unwrap`, `expect`, and `?` methods, you can effectively handle errors and ensure the stability of your Rust programs. Keep learning and see you in the next installment!