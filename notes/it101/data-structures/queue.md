# Queue (FIFO)
- maintains order
- fast insert/delete `O(1)` (enqueue/dequeue)
- no access by index
- used for **breadth-first search**, resource sharing (synchronization), scheduling
- implemented by array, linked list, or even a stack
    - 2 pointers - front and rear (same for deque)

## Priority queue
- sorted in a specific order
- usually implemented by heap, or by binary search tree or linked list
- used in operating systems to determine which programs should be given more priority
- **operations**
    - insert with priority
    - dequeue the highest priority

## Double-ended queue (deque)
- elements can be added to or removed from either the front (head) or back (tail)
- linked list with tail
- used by work stealing algorithms

## Circular queue (ring buffer)
- connected end to end
- if full, the oldest data might be overwritten
- used for buffering