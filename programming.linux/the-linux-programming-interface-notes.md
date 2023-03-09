# 2.1 The Kernel is the Core Operating System

How does a kernel simply software development?
It provides a software layer to manage the limited resources of a computer.

A kernel
- schedules processes
- creates and terminates processes
- manages memory
    - processes are isolated from one another
    - only parts of a prcess needs to be kept in memory
- provisions a file system
- controls accesses to devices
- networking
    - the kernel transmits and receives network messages(packets) on behalf of the user processes
- provides a system call application programming interface (API)

## Kernel mode vs User mode
- Modern processors architecture typically allow CPU to operate in at least two modes: user mode, kernel mode
    - areas of virtual memory are marked as `user space` or `kernel space`

## Process  vs Kernel view of the system

A running system has many processes.
Processes have no control over themselves.
The kernel controls the processes.

# 2.5 File I/O Model

- The kernel essentially provides one file type: a sequential stream of bytes.
- In UNIX systems end-of-file is represented by a read that returns no data

## File Descriptors

- Normally, processes inherit three open file descriptors when it is started by the shell
    - 0, standard input, stdin
    - 1, standard output, stdout
    - 2, standard error, stderr
- In an interactive shell or program, these descriptors are normally connected to the terminal

## Filters
What is a filter?
- Name often applied to a program that reads input from `stdin` performs some transformation of that input and writes transformed output to `stdout`, e.g. `cat`, `grep`, `tr`, `sort`, `wc`, `sed`, `awk`

# 2.7 Process
- A process is an instance of an executing program
- When a program is executed, the kernel
    - loads the program into virtual memory
    - allocates space for program variables
    - sets up kernel bookkeeping data structures: (process ID, termination status, user ID, group ID, etc)
    - the kernel coordinates sharing of computer resources for each process

Process Memory Division
- [ Text | Data | Heap | Stack ]
    - text: instructions of the program
    - data: static variables used by the program
    - heap: area where programs can dyanamically allocate extra memory
    - stack: piece of memory that grows and shrinks as functions are called and returned, used to allocate storage for local variables and function call linkage information

Process Creation and Program Excecution
- A process creates new process with `fork()` system call
- parent process.forks() -> child process
- the child can call `execve` to call and load a new program
    - the `execve` call destroys the existing memory structure and makes a new one based on the new program

Process ID and Parent ID
- process identifier (PID)
- parent identifier (PPID)

Process termination and termination status

- termination status 0 -> process succeeded
- termination status: nonzero -> error

Process user and Group identifiers (credentials)
- Each process has associated user IDs (UID) and group IDs(GID)
- real: user id group id
- effective: user id, group id
    - typically the real id = effective id
    - the effective ID can be changed
    - changing the effective id is a mechanism that allows processes to assumes privileges of other users or groups
- supplementary group IDs
- child processes inherit IDs from their parents

Privileged processes
- privileged process is one whose effective user ID is 0(superuser)
- UID = 0 -> privileged, UID != 0 -> non-privileged

Capabilities
- What are capabilities? Distinct units of privilegeds
- priviledged operation associated with capability
- security benefits, by granting subsets of capability to a process

The _init_ process
- when booting, kernel creates _init_ "the parent of all processes"
- what is `init`? the parent of all processes
    - comes from program file in `/sbin/init`
- the `init` process can't be killed
- it's task is to create and maintain processes required by the running system


## 3.1 System Calls
A system call is a controlled entry point into the kernel
- allowing a process to request the kernel perform some action on the process's behalf
 - child gets copies of the parent's memory structure


The kernel makes a range of of services accessible to programs via the system call application programming interface(API)
    - services include:
        - create new process
        - perform I/O
        - create pipe for interprocess communication

Why do system calls create overhead?
- switch from user to kernel mode
- kernel must verify system arguments
- the kernel must transfer data between user memory and kernel memory

The usual C library implementation is?
`glibc`

## printf format specifiers

int - %d
long %ld
long long %lld

How to prevent representation dependency in printf() call?
- use the %ld specifier and always cast the corresponding value to `long`
```c
pid_t mypid;

mypid = getpid();
printf("My PID is %ld\n", (long) mypid);
```

## How do you properly initialize structures?
SUSv3 does not specify the order of field definitions,

Consequently, somthing like this is not portable

Consider the struct `sembuf` which is used to represent a semaphore operation
``` c
struct sembuf {
    unsigned short sem_num; /* semaphore number */
    short          sem_op;  /* operation to be performed */
    short          sem_flg; /* Operation flags */
};
```
`struct sembuf s = {3,-1, SEM_UNDO};`

You should use explicit assignment
```c
struct sembuf s;

s.sem_num = 3;
s.sem_op = -1;
s.sem_flg = SEM_UNDO;
```
Why are file descriptors important?

What are file descriptors?

How does a process relate to a file descriptor?
Each process has its own set of file descriptors.

Glossary



Network Byte Order
- `htons()` host to network short
- `htonl()` host to network long
- `ntohs()` network to host short
- `ntohl()` network to host long

File IO
- io = input/output
- file offset = the location in the file at which the next read() or write() will start

crt0 = C runtime 0
glibc -> g-lib-c -> g=gnu, lib=library, c=c -> gnu,library,c -> GNU C Library


lib = library


std = standard

Users and Groups
- UID = User id
- GID = Group id

- util = utilities