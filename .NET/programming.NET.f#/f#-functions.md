In F# all function are values, they are known as function values

Because functions are values, they can be used as arguments to other functions

Example of function that takes function value as argument

```fs
let apply1 (transform: int -> int ) y = transform y

let increment x = x+1
let result1 = apply1 increment 100


// multiple arguments are separated by successive `->` tokens
let apply2 (f: int -> int -> int) x y  = f x y

let mul x y = x*y
let result2 = apply2 mul 10 20 // --> 200
```

- `apply` is a function that takes a function `transform` as an argument
- where `transform` is a function that takes an `integer` an returns an `integer`
- You specify the type of function value by using `->`
- left side type argument, right side return value -`type argument -> return value`
