# Containers

- support for custom memory allocators

## Common operations

- for loops
- `begin()/cbegin()` & `end()/cend()` - (constant) iterators
- `size()`, `empty()`, `reserve()`
- `[]` - doesn't check out of range
- `.at()` - throws `std::out_of_range`, small performance overhead
- `push_back(pair{1, "a"})`
- `emplace_back({1, "a"}))` - wraps into value type
- `c=c2` - copy all
- `c==c2` - equality of all elements

## Advices

- store pointers to get polymorphic behavior
- elements are **copied** into containers
- pass container by reference
- _unordered_ means faster lookup
- _resize_ corrupts iterators and pointers

## `array`

- OO version of built-in array
  ```
  include <array>
  std::array<int, 5> arr = {1, 2, 3, 4, 5};
  ```

## `vector`

- default choice for sequences
- dynamic array (~`ArrayList`)

## lists

### `list`

- doubly linked list

### `forward_list`

- singly linked list
- good for empty, 1-2 elements sequences because occupies only 1 word of memory

## map

- `[]` - creates a new element (default value) if it doesn't exist
- `find` - returns an iterator to the element if it exists, otherwise returns `end()` iterator
- ordered map (red-black tree)
    - `O(log n)` for insert, find, delete
- variants
    - `unordered_` - hash table
    - `multi` - multiple keys

## set & unordered_set

## deque

## Extra STL containers

- `bitset`
- `tuple`
- `pair`
- `vector<bool>` - store bools as bits
- `valarray`