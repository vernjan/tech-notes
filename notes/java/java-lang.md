# Java Language

## Sources
- 📙 Effective Java by Joshua Bloch
- [Jagged Array in Java](https://www.geeksforgeeks.org/jagged-array-in-java/) (GeeksForGeeks)
- [Cglib, Javassist, JDK dynamic proxy](https://programmer.group/cglib-javassist-jdk-dynamic-proxy.html) (Programmer Group)
- [Method Overloading with Autoboxing and Widening in Java](https://www.geeksforgeeks.org/method-overloading-autoboxing-widening-java/) (GeeksForGeeks)
- [How to make the most of Java enums](https://blogs.oracle.com/javamagazine/post/how-to-make-the-most-of-java-enums) (Oracle blog)

## Generics
- **invariant** - default
- **covariant** (PE - producers _extends_, e.g. reading from collection)
  ```
  List<? extends Number> l = new ArrayList<Integer>();
  Number number = l.get(0);
  l.add(null); // nothing else
  ```
- **contravariant** (CS - consumer _supports_, e.g. adding values to collection)
  ```
  List<? super Number> l = new ArrayList<Object>();
  Object object = l.get(0); // always object
  l.add(5);
  ```

### Arrays and generics
- don't combine - arrays are _covariant_ and _reified_ (type parameter is preserved at runtime)
    - **covariant** - `Object[] objects = new String[10]; // ok compile`
    - **reified** - type safety is checked at runtime (generics are not reified, type is erased at compile time)

## Arrays
- `Array.equals` compares just the array refs (`arr1 == arr2`)
    - `Arrays.equals` call equals on all elements - use for 1D arrays
    - `Arrays.deepEquals` make deep comparison - use for nested multidimensional arrays
- `List.toArray()` - returns `Object[]`
- `List.toArray(T[] a)` - returns `T[]` - can't be used for primitive types (use Guava or Stream API)
- `Arrays.binarySearch(..)` - arrays must be **sorted**

### Jagged arrays
```
Integer[][] array1 = {{1, 4}, null, {9, 7, 8}, {}};

// OR semantically the same  
Integer[][] array2 = new Integer[4][];
array2[0] = new Integer[] {1, 4};
array2[1] = null;
array2[2] = new Integer[] {9, 7, 8};
array2[3] = new Integer[] {};
```

## Hashcode & equals
- always override `hashcode` when overriding `equals`
    - otherwise, hash based collections will be broken (`HashSet`, `HashMap`)
    - simply because hashcode will point (most likely) to a different bucket
- equals and subclass with new components is always broken (e.g. `Point` and `ColorPoint`)
    - use composition
- **equals rules**
    - reflexive `x.equals(x)`
    - symmetric `x.equals(y)` then `y.equals(x)`
    - transitive
    - consistent - repeated calls return the same value
    - if `x != null` then `x.equals(null)` returns null
- **hashcode rules**
    - consistent - repeated calls return the same value
    - if `x.equals(y)` then hashcodes must be the same (the opposite is not necessarily true)
    - distinct object may produce same hashcodes

## Comparator & Comparable
- `Comparable<T>` interface
    - imposes a total ordering (or _natural ordering_) on the objects of each class that implements i
    - `Collections.sort()` and `Arrays.sort()`
    - objects can be used with sorted sets and maps (without explicit comparator)
        - **consistent with equals** - iff `e1.compareTo(e2)` ~ `e1.equals(e2)`
        - BigDecimal is not consistent with equals
            - `"1.00 !equals "1.0"` but `"1.00" compareTo "1.0"`
- `Comparator<T>` interface
    - methods
        - `compareTo(T o1, T o2)`
        - default methods
            - `naturalOrder`
            - `reverseOrder`
            - `nullsFirst`
            - `thenComparing`
    - examples
        - `Comparator.nullsFirst(Comparator.reverseOrder())`
        - `Comparator.nullsFirst(Comparator.comparingInt(String::length))`

## Reflection
- allows introspecting and executing code
    - code diagrams, method intellisense, framework annotations
    - dynamic proxies, executing tests
- via `java.lang.Class` object
- getting Class object
    - `Class.forName(String)` - dynamic
    - `anObject.getClass()`
    - `aClass.class` - access to primitives (`void.class`, `int.class`) and arrays (`int[].class`)

## Dynamic proxy
- creating objects that act like instances of interfaces but allow for customized method invocation
- proxy class is a class created at runtime that implements a specified list of interfaces, known as proxy interfaces
- generating bytecode at runtime
- **target object** - the object being proxied
- **proxy object** - dynamically generated proxy

### JDK dynamic proxy
- `Proxy` class - factory for creating proxy objects
- `InvocationHandler` - implements proxy logic

```java
import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.lang.reflect.Proxy;

class ProxyExample {

    // dynamically generated proxy will implement this interface
    interface Person {
        String hi();
    }

    public static void main(String[] args) {

        final Person target = new Person() {

            @Override
            public String hi() {
                return "hi";
            }
        };

        InvocationHandler handler = new InvocationHandler() {

            @Override
            public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                System.out.println("Proxying method " + method);
                // custom logic
                return method.invoke(target, args); // returns "hi"
                // custom logic
            }
        };

        Person proxy = (Person) Proxy.newProxyInstance(Person.class.getClassLoader(),
                new Class<?>[] {Person.class}, // possibly multiple interfaces
                handler);

        proxy.hi();
    }

}
```

### Cglib, javassist
- similar to JDK
- differs in implementation details and some restrictions
- javassist is more general purpose (byte code manipulation)
- cglib
    - writes class bytecode using the [ASM framework](https://asm.ow2.io/)
    - no longer maintained, no docs

## Weak references
- [Package java.lang.ref](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/ref/WeakReference.html)
- [Weak References in Java](https://www.baeldung.com/java-weak-reference) (Baeldung)
- A weakly referenced object is cleared by the Garbage Collector when it's weakly reachable
    - i.e. object has neither **strong** nor **soft** references pointing to it
- `WeakHashMap`

## Autoboxing
- Rule of thumb - in most operations, **boxed primitives gets unboxed**
    ```
    Integer i1 = 1000;
    int i2 = 1000;
    boolean compared = (i1 == i2); // i1 is unboxed
    ```
- unboxing can throw NPE

## Overloading
- priority order for **primitive types**:
    - Same type > Auto Widening > Boxing > Upcasting (Parent Class) > Super Class
- priority order for **reference types**:
    - Same type > Upcasting (Parent Class) > Super Class > Unboxing

## String interning
- **Java String Pool** — the special memory region where Strings are stored by the JVM (off heap, since JDK8)
- `"foo"` - creates the String in the pool, or return the existing one
- `new String("foo")` - avoid, it creates a new object on the heap which references to the String pool
- `String.itern()` - return the reference into String pool
    - `new String("foo").intern() == "foo"`
- if the String is known at compile time, it's created in the String pool

## String concatenation
- `"a" + "b"` - a new StringBuilder is created behind the scenes by the compiler

## Reference types
- see [Types of References in Java](https://www.geeksforgeeks.org/types-references-java/) (GeeksForGeeks)
- **strong** - standard reference
- **weak** - eligible for gc if only referenced by weak references (`WeakHashMap`)

## Enums
- compiled into a class extending from `java.lang.Enum`
    - inherits `name()`, `ordinal()`, `valufOf(..)`
- enum constants become anonymous classes - they can implement their own methods

## Notes
- `Array.length`, `String.length()`, `Collection.size()`
- `null instanceof Foo` - always false, instance of null-safe (1t operator)
- avoid `float == float` and `double == double`, use `Float.compare` and `Double.comapre` - reason is `Float.NaN` and `Double.NaN`
- code blocks are executed before constructors
