# Arrays and Slices

## Arrays

Syntax:

```rust
    // Array signature consists of Type T and length as [T; length].
    let my_array: [i32; 5] = [1, 2, 3, 4, 5];
```

Very similar to MATLAB, all elements should have the same types. The differences:

1. Rust array indexing starts from 0, unlike 1 as in MATLAB. More convenient if you are a Python user.
2. Syntax of calling element is `my_array[#index#]` unlike MATLAB's `my_array(#index#)`. It's more like Python.
   - However, it is much safer to **use my_array.get(#index#)** method because if the index we want to call is beyond the length of the array, the system *panics* (will be explained later, it's just bad as the system will try to look for non-existing element for a long time) and will give runtime error while `.get()` gives an option (will also be explained later) that tells if the index is beyond the maximum index.
     - More like `try` and `catch` in MATLAB
3. Rust array does not have orientation information unlike MATLAB does with `,` (horizontal) and `;` (vertical).
   - In MATLAB, `my_array = [1,2,3,4,5]` has size of `[1,5]`, but in Rust, `my_array: [i32; 5]` only has 1D dimension, it just simply implies *5 elements*.
   - We can have nested arrays in Rust, just like Python, to represent "row" and "column".

```rust
    // 1 x 3 (row)
    let row: [[i32; 3]; 1] = [[1, 2, 3]];

    // 3 x 1 (column)
    let col: [[i32; 1]; 3] = [[1], [2], [3]];
```

**However,** we know we use "row" and "col" to do some linear algebra stuff. It is strongly advised to use crates that define row vectors or column vectors that can be used for mathematical operations. Some of the crates are:

- `nalgebra`
- `ndarray`

We can also create an array of same values for all the elements, just like

```rust
    let ys: [i32; 500] = [0; 500];
```

This is equivalent to MATLAB's `zeros(1,500)`. In MATLAB, we only have `ones()` and `zeros()` for these. Other numbers? Nope. Rust can do it simply. In Rust, `[5; 500]` gives the equivalent array of `5 * ones(1,500)` in MATLAB.

### Useful methods

1. `array.len()` &rarr; `usize` returns the length of `array`
   - Same as `len(array)` in MATLAB
2. `array.is_empty()` &rarr; `bool` true if `array.len() == 0`
   - Same as `isempty(array)` in MATLAB
3. `array.first()` = `array[0]`, `array.first_mut()` gives mutable (useful for loop)
4. `array.last()` &rarr; returns the last element of array
   - Same as `array(end)` in MATLAB
5. `array.sort()` &rarr; sorts (requires `Ord`)
6. `array.iter().min()` &rarr; returns minimum value of array
   - Same as `min(array)` in MATLAB
7. `array.iter().max()` &rarr; returns maximum value of array
   - Same as `max(array)` in MATLAB

## Slices

Slices are similar to arrays, but the length is not known at compile time.

Slice is a two-word object:

1. Pointer to the data
2. Length of the slice

Slices can be used to borrow *a section* of an array, and have the type signature `&[T]`. It can be created by appending `&` in front of an array, like `&my_array`.

**Why is it useful?**

It is useful when we try to use a function that needs to accept any length of *array*s, such as

```rust
// This function borrows a slice.
fn analyze_slice(slice: &[i32]) {
    println!("First element of the slice: {}", slice[0]);
    println!("The slice has {} elements", slice.len());
}
```

Remember that array length is **fixed** throughout runtime and should be defined. Therefore, if we were to create a function that requires *arrays* as the input, we need to define the length of the array in the parameter of the function, like

```rust
fn analyze_array(array: &[i32, 4]) {
    println!("First element of the array: {}", array[0]);
    println!("The array has {} elements", array.len());
}
```

which only accepts an array **with length of 4** in it. This function analyzes the length of the array, and it only accepts an array where the length is always fixed. Therefore, if we were to call it using `analyze_array(my_array)`, `rustc` will give error because function `analyze_array` can only accept array of size 4 and `my_array` has 5. It works if we have `let xs = [1, 2, 3, 4];` and call `analyze_array(xs)`.

However, a function using slices as input parameter is more flexible as long as the type matches. We can do `analyze_slice(&my_array)`, `analyze_slice(&xs)`, `analyze_slice(&ys)`, and all will work just fine.

We can also **extract** parts of array into slice using syntax as

`&my_array[#start index# .. #end index#]`

For example, `&my_array[1 .. 3]` gives a slice of `[2, 3, 4]`. In MATLAB, it's same as `my_array(2:4)` but MATLAB gives another array as the concept `slice` doesn't exist in MATLAB.
