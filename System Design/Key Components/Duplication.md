# Duplication

The easiest way to add more capacity to a service to add more instances of the service and have a way of routing, or balancing, requests to it. Creating more instances is a fast and cheap way to scale a stateless service, _as long as you have taken into account the impact on its dependencies_.

For instance, adding multiple instances of a service is fine - unless all of them rely on the same datastore. This datastore will rapidly become a bottleneck, and so this will require duplication too.

A critical tool in duplication is the [[Load Balancers]].

## Replication
When the servers involved are stateless, creating new instances and fanning out is simple to achieve. However if there's state involved, it gets much more difficult to handle and there must be some form of coordination involved.

Replication is the process of storing a copy of the same data in multiple nodes of the system. Keeping this data in sync is the tricky part.

### Single Leader Replication
This is the most common approach to the problem, where you elect a leader with multiple followers. Clients write directly to one leader, which updates its local state and then replicates this change to its followers. Typically this is done with the Raft replication algorithm.

At its most basic, replication can happen either fully synchronously, fully asynchronously, or somewhere inbetween.

#### Async
- The leader receives a write request from a client
- The leader asynchronously broadcasts it to the followers and replies to the client
- The leader then responds to the client before the replication has completed

This approach is fast but not very fault tolerant. If the leader crashes before the followers have all updated, and a follower without the correct state is promoted to leader - you're in trouble. This is a terrible tradeoff.

There's also a lack of strong consistency here, where a successful write might not be visible by some or all replicas.

#### Sync
This requires leaders to wait for all replicas to finish writing before telling the client that the request has been successful.

There is obviously a performance penalty here - the entire request is only as fast as the slowest replica. If a replica is down, then the entire system won't respond - and the more followers/replicas there are, the more likely it is that this will happen.

As you can see, fully async or fully sync are extremes that have high tradeoffs. Most datstores use some combination of the two strategies.

#### Multi-Leader Replication
In this strategy, there is more than one node that can accept writes. This strategy is often used when the write throughput is too high for a single machine to handle, or when the leader needs to be highly geographically available.

The replication between leaders happens asynchronously. This means that there can be conflicts between two leaders, as they might have differing data due to data being updated concurrently between them. To resolve these conflicts, there has to be a resolution strategy.

The simplest solution is to avoid the need for multiple leaders in the first place. For example, if European requests are router to a European data centre, that centre can have a single leader and no conflicts. The leader could go down, but you can also have a backup in the same region.

If this isn't possible then conflicts are inevitable. One way to fix conflicts when updating a record is to store the conflicting writes and return them to the next client that reads the record. The client then has to resolve the conflict and update the datastore with the resolution.

Alternatively, the data store could allow clients to upload a conflict resolution procedure, which can be executed by the datastore when a conflict is detected.

The datastore could also leverage data structures which provide automatic conflict resolution, such as CRDTs.

#### Leaderless Replication
Imagine a world where any replica could accept writes from any clients - no leaders, and conflict resolution is offloaded to clients.

This is used in Dynamo-style datastores, and is even more complex than multi-leader replication.