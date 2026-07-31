# Session 22 — Inheritance & Polymorphism
## Module 5: Object-Oriented Programming | Professional Python Programming Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Build a Class Hierarchy

---

## Learning Objectives
By the end of this session, you will be able to:
1. Implement single and multi-level inheritance
2. Override methods in child classes
3. Use `super()` to call parent class methods
4. Understand and apply polymorphism
5. Work with multiple inheritance and MRO

---

## 22.1 What is Inheritance?

**Inheritance** allows a new class (child/subclass) to inherit attributes and methods from an existing class (parent/superclass), enabling code reuse and extension.

```
        Animal (Parent)
       /       \
    Dog         Cat (Children)
   /   \
Puppy  GuideDog (Grandchildren — multi-level)
```

### Why Inheritance?

| Benefit | Detail |
|---------|--------|
| **Code reuse** | Don't rewrite common functionality |
| **Extensibility** | Add features without modifying parent |
| **Hierarchy** | Model real-world relationships |
| **Maintainability** | Fix/update parent → all children updated |

---

## 22.2 Single Inheritance

### Syntax

```python
class Parent:
    # Parent class code
    pass

class Child(Parent):
    # Child inherits from Parent
    pass
```

### Example

```python
class Animal:
    def __init__(self, name, species):
        self.name = name
        self.species = species
    
    def speak(self):
        return f"{self.name} makes a sound"
    
    def info(self):
        return f"{self.name} is a {self.species}"

class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name, "Dog")   # Call parent constructor
        self.breed = breed
    
    def speak(self):                    # Override parent method
        return f"{self.name} says Woof!"
    
    def fetch(self):                    # New method — only for dogs
        return f"{self.name} fetches the ball!"

class Cat(Animal):
    def __init__(self, name, indoor=True):
        super().__init__(name, "Cat")
        self.indoor = indoor
    
    def speak(self):                    # Override
        return f"{self.name} says Meow!"
    
    def purr(self):
        return f"{self.name} is purring..."

# Usage
dog = Dog("Rex", "Labrador")
cat = Cat("Whiskers")

print(dog.speak())    # Rex says Woof! (overridden)
print(dog.info())     # Rex is a Dog (inherited from Animal)
print(dog.fetch())    # Rex fetches the ball! (Dog only)

print(cat.speak())    # Whiskers says Meow!
print(cat.info())     # Whiskers is a Cat (inherited)
print(cat.purr())     # Whiskers is purring...
```

---

## 22.3 The `super()` Function

### What is `super()`?

`super()` returns a proxy object that lets you call methods from the parent class.

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def display(self):
        print(f"Name: {self.name}, Age: {self.age}")

class Student(Person):
    def __init__(self, name, age, student_id, grade):
        super().__init__(name, age)    # Call Person's __init__
        self.student_id = student_id
        self.grade = grade
    
    def display(self):
        super().display()              # Call Person's display
        print(f"Student ID: {self.student_id}, Grade: {self.grade}")

s = Student("Alice", 20, "STU001", "A")
s.display()
# Name: Alice, Age: 20
# Student ID: STU001, Grade: A
```

### Why `super()` Instead of `Parent.__init__(self)`?

```python
# Works but less flexible
class Child(Parent):
    def __init__(self):
        Parent.__init__(self)    # Hard-coded parent name

# Better — uses MRO, works with multiple inheritance
class Child(Parent):
    def __init__(self):
        super().__init__()       # Automatically finds parent
```

---

## 22.4 Method Overriding

When a child class defines a method with the **same name** as the parent, the child's version is used.

```python
class Shape:
    def area(self):
        return 0
    
    def describe(self):
        return f"{self.__class__.__name__} with area {self.area():.2f}"

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height
    
    def area(self):            # Override
        return self.width * self.height

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius
    
    def area(self):            # Override
        return 3.14159 * self.radius ** 2

class Triangle(Shape):
    def __init__(self, base, height):
        self.base = base
        self.height = height
    
    def area(self):            # Override
        return 0.5 * self.base * self.height

# Each shape calculates area differently
shapes = [Rectangle(10, 5), Circle(7), Triangle(8, 6)]
for shape in shapes:
    print(shape.describe())
# Rectangle with area 50.00
# Circle with area 153.94
# Triangle with area 24.00
```

---

## 22.5 Multi-Level Inheritance

A chain of inheritance: Grandparent → Parent → Child.

```python
class Vehicle:
    def __init__(self, brand, year):
        self.brand = brand
        self.year = year
    
    def start(self):
        return f"{self.brand} engine started"

class Car(Vehicle):
    def __init__(self, brand, year, doors):
        super().__init__(brand, year)
        self.doors = doors
    
    def honk(self):
        return "Beep beep!"

class ElectricCar(Car):
    def __init__(self, brand, year, doors, battery_kwh):
        super().__init__(brand, year, doors)
        self.battery_kwh = battery_kwh
    
    def start(self):
        return f"{self.brand} silently starts (Electric)"
    
    def charge(self):
        return f"Charging {self.battery_kwh} kWh battery..."

tesla = ElectricCar("Tesla", 2024, 4, 100)
print(tesla.start())     # Tesla silently starts (Electric) — overridden
print(tesla.honk())      # Beep beep! — inherited from Car
print(tesla.charge())    # Charging 100 kWh battery... — ElectricCar only
print(tesla.year)        # 2024 — inherited from Vehicle
```

---

## 22.6 Multiple Inheritance

A class inherits from **more than one** parent class.

```python
class Flyable:
    def fly(self):
        return f"{self.__class__.__name__} is flying!"

class Swimmable:
    def swim(self):
        return f"{self.__class__.__name__} is swimming!"

class Duck(Animal, Flyable, Swimmable):
    def __init__(self, name):
        Animal.__init__(self, name, "Duck")
    
    def speak(self):
        return f"{self.name} says Quack!"

donald = Duck("Donald")
print(donald.speak())    # Donald says Quack!
print(donald.fly())      # Duck is flying!
print(donald.swim())     # Duck is swimming!
print(donald.info())     # Donald is a Duck (from Animal)
```

### Method Resolution Order (MRO)

When multiple parents have the same method, Python uses **MRO** (C3 linearization) to decide which to call.

```python
class A:
    def greet(self):
        return "Hello from A"

class B(A):
    def greet(self):
        return "Hello from B"

class C(A):
    def greet(self):
        return "Hello from C"

class D(B, C):
    pass

d = D()
print(d.greet())          # Hello from B — B comes first in MRO

# View the MRO
print(D.__mro__)
# (<class 'D'>, <class 'B'>, <class 'C'>, <class 'A'>, <class 'object'>)
print(D.mro())            # Same as above
```

### The Diamond Problem

```
      A
     / \
    B   C
     \ /
      D
```

Python's MRO resolves this — each class is called only once, in a predictable order.

---

## 22.7 isinstance() and issubclass()

```python
dog = Dog("Rex", "Labrador")

# isinstance — check if object is an instance of a class
print(isinstance(dog, Dog))       # True
print(isinstance(dog, Animal))    # True (Dog inherits from Animal)
print(isinstance(dog, Cat))       # False

# issubclass — check if class is a subclass
print(issubclass(Dog, Animal))    # True
print(issubclass(Cat, Animal))    # True
print(issubclass(Dog, Cat))       # False
print(issubclass(Animal, object)) # True (everything inherits from object)
```

---

## 22.8 Polymorphism

### What is Polymorphism?

**Poly** (many) + **morph** (forms) — same interface, different implementations. Objects of different classes respond to the same method call in their own way.

### Polymorphism Through Method Overriding

```python
class Shape:
    def area(self):
        raise NotImplementedError("Subclasses must implement area()")

class Rectangle(Shape):
    def __init__(self, w, h):
        self.w = w
        self.h = h
    def area(self):
        return self.w * self.h

class Circle(Shape):
    def __init__(self, r):
        self.r = r
    def area(self):
        return 3.14159 * self.r ** 2

# Polymorphism — same function works with different types
def print_area(shape):
    print(f"{shape.__class__.__name__}: {shape.area():.2f}")

print_area(Rectangle(10, 5))   # Rectangle: 50.00
print_area(Circle(7))          # Circle: 153.94
```

### Duck Typing

Python doesn't require objects to inherit from the same class — if it "walks like a duck and quacks like a duck," it's treated as a duck.

```python
class Printer:
    def output(self, text):
        print(f"Printer: {text}")

class Screen:
    def output(self, text):
        print(f"Screen: {text}")

class Logger:
    def output(self, text):
        print(f"Log: {text}")

# Works with any object that has an output() method
def display(device, message):
    device.output(message)

display(Printer(), "Hello")   # Printer: Hello
display(Screen(), "Hello")    # Screen: Hello
display(Logger(), "Hello")    # Log: Hello
```

### Operator Overloading (Polymorphism with Operators)

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)
    
    def __mul__(self, scalar):
        return Vector(self.x * scalar, self.y * scalar)
    
    def __abs__(self):
        return (self.x**2 + self.y**2) ** 0.5
    
    def __str__(self):
        return f"Vector({self.x}, {self.y})"

v1 = Vector(3, 4)
v2 = Vector(1, 2)
v3 = v1 + v2          # __add__
v4 = v1 * 3           # __mul__
print(v3)              # Vector(4, 6)
print(v4)              # Vector(9, 12)
print(abs(v1))         # 5.0 (3-4-5 triangle)
```

---

## 🔧 Hands-On Activity: Class Hierarchy

**Duration:** 25 minutes

Create a file `session22_inheritance.py`:

```python
# Session 22 — Inheritance & Polymorphism

# Part 1: Employee Hierarchy
class Employee:
    def __init__(self, name, emp_id, base_salary):
        self.name = name
        self.emp_id = emp_id
        self.base_salary = base_salary
    
    def calculate_salary(self):
        return self.base_salary
    
    def __str__(self):
        return f"{self.emp_id} | {self.name} | ₹{self.calculate_salary():,.2f}"

class Manager(Employee):
    def __init__(self, name, emp_id, base_salary, bonus_pct=0.20):
        super().__init__(name, emp_id, base_salary)
        self.bonus_pct = bonus_pct
    
    def calculate_salary(self):
        return self.base_salary * (1 + self.bonus_pct)

class Developer(Employee):
    def __init__(self, name, emp_id, base_salary, tech_allowance=5000):
        super().__init__(name, emp_id, base_salary)
        self.tech_allowance = tech_allowance
    
    def calculate_salary(self):
        return self.base_salary + self.tech_allowance

class Intern(Employee):
    def __init__(self, name, emp_id, stipend=15000):
        super().__init__(name, emp_id, stipend)
    
    def calculate_salary(self):
        return self.base_salary  # No extras

# Polymorphism
print("=== Employee Payroll ===")
employees = [
    Manager("Alice", "MGR001", 100000),
    Developer("Bob", "DEV001", 80000),
    Developer("Charlie", "DEV002", 85000, 8000),
    Intern("Diana", "INT001"),
]

total = 0
print(f"{'ID':<8} {'Name':<12} {'Type':<12} {'Salary':>12}")
print("-" * 48)
for emp in employees:
    emp_type = type(emp).__name__
    salary = emp.calculate_salary()
    total += salary
    print(f"{emp.emp_id:<8} {emp.name:<12} {emp_type:<12} ₹{salary:>10,.2f}")
print("-" * 48)
print(f"{'Total Payroll':<33} ₹{total:>10,.2f}")

# Type checking
print(f"\nAlice is Employee? {isinstance(employees[0], Employee)}")
print(f"Alice is Manager? {isinstance(employees[0], Manager)}")
print(f"Manager is subclass of Employee? {issubclass(Manager, Employee)}")

# Part 2: Shape Polymorphism
print("\n=== Shapes ===")

class Shape:
    def area(self):
        return 0
    def perimeter(self):
        return 0
    def __str__(self):
        return f"{self.__class__.__name__}: Area={self.area():.2f}, Perimeter={self.perimeter():.2f}"

class Rectangle(Shape):
    def __init__(self, w, h):
        self.w, self.h = w, h
    def area(self):
        return self.w * self.h
    def perimeter(self):
        return 2 * (self.w + self.h)

class Circle(Shape):
    def __init__(self, r):
        self.r = r
    def area(self):
        return 3.14159 * self.r ** 2
    def perimeter(self):
        return 2 * 3.14159 * self.r

shapes = [Rectangle(10, 5), Circle(7), Rectangle(3, 8), Circle(4)]
for s in shapes:
    print(f"  {s}")

print(f"\nTotal area: {sum(s.area() for s in shapes):.2f}")
print("\nDone!")
```

---

## Session 22 — Key Takeaways

1. **Inheritance** lets child classes reuse parent code — `class Child(Parent):`
2. **`super()`** calls parent methods — essential in `__init__` and overridden methods
3. **Method overriding** — child replaces parent's method with its own implementation
4. **Polymorphism** — same method name, different behavior depending on the object type
5. **Duck typing** — Python cares about behavior (methods), not class hierarchy
6. **MRO** resolves method lookup order in multiple inheritance

---

## Preparation for Session 23
- Practice: Add a `SeniorManager` that inherits from `Manager` with extra perks
- Think about: How do you prevent direct access to internal data?
- Review: What is encapsulation? What is abstraction?

---

*Session 22 of 30 | Module 5: Object-Oriented Programming*
*Professional Python Programming Certification — UpSkill Global Education Technologies Inc., Canada*
