# Returning Stuff

When it comes to returning data from functions, Rust differs from other languages in a couple of ways:
- There is no `return` keyword. To return a value, simply omit the semicolon (`;`) from the end of the line.
- You can define blocks *inside* existing functions so you can compute the value of a single variable using multiple lines.

Like other languages (including TypeScript), not returning anything from a function will return `void` by default. `void` values in Rust are denoted via empty parentheses `()`.

Let's take a look this in action:

```rust
fn my_func() -> u32 {
	let x = 5u32;
	 
    let y = {
        let x_squared = x * x;
        let x_cube = x_squared * x;

        // This expression will be assigned to `y`
        x_cube + x_squared + x
    };

	y // Returns `y`
}
```

## Additional Reading

- [Rust by Example: Expressions](https://doc.rust-lang.org/rust-by-example/expression.html)
- [Rust by Example: Functions](https://doc.rust-lang.org/rust-by-example/fn.html)