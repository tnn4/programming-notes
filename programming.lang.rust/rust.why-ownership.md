https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html

The main purpose of ownership is to manage heap data

Heap access is expensive because it requires following pointers. Imagine doing that 100,000 times a at a bigger scale. It gets expensive.