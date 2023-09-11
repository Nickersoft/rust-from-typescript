# Optionals

TypeScript doesn't technically have "optional" types. Instead, users must create union types that incorporate either `null` or `undefined`:

```typescript
const x: User | null = { name: 'Bill Gates' };

// Error: x is possibly 'null'
console.log(x.name);
```

Rust, on the other hand, has an official `Option` type. In fact, Rust's approach to optionals aligns very closely with that of [Swift](https://developer.apple.com/documentation/swift/optional).

In Rust, a variable of type `Option<T>` means that the variable is either:
- **`None`**: a safe way of representing `null`, or an "empty" value
- **`Some<T>`**: a wrapper around the value (of type `T`)

However – how do you know if a variable is `Some` or `None`? In TypeScript, you might use some form of [type narrowing](https://www.typescriptlang.org/docs/handbook/2/narrowing.html). In Rust, we have a full set of built-in keywords that make working with optionals a breeze.

## Matching

Although the [`match` keyword](../logic-flow/match.md) can function as a kind of `switch` statement, it also can be used to infer the value of optional types. 

Take for example the following code:

```rust
fn my_func(op: Option<i32>) {
    match op {
        None => {
	        println!("No value!")
	    },
        Some(value) => {
            println!("Contained value {}!", op)
        },
    }
}
```

## Conditionals

In TypeScript, ensuring a type is not null is pretty straightforward:

```typescript
if (x !== null) {
	console.log(x.name); // TSC knows that `x` is not null
}
```

However, seeing we have two separate types representing `null` and not-`null` in Rust, how do we write a similar `if` statement? Fortunately, Rust gives us the `if let` keyword:

```rust
if let x = Some(user) {
	println!("{}", user.name);
}
```

Of course, checking for `None` also works just like you'd expect:

```rust
if x == None {
	println!("Value is none!");
}
```


## Additional Reading

- [Rust by Example: Option](https://doc.rust-lang.org/rust-by-example/std/option.html?highlight=option#option)



