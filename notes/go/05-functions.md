# Functions

- functions are first-class citizens
- typed based on the signature (parameter types and return types)

```go
func add(a int, b int) int {
    return a + b
}
```

## Function Basics

### Named and Optional Parameters

- no direct support
- use structs

```go
type MyFuncOpts struct {
    FirstName string
    LastName  string
    Age       int
}

func MyFunc(opts MyFuncOpts) error {
    // do something here
}

func main() {
    MyFunc(MyFuncOpts{
        LastName: "Patel",
        Age:      50,
    })
    MyFunc(MyFuncOpts{
        FirstName: "Joe",
        LastName:  "Smith",
    })
}
```

### Variadic Parameters

- supported, treated as slices

```go
func addTo(base int, vals ...int) []int {
    out := make([]int, 0, len(vals))
    for _, v := range vals {
        out = append(out, base+v)
    }
    return out
}

func main() {
    fmt.Println(addTo(3))
    fmt.Println(addTo(3, 2))
    fmt.Println(addTo(3, 2, 4, 6, 8))
    a := []int{4, 3}
    fmt.Println(addTo(3, a...))
    fmt.Println(addTo(3, []int{1, 2, 3, 4, 5}...))
}
```

### Multiple Return Values

- convention is to return `error` as the last return value

```go
func divAndRemainder(num, denom int) (int, int, error) {  // num, denom int is also valid: both are ints
    if denom == 0 {
        return 0, 0, errors.New("cannot divide by zero")
    }
    return num / denom, num % denom, nil
}
```

### Named Return Values

- not commonly used, but can be useful for documentation and readability
- doesn't force the name outside the function, they are only scoped to the function body
- preinitialized to zero values
- **blank returns** - can return without specifying the return values, but only if they are named, avoid

```go
func divAndRemainder(num, denom int) (result int, remainder int, err error) {
    if denom == 0 {
        err = errors.New("cannot divide by zero")
        return result, remainder, err
    }
    result, remainder = num/denom, num%denom
    return result, remainder, err
}
```

## Functions as Types

- map of string keys to functions of type `func(int, int) int`

```go
var opMap = map[string]func(int, int) int{
    "+": add,
    "-": sub,
    "*": mul,
    "/": div,
}
```