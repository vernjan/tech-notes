# Object-Oriented Python

```
class Car:
    speed = 0

    def go(self, speed):
        self.speed = speed

    def print_status(self):
        print("Going %d" % self.speed)


car = Car()
car.go(150)
car.print_status()
```

## Constructors
```
def __init__(self, number):
       self.number = number
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