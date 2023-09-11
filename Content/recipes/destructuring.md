# Destructuring & Spreading

Just like in TypeScript, objects can have their properties destructured and spread.

Say we have the following TypeScript code:

```typescript
const user: User = {
	name: 'Spongebob Squarepants',
	age: 20
};

const { name: userName, ...rest } = user;

const newUser: User = { name: 'Patrick Star', ...rest };

console.log(`${userName}'s friend is ${newUser.name}.`);
```

In Rust, we would write:

```rust
struct User {
	name: String,
	age: i32
}

let user = User { name: "Spongebob Squarepants", age: 20 };

let User { name: userName } = user;

let newUser = User { name: 'Patrick Star', ..user };

println!("{}'s friend is {}.", userName, newUser.name);
```

You may have noticed we don't have a `...rest` parameter here. That is due to the fact that Rust doesn't support spread operations while destructuring.

Fortunately, the next line saves us: the `..` "spread" syntax (technically referred to as the [struct update syntax](https://doc.rust-lang.org/book/ch05-01-defining-structs.html#creating-instances-from-other-instances-with-struct-update-syntax)) is a shorthand for copying over any struct properties that are not currently defined in the target struct. In this case, it will copy over the `age` property of the `user` variable while preserving the `name` of "Patrick Star".