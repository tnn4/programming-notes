F#
- `if` is functional
- `if` is an expression and returns a result

C#
- `if` is imperative
- `if` is a statement and returns nothing
- NOTE: the ternary expressions in C# allow expression-based conditionals


``` cs
string GetWeatherDisplay(double tempInCelsius) => tempInCelsius < 20.0 ? "Cold." : "Perfect!";
```

- in functional programming, it is rare to mutate values with statements

### Impurity 
Impurity in functional programming is to be avoided:

this function depends on global, mutable state
- avoid this
``` fs
let mutable value = 1

let addOneToValue x = x + value
```

This function performs a side effect (writing to console)
- A side effect is any statement that has nothing to do with transforming the input
``` fs
let addOneToValue x =
    printfn $"x is %d{x}"
    x + 1

```
- Although this function does not depend on global value, it write the value of `x` to the console
- Side effects should be avoided because they may create unforeseen bugs
- For example,if another program depends on something external, such as the output buffer, calling this function that other part of your program

How do you solve?
- remove the printfn

``` fs
let addOneToValue x = x + 1
```

Lesson: isolatint impurity helps with debugging
- this has the beneficial corollary of keeping your functions smaller, more readable and more likely reusable

Immutability
- F# uses immutability by default
- "I need to change something" -> "I need to produce a new value"

``` fs
let value = 1
let secondValue = value + 1 // this produces a new value
value = value + 1 // This performs an equality check, Produces a 'bool' value!
```