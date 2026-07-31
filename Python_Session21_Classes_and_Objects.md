# Session 21 — Classes & Objects
## Module 5: Object-Oriented Programming | Professional Python Programming Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Create Classes for Real-World Entities

---

## Learning Objectives
By the end of this session, you will be able to:
1. Understand the principles of Object-Oriented Programming (OOP)
2. Define classes with attributes and methods
3. Create and use objects (instances)
4. Use the `__init__` constructor and `self` keyword
5. Implement special (dunder) methods for string representation

---

## 21.1 What is Object-Oriented Programming?

**OOP** is a programming paradigm that organizes code around **objects** — bundling data (attributes) and behavior (methods) together.

### Procedural vs OOP

| Procedural | Object-Oriented |
|-----------|----------------|
| Functions operate on data | Objects contain both data and functions |
| Data and functions are separate | Data and behavior are bundled together |
| Harder to manage as code grows | Easier to organize large programs |
| `calculate_area(length, width)` | `rectangle.area()` |

### Four Pillars of OOP

| Pillar | Description | Session |
|--------|-------------|---------|
| **Encapsulation** | Bundle data + methods; hide internals | Session 23 |
| **Abstraction** | Show only essential features; hide complexity | Session 23 |
| **Inheritance** | Create new classes from existing ones | Session 22 |
| **Polymorphism** | Same interface, different implementations | Session 22 |

### Real-World Analogy

| Concept | Real World | Python |
|---------|-----------|--------|
| **Class** | Blueprint of a car | `class Car:` |
| **Object** | An actual car (Toyota, Honda) | `my_car = Car("Toyota")` |
| **Attribute** | Color, speed, fuel | `self.color = "Red"` |
| **Method** | Start, stop, accelerate | `def start(self):` |

---

## 21.2 Defining a Class

### Syntax

```python
class ClassName:
    """Docstring describing the class."""
    
    # Class attribute (shared by all instances)
    class_attribute = value
    
    # Constructor (initializer)
    def __init__(self, param1, param2):
        # Instance attributes (unique to each object)
        self.param1 = param1
        self.param2 = param2
    
    # Instance method
    def method_name(self):
        # Access attributes with self
        return self.param1
```

### First Class Example

```python
class Student:
    """Represents a student."""
    
    # Class attribute — shared by all students
    school = "Python Academy"
    
    # Constructor
    def __init__(self, name, age, grade):
        # Instance attributes — unique to each student
        self.name = name
        self.age = age
        self.grade = grade
        self.courses = []    # Default empty list
    
    # Instance methods
    def enroll(self, course):
        """Enroll student in a course."""
        self.courses.append(course)
        print(f"{self.name} enrolled in {course}")
    
    def display(self):
        """Display student information."""
        print(f"Name: {self.name}")
        print(f"Age: {self.age}")
        print(f"Grade: {self.grade}")
        print(f"School: {self.school}")
        print(f"Courses: {', '.join(self.courses) if self.courses else 'None'}")
```

### Creating Objects (Instances)

```python
# Create objects
student1 = Student("Alice", 20, "A")
student2 = Student("Bob", 22, "B")

# Access attributes
print(student1.name)       # Alice
print(student2.age)        # 22
print(student1.school)     # Python Academy (class attribute)

# Call methods
student1.enroll("Python")
student1.enroll("Data Science")
student1.display()

# Each object is independent
student2.enroll("Java")
student2.display()
```

---

## 21.3 The `self` Parameter

### What is `self`?

`self` is a reference to the **current instance** of the class. It allows each object to access its own data.

```python
class Car:
    def __init__(self, brand, color):
        self.brand = brand     # self.brand belongs to THIS specific car
        self.color = color
    
    def describe(self):
        # self refers to the object calling this method
        return f"{self.color} {self.brand}"

car1 = Car("Toyota", "Red")
car2 = Car("Honda", "Blue")

print(car1.describe())   # Red Toyota — self = car1
print(car2.describe())   # Blue Honda — self = car2
```

### How `self` Works Internally

```python
# When you call:
car1.describe()

# Python internally translates it to:
Car.describe(car1)    # self = car1
```

### Key Rules

| Rule | Detail |
|------|--------|
| `self` is the **first parameter** of every instance method | Always required |
| `self` is **not a keyword** | Convention, could be anything (but always use `self`) |
| `self` is passed **automatically** | Don't pass it when calling `obj.method()` |
| Use `self.attribute` to access instance data | Without `self`, it's a local variable |

---

## 21.4 The `__init__` Constructor

### Purpose

`__init__` is called **automatically** when a new object is created. It initializes the object's attributes.

```python
class BankAccount:
    def __init__(self, owner, balance=0):
        """Initialize account with owner and optional balance."""
        self.owner = owner
        self.balance = balance
        self.transactions = []
        self.is_active = True
        print(f"Account created for {owner}")

# __init__ is called automatically
acc = BankAccount("Alice", 5000)
# Output: Account created for Alice
```

### Constructor with Validation

```python
class Product:
    def __init__(self, name, price, quantity=0):
        if not name:
            raise ValueError("Product name is required")
        if price < 0:
            raise ValueError("Price cannot be negative")
        if quantity < 0:
            raise ValueError("Quantity cannot be negative")
        
        self.name = name
        self.price = price
        self.quantity = quantity
    
    def total_value(self):
        return self.price * self.quantity

try:
    p = Product("Laptop", -5000)
except ValueError as e:
    print(f"Error: {e}")  # Error: Price cannot be negative
```

---

## 21.5 Instance vs Class Attributes

### Instance Attributes

- Defined inside `__init__` with `self.attr = value`
- **Unique** to each object
- Changed on one object → others unaffected

### Class Attributes

- Defined directly in the class body
- **Shared** by all instances
- Changed on the class → affects all instances that haven't overridden it

```python
class Employee:
    # Class attributes
    company = "TechCorp"
    employee_count = 0
    
    def __init__(self, name, salary):
        # Instance attributes
        self.name = name
        self.salary = salary
        Employee.employee_count += 1   # Modify class attribute

emp1 = Employee("Alice", 75000)
emp2 = Employee("Bob", 85000)

# Class attribute — same for all
print(emp1.company)          # TechCorp
print(emp2.company)          # TechCorp
print(Employee.company)      # TechCorp

# Instance attribute — different per object
print(emp1.name)             # Alice
print(emp2.name)             # Bob

# Class attribute tracking
print(Employee.employee_count)  # 2
```

### Modifying Class vs Instance Attributes

```python
# Change class attribute via CLASS — affects all
Employee.company = "NewCorp"
print(emp1.company)   # NewCorp
print(emp2.company)   # NewCorp

# Change via INSTANCE — creates instance attribute (shadows class attr)
emp1.company = "StartupCo"
print(emp1.company)   # StartupCo (instance)
print(emp2.company)   # NewCorp (still class attribute)
```

---

## 21.6 Instance Methods

### Types of Methods

```python
class MyClass:
    class_var = "shared"
    
    # Instance method — operates on instance (self)
    def instance_method(self):
        return f"Instance: {self}"
    
    # Class method — operates on class (cls)
    @classmethod
    def class_method(cls):
        return f"Class: {cls.class_var}"
    
    # Static method — no access to instance or class
    @staticmethod
    def static_method():
        return "Static: utility function"
```

### Comparison

| Type | First Param | Accesses | Decorator | Use For |
|------|------------|----------|-----------|---------|
| Instance | `self` | Instance + class attrs | None | Most methods |
| Class | `cls` | Class attrs only | `@classmethod` | Alternative constructors, class-level ops |
| Static | None | Neither | `@staticmethod` | Utility functions related to the class |

### Class Method — Alternative Constructors

```python
class Date:
    def __init__(self, year, month, day):
        self.year = year
        self.month = month
        self.day = day
    
    @classmethod
    def from_string(cls, date_str):
        """Create Date from 'YYYY-MM-DD' string."""
        year, month, day = map(int, date_str.split("-"))
        return cls(year, month, day)  # cls = Date
    
    @classmethod
    def today(cls):
        """Create Date for today."""
        from datetime import date
        t = date.today()
        return cls(t.year, t.month, t.day)
    
    def __str__(self):
        return f"{self.year}-{self.month:02d}-{self.day:02d}"

# Different ways to create a Date
d1 = Date(2024, 1, 15)
d2 = Date.from_string("2024-03-20")
d3 = Date.today()
print(d1, d2, d3)
```

### Static Method — Utility Functions

```python
class MathUtils:
    @staticmethod
    def is_prime(n):
        if n < 2:
            return False
        for i in range(2, int(n**0.5) + 1):
            if n % i == 0:
                return False
        return True
    
    @staticmethod
    def factorial(n):
        if n <= 1:
            return 1
        result = 1
        for i in range(2, n + 1):
            result *= i
        return result

print(MathUtils.is_prime(17))    # True
print(MathUtils.factorial(5))    # 120
```

---

## 21.7 Special (Dunder) Methods

### What are Dunder Methods?

**Dunder** = Double UNDERscore. Special methods that Python calls automatically in certain situations.

### String Representation

```python
class Product:
    def __init__(self, name, price):
        self.name = name
        self.price = price
    
    def __str__(self):
        """Called by print() and str() — user-friendly."""
        return f"{self.name} — ₹{self.price:,.2f}"
    
    def __repr__(self):
        """Called by repr() and in debugger — developer-friendly."""
        return f"Product('{self.name}', {self.price})"

p = Product("Laptop", 65000)
print(p)        # Laptop — ₹65,000.00  (__str__)
print(repr(p))  # Product('Laptop', 65000)  (__repr__)
print([p])      # [Product('Laptop', 65000)]  (__repr__ in lists)
```

### Comparison Methods

```python
class Student:
    def __init__(self, name, gpa):
        self.name = name
        self.gpa = gpa
    
    def __eq__(self, other):
        return self.gpa == other.gpa
    
    def __lt__(self, other):
        return self.gpa < other.gpa
    
    def __le__(self, other):
        return self.gpa <= other.gpa
    
    def __gt__(self, other):
        return self.gpa > other.gpa

s1 = Student("Alice", 3.8)
s2 = Student("Bob", 3.5)
print(s1 > s2)   # True
print(s1 == s2)   # False

# Now sorting works automatically!
students = [Student("Alice", 3.8), Student("Bob", 3.5), Student("Charlie", 3.9)]
students.sort()
print([s.name for s in students])  # ['Bob', 'Alice', 'Charlie']
```

### Other Useful Dunder Methods

| Method | Called By | Example |
|--------|----------|---------|
| `__init__(self)` | Object creation | `obj = Class()` |
| `__str__(self)` | `print()`, `str()` | `print(obj)` |
| `__repr__(self)` | `repr()`, debugger | `repr(obj)` |
| `__len__(self)` | `len()` | `len(obj)` |
| `__eq__(self, other)` | `==` | `obj1 == obj2` |
| `__lt__(self, other)` | `<` | `obj1 < obj2` |
| `__add__(self, other)` | `+` | `obj1 + obj2` |
| `__contains__(self, item)` | `in` | `item in obj` |
| `__getitem__(self, key)` | `[]` | `obj[key]` |
| `__iter__(self)` | `for x in obj` | Iteration |
| `__del__(self)` | Object deletion | `del obj` |

---

## 21.8 Properties — Controlled Attribute Access

```python
class Circle:
    def __init__(self, radius):
        self._radius = radius   # Convention: _ = "private"
    
    @property
    def radius(self):
        """Getter — called when accessing circle.radius"""
        return self._radius
    
    @radius.setter
    def radius(self, value):
        """Setter — called when setting circle.radius = value"""
        if value < 0:
            raise ValueError("Radius cannot be negative")
        self._radius = value
    
    @property
    def area(self):
        """Read-only computed property."""
        return 3.14159 * self._radius ** 2
    
    @property
    def circumference(self):
        return 2 * 3.14159 * self._radius

c = Circle(5)
print(c.radius)         # 5 (getter)
print(c.area)           # 78.54 (computed property — no parentheses!)
c.radius = 10           # Setter with validation
# c.radius = -5         # ValueError: Radius cannot be negative
# c.area = 100          # AttributeError: can't set (read-only property)
```

---

## 🔧 Hands-On Activity: Create Classes

**Duration:** 25 minutes

Create a file `session21_classes.py`:

```python
# Session 21 — Classes & Objects

# Part 1: BankAccount Class
class BankAccount:
    bank_name = "Python National Bank"
    total_accounts = 0
    
    def __init__(self, owner, balance=0):
        BankAccount.total_accounts += 1
        self.account_no = f"ACC{BankAccount.total_accounts:04d}"
        self.owner = owner
        self._balance = balance
        self.transactions = []
    
    @property
    def balance(self):
        return self._balance
    
    def deposit(self, amount):
        if amount <= 0:
            raise ValueError("Deposit must be positive")
        self._balance += amount
        self.transactions.append(("DEPOSIT", amount, self._balance))
        return self._balance
    
    def withdraw(self, amount):
        if amount <= 0:
            raise ValueError("Withdrawal must be positive")
        if amount > self._balance:
            raise ValueError("Insufficient funds")
        self._balance -= amount
        self.transactions.append(("WITHDRAW", amount, self._balance))
        return self._balance
    
    def statement(self):
        print(f"\n--- Statement: {self.account_no} ({self.owner}) ---")
        print(f"  {'Type':<12} {'Amount':>10} {'Balance':>10}")
        print(f"  {'-'*35}")
        for t_type, amount, bal in self.transactions:
            print(f"  {t_type:<12} ₹{amount:>9,.2f} ₹{bal:>9,.2f}")
        print(f"  {'-'*35}")
        print(f"  {'Current Balance':<12} {'':>10} ₹{self._balance:>9,.2f}")
    
    def __str__(self):
        return f"{self.account_no} | {self.owner} | ₹{self._balance:,.2f}"
    
    def __repr__(self):
        return f"BankAccount('{self.owner}', {self._balance})"

# Test
print("=== Bank Account Demo ===")
acc1 = BankAccount("Alice", 10000)
acc2 = BankAccount("Bob", 5000)

acc1.deposit(5000)
acc1.withdraw(3000)
acc1.deposit(2000)

acc2.deposit(10000)
acc2.withdraw(2500)

print(f"\n{acc1}")
print(f"{acc2}")
print(f"\nTotal accounts: {BankAccount.total_accounts}")

acc1.statement()
acc2.statement()

# Part 2: Product with computed properties
class Product:
    tax_rate = 0.18
    
    def __init__(self, name, price, quantity):
        self.name = name
        self.price = price
        self.quantity = quantity
    
    @property
    def total_value(self):
        return self.price * self.quantity
    
    @property
    def price_with_tax(self):
        return self.price * (1 + self.tax_rate)
    
    def __str__(self):
        return f"{self.name} | ₹{self.price:,.2f} | Qty: {self.quantity}"
    
    def __lt__(self, other):
        return self.price < other.price

print("\n=== Product Demo ===")
products = [
    Product("Laptop", 65000, 5),
    Product("Mouse", 500, 50),
    Product("Keyboard", 1200, 30),
]

for p in sorted(products):
    print(f"  {p} | Value: ₹{p.total_value:,.2f} | With Tax: ₹{p.price_with_tax:,.2f}")

print("\nDone!")
```

---

## Session 21 — Key Takeaways

1. **Class** = blueprint; **Object** = instance created from that blueprint
2. **`__init__`** initializes attributes automatically when creating an object
3. **`self`** refers to the current instance — required in every instance method
4. **Class attributes** are shared; **instance attributes** are unique per object
5. **Dunder methods** (`__str__`, `__repr__`, `__eq__`) customize object behavior
6. **`@property`** creates controlled attribute access with getters and setters

---

## Preparation for Session 22
- Practice: Add a `transfer()` method to BankAccount that moves money between accounts
- Think about: What if you want a SavingsAccount that is similar to BankAccount but has interest?
- Review: What is inheritance? What is method overriding?

---

*Session 21 of 30 | Module 5: Object-Oriented Programming*
*Professional Python Programming Certification — UpSkill Global Education Technologies Inc., Canada*
