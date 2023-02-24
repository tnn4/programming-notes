{https://www.reddit.com/r/csharp/comments/t55oyl/comment/hz3eb79/?utm_source=share&utm_medium=web2x&context=3

c-digs
·
6 mo. ago
· edited 6 mo. ago
GoldHelpful

C# has a lot of functional paradigms in it (in some areas, better than JS like with pattern matching).

I think if you are already familiar with idiomatic TypeScript (i.e. not just using it for intellisense and compile time type checking), you are going to have an easy transition into C#.

C# over the years and .NET has "converged" to JavaScript/TypeScript. C# had arrow functions in 2007 (lambdas) before JavaScript in 2015 and adopted var with type inference (obviously not the same as in JS where var is fully dynamic, but syntactically identical).

C# in general has moved more and more towards type inference over explicit typing and will likely have discriminated unions in the near future (since F#, the sister language already has it). This has cut down on a lot of the verbosity and there is a strong resemblance to JS/TS now.

C# also has dynamic types (equivalent of var x = {}) in the ExpandoObject so it's possible to use some dynamic techniques. I recently used it with the Jint library to build a rules engine.

Like JavaScript, functions in C# are first class objects via Func and Action. So you can pass/return functions just as you would in JS/TypeScript.

C# lambdas do behave a bit differently from JavaScript lambdas (arrow functions). Be aware of this (I have never been burned by C# closures but I have been by JS closures):

This:

// JS
class Test {
    doSomething() {
        let iterations = 0;
    
        [0,1,2,3,4,5].forEach(async (i) => {
            const value = await Promise.resolve(i)
            console.log(value)
            iterations++
        })
    
        console.log(`How many iterations? ${iterations}`)  // 0
    }
}

const test = new Test();    
test.doSomething();

Does not behave like this:

// JS
class Test {
    async doSomething() {
        let iterations = 0;
   
        for(const i of [0,1,2,3,4,5]) {
            const value = await Promise.resolve(i)
            console.log(value)
            iterations++
        }
  
        console.log(`How many iterations? ${iterations}`) // 6
    }
}

const test = new Test();   
await test.doSomething()

Which behaves like this:

// C#
class Test {
    public void DoSomething() {
        var iterations = 0;
		
        new [] {0,1,3,4,5}.ToList().ForEach(async (i) => {
            var value = await Task.FromResult(i);
            Console.WriteLine(value);
            iterations++;
        });
		
        Console.WriteLine($"How many iterations? {iterations}"); // 6
    }
}

var test = new Test();		
test.DoSomething();

The async/await syntax is also largely identical with the exception of Task vs Promise.

C# try-catch-finally exception handling is almost identical to JS but is a bit more sophisticated since you can catch and handle specific types of exceptions (multiple catch() statements) whereas JS can only catch an exception and then check the type.

The two languages are so similar that when teams consider TypeScript on the backend (especially Nest.js), I recommend considering .NET Web API because the lift for most JavaScript developers to something like Nest.js with what I consider idiomatic TypeScript is pretty much 80% of the way to C#/.NET without all of the performance, runtime, and language benefits.

I make the case here that startups considering TypeScript on Node should really consider .NET to save a lot of the headaches with working with Node (package dependency explosion, security, package churn, build times for large TS projects)

What you see happening with JavaScript and TypeScript and C# is that they are converging. JavaScript is in the late stages of implementing attributes, for example (though there is some nuanced difference with C# attributes). We'll probably see pattern matching in JS in the future. TypeScript of course adds strong compile time type checks and generics in the same style as C# (TypeScript was designed by the same guy that designed C#). C# is adopting more and more functional elements like discards and deconstructing; it will likely have discriminated unions at some point.

I think that overall, .NET 5/6 is a huge turning point (that started with .NET Core 2/3) for .NET and we'll see an uptick and we'll see more backend adoption of .NET. It addresses many issues that have plagued .NET's uptake for years.

Career wise, you'll find .NET used heavily in a enterprise workloads. Industries that tend to have .NET:

    Financial and banks. Backends in C#, front-ends in WPF and increasingly Blazor. Morgan Stanley, Blackrock, Fidelity, Barclays, Susquehanna, lots of broker-dealers have/are switching from Java to C#. WPF is used heavily in desktop trading applications.

    More mature internet tech companies. Match backend has C#, Grubhub, others. Once you need high throughput at scale, you'll be better off with C# (or Java, Rust, Go); Node and Python are a fraction of the throughput for web scale workloads but have advantages in terms of cold start. In fact, if you look at the job postings for Amazon, for example, their platform engineering all require knowledge of "Java, C++, C#, or OOP" in general (Google tends to skew toward Go).

    Insurance and healthcare. A lot of C# presence in this space

    Defense and industrials. Because of the more secure/stable runtime

Startups skew towards JavaScript because it's easier to hire a dev that knows one language for front- and back-end and have a full-stack developer than to find a developer that is polyglot and can write the back-end in a different language than the front-end when there are plenty of good reasons to avoid Node on the server. But there is an endless stream of bootcamp developers who know JS and are "full-stack" that can be had.

The problem is that when all you have is a hammer (JavaScript), every problem looks like a nail. Even Ryan Dahl, the creator of Node, called this out:

    I want programming computers to be like coloring with crayons and playing with duplo blocks. If my job was keeping Twitter up, of course I'd using a robust technology like the JVM.

    Node's problem is that some of its users want to use it for everything? So what? I have no interest in educating people to be well-rounded pragmatic server engineers, that's Tim O'Reilly's job (or maybe it's your job?). I just want to make computers suck less. Node has a large number of newbie programmers. I'm proud of that; I want to make things that lots of people use.

If JS and Node is like Lego Duplo, then TypeScript is like Regular Lego, and C# is like Lego Technic. You'll be able to build much more sophisticated structures with Technic, but it's still fundamentally Lego-like; you can see the clear progression and lineage from Duplo to Lego to Technic.

I wrote an article recently here: https://blog.devgenius.io/6-net-myths-dispelled-celebrating-21-years-of-net-652795c2ea27
}

{
    https://www.reddit.com/r/Kotlin/comments/upwwbg/comment/i8o9zt5/?utm_source=share&utm_medium=web2x&context=3

    What I don't like as much of C# it's that the experience is generally worse on non-Windows systems. No Visual Studio on Linux e.g.. Idk how well VSCode compares, and well there is Rider from JetBrains, but I don't love either

    I'd be curious to try again C#, but I've learned to appreciate enough the JVM ecosystem, besides Kotlin has imho a nicer syntax, and several interesting features
}