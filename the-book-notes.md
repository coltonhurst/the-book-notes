# Notes on "The Book"

These notes are based on [The Rust Programming Language](https://doc.rust-lang.org/book/title-page.html) (2018 edition) by Steve Klabnik and Carol Nichols, with contributions from the Rust Community. Content, code snippets, and other work from the book are attributed to the original authors and the community.

These notes were compiled by [Colton Hurst](https://www.coltonhurst.com).

## Chapter 1

### Installation

Install Rust on Linux or Mac OS X using `rustup`:

```
curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
```

For installation on Windows, follow the instructions [here](https://www.rust-lang.org/tools/install).

If you get linker errors when trying to compile a Rust program, then you need to install a linker on your system. Downloading a C compiler for your system should do the trick.

### Hello World

Compile with `rustc main.rs`, and run with `./main`. On Windows run with `.\main.exe`.

```rust
fn main() {
    println!("Hello, world!");
}
```

- The code is `main` is always the first code to be run in an executable Rust program.
- `println!` is a Rust macro. The `!` indicates it is a macro and not a function. You can read more about macros [here](https://doc.rust-lang.org/book/ch19-06-macros.html) (chapter 19 section 5).

### Hello Cargo

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

## Chapter 2

coming soon

## Appendix

### Cargo Commands

- `cargo new project_name` to create a new project
- `cargo --version` to check cargo's version
- `cargo new --vcs=git` you can change the default version control cargo sets up
- `cargo new --help` see the help page for `cargo new`
- `cargo build` to build a cargo project
- `cargo build --release` to build a cargo project release exectuable
- `cargo run` to build and run a cargo project
- `cargo check` checks to make sure your code will compile but does not create an executable

### Rustup Commands

- `rustup update` to update Rust
- `rustup self uninstall` uninstalls Rust and and rustup
- `rustup doc` opens local documentation in your browser

### Other Commands

- `rustfmt` to format Rust code.