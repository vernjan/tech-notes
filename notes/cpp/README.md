# C++

- [Functions & variables](functions-vars.md)
- [Initialization & assignment](initialization-assignment.md)
- [Pointers & references](pointers-refs.md)
- [STL](STL.md)
- [Containers](containers.md)
- [OOP](OOP.md)
- [Features](features.md)

## Reference

- [C++](https://en.cppreference.com/w/cpp)
- [C++ Language](https://en.cppreference.com/w/cpp/language)

## Basics

- compatible with C (or at least used to be)
- basic syntax is quite similar to Java
- `std::endl` vs `\n` - `std::endl` flushes the buffer, `\n` doesn't
    - flushing the buffer can be expensive, so use `\n` unless you need to flush the buffer (log statements, ...)
- `gcc` - GNU Compiler Collection
- `g++` - GNU C++ Compiler (C++ frontend for `gcc`, under the hood calls `gcc` with some flags)
- standard library is installed together with the compiler, located in `/usr/include/c++/VERSION`
    - `VERSION` is the version of the compiler, not C++ standard
    - unlike Java, compilers implement the new standards incrementally -
      see [C++ compiler support](https://en.cppreference.com/w/cpp/compiler_support)

## Compilation

## Libraries

- **static libraries** - `.a` files
    - part of the executable
- **dynamic libraries** - `.so` files (Linux), `.dll` files (Windows)
    - loaded at runtime

## Types

### Fundamental types

- **integers**
    - `signed`, `unsigned`
    - `short` - ~ 2 bytes (depends on the compiler/platform)
    - `long` - ~ 4 bytes
    - `long long` ~ 8 bytes
    - `int64`, `uint64`, ..
        ```c++
        typedef signed long int __int64_t;
        typedef unsigned long int __uint64_t;
        ```
- **floating numbers**
    - float, double, long double
- **characters**
    - `signed`, `unsigned`
    - `char` - 1 byte
    - `wchar_t` - 2 bytes (unicode) - uses prefix `L`
    - and more
- **boolean**
    - `true` = 1
    - `false` = 0
- `std::Byte` - 8 bits
- `size-t`

### Java comparison

- `auto` ~ `var`
- `nullptr` ~ `null`
- `include` ~ `import`
    - `include <something>` - search in system directories (STL)
    - `include "something"` - search in the current directory
- `using NAMESPACE` ~ `static import`
- `const var` ~ `final var`
- `templates` ~ `generics`, templates can do much more (compile-time code generation)
- `static` ~ `private static` - static objects/functions are not exported outside the CPP file
- `extern` ~ `public static`
- `thread_local` modifier ~ `ThreadLocal` class
- boolean expressions - `0` is `false`, anything else is `true`
    - `nullptr` is `0`, i.e. `false`
- C++
    - `char` is just a 1-byte integer
        - no `byte` type, use `char`
        - use `wchar_t` for Unicode
    - arrays don't know their size, either use `std::array` or hold the size separately
    - `[]` no range checks (containers, arrays) - goes into invalid memory

## Exception handling

1) Use error codes - failure is normal and expected (like reading a file), immediate caller
2) throw exception - caller is not immediate, undo action is possible
3) Terminate - irrecoverable errors

- `noexcept` - function will not throw exceptions
- `try { .. } catch (std::exception& e) { .. }`
- `try { .. } catch (...) { .. }` - expression `...` catches all exceptions

## Namespaces

- to avoid name collisions and organize code
- `::` - scope resolution operator
- global namespace - no prefix, we can even use e.g. `::MyObject`
- `using namespace std` - imports everything from a given namespace, not really recommended because it pollutes the global namespace
- `using std::cout, std::string` - selective imports - recommended
- `using foo = unsigned int` - aliases (types, function pointers, ...)
    - `using size_t = unsigned int;` - implementation specific, some compilers use `unsigned long` - dynamic!
    - template param partial binding - `template <typename K> using Map<K> = std::Map<K, Foo>;`
- `using` can be used on the global (namespace) level, in a function, or in a block

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

## Strings

- `std::string` is a class, not a primitive type
- is mutable
- `string s = "aaa"; s[0] = 'b';` works
    - you can use `const` to make it immutable
- `<cctype>` - `isalnum, isalpha, is..` util functions
- `<<` read by word, `getline(&s)` read by line
- C-style string is an array of characters terminated by a null character
    - best avoided
    -
- `"foo"` literal is `const char[N]`, to make it a string use suffix `s`

## Conversions

- prefer brace initialization (`int{5}`), it prevents most of the undefined and weird behavior
- any pointer can be implicitly converted to
    - `bool` - `nullptr` is `false`, anything else is `true`
    - `void*` pointer
- any number can be implicitly converted to
    - `bool` - `0` is `false`, anything else is `true`

### Type casting

#### Braced initialization

- always type safe and non-narrowing

#### C-style cast

- `(desired-type)object-to-cast` - mostly for compatibility with C, better avoid

#### User-Defined Type Conversions

```c++
[explicit] operator destination-type() const { }
```

- if explicit, compiler will not perform implicit conversions, a static cast is required

**Example**

```
operator bool() const { }
```

#### C++ casts

- explicit type conversions

- **static_cast** - compile-time cast
    - `static_cast <new_type> (expression);`
    - used to convert between related types (e.g. int to double or inherited classes)
- **dynamic_cast** - runtime cast - polymorphism
    - `dynamic_cast <new_type> (expression);`
    - mainly used to perform _downcasting_ (converting a pointer/reference of a base class to a derived class)
    - dynamic cast to a reference type - if the cast fails, an exception of type `std::bad_cast` is thrown
    - dynamic cast to a pointer type - if the cast fails, the result is a null pointer of the target type
- **const_cast** - cast away constness
    - `const_cast <new_type> (expression);`
    - used to add or remove `const` or `volatile` qualifiers
- **reinterpret_cast** - low-level cast
    - `reinterpret_cast <new_type> (expression);`
    - used to convert the pointer to any other type of pointer
    - no type checking is performed

## Snippets

- `!!err` is the same as `!(!err)` which means `err != nullptr`
    - `err` is a pointer
    - see https://stackoverflow.com/questions/11374810/defining-double-exclamation

## Memory management

- **dynamic memory** (heap, free store) - allocated at runtime
    - option 1 - `new` & `delete` - "C++" style (preferred)
        - `new` returns a pointer to the allocated memory
            - `int* myInt = new int(123);`
        - `delete` frees the memory
            - `delete myInt;`
    - option 2 - `malloc` & `free` - "C" style (avoid if possible)
        - `malloc` returns a pointer to the allocated memory
            - `int* myInt = (int*) malloc(sizeof(int));`
        - `free` frees the memory
            - `free(myInt);`
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

- templates provide a general mechanism for compile-time programming (code generation)
- templates are compile-time while virtual methods are runtime
- classes, functions, constructors, variables, ...

```c++
template<typename T>
class Vector {
private:
        T* elem;  // elem points to an array of sz elements of type T
        int sz;

// variable template
template<typename T>
constexpr T pi = T(3.1415926535897932385);
```

- **value template arguments**

```c++
template<typename T, int N>
struct Buffer {
        constexpr int size() { return N; }
        T elem[N]; 
```

## Operator overloading

- `operator[]`**subscript operator**
- `operator=` **assignment operator**
- `operator()` **application operator**, also called “function call” or just “call”
- `operator""` - user-defined literals
- `void * operator new(size_t size)` - custom memory allocation
- `void operator delete(void * p)` - custom memory deallocation

### placement new operator

- `void* operator new(size_t size, void * p);`
- `void operator delete(size_t size, void * p);`
- allows to construct an object in a pre-allocated memory
- constructed object must not be deleted with `delete`, a destructor must be called explicitly
- `new (address) Type;`
- see https://www.geeksforgeeks.org/placement-new-operator-cpp/

## Lambdas

- `[&](int a){ return a<x; }`
    - `[]` - **capture list**
        - `&` - capture by reference
        - `=` - capture by value (copy)
        - `this` - capture the `this` pointer
        - `a, b` - capture just `a` and `b` by value
- `mutable` - allows the lambda to modify the captured variables

## Attributes

- `[[deprecated]]`
- `[[nodiscard]]` - compiler will raise a warning if the function return value is not used
    - applies to pure functions, i.e. when the function has no side effects and calling it without using the returned value makes no sense
- `[[likely]]` and `[[unlikely]]` - hint to the compiler about the expected branch

## I/O File

- similar to `cout/cin`, uses `<<` and `>>` operators

```c++
#include <fstream>

// file write
ofstream myfile;
myfile.open("example.txt");
myfile << "Writing this to a file.\n";
myfile.close();

// file read
ifstream myfile;
myfile.open("example.txt");
string line;
while (!myfile.eof()) {
    getline(myfile, line);
    cout << line << endl;
}

```

## Compilation

- compile just `cpp` files, not `h` files (they are included in the `cpp` files)
- `g++ -o main main.cpp util.cpp` - compile and link
- 3 phases
    - files are compiled separately (aka **translation units)**, linker links them together
    - **preprocess** - process includes files (headers) and macros - one text file (translation unit)
    - **compile** - compile the preprocessed files (one by one, no dependencies, can be done in parallel) into object files (`foo.o`)
    - **link** - link object files and static libraries into an executable

## Arrays

- `[]` no range checks
- doesn't know its size, we always need to pass it
- values are not initialized by default!
    - we can provide fewer values than then total size, remaining values will be 0
        - `int counters[10] = {0}` - all zeroes
        - `int counters[10] = {1}` - 1 and nine 0s
- just a pointer to the first element
    - `int arr[10]` can be assigned as `int* ptr = arr`
- pointer arithmetic
    - `*ptr = 1` is the same as `arr[0] = 1`
    - `*(arr + 3)` is the same as `arr[3]`

## Compiler / Linker hints

https://stackoverflow.com/questions/1759300/when-should-i-write-the-keyword-inline-for-a-function-method

- **static**
    - "double-duty"
        - *internal linkage* - function/variable is only visible in the current file (translation unit)
        - lifetime is the entire program ("static")
- **extern**
    - *external linkage* - for global functions/variables, I'm saying it's defined somewhere else
    - implies lifetime is the entire program ("static")
- **inline** - this function will be defined in multiple translation units, don't worry about it

## Stack

- stack frames are added on top of each other (new stack frame has lower memory address than the previous one)
- frame consists of in the following order (ascending memory):
    - parameters
    - local variables
    - saved registers `rbp` and `rip`
- passing arguments between stack frames
    - **by reference** - pointer to the function argument is passed
    - **by value**
        - small objects (like ints) are copied directly into child's stack frame
        - large objects (like structs) are first copied on **parent's stack** as a new local variable and then a pointer to the copy is
          passed

## RAII

- **Resource Acquisition Is Initialization**
- pairing allocation with de-allocation - prevents memory leaks

```c++
struct Box {
    Box() { buffer = new char[1024]; }
    ~Box() { delete[] buffer; }

private:
    char * buffer;
}; 
```