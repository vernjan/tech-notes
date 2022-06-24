# Inter-Process Communication
- transfer data between address spaces
- shell command `ipcs`

## Message passing
- OS maintains the channel and provides the interfaces for send/recv via system calls
- simple to use but comes with overhead because of frequently entering the kernel mode (syscalls) and data copying

### Pipes
- specified by POSIX (shell `|`)
- carry byte stream between only 2 processes

### Message queues
- **sockets**
    - ports
    - also works between machines (TCP/IP)
    - syscalls `socket()`, `send()`, `recv()`

## Shared memory IPC
- specified by POSIX or SysV ("System 5")
- virtual memory of multiple processes map into the same physical memory
- generally faster - once established, kernel is not directly involved
- programmer is responsible for the protocol and communication

