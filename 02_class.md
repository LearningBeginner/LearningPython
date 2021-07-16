# Class & Ingeritance
```py
class Vehicle:
    COST = 10_000.00
    TYPE = 'Generic'
    serial_no = 0
    def __init__(self):
        self.a0 = self.COST
        self.a1 = self.__class__.serial_no
        self.a2 = type(self).serial_no
    
class Sedan(Vehicle):
    COST = 30_000.00
    def __init__(self):
        super().__init__()
```
## Avoid multiple Inheritance
```py
# A0 <- C1(A0) <- E3(D2, C1)
#    <- B1(A0) <- D2(B1) <- E3(D2, C1)
el = E3()
el.m1(...) # whrer is m1?
```
Though, there is a rule for this.

# Class Method vs Static Method
* A class method passes the class object as the first implicit argument (similar to instance method). 
* A static method does nothave any implicitly passed argument. Its main purpose is for better organizing the code.
```py
class Temp(object):
    variable = 1.0
    def __init__(self):
        pass
    @classmethod
    def f1(cls, new_var:float):
        print(cls.__name__)
        cls.variable = new_var
    @staticmethod
    def f2(a):
        print(a)
```
# Abstract Base Class and Abstract Method
* An abstract base class (ABC) and with its abstract methods (@abstractmethod) are the “blueprint” of concrete classes that inherit from the abstract base class
* A descendant class of an abstract base class cannot be instantiated until all the abstract methods of the abstract base class have been overridden by concrete methods.
* They are very useful in specifying the application programming interfaces (APIs)
```py
from abc import ABC, abstractmethod
class Temp(ABC):
    def __init__(self):
        print('__init__() in Temp')
    def f1(self):
        print('f1 in Temp')
    @abstractmethod
    def f2(self):
        print('f2 in Temp')

class Temp1(Temp):
    def __init__(self):
        print('__init__() in Temp1')
        super().__init__()
    def f2(self):
        super().f2()
        print('f2 in Temp1')from abc import ABC, abstractmethod
class Temp(ABC):
    def __init__(self):
        print('__init__() in Temp')
    def f1(self):
        print('f1 in Temp')
    @abstractmethod
    def f2(self):
        print('f2 in Temp')

class Temp1(Temp):
    def __init__(self):
        print('__init__() in Temp1')
        super().__init__()
    def f2(self):
        super().f2()
        print('f2 in Temp1')

class Temp2(Temp):
    def __init__(self):
        print('__init__() in Temp2')
        super().__init__()

class Temp2(Temp):
    def __init__(self):
        print('__init__() in Temp2')
        super().__init__()

(a := Temp1()).f1()
(b := Temp1()).f2()

# error
# (c := Temp2()).f2()
# TypeError: Can't instantiate abstract class Temp2 with abstract methods f2
```
[https://docs.python.org/3/whatsnew/3.8.html](https://docs.python.org/3/whatsnew/3.8.html)
