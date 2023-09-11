# Variables & Mutability

Like TypeScript, Rust has a `const`, `static`, and `let` keyword. Unfortunately, their meanings slightly vary.

- **`let`** variables, unlike in TypeScript, represent *immutable values*. To make a `let` variable mutable, you must use the `mut` keyword.
- **`const`** variables, like `let` variables (see below), represent immutable values. In other languages, this would most likely be referred to as a `static` variable (confusing, I know).
- **`static`** variables are (rarely used) *global variables* that represent memory addresses. The primary use cases are global locks, global atomic counters, and interfacing with legacy C libraries.

## The differences between `const` and `let`

As summed up nicely in [this article](https://nickymeuleman.netlify.app/garden/rust-let-const), there are a few notable differences between `const` and `let` variables:

- You aren’t allowed to use `mut` on constants.
- The type of a constant _must_ be declared, whereas the type of a variable _may_ be declared.
- Constants can only be set to a *constant* expression, not to the result of a function call or anything that could only be determined at runtime.

## Additional Reading

- [`const` vs. `static` RFC](https://github.com/rust-lang/rfcs/blob/master/text/0246-const-vs-static.md)
- [Rust: `let` vs. `const`](https://nickymeuleman.netlify.app/garden/rust-let-const)
- [Rust by Example: Mutability](https://doc.rust-lang.org/rust-by-example/variable_bindings/mut.html)
- [Rust by Example: Constants](https://doc.rust-lang.org/rust-by-example/custom_types/constants.html)
