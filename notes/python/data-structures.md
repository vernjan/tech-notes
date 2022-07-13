# Data Structures
- see https://docs.python.org/3/tutorial/datastructures.html
- no generics, collections contain just pointers to objects

## Sequences
- last element - `list[-1]`

## Sequences - Immutable

### Strings

### Tuples
- `tuple = (1, "a", ("John", 33))`
- similar to list but immutable
- operations are the same as for list

### Bytes

## Sequences - Mutable

### Lists
- `list = [1, "a", ["nested", "list"]]`
- convert from `range` - `list(range(10))`
- merge lists - `merged = list1 + list2`
- adding/removing elements
  ```
  list.insert(index, obj)
  list.remove(obj)
  list.append(obj) // push
  list.pop()
  ```
- contains - `in`, `not in`
- sorting - `list.sort()`

### Byte arrays

## Sets
- `set = {1, "a"}`
- empty set - `set()`
- can't contain mutable data structures (no lists, sets or dictionaries, tuples are OK)
- union - `set1 | set2`
- intersection - `set1 & set2`
- difference - `set1 - set2`

### Frozen sets
- immutable, `frozenset(..)`

## Mappings - Dictionaries
- `my_dict = {"John": 33, "Jane": 28}`, or `my_dict = dict(John=33, Jane=28)`
- unordered
- iteration - `for name, age in my_dict.items():`
- adding new entry - `my_dict["Harry"] = 55`
- contains a key - `"foo" in my_dict`
- removing a key - `del my_dict["John"]`
- list keys - `list(my_dict)`

## Conversions
- `list(..)`
    - `list(dict)` - keys only
    - `list(dict.items())` - list of tuples
- `tuple(..)`
- `set(..)`
- `dict(..)`