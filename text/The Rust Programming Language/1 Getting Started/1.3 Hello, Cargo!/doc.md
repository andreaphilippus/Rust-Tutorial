# Hello, Cargo!

Cargo: build system & package manager

What can Cargo do?

- Build code
- Download libraries of the code dependency
- Build libraries

Cargo is installed when installing Rust; check by
`$ cargo --version`

## Create a Project with Cargo

Create a new project using the following:
`$ cargo new hello_cargo`
`$ cd hello_cargo`
inside `./projects`.

It also creates a git files if there isn't one in the parent folder.

We then see:

- `src` folder: source folder including `main.rs`
- `Cargo.toml` that includes the following information:
  - Package: Cargo configuration with the following information:
    - name
    - version
    - edition
  - Dependencies: where we can list libraries (called the *crates* in Rust)

## Build Cargo Project

First build project by
`$ cargo build`

Then it compiles and creates an executable file under `debug` folder.

If you want to compile and run right afterwards, use
`$ cargo run`
which will automatically compile and run the executable file.

If you want to check if the code would work (with no error), instead of using `build` or `run` to compile, you can use
`$ cargo check`

For release version, use `$ cargo build --release`, which will take more time compiling but also does optimization such that the executable file runs faster.