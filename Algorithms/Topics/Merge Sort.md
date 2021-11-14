# Merge Sort
## Complexity
|  | Best | Worst |
| - | -| - |
| Time | $O(n \cdot log  \cdot n)$ | $O(n \cdot log  \cdot n)$ |
| Space | | $O(n)$ |

## Usecase
Merge Sort is preferable to [[Quick Sort]] in a few scenarios. For very very large datasets, say 200GB of data, you can use MapReduce to offload computation of Merge Sort across multiple machines. This cannot be done with [[Quick Sort]] because the entire dataset has to be held in memory.

## Basic Algorithm
- Divide the array to be sorted in half
- Sort each half
- Merge these arrays back together

It is this merging function which does all the heavy lifting.

This version operates by copying all elements from the target array segment into a helper array, and keeping track of where the start of the left and right halves should be.

We then iterate through the helper, copying the smaller element from each half into the array. Once this is done, we copy any remaining elements into the target array.

Note that this algorithm works in-place, and doesn't return a new array.

## Implementation

```kotlin
fun mergeSort(array: IntArray) {  
    val helperArray = IntArray(array.size)  
    mergeSort(array, helperArray, 0, array.size - 1)  
}  
  
private fun mergeSort(  
    array: IntArray,  
 	helperArray: IntArray,  
 	low: Int,  
 	high: Int  
) {  
    if (low < high) {  
        val middle = (low + high) / 2  
 		// Sort left half  
 		mergeSort(array, helperArray, low, middle)  
        // Sort right half  
 		mergeSort(array, helperArray, middle + 1, high)  
        // Merge left and right  
		merge(array, helperArray, low, middle, high)  
    }  
}  
  
private fun merge(  
    array: IntArray,  
	helperArray: IntArray,  
	low: Int,  
	middle: Int,  
	high: Int  
) {  
    // Copy both halves into helper array  
 	for (index in low..high) {  
        helperArray[index] = array[index]  
    }  
  
    var helperLeft = low  
 	var helperRight = middle + 1  
 	var current = low  
  
 	// Compare two halves, copying smaller element of left and right back  
 	// into the original array 
	while (helperLeft <= middle && helperRight <= high) { 
		// If left element is smaller, copy into array
        if (helperArray[helperLeft] <= helperArray[helperRight]) {  
            array[current] = helperArray[helperLeft]  
            helperLeft++  
        } else {  
			// If right element is smaller, copy into array
            array[current] = helperArray[helperRight]  
            helperRight++  
        }  
		// Increment array
        current++  
    }  
  	// Right half doesn't need to be copied - it's already there!
    val remaining = middle - helperLeft  
  
    for (index in 0..remaining) {  
        array[current + index] = helperArray[helperLeft + index]  
    }  
}
```

Consider `[1, 4, 5, || 2, 8, 9]`. Prior to merging, both the target and helper array will end in `[8, 9]`. Once we copy over four elements, `[1, 4, 5, 2]`, into the target array, the `8` and `9` will still be in place in both arrays. No need to copy.