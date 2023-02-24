What is a handler ond handle?

{
A handle (like the handle on a broom or a screwdriver) is a convenient way to hold some more complex object.

So, for example, in graphics - we might load some image, give it a bunch of complicated properties - then hand it over to the graphics system to manage. In return, the graphics system gives us a “handle” that corresponds to that image - which is probably either a pointer or some simple integer - which we can use to talk about that image in the future.

This is very convenient when a library takes control of an object - and you don’t want the original creator to be able to do anything to the object without going through the libraries’ official interface.

Handles are said to be “opaque objects” - you have no idea what’s inside them or anything at all about them - except that they exist, you can copy them freely - and you can pass them into that library.

Handles are almost always very small objects.

A handler (like a baggage handler at an airport) - is a piece of software that performs some service for you. So you might talk about a “File handler” - which does all of the grunt work of dealing with files on disk.

It is not uncommon for a handler to give you a handle - but the two terms are NOT related in any special way - it just happens that it’s quite common for handlers to do that.

To take the simplest example - the C language standard library.

When you call “fopen” to open a file - it gives you back a “FILE*” - which is a handle. You can’t do anything with the FILE* object it gave you - there is no useful data inside the object that it points to that you can safely use. In fact, it might not actually point to anything valid at all.

But when you want to read from the file (using ‘fread’, for example) - you present that function with the handle to your file - and it knows what to do with it. When you’re done with the file, you pass the handle to “fclose” and from that point onwards, your handle is useless.

In that case, the “FILE*” is a handle and the standard I/O library is the “handler”.
-Steve Baker, https://www.quora.com/In-programming-what-is-the-difference-between-a-handle-and-a-handler }