rust:Option represents optional value

Options are either Some or None

```
      [Some]
      /
Option
      \ 
    [None]
```

Why? Rust does not support "safe" use of NULL pointers.
None gives you a safe way of dealing with nulls.

It is represented as an enum:

Module std::option

Enum std::option::Option

Example

``` rs 
fn get(&self, index: usize) -> Option<&T>
```

returns an `Option` defined like:

``` rs
pub enum Option<T> {
    None,
    Some(T),
}
```
`None` and `Some` are _variants_ of the enum