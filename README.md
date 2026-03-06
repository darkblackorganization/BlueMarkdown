# Python Cheatsheet

A quick reference guide for common Python syntax and commands.

---

## Variables

```python
x = 10
name = "Bittu"
price = 99.99
```

---

## Data Types

| Type       | Example             |
| ---------- | ------------------- |
| Integer    | `10`                |
| Float      | `3.14`              |
| String     | `"hello"`           |
| Boolean    | `True` / `False`    |
| List       | `[1, 2, 3]`         |
| Dictionary | `{"name": "Bittu"}` |

---

## If Statement

```python
x = 5

if x > 3:
    print("x is greater than 3")
```

---

## Loops

### For Loop

```python
for i in range(5):
    print(i)
```

### While Loop

```python
count = 0

while count < 5:
    print(count)
    count += 1
```

---

## Functions

```python
def greet(name):
    return "Hello " + name

print(greet("Bittu"))
```

---

## Lists

```python
numbers = [1, 2, 3, 4]

numbers.append(5)
numbers.remove(2)

print(numbers)
```

---

## Dictionaries

```python
user = {
    "name": "Bittu",
    "age": 20,
    "role": "developer"
}

print(user["name"])
```

---

## File Reading

```python
with open("file.txt", "r") as f:
    data = f.read()
```

---

## Virtual Environment

```bash
python -m venv env
source env/bin/activate
```

---

## Install Package

```bash
pip install requests
```

---

## Quick Links

* Official Python Docs
  https://docs.python.org

* Python Package Index
  https://pypi.org

---

## Tips

* Use virtual environments for projects
* Write clean and readable code
* Use `pip freeze` to export dependencies

---

Happy Coding 🚀
# Cheat-sheet
