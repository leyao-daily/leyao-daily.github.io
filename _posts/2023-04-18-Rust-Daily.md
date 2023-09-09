---
layout: post
title: Rust Daily Learning - Day 23 - Foreign Function Interface (FFI)
categories: Rust
description: Learn how to create and use bindings between Rust and other languages using the Foreign Function Interface (FFI)
keywords: Rust, Programming, Daily Learning, FFI, Foreign Function Interface, C, C++, Bindings
---
# Rust Daily Learning - Day 23

- [Overview](#overview)
- [Creating a C Library](#creating-a-c-library)
- [Defining Rust FFI Bindings](#defining-rust-ffi-bindings)
- [Calling C Functions from Rust](#calling-c-functions-from-rust)
- [Exposing Rust Functions to C](#exposing-rust-functions-to-c)

## Overview

In today's Rust daily learning series, we'll introduce you to the Foreign Function Interface (FFI) in Rust. FFI allows you to create and use bindings between Rust and other programming languages, such as C and C++. This can be valuable for leveraging existing libraries or integrating Rust into existing projects.

## Creating a C Library

First, let's create a simple C library. Create a new directory called `c_lib` and add a file named `c_functions.h` with the following content:

```c
#ifndef C_FUNCTIONS_H
#define C_FUNCTIONS_H

int add(int a, int b);

#endif
```

Next, create a file named `c_functions.c` with the following content:

```c
#include "c_functions.h"

int add(int a, int b) {
    return a + b;
}
```

Compile the C library using the following command:

```bash
gcc -c c_functions.c -o c_functions.o
ar rcs libc_functions.a c_functions.o
```

This creates a static library named `libc_functions.a`.

## Defining Rust FFI Bindings

Now, create a new Rust project:

```bash
cargo new rust_ffi_example
```

Change into the `rust_ffi_example` directory:

```bash
cd rust_ffi_example
```

Add the `libc` crate to your `Cargo.toml` file:

```toml
[dependencies]
libc = "0.2"
```

Create a new directory named `c_lib` inside the Rust project and copy the `c_functions.h` and `libc_functions.a` files into it.

Edit the `src/main.rs` file to define Rust FFI bindings:

```rust
extern crate libc;
use libc::c_int;

#[link(name = "c_functions", kind = "static")]
extern "C" {
    fn add(a: c_int, b: c_int) -> c_int;
}
```

## Calling C Functions from Rust

Now, you can call the C `add` function from Rust:

```rust
fn main() {
    let a = 5;
    let b = 7;
    let result = unsafe { add(a, b) };
    println!("The sum of {} and {} is: {}", a, b, result);
}
```

Build and run your project:

```bash
cargo run
```

## Exposing Rust Functions to C

You can also expose Rust functions to C. Edit the `src/lib.rs` file and add the following content:

```rust
#[no_mangle]
pub extern "C" fn multiply(a: i32, b: i32) -> i32 {
    a * b
}
```

Update the `Cargo.toml` file to build a dynamic library:

```toml
[lib]
name = "rust_ffi_example"
crate-type = ["cdylib"]
```

Build the Rust library:

```bash
cargo build --release
```

Create a C file named `main.c` inside the `c_lib` directory with the following content:

```c
#include <stdio.h>
#include "c_functions.h"

extern int multiply(int a, int b);

int main() {
    int a = 5;
    int b = 7;
    int sum = add(a, b);
    int product = multiply(a, b);

    printf("The sum of %d and %d is: %d\n", a, b, sum);
    printf("The product of %d and %d is: %d\n", a, b, product);

    return 0;
}
```

Compile and link the C program with the Rust library:

```bash
gcc main.c -I. -L../rust_ffi_example/target/release -lrust_ffi_example -o main
```

Run the C program:

```bash
./main
```

You should see the output from both the C `add` function and the Rust `multiply` function.

That's it for today's lesson on Rust and the Foreign Function Interface (FFI). Keep experimenting with FFI and explore how you can use it to leverage existing libraries and integrate Rust code into your projects. Happy coding!