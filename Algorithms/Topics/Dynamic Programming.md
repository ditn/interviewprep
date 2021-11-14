# Dynamic Programming

### A Framework to Solve
Typically, dynamic programming problems can be solved with 3 main components:

1) First, we need a function or [[Array]] that represents the answer to the problem from a given state. This is often named `dp`.

For instance, we may have an [[Array]] `dp` where `dp[i]` represents the length of the longest increasing subsequence that ends with the $i^{th}$ element.

2) We need a way to transition between states - e.g. from `dp[5]` to `dp[7]`. This is called the **recurrence relation** and can be quite difficult to figure out.

Given that we know `dp[0]`, `dp[1]` and `dp[2]`, how can we calculate `dp[3]`?

In the case of the longest increasing subsequence, if `nums[3] > nums[2]`, we can simply take `dp[2]` and increase the length by 1.

Of course we're trying to maximise `dp[3]`, so we need to check `dp[0..2]`.

3) We need a **base case**. Typically for this, we initialize every element of `dp` to some value - perhaps `1` or `0`, sometimes `true` or `false`.

### Example - Longest Increasing Subsequence

1.  Initialize an array `dp` with length `nums.length` and all elements equal to 1. `dp[i]` represents the length of the longest increasing subsequence that ends with the element at index `i`.
2.  Iterate from `i = 1` to `i = nums.length - 1`. At each iteration, use a second for loop to iterate from `j = 0` to `j = i - 1` (all the elements before i). For each element before `i`, check if that element is smaller than `nums[i]`. If so, set `dp[i] = max(dp[i], dp[j] + 1)`.
3.  Return the max value from `dp`.

```kotlin
fun lengthOfLIS(nums: IntArray): Int {
	val dp = IntArray(nums.size) { 1 }

	for (i in 1 until nums.size) {
		// All elements before i
		for (j in 0 until i) {
			if (nums[j] < nums[i]) {
				dp[i] = Math.max(dp[i], dp[j] + 1)
			}
		}
	}

	return dp.max()!!
}
```