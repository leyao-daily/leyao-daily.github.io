---
layout: post
title: Rust Daily Learning - Day 18 - Cargo Basics
categories: Rust
description: Learn about Cargo, the Rust package manager
keywords: Rust, Programming, Daily Learning, Cargo, Package Manager, Dependencies, Build System
---
# Rust Daily Learning - Day 18

- [Creating a New Project](#createing-a-new-project)
- [Building and Running a Project](#building-and-running-a-project)
- [Dependencies](#dependencies)
- [Testing and Documentation](#testing-and-documentation)

Today, we'll explore Cargo, Rust's package manager and build system. Cargo streamlines the process of managing dependencies, building, testing, and publishing Rust projects.

## Creating a New Project

To create a new Rust project using Cargo, run the following command:

```rust
$ cargo new my_project
```

This command will generate a new directory named `my_project` with the following structure:

```css
my_project
├── Cargo.toml
└── src
    └── main.rs
```

`Cargo.toml` is the project's configuration file, and `src/main.rs` is the main source file.

## Building and Running a Project

To build your Rust project, use the `cargo build` command. This command compiles the project and creates an executable binary in the `target/debug` directory:

```bash
$ cargo build
```

To run the project, use the `cargo run` command. This command builds the project if necessary and then runs the generated executable:

```bash
$ cargo run
```

## Dependencies

Cargo makes it easy to manage your project's dependencies. To add a dependency, open the `Cargo.toml` file and add the package under the `[dependencies]` section:

```toml
[dependencies]
serde = "1.0"
```

When you build or run your project, Cargo automatically downloads the specified dependencies, along with their transitive dependencies, and compiles them.

To use the dependency in your Rust code, add an `extern crate` declaration and use the package's features:

```rust
extern crate serde;

// Use serde features
```

## Testing and Documentation

As we've seen in previous sessions, Cargo also handles testing and documentation. Run tests with the `cargo test` command and generate documentation using the `cargo doc` command.

Keep practicing Cargo commands and project management to streamline your Rust development experience!