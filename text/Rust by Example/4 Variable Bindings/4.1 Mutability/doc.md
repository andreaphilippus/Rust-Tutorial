# Mutability

When using `let` variables are by default **immutable**, but we can override by using `let mut`, which can be modified later in the code.

```rust
    let _immutable_binding = 1;
    let mut mutable_binding = 1;
```

Here, `_immutable_binding` cannot be modified while `mutable_binding` can be modified just as in MATLAB.

The following code will be tolerated:

```rust
    mutable_binding += 1;
```

but the following code will give compile error:

```rust
    _immutable_binding += 1;
```
