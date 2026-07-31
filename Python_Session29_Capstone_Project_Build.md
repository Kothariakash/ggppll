# Session 29 — Capstone Project Build
## Module 6: Automation & Capstone Project | Professional Python Programming Certification
### Duration: 1 Hour | Type: Hands-On Build | Build: Complete Your Capstone Project

---

## Learning Objectives
By the end of this session, you will be able to:
1. Implement the full capstone project from your Session 28 design
2. Build a data processing pipeline with CSV input and PDF output
3. Generate professional PDF reports with tables and charts
4. Integrate all course concepts into a cohesive application
5. Test and debug a multi-module Python project

---

## 29.1 Reference Build: PDF Report Generator

This session provides a complete reference implementation of the **PDF Report Generator** capstone. Use it as a guide or build your own chosen topic.

---

## 29.2 Sample Data — `data/sales_data.csv`

```csv
Date,Product,Category,Region,Quantity,Unit_Price,Discount
2024-01-05,Laptop,Electronics,North,3,65000,0.05
2024-01-08,Mouse,Electronics,South,25,500,0.00
2024-01-10,Notebook,Stationery,East,100,45,0.10
2024-01-12,Office Chair,Furniture,West,5,5500,0.00
2024-01-15,Pen Set,Stationery,North,200,120,0.15
2024-01-18,Monitor,Electronics,South,8,18000,0.05
2024-01-20,Desk,Furniture,East,3,8000,0.00
2024-01-22,Keyboard,Electronics,West,15,1200,0.00
2024-01-25,Printer Paper,Stationery,North,50,350,0.10
2024-01-28,Webcam,Electronics,South,10,3500,0.05
2024-02-02,Laptop,Electronics,East,5,65000,0.08
2024-02-05,Headphones,Electronics,West,20,2500,0.00
2024-02-08,Stapler,Stationery,North,80,150,0.00
2024-02-10,Bookshelf,Furniture,South,4,7500,0.10
2024-02-12,USB Drive,Electronics,East,50,800,0.05
2024-02-15,Whiteboard,Stationery,West,6,3000,0.00
2024-02-18,Filing Cabinet,Furniture,North,3,6000,0.00
2024-02-20,Mouse Pad,Electronics,South,40,350,0.00
2024-02-22,Marker Set,Stationery,East,60,250,0.10
2024-02-25,Standing Desk,Furniture,West,2,15000,0.05
```

---

## 29.3 Implementation — Model Layer

### `models/data_record.py`

```python
"""Data record models for sales data."""

class SalesRecord:
    """Represents a single sales transaction."""
    
    def __init__(self, date, product, category, region, quantity, unit_price, discount):
        self.date = date
        self.product = product
        self.category = category
        self.region = region
        self.quantity = int(quantity)
        self.unit_price = float(unit_price)
        self.discount = float(discount)
    
    @property
    def gross_amount(self):
        return self.quantity * self.unit_price
    
    @property
    def discount_amount(self):
        return self.gross_amount * self.discount
    
    @property
    def net_amount(self):
        return self.gross_amount - self.discount_amount
    
    @property
    def month(self):
        return self.date[:7]  # "2024-01"
    
    def __str__(self):
        return f"{self.date} | {self.product:<15} | {self.category:<12} | ₹{self.net_amount:>10,.2f}"
    
    def __repr__(self):
        return f"SalesRecord('{self.product}', qty={self.quantity}, net=₹{self.net_amount:,.2f})"
```

### `models/report.py`

```python
"""Abstract report engine."""

from abc import ABC, abstractmethod
from datetime import datetime

class ReportEngine(ABC):
    """Abstract base class for all reports."""
    
    def __init__(self, title, data):
        self.title = title
        self.data = data
        self.generated = datetime.now()
        self.summary = {}
    
    @abstractmethod
    def process_data(self):
        """Process raw data into summary statistics."""
        pass
    
    @abstractmethod
    def generate_report(self, output_path):
        """Generate the final report file."""
        pass
    
    @property
    def record_count(self):
        return len(self.data)
    
    def __str__(self):
        return f"{self.__class__.__name__}('{self.title}', {self.record_count} records)"
```

---

## 29.4 Implementation — Service Layer

### `services/data_loader.py`

```python
"""CSV data loading with validation."""

import csv
import logging
from models.data_record import SalesRecord

logger = logging.getLogger(__name__)

class DataLoader:
    """Loads and validates data from CSV files."""
    
    REQUIRED_FIELDS = ["Date", "Product", "Category", "Region", "Quantity", "Unit_Price", "Discount"]
    
    @staticmethod
    def load_csv(filepath):
        """Load sales data from CSV. Returns list of SalesRecord objects."""
        records = []
        errors = []
        
        try:
            with open(filepath, "r", encoding="utf-8") as f:
                reader = csv.DictReader(f)
                
                # Validate headers
                if reader.fieldnames:
                    missing = [h for h in DataLoader.REQUIRED_FIELDS if h not in reader.fieldnames]
                    if missing:
                        raise ValueError(f"Missing columns: {', '.join(missing)}")
                
                for i, row in enumerate(reader, 2):
                    try:
                        record = SalesRecord(
                            date=row["Date"],
                            product=row["Product"],
                            category=row["Category"],
                            region=row["Region"],
                            quantity=row["Quantity"],
                            unit_price=row["Unit_Price"],
                            discount=row["Discount"],
                        )
                        records.append(record)
                    except (ValueError, KeyError) as e:
                        errors.append(f"Row {i}: {e}")
                        logger.warning(f"Skipped row {i}: {e}")
        
        except FileNotFoundError:
            logger.error(f"File not found: {filepath}")
            raise
        except Exception as e:
            logger.error(f"Error loading {filepath}: {e}")
            raise
        
        logger.info(f"Loaded {len(records)} records, {len(errors)} errors from {filepath}")
        return records, errors
```

### `services/data_processor.py`

```python
"""Data analysis and processing."""

from collections import defaultdict

class DataProcessor:
    """Process sales records into summary statistics."""
    
    @staticmethod
    def summary_stats(records):
        """Calculate overall summary statistics."""
        if not records:
            return {}
        
        total_revenue = sum(r.net_amount for r in records)
        total_quantity = sum(r.quantity for r in records)
        total_discount = sum(r.discount_amount for r in records)
        
        return {
            "total_records": len(records),
            "total_revenue": total_revenue,
            "total_quantity": total_quantity,
            "total_discount": total_discount,
            "avg_order_value": total_revenue / len(records),
            "avg_discount_pct": total_discount / sum(r.gross_amount for r in records) * 100,
        }
    
    @staticmethod
    def by_category(records):
        """Group and summarize by category."""
        groups = defaultdict(lambda: {"count": 0, "quantity": 0, "revenue": 0})
        
        for r in records:
            groups[r.category]["count"] += 1
            groups[r.category]["quantity"] += r.quantity
            groups[r.category]["revenue"] += r.net_amount
        
        return dict(sorted(groups.items(), key=lambda x: x[1]["revenue"], reverse=True))
    
    @staticmethod
    def by_region(records):
        """Group and summarize by region."""
        groups = defaultdict(lambda: {"count": 0, "revenue": 0})
        
        for r in records:
            groups[r.region]["count"] += 1
            groups[r.region]["revenue"] += r.net_amount
        
        return dict(sorted(groups.items(), key=lambda x: x[1]["revenue"], reverse=True))
    
    @staticmethod
    def by_month(records):
        """Group and summarize by month."""
        groups = defaultdict(lambda: {"count": 0, "revenue": 0})
        
        for r in records:
            groups[r.month]["count"] += 1
            groups[r.month]["revenue"] += r.net_amount
        
        return dict(sorted(groups.items()))
    
    @staticmethod
    def top_products(records, n=5):
        """Top N products by revenue."""
        products = defaultdict(float)
        for r in records:
            products[r.product] += r.net_amount
        
        sorted_products = sorted(products.items(), key=lambda x: x[1], reverse=True)
        return sorted_products[:n]
```

---

## 29.5 Implementation — Chart Generation

### `utils/chart_maker.py`

```python
"""Chart generation using matplotlib."""

import matplotlib
matplotlib.use("Agg")  # Non-interactive backend for saving to file
import matplotlib.pyplot as plt

class ChartMaker:
    """Generate charts and save as image files."""
    
    COLORS = ["#2196F3", "#4CAF50", "#FF9800", "#F44336", "#9C27B0",
              "#00BCD4", "#795548", "#607D8B"]
    
    @staticmethod
    def bar_chart(labels, values, title, ylabel, output_path, color=None):
        """Generate a bar chart."""
        fig, ax = plt.subplots(figsize=(8, 5))
        colors = color or ChartMaker.COLORS[:len(labels)]
        ax.bar(labels, values, color=colors)
        ax.set_title(title, fontsize=14, fontweight="bold")
        ax.set_ylabel(ylabel)
        ax.tick_params(axis="x", rotation=45)
        
        # Add value labels on bars
        for i, v in enumerate(values):
            ax.text(i, v + max(values) * 0.02, f"₹{v:,.0f}", ha="center", fontsize=9)
        
        plt.tight_layout()
        plt.savefig(output_path, dpi=150, bbox_inches="tight")
        plt.close()
    
    @staticmethod
    def pie_chart(labels, values, title, output_path):
        """Generate a pie chart."""
        fig, ax = plt.subplots(figsize=(7, 7))
        colors = ChartMaker.COLORS[:len(labels)]
        wedges, texts, autotexts = ax.pie(
            values, labels=labels, autopct="%1.1f%%",
            colors=colors, startangle=90, textprops={"fontsize": 10}
        )
        ax.set_title(title, fontsize=14, fontweight="bold")
        plt.tight_layout()
        plt.savefig(output_path, dpi=150, bbox_inches="tight")
        plt.close()
    
    @staticmethod
    def line_chart(x_labels, values, title, ylabel, output_path):
        """Generate a line chart."""
        fig, ax = plt.subplots(figsize=(8, 5))
        ax.plot(x_labels, values, marker="o", color="#2196F3", linewidth=2)
        ax.fill_between(range(len(x_labels)), values, alpha=0.1, color="#2196F3")
        ax.set_title(title, fontsize=14, fontweight="bold")
        ax.set_ylabel(ylabel)
        ax.tick_params(axis="x", rotation=45)
        ax.grid(axis="y", alpha=0.3)
        
        for i, v in enumerate(values):
            ax.text(i, v + max(values) * 0.03, f"₹{v:,.0f}", ha="center", fontsize=9)
        
        plt.tight_layout()
        plt.savefig(output_path, dpi=150, bbox_inches="tight")
        plt.close()
```

---

## 29.6 Implementation — PDF Report Generator

### `services/report_generator.py`

```python
"""PDF report generation using fpdf2."""

import os
from datetime import datetime
from fpdf import FPDF
from models.report import ReportEngine

class SalesReportPDF(ReportEngine):
    """Generate a professional sales report as PDF."""
    
    def __init__(self, title, data):
        super().__init__(title, data)
        self.stats = {}
        self.cat_data = {}
        self.region_data = {}
        self.month_data = {}
        self.top_products = []
    
    @property
    def account_type(self):
        return "Sales"
    
    def process_data(self):
        """Process raw records into summary data."""
        from services.data_processor import DataProcessor
        self.stats = DataProcessor.summary_stats(self.data)
        self.cat_data = DataProcessor.by_category(self.data)
        self.region_data = DataProcessor.by_region(self.data)
        self.month_data = DataProcessor.by_month(self.data)
        self.top_products = DataProcessor.top_products(self.data, 5)
    
    def generate_report(self, output_path, chart_dir="output"):
        """Generate the complete PDF report."""
        os.makedirs(chart_dir, exist_ok=True)
        
        # Generate charts
        from utils.chart_maker import ChartMaker
        
        cat_labels = list(self.cat_data.keys())
        cat_values = [d["revenue"] for d in self.cat_data.values()]
        ChartMaker.bar_chart(cat_labels, cat_values, "Revenue by Category", "Revenue (₹)",
                            os.path.join(chart_dir, "chart_category.png"))
        
        ChartMaker.pie_chart(cat_labels, cat_values, "Revenue Distribution",
                            os.path.join(chart_dir, "chart_pie.png"))
        
        month_labels = list(self.month_data.keys())
        month_values = [d["revenue"] for d in self.month_data.values()]
        ChartMaker.line_chart(month_labels, month_values, "Monthly Revenue Trend", "Revenue (₹)",
                             os.path.join(chart_dir, "chart_monthly.png"))
        
        # Build PDF
        pdf = FPDF()
        pdf.set_auto_page_break(auto=True, margin=20)
        
        # --- Page 1: Title & Summary ---
        pdf.add_page()
        
        # Header
        pdf.set_fill_color(33, 82, 150)
        pdf.rect(0, 0, 210, 40, "F")
        pdf.set_text_color(255, 255, 255)
        pdf.set_font("Helvetica", "B", 22)
        pdf.set_y(10)
        pdf.cell(0, 12, self.title, align="C", new_x="LMARGIN", new_y="NEXT")
        pdf.set_font("Helvetica", "", 11)
        pdf.cell(0, 8, f"Generated: {self.generated.strftime('%d %B %Y, %I:%M %p')}", 
                 align="C", new_x="LMARGIN", new_y="NEXT")
        
        pdf.set_text_color(0, 0, 0)
        pdf.ln(15)
        
        # Summary cards
        pdf.set_font("Helvetica", "B", 14)
        pdf.cell(0, 10, "Executive Summary", new_x="LMARGIN", new_y="NEXT")
        pdf.ln(3)
        
        stats = self.stats
        summary_items = [
            ("Total Transactions", f"{stats['total_records']}"),
            ("Total Revenue", f"Rs. {stats['total_revenue']:,.2f}"),
            ("Total Quantity Sold", f"{stats['total_quantity']:,}"),
            ("Total Discounts", f"Rs. {stats['total_discount']:,.2f}"),
            ("Avg Order Value", f"Rs. {stats['avg_order_value']:,.2f}"),
            ("Avg Discount", f"{stats['avg_discount_pct']:.1f}%"),
        ]
        
        pdf.set_font("Helvetica", "", 11)
        col_width = 90
        for i, (label, value) in enumerate(summary_items):
            if i % 2 == 0 and i > 0:
                pdf.ln(8)
            x = 15 if i % 2 == 0 else 110
            pdf.set_xy(x, pdf.get_y())
            pdf.set_font("Helvetica", "", 10)
            pdf.cell(col_width, 6, label, new_x="LMARGIN", new_y="NEXT")
            pdf.set_xy(x, pdf.get_y())
            pdf.set_font("Helvetica", "B", 13)
            pdf.cell(col_width, 8, value, new_x="LMARGIN", new_y="NEXT")
            if i % 2 == 0:
                pdf.set_y(pdf.get_y() - 14)
        
        pdf.ln(20)
        
        # --- Category Table ---
        pdf.set_font("Helvetica", "B", 14)
        pdf.cell(0, 10, "Revenue by Category", new_x="LMARGIN", new_y="NEXT")
        pdf.ln(3)
        
        # Table header
        pdf.set_fill_color(33, 82, 150)
        pdf.set_text_color(255, 255, 255)
        pdf.set_font("Helvetica", "B", 10)
        pdf.cell(45, 8, "Category", fill=True, border=1)
        pdf.cell(30, 8, "Orders", fill=True, border=1, align="C")
        pdf.cell(35, 8, "Quantity", fill=True, border=1, align="C")
        pdf.cell(45, 8, "Revenue", fill=True, border=1, align="R")
        pdf.cell(25, 8, "%", fill=True, border=1, align="C")
        pdf.ln()
        
        # Table rows
        pdf.set_text_color(0, 0, 0)
        pdf.set_font("Helvetica", "", 10)
        total_rev = stats["total_revenue"]
        fill = False
        
        for cat, info in self.cat_data.items():
            if fill:
                pdf.set_fill_color(240, 245, 250)
            pdf.cell(45, 7, cat, fill=fill, border=1)
            pdf.cell(30, 7, str(info["count"]), fill=fill, border=1, align="C")
            pdf.cell(35, 7, f"{info['quantity']:,}", fill=fill, border=1, align="C")
            pdf.cell(45, 7, f"Rs. {info['revenue']:,.2f}", fill=fill, border=1, align="R")
            pct = info["revenue"] / total_rev * 100 if total_rev > 0 else 0
            pdf.cell(25, 7, f"{pct:.1f}%", fill=fill, border=1, align="C")
            pdf.ln()
            fill = not fill
        
        # --- Page 2: Charts ---
        pdf.add_page()
        pdf.set_font("Helvetica", "B", 14)
        pdf.cell(0, 10, "Visual Analysis", new_x="LMARGIN", new_y="NEXT")
        pdf.ln(5)
        
        chart_cat = os.path.join(chart_dir, "chart_category.png")
        chart_pie = os.path.join(chart_dir, "chart_pie.png")
        chart_monthly = os.path.join(chart_dir, "chart_monthly.png")
        
        if os.path.exists(chart_cat):
            pdf.image(chart_cat, x=10, w=190)
            pdf.ln(5)
        
        if os.path.exists(chart_pie):
            pdf.add_page()
            pdf.set_font("Helvetica", "B", 14)
            pdf.cell(0, 10, "Revenue Distribution", new_x="LMARGIN", new_y="NEXT")
            pdf.ln(5)
            pdf.image(chart_pie, x=30, w=150)
        
        if os.path.exists(chart_monthly):
            pdf.add_page()
            pdf.set_font("Helvetica", "B", 14)
            pdf.cell(0, 10, "Monthly Trend", new_x="LMARGIN", new_y="NEXT")
            pdf.ln(5)
            pdf.image(chart_monthly, x=10, w=190)
        
        # --- Top Products Table ---
        pdf.ln(15)
        pdf.set_font("Helvetica", "B", 14)
        pdf.cell(0, 10, "Top 5 Products by Revenue", new_x="LMARGIN", new_y="NEXT")
        pdf.ln(3)
        
        pdf.set_fill_color(33, 82, 150)
        pdf.set_text_color(255, 255, 255)
        pdf.set_font("Helvetica", "B", 10)
        pdf.cell(10, 8, "#", fill=True, border=1, align="C")
        pdf.cell(80, 8, "Product", fill=True, border=1)
        pdf.cell(50, 8, "Revenue", fill=True, border=1, align="R")
        pdf.cell(40, 8, "% of Total", fill=True, border=1, align="C")
        pdf.ln()
        
        pdf.set_text_color(0, 0, 0)
        pdf.set_font("Helvetica", "", 10)
        for i, (product, revenue) in enumerate(self.top_products, 1):
            pct = revenue / total_rev * 100 if total_rev > 0 else 0
            pdf.cell(10, 7, str(i), border=1, align="C")
            pdf.cell(80, 7, product, border=1)
            pdf.cell(50, 7, f"Rs. {revenue:,.2f}", border=1, align="R")
            pdf.cell(40, 7, f"{pct:.1f}%", border=1, align="C")
            pdf.ln()
        
        # --- Footer on all pages ---
        for page in range(1, pdf.pages_count + 1):
            pdf.page = page
            pdf.set_y(-15)
            pdf.set_font("Helvetica", "I", 8)
            pdf.set_text_color(128, 128, 128)
            pdf.cell(0, 10, f"Page {page}/{pdf.pages_count} | {self.title} | "
                     f"Generated: {self.generated.strftime('%d %b %Y')}",
                     align="C")
        
        # Save
        pdf.output(output_path)
        return output_path
```

---

## 29.7 Implementation — Main Entry Point

### `main.py`

```python
"""Capstone Project: PDF Report Generator — Main Entry Point."""

import os
import logging
from datetime import datetime

# Setup logging
os.makedirs("logs", exist_ok=True)
os.makedirs("output", exist_ok=True)

logging.basicConfig(
    level=logging.INFO,
    format="%(asctime)s | %(levelname)-8s | %(name)s | %(message)s",
    datefmt="%Y-%m-%d %H:%M:%S",
    handlers=[
        logging.FileHandler("logs/app.log"),
        logging.StreamHandler()
    ]
)
logger = logging.getLogger("Capstone")

def main():
    from services.data_loader import DataLoader
    from services.report_generator import SalesReportPDF
    
    print("=" * 55)
    print("   PDF REPORT GENERATOR — Capstone Project")
    print("=" * 55)
    
    while True:
        print("\n--- MENU ---")
        print("  1. Generate Sales Report (PDF)")
        print("  2. View Data Summary (Console)")
        print("  3. List Available Data Files")
        print("  0. Exit")
        
        choice = input("  Choice: ").strip()
        
        if choice == "1":
            csv_file = input("  CSV file path [data/sales_data.csv]: ").strip()
            if not csv_file:
                csv_file = "data/sales_data.csv"
            
            try:
                # Load data
                records, errors = DataLoader.load_csv(csv_file)
                if errors:
                    print(f"  ⚠ {len(errors)} rows skipped due to errors.")
                
                if not records:
                    print("  No valid records found.")
                    continue
                
                # Generate report
                report_title = input("  Report title [Sales Performance Report]: ").strip()
                if not report_title:
                    report_title = "Sales Performance Report"
                
                report = SalesReportPDF(report_title, records)
                report.process_data()
                
                timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
                output_path = f"output/report_{timestamp}.pdf"
                
                report.generate_report(output_path, chart_dir="output")
                print(f"\n  ✅ Report generated: {output_path}")
                print(f"  Records processed: {len(records)}")
                print(f"  Total revenue: ₹{report.stats['total_revenue']:,.2f}")
                
            except FileNotFoundError:
                print(f"  ❌ File not found: {csv_file}")
            except Exception as e:
                print(f"  ❌ Error: {e}")
                logger.exception("Report generation failed")
        
        elif choice == "2":
            csv_file = input("  CSV file path [data/sales_data.csv]: ").strip()
            if not csv_file:
                csv_file = "data/sales_data.csv"
            
            try:
                records, _ = DataLoader.load_csv(csv_file)
                from services.data_processor import DataProcessor
                
                stats = DataProcessor.summary_stats(records)
                cat = DataProcessor.by_category(records)
                top = DataProcessor.top_products(records, 5)
                
                print(f"\n  --- Summary ---")
                print(f"  Records: {stats['total_records']}")
                print(f"  Revenue: ₹{stats['total_revenue']:,.2f}")
                print(f"  Avg Order: ₹{stats['avg_order_value']:,.2f}")
                
                print(f"\n  --- By Category ---")
                for c, info in cat.items():
                    print(f"  {c:<15} {info['count']:>4} orders  ₹{info['revenue']:>12,.2f}")
                
                print(f"\n  --- Top Products ---")
                for i, (prod, rev) in enumerate(top, 1):
                    print(f"  {i}. {prod:<20} ₹{rev:>12,.2f}")
                
            except Exception as e:
                print(f"  ❌ Error: {e}")
        
        elif choice == "3":
            data_dir = "data"
            if os.path.exists(data_dir):
                files = [f for f in os.listdir(data_dir) if f.endswith(".csv")]
                if files:
                    print(f"\n  CSV files in '{data_dir}/':")
                    for f in files:
                        size = os.path.getsize(os.path.join(data_dir, f))
                        print(f"    {f} ({size:,} bytes)")
                else:
                    print(f"  No CSV files in '{data_dir}/'.")
            else:
                print(f"  Directory '{data_dir}' not found.")
        
        elif choice == "0":
            print("\n  Thank you! Goodbye!")
            break
        
        else:
            print("  Invalid choice.")

if __name__ == "__main__":
    main()
```

---

## 29.8 Build Checklist

| Step | Task | Status |
|------|------|--------|
| 1 | Create project folder structure | ☐ |
| 2 | Create `data/sales_data.csv` with sample data | ☐ |
| 3 | Implement `models/data_record.py` (SalesRecord class) | ☐ |
| 4 | Implement `models/report.py` (ReportEngine ABC) | ☐ |
| 5 | Implement `services/data_loader.py` (CSV loading) | ☐ |
| 6 | Implement `services/data_processor.py` (analysis) | ☐ |
| 7 | Implement `utils/chart_maker.py` (matplotlib charts) | ☐ |
| 8 | Implement `services/report_generator.py` (PDF output) | ☐ |
| 9 | Implement `main.py` (menu-driven entry point) | ☐ |
| 10 | Test end-to-end: CSV → Process → Charts → PDF | ☐ |
| 11 | Add error handling and logging | ☐ |
| 12 | Write `README.md` | ☐ |

---

## 29.9 Testing Your Project

### Quick Smoke Test

```python
# Run from project root:
# python main.py

# Expected:
# 1. Menu displays
# 2. Option 1: Reads CSV, generates charts, creates PDF
# 3. PDF file appears in output/ folder
# 4. PDF has title, summary, tables, charts, page numbers
```

### Manual Test Cases

| Test | Input | Expected Output |
|------|-------|----------------|
| Valid CSV | `data/sales_data.csv` | PDF generated with all sections |
| Missing file | `nonexistent.csv` | "File not found" error message |
| Empty CSV | CSV with only headers | "No valid records" message |
| Bad data rows | CSV with invalid numbers | Skipped rows + warning |
| Console summary | Option 2 | Formatted summary on screen |

---

## Session 29 — Key Takeaways

1. **Modular design** keeps code maintainable — models, services, utils are separate
2. **Abstract base class** (ReportEngine) ensures all reports follow the same interface
3. **fpdf2** generates professional PDFs with tables, headers, and embedded images
4. **matplotlib** creates publication-quality charts saved as PNG for PDF embedding
5. **Error handling** at every layer prevents crashes on bad data
6. **Test as you build** — verify each component before connecting them

---

## Preparation for Session 30
- Complete your capstone project build
- Run full end-to-end tests
- Prepare a 5-minute demo/presentation of your project
- Write final README.md documentation

---

*Session 29 of 30 | Module 6: Automation & Capstone Project*
*Professional Python Programming Certification — UpSkill Global Education Technologies Inc., Canada*
