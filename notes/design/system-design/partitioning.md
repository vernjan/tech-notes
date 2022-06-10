# Partitioning (sharding)
- splitting up a DB/table across multiple machines
- partition that receives more requests than others is called a **hot spot**
- see [consistent hashing](patterns/consistent-hashing.md)

## Sources
- [Hazelcast - Sharding](https://hazelcast.com/glossary/sharding/)

## Methods
- **horizontal** (by rows)
    - usually called **sharding**
    - **by key** (hash) - state, tenant
    - **by range** - date, age
    - **by list** - list of countries
- **vertical** (by columns or "features")

## Common issues
- data are not evenly distributed
    - be careful when choosing the partition method
- partition is hot - lots of queries targeting a single partition (_celebrity problem_)
- query requires data from multiple nodes - slow
    - use denormalization
- referential integrity between nodes
    - enforce in application code
- re-balancing
    - consistent hashing
