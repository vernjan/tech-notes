# P1L2: Introduction to Operating Systems

## Core principles
- a layer between user applications and hardware
- **abstraction** - hides HW complexity
- **coordination** - resource management and process isolation

## Architecture
- **monolithic** - one big ball
    - complex, possibly faster than modular
- **modular** - level of indirection, better maintainability
- **microkernel** - very small kernel, rest is implemented in the user space
    - small (for embedded devices), but poor portability and complexity of SW development

## User vs. kernel mode
- supported on the HW level (CPU flag)
- switching modes is costly (save & restore states, flushing caches)
- OS exposes **system calls**
    - `open (file)`, `mmap (memory)`, `send (socket)`, ..
- traps
- signals

# POSIX (Portable Operating System Interface)
- [family of standards](https://pubs.opengroup.org/onlinepubs/9699919799/) for maintaining compatibility between operating systems
- defines both the system and user-level API
    - processes
    - signals
    - pthread
    - shell utilities
    - file system layout
    - shell
    - environment variables
    - ...