Use F# records for data and local types. Use classes for everything else.

Also classes are better for performance (if that matters to you).


- Given that functions can be seen as values in F#, record fields can hold function values as well.
- This offers possibilities for state encapsulation

Note: unit in F# pretty much takes nothing and returns nothing
- The unit type is a type that indicates the absence of a specific value; the unit type has only a single value, which acts as a placeholder [src](https://docs.microsoft.com/en-us/dotnet/fsharp/language-reference/unit-type)

``` fs
module RecordFun =
    type CounterRecord = {
        GetState: unit -> int;
        Increment: unit -> unit;
    }

// Constructor
let makeRecord() =
    let count = ref 0 // a ref(reference cell holds an actual value; is is not just an address)
    // you use the `ref` operator before a  value to create a new reference cell that encapsulates the value
    // you can then change the underlying value because it is mutable
    {
        // the keyword: fun is used to define lambda expressions
        GetState = (fun () -> !count); // the ! (bang operator) dereferences a reference cell
        Increment = (fun () -> incr count)   
    }
```

Reference Cell