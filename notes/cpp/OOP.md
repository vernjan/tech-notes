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
- `this` - **pointer** to the object that the method is called on
- always visible, no public/private/protected keywords for classes

### Aggregates/PODs

- struct, class with no constructors, methods, inheritance, virtual functions, private members
- initialized with braces `{}`

```c++

## Unions

- similar to `struct`, but all members share the same memory location
- only one member can be active at a time - to safe memory
- built-in STL support - `variant`

## Enumerations

- plain enums (C compatible, "named" integers") and enum classes

```c++
// plain enum - unscpoed
enum Color { red, blue, green };

// enum class - scoped
enum class Color { red, blue, green };
Color col = Color::red;
```

## Class essentials

- constructors, destructors, copy and move
- default implementations are provided by the compiler (except for the "ordinary" constructor)
    - `=default` - explicitly request the compiler to generate the default implementation (and no others)
    - `=delete` - explicitly prevent the compiler from generating the default implementation
- **constructor vs. assignment operator**
    ```c++
    // constructors - assigning to an uninitialized object, i.e. a new object (this) must be created
    A source(1);              // constructor
    A a = source;             // copy constructor 
    A b = std::move(source);  // move constructor
    
    // assignments - assigning to an existing object, i.e. the current object (this) is updated
    A source(1);
    A a(2);
    a = source;             // assignment operator
    A b(3);
    b = std::move(source);  // move assignment
    ```

### Default implementations

- **rule of five** - if you need to provide one of the special member functions, you should provide all of them

```c++
class X {
public:
        X(Sometype);                    // "ordinary" constructor: create an object
        X();                            // default constructor
        
        // rule of five:
        X(const X&);                    // copy constructor
        X(X&&);                         // move constructor
        X& operator=(const X&);         // copy assignment
        X& operator=(X&&);              // move assignment
        ~X();                           // destructor: clean up
};

```

There are five situations in which an object can be copied or moved:

- As the source of an assignment
    - uses assignment operator `operator=`
- As an object initializer
- As a function argument - `f(a);`
- As a function return value - `return a;`
- As an exception - `throw a;`

### Copy & move

- default **copy** is member-wise, pointers are also copied but not the data they point to (shallow copy)
- we can provide our own copy constructor and assignment operator to perform a deep copy
    ```c++
    Vector(const Vector& a);                // copy constructor
    Vector& operator=(const Vector& a);     // copy assignment
    ```

- **move** is used to transfer ownership of resources (e.g. memory) from one object to another
    - it's useful performance optimization
        ```c++
        X(X&&);                    // move constructor
        X& operator=(X&&);         // move assignment: clean up target and move
    
        Vector f()
        {
            Vector x(1000);
            Vector y(2000);
            Vector z(3000);
            z = x;                 // we get a copy (x might be used later in f())
            y = std::move(x);      // we get a move (move assignment), std::move gets us an rvalue
            // ... better not use x here ...
            return z;              // we get a move (? compiler optimization ?)
        }
        ```

### Copy constructor

1) When an object of the class is **returned by value**.
2) When an object of the class is **passed (to a function) by value as an argument**.
3) When an object **is constructed based on another object** of the same class.
4) When the compiler generates a temporary object.

### Member initializer list

- `: member1(val1), member2(val2) {}`
- member variables are initialized before the constructor body is executed
- can be used to initialize `const` members
- members can belong to this or super class

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

## Virtual functions

- **polymorphic** - if the method is not virtual, it's not runtime polymorphic (static binding, like Java overloaded methods)
- `virtual int star1() const = 0;` =0 means **pure virtual function** and makes the class _abstract_
    - abstract class cannot be instantiated
    - derived class must override the pure virtual function

## Friend classes and functions

- class declares a friend class or function
- the friend class can access its private data

```c++
class A {
    friend class B;
    friend void f(A & a);
};
```

## `static` in classes

- works similarly to Java
- just call as `MyClass::staticMethod()` or `MyClass::staticVar`