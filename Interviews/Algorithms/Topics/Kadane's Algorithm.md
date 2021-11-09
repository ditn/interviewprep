# Kadane's Algorithm
Find the largest sum of any contiguous subarray.

## Pseudocode
```javascript
function max_subarray(numbers)
    best_sum = -inf
    current_sum = 0
    for x in numbers
        current_sum = max(0, current_sum + x)
        best_sum = max(best_sum, current_sum)
    return best_sum
```

## Implementation
```kotlin
fun maxSubArray(nums: IntArray): Int {
	var currentSubArray = nums.first()
	var maxSubArray = nums.first()

	for (index in 1 until nums.size) {
		val number = nums[index]
		// If current subarray sum is negative, discard it, otherwise add to it
		currentSubArray = Math.max(number, currentSubArray + number)
		maxSubArray = Math.max(maxSubArray, currentSubArray)
	}

	return maxSubArray
}
```