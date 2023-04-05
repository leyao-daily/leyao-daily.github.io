---
layout: post
title: Rust Daily Learning - Day 11 - Macros in Rust
categories: Rust
description: Learn about macros in Rust
keywords: Rust, Programming, Daily Learning, Macros, macro_rules, Procedural Macros
---
# Rust Daily Learning - Day 12

- [Overview](#overview)
- [Declarative Macros](#declarative-macros)
- [Procedural Macros](#procedural-macros)

## Overview

Welcome to Day 12 of the Rust daily learning series! Today, we'll explore macros in Rust, a powerful feature that enables code generation and metaprogramming. We'll look at the two types of macros in Rust: declarative macros and procedural macros.

## Declarative Macros

Declarative macros, also known as "macro_rules!" macros, allow you to define reusable code patterns in a concise way. They use pattern matching to generate code based on the input.

Here's a simple example of a declarative macro that calculates the maximum of two expressions:

```rust
macro_rules! max {
    ($a:expr, $b:expr) => {
        if $a > $b {
            $a
        } else {
            $b
        }
    };
}

fn main() {
    let result = max!(3 + 2, 4 * 2);
    println!("The maximum is: {}", result);
}
```

In this example, the `max!` macro takes two expressions as input and generates an if-else expression to compute their maximum.

## Procedural Macros

Procedural macros are more advanced and powerful than declarative macros. They are functions that accept a `TokenStream` as input and produce a `TokenStream` as output. Procedural macros can be used for custom #[derive] attributes, function-like macros, and attribute-like macros.

Here's an example of a custom `#[derive]` attribute that derives a `HelloWorld` trait for a struct:

```rust
extern crate proc_macro;

use proc_macro::TokenStream;
use quote::quote;
use syn::{parse_macro_input, DeriveInput};

#[proc_macro_derive(HelloWorld)]
pub fn hello_world(input: TokenStream) -> TokenStream {
    let input = parse_macro_input!(input as DeriveInput);
    let ident = input.ident;

    let expanded = quote! {
        impl HelloWorld for #ident {
            fn hello_world() {
                println!("Hello, World! My name is {}!", stringify!(#ident));
            }
        }
    };

    TokenStream::from(expanded)
}

// main.rs
#[macro_use]
extern crate hello_world_derive;

trait HelloWorld {
    fn hello_world();
}

#[derive(HelloWorld)]
struct MyStruct;

fn main() {
    MyStruct::hello_world();
}
```

In this example, we use the `syn` and `quote` crates to parse and generate Rust code. The `hello_world` procedural macro derives a `HelloWorld` trait for the given struct, allowing it to print a greeting message.