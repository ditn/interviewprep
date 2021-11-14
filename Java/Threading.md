# Threading

### When might you not want to use Coroutines?
Coroutines are lightweight, and you can spawn many coroutines within a thread. However, if you're doing something computationally expensive using a coroutine, you may find that it starves other coroutines of CPU time until the OS sends an interrupt.

This is why coroutines in Kotlin have multiple schedulers, so that a computationally heavy coroutine doesn't starve the UI thread, for example.

### Process vs Thread
A process is a self-contained execution environment - e.g. a program or application. A thread is a single task of execution within that process.

Threads share process resources, processes don't share resources for security reasons.

### Creating Threads
- Extend the `Thread` class
- Implement the `Runnable` interface and create a `Thread` from it

### Thread Pool
A thread pool manages a pool of worker threads, and contains a queue that holds tasks waiting to be executed. 

### Context Switching
This is the process of storing and restoring CPU state so that thread execution can be resumed from the same point at a later point in time. Context switching is an essential feature for multitasking operating systems in multi-threaded environments.

### Deadlock
For deadlock to occur, you must have 4 conditions be true:
1) Mutual exclusion - only one process can access a resource at a given time
2) Hold and wait - processes already holding a resource can request additional resources, without relinquishing their current resources
3) No preemption - one process cannot forcibly remove another process' resource
4) Circular wait - two or more processes form a circular chain where each process is waiting on another resource in the chain

Remove any of the above conditions to break a deadlock. Most deadlock algorithsm focus on avoiding the circular wait problem.

### Livelock
A livelock occurs when more than one process is continually attempting to get out of the way of another, which means that they never actually access the resource they want and therefore never complete.

A simple analogy for this is two people meeting in a corridor and attempting to pass eachother, but always stepping in the same direction.


