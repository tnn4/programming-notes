String.Split is going to create an array of strings, which means one new string object for every keyword originally in your keywords string plus one more object for the array.[1]

This can be potentially costly if you're splitting huge strings.

[1. Garbage Collector Basics](https://docs.microsoft.com/en-us/previous-versions/dotnet/articles/ms973837(v=msdn.10))