---
layout: post
title: Rust Daily Learning - Day 16 - Pattern Matching
categories: Rust
description: Learn about pattern matching in Rust
keywords: Rust, Programming, Daily Learning, Pattern Matching, Control Flow
---
# Rust Daily Learning - Day 16

- [Overview](#overview)
- [Pattern Matching](#pattern-matching)

## Overview

Welcome to Day 16 of the Rust daily learning series! Today, we'll learn about pattern matching in Rust, which is a powerful and flexible way to handle different cases in your code.

## Pattern Matching

Pattern matching is a powerful feature in Rust that allows you to destructure and match complex data structures. The `match` expression is used to perform pattern matching, making it easy to handle different cases in a concise and readable way.

Here's an example using pattern matching with an `enum`:

```rust
enum Color {
    Red,
    Green,
    Blue,
}

fn main() {
    let color = Color::Green;

    match color {
        Color::Red => println!("Red"),
        Color::Green => println!("Green"),
        Color::Blue => println!("Blue"),
    }
}
```

In this example, we define an `enum` called `Color` and then create a variable `color` with the value `Color::Green`. We use a `match` expression to print the name of the color. Each arm of the `match` expression is a pattern followed by a `=>` and an expression.

Pattern matching can also be used with more complex data structures, such as `structs` and `tuples`. Here's an example using pattern matching with a `tuple`:

```rust
fn main() {
    let point = (2, 3);

    match point {
        (0, 0) => println!("Origin"),
        (0, y) => println!("On the y-axis at {}", y),
        (x, 0) => println!("On the x-axis at {}", x),
        (x, y) => println!("At point ({}, {})", x, y),
    }
}
```

In this example, we create a `tuple` called `point` and then use a `match` expression to handle different cases. We can match on specific values, such as `(0, 0)`, or bind a variable to a value, such as `(0, y)`.

Pattern matching is an essential tool for writing clean and maintainable Rust code. It allows you to handle complex cases and destructure data structures with ease, leading to more readable and concise code.