https://doc.rust-lang.org/std/sync/struct.Arc.html

WTF is Rust Arc?

Arc = Atomically Reference Counted

A thread-safe reference counting pointer.

Unlike `Rc<T>`, `Arc<T>` use atomic operations for reference counting, so it is thread-safe.
But, this comes with the cost of more expensive memory access.

If you are not sharing reference-counted allocations between threads, consider `Rc<T>`.