# Decrementing

Don't forget that you can traverse an array backwards:

```kotlin
val list = listOf(1, 2, 3, 4, 5)

for (index in list.size - 1 downTo 0) {
    // Do something starting from the right-hand side
}
```

# Init'ing Lists
```kotlin
val list = MutableList(5) { index -> index * 2 }
```

# Largest Value in Map

```kotlin
val map = mapOf("one" to 1, "two" to 2, "three" to 3)

val max = map.maxBy { it.value }!!.key // "three"
```

# Sorting Lists
```kotlin
val randomList = listOf(3, 5, 1, -10, 89, 3)

// Create a new list - O(n) space, O(n log n) complexity
val newList = randomList.sorted()

// Sort in-place - O(1) space, O(n log n) complexity
randomList.sort()
```

# Indexes
```kotlin
val lastIndex = "123".size - 1
// or
val lastIndex = "123".lastIndex

for (index in 0 until list.size) {
	// Operation
}
// or
for (index in list.indices) {
	// Operation
}
```