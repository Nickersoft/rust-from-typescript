In the world of JavaScript or TypeScript, you'll typically see different functions for parsing strings into different objects. For dates, there is `Date.parse()`. For integers, there is `parseInt()`.

In Rust, there is just `FromStr`.

By having a struct conform to the `FromStr` trait, you can effectively tell a Rust string exactly how to parse it.

Let's look at a simple example first. `FromStr` is already implemented for the built-in `i32` (32-bit signed integer) type, so parsing a numerical string is super easy:

```rust
const num1: i32 = "10".parse()?; // 10
const num2 = "20".parse<i32>()?; // 20
```

Now let's say you want to be able to parse a string of the format "(10, 20)" into a `Point` struct. You can achieve this by manually adding your own `FromStr` implementation:

```rust
use std::str::FromStr;

#[derive(Debug, PartialEq)]
struct Point {
    x: i32,
    y: i32
}

#[derive(Debug, PartialEq, Eq)]
struct ParsePointError;

impl FromStr for Point {
    type Err = ParsePointError;

    fn from_str(s: &str) -> Result<Self, Self::Err> {
        let (x, y) = s
            .strip_prefix('(')
            .and_then(|s| s.strip_suffix(')'))
            .and_then(|s| s.split_once(','))
            .ok_or(ParsePointError)?;

        let x_fromstr = x.parse::<i32>().map_err(|_| ParsePointError)?;
        let y_fromstr = y.parse::<i32>().map_err(|_| ParsePointError)?;

        Ok(Point { x: x_fromstr, y: y_fromstr })
    }
}

let point1: Point = "(10, 20)".parse();
let point2: Point = Point::from_str("(20, 30)");
```

Notice that unlike [[Data Types/Casting|with casting and conversions]], `FromStr` always returns a [[Error Handling|Result]], as there's never any guarantee a string will be valid. Therefore, there is no `TryFromStr` trait like there is `TryFrom`.

## Additional Reading

- [`FromStr` docs](https://doc.rust-lang.org/std/str/trait.FromStr.html)