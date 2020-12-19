# Notes on "The Book"

These notes are based on [The Rust Programming Language](https://doc.rust-lang.org/book/title-page.html) (2018 edition) by Steve Klabnik and Carol Nichols, with contributions from the Rust Community. Content, code snippets, and other work from the book are attributed to the original authors and the community.

These notes were compiled by [Colton Hurst](https://www.coltonhurst.com). Hopefully they are helpful to people!

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

## Chapter 3

### Variables and Mutability

#### Variables

You can declare a variable with the `let` keyword.

By default variables are immutable. Make them mutable with the `mut` keyword.

Example (notice you *need* the `mut` keyword):

```rust
fn main() {
	let mut x = 5;
	println!("The value of x is: {}", x);
	x = 6;
	println!("The value of x is: {}", x);
}
```

#### Constants

You cannot use the `mut` keyword with constants, because they are always immutable. Declare a constant like this:

```rust
const MAX_POINTS: u32 = 100_000;
```

#### Shadowing

Shadowing is when you declare a new variable with the same name as the previous variable. Here is an example:

```rust
fn main() {
	let x = 5;
	
	let x = x + 1;

	let x = x * 2;
	
	println!("The value of x is: {}", x);
}
```

### Data Types

Two data types to look at in Rust...

#### Scalar Types

A scalar type represents a single value... there are four primary scalar types:

**_Integers_**

Signed integers can be negative or positive. Unsigned integers can only be non-negative (zero and up). Read more [here](https://en.wikipedia.org/wiki/Signedness). Signed numbers are stored using [two's complement](https://en.wikipedia.org/wiki/Two%27s_complement) representation.

Length  | Signed | Unsigned
------- | ------ | --------
8-bit   | `i8`   | `u8`
16-bit  | `i16`  | `u16`
32-bit  | `i32`  | `u32`
64-bit  | `i64`  | `u64`
128-bit | `i128` | `u128`
arch    | `isize`| `usize`

Integer literal chart:

Number literals | Example
--------------- | -------
Decimal         | `98_222`
Hex             | `0xff`
Octal           | `0o77`
Binary          | `0b1111_0000`
Byte (u8 only)  | `b'A'`

All number literals (except the byte literal) allow a type suffix and `_` as a visual separator. (Example: `57u8` or `1_000`)

**_Floating-point Numbers_**

Example:

```rust
fn main() {
	let x = 2.0; // f64

	let y: f32 = 3.0; // f32
}
```

**_Booleans_**

Booleans can only be true or false. An example:

```rust
fn main() {
	let t = true;
	
	let f: bool = false; // with explicit type annotation
}
```

**_Characters_**

The `char` type is the most primitive alphabetic type in Rust. It is four bytes in size and represents a Unicode Scalar Value.

Uses single quotes `''`, not double quotes `""`. Example:

```rust
fn main() {
	let c = 'z';
	let z = 'ℤ';
	let heart_eyed_cat = '😻';
}
```

#### Compound Types

Straight from the book: "Compound types can group multiple values into one type. Rust has two primitive compound types: tuples and arrays." 

**_Tuples_**

Can contain different data types.

Two examples of Tuples, destructuring them, and accessing them via the period (`.`):

```rust
fn main() {
	let tup = (500, 6.4, 1);

	let (x, y, z) = tup;

	println!("The value of y is: {}", y);
}
```

```rust
fn main() {
	let x: (i32, f64, u8) = (500, 6.4, 1);

	let five_hundred = x.0;

	let six_point_four = x.1;

	let one = x.2;
}
```

**_Arrays_**

Arrays in Rust are fixed length and must all be the same type. They are a single chunk of memory allocated on the stack. Example:

```rust
fn main() {
	let a = [1, 2, 3, 4, 5];
}
```
Making an array with the type annotation (5 elements of type `i32`):

```rust
let a: [i32; 5] = [1, 2, 3, 4, 5];
```

Assigning example:

```rust
fn main() {
	let a = [1, 2, 3, 4, 5];

	let first = a[0];
	let second = a[1];
}
```

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