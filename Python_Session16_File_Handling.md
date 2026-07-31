# Session 16 — File Handling in Python
## Module 4: File Handling & Exception Handling | Professional Python Programming Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Read, Write, and Manage Text Files

---

## Learning Objectives
By the end of this session, you will be able to:
1. Open, read, write, and close files using Python
2. Use the `with` statement for safe file handling
3. Work with different file modes (read, write, append)
4. Read files line by line and process text data
5. Manage file paths using `os` and `pathlib`

---

## 16.1 Why File Handling?

Variables only exist **while the program is running**. Files provide **persistent storage** — data survives after the program ends.

| In-Memory (Variables) | On Disk (Files) |
|----------------------|----------------|
| Lost when program ends | Persists permanently |
| Fast access | Slower access |
| Limited by RAM | Limited by disk space |
| Temporary | Permanent |

### Common File Operations

```
Create → Open → Read/Write → Close
```

---

## 16.2 Opening Files

### open() Function

```python
file = open(filename, mode, encoding)
```

### File Modes

| Mode | Description | Creates file? | Overwrites? |
|------|-------------|--------------|-------------|
| `"r"` | Read (default) | No — FileNotFoundError | No |
| `"w"` | Write | Yes | **Yes — erases all content!** |
| `"a"` | Append | Yes | No — adds to end |
| `"x"` | Exclusive create | Yes — FileExistsError if exists | No |
| `"r+"` | Read + Write | No | No |
| `"w+"` | Write + Read | Yes | **Yes** |
| `"a+"` | Append + Read | Yes | No |

### Text vs Binary Mode

| Suffix | Mode | Use For |
|--------|------|---------|
| `"t"` (default) | Text | `.txt`, `.csv`, `.json`, `.html` |
| `"b"` | Binary | `.jpg`, `.pdf`, `.xlsx`, `.zip` |

```python
# Text mode (default)
f = open("data.txt", "r")     # Same as open("data.txt", "rt")

# Binary mode
f = open("image.jpg", "rb")   # Read binary
```

---

## 16.3 The `with` Statement (Context Manager)

### The Problem with Manual Close

```python
# RISKY — if error occurs before close(), file stays open
f = open("data.txt", "r")
content = f.read()
# What if an error happens here?
f.close()   # May never execute!
```

### The Solution: `with` Statement

```python
# SAFE — file is automatically closed, even if an error occurs
with open("data.txt", "r") as f:
    content = f.read()
# File is automatically closed here
```

> **Always use `with` for file operations.** It guarantees the file is properly closed.

---

## 16.4 Reading Files

### Method 1: read() — Read Entire File

```python
with open("data.txt", "r") as f:
    content = f.read()
    print(content)
    print(type(content))    # <class 'str'>
    print(len(content))     # Number of characters
```

### Method 2: read(n) — Read n Characters

```python
with open("data.txt", "r") as f:
    first_100 = f.read(100)   # Read first 100 characters
    print(first_100)
```

### Method 3: readline() — Read One Line

```python
with open("data.txt", "r") as f:
    line1 = f.readline()      # First line (includes \n)
    line2 = f.readline()      # Second line
    print(line1.strip())      # Remove trailing newline
    print(line2.strip())
```

### Method 4: readlines() — Read All Lines into a List

```python
with open("data.txt", "r") as f:
    lines = f.readlines()     # List of strings (each includes \n)
    print(lines)
    
    # Clean version
    clean_lines = [line.strip() for line in lines]
    print(clean_lines)
```

### Method 5: Iterate Line by Line (Best for Large Files)

```python
with open("data.txt", "r") as f:
    for line in f:            # Memory efficient — reads one line at a time
        print(line.strip())
```

### Comparison of Read Methods

| Method | Returns | Memory | Best For |
|--------|---------|--------|----------|
| `read()` | Entire file as string | High | Small files |
| `read(n)` | n characters | Low | Partial reads |
| `readline()` | One line | Low | Line-by-line processing |
| `readlines()` | List of all lines | High | Small files needing list |
| `for line in f` | One line per iteration | **Low** | **Large files** |

---

## 16.5 Writing Files

### write() — Write a String

```python
# "w" mode — creates new file or OVERWRITES existing!
with open("output.txt", "w") as f:
    f.write("Hello, World!\n")
    f.write("This is line 2.\n")
    f.write("This is line 3.\n")
```

### writelines() — Write Multiple Strings

```python
lines = ["Line 1\n", "Line 2\n", "Line 3\n"]
with open("output.txt", "w") as f:
    f.writelines(lines)
```

### print() to File

```python
with open("output.txt", "w") as f:
    print("Hello, World!", file=f)
    print("This is line 2.", file=f)
    print(f"Calculation: {2 + 3}", file=f)
```

> `print(file=f)` automatically adds `\n`. `f.write()` does NOT.

---

## 16.6 Appending to Files

```python
# "a" mode — adds to end, does NOT erase existing content
with open("log.txt", "a") as f:
    from datetime import datetime
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    f.write(f"[{timestamp}] Application started.\n")
```

### Write vs Append

| Mode | Existing File | New File |
|------|--------------|----------|
| `"w"` | **Erases everything**, writes fresh | Creates it |
| `"a"` | Keeps existing, adds to end | Creates it |

> **Warning:** `"w"` mode **destroys** existing file content! Use `"a"` to preserve data.

---

## 16.7 File Position (Cursor)

```python
with open("data.txt", "r") as f:
    # tell() — current position
    print(f.tell())         # 0 (beginning)
    
    f.read(10)              # Read 10 chars
    print(f.tell())         # 10
    
    # seek() — move cursor
    f.seek(0)               # Go back to beginning
    print(f.tell())         # 0
    
    f.seek(5)               # Move to position 5
    rest = f.read()         # Read from position 5 to end
```

---

## 16.8 File & Directory Operations with os

```python
import os

# Check if file exists
print(os.path.exists("data.txt"))       # True/False
print(os.path.isfile("data.txt"))       # True if it's a file
print(os.path.isdir("my_folder"))       # True if it's a directory

# File info
print(os.path.getsize("data.txt"))      # File size in bytes
print(os.path.abspath("data.txt"))      # Full absolute path
print(os.path.basename("/path/to/file.txt"))   # "file.txt"
print(os.path.dirname("/path/to/file.txt"))    # "/path/to"
print(os.path.splitext("report.pdf"))          # ('report', '.pdf')

# Directory operations
os.makedirs("reports/2024", exist_ok=True)  # Create nested dirs
print(os.listdir("."))                       # List files in current dir

# Rename and delete
os.rename("old.txt", "new.txt")
os.remove("temp.txt")                       # Delete file
os.rmdir("empty_folder")                    # Delete empty dir

# Walk directory tree
for root, dirs, files in os.walk("."):
    for file in files:
        filepath = os.path.join(root, file)
        print(filepath)
```

---

## 16.9 pathlib — Modern Path Handling (Python 3.4+)

```python
from pathlib import Path

# Create path objects
p = Path("data") / "reports" / "sales.txt"
print(p)  # data/reports/sales.txt (or data\reports\sales.txt on Windows)

# Path properties
print(p.name)       # sales.txt
print(p.stem)       # sales
print(p.suffix)     # .txt
print(p.parent)     # data/reports
print(p.exists())   # True/False
print(p.is_file())  # True/False

# Read/write with pathlib
path = Path("output.txt")
path.write_text("Hello from pathlib!")
content = path.read_text()
print(content)

# List files
for f in Path(".").glob("*.py"):
    print(f.name)

# Recursive glob
for f in Path(".").rglob("*.txt"):
    print(f)

# Create directories
Path("output/reports").mkdir(parents=True, exist_ok=True)
```

### os.path vs pathlib

| Task | os.path | pathlib |
|------|---------|---------|
| Join paths | `os.path.join("a", "b")` | `Path("a") / "b"` |
| Get filename | `os.path.basename(p)` | `p.name` |
| Get extension | `os.path.splitext(p)[1]` | `p.suffix` |
| Check exists | `os.path.exists(p)` | `p.exists()` |
| Read file | `open(p).read()` | `p.read_text()` |
| Write file | `open(p, "w").write(s)` | `p.write_text(s)` |

> **Recommendation:** Use `pathlib` for new code — it's more readable and Pythonic.

---

## 16.10 Common File Patterns

### Pattern 1: Read & Process Line by Line

```python
total = 0
count = 0
with open("numbers.txt", "r") as f:
    for line in f:
        line = line.strip()
        if line and line.replace(".", "").replace("-", "").isdigit():
            total += float(line)
            count += 1
print(f"Sum: {total}, Count: {count}, Average: {total/count:.2f}")
```

### Pattern 2: Copy File with Transformation

```python
with open("input.txt", "r") as infile, open("output.txt", "w") as outfile:
    for line in infile:
        outfile.write(line.upper())
```

### Pattern 3: Log File Writer

```python
from datetime import datetime

def log(message, filename="app.log"):
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    with open(filename, "a") as f:
        f.write(f"[{timestamp}] {message}\n")

log("Application started")
log("User logged in")
log("Processing data...")
```

### Pattern 4: Safe File Reading

```python
import os

filename = "config.txt"
if os.path.exists(filename):
    with open(filename, "r") as f:
        config = f.read()
else:
    print(f"File '{filename}' not found.")
    config = ""
```

---

## 🔧 Hands-On Activity: File Operations

**Duration:** 25 minutes

Create a file `session16_files.py`:

```python
# Session 16 — File Handling Practice
import os

# Part 1: Write a file
print("=== Part 1: Writing ===")
students = [
    ("Alice", 85, "A"),
    ("Bob", 72, "B"),
    ("Charlie", 91, "A+"),
    ("Diana", 68, "B"),
    ("Eve", 95, "A+"),
]

with open("students.txt", "w") as f:
    f.write("Name,Score,Grade\n")
    for name, score, grade in students:
        f.write(f"{name},{score},{grade}\n")
print("students.txt created!")

# Part 2: Read and process
print("\n=== Part 2: Reading ===")
with open("students.txt", "r") as f:
    header = f.readline().strip()
    print(f"Header: {header}")
    
    total = 0
    count = 0
    for line in f:
        name, score, grade = line.strip().split(",")
        score = int(score)
        total += score
        count += 1
        print(f"  {name:<10} {score:>5} {grade:>3}")
    
    print(f"\n  Average Score: {total/count:.1f}")

# Part 3: Append
print("\n=== Part 3: Appending ===")
with open("students.txt", "a") as f:
    f.write("Frank,88,A\n")
print("Frank added!")

# Part 4: File info
print("\n=== Part 4: File Info ===")
size = os.path.getsize("students.txt")
print(f"File size: {size} bytes")
print(f"Absolute path: {os.path.abspath('students.txt')}")

# Part 5: Read final version
print("\n=== Part 5: Final File ===")
with open("students.txt", "r") as f:
    print(f.read())

# Cleanup
# os.remove("students.txt")
print("Done!")
```

---

## Session 16 — Key Takeaways

1. **Always use `with open(...) as f:`** — guarantees the file is closed properly
2. **Modes:** `"r"` read, `"w"` write (overwrites!), `"a"` append, `"x"` exclusive create
3. **For large files:** iterate line by line (`for line in f`) — most memory efficient
4. **`write()` needs explicit `\n`**; `print(file=f)` adds it automatically
5. **`pathlib.Path`** is the modern way to handle file paths
6. **Always check** `os.path.exists()` before reading — avoid FileNotFoundError

---

## Preparation for Session 17
- Practice: Write a program that counts lines, words, and characters in a file
- Think about: How would you handle structured data like CSV files?
- Review: What is a CSV file? How is it different from a text file?

---

*Session 16 of 30 | Module 4: File Handling & Exception Handling*
*Professional Python Programming Certification — UpSkill Global Education Technologies Inc., Canada*
