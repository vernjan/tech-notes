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

## Keywords
- `pass` keyword - do nothing
- `del` object - variable, class, function, dictionary entry, ...

## Data types
![](_img/python3-types.png)

**Source**: Wikipedia.org

- **integral**
    - integer (`int`) - variable size
    - booleans (`bool`) - `True/False`, `0/1`

## Strings formatting
- `%` operator
  ```
  "Hello %s!" % "world!"
  "Hello %s %d times!" % ("world", 5) 
  ```  
- **format** method
  ```
  "Foo is {0} {1} {0}".format(8, 2)
  "Foo is {foo}".format(foo=8)
  ```
- **patterns**
    - `%s` - string
    - `%d` - integer
    - `%f` - float
    - `%.2f` - decimal numbers
    - `%x`, `%X` - hexadecimal (lower/upper)

## Operators
- `**` - exponent
- `/` - float division
- `//` - floor division

### Sequence operators
- slicing - `[start:end:step]`
    - `[:8]` - from 0 to 8 (exclusive)
    - `[8::2]` - every second from 8th to the end
    - `[8:2:-1]` - slice in reverse
    - `[::-1]` - revert string
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
```
for i in range(1, 10, 2):
    print(i)

for i in ["a", "b", "c"]:
    print(i)
```

- `for/while else` - loops can have `else` block
    - executed once the condition is no longer true
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

## Modules
- `import MODULE [as ALIAS]`
- `from MODULE import CLASS` - just a single class
- **[PSL](https://docs.python.org/3/library/)** - Python Standard Library
    - datetime, math, random, ...
- **[PyPI](https://pypi.org/)** (Python Package Index)
    - Request, NumPy, Django, ...

### Custom modules
- **file.py** = module
- import using `import`
- module is initialized the first time it gets loaded (think `static` blocks in Java)
- static imports - `from my_lib import the_function`
- imports can be anywhere in the code - **dynamic imports**
  ```
  if visual_mode:
      import draw_visual as draw
  else:
      import draw_textual as draw
  ```