# Programming Rust 2nd Ed Notes


# Undefined behavior

Undefined behavior, the demons in your code.

In our case, storing this particular value in
the fourth element of this particular array happens to
corrupt the function call stack such that returning from the
main function, instead of exiting the program gracefully as
it should, jumps into the midst of code from the standard C
library for retrieving a password from a file in the user's
home directory. It doesn't go well.

Rust breaks the deadlock in a surprising way: by restricting
how your programs can use pointers. ... But the net effect of these restrictions is to bring just enough order to the chaos to allow Rust's compile-time checks to verify that your program is free of memory safety errors: dangling pointers, double frees, using uninitialized memory, and so on.

At run time, your pointers are simple addresses in memory, just as they
would be in C and C++.

Struct = "and" , X and Y
enum = "or"

# Moves and control flow
The general principle is that, if it's possible for a variable to
have had its value moved away and it hasn't definitely been
given a new value since, it's considered uninitialized.

``` rs
// Build a vector of the strings "101", "102", ... "105"
let mut v = Vec::new();
for i in 101 .. 106 {
v.push(i.to_string());
}// Pull out random elements from the vector.
let third = v[2]; // error: Cannot move out of index of Vec
let fifth = v[4]; // here too
```
You can't move elements out of a vector without replacing them.
How to access ? Use a reference: &v[2]

Collection types like Vec also generally offer methods to
consume all their elements in a loop

``` rs
let v = vec!["liberté".to_string(),
"égalité".to_string(),
"fraternité".to_string()];
for mut s in v {
    s.push('!');
    println!("{}", s);
}
```

When we pass the vector to the loop directly, as in for ...
in v, this moves the vector out of v, leaving v uninitialized.
The for loop's internal machinery takes ownership of the
vector and dissects it into its elements. At each iteration,
the loop moves another element to the variable s. Since s
now owns the string, we're able to modify it in the loop
body before printing it. And since the vector itself is no
longer visible to the code, nothing can observe it mid-loop
in some partially emptied state.

# Reference
shared vs mutable reference: *multiple readers, single writer*

Rust separates sharing a variable and modifying a variable 

If you only need to read: pass a reference

`this_is_shared(&variable_1);`
`this_gets_moved(variable_1);`

passing a variable by value(moving ownership into the function)


Iterating over a shared
reference to a HashMap is defined to produce shared
references to each entry's key and value: artist has
changed from a String to a &String, and works from a
Vec<String> to a &Vec<String>. The function just passes around non-owning references.

Reminder: references are just addresses at the machine level

## Lifetimes

Lifetimes are entirely figments of Rust's compile-time
imagination. At run time, a reference is nothing but an
address; its lifetime is part of its type and has no run-time
representation.

Here's one constraint that should seem pretty obvious: if
you have a variable x, then a reference to x must not
outlive x itself,

Beyond the point where x goes out of scope, the reference
would be a dangling pointer. We say that the 
variable's lifetime must contain or 
enclose that of the reference
borrowed from it.

If the reference can't live at least as long as the variable
does, then at some point r will be a dangling pointer. We
say that the reference's lifetime must contain or enclose
the variable's.

The first kind of constraint limits how large a reference's
lifetime can be, while the second kind limits how small it
can be. Rust simply tries to find a lifetime for each
reference that satisfies all these constraints. 

## Every type in Rust has a lifetime
It's not just references and types like S that have lifetimes.
Every type in Rust has a lifetime, including `i32` and `String`.
Most are simply `'static`, meaning that values of those
types can live for as long as you like; for example, 
- a `Vec<i32>` is self-contained and needn't be dropped before
any particular variable goes out of scope. 
- But a type like
`Vec<&'a i32>` has a lifetime that must be enclosed by `'a`: it
must be dropped while its referents are still alive.

Lifetime problem example
```
struct S<'a> {
    x: &'a i32,
    y: &'a i32,
}
```

```
let x = 10;
let r;
{
    let y = 20;
    {
        let s = S {x: &x, y: &y };
        r = s.x;
    }
}
println!("{}",r);
// There's an error.
// we initialized s.y with &y, requiring 'a to be no longer than y's lifetime
// i.e. here it's clear that y's lifetime is shorter than x's
// yet you claimed that they had equal lifetimes in the previous struct
// the compiler balks ( it's a paradox: no lifetime is shorter than y's scope but longer than r's)

// Solution: each ref gets a distinct lifetime
// Oprah: you get a lifetime! you get a lifetime!
struct S<'a, 'b> {
    x: &'a i32,
    y: &'b i32
}
// this struct is saying that a and b may live for different durations, more generally, they have independent lifetimes

```

function lifetime example

```rs
fn f<'a>(r: &'a i32, s: &'a i32) -> &'a i32 { r } // perhaps too tight
```

let lifetime parameters vary independently
```rs
fn f<'a, 'b>(r: &'a i32, s: &'b i32) -> &'a i32 { r } // looser
```

Implicit lifetimes

`self`'s lifetime is the default lifetime chosen for return values if you do not explicitly state lifetimes
``` rs
fn find_by_prefix(&self, prefix: &str) -> Option<&String>
```
becomes
```rs
fn find_by_prefix<'a, 'b>(&'a self, prefix: &'b str) -> Option<&'a String>
```


# Global Variable
static = global

Rust's equivalent of a global variable is called a
static: it's a
value that's created when the program starts and lasts until
it terminates.

What if we tried to pass &x to our function f from earlier
that stores its argument in a static?
```
fn f(p: &'static i32) { ... }
let x = 10;
f(&x);
```
This fails to compile: the reference &x must not outlive x,
but by passing it to f, we constrain it to live at least as long
as 'static. There's no way to satisfy everyone here, so
Rust rejects the code.

## Rc and Arc: Shared Ownership
Arc is for thread-safe code. Don't use it if you're not multithreading.

# Copy
If Rust copies a type by default that likely means its cheap.
`Does not implement copy trait` 
The type you're using is not a cheap value to copy.

When we pass the vector to the loop directly, as in for ...
in v, this
moves the vector out of v, leaving v uninitialized.
The for loop's internal machinery takes ownership of the
vector and dissects it into its elements. At each iteration,
the loop moves another element to the variable s. Since s
now owns the string, we're able to modify it in the loop
body before printing it. And since the vector itself is no
longer visible to the code, nothing can observe it mid-loop
in some partially emptied state.

## Struct
A struct assembles several values of assorted
types together into a single value so you can deal with
them as a unit.

And a struct can have methods
associated with it that operate on its components.

## Rc (Reference Count)
Recall that Rc stands for reference counting,
and a value in an Rc box is always shared and therefore
always immutable.

## Interior Mutability
Now suppose you want to add a little logging to the
SpiderRobot struct, using the standard File type. There's
a problem: a File has to be mut. All the methods for
writing to it require a mut reference.
This sort of situation comes up fairly often. 

What we need is a little bit of mutable data (a File) inside an otherwise immutable value (the SpiderRobot struct). This is calledinterior mutability. 

Rust offers several flavors of it; in this
section, we'll discuss the two most straightforward types:
Cell<T> and RefCell<T>, both in the std::cell module.

## Refcell
or logging, we need a mutable File, and File isn't
copyable.
The right tool in this case is a RefCell. Like Cell<T>,
RefCell<T> is a generic type that contains a single value of
type T. Unlike Cell, RefCell supports borrowing
references to its T value:RefCell::new(value)

### Refcell changes reference check from compile-time to run-time
normally, when you borrow a reference to
a variable, Rust checks
at compile time to ensure that
you're using the reference safely. If the checks fail, you get
a compiler error. RefCell enforces the same rule using run-
time checks.

##  Pattern Matching
Rust patterns are a little like regular
expressions for all your data. They're used to test whether
or not a value has a particular desired shape

## Concurrency, Multithreading
- `Send` - type is safe to send to another thread
- `Sync` - safe to share between threads (T is `Sync` if and only if `&T` is `Send`)

 Approaches that
systems programmers commonly use for concurrency include the following:
- A *background thread* that has a single job and
periodically wakes up to do it.

- General-purpose
*worker pools* that communicate
with clients via
*task queues*.

- *Pipelines* where data flows from one thread to the
next, with each thread doing a little of the work.

- *Data parallelism*, where it is assumed (rightly or
wrongly) that the whole computer will mainly just be
doing one large computation, which is therefore split
into
n pieces and run on
n threads in the hopes of
putting all
n of the machine's cores to work at once.

- *A sea of synchronized objects*, where multiple
threads have access to the same data, and races are
avoided using ad hoc
locking schemes based on low-
level primitives like mutexes. (Java includes built-in
support for this model, which was quite popular
during the 1990s and 2000s.)

- *Atomic integer operations* allow multiple cores to
communicate by passing information through fields
the size of one machine word. (This is even harder to
get right than all the others, unless the data being
exchanged is literally just integer values. In practice,
it's usually pointers.)

Rust allows all these models.

Incidentally, it's no coincidence that we've used a map
method and a reduce method. The MapReduce
programming model, popularized by Google and Apache
Hadoop, has a lot in common with fork-join. It can be seen
as a fork-join approach to querying distributed data.

## Share immutable data across threads with Arc
Data in an Arc is immutable.

# Channel
A channel is a one-way conduit for sending values from one
thread to another. In other words, it's a thread-safe queue.

Unix pipes are for
sending bytes, channels are for sending Rust values

# Async

When you write synchronous code, your programs will block.

But if you're working in a networked environment where your program will have to wait indeterminate amounts of time for I/O( input/output ), your program cannot afford to wait for long periods of time for data that may or may not arrive which will waste CPU cyles. In these cases you can't affor synchronous code, you'll have to find a different method.

You need asynchronous code, code that runs then immediately exits once it reaches the part it needs to `await` so it can be free to do other tasks and return to finish the task once it's alerted that the required data has arrived.

This uses the async_std crate's networking and task
modules and **adds .await after the calls that may block.**

``` rs
use std::io::prelude::*;
use std::net;
fn cheapo_request(host: &str, port: u16, path: &str) -> std::io::Result<String>
{
    let mut socket = net::TcpStream::connect((host, port))?;
    let request = format!("GET {} HTTP/1.  1\r\nHost: {}\r\n\r\n", path, host);
    socket.write_all(request.as_bytes())?;
    socket.shutdown(net::Shutdown::Write)?;
    let mut response = String::new();
    socket.read_to_string(&mut response)?;
    Ok(response)
}
```

![async synchronous example](./async-sync-example-00.PNG)

The darker gray backgrounds mark the times when the
program is waiting for the operating system to finish the
system call. We didn't draw these times to scale. If we had,
the entire diagram would be darker gray: in practice, this
function spends almost all of its time waiting for the
operating system. The execution of the preceding code
would be narrow slivers between the system calls.

We need to be able to take other work while we wait for the we wait for system calls to complete.
```
fn read_to_string(&mut self, buf: &mut String) ->
std::io::Result<usize>;
```
It's written right into the type: this function doesn't return
until the job is done, or something goes wrong. This
function is
synchronous: the caller resumes when the
operation is complete

We need a new tool.

### Async.Futures
We need futures

A Future represents an operation that you can test for
completion.

 A future's `poll` method never waits for the
operation to finish: it always returns immediately.

if ( operation is complete )
- `poll` returns `Poll::Ready(output)`

if not
- `poll` returns `Pending`

If and when the future is worth polling again, it
promises to let us know by invoking a
waker, a callback
function supplied in the Context.

We call this the “piñata
model” of asynchronous programming: the only thing you
can do with a future is whack it with a poll until a value
falls out.

You'll need to poll this future
until you get a Ready(result) from it. 

```
fn read_to_string<'a>(&'a mut self, buf: &'a mut String)
-> impl Future<Output = Result<usize>> + 'a; // return a thing that implements Future
```

### When to use async
Or, if your design is
naturally organized as many independent tasks
communicating with each other, then low per-task costs,
short creation times, and quick context switches are all
important advantages. This is why chat servers are the
classic example for asynchronous programming, but multi-
player games and network routers would probably be good
uses too.

# How to say
`&mut`: "ref mute T"