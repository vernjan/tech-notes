# Signals & Interrupts

## Interrupts (traps)
- external events (from network, disk IO, ..) to CPU
- defined on hardware level
- handled by OS
- (temporarily) suspend the current execution and trigger _interrupt handler_

## Signals
- events from processes or OS to other processes (SIGKILL, SIGSEGV, ..)
- form of inter-process communication (IPC)
- `kill` - utility for sending signals
- processes register signal handlers (default handlers exist)
- defined by [POSIX](https://en.wikipedia.org/wiki/Signal_(IPC)#POSIX_signals)
    - SIGINT - `ctrl + c`
    - SIGKILL
    - SIGSEGV
    - SIGHUP (nohup)
- signals can be filtered using _signal mask_