---
layout: post
title: Rust Daily Learning - Day 1
categories: Rust
description: A brief introduction to Rust and getting started with the "Hello, World!" program
keywords: Rust, Program, Daily, Notes
---
# Rust Daily Learning - Day 1

- [Overview](#overview)
- [Installation](#installation)
- [Hello World](#hello-world)

## Overview

Welcome to the Rust daily learning series! In this series, we will explore the Rust programming language in a systematic manner. Today, we will focus on installing Rust and compiling a basic program, namely the "Hello, World!" program.

## Installation

1. Navigate to the [Rust official website](https://www.rust-lang.org/tools/install).
2. Follow the installation instructions for your specific operating system.
3. Once the installation is complete, restart your terminal and run the following command: `rustc --version`.
4. If the installation was successful, you will see the Rust compiler version. If not, check your environment variables and try again.

## Hello World

1. Create a new file named `hello_world.rs`.
2. Insert the following code into the file:

```rust
fn main() {
    println!("Hello, world!");
}
```

1. Save the file and navigate to the file's directory using the terminal.
2. Run the following command to compile the program: `rustc hello_world.rs`.
3. Execute the generated binary file (e.g., `./hello_world` on Unix-based systems).
4. If the output displays "Hello, world!", your program has successfully compiled and executed.

Stay tuned for the next installment in this series, where we will delve into Rust's basic syntax and explore its unique features. Continue learning and discover the power of Rust!
