A rust box is a pointer. The pointer is stored on the stack but the data is allocated on the heap.

Written as `Box<T>`.

Boxes are pointers stored on the stack.

The Box points to data on the heap.


When to use:

Don't know compile time size but work in context that requres exact size
- When you have a type whose size can’t be known at compile time and you want to use a value of that type in a context that requires an exact size

Transfer ownership with no copying
- When you have a large amount of data and you want to transfer ownership but ensure the data won’t be copied when you do so

Only care the about the trait
- When you want to own a value and you care only that it’s a type that implements a particular trait rather than being of a specific type


``` 
enum List {
    Cons(i32, List),
    Nil,
}
```
VS
``` 
enum List {
    Cons(i32, Box<List>), // Note that the list is being pointed at now instead of a direct object
    Nil,
}
```