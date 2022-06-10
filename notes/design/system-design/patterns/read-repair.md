# Read Repair
- a node has stale data (network partition, it was down for a while, ...)
- this is detected during a read operation (all records has assigned logical clock timestamps)
- client is asked (**read repair** request) to fix the stale data