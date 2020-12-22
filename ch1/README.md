# Chapter 1 - Getting Started

## Installation

Install Rust on Linux or Mac OS X using `rustup`:

```
curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
```

For installation on Windows, follow the instructions [here](https://www.rust-lang.org/tools/install).

If you get linker errors when trying to compile a Rust program, then you need to install a linker on your system. Downloading a C compiler for your system should do the trick.

## Hello World

Compile with `rustc main.rs`, and run with `./main`. On Windows run with `.\main.exe`.

```rust
fn main() {
	println!("Hello, world!");
}
```

- The code is `main` is always the first code to be run in an executable Rust program.
- `println!` is a Rust macro. The `!` indicates it is a macro and not a function. You can read more about macros [here](https://doc.rust-lang.org/book/ch19-06-macros.html) (chapter 19 section 5).

## Hello Cargo

Make a new project with cargo using `cargo new hello_cargo`.

The `Cargo.toml` file is essentially the cargo configuration file. The file is in the [TOML](https://toml.io/en/) format.

Here is a sample `Cargo.toml` file:

```toml
[package]
name = "hello_cargo"
version = "0.1.0"
authors = ["Your Name <you@example.com>"]
edition = "2018"

[dependencies]
```
