# Session 18 — Exception Handling in Python
## Module 4: File Handling & Exception Handling | Professional Python Programming Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Build Robust Error-Proof Programs

---

## Learning Objectives
By the end of this session, you will be able to:
1. Understand what exceptions are and why they occur
2. Use try-except-else-finally for error handling
3. Handle specific exception types appropriately
4. Raise custom exceptions
5. Write robust programs that don't crash on bad input

---

## 18.1 What is an Exception?

An **exception** is an error that occurs during program execution. Without handling, exceptions **crash the program**.

```python
# This will crash!
print(10 / 0)          # ZeroDivisionError
print(int("hello"))    # ValueError
print(my_var)          # NameError
```

### Errors vs Exceptions

| Type | When | Example |
|------|------|---------|
| **Syntax Error** | Before execution (parsing) | `if True print("hi")` — missing colon |
| **Exception** | During execution (runtime) | `10 / 0` — division by zero |

> Syntax errors must be fixed in code. Exceptions can be **caught and handled** at runtime.

---

## 18.2 Common Exception Types

| Exception | Cause | Example |
|-----------|-------|---------|
| `ZeroDivisionError` | Division by zero | `10 / 0` |
| `ValueError` | Invalid value conversion | `int("hello")` |
| `TypeError` | Wrong type in operation | `"hi" + 5` |
| `NameError` | Variable not defined | `print(undefined_var)` |
| `IndexError` | List index out of range | `[1,2,3][10]` |
| `KeyError` | Dict key not found | `{"a":1}["b"]` |
| `FileNotFoundError` | File doesn't exist | `open("nofile.txt")` |
| `AttributeError` | Object has no attribute | `"hi".append("x")` |
| `ImportError` | Module not found | `import nonexistent` |
| `IOError` | I/O operation failed | File read/write failure |
| `PermissionError` | No permission | Writing to read-only file |
| `StopIteration` | Iterator exhausted | `next()` on empty iterator |
| `OverflowError` | Number too large | `math.exp(1000)` |
| `RecursionError` | Max recursion depth exceeded | Infinite recursion |

### Exception Hierarchy (Simplified)

```
BaseException
 └── Exception
      ├── ArithmeticError
      │    ├── ZeroDivisionError
      │    └── OverflowError
      ├── LookupError
      │    ├── IndexError
      │    └── KeyError
      ├── ValueError
      ├── TypeError
      ├── FileNotFoundError
      ├── PermissionError
      ├── AttributeError
      ├── NameError
      └── RuntimeError
           └── RecursionError
```

---

## 18.3 try-except — Basic Error Handling

### Syntax

```python
try:
    # Code that might raise an exception
    risky_code()
except ExceptionType:
    # Code that runs if the exception occurs
    handle_error()
```

### Basic Example

```python
try:
    num = int(input("Enter a number: "))
    result = 100 / num
    print(f"Result: {result}")
except ZeroDivisionError:
    print("Error: Cannot divide by zero!")
except ValueError:
    print("Error: Please enter a valid number!")
```

### Catch Multiple Exceptions

```python
# Method 1: Separate except blocks
try:
    value = int(input("Enter: "))
    result = 10 / value
except ValueError:
    print("Not a valid number!")
except ZeroDivisionError:
    print("Cannot divide by zero!")

# Method 2: Tuple of exceptions
try:
    value = int(input("Enter: "))
    result = 10 / value
except (ValueError, ZeroDivisionError) as e:
    print(f"Error: {e}")
```

### Catch All Exceptions (Use Carefully)

```python
try:
    risky_operation()
except Exception as e:
    print(f"Something went wrong: {e}")
    print(f"Error type: {type(e).__name__}")
```

> **Warning:** Catching all exceptions with bare `except:` or `except Exception:` can hide bugs. Always prefer specific exception types.

---

## 18.4 try-except-else-finally

### Full Syntax

```python
try:
    # Code that might fail
    risky_code()
except ExceptionType as e:
    # Runs ONLY if exception occurs
    handle_error(e)
else:
    # Runs ONLY if NO exception occurred
    success_code()
finally:
    # ALWAYS runs — exception or not
    cleanup_code()
```

### When Each Block Runs

| Scenario | try | except | else | finally |
|----------|-----|--------|------|---------|
| No exception | ✅ | ❌ | ✅ | ✅ |
| Exception caught | ✅ (until error) | ✅ | ❌ | ✅ |
| Exception NOT caught | ✅ (until error) | ❌ | ❌ | ✅ (then crash) |

### Example

```python
try:
    filename = input("Enter filename: ")
    f = open(filename, "r")
except FileNotFoundError:
    print(f"File '{filename}' not found!")
else:
    content = f.read()
    print(f"File has {len(content)} characters")
    f.close()
finally:
    print("Operation complete.")
```

### finally Use Cases

```python
# Guaranteed cleanup
connection = None
try:
    connection = create_database_connection()
    data = connection.query("SELECT * FROM users")
except DatabaseError as e:
    print(f"Database error: {e}")
finally:
    if connection:
        connection.close()  # Always close, even if error
        print("Connection closed.")
```

---

## 18.5 The `as` Keyword — Accessing Error Details

```python
try:
    result = 10 / 0
except ZeroDivisionError as e:
    print(f"Error message: {e}")           # division by zero
    print(f"Error type: {type(e).__name__}")  # ZeroDivisionError
    print(f"Error args: {e.args}")          # ('division by zero',)
```

---

## 18.6 Raising Exceptions

### raise — Manually Trigger an Exception

```python
def set_age(age):
    if not isinstance(age, int):
        raise TypeError("Age must be an integer")
    if age < 0:
        raise ValueError("Age cannot be negative")
    if age > 150:
        raise ValueError("Age cannot exceed 150")
    return age

try:
    set_age(-5)
except ValueError as e:
    print(f"Invalid age: {e}")
```

### Re-raising Exceptions

```python
try:
    result = dangerous_operation()
except ValueError as e:
    print(f"Logging error: {e}")
    raise  # Re-raise the same exception after logging
```

---

## 18.7 Custom Exceptions

### Creating Custom Exception Classes

```python
class InsufficientFundsError(Exception):
    """Raised when account balance is too low."""
    def __init__(self, balance, amount):
        self.balance = balance
        self.amount = amount
        self.deficit = amount - balance
        super().__init__(
            f"Cannot withdraw ₹{amount:,.2f}. "
            f"Balance: ₹{balance:,.2f}. "
            f"Short by: ₹{self.deficit:,.2f}"
        )

class InvalidAccountError(Exception):
    """Raised when account number is invalid."""
    pass

# Using custom exceptions
def withdraw(balance, amount):
    if amount <= 0:
        raise ValueError("Withdrawal amount must be positive")
    if amount > balance:
        raise InsufficientFundsError(balance, amount)
    return balance - amount

try:
    new_balance = withdraw(5000, 8000)
except InsufficientFundsError as e:
    print(f"Transaction failed: {e}")
    print(f"Deficit: ₹{e.deficit:,.2f}")
except ValueError as e:
    print(f"Invalid amount: {e}")
```

### Exception Class Hierarchy (Custom)

```python
class AppError(Exception):
    """Base exception for our application."""
    pass

class ValidationError(AppError):
    """Input validation errors."""
    pass

class DatabaseError(AppError):
    """Database operation errors."""
    pass

class AuthenticationError(AppError):
    """Authentication/login errors."""
    pass
```

---

## 18.8 Exception Handling Patterns

### Pattern 1: Input Validation Loop

```python
def get_positive_int(prompt):
    """Keep asking until a valid positive integer is entered."""
    while True:
        try:
            value = int(input(prompt))
            if value <= 0:
                raise ValueError("Must be positive")
            return value
        except ValueError as e:
            print(f"  Invalid: {e}. Try again.")

age = get_positive_int("Enter your age: ")
print(f"Age: {age}")
```

### Pattern 2: Safe File Reading

```python
def read_file_safely(filename):
    """Read file with comprehensive error handling."""
    try:
        with open(filename, "r", encoding="utf-8") as f:
            return f.read()
    except FileNotFoundError:
        print(f"File '{filename}' not found.")
        return None
    except PermissionError:
        print(f"No permission to read '{filename}'.")
        return None
    except UnicodeDecodeError:
        print(f"Cannot decode '{filename}' as UTF-8.")
        return None
    except Exception as e:
        print(f"Unexpected error reading '{filename}': {e}")
        return None
```

### Pattern 3: Safe Type Conversion

```python
def safe_int(value, default=0):
    """Convert to int safely, return default on failure."""
    try:
        return int(value)
    except (ValueError, TypeError):
        return default

def safe_float(value, default=0.0):
    """Convert to float safely, return default on failure."""
    try:
        return float(value)
    except (ValueError, TypeError):
        return default

print(safe_int("42"))       # 42
print(safe_int("hello"))    # 0
print(safe_float("3.14"))   # 3.14
print(safe_float("abc", -1))  # -1
```

### Pattern 4: EAFP vs LBYL

| Style | Approach | Example |
|-------|----------|---------|
| **LBYL** (Look Before You Leap) | Check before acting | `if key in dict: value = dict[key]` |
| **EAFP** (Easier to Ask Forgiveness) | Try and handle error | `try: value = dict[key] except KeyError: ...` |

```python
# LBYL — Look Before You Leap
if "name" in student:
    name = student["name"]
else:
    name = "Unknown"

# EAFP — Easier to Ask Forgiveness (Pythonic)
try:
    name = student["name"]
except KeyError:
    name = "Unknown"

# Best: Use .get() for dicts
name = student.get("name", "Unknown")
```

> **Python prefers EAFP** — it's often cleaner and can be faster when exceptions are rare.

---

## 18.9 Best Practices

| Practice | Why |
|----------|-----|
| **Catch specific exceptions** | `except ValueError` not bare `except` |
| **Don't silence errors** | Always log or handle — never empty `except: pass` |
| **Use `else` for success code** | Keep `try` block minimal |
| **Use `finally` for cleanup** | Close files, connections, release locks |
| **Use `as e` to access error** | Log the actual error message |
| **Raise meaningful errors** | Custom exceptions with clear messages |
| **Don't use exceptions for flow control** | Use if-else for expected conditions |
| **Keep try blocks small** | Easier to identify which line caused the error |

### Anti-Patterns (Don't Do This)

```python
# BAD: Bare except — catches EVERYTHING including KeyboardInterrupt
try:
    do_something()
except:
    pass

# BAD: Silencing errors
try:
    risky()
except Exception:
    pass  # Bugs hidden forever

# BAD: Too much code in try block
try:
    read_config()
    process_data()
    generate_report()
    send_email()
    update_database()
except Exception:
    print("Something failed")  # Which operation? No idea!
```

---

## 🔧 Hands-On Activity: Error-Proof Programs

**Duration:** 25 minutes

Create a file `session18_exceptions.py`:

```python
# Session 18 — Exception Handling Practice

# Part 1: Safe Calculator
print("=== Part 1: Safe Calculator ===")

def safe_divide(a, b):
    try:
        return a / b
    except ZeroDivisionError:
        return "Cannot divide by zero"
    except TypeError:
        return "Invalid types for division"

print(f"10 / 3 = {safe_divide(10, 3):.2f}")
print(f"10 / 0 = {safe_divide(10, 0)}")
print(f"'a' / 2 = {safe_divide('a', 2)}")

# Part 2: Input Validation
print("\n=== Part 2: Safe Input ===")

def get_valid_number(prompt, num_type=float):
    while True:
        try:
            value = num_type(input(prompt))
            return value
        except ValueError:
            print(f"  Please enter a valid {num_type.__name__}.")

# Uncomment to test interactively:
# number = get_valid_number("Enter a number: ")
# print(f"You entered: {number}")

# Part 3: File Error Handling
print("\n=== Part 3: File Handling ===")

for filename in ["session18_exceptions.py", "nonexistent.txt"]:
    try:
        with open(filename, "r") as f:
            lines = f.readlines()
            print(f"  '{filename}': {len(lines)} lines")
    except FileNotFoundError:
        print(f"  '{filename}': FILE NOT FOUND")
    except PermissionError:
        print(f"  '{filename}': PERMISSION DENIED")

# Part 4: Custom Exception
print("\n=== Part 4: Custom Exception ===")

class AgeError(Exception):
    def __init__(self, age, message="Invalid age"):
        self.age = age
        super().__init__(f"{message}: {age}")

def validate_age(age):
    if not isinstance(age, int):
        raise TypeError("Age must be an integer")
    if age < 0 or age > 150:
        raise AgeError(age, "Age out of range (0-150)")
    return True

test_ages = [25, -5, 200, "twenty", 0, 150]
for age in test_ages:
    try:
        validate_age(age)
        print(f"  Age {age}: Valid")
    except (AgeError, TypeError) as e:
        print(f"  Age {age}: {e}")

# Part 5: try-except-else-finally
print("\n=== Part 5: Full Pattern ===")

def process_number(value):
    try:
        num = float(value)
        result = 100 / num
    except ValueError:
        print(f"  '{value}' is not a number")
    except ZeroDivisionError:
        print(f"  Cannot divide by zero")
    else:
        print(f"  100 / {num} = {result:.2f}")
    finally:
        print(f"  Processing of '{value}' complete.")

for v in ["5", "0", "abc", "2.5"]:
    process_number(v)
    print()

print("Done!")
```

---

## Session 18 — Key Takeaways

1. **Exceptions** are runtime errors — handle them with `try-except` to prevent crashes
2. **Catch specific exceptions** (`ValueError`, `FileNotFoundError`) — never bare `except:`
3. **`else`** runs on success; **`finally`** always runs (cleanup)
4. **`raise`** lets you trigger exceptions manually with meaningful messages
5. **Custom exceptions** create domain-specific error types for your application
6. **Python prefers EAFP** — try first, handle errors if they occur

---

## Preparation for Session 19
- Practice: Add exception handling to your previous file-reading programs
- Think about: How would you combine file handling + exception handling for robust apps?
- Review: What patterns keep appearing across file I/O code?

---

*Session 18 of 30 | Module 4: File Handling & Exception Handling*
*Professional Python Programming Certification — UpSkill Global Education Technologies Inc., Canada*
