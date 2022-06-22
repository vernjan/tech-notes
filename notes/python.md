# Python
- interpreted, dynamically typed, garbage collected
- `snake_case` convention
- `pass` keyword - do nothing

## Data types
- numbers
    - integers - variable size
    - floats
    - complex numbers
- strings
- booleans
- `None`

### String slicing
- `[start:end:step]`
    - `[:8]` - from 0 to 8 (exclusive)
    - `[8::2]` - every second from 8th to the end
    - `[8:2:-1]` - slice in reverse
    - `[::-1]` - revert string

### String formatting
- `"Hello %s! % "world!"`

## Operators
- `**` - exponent
- `/` - float division
- `//` - floor division

### Comparators
- `==` - equal to
- `!=` - not equal to
- `is` - equal to (identity)
- `is not` - not equal to (identity)

### Strings
- `"A" * 32`
- `"Hell" in "Hello"` - contains

## Conditions
- **ternary operator** - `myVar = "Child" if age < 18 else "Adult"`
- `if - elif - else`

## Functions

### Built-in functions
- `print(*objects, sep=' ', end='/n')`
- `type(object)`
- `len(s)` - length of string or collection
- `map(function, iterable)`
- `filter(function, iterable)`
- `id(object)` - object's identity ("hashcode")

#### Type conversions
- `chr(i)` - Unicode code point to String character
- `ord(s)` - String character to Unicode code point
- `str(o)` - object to String
- `int(x, base=10)` - number or String to int
- `bool()`
- `float()`

### User-defined functions
```
def function_name(vars...)
```

## User input
```python
word = input("Give me a word:")
print(word.upper())
```

## Lambdas
```
lambda parameters: expression
```
- single line
- expressions

### Functions as arguments
- first class citizens
```python
def calc(operation, op1, op2):
    return operation(op1, op2)


print(calc(lambda a, b: a + b, 10, 5))
```

### map, filter
```
nums = [1, 2, 3, 4, 5]
map(lambda i: i * i, nums)
filter(lambda i: i < 3, nums)
```
- use `list()` to convert the result to list

## Loops
```
for i in range(1, 10, 2):
    print(i)

for i in ["a", "b", "c"]:
    print(i)

```