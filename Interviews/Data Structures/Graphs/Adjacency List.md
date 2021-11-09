# Adjacency List
Example input:
```javascript
Input: n = 5, edges = [[0,1],[0,2],[0,3],[1,4]]
Output: true
```

For a graph to be a valid tree, it must have _exactly_ `n - 1` edges, where `n` is the number of nodes. 

Any less, and it can't possibly be fully connected. Any more, and it _has_ to contain cycles. Additionally, if the graph is fully connected _and_ contains exactly `n - 1` edges, it can't _possibly_ contain a cycle, and therefore must be a tree!

```kotlin
// Where n is number of nodes
fun validTree(n: Int, edges: Array<IntArray>): Boolean {
	if (edges.size != n - 1) return false

	val adjacencyList = List(n) { mutableListOf<Int>() }
	val seen = mutableSetOf<Int>()

	// Build adjacency list
	for (edge in edges) {
		adjacencyList[edge[0]].add(edge[1])
		adjacencyList[edge[1]].add(edge[0])
	}

	val queue = LinkedList<Int>()
	queue.offer(0)
	seen.add(0)

	while (queue.isNotEmpty()) {
		val node = queue.poll()

		// BFS is just adding all neighbours to Queue
		for (neighbour in adjacencyList[node]) {
			if (seen.contains(neighbour)) continue

			queue.offer(neighbour)
			seen.add(neighbour)
		}
	}

	return seen.size == n
}
```