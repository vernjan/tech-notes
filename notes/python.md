# Python
- interpreted, dynamically typed, garbage collected
- `snake_case` convention

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

## Built-in functions
- `print`
- `type`
- `id`
- `len`
- `chr(i)` - return the string representing a character whose Unicode code point is the integer i

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