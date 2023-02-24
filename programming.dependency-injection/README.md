```py
from turtle import Turtle

def draw_square(turtle, size):
    for i in range(0, 4):
        turtle.forward(size)
        turtle.left(90)

turtle = Turtle()
draw_square(turtle, 100)
```

dependency injection. It just means that if a function needs some kind of object to do its work, like `draw_square` needs a `Turtle`, the caller is responsible for passing that object in as a parameter.