# System Design

- [API gateway](api-gateway.md)
- [Caching](caching.md)
- [CDN](cdn.md)
- [Compatibility](compatibility.md)
- [Data replication](data-replication.md)
- [Estimation](estimation.md)
- [Load balancing](load-balancing.md)
- [Messaging systems](messaging-systems.md)
- [Partitioning](partitioning.md)
- [Scaling](scaling.md)
- [Storage](storage.md)
- [Stream processing](stream-processing.md)
- [System design patterns](patterns/README.md)

## Glossary
- **distributed** - run on multiple machines
- **decentralized** - nodes are identical, no leader-follower paradigm
- **durable** - data is stored permanently

## Problem and solutions
- **partitioning** - consistent hashing
- **high availability for writes** - vector clocks with reconciliation during reads, write back cache
- **handling temporary failures** - sloppy quorum, hinted handoff
- **recovering from permanent failures** - merkle trees
- **membership and failure detection** - gossip protocol