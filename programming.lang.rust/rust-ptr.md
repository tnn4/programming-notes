# Rust Pointers
```
fn main() {
    let x = 5;
    let y = &x; // let y = ->(x) // ptr_to_(x) // ref(x)
    // y is a pointer to x
    // * means follow the pointer / deref
    
    assert_eq!(5, x);
    assert_eq!(5, *y);
    assert_eq!(5, y) // ERROR, note that y is a pointer and not an int : type mismatch
}
```


You can use deref on Box<T> the same way as you can regular pointers!
Listing 15-9
```

fn main() {
    let x = 5;
    let y = Box::new(x); // here we set y to be an instance of a box 
                         // pointing to a copied value of x 
                         // rather than a reference pointing to the value of x

    assert_eq!(5, x);
    assert_eq!(5, *y); // <-- y  is boxed
                       // *y = *(y.deref())
}

```
When we entered *y in Listing 15-9, behind the scenes Rust actually ran this code:

`*(y.deref())`


Turn a type into a Reference by Implementing Deref
```
use std::ops::Deref;

impl<T> Deref for MyBox<T> {
    type Target = T;

    fn deref(&self) -> &Self::Target {
        &self.0 // .0 accesses the first value in a tuple struct, 
                /
    }
}
// https://doc.rust-lang.org/book/ch05-01-defining-structs.html#using-tuple-structs-without-named-fields-to-create-different-types
```