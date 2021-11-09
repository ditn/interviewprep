# Representations

A graph is similar to a tree, but it has **no root node**. This distinction means it can be used to model all sorts of different types of data - social networks, for example.

This also means that there might be cycles - similar to a [[Linked List]], or disconnectivity where one node is orphaned.

Graphs _can_ be trees. For a graph to be a valid tree, it must have _exactly_ `n - 1` edges, where `n` is the number of nodes. 

Any less, and it can't possibly be fully connected. Any more, and it _has_ to contain cycles. Additionally, if the graph is fully connected _and_ contains exactly `n - 1` edges, it can't _possibly_ contain a cycle, and therefore must be a tree!

Graphs can be represented in 3 ways:

- An [[Adjacency List]]
- A matrix
- Objects and pointers

| Operation | Adjacency Matrix | Adjancency List |
| - | - | -|
| Storage space | Because of the use of a $V \cdot V$ matrix, space = $O(v^2)$ | $O(V \cdot E)$ |
| + vertex | Storage must increase to $(V +1)^2$, and to achieve this we must copy the entire array. Therefore, $O(n^2)$ | $O(1)$, as we're just adding an item to a list |
| + edge | `matrix[i][j] = 1`, so $O(1)$ | Same as adding a vertex, $O(1)$ |
| - vertex | Storage must be decreased, so $O(v^2)$ | To remove a vertex, we must search for it. After this we must search for edges, so $O(V \cdot E)$ |
| - edge | `matrix[i][j] = 0`, so $O(1)$| Must traverse through all edges, so $O(E)$ |
| Querying | Content of the matrix must be checked - this lookup is $O(1)$ | To check for an edge, we must check for vertices adjacent to a given vertex. A vertex can have $V$ neighbours and worst-case we have to check every one. So time complexity is $O(V)$. |



