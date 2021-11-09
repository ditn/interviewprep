# Red-Black Tree

A red-black tree is a self-balancing [[Binary Search Tree]] where each node has an extra bit - this bit is interpreted as red or black. These colours are then used to ensure that the tree remains balanced during insertions or deletions.

This balance may not be perfect, but it's enough to ensure around $O(log \cdot n)$ read time. Ergo, the height $h$ of a red-black tree is always $O(log \cdot n)$.

Quicker to add or delete items than an [[AVL Tree]], so often used in higher-write scenarios, or implementations of [[Hash Table]] data structures.