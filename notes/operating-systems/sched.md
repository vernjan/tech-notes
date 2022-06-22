# Sched

0-100 - real-time scheduler
100-139 - CFS

CFS
- one red-black tree (self-balancing) for all tasks
- schedule the task with least _vruntime_ (the leftmost node, O(1))
- once the currently running task _vruntime_ becomes larger than the leftmost node,
  it's inserted back in the tree
- _nice_ - adjusts how fast _vruntime_ ticks
    - for low priority tasks _vruntime_ ticks faster and thus get less real-time CPU

- **cache affinity** - schedule the same tasks on the same CPU/core
- **NUMA** - non-uniform memory access
    - **multiple memory nodes** - so not just multiple CPUs but also multiple memory nodes
    - access to local memory node is always faster
    - => keep tasks on CPU close to the memory node keeping the task data
- **hyper-threading**
    - single CPU with multiple registers - very fast context switch
    - it virtually presents as 2 (or more) hardware threads but in reality there is only one
- **hardware counters**
    - input for schedulers
    - L1/L2 cache misses, power and energy, IPC, ...
    - **cycles per instruction** (CPI)
      - CPU bound has low count
      - memory bound has high count
