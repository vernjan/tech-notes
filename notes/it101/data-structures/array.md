# Array
- continuous block of memory, fixed size, requires pre-allocation
- fast set and get by index `O(1)` (random access)
- slow insert/delete `O(n)` - need to shift all the elements
- slow search `O(n)`

## Sorted array
- required for binary search

## Multi-dimensional array
- array of arrays
- all values must have the same type (at least in Java)

## Tips & Tricks
- use boolean array for keeping track of visited nodes (cheaper than a set)
