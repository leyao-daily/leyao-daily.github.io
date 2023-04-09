---
layout: post
title: Rust Daily Learning - Day 15 - Iterators
categories: Rust
description: Learn about iterators in Rust
keywords: Rust, Programming, Daily Learning, Iterators, Collections, Loops
---
# Rust Daily Learning - Day 15

- [Overview](#overview)
- [Iterators](#iterators)

## Overview

Welcome to Day 15 of the Rust daily learning series! Today, we'll learn about iterators in Rust, which allow you to process a sequence of elements in a collection.

## Iterators

An iterator in Rust is an object that implements the `Iterator` trait. The `Iterator` trait defines a single method, `next`, which returns the next element in the sequence, wrapped in an `Option`. When there are no more elements, the iterator returns `None`.

Here's an example of using an iterator with a `Vec`:

```rust
fn main() {
    let numbers = vec![1, 2, 3, 4, 5];
    let mut iter = numbers.iter();

    println!("{:?}", iter.next()); // Some(1)
    println!("{:?}", iter.next()); // Some(2)
    println!("{:?}", iter.next()); // Some(3)
}
```

In this example, we create a vector `numbers` and obtain an iterator over its elements with the `iter()` method. We then call `next()` on the iterator, which returns `Some(1)` for the first call, `Some(2)` for the second call, and so on.

You can also use iterators with `for` loops, which simplifies the syntax:

```rust
fn main() {
    let numbers = vec![1, 2, 3, 4, 5];

    for number in numbers.iter() {
        println!("{}", number);
    }
}
```

This code will print each element of the `numbers` vector.

Rust provides many useful iterator methods, such as `map`, `filter`, `fold`, and `collect`. Here's an example that demonstrates some of these methods:

```rust
fn main() {
    let numbers = vec![1, 2, 3, 4, 5];
    let even_squared: Vec<_> = numbers.iter()
                                      .filter(|&x| x % 2 == 0)
                                      .map(|x| x * x)
                                      .collect();

    println!("{:?}", even_squared); // [4, 16]
}
```

In this example, we create a new vector `even_squared` by chaining iterator methods. And using Adapter to process the results. Adapters are methods that transform iterators. They are often used to perform operations like filtering, mapping, or reducing elements in a collection. We filter the even numbers, square them, and then collect the results into a new vector.

Understanding iterators and their associated methods is essential for writing concise and efficient code in Rust.