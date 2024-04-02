# Pointers & References

## Pass-by-value/reference

- pass-by-value - **copy** of the value is passed to the function (also applies to return values), default in C++
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
- user pointers to avoid copying large objects, the objects must be allocated on the heap

## Pointers

- **pointer** - variable that stores the memory address of another variable
- `int *p` - pointer to an integer
- pointer can point to another pointer
    ```c++
    double d = 3.14;
    double* dPtr = &d;
    double** dPtr2 = &dPtr;
    double*** dPtr3 = &dPtr2;
    ```
- `delete` frees the memory, doesn't change the pointer value! (must not be called twice)
- `delete []` - for arrays, no need to delete the individual elements, unless they are pointers
- **dangling pointers** - points to deleted memory

### Const pointers

```c++
int* const p = &x;  // p is a const pointer to an int - pointer cannot be reassigned
const int* p = &x;  // p is a pointer to a const int - value cannot be changed
const int* const p = &x;  // p is a const pointer to a const int
```

### Array pointers

- pointer to array of ints - `int *p = arr;`
- pointer to array of int pointers - `int **p = arr;`

### Function pointers

```c++
using void (*)(struct iocb *) aio_callback; // function pointer
void functionName(struct iocb *arg)) { ... } // function
```

aio_callback is a pointer to a function that takes a pointer to a struct iocb and returns void

## References

- similar to pointers
    - `int x = 5; int &rx = x;` - `rx` is a reference to `x`
    - reference must be initialized when declared and cannot be changed later (cannot point to another variable/memory location)
    - reference cannot point to `nullptr`
    - const references - value is read-only

- **lvalue reference** - `T& t`
- **rvalue reference** - `T&& t` - performance optimization to avoid unnecessary copies, works with `std:move`

## Smart (Managed) pointers

- C++ 11 Standard
- `#include <memory>`
- no need to call `delete`
- `unique_ptr` - single owner, cannot be copied (only moved with `std::move`), deallocated when out of scope
- `shared_ptr` - reference counting, can be copied
- `weak_ptr` - non-owning reference to an object managed by `shared_ptr`
