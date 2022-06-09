# Linked List
- data and _pointer_ to the next node
- optionally, we can keep a reference to _tail_
- slow set and get `O(n)` (there is no index), except for head/tail
- slow insert/delete to _non-head_ (and _non-tail_) `O(n)`
    - **Why?** You first have to search for the position to insert or delete (`O(n)`)
- slow search `O(n)`
- reverse traversing is not possible with a singly-linked list

## Usage
- hash maps collisions, file systems, adjacency lists
- dynamic memory allocation

## Doubly-linked list (DLL)
- can be traversed in both directions
- easier to implement deletes
- memory overhead
- double-ended queue ("deque")
- Java `LinkedList` is _doubly-linked_ and with _tail_

## Linked list with tail
- insert at the end is `O(1)`
- delete from the end is `O(n)` for a singly-linked list and `O(1)` for a doubly-linked list

## Insert & Delete
|               | Ins/Del head | Insert tail | Delete tail |
|---------------|--------------|-------------|-------------|
| SLL           | O(1)         | O(n)        | O(n)        |
| SLL with tail | O(1)         | O(1)        | **O(n)**    |
| DLL           | O(1)         | O(n)        | O(n)        |
| DLL with tail | O(1)         | O(1)        | O(1)        |

## Linked list vs. array
- memory allocation
    - dynamic vs. static
    - pointers overhead vs. pre-allocation
- fast (head) insertion and deletion vs. random access

## Tips & Tricks
- use linked list for "order reversing" while iterating - just append to the beginning
    - i.e. avoid `ArrayList.reverse`, use `LinkedList.add(0, E)`
- algorithms are usually about smart pointer manipulation, and it's common to use multiple pointers (fast & slow for example)