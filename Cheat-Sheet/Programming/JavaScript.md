## Introduction

**JavaScript** is a lightweight, interpreted, multi-paradigm programming language created by **Brendan Eich** in **1995**. It is the only programming language that runs natively in web browsers — making it the backbone of interactive web applications. JavaScript can manipulate HTML and CSS, respond to user events, fetch data from servers, and much more. With **Node.js**, JavaScript also runs on the server side. The modern standard is **ES6+** (ECMAScript 2015 and beyond) which brought classes, arrow functions, promises, modules, and many other powerful features.

## Basic Syntax

**Definition:** JavaScript runs in the browser or Node.js — it is case-sensitive and uses C-style syntax.

### Hello World
**Definition:** The simplest JavaScript program — display a message to the console or browser.
```javascript
console.log("Hello, World!");       // Print to browser console
alert("Hello!");                    // Browser popup (avoid in production)
document.write("Hello!");           // Write directly to HTML (avoid)
```

### Statements & Semicolons
**Definition:** Each statement is one instruction — semicolons are optional but recommended.
```javascript
let name = "Dark";                  // Statement with semicolon
let age = 25                        // Semicolon optional — but add it for safety
console.log(name, age)
```

### Comments
**Definition:** Comments are ignored by the engine — use them to explain your code.
```javascript
// This is a single-line comment

/*
  This is a
  multi-line comment
*/

/**
 * JSDoc comment — used for documentation
 * @param {string} name - The user's name
 * @returns {string} A greeting message
 */
function greet(name) {
    return `Hello, ${name}!`;
}
```

---

## Variables

**Definition:** Variables store data — use `const` by default, `let` when the value changes, never `var`.

### const
**Definition:** A constant reference — cannot be reassigned. Use for most things.
```javascript
const name = "Dark";
const PI   = 3.14159;
const user = { name: "Dark", age: 25 };   // Object — const means the reference
                                           // is fixed, not the contents

// name = "Other";  // TypeError — cannot reassign const
user.age = 26;      // OK — modifying object content is allowed
```

### let
**Definition:** A block-scoped variable — use when the value needs to change.
```javascript
let count = 0;
count = 1;          // OK — can reassign
count++;            // OK — increment

let score;          // Declared but undefined
score = 100;        // Assign later
```

### var (Avoid)
**Definition:** Old way — function-scoped, hoisted, and error-prone. Avoid in modern JS.
```javascript
var x = 10;         // Function-scoped — leaks out of blocks
// Use let/const instead
```

### var vs let vs const
**Definition:** Key differences to understand when choosing which declaration to use.

| | `var` | `let` | `const` |
|--|-------|-------|---------|
| Scope | Function | Block | Block |
| Reassignable | Yes | Yes | No |
| Hoisted | Yes (undefined) | Yes (TDZ) | Yes (TDZ) |
| Use today | ❌ Avoid | ✅ When value changes | ✅ Default choice |

---

## Data Types

**Definition:** JavaScript has 8 data types — 7 primitives and 1 object type.

### Primitive Types
**Definition:** Primitive values are immutable — they are stored and compared by value.
```javascript
let str     = "Hello";              // String
let num     = 42;                   // Number (integers and floats)
let float   = 3.14;                 // Number
let big     = 9007199254740991n;    // BigInt (very large numbers)
let bool    = true;                 // Boolean
let nothing = null;                 // Null — intentional absence of value
let undef   = undefined;            // Undefined — not yet assigned
let sym     = Symbol("id");         // Symbol — unique identifier
```

### Object Type
**Definition:** Objects, arrays, and functions are all objects — stored and compared by reference.
```javascript
let obj  = { name: "Dark" };        // Object
let arr  = [1, 2, 3];              // Array (special object)
let fn   = function() {};           // Function (callable object)
let date = new Date();              // Date object
```

### Checking Types
**Definition:** Use `typeof` for primitives — `Array.isArray()` for arrays.
```javascript
typeof "hello"        // "string"
typeof 42             // "number"
typeof true           // "boolean"
typeof undefined      // "undefined"
typeof null           // "object" ← known bug in JS
typeof {}             // "object"
typeof []             // "object"
typeof function(){}   // "function"
typeof Symbol()       // "symbol"

Array.isArray([])     // true  — use this for arrays
Array.isArray({})     // false
```

---

## Type Conversion

**Definition:** Convert values between types — explicitly (you do it) or implicitly (JS does it automatically).

### To String
**Definition:** Convert any value to a string.
```javascript
String(42)            // "42"
String(true)          // "true"
String(null)          // "null"
String(undefined)     // "undefined"
(42).toString()       // "42"
(255).toString(16)    // "ff" — hexadecimal
(8).toString(2)       // "1000" — binary
```

### To Number
**Definition:** Convert a value to a number — `NaN` (Not a Number) if conversion fails.
```javascript
Number("42")          // 42
Number("3.14")        // 3.14
Number("")            // 0
Number("abc")         // NaN
Number(true)          // 1
Number(false)         // 0
Number(null)          // 0
Number(undefined)     // NaN

parseInt("42px")      // 42   — parse integer, stop at non-numeric
parseFloat("3.14em")  // 3.14 — parse float, stop at non-numeric
parseInt("0xFF", 16)  // 255  — parse hexadecimal
```

### To Boolean
**Definition:** Convert to true or false — falsy values become `false`, everything else `true`.
```javascript
Boolean(0)          // false
Boolean("")         // false
Boolean(null)       // false
Boolean(undefined)  // false
Boolean(NaN)        // false
Boolean(false)      // false

Boolean(1)          // true
Boolean("hello")    // true
Boolean([])         // true  ← empty array is truthy!
Boolean({})         // true  ← empty object is truthy!
```

### Implicit Coercion
**Definition:** JavaScript automatically converts types in certain operations — can be surprising.
```javascript
"5" + 3       // "53"  — number becomes string (+ with string = concat)
"5" - 3       // 2     — string becomes number (- always numeric)
"5" * "3"     // 15    — both become numbers
true + 1      // 2     — true becomes 1
false + 1     // 1     — false becomes 0
null + 1      // 1     — null becomes 0
```

---

## String Operations

**Definition:** Strings are immutable sequences of characters — many built-in methods help manipulate them.

### Basic Info
**Definition:** Get the length or transform the case of a string.
```javascript
const s = "Hello, World!";
s.length              // 13
s.toUpperCase()       // "HELLO, WORLD!"
s.toLowerCase()       // "hello, world!"
```

### Search & Check
**Definition:** Find out if a string contains, starts with, or ends with a value.
```javascript
s.includes("World")       // true
s.startsWith("Hello")     // true
s.endsWith("!")           // true
s.indexOf("World")        // 7  — first occurrence index (-1 if not found)
s.lastIndexOf("l")        // 10 — last occurrence index
```

### Extract & Slice
**Definition:** Pull out part of a string using position and length.
```javascript
s.slice(7, 12)            // "World"       — from 7 to 11
s.slice(7)                // "World!"      — from 7 to end
s.slice(-6)               // "World!"      — last 6 characters
s.substring(7, 12)        // "World"       — same as slice (no negative)
s.charAt(0)               // "H"           — character at index 0
s[0]                      // "H"           — bracket notation
```

### Modify & Clean
**Definition:** Replace parts of a string or remove whitespace.
```javascript
s.replace("World", "JS")          // "Hello, JS!"
s.replaceAll("l", "L")            // "HeLLo, WorLd!"
"  hello  ".trim()                // "hello"
"  hello  ".trimStart()           // "hello  "
"  hello  ".trimEnd()             // "  hello"
```

### Split, Join & Pad
**Definition:** Break strings into arrays, or build strings with padding.
```javascript
"a,b,c".split(",")                // ["a", "b", "c"]
"hello".split("")                 // ["h","e","l","l","o"]
["a","b","c"].join("-")           // "a-b-c"

"5".padStart(3, "0")              // "005"  — pad left to length 3
"5".padEnd(3, "0")                // "500"  — pad right to length 3
"ha".repeat(3)                    // "hahaha"
```

---

## Template Literals

**Definition:** Backtick strings that support variable interpolation and multi-line text — use them instead of concatenation.

### Basic Interpolation
**Definition:** Embed variables and expressions directly inside strings using `${}`.
```javascript
const name = "Dark";
const age  = 25;

// Old way — string concatenation
console.log("Hello, " + name + "! You are " + age + " years old.");

// Modern way — template literal
console.log(`Hello, ${name}! You are ${age} years old.`);
console.log(`Next year you'll be ${age + 1}.`);
console.log(`Today: ${new Date().toDateString()}`);
```

### Multi-line Strings
**Definition:** Write strings across multiple lines without `\n` escape characters.
```javascript
const html = `
  <div class="card">
    <h2>${name}</h2>
    <p>Age: ${age}</p>
  </div>
`;
```

### Tagged Templates
**Definition:** A function that processes a template literal — used in CSS-in-JS libraries like styled-components.
```javascript
function tag(strings, ...values) {
    return strings.reduce((result, str, i) =>
        result + str + (values[i] !== undefined ? values[i].toUpperCase() : ""), "");
}

const greeting = tag`Hello, ${name}! You are ${age} years old.`;
// Hello, DARK! You are 25 years old.
```

---

## Numbers & Math

**Definition:** JavaScript has one number type for both integers and decimals — plus the `Math` object.

### Number Properties
**Definition:** Special numeric values and limits built into JavaScript.
```javascript
Number.MAX_SAFE_INTEGER    // 9007199254740991
Number.MIN_SAFE_INTEGER    // -9007199254740991
Number.MAX_VALUE           // Largest possible number
Number.POSITIVE_INFINITY   // Infinity
Number.NEGATIVE_INFINITY   // -Infinity
Number.NaN                 // Not a Number
Number.isInteger(42)       // true
Number.isNaN(NaN)          // true
Number.isFinite(Infinity)  // false
```

### Math Object
**Definition:** Built-in object with math constants and functions.
```javascript
Math.PI            // 3.141592653589793
Math.E             // 2.718281828459045
Math.round(4.6)    // 5   — round to nearest
Math.floor(4.9)    // 4   — round down
Math.ceil(4.1)     // 5   — round up
Math.trunc(4.9)    // 4   — remove decimal (toward zero)
Math.abs(-5)       // 5   — absolute value
Math.pow(2, 10)    // 1024
Math.sqrt(144)     // 12
Math.cbrt(27)      // 3   — cube root
Math.max(3, 1, 4, 1, 5)   // 5
Math.min(3, 1, 4, 1, 5)   // 1
Math.sign(-5)      // -1  — sign of number (-1, 0, 1)
Math.log(Math.E)   // 1   — natural log
Math.log2(8)       // 3
Math.log10(1000)   // 3
```

### Random Numbers
**Definition:** Generate random numbers — combine with `floor` and `ceil` for integers.
```javascript
Math.random()                       // 0 to 0.999...
Math.random() * 10                  // 0 to 9.999...
Math.floor(Math.random() * 10)      // 0 to 9 (integer)
Math.floor(Math.random() * 10) + 1  // 1 to 10

// Random integer between min and max (inclusive)
function randomInt(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
}
randomInt(1, 6)    // Dice roll — 1 to 6
```

### Number Formatting
**Definition:** Control how numbers are displayed as strings.
```javascript
(3.14159).toFixed(2)        // "3.14"   — fixed decimal places
(1234567).toLocaleString()  // "1,234,567"
(0.00123).toExponential(2)  // "1.23e-3"
(255).toString(16)          // "ff"     — hex
(255).toString(2)           // "11111111" — binary
```

---

## Operators

**Definition:** Symbols that perform operations on values — arithmetic, assignment, and more.

### Arithmetic
**Definition:** Basic math operations.
```javascript
5 + 3     // 8   — addition
5 - 3     // 2   — subtraction
5 * 3     // 15  — multiplication
5 / 3     // 1.666... — division (always float)
5 % 3     // 2   — modulo (remainder)
5 ** 3    // 125 — exponentiation (power)

let x = 10;
x++       // Post-increment: returns 10, then x = 11
++x       // Pre-increment: x = 12, returns 12
x--       // Post-decrement
--x       // Pre-decrement
```

### Assignment
**Definition:** Shorthand operators to update a variable using its current value.
```javascript
let x = 10;
x += 5    // x = x + 5  → 15
x -= 3    // x = x - 3  → 12
x *= 2    // x = x * 2  → 24
x /= 4    // x = x / 4  → 6
x %= 4    // x = x % 4  → 2
x **= 3   // x = x ** 3 → 8
x &&= 5   // x = x && 5 → assign if x is truthy
x ||= 5   // x = x || 5 → assign if x is falsy
x ??= 5   // x = x ?? 5 → assign only if x is null/undefined
```

### Bitwise
**Definition:** Operate directly on 32-bit binary representations of numbers.
```javascript
5 & 3     // 1  — AND
5 | 3     // 7  — OR
5 ^ 3     // 6  — XOR
~5        // -6 — NOT
5 << 1    // 10 — left shift
5 >> 1    // 2  — right shift
5 >>> 1   // 2  — unsigned right shift
```

---

## Comparison & Equality

**Definition:** Compare values — always use `===` (strict) instead of `==` (loose) to avoid type coercion surprises.

### Strict vs Loose Equality
**Definition:** `===` checks value AND type — `==` converts types first (can cause bugs).
```javascript
// Strict equality (===) — recommended
5 === 5          // true
5 === "5"        // false — different types
null === null    // true
null === undefined  // false

// Loose equality (==) — avoid
5 == "5"         // true  — "5" is converted to 5
0 == false       // true  — false is converted to 0
0 == ""          // true  — "" is converted to 0
null == undefined   // true — special case
```

### Comparison Operators
**Definition:** Compare magnitude of values — works on numbers and strings.
```javascript
5 > 3      // true
5 < 3      // false
5 >= 5     // true
5 <= 4     // false

// String comparison — alphabetical (by character code)
"banana" > "apple"    // true
"Z" < "a"             // true — uppercase letters have lower char codes
```

### NaN Comparison
**Definition:** `NaN` is the only value that is not equal to itself — use `Number.isNaN()`.
```javascript
NaN === NaN         // false — NaN is never equal to anything!
NaN == NaN          // false
Number.isNaN(NaN)   // true  — correct way to check
isNaN("hello")      // true  — isNaN() converts first, less reliable
```

---

## Logical Operators

**Definition:** Combine conditions — also used for short-circuit evaluation and default values.

### Basic Logical Operators
**Definition:** Evaluate two conditions and return a boolean-like result.
```javascript
true && true     // true  — AND
true && false    // false
false || true    // true  — OR
false || false   // false
!true            // false — NOT
!false           // true
```

### Short-Circuit Evaluation
**Definition:** JS stops evaluating as soon as the result is determined — used for conditional execution.
```javascript
// && returns first falsy value, or the last value
false && "hello"     // false  — stops at false
0 && "hello"         // 0      — 0 is falsy
"yes" && "hello"     // "hello"— "yes" is truthy, return last

// || returns first truthy value, or the last value
false || "hello"     // "hello"
0 || "default"       // "default"
"yes" || "hello"     // "yes"  — first truthy wins
```

### Nullish Coalescing (??)
**Definition:** Return the right side only if left is `null` or `undefined` — unlike `||` which checks all falsy.
```javascript
null ?? "default"        // "default"
undefined ?? "default"   // "default"
0 ?? "default"           // 0    ← 0 is NOT null/undefined
"" ?? "default"          // ""   ← "" is NOT null/undefined
false ?? "default"       // false

// Practical use — safe default values
const name = user.name ?? "Anonymous";
const port = config.port ?? 3000;
```

### Optional Chaining (?.)
**Definition:** Safely access nested object properties — returns `undefined` instead of throwing an error.
```javascript
const user = { address: { city: "Mumbai" } };

user?.address?.city          // "Mumbai"
user?.phone?.number          // undefined — no error!
user?.greet?.()              // undefined — safe method call
user?.items?.[0]             // undefined — safe array access

// Without optional chaining — can crash
user.phone.number            // TypeError if phone is undefined
```

---

## If Statements

**Definition:** Execute different blocks of code based on conditions.

### Basic If / Else
**Definition:** The simplest form — one path if true, another if false.
```javascript
const age = 20;

if (age >= 18) {
    console.log("Adult");
} else {
    console.log("Minor");
}
```

### If / Else If / Else
**Definition:** Chain multiple conditions — first match runs, rest are skipped.
```javascript
const score = 75;

if (score >= 90) {
    console.log("A grade");
} else if (score >= 80) {
    console.log("B grade");
} else if (score >= 70) {
    console.log("C grade");
} else {
    console.log("F grade");
}
```

---

## Switch Statement

**Definition:** Match a value against multiple cases — cleaner than many `else if` chains.

### Basic Switch
**Definition:** Each `case` is compared with `===` — always add `break` to prevent fall-through.
```javascript
const day = "Monday";

switch (day) {
    case "Monday":
        console.log("Start of work week");
        break;
    case "Friday":
        console.log("End of work week");
        break;
    case "Saturday":
    case "Sunday":                          // Fall-through — same block for both
        console.log("Weekend!");
        break;
    default:
        console.log("Midweek");
}
```

---

## Ternary Operator

**Definition:** A compact one-line if/else — ideal for simple conditional expressions and assignments.

### Basic Ternary
**Definition:** `condition ? valueIfTrue : valueIfFalse` — returns one of two values.
```javascript
const age = 20;
const label = age >= 18 ? "Adult" : "Minor";
console.log(label);    // Adult

// In JSX / template literals
console.log(`You are ${age >= 18 ? "an adult" : "a minor"}.`);

// Nested (use sparingly — gets hard to read)
const grade = score >= 90 ? "A" : score >= 80 ? "B" : score >= 70 ? "C" : "F";
```

---

## While Loop

**Definition:** Repeat a block while a condition is true — checks condition before each iteration.

### Basic While
**Definition:** Runs as long as the condition is true — always update the condition inside.
```javascript
let count = 1;
while (count <= 5) {
    console.log(`Count: ${count}`);
    count++;                              // Prevent infinite loop
}
```

### Do...While
**Definition:** Runs at least once before checking — condition is evaluated after first execution.
```javascript
let count = 1;
do {
    console.log(`Count: ${count}`);
    count++;
} while (count <= 5);
```

---

## For Loop

**Definition:** Different `for` loop forms for different use cases — arrays, objects, iterables.

### Classic For Loop
**Definition:** Counter-based loop — best when you need the index.
```javascript
for (let i = 0; i < 5; i++) {
    console.log(i);               // 0, 1, 2, 3, 4
}

// Reverse loop
for (let i = 4; i >= 0; i--) {
    console.log(i);               // 4, 3, 2, 1, 0
}
```

### for...of
**Definition:** Iterate over values of any iterable — arrays, strings, Maps, Sets.
```javascript
const fruits = ["apple", "banana", "cherry"];

for (const fruit of fruits) {
    console.log(fruit);
}

// With string
for (const char of "Hello") {
    console.log(char);            // H, e, l, l, o
}

// With index using entries()
for (const [index, fruit] of fruits.entries()) {
    console.log(`${index}: ${fruit}`);
}
```

### for...in
**Definition:** Iterate over the keys of an object — avoid using on arrays.
```javascript
const user = { name: "Dark", age: 25, city: "Mumbai" };

for (const key in user) {
    console.log(`${key}: ${user[key]}`);
}
// name: Dark
// age: 25
// city: Mumbai
```

### forEach
**Definition:** Array method that runs a callback for each element — cannot use `break`.
```javascript
const nums = [1, 2, 3, 4, 5];

nums.forEach((num, index) => {
    console.log(`${index}: ${num}`);
});
```

---

## Loop Control

**Definition:** Keywords to control loop execution — skip, stop, or label nested loops.

### break
**Definition:** Exit the loop immediately — no more iterations run.
```javascript
for (let i = 0; i < 10; i++) {
    if (i === 5) break;           // Stop at 5 → prints 0 1 2 3 4
    console.log(i);
}
```

### continue
**Definition:** Skip the current iteration — jump straight to the next one.
```javascript
for (let i = 0; i < 10; i++) {
    if (i % 2 === 0) continue;   // Skip even → prints 1 3 5 7 9
    console.log(i);
}
```

### Labeled Loops
**Definition:** Name a loop so you can `break` or `continue` an outer loop from inside a nested one.
```javascript
outer: for (let i = 0; i < 3; i++) {
    for (let j = 0; j < 3; j++) {
        if (j === 1) break outer;     // Break the outer loop
        console.log(i, j);
    }
}
```

---

## Functions

**Definition:** Reusable blocks of code — JavaScript has several ways to define functions.

### Function Declaration
**Definition:** Classic function — hoisted so it can be called before it's defined.
```javascript
function greet(name) {
    return `Hello, ${name}!`;
}
greet("Dark");    // Hello, Dark! — can call before declaration
```

### Function Expression
**Definition:** A function assigned to a variable — not hoisted.
```javascript
const greet = function(name) {
    return `Hello, ${name}!`;
};
greet("Dark");
```

### Default Parameters
**Definition:** Provide fallback values used when an argument is not given or is `undefined`.
```javascript
function greet(name = "Stranger", greeting = "Hello") {
    return `${greeting}, ${name}!`;
}
greet()                    // Hello, Stranger!
greet("Dark")              // Hello, Dark!
greet("Dark", "Hi")        // Hi, Dark!
```

### Rest Parameters
**Definition:** Collect any number of remaining arguments into an array.
```javascript
function sum(...numbers) {
    return numbers.reduce((total, n) => total + n, 0);
}
sum(1, 2, 3)           // 6
sum(1, 2, 3, 4, 5)     // 15
```

### Return Multiple Values
**Definition:** Return multiple values as an array or object — destructure when calling.
```javascript
function minMax(arr) {
    return [Math.min(...arr), Math.max(...arr)];
}
const [min, max] = minMax([3, 1, 7, 2, 9]);

function getUser() {
    return { name: "Dark", age: 25 };
}
const { name, age } = getUser();
```

---

## Arrow Functions

**Definition:** Shorter function syntax using `=>` — does NOT have its own `this` context.

### Basic Arrow Function
**Definition:** Replace `function` keyword with `=>` — concise and modern.
```javascript
// Regular function
function add(a, b) { return a + b; }

// Arrow function
const add = (a, b) => a + b;      // Implicit return for single expression

const square = x => x * x;        // Single param — no parentheses needed
const greet  = () => "Hello!";    // No params — empty parens required

// Multi-line — use curly braces and explicit return
const multiply = (a, b) => {
    const result = a * b;
    return result;
};
```

### Arrow Function vs Regular
**Definition:** The key difference — arrow functions don't have their own `this`.
```javascript
// Regular function — this depends on how it's called
const obj = {
    name: "Dark",
    greet: function() {
        console.log(this.name);   // "Dark" — this = obj
    }
};

// Arrow function — this is inherited from surrounding scope
const obj2 = {
    name: "Dark",
    greet: () => {
        console.log(this.name);   // undefined — this = outer scope
    }
};

// Arrow functions are great for callbacks
[1, 2, 3].map(n => n * 2);       // [2, 4, 6]
```

---

## Scope

**Definition:** Where variables are accessible — global, function, or block scope.

### Global Scope
**Definition:** Variables declared outside all functions — accessible everywhere.
```javascript
const globalName = "Dark";        // Global

function test() {
    console.log(globalName);      // "Dark" — accessible inside function
}
```

### Function Scope
**Definition:** Variables declared inside a function — only accessible within that function.
```javascript
function myFunc() {
    const local = "I'm local";
    console.log(local);           // "I'm local"
}
// console.log(local);            // ReferenceError — not accessible outside
```

### Block Scope
**Definition:** `let` and `const` are block-scoped — accessible only within their `{}` block.
```javascript
if (true) {
    let blockVar = "inside block";
    const blockConst = "also inside";
    var funcVar = "function scoped";  // var leaks out of block!
}

// console.log(blockVar);   // ReferenceError
// console.log(blockConst); // ReferenceError
console.log(funcVar);       // "function scoped" — var leaks!
```

### Hoisting
**Definition:** Declarations are moved to the top of their scope — but only `var` gets initialized.
```javascript
// var is hoisted and initialized to undefined
console.log(x);       // undefined (not ReferenceError)
var x = 5;

// let/const are hoisted but in Temporal Dead Zone (TDZ)
// console.log(y);    // ReferenceError
let y = 5;

// Function declarations are fully hoisted
greet("Dark");        // Works! "Hello, Dark!"
function greet(name) { return `Hello, ${name}!`; }
```

---

## Closures

**Definition:** A function that remembers and can access variables from its outer scope even after the outer function has returned.

### Basic Closure
**Definition:** The inner function captures a reference to outer variables — they stay alive.
```javascript
function makeCounter() {
    let count = 0;                // Outer variable

    return function() {           // Inner function — closes over count
        count++;
        return count;
    };
}

const counter = makeCounter();
counter()    // 1
counter()    // 2
counter()    // 3
// count is private — cannot access it from outside!
```

### Closure with Arguments
**Definition:** Create customized functions by closing over different values.
```javascript
function multiplier(factor) {
    return (number) => number * factor;    // Closes over factor
}

const double = multiplier(2);
const triple = multiplier(3);

double(5)    // 10
triple(5)    // 15
```

### Practical Use
**Definition:** Closures enable data privacy, factory functions, and module patterns.
```javascript
function createUser(name) {
    let loginCount = 0;           // Private variable

    return {
        getName:  () => name,
        login:    () => { loginCount++; },
        getLogins: () => loginCount
    };
}

const user = createUser("Dark");
user.login();
user.login();
user.getLogins()    // 2
user.loginCount     // undefined — truly private!
```

---

## Arrays

**Definition:** Ordered lists of values — dynamic, mixed types allowed, zero-indexed.

### Create Array
**Definition:** Different ways to create arrays.
```javascript
const fruits  = ["apple", "banana", "cherry"];
const nums    = [1, 2, 3, 4, 5];
const mixed   = [1, "hello", true, null, { x: 1 }];
const empty   = [];
const filled  = new Array(5).fill(0);     // [0, 0, 0, 0, 0]
const range   = Array.from({length: 5}, (_, i) => i + 1);  // [1, 2, 3, 4, 5]
```

### Access & Info
**Definition:** Get items by index and inspect array properties.
```javascript
fruits[0]            // "apple"   — first
fruits[1]            // "banana"  — second
fruits[-1]           // undefined — JS doesn't support negative index directly
fruits.at(-1)        // "cherry"  — last item (ES2022 .at() method)
fruits.at(-2)        // "banana"  — second to last
fruits.length        // 3
```

### Add & Remove
**Definition:** Modify array contents by adding or removing items.
```javascript
fruits.push("mango")           // Add to END → returns new length
fruits.pop()                   // Remove from END → returns removed item
fruits.unshift("kiwi")        // Add to START → returns new length
fruits.shift()                 // Remove from START → returns removed item

// splice(start, deleteCount, ...itemsToAdd)
fruits.splice(1, 0, "grape")   // Insert "grape" at index 1
fruits.splice(1, 1)            // Remove 1 item at index 1
fruits.splice(1, 1, "peach")   // Replace item at index 1
```

### Search
**Definition:** Find items and their positions in an array.
```javascript
fruits.indexOf("banana")       // 1  — first index (-1 if not found)
fruits.lastIndexOf("apple")    // Last occurrence index
fruits.includes("cherry")      // true — membership check
fruits.find(f => f.length > 5) // First item matching condition
fruits.findIndex(f => f.length > 5)  // Index of first match
```

---

## Array Methods

**Definition:** Powerful built-in methods that transform, filter, and reduce arrays — most return a new array.

### map
**Definition:** Transform every item — returns a new array of the same length.
```javascript
const nums    = [1, 2, 3, 4, 5];
const doubled = nums.map(n => n * 2);          // [2, 4, 6, 8, 10]
const strings = nums.map(n => `Item ${n}`);    // ["Item 1", "Item 2", ...]
const users   = [{name: "Dark"}, {name: "Alice"}];
const names   = users.map(u => u.name);        // ["Dark", "Alice"]
```

### filter
**Definition:** Keep only items that pass a test — returns a new (possibly shorter) array.
```javascript
const evens  = nums.filter(n => n % 2 === 0);        // [2, 4]
const long   = fruits.filter(f => f.length > 5);     // ["banana", "cherry"]
const active = users.filter(u => u.active === true);
```

### reduce
**Definition:** Accumulate array values into a single result — sum, product, object, etc.
```javascript
const sum     = nums.reduce((acc, n) => acc + n, 0);   // 15
const product = nums.reduce((acc, n) => acc * n, 1);   // 120

// Count occurrences
const words = ["cat", "dog", "cat", "bird", "dog", "cat"];
const count = words.reduce((acc, word) => {
    acc[word] = (acc[word] || 0) + 1;
    return acc;
}, {});
// { cat: 3, dog: 2, bird: 1 }
```

### find & findIndex
**Definition:** Return the first item (or its index) that passes a test.
```javascript
const users = [{id: 1, name: "Dark"}, {id: 2, name: "Alice"}];
const user  = users.find(u => u.id === 1);          // {id: 1, name: "Dark"}
const idx   = users.findIndex(u => u.id === 1);     // 0
```

### some & every
**Definition:** `some` — at least one matches; `every` — all must match.
```javascript
nums.some(n => n > 4)     // true  — at least one is > 4
nums.every(n => n > 0)    // true  — all are > 0
nums.every(n => n > 3)    // false — not all are > 3
```

### flat & flatMap
**Definition:** `flat` flattens nested arrays — `flatMap` maps then flattens one level.
```javascript
[[1, 2], [3, 4], [5]].flat()           // [1, 2, 3, 4, 5]
[1, [2, [3, [4]]]].flat(Infinity)      // [1, 2, 3, 4] — all levels

const sentences = ["Hello World", "Foo Bar"];
sentences.flatMap(s => s.split(" "))   // ["Hello", "World", "Foo", "Bar"]
```

### sort
**Definition:** Sort array items — always provide a comparison function for numbers.
```javascript
["banana", "apple", "cherry"].sort()   // alphabetical: ["apple", "banana", "cherry"]

[10, 3, 21, 1].sort()                  // WRONG: ["1", "10", "21", "3"] — lexicographic!
[10, 3, 21, 1].sort((a, b) => a - b)  // CORRECT ascending: [1, 3, 10, 21]
[10, 3, 21, 1].sort((a, b) => b - a)  // Descending: [21, 10, 3, 1]

users.sort((a, b) => a.name.localeCompare(b.name))   // Sort objects by name
```

### Other Useful Methods
**Definition:** Additional array methods for common operations.
```javascript
[1, 2, 3].concat([4, 5])         // [1, 2, 3, 4, 5]
[1, 2, 3, 4, 5].slice(1, 3)     // [2, 3] — extract without modifying
Array.from("hello")              // ["h","e","l","l","o"]
Array.from({length: 3}, (_, i) => i)   // [0, 1, 2]
[1, [2], [[3]]].flat(2)          // [1, 2, 3]
nums.reverse()                   // Reverse in place (modifies original!)
[...new Set([1,2,2,3,3])]        // [1, 2, 3] — remove duplicates
```

---

## Objects

**Definition:** Key-value collections — the most important data structure in JavaScript.

### Create Object
**Definition:** Objects can be created with literals, constructors, or `Object.create()`.
```javascript
// Object literal — most common
const user = {
    name: "Dark",
    age: 25,
    "is-admin": true,                // Keys with special chars need quotes
    address: {                        // Nested object
        city: "Mumbai",
        country: "India"
    },
    greet() {                         // Method shorthand (ES6)
        return `Hello, ${this.name}`;
    }
};
```

### Access Properties
**Definition:** Get values using dot notation or bracket notation.
```javascript
user.name                // "Dark"    — dot notation
user["name"]             // "Dark"    — bracket notation
user["is-admin"]         // true      — brackets needed for special keys
user.address.city        // "Mumbai"  — chained access
user.greet()             // "Hello, Dark"

const key = "name";
user[key]                // "Dark" — dynamic key access
```

### Modify Object
**Definition:** Add, update, or delete properties on an object.
```javascript
user.email = "dark@email.com";        // Add new property
user.age = 26;                        // Update existing
delete user.age;                      // Remove property

// Check if property exists
"name" in user                        // true
user.hasOwnProperty("name")          // true
user.email !== undefined              // true (but risky — use 'in')
```

### Computed Property Names
**Definition:** Use expressions as property names using `[]` in an object literal.
```javascript
const key = "name";
const obj = {
    [key]: "Dark",                    // Same as name: "Dark"
    [`${key}_upper`]: "DARK"          // name_upper: "DARK"
};
```

### Property Shorthand
**Definition:** When variable name matches key name — write it once.
```javascript
const name = "Dark";
const age  = 25;

// Old way
const user = { name: name, age: age };

// Shorthand (ES6)
const user = { name, age };
```

---

## Object Methods

**Definition:** Built-in static methods on the `Object` class for inspecting and transforming objects.

### Keys, Values, Entries
**Definition:** Get arrays of an object's keys, values, or key-value pairs.
```javascript
const user = { name: "Dark", age: 25, city: "Mumbai" };

Object.keys(user)      // ["name", "age", "city"]
Object.values(user)    // ["Dark", 25, "Mumbai"]
Object.entries(user)   // [["name","Dark"], ["age",25], ["city","Mumbai"]]

// Loop with entries
for (const [key, value] of Object.entries(user)) {
    console.log(`${key}: ${value}`);
}
```

### Assign & Merge
**Definition:** Copy or merge properties from one or more objects.
```javascript
const defaults = { theme: "light", lang: "en" };
const prefs    = { lang: "hi", fontSize: 16 };

// Merge — later objects overwrite earlier
const config = Object.assign({}, defaults, prefs);
// { theme: "light", lang: "hi", fontSize: 16 }

// Spread (modern — preferred)
const config = { ...defaults, ...prefs };
```

### Freeze & Seal
**Definition:** Prevent modifications to an object.
```javascript
const config = Object.freeze({ pi: 3.14 });
config.pi = 3;          // Silently fails (or throws in strict mode)

const user = Object.seal({ name: "Dark" });
user.name = "Alice";    // OK — can change existing
user.age  = 25;         // Fails — cannot add new properties
```

### Create & Prototype
**Definition:** Create objects with a specific prototype or inspect them.
```javascript
const proto = {
    greet() { return `Hello, ${this.name}`; }
};
const obj = Object.create(proto);
obj.name = "Dark";
obj.greet()    // "Hello, Dark"

Object.getPrototypeOf(obj)      // proto
Object.hasOwn(obj, "name")      // true (ES2022 — preferred over hasOwnProperty)
```

---

## Destructuring

**Definition:** Extract values from arrays and objects into variables — concise and readable.

### Array Destructuring
**Definition:** Unpack array values into named variables by position.
```javascript
const [a, b, c] = [1, 2, 3];         // a=1, b=2, c=3
const [x, , z]  = [1, 2, 3];         // x=1, z=3 — skip middle
const [first, ...rest] = [1, 2, 3];  // first=1, rest=[2,3]

// Swap variables
let p = 1, q = 2;
[p, q] = [q, p];                      // p=2, q=1

// With defaults
const [m = 0, n = 0] = [5];          // m=5, n=0
```

### Object Destructuring
**Definition:** Unpack object properties into named variables.
```javascript
const user = { name: "Dark", age: 25, city: "Mumbai" };

const { name, age }    = user;         // name="Dark", age=25
const { name: n, age: a } = user;     // Rename — n="Dark", a=25
const { name, country = "India" } = user;  // Default value

// Nested destructuring
const { address: { city } } = { address: { city: "Mumbai" } };

// In function parameters
function greet({ name, age }) {
    return `${name} is ${age}`;
}
greet(user);
```

---

## Spread & Rest

**Definition:** `...` does two things — **spread** expands iterables, **rest** collects remaining items.

### Spread Operator
**Definition:** Expand an array or object into individual elements — great for copying and merging.
```javascript
// Spread in arrays
const a = [1, 2, 3];
const b = [4, 5, 6];
const merged = [...a, ...b];           // [1, 2, 3, 4, 5, 6]
const copy   = [...a];                 // [1, 2, 3] — shallow copy

// Spread in function calls
Math.max(...[3, 1, 4, 1, 5])          // 5 — same as Math.max(3,1,4,1,5)

// Spread in objects
const obj1 = { a: 1, b: 2 };
const obj2 = { b: 3, c: 4 };
const merged = { ...obj1, ...obj2 };   // { a: 1, b: 3, c: 4 }
```

### Rest Operator
**Definition:** Collect remaining items into an array — used in function parameters and destructuring.
```javascript
// Rest in function
function sum(first, ...others) {
    return first + others.reduce((a, b) => a + b, 0);
}
sum(1, 2, 3, 4)    // 10

// Rest in destructuring
const [head, ...tail] = [1, 2, 3, 4];  // head=1, tail=[2,3,4]
const { name, ...rest } = user;         // name="Dark", rest={age:25, city:"Mumbai"}
```

---

## Classes & OOP

**Definition:** ES6 classes provide syntactic sugar over prototype-based inheritance — cleaner OOP syntax.

### Define a Class
**Definition:** A class is a blueprint — `constructor` runs when an object is created with `new`.
```javascript
class Person {
    constructor(name, age) {        // Runs on: new Person()
        this.name = name;
        this.age  = age;
    }

    greet() {                       // Instance method
        return `Hi, I'm ${this.name}`;
    }

    getAge() {
        return this.age;
    }
}

const p1 = new Person("Dark", 25);
p1.greet()     // "Hi, I'm Dark"
p1.age         // 25
```

### Static Methods & Properties
**Definition:** Belong to the class itself — not to instances. Call with `ClassName.method()`.
```javascript
class MathUtils {
    static PI = 3.14159;

    static add(a, b) { return a + b; }
    static multiply(a, b) { return a * b; }
}

MathUtils.add(3, 4)     // 7
MathUtils.PI            // 3.14159
// new MathUtils().add() — instances don't have static methods
```

### Getters & Setters
**Definition:** Define computed properties that look like regular properties but run functions.
```javascript
class Circle {
    constructor(radius) {
        this._radius = radius;
    }

    get radius() { return this._radius; }

    set radius(value) {
        if (value < 0) throw new Error("Radius cannot be negative");
        this._radius = value;
    }

    get area() {
        return Math.PI * this._radius ** 2;
    }
}

const c = new Circle(5);
c.radius        // 5  — calls getter
c.radius = 10;  // calls setter — validates first
c.area          // 314.159... — computed property
```

### Private Fields (ES2022)
**Definition:** Truly private class fields using `#` prefix — cannot be accessed from outside.
```javascript
class BankAccount {
    #balance = 0;                           // Private field

    deposit(amount) { this.#balance += amount; }
    withdraw(amount) {
        if (amount > this.#balance) throw new Error("Insufficient funds");
        this.#balance -= amount;
    }
    get balance() { return this.#balance; }
}

const account = new BankAccount();
account.deposit(100);
account.balance      // 100
account.#balance     // SyntaxError — cannot access private field
```

---

## Prototypes

**Definition:** Every JavaScript object has a prototype — the mechanism behind inheritance.

### Prototype Chain
**Definition:** When you access a property, JS looks up the prototype chain until it finds it or reaches `null`.
```javascript
function Animal(name) {
    this.name = name;
}

Animal.prototype.speak = function() {
    return `${this.name} makes a sound.`;
};

const dog = new Animal("Rex");
dog.speak()            // "Rex makes a sound." — found on prototype
dog.hasOwnProperty("name")    // true  — own property
dog.hasOwnProperty("speak")   // false — inherited from prototype
```

### Prototype Inspection
**Definition:** Inspect and modify prototype chains.
```javascript
Object.getPrototypeOf(dog)     // Animal.prototype
dog instanceof Animal          // true
dog instanceof Object          // true — everything inherits from Object
```

---

## Error Handling

**Definition:** Catch and respond to runtime errors gracefully — prevent crashes and help with debugging.

### Try / Catch / Finally
**Definition:** Wrap risky code in `try` — errors are caught in `catch` — `finally` always runs.
```javascript
try {
    const result = JSON.parse("invalid json");
} catch (error) {
    console.error(`Error: ${error.message}`);
    console.error(error.stack);             // Full stack trace
} finally {
    console.log("Always runs");             // Cleanup code
}
```

### Throw Errors
**Definition:** Manually create and throw errors — use built-in error types or custom ones.
```javascript
function divide(a, b) {
    if (typeof a !== "number") throw new TypeError("a must be a number");
    if (b === 0) throw new RangeError("Cannot divide by zero");
    return a / b;
}

try {
    divide(10, 0);
} catch (e) {
    if (e instanceof RangeError) console.log("Range error:", e.message);
    else throw e;                           // Re-throw unexpected errors
}
```

### Custom Errors
**Definition:** Create your own error classes for application-specific error types.
```javascript
class ValidationError extends Error {
    constructor(message, field) {
        super(message);
        this.name  = "ValidationError";
        this.field = field;
    }
}

class NetworkError extends Error {
    constructor(message, statusCode) {
        super(message);
        this.name       = "NetworkError";
        this.statusCode = statusCode;
    }
}

try {
    throw new ValidationError("Email is required", "email");
} catch (e) {
    if (e instanceof ValidationError) {
        console.log(`Field ${e.field}: ${e.message}`);
    }
}
```

### Error Types
**Definition:** Built-in error types for different situations.

| Error Type | When it occurs |
|------------|---------------|
| `Error` | Generic base error |
| `TypeError` | Wrong type — e.g. calling non-function |
| `RangeError` | Value out of range — e.g. invalid array length |
| `ReferenceError` | Variable not defined |
| `SyntaxError` | Invalid JavaScript syntax |
| `URIError` | Invalid URI encoding/decoding |
| `EvalError` | Error in `eval()` function |

---

## Promises

**Definition:** An object representing the eventual result of an async operation — pending, fulfilled, or rejected.

### Create a Promise
**Definition:** Wrap an async operation in a `Promise` — call `resolve` on success, `reject` on failure.
```javascript
const myPromise = new Promise((resolve, reject) => {
    const success = true;

    if (success) {
        resolve("Operation succeeded!");    // Fulfilled
    } else {
        reject(new Error("Operation failed!"));   // Rejected
    }
});
```

### Consume a Promise
**Definition:** Use `.then()` for success, `.catch()` for errors, `.finally()` for cleanup.
```javascript
myPromise
    .then(result => console.log(result))        // "Operation succeeded!"
    .catch(error => console.error(error))
    .finally(() => console.log("Done"));
```

### Promise Chaining
**Definition:** Chain `.then()` calls — each returns a new promise, enabling sequential async operations.
```javascript
fetch("/api/user")
    .then(response => response.json())
    .then(user => fetch(`/api/posts/${user.id}`))
    .then(response => response.json())
    .then(posts => console.log(posts))
    .catch(error => console.error("Error:", error));
```

### Promise Combinators
**Definition:** Run multiple promises together — different strategies for different use cases.
```javascript
// All resolve — fails if any one rejects
Promise.all([p1, p2, p3])
    .then(([r1, r2, r3]) => console.log(r1, r2, r3));

// All settle — never rejects, gives result of each
Promise.allSettled([p1, p2, p3])
    .then(results => results.forEach(r => console.log(r.status)));

// First to resolve — ignores rejections
Promise.any([p1, p2, p3])
    .then(first => console.log(first));

// First to settle — resolve OR reject
Promise.race([p1, p2, p3])
    .then(first => console.log(first));
```

---

## Async / Await

**Definition:** Syntactic sugar over promises — write async code that reads like synchronous code.

### Basic Async / Await
**Definition:** `async` marks a function as asynchronous — `await` pauses execution until a promise resolves.
```javascript
async function fetchUser(id) {
    const response = await fetch(`/api/users/${id}`);
    const user     = await response.json();
    return user;
}

// Call an async function
fetchUser(1).then(user => console.log(user));
```

### Error Handling with Async/Await
**Definition:** Use `try/catch` to handle errors in async functions.
```javascript
async function loadData() {
    try {
        const response = await fetch("/api/data");

        if (!response.ok) {
            throw new Error(`HTTP error: ${response.status}`);
        }

        const data = await response.json();
        return data;
    } catch (error) {
        console.error("Failed:", error.message);
        throw error;                        // Re-throw if needed
    } finally {
        console.log("Request completed");
    }
}
```

### Parallel Requests
**Definition:** Use `Promise.all` with `await` to run multiple async operations at the same time.
```javascript
async function loadAll() {
    // Sequential — slow (waits for each)
    const user  = await fetchUser(1);
    const posts = await fetchPosts(1);

    // Parallel — fast (runs simultaneously)
    const [user, posts] = await Promise.all([
        fetchUser(1),
        fetchPosts(1)
    ]);

    return { user, posts };
}
```

---

## Fetch API

**Definition:** Modern built-in API for making HTTP requests — returns Promises, replaces XMLHttpRequest.

### GET Request
**Definition:** Fetch data from a server — the default method is GET.
```javascript
async function getUser(id) {
    const response = await fetch(`https://api.example.com/users/${id}`);

    if (!response.ok) {
        throw new Error(`Error: ${response.status}`);
    }

    const user = await response.json();
    return user;
}
```

### POST Request
**Definition:** Send data to a server — specify method, headers, and body.
```javascript
async function createUser(userData) {
    const response = await fetch("https://api.example.com/users", {
        method:  "POST",
        headers: { "Content-Type": "application/json" },
        body:    JSON.stringify(userData)
    });

    const newUser = await response.json();
    return newUser;
}

createUser({ name: "Dark", email: "dark@email.com" });
```

### Other HTTP Methods
**Definition:** PUT, PATCH, and DELETE follow the same pattern as POST.
```javascript
// PUT — replace entire resource
await fetch(`/api/users/${id}`, {
    method:  "PUT",
    headers: { "Content-Type": "application/json" },
    body:    JSON.stringify(updatedUser)
});

// PATCH — partial update
await fetch(`/api/users/${id}`, {
    method:  "PATCH",
    headers: { "Content-Type": "application/json" },
    body:    JSON.stringify({ name: "New Name" })
});

// DELETE — remove resource
await fetch(`/api/users/${id}`, { method: "DELETE" });
```

### Response Methods
**Definition:** Parse the response body in different formats depending on what the server returns.
```javascript
response.json()        // Parse JSON body → object
response.text()        // Plain text body → string
response.blob()        // Binary data → Blob (images, files)
response.arrayBuffer() // Raw binary → ArrayBuffer

response.status        // HTTP status code (200, 404, 500...)
response.ok            // true if status 200-299
response.headers       // Response headers
```

---

## DOM Selection

**Definition:** Methods to find and select HTML elements from JavaScript — the foundation of DOM manipulation.

### Select Elements
**Definition:** Different methods to get references to HTML elements on the page.
```javascript
// By ID — returns single element
document.getElementById("header")

// By CSS selector — returns first match
document.querySelector(".card")
document.querySelector("#main h1")
document.querySelector("input[type='email']")

// By CSS selector — returns NodeList (all matches)
document.querySelectorAll(".card")
document.querySelectorAll("li")
document.querySelectorAll("p, h1, h2")

// By class name — returns HTMLCollection
document.getElementsByClassName("card")

// By tag name — returns HTMLCollection
document.getElementsByTagName("div")
```

### Traversing the DOM
**Definition:** Navigate from one element to its relatives in the DOM tree.
```javascript
const el = document.querySelector(".card");

el.parentElement          // Parent element
el.children               // Direct child elements
el.firstElementChild      // First child element
el.lastElementChild       // Last child element
el.nextElementSibling     // Next sibling element
el.previousElementSibling // Previous sibling element
el.closest(".container")  // Nearest ancestor matching selector
```

---

## DOM Manipulation

**Definition:** Create, modify, and delete HTML elements using JavaScript.

### Read & Write Content
**Definition:** Get or set the text and HTML inside elements.
```javascript
const el = document.querySelector("h1");

el.textContent           // Read text (safe — no HTML interpretation)
el.textContent = "New Heading"   // Write text (HTML is escaped)

el.innerHTML             // Read HTML including tags
el.innerHTML = "<span>Hello</span>"  // Write HTML (careful — XSS risk!)

el.innerText             // Like textContent but layout-aware
```

### Modify Attributes
**Definition:** Get, set, check, and remove HTML attributes.
```javascript
const img = document.querySelector("img");

img.getAttribute("src")          // Get attribute value
img.setAttribute("src", "new.jpg")  // Set attribute
img.removeAttribute("alt")       // Remove attribute
img.hasAttribute("src")          // Check if attribute exists

// Properties (faster than getAttribute for common attrs)
img.src = "photo.jpg";
img.alt = "A photo";
img.id  = "main-photo";
```

### Classes
**Definition:** Add, remove, toggle, and check CSS classes on elements.
```javascript
const el = document.querySelector(".card");

el.classList.add("active")           // Add class
el.classList.remove("active")        // Remove class
el.classList.toggle("active")        // Add if missing, remove if present
el.classList.contains("active")      // true/false — check
el.classList.replace("old", "new")   // Replace one class with another
el.className = "card active large"   // Set all classes at once
```

### Styles
**Definition:** Get and set CSS styles directly on elements.
```javascript
const el = document.querySelector("div");

el.style.color           = "red";
el.style.fontSize        = "18px";
el.style.backgroundColor = "blue";
el.style.display         = "none";   // Hide element
el.style.display         = "";       // Remove inline style (use CSS class)

// Read computed style (what's actually applied)
getComputedStyle(el).fontSize        // "18px" — actual computed value
```

### Create & Insert Elements
**Definition:** Build new elements and add them to the page.
```javascript
// Create
const div  = document.createElement("div");
const text = document.createTextNode("Hello");

// Add content
div.textContent = "Hello!";
div.classList.add("card");

// Insert into page
document.body.appendChild(div)          // Append to body
parent.insertBefore(div, sibling)       // Before a specific child
parent.append(div, text)                // Append multiple nodes/strings
parent.prepend(div)                     // Add at beginning
sibling.after(div)                      // After an element
sibling.before(div)                     // Before an element

// Efficient — build HTML string and set at once
container.innerHTML = `
    <div class="card">
        <h3>${name}</h3>
        <p>${description}</p>
    </div>
`;
```

### Remove Elements
**Definition:** Delete elements from the DOM.
```javascript
el.remove()                        // Remove element itself
parent.removeChild(child)          // Remove specific child
parent.innerHTML = ""              // Remove all children
```

---

## Events

**Definition:** JavaScript responds to user actions and browser events using event listeners.

### Add Event Listeners
**Definition:** Attach a function to run when an event happens — preferred over inline HTML handlers.
```javascript
const btn = document.querySelector("button");

// Add listener
btn.addEventListener("click", function(event) {
    console.log("Button clicked!");
    console.log(event.target);          // The element that was clicked
});

// Arrow function
btn.addEventListener("click", (e) => {
    console.log(e.target.textContent);
});

// Remove listener (must use named function)
function handleClick(e) { console.log("Clicked"); }
btn.addEventListener("click", handleClick);
btn.removeEventListener("click", handleClick);
```

### Common Events
**Definition:** Frequently used event types for user interaction.

| Event | Triggers when |
|-------|--------------|
| `click` | Element is clicked |
| `dblclick` | Element is double-clicked |
| `mouseover` | Mouse enters element |
| `mouseout` | Mouse leaves element |
| `mousemove` | Mouse moves over element |
| `keydown` | Key pressed down |
| `keyup` | Key released |
| `keypress` | Key pressed (deprecated) |
| `submit` | Form is submitted |
| `change` | Input value changed |
| `input` | Input value changes (real-time) |
| `focus` | Element gains focus |
| `blur` | Element loses focus |
| `load` | Page or image loaded |
| `DOMContentLoaded` | HTML parsed (before images) |
| `resize` | Browser window resized |
| `scroll` | Page or element scrolled |

### Event Object
**Definition:** The `event` object passed to every listener — contains info about what happened.
```javascript
document.addEventListener("keydown", (e) => {
    console.log(e.key)           // "a", "Enter", "ArrowLeft"...
    console.log(e.code)          // "KeyA", "Enter", "ArrowLeft"
    console.log(e.ctrlKey)       // true if Ctrl was held
    console.log(e.shiftKey)      // true if Shift was held
    console.log(e.altKey)        // true if Alt was held
});

document.addEventListener("click", (e) => {
    console.log(e.clientX, e.clientY)    // Mouse position
    console.log(e.target)                // Clicked element
    console.log(e.currentTarget)         // Element listener is attached to
});
```

### Event Propagation
**Definition:** Events bubble up from target to ancestors — stop with `stopPropagation()`.
```javascript
// Prevent default behavior (e.g. form submit, link follow)
form.addEventListener("submit", (e) => {
    e.preventDefault();
    // Handle form manually
});

// Stop event from bubbling to parent elements
child.addEventListener("click", (e) => {
    e.stopPropagation();
    // Parent click handler won't fire
});
```

### Event Delegation
**Definition:** Attach one listener to a parent to handle events from all current and future children.
```javascript
// Without delegation — attach to every item (bad for dynamic lists)
document.querySelectorAll("li").forEach(li => {
    li.addEventListener("click", handleClick);
});

// With delegation — one listener on parent (efficient)
document.querySelector("ul").addEventListener("click", (e) => {
    if (e.target.tagName === "LI") {
        console.log("Clicked:", e.target.textContent);
    }
});
```

---

## Local Storage & Session Storage

**Definition:** Browser storage for persisting data — `localStorage` survives page closes, `sessionStorage` does not.

### Local Storage
**Definition:** Stores key-value pairs that persist indefinitely until cleared manually.
```javascript
// Store
localStorage.setItem("username", "Dark");
localStorage.setItem("settings", JSON.stringify({ theme: "dark" }));

// Read
localStorage.getItem("username")         // "Dark"
const settings = JSON.parse(localStorage.getItem("settings"));

// Remove
localStorage.removeItem("username");
localStorage.clear();                    // Remove everything

// Check all keys
localStorage.length                      // Number of items
localStorage.key(0)                      // First key name
```

### Session Storage
**Definition:** Same API as localStorage — but data is cleared when the tab or browser closes.
```javascript
sessionStorage.setItem("token", "abc123");
sessionStorage.getItem("token")          // "abc123"
sessionStorage.removeItem("token");
sessionStorage.clear();
```

---

## JSON

**Definition:** JavaScript Object Notation — lightweight text format for data exchange between systems.

### Stringify (JS → JSON)
**Definition:** Convert a JavaScript value to a JSON string for storage or transmission.
```javascript
const user = { name: "Dark", age: 25, active: true };

JSON.stringify(user)                   // '{"name":"Dark","age":25,"active":true}'
JSON.stringify(user, null, 2)          // Pretty-printed with 2-space indent
JSON.stringify(user, ["name", "age"])  // Only include specific keys
JSON.stringify(user, (key, val) =>
    typeof val === "number" ? val * 2 : val)  // Replacer function
```

### Parse (JSON → JS)
**Definition:** Convert a JSON string back into a JavaScript value.
```javascript
const json = '{"name":"Dark","age":25}';

const obj = JSON.parse(json);
obj.name    // "Dark"
obj.age     // 25

// With reviver function
JSON.parse(json, (key, value) => {
    if (key === "age") return value + 1;
    return value;
});
```

---

## Modules (ES6)

**Definition:** Split code into separate files — use `export` to share, `import` to use.

### Named Exports
**Definition:** Export multiple items by name — import using the exact same names.
```javascript
// math.js
export const PI = 3.14159;
export function add(a, b) { return a + b; }
export function multiply(a, b) { return a * b; }

// main.js
import { PI, add, multiply } from "./math.js";
import { add as sum }        from "./math.js";  // Rename on import
import * as math             from "./math.js";  // Import everything as object
math.add(2, 3);
```

### Default Export
**Definition:** One default export per file — import with any name you choose.
```javascript
// utils.js
export default function greet(name) {
    return `Hello, ${name}!`;
}

// main.js
import greet          from "./utils.js";   // Any name works
import sayHello       from "./utils.js";   // Same thing, different name
import greet, { PI } from "./utils.js";   // Default + named together
```

---

## Regular Expressions

**Definition:** Patterns for searching and manipulating strings — created with `/pattern/flags`.

### Create & Test
**Definition:** Create a regex and test whether a string matches the pattern.
```javascript
const regex = /hello/i;               // Literal — i flag = case insensitive
const regex = new RegExp("hello", "i"); // Constructor

regex.test("Hello World")              // true — pattern found
regex.test("Goodbye")                  // false

"Hello World".match(/hello/i)          // ["Hello", ...] — match result
"Hello World".search(/world/i)         // 6 — index of match
"Hello World".replace(/world/i, "JS")  // "Hello JS"
```

### Common Patterns
**Definition:** Frequently used regex patterns for real-world tasks.
```javascript
/^\d+$/               // Only digits
/^[a-zA-Z]+$/         // Only letters
/^[\w.-]+@[\w.-]+\.\w{2,}$/   // Email
/^https?:\/\/[\w./%-]+$/      // URL
/^\d{3}-\d{3}-\d{4}$/        // Phone: 123-456-7890
/^(?=.*\d)(?=.*[a-z]).{8,}$/ // Password: 8+ chars, 1+ digit, 1+ lowercase
```

### Flags
**Definition:** Modifiers that change how the pattern matches.

| Flag | Meaning |
|------|---------|
| `i` | Case insensitive |
| `g` | Global — find all matches |
| `m` | Multiline — `^` and `$` match line start/end |
| `s` | `.` matches newlines too |
| `u` | Unicode mode |

### Capture Groups
**Definition:** Extract specific parts of a match using parentheses `()`.
```javascript
const date = "2025-01-15";
const [, year, month, day] = date.match(/(\d{4})-(\d{2})-(\d{2})/);
// year="2025", month="01", day="15"

// Named groups
const { groups: { y, m, d } } = "2025-01-15".match(
    /(?<y>\d{4})-(?<m>\d{2})-(?<d>\d{2})/
);
```

---

## Date & Time

**Definition:** Work with dates and times using the built-in `Date` object.

### Create Dates
**Definition:** Create a Date object for now or a specific point in time.
```javascript
new Date()                           // Current date and time
new Date("2025-01-15")               // From ISO string
new Date("January 15, 2025")         // From human-readable string
new Date(2025, 0, 15, 10, 30, 0)    // year, month(0-based), day, h, m, s
new Date(1705276200000)              // From Unix timestamp (ms)
Date.now()                           // Current timestamp in milliseconds
```

### Read Date Parts
**Definition:** Extract specific components from a Date object.
```javascript
const d = new Date("2025-01-15T10:30:00");

d.getFullYear()    // 2025
d.getMonth()       // 0  — 0-indexed! (0=Jan, 11=Dec)
d.getDate()        // 15 — day of month
d.getDay()         // 3  — day of week (0=Sun, 6=Sat)
d.getHours()       // 10
d.getMinutes()     // 30
d.getSeconds()     // 0
d.getTime()        // Unix timestamp in ms
```

### Format Dates
**Definition:** Convert a Date to a human-readable string in different formats.
```javascript
const d = new Date();

d.toISOString()                 // "2025-01-15T10:30:00.000Z"
d.toLocaleDateString()          // "1/15/2025" (locale-dependent)
d.toLocaleTimeString()          // "10:30:00 AM"
d.toLocaleString()              // "1/15/2025, 10:30:00 AM"

// Custom format using Intl
new Intl.DateTimeFormat("en-IN", {
    year: "numeric", month: "long", day: "numeric"
}).format(d)                    // "15 January 2025"
```

### Date Arithmetic
**Definition:** Calculate time differences and add/subtract time.
```javascript
const d1 = new Date("2025-01-01");
const d2 = new Date("2025-12-31");

const diffMs   = d2 - d1;                  // Milliseconds difference
const diffDays = diffMs / (1000*60*60*24); // Convert to days → 364

// Add days
const tomorrow = new Date(d1);
tomorrow.setDate(tomorrow.getDate() + 1);  // Mutates the date
```

---

## Iterators & Generators

**Definition:** Iterators produce values one at a time — generators are functions that yield values lazily.

### Iterators
**Definition:** Any object with a `next()` method that returns `{ value, done }`.
```javascript
function createRange(start, end) {
    let current = start;
    return {
        next() {
            if (current <= end) {
                return { value: current++, done: false };
            }
            return { value: undefined, done: true };
        }
    };
}

const range = createRange(1, 3);
range.next()    // { value: 1, done: false }
range.next()    // { value: 2, done: false }
range.next()    // { value: 3, done: false }
range.next()    // { value: undefined, done: true }
```

### Generators
**Definition:** Functions using `function*` and `yield` — pause and resume execution.
```javascript
function* countdown(from) {
    while (from > 0) {
        yield from--;           // Pause here, return value
    }
    yield "Go!";
}

const gen = countdown(3);
gen.next()    // { value: 3, done: false }
gen.next()    // { value: 2, done: false }
gen.next()    // { value: 1, done: false }
gen.next()    // { value: "Go!", done: false }
gen.next()    // { value: undefined, done: true }

// Use with for...of
for (const val of countdown(3)) {
    console.log(val);    // 3, 2, 1, "Go!"
}
```

---

## Map & Set

**Definition:** `Map` is like an object but with any key type — `Set` is a collection of unique values.

### Map
**Definition:** Stores key-value pairs — any value (including objects) can be a key.
```javascript
const map = new Map();

// Set values
map.set("name", "Dark");
map.set(42, "answer");
map.set({id: 1}, "user object key");

// Get values
map.get("name")      // "Dark"
map.get(42)          // "answer"
map.has("name")      // true
map.size             // 3

// Delete
map.delete("name");

// Iterate
for (const [key, value] of map) {
    console.log(key, value);
}

map.keys()           // Iterator of keys
map.values()         // Iterator of values
map.entries()        // Iterator of [key, value] pairs

// Create from array
const map = new Map([["a", 1], ["b", 2]]);
```

### Set
**Definition:** A collection of unique values — duplicates are automatically removed.
```javascript
const set = new Set([1, 2, 3, 2, 1]);   // {1, 2, 3}

set.add(4)           // Add item
set.has(2)           // true
set.delete(2)        // Remove item
set.size             // 3

// Iterate
for (const val of set) {
    console.log(val);
}

// Convert to array
[...set]             // [1, 3, 4]
Array.from(set)      // [1, 3, 4]

// Remove duplicates from array
const unique = [...new Set([1, 2, 2, 3, 3, 3])];    // [1, 2, 3]

// Set operations
const a = new Set([1, 2, 3]);
const b = new Set([2, 3, 4]);
const union        = new Set([...a, ...b]);          // {1,2,3,4}
const intersection = new Set([...a].filter(x => b.has(x)));  // {2,3}
const difference   = new Set([...a].filter(x => !b.has(x))); // {1}
```

---

## Symbol & WeakMap

**Definition:** Advanced data types for unique identifiers and memory-efficient collections.

### Symbol
**Definition:** A unique, immutable primitive value — useful for object property keys that won't collide.
```javascript
const id1 = Symbol("id");
const id2 = Symbol("id");
id1 === id2          // false — every Symbol is unique

const user = {
    name: "Dark",
    [id1]: 42        // Symbol as property key — won't show in for...in
};

user[id1]            // 42
Object.keys(user)    // ["name"] — symbols are hidden from Object.keys
```

### WeakMap
**Definition:** Like Map but keys must be objects and entries are garbage-collected when key has no other reference.
```javascript
const cache = new WeakMap();

let obj = { name: "Dark" };
cache.set(obj, { data: "cached result" });
cache.get(obj)       // { data: "cached result" }

obj = null;          // The WeakMap entry is garbage collected automatically
```

### WeakSet
**Definition:** Like Set but holds objects weakly — entries auto-removed when object is garbage collected.
```javascript
const seen = new WeakSet();
let node = { id: 1 };

seen.add(node);
seen.has(node)       // true

node = null;         // Entry removed automatically
```

---

## Proxy & Reflect

**Definition:** `Proxy` intercepts object operations — `Reflect` provides methods matching those operations.

### Proxy
**Definition:** Wrap an object to intercept and customize fundamental operations like get, set, and delete.
```javascript
const user = { name: "Dark", age: 25 };

const proxy = new Proxy(user, {
    get(target, key) {
        console.log(`Getting ${key}`);
        return target[key];
    },
    set(target, key, value) {
        if (key === "age" && typeof value !== "number") {
            throw new TypeError("Age must be a number");
        }
        target[key] = value;
        return true;
    },
    has(target, key) {
        return key in target;
    }
});

proxy.name           // Logs "Getting name" → "Dark"
proxy.age = "old"    // TypeError
"name" in proxy      // true
```

---

## Useful Built-in Methods

**Definition:** Handy global functions and methods available everywhere in JavaScript.

### Console Methods
**Definition:** Different types of console output for debugging and logging.
```javascript
console.log("Regular log");
console.info("Informational");
console.warn("Warning message");
console.error("Error message");
console.table([{a: 1}, {a: 2}]);      // Display as table
console.group("Group label");         // Start indented group
console.groupEnd();
console.time("timer");                // Start timer
console.timeEnd("timer");             // Log elapsed time
console.count("label");               // Count how many times called
console.clear();                      // Clear console
```

### setTimeout & setInterval
**Definition:** Schedule code to run after a delay or repeatedly at intervals.
```javascript
// Run once after delay (ms)
const id = setTimeout(() => {
    console.log("Runs after 2 seconds");
}, 2000);

clearTimeout(id);      // Cancel before it fires

// Run repeatedly at interval
const intervalId = setInterval(() => {
    console.log("Runs every second");
}, 1000);

clearInterval(intervalId);    // Stop repeating

// Zero timeout — run in next event loop cycle
setTimeout(() => console.log("After current stack"), 0);
```

### Structured Clone
**Definition:** Deep clone any value — handles circular references and complex types.
```javascript
const original = { a: 1, nested: { b: [1, 2, 3] } };
const clone    = structuredClone(original);    // ES2022 — deep copy
clone.nested.b.push(4);
original.nested.b    // [1, 2, 3] — unaffected
```

---

## Debugging

**Definition:** Tools and techniques to find and fix JavaScript errors.

### Browser DevTools
**Definition:** Press `F12` in any browser to open developer tools — the most important debugging tool.
```javascript
// Console tab — run JS, see errors and logs
// Sources tab — set breakpoints and step through code
// Network tab — inspect HTTP requests
// Elements tab — inspect and edit DOM
```

### Breakpoints
**Definition:** Pause JavaScript execution at a specific line to inspect state.
```javascript
debugger;    // Breakpoint in code — pauses when DevTools is open

// Or set breakpoints in browser Sources tab by clicking line numbers
```

### Console Tricks
**Definition:** Useful console patterns for effective debugging.
```javascript
// Log with label
console.log({ user, score });     // {user: ..., score: ...} — shows names!

// Log at specific conditions
const DEBUG = true;
DEBUG && console.log("debug info");

// Measure performance
console.time("operation");
// ... your code ...
console.timeEnd("operation");     // "operation: 123ms"

// Trace where a function was called from
console.trace("trace label");
```

---

## Tips & Tricks

**Definition:** Useful JavaScript shortcuts that help write cleaner, more concise code.

### Useful Shorthands
**Definition:** Common patterns written in the most concise way.
```javascript
// Optional chaining + nullish coalescing
const city = user?.address?.city ?? "Unknown";

// Short circuit for conditional execution
isLoggedIn && loadDashboard();
hasError || showSuccess();

// Convert to number
+"42"              // 42  — unary plus
+true              // 1
+false             // 0

// Convert to boolean
!!0                // false
!!"hello"          // true
!!null             // false
!![]               // true

// Remove duplicates
[...new Set(arr)]

// Flatten one level
arr.flat()

// Object clone (shallow)
const copy = { ...original };

// Array clone
const copy = [...original];
```

### Array Tricks
**Definition:** Common array operations done elegantly.
```javascript
// Last item
arr.at(-1)
arr[arr.length - 1]

// Shuffle array (Fisher-Yates)
arr.sort(() => Math.random() - 0.5)

// Array of numbers
Array.from({ length: 10 }, (_, i) => i)   // [0,1,2,...,9]

// Sum array
arr.reduce((a, b) => a + b, 0)

// Chunk array into groups
const chunk = (arr, n) =>
    Array.from({ length: Math.ceil(arr.length / n) }, (_, i) =>
        arr.slice(i * n, i * n + n));
```

### Object Tricks
**Definition:** Useful patterns for working with objects.
```javascript
// Pick specific keys from object
const { name, age } = user;
const picked = { name, age };

// Omit key (exclude one property)
const { password, ...safe } = user;   // safe has everything except password

// Check if object is empty
Object.keys(obj).length === 0

// Deep clone
const deep = JSON.parse(JSON.stringify(obj));   // Simple objects only
const deep = structuredClone(obj);              // Modern, handles more types

// Group array by property (ES2024)
Object.groupBy(users, user => user.role);
```

---

## Best Practices

**Definition:** Guidelines for writing clean, maintainable, and reliable JavaScript.

### Variables & Naming
**Definition:** Meaningful names and appropriate declaration keywords make code self-documenting.
```javascript
// Use const by default, let when reassigning
const MAX_RETRIES = 3;       // UPPER_CASE for constants
let currentRetry  = 0;       // camelCase for variables

// Meaningful names
const u  = getData();        // Bad — unclear
const user = fetchUserById(id);  // Good — clear intent

// Avoid magic numbers
if (score > 75) pass();      // Bad — what is 75?
const PASS_SCORE = 75;
if (score > PASS_SCORE) pass();  // Good
```

### Functions
**Definition:** Small, focused functions that do one thing are easier to test and maintain.
```javascript
// Bad — does too many things
function processOrder(order) {
    // validate, calculate, save, email, log — too much!
}

// Good — each function has one responsibility
function validateOrder(order) { }
function calculateTotal(order) { }
function saveOrder(order) { }
function notifyCustomer(order) { }
```

### Async Code
**Definition:** Always handle promise rejections — unhandled rejections can crash Node.js apps.
```javascript
// Bad — no error handling
fetch("/api/data").then(r => r.json()).then(console.log);

// Good — always handle errors
async function loadData() {
    try {
        const res  = await fetch("/api/data");
        if (!res.ok) throw new Error(`HTTP ${res.status}`);
        return await res.json();
    } catch (err) {
        console.error("loadData failed:", err);
        throw err;
    }
}
```

### Equality & Comparisons
**Definition:** Use strict equality to avoid type coercion surprises.
```javascript
// Bad — loose equality
if (value == null) { }     // Matches both null AND undefined (maybe intentional)
if (value == 0) { }        // Matches 0, "", false, null...

// Good — strict equality
if (value === null) { }    // Exactly null
if (value === 0) { }       // Exactly 0

// Check for null or undefined
if (value == null) { }     // Acceptable shorthand for null/undefined check
if (value === null || value === undefined) { }  // Explicit
```

### Immutability
**Definition:** Avoid mutating arrays and objects — return new ones instead.
```javascript
// Bad — mutates original array
function addItem(arr, item) {
    arr.push(item);
    return arr;
}

// Good — returns new array
function addItem(arr, item) {
    return [...arr, item];
}

// Bad — mutates original object
function updateUser(user, newAge) {
    user.age = newAge;
    return user;
}

// Good — returns new object
function updateUser(user, newAge) {
    return { ...user, age: newAge };
}
```

### Summary of Rules

* Use `const` by default — `let` when value changes — never `var`
* Use `===` strict equality — never `==` loose equality
* Always handle Promise rejections with `try/catch` or `.catch()`
* Use `async/await` instead of raw `.then()` chains for readability
* Use optional chaining `?.` and nullish coalescing `??` for safe access
* Prefer array methods (`map`, `filter`, `reduce`) over manual `for` loops
* Keep functions small and focused — one responsibility each
* Use descriptive variable and function names — avoid single letters
* Avoid mutating function arguments — return new values
* Always add `alt` text and use semantic HTML when manipulating the DOM
