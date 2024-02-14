# OOP

```
Rectangle r2 = Rectangle(5, 6);         // stack
Rectangle * r3 = new Rectangle(5, 6);   // heap (pointer)
```

## Structs & Classes

- `class` vs. `struct` - class was introduced in C++, same as struct, except for visibility rules for its members
    - `class` - default visibility is `private`
    - `struct` - default visibility is `public`
- `obj->method()` is a shortcut for `(*obj).method()`
- **member initializer list** - `: member1(val1), member2(val2) {}`
    - member variables are initialized before the constructor body is executed
    - can be used to initialize `const` members
    - members can belong to this or super class
- `std::initializer_list` - initializer list for constructors (for containers)
    - has impact on compiler - `Vector v = {1, 2, 3};`
- **object construction**
    - constructor - `Point p(1, 1);` (the same as `Point p = Point(1, 1);`)
    - member initialization - `Point p {1, 1};`

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

## Class essentials

- constructors, destructors, copy and move
- default implementations are provided by the compiler (except for the "ordinary" constructor)
    - `=default` - explicitly request the compiler to generate the default implementation (and no others)
    - `=delete` - explicitly prevent the compiler from generating the default implementation

```c++
class X {
public:
        X(Sometype);                    // "ordinary" constructor: create an object
        X();                            // default constructor
        X(const X&);                    // copy constructor
        X(X&&);                         // move constructor
        X& operator=(const X&);         // copy assignment: clean up target and copy
        X& operator=(X&&);              // move assignment: clean up target and move
        ~X();                           // destructor: clean up
};

```

There are five situations in which an object can be copied or moved:

- As the source of an assignment - `X b = a;`
    - uses assignment operator `operator=`
- As an object initializer - `X a(1);` or `X a = X(1)`
    - calls a constructor, not an assignment
- As a function argument - `f(a);`
- As a function return value - `return a;`
- As an exception - `throw a;`

### Copy & move constructor

### Converting constructor (`explicit`)

- constructor that can be called with a single argument
- can be used for implicit type conversion, use `explicit` to prevent it

```c++
struct Foo {
  Foo(int x) {} // converting constructor
};
Foo f = 5;  // works, implicit conversion, can be prevented with `explicit`
 ```

### Default constructor (`default`)

- prefer to `A() = {}`, see https://stackoverflow.com/questions/20828907/the-new-syntax-default-in-c11

```c++
class A
{
public:
    int x;
    A()=default;
};

```


