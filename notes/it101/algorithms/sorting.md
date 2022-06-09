# Sorting
- numerical and lexicographical
- best performance `O(n * log(n))`
- **stable sort** - doesn't change the order of values with the same sorting keys
    - `basket, banana, apple` -> **sort by 1st letter**, stable algos will always put `basket` before `banana`
- **in-place sort** - doesn't require additional memory
- prerequisite for other algorithms like binary search

## Sources
- ✅ [Analysis of different sorting techniques](https://www.geeksforgeeks.org/analysis-of-different-sorting-techniques/) (GeeksForGeeks)
- ✅ [Quicksort vs. Mergesort](https://www.baeldung.com/cs/quicksort-vs-mergesort) (Baeldung)

## Classic algorithms

### Selection sort
- works by iterating over the array and swapping each element with the minimum element found in the rest of the array
- time`O(n^2)` (always), space `O(1)` (in-place sort)
- _child's algorithm_ - simple, but inefficient

### Bubble ("sinking") sort
- works by comparing adjacent pairs of elements and swapping them if they are in the wrong order
- time`O(n^2)`, space `O(1)`

### Insertion sort
- iterates over the given array, figures out what the correct position of every element is, and inserts each element in its place
- time`O(n^2)`, space `O(1)`
- effective for almost sorted arrays

### Merge sort
- recursive divide and conquer algorithm
- best, average and worst case is always `O(n * log n)` but requires additional `O(n)` memory
  (extra array for merging the sorted arrays)
- stable
- faster than quick sort for large datasets
- preferable for linked lists

### Quick sort
- uses pivot(s)
- worst case is `O(n^2)`, average case `O(n * log n)`, in-place (no extra memory is required)
- unstable
- preferable for arrays

## Non-comparison based algorithms
- not general-purpose
- take advantage of some constraint (such as small cardinality of the sorted values - age, sex, ...)
- **bucket sort** - for values with limited cardinality - age, sex
- **radix sort** - for integers (finite number of bits)
