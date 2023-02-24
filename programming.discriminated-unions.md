Discriminated unions force correctness at compile-time.

Let's look at some OneOf code
First off, OneOf brings exhaustive pattern matching with `Match` and `Switch`. 
Meaning that you must explicitly declare all outcomes or else it won't compile. 
Compare to the built-in switch which lets you compile and forget that you have unmanaged cases.

```fs
OneOf<Yes, No, Maybe> union ... ;// Use Switch when you don't want to return anything
union.Switch(
    yes => Console.WriteLine("yes"),
    no => Console.WriteLine("no"),
    maybe => Console.WriteLine("maybe"));// Use Match to return a value
string response = union.Match(
   yes => "yes",
   no => "no",
   maybe => "maybe");
```