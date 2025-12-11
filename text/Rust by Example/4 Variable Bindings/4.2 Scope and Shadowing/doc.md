# Scope and Shadowing

## Scope

Variable bindings have a scope and constrained to **live in a *block***. Block here means `{}`, just like in `fn main() {}`, or any loop that uses `{}` block.

For example inside `fn main(){}`,

```rust
    let long_lived_binding = 1;
```

This will be accessible throughout `main()` function. However, suppose we create a block within `fn main(){}` like:

```rust
    // This is a block, and has a smaller scope than the main function
    {
        // This binding only exists in this block
        let short_lived_binding = 2;

        println!("inner short: {}", short_lived_binding);
        // inner short: 2
    }
    // End of the block
```

The `short_lived_binding` will not be accessible by any function calls or operations lines before (which is pretty obvious) and after the `}`. Suppose we have a line after that block in `fn main`:

```rust
    println!("outer short: {}", short_lived_binding);
```

This will give compile error because `short_lived_binding` doesn't exist anymore when we try to call `println!`. However, since `long_lived_binding` was defined within `fn main` but not confined by any other blocks, we can safely do

```rust
    println!("outer long: {}", long_lived_binding);
```

## Variable shadowing

[Explanation on variable shadowing](https://en.wikipedia.org/wiki/Variable_shadowing)

In a nutshell: 1) I declare a variable, 2) later I declare another variable with the same name, 3) first variable dies.

But what if we attempt to do variable shadowing *inside a block*?

```rust
fn main() {
    let shadowed_binding = 1;

    {
        println!("before being shadowed: {}", shadowed_binding);
        // before being shadowed: 1

        // This binding *shadows* the outer one
        let shadowed_binding = "abc";

        println!("shadowed in inner block: {}", shadowed_binding);
        // shadowed in inner block: abc
    }
}
```

We saw something similar in chapter 2: *why do we need to use `let mut` and not just shadowing inside loop?*

Here is the answer. After that block, if we call `shadowed_binding`, it will say `1` because `shadowed_binding` inside the block is kind of different variable but just has the same name as the one outside. The data is stored elsewhere. Therefore, although `shadowed_binding` could be called inside the block, even after we overwrite with `let`, it doesn't affect the original `shadow_binding`. We can think the block as "copy of the variables we have so far, storing them temporarily".

If we want to modify inside the block (just like the loops), we need to use `let mut` and modify it inside the block. That way we have access to the original variable and interfere with the outer world:

```rust
fn main() {
    let mut mutable_number = 1;

    {
        println!("{}", mutable_number);
        // 1

        mutable_number += 1;

        println!("{}", mutable_number);
        // 2
    }
    println!("outside inner block: {}", mutable_number);
    // outside inner block: 2
}
```
