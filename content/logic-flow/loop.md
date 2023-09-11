# Infinite Looping

Rust contains a special `loop` keyword that effectively acts as a shorthand for `while(true)`. You can use it to create infinite loops:

```rust
let mut count = 0u32;

// You can use the 'label: syntax to label loops and nest them!
'outer: loop {
	println!("Entered the outer loop");

	'inner: loop {
		println!("Entered the inner loop");

		count += 1;

		if count == 3 {
			// Skip the rest of this iteration
			continue;
		}

		if count == 4 {
			// Exit this loop
			break;
		}

		if count == 5 {
			// Exit the outer loop
			break 'outer;
		}
	}
}
```

## Additional Reading

- [Rust by Example: loop](https://doc.rust-lang.org/rust-by-example/flow_control/loop.html)