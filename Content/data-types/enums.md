# Enums

Just like TypeScript, Rust also has enums. That said, they are more akin to Swift-styled enums in the sense they can contain [associated values](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/enumerations/#Associated-Values). 

In fact, they go even a step beyond Swift, as they allow you to store *entire structs* as enum values.

TypeScript only allows scalar values for its enums, meaning you're stuck with this:

```typescript
enum WebEvent {
	PageLoad = 'PAGE_LOAD',
	PageUnload = 'PAGE_UNLOAD',
	// ...and so on...
}
```

To illustrate, let's just take a look at the example directly from the Book:

```rust
// Create an `enum` to classify a web event. Note how both
// names and type information together specify the variant:
// `PageLoad != PageUnload` and `KeyPress(char) != Paste(String)`.
// Each is different and independent.
enum WebEvent {
    // An `enum` variant may either be `unit-like`,
    PageLoad,
    PageUnload,
    // like tuple structs,
    KeyPress(char),
    Paste(String),
    // or c-like structures.
    Click { x: i64, y: i64 },
}

// A function which takes a `WebEvent` enum as an argument and
// returns nothing.
fn inspect(event: WebEvent) {
    match event {
        WebEvent::PageLoad => println!("page loaded"),
        WebEvent::PageUnload => println!("page unloaded"),
        // Destructure `c` from inside the `enum` variant.
        WebEvent::KeyPress(c) => println!("pressed '{}'.", c),
        WebEvent::Paste(s) => println!("pasted \"{}\".", s),
        // Destructure `Click` into `x` and `y`.
        WebEvent::Click { x, y } => {
            println!("clicked at x={}, y={}.", x, y);
        },
    }
}

fn main() {
    let pressed = WebEvent::KeyPress('x');
    // `to_owned()` creates an owned `String` from a string slice.
    let pasted  = WebEvent::Paste("my text".to_owned());
    let click   = WebEvent::Click { x: 20, y: 80 };
    let load    = WebEvent::PageLoad;
    let unload  = WebEvent::PageUnload;

    inspect(pressed);
    inspect(pasted);
    inspect(click);
    inspect(load);
    inspect(unload);
}
```

Rust also manages to one-up TypeScript by allowing you to import enum values directly without needing to prefix them:

```rust
// Explicitly `use` each name so they are available without 
// manual scoping.
use crate::Status::{Poor, Rich};
// Automatically `use` each name inside `Work`.
use crate::Work::*;

// Equivalent to `Status::Poor`.
let status = Poor;
// Equivalent to `Work::Civilian`.
let work = Civilian;
```

## Additional Reading

- [Rust by Example: Enums](https://doc.rust-lang.org/rust-by-example/custom_types/enum.html)