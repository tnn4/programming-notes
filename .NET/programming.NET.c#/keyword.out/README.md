- the `out` parameter causes arguments to be passed by reference
- `out` is like `ref` but `ref` requires variables to be initialized before it is passed
- it is like `in` but `in` does not allow the called method to modify the argument value
- to use `out` parameter, both the method definition and calling method must explicitly use the `out` keyword
``` cs
int initializedInMethod;
OutArgExample(out initializeInMethod);
Console.WriteLine(initializedInMethod); // value is now 44

void OutArgExample (out int number){

}
```

Why is `out` useful: it stops the caller from having to declare the variable separately
```cs
int foo;
GetValue(out foo);
```
vs

```cs
int foo = GetValue();
```