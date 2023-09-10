For all numeric types in Rust, you can simply append the desired type to the end of the number to cast it:

```rust
let x = 1u8;
let y = 2u32;
let z = 3f32;

// is equivalent to

let x: u8  = 1;
let y: u32 = 2;
let z: f32 = 3;
```
