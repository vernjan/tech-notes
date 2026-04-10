# Go

## Modules

```
go mod init <module-name>
```

Creates `go.mod` file. Don't edit it manually, use `go get` to add dependencies.

## Packages

### Main package

All programs start in the `main` package. The `main` function is the entry point of the program.

```
package main

func main() {
    fmt.Println("Hello, World!")
}
```

### Imports

```
import "fmt"
```

Go always imports the full package.

## Formatting

Go has a built-in tool for formatting code: `go fmt`. It enforces a consistent style across all Go code.
Incorrectly formatted code will not compile.

To reformat all Go files in the current directory and its subdirectories:

```
go fmt ./...
```

## Types

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
    - default value is `""`
    - use `==` for comparison (also `>`, `<`, ...)