# Classes

Like many languages, Rust uses [structs](https://en.wikipedia.org/wiki/Struct_(C_programming_language)) instead of classes. Fortunately, structs can have both methods and fields, just like TypeScript classes.

Where in TypeScript you might write:

```typescript
class User {
	constructor(private name: string) {}

	public printName() {
		console.log(`Hello ${name}!`);
	}
}
```

In Rust, you would write:

```rust 
#[derive(Debug)]
struct User {
	name: String
}

impl User { 
	fn print_name(&self) { 
		println!("Hello {}!", self.name); 
	} 
}
```

Similar to [Python](https://www.geeksforgeeks.org/self-in-python-class/), methods in Rust accept its current `self` (equivalent to `this`) as the first parameter.