# Python Basics
- interpreted, dynamically typed, garbage collected
- `snake_case` convention
- `pass` keyword - do nothing
- `del` object - variable, class, function, dictionary entry, ...

## Data types
- **numbers**
    - integers - variable size
    - floats
    - complex numbers
- **strings**
    - `"A" * 32`
    - `"Hell" in "Hello"` - contains
    - `"Hello %s! % "world!"` - formatting using `%` operator
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