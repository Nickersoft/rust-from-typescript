There are a couple of ways you can represent tuples in Rust: via literals or via structs. 

To illustrate, let's look at the following TypeScript example:

```typescript
type MyTuple = [number, boolean];

const myTuple: MyTuple = [1234, true] as const;

console.log(`Tuple values: ${myTuple[0]} and ${myTuple[1]}.`);
```

## Using a Literal

Perhaps the easiest way to represent a tuple in Rust is via its literal syntax:

```rust
type MyTuple = (i32, bool);

let my_tuple: MyTuple = (1234, true);

println!("Tuple values: {} and {}.", my_tuple.0, my_tuple.1);
```

## Using a Struct

Instead of using a [[Declaring Types|type alias]], you could also just use a struct:

```rust
struct MyTuple(i32, bool);

let my_tuple: MyTuple = MyTuple(1234, true);

println!("Tuple values: {} and {}.", my_tuple.0, my_tuple.1);
```

## Additional Reading

- [Rust by Example: Tuples](https://doc.rust-lang.org/rust-by-example/primitives/tuples.html)
- [Rust by Example: Structures](https://doc.rust-lang.org/rust-by-example/custom_types/structs.html)