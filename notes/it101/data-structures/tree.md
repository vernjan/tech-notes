# Tree
- root, nodes, edges (or pointers), parent nodes, child nodes, siblings, leaf nodes, ancestor, descendant, subtree
- **degree of a node** - number of child nodes
- **depth** - number of edges from parent (i.e. root 0, root child nodes 1)
- **level** - depth + 1
- **height of a node** - number of edges from this node to the deepest leaf node
- **height of a tree** - height of the root node
- **distance** - number of edges between two nodes
- **forest** - set of disjoint trees

### Graph is a tree if
- each node, except root, has **exactly one parent**
- there are no cycles (**acyclic**)
- graph is **connected**
- ==> tree always has exactly one root

## Tree types
- **N-ary tree** - each node has 0-N child nodes
    - **binary tree** is a 2-ary tree
        - **binary search tree**
            - AVL tree
            - Red-Black tree
    - 2-3 tree, 2-3-4 tree
    - B-tree

## Binary tree properties
- could be generalized for N-ary trees

![](_img/trees.png)

**Source**: https://towardsdatascience.com/5-types-of-binary-tree-with-cool-illustrations-9b335c430254

### Full (proper)
- each node has exactly 2 children (except for the leaf nodes which has 0, no node can have just 1 child)
- maps nicely to an array - level by level from left to right

### Complete
- every level, except possibly the last, is completely filled, and all nodes in the last level are as far left as possible
- **heap** is a good example of a complete binary tree
- **maximum number of nodes**: `2^(h+1) -1` (see [Geometric series](https://en.wikipedia.org/wiki/1_%2B_2_%2B_4_%2B_8_%2B_%E2%8B%AF))
- **total number of parent nodes**: `2^h - 1`
- **maximum number of leaf nodes**: `2^h`

### Degenerate
- each node has exactly 1 child
- **skewed left/right** - each node has exactly 1 left/right child

### Perfect
- full and complete
- **total number of nodes**: `2^(h+1) -1`

### Balanced
- left and right subtrees of every node differ in height by no more than 1
- for each node: `|Height(LeftSubTree) - Height(RightSubTree) |<= 1`
- start checking from leaf nodes and move to the root

## Binary search tree
- left child is smaller (or equal) than parent, right child is greater
    - more accurately, left _subtree_ contains smaller keys only, while the right subtree contains greater keys
- the most left leaf is MIN, the most right leaf is MAX
- used to quickly check whether an element is present in a set or not

### Operations
- **insert** `O(h)`
- **delete** `O(h)`
    - **leaf node** - easy
    - **parent node with 1 child** - easy, link the parent and the child of the deleted node
    - **parent node with 2 children** - also quite straightforward
        - find the minimum value of the deleted node right subtree ("left bottom" node of the subtree) - **in-order successor**
        - swap the minimum value with the deleted node value
        - delete the original minimum value node
- **search** `O(h)`

**Watch out**: `O(h) = O(log n)` just for balanced trees, for skewed trees, it's `O(n)`!

### AVL tree
- perfectly balanced BST (self-balancing)
- slower insert & delete, faster search compared to Red-black trees

### Red-black tree
- not-perfectly balanced BST (self-balancing)
- faster insert & delete, slower search compared to AVL trees
- nodes store color (red or black)
- used since Java 11 for handling map collisions (for >8 values)

## 2-3 tree
- not BST
- node can have 2 values and up to 3 children
- 2-3-4 tree, ...

## B-tree
- generalized BST (a node can contain more values and have more children)
    - tree is more compact for big data and thus faster
- keeps data sorted and allows searches, insertions, and deletions in logarithmic amortized time
- optimized for systems that read and write large blocks of data
- used in
    - databases and file systems
    - to store blocks of data (secondary storage media)
    - multilevel indexing

## DFS traversal
https://en.wikipedia.org/wiki/Tree_traversal#Depth-first_search

### Pre-order (natural)
- `root-left-right` ("parents before children" aka _topological_ order)
- root is visited as first
- represents prefix expressions
- in tries, returns words in alphabetical order

### In-order
- `left-root-right` (sequential)
- in binary search trees, visits node in ascending order

### Post-order
- `left-right-root` ("children before parents")
- root is visited as last
- represents postfix expressions