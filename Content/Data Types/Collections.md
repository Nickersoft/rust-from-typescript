While collections in TypeScript can almost always be represented by the `T[]` or `Array<T>` type annotations, collections are much more nuanced in Rust. 

There are three primary kinds of collections: vectors, arrays, and slices.

1. **Arrays** in Rust, like in many other languages, have a *static* length that is specified *when the array is initialized*. In the example used in the cheat sheet, we're initializing an array of type `T` with a max length of 5 elements.
2. **Slices** are just that: slices of other arrays. You can think of it as the result of calling `Array.slice` on an array. Unlike an array, the length of a slice is not known at compile time.
3. **Vectors**, like in C++, are arrays that can have a variable length not known at compile-time. For most purposes, you'll most likely end up using these.

## Additional Reading

- [Rust by Example: Arrays and Slices](https://doc.rust-lang.org/rust-by-example/primitives/array.html)
- [Rust by Example: Vectors](https://doc.rust-lang.org/rust-by-example/std/vec.html?highlight=vector#vectors)




