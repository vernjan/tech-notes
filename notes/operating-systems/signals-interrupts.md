# Signals & Interrupts

## Interrupts
- external event/signal from a hardware device (disk, network interface, ..) to CPU
- defined on hardware level
- handled by OS
- (temporarily) suspend the current execution and trigger _interrupt handler_

## Signals & Traps
- event/signal from a process or OS to other process (`SIGKILL`, `SIGSEGV`, ..)
- form of inter-process communication (IPC)
- `kill` - utility for sending signals
- processes register signal handlers (default handlers exist)
    - synchronous - user code is suspended
- signals defined by [POSIX](https://en.wikipedia.org/wiki/Signal_(IPC)#POSIX_signals)
    - SIGINT - `ctrl + c`
    - SIGKILL
    - SIGSEGV
    - SIGHUP (nohup)
- signals can be filtered using _signal mask_