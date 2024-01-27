# C++

- compatible with C (or at least used to be)
- basic syntax is quite similar to Java

## Java comparison

- `auto` ~ `var`
- `nullptr` ~ `null`
- `include` ~ `import`
- `using NAMESPACE` ~ `static import`
- `const` ~ `final`

## Features

- initialization
    - standard: `int a = 5;`
    - using double brackets: `int a {5}`, `int a[] {1, 2, 3}`

## Variables

- C++ supports **global variables**
- `const` - constant, cannot be changed later
- `static` - C++ supports **static local variables**
    - static variable, initialized only once, keeps its value between function calls
    - behaves like a global variable but with a limited scope

## Functions

- function must be declared before used - **function prototypes**
    - just header, with no body
- const methods - cannot modify the object

### Pass-by-value/reference

- pass-by-value - **copy** of the value is passed to the function, default in C++
- pass-by-reference - **reference** (alias) - use `&` operator (`int &foo`)
    - no copy is made (performance optimization)
    - can change the original value
      ```c++
      void swap(int &a, int &b) {  // a, b arguments must be variables, not literals
          int tmp = a;
          a = b;
          b = tmp;
      }
      ```
    - in some cases we might want to just pass by reference, but not change the original value - use `const` reference
      ```c++
      void print(const int &a) {
          // a = 5;  // error
          std::cout << a << std::endl;
      }
      ```

## OOP

- `class` vs `struct` - class was introduced in C++, very similar to struct, except for visibility rules for its members
    - `class` - default visibility is `private`
    - `struct` - default visibility is `public`
- `obj->method()` is a shortcut for `(*obj).method()`

## `struct`

TBD

## Containers

- `array` - OO version of built-in array
- `vector` - dynamic array (~ArrayList)

## Snippets

- `!!err` is the same as `!(!err)` which means `err != nullptr`
    - `err` is a pointer
    - see https://stackoverflow.com/questions/11374810/defining-double-exclamation
