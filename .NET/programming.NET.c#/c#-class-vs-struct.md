https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/choosing-between-class-and-struct

In general, classes are fine, but if you want more performance consider these:

Use a struct if:
the type has all of the following characteristics:

    It logically represents a single value, similar to primitive types (int, double, etc.).

    It has an instance size under 16 bytes.

    It is immutable.

    It will not have to be boxed frequently.
