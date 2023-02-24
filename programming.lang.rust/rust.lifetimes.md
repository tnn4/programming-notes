Rust lifetimes are a kind of generic so they go in the same spot as generic parameters like T in the angle brackets.

```
use std::fmt::Display;

fn longest_with_an_announcement<'a, T>(
    x: &'a str,
    y: &'a str,
    ann: T, 
) -> &'a str
where
    T: Display, // can be filled with any type that implements `Display` trait
{
    println!("Announcement! {}", ann);
    if x.len() > y.len() {
        x
    } else {
        y
    }
}


```
