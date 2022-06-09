# Recursion
- calls itself
- **base case** (stop condition) and **recursive case** (call to itself)
    - there can be multiple base cases (for example _check prime_ algorithm)
- **direct** (function calls itself) vs. **indirect** (function `a` calls function `b` which calls function `a`)
- can run out of stack - avoid using recursion unless it's a _tail recursion_ or a logarithmic complexity
- can be replaced with _stack_ data structure
- recursion is **most useful when** a problem
    - can be broken down to similar subtasks (divide and conquer)
    - requires dynamic number of nested loops (for example finding all permutations, iterating a graph or tree)
    - do something in reverse (print linked list)
- space `O(n)` (stack frames)

## Pros & cons
- `+` shorter code compared to iterative
- `+` some problems are inherently recursive (tree traversal)
- `-` memory (stack frames) and CPU overhead requires more memory
- `-` difficult to debug

## How to "debug" it
- visualize through a stack (for simple cases)
- **draw a recursive tree** and keep track of variables (!!!)

## My tricks for recursion
- always start with the base case (stop condition)
- arguments - there is a big difference between mutable and immutable data! Mutable is shared for all steps, immutable
  is unique per stack
- returns
    - you always must return the (partial) result
    - use conditions if there are multiple returns