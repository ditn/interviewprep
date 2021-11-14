# TreeMap

The `TreeMap` interface in Java is used to implement `Map`. The `Map` is sorted according to the natural ordering of its keys, or by a `Comparator` implementation.

Because these keys are sorted, you can fetch a submap using keys. This makes it particularly useful for questions where you might need to keep track of the incidences of something but also search that list.

```kotlin
fun <K,V> subMap(fromKey: K, toKey: K): SortedMap<K, V>
```

In Kotlin you can call `toSortedMap()` on a `Map`.

TreeMap provides a performance of $O(log \cdot n)$ for most operations like `add()`, `remove()` and `contains()`.

## Uses
TreeMaps are particularly useful when looking up ranges, such as time intervals.

## Implementation
Internally, a TreeMap is maintained via a [[Red-Black Tree]].

Therefore, operations like `add`, `remove` and `contains` are all $O(log \cdot n)$.