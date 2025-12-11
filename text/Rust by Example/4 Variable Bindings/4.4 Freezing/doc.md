# Freezing

What block can do also is *freezing*. We can do so by **shadowing a mutable variable by immutable declaration** like:

```rust
fn main() {
    let mut _mutable_integer = 7i32;

    {
        // Shadowing by immutable `_mutable_integer`
        let _mutable_integer = _mutable_integer;

        // Error! `_mutable_integer` is frozen in this scope
        _mutable_integer = 50;
    }
}
```

Within the block, `_mutable_integer` is shadowed by immutable declaration, such that it is frozen within the block. It is useful when we want to have a variable that needs to be modified throughout the program, but for certain blocks we need those information but they need to stay during that scope. Therefore we cannot modify `_mutable_integer` inside the block after that `let` froze.

Outside the block, we can modify it because the immutable `let _mutable_integer` dies once we come out of the block. Therefore, we can safely modify the variable like `_mutable_integer = 3;` after we get out of the block.
