`think of rust's `mut` as a key
- if you have a key you can change the data
- if you don't have a key, the data is locked, immutable

```rs
let x = 5; // data is locked , immutable
let y = &mut x // invalid borrow, the data is locked or immutable
```