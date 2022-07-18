# Object-Oriented Python
- methods and properties can be added to object dynamically

## Class
```
class Car:
    pass
```

## Initializers (constructors)
- special name `__init__`
```
def __init__(self, number):
    self.number = number
```

## Properties

### Class properties
```
class Car:
    instance_counter = 0
```            

### Instance properties
```
class Car:
    def __init__(self, name):
        self.name = name
```

## Methods
- **can't explicitly overloaded** - the latest definition will override the previous one
- implicit overloading - using **default values**

### Instance methods
- access to instance (and class) properties
- name convention for 1st param - `self`
```python
class Car:

    def print_id(self):
        print(id(self))
```

### Class methods
- access to class properties
- use annotation `@classmethod`
- name convention for 1st param - `cls`

```python
class Car:
    instance_counter = 0

    @classmethod
    def print_counter(cls):
        print(cls.instance_counter)
```

### Static methods
- no access to any properties (util methods)
- use annotation `@staticmethod`
```python
class Car:

    @staticmethod
    def print_hello():
        print("Hello from Car class")
```

## Example
```python
class Car:
    counter = 0

    def __init__(self, name="unknown"):
        self.name = name
        self.speed = 0

        Car.counter += 1

    def go(self, speed):
        self.speed = speed

    def print_status(self):
        print("%s is going %d mph" % (self.name, self.speed))


car1 = Car("Car1")
car1.go(150)
car1.print_status()

car2 = Car("Car2")
car2.print_status()

print(Car.counter)
```



## Inheritance
- multiple inheritance is allowed
- `super()` (with parenthesis) to refer to the parent class/object
    - unlike Java, call to _super_ doesn't have to be on the first line in a constructor

```
class MyChild(MyParent1, ...):
    def __init__(self, ...):
        super().__init__(...)
        ...
```

## Abstract base class
- not natively supported, import from `abc` module
```
from abc import ABC, abstractmethod


class Shape(ABC):  # Shape is a child class of ABC
    @abstractmethod
    def area(self):
        pass

```