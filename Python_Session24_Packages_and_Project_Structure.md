# Session 24 — Packages & Project Structure
## Module 5: Object-Oriented Programming | Professional Python Programming Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Build a Well-Structured Python Project

---

## Learning Objectives
By the end of this session, you will be able to:
1. Design and organize multi-file Python projects
2. Create packages with `__init__.py` and sub-packages
3. Manage imports across modules and packages
4. Follow Python project conventions and best practices
5. Use virtual environments and `requirements.txt`

---

## 24.1 Why Project Structure Matters

Small scripts work fine as single files. But as projects grow, you need organization.

### Single File vs Structured Project

```
# Single file (small script)
calculator.py          — Everything in one file

# Structured project (real application)
banking_app/
├── main.py
├── requirements.txt
├── README.md
├── models/
│   ├── __init__.py
│   ├── account.py
│   └── customer.py
├── services/
│   ├── __init__.py
│   ├── transaction.py
│   └── reporting.py
├── utils/
│   ├── __init__.py
│   ├── validators.py
│   └── formatters.py
├── data/
│   └── accounts.csv
├── tests/
│   ├── __init__.py
│   ├── test_account.py
│   └── test_transaction.py
└── logs/
    └── app.log
```

### Benefits of Good Structure

| Benefit | Detail |
|---------|--------|
| **Findability** | Know exactly where to look for code |
| **Separation of concerns** | Each file/folder has one responsibility |
| **Team collaboration** | Multiple developers work without conflicts |
| **Testability** | Test individual modules independently |
| **Reusability** | Import modules across projects |
| **Scalability** | Add features without restructuring |

---

## 24.2 Python Packages — Deep Dive

### What is a Package?

A **package** is a directory containing Python modules and a special `__init__.py` file.

```
my_package/
├── __init__.py        ← Makes it a package
├── module_a.py
├── module_b.py
└── sub_package/
    ├── __init__.py    ← Sub-package
    └── module_c.py
```

### `__init__.py` — The Package Initializer

`__init__.py` runs when the package is imported. It can be:

```python
# Option 1: Empty file (most common)
# Just marks directory as a package

# Option 2: Import convenience shortcuts
# my_package/__init__.py
from .module_a import ClassA, function_a
from .module_b import ClassB

# Now users can do:
# from my_package import ClassA
# instead of:
# from my_package.module_a import ClassA

# Option 3: Define __all__ for wildcard imports
__all__ = ['module_a', 'module_b']

# Option 4: Package-level variables/configuration
__version__ = "1.0.0"
__author__ = "Your Name"
```

### Relative vs Absolute Imports

```python
# Absolute import (preferred for clarity)
from my_package.module_a import ClassA
from my_package.sub_package.module_c import function_c

# Relative import (used within packages)
# In my_package/module_b.py:
from .module_a import ClassA           # Same package
from .sub_package.module_c import func # Sub-package
from ..other_package import something  # Parent package sibling
```

### Import Reference

| Syntax | Meaning |
|--------|---------|
| `.` | Current package |
| `..` | Parent package |
| `...` | Grandparent package |
| `from . import module` | Import module from current package |
| `from .module import item` | Import item from module in current package |

---

## 24.3 Standard Project Layout

### Minimal Project

```
my_project/
├── main.py              ← Entry point
├── README.md            ← Documentation
├── requirements.txt     ← Dependencies
└── .gitignore           ← Git exclusions
```

### Application Project

```
my_project/
├── main.py              ← Entry point
├── README.md
├── requirements.txt
├── config.py            ← Configuration
├── models/              ← Data classes / OOP models
│   ├── __init__.py
│   ├── user.py
│   └── product.py
├── services/            ← Business logic
│   ├── __init__.py
│   ├── auth_service.py
│   └── order_service.py
├── utils/               ← Helper functions
│   ├── __init__.py
│   ├── validators.py
│   └── formatters.py
├── data/                ← Data files (CSV, JSON)
│   ├── users.csv
│   └── config.json
├── tests/               ← Unit tests
│   ├── __init__.py
│   ├── test_user.py
│   └── test_order.py
└── logs/                ← Log files
    └── app.log
```

### Layer Architecture

```
┌─────────────────────────────────┐
│          main.py                │  ← Entry Point
├─────────────────────────────────┤
│         services/               │  ← Business Logic
├─────────────────────────────────┤
│          models/                │  ← Data Models (Classes)
├─────────────────────────────────┤
│          utils/                 │  ← Utilities & Helpers
├─────────────────────────────────┤
│       data/ + config            │  ← Data & Configuration
└─────────────────────────────────┘
```

---

## 24.4 Building a Structured Project — Example

### Step 1: Model Layer (`models/`)

```python
# models/__init__.py
from .account import BankAccount, SavingsAccount
from .customer import Customer

# models/account.py
class BankAccount:
    def __init__(self, account_no, owner, balance=0):
        self.account_no = account_no
        self.owner = owner
        self._balance = balance
        self._transactions = []
    
    @property
    def balance(self):
        return self._balance
    
    def deposit(self, amount):
        if amount <= 0:
            raise ValueError("Deposit must be positive")
        self._balance += amount
        self._transactions.append(("DEPOSIT", amount))
        return self._balance
    
    def withdraw(self, amount):
        if amount > self._balance:
            raise ValueError("Insufficient funds")
        self._balance -= amount
        self._transactions.append(("WITHDRAW", amount))
        return self._balance
    
    def get_transactions(self):
        return list(self._transactions)
    
    def __str__(self):
        return f"Account({self.account_no}, {self.owner}, ₹{self._balance:,.2f})"

class SavingsAccount(BankAccount):
    def __init__(self, account_no, owner, balance=0, interest_rate=0.04):
        super().__init__(account_no, owner, balance)
        self.interest_rate = interest_rate
    
    def apply_interest(self):
        interest = self._balance * self.interest_rate
        self.deposit(interest)
        return interest

# models/customer.py
class Customer:
    def __init__(self, customer_id, name, email, phone):
        self.customer_id = customer_id
        self.name = name
        self.email = email
        self.phone = phone
        self.accounts = []
    
    def add_account(self, account):
        self.accounts.append(account)
    
    def total_balance(self):
        return sum(acc.balance for acc in self.accounts)
    
    def __str__(self):
        return f"Customer({self.customer_id}, {self.name}, {len(self.accounts)} accounts)"
```

### Step 2: Service Layer (`services/`)

```python
# services/__init__.py
from .transaction import TransactionService
from .reporting import ReportService

# services/transaction.py
import logging
from datetime import datetime

logger = logging.getLogger(__name__)

class TransactionService:
    def __init__(self):
        self._history = []
    
    def transfer(self, from_account, to_account, amount):
        if amount <= 0:
            raise ValueError("Transfer amount must be positive")
        
        try:
            from_account.withdraw(amount)
            to_account.deposit(amount)
            
            record = {
                "from": from_account.account_no,
                "to": to_account.account_no,
                "amount": amount,
                "timestamp": datetime.now().isoformat(),
                "status": "SUCCESS"
            }
            self._history.append(record)
            logger.info(f"Transfer: {from_account.account_no} → {to_account.account_no}: ₹{amount}")
            return record
        except ValueError as e:
            logger.error(f"Transfer failed: {e}")
            raise
    
    def get_history(self):
        return list(self._history)

# services/reporting.py
class ReportService:
    @staticmethod
    def customer_summary(customer):
        lines = [
            f"Customer: {customer.name} ({customer.customer_id})",
            f"Email: {customer.email}",
            f"Accounts: {len(customer.accounts)}",
            f"Total Balance: ₹{customer.total_balance():,.2f}",
            "",
            f"{'Account':<12} {'Balance':>12}",
            "-" * 26,
        ]
        for acc in customer.accounts:
            lines.append(f"{acc.account_no:<12} ₹{acc.balance:>10,.2f}")
        return "\n".join(lines)
```

### Step 3: Utility Layer (`utils/`)

```python
# utils/__init__.py
from .validators import validate_email, validate_phone
from .formatters import format_currency, format_date

# utils/validators.py
import re

def validate_email(email):
    pattern = r'^[\w.+-]+@[\w-]+\.[\w.]+$'
    if not re.match(pattern, email):
        raise ValueError(f"Invalid email: {email}")
    return email

def validate_phone(phone):
    pattern = r'^[6-9]\d{9}$'
    if not re.match(pattern, phone):
        raise ValueError(f"Invalid phone: {phone}")
    return phone

# utils/formatters.py
from datetime import datetime

def format_currency(amount, symbol="₹"):
    return f"{symbol}{amount:,.2f}"

def format_date(dt=None, fmt="%d %b %Y"):
    if dt is None:
        dt = datetime.now()
    return dt.strftime(fmt)
```

### Step 4: Entry Point (`main.py`)

```python
# main.py — Application entry point
from models import BankAccount, SavingsAccount, Customer
from services import TransactionService, ReportService
from utils import validate_email, format_currency

def main():
    # Create customer
    customer = Customer("C001", "Alice", "alice@email.com", "9876543210")
    
    # Create accounts
    checking = BankAccount("ACC001", "Alice", 50000)
    savings = SavingsAccount("SAV001", "Alice", 100000, 0.06)
    
    customer.add_account(checking)
    customer.add_account(savings)
    
    # Transactions
    txn_service = TransactionService()
    txn_service.transfer(checking, savings, 10000)
    
    # Apply interest
    interest = savings.apply_interest()
    print(f"Interest earned: {format_currency(interest)}")
    
    # Report
    report = ReportService.customer_summary(customer)
    print(report)

if __name__ == "__main__":
    main()
```

---

## 24.5 Virtual Environments

### What is a Virtual Environment?

An isolated Python environment with its own packages — prevents conflicts between projects.

### Creating and Using venv

```bash
# Create virtual environment
python -m venv venv

# Activate (Windows)
venv\Scripts\activate

# Activate (Mac/Linux)
source venv/bin/activate

# Install packages (into venv only)
pip install requests pandas

# Deactivate
deactivate
```

### requirements.txt

```bash
# Generate requirements file
pip freeze > requirements.txt

# Install from requirements
pip install -r requirements.txt
```

### Example requirements.txt

```
requests==2.31.0
pandas==2.1.4
openpyxl==3.1.2
fpdf2==2.7.6
python-dotenv==1.0.0
```

---

## 24.6 Configuration Management

### config.py — Central Configuration

```python
# config.py
import os
import json

class Config:
    """Application configuration."""
    
    # Paths
    BASE_DIR = os.path.dirname(os.path.abspath(__file__))
    DATA_DIR = os.path.join(BASE_DIR, "data")
    LOG_DIR = os.path.join(BASE_DIR, "logs")
    REPORT_DIR = os.path.join(BASE_DIR, "reports")
    
    # App settings
    APP_NAME = "Banking Management System"
    VERSION = "1.0.0"
    DEBUG = False
    
    # Business rules
    MIN_BALANCE = 1000
    MAX_WITHDRAWAL = 50000
    INTEREST_RATE = 0.04
    
    @classmethod
    def ensure_dirs(cls):
        """Create necessary directories."""
        for d in [cls.DATA_DIR, cls.LOG_DIR, cls.REPORT_DIR]:
            os.makedirs(d, exist_ok=True)

# Usage in other files:
# from config import Config
# data_path = os.path.join(Config.DATA_DIR, "accounts.csv")
```

### Environment Variables with .env

```python
# .env file (add to .gitignore!)
DATABASE_URL=sqlite:///app.db
SECRET_KEY=my-secret-key-123
DEBUG=True

# Load with python-dotenv
from dotenv import load_dotenv
import os

load_dotenv()
db_url = os.getenv("DATABASE_URL")
debug = os.getenv("DEBUG", "False").lower() == "true"
```

---

## 24.7 The .gitignore File

```gitignore
# Python
__pycache__/
*.py[cod]
*.pyo
*.egg-info/
dist/
build/

# Virtual environment
venv/
.venv/
env/

# IDE
.vscode/
.idea/
*.swp

# Data and logs
data/*.csv
logs/*.log
*.db

# Environment
.env
.env.local

# OS
.DS_Store
Thumbs.db
```

---

## 24.8 README.md Template

```markdown
# Project Name

Brief description of the project.

## Features
- Feature 1
- Feature 2

## Installation

```bash
# Clone the repository
git clone https://github.com/user/project.git
cd project

# Create virtual environment
python -m venv venv
venv\Scripts\activate    # Windows
source venv/bin/activate # Mac/Linux

# Install dependencies
pip install -r requirements.txt
```

## Usage

```bash
python main.py
```

## Project Structure
```
project/
├── main.py
├── models/
├── services/
├── utils/
└── tests/
```

## License
MIT License
```

---

## 24.9 Best Practices

| Practice | Why |
|----------|-----|
| **One class per file** (for large classes) | Clear organization |
| **Group by feature, not by type** | Related code stays together |
| **Use `__init__.py` for convenience imports** | Clean public API |
| **Keep `main.py` thin** | Entry point, not business logic |
| **Use relative imports within packages** | Packages stay portable |
| **Config in one place** | Easy to modify settings |
| **Virtual environment per project** | Prevent dependency conflicts |
| **Always have requirements.txt** | Reproducible installs |
| **README.md** | Others (and future you) can understand the project |
| **.gitignore** | Don't commit generated/sensitive files |

---

## 🔧 Hands-On Activity: Structured Project

**Duration:** 25 minutes

Create the following project structure and verify imports work:

```
session24_project/
├── main.py
├── models/
│   ├── __init__.py
│   └── product.py
├── services/
│   ├── __init__.py
│   └── inventory.py
└── utils/
    ├── __init__.py
    └── helpers.py
```

**models/product.py:**
```python
class Product:
    def __init__(self, pid, name, price, qty):
        self.pid = pid
        self.name = name
        self.price = price
        self.qty = qty
    
    @property
    def value(self):
        return self.price * self.qty
    
    def __str__(self):
        return f"{self.pid} | {self.name} | ₹{self.price:,.2f} | Qty: {self.qty}"
```

**services/inventory.py:**
```python
class InventoryService:
    def __init__(self):
        self._products = []
    
    def add(self, product):
        self._products.append(product)
    
    def total_value(self):
        return sum(p.value for p in self._products)
    
    def list_all(self):
        return list(self._products)
```

**utils/helpers.py:**
```python
def format_currency(amount):
    return f"₹{amount:,.2f}"
```

**main.py:**
```python
from models.product import Product
from services.inventory import InventoryService
from utils.helpers import format_currency

def main():
    inv = InventoryService()
    inv.add(Product("P001", "Laptop", 65000, 5))
    inv.add(Product("P002", "Mouse", 500, 50))
    inv.add(Product("P003", "Keyboard", 1200, 30))
    
    print("=== Inventory ===")
    for p in inv.list_all():
        print(f"  {p}")
    print(f"\nTotal Value: {format_currency(inv.total_value())}")

if __name__ == "__main__":
    main()
```

---

## Session 24 — Key Takeaways

1. **Good project structure** separates models, services, utils, data, and tests
2. **`__init__.py`** makes a directory a package and defines its public API
3. **Relative imports** (`.module`) within packages; **absolute imports** from outside
4. **Virtual environments** (`venv`) isolate project dependencies
5. **`requirements.txt`** ensures reproducible installs
6. **Keep `main.py` thin** — it orchestrates, business logic lives in services

---

## Preparation for Session 25
- Review all Module 5 concepts: classes, inheritance, encapsulation, abstraction, packages
- Think about: How would you build a complete banking system with OOP?
- Be ready to code: Session 25 is the Module 5 project — Banking Management System

---

*Session 24 of 30 | Module 5: Object-Oriented Programming*
*Professional Python Programming Certification — UpSkill Global Education Technologies Inc., Canada*
