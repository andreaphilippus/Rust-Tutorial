# C-like

`enum` can be used as C-like enums. What is C-like enum?

- All variants are **fieldless** (no data attached)
- each variant has an associated **integer discriminator** (explicit or implicit)
  - Explicit: we designate our own number
  - Implicit: automatically starts from 0
- whole enum behaves like a bunch of **named integer constants**

Example:

```rust
// enum with implicit discriminator (starts at 0)
enum Number {
    Zero,
    One,
    Two,
}

// enum with explicit discriminator
enum Color {
    Red = 0xff0000,
    Green = 0x00ff00,
    Blue = 0x0000ff,
}
```

We see they don't carry any value (*unit variants* only for `enum Number`) and integers assigned to `enum Color`. However, we can call them as **integers** by `#enum#::#variant# as #integer_type#` such as `i32` and `u32`:

```rust
    // `enums` can be cast as integers.
    println!("zero is {}", Number::Zero as i32);
    // zero is 0
    println!("one is {}", Number::One as i32);
    // one is 1

    println!("roses are #{:06x}", Color::Red as u32);
    // roses are #ff0000
    println!("violets are #{:06x}", Color::Blue as u32);
    // violets are #0000ff
```

This is useful when we have **named integer constants**, could mostly be found for **codes** such as exit code:

```rust
enum ExitCode {
    Success = 0,
    UsageError = 64,
    IOError = 74,
}

std::process::exit(ExitCode::UsageError as i32);
```
