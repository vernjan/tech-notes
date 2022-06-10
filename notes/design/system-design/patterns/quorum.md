# Quorum
> minimum number of nodes on which a distributed operation needs to be performed successfully

- **write quorum** - number of ACKs to consider write a success (`w`)
- **read quorum** - number of responses to consider read consistent (`r`)
- **read-after-write consistency** - clients see their own writes = **strong consistency**
    - `n` all replicas
    - if `r + w > n` (for example n = 3, w = r = 2)
- configuration of `n, w, r` is a tradeoff between latency and consistency
    - `w = n, r = 1` - optimized for fast reads
    - `w = 1, r = n` - optimized for fast writes
- reads can tolerate `n - r` unavailable replicas, writes `n - w`