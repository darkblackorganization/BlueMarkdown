*   **Basic Syntax & Comments**
    *   `# This is a single-line comment`
    *   Variables: `x = 10`, `name = "Python"` (dynamic typing)
*   **Data Types**
    *   **Numbers**: `int` (10), `float` (3.14), `complex`
    *   **Strings**: `"hello"`, `'world'`, multi-line `"""multiple lines"""`
    *   **Lists**: Ordered, mutable collection `[1, 2, 'a']`
    *   **Tuples**: Ordered, immutable collection `(1, 2, 'a')`
    *   **Dictionaries**: Unordered, mutable key-value pairs `{'name': 'Alice', 'age': 30}`
    *   **Sets**: Unordered collection of unique elements `{1, 2, 3}`
*   **Operators**
    *   **Arithmetic**: `+`, `-`, `*`, `/`, `%` (modulo), `**` (exponent), `//` (floor division)
    *   **Comparison**: `==`, `!=`, `<`, `>`, `<=`, `>=`
    *   **Logical**: `and`, `or`, `not`
    *   **Assignment**: `=`, `+=`, `-=`, `*=` etc.
*   **Control Flow**
    *   **If/Elif/Else**:
        ```python
        if condition1:
            # code
        elif condition2:
            # code
        else:
            # code
        ```
    *   **For Loop** (iteration over sequences):
        ```python
        for item in [1, 2, 3]:
            print(item)
        for i in range(5): # 0, 1, 2, 3, 4
            print(i)
        ```
    *   **While Loop**:
        ```python
        count = 0
        while count < 3:
            print(count)
            count += 1
        ```
*   **Functions**
    *   **Definition**:
        ```python
        def greet(name):
            return f"Hello, {name}!"
        ```
    *   **Calling**: `message = greet("Bob")`
*   **Input/Output**
    *   **Output**: `print("Hello, World!")`, `print(f"Value is {var}")`
    *   **Input**: `name = input("Enter your name: ")` (returns string)
*   **Common String Methods**
    *   `str.lower()`, `str.upper()`
    *   `str.strip()` (removes whitespace)
    *   `str.split(',')` (splits into list)
    *   `"-".join(list_of_strings)`
    *   `str.replace('old', 'new')`
    *   `str.startswith('prefix')`, `str.endswith('suffix')`
*   **Common List Methods**
    *   `list.append(item)` (add to end)
    *   `list.insert(index, item)`
    *   `list.remove(item)` (first occurrence)
    *   `list.pop(index)` (remove by index, returns item)
    *   `list.sort()` or `sorted(list)`
    *   `list.count(item)`
    *   `len(list)` (length function)
*   **Importing Modules**
    *   `import math`
    *   `from datetime import date`
    *   `result = math.sqrt(16)`
    *   `today = date.today()`
