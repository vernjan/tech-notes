# C++

- compatible with C
- basic syntax is similar to Java

## Java comparison

- `auto` ~ `var`
- `nullptr` ~ `null`
- `include` ~ `import`
- `using NAMESPACE` ~ `static import`
- `const` ~ `final`

## Features

- initialization
    - `int a = 5;`
    - double brackets - `int a {5}`, `int a[] {1, 2, 3}`

## Variables

- C++ supports **global variables**
- `const` - constant, cannot be changed later
- `static` - C++ supports **static local variables**
    - static variable, initialized only once, keeps its value between function calls
    - behaves like a global variable but with limited scope

## Functions

- function must be declared before used - **function prototypes**
    - function header, has no body

### Pass-by-value/reference

- pass-by-value - **copy** of the value is passed to the function, default in C++
- pass-by-reference - **reference** (alias), can change the original value, use `&` operator (`int &foo`)
    ```c++
    void swap(int &a, int &b) {  // a, b arguments must be variables, not literals
        int tmp = a;
        a = b;
        b = tmp;
    }
    ```

## Containers

- `array` - OO version of built-in array
- `vector` - dynamic array (~ArrayList)

## Snippets

- `!!err` is the same as `!(!err)` which means `err != nullptr`
    - `err` is a pointer
    - see https://stackoverflow.com/questions/11374810/defining-double-exclamation
