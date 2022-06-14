# Processes and Process Management
- **process** - instance of an executing program
- **address space** - process is mapped into memory
    - addresses are _virtual_ (decoupled from physical memory - see TODO)
    - static parts
        - text and code
    - dynamic parts
        - stack and heap

## Sources
- [Difference between fork() and exec()](https://www.geeksforgeeks.org/difference-fork-exec/) (GeeksForGeeks)
- [Differences between fork and exec](https://stackoverflow.com/questions/1653340/differences-between-fork-and-exec) (Stack Overflow)

## Process control block
- OS keeps track of ... for each process
    - registries
        - PC - program counter
        - stack pointer
    - memory mappings (virtual to physical)
    - list of open files
- PCB is updated everytime a process gives up the CPU (a _context switch_)

## Context switch
- switching the CPU between processes
- costly
    - store & load PCB
    - cold cache

## Process lifecycle
![](_img/process-lifecycle.png)

**Source**: Introduction to Operating Systems (Udacity)

## Process creation
- initial (root) process(es)
- parent-child hierarchy
- parent of all processes (UNIX) - **init** (process 1)
- **fork**
    - duplicates the parent process (copies the parent's PCB) but with new process ID
    - both parent and child continues with the next instruction after fork
        - in code, call to _fork_ returns 0 in the new child process and child's PID in the parent process
- **exec**
    - loads a new program (replaces the current) and starts from the first instruction
- the typical pattern is to first call _fork_, then _exec_

## CPU scheduler
- picks one _ready_ process to run, and for how long
- OS must
    1. _preempt_ - interrupt and save the current context
    2. _schedule_ - OS run the CPU scheduler
    3. _dispatch_ - dispatch a process and switch into its context

## Inter process communication (IPC)
- transfer data into/between address spaces
- techniques
    - **message passing** through a shared buffer (system calls send/recv)
    - **shared memory** - virtual addresses from different processes point to the same physical memory