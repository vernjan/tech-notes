# NoSQL

## Sources
- [System design fundamentals: What is the CAP theorem?](https://www.educative.io/blog/what-is-cap-theorem) (Educative blog)
- [MongoDB vs PostgreSQL: What to consider when choosing a database](https://www.educative.io/blog/mongodb-versus-postgresql-databases) (Educative blog)
- [MongoDB vs MySQL: Which database to use](https://www.educative.io/blog/mongodb-vs-mysql) (Educative blog)
- [What are ACID properties in a database?](https://www.educative.io/edpresso/what-are-acid-properties-in-a-database) (Educative edpresso)
- [Cassandra vs. MongoDB](https://www.youtube.com/watch?v=3z2EzILA3Rk) (YouTube Jelvix)
- [Graph Databases for Beginners: ACID vs. BASE Explained](https://neo4j.com/blog/acid-vs-base-consistency-models-explained/) (Neo4j blog)
- [Wide-column Database](https://www.scylladb.com/glossary/wide-column-database/) (ScyllaDB glossary)

## SQL vs. NoSQL

|                   | SQL                 | NoSQL                                                    |
|-------------------|---------------------|----------------------------------------------------------|
| Data model        | tables              | documents, key-value pairs, graphs, columns, time-series |
| Data structure    | pre-defined schema  | no schema (or dynamic schema)                            |
| Data              | normalized (FKs)    | denormalized (duplicated) - no joins                     |
| Scalability       | vertical            | horizontal                                               |
| Query language    | SQL                 | programming languages (like JS, Python) or specific QLs  |
| Design properties | ACID (transactions) | BASE (eventual consistency)                              |

### When to use SQL
- if you need strong consistency and transactions (ACID)
- if your data is nicely structured
- if you don't need to scale massively
- stock trading, personal banking, ...

### When to use NoSQL
- if you need to handle a large number of read-write operations (big data)
- if schema is evolving
- if you don't mind eventual consistency (BASE)
- if you want to prototype (rapid development)
- if you need zero downtime

### Polyglot persistence
- each microservice has its own database (SQL or NoSQL)

## Consistency models

### ACID
- atomicity, consistency, isolation, durability
- common for relational databases
- reduces anomalies and protects data integrity
- locking is required (might be heavy-weight)

### BASE
- **B**asic **A**vailability - always returns a response
- **S**oft state — system can change over time, even during times of no input (due to eventual consistency)
- **E**ventual consistency - the data will spread to every node sooner or later
- looser than ACID
- Cassandra, Rika, Voldemort
    - on the other hand, those systems prefer consistency to availability - Redis, HBase, ZooKeeper

## Data models

### Key-value
- primary key access - low latency `O(1)`
- Redis, AWS DynamoDB, memcached
- good pick for
    - caching
    - user state or sessions
    - real-time data

### Document
- good pick when
    - working with semi-structured data (JSON)
    - need for flexible schema
    - high scalability and availability
- MongoDB, CouchDB, Amazon DocumentDB, Elasticsearch

### Graph
- good for complex relationships
    - social network, maps, recommendation systems
    - page rank
- Neo4j

### Time-series
- tracking (and aggregating) time based data (metrics)
    - IoT, sensors, stock market, self-driving vehicles, ...
- Prometheus, InfluxDB

### Wide-column
- a bit similar to relational, but without fixed schema
    - rows can have arbitrary number of columns (even billions)
    - columns can be added/removed without affecting other rows
    - "multi-level sorted map" (`Map<String, Map<String, Object>>`)
- handle massive amounts of data, technically called Big Data
- perfect for analytical use cases
- Cassandra, HBase, Google BigTable, ScyllaDB

### Multi-model
- Cosmos DB