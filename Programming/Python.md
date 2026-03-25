## Introduction

**Python** is a high-level, interpreted, general-purpose programming language created by **Guido van Rossum** and first released in **1991**. Python emphasizes **code readability** and simplicity — its clean syntax lets developers express ideas in fewer lines than most other languages. Python is used everywhere: **web development**, **data science**, **machine learning**, **automation**, **scripting**, **APIs**, and more. It runs on Windows, Linux, and macOS, and comes with a massive standard library plus a huge ecosystem of third-party packages via **pip**.


## Basic Syntax

**Definition:** Python uses indentation (spaces) instead of curly braces to define code blocks — no semicolons needed.

### Hello World
**Definition:** The simplest Python program — print text to the screen.
```python
print("Hello, World!")
```

### Comments
**Definition:** Comments are ignored by Python — use them to explain your code.
```python
# This is a single-line comment

"""
This is a
multi-line comment (docstring)
"""
```

### Indentation
**Definition:** Python uses 4 spaces of indentation to define blocks — this is NOT optional.
```python
if True:
    print("Indented block")    # 4 spaces — required
    print("Still in block")

print("Outside block")         # Back to no indent
```

### Print
**Definition:** Output values to the console — supports multiple items and custom separators.
```python
print("Hello")                    # Basic print
print("Name:", "Dark")            # Multiple items
print("A", "B", "C", sep="-")    # Custom separator → A-B-C
print("Hello", end=" ")          # No newline at end
print("World")                    # → Hello World
```

---

## Variables & Assignment

**Definition:** Variables hold data — no type declaration needed, Python figures it out automatically.

### Basic Assignment
**Definition:** Create a variable by writing `name = value` — Python detects the type automatically.
```python
name    = "Dark"       # String
age     = 25           # Integer
pi      = 3.14159      # Float
is_admin = True        # Boolean
nothing  = None        # None — represents absence of value
```

### Multiple Assignment
**Definition:** Assign multiple variables at once in a single line.
```python
a, b, c = 1, 2, 3        # a=1, b=2, c=3
x = y = z = 0            # All three get value 0
a, b = b, a              # Swap two values
```

### Augmented Assignment
**Definition:** Update a variable's value using shorthand operators.
```python
x = 10
x += 5     # x = x + 5  → 15
x -= 3     # x = x - 3  → 12
x *= 2     # x = x * 2  → 24
x /= 4     # x = x / 4  → 6.0
x //= 2    # x = x // 2 → 3  (floor division)
x **= 2    # x = x ** 2 → 9  (power)
x %= 4     # x = x % 4  → 1  (remainder)
```

### Delete Variable
**Definition:** Remove a variable from memory using `del`.
```python
del name       # Delete variable
# print(name)  # Would raise NameError
```

---

## Data Types

**Definition:** Python has several built-in data types — each stores a different kind of value.

### Checking Type
**Definition:** Find out what type a variable is using `type()`.
```python
print(type(42))          # <class 'int'>
print(type(3.14))        # <class 'float'>
print(type("hello"))     # <class 'str'>
print(type(True))        # <class 'bool'>
print(type(None))        # <class 'NoneType'>
print(type([1, 2]))      # <class 'list'>
print(type({"a": 1}))   # <class 'dict'>
```

### Numeric Types
**Definition:** Python has integers, floats, and complex numbers for different levels of precision.
```python
x = 10          # int — whole number
y = 3.14        # float — decimal number
z = 2 + 3j      # complex — real + imaginary part

big = 1_000_000         # Underscores for readability
binary  = 0b1010        # Binary → 10
octal   = 0o17          # Octal → 15
hexa    = 0xFF          # Hexadecimal → 255
```

### Boolean
**Definition:** `True` or `False` — used in conditions and comparisons.
```python
t = True
f = False

# Falsy values — treated as False in conditions
bool(0)        # False
bool("")       # False
bool([])       # False
bool(None)     # False

# Truthy values — everything else is True
bool(1)        # True
bool("hi")     # True
bool([1, 2])   # True
```

### None
**Definition:** `None` represents the absence of a value — like null in other languages.
```python
result = None

if result is None:
    print("No value yet")

def greet():
    pass           # Function returns None implicitly
```

---

## Type Conversion

**Definition:** Convert a value from one type to another — called casting.

### Explicit Conversion
**Definition:** Manually convert using built-in functions — Python won't do it automatically.
```python
int("42")          # String → int → 42
int(3.9)           # Float → int → 3  (truncates, not rounds)
float("3.14")      # String → float → 3.14
float(5)           # Int → float → 5.0
str(42)            # Int → string → "42"
str(3.14)          # Float → string → "3.14"
bool(0)            # Int → bool → False
bool(1)            # Int → bool → True
list("abc")        # String → list → ['a', 'b', 'c']
list((1, 2, 3))    # Tuple → list → [1, 2, 3]
tuple([1, 2, 3])   # List → tuple → (1, 2, 3)
set([1, 2, 2, 3])  # List → set → {1, 2, 3} (removes duplicates)
```

---

## String Operations

**Definition:** Strings are sequences of characters — they are immutable (cannot be changed in place).

### Creating Strings
**Definition:** Strings can use single, double, or triple quotes.
```python
s1 = 'Hello'
s2 = "World"
s3 = '''Multi
line string'''
s4 = """Also
multi-line"""
```

### Basic Info
**Definition:** Get the length or check basic properties of a string.
```python
s = "Hello, World!"
len(s)               # Length → 13
s.upper()            # HELLO, WORLD!
s.lower()            # hello, world!
s.title()            # Hello, World! (capitalize each word)
s.strip()            # Remove leading/trailing whitespace
s.lstrip()           # Remove only left whitespace
s.rstrip()           # Remove only right whitespace
```

### Search & Check
**Definition:** Find out if a string contains, starts with, or ends with something.
```python
s = "Hello, World!"
s.startswith("Hello")   # True
s.endswith("!")         # True
s.find("World")         # 7 — index of first match (-1 if not found)
s.count("l")            # 3 — how many times "l" appears
"World" in s            # True — membership check
```

### Replace & Split
**Definition:** Modify a string by replacing parts, or break it into a list of pieces.
```python
s = "Hello, World!"
s.replace("World", "Python")   # "Hello, Python!"
s.split(", ")                  # ["Hello", "World!"]
s.split()                      # Split on whitespace → ["Hello,", "World!"]
", ".join(["a", "b", "c"])     # "a, b, c" — join list into string
```

### Slicing
**Definition:** Extract a portion of a string using index positions.
```python
s = "Hello, World!"
s[0]        # First character → H
s[-1]       # Last character → !
s[0:5]      # From 0 to 4 → Hello
s[7:]       # From 7 to end → World!
s[:5]       # From start to 4 → Hello
s[::2]      # Every 2nd character → Hlo ol!
s[::-1]     # Reversed → !dlroW ,olleH
```

### String Formatting
**Definition:** Embed variables and expressions inside strings — f-strings are the modern preferred way.
```python
name = "Dark"
age  = 25

# f-string (Python 3.6+) — preferred
print(f"Name: {name}, Age: {age}")
print(f"Next year: {age + 1}")
print(f"Pi: {3.14159:.2f}")        # 2 decimal places → Pi: 3.14

# .format() method
print("Name: {}, Age: {}".format(name, age))
print("Name: {0}, Age: {1}".format(name, age))

# % formatting (old style)
print("Name: %s, Age: %d" % (name, age))
```

---

## Lists

**Definition:** An ordered, mutable (changeable) collection of items — items can be of any type.

### Create List
**Definition:** Make a list using square brackets with comma-separated values.
```python
fruits  = ["apple", "banana", "cherry"]
nums    = [1, 2, 3, 4, 5]
mixed   = [1, "hello", 3.14, True]       # Any types allowed
nested  = [[1, 2], [3, 4], [5, 6]]       # List of lists
empty   = []                              # Empty list
```

### Access Elements
**Definition:** Get items using their index — negative index counts from the end.
```python
fruits = ["apple", "banana", "cherry"]
fruits[0]        # apple — first item
fruits[-1]       # cherry — last item
fruits[1:3]      # ["banana", "cherry"] — slice
fruits[:2]       # ["apple", "banana"] — first two
fruits[::2]      # Every 2nd item
```

### Modify List
**Definition:** Change, add, or remove items — lists are mutable so they can be edited.
```python
fruits[1] = "blueberry"       # Update item at index 1

fruits.append("mango")        # Add to end
fruits.insert(1, "grape")     # Insert at index 1
fruits.extend(["kiwi", "pear"])  # Add multiple items

fruits.remove("apple")        # Remove first match by value
fruits.pop()                  # Remove and return last item
fruits.pop(1)                 # Remove and return item at index 1
del fruits[0]                 # Delete item at index 0
fruits.clear()                # Remove all items
```

### List Info & Search
**Definition:** Get information about the list — length, count, and position of items.
```python
fruits = ["apple", "banana", "cherry", "apple"]
len(fruits)             # 4 — number of items
fruits.count("apple")  # 2 — how many times "apple" appears
fruits.index("banana") # 1 — position of "banana"
"cherry" in fruits      # True — membership check
```

### Sort & Reverse
**Definition:** Rearrange list items in order or reverse order.
```python
nums = [3, 1, 4, 1, 5, 9]
nums.sort()                       # Sort in place: [1, 1, 3, 4, 5, 9]
nums.sort(reverse=True)           # Sort descending
nums.reverse()                    # Reverse in place

sorted(nums)                      # Return new sorted list (original unchanged)
sorted(nums, reverse=True)        # New list, descending
sorted(fruits, key=len)           # Sort by string length
```

### Copy List
**Definition:** Make an independent copy of a list — simple `=` just copies the reference.
```python
original = [1, 2, 3]
copy1 = original.copy()    # Shallow copy
copy2 = original[:]        # Slice copy — same result
copy3 = list(original)     # Convert — same result

import copy
deep = copy.deepcopy(original)   # Deep copy — for nested lists
```

---

## Tuples

**Definition:** An ordered, immutable (unchangeable) collection — like a list but cannot be modified after creation.

### Create Tuple
**Definition:** Make a tuple using parentheses — or just commas (parentheses are optional).
```python
coords  = (10, 20)
rgb     = (255, 128, 0)
single  = (42,)             # Single-item tuple — comma is required!
empty   = ()
also    = 1, 2, 3           # Parentheses optional — still a tuple
```

### Access & Unpack
**Definition:** Get items by index, or unpack all values into separate variables at once.
```python
point = (10, 20, 30)
point[0]         # 10
point[-1]        # 30
point[0:2]       # (10, 20)

x, y, z = point             # Unpack into variables
x, *rest = point            # x=10, rest=[20, 30]
first, *_, last = point     # first=10, last=30
```

### Tuple vs List
**Definition:** Use tuples for data that should not change — they are faster and safer than lists.

| Feature | List | Tuple |
|---------|------|-------|
| Mutable | Yes | No |
| Syntax | `[1, 2, 3]` | `(1, 2, 3)` |
| Speed | Slower | Faster |
| Use for | Changeable data | Fixed data |

---

## Sets

**Definition:** An unordered collection of unique values — duplicates are automatically removed.

### Create Set
**Definition:** Make a set using curly braces or `set()` — order is not guaranteed.
```python
fruits = {"apple", "banana", "cherry"}
nums   = {1, 2, 3, 2, 1}     # Duplicates removed → {1, 2, 3}
empty  = set()                # Empty set — NOT {} (that's a dict!)
```

### Modify Set
**Definition:** Add or remove items — but you cannot access by index since sets are unordered.
```python
fruits.add("mango")           # Add one item
fruits.update(["kiwi", "pear"])  # Add multiple items
fruits.remove("apple")        # Remove item — raises error if not found
fruits.discard("apple")       # Remove item — no error if not found
fruits.pop()                  # Remove and return a random item
fruits.clear()                # Remove all items
```

### Set Operations
**Definition:** Mathematical set operations — union, intersection, difference.
```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}

a | b              # Union — all items → {1, 2, 3, 4, 5, 6}
a & b              # Intersection — common items → {3, 4}
a - b              # Difference — in a but not b → {1, 2}
a ^ b              # Symmetric difference — not in both → {1, 2, 5, 6}

a.union(b)
a.intersection(b)
a.difference(b)
a.issubset(b)      # True if a is subset of b
a.issuperset(b)    # True if a contains all of b
```

---

## Dictionaries

**Definition:** A collection of key-value pairs — keys must be unique, values can be anything.

### Create Dictionary
**Definition:** Make a dictionary using curly braces with `key: value` pairs.
```python
user = {
    "name": "Dark",
    "age": 25,
    "city": "Mumbai"
}

empty = {}
also  = dict(name="Dark", age=25)    # Using dict() constructor
```

### Access Values
**Definition:** Get values using their key — two ways: brackets (raises error) or `.get()` (safe).
```python
user["name"]              # "Dark" — raises KeyError if missing
user.get("name")          # "Dark" — returns None if missing
user.get("email", "N/A")  # "N/A" — custom default if key missing
```

### Modify Dictionary
**Definition:** Add new keys, update existing values, or remove keys.
```python
user["email"] = "dark@email.com"   # Add new key
user["age"] = 26                   # Update existing value
user.update({"city": "Delhi", "age": 27})   # Update multiple at once

del user["city"]           # Delete a key — raises error if missing
user.pop("city")           # Delete and return value — raises error if missing
user.pop("city", None)     # Delete safely — returns None if missing
user.clear()               # Remove all items
```

### Loop & Check
**Definition:** Iterate over keys, values, or both — and check if a key exists.
```python
user = {"name": "Dark", "age": 25}

"name" in user             # True — check if key exists
user.keys()                # All keys → dict_keys(["name", "age"])
user.values()              # All values → dict_values(["Dark", 25])
user.items()               # All pairs → dict_items([("name", "Dark"), ...])

for key in user:
    print(key, user[key])

for key, value in user.items():
    print(f"{key}: {value}")
```

### Merge Dictionaries
**Definition:** Combine two dictionaries into one.
```python
a = {"x": 1, "y": 2}
b = {"y": 3, "z": 4}

merged = {**a, **b}       # Merge — b values overwrite a on conflict
a.update(b)               # Update a in place with b's items

# Python 3.9+
merged = a | b            # Merge operator
a |= b                    # Update in place
```

---

## Operators

**Definition:** Symbols that perform operations on values — arithmetic, comparison, logical, and more.

### Arithmetic
**Definition:** Basic math operations — note `//` for integer division and `**` for power.
```python
10 + 3     # Addition → 13
10 - 3     # Subtraction → 7
10 * 3     # Multiplication → 30
10 / 3     # Division → 3.333... (always float)
10 // 3    # Floor division → 3 (integer result)
10 % 3     # Modulo (remainder) → 1
10 ** 3    # Power → 1000
```

### Comparison
**Definition:** Compare two values — always returns `True` or `False`.
```python
5 == 5     # Equal → True
5 != 3     # Not equal → True
5 > 3      # Greater than → True
5 < 10     # Less than → True
5 >= 5     # Greater or equal → True
5 <= 5     # Less or equal → True
```

### Logical
**Definition:** Combine multiple conditions into one result.
```python
True and False    # Both must be True → False
True or False     # At least one True → True
not True          # Negate → False

# Short-circuit evaluation
x = 5
(x > 0) and (x < 10)    # True — both conditions met
(x < 0) or (x > 3)      # True — second condition met
```

### Identity & Membership
**Definition:** Check if two variables refer to the same object, or if a value is inside a collection.
```python
a = [1, 2, 3]
b = a
c = [1, 2, 3]

a is b       # True — same object in memory
a is c       # False — equal but different objects
a is not c   # True

2 in a       # True — membership check
5 not in a   # True
```

### Bitwise
**Definition:** Operate directly on bits — used in low-level programming and flags.
```python
a = 0b1010   # 10
b = 0b1100   # 12

a & b    # AND → 0b1000 = 8
a | b    # OR  → 0b1110 = 14
a ^ b    # XOR → 0b0110 = 6
~a       # NOT → -11
a << 1   # Left shift → 20
a >> 1   # Right shift → 5
```

---

## If Statements

**Definition:** Execute different code blocks based on whether a condition is true or false.

### Basic If / Else
**Definition:** The simplest form — one path if true, another if false.
```python
age = 20

if age >= 18:
    print("Adult")
else:
    print("Minor")
```

### If / Elif / Else
**Definition:** Chain multiple conditions — Python checks top to bottom, first match runs.
```python
score = 75

if score >= 90:
    print("A grade")
elif score >= 80:
    print("B grade")
elif score >= 70:
    print("C grade")
elif score >= 60:
    print("D grade")
else:
    print("F grade")
```

### Ternary (One-liner)
**Definition:** A compact one-line if/else — great for simple conditional assignments.
```python
age = 20
label = "Adult" if age >= 18 else "Minor"
print(label)    # Adult
```

### Nested If
**Definition:** An if statement inside another if — use sparingly to avoid deep nesting.
```python
num = 15

if num > 0:
    if num % 2 == 0:
        print("Positive even")
    else:
        print("Positive odd")
else:
    print("Not positive")
```

---

## While Loop

**Definition:** Repeat a block of code as long as a condition stays true — checks before each iteration.

### Basic While
**Definition:** Runs repeatedly while the condition is true — stops when it becomes false.
```python
count = 1
while count <= 5:
    print(f"Count: {count}")
    count += 1                  # Increment to avoid infinite loop
```

### While with Break
**Definition:** Exit the loop immediately when a certain condition is met.
```python
while True:
    user_input = input("Enter 'quit' to stop: ")
    if user_input == "quit":
        break                   # Exit loop immediately
    print(f"You typed: {user_input}")
```

### While with Continue
**Definition:** Skip the rest of the current iteration and go back to the condition check.
```python
count = 0
while count < 10:
    count += 1
    if count % 2 == 0:
        continue               # Skip even numbers
    print(count)               # Prints: 1 3 5 7 9
```

### While with Else
**Definition:** The `else` block runs only if the loop completed normally — not if `break` was used.
```python
count = 1
while count <= 3:
    print(count)
    count += 1
else:
    print("Loop finished normally")
```

---

## For Loop

**Definition:** Iterate over each item in a sequence — list, string, range, tuple, dictionary, etc.

### Basic For Loop
**Definition:** Go through each item in a collection one by one.
```python
fruits = ["apple", "banana", "cherry"]

for fruit in fruits:
    print(fruit)

# Loop over a string
for char in "Hello":
    print(char)
```

### Range
**Definition:** Generate a sequence of numbers to loop over — `range(start, stop, step)`.
```python
for i in range(5):          # 0, 1, 2, 3, 4
    print(i)

for i in range(1, 6):       # 1, 2, 3, 4, 5
    print(i)

for i in range(0, 10, 2):   # 0, 2, 4, 6, 8 (step=2)
    print(i)

for i in range(10, 0, -1):  # 10, 9, 8 ... 1 (countdown)
    print(i)
```

### Enumerate
**Definition:** Loop with both the index and the value at the same time.
```python
fruits = ["apple", "banana", "cherry"]

for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")
# 0: apple
# 1: banana
# 2: cherry

for index, fruit in enumerate(fruits, start=1):  # Start index at 1
    print(f"{index}: {fruit}")
```

### Zip
**Definition:** Loop over two or more lists at the same time — pairs up items by position.
```python
names  = ["Alice", "Bob", "Charlie"]
scores = [85, 92, 78]

for name, score in zip(names, scores):
    print(f"{name}: {score}")
```

### Loop over Dictionary
**Definition:** Iterate through dictionary keys, values, or key-value pairs.
```python
user = {"name": "Dark", "age": 25}

for key in user:                      # Keys only
    print(key)

for value in user.values():           # Values only
    print(value)

for key, value in user.items():       # Both
    print(f"{key}: {value}")
```

### For with Else
**Definition:** The `else` runs after the loop finishes normally — skipped if `break` was used.
```python
for i in range(5):
    if i == 3:
        break
else:
    print("Loop complete")   # Does NOT print because break was used
```

---

## Loop Control

**Definition:** Keywords to control how loops execute — skip, stop, or do nothing.

### break
**Definition:** Exit the loop completely — no further iterations run.
```python
for i in range(10):
    if i == 5:
        break              # Stop at 5 — prints 0 1 2 3 4
    print(i)
```

### continue
**Definition:** Skip the rest of the current iteration — go straight to the next one.
```python
for i in range(10):
    if i % 2 == 0:
        continue           # Skip even — prints 1 3 5 7 9
    print(i)
```

### pass
**Definition:** Do nothing — a placeholder for code you plan to write later.
```python
for i in range(5):
    pass                   # Loop runs but does nothing

def my_function():
    pass                   # Function exists but does nothing yet
```

---

## Functions

**Definition:** A named, reusable block of code — define once, call many times with different inputs.

### Basic Function
**Definition:** The simplest form — define with `def`, call by name.
```python
def say_hello():
    print("Hello, World!")

say_hello()    # Call the function
```

### Parameters
**Definition:** Accept input values — positional or keyword arguments.
```python
def greet(name):
    print(f"Hello, {name}!")

greet("Dark")           # Positional → Hello, Dark!
greet(name="Dark")      # Keyword → Hello, Dark!
```

### Default Parameters
**Definition:** Give a parameter a fallback value — used if the caller doesn't provide one.
```python
def greet(name, greeting="Hello"):
    print(f"{greeting}, {name}!")

greet("Dark")              # Hello, Dark!
greet("Dark", "Hi")        # Hi, Dark!
greet("Dark", greeting="Hey")   # Hey, Dark!
```

### Return Values
**Definition:** Send a result back to the caller using `return`.
```python
def add(a, b):
    return a + b

result = add(5, 3)
print(result)    # 8

def get_min_max(nums):
    return min(nums), max(nums)    # Return multiple values as tuple

lo, hi = get_min_max([3, 1, 7, 2])
print(lo, hi)    # 1 7
```

### *args — Variable Positional Arguments
**Definition:** Accept any number of positional arguments — collected into a tuple.
```python
def add_all(*nums):
    return sum(nums)

add_all(1, 2, 3)          # 6
add_all(1, 2, 3, 4, 5)    # 15
```

### **kwargs — Variable Keyword Arguments
**Definition:** Accept any number of keyword arguments — collected into a dictionary.
```python
def show_info(**info):
    for key, value in info.items():
        print(f"{key}: {value}")

show_info(name="Dark", age=25, city="Mumbai")
```

### Combined Parameters
**Definition:** Mix all parameter types in the right order — positional, defaults, *args, **kwargs.
```python
def full_func(name, age=0, *args, **kwargs):
    print(f"Name: {name}, Age: {age}")
    print(f"Extra args: {args}")
    print(f"Extra kwargs: {kwargs}")

full_func("Dark", 25, "extra1", color="blue")
```

---

## Lambda Functions

**Definition:** Small anonymous (unnamed) functions defined in a single line — great for short operations.

### Basic Lambda
**Definition:** Create a simple function without naming it — useful for quick, one-time use.
```python
# Regular function
def square(x):
    return x * x

# Same as lambda
square = lambda x: x * x

print(square(5))    # 25
```

### Lambda with Multiple Arguments
**Definition:** Lambda functions can take more than one parameter.
```python
add    = lambda a, b: a + b
result = add(3, 4)            # 7

power  = lambda base, exp: base ** exp
result = power(2, 10)         # 1024
```

### Lambda with Built-ins
**Definition:** Lambdas are most useful with functions like `sorted()`, `map()`, `filter()`.
```python
nums = [3, 1, 4, 1, 5, 9, 2, 6]

# Sort by custom key
sorted(nums, key=lambda x: -x)           # Descending → [9, 6, 5, 4, 3, 2, 1, 1]

people = [("Alice", 30), ("Bob", 25), ("Charlie", 35)]
sorted(people, key=lambda p: p[1])       # Sort by age

# map — apply function to each item
squares = list(map(lambda x: x**2, nums))   # [9, 1, 16, 1, 25, 81, 4, 36]

# filter — keep items where function returns True
evens = list(filter(lambda x: x % 2 == 0, nums))   # [4, 2, 6]
```

---

## Scope

**Definition:** Where a variable is accessible — local (inside function) or global (outside all functions).

### Local Scope
**Definition:** Variables created inside a function only exist inside that function.
```python
def my_func():
    x = 10          # Local variable
    print(x)

my_func()
# print(x)    # NameError — x doesn't exist outside
```

### Global Scope
**Definition:** Variables created outside all functions are global — readable everywhere.
```python
name = "Dark"       # Global variable

def greet():
    print(name)     # Reads global variable — OK

greet()
```

### Global Keyword
**Definition:** Use `global` to modify a global variable from inside a function.
```python
count = 0

def increment():
    global count    # Tell Python we mean the global count
    count += 1

increment()
increment()
print(count)        # 2
```

### Nonlocal Keyword
**Definition:** Access and modify a variable from an enclosing (outer) function — used in nested functions.
```python
def outer():
    x = 10

    def inner():
        nonlocal x      # Modify outer function's variable
        x = 20

    inner()
    print(x)            # 20

outer()
```

---

## Classes & OOP

**Definition:** Object-Oriented Programming — group related data (attributes) and behavior (methods) into a class.

### Define a Class
**Definition:** A class is a blueprint — `__init__` runs when an object is created.
```python
class Person:
    def __init__(self, name, age):   # Constructor
        self.name = name             # Instance attribute
        self.age  = age

    def greet(self):                 # Instance method
        print(f"Hi, I'm {self.name} and I'm {self.age}.")

# Create object (instance)
p1 = Person("Dark", 25)
p1.greet()              # Hi, I'm Dark and I'm 25.
print(p1.name)          # Dark
```

### Class vs Instance Attributes
**Definition:** Class attributes are shared by all instances — instance attributes belong to one object.
```python
class Dog:
    species = "Canis lupus"    # Class attribute — shared by all dogs

    def __init__(self, name):
        self.name = name       # Instance attribute — unique per dog

d1 = Dog("Rex")
d2 = Dog("Buddy")

print(d1.species)    # Canis lupus — from class
print(d1.name)       # Rex — from instance
print(d2.name)       # Buddy
```

### Class Methods & Static Methods
**Definition:** `@classmethod` receives the class — `@staticmethod` receives nothing special.
```python
class Circle:
    pi = 3.14159

    def __init__(self, radius):
        self.radius = radius

    def area(self):                     # Instance method
        return Circle.pi * self.radius ** 2

    @classmethod
    def from_diameter(cls, diameter):  # Class method — alternative constructor
        return cls(diameter / 2)

    @staticmethod
    def info():                         # Static method — no self or cls
        print("A circle is a round shape")

c1 = Circle(5)
c2 = Circle.from_diameter(10)
Circle.info()
```

### Magic / Dunder Methods
**Definition:** Special methods with double underscores — define how objects behave with operators and functions.
```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __str__(self):           # print(v) → "Vector(3, 4)"
        return f"Vector({self.x}, {self.y})"

    def __repr__(self):          # Developer representation
        return f"Vector(x={self.x}, y={self.y})"

    def __add__(self, other):    # v1 + v2
        return Vector(self.x + other.x, self.y + other.y)

    def __len__(self):           # len(v)
        return int((self.x**2 + self.y**2) ** 0.5)

    def __eq__(self, other):     # v1 == v2
        return self.x == other.x and self.y == other.y

v1 = Vector(3, 4)
v2 = Vector(1, 2)
print(v1)           # Vector(3, 4)
print(v1 + v2)      # Vector(4, 6)
```

---

## Inheritance

**Definition:** A child class inherits all attributes and methods from a parent class — and can add its own or override them.

### Basic Inheritance
**Definition:** Use `class Child(Parent)` syntax — child gets everything the parent has.
```python
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        print(f"{self.name} makes a sound")

class Dog(Animal):
    def speak(self):                    # Override parent method
        print(f"{self.name} says Woof!")

class Cat(Animal):
    def speak(self):
        print(f"{self.name} says Meow!")

d = Dog("Rex")
c = Cat("Whiskers")
d.speak()    # Rex says Woof!
c.speak()    # Whiskers says Meow!
```

### super()
**Definition:** Call the parent class's method — useful when overriding but still needing parent behavior.
```python
class Employee(Person):
    def __init__(self, name, age, company):
        super().__init__(name, age)    # Call Person's __init__
        self.company = company

    def greet(self):
        super().greet()                # Call parent greet
        print(f"I work at {self.company}")

e = Employee("Dark", 25, "Google")
e.greet()
```

### Multiple Inheritance
**Definition:** A class can inherit from more than one parent class.
```python
class Flyable:
    def fly(self):
        print("I can fly!")

class Swimmable:
    def swim(self):
        print("I can swim!")

class Duck(Flyable, Swimmable):
    pass

d = Duck()
d.fly()     # I can fly!
d.swim()    # I can swim!
```

### isinstance & issubclass
**Definition:** Check if an object is an instance of a class, or if a class inherits from another.
```python
d = Dog("Rex")
isinstance(d, Dog)       # True
isinstance(d, Animal)    # True — Dog is a subclass of Animal
issubclass(Dog, Animal)  # True
```

---

## Error Handling

**Definition:** Catch and handle errors gracefully so programs don't crash unexpectedly.

### Try / Except
**Definition:** Wrap risky code in `try` — if it fails, `except` handles the error.
```python
try:
    result = 10 / 0
    print(result)
except ZeroDivisionError:
    print("Cannot divide by zero!")
```

### Multiple Except Blocks
**Definition:** Handle different error types with separate except blocks.
```python
try:
    value = int(input("Enter a number: "))
    result = 10 / value
except ValueError:
    print("That's not a valid number!")
except ZeroDivisionError:
    print("Cannot divide by zero!")
except Exception as e:
    print(f"Unexpected error: {e}")
```

### Else & Finally
**Definition:** `else` runs if no exception occurred — `finally` always runs regardless.
```python
try:
    result = 10 / 2
except ZeroDivisionError:
    print("Error!")
else:
    print(f"Result: {result}")    # Runs only if no exception
finally:
    print("Always runs")          # Cleanup — always executes
```

### Raise Exceptions
**Definition:** Manually trigger an exception when something goes wrong in your logic.
```python
def divide(a, b):
    if b == 0:
        raise ValueError("Cannot divide by zero")
    return a / b

try:
    divide(10, 0)
except ValueError as e:
    print(e)
```

### Custom Exceptions
**Definition:** Create your own exception types by inheriting from `Exception`.
```python
class InsufficientFundsError(Exception):
    def __init__(self, amount, balance):
        self.message = f"Cannot withdraw {amount}. Balance: {balance}"
        super().__init__(self.message)

def withdraw(amount, balance):
    if amount > balance:
        raise InsufficientFundsError(amount, balance)
    return balance - amount

try:
    withdraw(500, 200)
except InsufficientFundsError as e:
    print(e)
```

### Common Built-in Exceptions
**Definition:** Frequently encountered Python exceptions and what causes them.

| Exception | Cause |
|-----------|-------|
| `ValueError` | Wrong value type or format |
| `TypeError` | Wrong data type in operation |
| `KeyError` | Dictionary key doesn't exist |
| `IndexError` | List index out of range |
| `ZeroDivisionError` | Division by zero |
| `FileNotFoundError` | File doesn't exist |
| `AttributeError` | Object doesn't have attribute |
| `ImportError` | Module not found |
| `NameError` | Variable not defined |
| `StopIteration` | Iterator exhausted |

---

## File Handling

**Definition:** Read from and write to files on disk using `open()` — always close files when done.

### Open Modes
**Definition:** The second argument to `open()` controls how the file is accessed.

| Mode | Meaning |
|------|---------|
| `r` | Read (default) — error if file missing |
| `w` | Write — creates file, overwrites existing |
| `a` | Append — adds to end, creates if missing |
| `x` | Create — error if file already exists |
| `b` | Binary mode — add to other modes (`rb`, `wb`) |
| `r+` | Read and write |

### Read Files
**Definition:** Open and read file content — fully or line by line.
```python
# Read entire file at once
with open("file.txt", "r") as f:
    content = f.read()

# Read line by line
with open("file.txt", "r") as f:
    for line in f:
        print(line.strip())

# Read all lines into a list
with open("file.txt", "r") as f:
    lines = f.readlines()
```

### Write Files
**Definition:** Write text to a file — overwrite with `w` or append with `a`.
```python
# Write (overwrite)
with open("file.txt", "w") as f:
    f.write("Hello, World!\n")
    f.write("Second line\n")

# Append to existing file
with open("file.txt", "a") as f:
    f.write("Added this line\n")

# Write multiple lines at once
lines = ["Line 1\n", "Line 2\n", "Line 3\n"]
with open("file.txt", "w") as f:
    f.writelines(lines)
```

### Binary Files
**Definition:** Read or write binary data — images, audio, PDFs, etc.
```python
# Read binary
with open("image.png", "rb") as f:
    data = f.read()

# Write binary
with open("copy.png", "wb") as f:
    f.write(data)
```

### With Statement
**Definition:** `with open()` automatically closes the file — always use this instead of manual `close()`.
```python
# Bad — manual close (easy to forget)
f = open("file.txt")
content = f.read()
f.close()

# Good — with statement handles closing automatically
with open("file.txt") as f:
    content = f.read()
```

---

## List Comprehensions

**Definition:** A concise, readable way to create lists — combines a loop and optional condition in one line.

### Basic Comprehension
**Definition:** Build a new list by applying an expression to each item in an iterable.
```python
# Regular loop
squares = []
for x in range(10):
    squares.append(x ** 2)

# Same as list comprehension
squares = [x ** 2 for x in range(10)]
# [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

### With Condition (Filter)
**Definition:** Add an `if` clause to include only items that meet a condition.
```python
evens  = [x for x in range(20) if x % 2 == 0]
# [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]

words  = ["apple", "banana", "cherry", "kiwi"]
long_words = [w for w in words if len(w) > 5]
# ["banana", "cherry"]
```

### Nested Comprehension
**Definition:** Flatten nested loops or create 2D structures in one expression.
```python
# Flatten a 2D list
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
flat   = [num for row in matrix for num in row]
# [1, 2, 3, 4, 5, 6, 7, 8, 9]

# Create multiplication table
table = [[i * j for j in range(1, 4)] for i in range(1, 4)]
# [[1, 2, 3], [2, 4, 6], [3, 6, 9]]
```

### Dict & Set Comprehensions
**Definition:** The same syntax works for dictionaries and sets too.
```python
# Dict comprehension
squares_dict = {x: x**2 for x in range(6)}
# {0: 0, 1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

# Filter dict
filtered = {k: v for k, v in squares_dict.items() if v > 5}

# Set comprehension
unique_lengths = {len(w) for w in ["apple", "banana", "kiwi"]}
# {4, 5, 6}
```

---

## Iterators & Generators

**Definition:** Objects that produce values one at a time — memory-efficient for large data.

### Iterators
**Definition:** Any object with `__iter__` and `__next__` — use `next()` to get values one by one.
```python
nums = [1, 2, 3]
it   = iter(nums)

next(it)    # 1
next(it)    # 2
next(it)    # 3
# next(it)  # StopIteration error — no more items
```

### Generators (Functions)
**Definition:** Use `yield` instead of `return` — produces values lazily, one at a time.
```python
def count_up(n):
    i = 1
    while i <= n:
        yield i         # Pause here, give value, resume next call
        i += 1

gen = count_up(5)
print(next(gen))   # 1
print(next(gen))   # 2

for num in count_up(5):
    print(num)     # 1 2 3 4 5
```

### Generator Expressions
**Definition:** Like list comprehensions but with `()` — lazy, memory-efficient.
```python
# List comprehension — builds entire list in memory
squares_list = [x**2 for x in range(1000000)]

# Generator expression — computes one at a time
squares_gen  = (x**2 for x in range(1000000))

# Use just like any iterator
total = sum(x**2 for x in range(1000))
```

---

## Decorators

**Definition:** A function that wraps another function to add behavior before or after it runs.

### Basic Decorator
**Definition:** Wrap a function using `@decorator` syntax — runs extra code around the original.
```python
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print("Before function runs")
        result = func(*args, **kwargs)
        print("After function runs")
        return result
    return wrapper

@my_decorator
def say_hello(name):
    print(f"Hello, {name}!")

say_hello("Dark")
# Before function runs
# Hello, Dark!
# After function runs
```

### Timer Decorator
**Definition:** A practical decorator that measures how long a function takes to run.
```python
import time

def timer(func):
    def wrapper(*args, **kwargs):
        start  = time.time()
        result = func(*args, **kwargs)
        end    = time.time()
        print(f"{func.__name__} took {end - start:.4f} seconds")
        return result
    return wrapper

@timer
def slow_function():
    time.sleep(1)
    return "done"

slow_function()   # slow_function took 1.0001 seconds
```

### functools.wraps
**Definition:** Preserves the original function's name and docstring when decorating.
```python
from functools import wraps

def my_decorator(func):
    @wraps(func)              # Keeps original function metadata
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs)
    return wrapper
```

---

## Modules & Imports

**Definition:** A module is a `.py` file containing reusable code — import it to use its functions and classes.

### Import Styles
**Definition:** Different ways to bring a module's contents into your script.
```python
import math                      # Import whole module
import math as m                 # Import with alias
from math import sqrt            # Import specific function
from math import sqrt, pi, floor # Import multiple specific items
from math import *               # Import everything (avoid — pollutes namespace)
```

### Using Modules
**Definition:** Access the module's functions and constants using dot notation.
```python
import math

math.sqrt(16)        # 4.0
math.pi              # 3.14159...
math.floor(3.9)      # 3
math.ceil(3.1)       # 4
math.pow(2, 10)      # 1024.0
math.log(100, 10)    # 2.0
math.factorial(5)    # 120
```

### Create Your Own Module
**Definition:** Any `.py` file is a module — save functions in it and import from other files.
```python
# File: myutils.py
def add(a, b):
    return a + b

def greet(name):
    return f"Hello, {name}!"

PI = 3.14159

# In another file:
import myutils
myutils.add(2, 3)      # 5
myutils.greet("Dark")  # Hello, Dark!
```

### __name__ Guard
**Definition:** Code inside this block only runs when the file is executed directly — not when imported.
```python
def main():
    print("Running main logic")

if __name__ == "__main__":
    main()     # Only runs if this file is executed, not imported
```

### Common Standard Library Modules
**Definition:** Useful modules that come built into Python — no installation needed.

| Module | Purpose |
|--------|---------|
| `os` | File system and OS operations |
| `sys` | System info and command-line args |
| `math` | Math functions |
| `random` | Random number generation |
| `datetime` | Dates and times |
| `json` | JSON encoding and decoding |
| `csv` | CSV file reading and writing |
| `re` | Regular expressions |
| `time` | Time-related functions |
| `collections` | Specialized data structures |
| `itertools` | Advanced iteration tools |
| `pathlib` | File path handling (modern) |
| `shutil` | File copy/move operations |
| `urllib` | URL handling |
| `logging` | Logging system |

---

## Built-in Functions

**Definition:** Functions available everywhere in Python — no import needed.

### Numeric Functions
**Definition:** Built-in functions for working with numbers.
```python
abs(-5)              # 5 — absolute value
round(3.14159, 2)    # 3.14 — round to 2 decimals
pow(2, 10)           # 1024 — power
divmod(10, 3)        # (3, 1) — quotient and remainder
max(3, 1, 4, 1, 5)  # 5
min(3, 1, 4, 1, 5)  # 1
sum([1, 2, 3, 4])   # 10
```

### Sequence Functions
**Definition:** Built-in functions for working with lists, tuples, strings, and other sequences.
```python
len([1, 2, 3])             # 3 — length
sorted([3, 1, 2])          # [1, 2, 3] — new sorted list
reversed([1, 2, 3])        # iterator in reverse
list(reversed([1, 2, 3]))  # [3, 2, 1]
enumerate([10, 20, 30])    # (0,10), (1,20), (2,30)
zip([1,2], [3,4])          # (1,3), (2,4)
map(str, [1, 2, 3])        # ['1', '2', '3']
filter(bool, [0,1,2,None]) # [1, 2] — removes falsy
any([False, True, False])  # True — any truthy?
all([True, True, False])   # False — all truthy?
```

### Object Functions
**Definition:** Inspect and interact with objects and their attributes.
```python
type(42)               # <class 'int'>
isinstance(42, int)    # True
id(42)                 # Memory address
dir([])                # List all methods of a list
vars(obj)              # Object's __dict__ attribute
hasattr(obj, "name")   # True if attribute exists
getattr(obj, "name")   # Get attribute value
setattr(obj, "name", "Dark")  # Set attribute
```

### Input / Output
**Definition:** Read from the user or display output.
```python
name = input("Enter name: ")    # Read string from user
print("Hello", name)            # Print to console
print("Hello", name, end="\n")  # Custom end character
```

---

## String Formatting

**Definition:** Methods to embed variables, numbers, and expressions neatly into strings.

### f-Strings (Recommended)
**Definition:** The modern, fastest, most readable way to format strings — Python 3.6+.
```python
name  = "Dark"
age   = 25
price = 1234.567

f"Name: {name}"                    # Name: Dark
f"Age next year: {age + 1}"        # Age next year: 26
f"Price: {price:.2f}"              # Price: 1234.57
f"Pi: {3.14159:.4f}"               # Pi: 3.1416
f"{name!u}"                        # DARK (uppercase)
f"{name!r}"                        # 'Dark' (repr)
f"{1000000:,}"                     # 1,000,000 (comma separator)
f"{0.85:.0%}"                      # 85% (percentage)
f"{'left':<10}"                    # 'left      ' (left align, width 10)
f"{'right':>10}"                   # '     right' (right align)
f"{'center':^10}"                  # '  center  ' (center align)
```

### .format() Method
**Definition:** Older but still widely used method — uses `{}` placeholders.
```python
"Hello, {}!".format("Dark")         # Hello, Dark!
"Name: {0}, Age: {1}".format("Dark", 25)
"Name: {name}".format(name="Dark")  # Named placeholders
"{:.2f}".format(3.14159)            # 3.14
```

### % Formatting (Old Style)
**Definition:** The oldest formatting method — still works but f-strings are preferred.
```python
"Hello, %s!" % "Dark"              # Hello, Dark!
"Age: %d" % 25                     # Age: 25
"Pi: %.2f" % 3.14159               # Pi: 3.14
"Name: %s, Age: %d" % ("Dark", 25)
```

---

## Regular Expressions

**Definition:** Pattern matching in strings using the `re` module — find, search, replace, and validate text.

### Import & Basic Match
**Definition:** Import the `re` module and use `match`, `search`, or `findall` to find patterns.
```python
import re

# re.match — match at beginning of string
re.match(r"\d+", "123abc")       # Match object
re.match(r"\d+", "abc123")       # None — no match at start

# re.search — find anywhere in string
re.search(r"\d+", "abc123def")   # Match "123"

# re.findall — return all matches as list
re.findall(r"\d+", "1a2b3c")    # ["1", "2", "3"]
```

### Common Patterns
**Definition:** Frequently used regex patterns for real-world validation tasks.
```python
# Email validation
re.match(r"^[\w.-]+@[\w.-]+\.\w{2,}$", "test@email.com")

# Phone number
re.match(r"^\d{3}-\d{3}-\d{4}$", "123-456-7890")

# URL
re.match(r"https?://[\w./%-]+", "https://google.com")

# Only letters
re.match(r"^[a-zA-Z]+$", "Hello")

# Only numbers
re.match(r"^\d+$", "12345")
```

### Replace & Split
**Definition:** Substitute matching text with something else, or split a string by a pattern.
```python
re.sub(r"\d+", "NUM", "I have 3 cats and 2 dogs")
# "I have NUM cats and NUM dogs"

re.sub(r"\s+", " ", "too   many    spaces")
# "too many spaces"

re.split(r"[,;]+", "a,b;;c,d")
# ["a", "b", "c", "d"]
```

### Regex Flags
**Definition:** Modify how a pattern is matched — case-insensitive, multiline, etc.
```python
re.search(r"hello", "Hello World", re.IGNORECASE)   # Case-insensitive
re.findall(r"^\w+", "line1\nline2", re.MULTILINE)   # Match each line start
```

### Quick Reference
**Definition:** Common regex symbols and what they mean.

| Pattern | Meaning |
|---------|---------|
| `.` | Any character except newline |
| `\d` | Digit (0-9) |
| `\w` | Word character (letter, digit, _) |
| `\s` | Whitespace |
| `^` | Start of string |
| `$` | End of string |
| `*` | 0 or more times |
| `+` | 1 or more times |
| `?` | 0 or 1 time |
| `{n}` | Exactly n times |
| `{n,m}` | Between n and m times |
| `[abc]` | Any of a, b, or c |
| `(abc)` | Capture group |

---

## Date & Time

**Definition:** Work with dates, times, and durations using the `datetime` module.

### Get Current Date/Time
**Definition:** Retrieve the current date, time, or both.
```python
from datetime import datetime, date, time, timedelta

now   = datetime.now()        # Current date and time
today = date.today()          # Current date only
print(now)                    # 2025-01-15 14:30:00.123456
print(today)                  # 2025-01-15
```

### Create Specific Date/Time
**Definition:** Build a date or datetime object for a specific point in time.
```python
dt = datetime(2025, 6, 15, 9, 30, 0)   # year, month, day, hour, min, sec
d  = date(2025, 6, 15)                  # date only
t  = time(9, 30, 0)                     # time only
```

### Format & Parse
**Definition:** Convert datetime to string and vice versa using format codes.
```python
now = datetime.now()

# Format datetime as string
now.strftime("%Y-%m-%d")           # "2025-01-15"
now.strftime("%d/%m/%Y %H:%M:%S")  # "15/01/2025 14:30:00"
now.strftime("%B %d, %Y")          # "January 15, 2025"

# Parse string to datetime
datetime.strptime("2025-01-15", "%Y-%m-%d")
datetime.strptime("15/06/2025", "%d/%m/%Y")
```

### Date Arithmetic
**Definition:** Add or subtract time from dates using `timedelta`.
```python
now = datetime.now()

tomorrow  = now + timedelta(days=1)
last_week = now - timedelta(weeks=1)
in_2_hrs  = now + timedelta(hours=2)

# Difference between two dates
d1 = date(2025, 1, 1)
d2 = date(2025, 12, 31)
diff = d2 - d1
print(diff.days)    # 364
```

---

## Math Module

**Definition:** Built-in `math` module for advanced mathematical operations.

### Basic Functions
**Definition:** Common math operations not available with operators alone.
```python
import math

math.sqrt(25)        # 5.0 — square root
math.pow(2, 10)      # 1024.0 — power
math.factorial(6)    # 720
math.gcd(12, 8)      # 4 — greatest common divisor
math.lcm(4, 6)       # 12 — least common multiple (Python 3.9+)
math.abs(-5)         # Use built-in abs() instead
```

### Rounding Functions
**Definition:** Different ways to round a number depending on the direction needed.
```python
math.floor(4.9)      # 4 — round down
math.ceil(4.1)       # 5 — round up
math.trunc(4.9)      # 4 — truncate decimal (toward zero)
round(4.5)           # 4 — banker's rounding (built-in)
round(3.14159, 2)    # 3.14
```

### Constants & Logarithms
**Definition:** Mathematical constants and logarithm functions.
```python
math.pi              # 3.141592653589793
math.e               # 2.718281828459045
math.inf             # Infinity
math.nan             # Not a Number

math.log(100, 10)    # 2.0 — log base 10
math.log2(8)         # 3.0 — log base 2
math.log(math.e)     # 1.0 — natural log
math.exp(1)          # 2.718... — e^x
```

### Trigonometry
**Definition:** Sine, cosine, and related functions — angles in radians.
```python
math.sin(math.pi / 2)    # 1.0
math.cos(0)              # 1.0
math.tan(math.pi / 4)    # 1.0
math.degrees(math.pi)    # 180.0 — radians to degrees
math.radians(180)        # 3.14... — degrees to radians
```

---

## Working with JSON

**Definition:** JSON (JavaScript Object Notation) is a common data format for APIs and config files.

### Encode (Python → JSON)
**Definition:** Convert Python objects to a JSON string using `json.dumps()`.
```python
import json

data = {
    "name": "Dark",
    "age": 25,
    "skills": ["Python", "SQL"],
    "active": True
}

json_str = json.dumps(data)                    # Compact JSON string
json_str = json.dumps(data, indent=2)          # Pretty-printed
json_str = json.dumps(data, sort_keys=True)    # Keys in alphabetical order
```

### Decode (JSON → Python)
**Definition:** Convert a JSON string back to Python objects using `json.loads()`.
```python
json_str = '{"name": "Dark", "age": 25}'

data = json.loads(json_str)
print(data["name"])    # Dark
print(data["age"])     # 25
```

### Read & Write JSON Files
**Definition:** Load JSON from a file or save Python data to a JSON file.
```python
# Write to file
with open("data.json", "w") as f:
    json.dump(data, f, indent=2)

# Read from file
with open("data.json", "r") as f:
    loaded = json.load(f)

print(loaded["name"])    # Dark
```

---

## Working with CSV

**Definition:** CSV (Comma-Separated Values) — a common format for tabular data like spreadsheets.

### Read CSV
**Definition:** Open and read rows from a CSV file — each row becomes a list or dictionary.
```python
import csv

# Read as lists
with open("data.csv", "r") as f:
    reader = csv.reader(f)
    for row in reader:
        print(row)           # ['Alice', '30', 'Engineer']

# Read as dicts (first row = headers)
with open("data.csv", "r") as f:
    reader = csv.DictReader(f)
    for row in reader:
        print(row["name"], row["age"])
```

### Write CSV
**Definition:** Write data to a CSV file — as rows or from dictionaries.
```python
# Write lists
with open("output.csv", "w", newline="") as f:
    writer = csv.writer(f)
    writer.writerow(["name", "age", "role"])   # Header
    writer.writerow(["Dark", 25, "Dev"])       # Data row
    writer.writerows([["Alice", 30, "PM"], ["Bob", 28, "QA"]])

# Write dicts
fields = ["name", "age", "role"]
rows   = [{"name": "Dark", "age": 25, "role": "Dev"}]

with open("output.csv", "w", newline="") as f:
    writer = csv.DictWriter(f, fieldnames=fields)
    writer.writeheader()
    writer.writerows(rows)
```

---

## OS & File System

**Definition:** Interact with the operating system — files, folders, paths, and environment.

### File Operations
**Definition:** Check, create, copy, move, and delete files and directories.
```python
import os
import shutil

os.path.exists("file.txt")      # True if path exists
os.path.isfile("file.txt")      # True if it's a file
os.path.isdir("folder")         # True if it's a directory
os.path.getsize("file.txt")     # File size in bytes

os.remove("file.txt")           # Delete a file
os.rename("old.txt", "new.txt") # Rename file
shutil.copy("a.txt", "b.txt")   # Copy file
shutil.move("a.txt", "dir/")    # Move file
```

### Directory Operations
**Definition:** Create, navigate, and delete directories.
```python
os.getcwd()                       # Current working directory
os.chdir("/home/user")            # Change directory
os.listdir(".")                   # List files in directory
os.mkdir("new_folder")            # Create one directory
os.makedirs("a/b/c", exist_ok=True)  # Create nested directories
os.rmdir("empty_folder")          # Remove empty directory
shutil.rmtree("folder")           # Remove directory and all contents
```

### Path Handling (pathlib — Modern)
**Definition:** The modern way to work with file paths — cleaner than `os.path`.
```python
from pathlib import Path

p = Path("/home/user/file.txt")

p.name         # "file.txt"
p.stem         # "file" (no extension)
p.suffix       # ".txt"
p.parent       # /home/user
p.exists()     # True/False
p.is_file()    # True/False
p.is_dir()     # True/False

p.read_text()              # Read file content
p.write_text("Hello")     # Write to file

# Build paths safely
home   = Path.home()
config = home / ".config" / "settings.json"   # Uses / operator!

list(Path(".").glob("*.py"))    # Find all .py files
list(Path(".").rglob("*.txt"))  # Find recursively
```

### Environment Variables
**Definition:** Read and set environment variables using `os.environ`.
```python
import os

os.environ.get("HOME")              # Get value (None if missing)
os.environ.get("PATH", "/usr/bin")  # With default
os.environ["MY_VAR"] = "value"      # Set variable

os.getenv("HOME")                   # Same as get()
```

---

## Virtual Environments

**Definition:** An isolated Python environment for each project — keeps dependencies separate.

### Create & Activate
**Definition:** Set up a new virtual environment and activate it for your project.
```bash
# Create virtual environment
python -m venv venv              # Creates venv/ folder

# Activate
# Windows:
venv\Scripts\activate

# Linux / macOS:
source venv/bin/activate

# Deactivate (when done)
deactivate
```

### Why Use Virtual Environments
**Definition:** Each project can have its own package versions — no conflicts between projects.
```
Project A → needs requests==2.28
Project B → needs requests==2.31
Solution  → each project has its own venv!
```

---

## pip — Package Manager

**Definition:** pip is Python's package installer — download and manage third-party libraries.

### Install & Uninstall
**Definition:** Add or remove packages from the current Python environment.
```bash
pip install requests             # Install latest version
pip install requests==2.28.0    # Install specific version
pip install "requests>=2.0"     # Install minimum version
pip install -r requirements.txt # Install all from file
pip uninstall requests           # Remove package
pip install --upgrade requests   # Upgrade to latest
```

### View Packages
**Definition:** List installed packages and check their versions.
```bash
pip list                         # All installed packages
pip show requests                # Info about one package
pip freeze                       # All packages with versions (for requirements.txt)
pip freeze > requirements.txt    # Save current environment to file
```

### requirements.txt
**Definition:** A text file listing all packages needed for a project — allows others to recreate your environment.
```
requests==2.28.0
flask==2.3.0
pandas>=1.5.0
numpy
```
```bash
pip install -r requirements.txt  # Install all listed packages
```

---

## Debugging

**Definition:** Finding and fixing errors in Python code — using print, assertions, or the debugger.

### Print Debugging
**Definition:** The simplest way — print values at key points to see what's happening.
```python
x = calculate_something()
print(f"DEBUG: x = {x}, type = {type(x)}")   # Quick inspection
```

### Assert
**Definition:** Check that a condition is true — crashes with `AssertionError` if it's not.
```python
def divide(a, b):
    assert b != 0, "Cannot divide by zero!"
    return a / b

divide(10, 0)   # AssertionError: Cannot divide by zero!
```

### pdb — Python Debugger
**Definition:** Built-in interactive debugger — pause execution and inspect variables step by step.
```python
import pdb

def buggy_function(x):
    pdb.set_trace()        # Execution pauses here
    result = x * 2
    return result

# Python 3.7+ shorthand
def buggy_function(x):
    breakpoint()           # Same as pdb.set_trace()
    result = x * 2
    return result
```

### pdb Commands
**Definition:** Commands you type at the `(Pdb)` prompt to control execution.

| Command | Action |
|---------|--------|
| `n` | Next line |
| `s` | Step into function |
| `c` | Continue until next breakpoint |
| `q` | Quit debugger |
| `p var` | Print variable value |
| `l` | Show current code |
| `b 10` | Set breakpoint at line 10 |

### Logging
**Definition:** A better alternative to `print()` for production code — shows timestamps and severity levels.
```python
import logging

logging.basicConfig(level=logging.DEBUG,
                    format="%(asctime)s - %(levelname)s - %(message)s")

logging.debug("Debug info")       # Only shown at DEBUG level
logging.info("Process started")
logging.warning("Disk almost full")
logging.error("Failed to connect")
logging.critical("System down!")
```

---

## Shortcut Tips

**Definition:** Handy Python tricks that help you write cleaner and faster code.

### Unpacking
**Definition:** Extract values from lists, tuples, or iterables into variables in one line.
```python
first, *rest       = [1, 2, 3, 4, 5]    # first=1, rest=[2,3,4,5]
*start, last       = [1, 2, 3, 4, 5]    # start=[1,2,3,4], last=5
first, *mid, last  = [1, 2, 3, 4, 5]    # first=1, mid=[2,3,4], last=5
a, b = b, a                              # Swap variables
```

### Walrus Operator (Python 3.8+)
**Definition:** Assign and use a value in the same expression using `:=`.
```python
# Old way — two lines
n = len(data)
if n > 10:
    print(n)

# Walrus — one line
if (n := len(data)) > 10:
    print(n)

# In while loop
while chunk := f.read(8192):
    process(chunk)
```

### Useful One-Liners
**Definition:** Common tasks written concisely in Python.
```python
# Flatten list of lists
flat = [x for sublist in nested for x in sublist]

# Remove duplicates preserving order
unique = list(dict.fromkeys(items))

# Count items
from collections import Counter
count = Counter(["a", "b", "a", "c", "a"])    # Counter({'a': 3, 'b': 1, 'c': 1})

# Default dict — no KeyError
from collections import defaultdict
d = defaultdict(list)
d["key"].append(1)      # No error even if "key" doesn't exist

# Chained comparison
1 < x < 10             # Cleaner than x > 1 and x < 10
0 <= age <= 120        # Check valid age range

# Get max/min with key
max(words, key=len)    # Longest word
min(nums, key=abs)     # Number closest to zero
```

---

## Best Practices

**Definition:** Guidelines for writing clean, readable, and Pythonic code.

### PEP 8 Style
**Definition:** The official Python style guide — follow it so your code is consistent with the community.
```python
# Variable and function names: lowercase_with_underscores
user_name = "dark"
def calculate_total():
    pass

# Class names: CapWords (PascalCase)
class UserAccount:
    pass

# Constants: UPPER_CASE
MAX_RETRIES = 3
PI = 3.14159

# Spaces around operators
x = 5 + 3       # Good
x=5+3           # Bad

# 2 blank lines between top-level definitions
def func_one():
    pass


def func_two():
    pass
```

### Write Readable Code
**Definition:** Code is read far more than it is written — prioritize clarity over cleverness.
```python
# Bad — unclear variable names
def f(x, y):
    return x * y / 100

# Good — self-documenting names
def calculate_discount(price, percent):
    return price * percent / 100

# Bad — magic number
if age > 65:
    pass

# Good — named constant
SENIOR_AGE = 65
if age > SENIOR_AGE:
    pass
```

### Use Context Managers
**Definition:** Always use `with` for files, database connections, and locks — ensures cleanup happens.
```python
# Bad — file might not close if exception occurs
f = open("file.txt")
data = f.read()
f.close()

# Good — closes automatically even if exception occurs
with open("file.txt") as f:
    data = f.read()
```

### Keep Functions Small
**Definition:** Each function should do one thing and do it well — easier to test and understand.
```python
# Bad — does too many things
def process_user(user):
    # validate
    # save to db
    # send email
    # log activity
    pass

# Good — each function has one responsibility
def validate_user(user): pass
def save_user(user): pass
def send_welcome_email(user): pass
def log_user_creation(user): pass
```

### Prefer List Comprehensions
**Definition:** Use comprehensions for simple transformations — they are more Pythonic and faster.
```python
# Less Pythonic
squares = []
for x in range(10):
    squares.append(x ** 2)

# More Pythonic
squares = [x ** 2 for x in range(10)]
```

### Handle Errors Specifically
**Definition:** Catch specific exceptions — never use bare `except` which hides real bugs.
```python
# Bad — catches everything including bugs you should see
try:
    result = do_something()
except:
    pass

# Good — handle only what you expect
try:
    result = do_something()
except ValueError as e:
    print(f"Value error: {e}")
except FileNotFoundError:
    print("File missing")
```

### Summary of Rules

* Follow **PEP 8** for naming and formatting
* Use **meaningful names** — `user_name` not `u` or `x`
* Write **docstrings** for functions and classes
* Use **`with`** for file and resource handling
* **Avoid bare `except`** — catch specific exceptions
* Keep functions **small and focused** — one task each
* Use **type hints** for better readability (Python 3.5+)
* Write **tests** — even basic ones catch regressions
* Use **list comprehensions** for simple loops
* **Don't repeat yourself (DRY)** — extract repeated code into functions
