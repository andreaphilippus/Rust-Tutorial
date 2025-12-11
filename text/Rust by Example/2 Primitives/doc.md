# Primitives

## Scalar Types

- Signed integers: `i8`, `i16`, `i32`, `i64`, `i128`, and `isize` (pointer size)
- Unsigned integers: `u8`, `u16`, `u32`, `u64`, `u128`, and `usize` (pointer size)
  - Unsigned integers only take positive values, `-3u32` is not a thing.
- Floating point: `f32`, `f64`
- Unicode scalar values: `char` (4 bytes each)
- Boolean: `bool` (gives either `true` or `false`)
- Unit type: `()`, only possible value is an empty tuple `()`

## Compound Types

- Arrays like `[1, 2, 3]`
- Tuples like `(1, true)`

We can see that arrays need to have elements of same types whereas tuples can have elements of different types.

When assigning a value, we can specify the data type such as:

```rust
    let logical: bool = true;

    let a_float: f64 = 1.0;  // Regular annotation
    let an_integer   = 5i32; // Suffix annotation
```

So the syntax is `let #name# : #data_type# = #value#`, or for numerical values, we can do `let #name# = #value##data_type#`.

If we don't specify the type, Rust assigns the following default data types:

- Integer: `i32`
- Float: `f64`
- Boolean: `bool` (quite obvious, no?)

## Variable overwrite

Basically, variable defined with `let` is by default not mutable. That means, we cannot overwrite another value after initializing it. For example, if we define a variable by `let number = 5;`, we cannot try to call it and assign new value like:

`number = 21;`

This will give error. We have to overwrite by defining a variable with same name (loses continuity) by

`let number = 21;`

Which is called *shadowing*. When we want to have a variable that evolves throughout the code, we don't want to do shadowing, for example,

```rust
let sum = 0;
let values = [1, 2, 3];
for v in values {
    let sum = sum + v;   // new sum *inside loop body* shadowing old one
}
println!("{sum}");
```

In Rust, variable inside loops bound by `{}` is a different binding from the variable with same name outside the loop. Above code will print `0`, because `sum` in line 1 does not get updated by the for loop because `sum` inside the loop created by `let` is just different thing.

To mitigate this, we can define a variable to be mutable, by using `let mut`. `let mut` is helpful because it allows change of the variable **but prevents overwriting by different type**. For example,

```rust
    let mut mutable = 12; // Mutable `i32`
    mutable = true;
```

will give error because `mutable` defined to be `i32` is attempted to be overwritten by `bool` type. Now, if we have:

```rust
let sum = 0;
let values = [1, 2, 3];
for v in values {
    sum += v;   // new sum *inside loop body* shadowing old one
}
println!("{sum}");
```

we will finally see the console printing `6`.
