# Session 12 — Tuples & Sets
## Module 3: Data Structures | Professional Python Programming Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Work with Immutable & Unique Collections

---

## Learning Objectives
By the end of this session, you will be able to:
1. Create and use tuples for immutable, ordered data
2. Understand when to use tuples vs lists
3. Create and use sets for unique, unordered collections
4. Perform set operations (union, intersection, difference)
5. Use frozensets for immutable sets

---

## 12.1 Tuples

### What is a Tuple?

A **tuple** is an ordered, immutable (unchangeable) collection of items.

```python
# Creating tuples
coordinates = (10, 20)
colors = ("red", "green", "blue")
mixed = (1, "hello", 3.14, True)
single = (42,)          # Single-item tuple — comma is required!
empty = ()
no_parens = 1, 2, 3     # Parentheses are optional

print(type(coordinates))  # <class 'tuple'>
```

### Tuple Properties

| Property | Detail |
|----------|--------|
| **Ordered** | Items maintain their order |
| **Immutable** | Cannot add, remove, or change items after creation |
| **Indexed** | Access by position (0-based) |
| **Allows duplicates** | Same value can appear multiple times |
| **Hashable** | Can be used as dictionary keys (if all items are hashable) |
| **Faster than lists** | Slightly better performance for read operations |

### Single-Item Tuple Gotcha

```python
# NOT a tuple — just a number in parentheses
not_tuple = (42)
print(type(not_tuple))  # <class 'int'>

# IS a tuple — trailing comma makes it a tuple
is_tuple = (42,)
print(type(is_tuple))   # <class 'tuple'>
```

---

## 12.2 Accessing Tuple Elements

```python
fruits = ("apple", "banana", "cherry", "date", "elderberry")

# Indexing
print(fruits[0])     # apple
print(fruits[-1])    # elderberry

# Slicing
print(fruits[1:3])   # ('banana', 'cherry')
print(fruits[::-1])  # Reversed tuple

# Unpacking
x, y, z = (10, 20, 30)
print(x, y, z)  # 10 20 30

# Extended unpacking
first, *rest = (1, 2, 3, 4, 5)
print(first)  # 1
print(rest)   # [2, 3, 4, 5] — rest is a list!

first, *middle, last = (1, 2, 3, 4, 5)
print(first, middle, last)  # 1 [2, 3, 4] 5
```

---

## 12.3 Tuple Operations & Methods

### Operations

```python
# Concatenation
t1 = (1, 2, 3)
t2 = (4, 5, 6)
t3 = t1 + t2
print(t3)  # (1, 2, 3, 4, 5, 6)

# Repetition
t4 = (0,) * 5
print(t4)  # (0, 0, 0, 0, 0)

# Membership
print(3 in t1)      # True
print(10 not in t1) # True

# Length
print(len(t1))  # 3

# Iteration
for item in t1:
    print(item)
```

### Methods (Only 2!)

| Method | Description | Example |
|--------|-------------|---------|
| `count(x)` | Count occurrences of x | `(1,2,2,3).count(2)` → 2 |
| `index(x)` | Index of first x | `(1,2,3).index(2)` → 1 |

```python
nums = (1, 2, 3, 2, 4, 2, 5)
print(nums.count(2))   # 3
print(nums.index(2))   # 1 (first occurrence)
```

### Tuples Are Immutable

```python
t = (1, 2, 3)
# t[0] = 10        # TypeError: 'tuple' object does not support item assignment
# t.append(4)      # AttributeError: 'tuple' object has no attribute 'append'
# del t[0]          # TypeError: 'tuple' object doesn't support item deletion

# But you CAN reassign the variable
t = (10, 20, 30)    # New tuple object — old one is discarded
```

---

## 12.4 When to Use Tuples vs Lists

| Use Tuple When | Use List When |
|---------------|--------------|
| Data should NOT change (coordinates, RGB) | Data needs to be modified |
| Dictionary keys | Dynamic collections |
| Function return values (multiple returns) | Ordered collection that grows/shrinks |
| Constant configuration values | Stacks, queues, buffers |
| Records/rows from a database | Shopping carts, to-do items |

### Common Tuple Use Cases

```python
# Coordinates
point = (10, 20)

# RGB Color
red = (255, 0, 0)

# Database record
employee = ("EMP001", "Alice", "Engineering", 75000)

# Function returning multiple values
def get_min_max(numbers):
    return min(numbers), max(numbers)

low, high = get_min_max([5, 2, 8, 1, 9])

# Dictionary keys (lists can't be keys!)
locations = {
    (28.6139, 77.2090): "New Delhi",
    (19.0760, 72.8777): "Mumbai",
    (13.0827, 80.2707): "Chennai",
}

# Named Tuples (structured tuples)
from collections import namedtuple

Student = namedtuple("Student", ["name", "age", "grade"])
s = Student("Alice", 20, "A")
print(s.name)    # Alice
print(s.grade)   # A
print(s[0])      # Alice (still works by index)
```

---

## 12.5 Sets

### What is a Set?

A **set** is an unordered collection of **unique** items. Duplicates are automatically removed.

```python
# Creating sets
numbers = {1, 2, 3, 4, 5}
fruits = {"apple", "banana", "cherry"}
mixed = {1, "hello", 3.14}
empty = set()          # NOT {} — that creates an empty dict!

# Duplicates are removed automatically
nums = {1, 2, 2, 3, 3, 3, 4}
print(nums)  # {1, 2, 3, 4}

# From a list (remove duplicates)
names = ["Alice", "Bob", "Alice", "Charlie", "Bob"]
unique_names = set(names)
print(unique_names)  # {'Alice', 'Bob', 'Charlie'}

print(type(numbers))  # <class 'set'>
```

### Set Properties

| Property | Detail |
|----------|--------|
| **Unordered** | No guaranteed order — cannot access by index |
| **Mutable** | Can add and remove items |
| **Unique** | No duplicate elements |
| **No indexing** | Cannot do `set[0]` |
| **Hashable items only** | Cannot contain lists, dicts, or other sets |
| **Fast membership** | `in` operator is O(1) average — very fast! |

---

## 12.6 Set Operations

### Add & Remove

```python
s = {1, 2, 3}

# Add a single item
s.add(4)
print(s)  # {1, 2, 3, 4}

# Add multiple items
s.update([5, 6, 7])
print(s)  # {1, 2, 3, 4, 5, 6, 7}

# Remove (raises KeyError if not found)
s.remove(3)
print(s)  # {1, 2, 4, 5, 6, 7}

# Discard (no error if not found)
s.discard(99)  # No error

# Pop (remove and return arbitrary item)
item = s.pop()
print(f"Popped: {item}")

# Clear
s.clear()
print(s)  # set()
```

---

## 12.7 Mathematical Set Operations

### Venn Diagram Concept

```
    Set A          Set B
  ┌───────┐    ┌───────┐
  │ 1   2 │    │ 3   4 │
  │       │ 2  │       │
  │       │ 3  │       │
  └───────┘    └───────┘
      A = {1, 2, 3}
      B = {2, 3, 4}
```

### Union (A | B) — All items from both

```python
A = {1, 2, 3}
B = {2, 3, 4}

print(A | B)           # {1, 2, 3, 4}
print(A.union(B))      # {1, 2, 3, 4}
```

### Intersection (A & B) — Items in both

```python
print(A & B)               # {2, 3}
print(A.intersection(B))   # {2, 3}
```

### Difference (A - B) — Items in A but not B

```python
print(A - B)              # {1}
print(A.difference(B))    # {1}
print(B - A)              # {4}
```

### Symmetric Difference (A ^ B) — Items in either but not both

```python
print(A ^ B)                        # {1, 4}
print(A.symmetric_difference(B))    # {1, 4}
```

### Subset & Superset

```python
C = {1, 2}
D = {1, 2, 3, 4, 5}

print(C.issubset(D))      # True  — C ⊂ D
print(D.issuperset(C))    # True  — D ⊃ C
print(C <= D)             # True  — subset operator
print(D >= C)             # True  — superset operator
print(A.isdisjoint({10, 20}))  # True — no common elements
```

### Set Operations Summary

| Operation | Operator | Method | Result |
|-----------|----------|--------|--------|
| Union | `A \| B` | `A.union(B)` | All from both |
| Intersection | `A & B` | `A.intersection(B)` | Common only |
| Difference | `A - B` | `A.difference(B)` | In A not B |
| Symmetric Diff | `A ^ B` | `A.symmetric_difference(B)` | In either not both |
| Subset | `A <= B` | `A.issubset(B)` | True if A ⊆ B |
| Superset | `A >= B` | `A.issuperset(B)` | True if A ⊇ B |
| Disjoint | — | `A.isdisjoint(B)` | True if no common |

---

## 12.8 Practical Set Applications

### Remove Duplicates from a List

```python
items = [1, 2, 2, 3, 3, 3, 4, 4, 4, 4]
unique = list(set(items))
print(unique)  # [1, 2, 3, 4] (order may vary)

# Preserve order (Python 3.7+)
unique_ordered = list(dict.fromkeys(items))
print(unique_ordered)  # [1, 2, 3, 4] (order preserved)
```

### Fast Membership Testing

```python
# List membership: O(n) — slow for large lists
big_list = list(range(1_000_000))
print(999_999 in big_list)  # Slow

# Set membership: O(1) — fast regardless of size
big_set = set(range(1_000_000))
print(999_999 in big_set)   # Fast!
```

### Find Common Items

```python
# Students in both classes
class_a = {"Alice", "Bob", "Charlie", "Diana"}
class_b = {"Charlie", "Diana", "Eve", "Frank"}

both_classes = class_a & class_b
print(f"In both: {both_classes}")     # {'Charlie', 'Diana'}

only_a = class_a - class_b
print(f"Only in A: {only_a}")         # {'Alice', 'Bob'}

all_students = class_a | class_b
print(f"All students: {all_students}")
```

### Set Comprehensions

```python
# Set comprehension — like list comprehension but with {}
squares = {x ** 2 for x in range(1, 11)}
print(squares)  # {1, 4, 9, 16, 25, 36, 49, 64, 81, 100}

# Unique first letters
words = ["apple", "avocado", "banana", "blueberry", "cherry"]
first_letters = {w[0] for w in words}
print(first_letters)  # {'a', 'b', 'c'}
```

---

## 12.9 Frozenset — Immutable Set

```python
# Cannot modify a frozenset
fs = frozenset([1, 2, 3, 4])
# fs.add(5)     # AttributeError
# fs.remove(1)  # AttributeError

# Can use as dictionary key or set member
locations = {
    frozenset({"Delhi", "Mumbai"}): "Western Route",
    frozenset({"Chennai", "Bangalore"}): "Southern Route",
}

# Supports all set operations (non-modifying)
a = frozenset({1, 2, 3})
b = frozenset({2, 3, 4})
print(a & b)  # frozenset({2, 3})
print(a | b)  # frozenset({1, 2, 3, 4})
```

---

## 12.10 Comparison: List vs Tuple vs Set

| Feature | List | Tuple | Set |
|---------|------|-------|-----|
| **Syntax** | `[1, 2, 3]` | `(1, 2, 3)` | `{1, 2, 3}` |
| **Ordered** | Yes | Yes | No |
| **Mutable** | Yes | No | Yes |
| **Duplicates** | Allowed | Allowed | Not allowed |
| **Indexing** | Yes `[0]` | Yes `[0]` | No |
| **Slicing** | Yes `[1:3]` | Yes `[1:3]` | No |
| **Dict key** | No | Yes | No (frozenset yes) |
| **Use case** | Dynamic collection | Fixed data, function returns | Unique items, math ops |
| **Speed** | Medium | Fastest | Fast membership |

---

## 🔧 Hands-On Activity: Tuples & Sets

**Duration:** 25 minutes

Create a file `session12_tuples_sets.py`:

```python
# Session 12 — Tuples & Sets

# Part 1: Tuples
print("=== Part 1: Tuples ===")
student = ("STU001", "Alice", 20, "Computer Science", 8.5)
roll, name, age, dept, gpa = student
print(f"Roll: {roll}")
print(f"Name: {name}")
print(f"Department: {dept}")
print(f"GPA: {gpa}")

# Named tuple
from collections import namedtuple
Point = namedtuple("Point", ["x", "y"])
p1 = Point(3, 4)
p2 = Point(6, 8)
distance = ((p2.x - p1.x)**2 + (p2.y - p1.y)**2) ** 0.5
print(f"\nDistance from {p1} to {p2}: {distance:.2f}")

# Part 2: Sets — Remove Duplicates
print("\n=== Part 2: Sets ===")
scores = [85, 92, 78, 92, 85, 95, 78, 88, 95, 85]
unique_scores = sorted(set(scores))
print(f"All scores: {scores}")
print(f"Unique scores: {unique_scores}")
print(f"Total: {len(scores)}, Unique: {len(unique_scores)}")

# Part 3: Set Operations
print("\n=== Part 3: Set Operations ===")
python_students = {"Alice", "Bob", "Charlie", "Diana", "Eve"}
java_students = {"Charlie", "Diana", "Frank", "Grace"}

print(f"Python: {python_students}")
print(f"Java: {java_students}")
print(f"Both: {python_students & java_students}")
print(f"Only Python: {python_students - java_students}")
print(f"Only Java: {java_students - python_students}")
print(f"All students: {python_students | java_students}")
print(f"Exactly one: {python_students ^ java_students}")

# Part 4: Practical — Unique Word Counter
print("\n=== Part 4: Word Analysis ===")
text = "the quick brown fox jumps over the lazy dog the fox"
words = text.split()
unique_words = set(words)
print(f"Total words: {len(words)}")
print(f"Unique words: {len(unique_words)}")
print(f"Words: {sorted(unique_words)}")

print("\nDone!")
```

---

## Session 12 — Key Takeaways

1. **Tuples** are immutable, ordered sequences — use for fixed data, function returns, dict keys
2. **Single-item tuple** needs a trailing comma: `(42,)` not `(42)`
3. **Sets** are unordered, unique collections — duplicates auto-removed
4. **Set operations:** union `|`, intersection `&`, difference `-`, symmetric diff `^`
5. **Sets are fast** for membership testing — O(1) vs O(n) for lists
6. **Frozenset** = immutable set — can be used as dict key

---

## Preparation for Session 13
- Practice: Use sets to find common elements between two lists
- Think about: How would you store student data with names as keys?
- Review: What is a dictionary? What is a key-value pair?

---

*Session 12 of 30 | Module 3: Data Structures*
*Professional Python Programming Certification — UpSkill Global Education Technologies Inc., Canada*
