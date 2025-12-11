# use

We know `use` because we use that to import crates. Remember we also use `::` to specify which sub-module we want to take from a bigger module. We call this act *scoping*. We can use `use` to import `enum` name to directly call their variants as tags!

Suppose we have two `enum` as:

```rust
enum Stage {
    Beginner,
    Advanced,
}

enum Role {
    Student,
    Teacher,
}
```

Syntax **inside `fn main()`**:

```rust
    use crate::Stage::{Beginner, Advanced};
    // Automatically `use` each name inside `Role`.
    use crate::Role::*;

    let stage = Beginner; // == Stage::Beginner
    let role = Student;   // == Role::Student
```

`crate`, when used inside a Rust file, simply means "this crate's root". It's the *top-level namespace* for the current project.

There are two ways of using `use` to import `enum` names:

1. Select only what I want to use by `use crate::#enum#::{#variant1, #variant2, ...};`
   - If we had more than 2 variant for `enum Stage`, say `Master` variant, the code above won't allow me to write `let stage = Master;` I only have to write `let stage = Stage::Master;` because I did not include it when `use`d it.
2. Import every variants in the enum by `use crate::#enum#::*;`

It helps shortening the code, but not advised when there are bunch of `enum`s that may confuse which variant comes from which `enum`, and of course we cannot use `use` when multiple `enum`s have same `variant` name. 

Also when using `match`, we don't have to call the full `enum` when we used `use`, like:

```rust
    match stage {
        // Note the lack of scoping because of the explicit `use` above.
        Beginner => println!("Beginners are starting their learning journey!"),
        Advanced => println!("Advanced learners are mastering their subjects..."),
    }

    match role {
        // Note again the lack of scoping.
        Student => println!("Students are acquiring knowledge!"),
        Teacher => println!("Teachers are spreading knowledge!"),
    }
```

The above code, without `use`, would be written as:

```rust
    let stage = Stage::Beginner; 
    let role = Role::Student;  

    match stage {
        Stage::Beginner => println!("Beginners are starting their learning journey!"),
        Stage::Advanced => println!("Advanced learners are mastering their subjects..."),
    }

    match role {
        Role::Student => println!("Students are acquiring knowledge!"),
        Role::Teacher => println!("Teachers are spreading knowledge!"),
    }
```
