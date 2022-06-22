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
## Lambdas
```
lambda parameters: expression
```
- single line only
- always expressions

### Functions as arguments
- functions are first class citizens
```
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