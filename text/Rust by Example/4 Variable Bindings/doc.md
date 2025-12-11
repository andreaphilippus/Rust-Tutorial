# Variable Bindings

As we all know, we can annotate the type when declaring a variable. But sometimes `rustc` will be able to infer the type of the variable from the context, such that we don't have to worry about annotation for most of the times.

`let` binds a value to variable, with a type.

`rustc` warns us in case a defined variable is not called/used throughout the program, and we can bypass that warning by adding a leading `_` in front of the variable that we know we won't use, like

```rust
    let _unused_variable = 3u32;
```

whereas the following line will make `rustc` give an error (still compiles though, it's just noisy):

```rust
    let noisy_unused_variable = 3u32;
```
