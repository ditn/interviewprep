# Big O Notation

$O(1)$ - Constant time

$O(log \cdot n)$ - Logarithmic time

$O(n)$ - Linear time

$O(n \cdot log \cdot n)$ - Log linear time

$O(n^2)$ - Quadratic time

$O(n^3)$ - Cubic time

$O(2^n)$ - Exponential time

$O(n!)$ - Factorial time

# Time Complexity

| Data Structure | Access | Search | Insertion | Deletion | 
|-|-|-|-|-|
| Array | $O(1)$ | $O(n)$ | $O(n)$ | $O(n)$ |
| Stack | $O(n)$ | $O(n)$ | $O(1)$ | $O(1)$ |
| Queue | $O(n)$ | $O(n)$ | $O(1)$ | $O(1)$ |
| Linked List | $O(n)$ | $O(n)$ | $O(1)$ | $O(1)$ |
| Doubly-Linked List | $O(n)$ | $O(n)$ | $O(1)$ | $O(1)$ |
| Hash Table | N/A | $O(1)$ | Best: $O(1)$ <br> Worst: $O(n)$ | Best: $O(1)$ <br> Worst: $O(n)$ |
| Binary Search Tree | Best: $O(log \cdot n)$ <br> Worst: $O(n)$ | Best: $O(log \cdot n)$ <br> Worst: $O(n)$ | Best: $O(log \cdot n)$ <br> Worst: $O(n)$ |  Best: $O(log \cdot n)$ <br> Worst: $O(n)$ |

| Algorithm | Best | Average | Worst | Space | 
|-|-|-|-|-|
| Quicksort | $O(n \cdot log \cdot n)$ | $O(n \cdot log \cdot n)$ | $O(n^2)$ | $O(log \cdot n)$ |
| Mergesort | $O(n \cdot log \cdot n)$ | $O(n \cdot log \cdot n)$ | $O(n \cdot log \cdot n)$ | $O(n)$ |
| Timsort | $O(n)$ | $O(n \cdot log \cdot n)$ | $O(n \cdot log \cdot n)$ | $O(n)$ |
| Heapsort | $O(n \cdot log \cdot n)$ | $O(n \cdot log \cdot n)$ | $O(n \cdot log \cdot n)$ | $O(1)$ |
| Bubblesort | $O(n)$ | $O(n^2)$ | $O(n^2)$ | $O(1)$ |
| Insertion Sort | $O(n)$ | $O(n^2)$ | $O(n^2)$ | $O(1)$ |
| Selection Sort | $O(n^2)$ | $O(n^2)$ | $O(n^2)$ | $O(1)$ |
| Tree Sort | $O(n \cdot log \cdot n)$ | $O(n \cdot log \cdot n)$ | $O(n^2)$ | $O(n)$ |
| Shell Sort | $O(n \cdot log \cdot n)$ | $O((n \cdot log \cdot n)^2)$ | $O((n \cdot log \cdot n)^2)$ | $O(1)$ |
| Bucket Sort | $O(n + k)$ | $O(n + k)$ | $O(n^2)$ | $O(n)$ |
| Radix Sort | $O(n + k)$ | $O(nk)$ | $O(nk)$ | $O(n + k)$ |
| Counting Sort | $O(n + k)$ | $O(n + k)$ | $O(n + k)$ | $O(k)$ |
| Cubesort | $O(n)$ | $O(n \cdot log \cdot n)$ | $O(n \cdot log \cdot n)$ | $O(n)$ |
