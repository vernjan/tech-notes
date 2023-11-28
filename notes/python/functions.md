# Functions

```
def function_name(vars...):
    body
    [return foo]
```

## Lambdas

```
lambda parameters: expression
```

- single line only
- always expressions

## Functions as arguments

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
    
foo()
```

## Properties

- if setter is not defined, then the property is read-only

```python
class Foo:
    def __init__(self):
        self._x = 0

    @property
    def x(self):
        print("getter")
        return self._x

    @x.setter
    def x(self, value):
        print("setter")
        self._x = value


f = Foo()
f.x = 1
print(f.x)

```