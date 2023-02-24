Rich Hickey
- Design is separating into things that can be composed.

- when you combine two pieces of data you get data, when you combine two machines you get trouble

- nobody wants to program with _mutable strings_ anymore, why do you want to program with _mutable collecctions_

- eventually with mutable objects you create an intractable mess, and encapsulation does not get rid of that. Encapsulation only means: "well I'm in charge of this mess

- Systems are dynamic and data driven. It might be a nice idea to use a language that is also dynamic and data driven.

James Trunk
- Clojure separates data from functionality
- whereas in OOP, data and functionality are encapsulated
- promote data to the syntax level of your language
- when data is syntax you can visualize data
- you can think of Clojure as JSON with super powers
- Clojure code itself is data
- Clojure collections are immutable