# Pointers & References

## Pass-by-value/reference

- pass-by-value - **copy** of the value is passed to the function
    - also applies to return values and variable assignments
    - default in C++
- pass-by-reference - **reference** (alias) - use `&` operator (`int& foo`)
    - no copy is made (which is faster)
    - can change the original value
      ```c++
      void swap(int& a, int& b) {  // a, b arguments must be variables, not literals
          int tmp = a;
          a = b;
          b = tmp;
      }
      ```
    - in some cases we might want to just pass by reference, but not change the original value - use `const` reference
      ```c++
      void print(const int& a) {
          // a = 5;  // error
          std::cout << a << std::endl;
      }
      ```
- user pointers to avoid copying large objects, the objects must be allocated on the heap

## Pointers

- **pointer** - variable that stores the memory address of another variable
- `int* p` - pointer to an integer (integer pointer)
- pointer can point to another pointer
    ```c++
    double d = 3.14;
    double*   dPtr1 = &d;
    double**  dPtr2 = &dPtr1;
    double*** dPtr3 = &dPtr2;
    ```
- `delete` frees the memory, doesn't change the pointer value! (must not be called twice)
- `delete []` - for arrays, no need to delete the individual elements, unless they are pointers
- **dangling pointers** - points to deleted memory

### Const pointers

```c++
int *const p = &x;  // p is a const pointer to an int - pointer cannot be reassigned: won't compile p = nullptr; this is a reference
const int *p = &x;  // p is a pointer to a const int - value cannot be changed: won't compile *p = 5;
const int *const p = &x;  // p is a const pointer to a const int, this is a const reference
```

- `int const ..` is the same as `const int ..`
- reference is a const pointer that is automatically dereferenced and must always be initialized (no `nullptr`)

#### Double const pointer

```
const int *const *const p2 = &p; // const pointer to const pointer to const int
p2 = nullptr;  // won't compile
*p2 = &x;      // won't compile
**p2 = 0;      // won't compile
```

### Array pointers

- pointer to array of ints - `int *p = arr;`
- pointer to array of int pointers - `int **p = arr; // double pointer`

### Function pointers

```c++
using void (*)(struct iocb *) aio_callback;  // function pointer
void functionName(struct iocb *arg)) { ... } // function
```

aio_callback is a pointer to a function that takes a pointer to a struct iocb and returns void

## References

- similar to pointers
    - `int x = 5; int &rx = x;` - `rx` is a reference to `x`
    - reference must be initialized when declared and cannot be changed later (cannot point to another variable/memory location)
    - reference cannot point to `nullptr`
    - const references - value is read-only (same as const pointer to const data/type)

### Lvalues and Rvalues

- every expression is either an lvalue or an rvalue
    - rvalue can be subdivided into xvalue and pure rvalues

- **lvalue reference** - `T& t`
    - left value = an expressions that yields object reference ("has a memory address/storage")
        - variable name - `int x = 5;`
        - array subscript reference - `arr[2] = 5;`
        - dereferenced pointer - `*p = 5;`
        - function call that returns a reference - `int & foo(); foo() = 5;`
        - increment/decrement operators - `x += 5; --x;`
        - struct members - `foo.bar = 10`
    - **const lvalue reference** - `const T& t`
        - can bind to rvalues - `const int& x = 5;`
        - can be used to pass temporary objects to functions
        - can be used to pass literals to functions
        - can be used to pass expressions
- **rvalue reference** - `T&& t`
    - right value = "not an lvalue" - temporary value, no name, no memory address/storage
        - the goal of rvalues is to enable move semantics and perfect forwarding
        - literal - `5`
        - expression like - `5 + 1`
        - temporary object - `Foo()`
        - function call that returns a temporary object - `foo()`
        - cast - `(int) 5`
        - `std::move` - `std::move(x)` - converts `x` to an rvalue

- An lvalue is converted implicitly to an rvalue when necessary, but an rvalue cannot be implicitly converted to an lvalue.

### Move semantics

- my understanding - if a function declares it accepts `&& t`, it's telling the caller that it will cripple the argument by riping out and
  taking its internals
- functions and constructors usually comes in pairs ("copy and move"):
    - `foo(const T &t)` - "slower", lvalue reference
    - `foo(T &&t)` - "faster", rvalue reference, the idea is to "steal" from the temporary object
        - `std::move` - converts an lvalue to an rvalue (sometimes we want to change lvalue to rvalue), no other effect at all

### Perfect forwarding

- `std::forward` - forwards the argument as an lvalue or rvalue
- used in templates to preserve the value category (lvalue or rvalue) of the argument
- reference collapsing rules - reference to a reference is just a reference:
    - `T& &`   -> `T&`
    - `T& &&`  -> `T&`
    - `T&& &`  -> `T&`
    - `T&& &&` -> `T&&`
- outside of templates, works like `std::move` (?)

### Special type deduction for rvalues

```
template <class T>
void func(T&& t) {
}
```

- This is quite different from "class" templates because class templates are resolved during object declaration
  while method templates are resolved during method call.
- Don't let `T&&` fool you here - `t` is not an rvalue reference. When it appears in a **type-deducing context** (
  templates, `auto`, `decltype`), `T&&` acquires a special meaning. When func is instantiated, `T` depends on whether the argument passed to
  func is an lvalue or an rvalue. If it's an lvalue of type U, T is deduced to U&. If it's an rvalue, T is deduced to U.

```c++
#include <iostream>
#include <utility>


struct Bar {
    int i;
};

struct Miau {
    static void YYY(Bar &b) { std::cout << "1"; }
    static void YYY(const Bar &) { std::cout << "2"; }
    static void YYY(Bar &&) { std::cout << "3"; }
    static void YYY(const Bar &&b) { std::cout << "4"; }
};

template<typename T>
struct Foo {
    //static void XXX(T t) { std::cout << "A"; }
    static void XXX(T &t) {
        std::cout << "B";
        Miau::YYY(t);
        Miau::YYY(std::forward<T>(t));// TODO Is there a reason to ever use forward if not in "type-deducing" context? Should I rather use std::move?
        Miau::YYY(std::move(t));
    }

    static void XXX(const T &t) {
        std::cout << "C";
        Miau::YYY(t);
        //        std::remove_const_t<T> t2 = t;
        Miau::YYY(std::forward<const T>(t));
        Miau::YYY(std::move(t));// Doesn't affect const qualifier
    }

    static void XXX(T &&t) {
        std::cout << "D";
        Miau::YYY(t);
        Miau::YYY(std::forward<T>(t));
        Miau::YYY(std::move(t));
    }

    template<typename Q>
    static void ZZZ(Q &&q) {// type-deducing context
        std::cout << "X";
        Miau::YYY(q);
        Miau::YYY(std::forward<Q>(q));
    }
};


int main() {
    Bar b1{};
    const Bar b2{1};
    Foo<Bar>::XXX(b1);// B
    std::cout << "\n";
    Foo<Bar>::XXX(b2);// C
    std::cout << "\n";
    Foo<Bar>::XXX(Bar{1});// D
    std::cout << "\n";
    Foo<Bar>::ZZZ(b1);// explicit template type: Foo<Bar>::ZZZ<Bar&>(b1);  Q = Bar&;  collapsed with Bar && to just Bar&
    std::cout << "\n";
    Foo<Bar>::ZZZ<Bar>(Bar{1});
    std::cout << "\n";
}

```

## Smart (Managed) pointers

- C++ 11 Standard
- `#include <memory>`
- no need to call `delete`
- `unique_ptr` - single owner, cannot be copied (only moved with `std::move`), deallocated when out of scope
- `shared_ptr` - reference counting, can be copied
- `weak_ptr` - non-owning reference to an object managed by `shared_ptr`
