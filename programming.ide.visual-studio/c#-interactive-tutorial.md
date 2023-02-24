visual studio has a built in c# repl

how to use it:
import a assembly(dll) you want to use with r#

r# "path/to/assembly"

now you can import libraries

e.g.

``` cs
#r "D:\projects\game-dev\monogame\test-game-1\test-game-1\bin\Debug\net6.0\MonoGame.Framework.dll"
using Microsoft.Xna.Framework;
using Microsoft.Xna.Framework.Graphics;
using Microsoft.Xna.Framework.Input;
```
Quit:


```
Environment.Exit(0);
```