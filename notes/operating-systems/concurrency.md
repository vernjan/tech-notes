# Concurrency

## Concurrency models
- **multi-process** - easy to program, isolated, big overhead
- **multi-thread**
    - **master-less workers** - "1 request = 1 worker"
    - **boss & workers**
        - boss accepts new tasks (must be fast), then delegate between workers (or pushes into a queue)
    - **pipeline** - task _steps_ are processed by individual threads
- **single-thread** (event loop) - requires asynchronous I/O

## Synchronization mechanism
- mutual exclusion - **mutex**
- waiting for a condition - **condition variables**
    - while waiting, the mutex is released
    - the mutex is reacquired once the waiting is over
- waking up other threads - **signals**

### Critical section
```
lock(mutex) {
    while (!predicate) {
        wait(cond) // mutex is released while waiting (and reacquired just before the wait exits) 
    }
    do_something() // the critical section
} // unlock
signal(any_cond) // in general, signal can be called without holding the mutex (not in Java though)
```

## Synchronization primitives

### Spinlock
- "wait in a loop" - burns CPU cycles
- require hardware support - **atomic instructions** (AI)
    - `test_and_set`, `compare_and_swap`, ...
    - AI bypass caches and goes directly into memory (slow)
- implements (randomized) _delay_ and "double locking" to be more effective

### Mutex
- only one thread at a time is allowed to hold the mutex, others have to wait
    - there is no order guarantee who will acquire the mutex next
- protects a _critical section_
- **attributes**
    - locked?
    - owner
    - blocked_threads
- basic building block for more advanced synchronization constructs

## Synchronization constructs
- mutexes and condition variables are basic building blocks
    - error-prone, lack expressive power

### Semaphores
- initialized with an integer
- incoming thread decrements the integer and enters the block
- if the integer is 0, the incoming threads has to wait until another thread leaves the block (incrementing the integer again)
- good for limiting the number of threads in a critical sections

### Read/write locks
- **read** - shared access, never modify data
- **write** - exclusive access

### Monitors
- takes care of explicit locking and unlocking
- for example Java's `synchronized`

### Barriers
- inverse of semaphores - block until N thread is ready

## Deadlocks
- prevention - avoid cycles in lock dependencies
- sometimes prevention is too costly - detect deadlocks and recover

## Cache coherency
- **cache-coherent** (CC) - hardware makes sure all caches are in sync
    - **techniques**
        - write and update
        - write and invalidate
- **non-cache-coherent** (NCC) - software has to make sure of that

### Caches
- **L1 cache**
    - per core
    - fastest but smallest
- **L2 cache**
    - per core
    - bigger than L1 but slower
- **L3 cache**
    - per CPU (shared among cores)
    - biggest but slowest