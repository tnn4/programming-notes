Design Principle: loose coupling

loose coupling

corollary of principle of least privilege
example

    object a b c
    a calls b and should know nothing about b's internal structure
    if c is inside b, a should know nothing about c
    the mistake is: you could write a to call c(inside b) which would introduce coupling and harder debugging

implementation:

    the law can be stated simply as "use only one dot". That is, the code a.m().n() breaks the law where a.m() does not

Tradeoffs

pros:

    more maintainable code

cons:

    more verbose code, requires more wrapper methods for call propagation to components

etymology:

    Demeter is the greek goddess of agriculture(growth)
    Demeter-style software development is about growing systems incrementally instead of monolithically building software

https://en.wikipedia.org/wiki/Law_of_Demeter

tags: design principles, information hiding, least privilege, loose coupling,