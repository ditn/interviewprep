# Binary Search

### Explanation

Binary search only works on a pre-sorted list.

```javascript
[2, 3, 5, 8, 10, 15, 22, 23]
 ^            ^           ^
low          mid         high
```
* If item at mid point is correct, return it.
* If item at mid point is greater than the target, move `high` to below the mid:

```javascript
[2, 3, 5, 8, 10, 15, 22, 23]
 ^        ^
low      high
```

* If item at mid point is lesser than the target, move `low` to above the mid:

```javascript
[2, 3, 5, 8, 10, 15, 22, 23]
                  ^       ^
                 low     high
```

Keep going until guess is found. This can be done both recursively and iteratively.

### < or <=?
* If you are returning from inside the loop, use `low <= high`
* If you are reducing the search space, use `low < high` and finally return a `low`

### Implementation

```kotlin
/**
 * Returns index of target item, or -1 if not found
 */
fun search(array: List<Int>, target: Int): Int {
	var low = 0
	var high = array.size - 1
	
	while (low <= high) {
		val mid = low + (high - low) / 2
		val guess = array[mid]
		
		if (guess == target) {
			return mid
		} else if (guess < target) {
			low = mid + 1
		} else {
			high = mid - 1
		}
	}
	
	return -1
}
```

### Big O

Runs in $O(log \cdot n)$ time.