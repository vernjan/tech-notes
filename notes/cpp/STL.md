# C++ Standard Library (STL)

- `std::move` - https://stackoverflow.com/questions/3413470/what-is-stdmove-and-when-should-it-be-used

## Containers

### array

- OO version of built-in array
  ```
  include <array>
  std::array<int, 5> arr = {1, 2, 3, 4, 5};
  ```

### vector

- dynamic array (~ArrayList)
- `[]` - doesn't check out of range vs. `.at()` - throws `std::out_of_range`

### list

- doubly linked list

### forward_list

- singly linked list

### map & unordered_map

- `std::map` - ordered map (red-black tree)
    - O(log n) for insert, find, delete
- `std::unordered_map` - unordered map (hash table)
- `[]` - creates a new element (default value) if it doesn't exist
- `find` - returns an iterator to the element if it exists, otherwise returns `end()` iterator