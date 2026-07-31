# Session 1 — Installing Python & Setting Up the Development Environment
## Module 1: Python Fundamentals | Professional Python Programming Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Install Python, VS Code, Write Your First Program

---

## Learning Objectives
By the end of this session, you will be able to:
1. Understand what Python is and why it's popular
2. Install Python on Windows/Mac/Linux
3. Set up VS Code as your Python IDE
4. Write and run your first Python program
5. Understand the Python execution model (Interpreter vs Compiler)

---

## 1.1 What is Python?

**Python** is a high-level, interpreted, general-purpose programming language created by **Guido van Rossum** in **1991**.

### Why Python?

| Reason | Detail |
|--------|--------|
| **Easy to learn** | Clean syntax, reads like English |
| **Versatile** | Web, Data Science, AI/ML, Automation, Desktop Apps |
| **Huge ecosystem** | 400,000+ packages on PyPI |
| **Community** | One of the largest developer communities worldwide |
| **Industry demand** | Used by Google, Netflix, Instagram, NASA, Spotify |
| **Cross-platform** | Runs on Windows, Mac, Linux |
| **Free & Open Source** | No licensing cost |

### Python Use Cases

| Domain | Libraries / Frameworks |
|--------|----------------------|
| **Web Development** | Django, Flask, FastAPI |
| **Data Science** | Pandas, NumPy, Matplotlib |
| **Machine Learning / AI** | Scikit-learn, TensorFlow, PyTorch |
| **Automation / Scripting** | Selenium, PyAutoGUI, os, shutil |
| **API Development** | FastAPI, Flask, Requests |
| **Desktop Applications** | Tkinter, PyQt |
| **Game Development** | Pygame |
| **DevOps / Cloud** | Boto3 (AWS), Azure SDK |

### Python Versions

| Version | Status | Notes |
|---------|--------|-------|
| Python 2.x | **End of Life** (Jan 2020) | Do NOT use |
| Python 3.x | **Active** | Always use Python 3.10+ |

> **Always use Python 3.** Python 2 is deprecated and no longer supported.

---

## 1.2 Installing Python

### Windows Installation

1. Go to [python.org/downloads](https://www.python.org/downloads/)
2. Download the latest **Python 3.12+** installer for Windows
3. **IMPORTANT:** Check ✅ **"Add Python to PATH"** on the first screen
4. Click **Install Now**
5. Wait for installation → click **Close**

### Verify Installation

Open **Command Prompt** (or PowerShell) and type:

```bash
python --version
```

Expected output:
```
Python 3.12.x
```

Also verify pip (package manager):
```bash
pip --version
```

Expected output:
```
pip 24.x.x from ... (python 3.12)
```

### Mac Installation

```bash
# Using Homebrew (recommended)
brew install python3

# Verify
python3 --version
pip3 --version
```

### Linux (Ubuntu/Debian)

```bash
sudo apt update
sudo apt install python3 python3-pip

# Verify
python3 --version
pip3 --version
```

---

## 1.3 Python Interpreter — Interactive Mode

### What is the Python Interpreter?

Python is an **interpreted language** — code is executed line by line by the Python interpreter, not compiled into machine code beforehand.

| Compiled Language (C, Java) | Interpreted Language (Python) |
|----------------------------|------------------------------|
| Source → Compiler → Machine Code → Run | Source → Interpreter → Run (line by line) |
| Errors found at compile time | Errors found at runtime |
| Faster execution | Slower execution (but fast enough for most tasks) |
| Must compile before running | Run immediately |

### Using the Interactive Interpreter (REPL)

REPL = **Read-Eval-Print-Loop**

Open terminal and type `python`:

```python
>>> 2 + 3
5
>>> "Hello, World!"
'Hello, World!'
>>> type(42)
<class 'int'>
>>> exit()
```

> The `>>>` prompt means Python is ready for input. Great for quick experiments.

---

## 1.4 Setting Up VS Code

### Why VS Code?

| Feature | Benefit |
|---------|---------|
| **Free & lightweight** | No cost, fast startup |
| **Python extension** | Syntax highlighting, IntelliSense, debugging |
| **Integrated terminal** | Run code without switching windows |
| **Extensions ecosystem** | Git, themes, linting, formatting |
| **Cross-platform** | Windows, Mac, Linux |

### Installation Steps

1. Download VS Code from [code.visualstudio.com](https://code.visualstudio.com/)
2. Install with default settings
3. Open VS Code
4. Install the **Python extension:**
   - Click Extensions icon (left sidebar) or press `Ctrl+Shift+X`
   - Search "Python"
   - Install the one by **Microsoft** (most popular)
5. Select Python Interpreter:
   - Press `Ctrl+Shift+P` → type "Python: Select Interpreter"
   - Choose the Python 3.12.x installation

### Recommended Additional Extensions

| Extension | Purpose |
|-----------|---------|
| **Pylance** | Fast Python language server (auto-installed with Python extension) |
| **Code Runner** | Run code with a single click |
| **indent-rainbow** | Colorful indentation guides |
| **Error Lens** | Show errors inline |

---

## 1.5 Your First Python Program

### Creating a Python File

1. Open VS Code
2. File → New File → Save as `hello.py`
3. Type the following code:

```python
# My first Python program
print("Hello, World!")
print("Welcome to Python Programming!")
```

### Running the Program

**Method 1: VS Code Terminal**
- Open terminal: `Ctrl + `` ` (backtick)
- Type: `python hello.py`

**Method 2: Run Button**
- Click the ▶️ Run button (top-right corner)

**Method 3: Right-click**
- Right-click in the editor → "Run Python File in Terminal"

### Expected Output

```
Hello, World!
Welcome to Python Programming!
```

---

## 1.6 Python Syntax Basics

### Comments

```python
# This is a single-line comment

"""
This is a
multi-line comment
(docstring)
"""
```

### The print() Function

```python
print("Hello")                    # String
print(42)                         # Integer
print(3.14)                       # Float
print(True)                       # Boolean
print("Age:", 25)                 # Multiple values (separated by space)
print("Name", "Age", sep=" | ")   # Custom separator
print("Line 1", end=" ")         # Custom end character (default is \n)
print("Line 2")
```

**Output:**
```
Hello
42
3.14
True
Age: 25
Name | Age
Line 1 Line 2
```

### Indentation is Mandatory

Python uses **indentation** (spaces/tabs) to define code blocks — not curly braces `{}`.

```python
# Correct — indented with 4 spaces
if True:
    print("This is inside the if block")
    print("Still inside")
print("This is outside")

# WRONG — inconsistent indentation causes IndentationError
if True:
print("Error!")  # IndentationError
```

> **Convention:** Use **4 spaces** per indentation level. Never mix tabs and spaces.

### Case Sensitivity

Python is **case-sensitive:**

```python
name = "Alice"
Name = "Bob"
NAME = "Charlie"
# All three are DIFFERENT variables
```

---

## 1.7 Python File Structure

### Anatomy of a Python Script

```python
#!/usr/bin/env python3          # Shebang (optional, for Unix/Mac)
"""
Module docstring — describes what this file does.
Author: Your Name
Date: 2024-01-01
"""

# Imports (always at the top)
import os
import sys

# Constants
MAX_RETRIES = 3
APP_NAME = "My App"

# Functions
def greet(name):
    """Greet a user by name."""
    print(f"Hello, {name}!")

# Main execution
if __name__ == "__main__":
    greet("Student")
    print("Program completed.")
```

### What is `if __name__ == "__main__"`?

| Scenario | `__name__` value |
|----------|-----------------|
| File is run directly (`python script.py`) | `"__main__"` |
| File is imported (`import script`) | `"script"` (module name) |

This guard ensures certain code only runs when the file is executed directly, not when imported.

---

## 1.8 pip — Python Package Manager

### What is pip?

**pip** (Pip Installs Packages) is Python's package manager — used to install third-party libraries from PyPI (Python Package Index).

### Common pip Commands

| Command | Purpose |
|---------|---------|
| `pip install package_name` | Install a package |
| `pip install package_name==1.2.3` | Install specific version |
| `pip uninstall package_name` | Uninstall a package |
| `pip list` | List installed packages |
| `pip show package_name` | Show package details |
| `pip freeze > requirements.txt` | Export installed packages to file |
| `pip install -r requirements.txt` | Install from requirements file |
| `pip install --upgrade package_name` | Upgrade a package |

### Virtual Environments

A **virtual environment** isolates project dependencies — each project gets its own set of packages.

```bash
# Create a virtual environment
python -m venv myenv

# Activate (Windows)
myenv\Scripts\activate

# Activate (Mac/Linux)
source myenv/bin/activate

# Deactivate
deactivate
```

> **Best Practice:** Always use a virtual environment for each project.

---

## 1.9 Interpreted vs Compiled — Deeper Look

### How Python Executes Code

```
Source Code (.py)
       │
       ▼
Python Interpreter
       │
       ├── Lexing & Parsing (syntax check)
       │
       ├── Compile to Bytecode (.pyc files in __pycache__)
       │
       ▼
Python Virtual Machine (PVM)
       │
       ▼
    Output
```

### Key Points

- Python **compiles** source code to **bytecode** (.pyc) — not machine code
- The **Python Virtual Machine (PVM)** executes the bytecode
- This makes Python **cross-platform** — bytecode runs on any OS with a Python interpreter
- `.pyc` files are cached in the `__pycache__` directory for faster subsequent runs

---

## 🔧 Hands-On Activity: Setup & First Program

**Duration:** 25 minutes

### Tasks

**Part 1 — Installation Verification (8 min)**
1. Open Command Prompt / Terminal
2. Run: `python --version` → verify Python 3.12+
3. Run: `pip --version` → verify pip is installed
4. Run: `python` → enter interactive mode
5. Type: `print("Python is working!")` → verify output
6. Type: `2 + 3` → verify it returns `5`
7. Type: `exit()` → exit interactive mode

**Part 2 — VS Code Setup (7 min)**
8. Open VS Code
9. Install the **Python extension** by Microsoft
10. Press `Ctrl+Shift+P` → "Python: Select Interpreter" → choose Python 3.12.x
11. Create a new folder: `PythonCourse`
12. Open the folder in VS Code (File → Open Folder)

**Part 3 — First Program (10 min)**
13. Create a file: `session01_hello.py`
14. Write the following:

```python
# Session 1 - My First Python Program
# Author: [Your Name]
# Date: [Today's Date]

# Basic print statements
print("=" * 40)
print("  Welcome to Python Programming!")
print("=" * 40)

# Print different data types
print("\nString:", "Hello, World!")
print("Integer:", 42)
print("Float:", 3.14)
print("Boolean:", True)

# Simple calculation
length = 10
width = 5
area = length * width
print(f"\nRectangle Area: {length} x {width} = {area}")

# Program end
print("\nProgram completed successfully!")
```

15. Run the program (▶️ button or `python session01_hello.py`)
16. Verify the output matches expected results
17. Save

---

## Session 1 — Key Takeaways

1. **Python** is a high-level, interpreted, versatile language — great for beginners and professionals
2. Always install **Python 3.12+** and check ✅ "Add to PATH"
3. **VS Code** with the Python extension is a professional, free IDE
4. `print()` is your first function — use it to display output
5. Python uses **indentation** for code blocks — 4 spaces, no curly braces
6. **pip** installs third-party packages; **virtual environments** isolate project dependencies

---

## Preparation for Session 2
- Practice: Write 5 more `print()` statements with different data
- Read about: What are variables? What are data types?
- Explore: Try `type(42)`, `type("hello")`, `type(3.14)` in the Python interactive mode

---

*Session 1 of 30 | Module 1: Python Fundamentals*
*Professional Python Programming Certification — UpSkill Global Education Technologies Inc., Canada*
