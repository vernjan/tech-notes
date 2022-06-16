# Threads and Concurrency
- each thread **has its own stack and registers**
- threads **share process address space** (like code and data)
    - more memory effective than having multiple processes
    - context switch is much faster

## Thread
- thread ID
- program counter
- stack & stack pointer
- registers
- attributes (for example priority or stack size)

## Synchronization mechanism
- **mutual exclusion** (mutex)
- **waiting** for a condition
- **waking up** other threads

### Mutex
- only one thread at a time is allowed to hold the mutex, others have to wait
    - there is no order guarantee who will acquire the mutex next
- protects a _critical section_
- **attributes**
    - locked?
    - owner
    - blocked_threads
- basic building block for more advanced synchronization constructs

### Producer-consumer
- can be done with just mutexes but it's wasteful
- to be effective, we need some kind of signalling between threads
    - **wait** on a condition variable
        - while waiting, the mutex is released
        - the mutex is reacquired once the waiting is over
    - **signal** on a condition variable

### Readers-writers
- allow multiple readers but only a single writer

## Critical section
```
lock(mutex) {
    while(!predicate) {
        wait(cond) // mutex is released while waiting (and reacquired just before the wait exits) 
    }
    do_something() // the critical section
} // unlock
signal(any_cond) // in general, signal can be called without holding the mutex (not in Java though)
```

## Deadlocks
- prevention - avoid cycles in locks dependency graph
- sometimes prevention is too costly - detect deadlocks and recover

## Kernel-level vs. user-level threads
- **one-to-one model** - one user-level thread maps to one kernel-level thread
  - expensive (switching from user to kernel mode)
  - OS might have limits on kernel-level threads
- **many-to-one model**
  - thread management is implemented in user space
  - portable - no dependency on kernel detail
  - IO operation can block the whole process
- **many-to-many model** - best of both worlds

## Patterns
- **boss & workers**
  - boss accepts new tasks (must be fast)
    - delegate between workers,
    - or pushes into a queue
- **pipeline** - task _steps_ are processed by individual threads

## Pthreads (POSIX thread)
- see [Pthreads](https://en.wikipedia.org/wiki/Pthreads) on Wiki
- standard API for working with threads
- includes
  - thread management (create, join, ..)
  - mutexes
  - condition variables
  - synchronization
- `trylock` - lock if mutex is free, otherwise return immediately