# Session 17 — CSV File Handling
## Module 4: File Handling & Exception Handling | Professional Python Programming Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Read, Write, and Process CSV Data

---

## Learning Objectives
By the end of this session, you will be able to:
1. Read and write CSV files using Python's `csv` module
2. Work with `csv.reader`, `csv.writer`, `csv.DictReader`, and `csv.DictWriter`
3. Handle different delimiters, quoting, and edge cases
4. Process CSV data for analysis and reporting
5. Work with JSON files as an alternative data format

---

## 17.1 What is a CSV File?

**CSV** = Comma-Separated Values — a simple text format for tabular data.

```
Name,Age,City,Salary
Alice,25,Delhi,75000
Bob,30,Mumbai,85000
Charlie,28,Bangalore,90000
```

### CSV Properties

| Property | Detail |
|----------|--------|
| **Plain text** | Human-readable, editable in any text editor |
| **Universal** | Supported by Excel, databases, APIs, every language |
| **Lightweight** | No formatting, just data |
| **Row-based** | One record per line |
| **First row** | Usually the header (column names) |
| **Delimiter** | Comma by default; can be tab, semicolon, pipe |

### CSV vs Other Formats

| Format | Best For | Supports Types? | Nested Data? |
|--------|----------|----------------|-------------|
| **CSV** | Tabular data, import/export | No (all strings) | No |
| **JSON** | APIs, nested/complex data | Yes | Yes |
| **Excel** | Business users, formatting | Yes | No |
| **XML** | Configuration, legacy systems | Yes | Yes |

---

## 17.2 Reading CSV with csv.reader

### Basic Reading

```python
import csv

with open("employees.csv", "r") as f:
    reader = csv.reader(f)
    
    # Read header
    header = next(reader)
    print(f"Columns: {header}")
    
    # Read data rows
    for row in reader:
        print(row)  # Each row is a list of strings
        # row = ['Alice', '25', 'Delhi', '75000']
```

### Accessing Columns by Index

```python
import csv

with open("employees.csv", "r") as f:
    reader = csv.reader(f)
    next(reader)  # Skip header
    
    for row in reader:
        name = row[0]
        age = int(row[1])
        city = row[2]
        salary = float(row[3])
        print(f"{name:<10} Age: {age}  City: {city:<12} Salary: ₹{salary:,.2f}")
```

### Read All Rows into a List

```python
import csv

with open("employees.csv", "r") as f:
    reader = csv.reader(f)
    header = next(reader)
    data = list(reader)  # List of lists

print(f"Total records: {len(data)}")
print(f"First record: {data[0]}")
```

---

## 17.3 Reading CSV with csv.DictReader

`DictReader` returns each row as a **dictionary** with column names as keys.

```python
import csv

with open("employees.csv", "r") as f:
    reader = csv.DictReader(f)
    
    for row in reader:
        # row is a dict: {'Name': 'Alice', 'Age': '25', 'City': 'Delhi', 'Salary': '75000'}
        print(f"{row['Name']:<10} {row['City']:<12} ₹{float(row['Salary']):>10,.2f}")
```

### DictReader with Custom Fieldnames

```python
# If CSV has no header row
with open("data_no_header.csv", "r") as f:
    reader = csv.DictReader(f, fieldnames=["name", "age", "city", "salary"])
    for row in reader:
        print(row["name"])
```

### reader vs DictReader

| Feature | `csv.reader` | `csv.DictReader` |
|---------|-------------|-----------------|
| Row type | List `['Alice', '25']` | Dict `{'Name': 'Alice', 'Age': '25'}` |
| Access | By index `row[0]` | By name `row['Name']` |
| Readability | Less readable | **More readable** |
| Header | Manual `next(reader)` | Automatic (first row) |
| Best for | Simple, quick processing | Named column access |

---

## 17.4 Writing CSV with csv.writer

### Basic Writing

```python
import csv

header = ["Name", "Age", "City", "Salary"]
data = [
    ["Alice", 25, "Delhi", 75000],
    ["Bob", 30, "Mumbai", 85000],
    ["Charlie", 28, "Bangalore", 90000],
]

with open("output.csv", "w", newline="") as f:
    writer = csv.writer(f)
    writer.writerow(header)       # Write header
    writer.writerows(data)        # Write all data rows

print("CSV file created!")
```

> **Important:** Always use `newline=""` when opening CSV files for writing on Windows. This prevents extra blank lines.

### Writing One Row at a Time

```python
import csv

with open("output.csv", "w", newline="") as f:
    writer = csv.writer(f)
    writer.writerow(["Name", "Score"])
    
    for i in range(5):
        name = f"Student_{i+1}"
        score = 70 + i * 5
        writer.writerow([name, score])
```

---

## 17.5 Writing CSV with csv.DictWriter

```python
import csv

header = ["Name", "Age", "City", "Salary"]
data = [
    {"Name": "Alice", "Age": 25, "City": "Delhi", "Salary": 75000},
    {"Name": "Bob", "Age": 30, "City": "Mumbai", "Salary": 85000},
    {"Name": "Charlie", "Age": 28, "City": "Bangalore", "Salary": 90000},
]

with open("output.csv", "w", newline="") as f:
    writer = csv.DictWriter(f, fieldnames=header)
    writer.writeheader()          # Write header row
    writer.writerows(data)        # Write all data

# Or write one at a time
with open("output.csv", "w", newline="") as f:
    writer = csv.DictWriter(f, fieldnames=header)
    writer.writeheader()
    for row in data:
        writer.writerow(row)
```

---

## 17.6 CSV Options & Edge Cases

### Custom Delimiters

```python
import csv

# Tab-separated (TSV)
with open("data.tsv", "r") as f:
    reader = csv.reader(f, delimiter="\t")
    for row in reader:
        print(row)

# Semicolon-separated (common in Europe)
with open("data_eu.csv", "r") as f:
    reader = csv.reader(f, delimiter=";")
    for row in reader:
        print(row)

# Pipe-separated
with open("data.psv", "r") as f:
    reader = csv.reader(f, delimiter="|")
    for row in reader:
        print(row)
```

### Handling Quoted Fields

```python
# CSV with quotes (handles commas within fields)
# Name,Address,Salary
# "Alice","123 Main St, Apt 4",75000
# "Bob","456 Oak Ave",85000

with open("quoted.csv", "r") as f:
    reader = csv.reader(f, quotechar='"')
    for row in reader:
        print(row)
# ['Alice', '123 Main St, Apt 4', '75000'] — comma in address handled correctly
```

### Quoting Options for Writing

```python
import csv

# QUOTE_MINIMAL (default) — quote only when needed
# QUOTE_ALL — quote every field
# QUOTE_NONNUMERIC — quote all non-numeric fields
# QUOTE_NONE — never quote

with open("output.csv", "w", newline="") as f:
    writer = csv.writer(f, quoting=csv.QUOTE_ALL)
    writer.writerow(["Name", "City"])
    writer.writerow(["Alice", "New Delhi"])
# "Name","City"
# "Alice","New Delhi"
```

### Encoding Issues

```python
# Handle Unicode/special characters
with open("data.csv", "r", encoding="utf-8") as f:
    reader = csv.reader(f)
    for row in reader:
        print(row)

# For Excel-generated CSVs on Windows
with open("data.csv", "r", encoding="utf-8-sig") as f:
    reader = csv.reader(f)
    for row in reader:
        print(row)
```

---

## 17.7 CSV Data Processing Patterns

### Pattern 1: Filter & Write Subset

```python
import csv

with open("employees.csv", "r") as infile, \
     open("high_salary.csv", "w", newline="") as outfile:
    
    reader = csv.DictReader(infile)
    writer = csv.DictWriter(outfile, fieldnames=reader.fieldnames)
    writer.writeheader()
    
    for row in reader:
        if float(row["Salary"]) > 80000:
            writer.writerow(row)
```

### Pattern 2: Aggregation

```python
import csv
from collections import defaultdict

city_totals = defaultdict(float)
city_counts = defaultdict(int)

with open("employees.csv", "r") as f:
    reader = csv.DictReader(f)
    for row in reader:
        city = row["City"]
        salary = float(row["Salary"])
        city_totals[city] += salary
        city_counts[city] += 1

print(f"{'City':<15} {'Avg Salary':>12}")
for city in city_totals:
    avg = city_totals[city] / city_counts[city]
    print(f"{city:<15} ₹{avg:>10,.2f}")
```

### Pattern 3: Update CSV (Read → Modify → Write)

```python
import csv

# Read all data
with open("employees.csv", "r") as f:
    reader = csv.DictReader(f)
    fieldnames = reader.fieldnames
    data = list(reader)

# Modify: give 10% raise
for row in data:
    row["Salary"] = str(float(row["Salary"]) * 1.10)

# Write back
with open("employees.csv", "w", newline="") as f:
    writer = csv.DictWriter(f, fieldnames=fieldnames)
    writer.writeheader()
    writer.writerows(data)
```

---

## 17.8 JSON Files

### What is JSON?

**JSON** (JavaScript Object Notation) — a lightweight format for structured data, supporting nested objects and arrays.

```json
{
    "name": "Alice",
    "age": 25,
    "skills": ["Python", "SQL", "Power BI"],
    "address": {
        "city": "Delhi",
        "pin": "110001"
    }
}
```

### Reading JSON

```python
import json

# Read from file
with open("data.json", "r") as f:
    data = json.load(f)

print(data["name"])          # Alice
print(data["skills"][0])     # Python
print(data["address"]["city"])  # Delhi

# Parse JSON string
json_str = '{"name": "Alice", "age": 25}'
data = json.loads(json_str)
print(data)
```

### Writing JSON

```python
import json

data = {
    "name": "Alice",
    "age": 25,
    "skills": ["Python", "SQL"],
    "active": True,
    "salary": None
}

# Write to file
with open("output.json", "w") as f:
    json.dump(data, f, indent=4)

# Convert to JSON string
json_str = json.dumps(data, indent=4)
print(json_str)
```

### JSON ↔ Python Type Mapping

| JSON | Python |
|------|--------|
| `{}` object | `dict` |
| `[]` array | `list` |
| `"string"` | `str` |
| `123` / `1.5` | `int` / `float` |
| `true` / `false` | `True` / `False` |
| `null` | `None` |

---

## 🔧 Hands-On Activity: CSV Processing

**Duration:** 25 minutes

Create a file `session17_csv.py`:

```python
# Session 17 — CSV File Handling
import csv
import os

# Part 1: Create a CSV
print("=== Part 1: Create CSV ===")
products = [
    {"ID": "P001", "Name": "Laptop", "Category": "Electronics", "Price": "65000", "Stock": "15"},
    {"ID": "P002", "Name": "Mouse", "Category": "Electronics", "Price": "500", "Stock": "100"},
    {"ID": "P003", "Name": "Notebook", "Category": "Stationery", "Price": "45", "Stock": "500"},
    {"ID": "P004", "Name": "Pen", "Category": "Stationery", "Price": "10", "Stock": "1000"},
    {"ID": "P005", "Name": "Desk", "Category": "Furniture", "Price": "8000", "Stock": "20"},
    {"ID": "P006", "Name": "Chair", "Category": "Furniture", "Price": "5500", "Stock": "25"},
    {"ID": "P007", "Name": "Monitor", "Category": "Electronics", "Price": "18000", "Stock": "12"},
    {"ID": "P008", "Name": "Stapler", "Category": "Stationery", "Price": "120", "Stock": "80"},
]

fieldnames = ["ID", "Name", "Category", "Price", "Stock"]
with open("products.csv", "w", newline="") as f:
    writer = csv.DictWriter(f, fieldnames=fieldnames)
    writer.writeheader()
    writer.writerows(products)
print("products.csv created!")

# Part 2: Read and display
print("\n=== Part 2: Read CSV ===")
with open("products.csv", "r") as f:
    reader = csv.DictReader(f)
    print(f"{'ID':<6} {'Name':<12} {'Category':<13} {'Price':>8} {'Stock':>6}")
    print("-" * 50)
    for row in reader:
        print(f"{row['ID']:<6} {row['Name']:<12} {row['Category']:<13} "
              f"₹{float(row['Price']):>7,.0f} {row['Stock']:>6}")

# Part 3: Analysis
print("\n=== Part 3: Analysis ===")
with open("products.csv", "r") as f:
    reader = csv.DictReader(f)
    data = list(reader)

total_value = sum(float(r["Price"]) * int(r["Stock"]) for r in data)
print(f"Total Inventory Value: ₹{total_value:,.2f}")

# Category summary
categories = set(r["Category"] for r in data)
for cat in sorted(categories):
    items = [r for r in data if r["Category"] == cat]
    cat_value = sum(float(r["Price"]) * int(r["Stock"]) for r in items)
    print(f"  {cat:<13}: {len(items)} products, ₹{cat_value:,.2f}")

# Part 4: Filter expensive items
print("\n=== Part 4: Filter (Price > 1000) ===")
with open("products.csv", "r") as f, \
     open("expensive.csv", "w", newline="") as out:
    reader = csv.DictReader(f)
    writer = csv.DictWriter(out, fieldnames=fieldnames)
    writer.writeheader()
    count = 0
    for row in reader:
        if float(row["Price"]) > 1000:
            writer.writerow(row)
            count += 1
print(f"expensive.csv created with {count} products.")

# Cleanup
# os.remove("products.csv")
# os.remove("expensive.csv")
print("\nDone!")
```

---

## Session 17 — Key Takeaways

1. **`csv.DictReader`** is preferred — access columns by name, not index
2. **`csv.DictWriter`** needs `fieldnames` parameter and `writeheader()` call
3. Always use **`newline=""`** when opening CSV for writing on Windows
4. **CSV values are always strings** — convert with `int()`, `float()` as needed
5. **JSON** supports nested data and types; CSV is flat tabular data only
6. **Common pattern:** Read → Process → Write back (filter, transform, aggregate)

---

## Preparation for Session 18
- Practice: Read a CSV file and calculate the average of a numeric column
- Think about: What happens when you try to open a file that doesn't exist?
- Review: What is an exception? What is error handling?

---

*Session 17 of 30 | Module 4: File Handling & Exception Handling*
*Professional Python Programming Certification — UpSkill Global Education Technologies Inc., Canada*
