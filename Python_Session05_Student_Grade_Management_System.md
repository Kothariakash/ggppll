# Session 5 — Student Grade Management System (Module 1 Project)
## Module 1: Python Fundamentals | Professional Python Programming Certification
### Duration: 1 Hour | Type: Hands-On Project | Project: Build a Student Grade Management System

---

## Learning Objectives
By the end of this session, you will be able to:
1. Apply all Module 1 concepts in a real-world project
2. Build an interactive console application
3. Collect, process, and display student data
4. Perform grade calculations and generate formatted reports
5. Validate user input effectively

---

## 5.1 Project Overview

### The Brief

> Build a **Student Grade Management System** that accepts student information and subject marks, calculates grades, and displays a formatted report card.

### Features

| Feature | Concepts Used |
|---------|--------------|
| Collect student name, roll number, age | Variables, input(), strings |
| Accept marks for 5 subjects | int/float conversion, input |
| Calculate total, percentage, grade | Arithmetic operators |
| Determine pass/fail status | Comparison operators, logical operators |
| Display a formatted report card | f-strings, print formatting |
| Input validation | String methods, conditional checks |
| Multiple student support | Loops (preview — covered in Session 7) |

---

## 5.2 Grading System

### Grade Criteria

| Percentage Range | Grade | Remark |
|-----------------|-------|--------|
| 90% and above | A+ | Outstanding |
| 80% – 89% | A | Excellent |
| 70% – 79% | B+ | Very Good |
| 60% – 69% | B | Good |
| 50% – 59% | C | Average |
| 40% – 49% | D | Below Average |
| Below 40% | F | Fail |

### Pass/Fail Rules

- **Pass:** Percentage ≥ 40% AND no individual subject below 33%
- **Fail:** Percentage < 40% OR any subject below 33%

---

## 5.3 Project Design

### Input Requirements

| Field | Type | Validation |
|-------|------|-----------|
| Student Name | str | Non-empty, alphabets and spaces only |
| Roll Number | str | Non-empty |
| Age | int | Between 5 and 25 |
| Subject Names | str | 5 subjects |
| Subject Marks | int/float | Between 0 and 100 |

### Output — Report Card Format

```
╔══════════════════════════════════════════════════╗
║              STUDENT REPORT CARD                 ║
╠══════════════════════════════════════════════════╣
║  Name       : Priya Sharma                      ║
║  Roll No    : STU-2024-001                       ║
║  Age        : 20 years                           ║
╠══════════════════════════════════════════════════╣
║  Subject          Marks    Max    Status         ║
║  ─────────────────────────────────────────       ║
║  Mathematics       85     100     Pass           ║
║  Physics           72     100     Pass           ║
║  Chemistry         68     100     Pass           ║
║  English           90     100     Pass           ║
║  Computer Sci      95     100     Pass           ║
╠══════════════════════════════════════════════════╣
║  Total Marks  : 410 / 500                        ║
║  Percentage   : 82.00%                           ║
║  Grade        : A                                ║
║  Result       : PASS                             ║
╚══════════════════════════════════════════════════╝
```

---

## 5.4 Step-by-Step Build Guide

### Step 1: Program Header

```python
# Student Grade Management System
# Module 1 Project — Python Fundamentals
# Author: [Your Name]
# Date: [Today's Date]

print("=" * 55)
print("   STUDENT GRADE MANAGEMENT SYSTEM")
print("   Module 1 Project — Python Fundamentals")
print("=" * 55)
```

### Step 2: Collect Student Information

```python
# --- Student Information ---
print("\n--- Enter Student Details ---\n")

# Name validation
while True:
    name = input("Student Name: ").strip().title()
    if name.replace(" ", "").isalpha() and len(name) > 0:
        break
    print("  ⚠ Invalid! Name must contain only letters and spaces.")

# Roll number
roll_no = input("Roll Number: ").strip()

# Age validation
while True:
    age_str = input("Age: ").strip()
    if age_str.isdigit() and 5 <= int(age_str) <= 25:
        age = int(age_str)
        break
    print("  ⚠ Invalid! Age must be between 5 and 25.")
```

### Step 3: Collect Subject Marks

```python
# --- Subject Marks ---
print("\n--- Enter Marks for 5 Subjects (0-100) ---\n")

subjects = ["Mathematics", "Physics", "Chemistry", "English", "Computer Science"]
marks = []
max_marks = 100

for i in range(5):
    while True:
        mark_str = input(f"  {subjects[i]}: ").strip()
        try:
            mark = float(mark_str)
            if 0 <= mark <= 100:
                marks.append(mark)
                break
            else:
                print("    ⚠ Marks must be between 0 and 100.")
        except ValueError:
            print("    ⚠ Invalid! Please enter a number.")
```

### Step 4: Calculate Results

```python
# --- Calculations ---
total_marks = sum(marks)
total_max = max_marks * len(subjects)
percentage = (total_marks / total_max) * 100

# Check individual subject pass (minimum 33 per subject)
min_pass_mark = 33
all_subjects_passed = all(m >= min_pass_mark for m in marks)

# Determine pass/fail
is_passed = percentage >= 40 and all_subjects_passed

# Determine grade
if percentage >= 90:
    grade = "A+"
    remark = "Outstanding"
elif percentage >= 80:
    grade = "A"
    remark = "Excellent"
elif percentage >= 70:
    grade = "B+"
    remark = "Very Good"
elif percentage >= 60:
    grade = "B"
    remark = "Good"
elif percentage >= 50:
    grade = "C"
    remark = "Average"
elif percentage >= 40:
    grade = "D"
    remark = "Below Average"
else:
    grade = "F"
    remark = "Fail"

# Override remark if failed due to individual subject
if not is_passed and percentage >= 40:
    remark = "Failed in individual subject(s)"
```

### Step 5: Display Report Card

```python
# --- Report Card ---
print("\n")
print("╔" + "═" * 55 + "╗")
print("║" + "STUDENT REPORT CARD".center(55) + "║")
print("╠" + "═" * 55 + "╣")

# Student info
print(f"║  {'Name':<14}: {name:<38}║")
print(f"║  {'Roll No':<14}: {roll_no:<38}║")
print(f"║  {'Age':<14}: {age} years{'':<32}║")

# Subject marks header
print("╠" + "═" * 55 + "╣")
print(f"║  {'Subject':<20} {'Marks':>6} {'Max':>6} {'Status':>10}     ║")
print(f"║  {'─' * 47}     ║")

# Subject rows
for i in range(len(subjects)):
    status = "Pass" if marks[i] >= min_pass_mark else "FAIL"
    print(f"║  {subjects[i]:<20} {marks[i]:>6.1f} {max_marks:>6} {status:>10}     ║")

# Summary
print("╠" + "═" * 55 + "╣")
print(f"║  {'Total Marks':<14}: {total_marks:.1f} / {total_max}{'':<28}║")
print(f"║  {'Percentage':<14}: {percentage:.2f}%{'':<33}║")
print(f"║  {'Grade':<14}: {grade}{'':<37}║")
print(f"║  {'Remark':<14}: {remark:<38}║")
print(f"║  {'Result':<14}: {'✅ PASS' if is_passed else '❌ FAIL':<38}║")
print("╚" + "═" * 55 + "╝")
```

### Step 6: Summary Statistics

```python
# --- Additional Statistics ---
print(f"\n--- Performance Summary ---")

highest_mark = max(marks)
lowest_mark = min(marks)
highest_subject = subjects[marks.index(highest_mark)]
lowest_subject = subjects[marks.index(lowest_mark)]
average_mark = total_marks / len(subjects)

print(f"  Highest Score : {highest_mark:.1f} ({highest_subject})")
print(f"  Lowest Score  : {lowest_mark:.1f} ({lowest_subject})")
print(f"  Average Score : {average_mark:.2f}")
print(f"  Subjects Above 80: {sum(1 for m in marks if m >= 80)}")
print(f"  Subjects Below 40: {sum(1 for m in marks if m < 40)}")
```

---

## 5.5 Complete Program — Simplified Version

For students who want a simpler version without loops (using only Session 1–4 concepts):

```python
# ============================================
# STUDENT GRADE MANAGEMENT SYSTEM (Simplified)
# ============================================

print("=" * 50)
print("  STUDENT GRADE MANAGEMENT SYSTEM")
print("=" * 50)

# Input
name = input("\nStudent Name: ").strip().title()
roll_no = input("Roll Number: ").strip()
age = int(input("Age: "))

print("\nEnter marks for each subject (0-100):")
math = float(input("  Mathematics: "))
physics = float(input("  Physics: "))
chemistry = float(input("  Chemistry: "))
english = float(input("  English: "))
computer = float(input("  Computer Science: "))

# Calculations
total = math + physics + chemistry + english + computer
percentage = (total / 500) * 100

# Grade determination
if percentage >= 90:
    grade, remark = "A+", "Outstanding"
elif percentage >= 80:
    grade, remark = "A", "Excellent"
elif percentage >= 70:
    grade, remark = "B+", "Very Good"
elif percentage >= 60:
    grade, remark = "B", "Good"
elif percentage >= 50:
    grade, remark = "C", "Average"
elif percentage >= 40:
    grade, remark = "D", "Below Average"
else:
    grade, remark = "F", "Fail"

# Pass/Fail check
min_pass = 33
passed_all = (math >= min_pass and physics >= min_pass and 
              chemistry >= min_pass and english >= min_pass and 
              computer >= min_pass)
is_passed = percentage >= 40 and passed_all
result = "PASS" if is_passed else "FAIL"

# Highest and lowest
scores = {"Mathematics": math, "Physics": physics, "Chemistry": chemistry,
          "English": english, "Computer Science": computer}

# Display Report Card
print("\n" + "=" * 50)
print("         REPORT CARD")
print("=" * 50)
print(f"  Name       : {name}")
print(f"  Roll No    : {roll_no}")
print(f"  Age        : {age}")
print("-" * 50)
print(f"  {'Subject':<20} {'Marks':>8} {'Status':>10}")
print(f"  {'-' * 40}")
print(f"  {'Mathematics':<20} {math:>8.1f} {'Pass' if math >= min_pass else 'FAIL':>10}")
print(f"  {'Physics':<20} {physics:>8.1f} {'Pass' if physics >= min_pass else 'FAIL':>10}")
print(f"  {'Chemistry':<20} {chemistry:>8.1f} {'Pass' if chemistry >= min_pass else 'FAIL':>10}")
print(f"  {'English':<20} {english:>8.1f} {'Pass' if english >= min_pass else 'FAIL':>10}")
print(f"  {'Computer Science':<20} {computer:>8.1f} {'Pass' if computer >= min_pass else 'FAIL':>10}")
print("-" * 50)
print(f"  Total      : {total:.1f} / 500")
print(f"  Percentage : {percentage:.2f}%")
print(f"  Grade      : {grade}")
print(f"  Remark     : {remark}")
print(f"  Result     : {result}")
print("=" * 50)

print(f"\n  Highest: {max(math, physics, chemistry, english, computer):.1f}")
print(f"  Lowest : {min(math, physics, chemistry, english, computer):.1f}")
print(f"  Average: {total / 5:.2f}")

print("\nReport generated successfully!")
```

---

## 5.6 Concepts Applied — Module 1 Recap

| Concept | Where Used | Session |
|---------|-----------|---------|
| `print()` with formatting | Report card display | Session 1 |
| Variables (str, int, float) | Student name, age, marks | Session 2 |
| f-strings with alignment | Table formatting | Session 2, 4 |
| Type conversion (`int()`, `float()`) | Converting input to numbers | Session 2 |
| Arithmetic operators (`+`, `/`, `*`) | Total, percentage, average | Session 3 |
| Comparison operators (`>=`, `<`) | Grade boundaries, pass/fail | Session 3 |
| Logical operators (`and`) | Combined pass/fail check | Session 3 |
| `input()` for user data | Collecting student information | Session 4 |
| String methods (`.strip()`, `.title()`) | Cleaning input | Session 4 |
| Input validation (`.isdigit()`, `.isalpha()`) | Validating name, age, marks | Session 4 |
| `max()`, `min()`, `sum()` | Statistics | Built-in functions |
| Conditional expressions | Ternary for pass/fail display | Session 3 |

---

## 🔧 Hands-On Activity: Build the Student Grade Management System

**Duration:** 40 minutes

### Requirements

1. Collect: Student name, roll number, age
2. Collect: Marks for 5 subjects (0–100)
3. Calculate: Total, percentage, grade (use the grading table in 5.2)
4. Determine: Pass/Fail (percentage ≥ 40 AND all subjects ≥ 33)
5. Display: Formatted report card with borders and alignment
6. Display: Highest, lowest, and average marks

### Submission Checklist

- [ ] Program runs without errors
- [ ] Input validation: name (alpha only), age (5-25), marks (0-100)
- [ ] Correct total, percentage, and grade calculation
- [ ] Pass/fail logic handles both overall and individual subject rules
- [ ] Report card is formatted with alignment and borders
- [ ] Statistics displayed (highest, lowest, average)
- [ ] Code is well-commented
- [ ] File saved as `session05_grade_system.py`

### Bonus Challenges

1. **Multiple students:** Ask "Add another student? (y/n)" and loop
2. **Class topper:** If multiple students, identify who scored highest
3. **Subject analysis:** Show which subject had the highest class average
4. **Save to file:** Write the report card to a `.txt` file using `print(file=f)`

---

## Session 5 — Key Takeaways

1. **Real-world applications** combine all fundamental concepts — variables, operators, I/O, formatting
2. **Input validation** is essential — never trust user input
3. **Formatted output** with f-strings creates professional-looking reports
4. **Conditional logic** drives business rules like grading and pass/fail
5. **Breaking a problem into steps** (input → process → output) is a fundamental programming pattern

---

## Module 1 Complete — Summary

| Session | Topic | Key Skill |
|---------|-------|-----------|
| 1 | Installation & Setup | Python install, VS Code, first program |
| 2 | Variables & Data Types | int, float, str, bool, None, type conversion |
| 3 | Operators | Arithmetic, comparison, logical, identity, membership |
| 4 | Input & Output | input(), f-strings, formatting, validation |
| 5 | Student Grade System | End-to-end project combining all Module 1 skills |

### Module 1 → Module 2 Bridge

You now know how to **store data, perform calculations, get user input, and display formatted output**. In Module 2 (Sessions 6–10), you'll learn **control flow** — how to make decisions (`if/elif/else`), repeat actions (`for/while` loops), organize code into reusable **functions**, and build an **Online Ticket Booking System**.

---

## Preparation for Session 6
- Review: What is an if/else statement?
- Think about: How would you check multiple conditions (e.g., age ranges for ticket pricing)?
- Practice: Try writing `if age >= 18: print("Adult")` in the Python interpreter

---

*Session 5 of 30 | Module 1: Python Fundamentals*
*Professional Python Programming Certification — UpSkill Global Education Technologies Inc., Canada*
