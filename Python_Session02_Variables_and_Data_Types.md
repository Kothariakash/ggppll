# Session 2 — Variables & Data Types
## Module 1: Python Fundamentals | Professional Python Programming Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Variable Declarations, Type Conversions & Explorations

---

## Learning Objectives
By the end of this session, you will be able to:
1. Declare and use variables in Python
2. Understand Python's dynamic typing
3. Work with all core data types (int, float, str, bool, None)
4. Perform type conversions (casting)
5. Use the `type()` and `id()` functions for introspection

---

## 2.1 What is a Variable?

A **variable** is a named container that stores a value in memory. Think of it as a label attached to a piece of data.

```python
name = "Alice"      # Variable 'name' stores the string "Alice"
age = 25            # Variable 'age' stores the integer 25
salary = 75000.50   # Variable 'salary' stores the float 75000.50
```

### How Variables Work in Python

```
Variable Name ──→ Reference ──→ Object in Memory
   name       ──→   ref     ──→  "Alice" (str object)
   age        ──→   ref     ──→  25 (int object)
```

- In Python, variables are **references** (labels) that point to objects in memory
- The variable does NOT contain the value — it points to it
- Multiple variables can point to the same object

```python
a = 10
b = a       # Both 'a' and 'b' point to the same object (10)
print(a)    # 10
print(b)    # 10
print(a is b)  # True — same object in memory
```

---

## 2.2 Variable Naming Rules

### Rules (Must Follow)

| Rule | Valid | Invalid |
|------|-------|---------|
| Start with letter or underscore | `name`, `_count` | `1name`, `@var` |
| Contain letters, digits, underscores | `student_1`, `total_score` | `student-1`, `total score` |
| Case-sensitive | `Name` ≠ `name` ≠ `NAME` | — |
| Cannot be a reserved keyword | `my_class` | `class`, `if`, `for` |

### Python Reserved Keywords (35)

```python
import keyword
print(keyword.kwlist)
```

```
False, None, True, and, as, assert, async, await, break, class,
continue, def, del, elif, else, except, finally, for, from, global,
if, import, in, is, lambda, nonlocal, not, or, pass, raise, return,
try, while, with, yield
```

### Naming Conventions (Best Practices)

| Convention | Use For | Example |
|-----------|---------|---------|
| `snake_case` | Variables, functions | `student_name`, `total_marks` |
| `UPPER_SNAKE_CASE` | Constants | `MAX_RETRIES`, `PI` |
| `PascalCase` | Classes | `StudentRecord`, `BankAccount` |
| `_single_leading_underscore` | Private/internal use | `_helper_func` |
| `__double_leading` | Name mangling (advanced) | `__private_var` |

### Good vs Bad Variable Names

| Bad | Good | Why |
|-----|------|-----|
| `x` | `total_revenue` | Descriptive |
| `n` | `student_count` | Self-documenting |
| `temp` | `celsius_temperature` | Clear meaning |
| `data` | `employee_records` | Specific |
| `lst` | `product_list` | Readable |

---

## 2.3 Multiple Assignments

### Assign Multiple Variables in One Line

```python
# Multiple assignment
x, y, z = 10, 20, 30
print(x, y, z)  # 10 20 30

# Same value to multiple variables
a = b = c = 100
print(a, b, c)  # 100 100 100

# Swap variables (Python magic!)
x, y = 10, 20
x, y = y, x
print(x, y)  # 20 10
```

### Unpacking

```python
# Unpack a list/tuple into variables
coordinates = (10, 20, 30)
x, y, z = coordinates
print(x)  # 10
print(y)  # 20
print(z)  # 30
```

---

## 2.4 Core Data Types

### Python's Built-in Data Types

| Category | Type | Example | Mutable? |
|----------|------|---------|----------|
| **Numeric** | `int` | `42`, `-7`, `0` | No |
| | `float` | `3.14`, `-0.5`, `2.0` | No |
| | `complex` | `3+4j` | No |
| **Text** | `str` | `"Hello"`, `'World'` | No |
| **Boolean** | `bool` | `True`, `False` | No |
| **None** | `NoneType` | `None` | No |
| **Sequence** | `list` | `[1, 2, 3]` | Yes |
| | `tuple` | `(1, 2, 3)` | No |
| | `range` | `range(10)` | No |
| **Mapping** | `dict` | `{"key": "value"}` | Yes |
| **Set** | `set` | `{1, 2, 3}` | Yes |
| | `frozenset` | `frozenset({1, 2})` | No |

> Sessions 11–14 cover Lists, Tuples, Dictionaries, Sets, and Strings in detail. This session focuses on **int, float, str, bool, None**.

---

## 2.5 Integer (int)

### What is an Integer?

Whole numbers — positive, negative, or zero. **No decimal point.**

```python
age = 25
temperature = -5
count = 0
population = 1_400_000_000   # Underscores for readability (1.4 billion)

print(type(age))  # <class 'int'>
```

### Integer Operations

```python
print(10 + 3)   # 13  — Addition
print(10 - 3)   # 7   — Subtraction
print(10 * 3)   # 30  — Multiplication
print(10 / 3)   # 3.3333  — Division (returns float!)
print(10 // 3)  # 3   — Floor division (integer result)
print(10 % 3)   # 1   — Modulus (remainder)
print(10 ** 3)  # 1000 — Exponentiation (power)
```

### Python Integers Have No Size Limit

```python
big_number = 999999999999999999999999999999999
print(big_number)       # Works! Python handles arbitrarily large integers
print(type(big_number)) # <class 'int'>
```

### Number Bases

```python
decimal = 42        # Base 10 (default)
binary = 0b101010   # Base 2 (prefix 0b)
octal = 0o52        # Base 8 (prefix 0o)
hexadecimal = 0x2A  # Base 16 (prefix 0x)

print(decimal, binary, octal, hexadecimal)  # 42 42 42 42
```

---

## 2.6 Float (float)

### What is a Float?

Numbers with a **decimal point** — representing real numbers.

```python
price = 99.99
pi = 3.14159
negative = -0.5
scientific = 2.5e6   # 2.5 × 10^6 = 2500000.0

print(type(price))  # <class 'float'>
```

### Float Precision Warning

```python
print(0.1 + 0.2)           # 0.30000000000000004 (NOT 0.3!)
print(0.1 + 0.2 == 0.3)    # False!
```

> **Why?** Floats use binary representation (IEEE 754) — some decimal numbers can't be represented exactly.

**Solutions:**
```python
# Round for display
print(round(0.1 + 0.2, 2))  # 0.3

# Use decimal module for exact arithmetic
from decimal import Decimal
print(Decimal('0.1') + Decimal('0.2'))  # 0.3
```

### Special Float Values

```python
print(float('inf'))    # Infinity
print(float('-inf'))   # Negative Infinity
print(float('nan'))    # Not a Number
```

---

## 2.7 String (str)

### What is a String?

A **sequence of characters** enclosed in quotes — single `'`, double `"`, or triple `'''` / `"""`.

```python
name = "Alice"
greeting = 'Hello, World!'
multiline = """This is
a multi-line
string"""
empty = ""

print(type(name))  # <class 'str'>
```

### String Operations (Preview)

```python
# Concatenation
full_name = "Alice" + " " + "Johnson"
print(full_name)  # Alice Johnson

# Repetition
line = "-" * 40
print(line)  # ----------------------------------------

# Length
print(len("Hello"))  # 5

# Indexing (0-based)
text = "Python"
print(text[0])   # P
print(text[-1])  # n (last character)

# Slicing
print(text[0:3])  # Pyt
print(text[2:])   # thon
```

### f-Strings (Formatted String Literals) — Python 3.6+

```python
name = "Alice"
age = 25
salary = 75000.50

# f-string formatting
print(f"Name: {name}")
print(f"Age: {age}")
print(f"Salary: ${salary:,.2f}")     # $75,000.50
print(f"Next year: {age + 1}")       # Expressions inside {}
print(f"{'Hello':>20}")              # Right-aligned in 20 chars
print(f"{'Hello':<20}")              # Left-aligned
print(f"{'Hello':^20}")              # Center-aligned
```

### Escape Characters

| Escape | Meaning | Example |
|--------|---------|---------|
| `\n` | Newline | `"Line1\nLine2"` |
| `\t` | Tab | `"Col1\tCol2"` |
| `\\` | Backslash | `"C:\\Users"` |
| `\'` | Single quote | `'It\'s OK'` |
| `\"` | Double quote | `"He said \"Hi\""` |

### Raw Strings

```python
# Raw string — backslashes are NOT treated as escape characters
path = r"C:\Users\Documents\file.txt"
print(path)  # C:\Users\Documents\file.txt
```

---

## 2.8 Boolean (bool)

### What is a Boolean?

A data type with only two values: `True` or `False`. Used for conditions and logic.

```python
is_active = True
is_admin = False

print(type(is_active))  # <class 'bool'>
```

### Booleans are Integers

```python
print(True + True)    # 2  (True = 1)
print(False + True)   # 1  (False = 0)
print(True * 10)      # 10
```

### Truthy and Falsy Values

In Python, every value has a boolean interpretation:

| Falsy (evaluates to False) | Truthy (evaluates to True) |
|---------------------------|---------------------------|
| `False` | `True` |
| `0`, `0.0`, `0j` | Any non-zero number |
| `""` (empty string) | Any non-empty string |
| `[]` (empty list) | Any non-empty list |
| `{}` (empty dict) | Any non-empty dict |
| `()` (empty tuple) | Any non-empty tuple |
| `set()` (empty set) | Any non-empty set |
| `None` | Everything else |

```python
print(bool(0))        # False
print(bool(""))       # False
print(bool([]))       # False
print(bool(None))     # False

print(bool(42))       # True
print(bool("Hello"))  # True
print(bool([1, 2]))   # True
```

---

## 2.9 None (NoneType)

### What is None?

`None` represents the **absence of a value** — similar to `null` in other languages.

```python
result = None
print(result)        # None
print(type(result))  # <class 'NoneType'>
```

### Common Uses of None

```python
# 1. Default function return
def greet(name):
    print(f"Hello, {name}")

result = greet("Alice")  # Prints "Hello, Alice"
print(result)            # None (function has no return statement)

# 2. Initialize a variable
user = None
# ... later in the code
user = "Alice"

# 3. Check for None
if user is None:
    print("No user set")
else:
    print(f"User: {user}")
```

> **Use `is None`** not `== None` for comparison. `is` checks identity, `==` checks value.

---

## 2.10 Type Checking & Type Conversion

### type() — Check the Type

```python
print(type(42))         # <class 'int'>
print(type(3.14))       # <class 'float'>
print(type("Hello"))    # <class 'str'>
print(type(True))       # <class 'bool'>
print(type(None))       # <class 'NoneType'>
```

### isinstance() — Check if Object is a Specific Type

```python
age = 25
print(isinstance(age, int))      # True
print(isinstance(age, float))    # False
print(isinstance(age, (int, float)))  # True (check multiple types)
```

### id() — Memory Address

```python
x = 42
print(id(x))  # e.g., 140234567890 (memory address)
```

### Type Conversion (Casting)

| Function | Converts To | Example |
|----------|------------|---------|
| `int()` | Integer | `int("42")` → `42` |
| `float()` | Float | `float("3.14")` → `3.14` |
| `str()` | String | `str(42)` → `"42"` |
| `bool()` | Boolean | `bool(1)` → `True` |

```python
# String to Integer
age_str = "25"
age_int = int(age_str)
print(age_int + 5)  # 30

# Integer to Float
x = float(10)
print(x)  # 10.0

# Float to Integer (truncates, doesn't round)
y = int(3.99)
print(y)  # 3

# Number to String
price = 99.99
price_str = str(price)
print("Price: $" + price_str)  # Price: $99.99

# Invalid conversion — raises ValueError
# int("Hello")  # ValueError: invalid literal for int()
```

### Safe Type Conversion

```python
user_input = "abc"

# Check before converting
if user_input.isdigit():
    number = int(user_input)
    print(f"Number: {number}")
else:
    print("Invalid number!")
```

---

## 2.11 Dynamic Typing

Python is **dynamically typed** — a variable's type is determined at runtime and can change.

```python
x = 10          # x is int
print(type(x))  # <class 'int'>

x = "Hello"     # x is now str — same variable, different type!
print(type(x))  # <class 'str'>

x = [1, 2, 3]   # x is now list
print(type(x))  # <class 'list'>
```

### Dynamic vs Static Typing

| Dynamic Typing (Python) | Static Typing (Java, C++) |
|-------------------------|--------------------------|
| Type determined at runtime | Type declared at compile time |
| Variable can change type | Variable type is fixed |
| `x = 10` then `x = "Hi"` → OK | `int x = 10;` then `x = "Hi";` → Error |
| Faster to write | Safer at compile time |

### Type Hints (Optional Annotations — Python 3.5+)

```python
# Type hints don't enforce types — they're for documentation and tools
name: str = "Alice"
age: int = 25
salary: float = 75000.50
is_active: bool = True

def greet(name: str) -> str:
    return f"Hello, {name}"
```

> Type hints are **not enforced** by Python — they help code editors and linters catch potential issues.

---

## 🔧 Hands-On Activity: Variables & Data Types

**Duration:** 25 minutes

### Tasks

**Part 1 — Variable Basics (8 min)**

Create a file `session02_variables.py`:

```python
# Part 1: Variable Declarations
first_name = "Priya"
last_name = "Sharma"
age = 28
height = 5.6
is_student = True

# Display all variables
print("=== Student Profile ===")
print(f"Name: {first_name} {last_name}")
print(f"Age: {age}")
print(f"Height: {height} ft")
print(f"Student: {is_student}")

# Check types
print(f"\nType of first_name: {type(first_name)}")
print(f"Type of age: {type(age)}")
print(f"Type of height: {type(height)}")
print(f"Type of is_student: {type(is_student)}")
```

**Part 2 — Type Conversions (8 min)**

```python
# Part 2: Type Conversions
print("\n=== Type Conversions ===")

# String to Integer
marks_str = "95"
marks_int = int(marks_str)
print(f"Marks + 5 = {marks_int + 5}")

# Integer to Float
quantity = 10
quantity_float = float(quantity)
print(f"Quantity as float: {quantity_float}")

# Float to Integer
price = 499.99
price_int = int(price)
print(f"Price truncated: {price_int}")

# Number to String (concatenation)
score = 85
print("Score: " + str(score) + "/100")
```

**Part 3 — Exploration (9 min)**

```python
# Part 3: Exploration
print("\n=== Exploration ===")

# Multiple assignment
x, y, z = 10, 20.5, "thirty"
print(f"x={x}, y={y}, z={z}")

# Swap
a, b = 100, 200
print(f"Before swap: a={a}, b={b}")
a, b = b, a
print(f"After swap: a={a}, b={b}")

# Truthy / Falsy
print(f"\nbool(0) = {bool(0)}")
print(f"bool('') = {bool('')}")
print(f"bool(None) = {bool(None)}")
print(f"bool(42) = {bool(42)}")
print(f"bool('Hello') = {bool('Hello')}")

# Dynamic typing
var = 42
print(f"\nvar = {var}, type = {type(var)}")
var = "Now I'm a string"
print(f"var = {var}, type = {type(var)}")

# None
result = None
print(f"\nresult is None: {result is None}")
```

Run and verify all output. Save.

---

## Session 2 — Key Takeaways

1. **Variables** are named references to objects in memory — use `snake_case` naming
2. **Core types:** `int` (whole numbers), `float` (decimals), `str` (text), `bool` (True/False), `None` (absence)
3. **Dynamic typing** — variables can change type at runtime
4. **Type conversion:** `int()`, `float()`, `str()`, `bool()` — always validate before converting
5. **f-strings** (`f"..."`) are the modern way to format strings with embedded expressions
6. **Falsy values:** `0`, `""`, `[]`, `{}`, `None`, `False` — everything else is truthy

---

## Preparation for Session 3
- Review: What mathematical operations can you do in Python?
- Practice: Create 5 variables of different types and print their types
- Think about: What is the difference between `==` and `is`?

---

*Session 2 of 30 | Module 1: Python Fundamentals*
*Professional Python Programming Certification — UpSkill Global Education Technologies Inc., Canada*
