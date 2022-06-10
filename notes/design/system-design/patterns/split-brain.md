# Split Brain
- 2 leaders at the same time
- can happen when the original leader becomes unavailable for some time, a new leader is elected, and then the original leader recovers
    - the recovered leader is called **zombie leader**
- we must prevent split brain

## Solutions
- ask the majority quorum for approvals before each command, or
- **generation clock** - logical clock, value is increased after each election, only the latest value is accepted
    - value must be included in each request
    - requires a shared database to check against (ZooKeeper in Kafka)