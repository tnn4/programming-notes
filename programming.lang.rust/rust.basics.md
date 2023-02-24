
Variables
    
variables are immutable by default

```rust
let x = 1; // x immutable
```


mut = mutable = value can change

{
    Constants can never be mut. Can never be a value that can only be computed at runtime.
    i.e. constants must be valid at compile-time
}

{
    Shadowing
    declare a new variable with the same name
    why is it useful? it spares you from having to think up a different name
```rust
    let x = 5; // x -> 5
    let x = x + 1; // x -> 6
```
}

{
    Ownership

    value:owner = 1:1

    one value may have one owner

    when owner exits scope -> drop value
}

# Static Lists
tuples cannot grow, can store different types

arrays cannot grow

# Statements vs Expressions

statements do not return value

statements = no return

expressions evaluate to a resulting value

in Rust, let x = 6 does not return a value, unlike C or Ruby

calling a function is an expressions
calling a macro is an expressions
new scope created with curly brackets is expression

```rust
let y = {
    let x = 3;
    x + 1
}
```

Note that expressions do not include ending semicolons(;)
adding one will turn it into a statement

Functions with Return value
functions can return values to code that call them

```rust
fn five() -> i32{
    5
}

fn main(){
    let x = five(); // call five and it will pass a value to x
}
```

if / control flow

if this condition is met run this block of code, if not don't run this block of code

# Loops

```rust
loop { 
    println!("again!");
}
```
break - escape the loop
continue - skip over remaining code in loop


## return values from loops
assigning a loop to a variable is valid

fn main() {
    let mut counter = 0;

    let result = loop {
        counter += 1;

        if counter == 10 {
            break counter * 2;
        }
    }
}

Loops can have labels

Rust has syntactic sugar for evaluating conditions while in a loop

```rust
let mut number = 3;
loop {
    if number != 0 {
        println!("{number}!}")
        number -= 1;
    }
    else {
        break;
    }
}
```

is same as

```rust
let mut number = 3;

while number != 0 {
    println!("{number}!})
    number -= 1;
}
```

## Rust Copying

Rust will never copy by default

```rust
s1 = string::from("hello");
s2 = s1; // s1 reference is now dropped
```

s2 is now the only owner of the data which mean memory cleanup happens once which is the default behavior

Can you deep copy in Rust, if so how?
You can deep copy. It must be called with clone.

```python
let s1 = STring::from("hello");
let s2 = s1.clone(); // copying from/to the heap can be an expensive situation
```

Reference Rules

1 mutable reference xor any number of immutable references

Raw string literal
r#""#