# Composite Types

## Arrays

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

## Slices

- slices can grow and shrink
- can't be compared with `==` (only with `nil`), use `slices.Equal` or `slices.EqualFunc` instead
    - avoid using `reflect.DeepEqual` for slices in new code
- len vs capacity, slice is copied to new location when appending and capacity is exceeded

```go
var x []int // empty slice, default value is nil
var x = []int{10, 20, 30} // size is not specified: [...] is array, [] is slice
```

### Slicing Slices

- similar to Python `[:]`
- Doesn't return a copy! Modifying slices is very confusing, better avoid!

```go
x := []string{"a", "b", "c", "d"}
y := x[:2]
y = append(y, "z")
fmt.Println("x:", x) // [a b z d]
fmt.Println("y:", y) // [a b z]
```

## Array - Slice Conversions

```go
// array to slice
xArray := [4]int{5, 6, 7, 8}
xSlice := xArray[:] // nothing is copied

// slice to aray
xSlice := []int{1, 2, 3, 4}
xArray := [4]int(xSlice) // this is a copy!
```

## Strings and Runes and Bytes

- immutable sequence of bytes
- slicing is supported but be careful with multi-byte characters (e.g. emojis)
- `len()` returns the number of bytes, not the number of characters (runes)!

```go
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

## Maps

- keys must be comparable (e.g. can't use slices as keys)
    - Go doesn’t require (or even allow) you to define your own hash algorithm or equality definition
- hash maps
- if the key doesn't exist, the zero value of the value type is returned (e.g. 0 for int, "" for string, nil for slices and maps)
- comparing: `maps.Equal` or `maps.EqualFunc` (same as for slices)
- there is no set type in Go, but you can use a map with empty struct values or boolean values to represent a set
    - union, intersection, and subtraction are not part of the standard

```go
var nilMap map[string]int
emptyMap := map[string]int{}

teams := map[string][]string { // map of strings to string slices
"Orcas": []string{"Fred", "Ralph", "Bijou"},
"Lions": []string{"Sarah", "Peter", "Billie"},
"Kittens": []string{"Waldo", "Raul", "Ze"},
}

delete(m, "Orcas") // delete a key from the map (doesn't return anything, doesn't cause an error if the key doesn't exist)

emptyMapOfSize10 := make(map[int][]string, 10)
```

### The comma ok Idiom

```go
m := map[string]int{
"foo": 5,
}
v, ok := m["foo"]
fmt.Println(v, ok) // Output: 5 true

v, ok = m["bar"]
fmt.Println(v, ok) // Output: 0 false
```

## Structs

- zero value is a struct with all fields set to their zero values
- struct is comparable if all its fields are comparable

```go
type person struct {
    name string
    age  int
    pet  string
}

julia := person{
    "Julia",
    40,
    "cat",
}

beth := person{
    age:  30,
    name: "Beth",
}
```

## Built-in Functions

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
