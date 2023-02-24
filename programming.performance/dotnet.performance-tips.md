Problem: passing big structs by value causes copy and performance hits

When you pass a structure-type variable to a method as an argument or return a structure-type value from a method, the whole instance of a structure type is copied. 

Pass by value can affect the performance of your code in high-performance scenarios that involve large structure types.

Solution:

You can avoid value copying by passing a structure-type variable by reference. 

Use the ref, out, or in method parameter modifiers to indicate that an argument must be passed by reference.