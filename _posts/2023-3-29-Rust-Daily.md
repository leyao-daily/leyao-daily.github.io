---
layout: post
title: Rust Daily Learning - Day 3 - Control Flow
categories: Rust
description: Dive into control flow with conditionals and loops in Rust
keywords: Rust, Programming, Daily Learning, Control Flow, Conditionals, Loops
---
# Rust Daily Learning - Day 3

- [Overview](#overview)
- [Conditionals](#conditionals)
- [Loops](#loops)

## Overview

Welcome to Day 3 of the Rust daily learning series! Today, we will explore control flow in Rust, including conditionals and loops. Mastering these concepts is crucial for creating efficient and flexible Rust programs.

## Conditionals

In Rust, the `if` statement is used for conditional execution of code. Unlike some languages, Rust doesn't use parentheses around the condition, but it does require braces for the code block. Here's an example:

```rust
fn main() {
    let number = 5;

    if number < 0 {
        println!("The number is negative.");
    } else if number == 0 {
        println!("The number is zero.");
    } else {
        println!("The number is positive.");
    }
}
```

### Using `if` in a `let` Statement

In Rust, you can also use the result of an `if` expression in a `let` statement. Here's an example:

```rust
fn main() {
    let condition = true;
    let number = if condition { 5 } else { 6 };

    println!("The value of number is: {}", number);
}
```

## Loops

Rust provides several looping constructs, allowing you to run a block of code multiple times.

### `loop`

The `loop` keyword creates an infinite loop. To exit the loop, use the `break` keyword:

```rust
fn main() {
    let mut counter = 0;

    loop {
        counter += 1;
        println!("Iteration: {}", counter);

        if counter == 5 {
            break;
        }
    }
}
```

### `while`

The `while` loop repeats a block of code as long as a condition remains true:

```rust
fn main() {
    let mut number = 3;

    while number != 0 {
        println!("{}!", number);
        number -= 1;
    }

    println!("Liftoff!");
}
```

### `for`

The `for` loop iterates over a collection, such as an array or a range, executing a block of code for each item:

```rust
fn main() {
    let arr = [10, 20, 30, 40, 50];

    for element in arr.iter() {
        println!("The value is: {}", element);
    }
}
```

That's all for today's lesson on control flow in Rust. In the next installment, we'll cover functions and their uses in Rust programs. Keep learning and see you soon!