# Session 7 — Loops in Python
## Module 2: Control Flow & Functions | Professional Python Programming Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Build Repetitive Processing Programs

---

## Learning Objectives
By the end of this session, you will be able to:
1. Use `for` loops to iterate over sequences
2. Use `while` loops for condition-based repetition
3. Control loops with `break`, `continue`, and `pass`
4. Work with `range()` for numeric iterations
5. Write nested loops for multi-dimensional processing
6. Use loop-else pattern and list comprehensions

---

## 7.1 Why Loops?

Without loops, repetitive tasks require duplicate code:

```python
# Without loop — printing 1 to 5
print(1)
print(2)
print(3)
print(4)
print(5)

# With loop — clean and scalable
for i in range(1, 6):
    print(i)
```

### Two Types of Loops

| Loop | Use When |
|------|----------|
| **`for`** | You know HOW MANY times to repeat (iterate over a sequence) |
| **`while`** | You know WHEN TO STOP (repeat until a condition is False) |

---

## 7.2 The for Loop

### Syntax

```python
for variable in iterable:
    # Code block — executes once for each item
    statement
```

### Iterating Over Different Sequences

```python
# List
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)

# String (character by character)
for char in "Python":
    print(char, end=" ")  # P y t h o n

# Tuple
colors = ("red", "green", "blue")
for color in colors:
    print(color)

# Dictionary (iterates over keys by default)
student = {"name": "Alice", "age": 25, "grade": "A"}
for key in student:
    print(f"{key}: {student[key]}")

# Dictionary — keys and values
for key, value in student.items():
    print(f"{key}: {value}")

# Set
unique_nums = {1, 2, 3, 4, 5}
for num in unique_nums:
    print(num)
```

---

## 7.3 The range() Function

### Syntax

```python
range(stop)              # 0 to stop-1
range(start, stop)       # start to stop-1
range(start, stop, step) # start to stop-1, stepping by step
```

### Examples

```python
# range(stop) — 0 to n-1
for i in range(5):
    print(i, end=" ")  # 0 1 2 3 4

# range(start, stop) — start to stop-1
for i in range(1, 6):
    print(i, end=" ")  # 1 2 3 4 5

# range(start, stop, step) — custom step
for i in range(0, 20, 5):
    print(i, end=" ")  # 0 5 10 15

# Counting backwards
for i in range(10, 0, -1):
    print(i, end=" ")  # 10 9 8 7 6 5 4 3 2 1

# Even numbers 2 to 20
for i in range(2, 21, 2):
    print(i, end=" ")  # 2 4 6 8 10 12 14 16 18 20
```

### range() Properties

| Property | Detail |
|----------|--------|
| **Lazy** | Doesn't generate all numbers in memory |
| **Immutable** | Cannot modify a range object |
| **Efficient** | Uses O(1) memory regardless of size |
| **Supports `in`** | `5 in range(10)` → True |

```python
# range is memory efficient
r = range(1_000_000_000)   # 1 billion — uses almost no memory!
print(999_999 in r)         # True — checks without generating all numbers
```

---

## 7.4 enumerate() — Index + Value

### The Problem

```python
fruits = ["apple", "banana", "cherry"]

# Without enumerate — manual index tracking
index = 0
for fruit in fruits:
    print(f"{index}: {fruit}")
    index += 1
```

### The Solution: enumerate()

```python
# With enumerate — clean and Pythonic
for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")

# Custom start index
for i, fruit in enumerate(fruits, start=1):
    print(f"{i}. {fruit}")
# Output:
# 1. apple
# 2. banana
# 3. cherry
```

---

## 7.5 The while Loop

### Syntax

```python
while condition:
    # Code block — repeats while condition is True
    statement
    # IMPORTANT: Must update condition to avoid infinite loop!
```

### Basic Examples

```python
# Count to 5
count = 1
while count <= 5:
    print(count, end=" ")
    count += 1  # 1 2 3 4 5

# Countdown
countdown = 10
while countdown > 0:
    print(countdown, end=" ")
    countdown -= 1
print("Launch!")
```

### User Input Loop

```python
# Keep asking until valid input
while True:
    age = input("Enter your age: ").strip()
    if age.isdigit() and 1 <= int(age) <= 150:
        age = int(age)
        break
    print("Invalid! Please enter a number between 1 and 150.")

print(f"Your age is {age}")
```

### Menu-Driven Program

```python
while True:
    print("\n=== MENU ===")
    print("1. Say Hello")
    print("2. Show Date")
    print("3. Exit")
    
    choice = input("Enter choice: ").strip()
    
    if choice == "1":
        print("Hello, World!")
    elif choice == "2":
        from datetime import date
        print(f"Today: {date.today()}")
    elif choice == "3":
        print("Goodbye!")
        break
    else:
        print("Invalid choice. Try again.")
```

---

## 7.6 for vs while — When to Use Which

| Scenario | Use | Example |
|----------|-----|---------|
| Iterate over a collection | **for** | `for item in list:` |
| Known number of iterations | **for** | `for i in range(10):` |
| Repeat until condition met | **while** | `while not found:` |
| User input validation | **while** | `while True: ... break` |
| Reading until EOF | **while** | `while line := f.readline():` |
| Infinite loops (servers, games) | **while** | `while True:` |
| Countdown/timer | **while** | `while time_left > 0:` |

---

## 7.7 Loop Control: break, continue, pass

### break — Exit the Loop Immediately

```python
# Find first negative number
numbers = [5, 3, 8, -2, 7, -4]
for num in numbers:
    if num < 0:
        print(f"First negative: {num}")
        break
    print(f"Checking: {num}")
# Output:
# Checking: 5
# Checking: 3
# Checking: 8
# First negative: -2
```

### continue — Skip Current Iteration

```python
# Print only odd numbers
for i in range(1, 11):
    if i % 2 == 0:
        continue  # Skip even numbers
    print(i, end=" ")
# Output: 1 3 5 7 9
```

### pass — Do Nothing (Placeholder)

```python
# Placeholder for future code
for i in range(10):
    if i % 2 == 0:
        pass  # TODO: Handle even numbers later
    else:
        print(i)

# Empty function placeholder
def process_data():
    pass  # Will implement later
```

### Comparison

| Statement | Effect | Use Case |
|-----------|--------|----------|
| `break` | Exits the entire loop | Found what you're looking for |
| `continue` | Skips to next iteration | Skip certain items |
| `pass` | Does nothing | Placeholder for future code |

---

## 7.8 The else Clause on Loops

### for-else

The `else` block runs if the loop completes **without** hitting `break`.

```python
# Search for a value
numbers = [1, 3, 5, 7, 9]
target = 4

for num in numbers:
    if num == target:
        print(f"Found {target}!")
        break
else:
    print(f"{target} not found in the list.")
# Output: 4 not found in the list.
```

### while-else

```python
attempts = 3
while attempts > 0:
    password = input("Enter password: ")
    if password == "secret123":
        print("Access granted!")
        break
    attempts -= 1
    print(f"Wrong! {attempts} attempts remaining.")
else:
    print("Account locked! Too many failed attempts.")
```

### When else Runs

| Scenario | else Runs? |
|----------|-----------|
| Loop completes normally (no break) | ✅ Yes |
| Loop exits via `break` | ❌ No |
| Loop never executes (empty sequence / False condition) | ✅ Yes |

---

## 7.9 Nested Loops

### Syntax

```python
for outer in sequence1:
    for inner in sequence2:
        # Runs len(sequence1) × len(sequence2) times
        statement
```

### Example: Multiplication Table

```python
for i in range(1, 6):
    for j in range(1, 11):
        print(f"{i} x {j} = {i*j:>3}", end="  ")
    print()  # New line after each row
```

### Example: Pattern Printing

```python
# Right triangle
n = 5
for i in range(1, n + 1):
    print("* " * i)
# Output:
# *
# * *
# * * *
# * * * *
# * * * * *

# Inverted triangle
for i in range(n, 0, -1):
    print("* " * i)

# Pyramid
for i in range(1, n + 1):
    spaces = " " * (n - i)
    stars = "* " * i
    print(spaces + stars)
```

### Breaking Out of Nested Loops

```python
# break only exits the innermost loop
for i in range(3):
    for j in range(3):
        if j == 2:
            break  # Breaks inner loop only
        print(f"({i}, {j})", end=" ")
    print()

# To break outer loop — use a flag
found = False
for i in range(10):
    for j in range(10):
        if i * j == 42:
            print(f"Found: {i} x {j} = 42")
            found = True
            break
    if found:
        break
```

---

## 7.10 List Comprehensions (Preview)

### Syntax

```python
new_list = [expression for item in iterable if condition]
```

### Examples

```python
# Traditional loop
squares = []
for x in range(1, 6):
    squares.append(x ** 2)
# squares = [1, 4, 9, 16, 25]

# List comprehension — same result, one line
squares = [x ** 2 for x in range(1, 6)]

# With condition
evens = [x for x in range(1, 21) if x % 2 == 0]
# [2, 4, 6, 8, 10, 12, 14, 16, 18, 20]

# Transform strings
names = ["alice", "bob", "charlie"]
upper_names = [name.upper() for name in names]
# ['ALICE', 'BOB', 'CHARLIE']

# With if-else
labels = ["even" if x % 2 == 0 else "odd" for x in range(1, 6)]
# ['odd', 'even', 'odd', 'even', 'odd']
```

> List comprehensions are covered in depth in Session 11 (Lists). This is a preview.

---

## 7.11 Common Loop Patterns

### Pattern: Accumulator

```python
# Sum of numbers
total = 0
for num in [10, 20, 30, 40, 50]:
    total += num
print(f"Total: {total}")  # 150
```

### Pattern: Counter

```python
# Count vowels
text = "Hello World"
vowel_count = 0
for char in text.lower():
    if char in "aeiou":
        vowel_count += 1
print(f"Vowels: {vowel_count}")  # 3
```

### Pattern: Maximum/Minimum

```python
numbers = [45, 23, 78, 12, 56]
max_val = numbers[0]
for num in numbers[1:]:
    if num > max_val:
        max_val = num
print(f"Maximum: {max_val}")  # 78
```

### Pattern: Build a Result List

```python
# Filter positive numbers
numbers = [5, -3, 8, -1, 7, -4, 2]
positives = []
for num in numbers:
    if num > 0:
        positives.append(num)
print(positives)  # [5, 8, 7, 2]
```

---

## 🔧 Hands-On Activity: Loop Programs

**Duration:** 25 minutes

Create a file `session07_loops.py`:

**Part 1 — Multiplication Table (8 min)**

```python
# Generate multiplication table for a number
num = int(input("Enter a number: "))
print(f"\n--- Multiplication Table for {num} ---")
for i in range(1, 11):
    print(f"{num} x {i:>2} = {num * i:>4}")
```

**Part 2 — Number Guessing Game (10 min)**

```python
import random

secret = random.randint(1, 50)
attempts = 0
max_attempts = 7

print("\n--- Number Guessing Game ---")
print(f"Guess a number between 1 and 50 (Max {max_attempts} attempts)")

while attempts < max_attempts:
    guess = int(input(f"\nAttempt {attempts + 1}: "))
    attempts += 1
    
    if guess == secret:
        print(f"Correct! You guessed it in {attempts} attempts!")
        break
    elif guess < secret:
        print("Too low!")
    else:
        print("Too high!")
else:
    print(f"\nGame over! The number was {secret}.")
```

**Part 3 — Pattern Printing (7 min)**

```python
# Diamond pattern
n = 5
# Upper half
for i in range(1, n + 1):
    print(" " * (n - i) + "* " * i)
# Lower half
for i in range(n - 1, 0, -1):
    print(" " * (n - i) + "* " * i)
```

Run and verify. Save.

---

## Session 7 — Key Takeaways

1. **`for` loops** iterate over sequences; **`while` loops** repeat until a condition is False
2. **`range(start, stop, step)`** generates number sequences efficiently
3. **`enumerate()`** gives index + value — cleaner than manual counters
4. **`break`** exits, **`continue`** skips, **`pass`** does nothing
5. **Loop-else** runs when loop completes without `break` — useful for search patterns
6. **List comprehensions** are concise one-line loop-filter-transform expressions

---

## Preparation for Session 8
- Practice: Build a prime number checker using loops
- Think about: What if you need to reuse the same code in different parts of your program?
- Review: What is a function? Why are functions useful?

---

*Session 7 of 30 | Module 2: Control Flow & Functions*
*Professional Python Programming Certification — UpSkill Global Education Technologies Inc., Canada*
