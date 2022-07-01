# Distributed systems
> system running on multiple nodes connected via a network

- **classic concurrency** - threads in a process
    - communication via shared memory
- **distributed system** - processes on multiple nodes
    - communication via unreliable network
    - thousands, perhaps millions of nodes, thousands of petabytes - pretty much no limits!

## Sources
- [Distributed Systems lecture series](https://www.youtube.com/playlist?list=PLeKd45zvjcDFUEv_ohr_HdUFe97RItdiB) (YouTube Martin Kleppmann)
- [A Thorough Introduction to Distributed Systems](https://www.freecodecamp.org/news/a-thorough-introduction-to-distributed-systems-3b91562c9b3c/) (freeCodeCamp blog)

## Pros & Cons

### Pros
- **availability and reliability**
    - fault-tolerance
    - updates without downtime
- **performance**
    - scale at exponential rates
    - low latency (geolocations)
    - parallel processing

### Cons
- network is unreliable, nodes may crash
- coordination is hard

## Use cases
- distributed storage (databases)
- distribute file systems (GFS, HDFS)
- distributed computing (MapReduce)
- distributed messaging (RabitMQ, Kafka)
- distributed applications (BitTorrent, Bitcoin)

## System model

### Network behavior
- message loss
- _network partition_ - some links dropping all messages for extended period of time
- 3 levels
    - **reliable**
    - **fair-loss**
        - messages might be loss, but they will eventually get through (retries)
        - closed networks
        - --> **use retry + dedup to make it ^^**
    - **adversary**
        - someone intentionally dropping or spoofing the messages
        - public Internet, public Wi-Fi
        - --> **use TLS to make it ^^**

### Node behavior
- node crashes at any time
- 3 types
    - **crash-stop** - never recovers from crash, permanent damage
    - **crash-recovery** - loss of memory
    - **Byzantine** - malicious, for example P2P model

### Timing behavior
- latency
- 3 choices
    - **synchronous** - latency has a defined upper bound
    - **partially synchronous** - switch between synchronous and asynchronous, closest to reality
    - **asynchronous** - no guarantees about latency

## Networking
- node A sends a message to node B over network
- latency
    - same datacenter ~1 ms
    - across continent ~100 ms

## Thought experiment
- in reality, we face both below described issues

### Two generals problem
- must attack at the same time
- can't communicate directly, only via unreliable messengers
    - General A sends a messenger but never receives the response. What happened?
        - messenger didn't arrive to general B
        - messenger arrived to general B but didn't come back
    - Even if messenger successfully returns to general A, general B can't know that.
    - This is infinite loop no matter how many times the messenger travels... General are never certain the latter will also attack.
- no common knowledge

### Byzantine generals problem
- 3 or more generals
- assumption - messaging is reliable
- some generals are traitors (`x`) - can lie and change messages
- honest generals must agree on a plan
- we need at least `3x + 1` generals in total to overcome the traitors

## Time and clocks

### Time
- **Greenwich Mean Time** (GMT) - astronomical time, bound to Earth rotation
    - Earth rotation is not so precise, for example earthquakes cause slight drifts
    - also a time zone
- **International Atomic Time** (TAI) - based on multiple atomic clocks
    - currently, ~37 seconds ahead GMT
- **Coordinate Universal Time** (UTC) - compromise between GMT and TAI
    - TAI is more precise, but we want to stay in sync with Earth rotation
    - **leap seconds** - every year on 30 June and 31 December at 23:59:59 UTC, one of below happens (announced beforehand)
        - negative leap second
        - no change
        - positive leap second
    - computers use _smear_ leap seconds - spread the leap second into a couple of hours
- Unix epoch time ignores leap seconds

#### Leap year
    - `% 400 == 0 --> YES`
    - `% 100 == 0 --> NO`
    - `% 4 == 0 --> YES`

### Clocks
- **physical clocks** - count number of seconds elapsed
    - quartz clock - common in computers, precision depends on, among other things, temperature
    - atomic clock - much more precise, much more expensive
        - caesium-133 resonates `9,192,631,770` times per second (`~9 GHz`)
- **logical clocks** - count events, e.g. messages sent
    - increase is always positive
    - in distributed systems, each process has its own clocks
    - Lamport clocks, vector clocks

### Clock synchronization
- **clock skew** is inevitable using quartz clocks, never rely on timestamps
- NTP - network time protocol
    - server has precise time (atomic clock, GPS)
    - clients synchronize with the server
        - the tricky part is that it happens over network
    - given good network conditions, the skew is a few milliseconds
    - correcting clock skew
        - `< 125 ms` - **slew** the clock - slightly speed up or slow down the client's clock until they are in sync
        - `> 125 ms && < 1000 s` - jump, reset the clock - hopefully, this happens just initially
            - `System.currentTimeMillis()` in Java is not **monotonic**! Never use it for measuring elapsed time
            - use `System.nanoTime()`
        - `> 1000 s` - panic, human has to resolve it

### The happens-before relation (`->`):
- event `a` happens before event `b` iff:
    - events occurred at the same node (and thread) and `a` occurred before `b`
    - event `a` is _sending a message_ and event `b` _receiving the same message_
    - transitivity - there exists event `c` which `a -> c` and `c -> b`
- partial order, if we can't establish the HB relation, then events are _concurrent_ (`a || b`)

### Lamport clocks
- each node has its own clock `t`
    - `t` starts at `0`
    - new events increment `t` by 1
        - i.e. we can associate the value of `t` to each event, written as `L(event)`, think "Lamport timestamp"
    - when sending a message, increment `t` by 1 and attach it to the message
    - when receiving a message, choose `max(t, t')` and increment by 1
- if `a -> b` then `L(a) < L(b)` - but the converse is not true!
- if `L(a) < L(b)` then NOT `b -> a` - doesn't really mean `b` couldn't happen before `a` but there is no happens before relation
- node name + `L(event)` is a unique ID

### Vector clocks
- see [vector clocks](system-design/patterns/vector-clocks.md)

## Broadcast protocols
- one node sending message to many (all) others
- different "levels of quality"
    - **best-effort broadcast** - no guarantees
    - **reliable broadcast** - messages are always (eventually) delivered
    - **FIFO broadcast** - messages sent from a single node must be delivered to other nodes in order
    - **casual broadcast** - messages sent from different nodes (assuming happens before relations between them) must be delivered in order
    - **total order broadcast** (atomic broadcast) - all messages are delivered to all nodes in the same order

### Reliable broadcast
- requires retries and deduplication
- the node may crash in the middle of broadcasting - how to fix?
    - **eager broadcast** - everytime a node receives a message for the first time, re-broadcast it
        - works, but `O(n^2)`
    - **gossip** - forward message to 3 random nodes, after a few rounds, there is high probability all nodes were reached

## Replication
- replicas periodically communicate among themselves to check for inconsistencies (**anti-entropy protocol**)
- see [tombstones](system-design/patterns/tombstones.md)
- **idempotence** - `f(x) = f(f(x))`

### Broadcast QoS
- **total order**
    - aka **state machine replication** - all operations are replicated in the exact same order, therefore all replicas end up in the same state
    - fully deterministic
    - SQL database leader replication to followers (transactions)
- **causal** - deterministic if concurrent updates are commutative
- **reliable** - deterministic if all updates are commutative

### Retry semantics
- **at-most-once** - send request, don't retry
- **at-least-once** - retry until acknowledged
- **exactly-once** - retry + idempotence or deduplication

### Resolving concurrent writes
- **last writer wins** (LWW)
    - use timestamps to determine total order (e.g. Lamport clocks)
    - we can lose data - the total ordering is arbitrary for concurrent events
- **multi-value register**
    - use timestamps with partial order (e.g. vector clocks)
    - preserve both values for concurrent events - the conflict must be resolved somehow
- conflict-free replicated data types (CRDTs)
    - concurrent changes can be applied in any order and will produce the same end result

### Fault tolerance (consistency)
- see [quorum](system-design/patterns/quorum.md), [hinted handoff](system-design/patterns/hinted-handoff.md) and [read repair](system-design/patterns/read-repair.md)

#### Consistency models
- see https://en.wikipedia.org/wiki/Consistency_model
- **strong**
    - reads always return the latest writes (client never sees stale data)
    - not ideal for HA
    - low performance
    - **strict** - total order is preserved, impractical
    - **sequential** - total order not required, however all clients must see the same order
    - **casual** - preserve order of somehow connected operations (respect causality)
- **weak**
    - need to use **synchronization operations** - `sync`
        - to make changes visible
            - modifying node has to call `sync` after the changes (make them visible)
            - reading node has to call `sync` to see the changes
    - **eventual**
        - given enough time, all updates are propagated and replicas are consistent
        - high performance, high availability
        - AWS Dynamo, Cassandra

## Consensus
- several nodes want to come to agreement about a single value - it's rather tricky
    - used for replicating machine states - must have for distributed systems
- protocols (algorithms)
    - **Raft** - etcd (distributed key-value store)
    - **Paxos** - Google
    - **Zab** - Zookeeper
    - those protocols don't assume malicious nodes, so for example Bitcoin (runs on public network) is using a different consensus protocol

### Leader election
- see [split brain](system-design/patterns/split-brain.md)
- requires majority quorum

### Raft
- [The Raft Consensus Algorithm](https://raft.github.io/)
- Replicated And Fault Tolerant
- node roles
    - **follower** - after (re)start
    - **candidate** - when a follower suspects leader failure
    - **leader** - candidate receives votes from quorum

## Replica consistency
- **distributed transactions** - updating data on multiple nodes
    - all nodes must commit, or all must abort
- **atomic commit** - similar to consensus but all nodes vote (not just majority) and decide unanimously

### Two-phase commit (2PC)
- guarantees atomicity (across shards/nodes)
- don't confuse with **Two-phase locking** (guarantees _serializability_, not atomicity)
- transaction commits go through **coordinator**
- coordinator asks everyone (_the cohort_) to prepare the commit (do all work, do all checks) and then vote yes/no
- cohort waits for coordinator's decision (commit or rollback)
- cohort acknowledges commit or rollback
- risk of deadlocks - coordinator waits for cohort votes and cohort waits for coordinator's decision
    - cohort can't make any individual decisions - risk of breaking the consistency
- fault-tolerant variant uses total order broadcast

## Consistency models

### Linearizability
- informally _strong consistency_
- strongest consistency model - multiple replicas behaves as if there is only a single replica
    - applies to concurrent programming as well
    - always return "up-to-date" value for all clients - if client A writes a new value, client B must see it in real time
- **how to achieve**
    - majority quorum + read repairs
- don't confuse with _serializability_
    - transaction isolation where transactions have the same effect as if they were executed in a serial order
- easy to use by applications but performance and availability suffers
- relies on total order broadcast

#### Compare and swap
- atomic instruction built in CPU
- `CAS(x, old, new)` - set `x` to `new` iff `x == old`

### Eventual consistency
- weaker consistency model
- replicas process operations based on their local state (no need for quorums)
    - can work without network communication
- replicas reach the same state _eventually_
- relies no causal broadcast
- conflicts need to be resolved

## Real-world examples

### Collaboration software
- calendar, Google Docs
- each user has local replica
- replica can be updated offline
- solution
    - CRDTs
        - **state based** - merging full structures
            - such as maps (key-value + timestamp)
        - **operation based** - merging just operations
            - such as update key 1 and remove key 2

## Google's Spanner
- millions of nodes, petabytes of data, distributed world-wide
- serializable, linearizable
- uses MVCC - we need to capture happens-before relationship
    - **TrueTime** - works with physical time
        - synced every 30 seconds with atomic clocks
        - probabilistic - earliest and latest timestamp (worst delta ~6 ms)
        - transactions wait for delta to ensure happens-before relationship
