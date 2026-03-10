
<style>
table, th, td { border: 1px solid #ccc; border-collapse: collapse; padding: 6px 12px; }
th { background-color: #f5f5f5; }
code { background-color: #f0f0f0; padding: 2px 6px; border-radius: 4px; font-size: 0.95em; }
pre { background-color: #f8f8f8; padding: 12px; border-radius: 6px; overflow-x: auto; }
blockquote { border-left: 4px solid #6319bf; padding-left: 10px; color: #555; margin-left: 0; font-style: italic; }
</style>

---

### 🔹 Headers

**ATX Style (using `#`)**

```markdown
# H1 - Largest
## H2
### H3
#### H4
##### H5
###### H6 - Smallest
```

**Setext Style (underline)**

```markdown
Header 1
========

Header 2
--------
```

> Tip: ATX style is preferred for modern Markdown; Setext is mostly for H1/H2.

---

### 🔹 Emphasis

```markdown
*italic* or _italic_
**bold** or __bold__
~~strikethrough~~
`inline code`
```

**Nested emphasis**

```markdown
**This is _bold and italic_ text**
```

---

### 🔹 Blockquotes

```markdown
> This is a blockquote
>
> > Nested blockquote
```

> Tip: You can include **lists, code blocks, or images** inside blockquotes.

---

### 🔹 Lists

**Unordered lists**

```markdown
- Item 1
- Item 2
  - Subitem 2a
  - Subitem 2b
+ Item 3
* Item 4
```

**Checkboxes (task lists)**

```markdown
- [ ] Task not done
- [x] Task done
```

**Ordered lists**

```markdown
1. First
2. Second
   1. Subitem 2a
   2. Subitem 2b
```

---

### 🔹 Links

```markdown
[Google](https://google.com)

[Google][google-ref]
[google-ref]: https://google.com "Google Homepage"

<https://google.com>
```

**Links with title/tooltips**

```markdown
[Hover me](https://example.com "This is a tooltip")
```

---

### 🔹 Images

```markdown
![Alt text](image_url "Optional Title")
```

**Images as links**

```markdown
[![Alt](image_url)](https://example.com)
```

**Reference style**

```markdown
![Logo][logo]

[logo]: /images/logo.png "Site Logo"
```

---

### 🔹 Code

**Inline code**

```markdown
Use `console.log()` to print output
```

**Code blocks**

```javascript
console.log('Hello World!');
```

**Alternate syntax**

```python
print("Hello World")
```

**Indented code (4 spaces)**

```markdown
    Indented code block
```

**Escaped backticks**

````markdown
```bash
echo "Nested code"
```
````

---

### 🔹 Horizontal Lines

```markdown
---
***
___
```

---

### 🔹 Tables

**Simple table**

```markdown
| Left | Center | Right |
| :--- | :----: | ----: |
| A    | B      | C     |
| 10   | 20     | 30    |
```

**Without pipes for simple notes**

```markdown
Left | Center | Right
:--- | :---:  | ---:
A    | B      | C
```

> Tip: Use [tableconvert.com](https://tableconvert.com/) for visual table building.

---

### 🔹 Advanced Markdown Tips

* **Footnotes**

```markdown
This is a footnote reference[^1].

[^1]: This is the footnote.
```

* **Emoji support** (GitHub/Markdown flavor)

```markdown
:smile: :rocket: :tada:
```

* **HTML inside Markdown**

```html
<span style="color:#6319bf">Colored text</span>
```

* **Highlight text** (GitHub style)

```markdown
==Highlighted text==
```

* **Task list progress**

```markdown
- [x] Step 1 complete
- [ ] Step 2 pending
```

---

### 🔹 Escaping Characters

| Character | Escape Syntax | Example             |
| --------- | ------------- | ------------------- |
| `\`       | `\\`          | `\\` → \            |
| `*`       | `\*`          | `\*text\*` → *text* |
| `_`       | `\_`          | `\_text\_` → *text* |
| `{}`      | `\{\}`        | `\{1,2\}` → {1,2}   |
| `[]`      | `\[\]`        | `\[` → [            |
| `()`      | `\(\)`        | `\(` → (            |
| `#`       | `\#`          | `\# Heading`        |
| `+`       | `\+`          | `\+ Item`           |
| `-`       | `\-`          | `\- Item`           |
| `.`       | `\.`          | `1\.` → 1.          |
| `!`       | `\!`          | `\!important`       |

---
