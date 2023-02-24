Remember what the purpose of asynchrony is: it is to manage high latency operations. -Eric Lippert

# (async and await)[https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/async/task-asynchronous-programming-model]

If you specify that a method is an async method by using the async modifier, you enable the following two capabilities.

    The marked async method can use await to designate suspension points. The await operator tells the compiler that the async method can't continue past that point until the awaited asynchronous process is complete. In the meantime, control returns to the caller of the async method.

    The suspension of an async method at an await expression doesn't constitute an exit from the method, and finally blocks don't run.

    The marked async method can itself be awaited by methods that call it.

An async method typically contains one or more occurrences of an await operator, but the absence of await expressions doesn't cause a compiler error. If an async method doesn't use an await operator to mark a suspension point, the method executes as a synchronous method does, despite the async modifier. The compiler issues a warning for such methods.

[How is async/await implemented?](https://learn.microsoft.com/en-us/dotnet/csharp/async#what-happens-under-the-covers)
Compiler transforms code into state machines.

Example of state machines:
![async-await-example-0](StateMachine-00.png)

``` c#
public static async Task<int> MyAsyncMethod(int firstDelay, int secondDelay)
{
    Console.WriteLine("Before first await.");
    
    await Task.Delay(firstDelay);
    
    Console.WriteLine("Before second await.");
    
    await Task.Delay(secondDelay);
    
    Console.WriteLine("Done.");
    return 42;
}
```
![async-await-example-0](StateMachineConceptually_State0.webp)

[stop sign state machine](https://www.google.com/imgres?imgurl=https%3A%2F%2Fcdn.vhdlwhiz.com%2Fwp-content%2Fuploads%2F2016%2F11%2Fintersection_fsm.gif&imgrefurl=https%3A%2F%2Fvhdlwhiz.com%2Ffinite-state-machine%2F&tbnid=LkoboE5hL21V5M&vet=12ahUKEwi6l9yZptn8AhUg0MkDHeDGC_MQMygCegUIARDKAQ..i&docid=I8Q2M0x69reuOM&w=748&h=308&q=finite%20state%20machine%20gif&client=firefox-b-1-d&ved=2ahUKEwi6l9yZptn8AhUg0MkDHeDGC_MQMygCegUIARDKAQ)

[skittles-sorter-1]()

Markov Chain vs FSM
While the finite-state machine is deterministic in nature, the Markov chain requires a distribution of probabilities to model the transition between states. In the limit case, where the transition from any state to the next is defined by a probability of 1, a Markov chain corresponds to a finite-state machine. [src](https://www.baeldung.com/cs/markov-chain-vs-finite-state-machine)

Whilst a Markov chain is a finite state machine, it is distinguished by its transitions being stochastic, i.e. random, and described by probabilities.