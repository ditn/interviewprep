# Strong vs Eventual Consistency

We aim for transations to be ACID, that is:

- **Atomic** - transactions either succeed or fail, there should be no inbetween state
- **Consistency** - a transaction cannot bring a database into an invalid state
- **Isolation** - execution of multiple transactions concurrently will have the same affect as if they had been executed sequentially
- **Durability** - any committed transaction is written to non-volative storage. It cannot be undone by a crash, power loss, network partition etc.

## Strong Consistency
Usually refers to ACID transactions.

## Eventual Consistency
A model where reads of a system might return stale data. Generally, an eventually consistent datastore will give guarantees that the datastore will eventually reflect writes within a given period. This could be 10 seconds, or it could be several minutes.