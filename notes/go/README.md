# Go

## 1) Basics

- pass by value

### Modules

```
go mod init <module-name>
```

Creates `go.mod` file. Don't edit it manually, use `go get` to add dependencies.

### Packages

#### Main package

All programs start in the `main` package. The `main` function is the entry point of the program.

```go
package main

func main() {
    fmt.Println("Hello, World!")
}
```

#### Imports

```
import "fmt"
```

Go always imports the full package.

### Formatting

Go has a built-in tool for formatting code: `go fmt`. It enforces a consistent style across all Go code.
Incorrectly formatted code will not compile.

To reformat all Go files in the current directory and its subdirectories:

```
go fmt ./...
```

## 2) Predeclared Types And Declarations

- strict explicit type conversion (no implicit conversions, e.g. from `int` to `float64`)

- `bool`
- integers: `int`, `int8`, `int16`, `int32`, `int64` (and their unsigned versions)
    - `uint8` is also called `byte` (alias, can be used interchangeably but prefer `byte`)
    - `int` and `uint` are platform dependent (32 or 64 bits)
- `rune` - like Java's `char`, represents a Unicode code point, alias for `int32`
  floating point: `float32`, `float64`
    - prefer `float64` for better precision
- `strings`
    - immutable sequence of _runes_
    - default value is `""` (not `nil`)
    - use `==` for comparison (also `>`, `<`, ...)

### Variables

- unused variables cause compilation error, use `_` to ignore them
- camel case convention

#### Declaration

```go
var x int // default value is 0, use explicit type declaration for 0s
var x byte = 20
var x = 10
x := 10 // only inside functions
```

In general, it's not recommended to declare variables outside of functions, use constants instead.

#### Multiple variables

```go
var x, y = 10, "hello" // mostly used for assigning multiple return values from functions
```

### Constants

- don't use UPPER_SNAKE_CASE, use camelCase instead

```go
const x int64 = 10

const (
idKey = "id"
nameKey = "name"
)
```

#### Typed vs untyped constants

```go
const x = 10 // can be assigned to any numeric type (int, int64, float64, ...)
const y int = 10
```

## 3) Composite Types

### Arrays

- use `==` and `!=` to compare two arrays
- `len` built-in function to get the length of an array
- rarely used directly (serve as a building block for more complex types), there are severe design limitations:
    - the size of the array is part of the type of the array

```go
var a [3]int // [0, 0, 0]
var b = [3]int{10, 20, 30}
var c = [...]int{10, 20, 30} // same as above, compiler infers the length from the number of elements: b == c is true
var d = [12]int{1, 5: 4, 6, 10: 100, 15} // [1, 0, 0, 0, 0, 4, 6, 0, 0, 0, 100, 15]
var x [2][3]int // 2D array (array of arrays)
```

### Slices

- slices can grow and shrink
- can't be compared with `==` (only with `nil`), use `slices.Equal` or `slices.EqualFunc` instead
    - avoid using `reflect.DeepEqual` for slices in new code

```go
var x []int // empty slice, default value is nil
var x = []int{10, 20, 30} // size is not specified: [...] is array, [] is slice
```

#### Common functions

```
len(x) // len(nil) is 0
var x []int
x = append(x, 10) // appending to empty (nil) slice is fine, append doesn't modify the original slice
y = append(x, 1, 2, 3)
z = append(x, y...) // append all elements of y to x
 
 
```
