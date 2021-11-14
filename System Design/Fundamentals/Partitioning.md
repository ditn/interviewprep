# Partitioning

When a dataset can no longer fit in a single node, it must be partitioned. This is a general technique that can be used in a variety of circumstances, such as sharding [[Network Protocols#TCP Transmission Control Protocol]] requests across backends in a load balancer.

## Strategies
When a client sends a request to a service that has been partitioned, the request needs to be routed to the datastore whic holds the data. This is often done using a [[Microservices#The API Gateway]] service which can route the request and knows how to map keys to partitions, and partitions to nodes.

This mapping is normally maintained in a strongly consistent configuration store such as etcd or Zookeeper.

Generally, two strategies for partioning are used:

### Range Partitioning
Data is split into partitions by key range in lexicographical order, and each partition contains a continuous range of keys. The data can be stored in sorted order, making scans very fast.

This doesn't make sense however if the distribution of keys isn't uniform - like much of the English language. Similarly, partitioning by date makes no sense, as recent data ends up in the same place. 

Creating unbalanced partitions can create hotspots in your system, which is likely to cause failures.

### Hash Partitioning
Hashing should alleviate this problem by uniformly distributing keys across partitions. Note that this _doesn't_ eliminate hotspots if the access pattern isn't uniform! If certain keys are accessed more frequently, these be broken down into subkeys.

Modular hashing, where you `mod` the number of servers/datastores/load balancers etc can be extremely problematic when you add or remove more resources. Reshuffling this data is expensive and uses a lot of bandwidth, so it is best avoided.

Ideally, if a partition is added, only $k/n$ keys should be shuffled around, where $k$ is the number of keys and $n$ the number of partitions. 

A hashing strategy that guarantees this is called **Stable or Consistent Hashing**. For more, see [[Hashing]].

One drawback of hash partitioning is you lose the sort order guarantees of range partitioning. However, the data inside each hashed partition can be sorted according to another subkey for quick lookup.