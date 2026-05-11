
# 🐍 Python Book — Chapter 4: Escape Characters

> "Mastering escape characters is the difference between a beginner who fights strings and a senior who controls them completely."

---

## 📚 Table of Contents
1. [What Are Escape Characters?](#1-what-are-escape-characters)
2. [Why Do They Exist?](#2-why-do-they-exist)
3. [Complete Escape Character Reference](#3-complete-escape-character-reference)
4. [How to Code Them](#4-how-to-code-them)
5. [All Use Cases](#5-all-use-cases)
6. [Real Examples & Huge Applications](#6-real-examples--huge-applications)
7. [Raw Strings — The Secret Weapon](#7-raw-strings--the-secret-weapon)
8. [Unicode & Special Characters](#8-unicode--special-characters)
9. [How to Think Like a Senior (100 Years Experience)](#9-how-to-think-like-a-senior-100-years-experience)

---

## 1. What Are Escape Characters?

An **escape character** is a special combination of characters that tells Python:

> *"Don't treat the next character normally — it has a special meaning."*

In Python, the escape sequence always starts with a **backslash** `\`.

When Python sees `\`, it "escapes" from normal reading mode and interprets what follows as a **special instruction** — like "go to next line", "add a tab", "insert a quote", etc.

```python
# Without escape character — this would CRASH
text = "He said "Hello""   # ❌ Python gets confused by the inner quotes

# With escape character — works perfectly
text = "He said \"Hello\""  # ✅ The \" means: literal quote mark
print(text)
# Output: He said "Hello"
```

---

## 2. Why Do They Exist?

Strings in Python are wrapped in quotes (`"` or `'`). This creates a **conflict**:

- What if you want to PUT a quote **inside** a string?
- What if you want a **new line** inside a string?
- What if you want a **tab space** inside a string?
- What if you want to include the **backslash itself**?

Escape characters solve ALL of these problems.

---

## 3. Complete Escape Character Reference

Here is **every escape character** in Python — nothing left out:

| Escape | Name | What It Does | Example Output |
|--------|------|--------------|----------------|
| `\\`   | Backslash | Inserts a literal `\` | `C:\Users` |
| `\'`   | Single Quote | Inserts `'` inside single-quoted string | `it's` |
| `\"`   | Double Quote | Inserts `"` inside double-quoted string | `say "hi"` |
| `\n`   | Newline | Moves to the next line | line1 ↵ line2 |
| `\t`   | Horizontal Tab | Inserts a tab space (~4-8 spaces) | `Name    Age` |
| `\r`   | Carriage Return | Moves cursor to the beginning of the line (overwrites) | (see below) |
| `\b`   | Backspace | Deletes the character before it | `Helo` from `Hello\b` |
| `\f`   | Form Feed | Page break (mostly used in old printing/files) | (rarely seen) |
| `\v`   | Vertical Tab | Vertical spacing (mostly used in old systems) | (rarely seen) |
| `\a`   | Bell / Alert | Makes a beep sound in supported terminals | 🔔 |
| `\0`   | Null Character | A character with ASCII value zero | (invisible) |
| `\N{name}` | Unicode Name | Inserts a Unicode character by name | `\N{SNOWMAN}` → ☃ |
| `\uXXXX`   | Unicode 16-bit | Inserts Unicode by 4-hex-digit code | `\u2764` → ❤ |
| `\UXXXXXXXX` | Unicode 32-bit | Inserts Unicode by 8-hex-digit code | `\U0001F600` → 😀 |
| `\xhh`  | Hex Value | Inserts character by hex ASCII value | `\x41` → `A` |
| `\ooo`  | Octal Value | Inserts character by octal ASCII value | `\101` → `A` |

---

## 4. How to Code Them

### `\n` — Newline (Most Used)

```python
# Basic newline
message = "Line 1\nLine 2\nLine 3"
print(message)
# Output:
# Line 1
# Line 2
# Line 3

# In a menu
menu = "1. Start Game\n2. Load Game\n3. Settings\n4. Exit"
print(menu)
# Output:
# 1. Start Game
# 2. Load Game
# 3. Settings
# 4. Exit
```

---

### `\t` — Tab (Alignment)

```python
# Simple tab
print("Name\tAge\tCity")
print("Ahmed\t25\tCairo")
print("Sara\t30\tAlex")
# Output:
# Name    Age     City
# Ahmed   25      Cairo
# Sara    30      Alex

# Nested tabs for sub-lists
print("Animals:")
print("\tMammals:")
print("\t\tDog")
print("\t\tCat")
print("\tBirds:")
print("\t\tEagle")
```

---

### `\\` — Literal Backslash

```python
# File paths (Windows)
path = "C:\\Users\\Ahmed\\Documents\\file.txt"
print(path)
# Output: C:\Users\Ahmed\Documents\file.txt

# Regex patterns
import re
pattern = "\\d+"   # means: one or more digits
# (see Raw Strings section for a better way to do this)

# Showing escape sequences as text
print("The newline character is: \\n")
# Output: The newline character is: \n
```

---

### `\'` and `\"` — Quotes Inside Strings

```python
# Using \" inside double-quoted string
quote = "Shakespeare wrote: \"To be or not to be\""
print(quote)
# Output: Shakespeare wrote: "To be or not to be"

# Using \' inside single-quoted string
message = 'It\'s a beautiful day'
print(message)
# Output: It's a beautiful day

# The smart alternative: mix quote types
message2 = "It's a beautiful day"          # No escape needed!
message3 = 'He said "Hello" to her'        # No escape needed!
```

---

### `\r` — Carriage Return (Tricky One)

```python
# \r moves the cursor back to the START of the same line
# Everything printed after overwrites what was before

print("Hello\rWorld")
# Output: World  (because "World" overwrites "Hello" from position 0)

# Real usage: progress bars in terminal
import time
import sys
for i in range(101):
    sys.stdout.write(f"\rProgress: {i}%")
    sys.stdout.flush()
    time.sleep(0.05)
# This shows a live updating progress bar on ONE line!
```

---

### `\b` — Backspace

```python
# \b deletes the character before it
print("Hello\b!")
# Output: Hell! (the 'o' gets deleted)

print("Python3\b2")
# Output: Python2 (3 gets replaced by 2)
```

---

### `\a` — Bell Alert

```python
# Plays a beep sound (if terminal supports it)
print("\aWARNING: Disk almost full!")
# 🔔 + text appears
```

---

### `\0` — Null Character

```python
# Null character — ASCII value 0
text = "Hello\0World"
print(text)          # May show: Hello World (or Hello World with hidden null)
print(len(text))     # 11 — null IS counted as a character!

# Used in: C-style string compatibility, binary file formats, protocols
```

---

### `\xhh` — Hex Escape

```python
# Every character has an ASCII code. You can use hex codes directly.
print("\x48\x65\x6c\x6c\x6f")
# Output: Hello
# (H=0x48, e=0x65, l=0x6c, l=0x6c, o=0x6f)

print("\x41\x42\x43")
# Output: ABC

# Useful for: embedding control characters, binary data, obfuscation
```

---

### `\ooo` — Octal Escape

```python
# Octal (base-8) ASCII codes
print("\101\102\103")
# Output: ABC
# (A=101 octal, B=102 octal, C=103 octal)

# Less common, but exists in Python for historical UNIX compatibility
```

---

### `\uXXXX` — Unicode (16-bit)

```python
# Insert any Unicode character using its 4-digit hex code
heart     = "\u2764"   # ❤
star      = "\u2605"   # ★
arrow     = "\u2192"   # →
checkmark = "\u2713"   # ✓
warning   = "\u26A0"   # ⚠
pi        = "\u03C0"   # π
omega     = "\u03A9"   # Ω
arabic_ba = "\u0628"   # ب
chinese   = "\u4e2d"   # 中

print(f"Status: {checkmark} Done")
print(f"Math: {pi} = 3.14159")
print(f"Warning {warning}: Check your input")
```

---

### `\UXXXXXXXX` — Unicode (32-bit)

```python
# For characters beyond the 16-bit range (emojis, rare symbols)
smile   = "\U0001F600"  # 😀
fire    = "\U0001F525"  # 🔥
rocket  = "\U0001F680"  # 🚀
snake   = "\U0001F40D"  # 🐍 (Python's mascot!)
trophy  = "\U0001F3C6"  # 🏆

print(f"Python {snake} is awesome {fire}")
print(f"You won! {trophy}")
```

---

### `\N{name}` — Unicode by Name

```python
# You can use the official Unicode character name
snowman    = "\N{SNOWMAN}"              # ☃
copyright  = "\N{COPYRIGHT SIGN}"      # ©
trademark  = "\N{TRADE MARK SIGN}"     # ™
registered = "\N{REGISTERED SIGN}"     # ®
degree     = "\N{DEGREE SIGN}"         # °
micro      = "\N{MICRO SIGN}"          # µ
bullet     = "\N{BULLET}"              # •
euro       = "\N{EURO SIGN}"           # €
pound      = "\N{POUND SIGN}"          # £

print(f"Temperature: 37{degree}C")
print(f"Price: {euro}99.99")
print(f"{copyright} 2024 MyCompany {registered}")
```

---

## 5. All Use Cases

### Use Case 1: Formatted Console Reports

```python
def print_report(data):
    print("=" * 50)
    print("SALES REPORT")
    print("=" * 50)
    print(f"Product\t\tQty\tPrice\tTotal")
    print("-" * 50)
    for item in data:
        total = item['qty'] * item['price']
        print(f"{item['name']}\t\t{item['qty']}\t${item['price']}\t${total}")
    print("=" * 50)

data = [
    {"name": "Laptop",  "qty": 5,  "price": 999},
    {"name": "Mouse",   "qty": 20, "price": 25},
    {"name": "Keyboard","qty": 15, "price": 75},
]
print_report(data)
```

---

### Use Case 2: Multi-line SQL Queries

```python
# Building readable SQL queries with \n
query = (
    "SELECT users.name, orders.total\n"
    "FROM users\n"
    "INNER JOIN orders ON users.id = orders.user_id\n"
    "WHERE orders.total > 100\n"
    "ORDER BY orders.total DESC;"
)
print(query)
```

---

### Use Case 3: File Paths (Windows/Linux/Mac)

```python
import os

# Windows path (escape backslash)
win_path = "C:\\Users\\Ahmed\\Desktop\\project\\main.py"

# Linux/Mac path (no backslash needed)
linux_path = "/home/ahmed/project/main.py"

# The best way: use os.path or pathlib (avoids escape issues)
path = os.path.join("C:\\Users", "Ahmed", "Desktop", "project")
print(path)  # Handles separators automatically per OS
```

---

### Use Case 4: JSON/Config String Embedding

```python
# Embedding JSON strings inside Python strings
json_template = "{\n\t\"name\": \"%s\",\n\t\"age\": %d,\n\t\"city\": \"%s\"\n}"
result = json_template % ("Ahmed", 25, "Cairo")
print(result)
# Output:
# {
#     "name": "Ahmed",
#     "age": 25,
#     "city": "Cairo"
# }
```

---

### Use Case 5: Email / Message Templates

```python
def create_email(name, order_id, amount):
    return (
        f"Dear {name},\n\n"
        f"Thank you for your order!\n\n"
        f"Order Details:\n"
        f"\tOrder ID:\t{order_id}\n"
        f"\tAmount:\t\t${amount}\n\n"
        f"Your order will be shipped within 2-3 business days.\n\n"
        f"Best regards,\n"
        f"The Sales Team"
    )

email = create_email("Ahmed", "ORD-9821", 149.99)
print(email)
```

---

### Use Case 6: Terminal Progress Bars

```python
import time
import sys

def progress_bar(task_name, total_steps):
    for step in range(total_steps + 1):
        percent = step / total_steps * 100
        filled = int(percent / 2)
        bar = "█" * filled + "░" * (50 - filled)
        sys.stdout.write(f"\r{task_name}: [{bar}] {percent:.1f}%")
        sys.stdout.flush()
        time.sleep(0.05)
    print()  # New line when done

progress_bar("Downloading", 100)
progress_bar("Installing",  100)
```

---

### Use Case 7: Log File Formatting

```python
import datetime

def log(level, message):
    now = datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    icons = {"INFO": "ℹ", "WARNING": "⚠", "ERROR": "✗", "SUCCESS": "✓"}
    icon = icons.get(level, "•")
    print(f"[{now}]\t{icon} {level}\t{message}")

log("INFO",    "Server started on port 8080")
log("SUCCESS", "Database connected")
log("WARNING", "High memory usage: 87%")
log("ERROR",   "Failed to connect to API")
```

---

### Use Case 8: Interactive CLI Menus

```python
def show_menu():
    print("\n" + "─" * 40)
    print("\t\t📋 MAIN MENU")
    print("─" * 40)
    print("\t1.\tNew File\t\t[Ctrl+N]")
    print("\t2.\tOpen File\t\t[Ctrl+O]")
    print("\t3.\tSave File\t\t[Ctrl+S]")
    print("\t4.\tSettings\t\t[Ctrl+,]")
    print("\t5.\tExit\t\t\t[Alt+F4]")
    print("─" * 40)

show_menu()
```

---

### Use Case 9: Data in Binary/Hex

```python
# Reading binary protocols (like network packets)
# Null byte as delimiter
header = "PROTOCOL_V2\x00\x01\x00\x10"

# Control characters in data streams
STX = "\x02"  # Start of Text
ETX = "\x03"  # End of Text
message = f"{STX}SENSOR_DATA:TEMP=37.5{ETX}"
```

---

## 6. Real Examples & Huge Applications

### 🌐 Web Development (Django/Flask)

```python
# HTML email template generation
def generate_html_email(user, product):
    return (
        "<!DOCTYPE html>\n"
        "<html>\n"
        "\t<head><title>Order Confirmation</title></head>\n"
        "\t<body>\n"
        f"\t\t<h1>Hello, {user['name']}!</h1>\n"
        f"\t\t<p>Your order for <strong>{product}</strong> is confirmed.</p>\n"
        "\t</body>\n"
        "</html>\n"
    )

print(generate_html_email({"name": "Ahmed"}, "MacBook Pro"))
```

---

### 🤖 Machine Learning / Data Science (Pandas/NumPy)

```python
import pandas as pd

# Pretty printing dataset info with tabs
def describe_dataset(df, name):
    print(f"\n📊 Dataset: {name}")
    print(f"{'─'*40}")
    print(f"Rows:\t\t{df.shape[0]:,}")
    print(f"Columns:\t{df.shape[1]}")
    print(f"Memory:\t\t{df.memory_usage(deep=True).sum() / 1024:.1f} KB")
    print(f"Missing:\t{df.isnull().sum().sum():,} values")
    print(f"{'─'*40}")

# describe_dataset(my_df, "Customer Purchases")
```

---

### 🔒 Cybersecurity & Ethical Hacking

```python
# Network packet inspection
def parse_packet(raw_bytes):
    # Packets often use null bytes as field separators
    fields = raw_bytes.split('\x00')
    print("Packet Fields:")
    for i, field in enumerate(fields):
        print(f"\tField {i+1}:\t{repr(field)}")

# Log analysis with escape-aware parsing
def parse_log_line(line):
    # Tabs separate fields in many log formats (Apache, Nginx, syslog)
    parts = line.split('\t')
    return {
        "timestamp": parts[0] if len(parts) > 0 else "",
        "level":     parts[1] if len(parts) > 1 else "",
        "message":   parts[2] if len(parts) > 2 else "",
    }
```

---

### 📱 CLI Application (Like Git, NPM)

```python
# Git-style status output
def git_status(staged, unstaged, untracked):
    print("\nOn branch main\n")
    
    if staged:
        print("Changes to be committed:")
        print('\t(use "git restore --staged <file>" to unstage)\n')
        for f in staged:
            print(f"\t\t\033[32mnew file:\t{f}\033[0m")
    
    if unstaged:
        print("\nChanges not staged for commit:")
        print('\t(use "git add <file>" to update what will be committed)\n')
        for f in unstaged:
            print(f"\t\t\033[31mmodified:\t{f}\033[0m")
    
    if untracked:
        print("\nUntracked files:")
        for f in untracked:
            print(f"\t\t\033[31m{f}\033[0m")

git_status(["README.md"], ["app.py", "utils.py"], ["temp.log"])
```

---

### 🗄️ Database Systems

```python
import sqlite3

# Escape characters in SQL query formatting for debugging
def debug_query(sql, params):
    print("\n🔍 Query Debug:")
    print(f"{'─'*50}")
    print(f"SQL:\n\t{sql.replace(chr(10), chr(10)+chr(9))}")
    print(f"Params:\t{params}")
    print(f"{'─'*50}\n")

sql = "SELECT * FROM users\nWHERE age > ?\nAND city = ?"
debug_query(sql, (18, "Cairo"))
```

---

## 7. Raw Strings — The Secret Weapon

A **raw string** (`r"..."`) tells Python to **ignore all escape sequences**. Every `\` is treated as a literal backslash.

```python
# Normal string — \n is a newline
normal = "C:\new_folder\data"
print(normal)
# Output:
# C:
# ew_folder\data   ← WRONG! \n became newline, \d is ignored

# Raw string — \n is literally \n
raw = r"C:\new_folder\data"
print(raw)
# Output: C:\new_folder\data  ← CORRECT!
```

### Raw Strings + Regex (Essential Pattern)

```python
import re

# Without raw string — you need double backslashes (messy)
pattern1 = "\\d{3}-\\d{3}-\\d{4}"   # Matches phone: 123-456-7890

# With raw string — clean and readable (professional way)
pattern2 = r"\d{3}-\d{3}-\d{4}"      # Same pattern, much cleaner!

text = "Call me at 123-456-7890 or 987-654-3210"
matches = re.findall(pattern2, text)
print(matches)  # ['123-456-7890', '987-654-3210']

# More regex examples with raw strings
email_pattern    = r"[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}"
url_pattern      = r"https?://[^\s]+"
ip_pattern       = r"\b\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}\b"
password_pattern = r"^(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$"
```

### Raw Strings for Windows Paths

```python
# The 3 ways to write Windows paths:
path1 = "C:\\Users\\Ahmed\\Documents"   # Escape backslashes
path2 = r"C:\Users\Ahmed\Documents"     # Raw string (cleanest!)
path3 = "C:/Users/Ahmed/Documents"      # Forward slashes (also works on Windows!)

# Best practice: use pathlib (Python 3.4+)
from pathlib import Path
path = Path("C:/Users/Ahmed/Documents/file.txt")
print(path)
print(path.parent)
print(path.name)
print(path.suffix)
```

---

## 8. Unicode & Special Characters

Python 3 strings are **Unicode by default**. This means you can include characters from any language.

```python
# Arabic text
arabic = "مرحباً بك في بايثون"
print(arabic)

# Multiple languages in one string
multilingual = "Hello / مرحبا / 你好 / Bonjour / Привет"
print(multilingual)

# Currency symbols
prices = f"USD: \u0024100  EUR: \u20AC90  GBP: \u00A380  EGP: \u00A3500"
print(prices)

# Mathematical symbols
math = f"\u03B1 + \u03B2 = \u03B3  |  \u03C0 \u2248 3.14159  |  \u221A4 = 2"
print(math)
# Output: α + β = γ  |  π ≈ 3.14159  |  √4 = 2

# Get the Unicode code of any character
char = "A"
print(f"Unicode of '{char}': U+{ord(char):04X}")   # U+0041
print(f"Unicode of '❤': U+{ord('❤'):04X}")          # U+2764

# Convert code point back to character
print(chr(0x0041))   # A
print(chr(0x2764))   # ❤
print(chr(0x1F600))  # 😀
```

---

## 9. How to Think Like a Senior (100 Years Experience)

### 🧠 Mindset Rules

**Rule 1: Prefer Readability Over Cleverness**

```python
# Junior — cram everything with escapes
msg = "Name:\tAhmed\nAge:\t25\nCity:\tCairo"

# Senior — use f-strings with triple quotes for complex text
msg = f"""
Name:   Ahmed
Age:    25
City:   Cairo
""".strip()
```

**Rule 2: Know When to Use Raw Strings**

```python
# Always use raw strings (r"...") when writing:
# - Regex patterns
# - Windows file paths
# - LaTeX expressions
# - Anything with lots of backslashes

# ❌ Amateur
pattern = "\\b\\w+\\b"
path    = "C:\\Users\\Ahmed\\file.txt"

# ✅ Professional
pattern = r"\b\w+"
path    = r"C:\Users\Ahmed\file.txt"
```

**Rule 3: Use Triple Quotes for Multi-line Strings**

```python
# ❌ Using \n everywhere — hard to read
sql = "SELECT *\nFROM users\nWHERE id = 1\nAND active = 1;"

# ✅ Triple quotes — looks exactly like what it outputs
sql = """
SELECT *
FROM users
WHERE id = 1
AND active = 1;
""".strip()
```

**Rule 4: Use `repr()` to Debug Escape Characters**

```python
# When something looks wrong, use repr() to see the raw string
text = "Hello\nWorld"
print(text)         # Shows: Hello (newline) World
print(repr(text))   # Shows: 'Hello\nWorld' — you see the actual \n!

# This is gold for debugging file reading, APIs, and user input
user_input = input("Enter something: ")
print(repr(user_input))  # Shows EXACTLY what the user typed, including hidden chars
```

**Rule 5: Understand the Difference Between `\r\n` and `\n`**

```python
# \n = Unix/Linux/Mac line ending
# \r\n = Windows line ending (CRLF)
# \r = Old Mac line ending (rare now)

# When reading files, Python handles this automatically with universal newlines
# But when working with APIs or network data, you'll encounter \r\n

data = "line1\r\nline2\r\nline3"
clean = data.replace("\r\n", "\n")  # Normalize to Unix
lines = clean.split("\n")
print(lines)  # ['line1', 'line2', 'line3']

# Professional way: use splitlines() — handles ALL line endings
lines = data.splitlines()
print(lines)  # ['line1', 'line2', 'line3']
```

**Rule 6: ANSI Escape Codes for Colored Terminal Output**

```python
# Real professionals know this: \033[ starts ANSI color codes
# Format: \033[{code}m

class Colors:
    RESET   = "\033[0m"
    RED     = "\033[91m"
    GREEN   = "\033[92m"
    YELLOW  = "\033[93m"
    BLUE    = "\033[94m"
    MAGENTA = "\033[95m"
    CYAN    = "\033[96m"
    WHITE   = "\033[97m"
    BOLD    = "\033[1m"
    DIM     = "\033[2m"
    UNDERLINE = "\033[4m"

def success(msg): print(f"{Colors.GREEN}✓ {msg}{Colors.RESET}")
def error(msg):   print(f"{Colors.RED}✗ {msg}{Colors.RESET}")
def warning(msg): print(f"{Colors.YELLOW}⚠ {msg}{Colors.RESET}")
def info(msg):    print(f"{Colors.CYAN}ℹ {msg}{Colors.RESET}")

success("Database connected!")
error("Failed to read config file")
warning("Memory usage is high: 87%")
info("Server running on http://localhost:8000")
```

**Rule 7: Be Aware of Null Bytes in Security**

```python
# Null byte injection is a real security vulnerability!
# Attackers use \x00 to bypass validation in some systems

# VULNERABLE — checking file extension after null byte
filename = "image.jpg\x00malicious.php"
# Some systems would read "image.jpg" for validation
# but "malicious.php" for execution!

# SAFE — always strip and validate properly
def safe_filename(filename):
    # Remove null bytes
    filename = filename.replace('\x00', '')
    # Strip whitespace
    filename = filename.strip()
    # Only allow safe characters
    import re
    if not re.match(r'^[\w\-. ]+$', filename):
        raise ValueError("Invalid filename!")
    return filename
```

**Rule 8: The Complete Senior Cheat Sheet**

```python
# QUICK REFERENCE — memorize this:
print("\n")        # New line
print("\t")        # Tab
print("\\")        # Literal backslash
print("\"")        # Literal double quote
print("\'")        # Literal single quote
print("\r")        # Carriage return (overwrite line)
print("\b")        # Backspace (delete one char)
print("\a")        # Bell/Alert beep
print("\0")        # Null character
print("\x41")      # Hex char (A)
print("\u2764")    # Unicode 16-bit (❤)
print("\U0001F600") # Unicode 32-bit (😀)
print(r"\n")       # Raw — literally \n, NO escape

# KNOW THESE BY HEART:
# \n  — newlines in text, emails, SQL
# \t  — table-style output, indentation
# \\  — file paths, regex patterns
# \"  — embedding quotes in strings
# \u  — Unicode symbols, emojis, special chars
# r"" — raw strings for regex and paths
```

---

## 🏁 Summary

| Concept | Key Point |
|---------|-----------|
| Escape Start | Always `\` (backslash) |
| Most Common | `\n` (newline), `\t` (tab), `\\` (backslash), `\"` (quote) |
| Unicode | `\uXXXX`, `\UXXXXXXXX`, `\N{name}` |
| Raw Strings | `r"..."` — disables ALL escape processing |
| Debugging | `repr()` shows raw string with escapes visible |
| Line Endings | `\n` (Unix), `\r\n` (Windows) — use `.splitlines()` |
| ANSI Colors | `\033[91m` = Red, `\033[0m` = Reset |

---
