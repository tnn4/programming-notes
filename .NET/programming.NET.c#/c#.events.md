# C# Events 

* Events allow classes to notify others when something specific occurs. Very common in GUI-based applications, where allowing buttons to send events allow class to be notified and handle the event
* Events rely on delegates to work. You need to have an understanding of delegates.
* 

```cs
```


`public event EventHandler PointChanged`

* `EventHandler`, is the name of the delegate event handlers must use,
* `PointChanged` is the name of the event

You raise events by first checking that there are event handlers attached, then raise the event:
```
if(PointChanged != null){ PointChanged(this, EventArgs.Empty); }
```
* To attach a method to an event, you use `+=` operator: `PointChanged += PointChangedHandler`
* To detach a method to an event, you use `-=` operator: `PointChanged -= PointChangedHandler`

Define event handler method whose signature matches delegate signature
- method signature = delegate signature 
```cs
void HandleCustomEvent(object sender, CustomEventArgs a){

}
```
=
```cs
public delegate void EventHandler(object? sender, EventArgs e);
```

Use the addition operator to attach the event handler to the event

```
publisher.RaiseCustomEvent += HandleCustomeEvent;
```

See Also:

delegates: reference to method