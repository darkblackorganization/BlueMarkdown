
## Introduction

**Java** is a high-level, class-based, object-oriented programming language developed by **James Gosling** at **Sun Microsystems** (now owned by Oracle) and released in **1995**. Java follows the principle of **"Write Once, Run Anywhere"** — code compiled to bytecode runs on any platform with a Java Virtual Machine (JVM). Java is statically typed, strongly typed, and platform-independent. It is widely used for **enterprise applications**, **Android development**, **web backends**, **big data**, and **microservices**. Major frameworks include Spring, Hibernate, and Maven. Java is one of the most popular programming languages in the world.

## Basic Syntax

**Definition:** Java programs are organized into classes — execution starts from the `main` method.

### Hello World
**Definition:** The simplest Java program — every Java file must have a class matching the filename.
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

### Compile & Run
**Definition:** Java compiles to bytecode (.class) which runs on the JVM.
```bash
javac HelloWorld.java    # Compile to bytecode
java HelloWorld          # Run the program
java -version            # Check installed version

# With classpath
javac -cp . HelloWorld.java
java -cp . HelloWorld
```

### Comments
**Definition:** Three types of comments — single-line, multi-line, and Javadoc for documentation.
```java
// Single-line comment

/*
 * Multi-line comment
 * spans multiple lines
 */

/**
 * Javadoc comment — generates documentation
 * @param name The user's name
 * @return A greeting string
 */
public String greet(String name) {
    return "Hello, " + name;
}
```

### Print Output
**Definition:** Different ways to print output to the console.
```java
System.out.println("Hello");              // Print + newline
System.out.print("Hello ");              // Print without newline
System.out.printf("Name: %s, Age: %d%n", name, age);  // Formatted
System.out.printf("Pi: %.2f%n", 3.14159);  // Pi: 3.14
String.format("Value: %d", 42);          // Format to string
System.err.println("Error message");      // Print to stderr
```

---

## Variables & Data Types

**Definition:** Java is statically typed — every variable must be declared with an explicit type.

### Primitive Types
**Definition:** Eight built-in primitive types — stored directly in memory, not objects.
```java
byte   b = 127;              // 8-bit  signed: -128 to 127
short  s = 32767;            // 16-bit signed: -32768 to 32767
int    i = 2147483647;       // 32-bit signed: ~2.1 billion
long   l = 9223372036854L;   // 64-bit signed: very large (note L suffix)
float  f = 3.14f;            // 32-bit float (note f suffix)
double d = 3.14159265358979; // 64-bit float (default for decimals)
char   c = 'A';              // 16-bit Unicode character
boolean ok = true;           // true or false

// Numeric literals for readability
int million  = 1_000_000;    // Underscores allowed in numbers
long bigNum  = 9_876_543_210L;
double pi    = 3.141_592_653;
int hex      = 0xFF;         // Hexadecimal = 255
int binary   = 0b1010;       // Binary = 10
```

### Variable Declaration
**Definition:** Declare before use — `var` (Java 10+) infers type from assigned value.
```java
int age = 25;                // Explicit type
String name = "Dark";        // Reference type

var count = 10;              // Type inferred as int (Java 10+)
var message = "Hello";       // Type inferred as String
var list = new ArrayList<String>(); // Inferred as ArrayList<String>

// Final variables (constants)
final int MAX_SIZE = 100;    // Cannot be reassigned
final String APP_NAME = "MyApp";
```

### Wrapper Classes
**Definition:** Object versions of primitives — needed for generics and collections.
```java
Integer  i = 42;             // Wrapper for int
Double   d = 3.14;           // Wrapper for double
Boolean  b = true;           // Wrapper for boolean
Character c = 'A';           // Wrapper for char
Long     l = 100L;           // Wrapper for long

// Autoboxing — auto-convert primitive to wrapper
int primitive = 5;
Integer boxed = primitive;   // Autoboxing

// Unboxing — auto-convert wrapper to primitive
Integer boxed2 = 10;
int prim2 = boxed2;          // Unboxing

// Useful methods
Integer.parseInt("42")       // String → int
Integer.toBinaryString(10)   // "1010"
Integer.MAX_VALUE            // 2147483647
Integer.MIN_VALUE            // -2147483648
Double.parseDouble("3.14")   // String → double
```

---

## Type Conversion

**Definition:** Convert between types — widening is automatic, narrowing requires explicit cast.

### Widening (Automatic)
**Definition:** Convert from smaller to larger type — safe, no data loss.
```java
int    i = 42;
long   l = i;        // int → long (automatic)
float  f = l;        // long → float (automatic)
double d = f;        // float → double (automatic)

// Order of widening:
// byte → short → int → long → float → double
```

### Narrowing (Explicit Cast)
**Definition:** Convert from larger to smaller type — requires cast, may lose data.
```java
double d = 3.99;
int    i = (int) d;     // 3 — decimal truncated, NOT rounded

long   l = 1000L;
int    n = (int) l;     // OK if value fits in int

double pi = 3.14;
int    x  = (int) pi;   // 3 — truncated
```

### String Conversions
**Definition:** Convert between strings and other types.
```java
// Primitive/Object → String
String s1 = String.valueOf(42);        // "42"
String s2 = String.valueOf(3.14);      // "3.14"
String s3 = Integer.toString(42);      // "42"
String s4 = "" + 42;                   // "42" — concatenation trick

// String → Primitive
int    i = Integer.parseInt("42");     // "42" → 42
double d = Double.parseDouble("3.14"); // "3.14" → 3.14
boolean b = Boolean.parseBoolean("true"); // "true" → true
long   l = Long.parseLong("123456789"); // "123456789" → 123456789
```

---

## String Operations

**Definition:** Strings in Java are immutable objects — the `String` class provides many useful methods.

### Create Strings
**Definition:** Two ways to create strings — literals use the string pool, `new` always creates a new object.
```java
String s1 = "Hello";           // String literal — uses pool
String s2 = new String("Hello"); // Always new object (avoid)
String s3 = "Hello, " + "World"; // Concatenation
String s4 = String.valueOf(42);   // From number

// Multiline (Java 15+)
String text = """
              Hello,
              World!
              """;
```

### Basic Info
**Definition:** Get information about a string's content.
```java
String s = "Hello, World!";

s.length()                    // 13
s.isEmpty()                   // false (length == 0)
s.isBlank()                   // false (Java 11+ — whitespace only?)
s.charAt(0)                   // 'H'
s.indexOf("World")            // 7 (-1 if not found)
s.lastIndexOf("l")            // 10
```

### Search & Check
**Definition:** Test string content for specific patterns or substrings.
```java
s.contains("World")           // true
s.startsWith("Hello")         // true
s.endsWith("!")               // true
s.matches("Hello.*")          // true (regex match)
s.equals("Hello, World!")     // true (content comparison)
s.equalsIgnoreCase("hello")   // false — "Hello, World!" vs "hello"
```

### Extract & Transform
**Definition:** Get parts of strings or create modified versions.
```java
s.substring(7)                // "World!"
s.substring(7, 12)            // "World"
s.toUpperCase()               // "HELLO, WORLD!"
s.toLowerCase()               // "hello, world!"
s.trim()                      // Remove leading/trailing whitespace
s.strip()                     // Like trim but Unicode-aware (Java 11+)
s.replace("World", "Java")    // "Hello, Java!"
s.replaceAll("[aeiou]", "*")  // Replace with regex
```

### Split & Join
**Definition:** Break strings into arrays or combine arrays into strings.
```java
"a,b,c".split(",")            // ["a", "b", "c"]
"a,b,c".split(",", 2)         // ["a", "b,c"] — max 2 parts
String.join(", ", "a", "b", "c")  // "a, b, c"
String.join("-", List.of("x","y")) // "x-y"
```

### String Comparison
**Definition:** Compare strings correctly — NEVER use `==` for content comparison.
```java
String a = "Hello";
String b = "Hello";
String c = new String("Hello");

a == b          // true  — same pool reference (coincidence)
a == c          // false — different objects!
a.equals(c)     // true  — compares content (ALWAYS use this)
a.compareTo(b)  // 0     — 0 if equal, negative if a<b, positive if a>b
```

---

## StringBuilder

**Definition:** A mutable sequence of characters — use when building strings in loops instead of `+` concatenation.

### Create & Modify
**Definition:** StringBuilder is efficient for repeated string modification — avoids creating many String objects.
```java
StringBuilder sb = new StringBuilder();
StringBuilder sb = new StringBuilder("Hello");
StringBuilder sb = new StringBuilder(100);    // Initial capacity

sb.append(" World");          // Append string
sb.append(42);                // Append number
sb.append('!');               // Append char
sb.insert(5, ",");            // Insert at position 5
sb.delete(5, 6);              // Delete from 5 to 5 (exclusive)
sb.deleteCharAt(0);           // Delete one character
sb.replace(0, 5, "Hi");       // Replace range with new string
sb.reverse();                  // Reverse all characters
sb.setCharAt(0, 'h');         // Change one character

sb.toString()                 // Convert to String
sb.length()                   // Current length
sb.charAt(0)                  // Character at index
sb.indexOf("World")           // Find position
```

---

## Operators

**Definition:** Symbols that perform operations on values — arithmetic, comparison, logical, and bitwise.

### Arithmetic
**Definition:** Basic math operations — integer division truncates.
```java
int a = 10, b = 3;
a + b     // 13
a - b     // 7
a * b     // 30
a / b     // 3   (integer division — truncated)
a % b     // 1   (remainder/modulo)

double x = 10.0 / 3;  // 3.333... (float division)

int i = 5;
i++        // Post-increment: use 5, then i = 6
++i        // Pre-increment: i = 7, then use 7
i--        // Post-decrement
--i        // Pre-decrement
```

### Comparison
**Definition:** Compare values — always returns `boolean`.
```java
5 == 5     // true
5 != 3     // true
5 > 3      // true
5 < 10     // true
5 >= 5     // true
5 <= 5     // true
```

### Logical
**Definition:** Combine boolean conditions — `&&` and `||` short-circuit evaluation.
```java
true && false    // false — AND
true || false    // true  — OR
!true            // false — NOT
true ^ true      // false — XOR

// Short-circuit: second expression not evaluated if result known
(x != 0) && (10 / x > 1)   // Safe — won't divide by zero
```

### Assignment
**Definition:** Shorthand to update variable values.
```java
int x = 10;
x += 5     // x = x + 5  → 15
x -= 3     // x = x - 3  → 12
x *= 2     // x = x * 2  → 24
x /= 4     // x = x / 4  → 6
x %= 4     // x = x % 4  → 2
```

### Bitwise
**Definition:** Operate on individual bits of integer values.
```java
5 & 3     // 1   — AND
5 | 3     // 7   — OR
5 ^ 3     // 6   — XOR
~5        // -6  — NOT (bitwise complement)
5 << 1    // 10  — left shift
5 >> 1    // 2   — right shift (signed)
5 >>> 1   // 2   — right shift (unsigned)
```

### Ternary & instanceof
**Definition:** Compact conditional expression and type check operator.
```java
int age = 20;
String label = (age >= 18) ? "Adult" : "Minor";

Object obj = "Hello";
boolean isString = (obj instanceof String);    // true

// Pattern matching instanceof (Java 16+)
if (obj instanceof String s) {
    System.out.println(s.toUpperCase());       // s is already cast
}
```

---

## If Statements

**Definition:** Execute different code blocks based on conditions.

### Basic If / Else
**Definition:** The simplest conditional — one path if true, another if false.
```java
int age = 20;

if (age >= 18) {
    System.out.println("Adult");
} else {
    System.out.println("Minor");
}
```

### If / Else If / Else
**Definition:** Chain multiple conditions — first matching block runs.
```java
int score = 75;

if (score >= 90) {
    System.out.println("A");
} else if (score >= 80) {
    System.out.println("B");
} else if (score >= 70) {
    System.out.println("C");
} else {
    System.out.println("F");
}
```

### Ternary (One-liner)
**Definition:** Compact one-line if/else for simple assignments.
```java
String result = (score >= 60) ? "Pass" : "Fail";
int max = (a > b) ? a : b;
```

---

## Switch Statement

**Definition:** Match a value against multiple cases — Java 14+ switch expressions add powerful new syntax.

### Traditional Switch
**Definition:** Classic switch with `break` to prevent fall-through.
```java
int day = 3;
String name;

switch (day) {
    case 1:
        name = "Monday";
        break;
    case 2:
        name = "Tuesday";
        break;
    case 3:
    case 4:                       // Fall-through — same block
        name = "Mid-week";
        break;
    default:
        name = "Other";
}
```

### Switch Expression (Java 14+)
**Definition:** Modern switch that returns a value — uses `->` arrows, no `break` needed.
```java
// Arrow switch — no fall-through, cleaner
String result = switch (day) {
    case 1    -> "Monday";
    case 2    -> "Tuesday";
    case 3, 4 -> "Mid-week";
    case 5    -> "Friday";
    default   -> "Weekend";
};

// With yield for multi-line blocks
String message = switch (status) {
    case "active" -> "User is active";
    case "banned" -> {
        logBannedAccess();
        yield "Access denied";    // yield returns the value
    }
    default -> "Unknown status";
};
```

### Switch on Strings (Java 7+)
**Definition:** Switch can match on String values since Java 7.
```java
String command = "start";

switch (command) {
    case "start"  -> startServer();
    case "stop"   -> stopServer();
    case "status" -> showStatus();
    default       -> System.out.println("Unknown command");
}
```

---

## While Loop

**Definition:** Repeat a block while a condition is true — checks condition before each iteration.

### Basic While
**Definition:** Runs as long as condition is true — update condition inside to avoid infinite loop.
```java
int count = 1;
while (count <= 5) {
    System.out.println("Count: " + count);
    count++;
}
```

### Do-While
**Definition:** Runs at least once before checking condition — condition evaluated after first execution.
```java
int count = 1;
do {
    System.out.println("Count: " + count);
    count++;
} while (count <= 5);

// Useful for menu loops
String input;
do {
    input = scanner.nextLine();
    process(input);
} while (!input.equals("quit"));
```

---

## For Loop

**Definition:** Different loop forms for counters, collections, and iterators.

### Classic For Loop
**Definition:** Counter-based loop — best when index is needed.
```java
for (int i = 0; i < 5; i++) {
    System.out.println(i);         // 0, 1, 2, 3, 4
}

// Reverse
for (int i = 4; i >= 0; i--) {
    System.out.println(i);         // 4, 3, 2, 1, 0
}

// Multiple variables
for (int i = 0, j = 10; i < j; i++, j--) {
    System.out.println(i + " " + j);
}
```

### Enhanced For (For-Each)
**Definition:** Iterate over arrays and collections cleanly — no index needed.
```java
int[] nums = {1, 2, 3, 4, 5};

for (int num : nums) {
    System.out.println(num);
}

List<String> fruits = List.of("apple", "banana", "cherry");
for (String fruit : fruits) {
    System.out.println(fruit);
}
```

---

## Loop Control

**Definition:** Keywords to control how loops behave — skip, stop, or jump.

### break
**Definition:** Exit the loop completely — no further iterations.
```java
for (int i = 0; i < 10; i++) {
    if (i == 5) break;
    System.out.println(i);        // Prints 0 to 4
}
```

### continue
**Definition:** Skip the current iteration — jump to the next one.
```java
for (int i = 0; i < 10; i++) {
    if (i % 2 == 0) continue;    // Skip even
    System.out.println(i);        // Prints 1, 3, 5, 7, 9
}
```

### Labeled Loops
**Definition:** Label an outer loop so inner `break`/`continue` can target it.
```java
outer:
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        if (j == 1) break outer;  // Breaks outer loop
        System.out.println(i + "," + j);
    }
}
```

---

## Arrays

**Definition:** Fixed-size ordered containers — all elements must be the same type.

### Declare & Initialize
**Definition:** Create arrays with a fixed size — size cannot change after creation.
```java
// Declaration and initialization
int[]    nums   = {1, 2, 3, 4, 5};
String[] fruits = {"apple", "banana", "cherry"};

// Declare then initialize
int[] scores = new int[5];          // [0, 0, 0, 0, 0]
scores[0] = 90;
scores[1] = 85;

// Declare only
double[] prices;
prices = new double[]{9.99, 14.99, 4.99};
```

### Access & Info
**Definition:** Get elements by index and inspect array properties.
```java
int[] arr = {10, 20, 30, 40, 50};

arr[0]           // 10 — first element
arr[arr.length - 1]  // 50 — last element
arr.length       // 5 — total elements
arr[2] = 99;     // Modify element
```

### Array Operations
**Definition:** Sort, copy, compare, and fill arrays using `Arrays` utility class.
```java
import java.util.Arrays;

int[] arr = {3, 1, 4, 1, 5, 9, 2, 6};

Arrays.sort(arr)                         // Sort in place: [1,1,2,3,4,5,6,9]
Arrays.sort(arr, 2, 5)                   // Sort only indices 2 to 4
Arrays.binarySearch(arr, 5)             // Binary search (array must be sorted)
Arrays.fill(arr, 0)                      // Fill all with 0
Arrays.copyOf(arr, 3)                    // Copy first 3 elements
Arrays.copyOfRange(arr, 1, 4)           // Copy indices 1 to 3
Arrays.equals(arr1, arr2)               // Compare contents
Arrays.toString(arr)                     // "[1, 1, 2, 3, ...]" for printing
```

### 2D Arrays
**Definition:** Arrays of arrays — used for matrices and tables.
```java
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

matrix[1][2]     // 6 — row 1, column 2

// Dynamic 2D array
int[][] grid = new int[3][4];    // 3 rows, 4 columns

// Jagged array — rows of different lengths
int[][] jagged = new int[3][];
jagged[0] = new int[]{1, 2};
jagged[1] = new int[]{3, 4, 5};
jagged[2] = new int[]{6};
```

---

## ArrayList

**Definition:** A dynamic array that grows automatically — part of `java.util`. Most commonly used list.

### Create & Add
**Definition:** Create an ArrayList and add elements — no fixed size limit.
```java
import java.util.ArrayList;

ArrayList<String> fruits = new ArrayList<>();
ArrayList<Integer> nums  = new ArrayList<>(List.of(1, 2, 3));   // From list

fruits.add("apple");              // Add to end
fruits.add(0, "kiwi");           // Insert at index 0
fruits.addAll(List.of("mango", "pear"));  // Add multiple
```

### Access & Modify
**Definition:** Get, change, and remove elements by index or value.
```java
fruits.get(0)                     // Get element at index 0
fruits.set(1, "banana")           // Replace element at index 1
fruits.remove(0)                  // Remove by index
fruits.remove("apple")            // Remove first matching value
fruits.size()                     // Number of elements
fruits.isEmpty()                  // true if empty
fruits.clear()                    // Remove all elements
```

### Search & Info
**Definition:** Check if an element exists and find its position.
```java
fruits.contains("apple")          // true
fruits.indexOf("banana")          // Index of first match (-1 if not found)
fruits.lastIndexOf("apple")       // Index of last match
```

### Iterate & Convert
**Definition:** Loop through elements and convert to array.
```java
// For-each
for (String fruit : fruits) {
    System.out.println(fruit);
}

// forEach with lambda
fruits.forEach(System.out::println);

// Convert to array
String[] arr = fruits.toArray(new String[0]);

// Sort
Collections.sort(fruits);                          // Alphabetical
Collections.sort(fruits, Collections.reverseOrder()); // Reverse
```

---

## LinkedList

**Definition:** A doubly-linked list — efficient insert/delete at head/tail but slower random access.

### Create & Use
**Definition:** LinkedList implements both List and Deque — good as a queue or stack.
```java
import java.util.LinkedList;

LinkedList<String> list = new LinkedList<>();

list.add("middle");            // Add to end
list.addFirst("first");        // Add to front
list.addLast("last");          // Add to end
list.addAll(List.of("a", "b"));

list.getFirst()                // Peek first (throws if empty)
list.getLast()                 // Peek last
list.peekFirst()               // Peek first (null if empty)
list.peekLast()                // Peek last

list.removeFirst()             // Remove and return first
list.removeLast()              // Remove and return last
list.pollFirst()               // Remove first (null if empty)

// Use as Queue (FIFO)
list.offer("item")             // Add to tail (enqueue)
list.poll()                    // Remove from head (dequeue)
list.peek()                    // Look at head without removing
```

---

## HashMap

**Definition:** A key-value map with O(1) average access — keys must be unique, no guaranteed order.

### Create & Add
**Definition:** Create a HashMap and add key-value pairs.
```java
import java.util.HashMap;

HashMap<String, Integer> ages = new HashMap<>();
HashMap<String, Integer> ages = new HashMap<>(Map.of("Dark", 25, "Alice", 30));

ages.put("Dark", 25)           // Add or update key-value pair
ages.putIfAbsent("Bob", 28)    // Add only if key doesn't exist
ages.putAll(otherMap)          // Add all from another map
```

### Access & Check
**Definition:** Get values safely and check existence of keys and values.
```java
ages.get("Dark")               // 25 (null if key missing)
ages.getOrDefault("Eve", 0)    // Return default if key missing
ages.containsKey("Dark")       // true
ages.containsValue(25)         // true
ages.size()                    // Number of entries
ages.isEmpty()                 // true if empty
```

### Modify & Remove
**Definition:** Update, compute, and delete entries.
```java
ages.put("Dark", 26)           // Update value
ages.replace("Dark", 27)       // Replace if key exists
ages.replace("Dark", 26, 27)   // Replace only if current value matches
ages.remove("Bob")             // Delete by key
ages.remove("Bob", 28)         // Delete only if value matches

// Compute new value
ages.compute("Dark", (k, v) -> v == null ? 1 : v + 1);
ages.computeIfAbsent("New", k -> 0);
ages.computeIfPresent("Dark", (k, v) -> v + 1);
ages.merge("Dark", 1, Integer::sum);  // Merge/accumulate values
```

### Iterate
**Definition:** Loop over keys, values, or key-value pairs.
```java
// Entries (key + value)
for (Map.Entry<String, Integer> entry : ages.entrySet()) {
    System.out.println(entry.getKey() + ": " + entry.getValue());
}

// Keys only
for (String key : ages.keySet()) {
    System.out.println(key);
}

// Values only
for (int val : ages.values()) {
    System.out.println(val);
}

// forEach with lambda
ages.forEach((key, val) -> System.out.println(key + " = " + val));
```

---

## HashSet

**Definition:** A collection of unique values — no duplicates, no guaranteed order, O(1) operations.

### Create & Use
**Definition:** Add elements — duplicates are silently ignored.
```java
import java.util.HashSet;

HashSet<String> set = new HashSet<>();
HashSet<String> set = new HashSet<>(Set.of("a", "b", "c"));

set.add("apple")               // Add element (returns false if duplicate)
set.addAll(List.of("x", "y")) // Add multiple
set.remove("apple")            // Remove element
set.contains("apple")          // true if present
set.size()                     // Number of unique elements
set.isEmpty()                  // true if empty
set.clear()                    // Remove all

// Iteration
for (String item : set) {
    System.out.println(item);
}
```

### Set Operations
**Definition:** Mathematical set operations — union, intersection, difference.
```java
Set<Integer> a = new HashSet<>(Set.of(1, 2, 3, 4));
Set<Integer> b = new HashSet<>(Set.of(3, 4, 5, 6));

// Union — all elements from both
Set<Integer> union = new HashSet<>(a);
union.addAll(b);               // {1, 2, 3, 4, 5, 6}

// Intersection — only common elements
Set<Integer> intersection = new HashSet<>(a);
intersection.retainAll(b);     // {3, 4}

// Difference — in a but not in b
Set<Integer> difference = new HashSet<>(a);
difference.removeAll(b);       // {1, 2}
```

---

## Stack & Queue

**Definition:** Stack (LIFO) and Queue (FIFO) are fundamental data structures — use `Deque` implementations.

### Stack
**Definition:** Last-In-First-Out — push to top, pop from top.
```java
import java.util.ArrayDeque;
import java.util.Deque;

// Modern — use Deque instead of legacy Stack class
Deque<Integer> stack = new ArrayDeque<>();

stack.push(1)                  // Push to top (addFirst)
stack.push(2)
stack.push(3)

stack.peek()                   // Look at top without removing: 3
stack.pop()                    // Remove and return top: 3
stack.isEmpty()                // false
stack.size()                   // 2
```

### Queue
**Definition:** First-In-First-Out — enqueue at tail, dequeue from head.
```java
import java.util.Queue;
import java.util.ArrayDeque;

Queue<String> queue = new ArrayDeque<>();

queue.offer("first")           // Add to tail (enqueue)
queue.offer("second")
queue.offer("third")

queue.peek()                   // Look at head without removing: "first"
queue.poll()                   // Remove and return head: "first"
queue.isEmpty()                // false
queue.size()                   // 2
```

### PriorityQueue
**Definition:** Elements dequeued in natural order (min-heap by default).
```java
import java.util.PriorityQueue;

PriorityQueue<Integer> pq = new PriorityQueue<>();          // Min-heap
PriorityQueue<Integer> maxPQ = new PriorityQueue<>(
    Collections.reverseOrder());                             // Max-heap

pq.offer(5);
pq.offer(1);
pq.offer(3);

pq.poll()    // 1 — always removes the smallest
pq.poll()    // 3
pq.poll()    // 5
```

---

## Methods

**Definition:** Reusable blocks of code — can accept parameters and return values.

### Basic Method
**Definition:** Declare a method with return type, name, parameters, and body.
```java
public int add(int a, int b) {
    return a + b;
}

public void printGreeting(String name) {    // void — no return value
    System.out.println("Hello, " + name);
}

public static String repeat(String s, int n) {
    return s.repeat(n);
}
```

### Method Overloading
**Definition:** Same method name, different parameters — Java picks the right one at compile time.
```java
public int add(int a, int b)          { return a + b; }
public double add(double a, double b) { return a + b; }
public int add(int a, int b, int c)   { return a + b + c; }

add(1, 2)            // Calls first
add(1.0, 2.0)        // Calls second
add(1, 2, 3)         // Calls third
```

### Varargs
**Definition:** Accept any number of arguments of the same type — treated as array inside method.
```java
public int sum(int... numbers) {
    int total = 0;
    for (int n : numbers) total += n;
    return total;
}

sum(1, 2, 3)           // 6
sum(1, 2, 3, 4, 5)     // 15
sum()                  // 0
```

### Pass by Value
**Definition:** Java always passes by value — primitives copy value, objects copy reference.
```java
// Primitives — original NOT modified
void addOne(int x) { x++; }
int n = 5;
addOne(n);
System.out.println(n);   // Still 5

// Objects — reference copied, object IS modified
void addItem(List<String> list) { list.add("new"); }
List<String> myList = new ArrayList<>();
addItem(myList);
System.out.println(myList);   // ["new"] — modified!
```

---

## Classes & Objects

**Definition:** A class is a blueprint — an object is an instance of that blueprint.

### Define a Class
**Definition:** Classes contain fields (data) and methods (behavior).
```java
public class Person {
    // Fields (instance variables)
    private String name;
    private int    age;
    private String email;

    // Constructor
    public Person(String name, int age) {
        this.name = name;
        this.age  = age;
    }

    // Getter methods
    public String getName()  { return name; }
    public int    getAge()   { return age;  }

    // Setter methods
    public void setName(String name) { this.name = name; }
    public void setAge(int age) {
        if (age >= 0) this.age = age;
    }

    // Instance method
    public String greet() {
        return "Hello, I'm " + name;
    }

    // Override toString for readable output
    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + "}";
    }
}
```

### Create & Use Objects
**Definition:** Use `new` to create instances — access members with dot notation.
```java
Person p1 = new Person("Dark", 25);
Person p2 = new Person("Alice", 30);

p1.getName()           // "Dark"
p1.getAge()            // 25
p1.greet()             // "Hello, I'm Dark"
p1.setAge(26)

System.out.println(p1) // Person{name='Dark', age=26}
```

---

## Constructors

**Definition:** Special methods that run when an object is created with `new` — same name as the class.

### Types of Constructors
**Definition:** Default, parameterized, and copy constructors — Java provides a no-arg default if none defined.
```java
public class Student {
    private String name;
    private int    grade;

    // No-arg constructor (default)
    public Student() {
        this.name  = "Unknown";
        this.grade = 0;
    }

    // Parameterized constructor
    public Student(String name, int grade) {
        this.name  = name;
        this.grade = grade;
    }

    // Copy constructor
    public Student(Student other) {
        this.name  = other.name;
        this.grade = other.grade;
    }

    // Constructor chaining with this()
    public Student(String name) {
        this(name, 0);    // Calls parameterized constructor
    }
}

Student s1 = new Student();
Student s2 = new Student("Dark", 10);
Student s3 = new Student(s2);          // Copy of s2
```

---

## Access Modifiers

**Definition:** Control visibility of classes, fields, and methods — fundamental to encapsulation.

### Four Access Levels
**Definition:** From most to least restrictive.

| Modifier | Same Class | Same Package | Subclass | Everywhere |
|----------|-----------|--------------|----------|------------|
| `private` | ✅ | ❌ | ❌ | ❌ |
| (default) | ✅ | ✅ | ❌ | ❌ |
| `protected` | ✅ | ✅ | ✅ | ❌ |
| `public` | ✅ | ✅ | ✅ | ✅ |

```java
public class Example {
    private   int privateField;     // Only this class
    int packageField;               // This package only (no modifier)
    protected int protectedField;   // This package + subclasses
    public    int publicField;      // Everywhere

    private   void privateMethod()   { }
    protected void protectedMethod() { }
    public    void publicMethod()    { }
}
```

---

## Static Members

**Definition:** Static fields and methods belong to the class itself — shared across all instances.

### Static Fields & Methods
**Definition:** Access via class name — no object needed.
```java
public class MathUtils {
    public static final double PI = 3.14159;    // Constant
    private static int instanceCount = 0;        // Shared counter

    public MathUtils() {
        instanceCount++;    // Track how many objects created
    }

    // Static method — no access to 'this' or instance fields
    public static int add(int a, int b) {
        return a + b;
    }

    public static int getCount() {
        return instanceCount;
    }
}

MathUtils.add(3, 4)       // 7 — called on class, not object
MathUtils.PI              // 3.14159
MathUtils.getCount()      // 0
new MathUtils();
MathUtils.getCount()      // 1
```

### Static Initializer Block
**Definition:** Runs once when the class is first loaded — used for complex static initialization.
```java
public class Config {
    static final Map<String, String> settings;

    static {
        settings = new HashMap<>();
        settings.put("host", "localhost");
        settings.put("port", "8080");
        System.out.println("Config class loaded");
    }
}
```

---

## Inheritance

**Definition:** A subclass inherits fields and methods from a superclass — use `extends` keyword.

### Basic Inheritance
**Definition:** Child class gets everything from the parent and can add or override behavior.
```java
// Parent class
public class Animal {
    protected String name;
    protected int    age;

    public Animal(String name, int age) {
        this.name = name;
        this.age  = age;
    }

    public void eat() {
        System.out.println(name + " is eating");
    }

    public String sound() {
        return "...";
    }
}

// Child class
public class Dog extends Animal {
    private String breed;

    public Dog(String name, int age, String breed) {
        super(name, age);    // Call parent constructor — must be first!
        this.breed = breed;
    }

    @Override
    public String sound() {     // Override parent method
        return "Woof!";
    }

    public void fetch() {       // New method in Dog
        System.out.println(name + " fetches the ball!");
    }
}

Dog dog = new Dog("Rex", 3, "Labrador");
dog.eat()          // Inherited: "Rex is eating"
dog.sound()        // Overridden: "Woof!"
dog.fetch()        // Own method: "Rex fetches the ball!"
```

### super Keyword
**Definition:** Access parent class members — constructor, fields, and methods.
```java
public class Cat extends Animal {
    public Cat(String name, int age) {
        super(name, age);          // Parent constructor
    }

    @Override
    public String sound() {
        String parentSound = super.sound();   // Parent method
        return "Meow! (not " + parentSound + ")";
    }
}
```

### final Class & Method
**Definition:** `final` class cannot be subclassed — `final` method cannot be overridden.
```java
public final class ImmutablePoint {    // Cannot extend this
    private final int x;
    private final int y;
    // ...
}

public class Base {
    public final void doNotOverride() {    // Cannot override in subclass
        System.out.println("Fixed behavior");
    }
}
```

---

## Polymorphism

**Definition:** One interface, many implementations — treat objects of different types uniformly.

### Runtime Polymorphism
**Definition:** The actual method called is determined at runtime based on the object's actual type.
```java
Animal[] animals = {
    new Dog("Rex", 3, "Lab"),
    new Cat("Whiskers", 5),
    new Animal("Generic", 1)
};

for (Animal a : animals) {
    System.out.println(a.sound());   // Calls correct overridden method
    // Dog → "Woof!", Cat → "Meow!", Animal → "..."
}
```

### Upcasting & Downcasting
**Definition:** Upcasting is automatic — downcasting requires explicit cast and type check.
```java
Animal a = new Dog("Rex", 3, "Lab");  // Upcasting — automatic
// a.fetch();    // Compile error — fetch() not in Animal type

Dog dog = (Dog) a;    // Downcasting — explicit cast
dog.fetch();          // Now accessible

// Safe downcast with instanceof
if (a instanceof Dog d) {   // Pattern matching (Java 16+)
    d.fetch();              // d is already the Dog type
}
```

---

## Abstraction

**Definition:** Hide implementation details — show only what is necessary through abstract classes and interfaces.

### Abstract Class
**Definition:** Cannot be instantiated — provides a partial implementation for subclasses to complete.
```java
public abstract class Shape {
    protected String color;

    public Shape(String color) {
        this.color = color;
    }

    // Abstract method — no body, must be implemented by subclasses
    public abstract double area();
    public abstract double perimeter();

    // Concrete method — inherited by all subclasses
    public void displayInfo() {
        System.out.printf("%s: area=%.2f%n", color, area());
    }
}

public class Rectangle extends Shape {
    private double width, height;

    public Rectangle(String color, double width, double height) {
        super(color);
        this.width  = width;
        this.height = height;
    }

    @Override
    public double area()      { return width * height; }

    @Override
    public double perimeter() { return 2 * (width + height); }
}

// Shape s = new Shape("red");  // Error — cannot instantiate abstract!
Shape r = new Rectangle("blue", 10, 5);
r.displayInfo();    // blue: area=50.00
```

---

## Interfaces

**Definition:** A contract of method signatures — classes implement interfaces to fulfill contracts.

### Define & Implement
**Definition:** Use `interface` keyword — implementing class provides all method bodies.
```java
// Define interface
public interface Drawable {
    void draw();                               // Abstract (default for interface)
    String getColor();

    // Default method — has body, optional to override (Java 8+)
    default void show() {
        System.out.println("Drawing: " + getColor());
    }

    // Static method (Java 8+)
    static Drawable of(String color) {
        return () -> System.out.println("Shape: " + color);
    }
}

// Implement interface
public class Circle implements Drawable {
    private String color;
    private double radius;

    @Override
    public void draw() {
        System.out.println("Drawing circle of radius " + radius);
    }

    @Override
    public String getColor() { return color; }
}

// Implement multiple interfaces
public class FancyCircle extends Circle implements Drawable, Serializable {
    // Must implement all abstract methods from all interfaces
}
```

### Functional Interface
**Definition:** An interface with exactly one abstract method — can be used with lambdas.
```java
@FunctionalInterface
public interface Calculator {
    int calculate(int a, int b);
}

// Use with lambda
Calculator add = (a, b) -> a + b;
Calculator mul = (a, b) -> a * b;

add.calculate(3, 4)    // 7
mul.calculate(3, 4)    // 12
```

---

## Enums

**Definition:** A special class that represents a fixed set of named constants.

### Basic Enum
**Definition:** Define a set of related constants — type-safe alternative to int constants.
```java
public enum Day {
    MONDAY, TUESDAY, WEDNESDAY,
    THURSDAY, FRIDAY, SATURDAY, SUNDAY
}

Day today = Day.MONDAY;

switch (today) {
    case MONDAY, TUESDAY -> System.out.println("Weekday");
    case SATURDAY, SUNDAY -> System.out.println("Weekend");
    default -> System.out.println("Mid-week");
}
```

### Enum with Fields & Methods
**Definition:** Enums can have fields, constructors, and methods — each constant can store data.
```java
public enum Planet {
    MERCURY(3.303e+23, 2.4397e6),
    VENUS  (4.869e+24, 6.0518e6),
    EARTH  (5.976e+24, 6.37814e6);

    private final double mass;
    private final double radius;

    // Enum constructor (always private)
    Planet(double mass, double radius) {
        this.mass   = mass;
        this.radius = radius;
    }

    // Method on enum
    double surfaceGravity() {
        final double G = 6.67300E-11;
        return G * mass / (radius * radius);
    }
}

Planet.EARTH.surfaceGravity()    // ~9.8 m/s²
Planet.values()                  // All constants as array
Planet.valueOf("EARTH")          // Planet.EARTH
Day.MONDAY.ordinal()            // 0 (position in declaration)
Day.MONDAY.name()               // "MONDAY"
```

---

## Generics

**Definition:** Write type-safe code that works with different types — checked at compile time.

### Generic Classes
**Definition:** Parameterize a class with a type — `T` is replaced with actual type at use.
```java
public class Box<T> {
    private T value;

    public Box(T value) { this.value = value; }
    public T getValue()  { return value; }
    public void setValue(T value) { this.value = value; }

    @Override
    public String toString() {
        return "Box[" + value + "]";
    }
}

Box<String>  strBox = new Box<>("Hello");
Box<Integer> intBox = new Box<>(42);

strBox.getValue()    // "Hello"
intBox.getValue()    // 42
```

### Generic Methods
**Definition:** A method with its own type parameter — independent of the class's type.
```java
public static <T> T firstOf(List<T> list) {
    if (list.isEmpty()) return null;
    return list.get(0);
}

public static <T extends Comparable<T>> T max(T a, T b) {
    return a.compareTo(b) >= 0 ? a : b;
}

firstOf(List.of(1, 2, 3))           // 1
max("apple", "banana")              // "banana"
max(10, 20)                         // 20
```

### Wildcards
**Definition:** Use `?` when the exact type doesn't matter — bounded wildcards add constraints.
```java
// Unbounded — any type
void printList(List<?> list) {
    for (Object elem : list) System.out.println(elem);
}

// Upper bounded — T or any subtype of Number
double sumList(List<? extends Number> list) {
    return list.stream().mapToDouble(Number::doubleValue).sum();
}

// Lower bounded — T or any supertype of Integer
void addNumbers(List<? super Integer> list) {
    list.add(1);
    list.add(2);
}
```

---

## Exception Handling

**Definition:** Handle runtime errors gracefully — prevents program crashes and enables recovery.

### Try-Catch-Finally
**Definition:** Wrap risky code in `try` — catch handles errors — finally always runs.
```java
try {
    int result = 10 / 0;
    String s   = null;
    s.length();   // NullPointerException
} catch (ArithmeticException e) {
    System.out.println("Math error: " + e.getMessage());
} catch (NullPointerException e) {
    System.out.println("Null error: " + e.getMessage());
} catch (Exception e) {
    System.out.println("General error: " + e.getMessage());
} finally {
    System.out.println("Always runs — cleanup here");
}

// Multi-catch (Java 7+)
try {
    riskyOperation();
} catch (IOException | SQLException e) {
    System.out.println("IO or SQL error: " + e.getMessage());
}
```

### Try-with-Resources
**Definition:** Automatically closes resources — no need for `finally` to close files/connections.
```java
// Resources must implement AutoCloseable
try (BufferedReader br = new BufferedReader(new FileReader("file.txt"));
     Connection conn = DriverManager.getConnection(url)) {
    String line = br.readLine();
    // br and conn closed automatically when try block exits
} catch (IOException | SQLException e) {
    e.printStackTrace();
}
```

### Throw & Throws
**Definition:** Manually throw exceptions — declare checked exceptions in method signature.
```java
// Throw — manually trigger an exception
public double divide(double a, double b) {
    if (b == 0) throw new IllegalArgumentException("Divisor cannot be zero");
    return a / b;
}

// Throws — declare checked exceptions the method may throw
public void readFile(String path) throws IOException, FileNotFoundException {
    FileReader fr = new FileReader(path);   // Can throw checked exceptions
}
```

### Custom Exceptions
**Definition:** Create application-specific exception types by extending `Exception` or `RuntimeException`.
```java
// Checked exception — must be caught or declared
public class InsufficientFundsException extends Exception {
    private double amount;

    public InsufficientFundsException(double amount) {
        super("Insufficient funds. Required: " + amount);
        this.amount = amount;
    }

    public double getAmount() { return amount; }
}

// Unchecked exception — no need to catch or declare
public class ValidationException extends RuntimeException {
    public ValidationException(String message) {
        super(message);
    }
}

// Use custom exception
void withdraw(double amount) throws InsufficientFundsException {
    if (amount > balance) {
        throw new InsufficientFundsException(amount);
    }
    balance -= amount;
}
```

### Common Exception Types
**Definition:** Frequently encountered Java exceptions.

| Exception | When it occurs |
|-----------|---------------|
| `NullPointerException` | Access on null reference |
| `ArrayIndexOutOfBoundsException` | Index beyond array size |
| `ClassCastException` | Invalid type cast |
| `ArithmeticException` | Divide by zero |
| `NumberFormatException` | Invalid string to number |
| `IllegalArgumentException` | Invalid method argument |
| `StackOverflowError` | Too many recursive calls |
| `OutOfMemoryError` | JVM out of memory |
| `IOException` | File/network I/O error (checked) |
| `SQLException` | Database error (checked) |

---

## File I/O

**Definition:** Read and write files using `java.io` and `java.nio.file` packages.

### Read Files
**Definition:** Different ways to read file content — use NIO for modern code.
```java
import java.nio.file.*;
import java.io.*;

// Read all content at once (NIO — recommended)
String content = Files.readString(Path.of("file.txt"));

// Read all lines
List<String> lines = Files.readAllLines(Path.of("file.txt"));

// Stream lines (memory efficient for large files)
try (Stream<String> stream = Files.lines(Path.of("file.txt"))) {
    stream.forEach(System.out::println);
}

// BufferedReader (classic approach)
try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
    String line;
    while ((line = br.readLine()) != null) {
        System.out.println(line);
    }
}
```

### Write Files
**Definition:** Write content to files — NIO is the modern approach.
```java
// Write string to file (overwrites)
Files.writeString(Path.of("output.txt"), "Hello, World!\n");

// Write lines
List<String> lines = List.of("Line 1", "Line 2", "Line 3");
Files.write(Path.of("output.txt"), lines);

// Append to file
Files.writeString(Path.of("log.txt"), "New entry\n",
    StandardOpenOption.APPEND, StandardOpenOption.CREATE);

// BufferedWriter (classic)
try (BufferedWriter bw = new BufferedWriter(new FileWriter("output.txt"))) {
    bw.write("Hello!");
    bw.newLine();
    bw.write("World!");
}
```

### File System Operations
**Definition:** Create, check, copy, move, and delete files and directories.
```java
Path path = Path.of("myfile.txt");

Files.exists(path)                         // Check if exists
Files.isDirectory(path)                    // Is it a directory?
Files.isRegularFile(path)                  // Is it a file?
Files.size(path)                           // File size in bytes

Files.createFile(path)                     // Create empty file
Files.createDirectory(Path.of("mydir"))    // Create directory
Files.createDirectories(Path.of("a/b/c")) // Create nested directories
Files.copy(source, target)                 // Copy file
Files.move(source, target)                 // Move/rename file
Files.delete(path)                         // Delete (throws if not found)
Files.deleteIfExists(path)                 // Delete if exists

// List directory contents
Files.list(Path.of("."))
     .forEach(System.out::println);

// Walk directory tree recursively
Files.walk(Path.of("."))
     .filter(p -> p.toString().endsWith(".java"))
     .forEach(System.out::println);
```

---

## Lambda Expressions

**Definition:** Anonymous functions — concise way to implement functional interfaces.

### Basic Lambda Syntax
**Definition:** Replace anonymous inner classes with shorter lambda syntax.
```java
// Old way — anonymous inner class
Runnable r = new Runnable() {
    @Override
    public void run() {
        System.out.println("Running!");
    }
};

// Lambda equivalent
Runnable r = () -> System.out.println("Running!");

// With parameters
Comparator<String> comp = (a, b) -> a.compareTo(b);

// With body block
Comparator<Integer> comp = (a, b) -> {
    if (a == b) return 0;
    return a > b ? 1 : -1;
};
```

### Method References
**Definition:** Even shorter syntax when lambda just calls an existing method.
```java
// Instance method of arbitrary object
Function<String, String> upper = String::toUpperCase;

// Static method
Function<String, Integer> parse = Integer::parseInt;

// Instance method of specific object
String prefix = "Hello, ";
Function<String, String> greet = prefix::concat;

// Constructor reference
Supplier<ArrayList<String>> listFactory = ArrayList::new;

// Common uses
list.forEach(System.out::println);         // Print each element
list.stream().map(String::toUpperCase)     // Transform
list.stream().filter(s -> !s.isEmpty())   // Filter
```

---

## Streams API

**Definition:** Process collections with functional-style operations — filter, map, reduce, and collect.

### Create Streams
**Definition:** Get a stream from a collection, array, or generate one.
```java
import java.util.stream.*;

// From collection
List<String> fruits = List.of("apple", "banana", "cherry");
Stream<String> stream = fruits.stream();
Stream<String> parallel = fruits.parallelStream();

// From array
Stream<String> arrStream = Arrays.stream(new String[]{"a", "b", "c"});

// Generated
Stream<Integer> infinite = Stream.iterate(0, n -> n + 1);
Stream<Double>  randoms  = Stream.generate(Math::random);
Stream<String>  of       = Stream.of("a", "b", "c");
IntStream range = IntStream.range(0, 10);       // 0 to 9
IntStream rangeClosed = IntStream.rangeClosed(1, 10); // 1 to 10
```

### Intermediate Operations
**Definition:** Transform the stream — lazy, only run when a terminal operation is called.
```java
List<String> fruits = List.of("apple", "banana", "cherry", "avocado");

fruits.stream()
    .filter(f -> f.startsWith("a"))       // Keep only "apple", "avocado"
    .map(String::toUpperCase)             // Transform to uppercase
    .sorted()                             // Sort alphabetically
    .distinct()                           // Remove duplicates
    .limit(3)                             // Take first 3
    .skip(1)                              // Skip first 1
    .peek(System.out::println)            // Debug — print without consuming
    .collect(Collectors.toList());        // Collect result
```

### Terminal Operations
**Definition:** Consume the stream and produce a result — triggers all intermediate operations.
```java
List<Integer> nums = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

// Collect results
List<Integer> evens = nums.stream()
    .filter(n -> n % 2 == 0)
    .collect(Collectors.toList());        // [2, 4, 6, 8, 10]

// Reduce to single value
int sum    = nums.stream().reduce(0, Integer::sum);           // 55
int product = nums.stream().reduce(1, (a, b) -> a * b);       // 3628800
Optional<Integer> max = nums.stream().max(Integer::compareTo);

// Aggregate
long count   = nums.stream().filter(n -> n > 5).count();  // 5
int  total   = nums.stream().mapToInt(Integer::intValue).sum();
double avg   = nums.stream().mapToInt(Integer::intValue).average().orElse(0);
int  maxVal  = nums.stream().mapToInt(Integer::intValue).max().orElse(0);

// Match
boolean anyOver5  = nums.stream().anyMatch(n -> n > 5);   // true
boolean allPositive = nums.stream().allMatch(n -> n > 0); // true
boolean noneNeg   = nums.stream().noneMatch(n -> n < 0);  // true

// Find
Optional<Integer> first = nums.stream().filter(n -> n > 5).findFirst();
```

### Collectors
**Definition:** Collect stream results into various data structures.
```java
// To list, set, map
Collectors.toList()
Collectors.toSet()
Collectors.toMap(Person::getName, Person::getAge)

// Grouping
Map<String, List<Person>> byCity = people.stream()
    .collect(Collectors.groupingBy(Person::getCity));

// Counting per group
Map<String, Long> countByCity = people.stream()
    .collect(Collectors.groupingBy(Person::getCity, Collectors.counting()));

// Joining strings
String result = fruits.stream()
    .collect(Collectors.joining(", ", "[", "]"));  // "[apple, banana, cherry]"

// Partitioning (split by true/false)
Map<Boolean, List<Integer>> partition = nums.stream()
    .collect(Collectors.partitioningBy(n -> n % 2 == 0));
```

---

## Optional

**Definition:** A container that may or may not hold a value — eliminates NullPointerException.

### Create Optional
**Definition:** Wrap a value in Optional — use `empty()` for no value, `ofNullable()` for possibly null.
```java
import java.util.Optional;

Optional<String> present = Optional.of("Hello");
Optional<String> empty   = Optional.empty();
Optional<String> maybe   = Optional.ofNullable(getValue());   // null-safe
```

### Use Optional
**Definition:** Extract, transform, and provide defaults for Optional values.
```java
Optional<String> opt = Optional.of("Hello, World!");

opt.isPresent()                       // true
opt.isEmpty()                         // false (Java 11+)
opt.get()                             // "Hello, World!" (throws if empty!)
opt.orElse("default")                 // "Hello, World!" or "default" if empty
opt.orElseGet(() -> computeDefault()) // Lazy default — only computed if empty
opt.orElseThrow()                     // Throw NoSuchElementException if empty
opt.orElseThrow(RuntimeException::new) // Throw custom exception

// Transform
opt.map(String::toUpperCase)          // Optional<String> with upper value
opt.filter(s -> s.length() > 5)       // Optional — empty if predicate fails
opt.flatMap(s -> Optional.of(s + "!"))// Flat map to avoid nested Optional

// Execute if present
opt.ifPresent(System.out::println);
opt.ifPresentOrElse(
    s -> System.out.println("Found: " + s),
    () -> System.out.println("Not found")
);
```

---

## Functional Interfaces

**Definition:** Built-in functional interfaces in `java.util.function` — use with lambdas and method refs.

### Core Interfaces
**Definition:** The four most important functional interfaces.
```java
import java.util.function.*;

// Function<T, R> — takes T, returns R
Function<String, Integer> length = String::length;
length.apply("Hello")    // 5

// Predicate<T> — takes T, returns boolean
Predicate<String> isEmpty = String::isEmpty;
isEmpty.test("")         // true

// Consumer<T> — takes T, returns nothing
Consumer<String> print = System.out::println;
print.accept("Hello")   // prints "Hello"

// Supplier<T> — takes nothing, returns T
Supplier<String> greeting = () -> "Hello!";
greeting.get()           // "Hello!"
```

### Composed Functions
**Definition:** Combine functional interfaces using built-in composition methods.
```java
Function<Integer, Integer> times2 = x -> x * 2;
Function<Integer, Integer> plus3  = x -> x + 3;

Function<Integer, Integer> times2ThenPlus3 = times2.andThen(plus3);
Function<Integer, Integer> plus3ThenTimes2 = times2.compose(plus3);

times2ThenPlus3.apply(5)    // (5*2)+3 = 13
plus3ThenTimes2.apply(5)    // (5+3)*2 = 16

Predicate<String> notEmpty    = s -> !s.isEmpty();
Predicate<String> startWithA  = s -> s.startsWith("A");
Predicate<String> combined    = notEmpty.and(startWithA);
combined.test("Alice")        // true
combined.test("")             // false
```

---

## Multithreading

**Definition:** Run multiple tasks simultaneously — Java's Thread class and Runnable interface.

### Create Threads
**Definition:** Two ways to create threads — extend Thread or implement Runnable.
```java
// Method 1: Extend Thread
class MyThread extends Thread {
    @Override
    public void run() {
        System.out.println("Thread: " + Thread.currentThread().getName());
    }
}
new MyThread().start();

// Method 2: Implement Runnable (preferred)
Runnable task = () -> {
    System.out.println("Runnable: " + Thread.currentThread().getName());
};
new Thread(task).start();

// Method 3: ExecutorService (best for production)
ExecutorService executor = Executors.newFixedThreadPool(4);
executor.submit(() -> System.out.println("Pool thread"));
executor.shutdown();
```

### ExecutorService
**Definition:** Thread pool management — reuse threads efficiently instead of creating new ones.
```java
import java.util.concurrent.*;

// Fixed thread pool
ExecutorService pool = Executors.newFixedThreadPool(4);

// Single thread
ExecutorService single = Executors.newSingleThreadExecutor();

// Cached pool — grows as needed
ExecutorService cached = Executors.newCachedThreadPool();

// Submit tasks
pool.submit(() -> doWork());

// Submit with result (Callable)
Future<Integer> future = pool.submit(() -> {
    Thread.sleep(1000);
    return 42;
});

int result = future.get();    // Blocks until done
int result = future.get(5, TimeUnit.SECONDS);  // With timeout

// Shutdown
pool.shutdown();                  // No new tasks, finish existing
pool.shutdownNow();               // Interrupt all running tasks
pool.awaitTermination(10, TimeUnit.SECONDS);
```

### Callable & Future
**Definition:** Callable is like Runnable but returns a value — Future holds the eventual result.
```java
Callable<String> task = () -> {
    Thread.sleep(2000);
    return "Task completed";
};

ExecutorService executor = Executors.newSingleThreadExecutor();
Future<String> future = executor.submit(task);

System.out.println("Doing other work...");
String result = future.get();    // Blocks here
System.out.println(result);

// CompletableFuture (Java 8+) — async/non-blocking
CompletableFuture<String> cf = CompletableFuture
    .supplyAsync(() -> fetchData())
    .thenApply(data -> process(data))
    .thenAccept(result -> save(result));
```

---

## Synchronization

**Definition:** Coordinate access to shared data from multiple threads — prevent race conditions.

### synchronized Keyword
**Definition:** Only one thread can execute synchronized code at a time.
```java
public class Counter {
    private int count = 0;

    // Synchronized method — lock on this
    public synchronized void increment() {
        count++;
    }

    public synchronized int getCount() {
        return count;
    }

    // Synchronized block — more granular control
    public void increment2() {
        synchronized (this) {
            count++;
        }
    }
}
```

### volatile Keyword
**Definition:** Ensures a variable is always read from main memory — not cached in CPU registers.
```java
public class SharedState {
    private volatile boolean running = true;    // Visible across threads

    public void stop() { running = false; }

    public void run() {
        while (running) {       // Always reads latest value
            doWork();
        }
    }
}
```

### ReentrantLock
**Definition:** More flexible than `synchronized` — supports try-lock, timeout, and fairness.
```java
import java.util.concurrent.locks.*;

ReentrantLock lock = new ReentrantLock();

lock.lock();
try {
    // Critical section
    count++;
} finally {
    lock.unlock();    // ALWAYS unlock in finally
}

// Try-lock — don't block indefinitely
if (lock.tryLock(1, TimeUnit.SECONDS)) {
    try {
        count++;
    } finally {
        lock.unlock();
    }
} else {
    System.out.println("Could not acquire lock");
}
```

---

## Java Collections Framework

**Definition:** A set of interfaces and classes for storing and manipulating groups of objects.

### Collection Hierarchy
**Definition:** The main interfaces and their common implementations.
```
Collection
├── List (ordered, allows duplicates)
│   ├── ArrayList    — dynamic array, fast random access
│   ├── LinkedList   — doubly linked, fast insert/delete at ends
│   └── Vector       — legacy, synchronized
├── Set (unique elements)
│   ├── HashSet      — hash table, no order, fastest
│   ├── LinkedHashSet — insertion order maintained
│   └── TreeSet      — sorted order (natural or Comparator)
└── Queue (FIFO)
    ├── LinkedList   — implements Queue and Deque
    ├── PriorityQueue — heap-based ordering
    └── ArrayDeque   — resizable array deque

Map (key-value pairs — not Collection)
├── HashMap          — hash table, no order
├── LinkedHashMap    — insertion order
├── TreeMap          — sorted by key
└── Hashtable        — legacy, synchronized
```

### Collections Utility Class
**Definition:** Static methods for working with collections.
```java
import java.util.Collections;

List<Integer> nums = new ArrayList<>(Arrays.asList(3, 1, 4, 1, 5, 9));

Collections.sort(nums)                          // [1, 1, 3, 4, 5, 9]
Collections.sort(nums, Collections.reverseOrder()) // [9, 5, 4, 3, 1, 1]
Collections.shuffle(nums)                       // Random order
Collections.reverse(nums)                       // Reverse in place
Collections.min(nums)                           // 1
Collections.max(nums)                           // 9
Collections.frequency(nums, 1)                  // 2 — how many 1s
Collections.binarySearch(nums, 4)              // Index (must be sorted)
Collections.fill(nums, 0)                       // Set all to 0
Collections.nCopies(5, "hello")                // List of 5 "hello"s
Collections.unmodifiableList(nums)             // Read-only view
Collections.synchronizedList(nums)             // Thread-safe wrapper
```

---

## Comparable & Comparator

**Definition:** Two interfaces for defining sort order — `Comparable` for natural order, `Comparator` for custom.

### Comparable
**Definition:** Implement on the class to define its natural ordering — used by default sort.
```java
public class Student implements Comparable<Student> {
    private String name;
    private double gpa;

    @Override
    public int compareTo(Student other) {
        return Double.compare(this.gpa, other.gpa);  // Sort by GPA ascending
        // return other.gpa.compareTo(this.gpa);      // Descending
    }
}

List<Student> students = new ArrayList<>();
Collections.sort(students);   // Uses compareTo — by GPA
```

### Comparator
**Definition:** Define custom sort orders externally — can have multiple, compose them together.
```java
// Simple comparator
Comparator<Student> byName = Comparator.comparing(Student::getName);
Comparator<Student> byGpa  = Comparator.comparingDouble(Student::getGpa);

// Reversed
Comparator<Student> byGpaDesc = byGpa.reversed();

// Chained — sort by GPA, then by name if GPA is equal
Comparator<Student> complex = Comparator
    .comparingDouble(Student::getGpa)
    .reversed()
    .thenComparing(Student::getName);

students.sort(byName);
students.sort(complex);

// Lambda comparator
students.sort((a, b) -> a.getName().compareTo(b.getName()));
```

---

## Records (Java 16+)

**Definition:** Compact, immutable data classes — automatically generate constructor, getters, `equals`, `hashCode`, and `toString`.

### Basic Record
**Definition:** One-line class for pure data carriers — fields are final by default.
```java
// Equivalent to a full class with constructor, getters, equals, hashCode, toString
public record Point(int x, int y) { }

public record Person(String name, int age, String email) {
    // Compact constructor — for validation
    public Person {
        if (age < 0) throw new IllegalArgumentException("Age cannot be negative");
        name = name.trim();    // Transform before storing
    }

    // Custom method
    public String greeting() {
        return "Hello, I'm " + name;
    }
}

Person p = new Person("Dark", 25, "dark@example.com");
p.name()       // "Dark"  — accessor (not getName())
p.age()        // 25
p.email()      // "dark@example.com"
p.greeting()   // "Hello, I'm Dark"
System.out.println(p);  // Person[name=Dark, age=25, email=dark@example.com]
```

---

## Sealed Classes (Java 17+)

**Definition:** Restrict which classes can extend a sealed class — exhaustive type hierarchies.

### Sealed Class
**Definition:** Only listed subclasses can extend — enables exhaustive pattern matching.
```java
// Sealed interface — only these three can implement it
public sealed interface Shape
    permits Circle, Rectangle, Triangle { }

public record Circle(double radius)          implements Shape { }
public record Rectangle(double w, double h)  implements Shape { }
public final class Triangle                  implements Shape {
    // Triangle cannot be further extended (final)
}

// Exhaustive switch — compiler checks all cases covered
double area = switch (shape) {
    case Circle    c -> Math.PI * c.radius() * c.radius();
    case Rectangle r -> r.w() * r.h();
    case Triangle  t -> computeTriangleArea(t);
    // No default needed — all cases covered!
};
```

---

## Pattern Matching

**Definition:** More powerful type checks and destructuring — reduces boilerplate casting.

### instanceof Pattern (Java 16+)
**Definition:** Combine type check and cast in one expression.
```java
Object obj = "Hello, World!";

// Old way
if (obj instanceof String) {
    String s = (String) obj;
    System.out.println(s.toUpperCase());
}

// New way — pattern variable s
if (obj instanceof String s) {
    System.out.println(s.toUpperCase());
}

// Combine with condition (guard)
if (obj instanceof String s && s.length() > 5) {
    System.out.println("Long string: " + s);
}
```

### Switch Pattern (Java 21+)
**Definition:** Pattern matching in switch — matches types and deconstructs records.
```java
Object value = 42;

String result = switch (value) {
    case Integer i -> "Integer: " + i;
    case String  s -> "String: " + s;
    case Double  d -> "Double: " + d;
    case null      -> "null value";
    default        -> "Unknown: " + value;
};

// Guard patterns
String label = switch (value) {
    case Integer i when i < 0 -> "Negative";
    case Integer i when i == 0 -> "Zero";
    case Integer i -> "Positive: " + i;
    default -> "Other";
};
```

---

## Date & Time

**Definition:** Use `java.time` (Java 8+) — the modern replacement for `java.util.Date`.

### Current Date & Time
**Definition:** Get the current date, time, or both.
```java
import java.time.*;

LocalDate     today   = LocalDate.now();       // 2025-01-15
LocalTime     now     = LocalTime.now();        // 14:30:00.123
LocalDateTime current = LocalDateTime.now();    // 2025-01-15T14:30:00
ZonedDateTime zoned   = ZonedDateTime.now();   // With timezone
Instant       instant = Instant.now();          // Epoch seconds (UTC)
```

### Create Specific Date/Time
**Definition:** Build a date/time for a specific point.
```java
LocalDate date = LocalDate.of(2025, 1, 15);
LocalDate date = LocalDate.of(2025, Month.JANUARY, 15);
LocalTime time = LocalTime.of(14, 30, 0);
LocalDateTime dt = LocalDateTime.of(2025, 1, 15, 14, 30, 0);

// Parse from string
LocalDate parsed = LocalDate.parse("2025-01-15");
LocalDateTime parsedDT = LocalDateTime.parse("2025-01-15T14:30:00");
```

### Format & Extract
**Definition:** Format dates to strings and extract specific components.
```java
import java.time.format.DateTimeFormatter;

LocalDate date = LocalDate.now();

// Predefined formatters
date.format(DateTimeFormatter.ISO_LOCAL_DATE)    // "2025-01-15"
date.format(DateTimeFormatter.ofPattern("dd/MM/yyyy"))  // "15/01/2025"
date.format(DateTimeFormatter.ofPattern("MMMM dd, yyyy"))  // "January 15, 2025"

// Extract parts
date.getYear()          // 2025
date.getMonth()         // JANUARY
date.getMonthValue()    // 1
date.getDayOfMonth()    // 15
date.getDayOfWeek()     // WEDNESDAY
```

### Date Arithmetic
**Definition:** Add, subtract, and compare dates.
```java
LocalDate today = LocalDate.now();

today.plusDays(7)          // Next week
today.plusMonths(1)        // Next month
today.plusYears(1)         // Next year
today.minusDays(3)         // 3 days ago

// Period — date-based (years, months, days)
Period period = Period.between(LocalDate.of(2020, 1, 1), today);
period.getYears()          // Full years difference

// Duration — time-based (hours, minutes, seconds)
Duration duration = Duration.between(startTime, endTime);
duration.toHours()         // Total hours
duration.toMinutes()       // Total minutes

// Compare
date1.isBefore(date2)      // true if date1 comes before date2
date1.isAfter(date2)       // true if date1 comes after date2
date1.isEqual(date2)       // true if same date
```

---

## Regular Expressions

**Definition:** Pattern matching in strings using `java.util.regex` package.

### Compile & Match
**Definition:** Create a Pattern and Matcher to search and extract from strings.
```java
import java.util.regex.*;

// Check if string matches pattern
boolean matches = "hello123".matches(".*\\d+.*");   // true

// Pattern and Matcher for complex use
Pattern pattern = Pattern.compile("\\d+");
Matcher matcher = pattern.matcher("abc123def456");

// Find all matches
while (matcher.find()) {
    System.out.println(matcher.group());   // "123", then "456"
    System.out.println(matcher.start());   // Start index
    System.out.println(matcher.end());     // End index
}

// Named groups
Pattern p = Pattern.compile("(?<year>\\d{4})-(?<month>\\d{2})-(?<day>\\d{2})");
Matcher m = p.matcher("2025-01-15");
if (m.matches()) {
    m.group("year")    // "2025"
    m.group("month")   // "01"
    m.group("day")     // "15"
}
```

### Replace & Split
**Definition:** Replace matches or split string by pattern.
```java
String s = "Hello, World! 123";

s.replaceAll("\\d+", "NUM")          // "Hello, World! NUM"
s.replaceFirst("\\w+", "Hi")         // "Hi, World! 123"
s.split("\\s+")                      // ["Hello,", "World!", "123"]
s.split(",", 2)                      // ["Hello", " World! 123"] — max 2 parts

// Pattern.split for pre-compiled pattern
Pattern.compile("\\s+").split(s)     // Split on whitespace
```

---

## Input / Output

**Definition:** Read input from the user console using `Scanner`.

### Scanner for User Input
**Definition:** Read different types of input from the keyboard.
```java
import java.util.Scanner;

Scanner scanner = new Scanner(System.in);

// Read different types
String  name  = scanner.nextLine();     // Read full line
String  word  = scanner.next();         // Read one word (whitespace separated)
int     num   = scanner.nextInt();      // Read integer
double  price = scanner.nextDouble();   // Read double
boolean flag  = scanner.nextBoolean();  // Read "true"/"false"

// Check if input available
if (scanner.hasNextInt()) {
    int n = scanner.nextInt();
}

// Read from string (for parsing)
Scanner strScanner = new Scanner("10 20 30");
while (strScanner.hasNextInt()) {
    System.out.println(strScanner.nextInt());
}

scanner.close();    // Close when done
```

---

## Useful Utility Classes

**Definition:** Important classes from the Java standard library.

### Math Class
**Definition:** Static methods for mathematical operations.
```java
Math.abs(-5)           // 5
Math.max(3, 7)         // 7
Math.min(3, 7)         // 3
Math.pow(2, 10)        // 1024.0
Math.sqrt(144)         // 12.0
Math.cbrt(27)          // 3.0
Math.round(3.7)        // 4
Math.floor(3.9)        // 3.0
Math.ceil(3.1)         // 4.0
Math.log(Math.E)       // 1.0
Math.log10(1000)       // 3.0
Math.random()          // 0.0 to 0.999...
Math.PI                // 3.141592653589793
Math.E                 // 2.718281828459045
```

### Random Class
**Definition:** Generate random numbers of different types.
```java
import java.util.Random;

Random rand = new Random();
Random rand = new Random(42);        // Seeded for reproducible results

rand.nextInt()                       // Any int
rand.nextInt(100)                    // 0 to 99
rand.nextInt(1, 101)                 // 1 to 100 (Java 17+)
rand.nextDouble()                    // 0.0 to 0.999...
rand.nextBoolean()                   // true or false
rand.nextLong()                      // Any long

// Java 17+ — RandomGenerator
import java.util.random.RandomGenerator;
RandomGenerator rng = RandomGenerator.getDefault();
rng.nextInt(10)
```

### Objects Class
**Definition:** Utility methods for working with objects safely.
```java
import java.util.Objects;

Objects.isNull(obj)                  // true if null
Objects.nonNull(obj)                 // true if not null
Objects.requireNonNull(obj)          // Throws NPE if null
Objects.requireNonNull(obj, "msg")   // Throws NPE with message
Objects.equals(a, b)                 // Null-safe equals
Objects.hash(name, age, email)       // Combine hash codes
Objects.toString(obj, "default")     // toString with null fallback
```

### Collections Factory Methods (Java 9+)
**Definition:** Create immutable collections with concise syntax.
```java
// Immutable — cannot add, remove, or change
List<String>        list = List.of("a", "b", "c");
Set<Integer>        set  = Set.of(1, 2, 3);
Map<String, Integer> map = Map.of("key1", 1, "key2", 2);

// Mutable copy from immutable
List<String> mutable = new ArrayList<>(List.of("a", "b", "c"));
```

---

## Debugging & Tools

**Definition:** Java development tools for building, testing, analyzing, and debugging code.

### Build Tools
**Definition:** Manage dependencies and build lifecycle.
```xml
<!-- Maven — pom.xml -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <version>3.2.0</version>
</dependency>
```
```bash
mvn compile              # Compile
mvn test                 # Run tests
mvn package              # Create JAR
mvn clean install        # Clean + build + install to local repo
mvn dependency:tree      # Show dependency tree
```

```groovy
// Gradle — build.gradle
dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-web:3.2.0'
    testImplementation 'org.junit.jupiter:junit-jupiter:5.10.0'
}
```
```bash
./gradlew build          # Build
./gradlew test           # Run tests
./gradlew run            # Run application
```

### JUnit Testing
**Definition:** Write and run unit tests — standard testing framework for Java.
```java
import org.junit.jupiter.api.*;
import static org.junit.jupiter.api.Assertions.*;

class CalculatorTest {

    @Test
    void testAdd() {
        assertEquals(5, Calculator.add(2, 3));
    }

    @Test
    void testDivideByZero() {
        assertThrows(IllegalArgumentException.class,
            () -> Calculator.divide(10, 0));
    }

    @Test
    void testWithMessage() {
        assertTrue(result > 0, "Result should be positive");
        assertNotNull(user, "User should not be null");
        assertEquals("Dark", user.getName(), "Name mismatch");
    }

    @BeforeEach
    void setUp() { /* Runs before each test */ }

    @AfterEach
    void tearDown() { /* Runs after each test */ }

    @BeforeAll
    static void setUpAll() { /* Runs once before all tests */ }

    @Disabled("Not implemented yet")
    @Test
    void skippedTest() { }
}
```

### Useful JVM Flags
**Definition:** Runtime options for memory, GC, and debugging.
```bash
java -Xmx512m Main         # Max heap size 512MB
java -Xms256m Main         # Initial heap size 256MB
java -verbose:gc Main      # GC logging
java -Xss2m Main           # Stack size 2MB
java -ea Main              # Enable assertions
java -cp ".:lib/*" Main    # Classpath with JAR folder
```

---

## Best Practices

**Definition:** Guidelines for writing clean, maintainable, and production-quality Java code.

### Code Style
**Definition:** Follow standard Java conventions for readability.
```java
// Class names — PascalCase
public class UserService { }
public class HttpRequest  { }

// Method and variable names — camelCase
public void getUserById() { }
int userCount = 0;

// Constants — UPPER_SNAKE_CASE
public static final int MAX_RETRY_COUNT = 3;
public static final String DEFAULT_HOST = "localhost";

// Package names — lowercase, no underscores
package com.company.project.service;
```

### Encapsulation
**Definition:** Keep fields private — provide controlled access through getters and setters.
```java
// Bad — public field, no control
public class Person {
    public int age;
}

// Good — private field, validated setter
public class Person {
    private int age;

    public int getAge() { return age; }

    public void setAge(int age) {
        if (age < 0 || age > 150)
            throw new IllegalArgumentException("Invalid age: " + age);
        this.age = age;
    }
}
```

### Prefer Modern APIs
**Definition:** Use new Java features — they are safer, more readable, and more efficient.
```java
// Use var for local variables (Java 10+)
var list = new ArrayList<String>();
var map  = new HashMap<String, Integer>();

// Use text blocks (Java 15+)
String json = """
              {
                "name": "Dark",
                "age": 25
              }
              """;

// Use records (Java 16+) instead of POJOs
public record Point(int x, int y) { }

// Use switch expressions (Java 14+)
String result = switch (day) {
    case MONDAY -> "Start";
    case FRIDAY -> "End";
    default     -> "Middle";
};

// Use Optional instead of null
Optional<User> findUser(int id) { }
```

### Performance Tips
**Definition:** Common patterns for efficient Java code.
```java
// Use StringBuilder for string building in loops
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 1000; i++) {
    sb.append(i);    // NOT: result += i
}

// Close resources with try-with-resources
try (InputStream in = new FileInputStream("file")) {
    // in closed automatically
}

// Use enhanced for loop over iterator
for (String item : list) { }     // Cleaner than for(int i=0...)

// Prefer isEmpty() over size() == 0
if (list.isEmpty()) { }          // NOT: list.size() == 0

// Use Collections.emptyList() instead of new ArrayList<>()
return Collections.emptyList();  // Immutable, singleton — no allocation
```

### Summary of Rules

* Make fields **`private`** — expose through getters/setters
* Use **`final`** for fields that should not change
* **Override** `equals()`, `hashCode()`, and `toString()` in value classes
* Handle **all checked exceptions** — don't swallow with empty catch
* Use **`try-with-resources`** for all `Closeable` resources
* Prefer **interface types** in declarations: `List<>` not `ArrayList<>`
* Use **`var`** for local variables to reduce boilerplate (Java 10+)
* Use **records** instead of boilerplate data classes (Java 16+)
* Prefer **streams and lambdas** over verbose loops for data transformation
* Always **close Scanner** and other resources when done
