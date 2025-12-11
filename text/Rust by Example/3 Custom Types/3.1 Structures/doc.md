# Structures

Three types of *structs* that can be created using the `struct`:

1. Classic `C structs`
2. Tuple structs (unnamed struct)
3. Unit structs (no field)

Refer to `.\3.1 structure.rs` file.



## Classic struct

Syntax:

```rust
struct Person {
    name: String,
    age: u8,
}
```
<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->


- `struct Person {...}` defines a **new custom type** called `Person`
- Inside the braces we have **fields with names and types**
  - `name: String` &rarr; a heap-allocated UTF-8 string type, with name `name`
  - `age: u8` &rarr; an 8-bit unsigned integer (0-255) = `uint8` in MATLAB, with name `age`

Inside `fn main{}`, we can assign values to a variable having this structure as:

```rust
    let name = String::from("Peter");
    let age = 27;
    let peter = Person { name, age };
```

- `rustc` will enforce that `name` is `String` and `age` is `u8`.
- We can extract the field value of a struct variable just like in MATLAB, like:
  - `peter.name` will return `"Peter"`
  - `peter.age` will return `27`

In MATLAB, we would be writing like:

```MATLAB
person = struct;
person.name = "Peter";
person.age = 27;
```

Rust enforces the structure with fields **predefined**. In a nutshell,

- Rust `struct` is a **type *definition***
  - If trying to store value to a field that doesn't exist in `struct`, `rustc` will give an error. For example, `let height = 170;` followed by `let peter = Person {name, age, height};` will give an error because `struct Person` does not have `height` field *predefined*.
- MATLAB `struct`, on the other hand, is not, and if we have `person.height = 170;`, MATLAB will just create a new field under `person`, not causing an error

### Some useful struct operations

We define a structure named `Point` with two fields `x` and `y` both having `f32` type as:

```rust
struct Point {
    x: f32,
    y: f32,
}
```

In `fn main{}`,

```rust
    // Instantiate a `Point`
    let point: Point = Point { x: 5.2, y: 0.4 };
    let another_point: Point = Point { x: 10.3, y: 0.2 };
```

We created `point` and `another_point` having exactly same structure, but instantly as seen above. It is equivalent to:

```rust
    let point_x = 5.2;
    let point_y = 0.4;
    let another_point_x = 10.3;
    let another_point_y = 0.2;

    let point = Point {point_x, point_y};
    let another_point = Point {another_point_x, another_point_y};
```

which is pretty long... The instant struct declaration syntax can be broken down into:

- `let` &rarr; we know this; to define a new variable (immutable)
- `point: Point` &rarr; explicit type annotation; equivalent to saying "`point` has type `Point`
- `= Point {}` &rarr; construct a value of type `Point`

We can see that `point: Point` part is unnecessary because we later assign `Point{}` typed value. Yes, `: Point` can be omitted, and we can idiomatically write as:

```rust
    // Instantiate a `Point`
    let point = Point { x: 5.2, y: 0.4 };
    let another_point = Point { x: 10.3, y: 0.2 };
```

As we already know, this `Point{}` struct is fixed to 2-D shape. **Can we add new fields to a struct at any time during runtime? NO**. It ensures the safety of the code, unlike MATLAB where we can possibly add `point.z` at any time.

#### Copying values from a struct variable

Example:

```rust
    let bottom_right = Point { x: 10.3, ..another_point };
```

We see a new syntax `..another_point`. Above line in natural language is:

> Create an immutable variable `bottom_right` with `Point` structure, having `x` value of `10.3` and **the rest of the values are to be copied from `another_point`**.

Therefore, `..another_point` in above line will automatically assign `y: 0.2`. It is equivalent to writing:

```rust
    let bottom_right = Point { x: 10.3, y: another_point.y};
```

Nothing much changed but imagine we have a struct variable with thousands of fields and want to change only a few fields from an existing variable. This is useful. In MATLAB, we could only do by copying the whole structure and changing the specific fields (at least 2 lines needed!), like:

```matlab
    bottom_right = another_point;
    bottom_right.x = 10.3;
```

A rule when using this syntax:

> `..another_point` should always come at the end of the field list

We **cannot** do `let bottom_right = Point { ..another_point, x: 10.3 };`

#### Parsing, destructing struct

Example:

```rust
    let Point { x: left_edge, y: top_edge } = point;
```

In natural language,

> Take `point` which has `Point` structure, and `let` its field `x` to a new immutable variable `left_edge`, and `y` to a new immutable variable `top_edge`

Basically equivalent to:

```rust
    let left_edge = point.x;
    let top_edge = point.y;
```

We can assign field values to new variables with **field name** by using the following syntax, but not recommended when there are multiple variables with same struct:

```rust
    let Point {x, y} = point;
```

which is equivalent to `let x = point.x;` and `let y = point.y;`.

If we want to parse only specific ones and ignore the others, we can use `..` as:

```rust
    let Point {x, ..} = point;
```

which doesn't do `let y = point.y;`. It is somewhat like `~` in MATLAB but since MATLAB doesn't have this whole struct destruction thing, just take the concept.

#### Nesting struct

Example:

```rust
struct Rectangle {
    top_left: Point,
    bottom_right: Point,
}
```

We can nest structures! The above structure has the layout of:

`Rectangle = { Point { x, y }, Point { x, y }}`

In `fn main{}`, we have the following

```rust
    let _rectangle = Rectangle {
        // struct instantiation is an expression too
        top_left: Point { x: left_edge, y: top_edge },
        bottom_right: bottom_right,
    };
```

We can see two things here:

1. `top_left` value is constructed using `Point{}` structure using `left_edge` and `top_edge`
2. `bottom_right` field gets its value from an existing variable `bottom_right` which also has `Point{}` struct.
   1. Quite confusing, but field name and existing variable to feed into the struct do not have to have different names.
   2. The important part is that the struct type should match.

Plus, a leading `_` from `_rectangle` just tells the compiler that we are aware that this variable is not used. `rustc` gives a warning (not error!) when a variable is not used. 

In MATLAB, it would work straightforward, like `rectangle.top_left.x = left_edge;`. Accessing nested field in Rust is just like MATLAB:

`_rectangle.top_left.x` will give the value `left_edge`.

**IMPORTANT THING:**

- In Rust, when using `let` to define a variable of a structure, **we must give values to ALL EXISTING FIELDS**. We cannot omit any single field when initializing. For example, 

```rust
    let _rectangle = Rectangle {
        top_left: Point {x: 1, y: 2},
    }
```

will give compile error. MATLAB can do it.

##### Parsing nested struct

Just like struct, we can destruct a nested struct like this:

```rust
    let Rectangle {
        top_left: Point { x: left, y: top},
        bottom_right: Point { x: right, y: bottom},
    } = _rectangle;
```

which is equivalent to

```rust
    let left = _rectangle.top_left.x;
    let top = _rectangle.top_left.y;
    let right = _rectangle.bottom_right.x;
    let bottom = _rectangle.bottom_right.y;
```

## Unit struct

Syntax:

```rust
struct Unit;
```

It's weird. A unit struct is a struct with **no fields at all**. It's got some traits:

- Got no data
- Has a distinct type name (`Unit`)
- **Size zero** at runtime

Why do we even want this? We can use it for the following cases:

### Marker / Tag Type

It is sometimes helpful to have a marker or tag to encode information in the type system. For example, state machine type with the following:

```rust
struct Idle;
struct Running;

// A generic struct parameterized by a state type
struct Machine<State> {
    speed: f32,
    state: std::marker::PhantomData<State>,
}

// Now Machine<Idle> and Machine<Running> are different types
```

This might be useful because in MATLAB, to represent such thing, we need to have another field with probably a string or something, like `Machine.state = "Idle";`.

## Tuple struct

Syntax:

```rust
struct Pair(i32, f32)
```

- Tuple struct is a struct **with no field names**, but each field is just numerical index valued from 0
  - We can say this is somewhat like array
- We can see we can define the number of fields (number of arguments) and data type of each field

In `fn main`:

```rust
    // Instantiate a tuple struct
    let pair = Pair(1, 0.1);
```

This creates a variable `pair`, with fields accessble by:

- `pair.0` &rarr; `1` (i32 integer)
- `pair.1` &rarr; `0.1` (f32 float)

We can destruct more simply than classical struct:

```rust
    let Pair(integer, decimal) = pair;
```

This is equivalent to:

```rust
    let integer = pair.0;
    let decimal = pair.1; 
```

**The order matters!**

MATLAB arrays require same type, so if we were to create such thing in MATLAB, we'd use a cell.
