# Built-in Functions
- see https://docs.python.org/3/library/functions.html

- `print(*objects, sep=' ', end='/n')`
- `len(s)` - length of string or collection
- `type(obj)`
- `id(object)` - object's identity ("hashcode")
- `input([prompt])` - read value from CLI
- `open(file)` - read file
- `range([start], stop, [step])`
- `reversed(seq)` - reverse a sequence
- `sorted(seq)`
- `eval(expr, globals, locals)` - evaluate Python expression
   ```
   x = 100
   res = eval("x * 2")
   ```

## Predicates
- `all(iterable)`
- `any(iterable)`

## Math
- `abs(x)`
- `max(args*)`, `min(args*)`
- `pow(base, exp, [mod])`
- `round(number, [places])`
- `sum(iterable)`

## Type conversions & Numbers
- `bin(x)` - integer to binary string (`bin(3)` -> `0b11`)
- `bool([x])` - converts `x` to bool, see [Truth Value Testing](https://docs.python.org/3/library/stdtypes.html#truth)
- `chr(i)` - Unicode code point to string character
- `complex([real, [imag]])` - complex numbers
- `float([x])`
- `hex(x)` - integer to hex string (`bin(16)` -> `0xa`)
- `int([x], base=10)` - number or string to int
- `ord(s)` - string character to Unicode code point
- `str(o)` - object to string

## Data structure factories
- bytearray
- bytes
- dict
- frozenset
- list
- set
- tuple

## Code introspection
- `dir([obj])` - names in the current scope, or object attributes (`__dirs__`)
- `vars([obj])` - attributes and their values (`__dict__`)
- `help(func)` - function docs
- `hasattr(obj, name)`,`getattr(object, name)`, `setattr(object, name, value)`
- `issubclass(class, classinfo)`,
- `isinstance(obj, classinfo)`

## Streams
- `map(func, iterable)` - supports multiple iterables -> multiple arguments for the function
  - accepts `iterable`, returns `iterator` (aka `map object`)
- `filter(func, iterable)`
- `zip(*iterables)`