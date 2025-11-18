# OOP Concepts & SOLID Principles 

# Table of Contents
1. Object-Oriented Programming (OOP) Concepts
   - Encapsulation
   - Inheritance
   - Polymorphism
   - Abstraction
2. SOLID Principles
   - Single Responsibility Principle (SRP)
   - Open/Closed Principle (OCP)
   - Liskov Substitution Principle (LSP)
   - Interface Segregation Principle (ISP)
   - Dependency Inversion Principle (DIP)
3. References

---

# Object-Oriented Programming (OOP) Concepts

## Encapsulation

### Description
Encapsulation refers to the practice of bundling data and methods that operate on that data within a single unit (class). It restricts direct access to internal variables, ensuring that It is a means of protecting object integrity and preventing unintended side effects.

### Example
```python
class BankAccount:
    def __init__(self, owner, balance=0):
        self.owner = owner
        self.__balance = balance  # private attribute

    def deposit(self, amount):
        self.__balance += amount

    def withdraw(self, amount):
        if amount <= self.__balance:
            self.__balance -= amount
        else:
            print("Insufficient balance")

    def get_balance(self):
        return self.__balance
```

---

## Inheritance

### Description
Inheritance allows a new class (child) to reuse attributes and methods of an existing class (parent). This promotes code reusability and enables hierarchical relationships where subclasses extend or override behaviors.

### Example
```python
class Vehicle:
    def start(self):
        return "Vehicle started"

class Car(Vehicle):
    def start(self):
        return "Car engine started"

car = Car()
print(car.start())
```

---

## Polymorphism

### Description
Polymorphism means “many forms,” allowing different classes to define methods with the same name but different behavior.  
Polymorphism can be defined as a way to write flexible, reusable code that operates on objects sharing a common interface.

### Example
```python
class Dog:
    def speak(self):
        return "Bark"

class Cat:
    def speak(self):
        return "Meow"

def animal_sound(animal):
    print(animal.speak())

animal_sound(Dog())
animal_sound(Cat())
```

---

## Abstraction

### Description
Abstraction hides complex implementation details while exposing only the essential behavior. Python supports abstraction using abstract base classes (`ABC`).  
Abstraction reduces complexity by focusing on *what* an object does rather than *how* it does it.

### Example
```python
from abc import ABC, abstractmethod

class Payment(ABC):
    @abstractmethod
    def pay(self, amount):
        pass

class CreditCard(Payment):
    def pay(self, amount):
        print(f"Paid ₹{amount} using Credit Card")

payment = CreditCard()
payment.pay(500)
```

---

# SOLID Principles

## Single Responsibility Principle (SRP)

### Description
SRP states that a class should have only *one reason to change*. Combining multiple responsibilities makes a class fragile and harder to maintain. Splitting responsibilities into separate components leads to better modularity.

### Example
Bad:
```python
class Report:
    def generate(self):
        return "Report content"

    def save_to_file(self, data):
        with open("report.txt", "w") as f:
            f.write(data)
```

Good:
```python
class Report:
    def generate(self):
        return "Report content"

class ReportSaver:
    def save(self, data):
        with open("report.txt", "w") as f:
            f.write(data)
```

---

## Open/Closed Principle (OCP)

### Description
OCP states that software entities should be *open for extension but closed for modification*.  
New behaviors should be added through extensions (subclasses, strategies) instead of altering existing code.

### Example
```python
class Discount:
    def apply(self, price):
        return price

class StudentDiscount(Discount):
    def apply(self, price):
        return price * 0.9

class SeniorCitizenDiscount(Discount):
    def apply(self, price):
        return price * 0.85
```

---

## Liskov Substitution Principle (LSP)

### Description
LSP requires that subclasses behave in accordance with the expectations set by the base class.  
It emphasizes substitutability: replacing a parent class with a child must not break functionality. Violations occur when subclasses remove functionality or introduce unexpected behavior.

### Example
Bad:
```python
class Bird:
    def fly(self):
        return "Flying"

class Ostrich(Bird):
    def fly(self):
        raise Exception("Ostriches cannot fly")  # violates LSP
```

Good:
```python
class Bird:
    pass

class FlyingBird(Bird):
    def fly(self):
        return "Flying"

class NonFlyingBird(Bird):
    pass
```

---

## Interface Segregation Principle (ISP)

### Description
ISP states that no client should be forced to depend on methods it does not use.  
It suggests dividing large interfaces into smaller, specific ones to avoid unnecessary dependencies.

### Example
```python
class Workable:
    def work(self):
        pass

class Eatable:
    def eat(self):
        pass

class Robot(Workable):
    def work(self):
        print("Robot working")

class Human(Workable, Eatable):
    def work(self):
        print("Human working")

    def eat(self):
        print("Human eating")
```

---

## Dependency Inversion Principle (DIP)

### Description
DIP defines two key rules:  
1. High-level modules must not depend on low-level modules.  
2. Both should depend on abstractions.  

This reduces coupling and increases flexibility.  
It strongly emphasizes the use of interfaces/abstractions to prevent direct dependency on concrete implementations.

### Example
```python
class Database:
    def connect(self):
        pass

class MySQLDatabase(Database):
    def connect(self):
        print("Connected to MySQL")

class Application:
    def __init__(self, db: Database):
        self.db = db

    def start(self):
        self.db.connect()

app = Application(MySQLDatabase())
app.start()
```

---

# References


- Python Documentation — Classes  
  https://docs.python.org/3/tutorial/classes.html  
- RealPython — OOP in Python  
  https://realpython.com/python3-object-oriented-programming/  
- FreeCodeCamp — SOLID Principles  
  https://www.freecodecamp.org/news/solid-principles-explained/  
- GeeksforGeeks — OOP Concepts  
  https://www.geeksforgeeks.org/object-oriented-programming-oops-concept-in-java/
