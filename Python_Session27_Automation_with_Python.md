# Session 27 — Automation with Python
## Module 6: Automation & Capstone Project | Professional Python Programming Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Build Automation Scripts

---

## Learning Objectives
By the end of this session, you will be able to:
1. Automate file and folder management tasks
2. Work with Excel files using `openpyxl`
3. Send automated emails using `smtplib`
4. Schedule tasks and automate workflows
5. Build practical automation scripts for everyday tasks

---

## 27.1 Why Automation?

Automation eliminates repetitive, time-consuming manual tasks.

### Common Automation Use Cases

| Category | Examples |
|----------|---------|
| **File Management** | Rename, move, organize, archive files |
| **Data Processing** | Read CSV/Excel, transform, generate reports |
| **Email** | Send bulk emails, alerts, reports |
| **Web** | Download files, scrape data, fill forms |
| **System** | Monitor disk space, clean temp files, backups |
| **Reporting** | Generate PDF/Excel reports on schedule |

### Automation Mindset

```
Manual Process          Automated Process
─────────────          ──────────────────
1. Open folder          1. Run script
2. Find files           2. Done ✅
3. Rename each one
4. Move to archive
5. Update spreadsheet
6. Send email
(30 minutes)            (3 seconds)
```

---

## 27.2 File & Folder Automation

### Bulk File Renaming

```python
import os
from pathlib import Path

def bulk_rename(folder, prefix="file", start=1):
    """Rename all files in a folder with sequential numbering."""
    folder = Path(folder)
    
    if not folder.exists():
        print(f"Folder not found: {folder}")
        return
    
    files = sorted(folder.iterdir())
    renamed = 0
    
    for i, file_path in enumerate(files, start):
        if file_path.is_file():
            ext = file_path.suffix
            new_name = f"{prefix}_{i:03d}{ext}"
            new_path = folder / new_name
            file_path.rename(new_path)
            print(f"  {file_path.name} → {new_name}")
            renamed += 1
    
    print(f"\nRenamed {renamed} files.")

# Usage
# bulk_rename("./photos", prefix="vacation", start=1)
```

### Organize Files by Extension

```python
import os
import shutil
from pathlib import Path

def organize_by_type(source_folder):
    """Move files into subfolders based on file extension."""
    
    type_map = {
        "Images": [".jpg", ".jpeg", ".png", ".gif", ".bmp", ".svg"],
        "Documents": [".pdf", ".doc", ".docx", ".txt", ".md", ".rtf"],
        "Spreadsheets": [".xlsx", ".xls", ".csv"],
        "Code": [".py", ".js", ".html", ".css", ".java", ".cpp"],
        "Archives": [".zip", ".rar", ".7z", ".tar", ".gz"],
        "Videos": [".mp4", ".avi", ".mkv", ".mov"],
        "Audio": [".mp3", ".wav", ".flac", ".aac"],
    }
    
    source = Path(source_folder)
    moved = 0
    
    for file_path in source.iterdir():
        if not file_path.is_file():
            continue
        
        ext = file_path.suffix.lower()
        dest_folder = "Other"
        
        for folder_name, extensions in type_map.items():
            if ext in extensions:
                dest_folder = folder_name
                break
        
        dest = source / dest_folder
        dest.mkdir(exist_ok=True)
        shutil.move(str(file_path), str(dest / file_path.name))
        print(f"  {file_path.name} → {dest_folder}/")
        moved += 1
    
    print(f"\nOrganized {moved} files.")

# Usage
# organize_by_type("./Downloads")
```

### Find and Clean Old Files

```python
import os
import time
from pathlib import Path
from datetime import datetime, timedelta

def find_old_files(folder, days=30):
    """Find files older than N days."""
    cutoff = time.time() - (days * 86400)
    old_files = []
    
    for file_path in Path(folder).rglob("*"):
        if file_path.is_file():
            modified = file_path.stat().st_mtime
            if modified < cutoff:
                age = (time.time() - modified) / 86400
                size = file_path.stat().st_size
                old_files.append({
                    "path": str(file_path),
                    "age_days": int(age),
                    "size_kb": size / 1024,
                })
    
    return old_files

# Usage
# old = find_old_files("./temp", days=30)
# for f in old:
#     print(f"  {f['age_days']}d old | {f['size_kb']:.1f} KB | {f['path']}")
```

### Directory Size Report

```python
from pathlib import Path

def dir_size_report(folder):
    """Report size of each subdirectory."""
    root = Path(folder)
    
    print(f"\n  Directory Size Report: {root}")
    print(f"  {'Folder':<30} {'Files':>6} {'Size':>12}")
    print(f"  {'-'*50}")
    
    total_size = 0
    total_files = 0
    
    for sub in sorted(root.iterdir()):
        if sub.is_dir():
            files = list(sub.rglob("*"))
            file_count = sum(1 for f in files if f.is_file())
            size = sum(f.stat().st_size for f in files if f.is_file())
            total_size += size
            total_files += file_count
            print(f"  {sub.name:<30} {file_count:>6} {size/1024/1024:>10.2f} MB")
    
    print(f"  {'-'*50}")
    print(f"  {'TOTAL':<30} {total_files:>6} {total_size/1024/1024:>10.2f} MB")
```

---

## 27.3 Working with Excel Files (openpyxl)

### Installation

```bash
pip install openpyxl
```

### Reading Excel Files

```python
from openpyxl import load_workbook

wb = load_workbook("data.xlsx")
ws = wb.active  # Active sheet

# Sheet info
print(f"Sheet: {ws.title}")
print(f"Rows: {ws.max_row}, Columns: {ws.max_column}")

# Read cells
print(ws["A1"].value)       # Cell A1
print(ws.cell(row=1, column=1).value)  # Same as above

# Read all rows
for row in ws.iter_rows(min_row=2, values_only=True):
    print(row)  # Tuple of values

# Read into list of dicts
headers = [cell.value for cell in ws[1]]
data = []
for row in ws.iter_rows(min_row=2, values_only=True):
    data.append(dict(zip(headers, row)))

for record in data:
    print(record)
```

### Writing Excel Files

```python
from openpyxl import Workbook
from openpyxl.styles import Font, Alignment, PatternFill, Border, Side

wb = Workbook()
ws = wb.active
ws.title = "Sales Report"

# Header styling
header_font = Font(bold=True, size=12, color="FFFFFF")
header_fill = PatternFill(start_color="2F5496", end_color="2F5496", fill_type="solid")
header_align = Alignment(horizontal="center")

# Write header
headers = ["Product", "Category", "Price", "Qty Sold", "Revenue"]
for col, header in enumerate(headers, 1):
    cell = ws.cell(row=1, column=col, value=header)
    cell.font = header_font
    cell.fill = header_fill
    cell.alignment = header_align

# Write data
data = [
    ("Laptop", "Electronics", 65000, 15, 975000),
    ("Mouse", "Electronics", 500, 100, 50000),
    ("Notebook", "Stationery", 45, 500, 22500),
    ("Chair", "Furniture", 5500, 25, 137500),
    ("Monitor", "Electronics", 18000, 12, 216000),
]

for row_idx, row_data in enumerate(data, 2):
    for col_idx, value in enumerate(row_data, 1):
        ws.cell(row=row_idx, column=col_idx, value=value)

# Column widths
ws.column_dimensions["A"].width = 15
ws.column_dimensions["B"].width = 15
ws.column_dimensions["C"].width = 12
ws.column_dimensions["D"].width = 10
ws.column_dimensions["E"].width = 15

# Number formatting
for row in range(2, len(data) + 2):
    ws.cell(row=row, column=3).number_format = "#,##0"
    ws.cell(row=row, column=5).number_format = "#,##0"

# Total row
total_row = len(data) + 2
ws.cell(row=total_row, column=1, value="TOTAL").font = Font(bold=True)
ws.cell(row=total_row, column=5, value=sum(d[4] for d in data)).font = Font(bold=True)
ws.cell(row=total_row, column=5).number_format = "#,##0"

# Save
wb.save("sales_report.xlsx")
print("Excel report created: sales_report.xlsx")
```

### Modifying Existing Excel Files

```python
from openpyxl import load_workbook

wb = load_workbook("sales_report.xlsx")
ws = wb.active

# Add a new column
ws.cell(row=1, column=6, value="Tax (18%)")
for row in range(2, ws.max_row + 1):
    revenue = ws.cell(row=row, column=5).value
    if revenue and isinstance(revenue, (int, float)):
        ws.cell(row=row, column=6, value=revenue * 0.18)

wb.save("sales_report.xlsx")
print("Updated with tax column.")
```

---

## 27.4 Sending Emails with Python

### Using smtplib

```python
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
from email.mime.base import MIMEBase
from email import encoders

def send_email(to_email, subject, body, attachment_path=None):
    """Send an email with optional attachment."""
    
    # Email configuration
    smtp_server = "smtp.gmail.com"
    smtp_port = 587
    sender_email = "your_email@gmail.com"
    sender_password = "your_app_password"  # Use App Password, not regular password
    
    # Create message
    msg = MIMEMultipart()
    msg["From"] = sender_email
    msg["To"] = to_email
    msg["Subject"] = subject
    
    # Body
    msg.attach(MIMEText(body, "plain"))
    
    # Attachment
    if attachment_path:
        with open(attachment_path, "rb") as f:
            part = MIMEBase("application", "octet-stream")
            part.set_payload(f.read())
            encoders.encode_base64(part)
            part.add_header(
                "Content-Disposition",
                f"attachment; filename={os.path.basename(attachment_path)}"
            )
            msg.attach(part)
    
    # Send
    try:
        server = smtplib.SMTP(smtp_server, smtp_port)
        server.starttls()
        server.login(sender_email, sender_password)
        server.send_message(msg)
        server.quit()
        print(f"Email sent to {to_email}")
    except Exception as e:
        print(f"Failed to send email: {e}")

# Usage
# send_email("recipient@email.com", "Monthly Report", "Please find the attached report.", "report.pdf")
```

> **Note:** For Gmail, use App Passwords (not your regular password). Enable 2FA first, then generate an App Password in Google Account settings.

### HTML Email

```python
def send_html_email(to_email, subject, html_body):
    """Send an HTML-formatted email."""
    msg = MIMEMultipart("alternative")
    msg["From"] = sender_email
    msg["To"] = to_email
    msg["Subject"] = subject
    
    html_part = MIMEText(html_body, "html")
    msg.attach(html_part)
    
    # Send using same SMTP logic...

# Usage
html = """
<html>
<body>
<h2>Monthly Sales Report</h2>
<table border="1">
    <tr><th>Product</th><th>Revenue</th></tr>
    <tr><td>Laptop</td><td>₹9,75,000</td></tr>
    <tr><td>Mouse</td><td>₹50,000</td></tr>
</table>
<p>Generated automatically by Python.</p>
</body>
</html>
"""
# send_html_email("boss@company.com", "Sales Report", html)
```

---

## 27.5 Task Scheduling

### Using `schedule` Library

```bash
pip install schedule
```

```python
import schedule
import time
from datetime import datetime

def backup_data():
    print(f"[{datetime.now().strftime('%H:%M:%S')}] Backup started...")
    # Backup logic here
    print("Backup complete!")

def send_daily_report():
    print(f"[{datetime.now().strftime('%H:%M:%S')}] Sending daily report...")

def check_disk_space():
    import shutil
    total, used, free = shutil.disk_usage("/")
    pct = used / total * 100
    print(f"Disk usage: {pct:.1f}%")
    if pct > 90:
        print("WARNING: Disk space critically low!")

# Schedule tasks
schedule.every(30).minutes.do(backup_data)
schedule.every().day.at("09:00").do(send_daily_report)
schedule.every(1).hours.do(check_disk_space)
schedule.every().monday.at("08:00").do(send_daily_report)

# Run scheduler
print("Scheduler started. Press Ctrl+C to stop.")
while True:
    schedule.run_pending()
    time.sleep(1)
```

### Simple Timer-Based Automation

```python
import time
from datetime import datetime

def run_every(seconds, func, *args):
    """Run a function every N seconds."""
    print(f"Running {func.__name__} every {seconds}s. Press Ctrl+C to stop.")
    try:
        while True:
            func(*args)
            time.sleep(seconds)
    except KeyboardInterrupt:
        print("\nStopped.")

# Usage
# run_every(60, check_disk_space)
```

---

## 27.6 Data Processing Automation

### CSV Report Generator

```python
import csv
import json
from datetime import datetime
from collections import defaultdict

def generate_sales_summary(csv_file, output_file):
    """Read sales CSV and generate summary report."""
    
    # Read data
    with open(csv_file, "r") as f:
        reader = csv.DictReader(f)
        data = list(reader)
    
    # Aggregate by category
    categories = defaultdict(lambda: {"count": 0, "revenue": 0})
    for row in data:
        cat = row["category"]
        categories[cat]["count"] += 1
        categories[cat]["revenue"] += float(row.get("revenue", 0))
    
    # Build report
    report = {
        "generated": datetime.now().isoformat(),
        "total_records": len(data),
        "total_revenue": sum(float(r.get("revenue", 0)) for r in data),
        "categories": dict(categories),
    }
    
    # Save
    with open(output_file, "w") as f:
        json.dump(report, f, indent=4)
    
    print(f"Summary report: {output_file}")
    return report
```

### Batch File Converter (CSV to JSON)

```python
from pathlib import Path
import csv
import json

def batch_csv_to_json(input_folder, output_folder):
    """Convert all CSV files in a folder to JSON."""
    input_path = Path(input_folder)
    output_path = Path(output_folder)
    output_path.mkdir(exist_ok=True)
    
    converted = 0
    for csv_file in input_path.glob("*.csv"):
        try:
            with open(csv_file, "r", encoding="utf-8") as f:
                data = list(csv.DictReader(f))
            
            json_file = output_path / f"{csv_file.stem}.json"
            with open(json_file, "w") as f:
                json.dump(data, f, indent=4)
            
            print(f"  ✅ {csv_file.name} → {json_file.name} ({len(data)} records)")
            converted += 1
        except Exception as e:
            print(f"  ❌ {csv_file.name}: {e}")
    
    print(f"\nConverted {converted} files.")
```

---

## 27.7 System Monitoring

### Disk Space Monitor

```python
import shutil
import platform

def system_info():
    """Display system information."""
    print("\n=== System Information ===")
    print(f"  OS: {platform.system()} {platform.release()}")
    print(f"  Machine: {platform.machine()}")
    print(f"  Python: {platform.python_version()}")
    
    # Disk usage
    total, used, free = shutil.disk_usage(".")
    print(f"\n=== Disk Usage ===")
    print(f"  Total: {total / (1024**3):.2f} GB")
    print(f"  Used:  {used / (1024**3):.2f} GB ({used/total*100:.1f}%)")
    print(f"  Free:  {free / (1024**3):.2f} GB ({free/total*100:.1f}%)")

system_info()
```

---

## 🔧 Hands-On Activity: Automation Scripts

**Duration:** 25 minutes

Create a file `session27_automation.py`:

```python
# Session 27 — Automation Scripts
import os
import csv
import json
from pathlib import Path
from datetime import datetime
from collections import defaultdict

# Part 1: File Organizer (simulation)
print("=== Part 1: File Extension Report ===")
current_dir = Path(".")
ext_count = defaultdict(int)
ext_size = defaultdict(int)

for f in current_dir.rglob("*"):
    if f.is_file():
        ext = f.suffix.lower() or "(no ext)"
        ext_count[ext] += 1
        ext_size[ext] += f.stat().st_size

print(f"  {'Extension':<12} {'Count':>6} {'Size':>12}")
print(f"  {'-'*32}")
for ext in sorted(ext_count, key=lambda x: ext_size[x], reverse=True)[:10]:
    print(f"  {ext:<12} {ext_count[ext]:>6} {ext_size[ext]/1024:>10.1f} KB")

# Part 2: CSV Data Processor
print("\n=== Part 2: Auto-Generate Report ===")

# Create sample sales data
sales_data = [
    {"date": "2024-01-05", "product": "Laptop", "category": "Electronics", "amount": "65000"},
    {"date": "2024-01-08", "product": "Mouse", "category": "Electronics", "amount": "500"},
    {"date": "2024-01-10", "product": "Notebook", "category": "Stationery", "amount": "45"},
    {"date": "2024-01-12", "product": "Chair", "category": "Furniture", "amount": "5500"},
    {"date": "2024-01-15", "product": "Pen", "category": "Stationery", "amount": "15"},
    {"date": "2024-01-18", "product": "Monitor", "category": "Electronics", "amount": "18000"},
    {"date": "2024-01-20", "product": "Desk", "category": "Furniture", "amount": "8000"},
    {"date": "2024-01-22", "product": "Keyboard", "category": "Electronics", "amount": "1200"},
]

# Write sample CSV
with open("sales_sample.csv", "w", newline="") as f:
    writer = csv.DictWriter(f, fieldnames=sales_data[0].keys())
    writer.writeheader()
    writer.writerows(sales_data)

# Process and summarize
with open("sales_sample.csv", "r") as f:
    data = list(csv.DictReader(f))

cat_summary = defaultdict(lambda: {"count": 0, "total": 0})
for row in data:
    cat = row["category"]
    cat_summary[cat]["count"] += 1
    cat_summary[cat]["total"] += float(row["amount"])

grand_total = sum(float(r["amount"]) for r in data)

# Generate report
report_lines = [
    f"Sales Summary Report — {datetime.now().strftime('%d %b %Y')}",
    "=" * 45,
    f"Total Transactions : {len(data)}",
    f"Total Revenue      : ₹{grand_total:,.2f}",
    "",
    f"{'Category':<15} {'Count':>6} {'Revenue':>14} {'%':>6}",
    "-" * 45,
]

for cat, info in sorted(cat_summary.items(), key=lambda x: x[1]["total"], reverse=True):
    pct = info["total"] / grand_total * 100
    report_lines.append(f"{cat:<15} {info['count']:>6} ₹{info['total']:>12,.2f} {pct:>5.1f}%")

report_lines.append("=" * 45)
report_text = "\n".join(report_lines)
print(report_text)

# Save report
with open("auto_report.txt", "w") as f:
    f.write(report_text)
print("\nReport saved to auto_report.txt")

# Save as JSON
report_json = {
    "generated": datetime.now().isoformat(),
    "total_transactions": len(data),
    "total_revenue": grand_total,
    "by_category": dict(cat_summary),
}
with open("auto_report.json", "w") as f:
    json.dump(report_json, f, indent=4)
print("JSON saved to auto_report.json")

# Cleanup
# os.remove("sales_sample.csv")
# os.remove("auto_report.txt")
# os.remove("auto_report.json")
print("\nDone!")
```

---

## Session 27 — Key Takeaways

1. **File automation** (rename, organize, clean) saves hours of manual work
2. **openpyxl** reads/writes Excel files with formatting, formulas, and styling
3. **smtplib** sends emails programmatically — use App Passwords for Gmail
4. **schedule** library runs functions at specific times or intervals
5. **Batch processing** converts, transforms, or reports on multiple files at once
6. **Always add error handling** to automation scripts — they run unattended

---

## Preparation for Session 28
- Review all course concepts: data types, control flow, functions, OOP, files, APIs
- Think about: What project would showcase all your Python skills?
- Start brainstorming: What problem would you solve with a capstone project?

---

*Session 27 of 30 | Module 6: Automation & Capstone Project*
*Professional Python Programming Certification — UpSkill Global Education Technologies Inc., Canada*
