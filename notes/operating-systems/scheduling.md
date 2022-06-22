# Scheduling
- **task** = process or thread
- schedule both **kernel** and **user-level threads**
- picks one task from the **ready queue**
    - new tasks (fork, exec)
    - after IO completes
    - after interrupt
- **triggered when**
    - CPU becomes idle
    - timeslice expires
    - synchronization - waiting for a lock
    - new task arrives
- mutexes can change tasks priority
    - a task holding a lock should be temporarily given a higher priority if there is another task waiting for that lock

## Types of schedulers
- **FIFO** - simple
- **shortest tasks first** - ordered queue, maximize throughput
    - it's hard to estimate tasks length
- **timeslicing**
    - **timeslice** - maximum time of uninterrupted CPU time
    - allows short task to finish quickly without knowing the tasks length
    - important for CPU bound tasks
    - comes with context switching overhead
    - longer timeslice - better CPU utilization but worse liveness

### Preemptive scheduling
- scheduler can interrupt a running task

## Scheduling process
1. context switch
2. enter user mode
3. set program counter
4. go

## Metrics
- **throughput**
- **avg. wait time** = how long a task spends on average waiting in the queue
- **avg. completion time** = avg. wait time + avg. process time

## Multi-level feedback queue
- multiple scheduling policies based on the task priority (queue level)
- scheduler keeps a **multi-level queue**
    1. highest priority and the shortest timeslices - new and I/O bound tasks (based on historical data)
    2. medium priority - mixed tasks
    3. low priority and the longest timeslices - CPU bound tasks

### How it works
- new tasks start with a high priority
    - if they use the whole timeslice (i.e. they are likely not I/O bound), they are moved into medium priority queue,
    - and so on
    - on the other hand, if a low priority task is yielding CPU due to I/O, its priority is boosted again
    - self-regulating mechanism

## Linux schedulers

### O(1)
- preemptive
- priority based
- multi-level (140 levels)
    - **0-99** - real-time tasks
        - 0 is the highest priority
    - **100-139** - use-level tasks
        - default is 120
        - **nice** from -20 to 19
- feedback based - priorities (and timeslices) are dynamically adjusted
- no longer used/default

### Completely fair scheduler (CFS)