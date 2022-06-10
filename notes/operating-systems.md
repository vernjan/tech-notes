# Operating Systems

## Source
- 🎥 [Introduction to Operating Systems](https://learn.udacity.com/courses/ud923) (Udacity)

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
