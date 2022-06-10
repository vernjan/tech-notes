# Cache
- web browser, DNS, CPU, application, memoization, disk, OS, database, CDN, ...
- improves latency, decreases the load and helps with HA (at least temporarily)
- caching a copy or pre-calculated data
- distributed cache - [Consistent hashing](patterns/consistent-hashing.md)
- coherency - caches are in sync

## Sources
- [Caching Strategies and How to Choose the Right One](https://codeahoy.com/2017/08/11/caching-strategies-and-how-to-choose-the-right-one/) (Medium blog)
- [Caching patterns](https://www.educative.io/edpresso/caching-patterns/) (Educative edpresso)

## Cache strategies

### Cache aside
- app checks cache
    - if hit, then return data from cache
    - else the app fetches the data from database, updates the cache and returns the data
- cache is lazy loaded (consider pre-warming)
- good for read heavy workloads
- Redis, memcached
- pros
    - cache failure might not be fatal
    - cache and database model can differ
- cons
    - cache and database must be kept in sync

### Read through
- app reads from cache, cache reads from database
- cache is lazy loaded
- good for read heavy workloads
- pros
    - app requires no extra logic, caching is transparent
- cons
    - cache failure might be fatal
    - cache and database model cannot differ
    - cache and database must be kept in sync

### Write through
- app writes to cache, cache writes to database
- usually combined with read-through cache as it's useless on its own
- pros
    - guarantees consistency between cache and database
- cons
    - adds extra latency

### Write back (or write behind)
- app writes to cache, cache immediately acknowledges writes and later (asynchronously) writes to the cache
- good for write heavy workloads
- pros
    - can tolerate some database downtimes
- cons
    - cache failure might be fatal

## Cache eviction
- **FIFO** - first in, first out (queue)
- **LRU** - least recently used
- **LFU** - least frequently used