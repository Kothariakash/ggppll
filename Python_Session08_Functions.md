# Session 8 — Functions in Python
## Module 2: Control Flow & Functions | Professional Python Programming Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Build a Function Library for Reusable Utilities

---

## Learning Objectives
By the end of this session, you will be able to:
1. Define and call functions using `def`
2. Work with parameters, arguments, and return values
3. Understand variable scope (local, global, nonlocal)
4. Use default, keyword, and variable-length arguments (*args, **kwargs)
5. Write lambda (anonymous) functions
6. Apply recursion for self-referencing problems

---

## 8.1 What is a Function?

A **function** is a reusable block of code that performs a specific task. It runs only when called.

### Why Functions?

| Benefit | Detail |
|---------|--------|
| **Reusability** | Write once, use many times |
| **Organization** | Break complex programs into manageable pieces |
| **Readability** | Named functions describe what they do |
| **Debugging** | Test and fix one function at a time |
| **DRY Principle** | Don't Repeat Yourself |

### Anatomy of a Function

```python
def function_name(parameters):
    """Docstring — describes what the function does."""
    # Function body
    result = ...
    return result   # Optional — returns a value to the caller
```

---

## 8.2 Defining and Calling Functions

### Basic Function

```python
# Define
def greet():
    print("Hello, World!")

# Call
greet()          # Hello, World!
greet()          # Hello, World! — can call multiple times
```

### Function with Parameters

```python
def greet(name):
    print(f"Hello, {name}!")

greet("Alice")   # Hello, Alice!
greet("Bob")     # Hello, Bob!
```

### Function with Return Value

```python
def add(a, b):
    return a + b

result = add(10, 20)
print(result)    # 30

# Use return value directly
print(add(5, 3))  # 8
```

### Multiple Return Values

```python
def get_stats(numbers):
    return min(numbers), max(numbers), sum(numbers) / len(numbers)

low, high, avg = get_stats([10, 20, 30, 40, 50])
print(f"Min: {low}, Max: {high}, Avg: {avg}")
# Min: 10, Max: 50, Avg: 30.0
```

### Return vs Print

| `return` | `print()` |
|----------|-----------|
| Sends value back to caller | Displays text on screen |
| Can be stored in a variable | Cannot be captured (returns None) |
| Exits the function immediately | Function continues |
| Used for computation | Used for output/debugging |

```python
def add_return(a, b):
    return a + b

def add_print(a, b):
    print(a + b)

x = add_return(5, 3)    # x = 8
y = add_print(5, 3)     # Prints 8, but y = None
```

---

## 8.3 Parameters and Arguments

### Terminology

| Term | Definition | Example |
|------|-----------|---------|
| **Parameter** | Variable in function definition | `def greet(name):` — `name` is a parameter |
| **Argument** | Value passed when calling | `greet("Alice")` — `"Alice"` is an argument |

### Positional Arguments

```python
def describe(name, age, city):
    print(f"{name}, age {age}, from {city}")

describe("Alice", 25, "Delhi")    # Positional — order matters!
describe(25, "Delhi", "Alice")    # WRONG order → wrong output
```

### Keyword Arguments

```python
# Name the parameters explicitly — order doesn't matter
describe(age=25, city="Delhi", name="Alice")   # Correct!
describe("Alice", city="Delhi", age=25)        # Mix positional + keyword
```

> **Rule:** Positional arguments must come before keyword arguments.

### Default Parameter Values

```python
def greet(name, greeting="Hello"):
    print(f"{greeting}, {name}!")

greet("Alice")              # Hello, Alice!
greet("Alice", "Hi")        # Hi, Alice!
greet("Alice", "Welcome")   # Welcome, Alice!
```

> **Rule:** Parameters with defaults must come after parameters without defaults.

```python
# WRONG
# def greet(greeting="Hello", name):  # SyntaxError!

# CORRECT
def greet(name, greeting="Hello"):
    pass
```

### Mutable Default Argument Trap

```python
# WRONG — mutable default is shared across calls
def add_item(item, items=[]):
    items.append(item)
    return items

print(add_item("a"))  # ['a']
print(add_item("b"))  # ['a', 'b'] — Bug! Expected ['b']

# CORRECT — use None as default
def add_item(item, items=None):
    if items is None:
        items = []
    items.append(item)
    return items

print(add_item("a"))  # ['a']
print(add_item("b"))  # ['b'] — Correct!
```

---

## 8.4 Variable-Length Arguments (*args, **kwargs)

### *args — Variable Positional Arguments

Collects extra positional arguments into a **tuple**.

```python
def total(*args):
    print(f"Type: {type(args)}")  # <class 'tuple'>
    return sum(args)

print(total(1, 2, 3))           # 6
print(total(10, 20, 30, 40))    # 100
print(total(5))                 # 5
```

### **kwargs — Variable Keyword Arguments

Collects extra keyword arguments into a **dictionary**.

```python
def show_info(**kwargs):
    print(f"Type: {type(kwargs)}")  # <class 'dict'>
    for key, value in kwargs.items():
        print(f"  {key}: {value}")

show_info(name="Alice", age=25, city="Delhi")
# Output:
#   name: Alice
#   age: 25
#   city: Delhi
```

### Combining All Parameter Types

```python
def example(a, b, *args, **kwargs):
    print(f"a={a}, b={b}")
    print(f"args={args}")
    print(f"kwargs={kwargs}")

example(1, 2, 3, 4, 5, name="Alice", age=25)
# a=1, b=2
# args=(3, 4, 5)
# kwargs={'name': 'Alice', 'age': 25}
```

### Parameter Order Rule

```
def func(positional, default=value, *args, keyword_only, **kwargs):
```

| Position | Type | Example |
|----------|------|---------|
| 1st | Positional | `a, b` |
| 2nd | Default values | `c=10` |
| 3rd | *args | `*args` |
| 4th | Keyword-only | `kw1, kw2` |
| 5th | **kwargs | `**kwargs` |

---

## 8.5 Variable Scope

### Local vs Global

```python
x = 100  # Global variable

def my_func():
    x = 10  # Local variable (different from global x)
    print(f"Inside function: x = {x}")

my_func()         # Inside function: x = 10
print(f"Outside: x = {x}")  # Outside: x = 100
```

### The global Keyword

```python
count = 0

def increment():
    global count    # Refer to the global variable
    count += 1

increment()
increment()
print(count)    # 2
```

### The nonlocal Keyword (Nested Functions)

```python
def outer():
    x = 10
    def inner():
        nonlocal x    # Refer to enclosing function's variable
        x += 5
    inner()
    print(x)    # 15

outer()
```

### LEGB Rule — Scope Resolution Order

```
L — Local        : Variables inside the current function
E — Enclosing    : Variables in enclosing (outer) functions
G — Global       : Variables at module (file) level
B — Built-in     : Python's built-in names (print, len, etc.)
```

```python
x = "global"

def outer():
    x = "enclosing"
    def inner():
        x = "local"
        print(x)    # "local" — L found first
    inner()

outer()
```

> **Best Practice:** Avoid using `global`. Pass values as arguments and return results instead.

---

## 8.6 Docstrings

### What is a Docstring?

A string literal that appears as the first statement in a function — documents its purpose.

```python
def calculate_bmi(weight_kg, height_m):
    """
    Calculate Body Mass Index (BMI).
    
    Parameters:
        weight_kg (float): Weight in kilograms
        height_m (float): Height in meters
    
    Returns:
        float: BMI value rounded to 2 decimal places
    
    Example:
        >>> calculate_bmi(70, 1.75)
        22.86
    """
    return round(weight_kg / (height_m ** 2), 2)

# Access the docstring
print(calculate_bmi.__doc__)
help(calculate_bmi)
```

---

## 8.7 Lambda Functions

### Syntax

```python
lambda parameters: expression
```

### Examples

```python
# Regular function
def square(x):
    return x ** 2

# Lambda equivalent
square = lambda x: x ** 2
print(square(5))   # 25

# Lambda with multiple parameters
add = lambda a, b: a + b
print(add(3, 7))   # 10

# Lambda in sorting
students = [("Alice", 85), ("Bob", 92), ("Charlie", 78)]
students.sort(key=lambda s: s[1], reverse=True)
print(students)  # [('Bob', 92), ('Alice', 85), ('Charlie', 78)]

# Lambda with map()
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x ** 2, numbers))
print(squared)   # [1, 4, 9, 16, 25]

# Lambda with filter()
evens = list(filter(lambda x: x % 2 == 0, numbers))
print(evens)     # [2, 4]
```

### When to Use Lambda

| Use Lambda | Use def |
|-----------|---------|
| Simple, one-line expressions | Multi-line logic |
| Throwaway functions (sorting keys) | Reusable functions |
| Passed as arguments to map/filter/sorted | Functions with docstrings |

---

## 8.8 Higher-Order Functions

Functions that **take other functions as arguments** or **return functions**.

### map() — Apply Function to Every Item

```python
numbers = [1, 2, 3, 4, 5]
doubled = list(map(lambda x: x * 2, numbers))
print(doubled)  # [2, 4, 6, 8, 10]

# With a named function
def to_upper(s):
    return s.upper()

names = ["alice", "bob", "charlie"]
upper_names = list(map(to_upper, names))
print(upper_names)  # ['ALICE', 'BOB', 'CHARLIE']
```

### filter() — Keep Items That Pass a Test

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
evens = list(filter(lambda x: x % 2 == 0, numbers))
print(evens)  # [2, 4, 6, 8, 10]
```

### sorted() with Key Function

```python
words = ["banana", "apple", "cherry", "date"]
by_length = sorted(words, key=len)
print(by_length)  # ['date', 'apple', 'banana', 'cherry']

# Sort by last character
by_last = sorted(words, key=lambda w: w[-1])
print(by_last)  # ['banana', 'apple', 'date', 'cherry']
```

---

## 8.9 Recursion

### What is Recursion?

A function that **calls itself** to solve a problem by breaking it into smaller sub-problems.

### Structure

```python
def recursive_func(params):
    if base_condition:
        return base_value        # Base case — stops recursion
    return recursive_func(smaller_params)  # Recursive case
```

### Example: Factorial

```python
# 5! = 5 × 4 × 3 × 2 × 1 = 120
def factorial(n):
    if n <= 1:
        return 1                 # Base case
    return n * factorial(n - 1)  # Recursive case

print(factorial(5))  # 120

# How it works:
# factorial(5) = 5 * factorial(4)
#              = 5 * 4 * factorial(3)
#              = 5 * 4 * 3 * factorial(2)
#              = 5 * 4 * 3 * 2 * factorial(1)
#              = 5 * 4 * 3 * 2 * 1
#              = 120
```

### Example: Fibonacci

```python
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

for i in range(10):
    print(fibonacci(i), end=" ")
# 0 1 1 2 3 5 8 13 21 34
```

### Recursion vs Iteration

| Recursion | Iteration |
|-----------|-----------|
| Elegant for tree/graph problems | Generally faster |
| Risk of stack overflow | No stack limit |
| Uses more memory (call stack) | Uses less memory |
| May be slower (function call overhead) | Usually faster |

> **Python's default recursion limit:** 1000 calls. Change with `sys.setrecursionlimit()`.

---

## 🔧 Hands-On Activity: Utility Function Library

**Duration:** 25 minutes

Create a file `session08_functions.py`:

```python
# Session 8 — Utility Function Library

# --- Part 1: Basic Functions ---
def celsius_to_fahrenheit(celsius):
    """Convert Celsius to Fahrenheit."""
    return (celsius * 9/5) + 32

def fahrenheit_to_celsius(fahrenheit):
    """Convert Fahrenheit to Celsius."""
    return (fahrenheit - 32) * 5/9

def calculate_bmi(weight_kg, height_m):
    """Calculate BMI and return (bmi, category)."""
    bmi = weight_kg / (height_m ** 2)
    if bmi < 18.5:
        category = "Underweight"
    elif bmi < 25:
        category = "Normal"
    elif bmi < 30:
        category = "Overweight"
    else:
        category = "Obese"
    return round(bmi, 2), category

# --- Part 2: Functions with *args / **kwargs ---
def calculate_total(*prices, tax_rate=0.18):
    """Calculate total with tax."""
    subtotal = sum(prices)
    tax = subtotal * tax_rate
    return round(subtotal + tax, 2)

def create_profile(**info):
    """Create a formatted profile string."""
    lines = []
    for key, value in info.items():
        lines.append(f"  {key.title():<15}: {value}")
    return "\n".join(lines)

# --- Part 3: Lambda + Higher-Order ---
def apply_operation(numbers, operation):
    """Apply a function to each number in the list."""
    return [operation(n) for n in numbers]

# --- Testing ---
print("=== Temperature Converter ===")
print(f"100°C = {celsius_to_fahrenheit(100)}°F")
print(f"212°F = {fahrenheit_to_celsius(212):.1f}°C")

print("\n=== BMI Calculator ===")
bmi, cat = calculate_bmi(70, 1.75)
print(f"BMI: {bmi} — {cat}")

print("\n=== Price Calculator ===")
print(f"Total: ₹{calculate_total(500, 300, 200)}")
print(f"Total (5% tax): ₹{calculate_total(500, 300, tax_rate=0.05)}")

print("\n=== Profile ===")
print(create_profile(name="Alice", age=25, city="Delhi", role="Developer"))

print("\n=== Lambda Operations ===")
nums = [1, 2, 3, 4, 5]
print(f"Squared: {apply_operation(nums, lambda x: x**2)}")
print(f"Doubled: {apply_operation(nums, lambda x: x*2)}")
```

Run and verify. Save.

---

## Session 8 — Key Takeaways

1. **Functions** organize code into reusable, named blocks — `def name(params): return result`
2. **Parameters:** positional, default, `*args` (tuple), `**kwargs` (dict)
3. **Scope:** Local → Enclosing → Global → Built-in (LEGB rule)
4. **Lambda** functions are one-line anonymous functions for simple operations
5. **Higher-order functions:** `map()`, `filter()`, `sorted()` accept functions as arguments
6. **Recursion** solves problems by self-reference — always needs a base case

---

## Preparation for Session 9
- Practice: Create a function that checks if a number is prime
- Think about: How do you reuse functions across multiple files?
- Review: What is a module? What is `import`?

---

*Session 8 of 30 | Module 2: Control Flow & Functions*
*Professional Python Programming Certification — UpSkill Global Education Technologies Inc., Canada*
