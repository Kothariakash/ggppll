# Session 3 — Operators in Python
## Module 1: Python Fundamentals | Professional Python Programming Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Build a Calculator Using All Operator Types

---

## Learning Objectives
By the end of this session, you will be able to:
1. Use all arithmetic operators for mathematical calculations
2. Apply comparison and logical operators for decision-making
3. Understand assignment operators and shorthand notations
4. Work with identity and membership operators
5. Apply operator precedence rules correctly

---

## 3.1 Categories of Python Operators

| Category | Operators | Purpose |
|----------|----------|---------|
| **Arithmetic** | `+  -  *  /  //  %  **` | Mathematical calculations |
| **Comparison** | `==  !=  >  <  >=  <=` | Compare values → True/False |
| **Logical** | `and  or  not` | Combine boolean conditions |
| **Assignment** | `=  +=  -=  *=  /=  //=  %=  **=` | Assign and update values |
| **Identity** | `is  is not` | Check if same object in memory |
| **Membership** | `in  not in` | Check if value exists in a sequence |
| **Bitwise** | `&  |  ^  ~  <<  >>` | Bit-level operations (advanced) |

---

## 3.2 Arithmetic Operators

### All Arithmetic Operators

| Operator | Name | Example | Result |
|----------|------|---------|--------|
| `+` | Addition | `10 + 3` | `13` |
| `-` | Subtraction | `10 - 3` | `7` |
| `*` | Multiplication | `10 * 3` | `30` |
| `/` | Division | `10 / 3` | `3.3333...` |
| `//` | Floor Division | `10 // 3` | `3` |
| `%` | Modulus (Remainder) | `10 % 3` | `1` |
| `**` | Exponentiation | `10 ** 3` | `1000` |

### Division Types — Critical Difference

```python
# True Division (/) — always returns float
print(10 / 3)    # 3.3333333333333335
print(10 / 2)    # 5.0 (float even when divisible!)

# Floor Division (//) — rounds DOWN to nearest integer
print(10 // 3)   # 3
print(-10 // 3)  # -4 (rounds DOWN, not toward zero)
print(10.0 // 3) # 3.0 (float input → float output)

# Modulus (%) — remainder after division
print(10 % 3)    # 1  (10 = 3*3 + 1)
print(15 % 5)    # 0  (perfectly divisible)
print(7 % 2)     # 1  (odd number check!)
```

### Practical Uses

```python
# Check if a number is even or odd
number = 42
if number % 2 == 0:
    print(f"{number} is EVEN")
else:
    print(f"{number} is ODD")

# Extract digits
num = 1234
last_digit = num % 10       # 4
remaining = num // 10       # 123

# Convert seconds to hours:minutes:seconds
total_seconds = 3725
hours = total_seconds // 3600         # 1
minutes = (total_seconds % 3600) // 60  # 2
seconds = total_seconds % 60           # 5
print(f"{hours}h {minutes}m {seconds}s")  # 1h 2m 5s
```

### Arithmetic with Different Types

```python
# int + int → int
print(5 + 3)        # 8 (int)

# int + float → float (automatic promotion)
print(5 + 3.0)      # 8.0 (float)

# int * float → float
print(5 * 2.5)      # 12.5 (float)

# String + String → Concatenation
print("Hello" + " " + "World")  # Hello World

# String * int → Repetition
print("Ha" * 3)     # HaHaHa
```

---

## 3.3 Comparison Operators

### All Comparison Operators

| Operator | Name | Example | Result |
|----------|------|---------|--------|
| `==` | Equal to | `5 == 5` | `True` |
| `!=` | Not equal to | `5 != 3` | `True` |
| `>` | Greater than | `5 > 3` | `True` |
| `<` | Less than | `5 < 3` | `False` |
| `>=` | Greater than or equal | `5 >= 5` | `True` |
| `<=` | Less than or equal | `3 <= 5` | `True` |

### Comparison Always Returns Boolean

```python
print(10 == 10)    # True
print(10 != 10)    # False
print(10 > 5)      # True
print(10 < 5)      # False
print(10 >= 10)    # True
print(10 <= 9)     # False

# Store comparison result in a variable
is_adult = age >= 18
print(is_adult)    # True or False
```

### Chained Comparisons (Python Special!)

```python
# Instead of: x > 5 and x < 10
x = 7
print(5 < x < 10)    # True — chained comparison!
print(1 < 2 < 3 < 4) # True
print(1 < 2 > 3)     # False (2 > 3 is False)
```

### Comparing Strings

```python
# Strings are compared lexicographically (dictionary order)
print("apple" < "banana")   # True  (a < b)
print("Apple" < "apple")    # True  (uppercase < lowercase in ASCII)
print("abc" == "abc")       # True
print("abc" == "ABC")       # False (case-sensitive)
```

---

## 3.4 Logical Operators

### All Logical Operators

| Operator | Meaning | Example | Result |
|----------|---------|---------|--------|
| `and` | Both must be True | `True and False` | `False` |
| `or` | At least one True | `True or False` | `True` |
| `not` | Inverts the value | `not True` | `False` |

### Truth Tables

**AND:**
| A | B | A and B |
|---|---|---------|
| True | True | **True** |
| True | False | False |
| False | True | False |
| False | False | False |

**OR:**
| A | B | A or B |
|---|---|--------|
| True | True | True |
| True | False | True |
| False | True | True |
| False | False | **False** |

**NOT:**
| A | not A |
|---|-------|
| True | False |
| False | True |

### Practical Examples

```python
age = 25
income = 50000

# AND — both conditions must be true
is_eligible = age >= 18 and income >= 30000
print(f"Loan eligible: {is_eligible}")  # True

# OR — at least one condition must be true
has_discount = age < 12 or age >= 60
print(f"Age discount: {has_discount}")  # False

# NOT — invert the condition
is_minor = not (age >= 18)
print(f"Is minor: {is_minor}")  # False

# Combined
can_vote = age >= 18 and not is_minor
print(f"Can vote: {can_vote}")  # True
```

### Short-Circuit Evaluation

Python stops evaluating as soon as the result is determined:

```python
# AND: If first is False, skip second (result is already False)
print(False and print("This won't print"))  # False — second operand never evaluated

# OR: If first is True, skip second (result is already True)
print(True or print("This won't print"))   # True — second operand never evaluated
```

### Logical Operators with Non-Boolean Values

```python
# 'and' returns the first falsy value, or the last value if all truthy
print(0 and 5)        # 0  (0 is falsy → returns 0)
print(3 and 5)        # 5  (3 is truthy → check 5, also truthy → returns 5)
print("" and "Hello") # "" (empty string is falsy)

# 'or' returns the first truthy value, or the last value if all falsy
print(0 or 5)         # 5  (0 is falsy → check 5, truthy → returns 5)
print(3 or 5)         # 3  (3 is truthy → returns 3 immediately)
print("" or "Hello")  # "Hello"
print(0 or "" or None) # None (all falsy → returns last)

# Common pattern: default values
name = "" or "Unknown"
print(name)  # "Unknown"
```

---

## 3.5 Assignment Operators

### Simple Assignment

```python
x = 10   # Assign 10 to x
```

### Compound Assignment (Shorthand)

| Operator | Equivalent | Example |
|----------|-----------|---------|
| `x += 5` | `x = x + 5` | Add and assign |
| `x -= 3` | `x = x - 3` | Subtract and assign |
| `x *= 2` | `x = x * 2` | Multiply and assign |
| `x /= 4` | `x = x / 4` | Divide and assign |
| `x //= 3` | `x = x // 3` | Floor divide and assign |
| `x %= 2` | `x = x % 2` | Modulus and assign |
| `x **= 3` | `x = x ** 3` | Power and assign |

```python
total = 100
total += 50    # 150
total -= 20    # 130
total *= 2     # 260
total //= 3    # 86
print(total)   # 86

# Works with strings too!
message = "Hello"
message += " World"
print(message)  # Hello World
```

> **Note:** Python does NOT have `++` or `--` operators. Use `x += 1` and `x -= 1`.

---

## 3.6 Identity Operators

### `is` and `is not`

| Operator | Meaning | Checks |
|----------|---------|--------|
| `is` | Same object | Memory identity (same `id()`) |
| `is not` | Different object | Different memory identity |

### `==` vs `is` — Critical Difference

```python
a = [1, 2, 3]
b = [1, 2, 3]
c = a

# == checks VALUE equality
print(a == b)    # True  (same values)
print(a == c)    # True  (same values)

# 'is' checks IDENTITY (same object in memory)
print(a is b)    # False (different objects, same values)
print(a is c)    # True  (c points to the same object as a)

# Verify with id()
print(id(a))     # e.g., 140234567890
print(id(b))     # e.g., 140234567920 (different!)
print(id(c))     # e.g., 140234567890 (same as a!)
```

### When to Use `is`

```python
# Use 'is' only for: None, True, False
x = None
print(x is None)      # True ✅
print(x == None)      # True, but not recommended ❌

# Integer caching (-5 to 256) — implementation detail
a = 256
b = 256
print(a is b)   # True (Python caches small integers)

a = 257
b = 257
print(a is b)   # False or True (depends on implementation — don't rely on this!)
```

> **Rule:** Use `==` for value comparison. Use `is` only for `None` checks.

---

## 3.7 Membership Operators

### `in` and `not in`

| Operator | Meaning | Example |
|----------|---------|---------|
| `in` | Value is present | `"a" in "apple"` → `True` |
| `not in` | Value is absent | `5 not in [1,2,3]` → `True` |

```python
# In a string
print("P" in "Python")       # True
print("x" in "Python")       # False
print("thon" in "Python")    # True

# In a list
fruits = ["apple", "banana", "cherry"]
print("banana" in fruits)    # True
print("grape" in fruits)     # False
print("grape" not in fruits) # True

# In a tuple
colors = ("red", "green", "blue")
print("red" in colors)       # True

# In a dictionary (checks KEYS, not values)
student = {"name": "Alice", "age": 25}
print("name" in student)     # True (key exists)
print("Alice" in student)    # False (values not checked by default)
print("Alice" in student.values())  # True (explicitly check values)

# In a range
print(5 in range(10))        # True
print(15 in range(10))       # False
```

---

## 3.8 Operator Precedence

### Precedence Table (High to Low)

| Priority | Operator | Description |
|----------|----------|-------------|
| 1 (Highest) | `()` | Parentheses |
| 2 | `**` | Exponentiation |
| 3 | `+x, -x, ~x` | Unary plus, minus, NOT |
| 4 | `*, /, //, %` | Multiplication, Division |
| 5 | `+, -` | Addition, Subtraction |
| 6 | `<<, >>` | Bitwise shifts |
| 7 | `&` | Bitwise AND |
| 8 | `^` | Bitwise XOR |
| 9 | `\|` | Bitwise OR |
| 10 | `==, !=, >, <, >=, <=, is, in` | Comparisons |
| 11 | `not` | Logical NOT |
| 12 | `and` | Logical AND |
| 13 (Lowest) | `or` | Logical OR |

### Examples

```python
# Multiplication before Addition
print(2 + 3 * 4)       # 14  (not 20)
print((2 + 3) * 4)     # 20  (parentheses override)

# Exponentiation before Multiplication
print(2 * 3 ** 2)      # 18  (3**2=9, then 2*9=18)

# Comparison before Logical
print(5 > 3 and 2 < 4) # True  (5>3 → True, 2<4 → True, True and True → True)

# NOT before AND before OR
print(True or False and False)   # True  (and first: False and False = False, then True or False = True)
print((True or False) and False) # False (parentheses: True or False = True, then True and False = False)
```

> **Best Practice:** When in doubt, use **parentheses** `()` to make precedence explicit. Code clarity > cleverness.

---

## 3.9 Walrus Operator `:=` (Python 3.8+)

### Assignment Expression

The walrus operator `:=` assigns a value to a variable as part of an expression.

```python
# Without walrus operator
n = len("Hello")
if n > 3:
    print(f"Length {n} is greater than 3")

# With walrus operator — assign and test in one line
if (n := len("Hello")) > 3:
    print(f"Length {n} is greater than 3")
```

### Useful in Loops

```python
# Read input until user types 'quit'
while (command := input("Enter command: ")) != "quit":
    print(f"You entered: {command}")
print("Goodbye!")
```

> Use sparingly — readability is more important than brevity.

---

## 🔧 Hands-On Activity: Build a Calculator

**Duration:** 25 minutes

### Tasks

Create a file `session03_calculator.py`:

**Part 1 — Arithmetic Calculator (10 min)**

```python
# Part 1: Arithmetic Calculator
print("=" * 40)
print("  Python Arithmetic Calculator")
print("=" * 40)

num1 = 25
num2 = 7

print(f"\nNumbers: {num1} and {num2}")
print(f"Addition:       {num1} + {num2} = {num1 + num2}")
print(f"Subtraction:    {num1} - {num2} = {num1 - num2}")
print(f"Multiplication: {num1} * {num2} = {num1 * num2}")
print(f"Division:       {num1} / {num2} = {num1 / num2:.4f}")
print(f"Floor Division: {num1} // {num2} = {num1 // num2}")
print(f"Modulus:        {num1} % {num2} = {num1 % num2}")
print(f"Power:          {num1} ** {num2} = {num1 ** num2}")
```

**Part 2 — Comparison & Logical (8 min)**

```python
# Part 2: Comparison & Logical
print("\n" + "=" * 40)
print("  Comparison & Logical Operators")
print("=" * 40)

age = 20
salary = 45000
experience = 3

print(f"\nAge: {age}, Salary: {salary}, Experience: {experience}")
print(f"Is adult (age >= 18): {age >= 18}")
print(f"Senior employee (exp > 5): {experience > 5}")
print(f"Eligible for loan (age >= 18 AND salary >= 30000): {age >= 18 and salary >= 30000}")
print(f"Eligible for discount (age < 12 OR age >= 60): {age < 12 or age >= 60}")
print(f"Is NOT minor: {not (age < 18)}")

# Chained comparison
score = 75
grade = "Pass" if 40 <= score <= 100 else "Fail"
print(f"\nScore: {score}, Result: {grade}")
```

**Part 3 — Membership & Identity (7 min)**

```python
# Part 3: Membership & Identity
print("\n" + "=" * 40)
print("  Membership & Identity Operators")
print("=" * 40)

languages = ["Python", "Java", "JavaScript", "C++"]
print(f"\nLanguages: {languages}")
print(f"'Python' in list: {'Python' in languages}")
print(f"'Ruby' in list: {'Ruby' in languages}")
print(f"'Go' not in list: {'Go' not in languages}")

# Identity check
a = [1, 2, 3]
b = [1, 2, 3]
c = a
print(f"\na == b: {a == b}")     # True (same values)
print(f"a is b: {a is b}")       # False (different objects)
print(f"a is c: {a is c}")       # True (same object)

# None check
result = None
print(f"\nresult is None: {result is None}")

print("\nProgram completed!")
```

Run and verify all output. Save.

---

## Session 3 — Key Takeaways

1. **Arithmetic:** `//` floor divides, `%` gives remainder, `**` is power — `/` always returns float
2. **Comparison:** `==` checks value, always returns `True` or `False` — supports chaining (`5 < x < 10`)
3. **Logical:** `and` (both True), `or` (at least one True), `not` (invert) — supports short-circuit
4. **Identity:** `is` checks same object (use only for `None`); `==` checks same value
5. **Membership:** `in` and `not in` check presence in sequences, strings, dicts
6. **Precedence:** When in doubt, use parentheses `()` for clarity

---

## Preparation for Session 4
- Practice: Create a temperature converter (Celsius to Fahrenheit) using arithmetic operators
- Think about: How do you get input from a user in Python?
- Review: What does `input()` function do?

---

*Session 3 of 30 | Module 1: Python Fundamentals*
*Professional Python Programming Certification — UpSkill Global Education Technologies Inc., Canada*
