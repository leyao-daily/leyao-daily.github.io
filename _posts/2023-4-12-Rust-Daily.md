---
layout: post
title: Rust Daily Learning - Day 17 - Testing and Documentation
categories: Rust
description: Learn about testing and documentation in Rust
keywords: Rust, Programming, Daily Learning, Testing, Documentation, Unit Testing, Integration Testing
---
# Rust Daily Learning - Day 17

- [Testing](#testing)
- [Documentation](#documentation)

In this session, we'll learn about testing and documentation in Rust. Rust has built-in support for both testing and documentation, making it easy to create quality code.

## Testing

Rust's testing framework is integrated into the language and the `cargo` tool. There are two types of tests in Rust: unit tests and integration tests.

### Unit Tests

Unit tests are small, focused tests that check the functionality of a single module, function, or method. They are usually located in the same file as the code they test, inside a `#[cfg(test)]` module.

```rust
fn add(a: i32, b: i32) -> i32 {
    a + b
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_add() {
        assert_eq!(add(1, 2), 3);
    }
}
```

### Integration Tests

Integration tests are located in the `tests` directory at the top level of your project. They test the interaction between multiple components of your application.

To create an integration test, create a new file in the `tests` directory:

```bash
$ touch tests/integration_test.rs
```

Then write the test:

```rust
use my_crate::add;

#[test]
fn test_add() {
    assert_eq!(add(1, 2), 3);
}
```

Run the tests using `cargo test`.

## Documentation

Rust has built-in support for generating documentation using the `rustdoc` tool. You can write documentation comments with triple slashes `///` and use Markdown for formatting.

```rust
/// Adds two numbers together.
///
/// # Examples
///
/// ```
/// use my_crate::add;
///
/// assert_eq!(add(1, 2), 3);
/// ```
pub fn add(a: i32, b: i32) -> i32 {
    a + b
}
```

Generate the documentation using `cargo doc`. It will create HTML documentation in the `target/doc` directory. Open the generated `index.html` file in your browser to view the documentation.

Keep practicing testing and documentation to ensure your Rust code is of high quality and well-documented!