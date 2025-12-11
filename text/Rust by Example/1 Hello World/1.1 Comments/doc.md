# Comments

There are two types of comments in Rust:

## Regular comments ignored by the compiler

Syntax:

- `//` &rarr; single line comment, equivalent to `%` in MATLAB
- `/* */` &rarr; block comment, *similar* to `%{ %}` in MATLAB
  - Difference: `/* */` can be used within a line to comment out certain columns but `%{ %}` in MATLAB can't do that

Example:

```rust
    // This is an example of a line comment.
    // There are two slashes at the beginning of the line.
    // And nothing written after these will be read by the compiler.
```

```rust
    /*
     * This is another type of comment, a block comment. In general,
     * line comments are the recommended comment style. But block comments
     * are extremely useful for temporarily disabling chunks of code.
     * /* Block comments can be /* nested, */ */ so it takes only a few
     * keystrokes to comment out everything in this main() function.
     * /*/*/* Try it yourself! */*/*/
     */

    /*
    Note: The previous column of `*` was entirely for style. There's
    no actual need for it.
    */
```

```rust
    let x = 5 + /* 90 + */ 5;
    println!("Is `x` 10 or 100? x = {}", x);
```

## Doc comments parsed into HTML library documentation

This is something MATLAB does not have. We have the following syntaxes:

- `///` &rarr; Generate library docs for the line
- `//!` &rarr; Generate library docs for the block
