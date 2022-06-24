# Data Structures
- [Python docs](https://docs.python.org/3/tutorial/datastructures.html)
- mutable (except _tuple_)

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

### List comprehension
- creates new list from a loop
```
[expresion for LOOP if CONDITION (optional)]
```

- simple example
    ```
    nums = [1, 2, 3]
    nums_double = [n * 2 for n in nums] // 2, 4, 6
    ```
- with condition
    ```
    nums = [1, 2, 3]
    nums_double = [n * 2 for n in nums if n != 2] // 2, 6
    ```
- multiple loops
  ```
  list1 = [..]
  list2 = [..]
  sum_list = [(n1, n2) for n1 in list1 for n2 in list2 if n1 + n2 > 100]
  ```

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

### Dictionary comprehension
```
houses = {1: "Gryffindor", 2: "Slytherin", 3: "Hufflepuff", 4: "Ravenclaw"}
new_houses = {n**2: house + "!" for (n, house) in houses.items()
```

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