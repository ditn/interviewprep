# Hash Table

A hash table is generally made of an [[Array]] of [[Linked List]] and a hash code function - this hashcode function is used to compute the position in the Array via modulo.

1) First, we compute the hashcode of the provided key - note that two different keys might have the same hashcode (collisions), so we may have an infinite number of keys with the same hashcode
2) Next, use the hashcode to compute the position in the Array.  Typically this is something like `hash(key) % array_length`. Two different codes could of course map to the same index.
3) At this index there is a [[Linked List]] of both keys and values. Store this item and key in the [[Linked List]] - this is done because there may be collisions.

To avoid collisions, we typically ensure that a HashTable has 50% of it's space free, otherwise it's performance becomes much worse. This means that a Hash Table typically takes up quite a lot of space in the form of sequential memory compared to an [[Array]].

## Big O
It is this potential collision which means that the _worst case_ lookup for an item is $O(n)$, where $n$ is the number of keys.

Best case, and the amortized case, is $O(1)$.

This is because looking up an item is the same process - compute the hashcode from the key, compute the index from the hashcode, and then search the [[Linked List]] for the key.

Alternatively, we can implement a hash table with a [[Binary Search Tree]] - this reduces the worst-case time complexity to $O(log n)$. This potentially uses less space since we no longer allocate a large array. We can also iterate through the keys in order, which is sometimes useful.

