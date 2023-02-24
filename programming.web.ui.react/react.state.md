Why does React need state?
- local variables do not persist between renders
- changes to local variables do not trigger renders
- result? nothing happens

To update a component, what do you need?
1. Retain the data between renders
2. Trigger React re-render(render component with new data)

How do you implement this?
You need the `useState` Hook.
``` js
import {useState} from 'react';
```
``` js
const [state_variable, setter_function] = useState(0);
const [stateVariable, setStateVariable] = useState(0);
const [x, setX] = useState(true);
```
``` js
const [index, setIndex] = useState(0)
```
```js
function handleClick(){
    setIndex(index + 1);
}
```

```js
<button onClick={handleClick}>
    Next
</button>
```

when you call `useState` you are telling React you need to remember something
```
const [index, setIndex] = useState(0);
```
the only argument to useState is initial value of state variable

Step-by-step useState
``` js
[0, setIndex] = useState(0);
click button -> render
[1, setIndex] = useState(0);
click button -> render
[2, setIndex] = useState(0);
...
so on
```

You can give a component multiple state variables
```

```

See Also:

Hook: Hooks(React) are special functions that are only available while React is rendering
- they begin with `use`
- they are limited, cannot be used in conditions, loops, or other nested functions

```

```