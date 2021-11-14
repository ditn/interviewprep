# Merge Intervals
- Sort the inputs by the first value - $O(n \cdot log \cdot n)$
- Check if the start of the current meeting (for instance) is greater than the end of the previous one
- Handle appropriately
	- Either update the interval or return false if attempting to work out meeting schedules


```kotlin
fun merge(intervals: Array<IntArray>): Array<IntArray> {
	intervals.sortBy { it.first() }
	
	val merged = LinkedList<IntArray>()

	for (array in intervals) {
		// if the list of merged intervals is empty or if the current
		// interval does not overlap with the previous, simply append it.
		if (merged.isEmpty() || merged.last()[1] < array.first()) {
			merged.add(array)  
		} else {
			// otherwise, there is overlap, so we merge the current and previous
            // intervals.
			merged.last()[1] = Math.max(merged.last()[1], array[1])
		}
	}

	return merged.toTypedArray()
}
```

```kotlin
fun canAttendMeetings(intervals: Array<IntArray>): Boolean {
	intervals.sortBy { it.first() }

	for (i in 0 until intervals.size - 1) {
		if (intervals[i][1] > intervals[i + 1][0]) return false
	}

	return true
}
```

```kotlin
fun minMeetingRooms(intervals: Array<IntArray>): Int {
	if (intervals.isEmpty()) return 0
	intervals.sortBy { it.first() }

	val minHeap = PriorityQueue<Int> { a, b -> a - b }

	minHeap.add(intervals.first()[1])

	for (interval in intervals.drop(1)) {
		if (interval[0] >= minHeap.peek()) {
			minHeap.poll()
		}

		minHeap.offer(interval[1])
	}

	return minHeap.size
}
```