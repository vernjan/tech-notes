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