# Knapsack Problem
## Problem
You're given an array of arrays, where each array represents an item. The first value in that array is the value, the second is the weight.

Fit the items in your knapsack without having the sum of the weights exceed the knapsack's capacity. Your goal is the maximise the combined value.

Return the maximised combined value and the indices of each item.

## Example
```javascript
items = [[1, 2], [4, 3], [5, 6], [6, 7]]
capacity = 10

output = [10, [1, 3]] // e.g. [4, 3] and [6, 7]
```

## Implementation
We can construct a 2D array to represent the capacity of the knapsack and the list of items. Each cell therefore contains the maximum value of the current combination.

$x$ axis = capacity
$y$ axis = items

| | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
| - | - | - | - |  - |  - |  - |  - |  - |  - |  - |  - |  
| [] | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 
| [1, 2] | 0 | 0 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 
| [4, 3] | 0 | 0 | 1 | 4 | 4 | 5 | 5 | 5 | 5 | 5 | 5 |
| [5, 6] | 0 | 0 | 1 | 4 | 4 | 5 | 5 | 5 | 6 | 9 | 9 |
| [6, 7] | 0 | 0 | 1 | 4 | 4 | 5 | 5 | 6 | 6 | 9 | 10 |

Remember that for dynamic programming, the base case is often `0` or an empty array, so your array should be init'd one larger than you might normally.

```kotlin
fun knapsack(items: List<List<Int>>, capacity: Int): Pair<Int, List<Int>> {
    val array = List(items.size + 1) { MutableList(capacity.size + 1) { 0 } }
	// ...
}
```

This also means that fetching any values from this array typically involves accessing `index - 1`, as each value is actually shifted due to adding the `0` and `[]` base cases.

For array `values`, where `w` is the weight of the item at `i` and `v` is the value of the current item at `i`:

```javascript
if (w <= j)
	values[i][j] = max(values[i - 1][j], values[i - 1][j - w] + v)
else 
	values[i][j] = values[i - 1][j]
```

Once the array is constructed, you'll need to work out which items were actually added to create this maximal value. To do this, you backtrack starting at the bottom right-most item. In the example above, this is `10`.

```javascript
max = values[items.size][capacity]
```

Compare this with the value directly above. If the value is the same, move one step up because no item was added.

If the value at your current index is *greater*, add the current position to the outputs, and then move both one row up and the weight of the current item backwards. In this example, we would move to 4 (`values[3, 3]`).

Continue repeating these steps until reaching a capacity of `0`. In this example, the steps look like:

| | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
| - | - | - | - |  - |  - |  - |  - |  - |  - |  - |  - |  
| [] | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 
| [1, 2] | **0** | 0 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 
| [4, 3] | 0 | 0 | 1 | **4** | 4 | 5 | 5 | 5 | 5 | 5 | 5 |
| [5, 6] | 0 | 0 | 1 | **4** | 4 | 5 | 5 | 5 | 6 | 9 | 9 |
| [6, 7] | 0 | 0 | 1 | 4 | 4 | 5 | 5 | 6 | 6 | 9 | **10** |

```javascript
values = [10, 4, 4, 0]
positions = [values[5, 10], values[3, 3], values[2, 3], values[1, 0]]
items = [[6, 7], [4, 3]]
```

## Complexity
$O(n \cdot c)$ time and space, where $n$ is the number of items and $c$ is the capacity of the knapsack.

## Implementation
```kotlin
fun knapsackProblem(items: List<List<Int>>, capacity: Int): Pair<Int, List<Int>> {
	val array = List(items.size + 1) { MutableList(capacity + 1) { 0 } }

	for (item in 1 until items.size + 1) {
		val (value, weight) = items[item - 1]

		for (cap in 0 until capacity + 1) {
			val previous = array[item - 1][cap]
			if (weight > cap) {
				array[item][cap] = previous
			} else {
				val potentialMax = array[item - 1][cap - weight] + value
				array[item][cap] = Math.max(previous, potentialMax)
			}
		}
	}

	val maximisedValue = array[items.size][capacity]

	return maximisedValue to reconstruct(array, items)
}

private fun reconstruct(
	array: List<List<Int>>, 
	items: List<List<Int>>
): List<Int> {
	val results = mutableListOf<Int>()

	var i = array.size - 1
	var c = array[0].size - 1

	while (i > 0) {
		if (array[i][c] == array[i - 1][c]) {
			i--
		} else {
			results.add(i - 1)
			val (_, weight) = items[i - 1]
			c -= weight
			i--
		}
		
		if (i == 0) break
	}

	return results
}
```
