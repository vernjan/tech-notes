# Go

## 1) Basics

- pass by value (by default)
- garbage collected
- Go runtime is compiled into every binary (hello world is ~ 2 MB)

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
    - immutable sequence of bytes (not runes)
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
- len vs capacity, slice is copied to new location when appending and capacity is exceeded

```go
var x []int // empty slice, default value is nil
var x = []int{10, 20, 30} // size is not specified: [...] is array, [] is slice
```

#### Slicing Slices

- similar to Python `[:]`
- Doesn't return a copy! Modifying slices is very confusing, better avoid!

```go
x := []string{"a", "b", "c", "d"}
y := x[:2]
y = append(y, "z")
fmt.Println("x:", x) // [a b z d]
fmt.Println("y:", y) // [a b z]
```

### Array - Slice Conversions

```go
// array to slice
xArray := [4]int{5, 6, 7, 8}
xSlice := xArray[:] // nothing is copied

// slice to aray
xSlice := []int{1, 2, 3, 4}
xArray := [4]int(xSlice) // this is a copy!
```

### Strings and Runes and Bytes

- immutable sequence of bytes
- slicing is supported but be careful with multi-byte characters (e.g. emojis)
- `len()` returns the number of bytes, not the number of characters (runes)!

```
// len
var s string = "Hello 😀"
fmt.Println(len(s)) // 10

// conversions
var a rune    = 'x'
var s string  = string(a)
var b byte    = 'y'
var s2 string = string(b)

var s string = "Hello, 😀"
var bs []byte = []byte(s) // [72 101 108 108 111 44 32 240 159 140 158]
var rs []rune = []rune(s) // [72 101 108 108 111 44 32 127774]
``` 

### Maps

### Built-in Functions

```go
// len
len(x) // len(nil) is 0

// append
var x []int // nil slice
var x = []int{}   // empty slice, not nil, but len is also 0, e.g. for json serialization
x = append(x, 10) // appending to empty (nil) slice is fine, append doesn't modify the original slice
y = append(x, 1, 2, 3)
z = append(x, y...) // append all elements of y to x

// cap
cap(x) // max capacity, for arrays alwayst the same as len

// make
x := make([]int, 5) // creates a slice of length 5 and capacity 5, initialized with zero values: [0, 0, 0, 0, 0]
x := make([]int, 5, 10) // creates a slice of length 5 and capacity 10

// clear
clear(x) // sets all elements to zero value, doesn't change the length or capacity of the slice

// copy
x := []int{1, 2, 3, 4}
y := make([]int, 4) // len and cap is 4
num := copy(y, x) // dest, source (if dest < smaller then only a subset is copied)
```
