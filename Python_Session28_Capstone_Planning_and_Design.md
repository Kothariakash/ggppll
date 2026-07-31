# Session 28 — Capstone Planning & Design
## Module 6: Automation & Capstone Project | Professional Python Programming Certification
### Duration: 1 Hour | Type: Theory + Workshop | Workshop: Plan and Design Your Capstone Project

---

## Learning Objectives
By the end of this session, you will be able to:
1. Select a meaningful capstone project topic
2. Write clear project requirements and specifications
3. Design the architecture using OOP principles
4. Plan the implementation with milestones and tasks
5. Set up the project structure and development environment

---

## 28.1 Capstone Project Purpose

The capstone project is your opportunity to demonstrate **all the skills** learned across the 30-session Python course. It should be a complete, functional application that solves a real-world problem.

### What the Capstone Must Demonstrate

| Module | Skills to Show |
|--------|---------------|
| **Module 1 — Fundamentals** | Variables, data types, operators, I/O |
| **Module 2 — Control Flow** | Conditionals, loops, functions, modules |
| **Module 3 — Data Structures** | Lists, dicts, tuples, sets, strings |
| **Module 4 — File Handling** | CSV/JSON read/write, exception handling, logging |
| **Module 5 — OOP** | Classes, inheritance, encapsulation, abstraction |
| **Module 6 — Automation** | APIs, automation, PDF report generation |

---

## 28.2 Suggested Capstone Topics

### Topic 1: PDF Report Generator (Recommended)

> Build a system that reads data from CSV files, processes it, and generates professional PDF reports with tables, charts, and summaries.

| Feature | Concepts |
|---------|---------|
| Read sales/employee data from CSV | File handling, csv module |
| Data validation and cleaning | Exception handling |
| Statistical analysis | Functions, data structures |
| PDF generation with tables | fpdf2 library |
| Charts and visualizations | matplotlib |
| Automated report scheduling | Automation |
| OOP-based report engine | Classes, inheritance |

### Topic 2: Student Information System

> Manage student records, courses, grades, and generate transcripts.

| Feature | Concepts |
|---------|---------|
| Student CRUD operations | OOP, dictionaries |
| Course enrollment | Lists, relationships |
| Grade calculation | Functions, operators |
| Transcript PDF generation | fpdf2 |
| Data persistence in CSV | File handling |
| Search and filtering | Strings, comprehensions |

### Topic 3: Personal Finance Tracker

> Track income, expenses, budgets, and generate financial reports.

| Feature | Concepts |
|---------|---------|
| Transaction management | OOP, file handling |
| Budget tracking and alerts | Conditionals, functions |
| Category analysis | Dictionaries, sets |
| Monthly/annual reports | CSV, PDF generation |
| Data visualization | matplotlib |
| Import from bank CSV | csv module |

### Topic 4: Library Management System

> Manage books, members, borrowing, and returns with fine calculation.

| Feature | Concepts |
|---------|---------|
| Book and member management | OOP, inheritance |
| Borrowing/return with dates | datetime, functions |
| Fine calculation | Conditionals, operators |
| Search and recommendations | Strings, lists |
| Report generation | File handling, PDF |
| Data storage | CSV/JSON |

### Topic 5: Employee Payroll System

> Calculate salaries, deductions, generate payslips, and manage employee data.

| Feature | Concepts |
|---------|---------|
| Employee hierarchy | OOP, inheritance |
| Salary calculation (base, OT, deductions) | Functions, operators |
| Tax computation | Conditionals |
| Payslip PDF generation | fpdf2 |
| Monthly payroll report | CSV, aggregation |
| Data persistence | File handling |

---

## 28.3 Project Requirements Document

### Template

```markdown
# Capstone Project: [Project Name]

## 1. Overview
Brief description of what the project does and who it's for.

## 2. Features
- Feature 1: Description
- Feature 2: Description
- Feature 3: Description
- ...

## 3. Technical Requirements
- Python 3.10+
- Libraries: fpdf2, matplotlib, openpyxl (list all)
- Data format: CSV for input, PDF for output
- Persistence: CSV/JSON files

## 4. Data Model
- Entity 1: attributes and relationships
- Entity 2: attributes and relationships

## 5. User Interface
- Menu-driven console application
- Menu structure and flow

## 6. Files and Folders
- Project directory structure

## 7. Milestones
- Milestone 1: Setup + Models (Day 1)
- Milestone 2: Core Features (Day 2)
- Milestone 3: Reports + PDF (Day 3)
- Milestone 4: Testing + Polish (Day 4)
```

---

## 28.4 Architecture Design

### Class Diagram (Example: PDF Report Generator)

```
┌────────────────────────┐
│     ReportEngine       │  (Abstract Base Class)
│────────────────────────│
│ - title                │
│ - data                 │
│ - generated_date       │
│────────────────────────│
│ + load_data()          │
│ + process_data()       │  (abstract)
│ + generate_report()    │  (abstract)
│ + save()               │
└────────┬───────────────┘
         │ inherits
    ┌────┴─────────┐
    │              │
┌───▼──────┐  ┌───▼──────────┐
│SalesReport│  │EmployeeReport│
│──────────│  │──────────────│
│+ process │  │+ process     │
│+ generate│  │+ generate    │
└──────────┘  └──────────────┘

┌─────────────┐    ┌──────────────┐
│ DataLoader   │    │ PDFBuilder   │
│─────────────│    │──────────────│
│+ load_csv() │    │+ add_title() │
│+ validate() │    │+ add_table() │
│+ clean()    │    │+ add_chart() │
└─────────────┘    │+ save_pdf()  │
                   └──────────────┘

┌─────────────┐    ┌──────────────┐
│ ChartMaker  │    │ Config       │
│─────────────│    │──────────────│
│+ bar_chart()│    │+ paths       │
│+ pie_chart()│    │+ settings    │
│+ line_chart│    │+ load()      │
└─────────────┘    └──────────────┘
```

### Package Structure

```
capstone_project/
├── main.py                 ← Entry point
├── requirements.txt        ← Dependencies
├── README.md               ← Documentation
├── config.py               ← Configuration
│
├── models/                 ← Data models
│   ├── __init__.py
│   ├── report.py           ← ReportEngine ABC
│   └── data_record.py      ← Data record classes
│
├── services/               ← Business logic
│   ├── __init__.py
│   ├── data_loader.py      ← CSV/JSON loading
│   ├── data_processor.py   ← Analysis & calculations
│   └── report_generator.py ← PDF generation
│
├── utils/                  ← Helpers
│   ├── __init__.py
│   ├── validators.py       ← Input validation
│   ├── formatters.py       ← Currency, date formatting
│   └── chart_maker.py      ← Chart generation
│
├── data/                   ← Input data files
│   ├── sales_data.csv
│   └── config.json
│
├── output/                 ← Generated reports
│   └── (PDF files go here)
│
├── logs/                   ← Application logs
│   └── app.log
│
└── tests/                  ← Unit tests
    ├── __init__.py
    └── test_data_loader.py
```

---

## 28.5 Implementation Plan

### Phase 1: Foundation (Session 28)

- [ ] Select project topic
- [ ] Write requirements document
- [ ] Design class hierarchy
- [ ] Set up project structure (folders, `__init__.py`, `requirements.txt`)
- [ ] Create virtual environment
- [ ] Install dependencies

### Phase 2: Data Layer (Session 29 — First Half)

- [ ] Create model classes (data records)
- [ ] Implement DataLoader (CSV reading with validation)
- [ ] Implement data processing/analysis functions
- [ ] Add error handling and logging
- [ ] Test with sample data

### Phase 3: Report Generation (Session 29 — Second Half)

- [ ] Implement PDF generation with fpdf2
- [ ] Add tables, headers, and formatting to PDF
- [ ] Generate charts with matplotlib
- [ ] Embed charts in PDF report
- [ ] Add summary statistics

### Phase 4: Integration & Polish (Session 30)

- [ ] Build menu-driven main program
- [ ] Connect all components
- [ ] End-to-end testing
- [ ] Error handling and edge cases
- [ ] Documentation (README)
- [ ] Prepare for presentation

---

## 28.6 Dependencies Setup

### requirements.txt

```
fpdf2==2.7.6
matplotlib==3.8.2
openpyxl==3.1.2
requests==2.31.0
python-dotenv==1.0.0
```

### Installation

```bash
# Create virtual environment
python -m venv venv

# Activate (Windows)
venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### fpdf2 Quick Reference

```python
from fpdf import FPDF

pdf = FPDF()
pdf.add_page()
pdf.set_font("Helvetica", size=24)
pdf.cell(0, 15, "My Report Title", align="C", new_x="LMARGIN", new_y="NEXT")
pdf.set_font("Helvetica", size=12)
pdf.cell(0, 10, "Subtitle text here", align="C", new_x="LMARGIN", new_y="NEXT")
pdf.ln(10)
pdf.cell(0, 8, "This is a paragraph of text in the PDF.", new_x="LMARGIN", new_y="NEXT")
pdf.output("sample.pdf")
print("PDF created!")
```

### matplotlib Quick Reference

```python
import matplotlib.pyplot as plt

# Bar chart
categories = ["Electronics", "Stationery", "Furniture"]
values = [84500, 22560, 13500]

plt.figure(figsize=(8, 5))
plt.bar(categories, values, color=["#2196F3", "#4CAF50", "#FF9800"])
plt.title("Revenue by Category")
plt.ylabel("Revenue (₹)")
plt.tight_layout()
plt.savefig("chart.png", dpi=150)
plt.close()
print("Chart saved!")
```

---

## 28.7 Evaluation Rubric

| Criterion | Points | Description |
|-----------|--------|-------------|
| **Functionality** | 25 | All features work correctly |
| **OOP Design** | 20 | Classes, inheritance, encapsulation, abstraction |
| **File Handling** | 15 | CSV/JSON read/write, PDF generation |
| **Error Handling** | 10 | Robust exception handling, no crashes |
| **Code Quality** | 10 | Clean, well-organized, documented code |
| **Project Structure** | 5 | Proper packages, modules, separation |
| **PDF Report Quality** | 10 | Professional formatting, tables, charts |
| **Presentation** | 5 | Clear demo and explanation |
| **Total** | **100** | |

---

## 28.8 Common Pitfalls to Avoid

| Pitfall | Solution |
|---------|---------|
| **Too ambitious scope** | Start with core features, add extras if time allows |
| **No error handling** | Add try-except from the start, not at the end |
| **Monolithic code** | Split into modules/packages from day one |
| **Hardcoded paths** | Use config.py or os.path.join() |
| **No sample data** | Create realistic sample CSV files early |
| **Poor PDF formatting** | Plan layout on paper before coding |
| **Skipping testing** | Test each component as you build it |
| **No documentation** | Write README as you go, not at the end |

---

## 🔧 Workshop Activity: Plan Your Capstone

**Duration:** 30 minutes

### Step 1: Select Your Topic (5 min)
Choose from the suggested topics or propose your own.

### Step 2: Write Requirements (10 min)
List 6–8 features your project will include.

### Step 3: Design Classes (10 min)
Sketch your class hierarchy on paper:
- What are the main classes?
- What attributes and methods does each have?
- Which classes inherit from others?

### Step 4: Set Up Project (5 min)
Create the project folder structure and `requirements.txt`.

```bash
mkdir capstone_project
cd capstone_project
mkdir models services utils data output logs tests
touch main.py config.py requirements.txt README.md
touch models/__init__.py services/__init__.py utils/__init__.py tests/__init__.py
```

---

## Session 28 — Key Takeaways

1. **Choose a focused topic** that demonstrates all course skills
2. **Plan before coding** — requirements document, class design, structure
3. **Set up properly** — virtual environment, packages, requirements.txt
4. **Phase your work** — Foundation → Data → Reports → Polish
5. **Start simple** — get core features working, then enhance
6. **fpdf2 + matplotlib** enable professional PDF reports with charts

---

## Preparation for Session 29
- Finalize your project topic and requirements
- Set up your project folder structure
- Install all dependencies (`pip install -r requirements.txt`)
- Prepare sample data (CSV files) for your project
- Be ready to code: Session 29 is the full build session

---

*Session 28 of 30 | Module 6: Automation & Capstone Project*
*Professional Python Programming Certification — UpSkill Global Education Technologies Inc., Canada*
