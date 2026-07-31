# Session 15 — Inventory Management System (Module 3 Project)
## Module 3: Data Structures | Professional Python Programming Certification
### Duration: 1 Hour | Type: Hands-On Project | Project: Build an Inventory Management System

---

## Learning Objectives
By the end of this session, you will be able to:
1. Apply lists, tuples, dictionaries, sets, and strings in a real-world project
2. Build a CRUD (Create, Read, Update, Delete) application
3. Implement search, filter, and reporting features
4. Structure data using dictionaries and lists of dictionaries
5. Generate formatted inventory reports

---

## 15.1 Project Overview

### The Brief

> Build an **Inventory Management System** for a retail store that allows the user to add, view, search, update, and delete products, track stock levels, and generate reports.

### Features

| Feature | Data Structures Used |
|---------|---------------------|
| Product catalog | List of dictionaries |
| Add/Update/Delete products | Dictionary operations |
| Search by name/category | String methods, list filtering |
| Category management | Sets (unique categories) |
| Stock alerts (low stock) | List comprehension, filtering |
| Sales recording | Tuples (immutable transaction records) |
| Inventory report | Formatted string output, aggregation |
| Price history | List of tuples per product |

---

## 15.2 Data Model

### Product Structure (Dictionary)

```python
product = {
    "id": "PRD001",
    "name": "Wireless Mouse",
    "category": "Electronics",
    "price": 599.00,
    "quantity": 45,
    "min_stock": 10,
    "supplier": "TechCorp",
}
```

### Inventory (List of Dictionaries)

```python
inventory = [
    {"id": "PRD001", "name": "Wireless Mouse", "category": "Electronics", "price": 599.00, "quantity": 45, "min_stock": 10, "supplier": "TechCorp"},
    {"id": "PRD002", "name": "USB Keyboard", "category": "Electronics", "price": 899.00, "quantity": 30, "min_stock": 5, "supplier": "TechCorp"},
    {"id": "PRD003", "name": "Notebook A4", "category": "Stationery", "price": 50.00, "quantity": 200, "min_stock": 50, "supplier": "PaperWorld"},
    {"id": "PRD004", "name": "Ballpoint Pen", "category": "Stationery", "price": 15.00, "quantity": 500, "min_stock": 100, "supplier": "PaperWorld"},
    {"id": "PRD005", "name": "Office Chair", "category": "Furniture", "price": 5500.00, "quantity": 8, "min_stock": 3, "supplier": "FurniPro"},
]
```

### Sales Log (List of Tuples)

```python
sales_log = []
# Each sale: (product_id, product_name, quantity_sold, sale_price, timestamp)
```

---

## 15.3 Function Design

```python
def generate_id(inventory):
    """Generate next product ID like PRD006."""

def add_product(inventory):
    """Add a new product to inventory."""

def view_all(inventory):
    """Display all products in a formatted table."""

def search_products(inventory, query):
    """Search by name or category (case-insensitive)."""

def update_product(inventory, product_id):
    """Update price, quantity, or other fields."""

def delete_product(inventory, product_id):
    """Remove a product from inventory."""

def record_sale(inventory, sales_log, product_id, qty):
    """Record a sale and reduce stock."""

def low_stock_alert(inventory):
    """Show products below minimum stock level."""

def category_report(inventory):
    """Show summary by category."""

def inventory_report(inventory, sales_log):
    """Generate full inventory report."""

def get_categories(inventory):
    """Return set of unique categories."""
```

---

## 15.4 Step-by-Step Build Guide

### Step 1: Utility Functions

```python
from datetime import datetime

def generate_id(inventory):
    """Generate next product ID."""
    if not inventory:
        return "PRD001"
    max_id = max(int(p["id"][3:]) for p in inventory)
    return f"PRD{max_id + 1:03d}"

def find_product(inventory, product_id):
    """Find product by ID. Returns product dict or None."""
    for product in inventory:
        if product["id"] == product_id.upper():
            return product
    return None

def get_valid_float(prompt):
    """Get a valid positive float."""
    while True:
        try:
            value = float(input(prompt))
            if value >= 0:
                return value
            print("  Value must be non-negative.")
        except ValueError:
            print("  Invalid number.")

def get_valid_int(prompt):
    """Get a valid non-negative integer."""
    while True:
        try:
            value = int(input(prompt))
            if value >= 0:
                return value
            print("  Value must be non-negative.")
        except ValueError:
            print("  Invalid number.")
```

### Step 2: CRUD Operations

```python
def add_product(inventory):
    """Add a new product."""
    print("\n--- Add New Product ---")
    product_id = generate_id(inventory)
    name = input("  Product Name: ").strip().title()
    category = input("  Category: ").strip().title()
    price = get_valid_float("  Price (₹): ")
    quantity = get_valid_int("  Quantity: ")
    min_stock = get_valid_int("  Min Stock Level: ")
    supplier = input("  Supplier: ").strip().title()
    
    product = {
        "id": product_id,
        "name": name,
        "category": category,
        "price": price,
        "quantity": quantity,
        "min_stock": min_stock,
        "supplier": supplier,
    }
    inventory.append(product)
    print(f"  ✅ Product '{name}' added with ID: {product_id}")

def view_all(inventory):
    """Display all products."""
    if not inventory:
        print("\n  Inventory is empty.")
        return
    print(f"\n  {'ID':<8} {'Name':<20} {'Category':<14} {'Price':>8} {'Qty':>5} {'Stock':>6}")
    print(f"  {'-'*65}")
    for p in inventory:
        status = "⚠ LOW" if p["quantity"] <= p["min_stock"] else "OK"
        print(f"  {p['id']:<8} {p['name']:<20} {p['category']:<14} "
              f"₹{p['price']:>7,.2f} {p['quantity']:>5} {status:>6}")
    print(f"\n  Total Products: {len(inventory)}")
    total_value = sum(p["price"] * p["quantity"] for p in inventory)
    print(f"  Total Inventory Value: ₹{total_value:,.2f}")

def update_product(inventory):
    """Update an existing product."""
    product_id = input("\n  Enter Product ID: ").strip().upper()
    product = find_product(inventory, product_id)
    if not product:
        print(f"  Product '{product_id}' not found.")
        return
    
    print(f"\n  Current: {product['name']} | ₹{product['price']:.2f} | Qty: {product['quantity']}")
    print("  Leave blank to keep current value.")
    
    name = input(f"  Name [{product['name']}]: ").strip()
    price = input(f"  Price [{product['price']}]: ").strip()
    quantity = input(f"  Quantity [{product['quantity']}]: ").strip()
    
    if name:
        product["name"] = name.title()
    if price:
        product["price"] = float(price)
    if quantity:
        product["quantity"] = int(quantity)
    
    print(f"  ✅ Product {product_id} updated!")

def delete_product(inventory):
    """Delete a product."""
    product_id = input("\n  Enter Product ID to delete: ").strip().upper()
    product = find_product(inventory, product_id)
    if not product:
        print(f"  Product '{product_id}' not found.")
        return
    
    confirm = input(f"  Delete '{product['name']}'? (yes/no): ").strip().lower()
    if confirm in ("y", "yes"):
        inventory.remove(product)
        print(f"  ✅ Product '{product['name']}' deleted!")
    else:
        print("  Cancelled.")
```

### Step 3: Search & Filter

```python
def search_products(inventory):
    """Search by name or category."""
    query = input("\n  Search query: ").strip().lower()
    results = [p for p in inventory 
               if query in p["name"].lower() or query in p["category"].lower()]
    
    if not results:
        print(f"  No products matching '{query}'.")
        return
    
    print(f"\n  Found {len(results)} result(s):")
    for p in results:
        print(f"  {p['id']} | {p['name']:<20} | {p['category']} | ₹{p['price']:,.2f} | Qty: {p['quantity']}")

def low_stock_alert(inventory):
    """Show products below minimum stock."""
    low = [p for p in inventory if p["quantity"] <= p["min_stock"]]
    
    if not low:
        print("\n  ✅ All products are adequately stocked.")
        return
    
    print(f"\n  ⚠ LOW STOCK ALERT — {len(low)} product(s):")
    print(f"  {'ID':<8} {'Name':<20} {'Current':>8} {'Minimum':>8} {'Deficit':>8}")
    print(f"  {'-'*55}")
    for p in low:
        deficit = p["min_stock"] - p["quantity"]
        print(f"  {p['id']:<8} {p['name']:<20} {p['quantity']:>8} {p['min_stock']:>8} {deficit:>8}")
```

### Step 4: Sales Recording

```python
def record_sale(inventory, sales_log):
    """Record a sale transaction."""
    product_id = input("\n  Product ID: ").strip().upper()
    product = find_product(inventory, product_id)
    if not product:
        print(f"  Product '{product_id}' not found.")
        return
    
    print(f"  Product: {product['name']} | Available: {product['quantity']} | Price: ₹{product['price']:.2f}")
    qty = get_valid_int("  Quantity to sell: ")
    
    if qty > product["quantity"]:
        print(f"  ❌ Insufficient stock! Only {product['quantity']} available.")
        return
    
    total = product["price"] * qty
    product["quantity"] -= qty
    
    sale = (product["id"], product["name"], qty, total, datetime.now().strftime("%Y-%m-%d %H:%M"))
    sales_log.append(sale)
    
    print(f"  ✅ Sale recorded: {qty} x {product['name']} = ₹{total:,.2f}")
    if product["quantity"] <= product["min_stock"]:
        print(f"  ⚠ Warning: Stock is now LOW ({product['quantity']} remaining)")
```

### Step 5: Reports

```python
def category_report(inventory):
    """Summary by category."""
    categories = set(p["category"] for p in inventory)
    
    print(f"\n  {'Category':<15} {'Products':>9} {'Total Qty':>10} {'Total Value':>14}")
    print(f"  {'-'*50}")
    
    grand_total = 0
    for cat in sorted(categories):
        products = [p for p in inventory if p["category"] == cat]
        count = len(products)
        total_qty = sum(p["quantity"] for p in products)
        total_val = sum(p["price"] * p["quantity"] for p in products)
        grand_total += total_val
        print(f"  {cat:<15} {count:>9} {total_qty:>10} ₹{total_val:>12,.2f}")
    
    print(f"  {'-'*50}")
    print(f"  {'TOTAL':<15} {len(inventory):>9} {'':<10} ₹{grand_total:>12,.2f}")

def sales_report(sales_log):
    """Display sales history."""
    if not sales_log:
        print("\n  No sales recorded yet.")
        return
    
    print(f"\n  {'Date':<18} {'Product':<20} {'Qty':>5} {'Amount':>12}")
    print(f"  {'-'*58}")
    total_sales = 0
    for sale in sales_log:
        pid, name, qty, amount, timestamp = sale
        print(f"  {timestamp:<18} {name:<20} {qty:>5} ₹{amount:>10,.2f}")
        total_sales += amount
    print(f"  {'-'*58}")
    print(f"  {'TOTAL SALES':<45} ₹{total_sales:>10,.2f}")
```

### Step 6: Main Menu

```python
def main():
    # Pre-loaded inventory
    inventory = [
        {"id": "PRD001", "name": "Wireless Mouse", "category": "Electronics", "price": 599.00, "quantity": 45, "min_stock": 10, "supplier": "TechCorp"},
        {"id": "PRD002", "name": "USB Keyboard", "category": "Electronics", "price": 899.00, "quantity": 30, "min_stock": 5, "supplier": "TechCorp"},
        {"id": "PRD003", "name": "Notebook A4", "category": "Stationery", "price": 50.00, "quantity": 200, "min_stock": 50, "supplier": "PaperWorld"},
        {"id": "PRD004", "name": "Ballpoint Pen", "category": "Stationery", "price": 15.00, "quantity": 500, "min_stock": 100, "supplier": "PaperWorld"},
        {"id": "PRD005", "name": "Office Chair", "category": "Furniture", "price": 5500.00, "quantity": 8, "min_stock": 3, "supplier": "FurniPro"},
    ]
    sales_log = []
    
    print("=" * 50)
    print("   INVENTORY MANAGEMENT SYSTEM")
    print("=" * 50)
    
    while True:
        print("\n--- MAIN MENU ---")
        print("  1. View All Products")
        print("  2. Add Product")
        print("  3. Update Product")
        print("  4. Delete Product")
        print("  5. Search Products")
        print("  6. Record Sale")
        print("  7. Low Stock Alert")
        print("  8. Category Report")
        print("  9. Sales Report")
        print("  0. Exit")
        
        choice = input("  Choice: ").strip()
        
        if choice == "1":
            view_all(inventory)
        elif choice == "2":
            add_product(inventory)
        elif choice == "3":
            update_product(inventory)
        elif choice == "4":
            delete_product(inventory)
        elif choice == "5":
            search_products(inventory)
        elif choice == "6":
            record_sale(inventory, sales_log)
        elif choice == "7":
            low_stock_alert(inventory)
        elif choice == "8":
            category_report(inventory)
        elif choice == "9":
            sales_report(sales_log)
        elif choice == "0":
            print("\n  Thank you! Goodbye!")
            break
        else:
            print("  Invalid choice.")

if __name__ == "__main__":
    main()
```

---

## 15.5 Concepts Applied — Module 3 Recap

| Concept | Where Used | Session |
|---------|-----------|---------|
| Lists | Inventory collection, search results | Session 11 |
| List comprehensions | Filtering products, low stock | Session 11 |
| Slicing | Display subsets | Session 11 |
| Tuples | Sales log records (immutable) | Session 12 |
| Sets | Unique categories extraction | Session 12 |
| Dictionaries | Product data structure | Session 13 |
| Nested access | `product["name"]` | Session 13 |
| Dict methods | `.get()`, `.items()`, `.pop()` | Session 13 |
| String methods | `.strip()`, `.title()`, `.lower()`, `.upper()` | Session 14 |
| f-string formatting | Report tables, alignment | Session 14 |
| String searching | `in` operator for search | Session 14 |
| `sum()`, `max()`, `min()` | Aggregations in reports | Built-in |

---

## 15.6 Evaluation Rubric

| Criterion | Points |
|-----------|--------|
| View all products (formatted table) | 10 |
| Add product with validation | 10 |
| Update product (partial update) | 10 |
| Delete product with confirmation | 10 |
| Search by name or category | 10 |
| Record sale with stock reduction | 10 |
| Low stock alert | 10 |
| Category report with aggregation | 10 |
| Sales report with total | 10 |
| Code uses functions, clean structure | 10 |
| **Total** | **100** |

---

## 🔧 Hands-On Activity: Build the Inventory Management System

**Duration:** 40 minutes

Follow the Step-by-Step Build Guide (Section 15.4). Save as `session15_inventory.py`.

### Bonus Challenges

1. **Export to text file:** Save inventory report to `inventory_report.txt`
2. **Restock feature:** Increase quantity for an existing product
3. **Price history:** Track price changes as a list of tuples per product
4. **Sort options:** Allow sorting inventory by name, price, or quantity

---

## Session 15 — Key Takeaways

1. **List of dictionaries** is the standard pattern for tabular data in Python
2. **CRUD operations** (Create, Read, Update, Delete) are the foundation of data management
3. **Sets** efficiently extract unique categories from data
4. **Tuples** make great immutable transaction records
5. **List comprehensions** with conditions power search and filter features

---

## Module 3 Complete — Summary

| Session | Topic | Key Skill |
|---------|-------|-----------|
| 11 | Lists | Indexing, slicing, methods, comprehensions, 2D lists |
| 12 | Tuples & Sets | Immutability, unpacking, set operations, uniqueness |
| 13 | Dictionaries | Key-value pairs, nesting, comprehensions, Counter |
| 14 | Strings | Methods, regex intro, formatting, text processing |
| 15 | Inventory System | End-to-end CRUD project with all data structures |

### Module 3 → Module 4 Bridge

You've mastered Python's **core data structures**. In Module 4 (Sessions 16–20), you'll learn **File Handling & Exception Handling** — reading/writing files, CSV processing, error handling — and build an **Expense Management System**.

---

## Preparation for Session 16
- Think about: How do programs save data permanently (beyond program execution)?
- Review: What happens to all your variables when a program ends?
- Practice: Try `open("test.txt", "w")` in Python

---

*Session 15 of 30 | Module 3: Data Structures*
*Professional Python Programming Certification — UpSkill Global Education Technologies Inc., Canada*
