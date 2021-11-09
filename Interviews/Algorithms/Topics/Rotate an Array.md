# Rotate an Array

Rotating an array by 90$^{\circ}$ is a common question which has a bit of a trick to it.

The key is you can achieve this by _transposing_, then _reflecting_ the matrix. _Transposing_ means to swap each entry about the diagonal, and _reflecting_ means reversing the array from left to right.

```kotlin
fun rotate(matrix: Array<IntArray>): Unit {
	transpose(matrix)
	reflect(matrix)
}

private fun transpose(matrix: Array<IntArray>): Unit {
	val length = matrix.size
	
	for (row in 0 until length) {
		// Note that we start iterating through columns at position == row
		// This is because we are working diagonally
		for (column in row until length) {
			val temp = matrix[row][column]
			matrix[row][column] = matrix[column][row]
			matrix[column][row] = temp
		}
	}
}

private fun reflect(matrix: Array<IntArray>): Unit {
	val length = matrix.size

	for (row in 0 until length) {
		// Note that we reflect until length / 2
		// No reason to keep going after halfway
		for (column in 0 until length / 2) {
			val temp = matrix[row][column]
			matrix[row][column] = matrix[row][length - column - 1]
			matrix[row][length - column - 1] = temp
		}
	}
}
```