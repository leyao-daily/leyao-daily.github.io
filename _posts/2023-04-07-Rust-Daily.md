---
layout: post
title: Rust Daily Learning - Day 12 - Traits and Generics
categories: Rust
description: Learn about traits and generics in Rust
keywords: Rust, Programming, Daily Learning, Traits, Generics, Associated Functions, Bounds
---
# Rust Daily Learning - Day 12

- [Overview](#overview)
- [Traits](#traits)
- [Generics](#generics)

## Overview

Welcome to Day 12 of the Rust daily learning series! Today, we'll explore traits and generics in Rust, which enable code reuse and abstraction.

## Traits

Traits define shared behavior across types. They are similar to interfaces in other languages. You can define a trait and implement it for various types, enabling a form of polymorphism.

Here's an example of defining and implementing a trait:

```rust
trait Drawable {
    fn draw(&self);
}

struct Circle {
    radius: f32,
}

struct Rectangle {
    width: f32,
    height: f32,
}

impl Drawable for Circle {
    fn draw(&self) {
        println!("Drawing a circle with radius {}", self.radius);
    }
}

impl Drawable for Rectangle {
    fn draw(&self) {
        println!("Drawing a rectangle with width {} and height {}", self.width, self.height);
    }
}
```

In this example, we define a `Drawable` trait with a `draw` method. We then implement the trait for `Circle` and `Rectangle` structs.

## Generics

Generics enable you to write abstract and reusable code without sacrificing performance. They let you write a single function or data structure that can work with different types.

Here's an example of using generics:

```rust
fn largest<T: PartialOrd>(list: &[T]) -> &T {
    let mut largest = &list[0];

    for item in list {
        if item > largest {
            largest = item;
        }
    }

    largest
}

fn main() {
    let numbers = vec![34, 50, 25, 100, 65];
    let largest_number = largest(&numbers);
    println!("The largest number is {}", largest_number);

    let chars = vec!['y', 'm', 'a', 'q'];
    let largest_char = largest(&chars);
    println!("The largest char is {}", largest_char);
}
```

In this example, we define a generic function `largest` with a type parameter `T`. The `T: PartialOrd` syntax specifies a trait bound, requiring the type `T` to implement the `PartialOrd` trait. The `largest` function can now be used with different types, such as integers and characters.

With traits and generics, you can write more abstract, flexible, and reusable code in Rust.