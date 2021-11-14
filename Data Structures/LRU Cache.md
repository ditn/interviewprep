# LRU Cache

A Least Recently Used Cache is typically implemented with a Doubly-Linked List and a Map:

```kotlin
class DoublyLinkedList {
    
    private var head: Entry = Entry(0, 0)
    private var tail: Entry = Entry(0, 0)
    
    init {
        head.next = tail
        tail.previous = head
    }
    
    fun insertHead(entry: Entry) {
        entry.previous = head
        entry.next = head.next
        
        head.next?.previous = entry
        head.next = entry
    }
    
    fun remove(entry: Entry) {
        entry.previous?.next = entry.next
        entry.next?.previous = entry.previous
    }
    
    fun removeTail(): Int {
        val node = tail.previous!!
        val key = node.key
        
        remove(node)
        
        return key
    }
}

class Entry(
    val key: Int,
    val value: Int,
    var next: Entry? = null,
    var previous: Entry? = null
)

class LRUCache(val capacity: Int) {
    
    private val cache = mutableMapOf<Int, Entry>()
    private val list = DoublyLinkedList()
    
    operator fun get(key: Int): Int {
        if (!cache.containsKey(key)) return -1
        update(key, cache[key]!!)
        
        return cache[key]!!.value
    }

    fun put(key: Int, value: Int) {
        val n = Entry(key, value)
        
        if (cache.containsKey(key)) {
            list.remove(cache[key]!!)
        } else if (cache.size >= capacity) {
            val k = list.removeTail()
            cache.remove(k)
        }
        
        list.insertHead(n)
        cache[key] = n
    }

    private fun update(key: Int, n: Entry) {
        list.remove(n)
        list.insertHead(n)
        cache[key] = n
    }
}
```