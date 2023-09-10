By default, Rust doesn't know how to print non-scalar data.

```rust
use std::fmt;

struct Structure(i32);

// Error: `Structure` doesn't implement `std::fmt::Display`!
println!("Now {} will print!", Structure(7));
```

To remedy this, we need to use either the `Display` trait or the `Debug` attribute. You can think of `Display` as overriding the structure's `toString()` method, whereas `Debug` is more akin to `JSON.stringify()` (or just passing the object directly to `console.log`).

## Debug

Let's look at some examples, starting with the easier of the two attributes: `Debug`.

To achieve the equivalent TypeScript code:

```typescript
class Structure { 
	constructor(public value: number) {} 
}

console.log(`Now ${new Structure(7)} will print!`);
```

You would just add the `Debug` attribute annotation and leverage the `{:?}` format string to print:

```rust
use std::fmt;

#[derive(Debug)]
struct Structure(i32);

// Output: Now Structure(7) will print!
println!("Now {:?} will print!", Structure(7));
```

You can also pretty-print your debugged object in an output style more akin to `JSON.stringify()` by using the `{:#?}` format string: 

```rust
use std::fmt;

#[derive(Debug)]
struct Person {
	age: u8 
}

let person = Person { age: 17 };

// Output: Person { age: 17 }
println!("{:#?}", person);
```
## Display

To *customize* the way an object is represented when printing to stdout, we'll need to use the `Display` [[Traits|trait]] instead. 

In TypeScript, you might achieve this by giving a class a custom `.toString()` method:

```typescript
class Structure { 
	constructor(public value: number) {} 

	toString() {
		return `The value is ${value}!`;
	}
}
```

In Rust, it's the same idea:

```rust
use std::fmt;

struct Structure(i32);

impl fmt::Display for Structure {
	fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result { 
		// Notice the lack of a semicolon below. 
		// This means we are returning the value of write!,
		// which in this case is a fmt:Result
		write!(f, "The value is {}!", self.0)
	} 
}

println!("{}", Structure(7));
```

## Additional Reading

- [Rust by Example: Formatted Print](https://doc.rust-lang.org/rust-by-example/hello/print.html)
- [`fmt` Module](https://doc.rust-lang.org/std/fmt)