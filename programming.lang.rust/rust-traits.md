# Rust traits

https://blog.rust-lang.org/2015/05/11/traits.html

Defining and implementing a trait is really nothing more than abstracting out a common interface satisfied by more than one type.

e.g. 

fn print_hash<T: Hash>(t: &T)
The function print_hash function is generic over an unknown T, but:

<T: Hash> , read as T must implement the Hash trait

static dispatch = direct static calls improve performance