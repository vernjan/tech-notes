# Asymptotic Analysis (Big O)

## Sources
- [What is Big O Notation Explained: Space and Time Complexity](https://www.freecodecamp.org/news/big-o-notation-why-it-matters-and-why-it-doesnt-1674cfa8a23c/) (freeCodeCamp article)
- [Big O Notation](https://www.youtube.com/watch?v=v4cd1O4zkGw) (YouTube HackerRank)
- [What Is Big O? (Comparing Algorithms)](https://www.youtube.com/watch?v=MyeV2_tGqvw) (YouTube UndefinedBehavior)
- [Data Structures for Coding Interviews in Java - Complexity Measures](https://www.educative.io/courses/data-structures-coding-interviews-java) (Educative)

## Overview
- gives us an idea of how complex the algorithm is with respect to the input size(s)
- the algorithm complexity won't grow any faster than _a constant multiple of `g(n)`_
    - for example, `O(n^2)` tells us that for a sufficiently big input (`> n0`) it won't grow any faster than `c * n^2`
    - doesn't hold for **all** values, but must hold for all values above the given threshold (`n0`)
- therefore, we only care about the _dominant terms_, and we do not care about the leading coefficients (constants)
    - `n^2 + 5n + 5` belongs to `O(n^2)`
- Big O can be used for both **time** and **space** (memory) complexity

![](_img/big-o.jpg)

**Source**: https://www.bigocheatsheet.com/

### Naming conventions
- `O(1)` - constant
- `O(log n)` - logarithmic
- `O(n)` - linear
- `O(n^2)` - squared
- `O(N^3)` - cubed
- `O(2^n)` - exponential

## Common examples
| Algorithm                      | Big O      | Notes                        |
|--------------------------------|------------|------------------------------|
| basic loop                     | O(n)       |                              |
| loop with k increment (`i+=3`) | O(n)       | coefficients are dropped     |
| loop with multiplied increment | O(logk(n)) |                              |
| independent nested loop        | O(n*m)     | letters represent 2 inputs   |
| dependent nested loop          | O(n^2)     |                              |

## Cheat sheet
See [Big-O Cheat Sheet](https://www.bigocheatsheet.com/)

## Other asymptotic notations
- **Big O** - upper bound
    - `f(n) <= c * g(n)`
    - for sufficiently large values of `n`, `f(n)` will grow no faster than a constant multiple of `g(n)`
- **Big Omega** - lower bound
    - `f(n) >= c * g(n)`
    - for sufficiently large values of `n`, `f(n)` will grow at least as fast as a constant multiple of `g(n)`
- **Big Theta** - exact bound
    - ` c_1 * g(n) <= f(n) <= c_2 * g(n)`
    - in fact, Big Theta is what the _industry_ means by Big O

### Example - Linear search in array
- **Big O**: `O(n), O(n^2), O(n!), ...` - all is technically correct (upper bound)
- **Big Omega**: `O(1), O(log n) O(n), ...` - all is technically correct (lower bound)
- **Big Theta**: `O(n)`

## Best, average and worst case
- no relation whatsoever to Big O, Big Omega and others - those are different concepts, don't confuse them
- average and worst case are interesting

## Amortized cost
- for example **ArrayList**
    - insert is `O(1)` except the case when the backing array gets full and must be resized `O(n)`
    - resize doubles the original array, it happens after 8, 16, 32, 64, ... inserts (sums up to `2*[number of inserts]`)
    - in total, the (amortized) cost of insert remains constant

## Gotchas
- `O(log2(n!) = O(n*log2(n))` (without `O` function, it's not `=` but `<`)
- `O(e^3n) != O(e^n)` !!! This is not a constant to be dropped, think `O(n^2)` vs. `O(n^3)`