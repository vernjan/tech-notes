# OOP

```
Rectangle r2 = Rectangle(5, 6);         // stack
Rectangle * r3 = new Rectangle(5, 6);   // heap (pointer)
```

## Structs & Classes

- `class` vs `struct` - class was introduced in C++, very similar to struct, except for visibility rules for its members
    - `class` - default visibility is `private`
    - `struct` - default visibility is `public`
- `obj->method()` is a shortcut for `(*obj).method()`
- **member initializer list** - `: member1(val1), member2(val2) {}`

## Unions

- similar to `struct`, but all members share the same memory location
- only one member can be active at a time - to safe memory
- built-in STL support - `variant`

## Enumerations

- plain enums (C compatible, "named" integers") and enum classes

```c++
// plain enum
enum Color { red, blue, green };

// enum class
enum class Color { red, blue, green };
Color col = Color::red;
```