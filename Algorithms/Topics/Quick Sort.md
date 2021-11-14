# Quick Sort
## Complexity
|  | Best | Worst |
| - | -| - |
| Time | $O(n \cdot log  \cdot n)$ | $O(n^2)$ |
| Space | | $(log  \cdot n)$ |

## Usecase
In general, prefer [[Merge Sort]] for larger arrays. However, Quick Sort tends to be faster in the real world because of fewer comparisons, and despite the worst-case performance being $O(n^2)$, this can generally be avoided by using a pivot picked at random.

That being said, avoid using Quick Sort on data sets which:
- Contain many duplicates
- Are largely sorted or reverse-sorted
- Can't be held in memory and require many reads from disk (Quick Sort does this with many random reads, whereas [[Merge Sort]] does this sequentially).

## Basic Algorithm

Quicksort == pivot

A pivot is an item in the array that meets the following 3 conditions when the array is sorted:

1) The pivot is in the correct position in the final, sorted array
2) Items to the left are smaller
3) Items to the right are larger

Method:
- Pick a random element and partition the array so that elements to the left of the partition element are smaller, and elements to the right are larger
- This occurs through a series of swaps
- Repeatedly partitioning the array and it's sub arrays this way yields a sorted array

In terms of time complexity, Quicksort can be very slow ($O(n^2)$) if the partition is chosen poorly (e.g. the first element of each subarray).

## Implementation

```kotlin
fun quickSort(array: IntArray) {
    quickSort(array, 0, array.size - 1)
}

private fun quickSort(array: IntArray, left: Int, right: Int) {
    val index = partition(array, left, right)
    
	if (left < index - 1) {
		// Sort left half
        quickSort(array, left, index - 1)
    }
    if (right > index) {
		// Sort right half
        quickSort(array, index, right)
    }
}

private fun partition(array: IntArray, left: Int, right: Int): Int {
    var leftIndex = left
    var rightIndex = right
    val middle = (left + right) / 2
    val pivot = array[middle]

    while (leftIndex <= rightIndex) {
		// Find element that should be on right
        while (array[leftIndex] < pivot) leftIndex++
		// Find element that should be on left
        while (array[rightIndex] > pivot) rightIndex--
	
		// Swap elements and move indices
        if (leftIndex <= rightIndex) {
            swap(array, leftIndex, rightIndex)
            leftIndex++
            rightIndex--
        }
    }

	// Return new pivot
    return leftIndex
}

private fun swap(array: IntArray, left: Int, right: Int) {
    val temp = array[left]
    array[left] = array[right]
    array[right] = temp
}
```