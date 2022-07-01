# Threads
- lightweight process (LWP)
- threads **share process address space** (for example code, data or heap)
    - more memory effective than having multiple processes
    - context switch is much faster
- each thread **has its own**
    - thread ID
    - program counter
    - registers
    - stack & stack pointer
    - attributes (for example priority or stack size)
- `ps -eLf `
    - **LWP** - unique thread identifier inside a process
    - **NLWP** - number of threads for a given process

## Sources
- [Linux Process vs. Thread](https://www.baeldung.com/linux/process-vs-thread)

## Kernel-level vs. user-level threads
- **one-to-one model** - one user-level thread maps to one kernel-level thread
    - expensive (switching from user to kernel mode)
    - OS might have limits on kernel-level threads
    - Java before Loom
- **many-to-one model**
    - thread management is implemented in user space
    - portable - no dependency on kernel details
    - IO operation can block the whole process (i.e. block the kernel thread)
- **many-to-many model** - best of both worlds
    - Java after loom

## Pthreads (POSIX thread)
- see [Pthreads](https://en.wikipedia.org/wiki/Pthreads) on Wiki
- standard API for working with threads
- includes
    - thread management (create, join, ..)
    - mutexes
    - condition variables
    - synchronization
- `trylock` - lock if mutex is free, otherwise return immediately