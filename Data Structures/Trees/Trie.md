# Trie
## Insertion $O(m)$
We insert a key by starting at the root and searching for a link which corresponds to the first character:
- If a link exists, move to that node
- If not, add that node as a link to the current node and move to it
	- If we reach the end of the word, mark the last node as the end

# Search $O(m)$
Each word is represented as a path from the root to a leaf node. We start from the root with the first character, looking for links corresponding to that character:
- If the link exists, we move to the next node in the path following this link
- If there's no keys in the search word left and the node isn't marked as `isEnd`, return false
- Otherwise return true

# Search Prefix
Exactly the same as searching for a word, but we don't need to check `isEnd`.


```kotlin
class Trie() {

    private val root = TrieNode()
    
    fun insert(word: String) {
        var node = root
        for (char in word) {
            if (!node.containsKey(char)) {
                node.put(char, TrieNode())
            }
            
            node = node.get(char)!!
        }
		
        node.setEnd()
    }

    /**
	* Returns true if the entire word is in the Trie
	*/
    fun search(word: String): Boolean {
        var node = root
        for (char in word) {
            if (!node.containsKey(char)) return false
            
            node = node.get(char)!!
        } 
        
        return node.isEnd()
    }

	/**
	* Returns true if there is any word in the trie that starts with the
	* given prefix
	*/
    fun startsWith(prefix: String): Boolean {
        var node = root
        for (char in prefix) {
            if (!node.containsKey(char)) return false
            
            node = node.get(char)!!
        } 
        
        return true
    }

}

class TrieNode {
    
    private val NUM_CHARS = 26
    
    private val links = Array<TrieNode?>(NUM_CHARS) { null }
    
    private var isEnd = false
    
    fun containsKey(char: Char): Boolean {
        return links[char - 'a'] != null
    }
    
    fun get(char: Char): TrieNode? {
        return links[char - 'a']
    }
    
    fun put(char: Char, node: TrieNode) {
        links[char - 'a'] = node 
    }
    
    fun setEnd() {
        isEnd = true
    }
    
    fun isEnd() = isEnd
}
```