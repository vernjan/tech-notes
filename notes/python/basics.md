# Python Basics
- interpreted, dynamically typed, garbage collected
- object oriented - everything is object
- `snake_case` convention
- `.pyc` - compiled python file (bytecode)
    - imported modules get compiled
- `pass` keyword - do nothing
- `del` object - variable, class, function, dictionary entry, ...
- repeat sequence operator `*`
    - strings - `"A" * 5` -> `"AAAAA"`
    - lists
        - `[0] * 5` -> `[0, 0, 0, 0, 0]`
        - `[0, 1] * 3` -> `[0, 1, 0, 1, 0, 1]`

## Data types
- **numbers**
    - integers - variable size
    - floats
    - complex numbers
- **strings**
    - `"Hell" in "Hello"` - contains
    - `"Hello %s! % "world!"` - formatting using `%` operator
        - `%s`, `%d`, `%f`
        - `%.2f` - decimal numbers
        - `%x`, `%X` - hexadecimal (lower/upper)
- **booleans**
- `None`

## Operators
- `**` - exponent
- `/` - float division
- `//` - floor division

## Comparators
- `==` - equal to
- `!=` - not equal to
- `is` - equal to (identity)
- `is not` - not equal to (identity)

## Slicing
- `[start:end:step]`
    - `[:8]` - from 0 to 8 (exclusive)
    - `[8::2]` - every second from 8th to the end
    - `[8:2:-1]` - slice in reverse
    - `[::-1]` - revert string

## Conditions
- **ternary operator** - `myVar = "Child" if age < 18 else "Adult"`
- `if - elif - else`
- empty objects are considered `False` (`[]`, `""`, ..)

## User input
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
  