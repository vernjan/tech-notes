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
- use `type` to create a named function type for better readability (e.g. `type BinaryOp func(int, int) int`)

```go
var opMap = map[string]func(int, int) int{ // map[string]BinaryOp
    "+": add,
    "-": sub,
    "*": mul,
    "/": div,
}
```

```go
var (
    add = func(i, j int) int { return i + j }
    sub = func(i, j int) int { return i - j }
    mul = func(i, j int) int { return i * j }
    div = func(i, j int) int { return i / j }
)

func main() {
    x := add(2, 3)
    fmt.Println(x)
}
```

## Anonymous Functions

```go
func main() {
    f := func(j int) {
        fmt.Println("printing", j, "from inside of an anonymous function")
    }
    for i := 0; i < 5; i++ {
        f(i)
    }
}
```

## Closures

- can be passed to other functions or returned
- capture by reference (so unlike Java lambdas, can modify the captured variables)

```go
func main() {
    a := 20
    f := func() {
        fmt.Println(a)
        a = 30 // a := 30 would shadow the variable
    }
    f()
    fmt.Println(a)
}
```

```go
func getFile(name string) (*os.File, func(), error) {
    file, err := os.Open(name)
    if err != nil {
        return nil, nil, err
    }
    return file, func() { // cleanup function a caller can call at will
        file.Close()
    }, nil
}
```

## `defer`

- for cleanup - `defer` delays the invocation until the surrounding function exits
- runs after function **return**
- multiple defers allowed, executed as LIFO

```go
f, err := os.Open(os.Args[1])
if err != nil {
    log.Fatal(err)
}
defer f.Close() // function, method or closure
// do someting useful  
```

```go
func DoSomeInserts(ctx context.Context, db *sql.DB, value1, value2 string)
                  (err error) {
    tx, err := db.BeginTx(ctx, nil)
    if err != nil {
        return err
    }
    defer func() { // runs a closure
        if err == nil {
            err = tx.Commit() // modifies the original err, i.e. returns err from tx.Commit()
        }
        if err != nil {
            tx.Rollback()
        }
    }()
    _, err = tx.ExecContext(ctx, "INSERT INTO FOO (val) values $1", value1)
    if err != nil {
        return err
    }
    // use tx to do more database inserts here
    return nil
}
```

## Call by Value
