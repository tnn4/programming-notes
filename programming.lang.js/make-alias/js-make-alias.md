Make alias:

``` js
var $ = document.getElementById.bind( document );
```

ECMAScript 5 introduces the bind() function that binds a function with an object so that it can be called directly without having to use func.call(thisObj) for each call.