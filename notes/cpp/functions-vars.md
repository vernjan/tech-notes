# Functions & Variables

## Variables

- C++ supports **global variables**
- `const` - constant, cannot be changed later
    - objects cannot be modified - i.e. you can call just const methods
    - it's more strict than Java's `final`
- `static` - C++ supports **static local variables**
    - static variable, initialized only once, keeps its value between function calls
    - behaves like a global variable but with a limited scope
- `if` can declare variables - scope limited

## Functions

- default is pass by value (copy)
- function must be declared before used - **function prototypes** (good practice)
    - just header, with no body
- const methods - cannot modify the object
- can be defined outside of the class
- supports default arguments (best defined on prototypes, cannot be defined on both prototype and definition)