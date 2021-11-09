# Queues
These support two operations, `enqueue` and `dequeue`.

Queues are an example of First-In, First-Out or FIFO - the opposite to a [[Stack]].

# Priority Queue
This is a special type of queue where `enqueue` takes both a value `T` but also a priority `p`.

Think of it like a queue in a hospital - those who are higher priority get seen first. A priority queue is often used in computer processors to work out what to compute next - for instance, keyboard input is first priority.

# Kotlin
In Kotlin, a Queue is normally represented with a [[Linked List]]:

```kotlin
val queue = LinkedList<Int>()

queue.add(1)
// or
queue.offer(1)

val dequeued = queue.remove()
// or
val dequeued = queue.poll()

val last = queue.peek()
```

## Implementation
Can be implemented with two stacks:

- on enqueue, move all items from stack one to stack two
- add item to stack one
- move all items back to stack one