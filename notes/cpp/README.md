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
- `templates` ~ `generics`
- `static` ~ `private` - static objects/functions are not exported outside of the CPP file

## Exception handling

1) Use error codes - failure is normal and expected (like reading a file), immediate caller
2) throw exception - caller is not immediate, undo action is possible
3) Terminate - irrecoverable errors

- `noexcept` - function will not throw exceptions

## Namespaces

- to avoid name collisions and organize code
- `::` - scope resolution operator
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
- `std::string` is a class, not a primitive type
    - C-style string literal is `const char[N]`, to make it string use suffix `s`

## Type casting

- `static_cast` - compile-time cast, no runtime checks, best avoided but sometimes necessary
- `dynamic_cast` - runtime check, used for polymorphism
    - dynamic cast to a reference type - if the cast fails, an exception of type `std::bad_cast` is thrown
    - dynamic cast to a pointer type - if the cast fails, the result is a null pointer of the target type

## Snippets

- `!!err` is the same as `!(!err)` which means `err != nullptr`
    - `err` is a pointer
    - see https://stackoverflow.com/questions/11374810/defining-double-exclamation

## Memory management

- **dynamic memory** (heap, free store) - allocated at runtime
    - allocation - `new`, `delete`
    - `new` returns a pointer to the allocated memory
    - `int* myInt = new int(123);`
- better to use smart pointers (`std::unique_ptr`, `std::shared_ptr`) instead of raw pointers

### Object lifecycle

- An object must be constructed (initialized) before it is used and will be destroyed at the end of its scope.
    - For a namespace object the point of destruction is the end of the program.
    - For a member, the point of destruction is determined by the point of destruction of the object of which it is a member.
    - An object created by new “lives” until destroyed by `delete` (or `delete[]` for arrays).
        - `delete` frees the memory, doesn't "destroy" the pointer
- Once the object is deleted, it's a good practice to set the pointer to `nullptr` to avoid dangling pointers
- It's important to delete the pointer (free the memory) before the pointer goes out of scope or is reassigned

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

## Templates

- compile-time - code generation
- classes, functions, constructors, ...

```c++
template<typename T>
class Vector {
private:
        T* elem;  // elem points to an array of sz elements of type T
        int sz;
```

- **value template arguments**

```c++
template<typename T, int N>
struct Buffer {
        constexpr int size() { return N; }
        T elem[N]; 
```

## Operator overloading

- `operator()` **application operator**, also called “function call” or just “call”
- `operator[]` **subscript operator**
- `operator""` - user-defined literals

## Lambdas

- `[&](int a){ return a<x; }`
    - `[]` - **capture list**
        - `&` - capture by reference
        - `=` - capture by value (copy)
        - `this` - capture the `this` pointer
        - `a, b` - capture just `a` and `b` by value
    - ``

## Attributes

- `[[deprecated]]`
- `[[nodiscard]]` - compiler will raise a warning if the function return value is not used
    - applies to pure functions, i.e. when the function has no side effects and calling it without using the returned value makes no sense
- `[[likely]]` and `[[unlikely]]` - hint to the compiler about the expected branch