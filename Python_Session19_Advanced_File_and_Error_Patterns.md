# Session 19 — Advanced File & Error Patterns
## Module 4: File Handling & Exception Handling | Professional Python Programming Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Build a Robust Data Processing Pipeline

---

## Learning Objectives
By the end of this session, you will be able to:
1. Combine file handling with exception handling for robust I/O
2. Work with multiple file formats (text, CSV, JSON)
3. Implement logging for production-quality applications
4. Build data processing pipelines with error recovery
5. Use context managers and decorators for clean resource management

---

## 19.1 Robust File I/O Patterns

### Pattern 1: Safe Read-Process-Write Pipeline

```python
import csv
import os

def process_csv(input_file, output_file):
    """Read CSV, process data, write results — with full error handling."""
    try:
        # Validate input file
        if not os.path.exists(input_file):
            raise FileNotFoundError(f"Input file '{input_file}' not found")
        
        # Read
        with open(input_file, "r", encoding="utf-8") as f:
            reader = csv.DictReader(f)
            data = list(reader)
        
        if not data:
            print("Warning: File is empty.")
            return 0
        
        # Process (example: add calculated column)
        for row in data:
            try:
                row["Total"] = str(float(row.get("Price", 0)) * int(row.get("Qty", 0)))
            except (ValueError, TypeError):
                row["Total"] = "0"
        
        # Write
        fieldnames = list(data[0].keys())
        with open(output_file, "w", newline="", encoding="utf-8") as f:
            writer = csv.DictWriter(f, fieldnames=fieldnames)
            writer.writeheader()
            writer.writerows(data)
        
        print(f"Processed {len(data)} records → {output_file}")
        return len(data)
    
    except FileNotFoundError as e:
        print(f"File Error: {e}")
        return -1
    except PermissionError:
        print(f"Permission denied for '{input_file}' or '{output_file}'")
        return -1
    except csv.Error as e:
        print(f"CSV Error: {e}")
        return -1
    except Exception as e:
        print(f"Unexpected error: {type(e).__name__}: {e}")
        return -1
```

### Pattern 2: Backup Before Overwrite

```python
import shutil
from datetime import datetime

def safe_overwrite(filename, new_content):
    """Create backup before overwriting a file."""
    if os.path.exists(filename):
        # Create backup
        timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
        backup = f"{filename}.backup_{timestamp}"
        shutil.copy2(filename, backup)
        print(f"Backup created: {backup}")
    
    try:
        with open(filename, "w") as f:
            f.write(new_content)
        print(f"File '{filename}' updated successfully.")
    except Exception as e:
        # Restore from backup
        if os.path.exists(backup):
            shutil.copy2(backup, filename)
            print(f"Error occurred. Restored from backup.")
        raise
```

### Pattern 3: Process Large Files in Chunks

```python
def process_large_file(filename, chunk_size=1000):
    """Process a large file line by line without loading entirely into memory."""
    line_count = 0
    error_count = 0
    
    try:
        with open(filename, "r", encoding="utf-8") as f:
            batch = []
            for line_num, line in enumerate(f, 1):
                try:
                    processed = line.strip().upper()
                    batch.append(processed)
                    line_count += 1
                    
                    if len(batch) >= chunk_size:
                        save_batch(batch, line_num)
                        batch = []
                
                except Exception as e:
                    error_count += 1
                    print(f"  Error on line {line_num}: {e}")
                    continue  # Skip bad lines, continue processing
            
            # Process remaining batch
            if batch:
                save_batch(batch, line_num)
    
    except FileNotFoundError:
        print(f"File '{filename}' not found.")
        return
    
    print(f"Processed: {line_count} lines, Errors: {error_count}")

def save_batch(batch, end_line):
    """Save a batch of processed lines."""
    print(f"  Saved batch ending at line {end_line} ({len(batch)} lines)")
```

---

## 19.2 Logging Module

### Why Logging?

`print()` is fine for development, but production apps need **structured logging** — with timestamps, severity levels, and file output.

### Basic Logging Setup

```python
import logging

# Configure logging
logging.basicConfig(
    level=logging.DEBUG,
    format="%(asctime)s | %(levelname)-8s | %(message)s",
    datefmt="%Y-%m-%d %H:%M:%S",
    handlers=[
        logging.FileHandler("app.log"),       # Log to file
        logging.StreamHandler()                # Also print to console
    ]
)

logger = logging.getLogger(__name__)
```

### Logging Levels

| Level | Value | Use For |
|-------|-------|---------|
| `DEBUG` | 10 | Detailed diagnostic info (development) |
| `INFO` | 20 | General operational messages |
| `WARNING` | 30 | Something unexpected but not critical |
| `ERROR` | 40 | An operation failed |
| `CRITICAL` | 50 | System-level failure |

### Using the Logger

```python
logger.debug("Starting data processing...")
logger.info("Connected to database successfully")
logger.warning("Configuration file not found — using defaults")
logger.error("Failed to save file: Permission denied")
logger.critical("Application cannot continue — exiting")

# Log with exception info
try:
    result = 10 / 0
except ZeroDivisionError:
    logger.exception("Division error occurred")  # Includes traceback
```

### Logging in File Operations

```python
import logging
import csv

logging.basicConfig(level=logging.INFO, format="%(asctime)s | %(levelname)s | %(message)s")
logger = logging.getLogger("DataProcessor")

def process_data(input_file, output_file):
    logger.info(f"Starting processing: {input_file}")
    
    try:
        with open(input_file, "r") as f:
            reader = csv.DictReader(f)
            data = list(reader)
        logger.info(f"Read {len(data)} records from {input_file}")
    except FileNotFoundError:
        logger.error(f"Input file not found: {input_file}")
        return False
    
    # Process
    processed = 0
    errors = 0
    for i, row in enumerate(data):
        try:
            row["processed"] = "yes"
            processed += 1
        except Exception as e:
            errors += 1
            logger.warning(f"Error processing row {i}: {e}")
    
    # Write
    try:
        fieldnames = list(data[0].keys())
        with open(output_file, "w", newline="") as f:
            writer = csv.DictWriter(f, fieldnames=fieldnames)
            writer.writeheader()
            writer.writerows(data)
        logger.info(f"Wrote {processed} records to {output_file} ({errors} errors)")
    except Exception as e:
        logger.error(f"Failed to write output: {e}")
        return False
    
    return True
```

---

## 19.3 Working with Multiple File Formats

### Reading Config from JSON, Data from CSV

```python
import json
import csv

def load_config(config_file="config.json"):
    """Load application configuration from JSON."""
    defaults = {
        "input_dir": "data",
        "output_dir": "output",
        "min_stock": 10,
        "tax_rate": 0.18,
    }
    try:
        with open(config_file, "r") as f:
            config = json.load(f)
        return {**defaults, **config}  # Merge with defaults
    except FileNotFoundError:
        print(f"Config not found. Using defaults.")
        return defaults
    except json.JSONDecodeError as e:
        print(f"Invalid JSON in config: {e}. Using defaults.")
        return defaults

def load_data(csv_file):
    """Load data from CSV."""
    try:
        with open(csv_file, "r", encoding="utf-8") as f:
            return list(csv.DictReader(f))
    except FileNotFoundError:
        print(f"Data file '{csv_file}' not found.")
        return []

def save_report(data, json_file):
    """Save report as JSON."""
    try:
        with open(json_file, "w") as f:
            json.dump(data, f, indent=4)
        print(f"Report saved to {json_file}")
    except Exception as e:
        print(f"Error saving report: {e}")
```

### Converting Between Formats

```python
import csv
import json

# CSV to JSON
def csv_to_json(csv_file, json_file):
    with open(csv_file, "r") as f:
        data = list(csv.DictReader(f))
    with open(json_file, "w") as f:
        json.dump(data, f, indent=4)

# JSON to CSV
def json_to_csv(json_file, csv_file):
    with open(json_file, "r") as f:
        data = json.load(f)
    if data:
        with open(csv_file, "w", newline="") as f:
            writer = csv.DictWriter(f, fieldnames=data[0].keys())
            writer.writeheader()
            writer.writerows(data)
```

---

## 19.4 Context Managers — Advanced

### Custom Context Manager with Class

```python
class FileProcessor:
    """Context manager for file processing with logging."""
    
    def __init__(self, filename, mode="r"):
        self.filename = filename
        self.mode = mode
        self.file = None
    
    def __enter__(self):
        print(f"Opening '{self.filename}'...")
        self.file = open(self.filename, self.mode)
        return self.file
    
    def __exit__(self, exc_type, exc_val, exc_tb):
        if self.file:
            self.file.close()
            print(f"Closed '{self.filename}'.")
        if exc_type:
            print(f"Error occurred: {exc_type.__name__}: {exc_val}")
        return False  # Don't suppress the exception

# Usage
with FileProcessor("data.txt", "w") as f:
    f.write("Hello from context manager!")
```

### Custom Context Manager with contextlib

```python
from contextlib import contextmanager

@contextmanager
def managed_file(filename, mode="r"):
    """Simple context manager using decorator."""
    f = None
    try:
        f = open(filename, mode)
        print(f"Opened: {filename}")
        yield f
    except FileNotFoundError:
        print(f"File not found: {filename}")
        yield None
    finally:
        if f:
            f.close()
            print(f"Closed: {filename}")

# Usage
with managed_file("data.txt") as f:
    if f:
        content = f.read()
```

### Timer Context Manager

```python
import time
from contextlib import contextmanager

@contextmanager
def timer(label="Operation"):
    start = time.time()
    try:
        yield
    finally:
        elapsed = time.time() - start
        print(f"{label}: {elapsed:.4f} seconds")

# Usage
with timer("File Processing"):
    with open("large_file.txt", "r") as f:
        lines = f.readlines()
    print(f"Read {len(lines)} lines")
```

---

## 19.5 Decorators for Error Handling

### Retry Decorator

```python
import time

def retry(max_attempts=3, delay=1):
    """Decorator that retries a function on failure."""
    def decorator(func):
        def wrapper(*args, **kwargs):
            for attempt in range(1, max_attempts + 1):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    print(f"Attempt {attempt}/{max_attempts} failed: {e}")
                    if attempt < max_attempts:
                        time.sleep(delay)
            print(f"All {max_attempts} attempts failed.")
            return None
        return wrapper
    return decorator

@retry(max_attempts=3, delay=0.5)
def fetch_data(url):
    """Simulate fetching data that might fail."""
    import random
    if random.random() < 0.7:  # 70% chance of failure
        raise ConnectionError("Network timeout")
    return {"status": "success", "data": [1, 2, 3]}

result = fetch_data("https://api.example.com")
```

### Error Logging Decorator

```python
import functools
import logging

def log_errors(logger=None):
    """Decorator that logs any exceptions from the function."""
    if logger is None:
        logger = logging.getLogger(__name__)
    
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            try:
                return func(*args, **kwargs)
            except Exception as e:
                logger.exception(f"Error in {func.__name__}: {e}")
                raise
        return wrapper
    return decorator

@log_errors()
def divide(a, b):
    return a / b
```

---

## 19.6 Data Validation Functions

### Comprehensive Validation Module

```python
def validate_required(value, field_name):
    """Check that a value is not empty."""
    if value is None or (isinstance(value, str) and not value.strip()):
        raise ValueError(f"{field_name} is required")
    return value

def validate_range(value, field_name, min_val=None, max_val=None):
    """Validate that a number is within range."""
    num = float(value)
    if min_val is not None and num < min_val:
        raise ValueError(f"{field_name} must be >= {min_val} (got {num})")
    if max_val is not None and num > max_val:
        raise ValueError(f"{field_name} must be <= {max_val} (got {num})")
    return num

def validate_type(value, field_name, expected_type):
    """Validate that a value can be converted to expected type."""
    try:
        if expected_type == int:
            return int(value)
        elif expected_type == float:
            return float(value)
        elif expected_type == bool:
            return str(value).lower() in ("true", "1", "yes")
        return expected_type(value)
    except (ValueError, TypeError):
        raise ValueError(f"{field_name} must be {expected_type.__name__} (got '{value}')")

def validate_record(record, schema):
    """Validate a data record against a schema."""
    errors = []
    clean = {}
    
    for field, rules in schema.items():
        value = record.get(field, "")
        try:
            if rules.get("required"):
                validate_required(value, field)
            if value and "type" in rules:
                value = validate_type(value, field, rules["type"])
            if value and "min" in rules:
                validate_range(value, field, min_val=rules["min"])
            if value and "max" in rules:
                validate_range(value, field, max_val=rules["max"])
            clean[field] = value
        except ValueError as e:
            errors.append(str(e))
    
    return clean, errors

# Usage
schema = {
    "name": {"required": True, "type": str},
    "age": {"required": True, "type": int, "min": 1, "max": 150},
    "salary": {"required": False, "type": float, "min": 0},
}

record = {"name": "Alice", "age": "25", "salary": "75000"}
clean, errors = validate_record(record, schema)
print(f"Clean: {clean}")  # {'name': 'Alice', 'age': 25, 'salary': 75000.0}
print(f"Errors: {errors}") # []
```

---

## 🔧 Hands-On Activity: Data Processing Pipeline

**Duration:** 25 minutes

Create a file `session19_pipeline.py`:

```python
# Session 19 — Data Processing Pipeline
import csv
import json
import os
import logging
from datetime import datetime

# Setup logging
logging.basicConfig(
    level=logging.INFO,
    format="%(asctime)s | %(levelname)-8s | %(message)s",
    datefmt="%H:%M:%S"
)
logger = logging.getLogger("Pipeline")

# Step 1: Create sample data
def create_sample_data():
    data = [
        {"name": "Alice", "dept": "Engineering", "salary": "85000", "rating": "4.5"},
        {"name": "Bob", "dept": "Marketing", "salary": "invalid", "rating": "3.8"},
        {"name": "Charlie", "dept": "Engineering", "salary": "90000", "rating": "4.2"},
        {"name": "", "dept": "HR", "salary": "55000", "rating": "4.0"},
        {"name": "Diana", "dept": "HR", "salary": "60000", "rating": "abc"},
        {"name": "Eve", "dept": "Engineering", "salary": "95000", "rating": "4.8"},
    ]
    with open("employees_raw.csv", "w", newline="") as f:
        writer = csv.DictWriter(f, fieldnames=data[0].keys())
        writer.writeheader()
        writer.writerows(data)
    logger.info("Sample data created: employees_raw.csv")

# Step 2: Read and validate
def read_and_validate(filename):
    valid = []
    invalid = []
    
    try:
        with open(filename, "r") as f:
            reader = csv.DictReader(f)
            for i, row in enumerate(reader, 1):
                errors = []
                if not row.get("name", "").strip():
                    errors.append("name is empty")
                try:
                    row["salary"] = float(row["salary"])
                except ValueError:
                    errors.append(f"invalid salary: {row['salary']}")
                try:
                    row["rating"] = float(row["rating"])
                except ValueError:
                    errors.append(f"invalid rating: {row['rating']}")
                
                if errors:
                    invalid.append({"row": i, "data": row, "errors": errors})
                    logger.warning(f"Row {i} invalid: {', '.join(errors)}")
                else:
                    valid.append(row)
    except FileNotFoundError:
        logger.error(f"File not found: {filename}")
        return [], []
    
    logger.info(f"Validation: {len(valid)} valid, {len(invalid)} invalid")
    return valid, invalid

# Step 3: Process (add calculated fields)
def process_data(data):
    for row in data:
        row["annual_salary"] = row["salary"] * 12
        row["tax"] = row["annual_salary"] * (0.20 if row["annual_salary"] > 1000000 else 0.10)
        row["net_annual"] = row["annual_salary"] - row["tax"]
        row["performance"] = "High" if row["rating"] >= 4.5 else "Mid" if row["rating"] >= 3.5 else "Low"
    logger.info(f"Processed {len(data)} records")
    return data

# Step 4: Generate report
def generate_report(data, report_file):
    report = {
        "generated": datetime.now().strftime("%Y-%m-%d %H:%M:%S"),
        "total_employees": len(data),
        "avg_salary": sum(r["salary"] for r in data) / len(data) if data else 0,
        "avg_rating": sum(r["rating"] for r in data) / len(data) if data else 0,
        "by_dept": {},
        "by_performance": {},
    }
    
    for row in data:
        dept = row["dept"]
        if dept not in report["by_dept"]:
            report["by_dept"][dept] = {"count": 0, "total_salary": 0}
        report["by_dept"][dept]["count"] += 1
        report["by_dept"][dept]["total_salary"] += row["salary"]
        
        perf = row["performance"]
        report["by_performance"][perf] = report["by_performance"].get(perf, 0) + 1
    
    with open(report_file, "w") as f:
        json.dump(report, f, indent=4)
    logger.info(f"Report saved: {report_file}")
    return report

# Step 5: Display summary
def display_summary(report):
    print(f"\n{'=' * 50}")
    print(f"  EMPLOYEE DATA REPORT")
    print(f"  Generated: {report['generated']}")
    print(f"{'=' * 50}")
    print(f"  Total Employees : {report['total_employees']}")
    print(f"  Avg Salary      : ₹{report['avg_salary']:,.2f}")
    print(f"  Avg Rating      : {report['avg_rating']:.2f}")
    print(f"\n  By Department:")
    for dept, info in report["by_dept"].items():
        avg = info["total_salary"] / info["count"]
        print(f"    {dept:<15}: {info['count']} employees, Avg ₹{avg:,.0f}")
    print(f"\n  By Performance:")
    for perf, count in report["by_performance"].items():
        print(f"    {perf:<8}: {count}")
    print(f"{'=' * 50}")

# Run Pipeline
if __name__ == "__main__":
    logger.info("=== Pipeline Started ===")
    create_sample_data()
    valid, invalid = read_and_validate("employees_raw.csv")
    if valid:
        processed = process_data(valid)
        report = generate_report(processed, "report.json")
        display_summary(report)
    logger.info("=== Pipeline Complete ===")
```

---

## Session 19 — Key Takeaways

1. **Combine** file handling + exception handling for production-quality I/O
2. **Logging module** replaces `print()` in real applications — supports levels, files, timestamps
3. **Backup before overwrite** — protect data from corruption
4. **Validate data early** — catch bad records before processing
5. **Context managers** (`with` + custom) ensure proper resource cleanup
6. **Decorators** like `@retry` add cross-cutting error handling to any function

---

## Preparation for Session 20
- Review all Module 4 concepts: file I/O, CSV, JSON, exceptions, logging
- Think about: How would you build an expense tracker that saves data to files?
- Be ready to code: Session 20 is the Module 4 project — Expense Management System

---

*Session 19 of 30 | Module 4: File Handling & Exception Handling*
*Professional Python Programming Certification — UpSkill Global Education Technologies Inc., Canada*
