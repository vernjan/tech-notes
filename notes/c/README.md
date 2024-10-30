# C

- `void *p` - void pointer - pointer of any type
- [pointer vs. array](https://www.geeksforgeeks.org/pointer-vs-array-in-c/)

## Arrays
- `int arr[5]` - array of 5 integers
  - unlike Java, brackets are placed after the type, not the name

## malloc, memset, free

- **malloc** - allocate memory
  - `int *p = (int *)malloc(5 * sizeof(int));`
- **memset** - set memory with the given value
  - `memset(p, 0, 5 * sizeof(int));`
- **free** - deallocate memory
  - `free(p);`