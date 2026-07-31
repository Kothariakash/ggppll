# Session 11 — Lists in Python
## Module 3: Data Structures | Professional Python Programming Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: List Operations and List Comprehensions

---

## Learning Objectives
By the end of this session, you will be able to:
1. Create, access, and modify lists
2. Use all essential list methods (append, insert, remove, sort, etc.)
3. Perform slicing operations on lists
4. Write list comprehensions for concise data transformations
5. Work with nested lists (2D lists/matrices)

---

## 11.1 What is a List?

A **list** is an ordered, mutable (changeable) collection of items. Lists can hold items of any data type, including mixed types.

```python
# Creating lists
numbers = [1, 2, 3, 4, 5]
names = ["Alice", "Bob", "Charlie"]
mixed = [1, "Hello", 3.14, True, None]
empty = []

print(type(numbers))  # <class 'list'>
print(len(numbers))   # 5
```

### List Properties

| Property | Detail |
|----------|--------|
| **Ordered** | Items maintain their insertion order |
| **Mutable** | Can add, remove, modify items after creation |
| **Indexed** | Access items by position (0-based) |
| **Allows duplicates** | Same value can appear multiple times |
| **Mixed types** | Can hold int, str, float, other lists, etc. |
| **Dynamic size** | Grows and shrinks as needed |

---

## 11.2 Accessing List Elements

### Indexing

```python
fruits = ["apple", "banana", "cherry", "date", "elderberry"]

# Positive indexing (left to right, starts at 0)
print(fruits[0])    # apple
print(fruits[1])    # banana
print(fruits[4])    # elderberry

# Negative indexing (right to left, starts at -1)
print(fruits[-1])   # elderberry (last item)
print(fruits[-2])   # date (second to last)
print(fruits[-5])   # apple (first item)
```

### Index Reference

```
 Index:   0        1         2        3          4
        ["apple", "banana", "cherry", "date", "elderberry"]
 Neg:   -5       -4        -3       -2         -1
```

### IndexError

```python
# Accessing an index that doesn't exist
print(fruits[10])   # IndexError: list index out of range
```

---

## 11.3 Slicing

### Syntax

```python
list[start:stop:step]
```

- `start`: Starting index (inclusive, default 0)
- `stop`: Ending index (exclusive, default end)
- `step`: Step size (default 1)

### Examples

```python
nums = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

# Basic slicing
print(nums[2:5])     # [2, 3, 4]       — index 2 to 4
print(nums[:4])      # [0, 1, 2, 3]    — start to 3
print(nums[6:])      # [6, 7, 8, 9]    — 6 to end
print(nums[:])       # [0, 1, 2, ..., 9] — full copy

# With step
print(nums[::2])     # [0, 2, 4, 6, 8] — every 2nd item
print(nums[1::2])    # [1, 3, 5, 7, 9] — odd-indexed items

# Negative step (reverse)
print(nums[::-1])    # [9, 8, 7, 6, 5, 4, 3, 2, 1, 0] — reversed
print(nums[8:2:-1])  # [8, 7, 6, 5, 4, 3]

# Slice assignment
nums[2:5] = [20, 30, 40]
print(nums)  # [0, 1, 20, 30, 40, 5, 6, 7, 8, 9]
```

---

## 11.4 Modifying Lists

### Change an Item

```python
colors = ["red", "green", "blue"]
colors[1] = "yellow"
print(colors)  # ['red', 'yellow', 'blue']
```

### Add Items

```python
fruits = ["apple", "banana"]

# append() — add to end
fruits.append("cherry")
print(fruits)  # ['apple', 'banana', 'cherry']

# insert() — add at specific position
fruits.insert(1, "avocado")
print(fruits)  # ['apple', 'avocado', 'banana', 'cherry']

# extend() — add multiple items
fruits.extend(["date", "elderberry"])
print(fruits)  # ['apple', 'avocado', 'banana', 'cherry', 'date', 'elderberry']

# + operator — concatenate (creates new list)
new_list = fruits + ["fig", "grape"]
```

### Remove Items

```python
fruits = ["apple", "banana", "cherry", "banana", "date"]

# remove() — removes FIRST occurrence by value
fruits.remove("banana")
print(fruits)  # ['apple', 'cherry', 'banana', 'date']

# pop() — removes by index and returns the item
removed = fruits.pop(1)     # Removes 'cherry'
print(removed)              # cherry
last = fruits.pop()         # Removes last item (default)

# del — delete by index or slice
del fruits[0]               # Delete first item
del fruits[1:3]             # Delete a slice

# clear() — remove all items
fruits.clear()
print(fruits)  # []
```

### Difference Between remove, pop, del

| Method | By | Returns | Error if not found |
|--------|----|---------|--------------------|
| `remove(value)` | Value | None | ValueError |
| `pop(index)` | Index (default -1) | The removed item | IndexError |
| `del list[index]` | Index/slice | Nothing | IndexError |

---

## 11.5 List Methods Reference

| Method | Description | Example | Returns |
|--------|-------------|---------|---------|
| `append(x)` | Add x to end | `l.append(5)` | None |
| `insert(i, x)` | Insert x at index i | `l.insert(0, 'a')` | None |
| `extend(iterable)` | Add all items from iterable | `l.extend([4,5])` | None |
| `remove(x)` | Remove first occurrence of x | `l.remove(3)` | None |
| `pop(i)` | Remove and return item at index i | `l.pop(0)` | item |
| `clear()` | Remove all items | `l.clear()` | None |
| `index(x)` | Return index of first x | `l.index('a')` | int |
| `count(x)` | Count occurrences of x | `l.count(3)` | int |
| `sort()` | Sort in place (ascending) | `l.sort()` | None |
| `sort(reverse=True)` | Sort descending | `l.sort(reverse=True)` | None |
| `reverse()` | Reverse in place | `l.reverse()` | None |
| `copy()` | Shallow copy | `l2 = l.copy()` | list |

### Sorting

```python
numbers = [5, 2, 8, 1, 9, 3]

# sort() — modifies in place, returns None
numbers.sort()
print(numbers)  # [1, 2, 3, 5, 8, 9]

numbers.sort(reverse=True)
print(numbers)  # [9, 8, 5, 3, 2, 1]

# sorted() — returns new list, original unchanged
original = [5, 2, 8, 1, 9]
new_sorted = sorted(original)
print(original)    # [5, 2, 8, 1, 9] — unchanged
print(new_sorted)  # [1, 2, 5, 8, 9]

# Sort with key
words = ["banana", "apple", "cherry", "date"]
words.sort(key=len)
print(words)  # ['date', 'apple', 'banana', 'cherry']

# Sort objects by a specific field
students = [("Alice", 85), ("Bob", 92), ("Charlie", 78)]
students.sort(key=lambda s: s[1], reverse=True)
print(students)  # [('Bob', 92), ('Alice', 85), ('Charlie', 78)]
```

---

## 11.6 List Copying

### Shallow Copy vs Reference

```python
# REFERENCE — both point to SAME list
a = [1, 2, 3]
b = a           # b is NOT a copy — it's the same list
b.append(4)
print(a)        # [1, 2, 3, 4] — a is also modified!

# COPY — separate lists
a = [1, 2, 3]
b = a.copy()    # OR: b = a[:]  OR: b = list(a)
b.append(4)
print(a)        # [1, 2, 3] — a is unchanged
print(b)        # [1, 2, 3, 4]
```

### Deep Copy (for Nested Lists)

```python
import copy

nested = [[1, 2], [3, 4]]
shallow = nested.copy()
deep = copy.deepcopy(nested)

nested[0][0] = 99
print(shallow)  # [[99, 2], [3, 4]] — inner list shared!
print(deep)     # [[1, 2], [3, 4]]  — fully independent
```

---

## 11.7 List Comprehensions

### Syntax

```python
new_list = [expression for item in iterable if condition]
```

### Examples

```python
# Squares of 1 to 10
squares = [x ** 2 for x in range(1, 11)]
# [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

# Even numbers only
evens = [x for x in range(1, 21) if x % 2 == 0]
# [2, 4, 6, 8, 10, 12, 14, 16, 18, 20]

# Transform strings
names = ["alice", "bob", "charlie"]
upper = [name.upper() for name in names]
# ['ALICE', 'BOB', 'CHARLIE']

# With if-else (expression, not filter)
labels = ["even" if x % 2 == 0 else "odd" for x in range(1, 6)]
# ['odd', 'even', 'odd', 'even', 'odd']

# Flatten nested list
nested = [[1, 2], [3, 4], [5, 6]]
flat = [item for sublist in nested for item in sublist]
# [1, 2, 3, 4, 5, 6]

# Filter and transform
prices = [100, 250, 50, 300, 75]
expensive = [f"₹{p}" for p in prices if p > 100]
# ['₹250', '₹300']
```

### Comprehension vs Loop — Comparison

```python
# Loop version
result = []
for x in range(10):
    if x % 2 == 0:
        result.append(x ** 2)

# Comprehension — same result
result = [x ** 2 for x in range(10) if x % 2 == 0]
# [0, 4, 16, 36, 64]
```

---

## 11.8 Nested Lists (2D Lists)

### Creating a Matrix

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Access elements: matrix[row][col]
print(matrix[0][0])  # 1  (row 0, col 0)
print(matrix[1][2])  # 6  (row 1, col 2)
print(matrix[2][1])  # 8  (row 2, col 1)

# Iterate through matrix
for row in matrix:
    for item in row:
        print(item, end=" ")
    print()
# Output:
# 1 2 3
# 4 5 6
# 7 8 9
```

### Matrix Operations

```python
# Sum all elements
total = sum(item for row in matrix for item in row)
print(f"Sum: {total}")  # 45

# Column sums
cols = len(matrix[0])
for col in range(cols):
    col_sum = sum(matrix[row][col] for row in range(len(matrix)))
    print(f"Column {col} sum: {col_sum}")

# Transpose
transposed = [[matrix[j][i] for j in range(len(matrix))] for i in range(len(matrix[0]))]
```

---

## 11.9 Useful Built-in Functions for Lists

| Function | Purpose | Example |
|----------|---------|---------|
| `len(list)` | Number of items | `len([1,2,3])` → 3 |
| `sum(list)` | Sum of numeric items | `sum([1,2,3])` → 6 |
| `min(list)` | Smallest item | `min([3,1,2])` → 1 |
| `max(list)` | Largest item | `max([3,1,2])` → 3 |
| `sorted(list)` | Return sorted copy | `sorted([3,1,2])` → [1,2,3] |
| `reversed(list)` | Return reversed iterator | `list(reversed([1,2,3]))` → [3,2,1] |
| `enumerate(list)` | Index + value pairs | `list(enumerate(['a','b']))` → [(0,'a'),(1,'b')] |
| `zip(l1, l2)` | Pair items from lists | `list(zip([1,2],['a','b']))` → [(1,'a'),(2,'b')] |
| `any(list)` | True if any truthy | `any([0, False, 1])` → True |
| `all(list)` | True if all truthy | `all([1, True, "hi"])` → True |

### zip() Examples

```python
names = ["Alice", "Bob", "Charlie"]
scores = [85, 92, 78]

# Pair them
for name, score in zip(names, scores):
    print(f"{name}: {score}")

# Create dictionary from two lists
student_dict = dict(zip(names, scores))
print(student_dict)  # {'Alice': 85, 'Bob': 92, 'Charlie': 78}
```

---

## 🔧 Hands-On Activity: List Operations

**Duration:** 25 minutes

Create a file `session11_lists.py`:

```python
# Session 11 — List Operations

# Part 1: Basic Operations
print("=== Part 1: Basic List Operations ===")
students = ["Alice", "Bob", "Charlie", "Diana", "Eve"]
print(f"Original: {students}")

students.append("Frank")
students.insert(2, "Grace")
print(f"After add: {students}")

students.remove("Bob")
popped = students.pop(-1)
print(f"After remove: {students}")
print(f"Popped: {popped}")

# Part 2: Slicing
print("\n=== Part 2: Slicing ===")
numbers = list(range(1, 21))
print(f"First 5: {numbers[:5]}")
print(f"Last 5: {numbers[-5:]}")
print(f"Every 3rd: {numbers[::3]}")
print(f"Reversed: {numbers[::-1]}")

# Part 3: List Comprehensions
print("\n=== Part 3: Comprehensions ===")
squares = [x**2 for x in range(1, 11)]
print(f"Squares: {squares}")

words = ["hello", "world", "python", "is", "great"]
long_words = [w.upper() for w in words if len(w) > 4]
print(f"Long words: {long_words}")

# Part 4: Sorting
print("\n=== Part 4: Sorting ===")
scores = [78, 92, 85, 63, 97, 45, 88]
print(f"Original: {scores}")
print(f"Sorted: {sorted(scores)}")
print(f"Top 3: {sorted(scores, reverse=True)[:3]}")

# Part 5: 2D List (Grade Table)
print("\n=== Part 5: Grade Table ===")
grades = [
    ["Alice", 85, 90, 78],
    ["Bob", 92, 88, 95],
    ["Charlie", 78, 72, 80],
]
print(f"{'Name':<10} {'Math':>5} {'Sci':>5} {'Eng':>5} {'Avg':>6}")
print("-" * 35)
for row in grades:
    avg = sum(row[1:]) / 3
    print(f"{row[0]:<10} {row[1]:>5} {row[2]:>5} {row[3]:>5} {avg:>6.1f}")

print("\nDone!")
```

---

## Session 11 — Key Takeaways

1. **Lists** are ordered, mutable, indexed collections — the most versatile data structure
2. **Indexing** starts at 0; negative indexing starts at -1 (last item)
3. **Slicing** `[start:stop:step]` extracts sub-lists — `[::-1]` reverses
4. **List comprehensions** `[expr for x in iterable if cond]` are concise and Pythonic
5. **sort()** modifies in place; **sorted()** returns a new list
6. **Copying:** `b = a` creates a reference; use `.copy()` or `[:]` for a true copy

---

## Preparation for Session 12
- Practice: Create a list of 10 numbers and find the sum, average, max, min
- Think about: What if you need a list that CANNOT be changed?
- Review: What is a tuple? What is a set?

---

*Session 11 of 30 | Module 3: Data Structures*
*Professional Python Programming Certification — UpSkill Global Education Technologies Inc., Canada*
