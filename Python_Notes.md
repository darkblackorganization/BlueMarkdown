# Python — Complete Study Notes

---

## Table of Contents

1. [Introduction to Python](#1-introduction-to-python)
2. *(More chapters will be added progressively...)*

---

## 1. Introduction to Python

### 1.1 What is Python?

Python is a **high-level**, **interpreted**, **general-purpose** programming language created by **Guido van Rossum** and first released in **1991**. It is designed with a philosophy that emphasizes **code readability**, **simplicity**, and **expressiveness** — allowing developers to write clean, logical code for both small scripts and large-scale systems.

> ⚡ **Important Definition:**  
> Python is an **interpreted language**, meaning code is executed **line by line** at runtime by an interpreter, rather than being compiled into machine code beforehand.

---

### 1.2 Key Characteristics of Python

| Feature | Description |
|---|---|
| **High-level** | Abstracts away hardware/memory details |
| **Interpreted** | Executed directly without a separate compile step |
| **Dynamically Typed** | Variable types are determined at runtime |
| **Garbage Collected** | Memory is managed automatically |
| **Multi-paradigm** | Supports OOP, functional, and procedural programming |
| **Cross-platform** | Runs on Windows, macOS, Linux without modification |

---

### 1.3 Why Python? — Real-World Relevance

Python is one of the **most widely used programming languages** in the world today. Here is why professionals and beginners choose it:

- 🌐 **Web Development** — Django, Flask, FastAPI
- 🤖 **Artificial Intelligence & Machine Learning** — TensorFlow, PyTorch, scikit-learn
- 📊 **Data Science & Analytics** — Pandas, NumPy, Matplotlib
- 🔒 **Cybersecurity & Ethical Hacking** — scripting, penetration testing tools
- ⚙️ **Automation & Scripting** — file management, task automation, web scraping
- ☁️ **Cloud & DevOps** — AWS Lambda, Ansible, infrastructure scripting
- 🎮 **Game Development** — Pygame

> 💡 **Key Insight:**  
> Python's biggest strength is its **ecosystem** — thousands of open-source libraries mean you rarely need to build things from scratch.

---

### 1.4 Python Versions — Python 2 vs Python 3

> ⚠️ **Common Mistake:**  
> Many beginners still encounter Python 2 tutorials online. **Python 2 reached End of Life on January 1, 2020** and should **not** be used for any new project.

| | Python 2 | Python 3 |
|---|---|---|
| **Status** | ❌ Discontinued | ✅ Actively maintained |
| **Print** | `print "Hello"` | `print("Hello")` |
| **Division** | `5 / 2 = 2` (integer) | `5 / 2 = 2.5` (float) |
| **Unicode** | ASCII by default | Unicode (UTF-8) by default |
| **`input()`** | Evaluates input as code | Always returns a string |

> ⚡ **Rule:** Always use **Python 3.x** (currently Python 3.12+). All notes here use Python 3.

---

### 1.5 How Python Works — Under the Hood

Understanding the execution model helps avoid confusion later.

```
Your Code (.py file)
        │
        ▼
  Python Interpreter
        │
        ▼
  Bytecode (.pyc file)   ← stored in __pycache__/
        │
        ▼
  Python Virtual Machine (PVM)
        │
        ▼
    Output / Result
```

**Step-by-step breakdown:**

1. You write Python source code in a `.py` file.
2. The interpreter **lexes and parses** the code, checking for syntax errors.
3. The code is compiled to **bytecode** — a lower-level, platform-independent representation.
4. The **Python Virtual Machine (PVM)** executes the bytecode line by line.
5. Results are produced (output, file changes, network requests, etc.).

> 💡 **Key Insight:**  
> The `.pyc` files inside `__pycache__/` are **auto-generated** bytecode caches. Python uses them to skip re-compilation on subsequent runs if the source hasn't changed. You should **never edit them manually**.

---

### 1.6 Installing Python

#### On Windows
1. Visit [https://www.python.org/downloads/](https://www.python.org/downloads/)
2. Download the latest Python 3.x installer.
3. ✅ **Check "Add Python to PATH"** during installation — this is critical.
4. Verify via Command Prompt:
```bash
python --version
```

#### On macOS
```bash
# Using Homebrew (recommended)
brew install python3

# Verify
python3 --version
```

#### On Linux (Debian/Ubuntu)
```bash
sudo apt update
sudo apt install python3 python3-pip

# Verify
python3 --version
```

> ⚠️ **Common Mistake:**  
> On macOS and Linux, `python` may point to Python 2 (if installed). Always use `python3` explicitly on these systems unless you've configured an alias.

---

### 1.7 Python Interactive Shell (REPL)

Python comes with a **REPL** — Read, Evaluate, Print, Loop — an interactive shell for testing code instantly without creating a file.

```bash
# Launch REPL
python3
```

```python
>>> 2 + 3
5
>>> print("Hello, World!")
Hello, World!
>>> name = "Python"
>>> name
'Python'
>>> exit()
```

> 💡 **Key Insight:**  
> The REPL is an excellent tool for **quick experimentation**, testing a function's behavior, or exploring a library — experienced developers use it constantly.

---

### 1.8 Your First Python Program

**File:** `hello.py`

```python
# This is a comment — Python ignores it
print("Hello, World!")
```

**Run it:**
```bash
python3 hello.py
```

**Output:**
```
Hello, World!
```

**Breaking it down:**

| Part | Meaning |
|---|---|
| `#` | Marks a **comment** — ignored by the interpreter |
| `print()` | A built-in **function** that outputs text to the terminal |
| `"Hello, World!"` | A **string literal** — text enclosed in quotes |

---

### 1.9 Python Code Style — PEP 8 (Introduction)

Python has an official style guide called **PEP 8** (Python Enhancement Proposal 8). Following it makes your code readable and professional.

**Core rules to know from the start:**

```python
# ✅ Good — clear, readable
user_name = "Alice"
total_price = 100 + 25

# ❌ Bad — hard to read
UserName="Alice"
totalprice=100+25
```

| Rule | Standard |
|---|---|
| Indentation | **4 spaces** (never tabs) |
| Variable names | `snake_case` |
| Class names | `PascalCase` |
| Constants | `ALL_CAPS` |
| Max line length | **79 characters** |
| Blank lines | 2 between top-level functions/classes |

> ⚡ **Important:**  
> Python uses **indentation** (whitespace) to define code blocks — unlike most languages that use `{}` braces. **Incorrect indentation causes `IndentationError`** — one of the most common beginner mistakes.

> ⚠️ **Common Mistake:**
> Mixing tabs and spaces for indentation. Always configure your editor to **convert tabs to 4 spaces** automatically.

---

### 1.10 Summary — Chapter 1

| Concept | Key Takeaway |
|---|---|
| What is Python | High-level, interpreted, general-purpose language |
| Python 2 vs 3 | Always use Python 3 — Python 2 is dead |
| How Python runs | Source → Bytecode → PVM → Output |
| REPL | Interactive shell for instant testing |
| PEP 8 | Official style guide — follow it from day one |
| Indentation | Not optional — it defines code structure |

---

> ✅ **Chapter 1 Complete.**  
> Type **`next`** to continue to **Chapter 2: Variables, Data Types & Type System**.
