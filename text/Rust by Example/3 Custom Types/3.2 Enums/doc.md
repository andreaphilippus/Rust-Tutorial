# Enums

`enum` keyword creates a type which may be one of a few different variants. This concept doesn't exist in MATLAB. It is more like **tagging**. The syntax is:

```rust
enum EnumName {
    // unit-like
    Unit_Variant1,
    Unit_Variant2,
    // tuple-like
    Tuple_Variant(char),
    Tuple_Variant(String),
    // struct-like
    Struct_Variant { field1: i32, field2: i32 },
}
```

and each variant can be called by `EnumName::#Variant_Name#` such as `EnumName::Unit_Variant1`.

Example:

```rust
enum WebEvent {
    // An `enum` variant may either be `unit-like`,
    PageLoad,
    PageUnload,
    // like tuple structs,
    KeyPress(char),
    Paste(String),
    // or c-like structures.
    Click { x: i64, y: i64 },
}
```

and in `fn main`,

```rust
    let pressed = WebEvent::KeyPress('x');
    // `to_owned()` creates an owned `String` from a string slice.
    let pasted  = WebEvent::Paste("my text".to_owned());
    let click   = WebEvent::Click { x: 20, y: 80 };
    let load    = WebEvent::PageLoad;
    let unload  = WebEvent::PageUnload;
```

What it does is: we assign a variable a value of a type, tagged by a variant in enum. For example, `pressed` variable is simply `'x'`. We could say `let pressed = 'x'`. However, using `WebEvent` enum adds tag of `KeyPress` to the value, so `pressed` variable contains two information.

This is different from `struct` because a variable has to either

1. Have all the fields
2. Not have the tag

This is useful when we try to access the value by searching for tag (mostly by using `match`, which is equivalent to `switch` and `case` in MATLAB). For example,

```rust
fn inspect(event: WebEvent) {
    match event {
        WebEvent::PageLoad => println!("page loaded"),
        WebEvent::PageUnload => println!("page unloaded"),
        // Destructure `c` from inside the `enum` variant.
        WebEvent::KeyPress(c) => println!("pressed '{}'.", c),
        WebEvent::Paste(s) => println!("pasted \"{}\".", s),
        // Destructure `Click` into `x` and `y`.
        WebEvent::Click { x, y } => {
            println!("clicked at x={}, y={}.", x, y);
        },
    }
}
```

The input parameter is an `WebEvent` which is `enum` and is referred as `event` in this `inspect` function. The cases are examined just by `enum::variant` because a variable passed to `inspect()` is expected to have `enum` tag.

This is useful because `pressed`, `pasted`, `click`, etc. all have mutable (although in the example we have immutable variables) variables and if the values keep changing we cannot effectively use `match` function.

## Type alias

A good code has a generic, easy-to-catch names, and it also applies to `enum` as well. We can copy `enum` quantity like:

```rust
enum VeryVerboseEnumOfThingsToDoWithNumbers {
    Add,
    Subtract,
}

// Creates a type alias
type Operations = VeryVerboseEnumOfThingsToDoWithNumbers;

fn main() {
    // We can refer to each variant via its alias, not its long and inconvenient
    // name.
    let x = Operations::Add;
}
```

which kind of loses its purpose of naming traditions. We use this type alias mostly in `impl` blocks using `Self` alias (will be covered later), such as:

```rust
enum VeryVerboseEnumOfThingsToDoWithNumbers {
    Add,
    Subtract,
}

impl VeryVerboseEnumOfThingsToDoWithNumbers {
    fn run(&self, x: i32, y: i32) -> i32 {
        match self {
            Self::Add => x + y,
            Self::Subtract => x - y,
        }
    }
}
```
