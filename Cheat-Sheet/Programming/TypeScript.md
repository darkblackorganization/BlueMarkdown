
## Introduction

**TypeScript** is a strongly typed superset of JavaScript developed by **Microsoft** and released in **2012**. It adds **optional static typing**, classes, interfaces, generics, and modern ECMAScript features that compile down to plain JavaScript. TypeScript catches type errors at compile time — before code runs — making large codebases easier to maintain, refactor, and understand. It is used everywhere JavaScript is used: **web frontends** (React, Angular, Vue), **backends** (Node.js), **mobile** (React Native), and **tooling**. Angular is built entirely in TypeScript, and most major JavaScript projects have added TypeScript support.

## Basic Syntax

**Definition:** TypeScript files use `.ts` (or `.tsx` for JSX) — compiled to JavaScript with the `tsc` compiler.

### Install & Compile
**Definition:** Set up TypeScript and compile `.ts` files to JavaScript.
```bash
npm install -g typescript          # Install globally
npm install --save-dev typescript  # Install as dev dependency

tsc hello.ts                       # Compile one file
tsc                                # Compile using tsconfig.json
tsc --watch                        # Watch mode — recompile on change
tsc --init                         # Create tsconfig.json
tsc --noEmit                       # Type check only, no output files

# Run TypeScript directly
npm install -g ts-node
ts-node script.ts

# Or with tsx (faster)
npm install -g tsx
tsx script.ts
```

### Basic Example
**Definition:** TypeScript looks like JavaScript with type annotations added after variable and parameter names.
```typescript
// JavaScript
function greet(name) {
    return "Hello, " + name;
}

// TypeScript — add types with `: type`
function greet(name: string): string {
    return `Hello, ${name}!`;
}

greet("Dark");     // ✅ OK
greet(42);         // ❌ Argument of type 'number' is not assignable to type 'string'
```

### Comments
**Definition:** Same as JavaScript — single line, multi-line, and JSDoc.
```typescript
// Single-line comment

/* Multi-line
   comment */

/**
 * JSDoc comment — used for IDE hints and docs
 * @param name - The user's name
 * @param age  - The user's age
 * @returns A greeting string
 */
function greet(name: string, age: number): string {
    return `Hello ${name}, age ${age}`;
}
```

---

## Type Annotations

**Definition:** Explicitly declare what type a variable, parameter, or return value should be.

### Variable Annotations
**Definition:** Add `: type` after a variable name to declare its type.
```typescript
let name:    string  = "Dark";
let age:     number  = 25;
let isAdmin: boolean = true;
let nothing: null    = null;
let undef:   undefined = undefined;

// Annotation without initialization
let score: number;
score = 100;     // ✅
score = "high";  // ❌ Type 'string' not assignable to 'number'

// Const — type inferred as literal
const PI = 3.14;     // Type: 3.14 (literal)
const NAME = "Dark"; // Type: "Dark" (literal)
```

### Function Annotations
**Definition:** Type every parameter and the return value.
```typescript
// Parameters and return type
function add(a: number, b: number): number {
    return a + b;
}

// Arrow function
const multiply = (a: number, b: number): number => a * b;

// No return value
function logMessage(msg: string): void {
    console.log(msg);
}

// Function type annotation
let operation: (a: number, b: number) => number;
operation = (x, y) => x + y;    // Types inferred from annotation
```

---

## Primitive Types

**Definition:** The basic building blocks — TypeScript's primitive types mirror JavaScript's.

### Core Primitives
**Definition:** The eight primitive types available in TypeScript.
```typescript
// String
let name: string = "Dark";
let greeting: string = `Hello, ${name}`;

// Number — integers and floats are both 'number'
let age:   number = 25;
let price: number = 9.99;
let hex:   number = 0xFF;
let big:   bigint = 9007199254740991n;    // BigInt

// Boolean
let isActive: boolean = true;
let isDone:   boolean = false;

// Symbol
let sym1: symbol = Symbol("key");
let sym2: unique symbol = Symbol();    // Unique symbol type

// Null and Undefined
let nothing: null      = null;
let undef:   undefined = undefined;
```

---

## Special Types

**Definition:** TypeScript-specific types that handle dynamic or unknown values — use carefully.

### any
**Definition:** Disables type checking — the escape hatch, but defeats the purpose of TypeScript.
```typescript
let data: any = "hello";
data = 42;         // ✅ OK
data = true;       // ✅ OK
data.foo.bar.baz;  // ✅ No error — but may crash at runtime!

// Avoid any — use unknown instead
```

### unknown
**Definition:** Like `any` but safer — must narrow the type before using it.
```typescript
let input: unknown = getUserInput();

// Must check type before using
if (typeof input === "string") {
    console.log(input.toUpperCase());   // ✅ Now known to be string
}

if (input instanceof Error) {
    console.log(input.message);        // ✅ Now known to be Error
}

// input.toUpperCase();   // ❌ Object is of type 'unknown'
```

### never
**Definition:** Represents values that never occur — functions that always throw or have infinite loops.
```typescript
// Function that always throws
function throwError(msg: string): never {
    throw new Error(msg);
}

// Function with infinite loop
function infiniteLoop(): never {
    while (true) { }
}

// Used in exhaustive checks
type Shape = "circle" | "square";

function getArea(shape: Shape): number {
    switch (shape) {
        case "circle":  return Math.PI;
        case "square":  return 1;
        default:
            const _exhaustive: never = shape;   // Errors if a case is missing
            throw new Error(`Unknown shape: ${shape}`);
    }
}
```

### void
**Definition:** For functions that don't return a meaningful value.
```typescript
function log(msg: string): void {
    console.log(msg);
    // No return statement (or return; with no value)
}

// void vs undefined
const result: void = log("test");    // void
let x: undefined = undefined;       // undefined is a value
```

### object
**Definition:** Any non-primitive value — use specific types instead when possible.
```typescript
let obj: object = { name: "Dark" };
let arr: object = [1, 2, 3];
let fn:  object = () => {};

// {} — any non-null, non-undefined value
let nonNullable: {} = "string";    // Also valid for primitives!

// Prefer specific interfaces over object type
```

---

## Type Inference

**Definition:** TypeScript automatically deduces types from values — you don't always need explicit annotations.

### Automatic Inference
**Definition:** TypeScript infers types when a value is assigned — no annotation needed.
```typescript
// TypeScript infers all these types
let name    = "Dark";        // string
let age     = 25;            // number
let isAdmin = true;          // boolean
let items   = [1, 2, 3];    // number[]
let point   = { x: 10, y: 20 };  // { x: number, y: number }

// Return type inferred
function double(n: number) {
    return n * 2;   // Return type inferred as number
}

// Contextual typing
const arr = [1, 2, 3];
arr.map(item => item.toFixed(2));   // item inferred as number
```

### When to Annotate
**Definition:** Add explicit types when TypeScript can't infer correctly or for clarity.
```typescript
// Good — explicit annotation when type isn't obvious
const userId: string | number = getIdFromDB();    // Can be either

// Good — function parameters always need types
function process(data: unknown): string { }

// Unnecessary — inferred from value
let x: number = 42;    // The ': number' is redundant but harmless
let x = 42;            // Preferred
```

---

## Type Assertions

**Definition:** Tell TypeScript the type you know a value to be — you take responsibility for correctness.

### as Keyword
**Definition:** Assert a type using `as` — most common assertion syntax.
```typescript
// When you know more than TypeScript
const canvas = document.getElementById("myCanvas") as HTMLCanvasElement;
const ctx    = canvas.getContext("2d")!;   // Non-null assertion

const input  = event.target as HTMLInputElement;
const value  = input.value;

// const assertion — make everything readonly and literal
const config = {
    host: "localhost",
    port: 5432
} as const;
// Type: { readonly host: "localhost", readonly port: 5432 }

config.host = "other";   // ❌ Cannot assign to 'host' — read only

// const assertion on arrays
const directions = ["north", "south", "east", "west"] as const;
// Type: readonly ["north", "south", "east", "west"]
type Direction = typeof directions[number];   // "north" | "south" | "east" | "west"
```

### Double Assertion
**Definition:** Use a double assertion when direct cast isn't possible — use sparingly.
```typescript
// Sometimes you need to go through unknown first
const str = (value as unknown) as string;
const num = "42" as unknown as number;    // Forces the type — risky!
```

---

## Union Types

**Definition:** A value can be one of several types — use `|` to combine types.

### Basic Union
**Definition:** Declare that a value can be any one of the listed types.
```typescript
let id: string | number;
id = "abc-123";   // ✅
id = 42;          // ✅
id = true;        // ❌ Not in the union

// Union in function parameters
function formatId(id: string | number): string {
    return `ID: ${id}`;
}

// Union of many types
type Input = string | number | boolean | null | undefined;
```

### Narrowing Unions
**Definition:** TypeScript narrows the type inside conditional blocks — use typeof, instanceof, etc.
```typescript
function processInput(input: string | number): string {
    if (typeof input === "string") {
        return input.toUpperCase();   // TypeScript knows it's string here
    } else {
        return input.toFixed(2);      // TypeScript knows it's number here
    }
}

function handleError(err: Error | string): string {
    if (err instanceof Error) {
        return err.message;           // err is Error
    }
    return err;                       // err is string
}
```

---

## Intersection Types

**Definition:** Combine multiple types into one — the result has ALL properties of both types.

### Basic Intersection
**Definition:** Use `&` to create a type with all properties from multiple types.
```typescript
type HasName = { name: string };
type HasAge  = { age: number };
type HasEmail = { email: string };

type User = HasName & HasAge & HasEmail;

const user: User = {
    name:  "Dark",
    age:   25,
    email: "dark@example.com"
};

// Mix interface and type
interface Serializable { serialize(): string; }
interface Loggable     { log(): void; }
type Service = Serializable & Loggable;
```

---

## Literal Types

**Definition:** Narrow a type to a specific value — great for constraining options to exact values.

### String & Number Literals
**Definition:** Use specific values as types — only that exact value is valid.
```typescript
// String literal type
type Direction = "north" | "south" | "east" | "west";

function move(dir: Direction): void {
    console.log(`Moving ${dir}`);
}

move("north");   // ✅
move("up");      // ❌ Not a valid Direction

// Number literal type
type DiceRoll = 1 | 2 | 3 | 4 | 5 | 6;

function roll(): DiceRoll {
    return Math.ceil(Math.random() * 6) as DiceRoll;
}

// Boolean literal (less common)
type AlwaysTrue = true;

// Combining literals and types
type Status = "active" | "inactive" | 0 | 1 | null;
```

---

## Template Literal Types

**Definition:** Create types by combining string literals with template literal syntax.

### Basic Template Literals
**Definition:** Build new string types by interpolating other types into a template.
```typescript
type EventName = "click" | "focus" | "blur";
type HandlerName = `on${Capitalize<EventName>}`;
// "onClick" | "onFocus" | "onBlur"

type CssProperty = "margin" | "padding";
type CssDirection = "top" | "right" | "bottom" | "left";
type CssClass = `${CssProperty}-${CssDirection}`;
// "margin-top" | "margin-right" | ... | "padding-left"

// With string interpolation
type ApiEndpoint = `/api/${string}`;
const url: ApiEndpoint = "/api/users";    // ✅
const url2: ApiEndpoint = "/users";       // ❌ Doesn't match pattern
```

---

## Arrays & Tuples

**Definition:** Type arrays by their element type — tuples have fixed length with known types at each position.

### Array Types
**Definition:** Two equivalent syntaxes for typed arrays.
```typescript
// Type[] syntax (preferred)
let numbers: number[] = [1, 2, 3, 4, 5];
let names:   string[] = ["Dark", "Alice", "Bob"];
let mixed:   (string | number)[] = [1, "two", 3];

// Generic Array<T> syntax (alternative)
let values: Array<number> = [1, 2, 3];
let pairs:  Array<[string, number]> = [["Dark", 25]];

// Readonly arrays
const immutable: readonly number[] = [1, 2, 3];
immutable.push(4);    // ❌ Cannot push to readonly array

const ro: ReadonlyArray<string> = ["a", "b"];
```

### Tuples
**Definition:** A fixed-length array where each position has a specific type.
```typescript
// Basic tuple
let point: [number, number] = [10, 20];
let entry: [string, number] = ["Dark", 25];

// Access typed positions
entry[0].toUpperCase();  // ✅ string method
entry[1].toFixed(2);     // ✅ number method

// Named tuple members (TypeScript 4.0+)
type Coordinate = [x: number, y: number, z?: number];
const pos: Coordinate = [10, 20];    // z is optional
const pos3d: Coordinate = [10, 20, 30];

// Tuple with rest elements
type StringsAndNumber = [...string[], number];
const arr: StringsAndNumber = ["a", "b", "c", 42];

// Readonly tuple
const rgb: readonly [number, number, number] = [255, 0, 128];
```

---

## Objects & Interfaces

**Definition:** Describe the shape of an object — its properties and their types.

### Inline Object Types
**Definition:** Describe object shape directly in the type annotation.
```typescript
let user: { name: string; age: number; email?: string } = {
    name: "Dark",
    age:  25
};

// Optional property (?)
function display(user: { name: string; age?: number }): void {
    console.log(user.name);
    console.log(user.age ?? "Age unknown");
}
```

### Interfaces
**Definition:** Named contracts for object shapes — can be extended and merged.
```typescript
interface User {
    readonly id:   number;      // Cannot be modified after creation
    name:          string;
    age:           number;
    email?:        string;      // Optional property
    address?: {                 // Optional nested object
        city:    string;
        country: string;
    };
}

const user: User = {
    id:   1,
    name: "Dark",
    age:  25
};

user.id = 2;    // ❌ Cannot assign to 'id' because it is read-only
```

### Index Signatures
**Definition:** Allow objects to have any number of properties with keys of a specific type.
```typescript
interface StringMap {
    [key: string]: string;
}

const config: StringMap = {
    host: "localhost",
    port: "5432",         // Must be string (not number)
    name: "mydb"
};

// Mixed: known properties + index signature
interface Mixed {
    id:   number;
    name: string;
    [key: string]: string | number;   // All other properties
}
```

### Interface Extension
**Definition:** Extend interfaces to create more specific types — supports multiple inheritance.
```typescript
interface Animal {
    name:  string;
    sound(): string;
}

interface Dog extends Animal {
    breed: string;
    fetch(): void;
}

// Multiple extension
interface WorkingDog extends Dog, Animal {
    task: string;
}

const rex: Dog = {
    name:  "Rex",
    breed: "Labrador",
    sound() { return "Woof!"; },
    fetch() { console.log("Fetched!"); }
};
```

### Interface Declaration Merging
**Definition:** Multiple interface declarations with the same name merge into one.
```typescript
interface Window {
    title: string;
}

interface Window {
    version: string;    // Added to Window
}

// Result: Window has both title and version
const w: Window = { title: "Home", version: "1.0" };
```

---

## Type Aliases

**Definition:** Create a name for any type — primitives, unions, intersections, and complex types.

### Basic Type Alias
**Definition:** Use `type` keyword to give a name to any type expression.
```typescript
type ID      = string | number;
type Name    = string;
type Age     = number;
type Callback = (err: Error | null, result: string) => void;
type Predicate<T> = (value: T) => boolean;

// Object type alias
type Point = {
    x: number;
    y: number;
    label?: string;
};

const p: Point = { x: 10, y: 20 };

// Complex alias
type ApiResponse<T> = {
    data:    T;
    status:  number;
    message: string;
    errors?: string[];
};
```

---

## Interface vs Type

**Definition:** Both describe types — interfaces are for objects and extendable, types are more flexible.

### Key Differences
**Definition:** Choose interfaces for object shapes and extendable contracts, types for everything else.
```typescript
// Extending
interface Animal { name: string; }
interface Dog extends Animal { breed: string; }    // Interface extends interface

type Animal = { name: string; };
type Dog    = Animal & { breed: string; };          // Type uses intersection

// Declaration merging — only interfaces can merge
interface User { name: string; }
interface User { age: number; }    // ✅ Merged: { name, age }

type User = { name: string; };
type User = { age: number; };      // ❌ Duplicate identifier

// Types can do things interfaces can't
type ID = string | number;          // Union — not possible with interface
type Pair = [string, number];       // Tuple
type Maybe<T> = T | null | undefined;
type IsString<T> = T extends string ? true : false;  // Conditional
```

| | `interface` | `type` |
|--|-------------|--------|
| Object shapes | ✅ | ✅ |
| Unions | ❌ | ✅ |
| Tuples | ❌ | ✅ |
| Extends/merges | ✅ Declaration merging | ✅ Intersection |
| Mapped types | ❌ | ✅ |
| Conditional types | ❌ | ✅ |
| **Use for** | OOP, extendable contracts | Everything else |

---

## Functions

**Definition:** TypeScript gives full type control over function signatures — parameters, return types, and overloads.

### Function Types
**Definition:** Type every parameter and return value for safe, self-documenting functions.
```typescript
// Regular function
function add(a: number, b: number): number {
    return a + b;
}

// Arrow function
const multiply = (a: number, b: number): number => a * b;

// Void return
const log = (msg: string): void => console.log(msg);

// Optional parameters
function greet(name: string, greeting?: string): string {
    return `${greeting ?? "Hello"}, ${name}!`;
}

// Default parameters (implicitly optional)
function createUser(name: string, role: string = "user"): object {
    return { name, role };
}

// Rest parameters
function sum(...nums: number[]): number {
    return nums.reduce((a, b) => a + b, 0);
}
sum(1, 2, 3, 4, 5);    // 15
```

### Function Type Signatures
**Definition:** Declare the type of a function as a value.
```typescript
// Type alias for function
type Transformer = (input: string) => string;
type Comparator<T> = (a: T, b: T) => number;
type Callback<T> = (err: Error | null, result: T) => void;

let transform: Transformer = (s) => s.toUpperCase();

// Call signatures in interfaces
interface Logger {
    (msg: string): void;
    level: "info" | "warn" | "error";
}

// Construct signatures
interface DateConstructor {
    new (timestamp: number): Date;
    new (dateString: string): Date;
}
```

### Function Overloads
**Definition:** Define multiple call signatures for a single function — different input/output combinations.
```typescript
// Overload signatures
function process(x: number):           number;
function process(x: string):           string;
function process(x: number[]):         number;

// Implementation (must handle all overloads)
function process(x: number | string | number[]): number | string {
    if (typeof x === "number") return x * 2;
    if (typeof x === "string") return x.toUpperCase();
    return x.reduce((a, b) => a + b, 0);
}

const n: number = process(5);        // TypeScript knows returns number
const s: string = process("hello"); // TypeScript knows returns string
```

---

## Generics

**Definition:** Write code that works with any type while maintaining type safety — parameterize types.

### Basic Generics
**Definition:** Use `<T>` to define a type parameter — replaced with actual type at use.
```typescript
// Generic function — works with any type
function identity<T>(arg: T): T {
    return arg;
}

const str = identity<string>("hello");   // Explicit: T = string
const num = identity(42);               // Inferred: T = number

// Generic with array
function firstOf<T>(arr: T[]): T | undefined {
    return arr[0];
}

firstOf([1, 2, 3]);          // Returns number | undefined
firstOf(["a", "b", "c"]);   // Returns string | undefined
```

### Generic Interfaces & Classes
**Definition:** Create interfaces and classes that work with any type.
```typescript
// Generic interface
interface Box<T> {
    value:   T;
    isEmpty: boolean;
    getValue(): T;
}

// Generic class
class Stack<T> {
    private items: T[] = [];

    push(item: T): void {
        this.items.push(item);
    }

    pop(): T | undefined {
        return this.items.pop();
    }

    peek(): T | undefined {
        return this.items[this.items.length - 1];
    }

    get size(): number {
        return this.items.length;
    }
}

const numStack = new Stack<number>();
numStack.push(1);
numStack.push(2);
numStack.pop();    // Returns number | undefined

const strStack = new Stack<string>();
strStack.push("hello");
```

### Multiple Type Parameters
**Definition:** Generics can have multiple type parameters.
```typescript
function pair<K, V>(key: K, value: V): [K, V] {
    return [key, value];
}

pair("name", "Dark");   // [string, string]
pair(1, true);          // [number, boolean]

// Generic with default
function createPair<K = string, V = number>(
    key: K,
    value: V
): Map<K, V> {
    return new Map([[key, value]]);
}
```

---

## Generic Constraints

**Definition:** Restrict what types can be used as a type parameter using `extends`.

### extends Constraint
**Definition:** Require type parameter to have certain properties.
```typescript
// T must have a .length property
function logLength<T extends { length: number }>(arg: T): void {
    console.log(arg.length);
}

logLength("hello");       // ✅ string has .length
logLength([1, 2, 3]);     // ✅ array has .length
logLength(42);            // ❌ number doesn't have .length

// keyof constraint — T must be a key of K
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
    return obj[key];
}

const user = { name: "Dark", age: 25 };
getProperty(user, "name");    // ✅ Returns string
getProperty(user, "age");     // ✅ Returns number
getProperty(user, "email");   // ❌ Not a key of user
```

### Conditional Constraint
**Definition:** Use conditional types within constraints for more flexible type parameters.
```typescript
// Only allow array types
function flatten<T extends any[]>(arr: T): T[number][] {
    return ([] as T[number][]).concat(...arr);
}

// Constraint with union
function process<T extends string | number>(value: T): T {
    return value;
}
```

---

## Enums

**Definition:** Named constants — numeric (auto-incremented) or string-based. TypeScript-specific feature.

### Numeric Enum
**Definition:** Members are automatically assigned incrementing numbers starting from 0.
```typescript
enum Direction {
    Up,        // 0
    Down,      // 1
    Left,      // 2
    Right      // 3
}

// Custom starting value
enum Status {
    Pending  = 1,
    Active   = 2,
    Inactive = 3,
    Banned   = 10
}

let dir: Direction = Direction.Up;     // 0
console.log(Direction[0]);             // "Up" — reverse mapping
console.log(Direction.Up);            // 0
```

### String Enum
**Definition:** Members have explicit string values — no reverse mapping, more readable.
```typescript
enum Color {
    Red   = "RED",
    Green = "GREEN",
    Blue  = "BLUE"
}

enum HttpMethod {
    GET    = "GET",
    POST   = "POST",
    PUT    = "PUT",
    DELETE = "DELETE"
}

let method: HttpMethod = HttpMethod.GET;    // "GET"
```

### Const Enum
**Definition:** Compiled away entirely — replaced with literal values for better performance.
```typescript
const enum Weekday {
    Monday = 1,
    Tuesday,
    Wednesday,
    Thursday,
    Friday
}

// Compiles to just the value, not an object
const day = Weekday.Monday;    // Compiles to: const day = 1;
```

---

## Classes

**Definition:** TypeScript enhances ES6 classes with access modifiers, readonly, and full type support.

### Basic Class
**Definition:** Define a class with typed properties, constructor, and methods.
```typescript
class Person {
    // Property declarations
    name:  string;
    age:   number;
    email: string;

    constructor(name: string, age: number, email: string) {
        this.name  = name;
        this.age   = age;
        this.email = email;
    }

    greet(): string {
        return `Hello, I'm ${this.name}`;
    }

    birthday(): void {
        this.age++;
    }
}

const person = new Person("Dark", 25, "dark@example.com");
console.log(person.greet());    // "Hello, I'm Dark"
```

### Constructor Shorthand
**Definition:** Declare and initialize properties directly in constructor parameters.
```typescript
class User {
    constructor(
        public    name:     string,
        private   password: string,
        protected age:      number,
        readonly  id:       number
    ) {
        // Properties automatically created and assigned
    }

    // Method using these properties
    authenticate(pwd: string): boolean {
        return this.password === pwd;
    }
}

const user = new User("Dark", "secret", 25, 1);
user.name;      // ✅ public
user.password;  // ❌ private
user.age;       // ❌ protected
user.id = 2;    // ❌ readonly
```

### Getters & Setters
**Definition:** Computed properties with validation logic on get/set.
```typescript
class Circle {
    private _radius: number;

    constructor(radius: number) {
        this._radius = radius;
    }

    get radius(): number {
        return this._radius;
    }

    set radius(value: number) {
        if (value < 0) throw new Error("Radius cannot be negative");
        this._radius = value;
    }

    get area(): number {
        return Math.PI * this._radius ** 2;
    }
}

const c = new Circle(5);
c.radius = 10;      // Uses setter
console.log(c.area); // Uses getter
```

### Static Members
**Definition:** Properties and methods on the class itself — shared across all instances.
```typescript
class MathUtils {
    static readonly PI: number = 3.14159;
    private static _count: number = 0;

    static increment(): number {
        return ++MathUtils._count;
    }

    static reset(): void {
        MathUtils._count = 0;
    }

    static add(a: number, b: number): number {
        return a + b;
    }
}

MathUtils.add(3, 4);        // 7
MathUtils.PI;               // 3.14159
MathUtils.increment();      // 1
```

---

## Access Modifiers

**Definition:** Control which code can access class members — public, private, protected, and readonly.

### Modifier Types
**Definition:** Four visibility modifiers — apply at class design time.
```typescript
class BankAccount {
    public     owner:   string;    // Accessible everywhere
    protected  bank:    string;    // Accessible in class + subclasses
    private    balance: number;    // Only accessible in this class
    readonly   id:      string;    // Can only be set in constructor

    // New JS private fields (runtime private)
    #secretKey: string;           // True private — not even in compiled JS

    constructor(owner: string, initialBalance: number) {
        this.owner   = owner;
        this.bank    = "State Bank";
        this.balance = initialBalance;
        this.id      = crypto.randomUUID();
        this.#secretKey = "secret";
    }

    // public method
    deposit(amount: number): void {
        if (amount > 0) this.balance += amount;
    }

    // private helper
    private validateAmount(amount: number): boolean {
        return amount > 0 && amount <= this.balance;
    }

    withdraw(amount: number): boolean {
        if (!this.validateAmount(amount)) return false;
        this.balance -= amount;
        return true;
    }

    getBalance(): number {
        return this.balance;
    }
}

class PremiumAccount extends BankAccount {
    getBank(): string {
        return this.bank;     // ✅ protected — accessible in subclass
        // this.balance       // ❌ private — not accessible
    }
}
```

---

## Abstract Classes

**Definition:** Cannot be instantiated directly — serve as base classes with partial implementation.

### Abstract Class Pattern
**Definition:** Define abstract methods that subclasses must implement.
```typescript
abstract class Shape {
    abstract area():      number;     // Must be implemented
    abstract perimeter(): number;     // Must be implemented

    // Concrete method — inherited as-is
    describe(): string {
        return `${this.constructor.name}: area=${this.area().toFixed(2)}`;
    }
}

class Rectangle extends Shape {
    constructor(
        private width:  number,
        private height: number
    ) {
        super();
    }

    area():      number { return this.width * this.height; }
    perimeter(): number { return 2 * (this.width + this.height); }
}

class Circle extends Shape {
    constructor(private radius: number) {
        super();
    }

    area():      number { return Math.PI * this.radius ** 2; }
    perimeter(): number { return 2 * Math.PI * this.radius; }
}

// const s = new Shape();   // ❌ Cannot instantiate abstract class

const shapes: Shape[] = [new Rectangle(10, 5), new Circle(7)];
shapes.forEach(s => console.log(s.describe()));
```

---

## Decorators

**Definition:** Functions that modify classes, methods, or properties — require `experimentalDecorators` in tsconfig.

### Class & Method Decorators
**Definition:** Wrap or annotate classes and methods with metadata or behavior.
```typescript
// Enable in tsconfig.json: "experimentalDecorators": true

// Class decorator
function sealed(constructor: Function) {
    Object.seal(constructor);
    Object.seal(constructor.prototype);
}

// Method decorator
function log(target: any, key: string, descriptor: PropertyDescriptor) {
    const original = descriptor.value;
    descriptor.value = function(...args: any[]) {
        console.log(`Calling ${key} with:`, args);
        const result = original.apply(this, args);
        console.log(`${key} returned:`, result);
        return result;
    };
    return descriptor;
}

// Property decorator
function readonly(target: any, key: string) {
    Object.defineProperty(target, key, { writable: false });
}

@sealed
class UserService {
    @readonly
    version = "1.0";

    @log
    getUser(id: number): string {
        return `User ${id}`;
    }
}
```

---

## Modules

**Definition:** TypeScript follows ES modules — `import` and `export` for sharing code between files.

### Export Types
**Definition:** Export values, types, interfaces, and classes from a module.
```typescript
// Named exports
export const PI = 3.14159;
export function add(a: number, b: number): number { return a + b; }
export interface User { name: string; age: number; }
export type ID = string | number;
export class UserService { }

// Default export — one per file
export default function greet(name: string): string {
    return `Hello, ${name}!`;
}

// Re-export from another module
export { PI as CirclePI } from './math';
export * from './utils';
export * as utils from './utils';
```

### Import Types
**Definition:** Import values, types, and modules — type imports are erased at compile time.
```typescript
// Named imports
import { add, PI, type User } from './math';

// Default import
import greet from './greet';

// Namespace import
import * as MathUtils from './math';
MathUtils.add(1, 2);

// Type-only import (never emitted in output)
import type { User, ID } from './types';

// Dynamic import (lazy loading)
const module = await import('./heavy-module');
module.doSomething();
```

---

## Namespaces

**Definition:** Group related code under a named scope — older alternative to ES modules.

### Namespace Usage
**Definition:** Organize code into logical groups — mostly used in declaration files.
```typescript
namespace Validation {
    export interface StringValidator {
        isAcceptable(s: string): boolean;
    }

    export class EmailValidator implements StringValidator {
        isAcceptable(s: string): boolean {
            return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(s);
        }
    }
}

const validator = new Validation.EmailValidator();
validator.isAcceptable("dark@example.com");   // true

// Nested namespaces
namespace App.Services {
    export class UserService { }
}
const svc = new App.Services.UserService();
```

---

## Utility Types

**Definition:** Built-in generic types that transform other types — TypeScript's standard type library.

### Object Utility Types
**Definition:** Transform object types by making properties optional, required, or readonly.
```typescript
interface User {
    id:      number;
    name:    string;
    email:   string;
    age:     number;
    role:    "admin" | "user";
}

// Partial<T> — all properties become optional
type PartialUser = Partial<User>;
// { id?: number; name?: string; email?: string; ... }

// Required<T> — all optional properties become required
interface Config {
    host?:  string;
    port?:  number;
    name?:  string;
}
type RequiredConfig = Required<Config>;
// { host: string; port: number; name: string; }

// Readonly<T> — all properties become readonly
type ReadonlyUser = Readonly<User>;
// All properties have 'readonly' modifier

// Pick<T, K> — select specific properties
type UserPreview = Pick<User, "id" | "name">;
// { id: number; name: string; }

// Omit<T, K> — exclude specific properties
type UserWithoutPassword = Omit<User, "email" | "role">;
// { id: number; name: string; age: number; }

// Record<K, V> — create object type with specific keys and value type
type StatusMap  = Record<"active" | "inactive", boolean>;
type UserById   = Record<number, User>;
type CacheEntry = Record<string, { value: unknown; expiry: number }>;
```

### Function Utility Types
**Definition:** Extract type information from function types.
```typescript
function getUser(id: number, name: string): User { }

// ReturnType<T> — extract return type
type UserReturn = ReturnType<typeof getUser>;        // User

// Parameters<T> — extract parameters as tuple
type GetUserParams = Parameters<typeof getUser>;     // [number, string]

// ConstructorParameters<T> — constructor parameter types
type DateParams = ConstructorParameters<typeof Date>; // string | number | ...

// InstanceType<T> — instance type of constructor
class MyClass { }
type Instance = InstanceType<typeof MyClass>;    // MyClass
```

### String Utility Types
**Definition:** Transform string literal types — uppercase, lowercase, capitalize.
```typescript
type Upper = Uppercase<"hello">;         // "HELLO"
type Lower = Lowercase<"HELLO">;         // "hello"
type Cap   = Capitalize<"hello">;        // "Hello"
type Uncap = Uncapitalize<"Hello">;      // "hello"

// With template literals
type EventName = "click" | "focus" | "change";
type HandlerName = `on${Capitalize<EventName>}`;
// "onClick" | "onFocus" | "onChange"
```

### Set Utility Types
**Definition:** Types for working with union types.
```typescript
// Exclude<T, U> — remove types from union
type Primitive = string | number | boolean | null | undefined;
type NonNullPrimitive = Exclude<Primitive, null | undefined>;
// string | number | boolean

// Extract<T, U> — keep only types in union
type StringOrNumber = Extract<Primitive, string | number>;
// string | number

// NonNullable<T> — remove null and undefined
type SafeString = NonNullable<string | null | undefined>;
// string
```

---

## Conditional Types

**Definition:** Types that depend on a condition — similar to ternary operator but for types.

### Basic Conditional Types
**Definition:** Use `T extends U ? X : Y` to create types that vary based on another type.
```typescript
// T extends U ? TypeIfTrue : TypeIfFalse
type IsString<T> = T extends string ? true : false;

type A = IsString<string>;   // true
type B = IsString<number>;   // false

// Useful conditional types
type IsArray<T>   = T extends any[]  ? true : false;
type Flatten<T>   = T extends Array<infer U> ? U : T;

// Flatten examples
type FlatString = Flatten<string[]>;    // string
type FlatNumber = Flatten<number[]>;    // number
type FlatNested = Flatten<string>;      // string (not an array, returns as-is)
```

### infer Keyword
**Definition:** Extract a type from within another type — used in conditional types.
```typescript
// Extract return type
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : never;

// Extract first parameter type
type FirstParam<T> = T extends (first: infer F, ...rest: any[]) => any ? F : never;

// Extract Promise value type
type Awaited<T> = T extends Promise<infer U> ? Awaited<U> : T;

type PromiseString = Awaited<Promise<string>>;  // string
type NestedPromise = Awaited<Promise<Promise<number>>>;  // number

// Extract array element type
type ArrayElement<T> = T extends (infer U)[] ? U : never;
type NumType = ArrayElement<number[]>;   // number
```

---

## Mapped Types

**Definition:** Create new types by transforming the properties of an existing type.

### Basic Mapped Types
**Definition:** Iterate over properties of a type and transform each one.
```typescript
// Make all properties optional (same as Partial<T>)
type Optional<T> = {
    [K in keyof T]?: T[K];
};

// Make all properties readonly (same as Readonly<T>)
type Immutable<T> = {
    readonly [K in keyof T]: T[K];
};

// Make all properties nullable
type Nullable<T> = {
    [K in keyof T]: T[K] | null;
};

// Make all properties string
type Stringify<T> = {
    [K in keyof T]: string;
};
```

### Property Modifiers
**Definition:** Add or remove modifiers with `+` and `-` prefixes.
```typescript
// Remove readonly
type Mutable<T> = {
    -readonly [K in keyof T]: T[K];
};

// Remove optional (make required)
type RequiredAll<T> = {
    [K in keyof T]-?: T[K];
};

// Add both readonly and optional
type StrictPartial<T> = {
    +readonly [K in keyof T]+?: T[K];
};
```

### Key Remapping (TypeScript 4.1+)
**Definition:** Transform key names in mapped types using `as`.
```typescript
type Getters<T> = {
    [K in keyof T as `get${Capitalize<string & K>}`]: () => T[K];
};

interface User { name: string; age: number; }
type UserGetters = Getters<User>;
// { getName: () => string; getAge: () => number; }

// Filter keys
type OnlyStrings<T> = {
    [K in keyof T as T[K] extends string ? K : never]: T[K];
};

type StringProps = OnlyStrings<{ name: string; age: number; active: boolean }>;
// { name: string }
```

---

## Template Literal Types (Advanced)

**Definition:** Combine string literals, unions, and transformations to create powerful string type patterns.

### Advanced Patterns
**Definition:** Build complex string type patterns for APIs, events, and CSS.
```typescript
type HttpMethod = "GET" | "POST" | "PUT" | "DELETE" | "PATCH";
type ApiVersion = "v1" | "v2";
type Resource   = "users" | "posts" | "comments";

// Create full API path type
type ApiPath = `/${ApiVersion}/${Resource}`;
// "/v1/users" | "/v1/posts" | "/v2/users" | ... (6 combinations)

// Event handler name generation
type EventMap = {
    click:    MouseEvent;
    keydown:  KeyboardEvent;
    resize:   UIEvent;
};

type EventHandlers = {
    [K in keyof EventMap as `on${Capitalize<K>}`]: (event: EventMap[K]) => void;
};
// { onClick: (event: MouseEvent) => void; onKeydown: ...; onResize: ...; }

// CSS property names
type Side = "top" | "right" | "bottom" | "left";
type Spacing = `${"margin" | "padding"}-${Side}`;
// "margin-top" | "margin-right" | ... | "padding-left"
```

---

## Index Types

**Definition:** Access the type of an object's properties — `keyof` for keys, `T[K]` for value types.

### keyof
**Definition:** Get the union of all keys of a type.
```typescript
interface User {
    id:    number;
    name:  string;
    email: string;
}

type UserKeys = keyof User;   // "id" | "name" | "email"

// Use keyof to constrain keys
function getField<T, K extends keyof T>(obj: T, key: K): T[K] {
    return obj[key];
}

const user: User = { id: 1, name: "Dark", email: "dark@ex.com" };
const name  = getField(user, "name");    // Returns string
const id    = getField(user, "id");      // Returns number
// getField(user, "phone")               // ❌ Not a key of User
```

### Indexed Access Types
**Definition:** Get the type of a specific property using `T[K]` syntax.
```typescript
type UserName   = User["name"];      // string
type UserId     = User["id"];        // number
type UserValues = User[keyof User];  // number | string (all value types)

// Array element type
type Arr    = string[];
type Elem   = Arr[number];    // string

// Tuple element type
type Tuple  = [string, number, boolean];
type First  = Tuple[0];       // string
type Second = Tuple[1];       // number
```

---

## Declaration Files (.d.ts)

**Definition:** Type definitions for JavaScript libraries — tell TypeScript about external code's types.

### Create Declaration File
**Definition:** Write `.d.ts` files to add types to untyped JavaScript libraries.
```typescript
// math.d.ts — declares types for a math.js file
declare function add(a: number, b: number): number;
declare function multiply(a: number, b: number): number;
declare const PI: number;
declare class Calculator {
    add(a: number, b: number): number;
}

// Declare a module (for npm packages)
declare module 'my-package' {
    export function greet(name: string): string;
    export interface Config { debug: boolean; }
    export default class MyClass { }
}

// Declare global augmentation
declare global {
    interface Window {
        myCustomProperty: string;
    }
    function myGlobalFunction(): void;
    var GLOBAL_CONFIG: { version: string };
}
```

### DefinitelyTyped (@types)
**Definition:** Community type definitions for popular JavaScript packages.
```bash
# Install type definitions
npm install --save-dev @types/node
npm install --save-dev @types/express
npm install --save-dev @types/lodash

# Libraries with built-in types (no @types needed)
# axios, zod, prisma, date-fns, etc.
```

---

## Type Guards

**Definition:** Functions and checks that narrow a type within a conditional block.

### Built-in Type Guards
**Definition:** Use typeof, instanceof, and in to narrow types automatically.
```typescript
// typeof — for primitives
function process(val: string | number): string {
    if (typeof val === "string") {
        return val.toUpperCase();   // string
    }
    return val.toFixed(2);         // number
}

// instanceof — for class instances
function format(val: Date | string): string {
    if (val instanceof Date) {
        return val.toISOString();   // Date
    }
    return val;                    // string
}

// in — check for property existence
interface Cat { meow(): void; }
interface Dog { bark(): void; }

function makeSound(animal: Cat | Dog): void {
    if ("meow" in animal) {
        animal.meow();    // Cat
    } else {
        animal.bark();    // Dog
    }
}
```

### Custom Type Guards
**Definition:** Write your own type narrowing functions using `is` return type.
```typescript
// Type predicate: 'value is Type'
function isString(value: unknown): value is string {
    return typeof value === "string";
}

function isError(value: unknown): value is Error {
    return value instanceof Error;
}

interface User { name: string; age: number; }
function isUser(value: unknown): value is User {
    return (
        typeof value === "object" &&
        value !== null &&
        "name" in value &&
        "age" in value &&
        typeof (value as User).name === "string" &&
        typeof (value as User).age  === "number"
    );
}

// Use the guard
const data: unknown = fetchData();
if (isUser(data)) {
    console.log(data.name);    // TypeScript knows data is User
}

// Assertion functions (TypeScript 3.7+)
function assertIsString(val: unknown): asserts val is string {
    if (typeof val !== "string") {
        throw new Error(`Expected string, got ${typeof val}`);
    }
}

let val: unknown = "hello";
assertIsString(val);
val.toUpperCase();    // ✅ TypeScript now knows val is string
```

---

## Discriminated Unions

**Definition:** Union types where a common "discriminant" property uniquely identifies each type — exhaustive matching.

### Pattern
**Definition:** Each union member has a unique literal type property — enables safe, exhaustive handling.
```typescript
// Each shape has a unique 'kind' property
type Circle    = { kind: "circle";    radius: number; };
type Rectangle = { kind: "rectangle"; width: number; height: number; };
type Triangle  = { kind: "triangle";  base: number;  height: number; };

type Shape = Circle | Rectangle | Triangle;

// TypeScript narrows based on 'kind'
function getArea(shape: Shape): number {
    switch (shape.kind) {
        case "circle":
            return Math.PI * shape.radius ** 2;    // shape is Circle
        case "rectangle":
            return shape.width * shape.height;     // shape is Rectangle
        case "triangle":
            return 0.5 * shape.base * shape.height; // shape is Triangle
        default:
            const _exhaustive: never = shape;       // Error if case missing
            throw new Error("Unknown shape");
    }
}

// Discriminated union for API responses
type ApiSuccess<T> = { status: "success"; data: T; };
type ApiError      = { status: "error"; error: string; code: number; };
type ApiResult<T>  = ApiSuccess<T> | ApiError;

function handleResult<T>(result: ApiResult<T>): T {
    if (result.status === "success") {
        return result.data;     // TypeScript knows: ApiSuccess<T>
    }
    throw new Error(`${result.code}: ${result.error}`);  // ApiError
}
```

---

## Nullability & Optional Chaining

**Definition:** TypeScript has strict null checking — use optional chaining and nullish coalescing for safety.

### Strict Null Checks
**Definition:** With `"strictNullChecks": true`, null and undefined are not assignable to other types.
```typescript
// With strictNullChecks enabled
let name: string  = "Dark";
name = null;       // ❌ null is not assignable to string

let nullableName: string | null = "Dark";
nullableName = null;    // ✅ explicitly allows null

// Optional properties are automatically T | undefined
interface User {
    name:   string;
    email?: string;    // string | undefined
}

function greet(user: User): string {
    return `Hello, ${user.email ?? "no email"}`;
}
```

### Optional Chaining
**Definition:** Access nested properties safely — returns undefined instead of throwing.
```typescript
interface User {
    name:     string;
    address?: {
        city?:    string;
        country?: string;
    };
    greet?(): string;
}

const user: User = { name: "Dark" };

// Without optional chaining — throws if address is undefined
user.address.city;         // ❌ TypeError!

// With optional chaining — returns undefined safely
user.address?.city;        // undefined (no error)
user.address?.city?.toLowerCase();   // undefined
user.greet?.();            // undefined if method doesn't exist

// With arrays
const arr: number[] | undefined = getNumbers();
arr?.[0];                  // Safe array access
```

### Non-null Assertion
**Definition:** Tell TypeScript a value is definitely not null or undefined — use carefully.
```typescript
// ! operator — use when you are sure it's not null
const canvas = document.getElementById("canvas")!;  // Assert non-null
const ctx    = canvas.getContext("2d")!;             // Assert non-null

// Use only when you're absolutely certain — no runtime check!
function processUser(user: User | null): string {
    // If you KNOW user is not null here for some external reason:
    return user!.name;     // Risky — will throw if user is actually null
}
```

---

## TypeScript with React

**Definition:** Type React components, hooks, events, and props — eliminates runtime type errors.

### Component Types
**Definition:** Type functional components with prop interfaces.
```typescript
import { FC, ReactNode, ReactElement } from 'react';

// Props interface
interface ButtonProps {
    label:     string;
    onClick:   () => void;
    variant?:  "primary" | "secondary" | "danger";
    disabled?: boolean;
    children?: ReactNode;    // Any renderable content
}

// FC (FunctionComponent) with generic props
const Button: FC<ButtonProps> = ({
    label,
    onClick,
    variant = "primary",
    disabled = false
}) => (
    <button
        className={`btn btn-${variant}`}
        onClick={onClick}
        disabled={disabled}
    >
        {label}
    </button>
);

// Or inline props (no FC)
function Card({
    title,
    children
}: {
    title:    string;
    children: ReactNode;
}): ReactElement {
    return <div><h2>{title}</h2>{children}</div>;
}
```

### Typed Hooks
**Definition:** Add types to useState, useRef, useReducer, and useContext.
```typescript
import { useState, useRef, useReducer, useContext, createContext } from 'react';

// useState
const [count,  setCount]  = useState<number>(0);
const [user,   setUser]   = useState<User | null>(null);
const [items,  setItems]  = useState<string[]>([]);

// useRef — DOM element
const inputRef = useRef<HTMLInputElement>(null);
const divRef   = useRef<HTMLDivElement>(null);

// useRef — mutable value
const timerRef = useRef<ReturnType<typeof setInterval>>(null);

// useReducer
type State  = { count: number; error: string | null; };
type Action = { type: "INCREMENT" } | { type: "SET_ERROR"; payload: string };

const [state, dispatch] = useReducer(
    (state: State, action: Action): State => {
        switch (action.type) {
            case "INCREMENT":  return { ...state, count: state.count + 1 };
            case "SET_ERROR":  return { ...state, error: action.payload };
        }
    },
    { count: 0, error: null }
);

// useContext with type
const ThemeContext = createContext<{ theme: string; toggle: () => void } | null>(null);
const { theme } = useContext(ThemeContext)!;
```

### Event Handlers
**Definition:** Type all event handlers with specific React event types.
```typescript
import {
    ChangeEvent, MouseEvent, FormEvent,
    KeyboardEvent, FocusEvent, DragEvent
} from 'react';

function Form() {
    const handleChange = (e: ChangeEvent<HTMLInputElement>): void => {
        console.log(e.target.value);
        console.log(e.target.name);
    };

    const handleTextArea = (e: ChangeEvent<HTMLTextAreaElement>): void => { };
    const handleSelect   = (e: ChangeEvent<HTMLSelectElement>): void => { };

    const handleClick  = (e: MouseEvent<HTMLButtonElement>): void => {
        console.log(e.clientX, e.clientY);
    };

    const handleSubmit = (e: FormEvent<HTMLFormElement>): void => {
        e.preventDefault();
    };

    const handleKey    = (e: KeyboardEvent<HTMLInputElement>): void => {
        if (e.key === "Enter") { }
        if (e.ctrlKey && e.key === "s") { }
    };

    return (
        <form onSubmit={handleSubmit}>
            <input onChange={handleChange} onKeyDown={handleKey} />
            <button onClick={handleClick}>Submit</button>
        </form>
    );
}
```

---

## TypeScript Config (tsconfig.json)

**Definition:** Configure TypeScript compiler behavior — affects what's checked and what's emitted.

### Common Configuration
**Definition:** A well-configured tsconfig for modern TypeScript projects.
```json
{
    "compilerOptions": {
        // Target & Module
        "target":       "ES2022",       // JS version to compile to
        "module":       "NodeNext",     // Module system (CommonJS, ESNext, NodeNext)
        "lib":          ["ES2022", "DOM", "DOM.Iterable"],  // Built-in type libs

        // Output
        "outDir":          "./dist",    // Where to put compiled JS
        "rootDir":         "./src",     // Where source TS files are
        "declaration":     true,        // Generate .d.ts files
        "declarationMap":  true,        // Source maps for .d.ts files
        "sourceMap":       true,        // Source maps for debugging

        // Type Checking — enable all for maximum safety
        "strict":                    true,  // Enable all strict checks below
        "noImplicitAny":             true,  // Error on implicit any
        "strictNullChecks":          true,  // null/undefined are separate types
        "strictFunctionTypes":       true,  // Strict function type checking
        "strictBindCallApply":       true,  // Strict bind/call/apply checking
        "strictPropertyInitialization": true, // Ensure class properties are initialized
        "noImplicitThis":            true,  // Error on implicit this
        "alwaysStrict":              true,  // Emit 'use strict'

        // Extra Checks
        "noUnusedLocals":            true,  // Error on unused variables
        "noUnusedParameters":        true,  // Error on unused parameters
        "noImplicitReturns":         true,  // All code paths must return
        "noFallthroughCasesInSwitch": true, // No fallthrough in switch
        "exactOptionalPropertyTypes": true,  // Strict optional properties

        // Module Resolution
        "moduleResolution": "NodeNext",  // Node.js module resolution
        "baseUrl":          "./",        // Base for non-relative imports
        "paths": {                       // Path aliases
            "@/*":           ["./src/*"],
            "@components/*": ["./src/components/*"]
        },
        "resolveJsonModule": true,       // Import JSON files
        "esModuleInterop":  true,        // Better CommonJS interop
        "allowSyntheticDefaultImports": true,

        // Misc
        "skipLibCheck":            true,  // Skip type checks in .d.ts files
        "forceConsistentCasingInFileNames": true,
        "experimentalDecorators":  true,
        "emitDecoratorMetadata":   true
    },
    "include": ["src/**/*"],
    "exclude": ["node_modules", "dist", "**/*.test.ts"]
}
```

---

## Tips & Tricks

**Definition:** Useful TypeScript patterns that improve type safety and developer experience.

### Useful Patterns
**Definition:** Practical TypeScript idioms for everyday code.
```typescript
// 1. satisfies operator (TS 4.9) — validate without widening
const config = {
    port: 3000,
    host: "localhost"
} satisfies Record<string, string | number>;
// TypeScript knows port is number (not string | number)

// 2. Infer object keys from const
const ROUTES = {
    HOME:    "/",
    ABOUT:   "/about",
    USERS:   "/users",
} as const;

type Route = typeof ROUTES[keyof typeof ROUTES];
// "/" | "/about" | "/users"

// 3. Extract type from array
const fruits = ["apple", "banana", "cherry"] as const;
type Fruit = typeof fruits[number];   // "apple" | "banana" | "cherry"

// 4. DeepReadonly — make everything recursively readonly
type DeepReadonly<T> = {
    readonly [K in keyof T]: T[K] extends object ? DeepReadonly<T[K]> : T[K];
};

// 5. Awaited — unwrap Promise type (built-in TS 4.5+)
type Result = Awaited<Promise<string>>;   // string

// 6. Prettify — flatten intersection types for readability
type Prettify<T> = { [K in keyof T]: T[K]; } & {};

type A = { name: string } & { age: number };
type PrettyA = Prettify<A>;   // { name: string; age: number }

// 7. NoInfer (TS 5.4+) — prevent type inference from a position
function createPair<T>(a: T, b: NoInfer<T>): [T, T] {
    return [a, b];
}

// 8. Use satisfies to validate config objects
const palette = {
    red:   [255, 0,   0  ],
    green: [0,   255, 0  ],
    blue:  [0,   0,   255],
} satisfies Record<string, [number, number, number]>;
palette.red;    // TypeScript knows it's [number, number, number]
```

### Type Manipulation
**Definition:** Common type utility patterns you'll want in your codebase.
```typescript
// Opaque types — branded types for type safety
type UserId  = string & { __brand: "UserId" };
type PostId  = string & { __brand: "PostId" };

function createUserId(id: string): UserId {
    return id as UserId;
}

const userId: UserId = createUserId("user-123");
// userId cannot be accidentally used where PostId is expected

// Writable<T> — remove readonly from all properties
type Writable<T> = { -readonly [K in keyof T]: T[K] };

// Deep Partial
type DeepPartial<T> = T extends object ? {
    [K in keyof T]?: DeepPartial<T[K]>;
} : T;

// XOR — exactly one of two types (mutually exclusive)
type XOR<T, U> =
    (T & { [K in Exclude<keyof U, keyof T>]?: never }) |
    (U & { [K in Exclude<keyof T, keyof U>]?: never });

// Either have 'email' OR 'phone' but not both
type Contact = XOR<{ email: string }, { phone: string }>;
```

---

## Best Practices

**Definition:** Guidelines for writing type-safe, maintainable, and idiomatic TypeScript.

### Enable Strict Mode
**Definition:** Always enable strict mode — catch more bugs at compile time.
```json
{
    "compilerOptions": {
        "strict": true    // Enable ALL strict checks — do this from day one
    }
}
```

### Prefer const & readonly
**Definition:** Immutability by default — use `const` for variables and `readonly` for properties.
```typescript
// Prefer const over let
const userId = 1;

// Readonly properties
interface Config {
    readonly host: string;
    readonly port: number;
}

// As const for literal types
const EVENTS = ["click", "hover", "focus"] as const;
type EventType = typeof EVENTS[number];
```

### Avoid any — Use unknown
**Definition:** `any` defeats the purpose of TypeScript — use `unknown` for truly unknown data.
```typescript
// BAD — any disables all type checking
function process(data: any): any {
    return data.foo.bar;    // No safety!
}

// GOOD — unknown forces you to check the type
function process(data: unknown): string {
    if (typeof data === "string") {
        return data.toUpperCase();
    }
    throw new Error("Expected string");
}

// GOOD — for external data, validate with a type guard
function parseResponse(raw: unknown): User {
    if (!isUser(raw)) throw new Error("Invalid user data");
    return raw;
}
```

### Use Discriminated Unions over Optional Properties
**Definition:** Model state with discriminated unions — prevents impossible states.
```typescript
// BAD — many impossible states possible
interface RequestState {
    loading: boolean;
    data?:   User;
    error?:  string;
}

// GOOD — every state is valid and explicit
type RequestState =
    | { status: "idle" }
    | { status: "loading" }
    | { status: "success"; data: User }
    | { status: "error";   error: string };
```

### Type Narrowing over Assertions
**Definition:** Prefer runtime checks over type assertions — safer and more correct.
```typescript
// BAD — assertion bypasses safety
const user = data as User;
user.name.toUpperCase();    // May throw if data isn't actually a User

// GOOD — type guard proves it at runtime
if (isUser(data)) {
    data.name.toUpperCase();   // Safe — proven to be User
}

// ACCEPTABLE — DOM references where you're certain
const canvas = document.getElementById("canvas") as HTMLCanvasElement;
```

### Organize Types
**Definition:** Keep types organized and colocated with their usage.
```typescript
// types.ts — central types file
export interface User { }
export type ID = string | number;

// Or colocate with usage
// user.service.ts
interface UserServiceConfig { }
export class UserService {
    constructor(private config: UserServiceConfig) { }
}
```

### Summary of Rules

* Always enable **`"strict": true`** in tsconfig — never disable it
* Use **`unknown`** instead of `any` for truly unknown data
* Prefer **interfaces** for object shapes, **types** for everything else
* Use **discriminated unions** to model state — prevents impossible states
* Use **type guards** instead of `as` assertions when possible
* Add **explicit return types** to public functions — documents intent
* Use **`as const`** for immutable literals and configuration objects
* Use **`readonly`** on properties that shouldn't change
* Keep **type definitions close** to where they're used
* Run **`tsc --noEmit`** in CI — type check without producing output
