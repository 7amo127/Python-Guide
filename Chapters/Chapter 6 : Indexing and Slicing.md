
# 📘 Python Mastery Book — Chapter 6 : Indexing and Slicing

> **"He who controls the index, controls the data."**
> This chapter will make you a surgeon with sequences — slicing with precision, indexing with confidence.

---

## 📚 Table of Contents

1. [What is Indexing?](#1-what-is-indexing)
2. [What is Slicing?](#2-what-is-slicing)
3. [Indexing in Depth](#3-indexing-in-depth)
4. [Slicing in Depth](#4-slicing-in-depth)
5. [Step / Stride in Slicing](#5-step--stride-in-slicing)
6. [Negative Indexing & Slicing](#6-negative-indexing--slicing)
7. [Slicing with All Three Parameters](#7-slicing-with-all-three-parameters)
8. [Slice Object](#8-slice-object)
9. [Mutable vs Immutable Slicing](#9-mutable-vs-immutable-slicing)
10. [Slicing Strings](#10-slicing-strings)
11. [Slicing Lists](#11-slicing-lists)
12. [Slicing Tuples](#12-slicing-tuples)
13. [Slicing with NumPy Arrays](#13-slicing-with-numpy-arrays)
14. [Slicing 2D Lists and Matrices](#14-slicing-2d-lists-and-matrices)
15. [Use Cases — All Possible](#15-use-cases--all-possible)
16. [Real World Applications](#16-real-world-applications)
17. [Senior / Professional Level Mastery](#17-senior--professional-level-mastery)
18. [Common Mistakes and How to Avoid Them](#18-common-mistakes-and-how-to-avoid-them)
19. [Practice Challenges](#19-practice-challenges)

---

## 1. What is Indexing?

**Indexing** means accessing a **single specific element** from a sequence (like a string, list, or tuple) using its **position number**.

In Python, every element in a sequence has an **address** — called an **index**.

Python uses **zero-based indexing**, meaning the FIRST element is at index `0`, not `1`.

```
Text:   P  y  t  h  o  n
Index:  0  1  2  3  4  5
```

### Why does Python start at 0?
It's a design inherited from C. The index represents an **offset from the beginning**. The first element is 0 steps away from the start.

---

## 2. What is Slicing?

**Slicing** means extracting a **portion (sub-sequence)** from a sequence — not just one element, but a **range of elements**.

The syntax is:
```python
sequence[start:stop:step]
```

- `start` — where to begin (inclusive)
- `stop`  — where to end (exclusive — this index is NOT included)
- `step`  — how many positions to jump each time (default = 1)

---

## 3. Indexing in Depth

### Basic Positive Indexing

```python
name = "Python"

print(name[0])   # P  — first character
print(name[1])   # y
print(name[2])   # t
print(name[3])   # h
print(name[4])   # o
print(name[5])   # n  — last character
```

### With Lists

```python
fruits = ["apple", "banana", "cherry", "date", "elderberry"]

print(fruits[0])   # apple
print(fruits[2])   # cherry
print(fruits[4])   # elderberry
```

### With Tuples

```python
coords = (10, 20, 30, 40)
print(coords[0])   # 10
print(coords[3])   # 40
```

### IndexError — What happens if index doesn't exist?

```python
name = "Python"
print(name[10])   # ❌ IndexError: string index out of range
```

Always check the length before indexing unknown data:

```python
data = [1, 2, 3]
index = 5

if index < len(data):
    print(data[index])
else:
    print("Index out of range!")
```

---

## 4. Slicing in Depth

### Syntax Reminder

```python
sequence[start:stop]
```

> ⚠️ **STOP is EXCLUSIVE** — it means "go up to but NOT including this index"

```python
name = "Python"
#       0123456

print(name[0:3])   # Pyt   — index 0, 1, 2 (NOT 3)
print(name[1:4])   # yth   — index 1, 2, 3
print(name[2:6])   # thon  — index 2, 3, 4, 5
```

### Omitting Start or Stop

```python
name = "Python"

print(name[:3])    # Pyt   — start defaults to 0
print(name[2:])    # thon  — stop defaults to end
print(name[:])     # Python — full copy
```

### Slicing Lists

```python
numbers = [10, 20, 30, 40, 50, 60, 70]

print(numbers[1:4])    # [20, 30, 40]
print(numbers[:3])     # [10, 20, 30]
print(numbers[4:])     # [50, 60, 70]
print(numbers[:])      # [10, 20, 30, 40, 50, 60, 70]  — full copy
```

---

## 5. Step / Stride in Slicing

The third parameter is the **step** — how many elements to skip between each selection.

```python
numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

print(numbers[::2])    # [0, 2, 4, 6, 8]    — every 2nd element
print(numbers[::3])    # [0, 3, 6, 9]        — every 3rd element
print(numbers[1::2])   # [1, 3, 5, 7, 9]    — odd-indexed elements
print(numbers[0:8:2])  # [0, 2, 4, 6]        — from 0 to 8, step 2
```

---

## 6. Negative Indexing & Slicing

Python allows **negative indices** — they count from the END of the sequence.

```
Text:    P   y   t   h   o   n
Pos:     0   1   2   3   4   5
Neg:    -6  -5  -4  -3  -2  -1
```

```python
name = "Python"

print(name[-1])    # n   — last character
print(name[-2])    # o   — second to last
print(name[-6])    # P   — same as name[0]
```

### Negative Slicing

```python
name = "Python"

print(name[-4:])      # thon  — last 4 characters
print(name[-4:-1])    # tho   — from -4 to -2 (not including -1)
print(name[:-2])      # Pyth  — everything except last 2
```

### Reversing with Negative Step

```python
name = "Python"
print(name[::-1])      # nohtyP  — full reverse!

numbers = [1, 2, 3, 4, 5]
print(numbers[::-1])   # [5, 4, 3, 2, 1]
```

This is one of the most famous Python tricks — reversing with `[::-1]`

---

## 7. Slicing with All Three Parameters

```python
# sequence[start:stop:step]

data = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

# From index 1 to 8, every 2 steps
print(data[1:8:2])    # [1, 3, 5, 7]

# From index 0 to end, every 3 steps
print(data[0::3])     # [0, 3, 6, 9]

# Reverse from index 8 down to index 1
print(data[8:1:-1])   # [8, 7, 6, 5, 4, 3, 2]

# Reverse from index 8 down to index 0 (inclusive)
print(data[8::-1])    # [8, 7, 6, 5, 4, 3, 2, 1, 0]
```

---

## 8. Slice Object

Python has a built-in `slice()` object — useful when you want to **store and reuse** a slice definition.

```python
s = slice(1, 5)        # equivalent to [1:5]
s2 = slice(0, 10, 2)   # equivalent to [0:10:2]

data = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]

print(data[s])         # [20, 30, 40, 50]
print(data[s2])        # [10, 30, 50, 70, 90]
```

### slice() attributes

```python
s = slice(2, 10, 3)
print(s.start)   # 2
print(s.stop)    # 10
print(s.step)    # 3
```

### Practical use — reusable slice definitions

```python
HEADER_SLICE = slice(0, 1)
DATA_SLICE = slice(1, -1)
FOOTER_SLICE = slice(-1, None)

rows = ["header", "row1", "row2", "row3", "footer"]

print(rows[HEADER_SLICE])   # ['header']
print(rows[DATA_SLICE])     # ['row1', 'row2', 'row3']
print(rows[FOOTER_SLICE])   # ['footer']
```

---

## 9. Mutable vs Immutable Slicing

### Immutable (Strings, Tuples) — Read Only

```python
name = "Python"
name[0] = "J"    # ❌ TypeError: 'str' object does not support item assignment
```

### Mutable (Lists) — Can Modify via Slice Assignment

```python
numbers = [1, 2, 3, 4, 5]

# Replace a slice
numbers[1:3] = [20, 30]
print(numbers)   # [1, 20, 30, 4, 5]

# Insert elements (replace empty slice)
numbers[2:2] = [100, 200]
print(numbers)   # [1, 20, 100, 200, 30, 4, 5]

# Delete a slice
numbers[2:4] = []
print(numbers)   # [1, 20, 30, 4, 5]

# Replace with more or fewer elements
numbers[1:4] = [99]
print(numbers)   # [1, 99, 5]
```

---

## 10. Slicing Strings

```python
sentence = "Hello, World! Welcome to Python."

# Get first word
print(sentence[:5])           # Hello

# Get last word
print(sentence[-7:-1])        # Python

# Get every other character
print(sentence[::2])          # Hlo ol!Wloet yhn

# Reverse the string
print(sentence[::-1])         # .nohtyP ot emocleW !dlroW ,olleH

# Check if a string is a palindrome
word = "racecar"
print(word == word[::-1])     # True

word2 = "python"
print(word2 == word2[::-1])   # False
```

---

## 11. Slicing Lists

```python
students = ["Ali", "Sara", "Omar", "Mona", "Karim", "Layla", "Tarek"]

# First 3 students
print(students[:3])         # ['Ali', 'Sara', 'Omar']

# Last 3 students
print(students[-3:])        # ['Karim', 'Layla', 'Tarek']

# Middle students (skip first and last)
print(students[1:-1])       # ['Sara', 'Omar', 'Mona', 'Karim', 'Layla']

# Every other student
print(students[::2])        # ['Ali', 'Omar', 'Karim', 'Tarek']

# Reverse the list
print(students[::-1])       # ['Tarek', 'Layla', 'Karim', 'Mona', 'Omar', 'Sara', 'Ali']

# Shallow copy of the list
copy = students[:]
print(copy)                 # Same as students, but a NEW list object
```

---

## 12. Slicing Tuples

Tuples behave exactly like lists for slicing, but the result is always a tuple:

```python
data = (10, 20, 30, 40, 50)

print(data[1:4])     # (20, 30, 40)
print(data[::-1])    # (50, 40, 30, 20, 10)
print(data[::2])     # (10, 30, 50)
```

---

## 13. Slicing with NumPy Arrays

NumPy is a scientific computing library — its slicing is extremely powerful.

```python
import numpy as np

arr = np.array([10, 20, 30, 40, 50, 60, 70, 80])

# Basic slicing (same as lists)
print(arr[2:5])       # [30 40 50]
print(arr[::-1])      # [80 70 60 50 40 30 20 10]

# NumPy slices return VIEWS, not copies
view = arr[2:5]
view[0] = 999
print(arr)            # [10 20 999 40 50 60 70 80]  ← original changed!

# To avoid this, use .copy()
safe = arr[2:5].copy()
safe[0] = 111
print(arr)            # unchanged
```

### 2D NumPy Array Slicing

```python
matrix = np.array([
    [1,  2,  3,  4],
    [5,  6,  7,  8],
    [9,  10, 11, 12],
    [13, 14, 15, 16]
])

# First 2 rows
print(matrix[:2])
# [[1 2 3 4]
#  [5 6 7 8]]

# First 2 rows, first 2 columns
print(matrix[:2, :2])
# [[1 2]
#  [5 6]]

# All rows, column 1
print(matrix[:, 1])   # [ 2  6 10 14]

# Every other row and column
print(matrix[::2, ::2])
# [[ 1  3]
#  [ 9 11]]
```

---

## 14. Slicing 2D Lists and Matrices

Pure Python 2D lists require a different approach:

```python
matrix = [
    [1,  2,  3,  4],
    [5,  6,  7,  8],
    [9,  10, 11, 12],
    [13, 14, 15, 16]
]

# Get first 2 rows
print(matrix[:2])       # [[1, 2, 3, 4], [5, 6, 7, 8]]

# Get a specific row
print(matrix[1])        # [5, 6, 7, 8]

# Get a specific element
print(matrix[2][3])     # 12

# Get a column (requires list comprehension)
col1 = [row[1] for row in matrix]
print(col1)             # [2, 6, 10, 14]

# Get a sub-matrix (rows 0-1, cols 0-1)
sub = [row[:2] for row in matrix[:2]]
print(sub)              # [[1, 2], [5, 6]]
```

---

## 15. Use Cases — All Possible

| Use Case | Code Example |
|----------|-------------|
| Get first N items | `data[:N]` |
| Get last N items | `data[-N:]` |
| Skip first N items | `data[N:]` |
| Skip last N items | `data[:-N]` |
| Reverse a sequence | `data[::-1]` |
| Every Nth element | `data[::N]` |
| Remove first and last | `data[1:-1]` |
| Get middle section | `data[N:M]` |
| Palindrome check | `s == s[::-1]` |
| Shallow copy | `data[:]` |
| Split at position | `data[:mid], data[mid:]` |
| Pagination (page N, size K) | `data[N*K:(N+1)*K]` |
| Batch processing | `for i in range(0,len(d),batch): chunk=d[i:i+batch]` |
| Rolling window | `for i in range(len(d)-n+1): window=d[i:i+n]` |
| CSV first/last rows | `rows[:5]`, `rows[-5:]` |

---

## 16. Real World Applications

### 🔹 Web Scraping — Extract specific columns from a table

```python
html_rows = ["<tr>header</tr>", "<tr>row1</tr>", "<tr>row2</tr>", "<tr>footer</tr>"]
data_rows = html_rows[1:-1]   # Skip header and footer
print(data_rows)
```

### 🔹 Machine Learning — Train/Test Split

```python
dataset = list(range(1000))   # 1000 samples
split = int(len(dataset) * 0.8)

train = dataset[:split]   # 800 samples
test  = dataset[split:]   # 200 samples

print(f"Train: {len(train)}, Test: {len(test)}")
```

### 🔹 Pagination System

```python
def paginate(data, page, page_size):
    start = page * page_size
    end = start + page_size
    return data[start:end]

articles = list(range(1, 101))  # 100 articles

print(paginate(articles, 0, 10))   # Page 1: [1..10]
print(paginate(articles, 1, 10))   # Page 2: [11..20]
print(paginate(articles, 9, 10))   # Page 10: [91..100]
```

### 🔹 Batch Processing (AI / ETL pipelines)

```python
records = list(range(1, 1001))   # 1000 records
BATCH_SIZE = 100

for i in range(0, len(records), BATCH_SIZE):
    batch = records[i:i + BATCH_SIZE]
    print(f"Processing batch {i//BATCH_SIZE + 1}: {batch[0]}–{batch[-1]}")
```

### 🔹 Sliding Window (Finance / Signal Processing)

```python
prices = [100, 102, 101, 105, 110, 108, 115, 120]
window_size = 3

for i in range(len(prices) - window_size + 1):
    window = prices[i:i + window_size]
    avg = sum(window) / window_size
    print(f"Window {i+1}: {window} → Average: {avg:.2f}")
```

### 🔹 String Processing — Parse File Extension

```python
filename = "document_report_2024.pdf"
extension = filename[-3:]     # pdf
basename = filename[:-4]      # document_report_2024
print(extension, basename)
```

### 🔹 Reverse Words in a Sentence

```python
sentence = "Hello World Python"
words = sentence.split()
reversed_sentence = " ".join(words[::-1])
print(reversed_sentence)   # Python World Hello
```

### 🔹 Image Processing (Pixel Manipulation)

```python
import numpy as np

# Simulate a 100x100 grayscale image
image = np.random.randint(0, 256, (100, 100))

# Crop top-left 50x50 region
crop = image[:50, :50]

# Flip horizontally
flipped = image[:, ::-1]

# Flip vertically
flipped_v = image[::-1, :]
```

---

## 17. Senior / Professional Level Mastery

### 🏆 Tip 1: Avoid copying large data unnecessarily

```python
# ❌ Bad — creates a copy every time
def process(data):
    return sum(data[:])

# ✅ Better — no copy needed
def process(data):
    return sum(data)
```

### 🏆 Tip 2: Use memoryview for zero-copy slicing of bytes

```python
data = b"Hello World Python"
mv = memoryview(data)

# Slice without copying
chunk = mv[6:11]
print(bytes(chunk))   # b'World'
```

### 🏆 Tip 3: Use islice from itertools for lazy slicing of iterators

```python
from itertools import islice

def infinite_counter():
    n = 0
    while True:
        yield n
        n += 1

gen = infinite_counter()
first_10 = list(islice(gen, 10))
print(first_10)   # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### 🏆 Tip 4: __getitem__ — implement slicing in your own class

```python
class MySequence:
    def __init__(self, data):
        self.data = data
    
    def __getitem__(self, key):
        if isinstance(key, slice):
            start, stop, step = key.indices(len(self.data))
            return [self.data[i] for i in range(start, stop, step or 1)]
        return self.data[key]
    
    def __len__(self):
        return len(self.data)

seq = MySequence([10, 20, 30, 40, 50])
print(seq[1:4])     # [20, 30, 40]
print(seq[::2])     # [10, 30, 50]
print(seq[-1])      # 50
```

### 🏆 Tip 5: Named slices for readable code

```python
# Instead of magic numbers everywhere:
data = "2024-04-20"
year  = data[0:4]
month = data[5:7]
day   = data[8:10]

# Use named slices:
YEAR  = slice(0, 4)
MONTH = slice(5, 7)
DAY   = slice(8, 10)

print(data[YEAR])    # 2024
print(data[MONTH])   # 04
print(data[DAY])     # 20
```

### 🏆 Tip 6: Deque for efficient front/back slicing

```python
from collections import deque

# Lists are slow for popping from the front: O(n)
# deque is O(1) for both ends
d = deque([1, 2, 3, 4, 5])
d.appendleft(0)
d.popleft()
print(list(d))   # [1, 2, 3, 4, 5]
```

---

## 18. Common Mistakes and How to Avoid Them

### ❌ Mistake 1: Off-by-one in stop index

```python
name = "Python"
print(name[0:3])   # Pyt — NOT Pyth (stop is exclusive!)
```

### ❌ Mistake 2: Expecting slice to raise error on out-of-range

```python
data = [1, 2, 3]
print(data[0:100])   # [1, 2, 3] — no error, just returns what exists
print(data[10:20])   # []         — empty, no error
```

### ❌ Mistake 3: Forgetting NumPy slices are VIEWS not copies

```python
import numpy as np
arr = np.array([1, 2, 3, 4, 5])
view = arr[1:3]
view[0] = 999        # This CHANGES arr!
print(arr)           # [1 999 3 4 5]
```

### ❌ Mistake 4: Modifying a list while slicing it

```python
data = [1, 2, 3, 4, 5]
# Never do this in a loop — use a copy instead
for item in data[:]:   # data[:] creates a copy — safe to modify data
    if item % 2 == 0:
        data.remove(item)
print(data)   # [1, 3, 5]
```

---

## 19. Practice Challenges

Try these on your own to master the lesson:

1. Given `"Hello, World!"` — extract just `"World"` using slicing
2. Reverse the string `"abcdefgh"` using slicing
3. Given a list of 20 numbers, extract every 3rd element
4. Write a function `is_palindrome(s)` using slicing
5. Implement a paginator that takes a list, page number, and page size
6. Given a 4x4 matrix (list of lists), extract the diagonal elements using slicing and list comprehension
7. Use a sliding window of size 5 to compute the rolling average of a price list
8. Implement `__getitem__` in a custom class that supports negative indexing and slicing

---

## 📌 Summary

| Concept | Syntax | Result |
|---------|--------|--------|
| Basic index | `s[i]` | Single element |
| Negative index | `s[-i]` | From end |
| Basic slice | `s[a:b]` | Elements a to b-1 |
| From start | `s[:b]` | Elements 0 to b-1 |
| To end | `s[a:]` | Elements a to end |
| Full copy | `s[:]` | All elements |
| Step | `s[::n]` | Every nth element |
| Reverse | `s[::-1]` | All elements reversed |
| Negative slice | `s[-b:-a]` | Counted from end |
| Slice object | `slice(a,b,c)` | Reusable slice |

---
