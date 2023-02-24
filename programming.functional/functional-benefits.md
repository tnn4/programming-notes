{https://www.quora.com/Is-functional-programming-suitable-for-game-development?share=1
Tikhon Jelvis
studied programming languages and did research on program synthesisAuthor has 1.8K answers and 14.5M answer views2y
Related
What would be the benefits of functional programming in the context of video game programming?

What are the benefits of functional programming for video games?

I’ll try to answer—but remember that I know a lot more about functional programming than I do about video games!

Ultimately, the benefits you would get from functional programming in video games aren’t too different from what you’d get in other applications. By making state management explicit, you can prevent whole classes of bugs involving mutation, which is especially important in a multithreaded context. Your functional code will be easier to maintain and debug. (I know this is a controversial statement! I’m pretty biased. ”Maintainability” is famously hard to measure so everybody goes by their own experiences; my experience is that the same logic in a functional style will be substantially easier to test, fix and extend over time.)

But would you get any benefits more specific to video games?

I think so. One aspect of video game programming that really stands out is managing time. Everything in your game runs on some internal clock and your logic has to be correct with respect to game time. (This is also true of simulations and, while I’ve never worked on a serious game project, I have spent several years working on supply chain simulations at Target.)

Functional programming makes managing time easier.

The key idea is that immutable data structures let you abstract over time in a way that is much harder otherwise.

In a mutable context, we only have one direct way to model time: the state of our mutable structures represents the state of our system at the current game time and we advance time by mutating the state. At any given point, we can only do two things:

    Inspect our state at the current game time.
    Change the state, implicitly advancing time.

This approach is limited and error-prone.

One problem is that we’re not just using mutable state for modeling game time, we’re also using it to implement our data structures and control flow. But how do you tell which is which? How do you tell that one kind of in-place update represents advancing the game state but another is an implementation detail of our data structures? How do you make sure that other parts of the code can track the game state over time but never see “partial” updates that temporarily violate invariants? How do you ensure that every part of your mutable game state update consistently?

I’ve seen a massive number of bugs—some small, some game-breaking—that come down to parts of the game state not updating when they should. You have multiple components that semantically reflect the same element in the game, each component has its own mutable state, and it doesn’t take much for them to get out of sync. Then you get anything from silly visual glitches to broken mechanics like invisible, unbreakable traps.

An invisible trap bug I found on the Rainbow Six subreddit—I would be willing to bet it’s an issue with a mutable update being interrupted in the middle.

Another problem is that we can only do two things at any given time:

    See the current state of the game.
    Update the state of the game, implicitly moving time forwards.

That “implicitly” is scary on its own. We have some kind of game clock and game actions have durations with respect to this clock, but that isn’t reflected directly in our mutable state. The game clock is (or should be¹) separate from the CPU time it takes to make a change to the state, so we need to correlate how we change the state in place with how the game clock is advancing.

But what if we want to do something more complicated? Slow down time? Speed it up? Gracefully interpolate over ragged framerates? Let players undo actions? Let the game consider several possible futures? Implement game logic that depends on history? All of these are at odds with the core abstraction of “mutable state = game state”. We can build abstractions to make all of these manageable—although you run into all the difficulties I mentioned earlier like distinguishing “game updates” from implementation details—but at that point you’ve added quite a bit more complexity than just “mutable state = game state” and it’s easy to accidentally have pockets of mutable state that exist outside these abstractions and inevitably get out of sync.

So how does functional programming help?

The most important part is that it makes changes in our state explicit. We don’t update our state by changing some shared mutable object in place; instead, we have functions from the old state to the new state. Do you want to compare the state before and after an action? Keep references to both versions around. Want to checkpoint states at certain points? Just save the value at that point.

Are you using mutable state in the middle of an operation for performance reasons? There’s no way to leak that out by accident. Code can only interact with the final state object that you return.

We still need to build some kind of abstraction for managing game time. What does “now” mean in the game? How do we handle actions that have durations or actions that happen simultaneously? In my experience with simulation code, building these abstractions in a functional style is only somewhat easier than in imperative style but using them correctly is far easier. The functional style forces us to thread our state through the code explicitly; we can’t have silent interactions from distant parts of the codebase that happen to modify the same part of the game state.

The downside, of course, is performance. For games pushing the absolute edge of performance it’s simply too slow. For other applications, the story is a bit more nuanced. Functional code in today’s languages comes with a particular performance profile:

    Functional code allocates. A lot. You will allocate a massive amount of small, short-lived objects on the heap.
    You need garbage collection. This makes the allocation side of things easier—we can tune modern garbage collectors to make allocation incredibly cheap—but it makes the performance of your code less consistent.

It takes a certain expertise but you can write surprisingly fast functional code, especially if you configure your runtime (GC, heap size… etc) in a way that works for your specific usage patterns.

You also don’t have to write everything in a functional style to get these benefits. I worked on a simulation project (with versions in both Haskell and Rust) where most of the domain code was purely functional but the core state was a big mutable array full of these immutable domain-specific objects. By keeping all the mutation centralized in one place, we managed to get sufficient runtime and memory performance without running into the issues I covered earlier. The key correctness challenge in this project was modeling complicated business processes—not too different from modeling complicated game rules!

This worked well because we followed a few concrete design principles:

    Keep mutable state limited and simple.
    Carefully control which parts of the code can modify the state.
    Distinguish between read-only and read-write state access.
    Never have multiple mutable objects for the same logical entity.

With Rust in particular, the “ownership” model also really helped keep our code correct. Language-level support for ensuring only one part of the code can change the state at one time goes a long way towards giving you the benefits of a functional style while using mutable memory under the hood. I’m excited to see whether linear types

in Haskell will let us do something similar.

If I end up working on another simulation or gaming project in the future, I will absolutely start with the logic in a functional or mostly functional style and only move away from that to the extent that performance requirements force me to.

footnotes

¹ If you don’t separate game time and execution time, you’ll end up with silly behavior like players running through the game world faster if they render the game at a higher FPS
—something that actually happened with Fallout 76!
}

{
    stumpyguy
    ·
    2 yr. ago
    I used f# a lot when building games in unity. C# did all the impure front end stuff, f# provided all the calculations etc. There's a bit more boiler plate type code than I would like, especially with interfaces and the unity class MonoBehaviour, but it let me code up a lot of the fun stuff in f# very easily.
    
}