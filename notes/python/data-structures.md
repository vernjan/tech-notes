# Data Structures
- [Python docs](https://docs.python.org/3/tutorial/datastructures.html)
- mutable (except _tuple_)
- no generics, contains just pointers to objects

## List
- `list = [1, "a", ["nested", "list"]]`
- convert from `range` - `list(range(10))`
- merge lists - merged = list1 + list2
- adding/removing elements
    ```
    list.insert(index, obj)
    list.remove(obj)
    list.append(obj) // push
    list.pop()
    ```
- slicing - same as for strings
- contains - `in` `not in`
- sorting - `list.sort()`
- last element - `list[-1]`

## Tuple
- `tuple = (1, "a", ("John", 33))`
- similar to list but immutable
- operations are the same as for list

## Dictionary
- `dict = {"John": 33, "Jane": 28}`, or `dict(John=33, Jane=28)`
- unordered
- iteration - `for name, age in dict.items():`
- contains key - `"foo" in my_dict`
- list keys - `list(my_dict)`
- removing a key - `del phonebook["John"]`

## Set
- `set = {1, "a"}`
- empty set - `set()`
- can't contain mutable data structures (no lists, sets or dictionaries, tuples are OK)
- union - `set1 | set2`
- intersection - `set1 & set2`
- difference - `set1 - set2`

## Conversions
- `list(..)`
    - `list(dict)` - keys only
    - `list(dict.items())` - list of tuples
- `tuple(..)`
- `set(..)`
- `dict(..)`