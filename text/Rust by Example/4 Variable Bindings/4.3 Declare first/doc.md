# Declare first

Remember we can modify a defined variable only with `let mut` declaration? What we mean by **"define"** is *assigning a value to a declared variable*.

We can assign a value after declaring a variable first. `let` does not allow modification of ***defined*** variable, but if we haven't *defined* by just declaring, we have **one chance** to do so after declaring. In `fn main`:

```rust
    let a_binding;

    {
        let x = 2;

        // Initialize the binding
        a_binding = x * x;
    }

    println!("a binding: {}", a_binding);
    // a binding: 4
```

We see that first we don't assign any value to `a_binding` but can *define* it (we call initialize), even inside the block (because it's not shadowed by `let a_binding` inside the block!). Once initialized, as we all know what `let` does, we cannot modify it like `a_binding = 6;` after that block, unless shadowing with `let a_binding = 6;` outside the block.

When we **only** declare a variable, we need to initialize it, assign value, to use it. Suppose we have:

```rust
fn main() {
    let another_binding;

    println!("another binding: {}", another_binding);
}
```

Above code will give error because `println!` has no idea what `another_binding` has for its value. However,

```rust
fn main() {
    let another_binding;

    another_binding = 1;

    println!("another binding: {}", another_binding);
}
```

Works perfectly fine.

We can also declare a variable with data type only without giving it value, like below:

```rust
fn main() {
    let number: u8;
}
```

However, in this case, if we were to assign a value that does not match the type when declared, like saying `number = -3;`, it will throw an error.
