# Graph
- very flexible
- social networks, GPS navigation, crawlers, garbage collection
- **vertices** (nodes) and **edges** (pair of nodes)
- **directed** (edges are unidirectional) vs. **undirected** (edges are bidirectional)
- **degree of vertex** - total number of connected edges
    - **in-degree of vertex**: total number of _incoming_ edges
    - **out-degree of vertex**: Total number of _outgoing_ edges
- **parallel edges** - more edges connecting the same nodes
- **self loop** - edge(x, x)
- **path**
    - shortest path
- **cycle**
- **neighbors**
- **connected** - at least one path between any two pairs
- **tree** is a connected graph without any cycle
- **DAG** - directed acyclic graph
- **spanning tree** - "kostra grafu" - connects all nodes using just 1 edge (i.e. it's a tree)

## Implementation
- see [Comparison between Adjacency List and Adjacency Matrix representation of Graph](https://www.geeksforgeeks.org/comparison-between-adjacency-list-and-adjacency-matrix-representation-of-graph/)

### Adjacency list
- array of linked lists
    - memory `O(V+E)`
- memory effective for sparse graph
- **operations cost**
    - add vertex `O(1)` - assuming a bigger array to start with, not counting for re-allocation
    - add edge `O(1)` - insert at tail
    - remove vertex `O(V+E)` - find vertex + remove all its edges
    - remove edge `O(E)` - traverse all edges of the given vertex
    - traversal `O(V+E)` - both DFS and BFS (`+E` because of possibly more edges pointing to the same node)

### Adjacency matrix
- 2-dim array (`V*V`)
    - memory `O(V^2)`
- cheap edge changes, costly adding/removing of vertices
- memory effective for dense graphs
- **operations cost**
    - add vertex `O(V^2)` - recreate 2-dim array
    - add edge `O(1)`
    - remove vertex `O(V^2)` - recreate 2-dim array
    - remove edge `O(1)`
    - traversal `O(V^2)` - both DFS and BFS

### Incidence matrix
- https://en.wikipedia.org/wiki/Incidence_matrix
- 2-dim array (`V*E`)
- for undirected graphs

### Backed by hash table
- `Map<String, List<String>>`

## Traversal
- don't forget to skip the already visited nodes!

### Depth-first search (DFS)
- "move on, then come back"
- think stack (or recursion)
- consumes less memory than BFS, preferred for "visit all nodes" tasks

### Breadth-first search (BFS, level-order)
- "visit all children first, then move on" or "level by level"
- think queue
- good strategy if we know the searched node is not very deep
- finds the shortest path between 2 nodes

#### Bidirectional search
- for finding the shortest path between 2 nodes
- it' `O(n^(d/2))` faster than searching from a single point

## Topological sort
- https://www.geeksforgeeks.org/topological-sorting/
- **pre-order** traversal
- topological sort is a graph traversal in which each node `v` is visited only after all its dependencies are visited ("roots before leaves")
- **TL;DR** - consider a directed acyclic graph (DAG), "arrows" point to dependencies, first come the dependencies, then the dependants

### Example
- construction/assembly guide
- planning a party
  ```
  Throw a party --> Make food --> Buy groceries
                --> Buy drinks
  ```
  **Valid sorts**
    - Buy groceries, Make food, Buy drinks, Throw a party
    - Buy groceries, Buy drinks, Make food, Throw a party
    - Buy drinks, Buy groceries, Make food, Throw a party


