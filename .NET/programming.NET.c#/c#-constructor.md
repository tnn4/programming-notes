A constructor is a method whose name is the same as the name of its type.

Constructors return the type being created.

They are invoked with the new operator.

The new operator creates a new instance of a type.

``` cs
public class Taxi
{
    public bool IsInitialized;

    public Taxi() // same name as its type
    {
        IsInitialized = true;
    }
}

class TestTaxi
{
    static void Main()
    {
        Taxi t = new Taxi(); // constructor invoked with new
        Console.WriteLine(t.IsInitialized);
    }
}
```

Sources:

[new](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/new-operator)

[constructors](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/constructors)