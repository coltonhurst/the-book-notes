# Chapter 4 - Understanding Ownership

## What is Ownership?

In Rust, "memory is managed through a system of ownership with a set of rules that the compiler checks at compile time". This is different from other languages that manage their own memory or have the programmer explicitly allocate and free the memory.

### The Three Rules of Ownership

1. Each value in Rust has a variable that’s called its owner.
2. There can only be one owner at a time.
3. When the owner goes out of scope, the value will be dropped.

### The String Type

String literals (when a string is hardcoded into the program) are immutable and are *not* on the heap. The `String` type *is* allocated on the heap and is mutable. Here we create the variable `s` that is the `String` type.

```rust
let s = String::from("hello");
```

We can mutate the `String` variable:

```rust
let mut s = String::from("hello");
	
s.push_str(", world!"); // push_str() appends a literal to a String
	
println!("{}", s); // This will print `hello, world!`
```

We can do this with the `String` variable but not with string literals because of the different ways these two types deal with memory (read about it [here](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html#memory-and-allocation)).

### Memory & Allocation

#### Drop

When a variable goes out of scope, Rust calls the `drop` function so the memory on the heap is returned to the OS.

#### Move

*Move* is when the ownership of data on the heap is *moved* from one variable to another. The actual data on the heap is not changed, moved, or copied. An example below:

```rust
let s1 = String::from("hello");
let s2 = s1;

println!("{}, world!", s1); // this line will not work
```

Above, we *move* the ownership of the data from `s1` to `s2`.

When we assign `s1` to `s2`, the `String` data is copied, meaning we copy the pointer, the length, and the capacity that are on the stack. We do not copy the data on the heap that the pointer refers to.

`s1` owns the data it's pointing to (holding the string `"hello"`) after the first line. After the second line, `s2` is now the owner of that data, and `s1` is no longer valid, so `s1` cannot be referenced again (hence the error on the last line).

"In addition, there’s a design choice that’s implied by this: Rust will never automatically create “deep” copies of your data. Therefore, any automatic copying can be assumed to be inexpensive in terms of runtime performance."

#### Clone

*Clone* is when the actual data on the heap is *copied* over.

```rust
let s1 = String::from("hello");
let s2 = s1.clone();

println!("s1 = {}, s2 = {}", s1, s2);
```

The above code is valid because the data `s1` was referencing was copied in the heap; `s2` points to a completely different location in memory than `s1`.


#### Copy

*Copy* is when the data is on the stack only, and it's copied on the stack. There is a special `copy` trait that certain types have that allow this functionality.

```rust
let x = 5;
let y = x;

println!("x = {}, y = {}", x, y);
```

Some types that have the `copy` trait:

- All the integer types, such as u32.
- The Boolean type, bool, with values true and false.
- All the floating point types, such as f64.
- The character type, char.
- Tuples, if they only contain types that are also Copy. For example, (i32, i32) is Copy, but (i32, String) is not.

If a type has the `copy` trait, an older variable is still usable after assignment, as the data hasn't been moved (and we're talking about the stack, not the heap).

### Ownership and Functions

Passing a value to a function is similar to assigning a value to a variable. Passing a value to a function will `move` or `copy` like an assignment does. Example:

```rust
fn main() {
	let s = String::from("hello");	// s comes into scope

	takes_ownership(s);					// s's value moves into the function...
											// ... and so is no longer valid here

	let x = 5;							// x comes into scope

	makes_copy(x);						// x would move into the function,
											// but i32 is Copy, so it’s okay to still
											// use x afterward

} // Here, x goes out of scope, then s. But because s's value was moved, nothing
  // special happens.

fn takes_ownership(some_string: String) { // some_string comes into scope
	println!("{}", some_string);
} // Here, some_string goes out of scope and `drop` is called. The backing
  // memory is freed.

fn makes_copy(some_integer: i32) { // some_integer comes into scope
	println!("{}", some_integer);
} // Here, some_integer goes out of scope. Nothing special happens.
```

### Return Values and Scope

Returning values can also transfer ownership.

```rust
fn main() {
	let s1 = gives_ownership();         // gives_ownership moves its return
                                        // value into s1

	let s2 = String::from("hello");     // s2 comes into scope

	let s3 = takes_and_gives_back(s2);  // s2 is moved into
                                        // takes_and_gives_back, which also
                                        // moves its return value into s3
} // Here, s3 goes out of scope and is dropped. s2 goes out of scope but was
  // moved, so nothing happens. s1 goes out of scope and is dropped.

fn gives_ownership() -> String {             // gives_ownership will move its
                                             // return value into the function
                                             // that calls it

	let some_string = String::from("hello"); // some_string comes into scope

	some_string                              // some_string is returned and
                                             // moves out to the calling
                                             // function
}

// takes_and_gives_back will take a String and return one
fn takes_and_gives_back(a_string: String) -> String { // a_string comes into
                                                      // scope

	a_string  // a_string is returned and moves out to the calling function
}
```

We can return more than one value with `tuples`.

```rust
fn main() {
	let s1 = String::from("hello");

	let (s2, len) = calculate_length(s1);

	println!("The length of '{}' is {}.", s2, len);
}

fn calculate_length(s: String) -> (String, usize) {
	let length = s.len(); // len() returns the length of a String

	(s, length)
}
```

What if we want to let a function use data on the heap without having to give the function ownership and then get ownership back?

You can use references!

## References and Borrowing