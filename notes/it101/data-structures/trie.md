# Trie (prefix tree)
- prefix trees that are used to store strings for fast retrieval by prefix
- each node has 26 children (for english alphabet), and a flag `isEndWord`
- depth of the trie depends on the longest word
- bigger space complexity compared to hash tables (due to many `null` nodes)
- treat all letters as lower-case

## Usages
- auto-complete
- spell-check
- searching for contacts (prefix search)

## Operations
- insert, search and delete `O(h)` (`h` is the word length)
- insert and search are quite easy to implement
- delete
    - find the word _end node_ (using recursion)
        - if it has no children (i.e. it's not a prefix for some other word), delete it
        - otherwise, remove the "end word" flag and exit
    - move 1 level up
        - if it's "end word" OR has children, don't touch it and exit
        - otherwise repeat