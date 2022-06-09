# Set
- contains unique values, without any particular order
- **contains** `O(1)` (the worst case is `O(n)` if there are many collisions)
- **union** `O(len(a)+len(b))`
- **intersection** `O( min(len(a), len(b)) )`
- **difference** ("minus") `O(len(b))`

## Power sets
- all permutations (`n^2`)
    - for example `{a, b, c} --> {}; a; b; c; ab; ac; bc; abc`