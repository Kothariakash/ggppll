# Session 4 — Input & Output
## Module 1: Python Fundamentals | Professional Python Programming Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Build an Interactive User Profile Generator

---

## Learning Objectives
By the end of this session, you will be able to:
1. Accept user input using the `input()` function
2. Convert input to appropriate data types safely
3. Format output using f-strings, `.format()`, and `%` formatting
4. Control print output with `sep`, `end`, and escape characters
5. Build interactive console programs

---

## 4.1 The input() Function

### Basic Input

```python
# input() always returns a STRING
name = input("Enter your name: ")
print(f"Hello, {name}!")
print(type(name))  # <class 'str'>
```

### How input() Works

```
1. Displays the prompt message (optional)
2. Pauses program execution
3. Waits for user to type and press Enter
4. Returns the typed text as a STRING
5. Program continues
```

### Input is Always a String

```python
age = input("Enter your age: ")    # User types: 25
print(type(age))                   # <class 'str'> — NOT int!
print(age + 5)                     # TypeError! Can't add str + int

# Must convert to int
age = int(input("Enter your age: "))
print(type(age))                   # <class 'int'>
print(age + 5)                     # 30 ✅
```

---

## 4.2 Type Conversion with Input

### Converting Input Types

```python
# Integer input
age = int(input("Enter your age: "))

# Float input
price = float(input("Enter the price: "))

# Boolean-like input
response = input("Are you a student? (yes/no): ")
is_student = response.lower() == "yes"

# Multiple values on one line
x, y = input("Enter two numbers (space-separated): ").split()
x, y = int(x), int(y)
print(f"Sum: {x + y}")
```

### Safe Input Conversion

```python
# Problem: User might enter invalid data
# int("hello") → ValueError!

# Solution 1: Check with isdigit()
age_str = input("Enter your age: ")
if age_str.isdigit():
    age = int(age_str)
    print(f"You are {age} years old")
else:
    print("Invalid input! Please enter a number.")

# Solution 2: try/except (covered in Session 18)
try:
    age = int(input("Enter your age: "))
    print(f"You are {age} years old")
except ValueError:
    print("Invalid input! Please enter a number.")
```

### Multiple Inputs

```python
# Method 1: Separate input() calls
first = input("First name: ")
last = input("Last name: ")

# Method 2: Split a single line
# User types: Alice 25 5.6
name, age, height = input("Enter name, age, height: ").split()
age = int(age)
height = float(height)

# Method 3: Using map() for numeric conversion
# User types: 10 20 30
a, b, c = map(int, input("Enter 3 numbers: ").split())
print(f"Sum: {a + b + c}")
```

### Handling Multiple Data Types in One Line

```python
# User types: Priya 28 75000.50
data = input("Enter name age salary: ").split()
name = data[0]
age = int(data[1])
salary = float(data[2])
print(f"{name}, Age: {age}, Salary: ${salary:,.2f}")
```

---

## 4.3 The print() Function — Deep Dive

### print() Syntax

```python
print(*objects, sep=' ', end='\n', file=sys.stdout, flush=False)
```

| Parameter | Default | Purpose |
|-----------|---------|---------|
| `*objects` | — | Values to print (comma-separated) |
| `sep` | `' '` (space) | Separator between objects |
| `end` | `'\n'` (newline) | What to print at the end |
| `file` | `sys.stdout` | Output destination |
| `flush` | `False` | Force flush the output buffer |

### Multiple Values

```python
print("Name:", "Alice", "Age:", 25)
# Output: Name: Alice Age: 25
```

### Custom Separator (sep)

```python
print("2024", "01", "15", sep="-")
# Output: 2024-01-15

print("Apple", "Banana", "Cherry", sep=", ")
# Output: Apple, Banana, Cherry

print("192", "168", "1", "1", sep=".")
# Output: 192.168.1.1

print("A", "B", "C", sep=" | ")
# Output: A | B | C

print("Hello", "World", sep="\n")
# Output:
# Hello
# World
```

### Custom End Character (end)

```python
# Default: each print adds a newline
print("Hello")
print("World")
# Output:
# Hello
# World

# Custom end — keep on same line
print("Hello", end=" ")
print("World")
# Output: Hello World

# Custom end — add custom suffix
print("Loading", end="...")
print("Done!")
# Output: Loading...Done!

# Useful for progress indicators
for i in range(5):
    print(i, end=" ")
# Output: 0 1 2 3 4
```

---

## 4.4 String Formatting Methods

### Method 1: f-Strings (Recommended — Python 3.6+)

```python
name = "Alice"
age = 25
salary = 75000.5678

# Basic embedding
print(f"Name: {name}, Age: {age}")

# Expressions inside braces
print(f"Next year: {age + 1}")
print(f"Name uppercase: {name.upper()}")

# Number formatting
print(f"Salary: ${salary:,.2f}")       # $75,000.57
print(f"Percentage: {0.856:.1%}")      # 85.6%
print(f"Integer with padding: {42:05d}")  # 00042
print(f"Scientific: {1234567.89:.2e}") # 1.23e+06
```

### f-String Formatting Codes

| Code | Meaning | Example | Output |
|------|---------|---------|--------|
| `:.2f` | 2 decimal places | `f"{3.14159:.2f}"` | `3.14` |
| `:,.2f` | Comma separator + 2 decimals | `f"{75000.5:.2f}"` | `75,000.50` |
| `:.1%` | Percentage with 1 decimal | `f"{0.856:.1%}"` | `85.6%` |
| `:05d` | Zero-padded integer (5 wide) | `f"{42:05d}"` | `00042` |
| `:>20` | Right-align in 20 chars | `f"{'Hi':>20}"` | `                  Hi` |
| `:<20` | Left-align in 20 chars | `f"{'Hi':<20}"` | `Hi                  ` |
| `:^20` | Center in 20 chars | `f"{'Hi':^20}"` | `         Hi         ` |
| `:>20.2f` | Right-align, 2 decimals | `f"{3.14:>20.2f}"` | `                3.14` |
| `:.2e` | Scientific notation | `f"{12345.67:.2e}"` | `1.23e+04` |
| `:b` | Binary | `f"{10:b}"` | `1010` |
| `:o` | Octal | `f"{10:o}"` | `12` |
| `:x` | Hexadecimal | `f"{255:x}"` | `ff` |

### Method 2: .format() Method

```python
# Positional arguments
print("Name: {}, Age: {}".format("Alice", 25))

# Indexed arguments
print("{0} is {1} years old. {0} lives in Delhi.".format("Alice", 25))

# Named arguments
print("Name: {name}, Age: {age}".format(name="Alice", age=25))

# Formatting
print("Price: {:.2f}".format(99.5))       # 99.50
print("Padded: {:>10}".format("Hello"))    #      Hello
```

### Method 3: % Formatting (Old Style)

```python
# %s = string, %d = integer, %f = float
name = "Alice"
age = 25
salary = 75000.50

print("Name: %s, Age: %d" % (name, age))
print("Salary: $%.2f" % salary)
print("Padded: %10s" % name)          #      Alice
print("Zero-padded: %05d" % age)      # 00025
```

### Comparison of Methods

| Feature | f-string | .format() | % operator |
|---------|----------|-----------|-----------|
| **Readability** | Best | Good | Poor |
| **Performance** | Fastest | Medium | Slowest |
| **Python version** | 3.6+ | 2.6+ | All versions |
| **Expressions** | Yes `{x+1}` | No | No |
| **Recommendation** | ✅ Use this | OK for compatibility | Avoid |

---

## 4.5 Escape Characters & Raw Strings

### Escape Characters

| Escape | Output | Example |
|--------|--------|---------|
| `\n` | Newline | `"Line1\nLine2"` |
| `\t` | Tab | `"Col1\tCol2"` |
| `\\` | Backslash | `"C:\\Users"` |
| `\'` | Single quote | `'It\'s Python'` |
| `\"` | Double quote | `"She said \"Hi\""` |
| `\0` | Null character | — |
| `\a` | Bell/alert | — |
| `\b` | Backspace | — |

```python
# Newlines
print("Line 1\nLine 2\nLine 3")

# Tabs for alignment
print("Name\tAge\tCity")
print("Alice\t25\tDelhi")
print("Bob\t30\tMumbai")

# File paths
print("C:\\Users\\Documents\\file.txt")
# Or use raw string:
print(r"C:\Users\Documents\file.txt")
```

### Multi-line Strings

```python
# Triple quotes preserve newlines
message = """
Dear Student,

Welcome to Python Programming.
We hope you enjoy the course.

Best regards,
Instructor
"""
print(message)
```

---

## 4.6 Printing Tables and Formatted Output

### Simple Table with Tabs

```python
print("Product\t\tPrice\tQty")
print("-" * 35)
print("Laptop\t\t₹75000\t5")
print("Mouse\t\t₹500\t20")
print("Keyboard\t₹1200\t15")
```

### Aligned Table with f-strings

```python
# Fixed-width columns using f-string alignment
products = [
    ("Laptop", 75000, 5),
    ("Mouse", 500, 20),
    ("Keyboard", 1200, 15),
    ("Monitor", 25000, 8),
]

print(f"{'Product':<15} {'Price':>10} {'Qty':>5}")
print("-" * 32)
for name, price, qty in products:
    print(f"{name:<15} {price:>10,.2f} {qty:>5}")
```

**Output:**
```
Product              Price   Qty
--------------------------------
Laptop           75,000.00     5
Mouse               500.00    20
Keyboard          1,200.00    15
Monitor          25,000.00     8
```

### Box Drawing

```python
def print_box(title, content):
    width = max(len(title), max(len(line) for line in content)) + 4
    print("┌" + "─" * width + "┐")
    print(f"│ {title:^{width-2}} │")
    print("├" + "─" * width + "┤")
    for line in content:
        print(f"│ {line:<{width-2}} │")
    print("└" + "─" * width + "┘")

print_box("Student Info", ["Name: Alice", "Age: 25", "Grade: A"])
```

---

## 4.7 Printing to Files

### Writing Output to a File

```python
# Print to a file instead of console
with open("output.txt", "w") as f:
    print("Hello, File!", file=f)
    print("Line 2", file=f)
    print(f"Today's date: 2024-01-15", file=f)
```

> File handling is covered in depth in Session 16. This is a preview of `print(file=...)`.

---

## 4.8 Common Input/Output Patterns

### Pattern 1: Menu-Driven Input

```python
print("\n=== Menu ===")
print("1. Add")
print("2. Subtract")
print("3. Multiply")
print("4. Exit")
choice = input("Enter your choice (1-4): ")
```

### Pattern 2: Yes/No Confirmation

```python
confirm = input("Are you sure? (y/n): ").strip().lower()
if confirm in ("y", "yes"):
    print("Confirmed!")
else:
    print("Cancelled.")
```

### Pattern 3: Input with Default Value

```python
name = input("Enter name (default: Guest): ").strip()
name = name if name else "Guest"
print(f"Welcome, {name}!")
```

### Pattern 4: Repeated Input Until Valid

```python
while True:
    age_str = input("Enter your age: ").strip()
    if age_str.isdigit() and 0 < int(age_str) < 150:
        age = int(age_str)
        break
    print("Invalid! Please enter a valid age (1-149).")
print(f"Your age is {age}")
```

### Pattern 5: Password Input (Hidden)

```python
import getpass
password = getpass.getpass("Enter password: ")
# Input is hidden — user types but nothing appears on screen
```

---

## 4.9 String Methods for Input Processing

### Cleaning User Input

```python
raw = "  Hello, World!  "

print(raw.strip())      # "Hello, World!" — remove leading/trailing whitespace
print(raw.lstrip())     # "Hello, World!  " — remove left whitespace
print(raw.rstrip())     # "  Hello, World!" — remove right whitespace
print(raw.lower())      # "  hello, world!  "
print(raw.upper())      # "  HELLO, WORLD!  "
print(raw.title())      # "  Hello, World!  "
print(raw.replace("World", "Python"))  # "  Hello, Python!  "
```

### Validation Methods

| Method | Returns True if | Example |
|--------|----------------|---------|
| `.isdigit()` | All digits | `"123".isdigit()` → True |
| `.isalpha()` | All letters | `"Hello".isalpha()` → True |
| `.isalnum()` | Letters + digits | `"Hello123".isalnum()` → True |
| `.isspace()` | All whitespace | `"   ".isspace()` → True |
| `.isupper()` | All uppercase | `"HELLO".isupper()` → True |
| `.islower()` | All lowercase | `"hello".islower()` → True |
| `.startswith(s)` | Starts with s | `"Hello".startswith("He")` → True |
| `.endswith(s)` | Ends with s | `"file.py".endswith(".py")` → True |

```python
# Validate email (basic)
email = input("Enter email: ").strip()
if "@" in email and "." in email:
    print("Valid email format")
else:
    print("Invalid email format")

# Validate phone number
phone = input("Enter phone (10 digits): ").strip()
if phone.isdigit() and len(phone) == 10:
    print("Valid phone number")
else:
    print("Invalid phone number")
```

---

## 🔧 Hands-On Activity: Interactive User Profile Generator

**Duration:** 25 minutes

### Tasks

Create a file `session04_profile.py`:

```python
# Session 4 — Interactive User Profile Generator

print("=" * 50)
print("     USER PROFILE GENERATOR")
print("=" * 50)

# Collect user information
first_name = input("\nFirst Name: ").strip().title()
last_name = input("Last Name: ").strip().title()
age = int(input("Age: "))
email = input("Email: ").strip().lower()
city = input("City: ").strip().title()
salary = float(input("Monthly Salary (₹): "))

# Calculate derived values
full_name = f"{first_name} {last_name}"
annual_salary = salary * 12
tax = annual_salary * 0.10 if annual_salary <= 500000 else annual_salary * 0.20
net_annual = annual_salary - tax
is_adult = age >= 18
retirement_years = max(0, 60 - age)

# Display formatted profile
print("\n" + "=" * 50)
print("     YOUR PROFILE")
print("=" * 50)

print(f"\n{'Full Name':<20}: {full_name}")
print(f"{'Age':<20}: {age} years")
print(f"{'Email':<20}: {email}")
print(f"{'City':<20}: {city}")
print(f"{'Adult':<20}: {'Yes' if is_adult else 'No'}")

print(f"\n{'--- Financial Summary ---':^50}")
print(f"{'Monthly Salary':<20}: ₹{salary:>12,.2f}")
print(f"{'Annual Salary':<20}: ₹{annual_salary:>12,.2f}")
print(f"{'Tax (estimated)':<20}: ₹{tax:>12,.2f}")
print(f"{'Net Annual Income':<20}: ₹{net_annual:>12,.2f}")

print(f"\n{'--- Career Info ---':^50}")
print(f"{'Years to Retirement':<20}: {retirement_years} years")
print(f"{'Retirement Year':<20}: {2024 + retirement_years}")

# Summary table
print(f"\n{'=' * 50}")
print(f"{'METRIC':<25} {'VALUE':>20}")
print(f"{'-' * 50}")
print(f"{'Monthly Income':<25} {'₹' + f'{salary:,.2f}':>20}")
print(f"{'Annual Income':<25} {'₹' + f'{annual_salary:,.2f}':>20}")
print(f"{'Tax Rate':<25} {'10%' if annual_salary <= 500000 else '20%':>20}")
print(f"{'Take-Home (Annual)':<25} {'₹' + f'{net_annual:,.2f}':>20}")
print(f"{'=' * 50}")

print("\nProfile generated successfully!")
```

### Bonus Challenge

Add input validation:
- Age must be between 1 and 120
- Email must contain `@` and `.`
- Salary must be positive
- Display an error message and re-prompt if validation fails

---

## Session 4 — Key Takeaways

1. **`input()`** always returns a string — convert with `int()`, `float()` as needed
2. **f-strings** (`f"..."`) are the best way to format output — support expressions, alignment, and number formatting
3. **`sep`** and **`end`** parameters of `print()` control output formatting
4. Always **`.strip()`** user input to remove accidental whitespace
5. **Validate input** before converting — use `.isdigit()`, `try/except`, or loops
6. Use **alignment specifiers** (`<`, `>`, `^`) for professional table output

---

## Preparation for Session 5
- Review all Session 1–4 concepts: variables, types, operators, input/output
- Think about: How would you build a student grade tracking program?
- Be ready to code: Session 5 is the Module 1 project — Student Grade Management System

---

*Session 4 of 30 | Module 1: Python Fundamentals*
*Professional Python Programming Certification — UpSkill Global Education Technologies Inc., Canada*
