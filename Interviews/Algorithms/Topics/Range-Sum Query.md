# Range-Sum Query

Given a 2D matrix `matrix`, handle multiple queries of the following type:

1.  Calculate the **sum** of the elements of `matrix` inside the rectangle defined by its **upper left corner** `(row1, col1)` and **lower right corner** `(row2, col2)`.

Implement the NumMatrix class:

-   `NumMatrix(int[][] matrix)` Initializes the object with the integer matrix `matrix`.
-   `int sumRegion(int row1, int col1, int row2, int col2)` Returns the **sum** of the elements of `matrix` inside the rectangle defined by its **upper left corner** `(row1, col1)` and **lower right corner** `(row2, col2)`.

`sums[i+1][j+1]` represents the sum of area from `matrix[0][0]` to `matrix[i][j]`

```
+-----+-+-------+     +--------+-----+     +-----+---------+     +-----+--------+
|     | |       |     |        |     |     |     |         |     |     |        |
|     | |       |     |        |     |     |     |         |     |     |        |
+-----+-+       |     +--------+     |     |     |         |     +-----+        |
|     | |       |  =  |              |  +  |     |         |  -  |              |
+-----+-+       |     |              |     +-----+         |     |              |
|               |     |              |     |               |     |              |
|               |     |              |     |               |     |              |
+---------------+     +--------------+     +---------------+     +--------------+

   sums[i][j]      =    sums[i-1][j]    +     sums[i][j-1]    -   sums[i-1][j-1]   +  

                        matrix[i-1][j-1]
```

So, we use the same idea to find the specific area's sum.

```
+---------------+   +---------+----+   +---+-----------+   +---------+----+   +---+----------+
|               |   |         |    |   |   |           |   |         |    |   |   |          |
|   (r1,c1)     |   |         |    |   |   |           |   |         |    |   |   |          |
|   +------+    |   |         |    |   |   |           |   +---------+    |   +---+          |
|   |      |    | = |         |    | - |   |           | - |      (r1,c2) | + |   (r1,c1)    |
|   |      |    |   |         |    |   |   |           |   |              |   |              |
|   +------+    |   +---------+    |   +---+           |   |              |   |              |
|        (r2,c2)|   |       (r2,c2)|   |   (r2,c1)     |   |              |   |              |
+---------------+   +--------------+   +---------------+   +--------------+   +--------------+
```

```kotlin
class NumMatrix(matrix: Array<IntArray>) {
    
    private val dp = Array(matrix.size + 1) { IntArray(matrix[0].size + 1) }

    init {
        if (matrix.isNotEmpty() && matrix[0].isNotEmpty()) {
            
			for (row in 0 until matrix.size) {
                for (column in 0 until matrix[0].size) {
                    dp[row + 1][column + 1] =
                        dp[row + 1][column] +
                            dp[row][column + 1] +
                            matrix[row][column] -
                            dp[row][column]
                }
            }
        }
    }

    fun sumRegion(row1: Int, col1: Int, row2: Int, col2: Int): Int {
        return dp[row2 + 1][col2 + 1] -
            dp[row1][col2 + 1] -
            dp[row2 + 1][col1] +
            dp[row1][col1]
    }
}
```