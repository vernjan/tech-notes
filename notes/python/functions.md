# Functions

## Built-in functions
- `print(*objects, sep=' ', end='/n')`
- `type(object)`
- `len(s)` - length of string or collection
- `map(function, iterable)`
- `filter(function, iterable)`
- `id(object)` - object's identity ("hashcode")
- `round`

### Type conversions
- `chr(i)` - Unicode code point to String character
- `ord(s)` - String character to Unicode code point
- `str(o)` - object to String
- `int(x, base=10)` - number or String to int
- `bool()`
- `float()`

### map, filter, reduce, zip
- use `list(..)` to convert the result to list
```
nums = [1, 2, 3, 4, 5]
map(lambda i: i * i, nums)
map(round, circle_areas, range(1, 7)) # 2 arguments for round !!!
filter(lambda i: i < 3, nums)
reduce()
zip()
```

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

## Closures
- access to variables in the enclosing scope is readonly
    ```
    def outer(msg):
        def inner():        # nested function
            print(msg)      # has access to msg (readonly)
        inner()
    
    outer("Hello")
    ```

- returning a function with closure
    ```
    def multiplier_of(n1):
        def mult(n2):
            return n1 * n2
        return mult
    
    multiplywith5 = multiplier_of(5)
    print(multiplywith5(9))
    ```            

## Decorators
- wrap a function into another functions
    - input checks, transactions, logging, ...
- `@decorator_name`

```
def auditable(old_function):
    def new_function(*args, **kwds):
        print("Calling %s" % old_function.__name__)
        return old_function(*args, **kwds)
    return new_function

@auditable
def foo():
    print("FOOOO")
  
```