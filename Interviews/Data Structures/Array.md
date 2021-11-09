# Arrays
Prefer an Array over a [[Linked List]] when:
- You frequently need to access to data at random positions
- You need extreme performance on lookup ($O(1)$)
- You know the size of the dataset in advance - remember there's a penalty for growing an Array

Typically, Arrays don't automatically resize, however the ArrayList class in Java do. Normal implementation is when the ArrayList is full, it doubles in size (resizing factor of 2).
    - This doubling takes $O(n)$.
    - It happens so infrequently that the amortized insertion time is still $O(1)$ for a single element
    - For many elements, $O(n)$

# Big O
### Time
- O(n) to add or remove an item at the start of the list
- O(1) to add or remove an item at the end of the list
- O(1) to find an access via an index
- O(1) to update or replace an item
- O(n) to insert or remove elsewhere

### Space
- Contiguous memory, and the proximity of the items helps performance
- Space required = (array capacity, which is >=n) * size of item = O(n)