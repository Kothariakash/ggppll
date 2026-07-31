# Session 10 — Online Ticket Booking System (Module 2 Project)
## Module 2: Control Flow & Functions | Professional Python Programming Certification
### Duration: 1 Hour | Type: Hands-On Project | Project: Build an Online Ticket Booking System

---

## Learning Objectives
By the end of this session, you will be able to:
1. Apply conditionals, loops, functions, and modules in a real-world project
2. Build a menu-driven console application
3. Implement business logic for pricing, discounts, and seat management
4. Structure a program using functions and modules
5. Handle user input validation robustly

---

## 10.1 Project Overview

### The Brief

> Build an **Online Ticket Booking System** for a cinema that allows users to view movies, select showtime, choose seat category, apply discounts, book tickets, and view booking history.

### Features

| Feature | Concepts Used |
|---------|--------------|
| Movie listing and selection | Lists, loops, formatted output |
| Showtime selection | Conditionals, input validation |
| Seat category pricing | if-elif-else, dictionaries |
| Discount rules (age, student, group) | Nested conditions, logical operators |
| Booking confirmation | Functions, f-string formatting |
| Booking history | Lists, accumulator pattern |
| Menu-driven navigation | while loop, match-case or if-elif |
| Input validation | Loops, string methods |
| Utility functions | Custom module, reusable functions |
| Unique booking ID | random module, string formatting |

---

## 10.2 System Design

### Movie Data

```python
movies = [
    {"id": 1, "title": "Interstellar", "genre": "Sci-Fi", "duration": "2h 49m", "rating": "8.7"},
    {"id": 2, "title": "The Dark Knight", "genre": "Action", "duration": "2h 32m", "rating": "9.0"},
    {"id": 3, "title": "Inception", "genre": "Thriller", "duration": "2h 28m", "rating": "8.8"},
    {"id": 4, "title": "Oppenheimer", "genre": "Drama", "duration": "3h 00m", "rating": "8.4"},
    {"id": 5, "title": "Dune: Part Two", "genre": "Sci-Fi", "duration": "2h 46m", "rating": "8.6"},
]
```

### Showtimes

```python
showtimes = ["10:00 AM", "01:30 PM", "05:00 PM", "09:00 PM"]
```

### Seat Categories and Pricing

| Category | Base Price (₹) |
|----------|---------------|
| Silver | 150 |
| Gold | 250 |
| Platinum | 400 |

### Discount Rules

| Rule | Discount | Condition |
|------|----------|-----------|
| Child (under 12) | 50% off | Age < 12 |
| Senior Citizen | 30% off | Age ≥ 60 |
| Student | 20% off | Student = yes |
| Group Discount | 10% off | 4+ tickets |
| Morning Show | ₹30 off per ticket | 10:00 AM show |

### Surcharges

| Rule | Surcharge |
|------|-----------|
| Weekend (Sat/Sun) | +₹50 per ticket |
| 3D Movie | +₹80 per ticket |

---

## 10.3 Function Design

### Recommended Functions

```python
def display_movies(movies):
    """Display all available movies in a formatted table."""

def select_movie(movies):
    """Let user choose a movie. Returns selected movie dict."""

def select_showtime(showtimes):
    """Let user choose a showtime. Returns selected time string."""

def select_seat_category():
    """Let user choose seat category. Returns (category, base_price)."""

def get_ticket_count():
    """Get number of tickets (1-10). Returns int."""

def get_customer_info():
    """Get customer name, age, student status. Returns dict."""

def calculate_price(base_price, count, customer, showtime, is_weekend, is_3d):
    """Calculate total price with all discounts and surcharges. Returns dict with breakdown."""

def generate_booking_id():
    """Generate a unique booking ID like BK-20240115-A3X7."""

def display_booking(booking):
    """Display formatted booking confirmation."""

def display_booking_history(bookings):
    """Display all past bookings."""

def get_valid_input(prompt, valid_options):
    """Get validated input from user. Returns valid choice."""
```

---

## 10.4 Step-by-Step Build Guide

### Step 1: Helper Functions

```python
import random
import string
from datetime import datetime

def generate_booking_id():
    """Generate a unique booking ID."""
    date_part = datetime.now().strftime("%Y%m%d")
    random_part = ''.join(random.choices(string.ascii_uppercase + string.digits, k=4))
    return f"BK-{date_part}-{random_part}"

def get_valid_int(prompt, min_val, max_val):
    """Get a validated integer input within range."""
    while True:
        try:
            value = int(input(prompt))
            if min_val <= value <= max_val:
                return value
            print(f"  Please enter a number between {min_val} and {max_val}.")
        except ValueError:
            print("  Invalid input. Please enter a number.")

def get_yes_no(prompt):
    """Get a yes/no response. Returns True for yes."""
    while True:
        response = input(prompt).strip().lower()
        if response in ("y", "yes"):
            return True
        if response in ("n", "no"):
            return False
        print("  Please enter 'yes' or 'no'.")
```

### Step 2: Display Functions

```python
def display_movies(movies):
    """Display all available movies."""
    print(f"\n{'─' * 65}")
    print(f"  {'#':<4} {'Title':<22} {'Genre':<12} {'Duration':<10} {'Rating'}")
    print(f"{'─' * 65}")
    for movie in movies:
        print(f"  {movie['id']:<4} {movie['title']:<22} {movie['genre']:<12} "
              f"{movie['duration']:<10} ★ {movie['rating']}")
    print(f"{'─' * 65}")

def display_showtimes(showtimes):
    """Display available showtimes."""
    print("\n  Available Showtimes:")
    for i, time in enumerate(showtimes, 1):
        print(f"    {i}. {time}")
```

### Step 3: Selection Functions

```python
def select_movie(movies):
    """Let user select a movie."""
    display_movies(movies)
    choice = get_valid_int("  Select movie number: ", 1, len(movies))
    return movies[choice - 1]

def select_showtime(showtimes):
    """Let user select a showtime."""
    display_showtimes(showtimes)
    choice = get_valid_int("  Select showtime: ", 1, len(showtimes))
    return showtimes[choice - 1]

def select_seat_category():
    """Let user select seat category."""
    categories = {
        "1": ("Silver", 150),
        "2": ("Gold", 250),
        "3": ("Platinum", 400),
    }
    print("\n  Seat Categories:")
    print(f"    1. Silver   — ₹150")
    print(f"    2. Gold     — ₹250")
    print(f"    3. Platinum — ₹400")
    choice = get_valid_int("  Select category: ", 1, 3)
    return categories[str(choice)]
```

### Step 4: Price Calculation

```python
def calculate_price(base_price, ticket_count, customer_info, showtime, is_weekend, is_3d):
    """Calculate total with all discounts and surcharges."""
    subtotal = base_price * ticket_count
    
    # Discounts
    discounts = {}
    
    # Age-based discount
    age = customer_info["age"]
    if age < 12:
        disc = subtotal * 0.50
        discounts["Child Discount (50%)"] = disc
    elif age >= 60:
        disc = subtotal * 0.30
        discounts["Senior Discount (30%)"] = disc
    
    # Student discount
    if customer_info["is_student"] and 12 <= age < 60:
        disc = subtotal * 0.20
        discounts["Student Discount (20%)"] = disc
    
    # Group discount
    if ticket_count >= 4:
        disc = subtotal * 0.10
        discounts["Group Discount (10%)"] = disc
    
    # Morning show discount
    if showtime == "10:00 AM":
        disc = 30 * ticket_count
        discounts["Morning Show (₹30/ticket)"] = disc
    
    total_discount = sum(discounts.values())
    
    # Surcharges
    surcharges = {}
    if is_weekend:
        sur = 50 * ticket_count
        surcharges["Weekend Surcharge (₹50/ticket)"] = sur
    if is_3d:
        sur = 80 * ticket_count
        surcharges["3D Surcharge (₹80/ticket)"] = sur
    
    total_surcharge = sum(surcharges.values())
    
    # Final total
    final_total = subtotal - total_discount + total_surcharge
    
    return {
        "subtotal": subtotal,
        "discounts": discounts,
        "total_discount": total_discount,
        "surcharges": surcharges,
        "total_surcharge": total_surcharge,
        "final_total": max(0, final_total),
    }
```

### Step 5: Booking Display

```python
def display_booking(booking):
    """Display formatted booking confirmation."""
    print("\n" + "╔" + "═" * 55 + "╗")
    print("║" + "BOOKING CONFIRMATION".center(55) + "║")
    print("╠" + "═" * 55 + "╣")
    print(f"║  Booking ID  : {booking['id']:<38}║")
    print(f"║  Date/Time   : {booking['timestamp']:<38}║")
    print("╠" + "═" * 55 + "╣")
    print(f"║  Customer    : {booking['customer']:<38}║")
    print(f"║  Movie       : {booking['movie']:<38}║")
    print(f"║  Showtime    : {booking['showtime']:<38}║")
    print(f"║  Category    : {booking['category']:<38}║")
    print(f"║  Tickets     : {booking['tickets']:<38}║")
    print("╠" + "═" * 55 + "╣")
    
    pricing = booking["pricing"]
    print(f"║  Subtotal    : ₹{pricing['subtotal']:>8,.2f}{'':<27}║")
    
    for name, amount in pricing["discounts"].items():
        print(f"║    - {name:<25}: -₹{amount:>8,.2f}  ║")
    
    for name, amount in pricing["surcharges"].items():
        print(f"║    + {name:<25}: +₹{amount:>8,.2f}  ║")
    
    print("╠" + "═" * 55 + "╣")
    print(f"║  TOTAL PAYABLE: ₹{pricing['final_total']:>8,.2f}{'':<26}║")
    print("╚" + "═" * 55 + "╝")
```

### Step 6: Main Program Loop

```python
def main():
    """Main program — menu-driven ticket booking."""
    # Data
    movies = [
        {"id": 1, "title": "Interstellar", "genre": "Sci-Fi", "duration": "2h 49m", "rating": "8.7"},
        {"id": 2, "title": "The Dark Knight", "genre": "Action", "duration": "2h 32m", "rating": "9.0"},
        {"id": 3, "title": "Inception", "genre": "Thriller", "duration": "2h 28m", "rating": "8.8"},
        {"id": 4, "title": "Oppenheimer", "genre": "Drama", "duration": "3h 00m", "rating": "8.4"},
        {"id": 5, "title": "Dune: Part Two", "genre": "Sci-Fi", "duration": "2h 46m", "rating": "8.6"},
    ]
    showtimes = ["10:00 AM", "01:30 PM", "05:00 PM", "09:00 PM"]
    bookings = []
    
    print("=" * 55)
    print("   ONLINE TICKET BOOKING SYSTEM")
    print("=" * 55)
    
    while True:
        print("\n--- MAIN MENU ---")
        print("  1. Book Tickets")
        print("  2. View Booking History")
        print("  3. View Movies")
        print("  4. Exit")
        
        choice = get_valid_int("  Enter choice: ", 1, 4)
        
        if choice == 1:
            # Book tickets
            movie = select_movie(movies)
            showtime = select_showtime(showtimes)
            category, base_price = select_seat_category()
            ticket_count = get_valid_int("  Number of tickets (1-10): ", 1, 10)
            
            # Customer info
            print("\n--- Customer Information ---")
            name = input("  Your name: ").strip().title()
            age = get_valid_int("  Your age: ", 1, 120)
            is_student = get_yes_no("  Are you a student? (yes/no): ")
            is_weekend = get_yes_no("  Is this for a weekend? (yes/no): ")
            is_3d = get_yes_no("  3D movie? (yes/no): ")
            
            customer_info = {"name": name, "age": age, "is_student": is_student}
            
            # Calculate
            pricing = calculate_price(base_price, ticket_count, customer_info, showtime, is_weekend, is_3d)
            
            # Create booking
            booking = {
                "id": generate_booking_id(),
                "timestamp": datetime.now().strftime("%d %b %Y, %I:%M %p"),
                "customer": name,
                "movie": movie["title"],
                "showtime": showtime,
                "category": category,
                "tickets": ticket_count,
                "pricing": pricing,
            }
            
            # Display and confirm
            display_booking(booking)
            
            if get_yes_no("\n  Confirm booking? (yes/no): "):
                bookings.append(booking)
                print("\n  ✅ Booking confirmed! Enjoy the movie!")
            else:
                print("\n  ❌ Booking cancelled.")
        
        elif choice == 2:
            # View history
            if not bookings:
                print("\n  No bookings yet.")
            else:
                print(f"\n--- Booking History ({len(bookings)} bookings) ---")
                for b in bookings:
                    print(f"  {b['id']} | {b['movie']:<20} | {b['showtime']} | "
                          f"{b['tickets']} tickets | ₹{b['pricing']['final_total']:,.2f}")
        
        elif choice == 3:
            display_movies(movies)
        
        elif choice == 4:
            print("\n  Thank you for using the Ticket Booking System!")
            print("  Goodbye!")
            break

if __name__ == "__main__":
    main()
```

---

## 10.5 Concepts Applied — Module 2 Recap

| Concept | Where Used | Session |
|---------|-----------|---------|
| if-elif-else | Age-based discounts, grade rules | Session 6 |
| Nested conditions | Discount eligibility logic | Session 6 |
| Ternary expressions | Display status text | Session 6 |
| for loops | Display movie list, iterate bookings | Session 7 |
| while loops | Menu loop, input validation | Session 7 |
| break | Exit menu loop | Session 7 |
| enumerate() | Numbered showtime display | Session 7 |
| Functions (def) | All operations split into functions | Session 8 |
| Parameters & return | All functions use params/return | Session 8 |
| Default parameters | Optional function arguments | Session 8 |
| Scope | Local variables in functions | Session 8 |
| import modules | random, string, datetime | Session 9 |
| `__name__` guard | Main entry point | Session 9 |

---

## 10.6 Evaluation Rubric

| Criterion | Points | Check |
|-----------|--------|-------|
| Movie listing displays correctly | 10 | |
| Showtime and seat selection works | 10 | |
| Ticket count validation (1-10) | 5 | |
| Customer info collected with validation | 10 | |
| All discount rules applied correctly | 15 | |
| Surcharges applied correctly | 10 | |
| Price breakdown displayed clearly | 10 | |
| Booking confirmation formatted | 10 | |
| Booking history works | 5 | |
| Menu-driven flow with exit | 5 | |
| Code uses functions (minimum 5) | 5 | |
| Input validation (no crashes) | 5 | |
| **Total** | **100** | |

---

## 🔧 Hands-On Activity: Build the Online Ticket Booking System

**Duration:** 40 minutes

### Minimum Requirements
1. Display at least 3 movies
2. Showtime selection (at least 3 options)
3. Seat category selection with pricing
4. At least 2 discount rules
5. Price calculation and display
6. Booking confirmation
7. Menu-driven with exit option
8. Use at least 5 functions

### Save as `session10_ticket_booking.py`

---

## Session 10 — Key Takeaways

1. **Real-world programs** combine conditionals, loops, functions, and modules
2. **Menu-driven design** with `while True` + `break` is a standard console app pattern
3. **Functions** make the code modular, testable, and readable
4. **Input validation** prevents crashes — never trust user input
5. **Separate concerns:** display functions, calculation functions, data functions

---

## Module 2 Complete — Summary

| Session | Topic | Key Skill |
|---------|-------|-----------|
| 6 | Conditional Statements | if-elif-else, nested, ternary, match-case |
| 7 | Loops | for, while, break/continue, enumerate, comprehensions |
| 8 | Functions | def, return, *args, **kwargs, lambda, recursion, scope |
| 9 | Modules & Packages | import, standard library, custom modules, pip |
| 10 | Ticket Booking System | End-to-end project with all Module 2 skills |

### Module 2 → Module 3 Bridge

You now know how to **make decisions, repeat actions, organize code into functions, and use modules**. In Module 3 (Sessions 11–15), you'll master Python's **Data Structures** — Lists, Tuples, Dictionaries, Sets, and Strings — and build an **Inventory Management System**.

---

## Preparation for Session 11
- Think about: What is the difference between a list and a tuple?
- Review: You've already used lists briefly — now we'll go deep
- Practice: Create a list of 5 items and try `.append()`, `.remove()`, `.sort()`

---

*Session 10 of 30 | Module 2: Control Flow & Functions*
*Professional Python Programming Certification — UpSkill Global Education Technologies Inc., Canada*
