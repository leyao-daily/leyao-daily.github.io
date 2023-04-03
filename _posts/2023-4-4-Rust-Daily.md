---
layout: post
title: Rust Daily Learning - Day 9 - Working with Collections
categories: Rust
description: Learn how to work with collections in Rust
keywords: Rust, Programming, Daily Learning, Collections, Vec, HashMap, HashSet
---
# Rust Daily Learning - Day 9

- [Overview](#overview)
- [Vectors](#vectors)
- [Hash Maps](#hash-maps)
- [Hash Sets](#hash-sets)

## Overview

Welcome to Day 9 of the Rust daily learning series! Today, we'll focus on working with collections in Rust. Collections are data structures that store multiple values of the same type, allowing you to organize and manipulate your data effectively.

## Vectors

A vector, or `Vec`, is a resizable array that can store elements of the same type. It is a widely used collection in Rust, as it provides a flexible way to store data.

To create a vector, you can use the `vec!` macro:

```rust
let v: Vec<i32> = vec![1, 2, 3, 4, 5];
```

You can also create an empty vector and push elements onto it:

```rust
let mut v = Vec::new();
v.push(1);
v.push(2);
v.push(3);
```

To access elements in a vector, you can use indexing or the `get` method:

```rust
let third: &i32 = &v[2];
let third: Option<&i32> = v.get(2);
```

## Hash Maps

A hash map, or `HashMap`, is a key-value store that allows you to associate values with unique keys. To use a `HashMap`, you'll need to import it from the `std::collections` module.

Here's an example of creating and using a hash map:

```rust
use std::collections::HashMap;

let mut scores = HashMap::new();
scores.insert(String::from("Blue"), 10);
scores.insert(String::from("Yellow"), 50);
```

You can retrieve values from a hash map by using the `get` method:

```rust
let team_name = String::from("Blue");
let score = scores.get(&team_name);
```

## Hash Sets

A hash set, or `HashSet`, is a collection of unique values, where each value can only occur once. Like `HashMap`, you'll need to import `HashSet` from the `std::collections` module.

Here's an example of creating and using a hash set:

```rust
use std::collections::HashSet;

let mut set: HashSet<i32> = HashSet::new();
set.insert(1);
set.insert(2);
set.insert(3);
```

You can check if a value is present in a hash set using the `contains` method:

```rust
if set.contains(&2) {
    println!("Set contains the value 2");
}
```

That's it for today's lesson on working with collections in Rust. By understanding and utilizing vectors, hash maps, and hash sets, you can create more efficient and organized Rust programs. Keep learning, and see you in the next installment!
