# Session 14 — Strings in Python (Deep Dive)
## Module 3: Data Structures | Professional Python Programming Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Text Processing & String Manipulation

---

## Learning Objectives
By the end of this session, you will be able to:
1. Master all essential string methods for text processing
2. Perform advanced slicing, searching, and replacing
3. Use regular expressions for pattern matching (intro)
4. Format strings for professional output
5. Build a text analysis tool

---

## 14.1 Strings Recap & Deep Dive

### String Creation

```python
# Different quote styles
single = 'Hello'
double = "Hello"
triple_single = '''Multi-line
string'''
triple_double = """Also multi-line
string"""
raw = r"C:\Users\new\folder"      # Raw — no escape processing
byte = b"Hello"                    # Bytes string
f_string = f"Value: {42}"          # Formatted string

# String from other types
s = str(42)         # "42"
s = str(3.14)       # "3.14"
s = str([1, 2, 3])  # "[1, 2, 3]"
```

### Strings Are Immutable Sequences

```python
text = "Python"

# Access characters (indexing)
print(text[0])      # P
print(text[-1])     # n

# Slicing
print(text[0:3])    # Pyt
print(text[::2])    # Pto
print(text[::-1])   # nohtyP

# Iteration
for char in text:
    print(char, end=" ")  # P y t h o n

# Length
print(len(text))    # 6

# Membership
print("th" in text)     # True
print("xyz" not in text) # True

# Cannot modify
# text[0] = "J"  # TypeError: 'str' object does not support item assignment
```

---

## 14.2 String Methods — Case Conversion

```python
text = "Hello, World! Python is GREAT."

print(text.upper())        # HELLO, WORLD! PYTHON IS GREAT.
print(text.lower())        # hello, world! python is great.
print(text.title())        # Hello, World! Python Is Great.
print(text.capitalize())   # Hello, world! python is great.
print(text.swapcase())     # hELLO, wORLD! pYTHON IS great.
print(text.casefold())     # hello, world! python is great. (more aggressive than lower)
```

---

## 14.3 String Methods — Search & Find

```python
text = "Python is powerful. Python is popular. Python is fun."

# find() — returns index of first occurrence, -1 if not found
print(text.find("Python"))      # 0
print(text.find("Python", 5))   # 20 (start searching from index 5)
print(text.find("Java"))        # -1

# rfind() — search from right
print(text.rfind("Python"))     # 40

# index() — like find, but raises ValueError if not found
print(text.index("Python"))     # 0
# text.index("Java")           # ValueError!

# count() — count non-overlapping occurrences
print(text.count("Python"))     # 3
print(text.count("is"))         # 3

# startswith() / endswith()
print(text.startswith("Python"))        # True
print(text.endswith("fun."))            # True
print(text.startswith(("Python", "Java")))  # True (tuple of prefixes)
```

---

## 14.4 String Methods — Modification

### replace()

```python
text = "Hello World Hello Python Hello"

# Replace all occurrences
print(text.replace("Hello", "Hi"))
# Hi World Hi Python Hi

# Replace only first N occurrences
print(text.replace("Hello", "Hi", 1))
# Hi World Hello Python Hello
```

### strip(), lstrip(), rstrip()

```python
text = "   Hello, World!   "

print(text.strip())      # "Hello, World!"
print(text.lstrip())     # "Hello, World!   "
print(text.rstrip())     # "   Hello, World!"

# Strip specific characters
csv_line = ",,Alice,25,Delhi,,"
print(csv_line.strip(","))   # "Alice,25,Delhi"

# Common use: clean user input
user_input = "  alice@email.com  \n"
clean = user_input.strip()
print(clean)  # "alice@email.com"
```

### split() and join()

```python
# split() — string to list
sentence = "Python is a great language"
words = sentence.split()
print(words)  # ['Python', 'is', 'a', 'great', 'language']

# Split by specific delimiter
csv = "Alice,25,Delhi,Engineer"
fields = csv.split(",")
print(fields)  # ['Alice', '25', 'Delhi', 'Engineer']

# Split with max splits
data = "name:Alice:age:25:city:Delhi"
parts = data.split(":", 2)
print(parts)  # ['name', 'Alice', 'age:25:city:Delhi']

# splitlines() — split by line breaks
multiline = "Line 1\nLine 2\nLine 3"
lines = multiline.splitlines()
print(lines)  # ['Line 1', 'Line 2', 'Line 3']

# join() — list to string
words = ["Python", "is", "fun"]
sentence = " ".join(words)
print(sentence)  # "Python is fun"

# Join with different separators
print(", ".join(words))      # "Python, is, fun"
print(" -> ".join(words))    # "Python -> is -> fun"
print("\n".join(words))      # Each word on new line

# Join numbers (must be strings)
nums = [1, 2, 3, 4, 5]
print("-".join(str(n) for n in nums))  # "1-2-3-4-5"
```

### Other Modification Methods

```python
# center, ljust, rjust — padding
print("Hello".center(20))         #        Hello
print("Hello".center(20, "-"))    # -------Hello--------
print("Hello".ljust(20, "."))     # Hello...............
print("Hello".rjust(20, "."))     # ...............Hello

# zfill — zero padding
print("42".zfill(5))     # 00042
print("-42".zfill(5))    # -0042

# expandtabs
print("A\tB\tC".expandtabs(10))  # A         B         C

# maketrans + translate — character replacement
table = str.maketrans("aeiou", "12345")
print("hello world".translate(table))  # h2ll4 w4rld

# Remove characters
remove_digits = str.maketrans("", "", "0123456789")
print("abc123def456".translate(remove_digits))  # abcdef
```

---

## 14.5 String Methods — Validation

| Method | Returns True if | Example |
|--------|----------------|---------|
| `.isalpha()` | All letters | `"Hello".isalpha()` → True |
| `.isdigit()` | All digits | `"123".isdigit()` → True |
| `.isalnum()` | Letters + digits | `"abc123".isalnum()` → True |
| `.isspace()` | All whitespace | `"   ".isspace()` → True |
| `.isupper()` | All uppercase | `"HELLO".isupper()` → True |
| `.islower()` | All lowercase | `"hello".islower()` → True |
| `.istitle()` | Title case | `"Hello World".istitle()` → True |
| `.isnumeric()` | Numeric chars | `"½".isnumeric()` → True |
| `.isdecimal()` | Decimal chars | `"123".isdecimal()` → True |
| `.isascii()` | ASCII chars | `"Hello".isascii()` → True |
| `.isprintable()` | Printable chars | `"Hello".isprintable()` → True |
| `.isidentifier()` | Valid variable name | `"my_var".isidentifier()` → True |

```python
# Practical validation
def validate_username(username):
    if not username:
        return "Username cannot be empty"
    if not username[0].isalpha():
        return "Must start with a letter"
    if not username.isalnum():
        return "Only letters and numbers allowed"
    if len(username) < 3 or len(username) > 20:
        return "Must be 3-20 characters"
    return "Valid"

print(validate_username("Alice123"))   # Valid
print(validate_username("1Alice"))     # Must start with a letter
print(validate_username("Al"))         # Must be 3-20 characters
```

---

## 14.6 String Methods — Complete Reference

| Method | Purpose | Example |
|--------|---------|---------|
| `upper()` | All uppercase | `"hi".upper()` → `"HI"` |
| `lower()` | All lowercase | `"HI".lower()` → `"hi"` |
| `title()` | Title case | `"hi there".title()` → `"Hi There"` |
| `capitalize()` | First letter upper | `"hi there".capitalize()` → `"Hi there"` |
| `swapcase()` | Swap case | `"Hi".swapcase()` → `"hI"` |
| `strip()` | Remove whitespace | `" hi ".strip()` → `"hi"` |
| `split(sep)` | String to list | `"a,b,c".split(",")` → `['a','b','c']` |
| `join(list)` | List to string | `",".join(['a','b'])` → `"a,b"` |
| `replace(old, new)` | Replace text | `"hi".replace("hi","hello")` → `"hello"` |
| `find(sub)` | Find index | `"hello".find("ll")` → `2` |
| `count(sub)` | Count occurrences | `"hello".count("l")` → `2` |
| `startswith(s)` | Starts with? | `"hello".startswith("he")` → `True` |
| `endswith(s)` | Ends with? | `"hello".endswith("lo")` → `True` |
| `center(w)` | Center pad | `"hi".center(10)` → `"    hi    "` |
| `ljust(w)` | Left justify | `"hi".ljust(10)` → `"hi        "` |
| `rjust(w)` | Right justify | `"hi".rjust(10)` → `"        hi"` |
| `zfill(w)` | Zero fill | `"42".zfill(5)` → `"00042"` |
| `encode(enc)` | Encode to bytes | `"hi".encode("utf-8")` → `b'hi'` |
| `partition(sep)` | Split into 3 | `"a:b:c".partition(":")` → `('a',':','b:c')` |

---

## 14.7 Regular Expressions (Introduction)

### What are Regular Expressions?

**Regex** (Regular Expressions) are patterns used to search, match, and manipulate text. Python's `re` module provides regex support.

```python
import re

text = "My phone is 9876543210 and email is alice@example.com"

# Find all numbers
numbers = re.findall(r'\d+', text)
print(numbers)  # ['9876543210']

# Find email
emails = re.findall(r'[\w.]+@[\w.]+', text)
print(emails)  # ['alice@example.com']

# Check if string matches pattern
if re.match(r'^\d{10}$', "9876543210"):
    print("Valid 10-digit number")

# Replace
cleaned = re.sub(r'\d', '#', text)
print(cleaned)  # My phone is ########## and email is alice@example.com

# Split by multiple delimiters
data = "Alice;Bob,Charlie:Diana"
names = re.split(r'[;,:]', data)
print(names)  # ['Alice', 'Bob', 'Charlie', 'Diana']
```

### Common Regex Patterns

| Pattern | Matches | Example |
|---------|---------|---------|
| `\d` | Any digit | `0-9` |
| `\D` | Non-digit | Letters, symbols |
| `\w` | Word character | `a-z, A-Z, 0-9, _` |
| `\W` | Non-word char | Spaces, symbols |
| `\s` | Whitespace | Space, tab, newline |
| `.` | Any character | Anything except newline |
| `+` | One or more | `\d+` → "123" |
| `*` | Zero or more | `\d*` → "" or "123" |
| `?` | Zero or one | `colou?r` → "color" or "colour" |
| `{n}` | Exactly n | `\d{3}` → "123" |
| `{n,m}` | n to m | `\d{2,4}` → "12" to "1234" |
| `^` | Start of string | `^Hello` |
| `$` | End of string | `World$` |
| `[abc]` | Character set | `[aeiou]` → any vowel |
| `[^abc]` | Not in set | `[^0-9]` → non-digit |
| `(...)` | Group | `(\d{3})-(\d{4})` |
| `\|` | OR | `cat\|dog` |

### Practical Regex Examples

```python
import re

# Validate email
def is_valid_email(email):
    pattern = r'^[\w.+-]+@[\w-]+\.[\w.]+$'
    return bool(re.match(pattern, email))

# Validate phone (Indian)
def is_valid_phone(phone):
    pattern = r'^[6-9]\d{9}$'
    return bool(re.match(pattern, phone))

# Extract dates from text
text = "Meeting on 15-01-2024 and deadline is 31-03-2024"
dates = re.findall(r'\d{2}-\d{2}-\d{4}', text)
print(dates)  # ['15-01-2024', '31-03-2024']

# Password validation
def is_strong_password(pwd):
    if len(pwd) < 8:
        return False
    if not re.search(r'[A-Z]', pwd):
        return False
    if not re.search(r'[a-z]', pwd):
        return False
    if not re.search(r'\d', pwd):
        return False
    if not re.search(r'[!@#$%^&*]', pwd):
        return False
    return True
```

> Regex is a deep topic — this is an introduction. For advanced regex, refer to Python's `re` module documentation.

---

## 14.8 String Encoding

```python
# UTF-8 encoding
text = "Hello, नमस्ते, こんにちは"
encoded = text.encode("utf-8")
print(encoded)
print(type(encoded))  # <class 'bytes'>

# Decode back
decoded = encoded.decode("utf-8")
print(decoded)  # Hello, नमस्ते, こんにちは

# ASCII encoding (limited)
ascii_text = "Hello"
encoded_ascii = ascii_text.encode("ascii")
# "नमस्ते".encode("ascii")  # UnicodeEncodeError!
```

---

## 🔧 Hands-On Activity: Text Analysis Tool

**Duration:** 25 minutes

Create a file `session14_text_analysis.py`:

```python
# Session 14 — Text Analysis Tool

import re
from collections import Counter

def analyze_text(text):
    """Perform comprehensive text analysis."""
    print("=" * 50)
    print("  TEXT ANALYSIS REPORT")
    print("=" * 50)
    
    # Basic stats
    char_count = len(text)
    char_no_spaces = len(text.replace(" ", ""))
    words = text.split()
    word_count = len(words)
    sentences = re.split(r'[.!?]+', text)
    sentences = [s.strip() for s in sentences if s.strip()]
    sentence_count = len(sentences)
    lines = text.splitlines()
    line_count = len(lines)
    
    print(f"\n--- Basic Statistics ---")
    print(f"  Characters (with spaces)  : {char_count}")
    print(f"  Characters (no spaces)    : {char_no_spaces}")
    print(f"  Words                     : {word_count}")
    print(f"  Sentences                 : {sentence_count}")
    print(f"  Lines                     : {line_count}")
    print(f"  Avg word length           : {char_no_spaces / max(word_count, 1):.1f}")
    print(f"  Avg words per sentence    : {word_count / max(sentence_count, 1):.1f}")
    
    # Character analysis
    vowels = sum(1 for c in text.lower() if c in "aeiou")
    consonants = sum(1 for c in text.lower() if c.isalpha() and c not in "aeiou")
    digits = sum(1 for c in text if c.isdigit())
    spaces = text.count(" ")
    
    print(f"\n--- Character Analysis ---")
    print(f"  Vowels      : {vowels}")
    print(f"  Consonants  : {consonants}")
    print(f"  Digits      : {digits}")
    print(f"  Spaces      : {spaces}")
    
    # Word frequency
    clean_words = re.findall(r'\b[a-zA-Z]+\b', text.lower())
    word_freq = Counter(clean_words)
    
    print(f"\n--- Top 5 Words ---")
    for word, count in word_freq.most_common(5):
        bar = "█" * count
        print(f"  {word:<15} {count:>3} {bar}")
    
    # Unique words
    unique = set(clean_words)
    print(f"\n--- Vocabulary ---")
    print(f"  Total words    : {len(clean_words)}")
    print(f"  Unique words   : {len(unique)}")
    print(f"  Richness ratio : {len(unique)/max(len(clean_words),1):.2%}")
    
    # Longest & shortest words
    if clean_words:
        longest = max(clean_words, key=len)
        shortest = min(clean_words, key=len)
        print(f"  Longest word   : {longest} ({len(longest)} chars)")
        print(f"  Shortest word  : {shortest} ({len(shortest)} chars)")
    
    print("=" * 50)

# Test with sample text
sample = """Python is a high-level programming language. Python is used for 
web development, data science, and automation. Python was created by 
Guido van Rossum in 1991. Today, Python is one of the most popular 
programming languages in the world. Over 8 million developers use Python."""

analyze_text(sample)
```

---

## Session 14 — Key Takeaways

1. **Strings are immutable sequences** — every method returns a new string
2. **`.split()` and `.join()`** are the most important string methods — convert between strings and lists
3. **`.strip()`** always clean user input — removes whitespace
4. **`.find()` returns -1** if not found; **`.index()` raises ValueError**
5. **Regular expressions** (`re` module) enable powerful pattern matching
6. **Validation methods** (`.isdigit()`, `.isalpha()`, etc.) check string content

---

## Preparation for Session 15
- Review all Module 3 concepts: lists, tuples, sets, dicts, strings
- Think about: How would you build a product inventory system?
- Be ready to code: Session 15 is the Module 3 project — Inventory Management System

---

*Session 14 of 30 | Module 3: Data Structures*
*Professional Python Programming Certification — UpSkill Global Education Technologies Inc., Canada*
