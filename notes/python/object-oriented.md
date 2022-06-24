# Object-oriented Python

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