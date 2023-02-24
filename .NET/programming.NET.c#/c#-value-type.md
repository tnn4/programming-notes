Value Types

    structs
    enums

    Built-in

    integral numeric
    floating point
    bool
    char

`T?` : nullable value type = T + null

Performance Considerations

To make your code less error-prone and more robust, define and use immutable value types.

Boxing: creating a new object from a value type.

Boxing/Unboxing is expensive: avoid doing it in code that runs often like in long-running loops.
Boxing can be up to 20x longer than simple reference assignments.
Unboxing 4x.

You can avoid boxing by using generic collections like `System.Collections.Generic.List<T>`