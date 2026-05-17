# 📘 TypeScript: The Complete Handbook
### From Basics to Advanced — A Beginner-Friendly Guide

> *"TypeScript is JavaScript with syntax for types."* — TypeScript Official Docs

![TypeScript](https://img.shields.io/badge/TypeScript-5.x-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![Level](https://img.shields.io/badge/Level-Beginner%20to%20Advanced-orange?style=for-the-badge)

---

## 🤔 What is TypeScript?

**TypeScript** is a **strongly-typed, object-oriented, compiled superset of JavaScript** developed and maintained by **Microsoft**. It adds optional static typing and class-based object-oriented programming to JavaScript.

In simple words: **TypeScript = JavaScript + Type Safety + Extra Features**

Every valid JavaScript file is also a valid TypeScript file. TypeScript compiles down to plain JavaScript that runs in any browser or Node.js environment.

---

## 🚀 Why Use TypeScript?

| Feature | Benefit |
|---|---|
| **Type Safety** | Catch bugs at compile time, not at runtime |
| **Better Tooling** | Autocomplete, IntelliSense, refactoring support in VS Code |
| **Scalability** | Ideal for large codebases with multiple developers |
| **Maintainability** | Self-documenting code, easier to understand and modify |
| **Modern Features** | Supports latest ECMAScript features + more |

---

## ⚡ TypeScript vs JavaScript

| Feature | JavaScript | TypeScript |
|---|---|---|
| Typing | Dynamic (runtime) | Static (compile-time) |
| Error Detection | Runtime | Compile-time |
| IDE Support | Basic | Excellent (IntelliSense) |
| OOP Support | Partial | Full (interfaces, abstract classes) |
| Compilation | Not needed | Compiles to JS |
| Learning Curve | Lower | Slightly higher |
| Large Projects | Harder to manage | Much easier |

---

## 📚 Table of Contents

1. [TypeScript Basics](#1-typescript-basics)
   - [Installation](#installation)
   - [Setting up tsconfig.json](#setting-up-tsconfigjson)
   - [Running & Compiling TypeScript](#running--compiling-typescript)
2. [Basic Syntax](#2-basic-syntax)
   - [Variables](#variables)
   - [Data Types](#data-types)
   - [Type Inference](#type-inference)
   - [Any, Unknown, Never](#any-unknown-never)
   - [Type Assertions](#type-assertions)
   - [Union Types](#union-types)
   - [Literal Types](#literal-types)
   - [Type Aliases](#type-aliases)
   - [Interfaces](#interfaces)
3. [Operators & Control Flow](#3-operators--control-flow)
4. [Functions](#4-functions)
5. [Arrays & Objects](#5-arrays--objects)
6. [Object-Oriented Programming](#6-object-oriented-programming-oop)
7. [Advanced TypeScript](#7-advanced-typescript)
8. [Modules](#8-modules)
9. [Async Programming](#9-async-programming)
10. [DOM & Browser](#10-dom--browser)
11. [Advanced Concepts](#11-advanced-concepts)
12. [TypeScript with Frameworks](#12-typescript-with-frameworks)
13. [Best Practices](#13-best-practices)
14. [Exercises & Challenges](#14-exercises--challenges)
15. [Conclusion & Resources](#15-conclusion--resources)

---

# 1. TypeScript Basics

## Installation

### Prerequisites
- Node.js installed (v16+ recommended)
- npm or yarn package manager

### Install TypeScript Globally

```bash
# Install TypeScript globally
npm install -g typescript

# Verify installation
tsc --version
# Output: Version 5.x.x
```

### Install in a Project

```bash
# Initialize project
mkdir my-ts-project
cd my-ts-project
npm init -y

# Install TypeScript locally
npm install --save-dev typescript

# Install Node.js types (for Node projects)
npm install --save-dev @types/node
```

### Install ts-node (Run TS directly without compiling)

```bash
npm install -g ts-node

# Run a TypeScript file directly
ts-node index.ts
```

---

## Setting up tsconfig.json

**`tsconfig.json`** is the configuration file for TypeScript. It tells the TypeScript compiler how to compile your code.

### Generate tsconfig.json

```bash
tsc --init
```

### Common tsconfig.json Setup

```json
{
  "compilerOptions": {
    "target": "ES6",              // Compile to ES6 JavaScript
    "module": "commonjs",         // Module system (commonjs for Node)
    "lib": ["ES6", "DOM"],        // Libraries to include
    "outDir": "./dist",           // Output directory for compiled JS
    "rootDir": "./src",           // Source TypeScript files location
    "strict": true,               // Enable all strict type checks
    "noImplicitAny": true,        // Disallow implicit 'any' types
    "esModuleInterop": true,      // Better module interoperability
    "skipLibCheck": true,         // Skip type checking of .d.ts files
    "forceConsistentCasingInFileNames": true
  },
  "include": ["src/**/*"],        // Files to include
  "exclude": ["node_modules", "dist"]
}
```

### Key Options Explained

| Option | Purpose |
|---|---|
| `target` | Which JS version to compile to (ES5, ES6, ES2020) |
| `strict` | Enables all strict checks — highly recommended |
| `outDir` | Where compiled `.js` files go |
| `rootDir` | Where your `.ts` source files live |
| `noImplicitAny` | Forces you to explicitly type things |

> 💡 **Best Practice:** Always enable `"strict": true` in new projects.

---

## Running & Compiling TypeScript

```bash
# Compile a single file
tsc index.ts

# Compile entire project (uses tsconfig.json)
tsc

# Watch mode — auto-recompile on file changes
tsc --watch

# Run directly without compiling (with ts-node)
ts-node index.ts
```

---

# 2. Basic Syntax

## Variables

TypeScript uses the same `let`, `const`, and `var` as JavaScript, but with type annotations.

### Syntax

```typescript
let variableName: type = value;
const constantName: type = value;
```

### Examples

```typescript
// Type annotations
let name: string = "Rohit";
let age: number = 25;
let isStudent: boolean = true;

// const — immutable
const PI: number = 3.14159;

// TypeScript infers type automatically
let city = "Nagpur"; // inferred as string
// city = 42; // ❌ Error: Type 'number' is not assignable to type 'string'
```

> ⚠️ **Common Mistake:** Using `var` — prefer `let` and `const` always.

---

## Data Types

### Primitive Types

```typescript
// string
let firstName: string = "Rohit";
let greeting: string = `Hello, ${firstName}!`; // Template literals work too

// number (integers & floats — no separate types)
let score: number = 95;
let price: number = 499.99;
let hex: number = 0xff;

// boolean
let isLoggedIn: boolean = true;
let hasPermission: boolean = false;

// null and undefined
let emptyValue: null = null;
let notAssigned: undefined = undefined;

// bigint (for very large numbers)
let bigNumber: bigint = 9007199254740991n;

// symbol (unique identifiers)
let id: symbol = Symbol("userId");
```

### Special Types

```typescript
// void — for functions that return nothing
function logMessage(msg: string): void {
  console.log(msg);
}

// any — opt out of type checking (avoid if possible)
let anything: any = "hello";
anything = 42;       // OK
anything = true;     // OK

// never — for functions that never return
function throwError(msg: string): never {
  throw new Error(msg);
}
```

---

## Type Inference

TypeScript can **automatically determine** the type of a variable based on its value — you don't always need to write the type explicitly.

```typescript
// TypeScript infers these types automatically
let message = "Hello TypeScript";  // inferred: string
let count = 10;                     // inferred: number
let active = true;                  // inferred: boolean

// Inferred from function return
function add(a: number, b: number) {
  return a + b; // return type inferred as number
}

// Array inference
let numbers = [1, 2, 3];           // inferred: number[]
let mixed = [1, "hello", true];    // inferred: (string | number | boolean)[]
```

> 💡 **Tip:** Let TypeScript infer simple types, but explicitly annotate function parameters and return types.

---

## Any, Unknown, Never

These are three special types that behave very differently.

```typescript
// =====================
// any — disables type checking
// =====================
let a: any = 5;
a = "hello";           // OK — no errors
a.foo.bar.baz;         // OK — TypeScript won't check this (dangerous!)

// =====================
// unknown — safer version of any
// =====================
let u: unknown = "hello";
// u.toUpperCase();    // ❌ Error — can't use without type checking

// Must check type first
if (typeof u === "string") {
  u.toUpperCase();     // ✅ OK — type is narrowed to string
}

// =====================
// never — values that never occur
// =====================
function infiniteLoop(): never {
  while (true) {} // never returns
}

function fail(msg: string): never {
  throw new Error(msg); // never returns normally
}
```

### Comparison Table

| Type | Use Case | Safe? |
|---|---|---|
| `any` | Migration, quick prototyping | ❌ No type safety |
| `unknown` | External data, API responses | ✅ Must validate first |
| `never` | Impossible cases, exhaustive checks | ✅ Correct by design |

> 💡 **Interview Tip:** Prefer `unknown` over `any` whenever you're unsure of a type.

---

## Type Assertions

Type assertions tell TypeScript: *"Trust me, I know what type this is."* They don't perform any runtime conversion.

```typescript
// Using 'as' keyword (preferred)
let someValue: unknown = "Hello TypeScript";
let strLength: number = (someValue as string).length;

// Using angle bracket syntax (not usable in JSX)
let strLength2: number = (<string>someValue).length;

// Practical example — DOM
const inputElement = document.getElementById("myInput") as HTMLInputElement;
inputElement.value = "Hello!"; // Now TS knows it's an input element

// Non-null assertion operator (!)
const el = document.getElementById("app")!; // tells TS: this won't be null
```

> ⚠️ **Warning:** Don't overuse type assertions. They bypass type safety. Use only when you're 100% sure.

---

## Union Types

Union types allow a variable to be **one of several types**.

```typescript
// Basic union
let id: string | number;
id = 101;       // ✅
id = "A001";    // ✅
// id = true;   // ❌ Error

// Function with union parameter
function formatId(id: string | number): string {
  if (typeof id === "number") {
    return id.toString().padStart(5, "0"); // "00101"
  }
  return id.toUpperCase(); // "A001"
}

// Union with arrays
let data: string[] | number[] = [1, 2, 3];

// Union with null (common pattern)
function getUser(id: number): string | null {
  if (id === 1) return "Rohit";
  return null;
}
```

---

## Literal Types

Literal types restrict a variable to a **specific set of exact values**.

```typescript
// String literal type
type Direction = "north" | "south" | "east" | "west";
let move: Direction = "north"; // ✅
// move = "up";               // ❌ Error

// Number literal type
type DiceRoll = 1 | 2 | 3 | 4 | 5 | 6;
let roll: DiceRoll = 4;       // ✅

// Boolean literal (less common)
type AlwaysTrue = true;

// Practical example
type Status = "pending" | "active" | "inactive" | "banned";

function updateStatus(userId: number, status: Status): void {
  console.log(`User ${userId} status: ${status}`);
}

updateStatus(1, "active");    // ✅
// updateStatus(1, "deleted"); // ❌ Error
```

---

## Type Aliases

A **type alias** gives a custom name to a type. It can represent primitives, unions, intersections, objects, or functions.

```typescript
// Simple alias
type ID = string | number;
type Name = string;

// Object shape
type User = {
  id: ID;
  name: Name;
  email: string;
  age?: number;       // optional property
};

const user: User = {
  id: 1,
  name: "Rohit",
  email: "rohit@example.com",
};

// Function type alias
type AddFunction = (a: number, b: number) => number;

const add: AddFunction = (a, b) => a + b;

// Intersection type (combine types)
type Employee = User & {
  department: string;
  salary: number;
};
```

---

## Interfaces

An **interface** defines the **shape/contract** of an object. It's like a blueprint.

```typescript
// Basic interface
interface Product {
  id: number;
  name: string;
  price: number;
  description?: string;  // optional
  readonly sku: string;  // cannot be changed after creation
}

const laptop: Product = {
  id: 1,
  name: "MacBook Pro",
  price: 150000,
  sku: "MBP-2024",
};

// laptop.sku = "NEW-SKU"; // ❌ Error: readonly

// Interface with methods
interface Animal {
  name: string;
  speak(): string;
  eat(food: string): void;
}

// Implementing an interface
class Dog implements Animal {
  name: string;

  constructor(name: string) {
    this.name = name;
  }

  speak(): string {
    return `${this.name} says: Woof!`;
  }

  eat(food: string): void {
    console.log(`${this.name} is eating ${food}`);
  }
}

// Interface extending another interface
interface Vehicle {
  brand: string;
  speed: number;
}

interface ElectricVehicle extends Vehicle {
  batteryCapacity: number;
  charge(): void;
}
```

### Type Alias vs Interface

| Feature | Type Alias | Interface |
|---|---|---|
| Object shapes | ✅ | ✅ |
| Primitives/unions | ✅ | ❌ |
| Extension | `&` intersection | `extends` keyword |
| Declaration merging | ❌ | ✅ |
| Implements in class | ✅ | ✅ |

> 💡 **Rule of Thumb:** Use `interface` for object shapes and class contracts. Use `type` for unions, primitives, and complex compositions.

---

## 📝 Exercises — Section 2

1. Create a `type` for a `Student` with name, roll number, grade (A/B/C/D/F only), and optional email.
2. Write a function that accepts `string | number` and returns its length/value as a string.
3. Create an `interface` for a `BankAccount` with deposit and withdraw methods.
4. What's the difference between `unknown` and `any`? Write code showing why `unknown` is safer.

---

# 3. Operators & Control Flow

## Operators

```typescript
// Arithmetic
let a: number = 10, b: number = 3;
console.log(a + b);   // 13
console.log(a - b);   // 7
console.log(a * b);   // 30
console.log(a / b);   // 3.333...
console.log(a % b);   // 1  (modulus/remainder)
console.log(a ** b);  // 1000 (exponentiation)

// Comparison
console.log(a === b);  // false (strict equality — checks type too)
console.log(a !== b);  // true
console.log(a > b);    // true
console.log(a <= b);   // false

// Logical
let x: boolean = true, y: boolean = false;
console.log(x && y);   // false (AND)
console.log(x || y);   // true  (OR)
console.log(!x);        // false (NOT)

// Nullish Coalescing (??)
let username: string | null = null;
let displayName = username ?? "Guest"; // "Guest"

// Optional Chaining (?.)
let user = { profile: { bio: "Developer" } };
let bio = user?.profile?.bio;  // "Developer"
let missing = user?.address?.city; // undefined (no error)

// Type-specific operators
let str: string = "Hello";
console.log(typeof str);       // "string"
console.log(str instanceof String); // false (primitive, not object)
```

## Conditionals

```typescript
// if-else
let temperature: number = 38;

if (temperature > 37) {
  console.log("You have a fever 🤒");
} else if (temperature === 37) {
  console.log("Normal temperature ✅");
} else {
  console.log("Below normal 🥶");
}

// Ternary operator
let age: number = 20;
let canVote: string = age >= 18 ? "Can vote ✅" : "Cannot vote ❌";

// Nullish coalescing for defaults
function greet(name: string | null): string {
  return `Hello, ${name ?? "Guest"}!`;
}
```

## Loops

```typescript
// for loop
for (let i: number = 0; i < 5; i++) {
  console.log(`Iteration: ${i}`);
}

// for...of (iterate over values)
const fruits: string[] = ["Apple", "Mango", "Banana"];
for (const fruit of fruits) {
  console.log(fruit);
}

// for...in (iterate over keys/indices)
const person = { name: "Rohit", age: 25, city: "Nagpur" };
for (const key in person) {
  console.log(`${key}: ${person[key as keyof typeof person]}`);
}

// while loop
let count: number = 0;
while (count < 3) {
  console.log(`Count: ${count}`);
  count++;
}

// Array methods (preferred in TS)
fruits.forEach((fruit, index) => {
  console.log(`${index}: ${fruit}`);
});
```

## Switch Statements

```typescript
type Day = "Mon" | "Tue" | "Wed" | "Thu" | "Fri" | "Sat" | "Sun";

function getDayType(day: Day): string {
  switch (day) {
    case "Sat":
    case "Sun":
      return "Weekend 🎉";
    case "Mon":
    case "Tue":
    case "Wed":
    case "Thu":
    case "Fri":
      return "Weekday 💼";
    default:
      return "Unknown day";
  }
}

console.log(getDayType("Sat")); // "Weekend 🎉"
console.log(getDayType("Mon")); // "Weekday 💼"
```

---

# 4. Functions

## Function Types

```typescript
// Basic function with types
function add(a: number, b: number): number {
  return a + b;
}

// Function expression with type annotation
const multiply: (x: number, y: number) => number = (x, y) => x * y;

// Named function type
type MathOperation = (a: number, b: number) => number;
const subtract: MathOperation = (a, b) => a - b;
```

## Optional Parameters

```typescript
// Optional parameters use '?'
function greet(name: string, greeting?: string): string {
  return `${greeting ?? "Hello"}, ${name}!`;
}

greet("Rohit");              // "Hello, Rohit!"
greet("Rohit", "Namaste");   // "Namaste, Rohit!"
```

## Default Parameters

```typescript
function createUser(
  name: string,
  role: string = "user",    // default value
  isActive: boolean = true  // default value
) {
  return { name, role, isActive };
}

createUser("Rohit");                        // { name: "Rohit", role: "user", isActive: true }
createUser("Admin", "admin");              // { name: "Admin", role: "admin", isActive: true }
createUser("SuperAdmin", "superadmin", false);
```

## Rest Parameters

```typescript
// Collect remaining arguments into an array
function sumAll(...numbers: number[]): number {
  return numbers.reduce((total, n) => total + n, 0);
}

console.log(sumAll(1, 2, 3));          // 6
console.log(sumAll(10, 20, 30, 40));   // 100

// Rest with typed tuple
function logInfo(message: string, ...details: string[]): void {
  console.log(message, details.join(", "));
}
```

## Arrow Functions

```typescript
// Arrow function syntax
const square = (n: number): number => n * n;

// Multi-line arrow function
const divide = (a: number, b: number): number => {
  if (b === 0) throw new Error("Division by zero!");
  return a / b;
};

// Arrow functions in arrays
const numbers: number[] = [1, 2, 3, 4, 5];
const doubled = numbers.map((n): number => n * 2);
const evens = numbers.filter((n): boolean => n % 2 === 0);
```

## Callback Functions

```typescript
// Callback type annotation
type Callback = (error: Error | null, result?: string) => void;

function fetchData(url: string, callback: Callback): void {
  // Simulate async operation
  try {
    const data = `Data from ${url}`;
    callback(null, data);
  } catch (err) {
    callback(new Error("Failed to fetch"));
  }
}

fetchData("https://api.example.com", (err, data) => {
  if (err) {
    console.error(err.message);
    return;
  }
  console.log(data);
});
```

## Function Overloading

Function overloading allows a function to accept different argument types and return different types based on the input.

```typescript
// Overload signatures
function formatValue(value: string): string;
function formatValue(value: number): string;
function formatValue(value: boolean): string;

// Implementation signature
function formatValue(value: string | number | boolean): string {
  if (typeof value === "string") return value.toUpperCase();
  if (typeof value === "number") return value.toFixed(2);
  return value ? "Yes" : "No";
}

console.log(formatValue("hello"));  // "HELLO"
console.log(formatValue(3.14159));  // "3.14"
console.log(formatValue(true));     // "Yes"
```

---

## 📝 Exercises — Section 4

1. Write an overloaded function `combine` that concatenates strings or adds numbers.
2. Create a `calculateTax(amount, rate?)` function with optional rate defaulting to 18%.
3. Write a function using rest parameters that finds the max of any number of values.

---

# 5. Arrays & Objects

## Arrays

```typescript
// Array type annotations
let scores: number[] = [95, 87, 92, 78];
let names: Array<string> = ["Rohit", "Priya", "Amit"]; // Generic syntax

// Multidimensional arrays
let matrix: number[][] = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
];

// Common array methods (all type-safe!)
scores.push(100);               // Add to end
scores.pop();                   // Remove from end
scores.unshift(70);             // Add to start
scores.shift();                 // Remove from start

const topScores = scores.filter(s => s >= 90);      // [95, 92]
const doubled = scores.map(s => s * 2);              // type: number[]
const total = scores.reduce((sum, s) => sum + s, 0); // type: number
const found = scores.find(s => s > 90);              // type: number | undefined

// Spread operator
const allScores: number[] = [...scores, 100, 99];
```

## Tuples

Tuples are arrays with a **fixed number of elements where each position has a known type**.

```typescript
// Basic tuple
let person: [string, number, boolean] = ["Rohit", 25, true];

// Accessing tuple elements
let name = person[0];   // type: string
let age = person[1];    // type: number

// Named tuples (TypeScript 4.0+)
type Point = [x: number, y: number, z?: number];
const origin: Point = [0, 0];
const point3D: Point = [1, 2, 3];

// Destructuring tuples
const [userName, userAge] = person;

// Practical use — React useState-like pattern
type StateResult<T> = [T, (value: T) => void];

function useState<T>(initial: T): StateResult<T> {
  let value = initial;
  const setter = (v: T) => { value = v; };
  return [value, setter];
}
```

## Objects

```typescript
// Object type annotation
const car: {
  brand: string;
  model: string;
  year: number;
  electric?: boolean;
} = {
  brand: "Tata",
  model: "Nexon",
  year: 2024,
};

// Using interface (better for reuse)
interface Config {
  host: string;
  port: number;
  debug?: boolean;
}

const serverConfig: Config = {
  host: "localhost",
  port: 3000,
};

// Object destructuring with types
function displayConfig({ host, port, debug = false }: Config): void {
  console.log(`${host}:${port} | Debug: ${debug}`);
}

// Spread with objects
const updatedConfig: Config = { ...serverConfig, debug: true };
```

## Readonly Properties

```typescript
// Readonly in interface
interface DatabaseConfig {
  readonly host: string;
  readonly port: number;
  password: string;
}

const dbConfig: DatabaseConfig = {
  host: "db.server.com",
  port: 5432,
  password: "secret123",
};

// dbConfig.host = "new.server.com"; // ❌ Error: Cannot assign to 'host' (readonly)
dbConfig.password = "newpassword";    // ✅ OK

// Readonly array — cannot be mutated
const ALLOWED_ROLES: readonly string[] = ["admin", "user", "moderator"];
// ALLOWED_ROLES.push("superadmin");  // ❌ Error

// Readonly<T> utility type
type ReadonlyUser = Readonly<{ name: string; age: number }>;
const frozenUser: ReadonlyUser = { name: "Rohit", age: 25 };
// frozenUser.name = "Amit"; // ❌ Error
```

---

# 6. Object-Oriented Programming (OOP)

## Classes

```typescript
// Basic class
class Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  introduce(): string {
    return `Hi, I'm ${this.name}, ${this.age} years old.`;
  }
}

const person = new Person("Rohit", 25);
console.log(person.introduce()); // "Hi, I'm Rohit, 25 years old."
```

## Constructors

```typescript
class Rectangle {
  width: number;
  height: number;

  constructor(width: number, height: number) {
    this.width = width;
    this.height = height;
  }

  getArea(): number {
    return this.width * this.height;
  }

  getPerimeter(): number {
    return 2 * (this.width + this.height);
  }
}

const rect = new Rectangle(10, 5);
console.log(rect.getArea());       // 50
console.log(rect.getPerimeter());  // 30
```

## Access Modifiers

TypeScript provides three access modifiers:

| Modifier | Class | Subclass | Outside |
|---|---|---|---|
| `public` | ✅ | ✅ | ✅ |
| `protected` | ✅ | ✅ | ❌ |
| `private` | ✅ | ❌ | ❌ |

```typescript
class BankAccount {
  public accountHolder: string;    // accessible everywhere
  protected accountNumber: string; // accessible in class + subclasses
  private balance: number;         // accessible only in this class
  #pin: number;                    // native JS private field

  constructor(holder: string, accNum: string, initialBalance: number) {
    this.accountHolder = holder;
    this.accountNumber = accNum;
    this.balance = initialBalance;
    this.#pin = 1234;
  }

  // Shorthand constructor — same as above!
  // constructor(
  //   public accountHolder: string,
  //   protected accountNumber: string,
  //   private balance: number
  // ) {}

  public deposit(amount: number): void {
    if (amount > 0) this.balance += amount;
  }

  public getBalance(): number {
    return this.balance; // can access private from within class
  }
}

const account = new BankAccount("Rohit", "SB001234", 50000);
console.log(account.accountHolder); // ✅ "Rohit"
// console.log(account.balance);    // ❌ Error: private
account.deposit(10000);
console.log(account.getBalance());  // ✅ 60000
```

## Getters & Setters

```typescript
class Temperature {
  private _celsius: number;

  constructor(celsius: number) {
    this._celsius = celsius;
  }

  // Getter
  get fahrenheit(): number {
    return (this._celsius * 9) / 5 + 32;
  }

  // Setter with validation
  set celsius(value: number) {
    if (value < -273.15) {
      throw new Error("Temperature below absolute zero!");
    }
    this._celsius = value;
  }

  get celsius(): number {
    return this._celsius;
  }
}

const temp = new Temperature(100);
console.log(temp.fahrenheit); // 212
temp.celsius = 37;
console.log(temp.celsius);    // 37
// temp.celsius = -300;        // ❌ Error thrown
```

## Static Members

Static members belong to the **class itself**, not to instances.

```typescript
class MathHelper {
  static readonly PI: number = 3.14159265;
  private static instanceCount: number = 0;

  constructor() {
    MathHelper.instanceCount++;
  }

  static circleArea(radius: number): number {
    return MathHelper.PI * radius * radius;
  }

  static getInstanceCount(): number {
    return MathHelper.instanceCount;
  }
}

// Access without creating an instance
console.log(MathHelper.circleArea(5));    // 78.539...
console.log(MathHelper.PI);               // 3.14159...

const m1 = new MathHelper();
const m2 = new MathHelper();
console.log(MathHelper.getInstanceCount()); // 2
```

## Inheritance

```typescript
// Base class
class Animal {
  constructor(public name: string, protected sound: string) {}

  makeSound(): string {
    return `${this.name} says: ${this.sound}`;
  }

  toString(): string {
    return `Animal: ${this.name}`;
  }
}

// Derived class
class Dog extends Animal {
  constructor(name: string, private breed: string) {
    super(name, "Woof"); // Call parent constructor
  }

  fetch(item: string): string {
    return `${this.name} fetches the ${item}!`;
  }

  // Override parent method
  makeSound(): string {
    return `${super.makeSound()} (${this.breed})`;
  }
}

class Cat extends Animal {
  constructor(name: string) {
    super(name, "Meow");
  }

  purr(): string {
    return `${this.name} is purring... 😸`;
  }
}

const dog = new Dog("Buddy", "Golden Retriever");
console.log(dog.makeSound()); // "Buddy says: Woof (Golden Retriever)"
console.log(dog.fetch("ball")); // "Buddy fetches the ball!"
```

## Abstract Classes

Abstract classes cannot be instantiated directly — they serve as blueprints for subclasses.

```typescript
abstract class Shape {
  abstract getArea(): number;      // Must be implemented by subclasses
  abstract getPerimeter(): number; // Must be implemented by subclasses

  // Concrete method — shared by all shapes
  describe(): string {
    return `This shape has area: ${this.getArea().toFixed(2)} and perimeter: ${this.getPerimeter().toFixed(2)}`;
  }
}

class Circle extends Shape {
  constructor(private radius: number) {
    super();
  }

  getArea(): number {
    return Math.PI * this.radius ** 2;
  }

  getPerimeter(): number {
    return 2 * Math.PI * this.radius;
  }
}

class Triangle extends Shape {
  constructor(
    private base: number,
    private height: number,
    private sideA: number,
    private sideB: number
  ) {
    super();
  }

  getArea(): number {
    return 0.5 * this.base * this.height;
  }

  getPerimeter(): number {
    return this.base + this.sideA + this.sideB;
  }
}

// const shape = new Shape(); // ❌ Error: Cannot instantiate abstract class

const circle = new Circle(5);
console.log(circle.describe()); // "This shape has area: 78.54 and perimeter: 31.42"
```

### Abstract Class vs Interface

| Feature | Abstract Class | Interface |
|---|---|---|
| Implementation | Can have concrete methods | No implementation |
| Constructor | Can have constructor | No constructor |
| State | Can have properties | No state |
| Inheritance | Single (extends) | Multiple (implements) |
| Access Modifiers | Yes | No (all public) |

## Interfaces (in OOP context)

```typescript
interface Printable {
  print(): void;
}

interface Serializable {
  serialize(): string;
  deserialize(data: string): void;
}

// A class can implement MULTIPLE interfaces
class Document implements Printable, Serializable {
  constructor(private content: string) {}

  print(): void {
    console.log(this.content);
  }

  serialize(): string {
    return JSON.stringify({ content: this.content });
  }

  deserialize(data: string): void {
    const parsed = JSON.parse(data);
    this.content = parsed.content;
  }
}
```

## Polymorphism

Polymorphism allows objects of different types to be treated as objects of a common type.

```typescript
abstract class Payment {
  abstract process(amount: number): string;
}

class CreditCard extends Payment {
  process(amount: number): string {
    return `Paid ₹${amount} via Credit Card 💳`;
  }
}

class UPI extends Payment {
  process(amount: number): string {
    return `Paid ₹${amount} via UPI 📱`;
  }
}

class NetBanking extends Payment {
  process(amount: number): string {
    return `Paid ₹${amount} via Net Banking 🏦`;
  }
}

// Polymorphic usage
function processPayment(method: Payment, amount: number): void {
  console.log(method.process(amount)); // Different behavior, same interface
}

processPayment(new CreditCard(), 5000);  // Paid ₹5000 via Credit Card 💳
processPayment(new UPI(), 1000);         // Paid ₹1000 via UPI 📱
processPayment(new NetBanking(), 25000); // Paid ₹25000 via Net Banking 🏦
```

---

## 📝 Exercises — Section 6

1. Create a `Vehicle` base class and `Car`, `Motorcycle`, `Truck` subclasses with overridden `fuelEfficiency()` method.
2. Design an abstract `Employee` class with `calculateSalary()` method, implemented by `FullTime` and `Contractor` classes.
3. Implement a simple `Stack<T>` class with push, pop, peek, and isEmpty methods.

---

# 7. Advanced TypeScript

## Generics

Generics let you write reusable code that works with multiple types while keeping type safety.

```typescript
// Generic function
function identity<T>(value: T): T {
  return value;
}

identity<string>("Hello");   // type: string
identity<number>(42);        // type: number
identity(true);              // type inferred: boolean

// Generic with constraints
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const user = { name: "Rohit", age: 25, email: "rohit@dev.com" };
getProperty(user, "name");   // ✅ "Rohit" — type: string
// getProperty(user, "phone"); // ❌ Error: "phone" doesn't exist on type

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

  isEmpty(): boolean {
    return this.items.length === 0;
  }
}

const numStack = new Stack<number>();
numStack.push(1);
numStack.push(2);
console.log(numStack.pop()); // 2

// Generic interface
interface Repository<T> {
  findById(id: number): T | undefined;
  findAll(): T[];
  save(item: T): void;
  delete(id: number): void;
}
```

## Utility Types

TypeScript has built-in utility types that transform existing types.

```typescript
interface User {
  id: number;
  name: string;
  email: string;
  password: string;
  createdAt: Date;
}

// Partial<T> — makes all properties optional
type UserUpdate = Partial<User>;
const update: UserUpdate = { name: "New Name" }; // Only updating name

// Required<T> — makes all properties required
type StrictUser = Required<User>;

// Readonly<T> — makes all properties readonly
type ImmutableUser = Readonly<User>;

// Pick<T, K> — select specific properties
type PublicUser = Pick<User, "id" | "name" | "email">;
const publicProfile: PublicUser = { id: 1, name: "Rohit", email: "r@dev.com" };

// Omit<T, K> — exclude specific properties
type SafeUser = Omit<User, "password">;

// Record<K, V> — create object type with specific keys and values
type UserRoles = Record<"admin" | "user" | "moderator", string[]>;
const roles: UserRoles = {
  admin: ["create", "delete", "update"],
  user: ["read"],
  moderator: ["read", "update"],
};

// Exclude<T, U> — remove types from union
type NumberTypes = "int" | "float" | "string" | "boolean";
type NumericOnly = Exclude<NumberTypes, "string" | "boolean">; // "int" | "float"

// Extract<T, U> — keep types that match
type StringOrBool = Extract<string | number | boolean, string | boolean>; // string | boolean

// NonNullable<T> — remove null and undefined
type SafeString = NonNullable<string | null | undefined>; // string

// ReturnType<T> — get return type of a function
function getUser() {
  return { id: 1, name: "Rohit" };
}
type UserResult = ReturnType<typeof getUser>; // { id: number; name: string }

// Parameters<T> — get parameter types of a function
function createOrder(id: number, amount: number, userId: string) {}
type OrderParams = Parameters<typeof createOrder>; // [number, number, string]
```

## keyof

`keyof` creates a union type of all keys in an object type.

```typescript
interface Config {
  theme: string;
  language: string;
  fontSize: number;
  darkMode: boolean;
}

type ConfigKey = keyof Config; // "theme" | "language" | "fontSize" | "darkMode"

function getSetting<T, K extends keyof T>(settings: T, key: K): T[K] {
  return settings[key];
}

const config: Config = {
  theme: "dark",
  language: "en",
  fontSize: 14,
  darkMode: true,
};

const theme = getSetting(config, "theme");       // type: string
const fontSize = getSetting(config, "fontSize"); // type: number
```

## typeof

`typeof` in TypeScript (at the type level) captures the type of a value.

```typescript
const defaultConfig = {
  apiUrl: "https://api.example.com",
  timeout: 5000,
  retries: 3,
};

// Capture the type of the object
type AppConfig = typeof defaultConfig;
// = { apiUrl: string; timeout: number; retries: number; }

// Get keys from a value
type ConfigKeys = keyof typeof defaultConfig; // "apiUrl" | "timeout" | "retries"

// Common pattern with enums
const Direction = {
  UP: "UP",
  DOWN: "DOWN",
  LEFT: "LEFT",
  RIGHT: "RIGHT",
} as const;

type DirectionType = (typeof Direction)[keyof typeof Direction];
// = "UP" | "DOWN" | "LEFT" | "RIGHT"
```

## Mapped Types

Mapped types create new types by transforming each property of an existing type.

```typescript
// Make all properties optional (like Partial)
type MyPartial<T> = {
  [K in keyof T]?: T[K];
};

// Make all properties required (like Required)
type MyRequired<T> = {
  [K in keyof T]-?: T[K]; // -? removes optionality
};

// Make all properties nullable
type Nullable<T> = {
  [K in keyof T]: T[K] | null;
};

// Transform property types
type Stringify<T> = {
  [K in keyof T]: string;
};

interface Point {
  x: number;
  y: number;
}

type StringPoint = Stringify<Point>; // { x: string; y: string }

// Getters mapped type
type Getters<T> = {
  [K in keyof T as `get${Capitalize<string & K>}`]: () => T[K];
};

type PersonGetters = Getters<{ name: string; age: number }>;
// = { getName: () => string; getAge: () => number; }
```

## Conditional Types

```typescript
// Basic conditional type
type IsString<T> = T extends string ? true : false;

type A = IsString<string>;  // true
type B = IsString<number>;  // false

// More practical use
type NonNullable2<T> = T extends null | undefined ? never : T;

// infer keyword — extract type from condition
type ReturnType2<T> = T extends (...args: any[]) => infer R ? R : never;

function greet(): string { return "Hello!"; }
type GreetReturn = ReturnType2<typeof greet>; // string

// Unwrap array type
type UnpackArray<T> = T extends Array<infer Item> ? Item : T;
type ItemType = UnpackArray<string[]>; // string
type NotArray = UnpackArray<number>;   // number
```

## Indexed Access Types

```typescript
interface Order {
  id: number;
  items: {
    productId: string;
    quantity: number;
    price: number;
  }[];
  status: "pending" | "confirmed" | "shipped" | "delivered";
  customer: {
    name: string;
    address: string;
  };
}

// Access a nested type
type OrderItem = Order["items"][number];
// = { productId: string; quantity: number; price: number; }

type OrderStatus = Order["status"];
// = "pending" | "confirmed" | "shipped" | "delivered"

type CustomerInfo = Order["customer"];
// = { name: string; address: string; }
```

## Enums

Enums define named constants.

```typescript
// Numeric enum (default — auto-increments from 0)
enum Direction {
  Up,    // 0
  Down,  // 1
  Left,  // 2
  Right, // 3
}

console.log(Direction.Up);     // 0
console.log(Direction[0]);     // "Up" (reverse mapping)

// String enum (preferred — more readable)
enum Status {
  Active = "ACTIVE",
  Inactive = "INACTIVE",
  Pending = "PENDING",
  Banned = "BANNED",
}

function checkStatus(status: Status): string {
  switch (status) {
    case Status.Active: return "User is active ✅";
    case Status.Banned: return "User is banned 🚫";
    default: return "Other status";
  }
}

// Const enum — inlined at compile time (no JS object generated)
const enum LogLevel {
  Debug = "DEBUG",
  Info = "INFO",
  Warning = "WARNING",
  Error = "ERROR",
}

const level: LogLevel = LogLevel.Error;
```

> 💡 **Tip:** Prefer `const enum` or union literal types over regular enums for better tree-shaking.

---

## 📝 Exercises — Section 7

1. Write a generic `cache<T>` function that stores and retrieves values by key.
2. Use utility types to create a `CreateUserDTO` and `UpdateUserDTO` from a `User` interface.
3. Write a conditional type `IsArray<T>` that returns `true` if T is an array type.

---

# 8. Modules

## Import & Export

```typescript
// ── math.ts ──
export const PI: number = 3.14159;

export function add(a: number, b: number): number {
  return a + b;
}

export interface MathOptions {
  precision?: number;
}

// Default export
export default class Calculator {
  add(a: number, b: number): number { return a + b; }
  subtract(a: number, b: number): number { return a - b; }
}

// ── main.ts ──
import Calculator, { PI, add, MathOptions } from "./math";

const calc = new Calculator();
console.log(calc.add(10, 5));  // 15
console.log(PI);                // 3.14159
console.log(add(3, 4));        // 7

// Rename imports
import { add as addNumbers } from "./math";

// Import everything
import * as MathUtils from "./math";
console.log(MathUtils.PI);
```

## Namespaces

Namespaces group related code to avoid naming conflicts (more useful before ES modules).

```typescript
// validation.ts
namespace Validation {
  export interface StringValidator {
    isValid(s: string): boolean;
  }

  export class EmailValidator implements StringValidator {
    isValid(s: string): boolean {
      return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(s);
    }
  }

  export class PhoneValidator implements StringValidator {
    isValid(s: string): boolean {
      return /^\d{10}$/.test(s);
    }
  }
}

const emailValidator = new Validation.EmailValidator();
console.log(emailValidator.isValid("rohit@example.com")); // true
```

## Module Resolution

```json
// tsconfig.json
{
  "compilerOptions": {
    "moduleResolution": "node",  // or "bundler" for Vite/webpack
    "baseUrl": ".",
    "paths": {
      "@utils/*": ["src/utils/*"],
      "@models/*": ["src/models/*"]
    }
  }
}
```

```typescript
// With path aliases
import { formatDate } from "@utils/date";
import { User } from "@models/user";
```

---

# 9. Async Programming

## Promises

```typescript
// Creating a Promise
function fetchUser(id: number): Promise<{ id: number; name: string }> {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (id > 0) {
        resolve({ id, name: "Rohit" });
      } else {
        reject(new Error("Invalid ID"));
      }
    }, 1000);
  });
}

// Using .then().catch()
fetchUser(1)
  .then((user) => console.log(user))  // { id: 1, name: "Rohit" }
  .catch((err: Error) => console.error(err.message));

// Promise.all — run in parallel
Promise.all([fetchUser(1), fetchUser(2)])
  .then(([user1, user2]) => {
    console.log(user1, user2);
  });

// Promise.allSettled — wait for all, regardless of failure
Promise.allSettled([fetchUser(1), fetchUser(-1)])
  .then((results) => {
    results.forEach((result) => {
      if (result.status === "fulfilled") {
        console.log("Success:", result.value);
      } else {
        console.log("Failed:", result.reason);
      }
    });
  });
```

## Async/Await

```typescript
// Clean async/await syntax
async function loadUserData(userId: number): Promise<void> {
  try {
    const user = await fetchUser(userId);
    console.log(`Loaded user: ${user.name}`);
  } catch (error) {
    if (error instanceof Error) {
      console.error(`Error: ${error.message}`);
    }
  }
}

// Real-world: API call with typed response
interface ApiResponse<T> {
  data: T;
  status: number;
  message: string;
}

interface Post {
  id: number;
  title: string;
  body: string;
}

async function fetchPosts(): Promise<Post[]> {
  const response = await fetch("https://jsonplaceholder.typicode.com/posts");

  if (!response.ok) {
    throw new Error(`HTTP Error: ${response.status}`);
  }

  const result: ApiResponse<Post[]> = await response.json();
  return result.data;
}

// Sequential vs Parallel
async function sequential(): Promise<void> {
  const user1 = await fetchUser(1);  // waits for user1
  const user2 = await fetchUser(2);  // then waits for user2 (~2 seconds total)
}

async function parallel(): Promise<void> {
  const [user1, user2] = await Promise.all([
    fetchUser(1),
    fetchUser(2),
  ]); // Both run simultaneously (~1 second total)
}
```

### Promise vs Async/Await

| Feature | Promise (.then) | Async/Await |
|---|---|---|
| Readability | Chained, moderate | Linear, excellent |
| Error handling | `.catch()` | `try/catch` |
| Debugging | Harder | Easier |
| Multiple async | `.then().then()` | Sequential lines |
| Parallel ops | `Promise.all()` | `await Promise.all()` |

## Error Handling

```typescript
// Custom error types
class ApiError extends Error {
  constructor(
    message: string,
    public statusCode: number,
    public endpoint: string
  ) {
    super(message);
    this.name = "ApiError";
  }
}

class ValidationError extends Error {
  constructor(message: string, public field: string) {
    super(message);
    this.name = "ValidationError";
  }
}

// Type-safe error handling
async function createUser(data: unknown): Promise<void> {
  try {
    // Validate
    if (typeof data !== "object" || data === null) {
      throw new ValidationError("Invalid data format", "body");
    }

    // API call
    const response = await fetch("/api/users", {
      method: "POST",
      body: JSON.stringify(data),
    });

    if (!response.ok) {
      throw new ApiError("Failed to create user", response.status, "/api/users");
    }

    console.log("User created successfully!");
  } catch (error) {
    if (error instanceof ValidationError) {
      console.error(`Validation failed on field '${error.field}': ${error.message}`);
    } else if (error instanceof ApiError) {
      console.error(`API Error ${error.statusCode} at ${error.endpoint}: ${error.message}`);
    } else if (error instanceof Error) {
      console.error(`Unexpected error: ${error.message}`);
    }
  }
}
```

---

# 10. DOM & Browser

## DOM Manipulation

```typescript
// Type-safe DOM selection
const heading = document.querySelector("h1") as HTMLHeadingElement;
const button = document.getElementById("submit-btn") as HTMLButtonElement;
const input = document.getElementById("username") as HTMLInputElement;

// Null-safe pattern
const container = document.querySelector<HTMLDivElement>(".container");
if (container) {
  container.style.backgroundColor = "lightblue";
  container.textContent = "Hello TypeScript! 🎉";
}

// Creating elements
function createCard(title: string, content: string): HTMLDivElement {
  const card = document.createElement("div");
  card.className = "card";

  const h2 = document.createElement("h2");
  h2.textContent = title;

  const p = document.createElement("p");
  p.textContent = content;

  card.appendChild(h2);
  card.appendChild(p);

  return card;
}

document.body.appendChild(createCard("TypeScript", "Great for large apps!"));
```

## Event Handling

```typescript
// Typed event handlers
const submitBtn = document.getElementById("submit") as HTMLButtonElement;

submitBtn.addEventListener("click", (event: MouseEvent) => {
  event.preventDefault();
  console.log(`Clicked at: ${event.clientX}, ${event.clientY}`);
});

// Form events
const form = document.querySelector("form") as HTMLFormElement;
form.addEventListener("submit", (event: SubmitEvent) => {
  event.preventDefault();
  const formData = new FormData(event.target as HTMLFormElement);
  console.log(Object.fromEntries(formData));
});

// Input events
const searchInput = document.querySelector<HTMLInputElement>("#search")!;
searchInput.addEventListener("input", (event: Event) => {
  const target = event.target as HTMLInputElement;
  console.log(`Search query: ${target.value}`);
});

// Keyboard events
document.addEventListener("keydown", (event: KeyboardEvent) => {
  if (event.key === "Escape") {
    console.log("Escape pressed");
  }
  if (event.ctrlKey && event.key === "s") {
    event.preventDefault();
    console.log("Save triggered");
  }
});
```

## Type Casting with DOM

```typescript
// Using 'as' keyword
const canvas = document.getElementById("myCanvas") as HTMLCanvasElement;
const ctx = canvas.getContext("2d") as CanvasRenderingContext2D;

ctx.fillStyle = "#3178C6"; // TypeScript blue!
ctx.fillRect(0, 0, 200, 100);

// Generic querySelector
const inputs = document.querySelectorAll<HTMLInputElement>("input[type='text']");
inputs.forEach((input) => {
  input.style.border = "2px solid blue";
  console.log(input.value);
});

// HTMLElement vs specific elements
function processElement(element: HTMLElement): void {
  // Only available on HTMLElement
  element.style.display = "none";

  // Need type guard for specific properties
  if (element instanceof HTMLInputElement) {
    console.log(element.value); // ✅
  }

  if (element instanceof HTMLImageElement) {
    console.log(element.src); // ✅
  }
}
```

---

# 11. Advanced Concepts

## Decorators

Decorators are special declarations that can be attached to classes, methods, or properties (experimental feature — enable with `experimentalDecorators: true` in tsconfig).

```typescript
// Class decorator
function Logger(prefix: string) {
  return function(target: Function) {
    console.log(`[${prefix}] Class created: ${target.name}`);
  };
}

// Method decorator
function readonly(target: any, key: string, descriptor: PropertyDescriptor) {
  descriptor.writable = false;
  return descriptor;
}

// Property decorator
function validate(target: any, propertyKey: string) {
  let value: string;

  Object.defineProperty(target, propertyKey, {
    get() { return value; },
    set(newValue: string) {
      if (!newValue || newValue.trim().length === 0) {
        throw new Error(`${propertyKey} cannot be empty`);
      }
      value = newValue;
    },
  });
}

@Logger("APP")
class UserService {
  @validate
  name: string = "";

  @readonly
  getVersion(): string {
    return "1.0.0";
  }
}
```

## Declaration Files

Declaration files (`.d.ts`) describe the shape of JavaScript modules for TypeScript.

```typescript
// mylib.d.ts — declaration file for a JS library
declare module "mylib" {
  export interface Options {
    timeout?: number;
    retries?: number;
  }

  export function initialize(options?: Options): void;
  export function fetch(url: string): Promise<Response>;

  export default class MyLib {
    constructor(options?: Options);
    get(path: string): Promise<unknown>;
    post(path: string, body: unknown): Promise<unknown>;
  }
}

// global.d.ts — extend global types
declare global {
  interface Window {
    gtag: (...args: any[]) => void;
    dataLayer: any[];
  }
}
```

## Type Guards

Type guards narrow the type within a conditional block.

```typescript
// typeof guard
function process(value: string | number): string {
  if (typeof value === "string") {
    return value.toUpperCase(); // TS knows it's a string here
  }
  return value.toFixed(2); // TS knows it's a number here
}

// instanceof guard
class Dog { bark() { return "Woof!"; } }
class Cat { meow() { return "Meow!"; } }

function makeSound(animal: Dog | Cat): string {
  if (animal instanceof Dog) {
    return animal.bark();
  }
  return animal.meow();
}

// in operator guard
interface Car { drive(): void; }
interface Boat { sail(): void; }

function move(vehicle: Car | Boat): void {
  if ("drive" in vehicle) {
    vehicle.drive();
  } else {
    vehicle.sail();
  }
}

// Custom type guard (type predicate)
interface Fish { swim(): void; }
interface Bird { fly(): void; }

function isFish(animal: Fish | Bird): animal is Fish {
  return (animal as Fish).swim !== undefined;
}

function move2(animal: Fish | Bird): void {
  if (isFish(animal)) {
    animal.swim(); // TS knows it's Fish
  } else {
    animal.fly();  // TS knows it's Bird
  }
}
```

## Narrowing

Narrowing is the process of refining types to more specific types within conditional branches.

```typescript
// Discriminated union — powerful narrowing pattern
type Shape =
  | { kind: "circle"; radius: number }
  | { kind: "square"; side: number }
  | { kind: "rectangle"; width: number; height: number };

function getArea(shape: Shape): number {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;      // TS knows radius exists
    case "square":
      return shape.side ** 2;                    // TS knows side exists
    case "rectangle":
      return shape.width * shape.height;         // TS knows width, height exist
  }
}

// Exhaustive check with never
function assertNever(x: never): never {
  throw new Error(`Unexpected value: ${JSON.stringify(x)}`);
}

function getArea2(shape: Shape): number {
  switch (shape.kind) {
    case "circle": return Math.PI * shape.radius ** 2;
    case "square": return shape.side ** 2;
    case "rectangle": return shape.width * shape.height;
    default: return assertNever(shape); // TS will error if we miss a case!
  }
}
```

## Optional Chaining

```typescript
interface Company {
  name: string;
  address?: {
    city?: string;
    country?: string;
  };
  ceo?: {
    name: string;
    email?: string;
  };
}

const company: Company = { name: "TechCorp" };

// Without optional chaining — verbose
const city1 = company.address ? company.address.city : undefined;

// With optional chaining — clean!
const city2 = company?.address?.city;          // undefined
const ceoEmail = company?.ceo?.email;          // undefined
const ceoName = company?.ceo?.name ?? "Unknown"; // "Unknown"

// With method calls
const upperCity = company?.address?.city?.toUpperCase(); // undefined

// With arrays
const users = [{ name: "Rohit", scores: [95, 87] }];
const firstScore = users[0]?.scores?.[0]; // 95
```

## Nullish Coalescing

```typescript
// ?? returns right side only if left side is null or undefined
// (unlike || which also triggers for 0, "", false)

const username: string | null = null;
const display = username ?? "Anonymous"; // "Anonymous"

const count: number | undefined = 0;
const total1 = count ?? 10;  // 0  ← 0 is not null/undefined!
const total2 = count || 10;  // 10 ← 0 is falsy, so falls back

// Nullish assignment operator (??=)
let config: { theme?: string } = {};
config.theme ??= "dark"; // Sets only if theme is null/undefined
console.log(config.theme); // "dark"

// Practical: API response handling
function displayUserName(user: { name?: string | null }): string {
  return user.name?.trim() ?? "Guest";
}
```

---

# 12. TypeScript with Frameworks

## TypeScript with React

```bash
# Create React app with TypeScript
npx create-react-app my-app --template typescript
# or with Vite (recommended)
npm create vite@latest my-app -- --template react-ts
```

```typescript
// ── types.ts ──
export interface User {
  id: number;
  name: string;
  email: string;
  avatar?: string;
}

// ── UserCard.tsx ──
import React, { useState, useEffect } from "react";
import { User } from "./types";

// Props interface
interface UserCardProps {
  user: User;
  onSelect?: (user: User) => void;
  isHighlighted?: boolean;
}

// Functional component with typed props
const UserCard: React.FC<UserCardProps> = ({
  user,
  onSelect,
  isHighlighted = false,
}) => {
  const [isHovered, setIsHovered] = useState<boolean>(false);

  const handleClick = (): void => {
    onSelect?.(user);
  };

  return (
    <div
      className={`card ${isHighlighted ? "highlighted" : ""}`}
      onClick={handleClick}
      onMouseEnter={() => setIsHovered(true)}
      onMouseLeave={() => setIsHovered(false)}
    >
      <h2>{user.name}</h2>
      <p>{user.email}</p>
    </div>
  );
};

// ── Custom Hook ──
function useUsers(): {
  users: User[];
  loading: boolean;
  error: string | null;
} {
  const [users, setUsers] = useState<User[]>([]);
  const [loading, setLoading] = useState<boolean>(true);
  const [error, setError] = useState<string | null>(null);

  useEffect(() => {
    fetch("/api/users")
      .then((r) => r.json())
      .then((data: User[]) => setUsers(data))
      .catch((e: Error) => setError(e.message))
      .finally(() => setLoading(false));
  }, []);

  return { users, loading, error };
}

export default UserCard;
```

## TypeScript with Node.js

```bash
# Setup Node.js + TypeScript project
mkdir node-ts-app && cd node-ts-app
npm init -y
npm install --save-dev typescript @types/node ts-node nodemon
npx tsc --init
```

```typescript
// ── src/index.ts ──
import * as fs from "fs";
import * as path from "path";
import * as http from "http";

// Reading files with types
function readJsonFile<T>(filePath: string): T {
  const absolutePath = path.resolve(filePath);
  const content = fs.readFileSync(absolutePath, "utf-8");
  return JSON.parse(content) as T;
}

interface AppConfig {
  port: number;
  host: string;
  debug: boolean;
}

const config = readJsonFile<AppConfig>("./config.json");

// Simple HTTP server
const server = http.createServer((req, res) => {
  res.writeHead(200, { "Content-Type": "application/json" });
  res.end(JSON.stringify({ message: "Hello from TypeScript Node.js!" }));
});

server.listen(config.port, config.host, () => {
  console.log(`Server running at http://${config.host}:${config.port}`);
});
```

## TypeScript with Express.js

```bash
npm install express
npm install --save-dev @types/express
```

```typescript
// ── src/app.ts ──
import express, { Request, Response, NextFunction, Application } from "express";

const app: Application = express();
app.use(express.json());

// Typed request body
interface CreateUserBody {
  name: string;
  email: string;
  password: string;
}

interface UserParams {
  id: string;
}

// Route with typed request/response
app.post(
  "/users",
  async (req: Request<{}, {}, CreateUserBody>, res: Response) => {
    const { name, email, password } = req.body;

    // Validation
    if (!name || !email || !password) {
      return res.status(400).json({ error: "All fields are required" });
    }

    // Create user logic...
    const user = { id: Date.now(), name, email };
    return res.status(201).json(user);
  }
);

app.get(
  "/users/:id",
  async (req: Request<UserParams>, res: Response) => {
    const userId = parseInt(req.params.id);
    // Fetch user...
    res.json({ id: userId, name: "Rohit" });
  }
);

// Global error handler middleware
app.use((err: Error, req: Request, res: Response, next: NextFunction) => {
  console.error(err.stack);
  res.status(500).json({ error: err.message });
});

app.listen(3000, () => console.log("Express + TypeScript running on port 3000"));
```

---

# 13. Best Practices

## Folder Structure

```
my-typescript-app/
├── src/
│   ├── types/           # Type definitions & interfaces
│   │   ├── index.ts
│   │   ├── user.types.ts
│   │   └── api.types.ts
│   ├── models/          # Data models/classes
│   ├── services/        # Business logic
│   ├── controllers/     # Request handlers
│   ├── utils/           # Helper functions
│   ├── constants/       # App constants & enums
│   ├── config/          # Configuration
│   └── index.ts         # Entry point
├── tests/               # Test files
├── dist/                # Compiled output (gitignore)
├── tsconfig.json
└── package.json
```

## Naming Conventions

```typescript
// Interfaces — PascalCase, optionally prefix with 'I' (avoid in modern TS)
interface UserProfile { }         // ✅ Preferred
interface IUserProfile { }        // ⚠️ Old style, avoid

// Types — PascalCase
type ApiResponse<T> = { data: T };

// Enums — PascalCase, values PascalCase or UPPER_CASE
enum UserRole { Admin, User, Moderator }
enum HttpStatus { OK = 200, NotFound = 404 }

// Classes — PascalCase
class UserService { }
class DatabaseConnection { }

// Functions & variables — camelCase
function getUserById(id: number) { }
const maxRetries = 3;

// Constants — UPPER_SNAKE_CASE
const MAX_CONNECTIONS: number = 10;
const API_BASE_URL: string = "https://api.example.com";

// Generic type parameters — single uppercase letter or descriptive PascalCase
function map<T, U>(array: T[], fn: (item: T) => U): U[] { return array.map(fn); }
interface Repository<TEntity, TId> { }
```

## Clean Code

```typescript
// ✅ DO: Explicit return types on functions
function calculateTax(amount: number, rate: number): number {
  return amount * (rate / 100);
}

// ✅ DO: Use const for values that don't change
const TAX_RATE: number = 18;

// ✅ DO: Prefer union types over enum for simple cases
type Theme = "light" | "dark" | "system";

// ✅ DO: Use optional chaining and nullish coalescing
const name = user?.profile?.displayName ?? "Anonymous";

// ✅ DO: Avoid any — use unknown and narrow it
function parseData(raw: unknown): string {
  if (typeof raw === "string") return raw;
  return String(raw);
}

// ❌ AVOID: implicit any
// function process(data) { } // data is implicitly any

// ❌ AVOID: non-null assertions without reason
// const el = document.getElementById("app")!;

// ✅ DO: Handle null explicitly
const el = document.getElementById("app");
if (!el) throw new Error("App element not found");
```

## Performance Tips

```typescript
// ✅ Use const enum for compile-time inlining
const enum Direction { North, South, East, West }

// ✅ Use type-only imports (tree-shaking)
import type { User } from "./types";

// ✅ Lazy load with dynamic imports
async function loadHeavyModule() {
  const { HeavyComponent } = await import("./HeavyComponent");
  return HeavyComponent;
}

// ✅ Use interface over type for object shapes (slightly faster in some cases)
interface Config { host: string; port: number; }

// ✅ Enable strict null checks — catches bugs early
// In tsconfig: "strictNullChecks": true

// ✅ Use ReadonlyArray for immutable arrays
function processItems(items: ReadonlyArray<string>): void {
  items.forEach(item => console.log(item));
  // items.push("new"); // ❌ Error — can't mutate
}
```

---

# 14. Exercises & Challenges

## 🟢 Beginner Challenges

1. **Type a Todo App** — Create interfaces for `Todo`, `TodoList`. Write functions to add, remove, and toggle todos.

2. **Calculator** — Build a typed calculator with `add`, `subtract`, `multiply`, `divide` functions that handle edge cases.

3. **Student Grade System** — Create a `Student` class with grades, a method to calculate GPA, and letter grade classification.

## 🟡 Intermediate Challenges

4. **Generic API Client** — Build a generic `ApiClient<T>` class with typed `get`, `post`, `put`, `delete` methods.

5. **Event Emitter** — Implement a type-safe `EventEmitter<Events>` where `Events` is a record of event names to callback signatures.

6. **Form Validator** — Create a validation library using types that validates objects against a schema.

## 🔴 Advanced Challenges

7. **Type-safe ORM** — Build a simple query builder with fluent API: `db.from("users").where("age", ">", 18).select("name", "email")`.

8. **Dependency Injection** — Implement a simple DI container using decorators and reflect-metadata.

9. **Utility Type Library** — Implement your own versions of `DeepPartial<T>`, `DeepReadonly<T>`, `FlattenType<T>`.

```typescript
// Starter for Challenge 9
type DeepPartial<T> = {
  [K in keyof T]?: T[K] extends object ? DeepPartial<T[K]> : T[K];
};

// Test it
interface Config {
  database: {
    host: string;
    port: number;
    credentials: { username: string; password: string };
  };
  server: { port: number };
}

const partialConfig: DeepPartial<Config> = {
  database: { host: "localhost" }, // ✅ No error — deeply partial
};
```

---

# 15. Conclusion & Resources

## 🎯 TypeScript Roadmap

```
Beginner Level
├── Setup & Configuration
├── Basic Types & Annotations
├── Interfaces & Type Aliases
├── Functions (typed)
└── Basic OOP (Classes, Inheritance)

Intermediate Level
├── Generics
├── Utility Types
├── Advanced OOP (Abstract, Decorators)
├── Async/Await
└── Modules & Namespaces

Advanced Level
├── Conditional Types
├── Mapped Types
├── Template Literal Types
├── Declaration Files
└── TypeScript Compiler API

Expert Level
├── Type System Internals
├── Custom Transformers
├── Language Server Extensions
└── Contributing to DefinitelyTyped
```

## 📚 Recommended Resources

### Official Documentation
- 🌐 [TypeScript Official Docs](https://www.typescriptlang.org/docs/)
- 🎮 [TypeScript Playground](https://www.typescriptlang.org/play)
- 📖 [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)

### GitHub Repositories
- ⭐ [microsoft/TypeScript](https://github.com/microsoft/TypeScript) — Official TS repo
- 📦 [DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped) — Community type definitions
- 🧩 [type-challenges](https://github.com/type-level-ts/type-challenges) — Practice type system
- 📚 [awesome-typescript](https://github.com/dzharii/awesome-typescript) — Curated resources

### Learning Platforms
- 🎓 [TypeScript Course — freeCodeCamp](https://www.youtube.com/c/freecodecamp)
- 🎓 [Total TypeScript](https://www.totaltypescript.com/) — Advanced patterns
- 🎓 [Execute Program — TypeScript](https://www.executeprogram.com/courses/typescript)

## 🛠️ Useful VS Code Extensions

| Extension | Purpose |
|---|---|
| **TypeScript Hero** | Auto-imports & sorting |
| **Error Lens** | Inline error highlighting |
| **Prettier** | Code formatting |
| **ESLint** | Code linting |
| **TypeScript Importer** | Auto-import suggestions |
| **Path Intellisense** | File path autocompletion |
| **Thunder Client** | API testing in VS Code |

## 🎉 Conclusion

You've just covered TypeScript from **zero to hero**! Here's a quick recap of your journey:

- ✅ **Basics** — Types, interfaces, functions, and OOP
- ✅ **Intermediate** — Generics, utility types, async programming
- ✅ **Advanced** — Conditional types, decorators, type guards
- ✅ **Real-world** — React, Node.js, Express integration

### Key Takeaways

1. **Always enable `strict` mode** — it makes TypeScript work for you, not against you.
2. **Prefer `unknown` over `any`** — safety first.
3. **Use interfaces for object shapes**, type aliases for unions and complex compositions.
4. **Generics are your best friend** for reusable, type-safe code.
5. **TypeScript is an investment** — the initial learning curve pays off massively in large projects.

---

> 💙 *"Strong types lead to fewer bugs, better documentation, and happier developers."*

**Happy Coding! Keep Building! 🚀**

---

*Made with ❤️ | TypeScript 5.x | Last updated: 2024*
