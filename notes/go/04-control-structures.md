# Blocks, Shadows, and Control Structures

- Be careful not to shadow predeclared identifiers (like `fmt`, `true`, ...)

## The Universe Block

- The universe block is the outermost block that contains all other blocks in a Go program.

🤦

```go
fmt.Println(true)
true := 10 // shadowing the predeclared boolean constant `true`
fmt.Println(true)
```

## If

- No parentheses around the condition
- Variables can be scoped to the if statement

```go
if x := compute(); x > 0 {
    fmt.Println("Positive")
} else if x < 0 {
    fmt.Println("Negative")
} else {
    fmt.Println("Zero")
}

## For