# Advanced Topics

## Good Python examples

- https://github.com/realpython/materials/blob/master/python-type-checking/hearts.py

## Multi-assignments & Sequence unpacking

```
a, b, c = 1, 2, 3
a, b, c = [1, 2, 3]
```

## Walrus operator `:=`

- Expression is evaluated and then assigned to the variable name. That value will also be returned.

```
print(num := 42)
print("Num is %d" % num)
```

## Generators

- lazily generate iterables
- execution jumps between iteration and generation

```
def my_gen():
    for i in range(3):
        print("Inside generator: %d" % i)
        yield i

    print("Last value")
    yield "END"


for j in my_gen():
    print("Iterating my generator: %s" % j)
```

**Output:**

```
Inside generator: 0
Iterating my generator: 0
Inside generator: 1
Iterating my generator: 1
Inside generator: 2
Iterating my generator: 2
Last value
Iterating my generator: END
```

### Fibonacci generator

```
def fib():
    a, b = 1, 1
    yield 1
    yield 1
    while True:
        a, b = a + b, a
        yield a
```

## For comprehensions

- a bit similar to streams - iterate, filter, map and always return a new collection

### List comprehension

```
[expresion for x in list [if CONDITION]]
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

### Dictionary comprehension

```
{expresion1: expression2 for (k,v) in dict.items() [if CONDITION]}
```

```
houses = {1: "Gryffindor", 2: "Slytherin", 3: "Hufflepuff", 4: "Ravenclaw"}
new_houses = {n**2: house + "!" for (n, house) in houses.items()
```

### Set comprehension

```
{expresion for x in set [if CONDITION]}
```

```
set_lower = {"a", "b", "c"}
set_upper = {item.upper() for item in set_lower}
print(set_upper)
```

## Varargs

- use `*`

```
def my_map(op, *values):
    return [op(v) for v in values]


print(my_map(str.upper, "a", "b", "c"))
```

## Dynamic arguments

- use `**`
- similar to using map, nicer syntax

```
def start(**options):
    if options.get("debug"):
        print("Debug mode ON")
    if options.get("verbose"):
        print("Verbose level %d" % options["verbose"])
    else:
        print("No verbose")

start(debug=True, verbose=5)
start(debug=True)
```

## Serialization

### JSON

```
import json
obj = json.loads(str)
str = json.dumps(obj)
```

### Pickle

- Python proprietary format

```
import pickle
obj = pickle.loads(str)
str = pickle.dumps(obj)
```

## Functional programming

- module `functools`
    - higher-order functions and operations on callable objects
    - partial functions - `partial(func, args*)`
- module `itertools` - a bit like streams in Java

## Dunder methods

- names begin and end with double-underscores (`__name__`)
- to allow user-defined classes to modify how they are handled by native operations including length, comparison, in arithmetic operations and type conversion

## Operator overloading

- implement one of the predefined methods, for example
    - `__plus__(self, other)`
    - `__sub__(self, other)`
    - `__and__(self, other)`
    - `__lt__(self, other)`
    - `__gt__(self, other)`
    - ...

## Type hints

- `from __future__ import annotations`
    - Python 3.7+
    - allows forward references to types which are not yet defined