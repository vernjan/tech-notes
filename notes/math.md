# Math

## Sources
- 📙 Cracking the Coding Interview - Math and Logic Puzzles
- [Výroková logika](http://www.nabla.cz/obsah/matematika/vyrokova-logika-vyrok-negace-konjunkce-disjunkce-implikace-ekvivalence.php)
- [Matematika polopatě](https://www.matweb.cz/)

## Common equations
- `a^n * b^n = (a*b)^n`
- `SUM 1..n = n * (n + 1) / 2` (sum of integers 1 through N) - think combining pairs: `0+5 + 1+4 + 2+3`
- `SUM 2^n = 2^(n + 1) - 1` (sum of powers of 2) - example `n=5: 16+8+4+2+1 = 32-1`
- `log(a) + log(b) = log(a*b)`
- `logb(k) = c` --> `k = b^c`
- `log2(a) = log10(a) / log10(2)`
- `log10(a) = log2(a) / log2(10)`

## Combinatorics

|                                                             | Formulae             | Example                        |
|-------------------------------------------------------------|----------------------|--------------------------------|
| **permutation**                                             | `n!`                 | `ABC, ACB, BAC, BCA, CAB, CBA` |
| **k-permutation** (or partial permutation, "česky variace") | `n! / (n - k)!`      | `k=2: AC, AB, BA, BC, CA, CB`  |
| **combination** (orderless, `(n_k)`)                        | `n! / (n - k)! * k!` | `k=2: AB, AC, BC`              |
| **k-permutation with reps** (think password generator)      | `n^k`                | `k=2: AA, AB, BA, BB`          |
| **power sets** (all subsets of a set)                       | `2^n`                | `n=2: {}, A, B, AB`            |

- **permutation**: `n! = n * (n-1) * (n-2) * ... * 1` - think how many options we have in each step
- **k-permutation**: `n! / (n - k)! = n * (n-1) * (n-2) * ... * (n-k+1)` - same as permutation, we just "stop earlier"
- **combination**: same as k-permutation, we just need to reduce it by permutation of `k` because the order doesn't matter

## Prime numbers
- **0 and 1 are not prime numbers**
- every positive integer can be decomposed into a product of primes (_factorization_)

### Checking for primality
- naive - test all numbers between `2 and n squared`
- the sieve of eratosthenes

### Greatest common divider
- **coprime numbers** - 2 numbers which have GCD 1 (for example 2 and 28)
- Euclid's algorithm - find the greatest common divisor (GCD) of 2 numbers
  ```
  public static int gcd(int num1, int num2) {
      if (num1 % num2 == 0) {
          return num2;
      }
      return gcd(num2, num1 % num2);
  }
  ```

## Prefix, infix, postfix
- **prefix** - topological
- **infix** - readable for humans but not for computers, require parentheses
- **postfix** - ideal for computer, requires little memory

| Prefix  | Infix          | Postfix |
|---------|----------------|---------|
| +AB     | A + B          | AB+     |
| -+ABC   | A + B - C      | AB+C-   |
| -*+ABCD | (A + B) * C -D | AB+C*D- |

- conversion by hand is quite easy - start evaluating subexpressions one by one, the key is to start at the right place

## Boolean algebra
[Boolean Expressions Calculator](https://www.dcode.fr/boolean-expressions-calculator)

- **implication** `=>`

| A   | B   | Result |
|-----|-----|--------|
| 1   | 1   | 1      |
| 1   | 0   | 0      |
| 0   | 1   | 1      |
| 0   | 0   | 1      |

- **equivalence** `<=>`

| A   | B   | Result |
|-----|-----|--------|
| 1   | 1   | 1      |
| 1   | 0   | 0      |
| 0   | 1   | 0      |
| 0   | 0   | 1      |

- `!(a && b)` == `!a || !b`
- `!(a || b)` == `!a && !b`