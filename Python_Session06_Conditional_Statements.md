# Session 6 — Conditional Statements
## Module 2: Control Flow & Functions | Professional Python Programming Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Build a Decision-Based Ticket Pricing System

---

## Learning Objectives
By the end of this session, you will be able to:
1. Use `if`, `elif`, and `else` for decision-making
2. Write nested conditional statements
3. Apply ternary (conditional) expressions
4. Combine conditions with logical operators
5. Use match-case (Python 3.10+ structural pattern matching)

---

## 6.1 The if Statement

### Syntax

```python
if condition:
    # Code block executes if condition is True
    statement1
    statement2
```

### How It Works

```
        condition
       /         \
    True         False
      |             |
  Execute        Skip
  block          block
```

### Example

```python
age = 20

if age >= 18:
    print("You are an adult.")
    print("You are eligible to vote.")

print("Program continues...")  # Always runs (not indented under if)
```

### Key Rules

| Rule | Detail |
|------|--------|
| **Colon** after condition | `if age >= 18:` — colon is mandatory |
| **Indentation** | Code block must be indented (4 spaces) |
| **Boolean expression** | Condition must evaluate to True or False |
| **Truthy/Falsy** | Non-boolean values are evaluated as truthy/falsy |

```python
# Truthy/Falsy in conditions
name = "Alice"
if name:            # Non-empty string is truthy
    print(f"Hello, {name}")

items = []
if not items:       # Empty list is falsy
    print("No items found")
```

---

## 6.2 The if-else Statement

### Syntax

```python
if condition:
    # Executes if True
    block_true
else:
    # Executes if False
    block_false
```

### Example

```python
temperature = 35

if temperature > 30:
    print("It's hot outside! Stay hydrated.")
else:
    print("The weather is pleasant.")
```

### Flow Diagram

```
        condition
       /         \
    True         False
      |             |
  if block      else block
      \           /
       \         /
    Continue program
```

---

## 6.3 The if-elif-else Chain

### Syntax

```python
if condition1:
    block1
elif condition2:
    block2
elif condition3:
    block3
else:
    default_block
```

### How It Works

- Conditions are checked **top to bottom**
- The **first** True condition's block executes
- If **no** condition is True, the `else` block executes
- Only **one block** ever executes

### Example: Grading System

```python
percentage = 78

if percentage >= 90:
    grade = "A+"
elif percentage >= 80:
    grade = "A"
elif percentage >= 70:
    grade = "B+"
elif percentage >= 60:
    grade = "B"
elif percentage >= 50:
    grade = "C"
elif percentage >= 40:
    grade = "D"
else:
    grade = "F"

print(f"Percentage: {percentage}% → Grade: {grade}")
```

### Order Matters!

```python
# WRONG order — first condition catches everything
score = 95
if score >= 40:
    print("Grade D")      # This runs! (95 >= 40 is True)
elif score >= 90:
    print("Grade A+")     # Never reached

# CORRECT order — most restrictive first
score = 95
if score >= 90:
    print("Grade A+")     # This runs correctly
elif score >= 40:
    print("Grade D")
```

---

## 6.4 Nested if Statements

### Syntax

```python
if condition1:
    if condition2:
        # Both condition1 AND condition2 are True
        block
    else:
        # condition1 is True, condition2 is False
        block
else:
    # condition1 is False
    block
```

### Example: Loan Eligibility

```python
age = 28
salary = 50000
credit_score = 720

if age >= 21:
    if salary >= 30000:
        if credit_score >= 700:
            print("Loan APPROVED!")
        else:
            print("Loan DENIED: Low credit score")
    else:
        print("Loan DENIED: Insufficient salary")
else:
    print("Loan DENIED: Must be 21 or older")
```

### Flattening Nested Conditions

Deeply nested `if` statements are hard to read. Flatten with logical operators:

```python
# Better — flattened version
if age >= 21 and salary >= 30000 and credit_score >= 700:
    print("Loan APPROVED!")
elif age < 21:
    print("Loan DENIED: Must be 21 or older")
elif salary < 30000:
    print("Loan DENIED: Insufficient salary")
else:
    print("Loan DENIED: Low credit score")
```

### Guard Clause Pattern

Return early for invalid conditions instead of nesting:

```python
def check_eligibility(age, salary, credit_score):
    if age < 21:
        return "DENIED: Must be 21 or older"
    if salary < 30000:
        return "DENIED: Insufficient salary"
    if credit_score < 700:
        return "DENIED: Low credit score"
    return "APPROVED!"
```

> **Best Practice:** Avoid nesting deeper than 2–3 levels. Use guard clauses or logical operators to flatten.

---

## 6.5 Ternary (Conditional) Expression

### Syntax

```python
value = true_value if condition else false_value
```

### Examples

```python
age = 20

# Traditional if-else
if age >= 18:
    status = "Adult"
else:
    status = "Minor"

# Ternary — same logic in one line
status = "Adult" if age >= 18 else "Minor"
print(status)  # Adult

# In print statements
print("Even" if 10 % 2 == 0 else "Odd")

# In f-strings
score = 85
print(f"Result: {'Pass' if score >= 40 else 'Fail'}")

# Nested ternary (avoid — hard to read)
grade = "A" if score >= 90 else "B" if score >= 80 else "C" if score >= 70 else "F"
```

> **Use ternary for simple conditions only.** For complex logic, use regular if-elif-else.

---

## 6.6 Multiple Conditions with Logical Operators

### Combining Conditions

```python
age = 25
income = 60000
is_employed = True

# AND — all must be True
if age >= 18 and income >= 30000 and is_employed:
    print("Eligible for credit card")

# OR — at least one must be True
if age < 12 or age >= 60:
    print("Eligible for senior/child discount")

# NOT — invert condition
if not is_employed:
    print("Currently unemployed")

# Complex combination
if (age >= 18 and income >= 50000) or (age >= 25 and is_employed):
    print("Premium membership available")
```

### Membership in Conditions

```python
day = "Saturday"

if day in ("Saturday", "Sunday"):
    print("It's the weekend!")
else:
    print("It's a weekday.")

# Check user role
role = "admin"
if role in ("admin", "superadmin", "owner"):
    print("Full access granted")
```

### String Checks in Conditions

```python
email = "user@example.com"

if "@" in email and "." in email.split("@")[1]:
    print("Valid email format")

filename = "report.pdf"
if filename.endswith((".pdf", ".doc", ".docx")):
    print("Document file detected")
```

---

## 6.7 match-case (Python 3.10+)

### Structural Pattern Matching

Similar to switch-case in other languages but more powerful.

### Syntax

```python
match variable:
    case pattern1:
        block1
    case pattern2:
        block2
    case _:
        default_block  # _ is the wildcard/default
```

### Example: Menu Selection

```python
choice = input("Enter choice (1-4): ")

match choice:
    case "1":
        print("You selected: Add Student")
    case "2":
        print("You selected: View Students")
    case "3":
        print("You selected: Delete Student")
    case "4":
        print("Exiting...")
    case _:
        print("Invalid choice!")
```

### Example: HTTP Status Codes

```python
def handle_status(status_code):
    match status_code:
        case 200:
            return "OK — Success"
        case 301:
            return "Moved Permanently"
        case 404:
            return "Not Found"
        case 500:
            return "Internal Server Error"
        case code if 200 <= code < 300:
            return f"Success ({code})"
        case code if 400 <= code < 500:
            return f"Client Error ({code})"
        case code if 500 <= code < 600:
            return f"Server Error ({code})"
        case _:
            return f"Unknown ({status_code})"
```

### Pattern Matching with OR

```python
command = "quit"

match command:
    case "quit" | "exit" | "q":
        print("Goodbye!")
    case "help" | "h" | "?":
        print("Available commands: quit, help, status")
    case _:
        print(f"Unknown command: {command}")
```

> **Note:** `match-case` requires Python 3.10+. For earlier versions, use if-elif-else.

---

## 6.8 Common Conditional Patterns

### Pattern 1: Input Validation

```python
while True:
    age = input("Enter age: ").strip()
    if not age.isdigit():
        print("Please enter a valid number.")
    elif int(age) < 1 or int(age) > 150:
        print("Age must be between 1 and 150.")
    else:
        age = int(age)
        break
```

### Pattern 2: Range-Based Classification

```python
bmi = 24.5

if bmi < 18.5:
    category = "Underweight"
elif 18.5 <= bmi < 25:
    category = "Normal"
elif 25 <= bmi < 30:
    category = "Overweight"
else:
    category = "Obese"

print(f"BMI: {bmi} → Category: {category}")
```

### Pattern 3: Multi-Criteria Decision

```python
has_ticket = True
age = 15
is_vip = False

if not has_ticket:
    print("Entry denied: No ticket")
elif age < 12 and not is_vip:
    print("Entry denied: Must be 12+ (unless VIP)")
elif is_vip:
    print("VIP entry: Welcome to the front row!")
else:
    print("General entry: Enjoy the show!")
```

### Pattern 4: Leap Year Check

```python
year = 2024

if (year % 4 == 0 and year % 100 != 0) or (year % 400 == 0):
    print(f"{year} is a leap year")
else:
    print(f"{year} is not a leap year")
```

---

## 6.9 Best Practices

| Practice | Why |
|----------|-----|
| **Most specific conditions first** | Prevents incorrect matches |
| **Avoid deep nesting (>3 levels)** | Use guard clauses or flatten |
| **Use `in` for multiple values** | `if x in (1, 2, 3)` vs `if x==1 or x==2 or x==3` |
| **Ternary for simple cases only** | Keep it readable |
| **Always have a default/else** | Handle unexpected cases |
| **Use parentheses for complex logic** | `(a and b) or c` is clearer than `a and b or c` |
| **Avoid comparing to True/False** | `if is_active:` not `if is_active == True:` |
| **Use `is` for None** | `if x is None:` not `if x == None:` |

---

## 🔧 Hands-On Activity: Ticket Pricing System

**Duration:** 25 minutes

Create a file `session06_ticket_pricing.py`:

```python
# Ticket Pricing System
print("=" * 45)
print("   MOVIE TICKET PRICING SYSTEM")
print("=" * 45)

# Input
age = int(input("\nEnter age: "))
day = input("Enter day (Mon-Sun): ").strip().title()
is_student = input("Are you a student? (yes/no): ").strip().lower() == "yes"
is_3d = input("3D movie? (yes/no): ").strip().lower() == "yes"

# Base price by age
if age < 5:
    base_price = 0
    category = "Free (Under 5)"
elif age < 12:
    base_price = 150
    category = "Child"
elif age < 60:
    base_price = 300
    category = "Adult"
else:
    base_price = 200
    category = "Senior Citizen"

# Day-based adjustment
if day in ("Saturday", "Sunday"):
    day_surcharge = 100
    day_type = "Weekend"
elif day == "Tuesday":
    day_surcharge = -50
    day_type = "Discount Tuesday"
else:
    day_surcharge = 0
    day_type = "Weekday"

# Student discount
student_discount = 50 if is_student and age >= 12 else 0

# 3D surcharge
surcharge_3d = 80 if is_3d else 0

# Final calculation
final_price = max(0, base_price + day_surcharge - student_discount + surcharge_3d)

# Display
print(f"\n{'=' * 45}")
print(f"   TICKET SUMMARY")
print(f"{'=' * 45}")
print(f"  Category       : {category}")
print(f"  Day            : {day} ({day_type})")
print(f"  Student        : {'Yes' if is_student else 'No'}")
print(f"  3D Movie       : {'Yes' if is_3d else 'No'}")
print(f"{'─' * 45}")
print(f"  Base Price     : ₹{base_price:>6}")
print(f"  Day Adjustment : ₹{day_surcharge:>+6}")
print(f"  Student Disc.  : ₹{-student_discount:>+6}")
print(f"  3D Surcharge   : ₹{surcharge_3d:>+6}")
print(f"{'─' * 45}")
print(f"  TOTAL          : ₹{final_price:>6}")
print(f"{'=' * 45}")
```

Run with different inputs to test all pricing paths. Save.

---

## Session 6 — Key Takeaways

1. **`if-elif-else`** checks conditions top-to-bottom — first True wins
2. **Condition order matters** — most specific/restrictive first
3. **Ternary expression** (`x if cond else y`) is concise for simple choices
4. **Avoid deep nesting** — use guard clauses or flatten with `and`/`or`
5. **`match-case`** (Python 3.10+) is Python's structural pattern matching
6. Always provide an **`else`/default** to handle unexpected cases

---

## Preparation for Session 7
- Practice: Add more pricing rules to the ticket system
- Think about: How would you process 10 tickets without writing the code 10 times?
- Review: What is a loop? What is the difference between `for` and `while`?

---

*Session 6 of 30 | Module 2: Control Flow & Functions*
*Professional Python Programming Certification — UpSkill Global Education Technologies Inc., Canada*
