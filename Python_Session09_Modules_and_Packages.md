# Session 9 — Modules & Packages
## Module 2: Control Flow & Functions | Professional Python Programming Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Create and Import Custom Modules

---

## Learning Objectives
By the end of this session, you will be able to:
1. Import and use built-in Python modules
2. Create your own custom modules
3. Understand the different import styles and their trade-offs
4. Work with Python's standard library (math, random, datetime, os)
5. Understand packages and the `__init__.py` file

---

## 9.1 What is a Module?

A **module** is simply a Python file (`.py`) containing functions, classes, and variables that can be reused in other programs.

### Why Modules?

| Benefit | Detail |
|---------|--------|
| **Reusability** | Write once, import anywhere |
| **Organization** | Split large programs into logical files |
| **Namespace** | Avoid naming conflicts between different code |
| **Maintainability** | Update one module, all importers get the update |
| **Community** | 400,000+ packages on PyPI — don't reinvent the wheel |

### Types of Modules

| Type | Description | Example |
|------|-------------|---------|
| **Built-in** | Come with Python installation | `math`, `os`, `sys`, `json` |
| **Standard Library** | Included in Python (no install needed) | `datetime`, `random`, `csv`, `re` |
| **Third-party** | Install via `pip` | `requests`, `pandas`, `flask` |
| **Custom** | Your own `.py` files | `utils.py`, `helpers.py` |

---

## 9.2 Importing Modules

### Import Styles

```python
# Style 1: Import entire module
import math
print(math.sqrt(16))     # 4.0
print(math.pi)           # 3.141592653589793

# Style 2: Import specific items
from math import sqrt, pi
print(sqrt(16))          # 4.0 — no prefix needed
print(pi)                # 3.141592653589793

# Style 3: Import with alias
import math as m
print(m.sqrt(16))        # 4.0

# Style 4: Import specific with alias
from math import sqrt as square_root
print(square_root(16))   # 4.0

# Style 5: Import everything (AVOID)
from math import *
print(sqrt(16))          # Works, but pollutes namespace
```

### Which Style to Use?

| Style | When to Use | Pros | Cons |
|-------|------------|------|------|
| `import module` | General use | Clear origin, no conflicts | Verbose (`math.sqrt`) |
| `from module import func` | Frequent use of specific items | Concise | Less clear origin |
| `import module as alias` | Long module names | Short + clear | Need to remember alias |
| `from module import *` | **Never in production** | Convenient for REPL | Namespace pollution |

> **Best Practice:** Use `import module` or `from module import specific_function`.

---

## 9.3 Built-in Modules — Essential Tour

### math — Mathematical Functions

```python
import math

# Constants
print(math.pi)        # 3.141592653589793
print(math.e)         # 2.718281828459045
print(math.inf)       # inf

# Functions
print(math.sqrt(144))     # 12.0
print(math.pow(2, 10))    # 1024.0
print(math.ceil(4.2))     # 5 (round up)
print(math.floor(4.8))    # 4 (round down)
print(math.fabs(-42))     # 42.0 (absolute value as float)
print(math.factorial(5))  # 120
print(math.gcd(24, 36))   # 12 (greatest common divisor)
print(math.log(100, 10))  # 2.0 (log base 10)
print(math.log2(256))     # 8.0
print(math.sin(math.radians(90)))  # 1.0
```

### random — Random Number Generation

```python
import random

# Random float 0.0 to 1.0
print(random.random())           # e.g., 0.7432

# Random integer in range
print(random.randint(1, 100))    # e.g., 42

# Random choice from a list
colors = ["red", "green", "blue", "yellow"]
print(random.choice(colors))     # e.g., "blue"

# Random sample (no repeats)
print(random.sample(range(1, 50), 6))  # e.g., [12, 37, 5, 42, 28, 3]

# Shuffle a list in place
cards = [1, 2, 3, 4, 5]
random.shuffle(cards)
print(cards)                     # e.g., [3, 1, 5, 2, 4]

# Random float in range
print(random.uniform(10.5, 75.5))  # e.g., 43.27

# Set seed for reproducibility
random.seed(42)
print(random.randint(1, 100))    # Always 82 with seed 42
```

### datetime — Date and Time

```python
from datetime import datetime, date, timedelta

# Current date and time
now = datetime.now()
print(now)                        # 2024-01-15 14:30:45.123456

# Current date only
today = date.today()
print(today)                      # 2024-01-15

# Create specific date
birthday = date(1995, 8, 20)
print(birthday)                   # 1995-08-20

# Date formatting
print(now.strftime("%d-%m-%Y"))           # 15-01-2024
print(now.strftime("%B %d, %Y"))          # January 15, 2024
print(now.strftime("%I:%M %p"))           # 02:30 PM
print(now.strftime("%A, %d %B %Y"))       # Monday, 15 January 2024

# Date arithmetic
tomorrow = today + timedelta(days=1)
next_week = today + timedelta(weeks=1)
age_days = (today - birthday).days
print(f"Age in days: {age_days}")

# Parse string to date
date_str = "2024-03-15"
parsed = datetime.strptime(date_str, "%Y-%m-%d")
print(parsed)
```

### Format Codes for datetime

| Code | Meaning | Example |
|------|---------|---------|
| `%Y` | 4-digit year | 2024 |
| `%m` | Month (01-12) | 01 |
| `%d` | Day (01-31) | 15 |
| `%H` | Hour 24h (00-23) | 14 |
| `%I` | Hour 12h (01-12) | 02 |
| `%M` | Minute (00-59) | 30 |
| `%S` | Second (00-59) | 45 |
| `%p` | AM/PM | PM |
| `%A` | Full weekday | Monday |
| `%B` | Full month name | January |
| `%a` | Short weekday | Mon |
| `%b` | Short month | Jan |

### os — Operating System Interface

```python
import os

# Current working directory
print(os.getcwd())

# List files in a directory
print(os.listdir("."))

# Check if file/directory exists
print(os.path.exists("hello.py"))
print(os.path.isfile("hello.py"))
print(os.path.isdir("my_folder"))

# Join paths (cross-platform)
path = os.path.join("documents", "reports", "sales.csv")
print(path)  # documents/reports/sales.csv (or \ on Windows)

# Get file size
if os.path.exists("hello.py"):
    size = os.path.getsize("hello.py")
    print(f"File size: {size} bytes")

# Environment variables
print(os.environ.get("USERNAME", "Unknown"))
```

### sys — System-Specific Parameters

```python
import sys

print(sys.version)           # Python version string
print(sys.platform)          # 'win32', 'linux', 'darwin'
print(sys.path)              # Module search paths
print(sys.argv)              # Command-line arguments
print(sys.getrecursionlimit())  # Default: 1000
```

### string — String Constants

```python
import string

print(string.ascii_lowercase)   # abcdefghijklmnopqrstuvwxyz
print(string.ascii_uppercase)   # ABCDEFGHIJKLMNOPQRSTUVWXYZ
print(string.digits)            # 0123456789
print(string.punctuation)       # !"#$%&'()*+,-./:;<=>?@[\]^_`{|}~

# Generate a random password
import random
chars = string.ascii_letters + string.digits + string.punctuation
password = ''.join(random.choices(chars, k=12))
print(f"Password: {password}")
```

---

## 9.4 Creating Custom Modules

### Step 1: Create a Module File

Create `my_utils.py`:

```python
# my_utils.py — Custom Utility Module

"""
A collection of utility functions for common calculations.
"""

PI = 3.14159265

def greet(name):
    """Return a greeting message."""
    return f"Hello, {name}!"

def circle_area(radius):
    """Calculate the area of a circle."""
    return PI * radius ** 2

def is_even(number):
    """Check if a number is even."""
    return number % 2 == 0

def celsius_to_fahrenheit(celsius):
    """Convert Celsius to Fahrenheit."""
    return (celsius * 9/5) + 32

def factorial(n):
    """Calculate factorial of n."""
    if n <= 1:
        return 1
    return n * factorial(n - 1)
```

### Step 2: Import and Use It

Create `main.py` (in the same directory):

```python
# main.py — Using our custom module

import my_utils

print(my_utils.greet("Alice"))
print(f"Circle area (r=5): {my_utils.circle_area(5):.2f}")
print(f"Is 42 even? {my_utils.is_even(42)}")

# Or import specific functions
from my_utils import celsius_to_fahrenheit, factorial

print(f"100°C = {celsius_to_fahrenheit(100)}°F")
print(f"5! = {factorial(5)}")
```

### Module Search Path

When you `import module`, Python searches in this order:

1. **Current directory** (where the script is)
2. **PYTHONPATH** environment variable directories
3. **Standard library** directories
4. **Site-packages** (pip-installed packages)

```python
import sys
print(sys.path)  # Shows all search paths
```

---

## 9.5 The `__name__` Variable

### What is `__name__`?

Every Python file has a built-in variable `__name__`:

| Scenario | `__name__` value |
|----------|-----------------|
| File is run directly (`python file.py`) | `"__main__"` |
| File is imported as a module | `"module_name"` (filename without .py) |

### Using `if __name__ == "__main__":`

```python
# my_utils.py

def greet(name):
    return f"Hello, {name}!"

def circle_area(radius):
    return 3.14159 * radius ** 2

# This code ONLY runs when file is executed directly
# NOT when imported as a module
if __name__ == "__main__":
    # Test / demo code
    print(greet("Test User"))
    print(f"Circle area: {circle_area(5):.2f}")
    print("All tests passed!")
```

```python
# main.py
import my_utils  # The test code in my_utils does NOT run

print(my_utils.greet("Alice"))  # Only this runs
```

> **Best Practice:** Always use `if __name__ == "__main__":` for test code in modules.

---

## 9.6 Packages

### What is a Package?

A **package** is a directory containing multiple modules, organized with an `__init__.py` file.

### Package Structure

```
my_project/
│
├── main.py
│
└── utils/                  ← Package (directory)
    ├── __init__.py         ← Makes it a package (can be empty)
    ├── math_utils.py       ← Module
    ├── string_utils.py     ← Module
    └── date_utils.py       ← Module
```

### `__init__.py`

```python
# utils/__init__.py

# Option 1: Empty file — just marks directory as a package

# Option 2: Import commonly used items for convenience
from .math_utils import circle_area, square_area
from .string_utils import clean_text

# Option 3: Define __all__ for 'from package import *'
__all__ = ['math_utils', 'string_utils', 'date_utils']
```

### Importing from Packages

```python
# Import a specific module from package
from utils import math_utils
result = math_utils.circle_area(5)

# Import a specific function from a module in a package
from utils.math_utils import circle_area
result = circle_area(5)

# If __init__.py has imports, can do:
from utils import circle_area
result = circle_area(5)
```

### Nested Packages

```
my_project/
└── company/
    ├── __init__.py
    ├── hr/
    │   ├── __init__.py
    │   ├── payroll.py
    │   └── attendance.py
    └── sales/
        ├── __init__.py
        ├── orders.py
        └── reports.py
```

```python
from company.hr.payroll import calculate_salary
from company.sales.reports import generate_report
```

---

## 9.7 Installing Third-Party Packages

### Using pip

```bash
# Install a package
pip install requests

# Install specific version
pip install requests==2.31.0

# Install multiple packages
pip install requests flask pandas

# Upgrade
pip install --upgrade requests

# Uninstall
pip uninstall requests

# List installed
pip list

# Save dependencies
pip freeze > requirements.txt

# Install from requirements file
pip install -r requirements.txt
```

### Popular Third-Party Packages

| Package | Purpose | Install |
|---------|---------|---------|
| `requests` | HTTP requests (API calls) | `pip install requests` |
| `pandas` | Data analysis | `pip install pandas` |
| `numpy` | Numerical computing | `pip install numpy` |
| `matplotlib` | Charts and plots | `pip install matplotlib` |
| `flask` | Web framework | `pip install flask` |
| `openpyxl` | Excel file handling | `pip install openpyxl` |
| `python-dotenv` | Environment variables | `pip install python-dotenv` |
| `fpdf2` | PDF generation | `pip install fpdf2` |

---

## 9.8 Module Best Practices

| Practice | Why |
|----------|-----|
| **One responsibility per module** | Easier to understand and maintain |
| **Use descriptive module names** | `math_utils.py` not `mu.py` |
| **Add docstrings** | Document what the module does |
| **Use `if __name__ == "__main__":`** | Separate test code from importable code |
| **Avoid circular imports** | Module A imports B, B imports A → error |
| **Keep imports at the top** | PEP 8 standard |
| **Group imports** | stdlib → third-party → local (with blank lines) |

### Import Ordering (PEP 8)

```python
# 1. Standard library imports
import os
import sys
from datetime import datetime

# 2. Third-party imports
import requests
import pandas as pd

# 3. Local/custom imports
from utils.math_utils import circle_area
from utils.string_utils import clean_text
```

---

## 🔧 Hands-On Activity: Create and Use Custom Modules

**Duration:** 25 minutes

### Part 1 — Create a Utility Module (10 min)

Create `calculator_module.py`:

```python
"""Calculator module with basic and advanced operations."""

def add(a, b):
    """Return the sum of two numbers."""
    return a + b

def subtract(a, b):
    """Return the difference of two numbers."""
    return a - b

def multiply(a, b):
    """Return the product of two numbers."""
    return a * b

def divide(a, b):
    """Return the quotient. Returns None if dividing by zero."""
    if b == 0:
        return None
    return a / b

def power(base, exp):
    """Return base raised to the power of exp."""
    return base ** exp

def percentage(value, total):
    """Return the percentage of value out of total."""
    if total == 0:
        return 0
    return (value / total) * 100

if __name__ == "__main__":
    print("--- Calculator Module Tests ---")
    print(f"add(5, 3) = {add(5, 3)}")
    print(f"divide(10, 3) = {divide(10, 3):.2f}")
    print(f"divide(10, 0) = {divide(10, 0)}")
    print(f"percentage(85, 100) = {percentage(85, 100):.1f}%")
    print("All tests passed!")
```

### Part 2 — Use the Module (8 min)

Create `session09_main.py`:

```python
"""Session 9 — Using custom and built-in modules."""
import random
from datetime import datetime
import calculator_module as calc

print("=" * 40)
print("  MODULE DEMO PROGRAM")
print("=" * 40)

# Using custom module
a, b = 25, 7
print(f"\n--- Calculator Module ---")
print(f"{a} + {b} = {calc.add(a, b)}")
print(f"{a} - {b} = {calc.subtract(a, b)}")
print(f"{a} * {b} = {calc.multiply(a, b)}")
print(f"{a} / {b} = {calc.divide(a, b):.4f}")
print(f"{a} ^ {b} = {calc.power(a, b)}")

# Using random module
print(f"\n--- Random Module ---")
print(f"Random number (1-100): {random.randint(1, 100)}")
print(f"Random choice: {random.choice(['Python', 'Java', 'C++'])}")

# Using datetime module
print(f"\n--- DateTime Module ---")
now = datetime.now()
print(f"Now: {now.strftime('%d %B %Y, %I:%M %p')}")

print("\nProgram completed!")
```

### Part 3 — Explore Standard Library (7 min)

```python
# Explore 3 standard library modules
import math
import string
import os

print(f"Pi = {math.pi}")
print(f"e = {math.e}")
print(f"sqrt(256) = {math.sqrt(256)}")
print(f"\nAlphabet: {string.ascii_lowercase}")
print(f"Current dir: {os.getcwd()}")
print(f"Files here: {os.listdir('.')[:5]}")
```

Run and verify. Save.

---

## Session 9 — Key Takeaways

1. **Modules** are `.py` files that contain reusable functions, classes, and variables
2. **Import styles:** `import module`, `from module import func`, `import module as alias`
3. **Standard library** includes `math`, `random`, `datetime`, `os`, `sys`, `json`, `csv`
4. **`if __name__ == "__main__":`** separates test/demo code from importable code
5. **Packages** are directories with `__init__.py` — organize related modules together
6. **pip** installs third-party packages: `pip install package_name`

---

## Preparation for Session 10
- Review all Module 2 concepts: conditionals, loops, functions, modules
- Think about: How would you build a movie ticket booking system?
- Be ready to code: Session 10 is the Module 2 project — Online Ticket Booking System

---

*Session 9 of 30 | Module 2: Control Flow & Functions*
*Professional Python Programming Certification — UpSkill Global Education Technologies Inc., Canada*
