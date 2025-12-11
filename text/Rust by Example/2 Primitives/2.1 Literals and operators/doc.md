# Literals and operators

## Literals

*From [wikipedia](https://en.wikipedia.org/wiki/Literal_(computer_programming)):*

> In computer science, a literal is a textual representation (notation) of a value as it is written in source code.

### Integers in different notions

We can store numerical integers in different formats:

- `0x` &rarr; hexadecimal
- `0o` &rarr; octal
- `0b` &rarr; binary
  
We don't use these a lot, however, maybe useful for describing sets of states that have binary values such as:

- Swarm of multiple devices having `on` and `off` switch.

For example, we can have an array to describe the power state of 8 devices using 0 (for state `off`) and 1 (for state `on`) like

```rust
    let on_off_state: [u8; 8] = [0, 1, 1, 0, 0, 0, 1, 1];
```

But we can reduce the data size consumed for this information using `0b` such as:

```rust
    let on_off_state = 0b01100011u8;
```

The default integer type is `i32` for these integer values, but if they do not fit, such as `let a = 0xFFFF_FFFF_FFFF_FFFF;` when converted to binary it has more than 32 digits, `rustc` will try to infer another integer type like `i64` or higher, but generally recommended to assign the appropriate data type when defining with high value.

### Underscores

We can use underscores to improve the readability within the code to help the programmers, while it does not have any effects. We generally can use underscores every 3 digits such as:

```rust
    println!("One million is written as {}", 1_000_000u32);
    // One million is written as 1000000
```

```rust
    println!("Nano is {}", 0.000_000_001f32);
    // Nano is 0.000000001
```

See how easy it is to read with the placer.

### E-notation

We love E-notation, and it works just like MATLAB. `1e6`, `7.4e-7`, etc. The associated type is `f64` by default.

```rust
    println!("1e4 is {}, -2.5e-3 is {}", 1e4, -2.5e-3);
    //1e4 is 10000, -2.5e-3 is -0.0025
```

## Operators

You can find the [list of operators here](https://doc.rust-lang.org/reference/expressions.html#expression-precedence), they are C-like, including MATLAB.
