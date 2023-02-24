# What's the point of borrowing?

The borrowing is what keeps code safe and performant.

It's about memory management.

Good memory management keeps your program performant and safe.

Rust enforces proper memory management with the borrow checker.

Pros of the Rust Model:
- the borrow checker makes creating data race conditions harder so concurrency is easier

Cons:
- certain data structures that are simple to create in other languages are hard to get right in Rust 

If you can't copy, clone. Clone is expensive.

Don't clone if you can let someone else borrow it.

Borrowing is cheap and allow other functions to temporarily use the data and return it when done.

[introducing the rust borrow checker](https://blog.logrocket.com/introducing-the-rust-borrow-checker/)