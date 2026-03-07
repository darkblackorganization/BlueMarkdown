# PHP Conditionals

<style>
.code-card{
position:relative;
background:#1e293b;
padding:22px;
border-radius:14px;
margin:30px 0;
box-shadow:0 10px 25px rgba(0,0,0,0.3);
}

.code-label{
position:absolute;
top:-12px;
right:15px;

background:linear-gradient(90deg,#7c3aed,#a855f7);
color:white;

padding:6px 14px;
font-size:12px;
border-radius:8px;
font-weight:500;
}

pre{
background:#0f172a;
padding:15px;
border-radius:10px;
overflow:auto;
color:#e2e8f0;
}
</style>

---

<div class="code-card">

<span class="code-label">If elseif else</span>

```php
$a = 10;
$b = 20;

if ($a > $b) {
    echo "a is bigger than b";
} elseif ($a == $b) {
    echo "a is equal to b";
} else {
    echo "a is smaller than b";
}
```

</div>

---

<div class="code-card">

<span class="code-label">Switch</span>

```php
$x = 0;

switch ($x) {
    case '0':
        print "it's zero";
        break;

    case 'two':
    case 'three':
        // do something
        break;

    default:
        // do something
}
```

</div>

---

<div class="code-card">

<span class="code-label">Ternary operator</span>

```php
print (false ? 'Not' : 'Does');

$x = false;
print($x ?: 'Does');

$a = null;
$b = 'Does print';

echo $a ?? 'a is unset';
echo $b ?? 'b is unset';
```

</div>    *   `"-".join(list_of_strings)`
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
