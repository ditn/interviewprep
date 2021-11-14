# Linked-Lists
Prefer a Linked List over an [[Array]] when:
- You require very fast insertions or deletions
- You don't need random access to items in the list (you have to start from position 0 and iterate)
- You can't evaluate the exact size of the list (it may grow or shrink during execution)

# Big O
### Time
- $O(1)$ to add or remove an item at the start of the list
- $O(n)$ to add or remove an item at the end of the list
- $O(n)$ to find and access via an index
- $O(1)$ to update
- $O(n)$ to insert or remove elsewhere

# Singley-Linked
Has a nullable reference to the next node in the List:
```java
class Node<T> {
	T item;
	@Nullable next Node;
}
```

# Doubley-Linked
Has nullable references to both the next and previous nodes in the list:
```java
class Node<T> {
	T item;
	@Nullable next Node;
    @Nullable previous Node;
}
```

# Delete Kth Node from LinkedList
* Use two pointers 
	* Move the first pointer `k` steps away from the head
	* Move both in unison until the end of the list
	* Delete the node at the first pointer

```kotlin
fun removeKthNodeFromEnd(head: LinkedList, k: Int) {
    var counter = 1
	var first = head
	var current: LinkedList? = head
	
	while (counter <= k) {
		current = current!!.next
		counter++
	}
	
	if (current == null) {
		head.value = head.next!!.value
		head.next = head.next!!.next
		return
	}
	
	while (current!!.next != null) {
		current = current.next
		first = first.next!!
	}
	
	first.next = first.next!!.next
}
```

# Reverse Linked List

```kotlin
fun reverseList(head: ListNode?): ListNode? {
	var previous: ListNode? = null
	var current: ListNode? = head

	while (current != null) {
		val temp = current.next
		current.next = previous
		previous = current
		current = temp
	}

	return previous
}
```