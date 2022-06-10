# Tombstones
- equivalent to **soft delete**
- Cassandra
- items are not really removed, just **marked as removed**
    - it's fast - no need to seek and delete, just append new data (sequential writes are fast)
    - necessary for resolving potential conflicts - imagine a node was done and missed a delete request 