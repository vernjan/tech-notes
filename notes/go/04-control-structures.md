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
```

## For

- 4 variants
    - **C-style**
        ```go
        for i := 0; i < 10; i++ {
            fmt.Println(i)
        }
        ```
    - **While-style**
        ```go
        i := 0
        for i < 10 {
           fmt.Println(i)
            i++
        }
        ```
    - **Infinite loop**
        ```go
        for {
            // do something
            break // to exit the loop
        }
        ```
    - **Range loop**
        ```go
        evenVals := []int{2, 4, 6, 8, 10, 12} // slice
        for i, v := range evenVals { // idiomatic names: i (index), v or k (key), v; use _ if you don't need the "index"
            fmt.Println(i, v)
        }
      
        uniqueNames := map[string]bool{"Fred": true, "Raul": true, "Wilma": true}
        for k := range uniqueNames { // only need the key, not the value, typically used for Go "sets"
            fmt.Println(k)
        }
        ```

        - Iteration order for maps is randomized!
            - `fmt.Println` will print the keys ascending order for easier debugging
        - For strings, it iterates over Unicode code points (runes), not bytes

- labels are supported