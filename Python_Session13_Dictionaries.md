# Session 13 — Dictionaries in Python
## Module 3: Data Structures | Professional Python Programming Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Build a Contact Book Using Dictionaries

---

## Learning Objectives
By the end of this session, you will be able to:
1. Create, access, and modify dictionaries
2. Use all essential dictionary methods
3. Iterate over keys, values, and items
4. Work with nested dictionaries
5. Apply dictionary comprehensions

---

## 13.1 What is a Dictionary?

A **dictionary** is an unordered (insertion-ordered in 3.7+) collection of **key-value pairs**. Each key maps to a value.

```python
# Creating dictionaries
student = {
    "name": "Alice",
    "age": 20,
    "grade": "A",
    "courses": ["Math", "Physics"]
}

# Alternative creation methods
empty = {}
from_constructor = dict(name="Alice", age=20)
from_tuples = dict([("name", "Alice"), ("age", 20)])
from_keys = dict.fromkeys(["a", "b", "c"], 0)  # {'a': 0, 'b': 0, 'c': 0}

print(type(student))  # <class 'dict'>
```

### Dictionary Properties

| Property | Detail |
|----------|--------|
| **Key-value pairs** | Each item is a `key: value` pair |
| **Ordered** | Maintains insertion order (Python 3.7+) |
| **Mutable** | Can add, modify, delete key-value pairs |
| **Keys must be unique** | Duplicate keys overwrite previous values |
| **Keys must be hashable** | Strings, numbers, tuples — NOT lists or dicts |
| **Values can be anything** | Any data type, including other dicts |
| **Fast lookup** | O(1) average for key access |

---

## 13.2 Accessing Dictionary Values

### By Key

```python
student = {"name": "Alice", "age": 20, "grade": "A"}

# Direct access
print(student["name"])    # Alice
print(student["age"])     # 20
# print(student["email"])  # KeyError! Key doesn't exist

# Safe access with .get()
print(student.get("name"))      # Alice
print(student.get("email"))     # None (no error!)
print(student.get("email", "N/A"))  # N/A (custom default)
```

### `[]` vs `.get()` Comparison

| Method | Key exists | Key missing |
|--------|-----------|-------------|
| `dict["key"]` | Returns value | **KeyError** |
| `dict.get("key")` | Returns value | Returns `None` |
| `dict.get("key", default)` | Returns value | Returns default |

> **Best Practice:** Use `.get()` when a key might not exist. Use `[]` when the key MUST exist.

---

## 13.3 Adding & Modifying Values

```python
student = {"name": "Alice", "age": 20}

# Add a new key-value pair
student["grade"] = "A"
student["email"] = "alice@email.com"

# Modify an existing value
student["age"] = 21

# Update multiple values at once
student.update({"age": 22, "city": "Delhi", "phone": "9876543210"})

# setdefault() — set only if key doesn't exist
student.setdefault("grade", "B")      # No change — "grade" already exists
student.setdefault("gpa", 8.5)        # Added — "gpa" didn't exist

print(student)
```

---

## 13.4 Removing Items

```python
student = {"name": "Alice", "age": 20, "grade": "A", "city": "Delhi"}

# pop() — remove by key, return value
age = student.pop("age")
print(f"Removed age: {age}")        # 20
# student.pop("email")              # KeyError!
email = student.pop("email", None)  # No error, returns None

# popitem() — remove and return last inserted pair
last = student.popitem()
print(f"Last item: {last}")         # ('city', 'Delhi')

# del — delete by key
del student["grade"]

# clear() — remove all items
student.clear()
print(student)  # {}
```

---

## 13.5 Dictionary Methods Reference

| Method | Description | Returns |
|--------|-------------|---------|
| `d.get(key, default)` | Get value safely | Value or default |
| `d.keys()` | All keys | dict_keys view |
| `d.values()` | All values | dict_values view |
| `d.items()` | All key-value pairs | dict_items view |
| `d.update(other)` | Merge other dict into d | None |
| `d.pop(key, default)` | Remove key, return value | Value or default |
| `d.popitem()` | Remove last pair | (key, value) tuple |
| `d.setdefault(key, default)` | Get or set if missing | Value |
| `d.clear()` | Remove all items | None |
| `d.copy()` | Shallow copy | dict |
| `dict.fromkeys(keys, value)` | Create from keys | dict |

---

## 13.6 Iterating Over Dictionaries

```python
student = {"name": "Alice", "age": 20, "grade": "A", "city": "Delhi"}

# Iterate over keys (default)
for key in student:
    print(key)

# Iterate over keys (explicit)
for key in student.keys():
    print(key)

# Iterate over values
for value in student.values():
    print(value)

# Iterate over key-value pairs
for key, value in student.items():
    print(f"{key}: {value}")

# Check if key exists
if "name" in student:
    print(f"Name: {student['name']}")

# Check if value exists
if "Alice" in student.values():
    print("Alice is in the dictionary")
```

---

## 13.7 Nested Dictionaries

### Creating Nested Dicts

```python
company = {
    "engineering": {
        "lead": "Alice",
        "team_size": 15,
        "projects": ["API", "Frontend", "Database"]
    },
    "marketing": {
        "lead": "Bob",
        "team_size": 8,
        "projects": ["Campaign", "SEO"]
    },
    "hr": {
        "lead": "Charlie",
        "team_size": 5,
        "projects": ["Hiring", "Training"]
    }
}

# Access nested values
print(company["engineering"]["lead"])           # Alice
print(company["engineering"]["projects"][0])    # API
print(company["marketing"]["team_size"])        # 8

# Safe nested access
eng_budget = company.get("engineering", {}).get("budget", "Not set")
print(eng_budget)  # Not set
```

### Iterating Nested Dicts

```python
for dept, info in company.items():
    print(f"\n{dept.upper()}")
    print(f"  Lead: {info['lead']}")
    print(f"  Team Size: {info['team_size']}")
    print(f"  Projects: {', '.join(info['projects'])}")
```

### List of Dictionaries (Records)

```python
employees = [
    {"id": 1, "name": "Alice", "dept": "Engineering", "salary": 85000},
    {"id": 2, "name": "Bob", "dept": "Marketing", "salary": 65000},
    {"id": 3, "name": "Charlie", "dept": "Engineering", "salary": 90000},
    {"id": 4, "name": "Diana", "dept": "HR", "salary": 55000},
]

# Find all engineers
engineers = [e for e in employees if e["dept"] == "Engineering"]
print(f"Engineers: {[e['name'] for e in engineers]}")

# Average salary
avg_salary = sum(e["salary"] for e in employees) / len(employees)
print(f"Average salary: ₹{avg_salary:,.2f}")

# Sort by salary
by_salary = sorted(employees, key=lambda e: e["salary"], reverse=True)
for e in by_salary:
    print(f"  {e['name']:<10} ₹{e['salary']:>8,}")

# Group by department
from collections import defaultdict
dept_groups = defaultdict(list)
for e in employees:
    dept_groups[e["dept"]].append(e["name"])
print(dict(dept_groups))
```

---

## 13.8 Dictionary Comprehensions

### Syntax

```python
new_dict = {key_expr: value_expr for item in iterable if condition}
```

### Examples

```python
# Squares
squares = {x: x**2 for x in range(1, 6)}
# {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

# Swap keys and values
original = {"a": 1, "b": 2, "c": 3}
swapped = {v: k for k, v in original.items()}
# {1: 'a', 2: 'b', 3: 'c'}

# Filter
scores = {"Alice": 85, "Bob": 42, "Charlie": 92, "Diana": 38}
passed = {name: score for name, score in scores.items() if score >= 50}
# {'Alice': 85, 'Charlie': 92}

# Transform values
prices_usd = {"laptop": 1000, "mouse": 25, "keyboard": 50}
prices_inr = {item: price * 83 for item, price in prices_usd.items()}
# {'laptop': 83000, 'mouse': 2075, 'keyboard': 4150}

# From two lists
keys = ["name", "age", "city"]
values = ["Alice", 25, "Delhi"]
person = {k: v for k, v in zip(keys, values)}
# {'name': 'Alice', 'age': 25, 'city': 'Delhi'}
```

---

## 13.9 Merging Dictionaries

```python
defaults = {"color": "blue", "size": "medium", "font": "Arial"}
user_prefs = {"color": "red", "font_size": 14}

# Method 1: update() — modifies in place
config = defaults.copy()
config.update(user_prefs)
print(config)  # {'color': 'red', 'size': 'medium', 'font': 'Arial', 'font_size': 14}

# Method 2: ** unpacking (Python 3.5+)
config = {**defaults, **user_prefs}
print(config)

# Method 3: | operator (Python 3.9+)
config = defaults | user_prefs
print(config)
```

---

## 13.10 Counter and defaultdict

### Counter — Count Occurrences

```python
from collections import Counter

words = "the quick brown fox jumps over the lazy dog the fox".split()
word_count = Counter(words)
print(word_count)
# Counter({'the': 3, 'fox': 2, 'quick': 1, 'brown': 1, ...})

print(word_count.most_common(3))
# [('the', 3), ('fox', 2), ('quick', 1)]

# Count characters
char_count = Counter("mississippi")
print(char_count)
# Counter({'s': 4, 'i': 4, 'p': 2, 'm': 1})
```

### defaultdict — Auto-Initialize Missing Keys

```python
from collections import defaultdict

# Group items
dd = defaultdict(list)
pairs = [("fruit", "apple"), ("veggie", "carrot"), ("fruit", "banana"), ("veggie", "pea")]
for category, item in pairs:
    dd[category].append(item)
print(dict(dd))  # {'fruit': ['apple', 'banana'], 'veggie': ['carrot', 'pea']}

# Count with defaultdict
counter = defaultdict(int)
for word in "hello world hello python hello".split():
    counter[word] += 1
print(dict(counter))  # {'hello': 3, 'world': 1, 'python': 1}
```

---

## 🔧 Hands-On Activity: Contact Book

**Duration:** 25 minutes

Create a file `session13_contact_book.py`:

```python
# Session 13 — Contact Book with Dictionaries

contacts = {}

def add_contact(contacts):
    name = input("  Name: ").strip().title()
    phone = input("  Phone: ").strip()
    email = input("  Email: ").strip().lower()
    city = input("  City: ").strip().title()
    contacts[name] = {"phone": phone, "email": email, "city": city}
    print(f"  ✅ {name} added!")

def view_contacts(contacts):
    if not contacts:
        print("  No contacts.")
        return
    print(f"\n  {'Name':<15} {'Phone':<15} {'Email':<25} {'City'}")
    print(f"  {'-'*65}")
    for name, info in sorted(contacts.items()):
        print(f"  {name:<15} {info['phone']:<15} {info['email']:<25} {info['city']}")

def search_contact(contacts):
    name = input("  Search name: ").strip().title()
    if name in contacts:
        info = contacts[name]
        print(f"  Name: {name}")
        for key, value in info.items():
            print(f"  {key.title()}: {value}")
    else:
        print(f"  '{name}' not found.")

def delete_contact(contacts):
    name = input("  Name to delete: ").strip().title()
    if name in contacts:
        contacts.pop(name)
        print(f"  ✅ {name} deleted!")
    else:
        print(f"  '{name}' not found.")

# Pre-load sample data
contacts = {
    "Alice": {"phone": "9876543210", "email": "alice@email.com", "city": "Delhi"},
    "Bob": {"phone": "9123456789", "email": "bob@email.com", "city": "Mumbai"},
}

print("=" * 40)
print("  CONTACT BOOK")
print("=" * 40)

while True:
    print("\n  1. Add Contact")
    print("  2. View All")
    print("  3. Search")
    print("  4. Delete")
    print("  5. Exit")
    choice = input("  Choice: ").strip()

    if choice == "1":
        add_contact(contacts)
    elif choice == "2":
        view_contacts(contacts)
    elif choice == "3":
        search_contact(contacts)
    elif choice == "4":
        delete_contact(contacts)
    elif choice == "5":
        print("  Goodbye!")
        break
    else:
        print("  Invalid choice.")
```

---

## Session 13 — Key Takeaways

1. **Dictionaries** store key-value pairs — fast O(1) lookup by key
2. Use **`.get(key, default)`** for safe access; **`[]`** for guaranteed keys
3. **`.items()`** iterates over (key, value) pairs — most common iteration pattern
4. **Nested dicts** model complex data; **list of dicts** model records/rows
5. **Dict comprehensions** `{k: v for ...}` are concise transformations
6. **Counter** and **defaultdict** from `collections` simplify common patterns

---

## Preparation for Session 14
- Practice: Build a word frequency counter using dictionaries
- Think about: What string operations do you use most often?
- Review: What are string methods like `.split()`, `.join()`, `.replace()`?

---

*Session 13 of 30 | Module 3: Data Structures*
*Professional Python Programming Certification — UpSkill Global Education Technologies Inc., Canada*
