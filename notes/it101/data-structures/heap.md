# Binary Heap
- root node holds min/max value `O(1)`
- ordered according to the heap property - **min heap** or **max heap**
    - parent node is always greater (or smaller) then the child nodes
- delete/insert `O(log n)`
- building heap `O(n*log(n))` - repeated inserts (so called _heapify_)
    - upper bound, more realistically just `O(n)`
- search `O(n)`
- **get min/max** `O(1)`
- used for implementing
    - priority queues (`PriorityQueue` in Java)
    - Dijkstra's algorithm
    - heap sort
    - finding min/max in arrays

## Implementation
- must be a **complete binary tree**
    - easily implemented by an **array** (there are rules for indexes, see below)
    - parents are in the first half, child nodes in the second half

### Indexes
- `n` is the total size
- root at `0`
- last node at `n - 1`
- last parent at `(2 / n) - 1` - DON'T CONFUSE `n` with `i`!
- parent at  `floor((i - 1) / 2)` - works for both left and right children
- left child at `2i + 1`
- right child at `2i + 2`

## Operations
- **heapify** - the core operation
- **insert** - add new element to the end, then heapify
- **remove** - swap the to be removed element with the last element, remove last element, then heapify