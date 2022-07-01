# Introduction to Operating Systems
- a layer between user applications and hardware
- **main responsibilities**
    - resource management (CPU, memory, devices)
    - multi-tasking and process isolation
    - hide hardware complexity

## Architecture
- **monolithic** - one big ball
    - complex, possibly faster than modular
- **modular** - level of indirection, better maintainability
- **microkernel** - very small kernel, rest is implemented in the user space
    - small (for embedded devices), but poor portability and high complexity of SW development

### User vs. kernel mode
- supported on the hardware level (CPU flag)
- switching modes is costly (save & restore states, flushing caches)

## API
- [system calls](https://man7.org/linux/man-pages/dir_section_2.html)
    - `open (file)`, `mmap (memory)`, `send (socket)`, ..
- interrupts
- signals & traps

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
    - and so on