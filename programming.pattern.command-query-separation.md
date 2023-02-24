minimizng side effects in OOP

a method should be a _command_ that performs an action or _query_ that returns data to caller, but not both 

i.e. ( method = action XOR query )

_asking a question should not change the answer_

methods that mutate state do not return values

formal, method should return value only if they are referentially transparent / no side effects



https://en.wikipedia.org/wiki/Command%E2%80%93query_separation

https://stackoverflow.com/questions/1188222/what-are-the-best-resources-for-learning-how-to-avoid-side-effects-and-state-in