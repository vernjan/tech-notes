# CAP Theorem
- **TL;DR** - distributed systems choose between consistency (`CP`) and availability (`AP`) (you can't have both)
- **C - consistency**
    - all nodes see the same data simultaneously
- **A - availability**
    - system remains operational all the time
    - no guarantee that the response will be the most recent write operation
- **P - partition-tolerance**
    - system does not fail, regardless of whether messages are dropped or delayed between nodes
    - a must-have for distributed system - therefore the choice is really between consistency and availability

## PACELC
- extension to CAP
- if the system is partitioned (ongoing network issue), we choose between availability or consistency (**CAP**)
- if the system is NOT partitioned (normal situation), we choose between latency and consistency  (**PACELC**)
    - `Partition: Availability or Consistency, Else: Latency or Consistency`