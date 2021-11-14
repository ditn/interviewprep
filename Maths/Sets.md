A set is just a collection of items.

# Subset
A collection of objects that are contained inside another set.

# Union
Given two sets, $S_1$ and $S_2$, the items which belong to _either_ $S_1$ or $S_2$ is described as the _union_ of the two sets.

$$S_3 = S_1 \cup S_2$$

# Intersection
Given two sets, $S_1$ and $S_2$, the items which belong to both $S_1$ and $S_2$ is described as the _intersection_ of the two sets.

$$S_3 = S_1 \cap S_2$$

# Power Set
Given a collection of objects $S$, a power set is a set of all subsets of $S$.

$$P_s = {S_1,S_2,...,S_{16}}$$

For a simple example:

> You are given a set of fragrances, `F`. Compute a set which contains all possible combinations of `F` - list all fragrances that can be made.

Computing this requires nested `for` loops. An outer loop keeps track of the next flower to consider. The inner loop duplicate the fragrances, adding the current flower to the duplicates:

```javascript
function power_set(flowers)
    fragrances <- Set.new
    fragrances.add(Set.new)
    
    for each flower in flowers
        new_fragrances <- copy(fragrances)
        
        for each fragrance in new_fragrances
            fragrance.add(flower)
        fragrances <- fragrances + new_fragrances

return fragrances
```

Each extra flower causes `fragrances` to double in size - O(2^n) complexity.

Generating a power set is equivalent to generating a truth table - it gets out of hand quickly.

```kotlin
fun subsets(nums: IntArray): List<List<Int>> {  
    val results = mutableListOf<MutableList<Int>>()  
    results.add(mutableListOf())  
  
    for (num in nums) {  
        val newSubsets = mutableListOf<MutableList<Int>>()  
  
        for (current in results) {  
            val subset = current + num  
            newSubsets.add(subset.toMutableList())  
        }  
  
        results.addAll(newSubsets)  
    }  
  
    return results  
}
```