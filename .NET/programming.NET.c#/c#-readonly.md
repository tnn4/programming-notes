https://www.reddit.com/r/csharp/comments/wqxt70/comment/ikrn83r/?utm_source=share&utm_medium=web2x&context=3

Yes because they all have different semantics and implication.

    const: value must exist at compile time. It will never change.

    readonly: value cannot be changed from anywhere, including the owner of that value (the class instance for example). Reflection can cheat though but it might break some caching optimization.

    init: compiler sugar. From the runtime point of view the value is mutable but the compiler ensures it is only written to once.

    property with just get: the value is only readonly from the perspective of a consumer of the property but the owner can still change it. It could also have behind a computational method that does give a different value each time.

    https://www.reddit.com/r/csharp/comments/wqxt70/comment/ikrn83r/?utm_source=share&utm_medium=web2x&context=3