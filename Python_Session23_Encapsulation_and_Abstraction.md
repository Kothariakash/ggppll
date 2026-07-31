# Session 23 — Encapsulation & Abstraction
## Module 5: Object-Oriented Programming | Professional Python Programming Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Design Protected & Abstract Classes

---

## Learning Objectives
By the end of this session, you will be able to:
1. Implement encapsulation using access modifiers (public, protected, private)
2. Use properties for controlled attribute access
3. Create abstract base classes (ABCs) with `abc` module
4. Understand the difference between encapsulation and abstraction
5. Apply information hiding and interface design in real projects

---

## 23.1 What is Encapsulation?

**Encapsulation** = bundling data (attributes) and the methods that operate on that data into a single unit (class), and **restricting direct access** to some of the object's internals.

### Why Encapsulation?

| Benefit | Detail |
|---------|--------|
| **Data protection** | Prevent accidental modification of internal state |
| **Controlled access** | Validate data before setting |
| **Flexibility** | Change internal implementation without affecting users |
| **Debugging** | Easier to track where data changes |

### Real-World Analogy

| Concept | Example |
|---------|---------|
| **Public** | A car's steering wheel — anyone can use it |
| **Protected** | Engine warning light — mechanic interprets it |
| **Private** | Engine's internal wiring — only manufacturer touches it |

---

## 23.2 Access Modifiers in Python

Python uses **naming conventions** (not keywords) to indicate access levels.

| Convention | Access | Syntax | Usage |
|-----------|--------|--------|-------|
| **Public** | Accessible everywhere | `self.name` | Default — external API |
| **Protected** | Accessible within class and subclasses | `self._name` | Internal, but subclasses may use |
| **Private** | Accessible within class only | `self.__name` | Truly internal, name-mangled |

### Example

```python
class Employee:
    def __init__(self, name, salary, ssn):
        self.name = name           # Public
        self._salary = salary      # Protected (convention)
        self.__ssn = ssn           # Private (name-mangled)
    
    def get_info(self):
        return f"{self.name} — Salary: ₹{self._salary:,.2f}"
    
    def get_masked_ssn(self):
        return f"XXX-XX-{self.__ssn[-4:]}"

emp = Employee("Alice", 85000, "123-45-6789")

# Public — accessible
print(emp.name)              # Alice

# Protected — accessible but shouldn't be used externally
print(emp._salary)           # 85000 (works, but convention says don't)

# Private — NOT directly accessible
# print(emp.__ssn)           # AttributeError!
print(emp.get_masked_ssn())  # XXX-XX-6789

# Name mangling — Python renames __attr to _ClassName__attr
print(emp._Employee__ssn)    # 123-45-6789 (possible, but DON'T do this)
```

### Name Mangling Details

```python
class MyClass:
    def __init__(self):
        self.__private = "secret"

obj = MyClass()

# Python renames __private to _MyClass__private
print(dir(obj))  # [..., '_MyClass__private', ...]
print(obj._MyClass__private)  # "secret" — accessible but strongly discouraged

# This is NOT true private — it's "don't touch this" by convention
```

> **Python philosophy:** "We're all consenting adults." Python relies on convention, not enforcement.

---

## 23.3 Properties — The Pythonic Way

### Using @property for Encapsulation

```python
class BankAccount:
    def __init__(self, owner, balance=0):
        self._owner = owner
        self._balance = balance
        self._is_frozen = False
    
    @property
    def balance(self):
        """Getter — read the balance."""
        return self._balance
    
    @balance.setter
    def balance(self, value):
        """Setter — control how balance is set."""
        raise AttributeError("Cannot set balance directly. Use deposit/withdraw.")
    
    @property
    def owner(self):
        return self._owner
    
    @owner.setter
    def owner(self, value):
        if not value or not isinstance(value, str):
            raise ValueError("Owner name must be a non-empty string")
        self._owner = value.strip().title()
    
    @property
    def is_frozen(self):
        return self._is_frozen
    
    def deposit(self, amount):
        if self._is_frozen:
            raise RuntimeError("Account is frozen")
        if amount <= 0:
            raise ValueError("Deposit must be positive")
        self._balance += amount
        return self._balance
    
    def withdraw(self, amount):
        if self._is_frozen:
            raise RuntimeError("Account is frozen")
        if amount <= 0:
            raise ValueError("Withdrawal must be positive")
        if amount > self._balance:
            raise ValueError("Insufficient funds")
        self._balance -= amount
        return self._balance
    
    def freeze(self):
        self._is_frozen = True
    
    def unfreeze(self):
        self._is_frozen = False

# Usage
acc = BankAccount("Alice", 10000)
print(acc.balance)       # 10000 (getter)
# acc.balance = 99999    # AttributeError — can't set directly!
acc.deposit(5000)        # Must use methods
print(acc.balance)       # 15000
acc.owner = "alice smith"
print(acc.owner)         # Alice Smith (auto-formatted)
```

### Computed Properties

```python
class Rectangle:
    def __init__(self, width, height):
        self._width = width
        self._height = height
    
    @property
    def width(self):
        return self._width
    
    @width.setter
    def width(self, value):
        if value <= 0:
            raise ValueError("Width must be positive")
        self._width = value
    
    @property
    def height(self):
        return self._height
    
    @height.setter
    def height(self, value):
        if value <= 0:
            raise ValueError("Height must be positive")
        self._height = value
    
    @property
    def area(self):
        """Computed property — no setter needed."""
        return self._width * self._height
    
    @property
    def perimeter(self):
        return 2 * (self._width + self._height)
    
    @property
    def is_square(self):
        return self._width == self._height

r = Rectangle(10, 5)
print(r.area)        # 50 (computed, no parentheses)
print(r.perimeter)   # 30
print(r.is_square)   # False
r.width = 5
print(r.is_square)   # True
```

---

## 23.4 What is Abstraction?

**Abstraction** = hiding complex implementation details and showing only the essential interface. Users interact with **what** an object does, not **how** it does it.

### Encapsulation vs Abstraction

| Encapsulation | Abstraction |
|--------------|-------------|
| **Hides data** (attributes) | **Hides implementation** (how methods work) |
| Achieved with access modifiers | Achieved with abstract classes/interfaces |
| "Don't touch my internals" | "You don't need to know how this works" |
| Implementation detail | Design concept |

### Real-World Abstraction

| Interface | Hidden Complexity |
|-----------|-------------------|
| TV Remote buttons | Signal processing, circuit boards |
| `print("Hello")` | System calls, buffer management, encoding |
| `list.sort()` | TimSort algorithm, memory management |
| ATM "Withdraw" button | Network calls, security checks, database updates |

---

## 23.5 Abstract Base Classes (ABC)

### What is an Abstract Class?

An **abstract class** cannot be instantiated directly. It defines a **contract** — subclasses MUST implement certain methods.

### Using the `abc` Module

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    """Abstract base class — cannot be instantiated."""
    
    @abstractmethod
    def area(self):
        """Subclasses MUST implement this method."""
        pass
    
    @abstractmethod
    def perimeter(self):
        """Subclasses MUST implement this method."""
        pass
    
    # Concrete method — shared by all subclasses
    def describe(self):
        return f"{self.__class__.__name__}: Area={self.area():.2f}, Perimeter={self.perimeter():.2f}"

# Cannot instantiate abstract class
# s = Shape()  # TypeError: Can't instantiate abstract class Shape

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height
    
    def area(self):          # MUST implement
        return self.width * self.height
    
    def perimeter(self):     # MUST implement
        return 2 * (self.width + self.height)

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius
    
    def area(self):
        return 3.14159 * self.radius ** 2
    
    def perimeter(self):
        return 2 * 3.14159 * self.radius

# If subclass doesn't implement ALL abstract methods:
# class Incomplete(Shape):
#     def area(self):
#         return 0
#     # Missing perimeter() → TypeError on instantiation!

# Usage
r = Rectangle(10, 5)
c = Circle(7)
print(r.describe())   # Rectangle: Area=50.00, Perimeter=30.00
print(c.describe())   # Circle: Area=153.94, Perimeter=43.98
```

---

## 23.6 Abstract Properties

```python
from abc import ABC, abstractmethod

class Vehicle(ABC):
    def __init__(self, brand, year):
        self._brand = brand
        self._year = year
    
    @property
    @abstractmethod
    def fuel_type(self):
        """Subclasses must define fuel type."""
        pass
    
    @abstractmethod
    def start(self):
        pass
    
    def info(self):
        return f"{self._brand} ({self._year}) — {self.fuel_type}"

class PetrolCar(Vehicle):
    @property
    def fuel_type(self):
        return "Petrol"
    
    def start(self):
        return f"{self._brand} petrol engine started"

class ElectricCar(Vehicle):
    @property
    def fuel_type(self):
        return "Electric"
    
    def start(self):
        return f"{self._brand} electric motor activated"

car1 = PetrolCar("Toyota", 2023)
car2 = ElectricCar("Tesla", 2024)
print(car1.info())    # Toyota (2023) — Petrol
print(car2.start())   # Tesla electric motor activated
```

---

## 23.7 Interface Design Pattern

### Defining Contracts with ABCs

```python
from abc import ABC, abstractmethod

class PaymentProcessor(ABC):
    """Interface — all payment processors must implement these methods."""
    
    @abstractmethod
    def authorize(self, amount):
        """Authorize a payment. Returns transaction ID."""
        pass
    
    @abstractmethod
    def capture(self, transaction_id):
        """Capture an authorized payment."""
        pass
    
    @abstractmethod
    def refund(self, transaction_id, amount):
        """Refund a captured payment."""
        pass

class CreditCardProcessor(PaymentProcessor):
    def authorize(self, amount):
        print(f"Credit card: Authorizing ₹{amount:,.2f}")
        return "CC-TXN-001"
    
    def capture(self, transaction_id):
        print(f"Credit card: Capturing {transaction_id}")
        return True
    
    def refund(self, transaction_id, amount):
        print(f"Credit card: Refunding ₹{amount:,.2f} for {transaction_id}")
        return True

class UPIProcessor(PaymentProcessor):
    def authorize(self, amount):
        print(f"UPI: Authorizing ₹{amount:,.2f}")
        return "UPI-TXN-001"
    
    def capture(self, transaction_id):
        print(f"UPI: Capturing {transaction_id}")
        return True
    
    def refund(self, transaction_id, amount):
        print(f"UPI: Refunding ₹{amount:,.2f} for {transaction_id}")
        return True

# Function works with ANY payment processor
def process_payment(processor: PaymentProcessor, amount):
    txn_id = processor.authorize(amount)
    processor.capture(txn_id)
    return txn_id

# Polymorphism through abstraction
cc = CreditCardProcessor()
upi = UPIProcessor()
process_payment(cc, 5000)
process_payment(upi, 2000)
```

---

## 23.8 Practical Encapsulation Patterns

### Pattern 1: Immutable Object

```python
class ImmutablePoint:
    """A point that cannot be changed after creation."""
    
    def __init__(self, x, y):
        self._x = x
        self._y = y
    
    @property
    def x(self):
        return self._x
    
    @property
    def y(self):
        return self._y
    
    def __str__(self):
        return f"Point({self._x}, {self._y})"
    
    def __eq__(self, other):
        return self._x == other._x and self._y == other._y
    
    def __hash__(self):
        return hash((self._x, self._y))

p = ImmutablePoint(3, 4)
print(p.x)       # 3
# p.x = 10       # AttributeError — no setter!
```

### Pattern 2: Validated Container

```python
class TemperatureLog:
    """A log that only accepts valid temperature readings."""
    
    def __init__(self):
        self._readings = []
    
    def add(self, temp):
        if not isinstance(temp, (int, float)):
            raise TypeError("Temperature must be a number")
        if temp < -273.15:
            raise ValueError("Temperature below absolute zero")
        self._readings.append(float(temp))
    
    @property
    def count(self):
        return len(self._readings)
    
    @property
    def average(self):
        if not self._readings:
            return 0
        return sum(self._readings) / len(self._readings)
    
    @property
    def min_temp(self):
        return min(self._readings) if self._readings else None
    
    @property
    def max_temp(self):
        return max(self._readings) if self._readings else None
    
    def __len__(self):
        return len(self._readings)
    
    def __str__(self):
        return f"TemperatureLog({self.count} readings, avg={self.average:.1f}°C)"
```

### Pattern 3: Access-Controlled Manager

```python
class UserManager:
    """Manages users with role-based access control."""
    
    def __init__(self):
        self.__users = {}           # Private — internal storage
        self.__admin_password = "admin123"  # Private
    
    def add_user(self, username, role="viewer"):
        if username in self.__users:
            raise ValueError(f"User '{username}' already exists")
        self.__users[username] = {"role": role, "active": True}
    
    def get_user(self, username):
        user = self.__users.get(username)
        if user:
            return {"username": username, "role": user["role"]}  # Don't expose internal dict
        return None
    
    @property
    def user_count(self):
        return len(self.__users)
    
    def list_users(self):
        return [{"username": u, "role": d["role"]} for u, d in self.__users.items() if d["active"]]
    
    def delete_user(self, username, admin_password):
        if admin_password != self.__admin_password:
            raise PermissionError("Invalid admin password")
        if username not in self.__users:
            raise ValueError(f"User '{username}' not found")
        self.__users[username]["active"] = False
```

---

## 23.9 Best Practices

| Practice | Why |
|----------|-----|
| **Use `_` prefix for protected** | Signals "internal use" to other developers |
| **Use `__` prefix sparingly** | Only when name-mangling is truly needed |
| **Prefer `@property` over getters/setters** | Pythonic — `obj.value` not `obj.get_value()` |
| **Use ABCs for contracts** | Enforce interface implementation |
| **Keep public interface minimal** | Expose only what users need |
| **Validate in setters** | Protect data integrity |
| **Return copies, not references** | Prevent external mutation of internal data |
| **Document the public API** | Docstrings on all public methods |

---

## 🔧 Hands-On Activity: Protected & Abstract Classes

**Duration:** 25 minutes

Create a file `session23_encapsulation.py`:

```python
# Session 23 — Encapsulation & Abstraction
from abc import ABC, abstractmethod

# Part 1: Abstract Base Class
class DatabaseConnector(ABC):
    @abstractmethod
    def connect(self):
        pass
    
    @abstractmethod
    def execute(self, query):
        pass
    
    @abstractmethod
    def disconnect(self):
        pass
    
    def status(self):
        return f"{self.__class__.__name__} connector"

class SQLiteConnector(DatabaseConnector):
    def __init__(self, db_name):
        self._db_name = db_name
        self._connected = False
    
    def connect(self):
        self._connected = True
        return f"Connected to SQLite: {self._db_name}"
    
    def execute(self, query):
        if not self._connected:
            raise RuntimeError("Not connected!")
        return f"SQLite executing: {query}"
    
    def disconnect(self):
        self._connected = False
        return "SQLite disconnected"

class MySQLConnector(DatabaseConnector):
    def __init__(self, host, port=3306):
        self._host = host
        self._port = port
        self._connected = False
    
    def connect(self):
        self._connected = True
        return f"Connected to MySQL: {self._host}:{self._port}"
    
    def execute(self, query):
        if not self._connected:
            raise RuntimeError("Not connected!")
        return f"MySQL executing: {query}"
    
    def disconnect(self):
        self._connected = False
        return "MySQL disconnected"

# Polymorphism with abstraction
print("=== Part 1: Abstract Database ===")
for db in [SQLiteConnector("app.db"), MySQLConnector("localhost")]:
    print(f"  {db.status()}")
    print(f"  {db.connect()}")
    print(f"  {db.execute('SELECT * FROM users')}")
    print(f"  {db.disconnect()}")
    print()

# Part 2: Encapsulated Class
class SecureWallet:
    def __init__(self, owner, pin):
        self._owner = owner
        self.__pin = pin
        self.__balance = 0.0
        self.__transactions = []
    
    def _verify_pin(self, pin):
        return pin == self.__pin
    
    def deposit(self, amount):
        if amount <= 0:
            raise ValueError("Amount must be positive")
        self.__balance += amount
        self.__transactions.append(("DEPOSIT", amount))
        return f"Deposited ₹{amount:,.2f}"
    
    def withdraw(self, amount, pin):
        if not self._verify_pin(pin):
            raise PermissionError("Invalid PIN")
        if amount <= 0:
            raise ValueError("Amount must be positive")
        if amount > self.__balance:
            raise ValueError("Insufficient funds")
        self.__balance -= amount
        self.__transactions.append(("WITHDRAW", amount))
        return f"Withdrew ₹{amount:,.2f}"
    
    @property
    def balance(self):
        return self.__balance
    
    def get_statement(self, pin):
        if not self._verify_pin(pin):
            raise PermissionError("Invalid PIN")
        return list(self.__transactions)  # Return copy, not reference
    
    def change_pin(self, old_pin, new_pin):
        if not self._verify_pin(old_pin):
            raise PermissionError("Invalid current PIN")
        if len(str(new_pin)) != 4:
            raise ValueError("PIN must be 4 digits")
        self.__pin = new_pin
        return "PIN changed successfully"

print("=== Part 2: Secure Wallet ===")
wallet = SecureWallet("Alice", "1234")
print(wallet.deposit(10000))
print(wallet.deposit(5000))
print(wallet.withdraw(3000, "1234"))
print(f"Balance: ₹{wallet.balance:,.2f}")

try:
    wallet.withdraw(1000, "0000")
except PermissionError as e:
    print(f"Error: {e}")

print(f"Transactions: {wallet.get_statement('1234')}")
print(wallet.change_pin("1234", "5678"))

print("\nDone!")
```

---

## Session 23 — Key Takeaways

1. **Encapsulation** protects data — `_protected`, `__private` naming conventions
2. **Name mangling** (`__attr` → `_Class__attr`) discourages but doesn't prevent access
3. **`@property`** is the Pythonic way to create getters/setters with validation
4. **Abstract Base Classes** (ABC) define contracts — subclasses MUST implement abstract methods
5. **Abstraction** hides complexity — expose WHAT, hide HOW
6. **Return copies** of internal data to prevent external mutation

---

## Preparation for Session 24
- Practice: Add PIN-protected features to the BankAccount class
- Think about: How would you organize a large Python project into folders?
- Review: What is `__init__.py`? How do packages work?

---

*Session 23 of 30 | Module 5: Object-Oriented Programming*
*Professional Python Programming Certification — UpSkill Global Education Technologies Inc., Canada*
