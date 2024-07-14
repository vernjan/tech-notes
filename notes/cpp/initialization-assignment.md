# Initialization & Assignment

- also takes place during function calls: **function parameters** and the **function return values** are also initialized
    - (remember - values are copied)
- no-arg constructors
    - call like `Point p;` (no parentheses) - with parentheses it's a function declaration

## Initialization

### 1) Direct-initialization

```c++
Point p1(1, 2); // calls ctor
```

### 2) Copy-initialization

- calls copy ctor
    ```c++
    Point p2 = p1;                              // variable init
    Point foo() { Point(1, 2) p; return p }     // function return value
    foo(p1);                                    // function parameter
    Point p3(p2);                               // direct call of copy ctor
    ```

- **note: **copy ctor is not called for unscoped (unnamed) temporary objects
    ```c++
    Point p2 = Point(1, 2);
    Point foo() { return Point(1, 2) }
    foo(Point(1, 2));
    ```

### 3) Aggregate/POD initialization

- a bit like Java's `POJO` (Plain Old Java Object)
- **aggregate** - array or class with
    - no user-declared constructors (`default` constructor is allowed),
    - no private or protected non-static data members,
    - no base classes,
    - and no virtual functions

```c++
Pod p{1, 2};    // Pod is an aggregate
Pod p{};        // default initialization - all fields are zeroed
Pod p{1};       // same as {1, 0}
```

#### Arrays

```c++
int array_1[]{ 1, 2, 3 };   // Array of length 3; 1, 2, 3
int array_2[5]{};           // Array of length 5; 0, 0, 0, 0, 0
int array_3[5]{ 1, 2, 3 };  // Array of length 5; 1, 2, 3, 0, 0
int array_4[5];             // Array of length 5; uninitialized values
```

### 4) List initialization

- since C++11
- initializes an object from **braced-init-list** (constructors, methods)
- prevents narrowing conversions
- first looks for `std::initializer_list` (with matching type), then for constructor with matching arguments, or aggregates
    - see https://en.cppreference.com/w/cpp/utility/initializer_list

```c++
Point p1{1, 1};      direct-list initialization
Point p1 = {1, 1};   copy-list initialization (doesn't really call copy constructor)
foo({1, 2, 3});      method call (method accepts std::initializer_list<int>)
```

## Assignment

- **assignment operator** is called when an object is assigned a new value
- doesn't happen on object initialization, the variable must be already initialized

```c++
Point p1 = Point(1, 2); // not assignment, but copy-initialization
p1 = Point(3, 4);       // assignment
```