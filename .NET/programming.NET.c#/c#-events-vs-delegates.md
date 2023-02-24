https://docs.microsoft.com/en-us/dotnet/csharp/distinguish-delegates-events

Are there attached subscribers?

If your code must call code on the subscriber:
    you should use delegates when implementing callbacks.

If your code can complete all work without calling subscribers:
    use events.


Examples:

### Delegates
`List.Sort()` must be given a comparer function to properly sort elements.

LINQ queries requires delegates to determine elements to return

Both use delegate design.

### Event
`Progress` event reports progress on a task.

The task proceeds regardless of any listeners.


## Events have private invocation

Foreign classes can only add or remove event listeners.
Only the class containing the event can invoke it.

OTOH, delegates are often passed as parameters, can be stored as private class members.

Can't decide?
Prototype both. They can do 