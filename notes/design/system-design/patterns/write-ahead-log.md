# Write-ahead Log (WAL)
- also known as _transaction log_ or _commit log_
- to guarantee durability and data integrity, each modification to the system is first written to an append-only log on the disk
    - writing log is faster than updating all the data in the system
- redo/undo
- Cassandra, Kafka