# Bubble Sort

### Explanation
```javascript
[8, 5, 2, 9, 5, 6, 3]
```

Given an unsorted array, we iterate through the array and compare each item to the next item. If we find that the first item is larger than the second item, we swap them.

This causes the largest number in the set to "bubble up" to the end of the array. This also means on each pass, we _know_ that the last number is the largest, so we can decrement a pointer from the end of the array and slowly shrink the comparison set.

We repeat this over and over until the array is sorted.

### Big O

Best case with a sorted array - $O(n)$
Worst case - $O(n^2)$

### Implementation

```kotlin
fun bubbleSort(array: MutableList<Int>): List<Int> {
    var endPointer = array.size - 1
	
	while (endPointer > 0) {
		for (index in 0 until endPointer) {
			val firstItem = array[index]
			val secondItem = array[index + 1]
			if (firstItem > secondItem) {
				array[index] = secondItem
				array[index + 1] = firstItem 
			}
		}
		
		endPointer--
	}
	
    return array
}
```