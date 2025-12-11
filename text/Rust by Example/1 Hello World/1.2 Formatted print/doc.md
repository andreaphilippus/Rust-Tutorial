# Formatted print

Printing types:

- `format!` &rarr; write formatted text to `String` (to build `String`)
- `print!` &rarr; same as `format!` but the text is printed to the console
- `println!` &rarr; same as `print!` but a newline is appended
- `eprint!` &rarr; same as `print!` but is output as error
- `eprintln!` &rarr; same as `eprint!` but a newline is appended

Compare to MATLAB:

| Rust    | MATLAB |
| -------- | ------- |
| `format!`  | `sprintf`    |
| `print!` | `fprintf` or `disp`     |
| `println!`    | `fprintf("...\n")`    |
| `eprint!` | `error()` |
| `eprintln!` | `error("...\n")` |

## Adding variable to print

We use `{}` to replace with variable like:

```rust
    println!("{} days", 31);
    // 31 days
```

Number `31` will be stringified automatically.

If there are multiple arguments and are used multiple times, we can use indexed arguments using `{1}`, `{2}`, ... such as:

```rust
    println!("{0}, this is {1}. {1}, this is {0}", "Alice", "Bob");
    // Alice, this is Bob. Bob, this is Alice 
```

We can also do named arguments such as:

```rust
    println!("{subject} {verb} {object}",
             object="the lazy dog",
             subject="the quick brown fox",
             verb="jumps over");
    // the lazy dog jumps over the quick brown fox
```

For a number, we can change the bases when printing out:

```rust
    // Different formatting can be invoked by specifying the format character
    // after a `:`.
    println!("Base 10:               {}",   69420); // 69420
    println!("Base 2 (binary):       {:b}", 69420); // 10000111100101100
    println!("Base 8 (octal):        {:o}", 69420); // 207454
    println!("Base 16 (hexadecimal): {:x}", 69420); // 10f2c
```
