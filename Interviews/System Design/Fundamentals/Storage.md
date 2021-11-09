# Storage

The predominant storage solution for systems design is a **database**. These come in many forms, each one optimised for different things - certain guarantees about your data, speed, consistency etc.

- Databases, at the end of the day, are just servers
- This means that _persistence_ is something that we have to think about
- If the power goes down and you're executing transations to RAM - that data is lost forever
- However, writing to disk for guaranteed persistence is extremely slow (see [[Latency and Throughput#Comparisions]])
- Writing to SSD is quicker, but much more expensive and may not be ideal for situations where lots of writes occur

Remember that there are distributed databases - how are these managed? How is data sharded?

## SQL vs NoSQL

1.  SQL databases are relational, NoSQL databases are non-relational.
2.  SQL databases use structured query language and have a predefined schema. NoSQL databases have dynamic schemas for unstructured data.
3.  SQL databases are vertically scalable, while NoSQL databases are horizontally scalable.
4.  SQL databases are table-based, while NoSQL databases are document, key-value, graph, or wide-column stores.
5.  SQL databases are better for multi-row transactions, while NoSQL is better for unstructured data like documents or JSON.