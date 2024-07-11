# Databases

## Sources

- [High-Performance Java Persistence](https://vladmihalcea.com/books/high-performance-java-persistence/) (~461 pages)
- [An Introduction to Transaction Isolation Levels](https://fauna.com/blog/introduction-to-transaction-isolation-levels) (Fauna blog)

## Data

- structured (normalized, relational)
- semi-structured (JSON, XML)
- unstructured (text, audio/video, pdf)

## Object hierarchy

- see https://stackoverflow.com/questions/7022755/whats-the-difference-between-a-catalog-and-a-schema-in-a-relational-database
- database server
    - databases (or catalogs) - isolated, think different apps
        - schemas (or namespaces)
            - tables
                - rows & columns
- fully qualified query is **database.schema.table**

## Connection pooling

- see https://github.com/brettwooldridge/HikariCP/wiki/About-Pool-Sizing
- PostgreSQL recommends
    - `connections = (core_count * 2) + effective_spindle_count`
    - i.e. approx. 10 connections for 4 cores

## Random notes

- normalization vs. denormalization
    - denormalization for performance reasons (optimize read time), especially for read-only data

## Isolation levels

- see https://jepsen.io/consistency
- specify what data is visible to statements within a transaction
- the better isolation, the lower performance
- see https://fauna.com/blog/introduction-to-transaction-isolation-levels

- **serializable**
    - holds R+W locks including ranged locks
    - no anomaly can occur
- **repeatable reads**
    - holds R+W locks excluding ranged locks
    - _phantom reads_ can occur
- **read committed**
    - holds W lock
    - guarantees reading committed data only
    - _non-repeatable reads_ can occur
- **read uncommitted**
    - prevents _lost updates_
    - _dirty reads_ can occur

### Anomalies (read phenomena)

0) **lost update**
    - transactions mutually override data - this is never allowed
1) **dirty reads**
    - a transaction sees not yet committed data of another transaction
2) **non-repeatable reads**
    - transaction A reads data
    - transaction B changes the same data and commits
    - transaction A reads the same data again and sees the new data
    - (in case of serializable isolation, it must still see the original data)
3) **phantom reads** - concerns RANGE queries (i.e. WHERE clause)
    - a transaction sees new row(s) inserted by another transaction

### Hibernate issues

- watch out for N+1 queries
- watch out for very long queries (we had ~11,000 characters long query in Sapho server)
- be careful with eager fetching - usually leads to retrieving more data than (always) required
- anti-patterns
    - Open Session In View (OSIV)
        - https://blog.frankel.ch/the-opensessioninview-antipattern/
        - https://vladmihalcea.com/the-open-session-in-view-anti-pattern/
    - `hibernate.enable_lazy_load_no_trans = true` (by default its `false`)
        - https://vladmihalcea.com/the-hibernate-enable_lazy_load_no_trans-anti-pattern/
        - treats symptoms (suppresses `LazyInitializationException`), ignores root cause, the price to pay is performance

### Auto-commits

- Not good for multiple modifying statements.
    - https://vladmihalcea.com/why-you-should-always-use-hibernate-connection-provider_disables_autocommit-for-resource-local-jpa-transactions/
      https://www.postgresql.org/docs/9.3/static/populate.html#DISABLE-AUTOCOMMIT
      https://dev.mysql.com/doc/refman/5.7/en/optimizing-innodb-transaction-management.html
      https://dev.mysql.com/doc/refman/5.7/en/innodb-autocommit-commit-rollback.html

### Read-only transactions

- switching to read only transactions (https://vladmihalcea.com/spring-read-only-transaction-hibernate-optimization/)
    - no transaction log
    - optimizations in Spring

## Indexes

- see https://medium.com/must-know-computer-science/system-design-indexes-f6ad3de9925d
- B tree - auto-balancing
    - fast access
    - slower insert/update/delete
    - similar to binary search tree but nodes may have multiple values
    - leaf nodes contain pointers to data
- maps the key to physical location
- clustered index
    - only 1 per table
    - matches how data are physically stored

## Partitioning vs. replication

- **partitioning** - different data on multiple nodes
- **replication** - same data on multiple nodes

## Two-phase locking

- see https://vladmihalcea.com/2pl-two-phase-locking/
- guarantees **strict serializability**
- lock types
    - **read or share lock** prevents a resource from being written while allowing other concurrent reads
    - **write or exclusive lock** disallows both read and write operations on a given resource
- two phases
    - expanding - locks are acquired, no locks are released - start of transaction
    - shrinking - locks are release, no locks are acquired - commit or rollback

## MVCC (multi-version concurrency control)

- consistent snapshot - enables read-only transactions without any locking
- every write transaction has associated a **commit timestamp**
- data are not overwritten but kept together with the commit timestamp
- read only transactions simply ignore data with later timestamp
    - honors happens-before relationship

## Transactions

- by default, connections are usually auto-committing
- nested transactions requires **savepoints**

## Views

- **view** - named SQL query / virtual table, data are not stored
- **materialized view** - physical table with data, needs to be updated periodically