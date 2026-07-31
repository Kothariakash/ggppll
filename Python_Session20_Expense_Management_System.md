# Session 20 — Expense Management System (Module 4 Project)
## Module 4: File Handling & Exception Handling | Professional Python Programming Certification
### Duration: 1 Hour | Type: Hands-On Project | Project: Build an Expense Management System

---

## Learning Objectives
By the end of this session, you will be able to:
1. Apply file handling (text, CSV, JSON) in a real-world project
2. Build a persistent application that saves and loads data from files
3. Implement robust error handling throughout the application
4. Generate reports and export data in multiple formats
5. Use logging for application diagnostics

---

## 20.1 Project Overview

### The Brief

> Build an **Expense Management System** that allows users to record expenses, categorize them, save data to CSV files, generate reports, and export summaries. All data persists between program runs.

### Features

| Feature | Module 4 Concepts |
|---------|-------------------|
| Add expense with validation | Exception handling, input validation |
| Save/Load expenses from CSV | csv.DictWriter, csv.DictReader |
| Application settings in JSON | json.load, json.dump |
| Category-wise summary | File reading + data processing |
| Monthly report generation | File writing, formatted output |
| Export report to text file | File writing, f-strings |
| Activity logging | logging module |
| Error recovery | try-except-else-finally |

---

## 20.2 Data Model

### Expense Record (Dictionary)

```python
expense = {
    "id": "EXP001",
    "date": "2024-01-15",
    "category": "Food",
    "description": "Lunch at restaurant",
    "amount": 450.00,
    "payment": "UPI",
}
```

### Categories

```python
categories = ["Food", "Transport", "Shopping", "Bills", "Entertainment", "Health", "Education", "Other"]
```

### Payment Methods

```python
payments = ["Cash", "UPI", "Credit Card", "Debit Card", "Net Banking"]
```

### File Structure

```
expense_app/
├── data/
│   ├── expenses.csv          # All expense records
│   └── config.json           # App settings (budget, categories)
├── reports/
│   └── report_2024_01.txt    # Monthly reports
├── logs/
│   └── app.log               # Application log
└── expense_manager.py        # Main program
```

---

## 20.3 Step-by-Step Build Guide

### Step 1: Setup and Configuration

```python
import csv
import json
import os
import logging
from datetime import datetime, date

# Directory setup
os.makedirs("data", exist_ok=True)
os.makedirs("reports", exist_ok=True)
os.makedirs("logs", exist_ok=True)

# Logging setup
logging.basicConfig(
    level=logging.INFO,
    format="%(asctime)s | %(levelname)-8s | %(message)s",
    datefmt="%Y-%m-%d %H:%M:%S",
    handlers=[
        logging.FileHandler("logs/app.log"),
        logging.StreamHandler()
    ]
)
logger = logging.getLogger("ExpenseManager")

# Constants
DATA_FILE = "data/expenses.csv"
CONFIG_FILE = "data/config.json"
FIELDNAMES = ["id", "date", "category", "description", "amount", "payment"]

DEFAULT_CONFIG = {
    "monthly_budget": 30000,
    "categories": ["Food", "Transport", "Shopping", "Bills", "Entertainment", "Health", "Education", "Other"],
    "payments": ["Cash", "UPI", "Credit Card", "Debit Card", "Net Banking"],
    "currency": "INR",
    "currency_symbol": "₹",
}
```

### Step 2: Config Management

```python
def load_config():
    """Load configuration from JSON file."""
    try:
        with open(CONFIG_FILE, "r") as f:
            config = json.load(f)
        logger.info("Configuration loaded.")
        return {**DEFAULT_CONFIG, **config}
    except FileNotFoundError:
        logger.info("Config not found. Creating default.")
        save_config(DEFAULT_CONFIG)
        return DEFAULT_CONFIG.copy()
    except json.JSONDecodeError as e:
        logger.error(f"Invalid config JSON: {e}. Using defaults.")
        return DEFAULT_CONFIG.copy()

def save_config(config):
    """Save configuration to JSON file."""
    try:
        with open(CONFIG_FILE, "w") as f:
            json.dump(config, f, indent=4)
        logger.info("Configuration saved.")
    except Exception as e:
        logger.error(f"Failed to save config: {e}")
```

### Step 3: Data Persistence (CSV)

```python
def load_expenses():
    """Load all expenses from CSV file."""
    try:
        if not os.path.exists(DATA_FILE):
            return []
        with open(DATA_FILE, "r", encoding="utf-8") as f:
            reader = csv.DictReader(f)
            expenses = []
            for row in reader:
                row["amount"] = float(row["amount"])
                expenses.append(row)
        logger.info(f"Loaded {len(expenses)} expenses.")
        return expenses
    except Exception as e:
        logger.error(f"Error loading expenses: {e}")
        return []

def save_expenses(expenses):
    """Save all expenses to CSV file."""
    try:
        with open(DATA_FILE, "w", newline="", encoding="utf-8") as f:
            writer = csv.DictWriter(f, fieldnames=FIELDNAMES)
            writer.writeheader()
            for exp in expenses:
                row = exp.copy()
                row["amount"] = f"{exp['amount']:.2f}"
                writer.writerow(row)
        logger.info(f"Saved {len(expenses)} expenses.")
    except Exception as e:
        logger.error(f"Error saving expenses: {e}")

def generate_id(expenses):
    """Generate next expense ID."""
    if not expenses:
        return "EXP001"
    max_num = max(int(e["id"][3:]) for e in expenses)
    return f"EXP{max_num + 1:03d}"
```

### Step 4: Core Operations

```python
def add_expense(expenses, config):
    """Add a new expense entry."""
    print("\n--- Add New Expense ---")
    
    # Date
    date_str = input(f"  Date (YYYY-MM-DD) [today]: ").strip()
    if not date_str:
        date_str = date.today().isoformat()
    else:
        try:
            datetime.strptime(date_str, "%Y-%m-%d")
        except ValueError:
            print("  Invalid date format. Using today.")
            date_str = date.today().isoformat()
    
    # Category
    cats = config["categories"]
    print("  Categories:")
    for i, cat in enumerate(cats, 1):
        print(f"    {i}. {cat}")
    try:
        cat_idx = int(input("  Select category: ")) - 1
        category = cats[cat_idx]
    except (ValueError, IndexError):
        print("  Invalid. Using 'Other'.")
        category = "Other"
    
    # Description
    description = input("  Description: ").strip()
    if not description:
        description = category
    
    # Amount
    while True:
        try:
            amount = float(input(f"  Amount ({config['currency_symbol']}): "))
            if amount <= 0:
                raise ValueError("Amount must be positive")
            break
        except ValueError as e:
            print(f"  Invalid amount: {e}")
    
    # Payment method
    payments = config["payments"]
    print("  Payment Methods:")
    for i, pm in enumerate(payments, 1):
        print(f"    {i}. {pm}")
    try:
        pm_idx = int(input("  Select payment: ")) - 1
        payment = payments[pm_idx]
    except (ValueError, IndexError):
        payment = "Cash"
    
    # Create expense
    expense = {
        "id": generate_id(expenses),
        "date": date_str,
        "category": category,
        "description": description,
        "amount": amount,
        "payment": payment,
    }
    
    expenses.append(expense)
    save_expenses(expenses)
    
    print(f"\n  ✅ Expense added: {expense['id']} — {category} — "
          f"{config['currency_symbol']}{amount:,.2f}")
    logger.info(f"Added expense {expense['id']}: {category} {amount}")
    
    # Budget check
    check_budget(expenses, config)

def view_expenses(expenses, config):
    """Display all expenses."""
    if not expenses:
        print("\n  No expenses recorded.")
        return
    
    sym = config["currency_symbol"]
    print(f"\n  {'ID':<8} {'Date':<12} {'Category':<14} {'Description':<20} {'Amount':>10} {'Payment'}")
    print(f"  {'-'*75}")
    
    total = 0
    for e in expenses:
        print(f"  {e['id']:<8} {e['date']:<12} {e['category']:<14} "
              f"{e['description'][:18]:<20} {sym}{e['amount']:>9,.2f} {e['payment']}")
        total += e["amount"]
    
    print(f"  {'-'*75}")
    print(f"  {'TOTAL':<56} {sym}{total:>9,.2f}")
    print(f"  Total Expenses: {len(expenses)}")

def delete_expense(expenses):
    """Delete an expense by ID."""
    exp_id = input("\n  Enter Expense ID to delete: ").strip().upper()
    
    for i, e in enumerate(expenses):
        if e["id"] == exp_id:
            confirm = input(f"  Delete {e['description']} ({e['amount']})? (yes/no): ").strip().lower()
            if confirm in ("y", "yes"):
                removed = expenses.pop(i)
                save_expenses(expenses)
                print(f"  ✅ Deleted: {removed['id']}")
                logger.info(f"Deleted expense {removed['id']}")
            else:
                print("  Cancelled.")
            return
    
    print(f"  Expense '{exp_id}' not found.")

def search_expenses(expenses, config):
    """Search expenses by keyword or category."""
    query = input("\n  Search (name/category/date): ").strip().lower()
    results = [e for e in expenses if 
               query in e["description"].lower() or
               query in e["category"].lower() or
               query in e["date"]]
    
    if not results:
        print(f"  No results for '{query}'.")
        return
    
    sym = config["currency_symbol"]
    print(f"\n  Found {len(results)} result(s):")
    total = 0
    for e in results:
        print(f"  {e['id']} | {e['date']} | {e['category']:<12} | "
              f"{e['description'][:20]:<20} | {sym}{e['amount']:>9,.2f}")
        total += e["amount"]
    print(f"  Total: {sym}{total:,.2f}")
```

### Step 5: Reports

```python
def check_budget(expenses, config):
    """Check spending against monthly budget."""
    current_month = date.today().strftime("%Y-%m")
    month_total = sum(e["amount"] for e in expenses if e["date"].startswith(current_month))
    budget = config["monthly_budget"]
    sym = config["currency_symbol"]
    remaining = budget - month_total
    pct = (month_total / budget * 100) if budget > 0 else 0
    
    if pct >= 100:
        print(f"\n  ⚠ BUDGET EXCEEDED! Spent {sym}{month_total:,.2f} / {sym}{budget:,.2f} ({pct:.0f}%)")
    elif pct >= 80:
        print(f"\n  ⚠ Budget warning: {sym}{remaining:,.2f} remaining ({pct:.0f}% used)")

def category_report(expenses, config):
    """Generate category-wise spending report."""
    if not expenses:
        print("\n  No expenses to report.")
        return
    
    sym = config["currency_symbol"]
    total = sum(e["amount"] for e in expenses)
    
    # Group by category
    cat_totals = {}
    for e in expenses:
        cat = e["category"]
        cat_totals[cat] = cat_totals.get(cat, 0) + e["amount"]
    
    print(f"\n  {'Category':<15} {'Amount':>12} {'%':>7} {'Bar'}")
    print(f"  {'-'*55}")
    
    for cat, amount in sorted(cat_totals.items(), key=lambda x: x[1], reverse=True):
        pct = (amount / total * 100) if total > 0 else 0
        bar = "█" * int(pct / 2)
        print(f"  {cat:<15} {sym}{amount:>10,.2f} {pct:>6.1f}% {bar}")
    
    print(f"  {'-'*55}")
    print(f"  {'TOTAL':<15} {sym}{total:>10,.2f} {'100.0%':>7}")

def monthly_report(expenses, config):
    """Generate and export monthly report."""
    month_str = input("\n  Month (YYYY-MM) [current]: ").strip()
    if not month_str:
        month_str = date.today().strftime("%Y-%m")
    
    month_expenses = [e for e in expenses if e["date"].startswith(month_str)]
    
    if not month_expenses:
        print(f"  No expenses for {month_str}.")
        return
    
    sym = config["currency_symbol"]
    total = sum(e["amount"] for e in month_expenses)
    budget = config["monthly_budget"]
    
    # Build report text
    report = []
    report.append("=" * 60)
    report.append(f"  MONTHLY EXPENSE REPORT — {month_str}")
    report.append(f"  Generated: {datetime.now().strftime('%Y-%m-%d %H:%M:%S')}")
    report.append("=" * 60)
    report.append(f"\n  Total Expenses : {sym}{total:,.2f}")
    report.append(f"  Budget         : {sym}{budget:,.2f}")
    report.append(f"  Remaining      : {sym}{budget - total:,.2f}")
    report.append(f"  Usage          : {total/budget*100:.1f}%")
    report.append(f"  Transactions   : {len(month_expenses)}")
    
    # Category breakdown
    cat_totals = {}
    for e in month_expenses:
        cat_totals[e["category"]] = cat_totals.get(e["category"], 0) + e["amount"]
    
    report.append(f"\n  --- By Category ---")
    report.append(f"  {'Category':<15} {'Amount':>12} {'%':>7}")
    report.append(f"  {'-'*36}")
    for cat, amt in sorted(cat_totals.items(), key=lambda x: x[1], reverse=True):
        pct = amt / total * 100
        report.append(f"  {cat:<15} {sym}{amt:>10,.2f} {pct:>6.1f}%")
    
    # Transaction list
    report.append(f"\n  --- Transactions ---")
    report.append(f"  {'Date':<12} {'Category':<14} {'Description':<20} {'Amount':>10}")
    report.append(f"  {'-'*58}")
    for e in sorted(month_expenses, key=lambda x: x["date"]):
        report.append(f"  {e['date']:<12} {e['category']:<14} "
                      f"{e['description'][:18]:<20} {sym}{e['amount']:>9,.2f}")
    
    report.append("=" * 60)
    report_text = "\n".join(report)
    
    # Display
    print(report_text)
    
    # Save to file
    report_file = f"reports/report_{month_str.replace('-', '_')}.txt"
    try:
        with open(report_file, "w", encoding="utf-8") as f:
            f.write(report_text)
        print(f"\n  ✅ Report saved: {report_file}")
        logger.info(f"Report generated: {report_file}")
    except Exception as e:
        print(f"  Error saving report: {e}")
```

### Step 6: Main Menu

```python
def main():
    """Main program loop."""
    logger.info("Application started.")
    config = load_config()
    expenses = load_expenses()
    
    print("=" * 50)
    print("   EXPENSE MANAGEMENT SYSTEM")
    print("=" * 50)
    
    while True:
        print("\n--- MAIN MENU ---")
        print("  1. Add Expense")
        print("  2. View All Expenses")
        print("  3. Search Expenses")
        print("  4. Delete Expense")
        print("  5. Category Report")
        print("  6. Monthly Report")
        print("  7. Budget Status")
        print("  8. Settings")
        print("  0. Exit")
        
        choice = input("  Choice: ").strip()
        
        try:
            if choice == "1":
                add_expense(expenses, config)
            elif choice == "2":
                view_expenses(expenses, config)
            elif choice == "3":
                search_expenses(expenses, config)
            elif choice == "4":
                delete_expense(expenses)
            elif choice == "5":
                category_report(expenses, config)
            elif choice == "6":
                monthly_report(expenses, config)
            elif choice == "7":
                check_budget(expenses, config)
            elif choice == "8":
                new_budget = input(f"  Monthly budget [{config['monthly_budget']}]: ").strip()
                if new_budget:
                    config["monthly_budget"] = float(new_budget)
                    save_config(config)
                    print("  ✅ Budget updated!")
            elif choice == "0":
                save_expenses(expenses)
                print("\n  Thank you! Goodbye!")
                logger.info("Application closed.")
                break
            else:
                print("  Invalid choice.")
        except Exception as e:
            print(f"  Error: {e}")
            logger.exception(f"Unhandled error in menu choice '{choice}'")

if __name__ == "__main__":
    main()
```

---

## 20.4 Concepts Applied — Module 4 Recap

| Concept | Where Used | Session |
|---------|-----------|---------|
| File read/write (text) | Report export, log files | Session 16 |
| `with` statement | All file operations | Session 16 |
| `os.path`, `os.makedirs` | Directory and file checks | Session 16 |
| CSV DictReader/DictWriter | Load/save expenses | Session 17 |
| JSON load/dump | Config management | Session 17 |
| try-except-else-finally | Input validation, file I/O | Session 18 |
| Custom exceptions | Validation errors | Session 18 |
| Raising exceptions | Amount validation | Session 18 |
| Logging module | App diagnostics | Session 19 |
| Data validation | Input processing | Session 19 |
| Robust pipelines | Read-process-write flow | Session 19 |

---

## 20.5 Evaluation Rubric

| Criterion | Points |
|-----------|--------|
| Add expense with full validation | 15 |
| Save/load expenses from CSV (persistence) | 15 |
| Config in JSON with defaults | 10 |
| View, search, delete operations | 15 |
| Category report with percentages | 10 |
| Monthly report exported to file | 10 |
| Budget tracking and alerts | 5 |
| Logging to file | 5 |
| Error handling (no crashes) | 10 |
| Code structure (functions, modules) | 5 |
| **Total** | **100** |

---

## 🔧 Hands-On Activity: Build the Expense Management System

**Duration:** 40 minutes

Follow the Step-by-Step Build Guide. Save as `session20_expense_manager.py`.

### Submission Checklist

- [ ] Add expense with date, category, description, amount, payment
- [ ] Expenses saved to `data/expenses.csv` and persist between runs
- [ ] Config stored in `data/config.json`
- [ ] View all, search, delete operations work
- [ ] Category report with amounts and percentages
- [ ] Monthly report exported to `reports/` folder
- [ ] Budget check with warnings
- [ ] Logging to `logs/app.log`
- [ ] No crashes on invalid input

---

## Session 20 — Key Takeaways

1. **Persistent data** via CSV files makes applications useful between sessions
2. **JSON config** provides flexible, human-readable application settings
3. **Logging** replaces `print()` for production diagnostics
4. **Error handling everywhere** — every file operation and user input needs protection
5. **Directory structure** (`data/`, `reports/`, `logs/`) organizes project files

---

## Module 4 Complete — Summary

| Session | Topic | Key Skill |
|---------|-------|-----------|
| 16 | File Handling | open, read, write, append, pathlib, os |
| 17 | CSV File Handling | csv.reader, DictReader, DictWriter, JSON |
| 18 | Exception Handling | try-except-else-finally, raise, custom exceptions |
| 19 | Advanced Patterns | Logging, pipelines, context managers, decorators |
| 20 | Expense Manager | End-to-end project with persistent file storage |

### Module 4 → Module 5 Bridge

You can now build applications that **save data permanently, handle errors gracefully, and log activity**. In Module 5 (Sessions 21–25), you'll learn **Object-Oriented Programming** — classes, objects, inheritance, and packages — and build a **Banking Management System**.

---

## Preparation for Session 21
- Think about: What is a "class" in programming? What is an "object"?
- Review: How are functions different from methods?
- Practice: Think of real-world objects (Car, Student, BankAccount) and their properties/actions

---

*Session 20 of 30 | Module 4: File Handling & Exception Handling*
*Professional Python Programming Certification — UpSkill Global Education Technologies Inc., Canada*
