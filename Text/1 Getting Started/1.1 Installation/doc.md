# Installation

Rust can be installed using the executable file from the [official website (x64)](https://static.rust-lang.org/rustup/dist/x86_64-pc-windows-msvc/rustup-init.exe).

Check whether Rust is installed correctly or not by running `$ rustc --version`

## Update

`$ rustup update`

## Uninstall

`$ rustup self uninstall`

## Local Documentation

Basically a more detailed version of this doc. Open by

`$ rustup doc`

### Packages for the tutorial
`$ cargo new get-dependencies`
`$ cd get-dependencies`
`$ cargo add rand@0.8.5 trpl@0.2.0`