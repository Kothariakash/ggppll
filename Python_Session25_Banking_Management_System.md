# Session 25 — Banking Management System (Module 5 Project)
## Module 5: Object-Oriented Programming | Professional Python Programming Certification
### Duration: 1 Hour | Type: Hands-On Project | Project: Build a Banking Management System

---

## Learning Objectives
By the end of this session, you will be able to:
1. Apply all OOP concepts (classes, inheritance, encapsulation, abstraction) in a real project
2. Design a class hierarchy for a banking domain
3. Implement persistent data storage with CSV/JSON
4. Build a multi-feature menu-driven banking application
5. Structure a project using packages and modules

---

## 25.1 Project Overview

### The Brief

> Build a **Banking Management System** using OOP that supports customer management, multiple account types, transactions (deposit, withdraw, transfer), statement generation, and data persistence via CSV files.

### Features

| Feature | OOP Concept |
|---------|------------|
| Account base class + SavingsAccount, CurrentAccount | Inheritance |
| Private balance, PIN-protected operations | Encapsulation |
| Common interface for all account types | Polymorphism / Abstraction |
| Customer → Accounts relationship | Composition |
| Transaction logging with immutable records | Properties, tuples |
| Data persistence (CSV/JSON) | File handling |
| Structured project (models, services, utils) | Packages |

---

## 25.2 Class Hierarchy

```
                Account (ABC)
               /             \
    SavingsAccount      CurrentAccount
         |
    FixedDepositAccount

    Customer ──has──▶ [Account, Account, ...]
    
    TransactionService ──uses──▶ Account
    ReportService ──uses──▶ Customer, Account
    DataService ──uses──▶ CSV files
```

---

## 25.3 Data Model Design

### Account (Abstract Base Class)

```python
from abc import ABC, abstractmethod
from datetime import datetime

class Account(ABC):
    """Abstract base class for all bank accounts."""
    
    _next_id = 1000
    
    def __init__(self, owner, balance=0, pin="1234"):
        Account._next_id += 1
        self._account_no = f"ACC{Account._next_id}"
        self._owner = owner
        self._balance = balance
        self.__pin = pin
        self._transactions = []
        self._created = datetime.now().isoformat()
        self._active = True
    
    @property
    def account_no(self):
        return self._account_no
    
    @property
    def owner(self):
        return self._owner
    
    @property
    def balance(self):
        return self._balance
    
    @property
    def is_active(self):
        return self._active
    
    @property
    @abstractmethod
    def account_type(self):
        """Return account type string."""
        pass
    
    @abstractmethod
    def calculate_interest(self):
        """Calculate interest for this account type."""
        pass
    
    def verify_pin(self, pin):
        return pin == self.__pin
    
    def change_pin(self, old_pin, new_pin):
        if not self.verify_pin(old_pin):
            raise PermissionError("Invalid PIN")
        if len(new_pin) != 4 or not new_pin.isdigit():
            raise ValueError("PIN must be exactly 4 digits")
        self.__pin = new_pin
    
    def deposit(self, amount):
        if not self._active:
            raise RuntimeError("Account is inactive")
        if amount <= 0:
            raise ValueError("Deposit amount must be positive")
        self._balance += amount
        self._record_transaction("DEPOSIT", amount)
        return self._balance
    
    def withdraw(self, amount, pin):
        if not self._active:
            raise RuntimeError("Account is inactive")
        if not self.verify_pin(pin):
            raise PermissionError("Invalid PIN")
        if amount <= 0:
            raise ValueError("Withdrawal amount must be positive")
        if amount > self._balance:
            raise ValueError(f"Insufficient funds. Balance: ₹{self._balance:,.2f}")
        self._balance -= amount
        self._record_transaction("WITHDRAW", amount)
        return self._balance
    
    def _record_transaction(self, txn_type, amount, note=""):
        txn = {
            "timestamp": datetime.now().strftime("%Y-%m-%d %H:%M:%S"),
            "type": txn_type,
            "amount": amount,
            "balance": self._balance,
            "note": note,
        }
        self._transactions.append(txn)
    
    def get_statement(self, pin):
        if not self.verify_pin(pin):
            raise PermissionError("Invalid PIN")
        return list(self._transactions)
    
    def deactivate(self):
        self._active = False
    
    def __str__(self):
        status = "Active" if self._active else "Inactive"
        return f"{self._account_no} | {self.account_type} | {self._owner} | ₹{self._balance:,.2f} | {status}"
```

### SavingsAccount

```python
class SavingsAccount(Account):
    MIN_BALANCE = 1000
    INTEREST_RATE = 0.04
    
    def __init__(self, owner, balance=0, pin="1234"):
        if balance < self.MIN_BALANCE:
            raise ValueError(f"Minimum balance for savings: ₹{self.MIN_BALANCE:,.2f}")
        super().__init__(owner, balance, pin)
    
    @property
    def account_type(self):
        return "Savings"
    
    def calculate_interest(self):
        return self._balance * self.INTEREST_RATE
    
    def apply_interest(self):
        interest = self.calculate_interest()
        self._balance += interest
        self._record_transaction("INTEREST", interest, f"Annual rate: {self.INTEREST_RATE:.1%}")
        return interest
    
    def withdraw(self, amount, pin):
        if self._balance - amount < self.MIN_BALANCE:
            raise ValueError(f"Cannot withdraw. Minimum balance ₹{self.MIN_BALANCE:,.2f} required")
        return super().withdraw(amount, pin)
```

### CurrentAccount

```python
class CurrentAccount(Account):
    OVERDRAFT_LIMIT = 10000
    
    def __init__(self, owner, balance=0, pin="1234"):
        super().__init__(owner, balance, pin)
        self._overdraft_limit = self.OVERDRAFT_LIMIT
    
    @property
    def account_type(self):
        return "Current"
    
    def calculate_interest(self):
        return 0  # No interest on current accounts
    
    @property
    def available_balance(self):
        return self._balance + self._overdraft_limit
    
    def withdraw(self, amount, pin):
        if not self._active:
            raise RuntimeError("Account is inactive")
        if not self.verify_pin(pin):
            raise PermissionError("Invalid PIN")
        if amount <= 0:
            raise ValueError("Withdrawal amount must be positive")
        if amount > self.available_balance:
            raise ValueError(f"Exceeds overdraft limit. Available: ₹{self.available_balance:,.2f}")
        self._balance -= amount
        self._record_transaction("WITHDRAW", amount)
        if self._balance < 0:
            self._record_transaction("ALERT", 0, f"Overdraft active: ₹{abs(self._balance):,.2f}")
        return self._balance
```

---

## 25.4 Customer Class

```python
class Customer:
    _next_id = 100
    
    def __init__(self, name, email, phone):
        Customer._next_id += 1
        self.customer_id = f"CUS{Customer._next_id}"
        self.name = name
        self.email = email
        self.phone = phone
        self.accounts = []
        self.created = datetime.now().isoformat()
    
    def add_account(self, account):
        self.accounts.append(account)
    
    def get_account(self, account_no):
        for acc in self.accounts:
            if acc.account_no == account_no:
                return acc
        return None
    
    def total_balance(self):
        return sum(acc.balance for acc in self.accounts if acc.is_active)
    
    def active_accounts(self):
        return [acc for acc in self.accounts if acc.is_active]
    
    def __str__(self):
        return (f"{self.customer_id} | {self.name} | {self.email} | "
                f"{len(self.active_accounts())} accounts | ₹{self.total_balance():,.2f}")
```

---

## 25.5 Service Layer

### TransactionService

```python
import logging

logger = logging.getLogger(__name__)

class TransactionService:
    def __init__(self):
        self._transfer_log = []
    
    def transfer(self, from_account, to_account, amount, pin):
        """Transfer funds between accounts."""
        if from_account.account_no == to_account.account_no:
            raise ValueError("Cannot transfer to the same account")
        if amount <= 0:
            raise ValueError("Transfer amount must be positive")
        
        # Withdraw from source
        from_account.withdraw(amount, pin)
        
        # Deposit to destination
        to_account.deposit(amount)
        
        # Log transfer
        record = {
            "from": from_account.account_no,
            "to": to_account.account_no,
            "amount": amount,
            "timestamp": datetime.now().strftime("%Y-%m-%d %H:%M:%S"),
        }
        self._transfer_log.append(record)
        logger.info(f"Transfer: {record['from']} → {record['to']}: ₹{amount:,.2f}")
        return record
    
    def get_transfer_history(self):
        return list(self._transfer_log)
```

### ReportService

```python
class ReportService:
    @staticmethod
    def account_statement(account, pin):
        """Generate formatted account statement."""
        transactions = account.get_statement(pin)
        lines = [
            "=" * 65,
            f"  ACCOUNT STATEMENT — {account.account_no}",
            f"  Type: {account.account_type} | Owner: {account.owner}",
            "=" * 65,
        ]
        
        if transactions:
            lines.append(f"  {'Date':<20} {'Type':<12} {'Amount':>10} {'Balance':>12}")
            lines.append(f"  {'-'*58}")
            for t in transactions:
                lines.append(f"  {t['timestamp']:<20} {t['type']:<12} "
                             f"₹{t['amount']:>9,.2f} ₹{t['balance']:>10,.2f}")
        else:
            lines.append("  No transactions yet.")
        
        lines.append("=" * 65)
        lines.append(f"  Current Balance: ₹{account.balance:>10,.2f}")
        lines.append("=" * 65)
        return "\n".join(lines)
    
    @staticmethod
    def customer_summary(customer):
        """Generate customer summary report."""
        lines = [
            "=" * 55,
            f"  CUSTOMER SUMMARY — {customer.customer_id}",
            "=" * 55,
            f"  Name  : {customer.name}",
            f"  Email : {customer.email}",
            f"  Phone : {customer.phone}",
            f"  Since : {customer.created[:10]}",
            "",
            f"  {'Account':<10} {'Type':<10} {'Balance':>12} {'Status'}",
            f"  {'-'*45}",
        ]
        
        for acc in customer.accounts:
            status = "Active" if acc.is_active else "Closed"
            lines.append(f"  {acc.account_no:<10} {acc.account_type:<10} "
                         f"₹{acc.balance:>10,.2f} {status}")
        
        lines.append(f"  {'-'*45}")
        lines.append(f"  {'Total Balance':<22} ₹{customer.total_balance():>10,.2f}")
        lines.append("=" * 55)
        return "\n".join(lines)
```

---

## 25.6 Main Application

```python
import os
import logging
from datetime import datetime

# Setup
logging.basicConfig(level=logging.INFO, format="%(asctime)s | %(levelname)s | %(message)s")
logger = logging.getLogger("BankingApp")

def main():
    customers = []
    txn_service = TransactionService()
    
    # Pre-load demo data
    c1 = Customer("Alice Johnson", "alice@email.com", "9876543210")
    c1.add_account(SavingsAccount("Alice Johnson", 50000, "1111"))
    c1.add_account(CurrentAccount("Alice Johnson", 25000, "1111"))
    customers.append(c1)
    
    c2 = Customer("Bob Smith", "bob@email.com", "9123456789")
    c2.add_account(SavingsAccount("Bob Smith", 30000, "2222"))
    customers.append(c2)
    
    print("=" * 55)
    print("   BANKING MANAGEMENT SYSTEM")
    print("=" * 55)
    
    while True:
        print("\n--- MAIN MENU ---")
        print("  1. View All Customers")
        print("  2. Create Customer")
        print("  3. Open Account")
        print("  4. Deposit")
        print("  5. Withdraw")
        print("  6. Transfer")
        print("  7. Account Statement")
        print("  8. Customer Summary")
        print("  9. Apply Interest (Savings)")
        print("  0. Exit")
        
        choice = input("  Choice: ").strip()
        
        try:
            if choice == "1":
                if not customers:
                    print("\n  No customers.")
                else:
                    print(f"\n  {'ID':<8} {'Name':<20} {'Email':<22} {'Accounts':>8} {'Balance':>12}")
                    print(f"  {'-'*72}")
                    for c in customers:
                        print(f"  {c.customer_id:<8} {c.name:<20} {c.email:<22} "
                              f"{len(c.active_accounts()):>8} ₹{c.total_balance():>10,.2f}")
            
            elif choice == "2":
                name = input("  Name: ").strip().title()
                email = input("  Email: ").strip().lower()
                phone = input("  Phone: ").strip()
                c = Customer(name, email, phone)
                customers.append(c)
                print(f"  ✅ Customer created: {c.customer_id}")
            
            elif choice == "3":
                cid = input("  Customer ID: ").strip().upper()
                customer = next((c for c in customers if c.customer_id == cid), None)
                if not customer:
                    print("  Customer not found.")
                    continue
                
                print("  Account Types:")
                print("    1. Savings (Min ₹1,000)")
                print("    2. Current (Overdraft ₹10,000)")
                acc_type = input("  Select type: ").strip()
                
                balance = float(input("  Initial deposit (₹): "))
                pin = input("  Set 4-digit PIN: ").strip()
                
                if acc_type == "1":
                    acc = SavingsAccount(customer.name, balance, pin)
                elif acc_type == "2":
                    acc = CurrentAccount(customer.name, balance, pin)
                else:
                    print("  Invalid type.")
                    continue
                
                customer.add_account(acc)
                print(f"  ✅ Account opened: {acc.account_no} ({acc.account_type})")
            
            elif choice == "4":
                acc_no = input("  Account No: ").strip().upper()
                acc = _find_account(customers, acc_no)
                if not acc:
                    print("  Account not found.")
                    continue
                amount = float(input("  Amount (₹): "))
                new_bal = acc.deposit(amount)
                print(f"  ✅ Deposited. New balance: ₹{new_bal:,.2f}")
            
            elif choice == "5":
                acc_no = input("  Account No: ").strip().upper()
                acc = _find_account(customers, acc_no)
                if not acc:
                    print("  Account not found.")
                    continue
                amount = float(input("  Amount (₹): "))
                pin = input("  PIN: ").strip()
                new_bal = acc.withdraw(amount, pin)
                print(f"  ✅ Withdrawn. New balance: ₹{new_bal:,.2f}")
            
            elif choice == "6":
                from_no = input("  From Account: ").strip().upper()
                to_no = input("  To Account: ").strip().upper()
                from_acc = _find_account(customers, from_no)
                to_acc = _find_account(customers, to_no)
                if not from_acc or not to_acc:
                    print("  Account not found.")
                    continue
                amount = float(input("  Amount (₹): "))
                pin = input("  From Account PIN: ").strip()
                record = txn_service.transfer(from_acc, to_acc, amount, pin)
                print(f"  ✅ Transferred ₹{amount:,.2f}: {from_no} → {to_no}")
            
            elif choice == "7":
                acc_no = input("  Account No: ").strip().upper()
                acc = _find_account(customers, acc_no)
                if not acc:
                    print("  Account not found.")
                    continue
                pin = input("  PIN: ").strip()
                print(ReportService.account_statement(acc, pin))
            
            elif choice == "8":
                cid = input("  Customer ID: ").strip().upper()
                customer = next((c for c in customers if c.customer_id == cid), None)
                if not customer:
                    print("  Customer not found.")
                    continue
                print(ReportService.customer_summary(customer))
            
            elif choice == "9":
                for c in customers:
                    for acc in c.accounts:
                        if isinstance(acc, SavingsAccount) and acc.is_active:
                            interest = acc.apply_interest()
                            print(f"  {acc.account_no} ({acc.owner}): +₹{interest:,.2f} interest")
                print("  ✅ Interest applied to all savings accounts.")
            
            elif choice == "0":
                print("\n  Thank you for banking with us! Goodbye!")
                break
            
            else:
                print("  Invalid choice.")
        
        except (ValueError, PermissionError, RuntimeError) as e:
            print(f"  ❌ Error: {e}")
        except Exception as e:
            print(f"  ❌ Unexpected error: {e}")
            logger.exception("Unhandled error")

def _find_account(customers, account_no):
    """Find account across all customers."""
    for c in customers:
        acc = c.get_account(account_no)
        if acc:
            return acc
    return None

if __name__ == "__main__":
    main()
```

---

## 25.7 Concepts Applied — Module 5 Recap

| Concept | Where Used | Session |
|---------|-----------|---------|
| Classes & Objects | Account, Customer, Services | Session 21 |
| `__init__`, `self`, properties | All classes | Session 21 |
| Dunder methods (`__str__`) | All model classes | Session 21 |
| Inheritance | SavingsAccount, CurrentAccount from Account | Session 22 |
| `super()` | Child constructors and method overrides | Session 22 |
| Method overriding | `withdraw()`, `calculate_interest()` | Session 22 |
| Polymorphism | Same interface for all account types | Session 22 |
| Abstract Base Class (ABC) | Account base class | Session 23 |
| Encapsulation (`__pin`, `_balance`) | Private/protected attributes | Session 23 |
| `@property` | balance, account_type, available_balance | Session 23 |
| Project structure | models, services, utils separation | Session 24 |
| Composition | Customer has Accounts | Session 24 |

---

## 25.8 Evaluation Rubric

| Criterion | Points |
|-----------|--------|
| Account hierarchy (ABC + 2 types) | 15 |
| Customer class with multiple accounts | 10 |
| Deposit, withdraw with PIN validation | 15 |
| Transfer between accounts | 10 |
| Encapsulation (private balance, PIN) | 10 |
| Account statement generation | 10 |
| Customer summary report | 5 |
| Interest calculation (savings) | 5 |
| Menu-driven with error handling | 10 |
| Code structure (classes, methods, separation) | 10 |
| **Total** | **100** |

---

## 🔧 Hands-On Activity: Build the Banking Management System

**Duration:** 40 minutes

Follow the design and code from Sections 25.3–25.6. Save as `session25_banking.py`.

### Bonus Challenges

1. **Data persistence:** Save accounts to CSV and reload on startup
2. **Fixed Deposit account:** No withdrawals until maturity date, higher interest
3. **Transaction limits:** Daily withdrawal limit per account type
4. **Account closure:** Close account and transfer remaining balance

---

## Session 25 — Key Takeaways

1. **Abstract Base Classes** define contracts for account types — ensures consistency
2. **Inheritance** enables code reuse across Savings and Current accounts
3. **Encapsulation** with private PIN and protected balance prevents unauthorized access
4. **Polymorphism** lets the main program treat all account types uniformly
5. **Composition** models "Customer has Accounts" — a real-world relationship

---

## Module 5 Complete — Summary

| Session | Topic | Key Skill |
|---------|-------|-----------|
| 21 | Classes & Objects | class, __init__, self, properties, dunder methods |
| 22 | Inheritance & Polymorphism | super(), overriding, MRO, duck typing |
| 23 | Encapsulation & Abstraction | Access modifiers, ABC, @property, interfaces |
| 24 | Packages & Project Structure | __init__.py, imports, venv, project layout |
| 25 | Banking System | End-to-end OOP project with full class hierarchy |

### Module 5 → Module 6 Bridge

You've mastered **Object-Oriented Programming** and can design, build, and organize complex Python applications. In Module 6 (Sessions 26–30), you'll learn **Automation & Capstone** — working with APIs, automating tasks, and building your final capstone project with PDF report generation.

---

## Preparation for Session 26
- Think about: What is an API? How do websites get data from servers?
- Review: What is HTTP? What are GET and POST requests?
- Install: `pip install requests`

---

*Session 25 of 30 | Module 5: Object-Oriented Programming*
*Professional Python Programming Certification — UpSkill Global Education Technologies Inc., Canada*
