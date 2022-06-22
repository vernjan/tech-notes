# Memory Management

- processes use **virtual memory**
    - maps into physical memory (RAM, swap, ..)

## Virtual memory
- **page-based**
    - virtual memory is split into **fixed size pages** which maps into physical memory **page frames** of the same size
    - mapping is kept in **page tables**
- **segment-based**
    - virtual memory is split into **dynamically sized segments**
    - mapping is kept in **segment registry**
- supported by CPU hardware
    - **memory management unit** (MMU) - address translation, access control
    - **special registers** - direct access to memory
    - **translation look-aside buffer** (TLB) - cache
- lazy allocation of physical memory (_on first touch_)
- multiple processes can share the same portions of physical memory
    - **copy on write** (COW) - lazy copying, at first just point to the same physical memory and make a real
      copy only if there is a write request

### Page tables
- per process (i.e. must be context switched - updating `CR3` register on x86)
- hold just the first page, rest can be computed using offsets
    - for example just the start of an array
- typical page size is 4 kB
    - large pages - 2 MB
    - huge pages - 1 GB
- **hierarchical** - a flat structure would use too much space (especially on 64-bit)
- page pinning - the page can't be swapped out of the main memory

### Page table entry
- **structure**
    - physical page frame
    - **flags**
        - present - lazy allocation
        - dirty (for caching)
        - R/W permission
        - user/kernel mode access
- used by MMU (translation, access control)
    - **MMU generates traps (interrupts) for kernel**
    - for example handling page faults
        - allocate page
        - SIGSEGV

## Memory allocation
- determines virtual memory to physical memory mapping
- **kernel level** - static process state
    - buddy and slab allocator
- **user level** - dynamic process state (heap)
    - malloc/free