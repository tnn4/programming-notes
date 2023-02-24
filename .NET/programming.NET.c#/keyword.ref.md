Why use ref?

I know. out (and ref as well) is also really useful if you do not wish your method do instantiate a new object to return. This is very relevant in high-performance systems where you want to achieve sub microsecond performance for your method. instantiating is relatively expensive seen from a memory access perspective. [src](https://stackoverflow.com/a/33026024)

How does ref work?
The ref keyword makes the formal parameter an alias for the argument, which must be a variable. In other words, any operation on the parameter is made on the argument.

```
void Method(ref int refArgument)
{
    refArgument = refArgument + 44;
}

int number = 1;
Method(ref number);
Console.WriteLine(number);
// Output: 45

```

[csharp lang reference: keyword ref](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/ref)