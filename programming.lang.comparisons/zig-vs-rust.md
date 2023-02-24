https://www.reddit.com/r/Zig/comments/srk7ws/comment/hwt9aj4/?utm_source=share&utm_medium=web2x&context=3

pron98
·
7 mo. ago
· edited 6 mo. ago

It's often a matter of personal taste. Rust is far too complex and is way too implicit for my taste. It also follows in C++'s footsteps of aiming to make low-level code look like high-level code (of course, without actually making it as easy to maintain), which, in my personal view, is not the right direction for a low-level language.

As for safety, there is no doubt Rust is a safer language in the sense that the language itself prevents more bugs, but the goal isn't to use a safer language, but write more correct programs, and I am not at all certain Rust has an advantage here. While it eliminates more memory safety issues than Zig, its complexity and implicitness makes code review harder, and its slow compilation means you get to write and run fewer tests. Because testing and code reviews are known to catch many bugs, Rust might be trading off memory safety for other kinds of bugs, while Zig might let some more memory safety bugs through, but helps more with review and testing. All in all, it's really hard to say without more data which of them, if any, would result in more correct programs, i.e. programs with fewer bugs. All in all, it is almost certainly not the case that a language with more built-in safety always yields more correct programs, or we'd all be writing low-level programs in ATS. Obviously, even Rust's designers agree that not every increase in safety is worth any increase in programming complexity, they just disagree with Zig on where the sweet spot is.

Anyway, I expect it to mostly be a matter of personal preference. Some programmers would find Rust more appealing, while others would prefer Zig. So try both and see which suits your taste better.