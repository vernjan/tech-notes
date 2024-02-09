# Pointers & References

## Pass-by-value/reference

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
- user pointers to avoid copying large objects, the objects must be allocated on the heap

## Pointers

- **pointer** - variable that stores the memory address of another variable
- `int *p` - pointer to an integer

## References

- similar to pointers

    - `int x = 5; int &rx = x;` - `rx` is a reference to `x`
    - reference must be initialized when declared and cannot be changed later (cannot point to another variable/memory location)
    - reference cannot point to `nullptr`
    - const references - value is read-only

- **lvalue reference** - `T& t`
- **rvalue reference** - `T&& t` - performance optimization to avoid unnecessary copies, works with `std:move`