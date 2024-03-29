# Python Basics

- interpreted, dynamically typed, garbage collected
    - **duck typing**
        - "If it walks like a duck, and it quacks like a duck, then it must be a duck"
        - object is of a given type if it has all methods and properties required by that type
- **object-oriented**
    - everything is object, no primitives
    - dynamic classes - easy to add/remove fields or methods at runtime
- compiles from top to bottom (define classes before using objects)
- **CPython** - reference implementation
    - Jython (Java), IronPython (.NET), ...
- `snake_case` convention
- `.pyc` - compiled python file (bytecode)
    - imported modules get compiled
- **[PSL](https://docs.python.org/3/library/)** - Python Standard Library
    - datetime, math, random, ...
- **[PyPI](https://pypi.org/)** (Python Package Index)
    - Request, NumPy, Django, ...
- running Python module as a script `python -m MODULE [args]`

## Keywords

- `pass` keyword - do nothing
- `del` object - variable, class, function, dictionary entry, ...

## Data types

![](_img/python3-types.png)

**Source**: Wikipedia.org

### Numbers

- **integer** (`int`) - variable size
- **boolean** (`bool`) - `True/False`, `0/1`
- **float** (`float`) - `1.0`

### Strings

- single or double quotes - no real difference
    - `"I don't know."` vs. `'She said "No!"'`
- **raw strings** - `r"C:\foo\name"` - `\n` is not interpreted
- **multiline strings** - `'''` or `"""`
    - `\` - don't add new line

## Strings formatting

- `%` operator - not recommended anymore, this is the old way
  ```
  "Hello %s!" % "world!"
  "Hello %s %d times!" % ("world", 5) 
  ```  
- **String.format** method
  ```
  "Foo is {0} {1} {0}".format(8, 2)
  "Foo is {foo}".format(foo=8)
  ```
- **f-strings** - since Python 3.6 (default choice)
  ```
  name = "John"
  f"Hello {name.upper()}"
  ```
- **patterns**
    - `%s` - string
    - `%d` - integer
    - `%f` - float
    - `%.2f` - decimal numbers
    - `%x`, `%X` - hexadecimal (lower/upper)

## Variables

- multi-assignments
    - `a = b = 5` - single value
    - `a, b = 1, 2` - multi value
- swaps
    - `a, b = b, a`

## Operators

- `**` - exponent
- `/` - float division - returns `float`
- `//` - _floor_ division - returns `int`
- `%` - modulo (remainder)

### Sequence operators

- slicing - `[start:end:step]`
    - `[:8]` - from 0 to 8 (exclusive)
    - `[8::2]` - every second from 8th to the end
    - `[8:2:-1]` - slice in reverse
    - `[::-1]` - revert string
    - `[:]` - make copy (for immutable strings and tuples returns the same object, for lists creates a copy)
- repeat sequence operator `*`
    - strings - `"A" * 5` -> `"AAAAA"`
    - lists
        - `[0] * 5` -> `[0, 0, 0, 0, 0]`
        - `[0, 1] * 3` -> `[0, 1, 0, 1, 0, 1]`

## Comparators

- `==` - equal to
- `!=` - not equal to
- `is` - equal to (identity)
- `is not` - not equal to (identity)
- multi-comparators: `if (a < b < c): ...`

## Conditions

- **ternary operator** - `myVar = "Child" if age < 18 else "Adult"`
- `if - elif - else`
- empty objects are considered `False` (`[]`, `""`, ..)

## User input from CLI

```
word = input("Give me a word:")
print(word.upper())
```

## Loops

- foreach and while loop only, there is no "classic" for loop
- foreach loops over `iterable` (`list`, `range`, ...)
- built-ins
    - `iter()` - creates iterator from `iterable`
    - `next(iter)` - fetches next element

```
for i in ["a", "b", "c"]:
    print(i)
    
itr = iter(["a", "b", "c"])
next(itr)
> a
next(itr)
> b
...
> StopIteration exception
```

### range(from, to, step)

```
for i in range(1, 10, 2):
    print(i)
> 1, 3, 5, 7, 9 

list(range(1,6))
> [1, 2, 3, 4, 5]
```

### Loop `else`

- `for/while` - loops can have `else` block
    - executed once the condition is no longer true (think classic if-else)
    - skipped on break

## Exception handling

- see [Built-in Exceptions](https://docs.python.org/3/library/exceptions.html)

```
try:
    something()
except FooError:
    handle()
```

## `with`

- similar to Java's `try-with-resources`

## Access modifiers

- properties and methods are **public by default**
- to make them private, use naming pattern `__foo`
- even private members can be accessed using `_ClassName__foo`

## args & kwargs

- similar concept to Java's varargs
- `*` - unpacking operator (iterables)
- `**` - unpacking operator (dicts)

```python3
def fun_with_args(a, *args):
    print(type(args))  # <class 'tuple'>
    print(args)  # (2, 3)


def fun_with_kwargs(a, **kwargs):
    print(type(kwargs))  # <class 'dict'>
    print(kwargs)  # {'b': 2, 'c': 3}


def call_fun_with_args(*args):
    fun_with_args(1, *args)  # unwind the args from tuple to "2, 3"


def call_fun_with_kwargs(**kwargs):
    fun_with_kwargs(a=1, **kwargs)  # unwind the kwargs from dict to "b=2, c=3"


call_fun_with_args(2, 3)
call_fun_with_kwargs(b=2, c=3)

```

## Scopes & namespaces

- **namespace** - like a dictionary
    - `globals()` - global namespace - returns a modifiable dictionary
    - `locals()` - local namespace - returns a copy, cannot be modified
- **scopes**
    - **built-in** - `dir(__builtins__)` - functions, classes, errors, `None`, `True`, `False`, ...
    - **global** - for main program and any imported modules
    - **local & enclosing**
        - each function has its own local scope
        - if a function is defined in (enclosed by) another function, it has access to the enclosing function's scope
      ```python
      a = 1  # global scope
      def f1():
          def f2():
              c = 6
              print(x, a, b)  # c is local, b is enclosing, a is global, print is built-in
  
          b = 5
          f2()

    - LEGB rule - **L**ocal, **E**nclosing, **G**lobal, **B**uilt-in
        - search order when looking for a variable name, if not found, then `NameError` is raised
        - you cannot modify global variables from local scope
        ```python
        x = 1
        def f1():
            # global x  # uncomment to modify global variable x, similarly use 'nonlocal' for modifying enclosing scope
            x = 2  # this is a new local temporary assignment, not overrding the global scope
            print(x)  # 2
        f1()
        print(x)  # 1
        ``` 
