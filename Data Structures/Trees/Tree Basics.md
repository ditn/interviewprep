# Trees

Like a [[Linked List]], Tree data structures don't require items in contiguous memory.

### Basic Definitions
- **Node** - an item in the tree
- **Root node** - the root of the tree
- **Edge** - a pointer to another node
- **Leaf node** - a node with no pointers to other nodes
- Nodes must have exactly one **parent**
- Nodes that have the same parent are **siblings**
- A node's **level** is the number of steps from it to the **root node**
- A tree's **height** is the level from the bottom-most node to the **root node**
- A **branch** is the path from the root to a **leaf node**

```kotlin
class Node<T> {
    
    val value: T? = null
    val edges: List<Node> = emptyList()
}
```

### Tree Definitions

A [[Binary Search Tree]] is a tree that can be efficiently searched. Typically, this is possibly because the tree is ordered, and there are strict rules regarding the number of children per node (there can only be two, i.e. binary!).