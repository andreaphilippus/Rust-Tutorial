# constants

Rust has two different types of constants:

1. `const` &rarr; an **unchangeable** value (most common)
2. `static` &rarr; a *possibly mutable* variable with `static` lifetime
   - Static lifetime is *inferred* and does not have to be *specified*
   - It is stored somewhere in the memory for the **whole duration of program run** and it is **global** variable
   - Making it mutable is unsafe, any jobs that modifies `static` constant needs to be wrapped by `unsafe{}`

Example:

```rust
static LANGUAGE: &str = "Rust";
const THRESHOLD: i32 = 10;
```

We cannot modify `const`, so in `fn main` if we try to do below:

```rust
    THRESHOLD = 5;
```

It will give an error.

However, we can access these constants anywhere, as long as the constants are declared at the top. Just like the function below:

```rust
fn is_big(n: i32) -> bool {
    // Access constant in some function
    n > THRESHOLD
}
```

The function does not define `THRESHOLD` inside nor take `THRESHOLD` as an input parameter but it works as `THRESHOLD` is a global constant.

Example usage in `fn main`:

```rust
    let n = 16;

    // Access constant in the main thread
    println!("This is {}", LANGUAGE);
    // This is Rust
    println!("The threshold is {}", THRESHOLD);
    // The threshold is 10
    println!("{} is {}", n, if is_big(n) { "big" } else { "small" });
    // 16 is big
```
