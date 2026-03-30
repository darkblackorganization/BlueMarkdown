
## Introduction

**Go** (also called **Golang**) is an open-source, statically typed, compiled programming language designed at **Google** by Robert Griesemer, Rob Pike, and Ken Thompson, released in **2009**. Go was built to solve the problems of large-scale software engineering — fast compilation, simple syntax, built-in concurrency, and efficient execution. It combines the performance of C with the readability of Python. Go is widely used for **web servers**, **APIs**, **CLI tools**, **cloud infrastructure**, **microservices**, and **DevOps tooling**. Famous Go projects include Docker, Kubernetes, Terraform, and Hugo.


## Basic Syntax

**Definition:** Go programs start at the `main` function inside the `main` package — every file must declare its package.

### Hello World
**Definition:** The simplest Go program — every Go file starts with a package declaration.
```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

### Run & Build
**Definition:** Commands to execute and compile Go programs.
```bash
go run main.go          # Compile and run in one step
go build main.go        # Compile to binary
go build -o myapp .     # Compile to named binary
go build ./...          # Build all packages in project

./myapp                 # Run the compiled binary
```

### Comments
**Definition:** Single-line and multi-line comments — ignored by the compiler.
```go
// This is a single-line comment

/*
   This is a
   multi-line comment
*/

// godoc comments — appear in documentation
// Package main provides the entry point of the program.
package main

// Add returns the sum of two integers.
func Add(a, b int) int {
    return a + b
}
```

### Code Formatting
**Definition:** Go has one official style — always run `gofmt` or `goimports`.
```bash
gofmt -w main.go        # Format a file in place
gofmt -w .              # Format all files in current directory
goimports -w .          # Format + auto-manage imports
go vet ./...            # Check for common mistakes
```

---

## Variables & Constants

**Definition:** Go is statically typed — every variable has a fixed type determined at compile time.

### Declare Variables
**Definition:** Three ways to declare variables — use short declaration inside functions.
```go
// Explicit type declaration
var name string = "Dark"
var age  int    = 25
var pi   float64 = 3.14

// Type inferred from value
var name = "Dark"
var age  = 25

// Short variable declaration (inside functions only)
name := "Dark"
age  := 25
pi   := 3.14

// Multiple variables at once
var x, y, z int = 1, 2, 3
a, b, c := 10, "hello", true
```

### Zero Values
**Definition:** Every variable in Go is automatically initialized to its zero value — no garbage values.
```go
var i   int     // 0
var f   float64 // 0.0
var s   string  // ""  (empty string)
var b   bool    // false
var p   *int    // nil (nil pointer)
var sl  []int   // nil (nil slice)
var m   map[string]int // nil (nil map)
```

### Constants
**Definition:** Constants are fixed values — evaluated at compile time, cannot be changed.
```go
const Pi     = 3.14159
const AppName = "MyApp"
const MaxSize = 100

// Grouped constants
const (
    StatusOK       = 200
    StatusNotFound = 404
    StatusError    = 500
)
```

### Iota
**Definition:** `iota` is a special constant incrementor — resets to 0 in each `const` block.
```go
const (
    Sunday    = iota    // 0
    Monday              // 1
    Tuesday             // 2
    Wednesday           // 3
    Thursday            // 4
    Friday              // 5
    Saturday            // 6
)

// With expression
const (
    KB = 1 << (10 * (iota + 1))   // 1024
    MB                              // 1048576
    GB                              // 1073741824
    TB                              // 1099511627776
)
```

---

## Data Types

**Definition:** Go's built-in types — each has a fixed size and zero value.

### Integer Types
**Definition:** Go has signed and unsigned integers of different sizes — use `int` for most cases.
```go
int     // Platform-dependent (32 or 64 bit)
int8    // -128 to 127
int16   // -32768 to 32767
int32   // -2147483648 to 2147483647
int64   // Very large range

uint    // Unsigned platform-dependent
uint8   // 0 to 255 (alias: byte)
uint16  // 0 to 65535
uint32  // 0 to 4294967295
uint64  // Very large range

byte   = uint8   // Alias — used for raw bytes
rune   = int32   // Alias — used for Unicode code points
uintptr          // Large enough to hold a pointer
```

### Floating Point
**Definition:** Two float types — use `float64` for most numeric work.
```go
float32    // ~7 decimal digits precision
float64    // ~15 decimal digits precision (recommended)

complex64  // Complex with float32 real and imaginary
complex128 // Complex with float64 real and imaginary

// Declare
x := 3.14          // float64 (default)
y := float32(3.14)
z := complex(2, 3) // 2+3i
```

### Boolean & String
**Definition:** Simple bool and immutable string types.
```go
var ok   bool   = true
var done bool   // false (zero value)

var s string    = "Hello, 世界"   // UTF-8 encoded
s := "Go lang"
len(s)                             // Byte length, not character count
len([]rune(s))                     // Character (rune) count
```

### Type Aliases & Definitions
**Definition:** Create named types for clarity and type safety.
```go
type Celsius    float64    // New type — not assignable to float64 directly
type Fahrenheit float64

type UserID     int
type Email      string

// Type alias — same type, just another name
type MyInt = int
```

---

## Type Conversion

**Definition:** Go requires explicit type conversion — no implicit casting between types.

### Basic Conversions
**Definition:** Convert between numeric types, strings, and byte slices explicitly.
```go
// Numeric conversions
var i   int     = 42
var f   float64 = float64(i)     // int → float64
var u   uint    = uint(f)        // float64 → uint

// Integer to/from string — use strconv, NOT string(int)
import "strconv"

s   := strconv.Itoa(42)           // int → "42"
n, err := strconv.Atoi("42")      // "42" → int, error

s   := strconv.FormatFloat(3.14, 'f', 2, 64)  // float64 → "3.14"
f, err := strconv.ParseFloat("3.14", 64)       // "3.14" → float64

b, err := strconv.ParseBool("true")            // "true" → bool
s   := strconv.FormatBool(true)                // bool → "true"

// String ↔ byte slice
bs := []byte("hello")             // string → []byte
s  := string(bs)                  // []byte → string

// String ↔ rune slice (for Unicode)
rs := []rune("Hello, 世界")       // string → []rune
s  := string(rs)                  // []rune → string
```

---

## String Operations

**Definition:** Strings in Go are immutable byte sequences — use the `strings` and `strconv` packages.

### Basic Operations
**Definition:** Get info about a string and check its contents.
```go
import "strings"

s := "Hello, World!"

len(s)                         // Byte length → 13
strings.ToUpper(s)             // "HELLO, WORLD!"
strings.ToLower(s)             // "hello, world!"
strings.TrimSpace("  hi  ")   // "hi"
strings.Trim(s, "!")           // Remove "!" from both ends
strings.TrimLeft(s, "H")      // Remove "H" from left
strings.TrimRight(s, "!")     // Remove "!" from right
```

### Search & Check
**Definition:** Find and verify content inside a string.
```go
strings.Contains(s, "World")       // true
strings.HasPrefix(s, "Hello")      // true
strings.HasSuffix(s, "!")          // true
strings.Index(s, "World")          // 7  (-1 if not found)
strings.LastIndex(s, "l")          // 10
strings.Count(s, "l")              // 3
strings.ContainsAny(s, "aeiou")    // true — any of these chars?
strings.ContainsRune(s, 'W')       // true
```

### Replace & Transform
**Definition:** Modify string content by replacing, splitting, or joining parts.
```go
strings.Replace(s, "World", "Go", 1)   // Replace first occurrence
strings.ReplaceAll(s, "l", "L")        // Replace all
strings.Split("a,b,c", ",")           // ["a", "b", "c"]
strings.SplitN("a,b,c", ",", 2)       // ["a", "b,c"] — max 2 parts
strings.Join([]string{"a","b"}, "-")  // "a-b"
strings.Repeat("ab", 3)               // "ababab"
strings.Title("hello world")          // "Hello World" (deprecated → use cases)
```

### Build Strings Efficiently
**Definition:** Use `strings.Builder` for building strings in a loop — much faster than `+` concatenation.
```go
import "strings"

var sb strings.Builder
for i := 0; i < 5; i++ {
    fmt.Fprintf(&sb, "item %d\n", i)
}
result := sb.String()

// Or with WriteString
sb.WriteString("Hello")
sb.WriteString(", ")
sb.WriteString("World!")
fmt.Println(sb.String())    // Hello, World!
```

---

## Operators

**Definition:** Go supports standard arithmetic, comparison, logical, and bitwise operators.

### Arithmetic
**Definition:** Basic math operations — note integer division truncates toward zero.
```go
10 + 3    // 13
10 - 3    // 7
10 * 3    // 30
10 / 3    // 3   (integer division — truncated)
10.0 / 3  // 3.3333... (float division)
10 % 3    // 1   (remainder)

x := 5
x++       // x = 6 (post-increment — no prefix ++ in Go)
x--       // x = 5
```

### Comparison
**Definition:** Compare values — result is always `bool`.
```go
5 == 5     // true
5 != 3     // true
5 > 3      // true
5 < 10     // true
5 >= 5     // true
5 <= 5     // true
```

### Logical
**Definition:** Combine boolean conditions.
```go
true && false    // false — AND
true || false    // true  — OR
!true            // false — NOT
```

### Bitwise
**Definition:** Operate on individual bits of integer values.
```go
5 & 3     // 1   — AND
5 | 3     // 7   — OR
5 ^ 3     // 6   — XOR
5 &^ 3    // 4   — AND NOT (bit clear)
5 << 1    // 10  — left shift
5 >> 1    // 2   — right shift
```

---

## If Statements

**Definition:** Conditional execution — Go's `if` does not require parentheses around the condition.

### Basic If / Else
**Definition:** Execute different code based on whether a condition is true or false.
```go
age := 20

if age >= 18 {
    fmt.Println("Adult")
} else {
    fmt.Println("Minor")
}

// If / else if / else
if age > 65 {
    fmt.Println("Senior")
} else if age >= 18 {
    fmt.Println("Adult")
} else {
    fmt.Println("Minor")
}
```

### If with Init Statement
**Definition:** Declare a variable in the `if` statement — scoped to the if/else block only.
```go
// Very common pattern for error handling
if err := doSomething(); err != nil {
    fmt.Println("Error:", err)
    return
}

if val, ok := myMap["key"]; ok {
    fmt.Println("Found:", val)
} else {
    fmt.Println("Key not found")
}
```

---

## Switch Statement

**Definition:** Match a value against multiple cases — cleaner than long if/else chains. No `break` needed.

### Basic Switch
**Definition:** Each case is checked — first match runs, then exits automatically (no fall-through by default).
```go
day := "Monday"

switch day {
case "Monday":
    fmt.Println("Start of work week")
case "Friday":
    fmt.Println("End of work week")
case "Saturday", "Sunday":      // Multiple values in one case
    fmt.Println("Weekend!")
default:
    fmt.Println("Midweek")
}
```

### Switch with No Condition
**Definition:** A switch with no value acts like a chain of if/else — first true case runs.
```go
score := 75

switch {
case score >= 90:
    fmt.Println("A")
case score >= 80:
    fmt.Println("B")
case score >= 70:
    fmt.Println("C")
default:
    fmt.Println("F")
}
```

### Switch with Init Statement
**Definition:** Initialize a variable in the switch expression — scoped to the switch block.
```go
switch os := runtime.GOOS; os {
case "linux":
    fmt.Println("Linux")
case "darwin":
    fmt.Println("macOS")
default:
    fmt.Printf("Other: %s\n", os)
}
```

### Fallthrough
**Definition:** Explicitly fall through to the next case — runs next case's body unconditionally.
```go
switch num := 2; num {
case 1:
    fmt.Println("One")
    fallthrough             // Also runs next case
case 2:
    fmt.Println("Two")
    fallthrough
case 3:
    fmt.Println("Three")   // All three print if num == 1
default:
    fmt.Println("Other")
}
```

---

## For Loop

**Definition:** Go has only ONE loop keyword — `for` — it covers all loop patterns.

### Classic C-Style For
**Definition:** Counter-based loop with init, condition, and post statement.
```go
for i := 0; i < 5; i++ {
    fmt.Println(i)          // 0, 1, 2, 3, 4
}

// Reverse loop
for i := 4; i >= 0; i-- {
    fmt.Println(i)          // 4, 3, 2, 1, 0
}
```

### While-Style Loop
**Definition:** Omit init and post — acts like a `while` loop.
```go
count := 0
for count < 5 {
    fmt.Println(count)
    count++
}
```

### Infinite Loop
**Definition:** `for` with no condition runs forever — exit with `break` or `return`.
```go
for {
    input := readInput()
    if input == "quit" {
        break
    }
    process(input)
}
```

### Range Loop
**Definition:** Iterate over arrays, slices, maps, strings, and channels.
```go
fruits := []string{"apple", "banana", "cherry"}

// Index and value
for i, fruit := range fruits {
    fmt.Printf("%d: %s\n", i, fruit)
}

// Index only
for i := range fruits {
    fmt.Println(i)
}

// Value only (blank identifier)
for _, fruit := range fruits {
    fmt.Println(fruit)
}

// Range over map
m := map[string]int{"a": 1, "b": 2}
for key, val := range m {
    fmt.Printf("%s: %d\n", key, val)
}

// Range over string (runes)
for i, r := range "Hello, 世界" {
    fmt.Printf("%d: %c\n", i, r)
}
```

### Break, Continue, Goto
**Definition:** Control loop execution — skip, stop, or jump.
```go
// break — exit loop
for i := 0; i < 10; i++ {
    if i == 5 { break }
    fmt.Println(i)
}

// continue — skip to next iteration
for i := 0; i < 10; i++ {
    if i%2 == 0 { continue }
    fmt.Println(i)    // 1, 3, 5, 7, 9
}

// Labeled break — exit outer loop from inner loop
outer:
for i := 0; i < 3; i++ {
    for j := 0; j < 3; j++ {
        if j == 1 { break outer }
        fmt.Println(i, j)
    }
}
```

---

## Arrays

**Definition:** Fixed-size, ordered collections — size is part of the type. Rarely used directly — prefer slices.

### Declare Array
**Definition:** Arrays have a fixed size set at declaration time — cannot grow.
```go
var arr [5]int                        // [0, 0, 0, 0, 0]
arr := [5]int{1, 2, 3, 4, 5}
arr := [...]int{1, 2, 3}             // Size inferred → [3]int
arr := [5]int{0: 10, 2: 30}         // Specific indices: [10, 0, 30, 0, 0]
```

### Access & Info
**Definition:** Get or set elements by index — arrays are copied on assignment.
```go
arr := [5]int{10, 20, 30, 40, 50}

arr[0]           // 10 — first element
arr[4]           // 50 — last element
arr[2] = 99      // Modify element
len(arr)         // 5 — number of elements

// 2D array
matrix := [3][3]int{
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9},
}
matrix[1][2]     // 6
```

---

## Slices

**Definition:** Dynamic, flexible views into arrays — the most commonly used data structure in Go.

### Create Slice
**Definition:** Slices can be created from arrays, literals, or with `make`.
```go
// Slice literal
fruits := []string{"apple", "banana", "cherry"}

// From array
arr := [5]int{1, 2, 3, 4, 5}
sl  := arr[1:3]             // [2, 3] — indices 1 and 2

// Using make(type, length, capacity)
sl  := make([]int, 5)       // len=5, cap=5, all zeros
sl  := make([]int, 3, 10)   // len=3, cap=10

// Nil slice
var sl []int                // nil — len=0, cap=0
```

### Slice Info
**Definition:** Check the length and capacity of a slice.
```go
sl := []int{1, 2, 3, 4, 5}
len(sl)     // 5 — number of elements
cap(sl)     // Capacity of underlying array
sl == nil   // false (slice with elements is not nil)
```

### Append
**Definition:** Add elements to a slice — Go automatically grows the underlying array if needed.
```go
sl := []int{1, 2, 3}
sl  = append(sl, 4)           // [1, 2, 3, 4]
sl  = append(sl, 5, 6, 7)    // [1, 2, 3, 4, 5, 6, 7]

// Append another slice
other := []int{8, 9}
sl = append(sl, other...)     // Spread with ...
```

### Slice Operations
**Definition:** Copy, reslice, and manipulate slices.
```go
// Copy slice
src := []int{1, 2, 3}
dst := make([]int, len(src))
n   := copy(dst, src)         // n = number of elements copied

// Delete element at index i
sl = append(sl[:i], sl[i+1:]...)

// Insert at index i
sl = append(sl[:i], append([]int{99}, sl[i:]...)...)

// Reverse
for i, j := 0, len(sl)-1; i < j; i, j = i+1, j-1 {
    sl[i], sl[j] = sl[j], sl[i]
}
```

### 2D Slices
**Definition:** Slices of slices — used for matrices, grids, and tables.
```go
matrix := [][]int{
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9},
}
matrix[1][2]    // 6

// Create dynamically
rows, cols := 3, 4
grid := make([][]int, rows)
for i := range grid {
    grid[i] = make([]int, cols)
}
```

---

## Maps

**Definition:** Unordered key-value stores — keys must be comparable, values can be any type.

### Create Map
**Definition:** Create a map with `make` or a map literal — always initialize before use.
```go
// Map literal
ages := map[string]int{
    "Dark":  25,
    "Alice": 30,
    "Bob":   28,
}

// Using make
scores := make(map[string]int)
scores["Math"]    = 90
scores["Science"] = 85

// Nil map — DO NOT write to it
var m map[string]int    // nil map — read is OK, write panics!
```

### Access & Check
**Definition:** Get values safely using the two-value form to check if key exists.
```go
val := ages["Dark"]             // 25 (zero value if key missing)

// Safe access — check if key exists
val, ok := ages["Dark"]
if ok {
    fmt.Println("Found:", val)
} else {
    fmt.Println("Not found")
}

// Check if key exists
_, exists := ages["Unknown"]    // exists = false
```

### Modify Map
**Definition:** Add, update, and delete key-value pairs.
```go
ages["Eve"] = 22                // Add new key
ages["Dark"] = 26               // Update existing key
delete(ages, "Bob")             // Delete a key (no error if missing)

len(ages)                       // Number of key-value pairs
```

### Iterate Map
**Definition:** Loop over all key-value pairs — order is random each time.
```go
for key, val := range ages {
    fmt.Printf("%s: %d\n", key, val)
}

// Keys only
for key := range ages {
    fmt.Println(key)
}
```

### Nested Maps
**Definition:** Maps whose values are also maps — useful for hierarchical data.
```go
config := map[string]map[string]string{
    "database": {
        "host": "localhost",
        "port": "5432",
    },
    "cache": {
        "host": "localhost",
        "port": "6379",
    },
}
config["database"]["host"]    // "localhost"
```

---

## Structs

**Definition:** A composite type that groups related fields together — Go's primary way to model data.

### Define & Create Struct
**Definition:** Declare a struct type and create instances with field values.
```go
type Person struct {
    Name    string
    Age     int
    Email   string
    Address Address    // Nested struct
}

type Address struct {
    City    string
    Country string
}

// Create struct instances
p1 := Person{
    Name:    "Dark",
    Age:     25,
    Email:   "dark@example.com",
    Address: Address{City: "Mumbai", Country: "India"},
}

p2 := Person{"Alice", 30, "alice@example.com", Address{}}  // Positional (avoid)
p3 := Person{Name: "Bob"}    // Only set some fields — others get zero values
```

### Access & Modify
**Definition:** Get and set struct fields using the dot `.` operator.
```go
fmt.Println(p1.Name)           // "Dark"
fmt.Println(p1.Address.City)   // "Mumbai"

p1.Age = 26                    // Modify field
p1.Address.City = "Delhi"      // Modify nested field
```

### Struct Pointer
**Definition:** Pass a pointer to a struct to modify it in a function.
```go
p := &Person{Name: "Dark", Age: 25}   // Pointer to struct

p.Age = 26          // Auto-dereferenced — same as (*p).Age = 26
fmt.Println(p.Name) // "Dark"
```

### Anonymous Structs
**Definition:** One-off struct types without a named type — useful for temporary data.
```go
point := struct {
    X, Y int
}{X: 10, Y: 20}

fmt.Println(point.X, point.Y)    // 10 20
```

### Struct Tags
**Definition:** Metadata attached to struct fields — used by JSON, database, and validation packages.
```go
type User struct {
    ID       int    `json:"id"`
    Name     string `json:"name"`
    Email    string `json:"email,omitempty"`   // Omit if empty
    Password string `json:"-"`                 // Never include in JSON
    Age      int    `json:"age" db:"user_age"` // Multiple tags
}
```

---

## Pointers

**Definition:** A pointer stores the memory address of a value — allows functions to modify variables and avoids large data copies.

### Basics
**Definition:** Use `&` to get an address and `*` to dereference (get the value at the address).
```go
x := 42
p := &x           // p is a pointer to x — type: *int
fmt.Println(p)    // Memory address e.g. 0xc000018090
fmt.Println(*p)   // 42 — dereference to get value
*p = 100          // Modify x through pointer
fmt.Println(x)    // 100

// nil pointer
var ptr *int      // nil — points to nothing
if ptr == nil {
    fmt.Println("pointer is nil")
}
```

### Pointers to Structs
**Definition:** Creating a pointer to a struct is the standard way to share and modify structs.
```go
type Point struct { X, Y int }

p := &Point{X: 10, Y: 20}    // Create pointer directly
p.X = 50                      // No need to write (*p).X
fmt.Println(p.X, p.Y)         // 50 20

// new() — allocates zero-value struct, returns pointer
p2 := new(Point)
p2.X = 100
```

### Pass by Value vs Pointer
**Definition:** Go passes everything by value — use pointers when you need to modify the original.
```go
// Pass by value — modifies a copy, original unchanged
func addOne(n int) int {
    return n + 1
}

// Pass by pointer — modifies original
func addOnePtr(n *int) {
    *n++
}

x := 5
addOnePtr(&x)
fmt.Println(x)    // 6
```

---

## Functions

**Definition:** Functions are first-class values in Go — they can be assigned, passed, and returned.

### Basic Function
**Definition:** Declare with `func`, parameter types after names, return types after parameters.
```go
func greet(name string) string {
    return "Hello, " + name + "!"
}

func add(a, b int) int {     // Both params same type — share the type
    return a + b
}

func swap(a, b int) (int, int) {   // Multiple return values
    return b, a
}

x, y := swap(1, 2)   // x=2, y=1
```

### Named Return Values
**Definition:** Name the return values — they act as pre-declared variables, can use bare `return`.
```go
func divide(a, b float64) (result float64, err error) {
    if b == 0 {
        err = fmt.Errorf("cannot divide by zero")
        return      // Bare return — returns named values
    }
    result = a / b
    return          // Returns result and nil error
}
```

### Functions as Values
**Definition:** Functions are first-class — assign to variables and pass to other functions.
```go
// Assign function to variable
add := func(a, b int) int { return a + b }
result := add(3, 4)    // 7

// Pass function as argument
func apply(nums []int, fn func(int) int) []int {
    result := make([]int, len(nums))
    for i, n := range nums {
        result[i] = fn(n)
    }
    return result
}

doubled := apply([]int{1, 2, 3}, func(n int) int { return n * 2 })
// [2, 4, 6]
```

### init Function
**Definition:** Runs automatically before `main` — used for package initialization.
```go
var config map[string]string

func init() {
    config = loadConfig()    // Runs before main()
    fmt.Println("Config loaded")
}

func main() {
    fmt.Println("App started")
}
```

---

## Variadic Functions

**Definition:** Functions that accept any number of arguments of the same type — collected into a slice.

### Define & Call
**Definition:** Use `...` before the type to accept variable number of arguments.
```go
func sum(nums ...int) int {
    total := 0
    for _, n := range nums {    // nums is []int inside the function
        total += n
    }
    return total
}

sum(1, 2, 3)           // 6
sum(1, 2, 3, 4, 5)    // 15
sum()                  // 0 — zero arguments is valid
```

### Spread Slice into Variadic
**Definition:** Pass a slice to a variadic function using `...` spread operator.
```go
nums := []int{1, 2, 3, 4, 5}
total := sum(nums...)    // Spread slice as individual arguments
```

---

## Closures

**Definition:** A function that captures and remembers variables from its surrounding scope.

### Basic Closure
**Definition:** Inner functions can access and modify variables from their enclosing function.
```go
func makeCounter() func() int {
    count := 0                // Captured variable
    return func() int {
        count++               // Modifies outer count
        return count
    }
}

counter := makeCounter()
fmt.Println(counter())    // 1
fmt.Println(counter())    // 2
fmt.Println(counter())    // 3
```

### Closure with Arguments
**Definition:** Create configured functions by closing over different values.
```go
func multiplier(factor int) func(int) int {
    return func(n int) int {
        return n * factor     // Closes over factor
    }
}

double := multiplier(2)
triple := multiplier(3)

fmt.Println(double(5))    // 10
fmt.Println(triple(5))    // 15
```

---

## Methods

**Definition:** Functions with a receiver — attach behavior to types. Go's way of doing object-oriented programming.

### Value Receiver
**Definition:** The method receives a copy of the value — cannot modify the original.
```go
type Rectangle struct {
    Width, Height float64
}

// Value receiver — works on a copy
func (r Rectangle) Area() float64 {
    return r.Width * r.Height
}

func (r Rectangle) Perimeter() float64 {
    return 2 * (r.Width + r.Height)
}

rect := Rectangle{Width: 10, Height: 5}
fmt.Println(rect.Area())        // 50
fmt.Println(rect.Perimeter())   // 30
```

### Pointer Receiver
**Definition:** The method receives a pointer — can modify the original struct.
```go
// Pointer receiver — modifies the original
func (r *Rectangle) Scale(factor float64) {
    r.Width  *= factor
    r.Height *= factor
}

rect := Rectangle{Width: 10, Height: 5}
rect.Scale(2)
fmt.Println(rect.Width)    // 20 — modified!
```

### Methods on Non-Struct Types
**Definition:** You can define methods on any named type in the same package.
```go
type Celsius float64
type Fahrenheit float64

func (c Celsius) ToFahrenheit() Fahrenheit {
    return Fahrenheit(c*9/5 + 32)
}

func (f Fahrenheit) ToCelsius() Celsius {
    return Celsius((f - 32) * 5 / 9)
}

boiling := Celsius(100)
fmt.Printf("%.2f°F\n", boiling.ToFahrenheit())    // 212.00°F
```

---

## Interfaces

**Definition:** An interface defines a set of method signatures — any type that implements those methods satisfies the interface implicitly.

### Define & Implement
**Definition:** No `implements` keyword — a type satisfies an interface automatically by having the right methods.
```go
// Define interface
type Shape interface {
    Area() float64
    Perimeter() float64
}

// Rectangle implicitly implements Shape
type Rectangle struct { Width, Height float64 }
func (r Rectangle) Area() float64      { return r.Width * r.Height }
func (r Rectangle) Perimeter() float64 { return 2 * (r.Width + r.Height) }

// Circle implicitly implements Shape
type Circle struct { Radius float64 }
func (c Circle) Area() float64      { return math.Pi * c.Radius * c.Radius }
func (c Circle) Perimeter() float64 { return 2 * math.Pi * c.Radius }

// Use the interface
func printShapeInfo(s Shape) {
    fmt.Printf("Area: %.2f, Perimeter: %.2f\n", s.Area(), s.Perimeter())
}

printShapeInfo(Rectangle{10, 5})
printShapeInfo(Circle{7})
```

### Empty Interface
**Definition:** `interface{}` (or `any` in Go 1.18+) accepts any type — like `Object` in Java.
```go
func printAnything(val interface{}) {
    fmt.Println(val)
}

// Modern Go 1.18+
func printAnything(val any) {
    fmt.Println(val)
}

printAnything(42)
printAnything("hello")
printAnything([]int{1, 2, 3})
```

### Type Assertion
**Definition:** Extract the concrete type stored inside an interface.
```go
var val interface{} = "hello"

// Unsafe — panics if wrong type
s := val.(string)
fmt.Println(s)    // "hello"

// Safe — check with ok
s, ok := val.(string)
if ok {
    fmt.Println("String:", s)
} else {
    fmt.Println("Not a string")
}
```

### Type Switch
**Definition:** Switch on the dynamic type stored inside an interface.
```go
func describe(i interface{}) {
    switch v := i.(type) {
    case int:
        fmt.Printf("Integer: %d\n", v)
    case string:
        fmt.Printf("String: %q\n", v)
    case bool:
        fmt.Printf("Boolean: %t\n", v)
    case []int:
        fmt.Printf("Int slice of length %d\n", len(v))
    default:
        fmt.Printf("Unknown type: %T\n", v)
    }
}
```

### Common Interfaces
**Definition:** Important interfaces from the standard library — implement these for interoperability.
```go
// fmt.Stringer — controls how type prints with %v and fmt.Println
type Stringer interface {
    String() string
}

// error — the built-in error interface
type error interface {
    Error() string
}

// io.Reader — anything that can be read from
type Reader interface {
    Read(p []byte) (n int, err error)
}

// io.Writer — anything that can be written to
type Writer interface {
    Write(p []byte) (n int, err error)
}
```

---

## Embedding

**Definition:** Embed one type inside another to inherit its methods — Go's form of composition over inheritance.

### Struct Embedding
**Definition:** Include another type's fields and methods by embedding it — no explicit delegation needed.
```go
type Animal struct {
    Name string
}

func (a Animal) Speak() string {
    return a.Name + " makes a sound"
}

type Dog struct {
    Animal              // Embedded — Dog gets Animal's fields and methods
    Breed string
}

func (d Dog) Speak() string {
    return d.Name + " barks!"    // Override embedded method
}

d := Dog{Animal: Animal{Name: "Rex"}, Breed: "Lab"}
fmt.Println(d.Name)      // "Rex" — promoted from Animal
fmt.Println(d.Speak())   // "Rex barks!" — overridden method
```

### Interface Embedding
**Definition:** Compose interfaces from other interfaces — creates larger interface contracts.
```go
type Reader interface {
    Read(p []byte) (n int, err error)
}

type Writer interface {
    Write(p []byte) (n int, err error)
}

// Composed interface
type ReadWriter interface {
    Reader    // Embed Reader
    Writer    // Embed Writer
}
```

---

## Error Handling

**Definition:** Go handles errors explicitly using return values — no exceptions. Errors are values.

### The error Interface
**Definition:** Functions return an `error` as their last return value — always check it.
```go
import "errors"

func divide(a, b float64) (float64, error) {
    if b == 0 {
        return 0, errors.New("cannot divide by zero")
    }
    return a / b, nil       // nil means no error
}

result, err := divide(10, 0)
if err != nil {
    fmt.Println("Error:", err)
    return
}
fmt.Println("Result:", result)
```

### fmt.Errorf & %w
**Definition:** Create formatted errors and wrap existing ones to add context.
```go
// Create formatted error
err := fmt.Errorf("user %d not found", userID)

// Wrap error with %w — preserves original for unwrapping
err := fmt.Errorf("getUser failed: %w", originalErr)

// Unwrap
import "errors"

var notFoundErr *NotFoundError
if errors.As(err, &notFoundErr) {
    fmt.Println("Not found:", notFoundErr)
}

if errors.Is(err, ErrNotFound) {
    fmt.Println("Is ErrNotFound")
}
```

### Custom Error Types
**Definition:** Create struct-based errors to carry additional context data.
```go
type ValidationError struct {
    Field   string
    Message string
}

func (e *ValidationError) Error() string {
    return fmt.Sprintf("validation error on %s: %s", e.Field, e.Message)
}

func validateAge(age int) error {
    if age < 0 || age > 150 {
        return &ValidationError{
            Field:   "age",
            Message: "must be between 0 and 150",
        }
    }
    return nil
}

err := validateAge(-5)
var ve *ValidationError
if errors.As(err, &ve) {
    fmt.Println("Field:", ve.Field)
}
```

### Sentinel Errors
**Definition:** Package-level errors for expected error conditions — compare with `errors.Is()`.
```go
var (
    ErrNotFound   = errors.New("not found")
    ErrUnauthorized = errors.New("unauthorized")
    ErrTimeout    = errors.New("request timeout")
)

func findUser(id int) (*User, error) {
    if id <= 0 {
        return nil, ErrNotFound
    }
    // ...
}

_, err := findUser(-1)
if errors.Is(err, ErrNotFound) {
    fmt.Println("User not found")
}
```

---

## Panic & Recover

**Definition:** `panic` stops normal execution — `recover` catches a panic and prevents the program from crashing.

### Panic
**Definition:** Stops the current goroutine immediately — unwinds the stack, runs deferred functions, then crashes.
```go
func mustDivide(a, b int) int {
    if b == 0 {
        panic("cannot divide by zero")   // Stops execution
    }
    return a / b
}

// panic with error
panic(fmt.Errorf("critical failure: %v", err))
```

### Recover
**Definition:** Catch a panic inside a deferred function — must be called directly by a deferred function.
```go
func safeDiv(a, b int) (result int, err error) {
    defer func() {
        if r := recover(); r != nil {
            err = fmt.Errorf("recovered from panic: %v", r)
        }
    }()
    return a / b, nil    // Will panic if b==0 — caught by recover
}

result, err := safeDiv(10, 0)
if err != nil {
    fmt.Println(err)    // "recovered from panic: runtime error: ..."
}
```

---

## Goroutines

**Definition:** Lightweight threads managed by the Go runtime — launch thousands simultaneously with minimal overhead.

### Start Goroutine
**Definition:** Prefix any function call with `go` to run it concurrently in a new goroutine.
```go
func sayHello(name string) {
    fmt.Printf("Hello, %s!\n", name)
}

// Run synchronously
sayHello("Dark")

// Run concurrently in a goroutine
go sayHello("Dark")
go sayHello("Alice")
go sayHello("Bob")

// Anonymous goroutine
go func() {
    fmt.Println("Running in background")
}()

// With argument — capture variable correctly
for i := 0; i < 5; i++ {
    i := i                // Capture loop variable
    go func() {
        fmt.Println(i)
    }()
}
```

### WaitGroup
**Definition:** Wait for multiple goroutines to finish before proceeding.
```go
import "sync"

var wg sync.WaitGroup

for i := 0; i < 5; i++ {
    wg.Add(1)               // Increment counter
    go func(id int) {
        defer wg.Done()     // Decrement counter when done
        fmt.Printf("Worker %d done\n", id)
    }(i)
}

wg.Wait()                   // Block until counter reaches 0
fmt.Println("All workers done")
```

---

## Channels

**Definition:** Typed pipelines for communication between goroutines — "share memory by communicating."

### Create & Use
**Definition:** Channels are created with `make` — send with `<-` and receive with `<-`.
```go
// Unbuffered channel — sender blocks until receiver is ready
ch := make(chan int)

// Send in goroutine (must not block main)
go func() {
    ch <- 42         // Send value
}()

val := <-ch          // Receive value
fmt.Println(val)     // 42
```

### Buffered Channels
**Definition:** Has a queue — sender only blocks when buffer is full.
```go
ch := make(chan int, 5)    // Buffer of 5

// Can send without a receiver ready (up to buffer size)
ch <- 1
ch <- 2
ch <- 3

fmt.Println(<-ch)    // 1
fmt.Println(<-ch)    // 2
```

### Close & Range Over Channel
**Definition:** Close signals no more values will be sent — range receives until closed.
```go
ch := make(chan int)

go func() {
    for i := 0; i < 5; i++ {
        ch <- i
    }
    close(ch)           // Signal: no more values
}()

// Receive until channel closed
for val := range ch {
    fmt.Println(val)    // 0, 1, 2, 3, 4
}

// Check if channel is closed
val, ok := <-ch
if !ok {
    fmt.Println("Channel closed")
}
```

### Directional Channels
**Definition:** Restrict a channel to send-only or receive-only — adds type safety.
```go
func producer(out chan<- int) {    // Send-only
    for i := 0; i < 5; i++ {
        out <- i
    }
    close(out)
}

func consumer(in <-chan int) {     // Receive-only
    for val := range in {
        fmt.Println(val)
    }
}

ch := make(chan int)
go producer(ch)
consumer(ch)
```

---

## Select Statement

**Definition:** Like a `switch` but for channels — waits for whichever case is ready first.

### Basic Select
**Definition:** Block until one channel is ready — chosen randomly if multiple are ready.
```go
ch1 := make(chan string)
ch2 := make(chan string)

go func() { ch1 <- "one" }()
go func() { ch2 <- "two" }()

select {
case msg1 := <-ch1:
    fmt.Println("Received from ch1:", msg1)
case msg2 := <-ch2:
    fmt.Println("Received from ch2:", msg2)
}
```

### Select with Default
**Definition:** `default` makes select non-blocking — runs immediately if no channel is ready.
```go
select {
case msg := <-ch:
    fmt.Println("Received:", msg)
default:
    fmt.Println("No message ready — continue")
}
```

### Timeout with Select
**Definition:** Use `time.After` to implement timeouts on channel operations.
```go
import "time"

select {
case result := <-ch:
    fmt.Println("Got result:", result)
case <-time.After(2 * time.Second):
    fmt.Println("Timeout! No response in 2 seconds")
}
```

---

## sync Package

**Definition:** Provides synchronization primitives for safe concurrent access to shared data.

### Mutex
**Definition:** A mutual exclusion lock — only one goroutine can hold it at a time.
```go
import "sync"

type SafeCounter struct {
    mu    sync.Mutex
    count int
}

func (c *SafeCounter) Increment() {
    c.mu.Lock()
    defer c.mu.Unlock()    // Always unlock with defer
    c.count++
}

func (c *SafeCounter) Value() int {
    c.mu.Lock()
    defer c.mu.Unlock()
    return c.count
}
```

### RWMutex
**Definition:** Allows multiple readers OR one writer — more efficient than Mutex for read-heavy workloads.
```go
type Cache struct {
    mu   sync.RWMutex
    data map[string]string
}

func (c *Cache) Get(key string) (string, bool) {
    c.mu.RLock()               // Multiple readers allowed simultaneously
    defer c.mu.RUnlock()
    val, ok := c.data[key]
    return val, ok
}

func (c *Cache) Set(key, val string) {
    c.mu.Lock()                // Only one writer at a time
    defer c.mu.Unlock()
    c.data[key] = val
}
```

### Once
**Definition:** Ensures a function is executed exactly once — even if called from multiple goroutines.
```go
var (
    instance *DB
    once     sync.Once
)

func GetDB() *DB {
    once.Do(func() {
        instance = &DB{} // Called exactly once — thread-safe singleton
        instance.connect()
    })
    return instance
}
```

### atomic
**Definition:** Lock-free atomic operations on simple numeric types — faster than mutex for counters.
```go
import "sync/atomic"

var counter int64

// Atomically increment
atomic.AddInt64(&counter, 1)

// Atomically read
val := atomic.LoadInt64(&counter)

// Atomically store
atomic.StoreInt64(&counter, 100)

// Atomically compare-and-swap
swapped := atomic.CompareAndSwapInt64(&counter, 100, 200)
```

---

## Defer

**Definition:** Schedule a function to run when the surrounding function returns — always runs, even on panic.

### Basic Defer
**Definition:** Deferred calls run in LIFO order (last-in, first-out) when the function returns.
```go
func processFile(filename string) error {
    f, err := os.Open(filename)
    if err != nil {
        return err
    }
    defer f.Close()             // Will run when processFile returns

    // Process file...
    return nil
}
```

### Multiple Defers (LIFO)
**Definition:** Multiple defers execute in reverse order — last deferred runs first.
```go
func demo() {
    defer fmt.Println("First deferred — runs last")
    defer fmt.Println("Second deferred — runs second")
    defer fmt.Println("Third deferred — runs first")
    fmt.Println("Function body")
}
// Output:
// Function body
// Third deferred — runs first
// Second deferred — runs second
// First deferred — runs last
```

### Defer with Arguments
**Definition:** Arguments to deferred functions are evaluated immediately, not when deferred function runs.
```go
func countDown() {
    for i := 3; i >= 0; i-- {
        defer fmt.Println(i)    // i captured at each iteration
    }
}
// Output: 0, 1, 2, 3 (LIFO)
```

---

## Packages & Modules

**Definition:** Go code is organized into packages — modules group related packages with version management.

### Package Rules
**Definition:** Every Go file belongs to a package — exported names start with uppercase.
```go
// math/calculator.go
package math              // Package name

// Exported — accessible from other packages (uppercase)
func Add(a, b int) int {
    return a + b
}

// Unexported — only within this package (lowercase)
func helper(x int) int {
    return x * 2
}
```

### Go Modules
**Definition:** `go.mod` tracks the module path and dependencies — created with `go mod init`.
```bash
go mod init github.com/username/myproject   # Initialize module
go mod tidy                                  # Remove unused, add missing deps
go get github.com/gin-gonic/gin             # Add a dependency
go get github.com/gin-gonic/gin@v1.9.0     # Specific version
go get github.com/gin-gonic/gin@latest      # Latest version
go list -m all                              # List all dependencies
go mod download                             # Download all dependencies
go mod verify                               # Verify dependencies
```

### go.mod File
**Definition:** Defines module identity and required dependencies.
```
module github.com/username/myproject

go 1.21

require (
    github.com/gin-gonic/gin v1.9.0
    github.com/stretchr/testify v1.8.4
)
```

---

## Importing Packages

**Definition:** Import standard library and third-party packages at the top of each file.

### Import Styles
**Definition:** Different ways to import packages — grouped imports are preferred.
```go
// Single import
import "fmt"

// Grouped imports (preferred)
import (
    "fmt"
    "math"
    "strings"

    "github.com/gin-gonic/gin"     // Third-party
)

// Aliased import
import (
    "fmt"
    f    "fmt"           // Alias — use f.Println()
    str "strings"        // Alias
)

// Blank import — side effects only (runs init())
import _ "github.com/lib/pq"

// Dot import — import into current namespace (avoid)
import . "fmt"
Println("Hello")         // No prefix needed
```

---

## File I/O

**Definition:** Read and write files using the `os`, `bufio`, and `io` packages.

### Read Files
**Definition:** Different ways to read file content — use `bufio.Scanner` for line-by-line reading.
```go
import (
    "bufio"
    "fmt"
    "os"
)

// Read entire file at once
data, err := os.ReadFile("file.txt")
if err != nil {
    log.Fatal(err)
}
fmt.Println(string(data))

// Read line by line (memory efficient for large files)
f, err := os.Open("file.txt")
if err != nil {
    log.Fatal(err)
}
defer f.Close()

scanner := bufio.NewScanner(f)
for scanner.Scan() {
    fmt.Println(scanner.Text())    // One line at a time
}
```

### Write Files
**Definition:** Write content to files — truncate with WriteFile or append with OpenFile.
```go
// Write entire file (creates or overwrites)
err := os.WriteFile("output.txt", []byte("Hello, World!\n"), 0644)

// Write with buffered writer (efficient for many writes)
f, err := os.Create("output.txt")
if err != nil {
    log.Fatal(err)
}
defer f.Close()

w := bufio.NewWriter(f)
fmt.Fprintln(w, "Line 1")
fmt.Fprintln(w, "Line 2")
w.Flush()                          // Flush buffer to file

// Append to file
f, err := os.OpenFile("log.txt",
    os.O_APPEND|os.O_CREATE|os.O_WRONLY, 0644)
defer f.Close()
fmt.Fprintln(f, "New log entry")
```

### File System Operations
**Definition:** Create, check, rename, and delete files and directories.
```go
// Check if file exists
if _, err := os.Stat("file.txt"); os.IsNotExist(err) {
    fmt.Println("File does not exist")
}

os.Mkdir("mydir", 0755)            // Create one directory
os.MkdirAll("a/b/c", 0755)        // Create nested directories
os.Remove("file.txt")              // Delete file or empty directory
os.RemoveAll("mydir")              // Delete directory recursively
os.Rename("old.txt", "new.txt")    // Rename or move file

// List directory contents
entries, err := os.ReadDir(".")
for _, e := range entries {
    fmt.Printf("%s (dir: %v)\n", e.Name(), e.IsDir())
}
```

---

## JSON

**Definition:** Encode and decode JSON using the `encoding/json` package — uses struct tags for field mapping.

### Marshal (Go → JSON)
**Definition:** Convert Go values to JSON strings or byte slices.
```go
import "encoding/json"

type User struct {
    ID    int    `json:"id"`
    Name  string `json:"name"`
    Email string `json:"email,omitempty"`
    Pass  string `json:"-"`             // Never include
}

user := User{ID: 1, Name: "Dark", Email: "dark@example.com"}

// Marshal to bytes
data, err := json.Marshal(user)
fmt.Println(string(data))
// {"id":1,"name":"Dark","email":"dark@example.com"}

// Pretty print
data, err = json.MarshalIndent(user, "", "  ")
```

### Unmarshal (JSON → Go)
**Definition:** Parse JSON bytes into Go structs or maps.
```go
jsonStr := `{"id":1,"name":"Dark","email":"dark@example.com"}`

var user User
err := json.Unmarshal([]byte(jsonStr), &user)
if err != nil {
    log.Fatal(err)
}
fmt.Println(user.Name)    // "Dark"

// Into a map (when structure is unknown)
var result map[string]interface{}
json.Unmarshal([]byte(jsonStr), &result)
fmt.Println(result["name"])    // "Dark"
```

### Stream JSON (Encoder/Decoder)
**Definition:** Encode/decode JSON from/to `io.Reader`/`io.Writer` — efficient for files and HTTP.
```go
// Encode to writer (e.g. HTTP response, file)
json.NewEncoder(w).Encode(user)

// Decode from reader (e.g. HTTP request, file)
var user User
json.NewDecoder(r.Body).Decode(&user)
```

---

## HTTP Server

**Definition:** Build web servers using the standard `net/http` package — no framework needed for simple APIs.

### Basic HTTP Server
**Definition:** Create routes and start a server — handlers receive a `ResponseWriter` and `*Request`.
```go
import (
    "fmt"
    "net/http"
)

func helloHandler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintln(w, "Hello, World!")
}

func main() {
    http.HandleFunc("/", helloHandler)
    http.HandleFunc("/health", func(w http.ResponseWriter, r *http.Request) {
        w.WriteHeader(http.StatusOK)
        fmt.Fprintln(w, "OK")
    })

    fmt.Println("Server running on :8080")
    log.Fatal(http.ListenAndServe(":8080", nil))
}
```

### JSON API Handler
**Definition:** Parse JSON request bodies and return JSON responses.
```go
func createUser(w http.ResponseWriter, r *http.Request) {
    if r.Method != http.MethodPost {
        http.Error(w, "Method not allowed", http.StatusMethodNotAllowed)
        return
    }

    var user User
    if err := json.NewDecoder(r.Body).Decode(&user); err != nil {
        http.Error(w, err.Error(), http.StatusBadRequest)
        return
    }

    // Process...
    w.Header().Set("Content-Type", "application/json")
    w.WriteHeader(http.StatusCreated)
    json.NewEncoder(w).Encode(user)
}
```

### Middleware
**Definition:** Wrap handlers to add cross-cutting concerns like logging and authentication.
```go
func loggingMiddleware(next http.Handler) http.Handler {
    return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        start := time.Now()
        next.ServeHTTP(w, r)
        fmt.Printf("%s %s — %v\n", r.Method, r.URL.Path, time.Since(start))
    })
}

func authMiddleware(next http.Handler) http.Handler {
    return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        token := r.Header.Get("Authorization")
        if token == "" {
            http.Error(w, "Unauthorized", http.StatusUnauthorized)
            return
        }
        next.ServeHTTP(w, r)
    })
}

mux := http.NewServeMux()
mux.HandleFunc("/api/users", createUser)
handler := loggingMiddleware(authMiddleware(mux))
log.Fatal(http.ListenAndServe(":8080", handler))
```

---

## HTTP Client

**Definition:** Make HTTP requests to external services using `net/http` — always set timeouts.

### GET Request
**Definition:** Fetch data from an external URL.
```go
import (
    "encoding/json"
    "net/http"
    "time"
)

client := &http.Client{Timeout: 10 * time.Second}    // Always set timeout

resp, err := client.Get("https://api.example.com/users")
if err != nil {
    return err
}
defer resp.Body.Close()

if resp.StatusCode != http.StatusOK {
    return fmt.Errorf("unexpected status: %d", resp.StatusCode)
}

var users []User
json.NewDecoder(resp.Body).Decode(&users)
```

### POST Request
**Definition:** Send JSON data to an API endpoint.
```go
import "bytes"

user := User{Name: "Dark", Email: "dark@example.com"}
body, err := json.Marshal(user)

req, err := http.NewRequest("POST",
    "https://api.example.com/users",
    bytes.NewBuffer(body))
req.Header.Set("Content-Type", "application/json")
req.Header.Set("Authorization", "Bearer token123")

client := &http.Client{Timeout: 10 * time.Second}
resp, err := client.Do(req)
defer resp.Body.Close()
```

---

## Context

**Definition:** Carries deadlines, cancellation signals, and request-scoped values across API boundaries.

### Create Context
**Definition:** Different contexts for different use cases — always pass context as first argument.
```go
import "context"

ctx := context.Background()              // Top-level — never cancelled
ctx := context.TODO()                    // Placeholder — plan to add proper context

// With cancellation
ctx, cancel := context.WithCancel(context.Background())
defer cancel()                           // Always call cancel to free resources

// With timeout
ctx, cancel := context.WithTimeout(context.Background(), 5*time.Second)
defer cancel()

// With deadline
deadline := time.Now().Add(10 * time.Second)
ctx, cancel := context.WithDeadline(context.Background(), deadline)
defer cancel()

// With value
ctx = context.WithValue(ctx, "userID", 42)
userID := ctx.Value("userID").(int)
```

### Using Context
**Definition:** Check for cancellation and pass context through the call chain.
```go
func fetchData(ctx context.Context, url string) ([]byte, error) {
    req, err := http.NewRequestWithContext(ctx, "GET", url, nil)
    if err != nil {
        return nil, err
    }

    resp, err := http.DefaultClient.Do(req)
    if err != nil {
        // Context cancelled or timed out
        if ctx.Err() != nil {
            return nil, fmt.Errorf("request cancelled: %w", ctx.Err())
        }
        return nil, err
    }
    defer resp.Body.Close()
    return io.ReadAll(resp.Body)
}
```

---

## Testing

**Definition:** Go has built-in testing — write test functions in `*_test.go` files, run with `go test`.

### Basic Tests
**Definition:** Test functions start with `Test` and take `*testing.T` — use `t.Error` or `t.Fatal` to fail.
```go
// math_test.go
package math

import "testing"

func TestAdd(t *testing.T) {
    result := Add(2, 3)
    if result != 5 {
        t.Errorf("Add(2, 3) = %d; want 5", result)
    }
}

func TestDivide(t *testing.T) {
    result, err := Divide(10, 2)
    if err != nil {
        t.Fatalf("Unexpected error: %v", err)
    }
    if result != 5 {
        t.Errorf("Divide(10, 2) = %.1f; want 5", result)
    }
}
```

### Table-Driven Tests
**Definition:** Test many input/output combinations cleanly using a slice of test cases.
```go
func TestAdd(t *testing.T) {
    tests := []struct {
        name     string
        a, b     int
        expected int
    }{
        {"positive numbers", 2, 3, 5},
        {"negative numbers", -2, -3, -5},
        {"zero", 0, 5, 5},
        {"large numbers", 100, 200, 300},
    }

    for _, tc := range tests {
        t.Run(tc.name, func(t *testing.T) {
            result := Add(tc.a, tc.b)
            if result != tc.expected {
                t.Errorf("Add(%d, %d) = %d; want %d",
                    tc.a, tc.b, result, tc.expected)
            }
        })
    }
}
```

### Benchmarks
**Definition:** Measure performance — functions start with `Benchmark` and take `*testing.B`.
```go
func BenchmarkAdd(b *testing.B) {
    for i := 0; i < b.N; i++ {    // b.N is set automatically
        Add(2, 3)
    }
}
```

### Run Tests
**Definition:** Commands to run, filter, and benchmark tests.
```bash
go test ./...                    # Run all tests in all packages
go test ./math/...               # Run tests in specific package
go test -run TestAdd             # Run tests matching pattern
go test -v ./...                 # Verbose — show test names
go test -cover ./...             # Show coverage percentage
go test -coverprofile=c.out ./...# Save coverage to file
go tool cover -html=c.out        # Open coverage in browser
go test -bench=. ./...           # Run benchmarks
go test -race ./...              # Detect race conditions
```

---

## Generics

**Definition:** Write functions and types that work with multiple types — added in Go 1.18.

### Generic Functions
**Definition:** Use type parameters in square brackets — constrain with interfaces.
```go
// T is a type parameter constrained by "comparable"
func Contains[T comparable](slice []T, item T) bool {
    for _, v := range slice {
        if v == item {
            return true
        }
    }
    return false
}

Contains([]int{1, 2, 3}, 2)          // true
Contains([]string{"a", "b"}, "c")   // false
```

### Type Constraints
**Definition:** Use the `constraints` package or define your own interface constraints.
```go
import "golang.org/x/exp/constraints"

func Min[T constraints.Ordered](a, b T) T {
    if a < b {
        return a
    }
    return b
}

Min(3, 5)           // 3 — int
Min(3.14, 2.71)     // 2.71 — float64
Min("apple", "banana")  // "apple" — string

// Custom constraint
type Number interface {
    ~int | ~int32 | ~int64 | ~float32 | ~float64
}

func Sum[T Number](nums []T) T {
    var total T
    for _, n := range nums {
        total += n
    }
    return total
}
```

### Generic Types
**Definition:** Create data structures that work with any type.
```go
type Stack[T any] struct {
    items []T
}

func (s *Stack[T]) Push(item T) {
    s.items = append(s.items, item)
}

func (s *Stack[T]) Pop() (T, bool) {
    var zero T
    if len(s.items) == 0 {
        return zero, false
    }
    item := s.items[len(s.items)-1]
    s.items = s.items[:len(s.items)-1]
    return item, true
}

s := Stack[int]{}
s.Push(1)
s.Push(2)
val, ok := s.Pop()    // 2, true
```

---

## Common Standard Library

**Definition:** Important packages included with Go — no installation needed.

### fmt — Formatted I/O
**Definition:** Print, scan, and format values.
```go
fmt.Println("Hello")              // Print with newline
fmt.Printf("Name: %s, Age: %d\n", name, age)
fmt.Sprintf("Value: %v", val)    // Format to string
fmt.Errorf("error: %w", err)     // Format error (wraps)
fmt.Scan(&name)                   // Read from stdin
fmt.Scanf("%s %d", &name, &age)  // Read formatted

// Format verbs
%v   // Default format
%+v  // Struct with field names
%#v  // Go syntax representation
%T   // Type of value
%d   // Integer
%f   // Float
%s   // String
%q   // Quoted string
%p   // Pointer address
%b   // Binary
%x   // Hex lowercase
%X   // Hex uppercase
```

### time — Date & Time
**Definition:** Work with time, durations, and timers.
```go
import "time"

now  := time.Now()
t    := time.Date(2025, time.January, 15, 10, 30, 0, 0, time.UTC)

now.Format("2006-01-02 15:04:05")    // Format (use this exact reference time)
now.Format(time.RFC3339)              // "2025-01-15T10:30:00Z"
time.Parse("2006-01-02", "2025-01-15")

now.Year()         // 2025
now.Month()        // January
now.Day()          // 15
now.Hour()         // 10
now.Weekday()      // Wednesday

// Duration
d := 2*time.Hour + 30*time.Minute
time.Sleep(100 * time.Millisecond)
start := time.Now()
elapsed := time.Since(start)

// Timer and Ticker
timer  := time.NewTimer(2 * time.Second)
ticker := time.NewTicker(1 * time.Second)
defer ticker.Stop()
```

### sort — Sorting
**Definition:** Sort slices and implement custom sorting.
```go
import "sort"

nums := []int{3, 1, 4, 1, 5, 9}
sort.Ints(nums)                        // Ascending: [1,1,3,4,5,9]
sort.Sort(sort.Reverse(sort.IntSlice(nums)))  // Descending

strs := []string{"banana", "apple", "cherry"}
sort.Strings(strs)                     // Alphabetical

// Sort structs by field
type Person struct { Name string; Age int }
people := []Person{{"Bob", 30}, {"Alice", 25}, {"Charlie", 35}}
sort.Slice(people, func(i, j int) bool {
    return people[i].Age < people[j].Age    // Sort by age ascending
})

// Check if sorted
sort.IntsAreSorted(nums)               // true/false
sort.SearchInts(nums, 4)               // Binary search — returns index
```

### log — Logging
**Definition:** Simple logging with timestamp prefix.
```go
import "log"

log.Println("Info message")
log.Printf("Value: %d\n", val)
log.Fatal("Fatal error — calls os.Exit(1)")
log.Panic("Panic — calls panic()")

// Custom logger
logger := log.New(os.Stdout, "APP: ", log.Ldate|log.Ltime|log.Lshortfile)
logger.Println("Custom log message")
```

### math/rand — Random Numbers
**Definition:** Generate pseudo-random numbers — seed for different sequences.
```go
import (
    "math/rand"
    "time"
)

// Seed for randomness (Go 1.20+ auto-seeds)
rand.Seed(time.Now().UnixNano())

rand.Intn(100)             // Random int [0, 100)
rand.Float64()             // Random float [0.0, 1.0)
rand.Shuffle(len(sl), func(i, j int) {
    sl[i], sl[j] = sl[j], sl[i]
})
```

---

## CLI with os & flag

**Definition:** Build command-line tools using the `os` and `flag` packages.

### os Package
**Definition:** Access command-line arguments, environment variables, and exit codes.
```go
import "os"

os.Args              // ["./program", "arg1", "arg2"]
os.Args[0]           // Program name
os.Args[1:]          // All arguments after program name

os.Getenv("HOME")    // Get environment variable
os.Setenv("KEY", "value")
os.LookupEnv("KEY")  // Returns (value, exists)

os.Exit(0)           // Exit with success
os.Exit(1)           // Exit with error code
os.Getpid()          // Current process ID
os.Hostname()        // Machine hostname
```

### flag Package
**Definition:** Parse command-line flags — like `--name="Dark" --count=5 --verbose`.
```go
import "flag"

// Define flags
name    := flag.String("name", "World", "Name to greet")
count   := flag.Int("count", 1, "Number of greetings")
verbose := flag.Bool("verbose", false, "Enable verbose output")

flag.Parse()    // Parse os.Args after flags defined

// Use flag values (dereference pointers)
for i := 0; i < *count; i++ {
    fmt.Printf("Hello, %s!\n", *name)
}
if *verbose {
    fmt.Println("Verbose mode on")
}
```

```bash
./app --name="Dark" --count=3 --verbose
```

---

## Regular Expressions

**Definition:** Pattern matching in strings using the `regexp` package.

### Compile & Match
**Definition:** Compile a pattern once, then reuse it — use `MustCompile` for fixed patterns.
```go
import "regexp"

// Compile pattern (returns error)
re, err := regexp.Compile(`\d+`)

// MustCompile — panics if invalid (use for fixed patterns)
re := regexp.MustCompile(`\d+`)

re.MatchString("abc123")     // true
re.FindString("abc123def")   // "123" — first match
re.FindAllString("a1b2c3", -1)   // ["1","2","3"] — all matches
re.ReplaceAllString("a1b2", `\d+`, "N")   // "aNbN"
re.Split("a1b2c3", -1)       // ["a","b","c",""] — split on matches
re.FindStringSubmatch(`(\d+)-(\d+)`)  // Group captures
```

### Common Patterns
**Definition:** Ready-to-use patterns for validation.
```go
var (
    emailRe   = regexp.MustCompile(`^[\w.+-]+@[\w-]+\.[\w.]+$`)
    phoneRe   = regexp.MustCompile(`^\+?[\d\s\-()]{7,15}$`)
    urlRe     = regexp.MustCompile(`^https?://[\w\-.]+(:\d+)?(/[\w\-./]*)?$`)
    alphaRe   = regexp.MustCompile(`^[a-zA-Z]+$`)
    numericRe = regexp.MustCompile(`^\d+$`)
)

emailRe.MatchString("dark@example.com")    // true
```

---

## Debugging & Tools

**Definition:** Go toolchain commands for formatting, analyzing, profiling, and debugging.

### Essential Go Commands
**Definition:** The most important commands in the Go toolchain.
```bash
go run main.go          # Compile and run
go build ./...          # Compile all packages
go test ./...           # Run all tests
go test -race ./...     # Detect data race conditions
go vet ./...            # Static analysis — find likely bugs
go fmt ./...            # Format all files (use gofmt -w instead)
gofmt -w .              # Format and write files
goimports -w .          # Format + fix imports

go doc fmt.Println      # Read documentation
go doc -all fmt         # All docs for a package

go env                  # Show Go environment variables
go version              # Go version
```

### pprof Profiling
**Definition:** Profile CPU, memory, and goroutines to find performance bottlenecks.
```go
import _ "net/http/pprof"    // Import for side effects — registers routes

// Add to HTTP server
go func() {
    log.Println(http.ListenAndServe("localhost:6060", nil))
}()
```
```bash
go tool pprof http://localhost:6060/debug/pprof/profile   # CPU profile
go tool pprof http://localhost:6060/debug/pprof/heap      # Memory profile
```

### Race Detector
**Definition:** Detect data races at runtime — always use during development and testing.
```bash
go test -race ./...         # Run tests with race detector
go run -race main.go        # Run program with race detector
go build -race -o app .     # Build with race detector enabled
```

---

## Tips & Tricks

**Definition:** Useful Go patterns and idioms for cleaner, more idiomatic code.

### Useful Patterns
**Definition:** Common Go idioms worth knowing.
```go
// Multiple return values
x, y := swap(1, 2)

// Ignore a return value with blank identifier
val, _ := divide(10, 2)     // Ignore error (only when safe!)

// Short variable declaration with type assertion
val := i.(string)

// Slice tricks
last := sl[len(sl)-1]       // Last element
sl   = sl[:len(sl)-1]       // Remove last
sl   = sl[1:]               // Remove first

// Map as set (no built-in set in Go)
seen := make(map[string]struct{})
seen["item"] = struct{}{}
_, exists := seen["item"]   // Check membership (true)

// Empty struct uses zero memory
type empty struct{}
ch := make(chan struct{})    // Signal channel — no data needed
close(ch)                   // Signal by closing

// String conversion
[]byte("hello")             // string → bytes
string([]byte{72, 101})     // bytes → string
```

### Printf Formatting Tricks
**Definition:** Useful format verbs for debugging.
```go
fmt.Printf("%T\n", variable)   // Print type
fmt.Printf("%v\n", struct)     // Default format
fmt.Printf("%+v\n", struct)    // With field names
fmt.Printf("%#v\n", struct)    // Go syntax
fmt.Printf("%p\n", &variable)  // Pointer address
fmt.Printf("%08b\n", 42)       // Binary, zero-padded: 00101010
fmt.Printf("%-10s|\n", "left") // Left-aligned with width
fmt.Printf("%10s|\n", "right") // Right-aligned with width
```

### Idiomatic Go
**Definition:** Patterns that experienced Go developers follow.
```go
// Error handling immediately after call
result, err := someFunc()
if err != nil {
    return fmt.Errorf("someFunc failed: %w", err)
}

// Prefer early return over nested ifs
func process(val int) error {
    if val < 0 {
        return errors.New("negative value")
    }
    if val == 0 {
        return errors.New("zero value")
    }
    // Happy path — no nesting
    doWork(val)
    return nil
}

// Use defer for cleanup
f, _ := os.Open("file.txt")
defer f.Close()    // Guaranteed cleanup

// Table-driven tests
// Named return values for documentation
func getUser(id int) (user *User, err error)
```

---

## Best Practices

**Definition:** Guidelines for writing idiomatic, maintainable, and production-ready Go code.

### Code Organization
**Definition:** Structure packages and files for clarity and maintainability.
```
myproject/
├── cmd/
│   └── server/
│       └── main.go        ← Entry points
├── internal/
│   ├── handler/           ← HTTP handlers
│   ├── service/           ← Business logic
│   └── repository/        ← Data access
├── pkg/
│   └── utils/             ← Shared utilities
├── go.mod
└── go.sum
```

### Naming Conventions
**Definition:** Go naming rules that every developer should follow.
```go
// Package names — short, lowercase, no underscores
package httputil     // Good
package http_util    // Bad

// Exported names — CapitalCase (PascalCase)
func GetUser() {}    // Exported — accessible outside package
func getUser() {}    // Unexported — package-private

// Variables and functions — camelCase
userID  := 42       // camelCase
var maxRetries = 3

// Constants — CamelCase (not UPPER_CASE like other languages)
const MaxRetries = 3
const defaultTimeout = 30 * time.Second

// Interfaces — often end in -er
type Reader interface { Read() }
type Stringer interface { String() string }
type UserRepository interface { FindByID(id int) (*User, error) }

// Error variables — prefix with Err
var ErrNotFound = errors.New("not found")
var ErrInvalid  = errors.New("invalid")
```

### Error Handling
**Definition:** Handle errors explicitly — never ignore them silently.
```go
// Bad — ignore error
result, _ := riskyOperation()

// Good — handle every error
result, err := riskyOperation()
if err != nil {
    return fmt.Errorf("riskyOperation failed: %w", err)
}

// Wrap errors to add context
if err := db.Query(q); err != nil {
    return fmt.Errorf("database query %q failed: %w", q, err)
}
```

### Concurrency
**Definition:** Safe patterns for working with goroutines and shared data.
```go
// Always pass context for cancellation
func fetchData(ctx context.Context) error { }

// Protect shared data with mutex
type SafeMap struct {
    mu sync.RWMutex
    m  map[string]string
}

// Close channels from the sender, not receiver
// Start goroutines after setting up channels
// Use WaitGroup to wait for goroutines to finish
// Prefer channels for communication, mutex for protecting state
```

### Summary of Rules

* Use `gofmt` and `go vet` — always keep code formatted and linted
* Handle **every error** — never ignore with `_` unless intentional
* Use **`defer`** for cleanup — files, mutexes, connections
* Keep **interfaces small** — one or two methods is ideal
* Prefer **composition** over inheritance — embed types
* Pass **context** as the first parameter for cancellation support
* Write **table-driven tests** for comprehensive coverage
* Use **`go test -race`** during development to catch data races
* Name packages **short and lowercase** — no underscores
* Exported names need **godoc comments** — start with the name
