## Introduction

**PHP** (Hypertext Preprocessor) is a widely-used, open-source, server-side scripting language designed specifically for web development. Created by **Rasmus Lerdorf** in **1994**, PHP code is embedded directly into HTML and runs on the server before the page is sent to the browser. PHP powers over **75% of all websites** with a server-side language, including WordPress, Facebook (early days), Wikipedia, and countless web apps. PHP 8.x (released 2020) brought major improvements including JIT compilation, named arguments, union types, match expressions, and fibers. PHP is excellent for **web backends, APIs, CMS platforms, and database-driven applications**.

## Basic Syntax

**Definition:** PHP code is embedded in HTML using `<?php ?>` tags — every statement ends with a semicolon.

### PHP Tags
**Definition:** PHP code starts with `<?php` and ends with `?>` — can be embedded anywhere in an HTML file.
```php
<?php
// PHP code here
echo "Hello, World!";
?>

<!-- PHP inside HTML -->
<!DOCTYPE html>
<html>
<body>
    <h1><?php echo "Hello!"; ?></h1>
    <p><?= "Short echo tag" ?></p>  <!-- <?= is shorthand for <?php echo -->
</body>
</html>

<?php
// If file is pure PHP — omit the closing ?> to prevent whitespace issues
echo "Pure PHP file";
```

### Output
**Definition:** Different ways to output text and variables to the browser.
```php
echo "Hello, World!";          // Output — can take multiple comma-separated values
echo "Hello", " ", "World";    // Multiple arguments with echo

print "Hello!";                // Output — returns 1, only one argument
print("Hello!");

var_dump($var);                 // Debug — type + value
print_r($array);               // Human-readable — good for arrays
var_export($var);               // Output as valid PHP code

printf("Name: %s, Age: %d\n", $name, $age);  // Formatted output
$str = sprintf("Value: %.2f", 3.14);          // Format to string
```

### Comments
**Definition:** Three comment styles — single-line and multi-line.
```php
// Single-line comment

# Also single-line (shell style)

/*
 * Multi-line comment
 * Spans multiple lines
 */

/**
 * PHPDoc comment — for documentation generation
 * @param string $name The user's name
 * @param int    $age  The user's age
 * @return string A greeting
 */
function greet(string $name, int $age): string {
    return "Hello, $name!";
}
```

---

## Variables

**Definition:** Variables start with `$` — no type declaration needed, PHP is dynamically typed.

### Declare & Assign
**Definition:** Create a variable by assigning a value — PHP infers the type automatically.
```php
$name    = "Dark";           // String
$age     = 25;               // Integer
$price   = 9.99;             // Float
$isAdmin = true;             // Boolean
$nothing = null;             // Null

// Multiple assignment
$a = $b = $c = 0;           // All set to 0

// Assign by reference
$original = "Hello";
$copy      = $original;      // $copy is a separate copy
$ref       = &$original;     // $ref is a reference — changes affect $original
```

### Variable Variables
**Definition:** Use a variable's value as another variable's name — dynamic variable naming.
```php
$varName  = "city";
$$varName = "Mumbai";        // Creates $city = "Mumbai"
echo $city;                  // Mumbai
echo $$varName;              // Mumbai
```

### Variable Scope
**Definition:** PHP variables are local by default — use `global` or `$GLOBALS` to access outer scope.
```php
$globalVar = "I am global";

function myFunc() {
    // $globalVar not accessible here — PHP scope is strict
    global $globalVar;           // Declare as global to access
    echo $globalVar;

    // Or use $GLOBALS superglobal
    echo $GLOBALS['globalVar'];

    $localVar = "I am local";    // Only inside this function
    static $counter = 0;         // Static — persists between calls
    $counter++;
    echo $counter;
}

myFunc();    // 1
myFunc();    // 2
myFunc();    // 3 — static persists
```

### Constants
**Definition:** Constants hold a fixed value — cannot be changed after definition.
```php
define('MAX_SIZE', 100);           // Old way
define('APP_NAME', 'MyApp');

const DB_HOST = 'localhost';       // Modern way (PHP 5.3+)
const DB_PORT = 5432;

// Class constants
class Config {
    const VERSION = '1.0.0';
    const MAX_USERS = 1000;
}

echo Config::VERSION;              // 1.0.0
echo MAX_SIZE;                     // 100
```

---

## Data Types

**Definition:** PHP has 8 primitive types — PHP converts between them automatically (type juggling).

### Scalar Types
**Definition:** The four basic types that hold single values.
```php
// Integer — whole numbers
$i = 42;
$i = -17;
$i = 0b1010;   // Binary  → 10
$i = 0o17;     // Octal   → 15 (PHP 8.1+)
$i = 0x1A;     // Hex     → 26
$i = 1_000_000; // Underscores for readability (PHP 7.4+)

// Float (double)
$f = 3.14;
$f = 1.2e3;    // 1200.0
$f = 7E-10;

// String
$s = "Double quoted — $name interpolated";
$s = 'Single quoted — $name literal';
$s = <<<EOT
Heredoc string — variables $name interpolated
Spans multiple lines
EOT;

$s = <<<'EOT'
Nowdoc — like single quotes, no interpolation
Spans multiple lines
EOT;

// Boolean
$b = true;
$b = false;
// Falsy values: false, 0, 0.0, "0", "", null, []
```

### Compound Types
**Definition:** Types that hold multiple values or complex structures.
```php
$arr = [1, 2, 3];                        // Array
$obj = new stdClass();                   // Object
$obj->name = "Dark";

$fn  = function($x) { return $x * 2; }; // Callable / closure
```

### Special Types
**Definition:** Null and resource types.
```php
$nothing = null;                         // Null
$file    = fopen("file.txt", "r");       // Resource
```

### Check Types
**Definition:** Functions to inspect and verify the type of a variable.
```php
is_int($var)         // Is integer?
is_float($var)       // Is float?
is_string($var)      // Is string?
is_bool($var)        // Is boolean?
is_null($var)        // Is null?
is_array($var)       // Is array?
is_object($var)      // Is object?
is_numeric($var)     // Is numeric (int or numeric string)?
is_callable($var)    // Is callable?

gettype($var)        // Returns type name as string
get_class($obj)      // Returns class name

isset($var)          // Is variable set and not null?
empty($var)          // Is variable empty (falsy)?
isset($arr['key'])   // Check array key exists and not null
array_key_exists('key', $arr)  // Check array key exists (even if null)
```

---

## Type Juggling & Casting

**Definition:** PHP automatically converts types as needed — explicit casting forces a specific type.

### Explicit Casting
**Definition:** Force a value to a specific type using cast operators.
```php
$str = "42";
$num = "3.14";
$bool = "1";

(int)    $str      // 42
(float)  $num      // 3.14
(string) 42        // "42"
(bool)   $str      // true
(array)  "hello"   // ["hello"]
(object) ['a'=>1]  // stdClass with property a = 1

// intval(), floatval(), strval() — function equivalents
intval("42px")     // 42 — parses until non-numeric
floatval("3.14em") // 3.14
strval(42)         // "42"
boolval(0)         // false
```

### Type Comparison
**Definition:** Loose vs strict comparison — always use `===` to avoid type juggling surprises.
```php
// Loose comparison (==) — type juggling
0    == "foo"    // true  (string converts to 0)
0    == ""       // true
0    == "0"      // true
"1"  == "01"     // true
100  == "1e2"    // true
null == false    // true
null == 0        // true

// Strict comparison (===) — type + value
0    === "0"     // false — different types
null === false   // false
1    === true    // false

// Always prefer === in PHP!
```

---

## String Operations

**Definition:** PHP has a rich string library — strings are byte sequences with many manipulation functions.

### Create & Access
**Definition:** Create strings with different quote types — access characters by index.
```php
$s = "Hello, World!";

strlen($s)                // 13 — character count
$s[0]                     // "H" — access by index
$s[-1]                    // "!" — negative index (PHP 7.1+)
substr($s, 7, 5)          // "World" — from index 7, length 5
substr($s, 7)             // "World!" — from index 7 to end
substr($s, -6)            // "World!" — last 6 characters
```

### Search & Check
**Definition:** Find substrings and test string content.
```php
strpos($s, "World")            // 7 — first position (false if not found)
strrpos($s, "l")               // 10 — last position
str_contains($s, "World")      // true (PHP 8.0+)
str_starts_with($s, "Hello")   // true (PHP 8.0+)
str_ends_with($s, "!")         // true (PHP 8.0+)
substr_count($s, "l")          // 3 — how many times "l" appears
```

### Transform
**Definition:** Modify and clean string content.
```php
strtoupper($s)                 // "HELLO, WORLD!"
strtolower($s)                 // "hello, world!"
ucfirst("hello world")         // "Hello world"
ucwords("hello world")         // "Hello World"
trim("  hello  ")              // "hello"
ltrim("  hello  ")             // "hello  "
rtrim("  hello  ")             // "  hello"
str_pad("42", 5, "0", STR_PAD_LEFT)  // "00042"
str_repeat("ab", 3)            // "ababab"
wordwrap($text, 80, "\n", true) // Wrap at 80 chars
```

### Replace & Extract
**Definition:** Substitute and pull out parts of strings.
```php
str_replace("World", "PHP", $s)         // "Hello, PHP!"
str_ireplace("world", "PHP", $s)        // Case-insensitive replace
str_replace(["a","e"], ["@","3"], $s)   // Multiple replacements
preg_replace('/\d+/', 'NUM', $s)        // Regex replace

explode(",", "a,b,c")           // ["a", "b", "c"]
explode(",", "a,b,c", 2)        // ["a", "b,c"] — max 2 parts
implode(", ", ["a","b","c"])    // "a, b, c"
join(" | ", $arr)               // Alias for implode

sprintf("Name: %s, Age: %d", "Dark", 25)  // Formatted string
number_format(1234567.891, 2, '.', ',')   // "1,234,567.89"
```

### String Interpolation
**Definition:** Variables inside double-quoted strings are replaced with their values.
```php
$name = "Dark";
$age  = 25;
$arr  = ['key' => 'value'];

echo "Hello, $name!";                    // Simple variable
echo "Hello, {$name}!";                  // With braces (clearer)
echo "Age next year: {$age + 1}";        // Won't work — no expressions in strings
echo "Array: {$arr['key']}";             // Array access in string
echo "Obj: {$obj->property}";            // Object property in string

// For expressions, use concatenation or sprintf
echo "Age next year: " . ($age + 1);
echo sprintf("Age next year: %d", $age + 1);
```

---

## Numbers & Math

**Definition:** PHP supports integers, floats, and a full Math library — watch out for floating-point precision.

### Integer Functions
**Definition:** Work with whole numbers.
```php
abs(-5)           // 5 — absolute value
PHP_INT_MAX       // 9223372036854775807 — max integer
PHP_INT_MIN       // Minimum integer value
PHP_INT_SIZE      // 8 — bytes (on 64-bit)
intdiv(10, 3)     // 3 — integer division (PHP 7+)
10 % 3            // 1 — modulo operator
```

### Float Functions
**Definition:** Work with decimal numbers.
```php
round(3.14159, 2)     // 3.14 — round to 2 decimal places
ceil(4.1)             // 5    — round up
floor(4.9)            // 4    — round down
fmod(10.5, 3.2)       // 0.9  — float modulo
PHP_FLOAT_MAX         // Maximum float
PHP_FLOAT_EPSILON     // Smallest float difference (~2.2e-16)

// Floating point comparison (never use ==)
$a = 0.1 + 0.2;
$b = 0.3;
abs($a - $b) < PHP_FLOAT_EPSILON  // Correct comparison
```

### Math Functions
**Definition:** Common math operations.
```php
pow(2, 10)        // 1024 — power
sqrt(144)         // 12   — square root
log(M_E)          // 1    — natural log
log10(1000)       // 3    — log base 10
log(8, 2)         // 3    — log base 2

M_PI              // 3.14159...
M_E               // 2.71828...

max(3, 1, 4, 1, 5)   // 5
min(3, 1, 4, 1, 5)   // 1
max([3, 1, 4])         // 5 — also accepts array

// Random
rand(1, 10)            // Random int 1 to 10
random_int(1, 10)      // Cryptographically secure random int
shuffle($arr)          // Shuffle array randomly
array_rand($arr, 2)    // Random keys from array
```

---

## Operators

**Definition:** Symbols that perform operations on values — PHP has all standard plus some unique ones.

### Arithmetic
**Definition:** Basic math operations.
```php
5 + 3     // 8
5 - 3     // 2
5 * 3     // 15
5 / 2     // 2.5  — always float if not divisible
5 % 2     // 1    — modulo
5 ** 3    // 125  — power (PHP 5.6+)
intdiv(5, 2)  // 2 — integer division
```

### Comparison
**Definition:** Compare values — note PHP's unique spaceship and strict equality operators.
```php
5 == "5"      // true  — loose: type juggling
5 === "5"     // false — strict: same type AND value
5 != "4"      // true  — loose not equal
5 !== "5"     // true  — strict not equal
5 <> "4"      // true  — alias for !=
5 > 3         // true
5 < 10        // true
5 >= 5        // true
5 <= 5        // true

// Spaceship operator (PHP 7+) — returns -1, 0, or 1
5 <=> 3       // 1  (left > right)
3 <=> 5       // -1 (left < right)
5 <=> 5       // 0  (equal)
```

### Logical
**Definition:** Combine boolean conditions.
```php
true && false   // false — AND (higher precedence)
true || false   // true  — OR  (higher precedence)
!true           // false — NOT
true and false  // false — AND (lower precedence)
true or false   // true  — OR  (lower precedence)
true xor true   // false — Exclusive OR
```

### Null Coalescing
**Definition:** PHP 7+ shorthand for checking null/undefined values safely.
```php
$name = $user['name'] ?? 'Anonymous';   // Use 'Anonymous' if key missing or null
$age  = $obj->age    ?? 0;

// Chaining
$value = $a ?? $b ?? $c ?? 'default';

// Null coalescing assignment (PHP 7.4+)
$arr['key'] ??= 'default';    // Set if null or undefined
```

### String
**Definition:** Concatenate and append strings.
```php
"Hello" . " " . "World"    // "Hello World" — concatenation
$str .= " appended";       // Append to existing string
```

---

## If Statements

**Definition:** Conditional execution — run different code based on conditions.

### Basic If / Elseif / Else
**Definition:** Execute code blocks based on true/false conditions.
```php
$age = 20;

if ($age >= 18) {
    echo "Adult";
} elseif ($age >= 13) {
    echo "Teen";
} else {
    echo "Child";
}

// Shorthand (without braces) — single statement only
if ($age >= 18) echo "Adult";
else echo "Minor";

// Ternary
$label = ($age >= 18) ? "Adult" : "Minor";

// Short ternary (Elvis operator — PHP 5.3+)
$name = $user['name'] ?: 'Anonymous';    // Use $user['name'] if truthy, else 'Anonymous'
```

### Alternative Syntax
**Definition:** Alternative if syntax for embedding in HTML templates.
```php
<?php if ($isLoggedIn): ?>
    <p>Welcome back!</p>
<?php elseif ($isGuest): ?>
    <p>Hello, Guest!</p>
<?php else: ?>
    <p>Please log in.</p>
<?php endif; ?>
```

---

## Switch & Match

**Definition:** Match a value against multiple cases — PHP 8 adds the powerful `match` expression.

### Switch Statement
**Definition:** Classic switch — uses loose comparison, requires `break` to prevent fall-through.
```php
$day = "Monday";

switch ($day) {
    case "Monday":
        echo "Start of week";
        break;
    case "Friday":
        echo "End of week";
        break;
    case "Saturday":
    case "Sunday":           // Fall-through — same code for both
        echo "Weekend!";
        break;
    default:
        echo "Midweek";
}
```

### Match Expression (PHP 8.0+)
**Definition:** Modern replacement for switch — strict comparison, returns value, no fall-through, no `break`.
```php
$status = 'active';

$label = match($status) {
    'active'   => 'Active User',
    'banned'   => 'Banned',
    'inactive' => 'Inactive',
    default    => 'Unknown',
};

// Multiple conditions per arm
$type = match(true) {
    $age < 13  => 'child',
    $age < 18  => 'teen',
    $age < 65  => 'adult',
    default    => 'senior',
};

// match throws UnhandledMatchError if no arm matches and no default
```

---

## While Loops

**Definition:** Repeat code while a condition is true.

### While Loop
**Definition:** Check condition before each iteration — may not execute at all.
```php
$count = 1;
while ($count <= 5) {
    echo $count;
    $count++;
}
// Output: 12345
```

### Do-While Loop
**Definition:** Check condition after each iteration — always executes at least once.
```php
$count = 1;
do {
    echo $count;
    $count++;
} while ($count <= 5);
// Output: 12345

// Useful for menus — run at least once
do {
    $input = readline("Enter command: ");
    process($input);
} while ($input !== 'quit');
```

---

## For Loops

**Definition:** Counter-based loops and array iteration.

### For Loop
**Definition:** Classic counter-based loop — init, condition, and increment in one line.
```php
for ($i = 0; $i < 5; $i++) {
    echo $i;    // 0 1 2 3 4
}

// Reverse
for ($i = 10; $i >= 0; $i--) {
    echo "$i ";
}

// Step
for ($i = 0; $i <= 20; $i += 5) {
    echo "$i ";    // 0 5 10 15 20
}
```

### Foreach Loop
**Definition:** Iterate over arrays and objects — the most common loop in PHP.
```php
$fruits = ["apple", "banana", "cherry"];

// Value only
foreach ($fruits as $fruit) {
    echo $fruit;
}

// Index and value
foreach ($fruits as $index => $fruit) {
    echo "$index: $fruit\n";
}

// Associative array
$user = ['name' => 'Dark', 'age' => 25, 'city' => 'Mumbai'];
foreach ($user as $key => $value) {
    echo "$key: $value\n";
}

// Modify elements with reference
foreach ($numbers as &$num) {
    $num *= 2;    // Doubles each element in place
}
unset($num);     // IMPORTANT — unset reference after loop!
```

---

## Loop Control

**Definition:** Control loop execution — skip iterations or exit loops early.

### break & continue
**Definition:** `break` exits the loop — `continue` skips to the next iteration.
```php
// break — exit loop
for ($i = 0; $i < 10; $i++) {
    if ($i === 5) break;
    echo $i;    // 0 1 2 3 4
}

// continue — skip iteration
for ($i = 0; $i < 10; $i++) {
    if ($i % 2 === 0) continue;
    echo $i;    // 1 3 5 7 9
}

// break/continue with levels — break out of nested loops
for ($i = 0; $i < 3; $i++) {
    for ($j = 0; $j < 3; $j++) {
        if ($j === 1) break 2;    // Break outer loop (2 levels)
        echo "$i,$j ";
    }
}
```

---

## Functions

**Definition:** Reusable named blocks of code — PHP supports default values, type hints, and return types.

### Basic Functions
**Definition:** Define with `function` keyword — call by name.
```php
function greet(string $name): string {
    return "Hello, $name!";
}

echo greet("Dark");    // Hello, Dark!
```

### Default Parameters
**Definition:** Parameters with default values — used when caller doesn't provide them.
```php
function createUser(string $name, int $age = 18, string $role = 'user'): array {
    return ['name' => $name, 'age' => $age, 'role' => $role];
}

createUser("Dark");                    // age=18, role='user'
createUser("Alice", 30);               // role='user'
createUser("Bob", 25, 'admin');
```

### Type Declarations
**Definition:** Type hints enforce parameter and return types — PHP 8 supports union and nullable types.
```php
// Parameter types
function add(int $a, int $b): int { return $a + $b; }
function format(string|int $value): string { return (string)$value; }  // Union (PHP 8)
function findUser(?int $id): ?array { /* ... */ }    // Nullable — ? prefix

// Return types
function divide(int $a, int $b): float|false { }
function processOrNull(int $id): ?string { }
function neverReturns(): never { throw new Exception(); }    // PHP 8.1
function noReturn(): void { /* no return statement */ }

// Strict types — optional, forces exact type matching
declare(strict_types=1);    // At top of file
```

### Variadic Functions
**Definition:** Accept any number of arguments using `...` — collected into an array.
```php
function sum(int ...$numbers): int {
    return array_sum($numbers);
}

echo sum(1, 2, 3, 4, 5);    // 15
echo sum(...[1, 2, 3]);      // Spread array as arguments — 6
```

### Anonymous Functions & Closures
**Definition:** Functions without names — assign to variables or pass as arguments.
```php
// Anonymous function
$double = function(int $n): int { return $n * 2; };
echo $double(5);    // 10

// Closure — captures outer variables with use
$multiplier = 3;
$multiply = function(int $n) use ($multiplier): int {
    return $n * $multiplier;
};
echo $multiply(5);    // 15

// Capture by reference
$count = 0;
$increment = function() use (&$count) { $count++; };
$increment();
$increment();
echo $count;    // 2

// Short arrow functions (PHP 7.4+) — auto-capture outer variables
$multiplier = 3;
$multiply = fn($n) => $n * $multiplier;    // No need for 'use'
echo $multiply(5);    // 15
```

### Named Arguments (PHP 8.0+)
**Definition:** Pass arguments by name — order doesn't matter, improves readability.
```php
function createProfile(string $name, int $age, string $city = 'Unknown'): array {
    return compact('name', 'age', 'city');
}

// Named arguments — any order, skip defaults
createProfile(age: 25, name: 'Dark');
createProfile(name: 'Alice', city: 'Delhi', age: 30);

// Useful with built-in functions
array_slice(array: $arr, offset: 2, length: 3, preserve_keys: true);
```

---

## Arrays

**Definition:** PHP arrays are ordered maps — they can hold any type and grow dynamically.

### Create Arrays
**Definition:** Different ways to create and initialize arrays.
```php
// Short syntax (PHP 5.4+)
$fruits = ["apple", "banana", "cherry"];

// Long syntax
$nums = array(1, 2, 3, 4, 5);

// Empty array
$empty = [];

// Range
$range = range(1, 10);        // [1, 2, 3, ..., 10]
$range = range(0, 10, 2);     // [0, 2, 4, 6, 8, 10] — with step
$letters = range('a', 'z');   // ['a', 'b', ..., 'z']
```

### Access & Modify
**Definition:** Get and set array elements by index.
```php
$fruits = ["apple", "banana", "cherry"];

$fruits[0]              // "apple"
$fruits[count($fruits) - 1]  // Last: "cherry"

$fruits[] = "mango"     // Append to end
$fruits[1] = "blueberry" // Update index 1
unset($fruits[1])        // Delete element (reindexes? No — leaves gap)
$fruits = array_values($fruits)  // Re-index after unset

count($fruits)           // Number of elements
in_array("apple", $fruits)  // true — check if value exists
array_search("banana", $fruits)  // Returns key/index or false
```

---

## Array Functions

**Definition:** PHP has 70+ built-in array functions — the most powerful part of the language.

### Add & Remove
**Definition:** Add or remove elements at different positions.
```php
$arr = [1, 2, 3];

array_push($arr, 4, 5)        // Add to end — [1,2,3,4,5]
$arr[] = 6;                   // Same as array_push but faster

array_pop($arr)               // Remove & return last — returns 6
array_shift($arr)             // Remove & return first — returns 1
array_unshift($arr, 0)        // Add to start — [0,2,3,4,5]

array_splice($arr, 1, 2)          // Remove 2 elements at index 1
array_splice($arr, 1, 0, [10,11]) // Insert at index 1
array_splice($arr, 1, 1, [99])    // Replace element at index 1
```

### Sort
**Definition:** Sort arrays in various orders — many sorting options.
```php
$nums = [3, 1, 4, 1, 5, 9];

sort($nums)              // Ascending, re-index:  [1,1,3,4,5,9]
rsort($nums)             // Descending, re-index: [9,5,4,3,1,1]
asort($nums)             // Ascending, keep keys
arsort($nums)            // Descending, keep keys
ksort($arr)              // Sort by key ascending
krsort($arr)             // Sort by key descending
natsort($arr)            // Natural order (1,2,10 not 1,10,2)
natcasesort($arr)        // Natural order, case-insensitive

// Custom sort with comparison function
usort($arr, function($a, $b) { return $a <=> $b; });
uasort($arr, fn($a, $b) => $a <=> $b);   // Keep keys
uksort($arr, fn($a, $b) => $a <=> $b);   // Sort by key with custom function
```

### Transform
**Definition:** Create new arrays by transforming existing ones.
```php
$nums = [1, 2, 3, 4, 5];

// array_map — transform each element
$doubled  = array_map(fn($n) => $n * 2, $nums);      // [2,4,6,8,10]
$strings  = array_map('strval', $nums);                // ["1","2","3","4","5"]

// array_filter — keep elements matching condition (preserves keys)
$evens    = array_filter($nums, fn($n) => $n % 2 === 0);  // [2,4]
$nonempty = array_filter($arr);                            // Remove falsy values

// array_reduce — reduce to single value
$sum      = array_reduce($nums, fn($carry, $n) => $carry + $n, 0);  // 15
$product  = array_reduce($nums, fn($carry, $n) => $carry * $n, 1);  // 120

// array_walk — modify in place with key
array_walk($arr, function(&$val, $key) { $val = "$key: $val"; });
```

### Search & Info
**Definition:** Find elements and get information about arrays.
```php
// Search
in_array(3, $nums)              // true — value exists
array_search(3, $nums)          // 2  — returns key (false if not found)
array_key_exists('name', $arr)  // Check if key exists (even if null)
isset($arr['key'])              // Check key exists and not null

// Info
count($arr)                     // Number of elements
array_count_values($arr)        // Count occurrences of each value
array_sum($nums)                // Sum all numeric values — 15
array_product($nums)            // Product of all values — 120

// Unique & flip
array_unique($arr)              // Remove duplicates
array_flip($arr)                // Swap keys and values
array_reverse($arr)             // Reverse order
```

### Slice & Combine
**Definition:** Extract portions and combine multiple arrays.
```php
$arr = [10, 20, 30, 40, 50];

// Slice
array_slice($arr, 1, 3)         // [20, 30, 40] — offset, length
array_slice($arr, -2)           // [40, 50] — last 2
array_chunk($arr, 2)            // [[10,20],[30,40],[50]] — split into chunks

// Combine & merge
array_merge([1,2], [3,4])       // [1,2,3,4] — reindexes numeric
array_merge(['a'=>1], ['b'=>2]) // ['a'=>1,'b'=>2] — assoc merge
$arr1 + $arr2                   // Union — first array's keys win
array_combine($keys, $values)   // Create assoc array from two arrays

// Flatten
array_merge(...$nestedArray)    // Flatten one level
```

---

## Associative Arrays

**Definition:** Arrays with named keys instead of numeric indexes — like dictionaries or hash maps.

### Create & Access
**Definition:** Key-value pairs where keys are strings.
```php
$user = [
    'name'  => 'Dark',
    'age'   => 25,
    'email' => 'dark@example.com',
    'roles' => ['admin', 'editor']
];

$user['name']          // "Dark"
$user['roles'][0]      // "admin"
$user['phone'] ?? 'N/A'  // Safe access with default
```

### Add & Update & Remove
**Definition:** Modify associative array entries.
```php
$user['city'] = 'Mumbai';      // Add new key
$user['age']  = 26;            // Update existing
unset($user['email']);         // Remove key

// Check key exists
isset($user['name'])                   // true
array_key_exists('name', $user)        // true (even if value is null)
```

### Useful Assoc Functions
**Definition:** Functions specifically useful for associative arrays.
```php
array_keys($user)              // ['name', 'age', 'city', 'roles']
array_values($user)            // ['Dark', 26, 'Mumbai', [...]]
array_keys($user, 'Dark')      // Keys where value is 'Dark' → ['name']

// Extract subset
$subset = array_intersect_key($user, array_flip(['name', 'age']));

// Extract to variables
extract($user);    // Creates $name, $age, $email variables — use carefully!
compact('name', 'age', 'city')  // Create array from variables
```

---

## Multidimensional Arrays

**Definition:** Arrays containing other arrays — used for tables, nested data, and records.

### 2D Array
**Definition:** Array of arrays — like a database table.
```php
$users = [
    ['id' => 1, 'name' => 'Dark',  'age' => 25],
    ['id' => 2, 'name' => 'Alice', 'age' => 30],
    ['id' => 3, 'name' => 'Bob',   'age' => 28],
];

$users[0]['name']       // "Dark"
$users[1]['age']        // 30

// Loop over 2D array
foreach ($users as $user) {
    echo "{$user['name']}: {$user['age']}\n";
}

// Sort 2D array by a column
usort($users, fn($a, $b) => $a['age'] <=> $b['age']);

// Filter 2D array
$adults = array_filter($users, fn($u) => $u['age'] >= 18);

// Extract one column
$names = array_column($users, 'name');            // ['Dark', 'Alice', 'Bob']
$byId  = array_column($users, null, 'id');        // Indexed by 'id'
$nameById = array_column($users, 'name', 'id');   // ['1'=>'Dark', '2'=>'Alice', ...]
```

---

## Classes & OOP

**Definition:** PHP supports full object-oriented programming — classes, objects, inheritance, interfaces, and traits.

### Define a Class
**Definition:** A class is a blueprint for objects — contains properties and methods.
```php
class User {
    // Properties
    public string  $name;
    protected int  $age;
    private string $password;
    public readonly int $id;    // PHP 8.1 — can only be set once

    // Class constant
    public const MAX_AGE = 150;

    // Constructor
    public function __construct(
        int $id, string $name, int $age, string $password
    ) {
        $this->id       = $id;
        $this->name     = $name;
        $this->age      = $age;
        $this->password = password_hash($password, PASSWORD_DEFAULT);
    }

    // Constructor property promotion (PHP 8.0+)
    // public function __construct(
    //     public readonly int $id,
    //     public string $name,
    //     protected int $age,
    // ) {}

    // Methods
    public function getName(): string {
        return $this->name;
    }

    public function getAge(): int {
        return $this->age;
    }

    public function setAge(int $age): void {
        if ($age < 0 || $age > self::MAX_AGE) {
            throw new InvalidArgumentException("Invalid age: $age");
        }
        $this->age = $age;
    }

    // Magic method — called when object used as string
    public function __toString(): string {
        return "User({$this->id}, {$this->name})";
    }
}

// Create object
$user = new User(1, "Dark", 25, "secret");
echo $user->name;          // Dark
echo $user->getName();     // Dark
$user->setAge(26);
echo $user;                // User(1, Dark)
```

### Magic Methods
**Definition:** Special methods PHP calls automatically in certain situations.
```php
class MagicClass {
    private array $data = [];

    // Object creation and destruction
    public function __construct() { }
    public function __destruct() { }      // Called when object is destroyed

    // Property access (for private/protected)
    public function __get(string $name): mixed { return $this->data[$name] ?? null; }
    public function __set(string $name, mixed $value): void { $this->data[$name] = $value; }
    public function __isset(string $name): bool { return isset($this->data[$name]); }
    public function __unset(string $name): void { unset($this->data[$name]); }

    // Callable
    public function __invoke(int $n): int { return $n * 2; }  // $obj(5) → 10

    // String conversion
    public function __toString(): string { return json_encode($this->data); }

    // Serialization
    public function __sleep(): array { return ['data']; }      // Before serialize()
    public function __wakeup(): void { }                       // After unserialize()
    public function __serialize(): array { return $this->data; }     // PHP 7.4+
    public function __unserialize(array $data): void { $this->data = $data; }

    // Cloning
    public function __clone() { /* deep copy logic */ }

    // Debugging
    public function __debugInfo(): array { return $this->data; }  // For var_dump()

    // Static factory
    public static function __set_state(array $props): static { /* ... */ }
}
```

### Static Members
**Definition:** Properties and methods belonging to the class — not individual objects.
```php
class Counter {
    private static int $count = 0;

    public static function increment(): void {
        self::$count++;           // self:: for current class
    }

    public static function getCount(): int {
        return self::$count;
    }

    public static function create(): static {
        return new static();      // static:: for late static binding (LSB)
    }
}

Counter::increment();
Counter::increment();
echo Counter::getCount();    // 2
```

---

## Inheritance

**Definition:** A child class inherits properties and methods from a parent — use `extends`.

### Basic Inheritance
**Definition:** Extend a class to create a specialized version — override methods as needed.
```php
class Animal {
    public function __construct(
        protected string $name,
        protected int $age
    ) {}

    public function eat(): void {
        echo "{$this->name} is eating\n";
    }

    public function sound(): string {
        return "...";
    }

    public function describe(): string {
        return "{$this->name} ({$this->age}y): " . $this->sound();
    }
}

class Dog extends Animal {
    public function __construct(string $name, int $age, private string $breed) {
        parent::__construct($name, $age);    // Call parent constructor
    }

    // Override parent method
    public function sound(): string {
        return "Woof!";
    }

    // New method
    public function fetch(): void {
        echo "{$this->name} fetches!\n";
    }
}

class Cat extends Animal {
    public function sound(): string { return "Meow!"; }
}

$dog = new Dog("Rex", 3, "Labrador");
$dog->eat();            // Rex is eating (inherited)
echo $dog->sound();     // Woof! (overridden)
echo $dog->describe();  // Rex (3y): Woof!
$dog->fetch();          // Rex fetches!

// Final class — cannot be extended
final class Singleton {
    private static ?self $instance = null;
    public static function getInstance(): static {
        return self::$instance ??= new static();
    }
}

// Final method — cannot be overridden
class Base {
    final public function criticalMethod(): void { }
}
```

---

## Interfaces & Abstract Classes

**Definition:** Define contracts — interfaces are pure contracts, abstract classes provide partial implementation.

### Interface
**Definition:** Define method signatures that implementing classes must fulfill — no method bodies.
```php
interface Printable {
    public function print(): void;
    public function getContent(): string;
}

interface Serializable {
    public function serialize(): string;
    public static function deserialize(string $data): static;
}

// Implement multiple interfaces
class Document implements Printable, Serializable {
    public function __construct(private string $content) {}

    public function print(): void {
        echo $this->content;
    }

    public function getContent(): string {
        return $this->content;
    }

    public function serialize(): string {
        return json_encode(['content' => $this->content]);
    }

    public static function deserialize(string $data): static {
        $arr = json_decode($data, true);
        return new static($arr['content']);
    }
}

// Interface can extend other interfaces
interface ReadWriteInterface extends Printable, Serializable {
    public function save(): bool;
}
```

### Abstract Class
**Definition:** Cannot be instantiated — provides partial implementation for subclasses to complete.
```php
abstract class Shape {
    abstract public function area(): float;
    abstract public function perimeter(): float;

    // Concrete method — inherited as-is
    public function describe(): string {
        return sprintf("%s: area=%.2f, perimeter=%.2f",
            get_class($this), $this->area(), $this->perimeter());
    }
}

class Rectangle extends Shape {
    public function __construct(
        private float $width,
        private float $height
    ) {}

    public function area(): float      { return $this->width * $this->height; }
    public function perimeter(): float { return 2 * ($this->width + $this->height); }
}

class Circle extends Shape {
    public function __construct(private float $radius) {}

    public function area(): float      { return M_PI * $this->radius ** 2; }
    public function perimeter(): float { return 2 * M_PI * $this->radius; }
}

$shapes = [new Rectangle(10, 5), new Circle(7)];
foreach ($shapes as $shape) {
    echo $shape->describe() . "\n";
}
```

---

## Traits

**Definition:** Reusable code snippets that can be included in multiple classes — PHP's solution to multiple inheritance.

### Basic Trait
**Definition:** Define reusable methods in a trait — include with `use` keyword.
```php
trait Timestamps {
    private ?DateTime $createdAt = null;
    private ?DateTime $updatedAt = null;

    public function setCreatedAt(): void {
        $this->createdAt = new DateTime();
    }

    public function setUpdatedAt(): void {
        $this->updatedAt = new DateTime();
    }

    public function getCreatedAt(): ?DateTime {
        return $this->createdAt;
    }
}

trait SoftDelete {
    private bool $deleted = false;
    private ?DateTime $deletedAt = null;

    public function softDelete(): void {
        $this->deleted   = true;
        $this->deletedAt = new DateTime();
    }

    public function isDeleted(): bool {
        return $this->deleted;
    }
}

class Post {
    use Timestamps, SoftDelete;    // Use multiple traits

    public function __construct(
        public string $title,
        public string $content
    ) {
        $this->setCreatedAt();
    }
}

$post = new Post("Hello", "Content");
$post->softDelete();
echo $post->isDeleted() ? "Deleted" : "Active";
```

---

## Namespaces & Autoloading

**Definition:** Namespaces organize code and prevent name collisions — autoloading loads classes on demand.

### Namespaces
**Definition:** Group related classes under a namespace path — like packages in Java.
```php
<?php
// File: src/App/Models/User.php
namespace App\Models;

use App\Services\AuthService;
use PDO;            // Import from global namespace
use DateTime as DT; // Alias

class User {
    // ...
}
```

```php
<?php
// File: src/App/Controllers/UserController.php
namespace App\Controllers;

use App\Models\User;
use App\Models\Post;
use App\Services\{UserService, EmailService};  // Multiple imports
use App\Repository\UserRepository as UserRepo; // Alias

class UserController {
    public function index(): void {
        $user = new User();
        // ...
    }
}
```

### PSR-4 Autoloading with Composer
**Definition:** Automatically load classes without manual `require` — standard practice.
```json
// composer.json
{
    "autoload": {
        "psr-4": {
            "App\\": "src/"
        }
    }
}
```

```php
// bootstrap.php or index.php
require 'vendor/autoload.php';

// Now classes auto-load:
// App\Models\User → src/Models/User.php
// App\Controllers\UserController → src/Controllers/UserController.php
```

---

## Error Handling

**Definition:** PHP has multiple error handling mechanisms — exceptions, try/catch, and error handlers.

### Try / Catch / Finally
**Definition:** Wrap risky code to catch exceptions — `finally` always runs.
```php
try {
    $result = divide(10, 0);
} catch (DivisionByZeroError $e) {
    echo "Math error: " . $e->getMessage();
} catch (InvalidArgumentException $e) {
    echo "Invalid arg: " . $e->getMessage();
} catch (Exception $e) {
    echo "General error: " . $e->getMessage();
    echo "\nFile: " . $e->getFile();
    echo "\nLine: " . $e->getLine();
    echo "\nTrace: " . $e->getTraceAsString();
} finally {
    echo "Always runs";
}

// Multiple exception types in one catch (PHP 8.0+)
catch (TypeError | ValueError $e) {
    echo "Type or value error: " . $e->getMessage();
}
```

### Throw Exceptions
**Definition:** Create and throw exceptions — can throw any Throwable.
```php
function divide(float $a, float $b): float {
    if ($b == 0) {
        throw new InvalidArgumentException("Cannot divide by zero");
    }
    return $a / $b;
}

// Throw expression (PHP 8.0+) — can throw in expressions
$value = $arr['key'] ?? throw new RuntimeException("Key missing");
$user  = getUser($id) ?: throw new NotFoundException("User $id not found");
```

### Custom Exceptions
**Definition:** Create application-specific exception classes for better error handling.
```php
class AppException extends RuntimeException {
    public function __construct(
        string $message,
        private readonly string $context = '',
        int $code = 0,
        ?\Throwable $previous = null
    ) {
        parent::__construct($message, $code, $previous);
    }

    public function getContext(): string {
        return $this->context;
    }
}

class NotFoundException extends AppException {
    public function __construct(string $resource, int $id) {
        parent::__construct("$resource with ID $id not found", $resource, 404);
    }
}

class ValidationException extends AppException {
    public function __construct(private array $errors) {
        parent::__construct("Validation failed", implode(', ', $errors), 422);
    }

    public function getErrors(): array { return $this->errors; }
}
```

### Error Handler
**Definition:** Set custom functions to handle PHP errors and unhandled exceptions.
```php
// Handle all errors
set_error_handler(function(int $level, string $message, string $file, int $line): bool {
    throw new ErrorException($message, 0, $level, $file, $line);
});

// Handle uncaught exceptions
set_exception_handler(function(\Throwable $e): void {
    http_response_code(500);
    error_log($e->getMessage() . "\n" . $e->getTraceAsString());
    echo "An unexpected error occurred";
});

// Restore handlers
restore_error_handler();
restore_exception_handler();
```

---

## File Handling

**Definition:** PHP has comprehensive file I/O functions for reading, writing, and managing files.

### Read Files
**Definition:** Read file contents in different ways depending on needs.
```php
// Read entire file as string
$content = file_get_contents('file.txt');

// Read line by line (memory efficient)
$handle = fopen('file.txt', 'r');
while (!feof($handle)) {
    $line = fgets($handle);     // Read one line
    echo trim($line) . "\n";
}
fclose($handle);

// Read into array of lines
$lines = file('file.txt', FILE_IGNORE_NEW_LINES | FILE_SKIP_EMPTY_LINES);

// Read CSV
$handle = fopen('data.csv', 'r');
$header = fgetcsv($handle);    // First row as headers
while ($row = fgetcsv($handle)) {
    $data[] = array_combine($header, $row);
}
fclose($handle);
```

### Write Files
**Definition:** Write content to files — create, overwrite, or append.
```php
// Write (create or overwrite)
file_put_contents('output.txt', "Hello, World!\n");

// Append
file_put_contents('log.txt', "New line\n", FILE_APPEND | LOCK_EX);

// Write with handle (more control)
$handle = fopen('output.txt', 'w');    // Modes: r, r+, w, w+, a, a+, x, x+
fwrite($handle, "Line 1\n");
fwrite($handle, "Line 2\n");
fclose($handle);

// Write CSV
$handle = fopen('output.csv', 'w');
fputcsv($handle, ['Name', 'Age', 'City']);    // Header
fputcsv($handle, ['Dark', 25, 'Mumbai']);
fclose($handle);
```

### File System Operations
**Definition:** Check, create, copy, move, and delete files and directories.
```php
// Check
file_exists('file.txt')         // Exists (file or dir)
is_file('file.txt')             // Is regular file
is_dir('folder')                // Is directory
is_readable('file.txt')         // Is readable
is_writable('file.txt')         // Is writable
filesize('file.txt')            // Size in bytes
filemtime('file.txt')           // Last modification time

// Operations
copy('source.txt', 'dest.txt')  // Copy file
rename('old.txt', 'new.txt')    // Rename or move
unlink('file.txt')              // Delete file
mkdir('new_dir', 0755, true)    // Create directory (true = recursive)
rmdir('empty_dir')              // Delete empty directory
touch('file.txt')               // Create or update timestamp

// List directory
$files = scandir('folder/');    // Array of filenames
$files = glob('src/*.php');     // Glob pattern matching

// Recursive delete
function deleteDirectory(string $dir): void {
    foreach (scandir($dir) as $file) {
        if ($file === '.' || $file === '..') continue;
        $path = "$dir/$file";
        is_dir($path) ? deleteDirectory($path) : unlink($path);
    }
    rmdir($dir);
}
```

---

## Form Handling

**Definition:** Process HTML form data submitted via GET or POST — always validate and sanitize input.

### Receive Form Data
**Definition:** Access submitted form data from superglobal arrays.
```php
// GET request — data in URL query string
$name = $_GET['name'] ?? '';
$page = (int)($_GET['page'] ?? 1);

// POST request — data in request body
$email    = $_POST['email']    ?? '';
$password = $_POST['password'] ?? '';

// Either GET or POST
$value = $_REQUEST['key'] ?? '';

// File upload
$file = $_FILES['photo'] ?? null;
if ($file && $file['error'] === UPLOAD_ERR_OK) {
    $tmpPath  = $file['tmp_name'];
    $filename = basename($file['name']);
    $size     = $file['size'];
    $type     = $file['type'];
    move_uploaded_file($tmpPath, "uploads/$filename");
}
```

### Validate Input
**Definition:** Always validate user input before using it — never trust user data.
```php
// Filter and validate
$email = filter_input(INPUT_POST, 'email', FILTER_VALIDATE_EMAIL);
if (!$email) {
    $errors[] = "Invalid email address";
}

$age = filter_input(INPUT_POST, 'age', FILTER_VALIDATE_INT, [
    'options' => ['min_range' => 1, 'max_range' => 150]
]);

$url = filter_input(INPUT_POST, 'website', FILTER_VALIDATE_URL);

// filter_var — validate/sanitize a variable (not from superglobal)
$isEmail = filter_var($email, FILTER_VALIDATE_EMAIL) !== false;
$safeStr = filter_var($str, FILTER_SANITIZE_SPECIAL_CHARS);
$intVal  = filter_var($num, FILTER_VALIDATE_INT);

// Manual validation
$name = trim($_POST['name'] ?? '');
if (empty($name)) {
    $errors[] = "Name is required";
} elseif (strlen($name) < 2 || strlen($name) > 50) {
    $errors[] = "Name must be 2-50 characters";
} elseif (!preg_match('/^[a-zA-Z\s]+$/', $name)) {
    $errors[] = "Name can only contain letters and spaces";
}
```

### Sanitize & Output
**Definition:** Clean input and safely output it to prevent XSS attacks.
```php
// Prevent XSS — escape output
echo htmlspecialchars($userInput, ENT_QUOTES, 'UTF-8');
echo htmlentities($userInput, ENT_QUOTES, 'UTF-8');

// Strip HTML tags
$clean = strip_tags($html);
$clean = strip_tags($html, '<b><i>');    // Allow only <b> and <i>

// Sanitize for different contexts
$safeHtml = htmlspecialchars($str, ENT_QUOTES | ENT_HTML5, 'UTF-8');
$safeUrl  = urlencode($param);           // For URL parameters
$safeJson = json_encode($data, JSON_HEX_TAG | JSON_HEX_APOS | JSON_HEX_AMP);
```

---

## Working with JSON

**Definition:** PHP has native JSON encoding and decoding — essential for APIs and data exchange.

### Encode (PHP → JSON)
**Definition:** Convert PHP arrays and objects to JSON strings.
```php
$data = [
    'name'   => 'Dark',
    'age'    => 25,
    'skills' => ['PHP', 'MySQL'],
    'active' => true
];

$json = json_encode($data);
// {"name":"Dark","age":25,"skills":["PHP","MySQL"],"active":true}

$pretty = json_encode($data, JSON_PRETTY_PRINT);
$safe   = json_encode($data, JSON_UNESCAPED_UNICODE | JSON_UNESCAPED_SLASHES);
$flags  = json_encode($data, JSON_PRETTY_PRINT | JSON_UNESCAPED_UNICODE | JSON_THROW_ON_ERROR);

// Check for errors
if (json_last_error() !== JSON_ERROR_NONE) {
    throw new RuntimeException("JSON encode error: " . json_last_error_msg());
}
```

### Decode (JSON → PHP)
**Definition:** Parse JSON strings into PHP arrays or objects.
```php
$json = '{"name":"Dark","age":25,"skills":["PHP","MySQL"]}';

// Decode to associative array (second param true)
$data = json_decode($json, true);
echo $data['name'];     // Dark
echo $data['skills'][0]; // PHP

// Decode to object (default)
$obj = json_decode($json);
echo $obj->name;        // Dark
echo $obj->skills[0];   // PHP

// With error handling (PHP 7.3+)
try {
    $data = json_decode($json, true, 512, JSON_THROW_ON_ERROR);
} catch (\JsonException $e) {
    echo "JSON error: " . $e->getMessage();
}
```

### JSON API Response
**Definition:** Send a proper JSON API response from PHP.
```php
function jsonResponse(mixed $data, int $statusCode = 200): void {
    http_response_code($statusCode);
    header('Content-Type: application/json; charset=utf-8');
    echo json_encode($data, JSON_PRETTY_PRINT | JSON_UNESCAPED_UNICODE | JSON_THROW_ON_ERROR);
    exit;
}

// Usage
jsonResponse(['status' => 'success', 'user' => $user], 201);
jsonResponse(['error' => 'Not found'], 404);
```

---

## Regular Expressions

**Definition:** Pattern matching using PCRE (Perl-Compatible Regular Expressions) — PHP's `preg_*` functions.

### Test & Match
**Definition:** Test if a pattern matches and extract matches.
```php
// Test if pattern matches
preg_match('/^\d+$/', '12345')          // 1 (match found)
preg_match('/^\d+$/', 'abc')            // 0 (no match)

// Get first match + capture groups
preg_match('/(\d{4})-(\d{2})-(\d{2})/', '2025-01-15', $matches);
// $matches[0] = "2025-01-15" (full match)
// $matches[1] = "2025" (group 1)
// $matches[2] = "01"   (group 2)
// $matches[3] = "15"   (group 3)

// Get all matches
preg_match_all('/\d+/', 'abc 123 def 456', $matches);
// $matches[0] = ["123", "456"]

// Named groups
preg_match('/(?P<year>\d{4})-(?P<month>\d{2})/', '2025-01', $m);
echo $m['year'];   // 2025
echo $m['month'];  // 01
```

### Replace & Split
**Definition:** Replace pattern matches or split strings by pattern.
```php
// Replace
preg_replace('/\d+/', 'NUM', 'abc 123 def 456')  // "abc NUM def NUM"
preg_replace('/\s+/', ' ', "too   many    spaces")  // "too many spaces"

// Replace with callback
preg_replace_callback('/\d+/', function($matches) {
    return $matches[0] * 2;    // Double each number
}, "I have 3 cats and 2 dogs");  // "I have 6 cats and 4 dogs"

// Split
preg_split('/[\s,;]+/', 'a b,c;d')     // ['a', 'b', 'c', 'd']
preg_split('/\s+/', $text, -1, PREG_SPLIT_NO_EMPTY)  // Remove empty parts
```

### Common Patterns
**Definition:** Ready-to-use regex patterns for validation.
```php
// Email
'/^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/'

// URL
'/^https?:\/\/(www\.)?[-a-zA-Z0-9@:%._\+~#=]{1,256}\.[a-zA-Z0-9()]{1,6}\b/'

// Phone (Indian)
'/^(\+91|0)?[6-9][0-9]{9}$/'

// Date YYYY-MM-DD
'/^\d{4}-(0[1-9]|1[0-2])-(0[1-9]|[12][0-9]|3[01])$/'

// Password (8+ chars, 1 uppercase, 1 lowercase, 1 digit)
'/^(?=.*[a-z])(?=.*[A-Z])(?=.*\d).{8,}$/'

// Only letters and spaces
'/^[a-zA-Z\s]+$/'

// Hex color
'/^#([A-Fa-f0-9]{6}|[A-Fa-f0-9]{3})$/'
```

---

## Date & Time

**Definition:** PHP has two date APIs — the procedural `date()`/`strtotime()` and the OOP `DateTime` class.

### Procedural Date Functions
**Definition:** Simple functions for common date formatting and parsing.
```php
date('Y-m-d')              // "2025-01-15" — current date
date('H:i:s')              // "14:30:00"   — current time
date('Y-m-d H:i:s')        // "2025-01-15 14:30:00"
date('D, d M Y', time())   // "Wed, 15 Jan 2025"
date('U')                  // Unix timestamp (seconds since 1970)
time()                     // Current Unix timestamp

// Parse string to timestamp
strtotime('2025-01-15')           // Unix timestamp
strtotime('+7 days')              // One week from now
strtotime('-1 month')             // One month ago
strtotime('next Monday')
strtotime('last day of this month')

// Format a past timestamp
date('Y-m-d', strtotime('2020-06-15'))   // "2020-06-15"
```

### DateTime Class (OOP)
**Definition:** Modern, more powerful date handling — timezone aware, immutable variants.
```php
// Create
$now  = new DateTime();
$date = new DateTime('2025-01-15');
$date = new DateTime('2025-01-15 14:30:00', new DateTimeZone('Asia/Kolkata'));

// DateTimeImmutable — returns new object instead of modifying
$immutable = new DateTimeImmutable('2025-01-15');

// Format
echo $date->format('Y-m-d H:i:s');     // "2025-01-15 14:30:00"
echo $date->format('D, d M Y');         // "Wed, 15 Jan 2025"

// Modify
$nextWeek    = $date->modify('+7 days');      // Mutates DateTime
$nextWeek    = $immutable->modify('+7 days'); // Returns new DateTimeImmutable

// Date arithmetic
$date->add(new DateInterval('P7D'));     // Add 7 days
$date->sub(new DateInterval('P1M'));     // Subtract 1 month

// Compare
$diff = $date1->diff($date2);
echo $diff->days;     // Total days difference
echo $diff->months;   // Months difference

// Compare
$date1 < $date2       // true if date1 is earlier
$date1 == $date2      // true if same moment

// Parse any format
$date = DateTime::createFromFormat('d/m/Y', '15/01/2025');
```

---

## Database — PDO

**Definition:** PHP Data Objects (PDO) — database-agnostic interface for MySQL, PostgreSQL, SQLite, and more.

### Connect
**Definition:** Create a PDO connection — use prepared statements for all queries.
```php
$dsn = "mysql:host=localhost;dbname=mydb;charset=utf8mb4";

try {
    $pdo = new PDO($dsn, 'username', 'password', [
        PDO::ATTR_ERRMODE            => PDO::ERRMODE_EXCEPTION,   // Throw exceptions
        PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,         // Fetch as assoc array
        PDO::ATTR_EMULATE_PREPARES   => false,                    // Use native prepares
    ]);
} catch (PDOException $e) {
    die("Connection failed: " . $e->getMessage());
}
```

### SELECT
**Definition:** Query data using prepared statements with bound parameters.
```php
// Fetch all rows
$stmt = $pdo->query("SELECT * FROM users ORDER BY name");
$users = $stmt->fetchAll();              // All rows as array
$users = $stmt->fetchAll(PDO::FETCH_OBJ); // As objects

// Prepared statement with parameters
$stmt = $pdo->prepare("SELECT * FROM users WHERE age > ? AND city = ?");
$stmt->execute([18, 'Mumbai']);
$users = $stmt->fetchAll();

// Named parameters
$stmt = $pdo->prepare("SELECT * FROM users WHERE email = :email");
$stmt->execute([':email' => $email]);
$user = $stmt->fetch();                  // Single row

// Inline execute
$users = $pdo->prepare("SELECT * FROM users WHERE id = ?")->execute([$id]);

// rowCount and column
$stmt->rowCount()                        // Number of rows returned/affected
$stmt->fetchColumn()                     // Single column from current row
```

### INSERT, UPDATE, DELETE
**Definition:** Execute data modification queries with bound parameters.
```php
// Insert
$stmt = $pdo->prepare(
    "INSERT INTO users (name, email, age, created_at)
     VALUES (:name, :email, :age, NOW())"
);
$stmt->execute([
    ':name'  => $name,
    ':email' => $email,
    ':age'   => $age,
]);
$newId = $pdo->lastInsertId();    // ID of inserted row

// Update
$stmt = $pdo->prepare("UPDATE users SET name = ?, age = ? WHERE id = ?");
$stmt->execute([$newName, $newAge, $id]);
$affected = $stmt->rowCount();    // Number of updated rows

// Delete
$stmt = $pdo->prepare("DELETE FROM users WHERE id = ?");
$stmt->execute([$id]);
```

### Transactions
**Definition:** Group multiple queries into an atomic operation — all succeed or all roll back.
```php
try {
    $pdo->beginTransaction();

    $pdo->prepare("UPDATE accounts SET balance = balance - ? WHERE id = ?")
        ->execute([$amount, $fromId]);

    $pdo->prepare("UPDATE accounts SET balance = balance + ? WHERE id = ?")
        ->execute([$amount, $toId]);

    $pdo->prepare("INSERT INTO transfers (from_id, to_id, amount) VALUES (?, ?, ?)")
        ->execute([$fromId, $toId, $amount]);

    $pdo->commit();
    echo "Transfer successful";
} catch (PDOException $e) {
    $pdo->rollBack();
    throw new RuntimeException("Transfer failed: " . $e->getMessage(), 0, $e);
}
```

---

## Sessions & Cookies

**Definition:** Persist data across HTTP requests — sessions on server side, cookies on client side.

### Sessions
**Definition:** Store user-specific data server-side — identified by a session ID cookie.
```php
session_start();    // Must call before any output — start or resume session

// Store data
$_SESSION['user_id']  = $userId;
$_SESSION['username'] = $username;
$_SESSION['role']     = 'admin';

// Read data
$userId = $_SESSION['user_id'] ?? null;
if (!isset($_SESSION['user_id'])) {
    header('Location: /login');
    exit;
}

// Delete specific key
unset($_SESSION['temp_data']);

// Regenerate ID — do this after login! (prevent session fixation)
session_regenerate_id(true);

// Destroy entire session (logout)
$_SESSION = [];                          // Clear all data
session_destroy();                       // Destroy session
if (ini_get("session.use_cookies")) {   // Delete session cookie
    $params = session_get_cookie_params();
    setcookie(session_name(), '', time() - 42000,
        $params["path"], $params["domain"],
        $params["secure"], $params["httponly"]
    );
}
```

### Cookies
**Definition:** Small pieces of data stored in the browser — sent with every request.
```php
// Set cookie
setcookie(
    name:     'username',
    value:    'Dark',
    expires:  time() + (86400 * 30),    // 30 days
    path:     '/',
    domain:   '',
    secure:   true,        // HTTPS only
    httponly: true         // No JavaScript access
);

// Set in options array (PHP 7.3+)
setcookie('theme', 'dark', [
    'expires'  => time() + 86400 * 30,
    'path'     => '/',
    'secure'   => true,
    'httponly' => true,
    'samesite' => 'Lax'   // CSRF protection: Strict, Lax, or None
]);

// Read cookie
$username = $_COOKIE['username'] ?? 'Guest';

// Delete cookie — set expiry in the past
setcookie('username', '', time() - 3600, '/');
```

---

## HTTP Headers & Redirects

**Definition:** Send HTTP headers before any HTML output — control caching, redirects, content type.

### Headers
**Definition:** Must be sent before any output — use `ob_start()` if needed.
```php
// Content type
header('Content-Type: application/json; charset=utf-8');
header('Content-Type: text/csv');
header('Content-Type: application/pdf');
header('Content-Disposition: attachment; filename="report.pdf"');

// Cache control
header('Cache-Control: no-cache, no-store, must-revalidate');
header('Pragma: no-cache');
header('Expires: 0');

// Security headers
header('X-Frame-Options: DENY');
header('X-Content-Type-Options: nosniff');
header('X-XSS-Protection: 1; mode=block');
header('Strict-Transport-Security: max-age=31536000; includeSubDomains');
header("Content-Security-Policy: default-src 'self'");

// CORS
header('Access-Control-Allow-Origin: *');
header('Access-Control-Allow-Methods: GET, POST, PUT, DELETE, OPTIONS');
header('Access-Control-Allow-Headers: Content-Type, Authorization');

// Status codes
http_response_code(200);
http_response_code(201);    // Created
http_response_code(400);    // Bad Request
http_response_code(401);    // Unauthorized
http_response_code(403);    // Forbidden
http_response_code(404);    // Not Found
http_response_code(500);    // Internal Server Error
```

### Redirects
**Definition:** Send browser to a different URL.
```php
// Temporary redirect (default)
header('Location: /dashboard');
exit;    // ALWAYS exit after redirect!

// Permanent redirect
header('Location: https://new-domain.com', true, 301);
exit;

// Back to previous page
header('Location: ' . ($_SERVER['HTTP_REFERER'] ?? '/'));
exit;

// With message via session
$_SESSION['flash'] = ['type' => 'success', 'message' => 'Saved!'];
header('Location: /users');
exit;
```

---

## PHP 8 Features

**Definition:** Major improvements in PHP 8.0, 8.1, 8.2, and 8.3 — write more expressive, safer code.

### PHP 8.0 Features
**Definition:** Named arguments, match, nullsafe operator, union types, and more.
```php
// Named arguments
array_slice(array: $arr, offset: 2, length: 3);

// Match expression (covered earlier)

// Nullsafe operator
$city = $user?->getAddress()?->getCity();

// Union types
function process(int|string $value): bool|null { }

// Constructor property promotion
class User {
    public function __construct(
        public readonly int $id,
        public string $name,
        protected int $age = 18,
    ) {}
}

// Throw as expression
$val = $arr['key'] ?? throw new RuntimeException("Missing key");

// str_contains, str_starts_with, str_ends_with
str_contains($str, 'needle');
str_starts_with($str, 'prefix');
str_ends_with($str, 'suffix');

// Attributes (PHP 8.0+)
#[Route('/users', methods: ['GET'])]
#[Deprecated("Use newMethod() instead")]
class UserController { }
```

### PHP 8.1 Features
**Definition:** Enums, fibers, intersection types, never return type, readonly properties.
```php
// Enums
enum Status {
    case Active;
    case Inactive;
    case Banned;
}

enum Color: string {    // Backed enum
    case Red   = 'red';
    case Green = 'green';
    case Blue  = 'blue';
}

$status = Status::Active;
$color  = Color::Red;
echo $color->value;    // "red"
Color::from('red');    // Color::Red
Color::tryFrom('xyz'); // null (no exception)

// Readonly properties
class Product {
    public readonly float $price;
    public function __construct(float $price) {
        $this->price = $price;    // Can only be set once
    }
}

// Intersection types
function process(Iterator&Countable $collection) { }

// First-class callables
$fn = strlen(...);            // Closure for strlen
$fn = $obj->method(...);      // Closure for method
$arr = array_map(strlen(...), $strings);

// never return type
function redirect(string $url): never {
    header("Location: $url");
    exit;
}

// Fibers (cooperative multitasking)
$fiber = new Fiber(function(): void {
    $val = Fiber::suspend('fiber started');
    echo "Got: $val\n";
});
$val = $fiber->start();       // "fiber started"
$fiber->resume('hello');      // "Got: hello"
```

### PHP 8.2 Features
**Definition:** Readonly classes, DNF types, null/false/true as standalone types.
```php
// Readonly class — all properties readonly
readonly class Point {
    public function __construct(
        public float $x,
        public float $y,
        public float $z = 0.0,
    ) {}
}

// DNF types (Disjunctive Normal Form)
function process((Stringable&Countable)|null $value) { }

// Standalone null, false, true types
function alwaysFalse(): false { return false; }
function alwaysNull(): null { return null; }
function alwaysTrue(): true { return true; }
```

---

## Composer & Packages

**Definition:** Composer is PHP's dependency manager — declare packages in `composer.json`, install with `composer install`.

### Basic Commands
**Definition:** Essential Composer commands for managing dependencies.
```bash
composer init                    # Initialize new project
composer install                 # Install from composer.lock
composer update                  # Update all dependencies
composer require vendor/package  # Add a package
composer require vendor/package:^2.0   # Specific version constraint
composer require --dev phpunit/phpunit # Dev dependency only
composer remove vendor/package   # Remove a package
composer show                    # List installed packages
composer outdated                # Show outdated packages
composer dump-autoload           # Regenerate autoloader
```

### composer.json
**Definition:** Project manifest file — declare dependencies, autoloading, and scripts.
```json
{
    "name": "myapp/project",
    "description": "My PHP Application",
    "type": "project",
    "require": {
        "php": "^8.1",
        "guzzlehttp/guzzle": "^7.5",
        "vlucas/phpdotenv": "^5.5"
    },
    "require-dev": {
        "phpunit/phpunit": "^10.0",
        "phpstan/phpstan": "^1.0"
    },
    "autoload": {
        "psr-4": {
            "App\\": "src/"
        }
    },
    "autoload-dev": {
        "psr-4": {
            "Tests\\": "tests/"
        }
    },
    "scripts": {
        "test":   "phpunit",
        "lint":   "phpstan analyse src"
    }
}
```

### Version Constraints
**Definition:** Semver constraints for controlling which package versions to allow.
```
^2.0       — Compatible with 2.x (>=2.0.0 <3.0.0)
~2.5       — Reasonably close (>=2.5.0 <3.0.0)
>=2.0      — Minimum 2.0
2.0.*      — Exactly 2.0.x
2.0.0      — Exactly this version
*          — Any version (avoid!)
```

---

## Security

**Definition:** Essential PHP security practices — protect against SQL injection, XSS, CSRF, and more.

### SQL Injection Prevention
**Definition:** Always use prepared statements — never interpolate user input into SQL.
```php
// VULNERABLE — never do this!
$id = $_GET['id'];
$pdo->query("SELECT * FROM users WHERE id = $id");   // SQL injection!

// SAFE — always use prepared statements
$stmt = $pdo->prepare("SELECT * FROM users WHERE id = ?");
$stmt->execute([$id]);

$stmt = $pdo->prepare("SELECT * FROM users WHERE email = :email AND active = :active");
$stmt->execute([':email' => $email, ':active' => 1]);
```

### XSS Prevention
**Definition:** Escape all user data before outputting to HTML — one mistake can compromise users.
```php
// VULNERABLE — echoing raw user input
echo $_GET['name'];   // XSS!

// SAFE — always escape output
echo htmlspecialchars($_GET['name'], ENT_QUOTES | ENT_HTML5, 'UTF-8');

// Helper function
function e(string $str): string {
    return htmlspecialchars($str, ENT_QUOTES | ENT_HTML5, 'UTF-8');
}
echo e($userInput);
```

### CSRF Protection
**Definition:** Generate and validate tokens to prevent cross-site request forgery.
```php
// Generate token on form display
function generateCsrfToken(): string {
    if (!isset($_SESSION['csrf_token'])) {
        $_SESSION['csrf_token'] = bin2hex(random_bytes(32));
    }
    return $_SESSION['csrf_token'];
}

// In form
echo '<input type="hidden" name="csrf_token" value="' . generateCsrfToken() . '">';

// Validate on form submission
function validateCsrfToken(string $token): bool {
    return isset($_SESSION['csrf_token']) &&
           hash_equals($_SESSION['csrf_token'], $token);
}

if (!validateCsrfToken($_POST['csrf_token'] ?? '')) {
    http_response_code(403);
    die("CSRF token validation failed");
}
```

### Password Hashing
**Definition:** Always hash passwords before storage — never store plain text passwords.
```php
// Hash password (bcrypt by default)
$hash = password_hash($password, PASSWORD_DEFAULT);
$hash = password_hash($password, PASSWORD_BCRYPT, ['cost' => 12]);
$hash = password_hash($password, PASSWORD_ARGON2ID);    // PHP 7.3+

// Verify password
if (password_verify($inputPassword, $storedHash)) {
    echo "Password correct";
}

// Check if rehash needed (if algorithm changed)
if (password_needs_rehash($hash, PASSWORD_DEFAULT)) {
    $newHash = password_hash($password, PASSWORD_DEFAULT);
    // Update stored hash
}
```

### Input Sanitization
**Definition:** Validate type and range, sanitize format — defense in depth.
```php
// Validate integers
$id = filter_var($_GET['id'], FILTER_VALIDATE_INT);
if ($id === false || $id < 1) {
    http_response_code(400);
    die("Invalid ID");
}

// Validate email
$email = filter_var($_POST['email'], FILTER_VALIDATE_EMAIL);
if (!$email) die("Invalid email");

// Sanitize string (remove dangerous chars)
$name = filter_var($_POST['name'], FILTER_SANITIZE_SPECIAL_CHARS);

// Integer range
$age = filter_var($_POST['age'], FILTER_VALIDATE_INT, [
    'options' => ['min_range' => 1, 'max_range' => 150]
]);

// Whitelist allowed values
$allowed = ['asc', 'desc'];
$order   = in_array($_GET['order'] ?? '', $allowed) ? $_GET['order'] : 'asc';
```

---

## Debugging & Tools

**Definition:** Tools and techniques for finding and fixing bugs in PHP applications.

### Debug Output
**Definition:** Inspect variables and state during development.
```php
var_dump($var);         // Type + value — most informative
print_r($arr);          // Human-readable — good for arrays
var_export($var);       // Valid PHP syntax output

// Formatted debug output
echo '<pre>' . print_r($arr, true) . '</pre>';
echo '<pre>' . var_export($arr, true) . '</pre>';

// Die with dump (quick debug)
die(var_dump($data));

// Xdebug helper (if installed)
xdebug_var_dump($var);
```

### Error Reporting
**Definition:** Control which PHP errors are shown — important for development vs production.
```php
// Development — show all errors
error_reporting(E_ALL);
ini_set('display_errors', '1');
ini_set('display_startup_errors', '1');

// Production — log errors, don't display
error_reporting(E_ALL);
ini_set('display_errors', '0');
ini_set('log_errors', '1');
ini_set('error_log', '/path/to/error.log');

// PHP error levels
E_ERROR        // Fatal runtime errors
E_WARNING      // Non-fatal warnings
E_NOTICE       // Notices (undefined variables etc.)
E_DEPRECATED   // Deprecated features
E_ALL          // All errors, warnings, and notices
```

### PHP CLI
**Definition:** Run PHP from the command line — great for scripts and testing.
```bash
php script.php                    # Run a script
php -r "echo phpversion();"       # Run one-liner
php -l script.php                 # Lint (syntax check only)
php -a                            # Interactive REPL shell
php --ini                         # Show loaded php.ini
php -i | grep "extension"        # Show configuration
php -m                            # List loaded modules/extensions
php artisan migrate               # Laravel Artisan
php composer.phar install         # Run Composer
```

### Useful php.ini Settings
**Definition:** Important configuration options for development and production.
```ini
; Memory and execution
memory_limit      = 256M
max_execution_time = 30
max_input_time    = 60

; File uploads
upload_max_filesize = 10M
post_max_size      = 12M
max_file_uploads   = 20

; Error handling
display_errors     = Off     ; Production: Off, Development: On
log_errors         = On
error_log          = /var/log/php_errors.log

; Sessions
session.cookie_secure   = 1   ; HTTPS only
session.cookie_httponly = 1   ; No JS access
session.cookie_samesite = Lax

; Timezone
date.timezone = Asia/Kolkata
```

---

## Best Practices

**Definition:** Guidelines for writing clean, secure, maintainable, and professional PHP code.

### Code Style (PSR Standards)
**Definition:** Follow PSR (PHP Standards Recommendations) for consistent, interoperable code.
```php
<?php
// PSR-12: Extended Coding Style

declare(strict_types=1);    // Use strict types

namespace App\Services;

use App\Models\User;
use InvalidArgumentException;

class UserService
{
    // Constructor property promotion (PHP 8+)
    public function __construct(
        private readonly UserRepository $repository,
        private readonly EmailService   $emailService,
    ) {}

    // Method naming: camelCase
    public function createUser(string $name, string $email): User
    {
        // Constants: UPPER_SNAKE_CASE
        if (strlen($name) > self::MAX_NAME_LENGTH) {
            throw new InvalidArgumentException("Name too long");
        }

        $user = new User($name, $email);
        $this->repository->save($user);
        $this->emailService->sendWelcome($user);

        return $user;
    }
}
```

### Type Safety
**Definition:** Use type declarations everywhere — catch bugs at the type level.
```php
// Always use type hints
function greet(string $name, int $age): string {
    return "Hello $name, you are $age years old";
}

// Use strict types
declare(strict_types=1);
greet(42, "test");   // TypeError in strict mode

// Use nullable types properly
function findUser(?int $id): ?User {
    if ($id === null) return null;
    return $this->repository->find($id);
}

// Return type declarations
function getUsers(): array { }
function getUser(): User { }
function maybeUser(): ?User { }
```

### Modern PHP Patterns
**Definition:** Use modern PHP features for cleaner, more expressive code.
```php
// Use match instead of switch
$label = match($status) {
    'active'   => 'Active',
    'inactive' => 'Inactive',
    default    => throw new InvalidArgumentException("Unknown status: $status"),
};

// Use null coalescing
$name = $user['name'] ?? 'Anonymous';
$config['timeout'] ??= 30;

// Use spread operator
$merged = [...$defaultConfig, ...$userConfig];

// Use array destructuring
[$first, $second] = $array;
['name' => $name, 'age' => $age] = $user;

// Use short closures
$doubled = array_map(fn($n) => $n * 2, $numbers);

// Use named arguments for clarity
setcookie(name: 'theme', value: 'dark', expires: time() + 86400, path: '/', secure: true);

// Use constructor promotion
class Config {
    public function __construct(
        public readonly string $host,
        public readonly int    $port = 3306,
        public readonly string $name = 'mydb',
    ) {}
}
```

### Summary of Rules

* Use **`declare(strict_types=1)`** at the top of every file
* Always use **prepared statements** — never interpolate user input into SQL
* **Escape all output** with `htmlspecialchars()` — prevent XSS
* **Hash passwords** with `password_hash()` — never store plain text
* Use **`===` strict equality** — avoid type juggling surprises
* Use **namespaces and autoloading** — never use `require`/`include` manually
* Use **type declarations** on all function parameters and return types
* Use **Composer** for all dependencies — no manual library management
* Never trust **`$_GET`, `$_POST`, `$_COOKIE`** — always validate and sanitize
* Use **`null coalescing ??`** instead of `isset()` checks
