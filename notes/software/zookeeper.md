# ZooKeeper
- used by Kafka, Hadoop, HBase, ...
- alternatives - etcd
- in a nutshell, it's a **distributed file system** (tree structure)
    - strong consistency
    - dir/file - **zNode**
        - persistent or ephemeral (deleted when client disconnects)
        - can store data
        - can be watched for changes
        - can't be renamed
    - path - **zPath**
- **API** - primitive operations
    - create, delete, exists
    - setData, getData
    - getChildren
- **use cases**
    - distributed configuration management
    - naming registry
    - locks
    - key-value store
    - leader election
    - crash detection

## Sources
- [ZooKeeper explained](https://www.youtube.com/watch?v=gZj16chk0Ss) (YouTube)