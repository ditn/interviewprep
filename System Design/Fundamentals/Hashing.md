# Hashing

Hashing is often used to help balance traffic loads. This can be done by computing a hash of:
- The client IP
- The user ID
- Or any other thing which makes sense for the problem you're solving

Hash functions could naively work like the hash functions used in storing/retrieving items in [[Hash Table]] data structures.

`input -> number % server count -> server index`

However this would mean that spinning up new servers due to traffic, or a server going down, would result in a complete re-compute of all indexes, resulting in client traffic hitting entirely new servers and a tonne of cache misses.

# Consistent Hashing
This is a type of hashing that minimises the number of remapped keys when a server is added or removed. This therefore minimises the number of requests which end up hitting new servers.

This is implemented in a closest-neighbour way - it can be thought of as distributing traffic across a circle or a hash ring.

# Rendezvous Hashing
This type of hasing is also known as "highest random weight" hashing.

1) Calculate a score for each of your servers
2) Pick the highest one
	1) If your server goes down, pick the second highest
	2) If a new server is added, it doesn't affect you
	