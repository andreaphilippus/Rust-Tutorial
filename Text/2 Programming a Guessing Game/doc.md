# Programming a Guessing Game

Things covered:

- `let`
- `match`
- methods
- use of functions
- external crates

## Set up new project

`$ cargo new guessing_game`

And run the auto-generated code (that will say hello world)

## Processing a Guess

Refer to `main.rs`. 

In order to take user input and print output, we use `io` crater, which is from the standard `std` library. We can tell the Rust code to use such crater by declaring them in the first place by
`use std::io;`. `A::B` represents that there is a function `B` associated to `A`.

`fn main(){}` function is the entry point into the program.

- `fn` is a syntax for declaring new function
- `()` for parameters
- `{}` encloses the body of the function

`println!`, where `!` represents macro, obviously prints something out

## Storing Values with Variables

We create a variable by using `let` like
`let *name*` but `let` by default is a variable that is IMMUTABLE.

So if we have `let a = 5;`, it means `a` will remain `5` for the whole period, and if we try to do `a = 6` to change the value assigned to `a`, the compiler will give an error. 

If we want to change the value from the name, which is by definition variable, we use `let mut *name*`, where we can change the value later.

## Receive user input

Function for taking input is in `io`: `io::stdin().read_line()`, and the argument is to store the input value to a variable. 

Instead of `io::stdin().read_line()` after `use std::io`, we can directly use this function by `std:io::stdin().read_line()` without declaring `use std::io`.

