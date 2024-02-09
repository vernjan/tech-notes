# C++

- [Functions & variables](functions-vars.md)
- [Pointers & references](pointers-refs.md)
- [STL](STL.md)
- [OOP](OOP.md)

## Basics

- compatible with C (or at least used to be)
- basic syntax is quite similar to Java

### Java comparison

- `auto` ~ `var`
- `nullptr` ~ `null`
- `include` ~ `import`
- `using NAMESPACE` ~ `static import`
- `const var` ~ `final var`

## Namespaces

- to avoid name collisions and organize code
- global namespace - no prefix, we can even use e.g. `::MyObject`
- `using namespace std` - imports everything from a given namespace, not really recommended because it pollutes the global namespace
- `using std::cout, std::string` - selective imports - recommended
- `using` can be used inside functions to limit the scope

## Features

- initialization
    - standard: `int a = 5;`
    - using double brackets: `int a {5}`, `int a[] {1, 2, 3}`
- `constexpr` - compile-time constants and pure functions, stored in read-only memory
    - `constexpr int dmv = 17;`
    - `constexpr double square(double x) { return x*x; }` - pure functions
- test auto conversions
    - `if (x)` - `x` is converted to `bool`
        - `0` to false
        - `nullptr` to false
- `std::string` is mutable
    - `string s = "aaa"; s[0] = 'b';` works
    - you can use `const` to make it immutable

## Snippets

- `!!err` is the same as `!(!err)` which means `err != nullptr`
    - `err` is a pointer
    - see https://stackoverflow.com/questions/11374810/defining-double-exclamation

## Memory management

### Object lifecycle

- An object must be constructed (initialized) before it is used and will be destroyed at the end of its scope.
    - For a namespace object the point of destruction is the end of the program.
    - For a member, the point of destruction is determined by the point of destruction of the object of which it is a member.
    - An object created by new “lives” until destroyed by `delete`.

### Stack vs. Heap

- by default, variables are allocated on the stack, heap is used for dynamic memory allocation (new, malloc)

## Include guards

- to prevent multiple inclusion of the same (header) file (alternative is `#pragma once`)
    - prevents double declaration of any identifiers such as types, enums and static variables
    - prevents infinite recursion

```
#ifndef LEARNING_CPP_HOUSE_H
#define LEARNING_CPP_HOUSE_H

...

#endif //LEARNING_CPP_HOUSE_H
```