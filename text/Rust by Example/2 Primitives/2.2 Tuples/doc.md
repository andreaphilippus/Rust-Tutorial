# Tuples

Syntax:

```rust
    // Tuple is a collection of values of different types
    // and is constructed using parentheses ().
    let my_tuple = (5u32, 1u8, true, -5.04f32);
```

In MATLAB, we can think of tuple as a cell. However, the differences are:

1. Rust tuples do not allow resizing after compiling. While in MATLAB, we can simply add element to cell by `my_tuple{end+1} = something`.
2. Tuple elements are called using `.` index, such as `my_tuple.0` gives `5` while MATLAB uses `{}` to call.

General rules of tuples:

- Tuples are constructed using parenthesis `()`
- Each element has a value with type signature
  - Meaning each element can have different type
- Functions can use tuples to return multiple values of different types
- Tuples, for printing, uses the denominator of `{:?}`

That's why we can see tuples. We use them mostly for function arguments and return outputs when there are multiple just as below:

```rust
fn reverse(pair: (i32, bool)) -> (bool, i32) {
    // `let` can be used to bind the members of a tuple to variables.
    let (int_param, bool_param) = pair;

    (bool_param, int_param)
}
```

Above function groups two inputs as a tuple, naming the input as `pair`. This means the function argument should only be a tuple with length of 2. We use this function for single-input-single-output (SISO) of tuple:

```rust
    let pair = (1, true);
    println!("Pair is {:?}", pair);
    // Pair is (1, true)
    println!("The reversed pair is {:?}", reverse(pair));
    // The reversed pair is (true, 1)
```

We see that `reverse(pair)` gives single output of a tuple: `(true, 1)`.

Tuples can also have nested tuples inside one such as:

```rust
    let tuple_of_tuples = ((1u8, 2u16, 2u32), (4u64, -1i8), -2i16);
```

We can also destruct tuples and assign to different variables:

```rust
    let tuple = (1, "hello", 4.5, true);

    let (a, b, c, d) = tuple;
    println!("{:?}, {:?}, {:?}, {:?}", a, b, c, d);
```
