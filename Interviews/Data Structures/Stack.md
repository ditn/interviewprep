# Stacks

Supports two operations - `push` to add an item and `pop` to remove.

Stacks are known as Last-In, First-Out (LIFO), which is the opposite of a [[Queue]].

In Kotlin, these are also represented by a [[Linked List]]:

```kotlin
val stack = LinkedList<Int>()

stack.push(1)

stack.pop() `should be equal to` 1
```