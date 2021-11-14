# Caching

Caching is used to speed up systems in various ways, reducing latency by storing the result of previous requests or expensive computations.

- Caching can be done in hardware or software.
- Can be client-side, server-side or anywhere inbetween various systems including the DB
- Client-side can be used to reduce network requests
- Server-side can be used to reduce computational loads
- A cache over the DB can reduce DB reads
- Hashes of incoming requests can be stored in a key/value store like Redis, and data returned without hitting a DB.

## Consistency
One pitfall with caching is that there can be two or more sources of truth! There are various ways to tackle this:

**Write-Through Caching**
- Edits to data (say a Facebook post) are written to the cache, then the database, then returned to the user
- However, we still have to go to the DB! We haven't reduced writes or decreased latency

**Writeback Caching**
- Edits to data update the cache and data is returned to the user
- The cache is out of sync with the database
- Later on, we asynchronously write this data to the database, grouped with other transactions
- This can be done on a schedule basis, or when the cache is full

The downside with this is that if the cache hasn't been written to the database yet and we lose the cache, we also lose all of the transactions!

## Stale Data
Data can end up stale when a cache is _behind_ the source of truth or other caches.

This may or may not be acceptable in some cases - view counts on YouTube videos for instance are probably absolutely fine to be stale sometimes.

## Cache Hits/Misses
A cache **hit** is where data is found in the cache.

A cache **miss** is where data isn't found - typically this is a sign that something has gone wrong. An example of this is a server being down, requiring a load balancer to hit a different server, likely resulting in a cache miss.

## Eviction Policies
This is also critical when caching - we cannot store infinite data.

- How do you get rid of old or stale data?
- LRU (Least Recently Used) caches are popular
- Least Frequently Used caches are also a thing - for instance the Instagram profile of a famous person is probably quite high in an LFU cache
- FIFO/LIFO caching
