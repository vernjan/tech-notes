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
- attributes (for example priority)

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

### Producer-consumer
- can be done with just mutexes but it's wasteful
- to be effective, we need some kind of signalling between threads
    - **wait** on a condition variable
        - while waiting, the mutex is released
        - the mutex is reacquired once the waiting is over
    - **signal** on a condition variable