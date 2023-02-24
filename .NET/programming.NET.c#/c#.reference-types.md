When a reference type is passed "by reference," the method intends to use the parameter to return a different instance of the object. 

Passing a reference type by reference is also known as using a double pointer, pointer to a pointer, or double indirection. 

Using the default calling convention, which is pass "by value," a parameter that takes a reference type already receives a pointer to the object. 

The pointer, not the object to which it points, is passed by value. 

Pass by value means that the method cannot change the pointer to have it point to a new instance of the reference type, but can alter the contents of the object to which it points. For most applications this is sufficient and yields the desired behavior. [src](https://docs.microsoft.com/en-us/previous-versions/dotnet/netframework-3.0/ms182131(v=vs.80)?redirectedfrom=MSDN)