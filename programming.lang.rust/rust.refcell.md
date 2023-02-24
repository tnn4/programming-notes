Refcell allows data mutation under immutable refernces. Warning: this is `unsafe`, there are no memory guarantees when you do this

The RefCell<T> type is useful when you’re sure your code follows the borrowing rules but the compiler is unable to understand and guarantee that.

I.e. use RefCell if you know what you are doing

[Rust Interior Mutability](https://doc.rust-lang.org/book/ch15-05-interior-mutability.html)

interior mutability: mutate data even with immutable references, i.e. mutable borrow to immutable value