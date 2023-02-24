https://hirrolot.github.io/posts/rust-is-hard-or-the-misery-of-mainstream-programming.html

Hi @Hirrolot nice to talk to you here too! Cool post by the way. 😉

What I wrote is not an analysis it's somewhere between a rant and a personal conclusions. For the most part I'm just stating obvious and (relatively) widely known.

But what are we discussing here exactly? You stated the need for "an adequate high-level language with decent performance" and of course we have such languages, yes with perfectly adequate performance and development effort otherwise pretty much nothing around us would work! 😄 For sure we have way too many free services to whine about costs too high and everything. 😃

I think what we really need or at least want are applications with adequate performance. At least Jonathan Blow and Casey Muratory rant about that a lot. And I agree a lot.

The catch is — as I already mentioned — no programming language guarantee adequate performance to your application! Do we have huge bloated and slow C++ applications? I bet you're using at least one right now. Do we have surprisingly fast and responsive JavaScript applications? I can find a bunch of 3D games.

What conclusion can we make? Application performance mostly depend on the architecture and design, which stem from developer knowledge and experience (also dedication and time), not the programming language. Thus it's mostly an educational issue, not a technical one. As long as majority of employed programmers graduate from 6-months "get into IT quick" programs no change in programming languages' popularity will change the applications' performance distribution.

Contrary to the popular belief adequate on average performance of majority of (Web-)applications is a great testament to the amount of ingenious engineering going into JVM, CLR and alike and the evidence of their stellar efficiency which allows developers to deliver reasonable solutions without any regard to "systems" levels.

Again to me Rust's good track of efficient applications and libraries (so far) is a social thing. Rust attracts people who care about performance (and correctness) more than about their comfort (and "productivity"). Those who don't care just don't use Rust. (Many of those who do care still don't use Rust, as I mentioned too one can write very performant code in pretty much any language.)

So what do we get as a bottom line? If you personally want a "high level yet performant" language (for personal projects) you have quite a number of options: D and Nim on imperative OOP side (as long as Rust, Zig, Go are a bit too low-level); Haskell and OCaml on the FP side (and more advanced type systems). And these are pretty "mainstream" (at least production-ready) ones, if you're willing to venture into more "experimental land" you can find many more interesting languages (say, Koka).

And nothing we discuss and decide here among ourselves can affect the "grand scheme of things" in the "industrial mainstream" in a slightest! 😂
