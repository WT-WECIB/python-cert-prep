# Python Obscure Topics Cheatsheet

## datetime Module

```python
import datetime

# Current date and time
now = datetime.datetime.now()

# Format as string
now.strftime("%Y-%m-%d")     # "2025-01-08"
now.strftime("%H:%M:%S")     # "14:30:45"
now.strftime("%A")           # "Wednesday" (full day name)
now.strftime("%a")           # "Wed" (abbreviated)
now.strftime("%B")           # "January" (full month)
now.strftime("%b")           # "Jan" (abbreviated)

# Day of week (0=Monday, 6=Sunday)
now.weekday()                # 2 = Wednesday

# Date only
datetime.date.today()        # 2025-01-08 (no time)
```

## File I/O - Syntax & Edge Cases

```python
# Writing (overwrites existing)
with open("file.txt", "w") as f:
    f.write("Hello")

# Appending (adds to end)
with open("file.txt", "a") as f:
    f.write("World")

# Reading entire file as string
with open("file.txt", "r") as f:
    content = f.read()

# Reading all lines as list (with \n)
with open("file.txt", "r") as f:
    lines = f.readlines()    # ['line1\n', 'line2\n']

# Iterating line by line
with open("file.txt", "r") as f:
    for line in f:
        print(line.strip())   # strip() removes \n

# WITHOUT 'with' (NOT recommended - file stays open)
f = open("file.txt")
data = f.read()
# File never closed - resource leak!

# Correct way without 'with'
f = open("file.txt")
data = f.read()
f.close()                     # Must manually close
```

## sys.argv - Command-Line Arguments

```python
import sys

# python script.py arg1 arg2 arg3
print(sys.argv)              # ['script.py', 'arg1', 'arg2', 'arg3']
print(sys.argv[0])           # 'script.py' (script name)
print(sys.argv[1])           # 'arg1' (first argument)

# Check if arguments provided
if len(sys.argv) > 1:
    print(f"Got args: {sys.argv[1:]}")
```

## math Module - Key Functions

```python
import math

# Rounding
math.ceil(4.1)               # 5 (round UP)
math.floor(4.9)              # 4 (round DOWN)
math.trunc(4.9)              # 4 (truncate - same as floor for positive)

# Square root
math.sqrt(16)                # 4.0 (returns float)
math.isqrt(17)               # 4 (integer square root)

# Power
math.pow(2, 3)               # 8.0 (returns float)

# Constants
math.pi                      # 3.14159...

# NaN check
math.isnan(float("nan"))     # True
math.nan                     # NaN value

# Modulo (remainder)
math.fmod(10, 3)             # 1.0
```

## random Module - Inclusive vs Exclusive

```python
import random

# INCLUSIVE on both ends
random.randint(1, 10)        # 1, 2, 3, ... 10 (can be 1 OR 10)

# EXCLUSIVE on end (like range)
random.randrange(1, 10)      # 1, 2, 3, ... 9 (NOT 10)
random.randrange(0, 10, 2)   # 0, 2, 4, 6, 8 (step by 2)

# Pick one element
random.choice([1, 2, 3])     # 2 (random single element)

# Pick k UNIQUE elements
random.sample([1, 2, 3, 4, 5], 3)  # [3, 1, 4] (no duplicates)

# Shuffle list in place
nums = [1, 2, 3, 4]
random.shuffle(nums)         # Modifies nums: [3, 1, 4, 2]

# Random float 0.0 to 1.0
random.random()              # 0.1234...
```

## os.path - File & Directory Operations

```python
import os

# Check if path exists (file OR directory)
os.path.exists("file.txt")   # True/False

# Check if it's specifically a file
os.path.isfile("file.txt")   # True/False (False if directory)

# Check if it's specifically a directory
os.path.isdir("mydir")       # True/False

# List contents of directory
os.listdir(".")              # ['file.txt', 'mydir', ...]

# Delete file (permanent!)
os.remove("file.txt")        # Deletes file immediately

# Get absolute path
os.path.abspath("file.txt")  # '/full/path/to/file.txt'

# Join paths (portable across OS)
os.path.join("folder", "file.txt")  # 'folder/file.txt'
```

## unittest Assertions

```python
import unittest

class TestExample(unittest.TestCase):
    # Check equality
    self.assertEqual(5, 5)           # Pass if equal
    self.assertNotEqual(5, 4)        # Pass if NOT equal
    
    # Check boolean
    self.assertTrue(True)             # Pass if True
    self.assertFalse(False)           # Pass if False
    
    # Check membership
    self.assertIn(1, [1, 2, 3])      # Pass if first in second
    self.assertNotIn(5, [1, 2, 3])   # Pass if NOT in
    
    # Check type
    self.assertIsInstance(5, int)    # Pass if correct type
    self.assertNotIsInstance(5, str) # Pass if wrong type
```

---

## Quick Reference Card

| Topic | Key Point |
|-------|-----------|
| **datetime.datetime.now()** | Returns both date and time |
| **strftime("%Y-%m-%d")** | Format date as string |
| **weekday()** | 0=Mon, 1=Tue, ... 6=Sun |
| **open("f", "w")** | Write (overwrites) |
| **open("f", "a")** | Append |
| **with open()** | Auto-closes file |
| **readlines()** | Returns list with \n |
| **read()** | Returns entire file as string |
| **sys.argv[0]** | Script name |
| **sys.argv[1]** | First argument |
| **math.ceil()** | Round UP |
| **math.floor()** | Round DOWN |
| **math.sqrt()** | Square root (float) |
| **randint(a,b)** | INCLUSIVE both ends |
| **randrange(a,b)** | EXCLUSIVE end (like range) |
| **random.sample()** | Pick k unique items |
| **os.path.exists()** | True/False if exists |
| **os.path.isfile()** | True if file (not dir) |
| **os.remove()** | Delete file |
| **assertEqual()** | Passes if equal |
| **assertTrue()** | Passes if True |
| **assertIn()** | Passes if in collection |
