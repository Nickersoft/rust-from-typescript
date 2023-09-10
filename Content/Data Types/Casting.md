Just like in TypeScript, you can explicitly cast any literal in Rust via the `as` keyword. 

```rust
let decimal = 65.4321_f32;
let integer = decimal as u8; 
```

However, the system breaks down when you are dealing with structs and enums. For instance, you can't simply cast a literal to a struct (to be fair, I'm not sure you can in TypeScript either):

```rust
// Error: non-primitive cast: `i32` as `Number`
let user = 30 as Number;
```

To cast properly, we'll need to use either the `From` or `Into` [[Traits|trait]]:
- **`From`** allows you to write a method that instantiates a new struct *from a passed value*
- **`Into`** allows you to *convert an existing value* into the desired struct

They seem very similar, don't they? Let's look at two examples, both of which allow us to convert the above number (30) into a `Number`.

```rust
use std::convert::{From, Into};

#[derive(Debug)]
struct Number {
    value: i32,
}

impl From<i32> for Number {
    fn from(item: i32) -> Self {
        Number { value: item }
    }
}

impl Into<Number> for i32 {
    fn into(self) -> Number {
        Number { value: self }
    }
}

fn main() {
	// Creates a new Number struct from 30
    let num1: Number = Number::from(30);
    
    // Converts 30 into a Number
	// Note that a type annotation is needed for into() to work
    let num2: Number = 30.into();
}
```

In fact, the `Into` implementation in the above code isn't even really needed – if `From` is implemented on the type, `into` will be added for free!

## Dealing with Errors

However – what if our type conversion can actually fail? For instance, what if we only wanted `Number` to store even numbers and error otherwise?

For this case, we would instead use the `TryFrom` and `TryInto` traits. These traits return a [[Error Handling|Result]] instead of just the value:

```rust
#[derive(Debug, PartialEq)]
struct EvenNumber(i32);

impl TryFrom<i32> for EvenNumber {
    type Error = ();

    fn try_from(value: i32) -> Result<Self, Self::Error> {
        if value % 2 == 0 {
            Ok(EvenNumber(value))
        } else {
            Err(())
        }
    }
}

fn main() {
    // Ok(EvenNumber(8))
	let num1: Result<EvenNumber, ()> = EvenNumber::try_from(8);
	// Err(())
    let num2: Result<EvenNumber, ()> = 5i32.try_into();
}
```

## Additional Reading

- [Rust by Example: Casting](https://doc.rust-lang.org/rust-by-example/types/cast.html)
- [Rust by Example: Conversion](https://doc.rust-lang.org/rust-by-example/conversion.html)
