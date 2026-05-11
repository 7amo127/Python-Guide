

# 🐍 Python Mastery Book — Chapter 3
# Type Casting: Converting Between All Python Objects

> **"Type casting is the art of speaking different data languages fluently — and knowing when each conversion is safe, lossy, or simply impossible."**

---

## 📚 Table of Contents

1. [What is Type Casting?](#1-what-is-type-casting)
2. [Python's Type Hierarchy — All Built-in Types](#2-pythons-type-hierarchy)
3. [Implicit vs Explicit Type Conversion](#3-implicit-vs-explicit-type-conversion)
4. [All Possible Conversions — The Complete Matrix](#4-all-possible-conversions--the-complete-matrix)
5. [Number Conversions](#5-number-conversions-int-float-complex-bool)
6. [String Conversions](#6-string-conversions)
7. [Collection Conversions (List, Tuple, Set, Dict)](#7-collection-conversions)
8. [Bytes and Bytearray Conversions](#8-bytes-and-bytearray)
9. [Special Conversions and Edge Cases](#9-special-conversions-and-edge-cases)
10. [All Possible Errors and How to Handle Them](#10-all-possible-errors-and-how-to-handle-them)
11. [Use Cases](#11-use-cases)
12. [Real-World Applications](#12-real-world-applications)
13. [Senior & Professional Tips](#13-senior--professional-tips)

---

## 1. What is Type Casting?

**Type casting** (also called **type conversion**) means taking an object of one type and producing an equivalent object of another type.

In Python, since **everything is an object**, type casting is really about creating a **new object** of the target type that represents the same data (or as much of it as possible).
Create a **new object** of a different type **using data from an old object**.


There are two kinds:
- **Implicit (automatic)**: Python converts types for you silently.
- **Explicit (manual)**: You do it intentionally using built-in functions.

```python
# Implicit — Python does it automatically
result = 3 + 1.5     # int + float → Python promotes int to float
print(result)        # 4.5
print(type(result))  # <class 'float'>

# Explicit — you do it on purpose
result = int(3.9)    # You explicitly convert float → int
print(result)        # 3 (truncated, NOT rounded!)
```

---

## 2. Python's Type Hierarchy

Understanding what types exist is the foundation. Here are ALL the built-in Python types:

```
Python Built-in Types
│
├── Numeric
│   ├── int          → 42, -7, 0, 1_000_000
│   ├── float        → 3.14, -0.5, 1.0e10
│   ├── complex      → 3+4j, 1j
│   └── bool         → True, False  (subclass of int!)
│
├── Sequences (ordered)
│   ├── str          → "hello", 'world'
│   ├── list         → [1, 2, 3]
│   ├── tuple        → (1, 2, 3)
│   ├── range        → range(0, 10, 2)
│   └── bytes        → b"hello"
│
├── Collections (unordered or key-based)
│   ├── set          → {1, 2, 3}
│   ├── frozenset    → frozenset({1, 2, 3})
│   ├── dict         → {"key": "value"}
│   └── bytearray    → bytearray(b"hello")
│
├── Other
│   ├── NoneType     → None
│   ├── memoryview   → memoryview(b"hello")
│   └── type         → type(42) → <class 'int'>
```

---

## 3. Implicit vs Explicit Type Conversion

### 🔸 Implicit (Coercion)

Python automatically converts types when it's **safe and lossless**:

```python
# int → float (safe — no data lost)
print(5 + 2.0)       # 7.0  (int promoted to float)
print(type(5 + 2.0)) # <class 'float'>

# bool → int (True=1, False=0)
print(True + 1)      # 2
print(False + 5)     # 5
print(True + True)   # 2

# Python will NEVER implicitly convert between types where data loss is possible:
print("5" + 5)       # ❌ TypeError — Python won't auto-convert here
```

**Why does Python choose float over int?**
Because float has more range. Going int→float loses no information. Going float→int loses the decimal part, so Python makes you do it explicitly.

### 🔸 Explicit (Type Casting Functions)

```python
int()        # Convert to integer
float()      # Convert to float
complex()    # Convert to complex
bool()       # Convert to boolean
str()        # Convert to string
list()       # Convert to list
tuple()      # Convert to tuple
set()        # Convert to set
frozenset()  # Convert to frozenset
dict()       # Convert to dict
bytes()      # Convert to bytes
bytearray()  # Convert to bytearray
repr()       # Convert to detailed string representation
bin()        # Convert int to binary string
oct()        # Convert int to octal string
hex()        # Convert int to hexadecimal string
ord()        # Convert single char to its Unicode integer
chr()        # Convert integer to Unicode character
```

---

## 4. All Possible Conversions — The Complete Matrix

Legend: ✅ Works | ⚠️ Works with conditions/data loss | ❌ Fails | 🔧 Needs workaround

| FROM ↓  TO →  | int   | float | bool  | str   | list  | tuple | set   | dict  | bytes |
|---------------|-------|-------|-------|-------|-------|-------|-------|-------|-------|
| **int**       | —     | ✅    | ✅    | ✅    | ❌    | ❌    | ❌    | ❌    | ✅    |
| **float**     | ⚠️    | —     | ✅    | ✅    | ❌    | ❌    | ❌    | ❌    | ❌    |
| **bool**      | ✅    | ✅    | —     | ✅    | ❌    | ❌    | ❌    | ❌    | ❌    |
| **str**       | ⚠️    | ⚠️    | ✅    | —     | ✅    | ✅    | ✅    | 🔧    | ✅    |
| **list**      | ❌    | ❌    | ✅    | ✅    | —     | ✅    | ✅    | ⚠️    | ❌    |
| **tuple**     | ❌    | ❌    | ✅    | ✅    | ✅    | —     | ✅    | ⚠️    | ❌    |
| **set**       | ❌    | ❌    | ✅    | ✅    | ✅    | ✅    | —     | ❌    | ❌    |
| **dict**      | ❌    | ❌    | ✅    | ✅    | ✅    | ✅    | ✅    | —     | ❌    |
| **bytes**     | ✅    | ❌    | ✅    | ✅    | ✅    | ✅    | ✅    | ❌    | —     |
| **NoneType**  | ❌    | ❌    | ✅    | ✅    | ❌    | ❌    | ❌    | ❌    | ❌    |

---

## 5. Number Conversions (int, float, complex, bool)

### int ↔ float

```python
# int → float
x = int(3.9)     # 3 — TRUNCATES (not rounds!) the decimal
y = int(3.1)     # 3
z = int(-3.9)    # -3 — truncates towards zero
w = int(3.0)     # 3

# float → int (various rounding methods)
import math
x = 3.7
int(x)           # 3 — truncate (always towards zero)
round(x)         # 4 — standard rounding (banker's rounding!)
math.floor(x)    # 3 — always round down
math.ceil(x)     # 4 — always round up
math.trunc(x)    # 3 — same as int()

# Special float values
int(float('inf'))   # ❌ OverflowError
int(float('nan'))   # ❌ ValueError

# Scientific notation floats
x = 1.5e3          # 1500.0
int(x)             # 1500
```

### int ↔ bool

```python
# Everything has a truth value in Python!
# Falsy values (evaluate to False)
bool(0)        # False
bool(0.0)      # False
bool("")       # False — empty string
bool([])       # False — empty list
bool(())       # False — empty tuple
bool({})       # False — empty dict
bool(set())    # False — empty set
bool(None)     # False

# Truthy values (evaluate to True)
bool(1)        # True
bool(-1)       # True — any non-zero number
bool(0.001)    # True
bool("a")      # True — any non-empty string
bool([0])      # True — list with one element (even if element is falsy)
bool(" ")      # True — space is not empty!

# bool → int
int(True)      # 1
int(False)     # 0
True + True    # 2
True * 5       # 5
False * 100    # 0

# Real use cases
score = 85
passed = bool(score >= 60)    # True
print(int(passed))            # 1
```

### int → String Bases

```python
x = 255

bin(x)    # '0b11111111' — binary
oct(x)    # '0o377' — octal
hex(x)    # '0xff' — hexadecimal

# Remove prefix
bin(x)[2:]   # '11111111'
hex(x)[2:]   # 'ff'

# Format strings for bases
f"{x:b}"    # '11111111' — binary without prefix
f"{x:o}"    # '377' — octal without prefix
f"{x:x}"    # 'ff' — hex lowercase
f"{x:X}"    # 'FF' — hex uppercase
f"{x:08b}"  # '11111111' — padded to 8 digits

# String back to int with base
int('11111111', 2)   # 255 — binary string
int('ff', 16)        # 255 — hex string
int('377', 8)        # 255 — octal string
int('255', 10)       # 255 — decimal (default)
```

### complex

```python
# Creating complex numbers
z1 = complex(3, 4)      # 3+4j
z2 = complex(5)         # 5+0j
z3 = 3 + 4j             # literal syntax

# Accessing parts
print(z1.real)    # 3.0
print(z1.imag)    # 4.0

# int/float → complex
complex(5)        # (5+0j)
complex(3.14)     # (3.14+0j)

# complex → int/float ❌ — NOT directly possible
int(3+4j)         # ❌ TypeError: can't convert complex to int
float(3+4j)       # ❌ TypeError

# But you CAN extract real/imag as floats
c = 3+4j
real_part = c.real     # 3.0 (float)
imag_part = c.imag     # 4.0 (float)
magnitude = abs(c)     # 5.0 — √(3²+4²)
```

---

## 6. String Conversions

### str → int / float

```python
# str → int
int("42")          # 42 — works
int("  42  ")      # 42 — strips whitespace automatically
int("-17")         # -17 — negative works
int("42.0")        # ❌ ValueError — int() can't handle decimal point
int("hello")       # ❌ ValueError — not a number
int("")            # ❌ ValueError — empty string
int("0b1010", 2)   # 10 — binary string with base
int("FF", 16)      # 255 — hex string with base

# str → float
float("3.14")      # 3.14
float("3")         # 3.0
float("-1.5e-3")   # -0.0015 — scientific notation works!
float("inf")       # inf — infinity!
float("-inf")      # -inf
float("nan")       # nan — not a number
float("hello")     # ❌ ValueError
float("")          # ❌ ValueError
```

### int/float → str

```python
# Basic conversion
str(42)           # "42"
str(3.14)         # "3.14"
str(True)         # "True"
str(None)         # "None"
str([1, 2, 3])    # "[1, 2, 3]"

# Formatted strings (use these for display!)
name = "Ahmed"
age = 25
price = 99.9

# f-string (best — Python 3.6+)
f"Name: {name}, Age: {age}"         # "Name: Ahmed, Age: 25"
f"Price: {price:.2f}"               # "Price: 99.90"
f"Big number: {1000000:,}"          # "Big number: 1,000,000"
f"Hex: {255:#x}"                    # "Hex: 0xff"
f"Padded: {42:010d}"                # "Padded: 0000000042"
f"Percentage: {0.856:.1%}"          # "Percentage: 85.6%"

# .format() method (older but still common)
"Hello, {}!".format(name)
"{:.2f}".format(price)

# % formatting (old style, still seen in legacy code)
"%s is %d years old" % (name, age)

# repr() vs str()
x = "hello\nworld"
print(str(x))    # hello
                 # world   ← processes escape sequences
print(repr(x))   # 'hello\nworld'  ← shows raw representation
```

### str → list/tuple/set

```python
# str → list (each character becomes an element)
list("hello")       # ['h', 'e', 'l', 'l', 'o']
tuple("hello")      # ('h', 'e', 'l', 'l', 'o')
set("hello")        # {'h', 'e', 'l', 'o'}  — no duplicates!

# Split string into list of words
"hello world".split()           # ['hello', 'world']
"a,b,c,d".split(",")           # ['a', 'b', 'c', 'd']
"a::b::c".split("::")          # ['a', 'b', 'c']
"hello".split("l")             # ['he', '', 'o']

# Split with max splits
"a-b-c-d".split("-", 2)        # ['a', 'b', 'c-d'] — max 2 splits

# Join list back to string
words = ['hello', 'world']
" ".join(words)                # "hello world"
",".join(["a", "b", "c"])     # "a,b,c"
"".join(['h','e','l','l','o']) # "hello"
"-".join(str(x) for x in [1,2,3])  # "1-2-3"
```

---

## 7. Collection Conversions

### List ↔ Tuple ↔ Set

```python
lst   = [1, 2, 3, 2, 1]
tpl   = (1, 2, 3, 2, 1)
st    = {1, 2, 3}

# list ↔ tuple (easy, reversible)
tuple(lst)         # (1, 2, 3, 2, 1) — keeps order, keeps duplicates
list(tpl)          # [1, 2, 3, 2, 1] — keeps order, keeps duplicates

# list/tuple → set (LOSES order and duplicates!)
set(lst)           # {1, 2, 3} — duplicates removed, order NOT guaranteed
set(tpl)           # {1, 2, 3}

# set → list/tuple (LOSES original order, but you get a new order)
list(st)           # e.g., [1, 2, 3] — order is arbitrary!
tuple(st)          # e.g., (1, 2, 3) — order is arbitrary!

# Trick: remove duplicates while preserving order (Python 3.7+)
original = [3, 1, 4, 1, 5, 9, 2, 6, 5, 3]
no_duplicates = list(dict.fromkeys(original))   # [3, 1, 4, 5, 9, 2, 6]
# dict.fromkeys preserves insertion order and removes duplicates

# set → frozenset (and back)
fs = frozenset({1, 2, 3})
s  = set(fs)               # Back to mutable set
```

### List/Tuple → Dict (Important Patterns!)

```python
# From list of pairs (key-value tuples) → dict
pairs = [("name", "Ahmed"), ("age", 25), ("city", "Cairo")]
d = dict(pairs)
# {"name": "Ahmed", "age": 25, "city": "Cairo"}

# From two lists → dict (using zip)
keys   = ["name", "age", "city"]
values = ["Ahmed", 25,    "Cairo"]
d = dict(zip(keys, values))
# {"name": "Ahmed", "age": 25, "city": "Cairo"}

# dict comprehension from two lists
d = {k: v for k, v in zip(keys, values)}

# From list of alternating key-value pairs
flat = ["name", "Ahmed", "age", 25]
d = dict(zip(flat[::2], flat[1::2]))   # {"name": "Ahmed", "age": 25}

# CANNOT do: dict([1, 2, 3]) or dict("hello") — ❌ TypeError
```

### Dict → List/Tuple/Set

```python
d = {"name": "Ahmed", "age": 25, "city": "Cairo"}

# dict → list of keys (default behavior!)
list(d)               # ['name', 'age', 'city']
tuple(d)              # ('name', 'age', 'city')
set(d)                # {'name', 'age', 'city'}

# dict → list of values
list(d.values())      # ['Ahmed', 25, 'Cairo']

# dict → list of (key, value) tuples
list(d.items())       # [('name', 'Ahmed'), ('age', 25), ('city', 'Cairo')]

# dict → sorted by key
sorted(d)             # ['age', 'city', 'name'] — returns sorted list of keys

# Sort dict by value
sorted(d.items(), key=lambda x: str(x[1]))
```

### Set ↔ Dict — The Tricky Case

```python
# ❌ You CANNOT directly convert set → dict
d = dict({1, 2, 3})      # ❌ TypeError — set elements aren't key-value pairs

# ✅ You CAN convert set to dict with a rule
s = {"apple", "banana", "cherry"}
d = {fruit: len(fruit) for fruit in s}
# e.g., {"apple": 5, "banana": 6, "cherry": 6}

# ✅ dict → set (gives you set of keys)
d = {"a": 1, "b": 2, "c": 3}
set(d)               # {'a', 'b', 'c'}
set(d.values())      # {1, 2, 3}
set(d.items())       # {('a', 1), ('b', 2), ('c', 3)}  — set of tuples
```

### range Conversions

```python
r = range(0, 10, 2)   # range object

list(r)    # [0, 2, 4, 6, 8]
tuple(r)   # (0, 2, 4, 6, 8)
set(r)     # {0, 2, 4, 6, 8}

# range is NOT directly iterable to dict or str
# len() works on range without converting:
len(r)     # 5 — fast O(1) operation!
```

---

## 8. Bytes and Bytearray

```python
# str → bytes (requires encoding)
s = "Hello, World!"
b = s.encode("utf-8")        # b'Hello, World!'
b = s.encode("ascii")        # b'Hello, World!'
b = s.encode("utf-16")       # b'\xff\xfeH\x00e\x00...' — different bytes!

# bytes → str (requires decoding)
b = b"Hello, World!"
s = b.decode("utf-8")        # "Hello, World!"
s = b.decode("ascii")        # "Hello, World!"

# bytes → list (each byte as an integer 0-255)
list(b"Hello")    # [72, 101, 108, 108, 111]
tuple(b"Hello")   # (72, 101, 108, 108, 111)

# int → bytes
n = 255
n.to_bytes(1, byteorder="big")     # b'\xff'
n.to_bytes(4, byteorder="little")  # b'\xff\x00\x00\x00'

# bytes → int
int.from_bytes(b'\xff', byteorder="big")     # 255
int.from_bytes(b'\x00\x10', byteorder="big") # 16

# bytearray — mutable version of bytes
ba = bytearray(b"Hello")
ba[0] = 74         # Change 'H'(72) to 'J'(74)
print(ba)          # bytearray(b'Jello')
bytes(ba)          # Convert back to immutable bytes
```

---

## 9. Special Conversions and Edge Cases

### None Conversions

```python
bool(None)    # False
str(None)     # "None" — the string "None"!
int(None)     # ❌ TypeError
float(None)   # ❌ TypeError
list(None)    # ❌ TypeError

# Watch out for this bug!
value = None
result = str(value)   # "None" — the string, not None itself!
if result == "None":  # ← This can cause subtle bugs
    pass
```

### Numeric Edge Cases

```python
# Float precision issues
float("0.1") + float("0.2")   # 0.30000000000000004 — IEEE 754!
round(0.1 + 0.2, 10)          # 0.3 — workaround
from decimal import Decimal
Decimal("0.1") + Decimal("0.2")  # Decimal('0.3') — exact!

# Large integers (Python handles them perfectly)
2 ** 1000    # Works! Python ints are arbitrary precision
int(2e308)   # ❌ OverflowError — float overflow first

# String with whitespace and signs
int("  +42  ")    # 42 — handles leading/trailing space and + sign
int("  -42  ")    # -42
float("  +3.14")  # 3.14

# Locale-specific numbers — TRICKY!
int("1,000")      # ❌ ValueError — comma not valid in int()
# Solution:
int("1,000".replace(",", ""))  # 1000
```

### Nested Structure Conversions

```python
# Nested list → nested tuple (requires recursion)
nested = [[1, 2], [3, 4], [5, 6]]
tuple(nested)           # ([1, 2], [3, 4], [5, 6]) — outer is tuple, inner still lists!

# To fully convert:
tuple(tuple(inner) for inner in nested)   # ((1,2),(3,4),(5,6))

# Or recursively:
def deep_tuple(obj):
    if isinstance(obj, list):
        return tuple(deep_tuple(x) for x in obj)
    return obj
```

---

## 10. All Possible Errors and How to Handle Them

This section is **critical for writing robust code**. Every type conversion that can fail should be wrapped in error handling.

### ValueError — Wrong value format

```python
# Happens when the value is the right type but wrong format for conversion
int("hello")       # ValueError: invalid literal for int() with base 10: 'hello'
int("3.14")        # ValueError: invalid literal for int() with base 10: '3.14'
float("abc")       # ValueError: could not convert string to float: 'abc'

# Safe conversion pattern
def safe_int(value, default=0):
    try:
        return int(value)
    except (ValueError, TypeError):
        return default

safe_int("42")       # 42
safe_int("hello")    # 0
safe_int(None)       # 0
safe_int("  15  ")   # 15
```

### TypeError — Wrong type entirely

```python
# Happens when you try to convert a type that makes no sense
int([1, 2, 3])      # TypeError: int() argument must be a string, a bytes-like object or a real number, not 'list'
float(None)         # TypeError: float() argument must be a string or a real number, not 'NoneType'
dict("hello")       # TypeError: cannot convert 'str' object to dict items
int(3+4j)           # TypeError: can't convert complex to int

# Checking type before conversion
def convert_to_int(value):
    if isinstance(value, (int, float, str, bool)):
        try:
            return int(value)
        except (ValueError, OverflowError):
            return None
    return None
```

### OverflowError — Number too large

```python
int(float('inf'))        # OverflowError: cannot convert float infinity to integer
int(10 ** 309)           # Works! Python int is arbitrary precision
float(10 ** 309)         # OverflowError: int too large to convert to float
```

### KeyError — Dict operations

```python
# When using dict() with invalid input
dict([(1, 2), (3,)])     # ValueError: dictionary update sequence element #1 has length 1; 2 is required

# When accessing a dict key that doesn't exist
d = {"a": 1}
d["b"]               # KeyError: 'b'
d.get("b", "N/A")    # "N/A" — safe access
```

### UnicodeDecodeError / UnicodeEncodeError

```python
# When decoding bytes with wrong encoding
b"\xff\xfe".decode("ascii")    # UnicodeDecodeError: 'ascii' codec can't decode byte 0xff

# Always use utf-8 or specify errors parameter
b"\xff\xfe".decode("utf-8", errors="ignore")    # '' — ignores bad bytes
b"\xff\xfe".decode("utf-8", errors="replace")   # '��' — replaces with placeholder
b"\xff\xfe".decode("utf-16")                    # '' — correct encoding!
```

### Full Safe Conversion Template

```python
def safe_convert(value, target_type, default=None):
    """
    Safely convert value to target_type.
    Returns default if conversion fails.
    """
    try:
        return target_type(value)
    except (ValueError, TypeError, OverflowError, UnicodeDecodeError):
        return default

# Usage
safe_convert("42", int)           # 42
safe_convert("hello", int)        # None
safe_convert("3.14", float)       # 3.14
safe_convert(None, str)           # "None" ← Watch out! str(None) = "None"
safe_convert([1,2,3], tuple)      # (1, 2, 3)
safe_convert({1,2,3}, list)       # [1, 2, 3]
```

### isinstance() and type() for Type Checking

```python
# isinstance() — preferred (works with inheritance)
isinstance(42, int)           # True
isinstance(42, (int, float))  # True — check multiple types at once
isinstance(True, int)         # True — bool IS a subclass of int!
isinstance([], (list, tuple)) # True

# type() — strict equality (no inheritance)
type(42) == int               # True
type(True) == int             # False — True is bool, not int
type(True) == bool            # True

# Checking all numeric types
import numbers
isinstance(42, numbers.Number)      # True
isinstance(3.14, numbers.Number)    # True
isinstance(3+4j, numbers.Number)    # True

# Check if string represents a number
"42".isdigit()         # True
"-42".isdigit()        # False — doesn't handle negatives
"3.14".isdigit()       # False — doesn't handle decimals
"42abc".isdigit()      # False

# Better check:
def is_number(s: str) -> bool:
    try:
        float(s)
        return True
    except ValueError:
        return False

is_number("42")     # True
is_number("3.14")   # True
is_number("-5")     # True
is_number("1e10")   # True
is_number("hello")  # False
```

---

## 11. Use Cases

### Remove Duplicates from List (list → set → list)
```python
names = ["Ahmed", "Sara", "Ahmed", "Omar", "Sara"]
unique_names = list(set(names))
# Note: order is not preserved! Use dict.fromkeys() to preserve order
unique_names = list(dict.fromkeys(names))  # ["Ahmed", "Sara", "Omar"]
```

### Convert User Input Safely
```python
user_input = input("Enter your age: ")   # Always returns a string
age = safe_int(user_input, default=-1)
if age == -1:
    print("Invalid age entered")
elif age < 0 or age > 150:
    print("Age out of reasonable range")
else:
    print(f"You are {age} years old")
```

### Convert API JSON Data
```python
import json

# JSON always comes as strings
json_str = '{"price": "99.99", "quantity": "5"}'
data = json.loads(json_str)   # dict with string values
price = float(data["price"])
quantity = int(data["quantity"])
total = price * quantity
```

### Convert Database Rows to Dicts
```python
# Many DB drivers return rows as tuples
columns = ["id", "name", "email", "age"]
row = (1, "Ahmed", "ahmed@example.com", 25)
user = dict(zip(columns, row))
# {"id": 1, "name": "Ahmed", "email": "ahmed@example.com", "age": 25}

# For multiple rows
rows = [(1, "Ahmed"), (2, "Sara"), (3, "Omar")]
users = [dict(zip(columns, row)) for row in rows]
```

### Convert Config Values
```python
import os
# Environment variables are always strings
DEBUG = bool(int(os.getenv("DEBUG", "0")))
PORT = int(os.getenv("PORT", "8000"))
TIMEOUT = float(os.getenv("TIMEOUT", "30.0"))
ALLOWED_HOSTS = os.getenv("ALLOWED_HOSTS", "localhost").split(",")
```

---

## 12. Real-World Applications

### Django/Flask Web Frameworks:
All HTTP data arrives as strings. Converting to proper types is a daily task:
```python
# URL parameters, form data, headers — all strings
def update_user_age(request):
    raw_age = request.GET.get("age", "")      # str
    age = int(raw_age)                         # int
    # But if raw_age is not a number: ValueError!
    # Production code:
    try:
        age = int(raw_age)
    except ValueError:
        return JsonResponse({"error": "Invalid age"}, status=400)
```

### Data Science (Pandas):
```python
import pandas as pd
df = pd.read_csv("data.csv")   # Often imports numbers as strings

# Convert column types
df["age"] = df["age"].astype(int)
df["price"] = df["price"].astype(float)
df["date"] = pd.to_datetime(df["date"])
df["category"] = df["category"].astype("category")  # efficient for repeated strings

# Handle errors during conversion
df["age"] = pd.to_numeric(df["age"], errors="coerce")  # NaN for invalid values
```

### Machine Learning (scikit-learn):
```python
# Features must be floats for most ML algorithms
from sklearn.preprocessing import LabelEncoder
import numpy as np

labels = ["cat", "dog", "cat", "bird", "dog"]
le = LabelEncoder()
encoded = le.fit_transform(labels)    # [1, 2, 1, 0, 2] — int array
floats = encoded.astype(float)        # [1., 2., 1., 0., 2.] — float array
```

### Network/Serialization:
```python
import struct

# Pack numbers into bytes for network transmission
data = struct.pack(">HH", 1920, 1080)   # Two unsigned shorts, big-endian
width, height = struct.unpack(">HH", data)  # Unpack back

# Convert IP address
ip = "192.168.1.1"
parts = [int(x) for x in ip.split(".")]   # [192, 168, 1, 1]
packed = bytes(parts)                       # b'\xc0\xa8\x01\x01'
```

---

## 13. Senior & Professional Tips

### 🔥 Tip 1: Know When NOT to Convert

```python
# Don't convert unnecessarily — check type first
def process_items(items):
    # ❌ Bad — always converts even if already a list
    items = list(items)
    
    # ✅ Better — only convert if needed
    if not isinstance(items, list):
        items = list(items)
    
    # ✅ Best for read-only access — accept any iterable
    for item in items:   # Works on list, tuple, set, generator...
        process(item)
```

### 🔥 Tip 2: Use `ast.literal_eval` for Safe String → Python Object

```python
import ast

# ❌ NEVER use eval() on user input — security risk!
eval("[1, 2, 3]")   # Works but dangerous

# ✅ Use ast.literal_eval for safe conversion
ast.literal_eval("[1, 2, 3]")       # [1, 2, 3]
ast.literal_eval("{'a': 1}")        # {'a': 1}
ast.literal_eval("(1, 2, 3)")       # (1, 2, 3)
ast.literal_eval("True")            # True
ast.literal_eval("import os")       # ❌ ValueError — won't execute code!
```

### 🔥 Tip 3: Use `Decimal` for Financial Calculations

```python
from decimal import Decimal, ROUND_HALF_UP

# ❌ Float precision nightmare for money
price = 0.1 + 0.2         # 0.30000000000000004

# ✅ Decimal for exact financial math
price = Decimal("0.10") + Decimal("0.20")   # Decimal('0.30') exactly!
price = price.quantize(Decimal("0.01"), rounding=ROUND_HALF_UP)  # Round to cents
```

### 🔥 Tip 4: Type Guards Pattern

```python
from typing import TypeGuard

def is_list_of_ints(val: list) -> TypeGuard[list[int]]:
    return all(isinstance(x, int) for x in val)

def process(data: list):
    if is_list_of_ints(data):
        total = sum(data)   # Safe — mypy knows it's list[int]
```

### 🔥 Tip 5: Conversion in Dataclasses

```python
from dataclasses import dataclass

@dataclass
class User:
    name: str
    age: int
    score: float

    def __post_init__(self):
        # Auto-convert types on creation
        self.name = str(self.name)
        self.age = int(self.age)
        self.score = float(self.score)

# Now this works safely:
u = User(name=b"Ahmed".decode(), age="25", score="99.5")
print(u)   # User(name='Ahmed', age=25, score=99.5)
```

### 🔥 Tip 6: The `__int__`, `__float__`, `__str__` Protocol

```python
# Python calls these dunder methods when you call int(), float(), str()
class Temperature:
    def __init__(self, celsius: float):
        self.celsius = celsius
    
    def __int__(self):
        return int(self.celsius)
    
    def __float__(self):
        return float(self.celsius)
    
    def __str__(self):
        return f"{self.celsius}°C"
    
    def __repr__(self):
        return f"Temperature({self.celsius})"

t = Temperature(98.6)
print(int(t))     # 98
print(float(t))   # 98.6
print(str(t))     # 98.6°C
```

---

## 🏁 Chapter Summary

| Conversion                  | Function        | Gotcha                                        |
|-----------------------------|----------------|-----------------------------------------------|
| str → int                   | `int(s)`        | Only if s looks like an integer (no decimal)  |
| str → float                 | `float(s)`      | Handles scientific notation                   |
| float → int                 | `int(f)`        | TRUNCATES, doesn't round                      |
| int → str                   | `str(n)`        | Easy, always works                            |
| list → tuple                | `tuple(lst)`    | Easy, keeps order                             |
| list → set                  | `set(lst)`      | Loses duplicates AND order                    |
| set → list                  | `list(s)`       | Order is arbitrary                            |
| list of pairs → dict        | `dict(pairs)`   | Elements must be length-2 iterables           |
| set → dict                  | Can't directly  | Use dict comprehension                        |
| str → bytes                 | `s.encode()`    | Must specify encoding (use "utf-8")           |
| bytes → str                 | `b.decode()`    | Must specify encoding (use "utf-8")           |
| Anything → bool             | `bool(x)`       | Know falsy values: 0, "", [], {}, None        |
| Invalid conversion          | —               | Raises ValueError or TypeError                |

---
