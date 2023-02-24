https://doc.rust-lang.org/book/ch13-01-closures.html

Rust closures are anonymous functions that you can save in variables, or
pass as arguments to other functions. 

You can create a closure in one place and then call the closure to evaluate it in a different context.

Closures can capture the values from the scope they are defined.

Which one are closure and which ones are function definitions?

``` rs
fn  add_one_v1   (x: u32) -> u32 { x + 1 }
let add_one_v2 = |x: u32| -> u32 { x + 1 };
let add_one_v3 = |x|             { x + 1 };
let add_one_v4 = |x|               x + 1  ;
```



``` rs
#[derive(Debug, PartialEq, Copy, Clone)]
enum ShirtColor {
    Red,
    Blue,
}

struct Inventory {
    shirts: Vec<ShirtColor>,
}

impl Inventory {
    fn giveaway(&self, user_preference: Option<ShirtColor>) -> ShirtColor {
        user_preference.unwrap_or_else(|| self.most_stocked()) // <-- closure defined here
        // The closure captures an immutable reference to the self Inventory instance 
        // and passes it with the code we specified to the unwrap_or_else method.
    }

    fn most_stocked(&self) -> ShirtColor {
        let mut num_red = 0;
        let mut num_blue = 0;

        for color in &self.shirts {
            match color {
                ShirtColor::Red => num_red += 1,
                ShirtColor::Blue => num_blue += 1,
            }
        }
        if num_red > num_blue {
            ShirtColor::Red
        } else {
            ShirtColor::Blue
        }
    }
}

fn main() {
    let store = Inventory {
        shirts: vec![ShirtColor::Blue, ShirtColor::Red, ShirtColor::Blue],
    };

    let user_pref1 = Some(ShirtColor::Red);
    let giveaway1 = store.giveaway(user_pref1); //<-- closure called here
    // This is interesting because we’ve passed a closure that calls self.most_stocked() on the current Inventory instance.

    // The closure captured an immutable reference to the self Inventory instance and passed it with the code we specified to the unwrap_or_else method.

    // functions cannot capture their environment like this

    println!(
        "The user with preference {:?} gets {:?}",
        user_pref1, giveaway1
    );

    let user_pref2 = None;
    let giveaway2 = store.giveaway(user_pref2);
    println!(
        "The user with preference {:?} gets {:?}",
        user_pref2, giveaway2
    );
}

```


``` rs

let example_closure = |x| x; // toy closure returns valus it received as a parameter 
```

This example also illustrates that a variable can bind to a closure definition, and the closure can later be called by using the variable name and parentheses as if the variable name were a function name:

``` rs 
fn main() {
    let list = vec![1, 2, 3];
    println!("Before defining closure: {:?}", list);

    let only_borrows = || println!("From closure: {:?}", list);

    println!("Before calling closure: {:?}", list);
    only_borrows(); // the variable name is called !!!
    println!("After calling closure: {:?}", list);
}
```