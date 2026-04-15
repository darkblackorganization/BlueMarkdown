# Python — Complete Professional Study Notes

> **How to use these notes:**  
> Read linearly for learning. Use section headers for revision. Code blocks are meant to be typed, not just read.

---

## Table of Contents

| # | Chapter | Status |
|---|---|---|
| 1 | Introduction to Python | ✅ Current |
| 2 | Variables, Data Types & Type System | *(coming next)* |
| 3 | Operators & Expressions | *(coming next)* |
| 4 | Strings — Deep Dive | *(coming next)* |
| 5 | Control Flow — if / elif / else | *(coming next)* |
| 6 | Loops — for & while | *(coming next)* |
| 7 | Functions | *(coming next)* |
| 8 | Data Structures — Lists, Tuples, Dicts, Sets | *(coming next)* |
| 9 | File Handling | *(coming next)* |
| 10 | Object-Oriented Programming | *(coming next)* |
| 11 | Error & Exception Handling | *(coming next)* |
| 12 | Modules & Packages | *(coming next)* |

---

## Chapter 1 — Introduction to Python

---

### 1.1 What is Python?

Python is a **high-level**, **interpreted**, **dynamically typed**, **general-purpose** programming language.

It was created by **Guido van Rossum** and officially released in **1991**.  
The name "Python" was inspired by the British comedy show *Monty Python's Flying Circus* — not the snake.

Python is built on a core philosophy known as the **Zen of Python**, which includes principles like:

- *"Beautiful is better than ugly."*
- *"Simple is better than complex."*
- *"Readability counts."*

You can read the full Zen of Python by running this in any Python environment:

```python
import this
```

---

> ⚡ **Definition — High-Level Language:**  
> A language that abstracts away hardware details (memory addresses, CPU registers). You work with human-readable logic, not machine instructions.

> ⚡ **Definition — Interpreted Language:**  
> Code is executed **line by line** at runtime by an interpreter. There is no separate manual compilation step like in C or Java.

> ⚡ **Definition — Dynamically Typed:**  
> Variable types are checked **at runtime**, not at compile time. You do not declare types manually — Python infers them automatically.

---

### 1.2 Core Characteristics of Python

| Characteristic | What it Means in Practice |
|---|---|
| **High-level** | No manual memory management, no pointers |
| **Interpreted** | Run code instantly; no compile step |
| **Dynamically typed** | `x = 5` then `x = "hello"` — both are valid |
| **Strongly typed** | `"5" + 5` raises a `TypeError` — no silent coercion |
| **Garbage collected** | Unused memory is freed automatically |
| **Multi-paradigm** | Write procedural, object-oriented, or functional code |
| **Cross-platform** | Same `.py` file runs on Windows, macOS, Linux |
| **Batteries included** | Rich standard library — no installation needed for most tasks |

---

> ⚠️ **Common Confusion — Dynamic vs Weak Typing:**  
> Python is **dynamically typed** (types resolved at runtime) but also **strongly typed** (it does NOT silently convert between incompatible types).  
> JavaScript is dynamically typed AND weakly typed — that is why `"5" + 5 = "55"` in JS, but Python raises a `TypeError` instead.

---

### 1.3 Where Python is Used — Real-World Applications

Python is a dominant language across multiple professional fields.

**Web Development**  
Frameworks like Django (full-stack), Flask (micro), and FastAPI (async APIs) power thousands of production applications.

**Data Science & Analytics**  
Libraries like Pandas, NumPy, and Matplotlib form the backbone of modern data analysis workflows.

**Machine Learning & AI**  
TensorFlow, PyTorch, Keras, and scikit-learn are all Python-first. The ML industry runs largely on Python.

**Automation & Scripting**  
Python is the go-to language for automating repetitive tasks — renaming files, scraping websites, sending emails, parsing logs.

**Cybersecurity**  
Used extensively for writing exploit scripts, penetration testing tools, and network scanners.

**Cloud & DevOps**  
AWS Lambda, Google Cloud Functions, Ansible, and many CI/CD tools support Python natively.

**Scientific Computing**  
Fields like physics, genomics, finance, and astronomy use Python (SciPy, BioPython, QuantLib).

---

> ✅ **Why Python Dominates:**  
> Its combination of readable syntax + massive ecosystem + active community makes it the fastest path from idea to working software across almost any domain.

---

### 1.4 Python 2 vs Python 3 — Know the Difference

> ⚠️ **Critical Warning:**  
> **Python 2 reached End of Life on January 1, 2020.**  
> No security patches. No updates. Never use Python 2 for new work.  
> You may still encounter Python 2 in old tutorials, legacy codebases, or some Linux system tools — do not be misled by them.

| Feature | Python 2 | Python 3 |
|---|---|---|
| **Maintenance** | ✗ Dead | ✅ Active |
| **`print`** | Statement: `print "hi"` | Function: `print("hi")` |
| **Integer Division** | `5 / 2 → 2` | `5 / 2 → 2.5` |
| **Floor Division** | `5 / 2 → 2` | `5 // 2 → 2` |
| **`input()`** | Evaluates as code (dangerous) | Always returns a string (safe) |
| **String default** | ASCII | Unicode (UTF-8) |
| **`range()`** | Returns a list | Returns an iterator (memory-efficient) |
| **`xrange()`** | Exists | Removed — use `range()` |
| **`unicode` type** | Separate type | All strings are Unicode |

```python
# Python 2 style — DO NOT USE
print "Hello"          # SyntaxError in Python 3
print 5 / 2            # Prints 2, not 2.5

# Python 3 style — CORRECT
print("Hello")         # Output: Hello
print(5 / 2)           # Output: 2.5
print(5 // 2)          # Output: 2  (floor division)
```

---

### 1.5 How Python Works — Execution Model (Deep Dive)

Most beginners skip this. Understanding the execution pipeline prevents confusion about `.pyc` files, imports, and performance.

```
+--------------------------------------------------------------+
|                    PYTHON EXECUTION FLOW                     |
|                                                              |
|   your_script.py                                             |
|         |                                                    |
|         v                                                    |
|   +-----------+                                              |
|   |   Lexer   |   Breaks source code into tokens            |
|   +-----------+                                              |
|         |                                                    |
|         v                                                    |
|   +-----------+                                              |
|   |   Parser  |   Builds Abstract Syntax Tree (AST)         |
|   +-----------+                                              |
|         |                                                    |
|         v                                                    |
|   +-----------+                                              |
|   | Compiler  |   Converts AST to Bytecode (.pyc)           |
|   +-----------+                                              |
|         |                                                    |
|         v                                                    |
|   +---------------------+                                   |
|   | Python Virtual      |   Executes bytecode               |
|   | Machine  (PVM)      |   instruction by instruction      |
|   +---------------------+                                   |
|         |                                                    |
|         v                                                    |
|      OUTPUT                                                  |
+--------------------------------------------------------------+
```

#### Step 1 — Lexing (Tokenization)

The source code is read character by character and broken into meaningful units called **tokens**: keywords, operators, identifiers, and literals.

```
x = 10 + 5
→ Tokens: [NAME:'x'] [OP:'='] [NUMBER:10] [OP:'+'] [NUMBER:5]
```

#### Step 2 — Parsing

Tokens are organized into an **Abstract Syntax Tree (AST)** — a hierarchical tree representing the grammatical structure of the program. **Syntax errors are caught at this stage.**

#### Step 3 — Compilation to Bytecode

The AST is compiled into **bytecode** — a compact, low-level, platform-independent representation of your code. This bytecode is stored in `.pyc` files inside the `__pycache__/` directory.

#### Step 4 — PVM Execution

The **Python Virtual Machine (PVM)** reads and executes bytecode instructions one by one. It interacts with the OS, memory, file system, and network as required.

---

> ⚡ **What is `__pycache__`?**  
> When you run or import a Python file, Python saves compiled bytecode (`.pyc`) in a `__pycache__/` folder. On subsequent runs, if the source has not changed, Python skips re-compilation and loads the cached bytecode directly — this speeds up startup.  
> Rule: **Never edit `.pyc` files manually. Add `__pycache__/` to your `.gitignore`.**

> ⚡ **What is CPython?**  
> The standard Python interpreter from python.org is called **CPython** — it is written in the C programming language. Other implementations exist: PyPy (JIT-compiled, faster), Jython (runs on JVM), IronPython (.NET). But CPython is the reference and what you will use by default.

---

### 1.6 Installing Python

#### Windows

1. Go to `https://www.python.org/downloads/`
2. Download the latest Python 3.x Windows installer
3. Run the installer

> ⚠️ **Critical Step:** On the first screen, check **"Add Python to PATH"** BEFORE clicking Install. If you miss this, the terminal will not find Python.

4. Verify:

```cmd
python --version
pip --version
```

#### macOS

```bash
# Recommended: use Homebrew
brew install python3

# Verify
python3 --version
pip3 --version
```

> ⚠️ **Warning:** macOS ships with a system Python. Never modify or use the system Python. Always use your own installation via Homebrew.

#### Linux — Debian / Ubuntu

```bash
sudo apt update
sudo apt install python3 python3-pip -y

# Verify
python3 --version
pip3 --version
```

> ⚡ **Linux Note:**  
> On most distros, `python` may point to Python 2. Always use `python3`. Or add a permanent alias in `~/.bashrc`:
> ```bash
> alias python=python3
> alias pip=pip3
> ```

---

### 1.7 Choosing an Editor / IDE

| Tool | Type | Best For |
|---|---|---|
| **VS Code** | Editor + Extensions | All-around — recommended for most |
| **PyCharm** | Full IDE | Large projects, professional use |
| **Jupyter Notebook** | Notebook | Data science, exploration, teaching |
| **Thonny** | Simple IDE | Absolute beginners |
| **Vim / Neovim** | Terminal Editor | Advanced users |
| **IDLE** | Built-in Editor | Quick testing — comes with Python |

> ✅ **Recommendation:**  
> Start with **VS Code** + the **Python extension by Microsoft**. It provides syntax highlighting, IntelliSense autocomplete, integrated debugger, and a terminal — everything needed without overwhelming complexity.

---

### 1.8 The Python REPL — Interactive Shell

**REPL** stands for **Read → Evaluate → Print → Loop**.  
It is an interactive Python session where every line you type is executed immediately.

```bash
# Launch the REPL
python3
```

```
Python 3.12.0 (main, ...)
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

```python
>>> 2 + 3
5

>>> 10 / 3
3.3333333333333335

>>> "Python" * 3
'PythonPythonPython'

>>> name = "Alice"
>>> print(f"Hello, {name}!")
Hello, Alice!

>>> type(42)
<class 'int'>

>>> type("hello")
<class 'str'>

>>> exit()
```

> ⚡ **When to Use the REPL:**
> - Testing a single expression or function quickly
> - Exploring an unfamiliar library interactively
> - Checking what a method returns before writing a full script
> - Quick arithmetic or string manipulation

> ⚠️ **Limitation:**  
> Code typed in the REPL is **not saved**. Once you exit, everything is lost. For anything beyond a few lines, write a `.py` file.

---

### 1.9 Writing and Running Your First Python Script

**File:** `hello.py`

```python
# hello.py
# The hash symbol begins a comment — Python ignores everything after it on that line

# print() is a built-in function that outputs text to the terminal
print("Hello, World!")
print("Python version 3 is running.")

# You can print multiple values separated by commas
# print() automatically inserts a space between them
print("The result of 5 + 3 is:", 5 + 3)

# Variables store data — no type declaration needed
language = "Python"
year = 1991
print(language, "was created in", year)
```

**Run from terminal:**
```bash
python3 hello.py
```

**Output:**
```
Hello, World!
Python version 3 is running.
The result of 5 + 3 is: 8
Python was created in 1991
```

---

**Line-by-line breakdown:**

| Code | Element | What it does |
|---|---|---|
| `# comment text` | Comment | Ignored by Python; explains the code for humans |
| `print(...)` | Built-in function | Sends output to the terminal (stdout) |
| `"Hello, World!"` | String literal | A piece of text enclosed in quotes |
| `5 + 3` | Expression | Evaluated to `8` before being passed to `print` |
| `language = "Python"` | Assignment statement | Creates a variable and stores a value in it |
| `print(a, b, c)` | Multi-argument print | Prints each argument with a space separator |

---

### 1.10 Python Code Style — PEP 8 (Foundation)

**PEP 8** is the official Python style guide. It defines how Python code should look to maximize readability and consistency across codebases.

**PEP = Python Enhancement Proposal** — numbered documents that define language standards, new features, and community conventions.

Following PEP 8 is an industry expectation for professional Python code.

---

#### Naming Conventions

```python
# Variables and functions → snake_case
user_name = "Alice"
total_price = 250.75

def calculate_total(price, tax):
    return price + tax


# Constants → ALL_CAPS_SNAKE_CASE
MAX_RETRIES = 5
PI = 3.14159
DATABASE_URL = "localhost:5432"


# Classes → PascalCase (also called UpperCamelCase)
class BankAccount:
    pass

class UserProfileManager:
    pass


# Private attributes (internal use) → single underscore prefix
_internal_counter = 0

# Name-mangled attributes (class-level private) → double underscore prefix
__secret_key = "abc123"
```

---

#### Indentation Rules

```python
# ✅ CORRECT — exactly 4 spaces per indentation level
def greet(name):
    if name:
        print("Hello,", name)
    else:
        print("Hello, stranger")


# ✗ WRONG — mixing 2 and 8 spaces → IndentationError
def greet(name):
  if name:          # 2 spaces
        print(name) # 8 spaces → Python raises IndentationError
```

> ⚡ **Critical Rule:**  
> Python uses **indentation (whitespace) to define code blocks** — not curly braces `{}` like C, Java, or JavaScript.  
> Incorrect indentation does not just look bad — it **changes behavior or crashes the program**.

> ⚠️ **Most Common Beginner Error:**  
> Mixing **tabs and spaces**. Even if it looks correct visually, Python 3 raises a `TabError` at runtime. Configure your editor to convert the Tab key into 4 spaces automatically.

---

#### Spacing Around Operators and Commas

```python
# ✅ Correct — single space around operators
x = 10
result = x * 2 + 5
is_valid = x > 0 and x < 100

# ✗ Wrong — no spaces (hard to read)
x=10
result=x*2+5

# ✅ Correct — space after each comma
def add(a, b, c):
    return a + b + c

my_list = [1, 2, 3, 4]

# ✗ Wrong — no space after comma
def add(a,b,c):
    return a+b+c
```

---

#### Line Length and Line Continuation

```python
# PEP 8 recommends max 79 characters per line
# For long expressions, use parentheses for implicit continuation:

# ✅ Correct — natural line break inside parentheses
total = (
    first_value
    + second_value
    + third_value
)

# ✅ Long function call — broken correctly
result = some_long_function_name(
    argument_one,
    argument_two,
    argument_three,
)

# ✗ Avoid — backslash continuation (fragile, less readable)
total = first_value + \
        second_value
```

---

#### Writing Comments Correctly

```python
# ✅ Good comment — explains WHY the code does this, not WHAT it does
# Multiply by 1000 to convert from seconds to milliseconds
duration_ms = duration_s * 1000

# ✗ Bad comment — just restates the code in words (adds no value)
# Set duration_ms to duration_s times 1000
duration_ms = duration_s * 1000


# Inline comments must be separated by at least 2 spaces
x = x + 1  # Compensate for the border offset


# Docstrings document functions, classes, and modules
def calculate_discount(price, rate):
    """
    Calculate the discounted price after applying a rate.

    Args:
        price (float): Original price in dollars.
        rate (float): Discount rate as a decimal (e.g., 0.2 for 20%).

    Returns:
        float: Final price after applying the discount.

    Example:
        >>> calculate_discount(100, 0.2)
        80.0
    """
    return price * (1 - rate)
```

> ⚡ **Comments vs Docstrings:**  
> `#` comments are for developers reading the source code.  
> `"""docstrings"""` are for users of a function or class — they are readable at runtime via `help()` and by documentation tools.

---

### 1.11 Built-in Help — `help()` and `dir()`

Python has built-in tools for exploring documentation without leaving the terminal.

```python
# help() shows full documentation for any function, class, or module
help(print)
help(str)
help(list)

# dir() lists all attributes and methods of any object
dir(str)       # All string methods
dir([])        # All list methods
dir(42)        # All integer methods

# Practical usage — explore what a string can do
print(dir("hello"))
# Output includes: 'capitalize', 'find', 'format', 'join',
#                  'lower', 'replace', 'split', 'strip', 'upper', ...

# Get documentation for a specific method
help(str.split)
help(list.append)
```

> ✅ **Professional Habit:**  
> Before searching online, try `help()` and `dir()` in the REPL. It works offline, is always accurate for your Python version, and trains you to read official documentation directly.

---

### 1.12 Common Errors — Chapter 1 Context

Understanding errors from the very beginning builds the habit of reading error messages carefully rather than panicking.

#### SyntaxError — Invalid code structure

```python
print("Hello"
# SyntaxError: '(' was never closed

if x > 5
    print(x)
# SyntaxError: expected ':'
```

#### IndentationError — Wrong indentation

```python
def greet():
print("Hello")
# IndentationError: expected an indented block after function definition
```

#### NameError — Using undefined variable

```python
print(message)
# NameError: name 'message' is not defined
```

#### TypeError — Incompatible types

```python
print("My age is: " + 25)
# TypeError: can only concatenate str (not "int") to str
```

---

#### How to Read a Traceback

```
Traceback (most recent call last):
  File "hello.py", line 3, in <module>
    print("My age is: " + 25)
          ~~~~~~~~~~~~~~~~~~~
TypeError: can only concatenate str (not "int") to str
```

| Part of Traceback | What it Tells You |
|---|---|
| `Traceback (most recent call last)` | The call stack — functions that were running |
| `File "hello.py", line 3` | Exact file name and line number |
| `print("My age is: " + 25)` | The exact code that failed |
| `TypeError: ...` | Error type and a human-readable explanation |

> ⚡ **Golden Rule for Reading Errors:**  
> Always read the **last line first** — it tells you the error type and message.  
> Then trace upward through the Traceback to find the line that caused it.

---

### 1.13 Chapter 1 — Complete Summary & Revision Table

| Concept | Key Point |
|---|---|
| **Python** | High-level, interpreted, dynamically typed, general-purpose language |
| **Creator** | Guido van Rossum — first released 1991 |
| **Python 2 vs 3** | Python 2 is dead (EOL Jan 2020) — always use Python 3 |
| **Execution Flow** | Source → Lexer → Parser → Bytecode → PVM → Output |
| **`__pycache__`** | Stores compiled `.pyc` bytecode — never edit manually |
| **CPython** | Standard interpreter written in C — what you use by default |
| **REPL** | Interactive shell for quick testing — not for saving code |
| **`print()`** | Built-in function that outputs to terminal (stdout) |
| **PEP 8** | Official style guide — snake_case, 4 spaces, 79-char limit |
| **Indentation** | Defines code blocks — not optional — must be consistent |
| **`help()`** | Shows documentation for any function or object |
| **`dir()`** | Lists all attributes and methods of any object |
| **SyntaxError** | Code structure is invalid — caught at parse time |
| **IndentationError** | Wrong or inconsistent indentation |
| **NameError** | Variable used before being defined |
| **TypeError** | Operation attempted on incompatible types |

---

> ✅ **Chapter 1 — Complete.**  
> Type **`next`** to continue to **Chapter 2: Variables, Data Types & the Type System.**
