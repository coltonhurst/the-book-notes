# Chapter 3 - Common Programming Concepts

## Variables and Mutability

### Variables

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

### Constants

You cannot use the `mut` keyword with constants, because they are always immutable. Declare a constant like this:

```rust
const MAX_POINTS: u32 = 100_000;
```

### Shadowing

Shadowing is when you declare a new variable with the same name as the previous variable. Here is an example:

```rust
fn main() {
	let x = 5;
	
	let x = x + 1;

	let x = x * 2;
	
	println!("The value of x is: {}", x);
}
```

## Data Types

Two data types to look at in Rust...

### Scalar Types

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

### Compound Types

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

## Comments

In Rust you can comment with `//` or `/* */`.

## Control Flow

### `if` Expressions

In Rust, `if` statements are expressions. The condition must be a `bool` type. Here is an example:

```rust
fn main() {
	let number = 3;
	
	if number < 5 {
		println!("condition was true");
	} else if number > 5 {
		println!("condition was false");
	} else {
		println!("It's a five!");
	}
}
```

Because `if`'s are expressions, you can also use them in a `let` statement like so:

```rust
fn main() {
	let condition = true;
	let number = if condition { 5 } else { 6 };

	println!("The value of number is: {}", number);
}
```

Note that the possible return values from each "arm" of the `if` must be the same type.

### Loops

Rust has 3 types of loops, `loop`, `while`, and `for`.

#### `loop`

Loop until the `break` statement.

Two examples:

```rust
fn main() {
	loop {
		println!("again!");
	}
}
```

```rust
fn main() {
	let mut counter = 0;

	let result = loop {
		counter += 1;

		if counter == 10 {
			break counter * 2;
		}
	};

	println!("The result is {}", result);
}
```

Notice that `loop` can return a value.

#### `while`

Loop as long as the condition is true.

```rust
fn main() {
	let mut number = 3;

	while number != 0 {
		println!("{}!", number);

		number -= 1;
	}

	println!("LIFTOFF!!!");
}
```

#### `for`

You can use `for` to loop through each item in a collection. Example:

```rust
fn main() {
	let a = [10, 20, 30, 40, 50];

	for element in a.iter() {
		println!("the value is: {}", element);
	}
}
```

We can also use the `Range` type te generate numbers in a sequence from one number to ending right before the last number. Example:

```rust
fn main() {
	for number in (1..4).rev() {
		println!("{}!", number);
	}
	println!("LIFTOFF!!!");
}
```

The output of the above code will be:

```
3!
2!
1!
LIFTOFF!!!
```
