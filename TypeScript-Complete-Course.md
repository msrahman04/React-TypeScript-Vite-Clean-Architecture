# TypeScript Complete Course: From Beginner to Expert

## Table of Contents

1. [Introduction to TypeScript](#1-introduction-to-typescript)
2. [Setting Up Your Development Environment](#2-setting-up-your-development-environment)
3. [Basic Types and Variables](#3-basic-types-and-variables)
4. [Functions in TypeScript](#4-functions-in-typescript)
5. [Interfaces and Type Aliases](#5-interfaces-and-type-aliases)
6. [Classes and Object-Oriented Programming](#6-classes-and-object-oriented-programming)
7. [Advanced Types](#7-advanced-types)
8. [Modules and Namespaces](#8-modules-and-namespaces)
9. [Generics](#9-generics)
10. [Decorators](#10-decorators)
11. [Configuration and Compiler Options](#11-configuration-and-compiler-options)
12. [Working with External Libraries](#12-working-with-external-libraries)
13. [TypeScript with Popular Frameworks](#13-typescript-with-popular-frameworks)
14. [Testing TypeScript Applications](#14-testing-typescript-applications)
15. [Best Practices and Patterns](#15-best-practices-and-patterns)
16. [Real-World Projects](#16-real-world-projects)

---

## 1. Introduction to TypeScript

### What is TypeScript?

TypeScript is a **statically typed superset** of JavaScript that compiles to plain JavaScript. It was developed by Microsoft and adds optional static type definitions to JavaScript.

#### Key Benefits:

1. **Type Safety**: Catch errors at compile time, not runtime
2. **Better IDE Support**: Enhanced autocomplete, refactoring, and navigation
3. **Self-Documenting Code**: Types serve as inline documentation
4. **Easier Refactoring**: Safe code changes across large codebases
5. **JavaScript Compatibility**: All JavaScript is valid TypeScript

### TypeScript vs JavaScript

```typescript
// JavaScript - Runtime error
function greet(name) {
    return "Hello, " + name.toUppercase(); // TypeError at runtime!
}

greet(42); // No error until execution

// TypeScript - Compile-time error
function greet(name: string): string {
    return "Hello, " + name.toUppercase(); // TS error: Property 'toUppercase' does not exist
}

greet(42); // TS error: Argument of type 'number' is not assignable to parameter of type 'string'
```

### How TypeScript Works

```
TypeScript Code (.ts) → TypeScript Compiler (tsc) → JavaScript Code (.js) → Runtime
```

1. **Development**: Write TypeScript with types
2. **Compilation**: TypeScript compiler checks types and emits JavaScript
3. **Runtime**: JavaScript executes normally (types are erased)

### Why Learn TypeScript?

- **Industry Adoption**: Used by Microsoft, Google, Facebook, and many others
- **Career Growth**: High demand for TypeScript developers
- **Code Quality**: Significantly reduces bugs and improves maintainability
- **Team Collaboration**: Types make code more readable and self-documenting
- **Future-Proof**: TypeScript often gets JavaScript features early

---

## 2. Setting Up Your Development Environment

### Prerequisites

- Basic JavaScript knowledge
- Node.js installed on your system
- A code editor (VS Code recommended)

### Installing TypeScript

#### Global Installation:
```bash
# Install TypeScript globally
npm install -g typescript

# Check version
tsc --version

# Create a TypeScript file
echo 'console.log("Hello, TypeScript!");' > hello.ts

# Compile and run
tsc hello.ts
node hello.js
```

#### Local Project Installation:
```bash
# Create a new project
mkdir my-typescript-project
cd my-typescript-project

# Initialize npm project
npm init -y

# Install TypeScript as dev dependency
npm install -D typescript
npm install -D @types/node  # Node.js type definitions

# Install ts-node for direct execution
npm install -D ts-node

# Create TypeScript config
npx tsc --init
```

### VS Code Setup

#### Essential Extensions:
1. **TypeScript Importer** - Auto import suggestions
2. **Prettier** - Code formatting
3. **ESLint** - Code linting
4. **Error Lens** - Inline error display

#### VS Code Settings for TypeScript:
```json
// .vscode/settings.json
{
  "typescript.preferences.quoteStyle": "single",
  "typescript.updateImportsOnFileMove.enabled": "always",
  "typescript.suggest.autoImports": true,
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.organizeImports": true
  }
}
```

### Project Structure

```
my-typescript-project/
├── src/
│   ├── index.ts
│   ├── types/
│   │   └── index.ts
│   ├── utils/
│   │   └── helpers.ts
│   └── models/
│       └── User.ts
├── dist/          # Compiled JavaScript
├── tests/
├── package.json
├── tsconfig.json
└── .gitignore
```

### Basic tsconfig.json

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
```

### Package.json Scripts

```json
{
  "scripts": {
    "build": "tsc",
    "start": "node dist/index.js",
    "dev": "ts-node src/index.ts",
    "watch": "tsc --watch",
    "clean": "rm -rf dist"
  }
}
```

---

## 3. Basic Types and Variables

### Primitive Types

#### String
```typescript
let firstName: string = "John";
let lastName: string = 'Doe';
let fullName: string = `${firstName} ${lastName}`;

// Template literals
let greeting: string = `Hello, ${fullName}!`;
```

#### Number
```typescript
let age: number = 30;
let price: number = 99.99;
let binary: number = 0b1010;    // Binary
let octal: number = 0o744;      // Octal
let hex: number = 0xf00d;       // Hexadecimal
```

#### Boolean
```typescript
let isActive: boolean = true;
let isCompleted: boolean = false;
let hasPermission: boolean = age >= 18;
```

#### Arrays
```typescript
// Array of numbers
let numbers: number[] = [1, 2, 3, 4, 5];
let scores: Array<number> = [85, 92, 78, 96];

// Array of strings
let fruits: string[] = ["apple", "banana", "orange"];
let colors: Array<string> = ["red", "green", "blue"];

// Mixed array (avoid when possible)
let mixed: (string | number)[] = ["hello", 42, "world"];
```

#### Tuples
```typescript
// Fixed-length array with specific types
let person: [string, number] = ["Alice", 30];
let coordinates: [number, number] = [10.5, 20.3];

// Named tuples (TypeScript 4.0+)
let employee: [name: string, age: number, isManager: boolean] = 
  ["John", 35, true];

// Accessing tuple elements
console.log(person[0]); // "Alice"
console.log(person[1]); // 30
```

#### Enums
```typescript
// Numeric enum
enum Color {
  Red,    // 0
  Green,  // 1
  Blue    // 2
}

let favoriteColor: Color = Color.Blue;
console.log(favoriteColor); // 2

// String enum
enum Direction {
  Up = "UP",
  Down = "DOWN",
  Left = "LEFT",
  Right = "RIGHT"
}

let move: Direction = Direction.Up;
console.log(move); // "UP"

// Mixed enum
enum Status {
  Pending = 1,
  Success = "SUCCESS",
  Error = "ERROR"
}
```

### Special Types

#### Any
```typescript
// Avoid using 'any' when possible
let dynamic: any = 42;
dynamic = "Hello";
dynamic = true;
dynamic = { name: "John" };

// Use any for migrating JavaScript code
let legacyData: any = JSON.parse('{"name": "John", "age": 30}');
```

#### Unknown
```typescript
// Safer alternative to 'any'
let userInput: unknown;
userInput = 5;
userInput = "hello";

// Type checking required before use
if (typeof userInput === "string") {
  console.log(userInput.toUpperCase()); // Safe
}

// Type assertion (use with caution)
let strLength: number = (userInput as string).length;
```

#### Void
```typescript
// Function that doesn't return anything
function logMessage(message: string): void {
  console.log(message);
}

// Variable of type void (rarely used)
let unusable: void = undefined;
```

#### Never
```typescript
// Function that never returns
function throwError(message: string): never {
  throw new Error(message);
}

// Function with infinite loop
function infiniteLoop(): never {
  while (true) {
    // Never ends
  }
}

// Exhaustive type checking
function processValue(value: string | number): string {
  if (typeof value === "string") {
    return value.toUpperCase();
  }
  if (typeof value === "number") {
    return value.toString();
  }
  
  // This should never be reached
  const exhaustive: never = value;
  return exhaustive;
}
```

#### Null and Undefined
```typescript
// With strict null checks enabled
let nullable: string | null = null;
let optional: string | undefined = undefined;

// Optional chaining and nullish coalescing
interface User {
  name: string;
  email?: string;
}

function greetUser(user: User | null) {
  // Optional chaining
  console.log(user?.email?.toLowerCase());
  
  // Nullish coalescing
  const email = user?.email ?? "No email provided";
}
```

### Type Assertions

```typescript
// Angle bracket syntax (not recommended in JSX)
let someValue: unknown = "Hello, TypeScript!";
let strLength: number = (<string>someValue).length;

// As syntax (preferred)
let strLength2: number = (someValue as string).length;

// Non-null assertion operator
let element = document.getElementById("myButton")!; // Tells TS it's not null
```

### Type Inference

```typescript
// TypeScript infers types automatically
let message = "Hello"; // Inferred as string
let count = 42;        // Inferred as number
let isReady = true;    // Inferred as boolean

// Inference with arrays
let numbers = [1, 2, 3]; // Inferred as number[]
let mixed = [1, "hello"]; // Inferred as (string | number)[]

// Inference with objects
let user = {
  name: "John",
  age: 30
}; // Inferred as { name: string; age: number; }

// Function return type inference
function add(a: number, b: number) {
  return a + b; // Return type inferred as number
}
```

### Practice Exercises

```typescript
// Exercise 1: Basic Types
let studentName: string = "Alice Johnson";
let studentAge: number = 20;
let isEnrolled: boolean = true;
let grades: number[] = [85, 92, 78, 96, 89];

// Calculate average grade
function calculateAverage(scores: number[]): number {
  const sum = scores.reduce((total, score) => total + score, 0);
  return sum / scores.length;
}

console.log(`${studentName} (${studentAge}) average: ${calculateAverage(grades)}`);

// Exercise 2: Enums and Tuples
enum CourseStatus {
  NotStarted = "NOT_STARTED",
  InProgress = "IN_PROGRESS",
  Completed = "COMPLETED",
  Dropped = "DROPPED"
}

type Course = [string, number, CourseStatus]; // [name, credits, status]

let courses: Course[] = [
  ["Mathematics", 3, CourseStatus.Completed],
  ["Physics", 4, CourseStatus.InProgress],
  ["Chemistry", 3, CourseStatus.NotStarted]
];

function getCourseInfo(course: Course): string {
  const [name, credits, status] = course;
  return `${name} (${credits} credits): ${status}`;
}

courses.forEach(course => console.log(getCourseInfo(course)));

// Exercise 3: Type Guards
function processInput(input: string | number | boolean): string {
  if (typeof input === "string") {
    return `String: ${input.toUpperCase()}`;
  } else if (typeof input === "number") {
    return `Number: ${input.toFixed(2)}`;
  } else {
    return `Boolean: ${input ? "Yes" : "No"}`;
  }
}

console.log(processInput("hello"));
console.log(processInput(42.567));
console.log(processInput(true));
```

---

## 4. Functions in TypeScript

### Function Declarations

```typescript
// Basic function with types
function add(a: number, b: number): number {
  return a + b;
}

// Function with optional parameters
function greet(name: string, title?: string): string {
  if (title) {
    return `Hello, ${title} ${name}!`;
  }
  return `Hello, ${name}!`;
}

// Function with default parameters
function createUser(name: string, age: number = 18, isActive: boolean = true): object {
  return { name, age, isActive };
}

// Rest parameters
function sum(...numbers: number[]): number {
  return numbers.reduce((total, num) => total + num, 0);
}

console.log(sum(1, 2, 3, 4, 5)); // 15
```

### Function Expressions

```typescript
// Function expression with explicit types
const multiply = function(a: number, b: number): number {
  return a * b;
};

// Arrow function
const divide = (a: number, b: number): number => {
  if (b === 0) {
    throw new Error("Cannot divide by zero");
  }
  return a / b;
};

// Arrow function with implicit return
const square = (n: number): number => n * n;

// Function with no parameters
const getCurrentTime = (): string => new Date().toISOString();
```

### Function Types

```typescript
// Defining function types
type MathOperation = (a: number, b: number) => number;
type StringProcessor = (input: string) => string;

// Using function types
const operations: MathOperation[] = [
  (a, b) => a + b,  // add
  (a, b) => a - b,  // subtract
  (a, b) => a * b,  // multiply
  (a, b) => a / b   // divide
];

const processors: StringProcessor[] = [
  (str) => str.toUpperCase(),
  (str) => str.toLowerCase(),
  (str) => str.trim(),
  (str) => str.split('').reverse().join('')
];

// Function that takes another function as parameter
function calculate(a: number, b: number, operation: MathOperation): number {
  return operation(a, b);
}

console.log(calculate(10, 5, (x, y) => x + y)); // 15
```

### Function Overloads

```typescript
// Function overload signatures
function format(value: string): string;
function format(value: number): string;
function format(value: boolean): string;
function format(value: Date): string;

// Implementation signature
function format(value: string | number | boolean | Date): string {
  if (typeof value === "string") {
    return `"${value}"`;
  } else if (typeof value === "number") {
    return value.toFixed(2);
  } else if (typeof value === "boolean") {
    return value ? "Yes" : "No";
  } else if (value instanceof Date) {
    return value.toLocaleDateString();
  }
  return String(value);
}

// Usage
console.log(format("Hello"));        // "Hello"
console.log(format(42.567));         // 42.57
console.log(format(true));           // Yes
console.log(format(new Date()));     // 12/25/2023
```

### Advanced Function Patterns

#### Higher-Order Functions
```typescript
// Function that returns a function
function createMultiplier(factor: number): (num: number) => number {
  return (num: number) => num * factor;
}

const double = createMultiplier(2);
const triple = createMultiplier(3);

console.log(double(5)); // 10
console.log(triple(4)); // 12

// Function composition
function compose<T, U, V>(
  f: (x: U) => V,
  g: (x: T) => U
): (x: T) => V {
  return (x: T) => f(g(x));
}

const addOne = (n: number) => n + 1;
const toString = (n: number) => n.toString();
const addOneAndStringify = compose(toString, addOne);

console.log(addOneAndStringify(5)); // "6"
```

#### Callback Functions
```typescript
// Callback with error handling
type Callback<T> = (error: Error | null, result?: T) => void;

function fetchData(url: string, callback: Callback<string>): void {
  // Simulate async operation
  setTimeout(() => {
    if (url.includes("error")) {
      callback(new Error("Failed to fetch data"));
    } else {
      callback(null, `Data from ${url}`);
    }
  }, 1000);
}

// Usage
fetchData("https://api.example.com/users", (error, data) => {
  if (error) {
    console.error("Error:", error.message);
  } else {
    console.log("Success:", data);
  }
});
```

#### Async Functions
```typescript
// Async function returning Promise
async function fetchUser(id: number): Promise<{id: number, name: string}> {
  // Simulate API call
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve({ id, name: `User ${id}` });
    }, 1000);
  });
}

// Using async/await
async function getUsers(): Promise<void> {
  try {
    const user1 = await fetchUser(1);
    const user2 = await fetchUser(2);
    
    console.log("Users:", [user1, user2]);
  } catch (error) {
    console.error("Error fetching users:", error);
  }
}

// Promise-based function
function processData(data: string[]): Promise<string[]> {
  return Promise.resolve(data.map(item => item.toUpperCase()));
}
```

### Method Signatures

```typescript
interface Calculator {
  // Method signatures
  add(a: number, b: number): number;
  subtract(a: number, b: number): number;
  multiply(a: number, b: number): number;
  divide(a: number, b: number): number;
  
  // Method with optional parameter
  power(base: number, exponent?: number): number;
  
  // Method with rest parameters
  sum(...numbers: number[]): number;
}

class BasicCalculator implements Calculator {
  add(a: number, b: number): number {
    return a + b;
  }
  
  subtract(a: number, b: number): number {
    return a - b;
  }
  
  multiply(a: number, b: number): number {
    return a * b;
  }
  
  divide(a: number, b: number): number {
    if (b === 0) throw new Error("Division by zero");
    return a / b;
  }
  
  power(base: number, exponent: number = 2): number {
    return Math.pow(base, exponent);
  }
  
  sum(...numbers: number[]): number {
    return numbers.reduce((total, num) => total + num, 0);
  }
}
```

### Practice Exercises

```typescript
// Exercise 1: Function Factory
function createValidator<T>(
  validate: (value: T) => boolean,
  errorMessage: string
): (value: T) => T {
  return (value: T): T => {
    if (!validate(value)) {
      throw new Error(errorMessage);
    }
    return value;
  };
}

const validateEmail = createValidator(
  (email: string) => email.includes("@"),
  "Invalid email format"
);

const validateAge = createValidator(
  (age: number) => age >= 0 && age <= 120,
  "Age must be between 0 and 120"
);

// Usage
try {
  console.log(validateEmail("john@example.com")); // ✓
  console.log(validateAge(25)); // ✓
  validateEmail("invalid-email"); // ✗ Throws error
} catch (error) {
  console.error(error.message);
}

// Exercise 2: Functional Programming Utilities
function map<T, U>(array: T[], transform: (item: T) => U): U[] {
  const result: U[] = [];
  for (const item of array) {
    result.push(transform(item));
  }
  return result;
}

function filter<T>(array: T[], predicate: (item: T) => boolean): T[] {
  const result: T[] = [];
  for (const item of array) {
    if (predicate(item)) {
      result.push(item);
    }
  }
  return result;
}

function reduce<T, U>(
  array: T[],
  reducer: (accumulator: U, current: T) => U,
  initialValue: U
): U {
  let accumulator = initialValue;
  for (const item of array) {
    accumulator = reducer(accumulator, item);
  }
  return accumulator;
}

// Usage
const numbers = [1, 2, 3, 4, 5];

const doubled = map(numbers, x => x * 2);
const evens = filter(numbers, x => x % 2 === 0);
const sum = reduce(numbers, (acc, curr) => acc + curr, 0);

console.log("Doubled:", doubled); // [2, 4, 6, 8, 10]
console.log("Evens:", evens);     // [2, 4]
console.log("Sum:", sum);         // 15

// Exercise 3: Currying
function curry<T, U, V>(fn: (a: T, b: U) => V): (a: T) => (b: U) => V {
  return (a: T) => (b: U) => fn(a, b);
}

const add = (a: number, b: number) => a + b;
const curriedAdd = curry(add);

const addFive = curriedAdd(5);
console.log(addFive(3)); // 8
console.log(addFive(7)); // 12
```

---

## 5. Interfaces and Type Aliases

### Interface Basics

```typescript
// Basic interface definition
interface User {
  id: number;
  name: string;
  email: string;
  isActive: boolean;
}

// Using the interface
const user: User = {
  id: 1,
  name: "John Doe",
  email: "john@example.com",
  isActive: true
};

// Function parameter with interface
function displayUser(user: User): void {
  console.log(`${user.name} (${user.email}) - ${user.isActive ? 'Active' : 'Inactive'}`);
}
```

### Optional and Readonly Properties

```typescript
interface Product {
  readonly id: number;        // Cannot be changed after creation
  name: string;
  price: number;
  description?: string;       // Optional property
  category?: string;          // Optional property
  readonly createdAt: Date;   // Cannot be changed
}

const product: Product = {
  id: 1,
  name: "Laptop",
  price: 999.99,
  createdAt: new Date()
};

// product.id = 2;           // Error: Cannot assign to 'id' because it is read-only
product.name = "Gaming Laptop"; // OK
product.description = "High-performance gaming laptop"; // OK
```

### Index Signatures

```typescript
// String index signature
interface StringDictionary {
  [key: string]: string;
}

const countries: StringDictionary = {
  "US": "United States",
  "UK": "United Kingdom",
  "CA": "Canada"
};

// Number index signature
interface NumberArray {
  [index: number]: string;
}

const fruits: NumberArray = ["apple", "banana", "orange"];

// Mixed index signatures
interface MixedDictionary {
  [key: string]: string | number;
  length: number; // Specific property must be compatible with index signature
}

const data: MixedDictionary = {
  length: 3,
  "item1": "hello",
  "item2": 42,
  "item3": "world"
};
```

### Function Types in Interfaces

```typescript
interface Calculator {
  // Method signatures
  add(a: number, b: number): number;
  subtract(a: number, b: number): number;
  
  // Function property
  multiply: (a: number, b: number) => number;
  
  // Optional method
  divide?(a: number, b: number): number;
}

const calculator: Calculator = {
  add(a, b) { return a + b; },
  subtract(a, b) { return a - b; },
  multiply: (a, b) => a * b
  // divide is optional, so we can omit it
};

// Call signature
interface Callable {
  (input: string): string;
  description: string;
}

const processor: Callable = function(input: string): string {
  return input.toUpperCase();
} as Callable;

processor.description = "Converts string to uppercase";
```

### Interface Inheritance

```typescript
// Base interface
interface Animal {
  name: string;
  age: number;
  makeSound(): void;
}

// Extending interface
interface Dog extends Animal {
  breed: string;
  wagTail(): void;
}

// Multiple inheritance
interface Pet {
  owner: string;
  isVaccinated: boolean;
}

interface DomesticDog extends Dog, Pet {
  registrationNumber: string;
}

const myDog: DomesticDog = {
  name: "Buddy",
  age: 3,
  breed: "Golden Retriever",
  owner: "John",
  isVaccinated: true,
  registrationNumber: "DOG123",
  makeSound() {
    console.log("Woof!");
  },
  wagTail() {
    console.log("Wagging tail happily!");
  }
};
```

### Type Aliases

```typescript
// Basic type alias
type UserID = string | number;
type Status = "pending" | "approved" | "rejected";

// Object type alias
type Point = {
  x: number;
  y: number;
};

// Function type alias
type EventHandler = (event: Event) => void;
type AsyncFunction<T> = () => Promise<T>;

// Union type alias
type Theme = "light" | "dark" | "auto";
type Size = "small" | "medium" | "large";

// Using type aliases
let userId: UserID = "user123";
userId = 456; // Also valid

const point: Point = { x: 10, y: 20 };
const status: Status = "pending";
```

### Advanced Type Aliases

```typescript
// Generic type alias
type Result<T, E = Error> = {
  success: true;
  data: T;
} | {
  success: false;
  error: E;
};

// Utility type aliases
type Partial<T> = {
  [P in keyof T]?: T[P];
};

type Required<T> = {
  [P in keyof T]-?: T[P];
};

// Conditional type alias
type NonNullable<T> = T extends null | undefined ? never : T;

// Usage examples
type UserResult = Result<User>;
type PartialUser = Partial<User>;

function handleResult(result: UserResult): void {
  if (result.success) {
    console.log("User data:", result.data);
  } else {
    console.error("Error:", result.error);
  }
}
```

### Interfaces vs Type Aliases

```typescript
// Interface - can be extended and merged
interface UserInterface {
  name: string;
}

interface UserInterface {
  age: number; // Declaration merging
}

// Type alias - cannot be merged
type UserType = {
  name: string;
};

// type UserType = {        // Error: Duplicate identifier
//   age: number;
// };

// Interface extension
interface ExtendedUser extends UserInterface {
  email: string;
}

// Type alias intersection
type ExtendedUserType = UserType & {
  email: string;
};

// Both work similarly for most use cases
const user1: ExtendedUser = {
  name: "John",
  age: 30,
  email: "john@example.com"
};

const user2: ExtendedUserType = {
  name: "Jane",
  email: "jane@example.com"
};
```

### Complex Interface Examples

```typescript
// API Response interface
interface APIResponse<T> {
  success: boolean;
  data?: T;
  error?: {
    code: number;
    message: string;
    details?: Record<string, any>;
  };
  meta: {
    timestamp: string;
    requestId: string;
    version: string;
  };
}

// Database Entity interface
interface BaseEntity {
  id: string;
  createdAt: Date;
  updatedAt: Date;
  deletedAt?: Date;
}

interface User extends BaseEntity {
  username: string;
  email: string;
  profile: UserProfile;
  settings: UserSettings;
}

interface UserProfile {
  firstName: string;
  lastName: string;
  avatar?: string;
  bio?: string;
  socialLinks: {
    twitter?: string;
    linkedin?: string;
    github?: string;
  };
}

interface UserSettings {
  theme: Theme;
  notifications: {
    email: boolean;
    push: boolean;
    sms: boolean;
  };
  privacy: {
    profileVisible: boolean;
    showEmail: boolean;
  };
}

// Event system interfaces
interface EventMap {
  "user:created": { user: User };
  "user:updated": { user: User; changes: Partial<User> };
  "user:deleted": { userId: string };
}

interface EventEmitter {
  on<K extends keyof EventMap>(event: K, handler: (data: EventMap[K]) => void): void;
  emit<K extends keyof EventMap>(event: K, data: EventMap[K]): void;
  off<K extends keyof EventMap>(event: K, handler: (data: EventMap[K]) => void): void;
}
```

### Practice Exercises

```typescript
// Exercise 1: Library Management System
interface Book {
  readonly isbn: string;
  title: string;
  author: string;
  publishedYear: number;
  genre: string;
  isAvailable: boolean;
}

interface Member {
  readonly id: string;
  name: string;
  email: string;
  joinDate: Date;
  borrowedBooks: string[]; // ISBN numbers
}

interface Library {
  name: string;
  books: Book[];
  members: Member[];
  
  addBook(book: Book): void;
  removeBook(isbn: string): boolean;
  borrowBook(memberID: string, isbn: string): boolean;
  returnBook(memberID: string, isbn: string): boolean;
  findBooks(criteria: Partial<Pick<Book, 'title' | 'author' | 'genre'>>): Book[];
}

class PublicLibrary implements Library {
  name: string;
  books: Book[] = [];
  members: Member[] = [];
  
  constructor(name: string) {
    this.name = name;
  }
  
  addBook(book: Book): void {
    this.books.push(book);
  }
  
  removeBook(isbn: string): boolean {
    const index = this.books.findIndex(book => book.isbn === isbn);
    if (index > -1) {
      this.books.splice(index, 1);
      return true;
    }
    return false;
  }
  
  borrowBook(memberID: string, isbn: string): boolean {
    const book = this.books.find(b => b.isbn === isbn && b.isAvailable);
    const member = this.members.find(m => m.id === memberID);
    
    if (book && member) {
      book.isAvailable = false;
      member.borrowedBooks.push(isbn);
      return true;
    }
    return false;
  }
  
  returnBook(memberID: string, isbn: string): boolean {
    const book = this.books.find(b => b.isbn === isbn);
    const member = this.members.find(m => m.id === memberID);
    
    if (book && member) {
      const bookIndex = member.borrowedBooks.indexOf(isbn);
      if (bookIndex > -1) {
        book.isAvailable = true;
        member.borrowedBooks.splice(bookIndex, 1);
        return true;
      }
    }
    return false;
  }
  
  findBooks(criteria: Partial<Pick<Book, 'title' | 'author' | 'genre'>>): Book[] {
    return this.books.filter(book => {
      return Object.entries(criteria).every(([key, value]) => {
        return book[key as keyof Book] === value;
      });
    });
  }
}

// Exercise 2: Configuration System
type Environment = "development" | "staging" | "production";
type LogLevel = "debug" | "info" | "warn" | "error";

interface DatabaseConfig {
  host: string;
  port: number;
  username: string;
  password: string;
  database: string;
  ssl?: boolean;
}

interface RedisConfig {
  host: string;
  port: number;
  password?: string;
  database?: number;
}

interface AppConfig {
  environment: Environment;
  port: number;
  logLevel: LogLevel;
  database: DatabaseConfig;
  redis: RedisConfig;
  features: {
    [featureName: string]: boolean;
  };
  secrets: {
    jwtSecret: string;
    apiKey: string;
  };
}

// Configuration factory
type ConfigInput = {
  [K in keyof AppConfig]?: K extends "features" ? Record<string, boolean> : 
                         K extends "database" | "redis" ? Partial<AppConfig[K]> :
                         AppConfig[K];
};

function createConfig(input: ConfigInput): AppConfig {
  const defaults: AppConfig = {
    environment: "development",
    port: 3000,
    logLevel: "info",
    database: {
      host: "localhost",
      port: 5432,
      username: "postgres",
      password: "password",
      database: "myapp"
    },
    redis: {
      host: "localhost",
      port: 6379
    },
    features: {},
    secrets: {
      jwtSecret: "default-secret",
      apiKey: "default-api-key"
    }
  };
  
  return {
    ...defaults,
    ...input,
    database: { ...defaults.database, ...input.database },
    redis: { ...defaults.redis, ...input.redis },
    features: { ...defaults.features, ...input.features },
    secrets: { ...defaults.secrets, ...input.secrets }
  };
}

const config = createConfig({
  environment: "production",
  database: {
    host: "prod-db.example.com",
    ssl: true
  },
  features: {
    newUI: true,
    betaFeatures: false
  }
});
```

---

## 6. Classes and Object-Oriented Programming

### Basic Class Syntax

```typescript
class Person {
  // Properties
  name: string;
  age: number;
  private _id: string;
  
  // Constructor
  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
    this._id = this.generateId();
  }
  
  // Methods
  greet(): string {
    return `Hello, my name is ${this.name}`;
  }
  
  haveBirthday(): void {
    this.age++;
    console.log(`Happy birthday! Now ${this.age} years old.`);
  }
  
  // Private method
  private generateId(): string {
    return Math.random().toString(36).substr(2, 9);
  }
  
  // Getter
  get id(): string {
    return this._id;
  }
  
  // Setter
  set id(value: string) {
    if (value.length > 0) {
      this._id = value;
    }
  }
}

// Using the class
const person = new Person("Alice", 25);
console.log(person.greet());
console.log(person.id); // Getter
person.haveBirthday();
```

### Access Modifiers

```typescript
class BankAccount {
  public accountHolder: string;     // Public (default)
  protected accountNumber: string;  // Accessible in subclasses
  private balance: number;          // Only accessible within this class
  readonly bankName: string;        // Cannot be changed after initialization
  
  constructor(accountHolder: string, initialBalance: number = 0) {
    this.accountHolder = accountHolder;
    this.accountNumber = this.generateAccountNumber();
    this.balance = initialBalance;
    this.bankName = "TypeScript Bank";
  }
  
  public deposit(amount: number): void {
    if (amount > 0) {
      this.balance += amount;
      console.log(`Deposited $${amount}. New balance: $${this.balance}`);
    }
  }
  
  public withdraw(amount: number): boolean {
    if (amount > 0 && amount <= this.balance) {
      this.balance -= amount;
      console.log(`Withdrew $${amount}. New balance: $${this.balance}`);
      return true;
    }
    console.log("Insufficient funds or invalid amount");
    return false;
  }
  
  public getBalance(): number {
    return this.balance;
  }
  
  protected generateAccountNumber(): string {
    return `ACC${Math.random().toString().substr(2, 8)}`;
  }
  
  private validateAmount(amount: number): boolean {
    return amount > 0 && amount <= 10000;
  }
}

const account = new BankAccount("John Doe", 1000);
account.deposit(500);
account.withdraw(200);
console.log(`Balance: $${account.getBalance()}`);
// console.log(account.balance); // Error: Property 'balance' is private
```

### Parameter Properties

```typescript
// Shorthand for constructor parameters
class Product {
  constructor(
    public readonly id: string,
    public name: string,
    private _price: number,
    protected category: string
  ) {
    // Properties are automatically created and assigned
  }
  
  get price(): number {
    return this._price;
  }
  
  set price(value: number) {
    if (value >= 0) {
      this._price = value;
    }
  }
  
  getInfo(): string {
    return `${this.name} - $${this._price}`;
  }
}

// Equivalent to the longer form above
const product = new Product("P001", "Laptop", 999.99, "Electronics");
```

### Inheritance

```typescript
// Base class
class Vehicle {
  protected speed: number = 0;
  
  constructor(public make: string, public model: string, public year: number) {}
  
  start(): void {
    console.log(`${this.make} ${this.model} is starting...`);
  }
  
  accelerate(increment: number): void {
    this.speed += increment;
    console.log(`Speed increased to ${this.speed} mph`);
  }
  
  brake(): void {
    this.speed = Math.max(0, this.speed - 10);
    console.log(`Braking... Speed: ${this.speed} mph`);
  }
  
  getSpeed(): number {
    return this.speed;
  }
}

// Derived class
class Car extends Vehicle {
  constructor(
    make: string,
    model: string,
    year: number,
    public doors: number,
    private fuelType: string
  ) {
    super(make, model, year); // Call parent constructor
  }
  
  // Override parent method
  start(): void {
    console.log("Inserting key...");
    super.start(); // Call parent method
    console.log("Car is ready to drive!");
  }
  
  // New method specific to Car
  honk(): void {
    console.log("Beep beep!");
  }
  
  getFuelType(): string {
    return this.fuelType;
  }
}

class Motorcycle extends Vehicle {
  constructor(
    make: string,
    model: string,
    year: number,
    public engineSize: number
  ) {
    super(make, model, year);
  }
  
  start(): void {
    console.log("Kick starting...");
    super.start();
    console.log("Motorcycle is ready!");
  }
  
  wheelie(): void {
    if (this.speed > 20) {
      console.log("Performing wheelie!");
    } else {
      console.log("Need more speed for wheelie");
    }
  }
}

// Usage
const car = new Car("Toyota", "Camry", 2023, 4, "Gasoline");
const motorcycle = new Motorcycle("Harley-Davidson", "Street 750", 2023, 750);

car.start();
car.accelerate(30);
car.honk();

motorcycle.start();
motorcycle.accelerate(25);
motorcycle.wheelie();
```

### Abstract Classes

```typescript
// Abstract base class
abstract class Shape {
  constructor(protected color: string) {}
  
  // Abstract method - must be implemented by subclasses
  abstract calculateArea(): number;
  abstract calculatePerimeter(): number;
  
  // Concrete method - available to all subclasses
  getColor(): string {
    return this.color;
  }
  
  // Another concrete method
  describe(): string {
    return `A ${this.color} shape with area ${this.calculateArea().toFixed(2)}`;
  }
}

class Rectangle extends Shape {
  constructor(
    color: string,
    private width: number,
    private height: number
  ) {
    super(color);
  }
  
  calculateArea(): number {
    return this.width * this.height;
  }
  
  calculatePerimeter(): number {
    return 2 * (this.width + this.height);
  }
  
  getDimensions(): { width: number; height: number } {
    return { width: this.width, height: this.height };
  }
}

class Circle extends Shape {
  constructor(color: string, private radius: number) {
    super(color);
  }
  
  calculateArea(): number {
    return Math.PI * this.radius * this.radius;
  }
  
  calculatePerimeter(): number {
    return 2 * Math.PI * this.radius;
  }
  
  getRadius(): number {
    return this.radius;
  }
}

// Usage
const rectangle = new Rectangle("blue", 10, 5);
const circle = new Circle("red", 7);

console.log(rectangle.describe());
console.log(circle.describe());

// const shape = new Shape("green"); // Error: Cannot create instance of abstract class
```

### Static Members

```typescript
class MathUtils {
  static readonly PI = 3.14159;
  private static instanceCount = 0;
  
  constructor() {
    MathUtils.instanceCount++;
  }
  
  static calculateCircleArea(radius: number): number {
    return MathUtils.PI * radius * radius;
  }
  
  static calculateDistance(x1: number, y1: number, x2: number, y2: number): number {
    return Math.sqrt(Math.pow(x2 - x1, 2) + Math.pow(y2 - y1, 2));
  }
  
  static getInstanceCount(): number {
    return MathUtils.instanceCount;
  }
  
  // Static factory method
  static createPoint(x: number, y: number): Point {
    return new Point(x, y);
  }
}

class Point {
  constructor(public x: number, public y: number) {}
  
  distanceTo(other: Point): number {
    return MathUtils.calculateDistance(this.x, this.y, other.x, other.y);
  }
}

// Usage of static members
console.log(MathUtils.calculateCircleArea(5));
console.log(MathUtils.PI);

const point1 = MathUtils.createPoint(0, 0);
const point2 = MathUtils.createPoint(3, 4);
console.log(point1.distanceTo(point2)); // 5
```

### Implementing Interfaces

```typescript
// Interface definitions
interface Flyable {
  fly(): void;
  altitude: number;
}

interface Swimmable {
  swim(): void;
  depth: number;
}

interface Animal {
  name: string;
  age: number;
  makeSound(): void;
}

// Class implementing multiple interfaces
class Duck implements Animal, Flyable, Swimmable {
  altitude: number = 0;
  depth: number = 0;
  
  constructor(public name: string, public age: number) {}
  
  makeSound(): void {
    console.log("Quack!");
  }
  
  fly(): void {
    this.altitude = 100;
    console.log(`${this.name} is flying at ${this.altitude} feet`);
  }
  
  swim(): void {
    this.depth = 5;
    console.log(`${this.name} is swimming at ${this.depth} feet deep`);
  }
  
  land(): void {
    this.altitude = 0;
    console.log(`${this.name} has landed`);
  }
}

// Class implementing single interface
class Fish implements Animal, Swimmable {
  depth: number = 0;
  
  constructor(public name: string, public age: number) {}
  
  makeSound(): void {
    console.log("Blub blub");
  }
  
  swim(): void {
    this.depth = 20;
    console.log(`${this.name} is swimming at ${this.depth} feet deep`);
  }
}

const duck = new Duck("Donald", 3);
const fish = new Fish("Nemo", 1);

duck.makeSound();
duck.fly();
duck.swim();
duck.land();

fish.makeSound();
fish.swim();
```

### Getters and Setters

```typescript
class Temperature {
  private _celsius: number;
  
  constructor(celsius: number) {
    this._celsius = celsius;
  }
  
  // Getter for Fahrenheit
  get fahrenheit(): number {
    return (this._celsius * 9/5) + 32;
  }
  
  // Setter for Fahrenheit
  set fahrenheit(value: number) {
    this._celsius = (value - 32) * 5/9;
  }
  
  // Getter for Celsius
  get celsius(): number {
    return this._celsius;
  }
  
  // Setter for Celsius with validation
  set celsius(value: number) {
    if (value < -273.15) {
      throw new Error("Temperature cannot be below absolute zero");
    }
    this._celsius = value;
  }
  
  // Getter for Kelvin
  get kelvin(): number {
    return this._celsius + 273.15;
  }
  
  // Setter for Kelvin
  set kelvin(value: number) {
    if (value < 0) {
      throw new Error("Kelvin cannot be negative");
    }
    this._celsius = value - 273.15;
  }
  
  toString(): string {
    return `${this._celsius}°C (${this.fahrenheit.toFixed(1)}°F, ${this.kelvin.toFixed(1)}K)`;
  }
}

const temp = new Temperature(25);
console.log(temp.toString()); // 25°C (77.0°F, 298.1K)

temp.fahrenheit = 100;
console.log(temp.toString()); // 37.8°C (100.0°F, 310.9K)

temp.kelvin = 300;
console.log(temp.toString()); // 26.9°C (80.3°F, 300.0K)
```

### Practice Exercises

```typescript
// Exercise 1: Task Management System
abstract class Task {
  protected static idCounter = 0;
  public readonly id: string;
  public createdAt: Date;
  
  constructor(
    public title: string,
    public description: string,
    protected _status: "pending" | "in-progress" | "completed" = "pending"
  ) {
    this.id = `task-${++Task.idCounter}`;
    this.createdAt = new Date();
  }
  
  get status(): string {
    return this._status;
  }
  
  abstract start(): void;
  abstract complete(): void;
  
  getInfo(): string {
    return `${this.title} (${this._status})`;
  }
}

class SimpleTask extends Task {
  start(): void {
    if (this._status === "pending") {
      this._status = "in-progress";
      console.log(`Started task: ${this.title}`);
    }
  }
  
  complete(): void {
    if (this._status === "in-progress") {
      this._status = "completed";
      console.log(`Completed task: ${this.title}`);
    }
  }
}

class ProjectTask extends Task {
  private subtasks: SimpleTask[] = [];
  
  constructor(
    title: string,
    description: string,
    public deadline: Date
  ) {
    super(title, description);
  }
  
  addSubtask(title: string, description: string): void {
    const subtask = new SimpleTask(title, description);
    this.subtasks.push(subtask);
  }
  
  start(): void {
    if (this._status === "pending") {
      this._status = "in-progress";
      console.log(`Started project: ${this.title}`);
    }
  }
  
  complete(): void {
    const allCompleted = this.subtasks.every(task => task.status === "completed");
    if (allCompleted && this._status === "in-progress") {
      this._status = "completed";
      console.log(`Completed project: ${this.title}`);
    } else {
      console.log("Cannot complete project: subtasks still pending");
    }
  }
  
  getProgress(): number {
    if (this.subtasks.length === 0) return 0;
    const completed = this.subtasks.filter(task => task.status === "completed").length;
    return (completed / this.subtasks.length) * 100;
  }
  
  getSubtasks(): SimpleTask[] {
    return [...this.subtasks]; // Return copy to prevent modification
  }
}

// Usage
const project = new ProjectTask("Build Website", "Create a company website", new Date("2024-12-31"));
project.addSubtask("Design mockups", "Create visual designs");
project.addSubtask("Implement frontend", "Code the user interface");
project.addSubtask("Setup backend", "Create API and database");

project.start();
const subtasks = project.getSubtasks();
subtasks[0].start();
subtasks[0].complete();

console.log(`Project progress: ${project.getProgress()}%`);

// Exercise 2: Game Character System
interface Combatant {
  health: number;
  attack(target: Combatant): void;
  takeDamage(amount: number): void;
  isAlive(): boolean;
}

abstract class Character implements Combatant {
  protected maxHealth: number;
  private _health: number;
  protected _level: number = 1;
  protected _experience: number = 0;
  
  constructor(
    public name: string,
    maxHealth: number,
    protected attackPower: number
  ) {
    this.maxHealth = maxHealth;
    this._health = maxHealth;
  }
  
  get health(): number {
    return this._health;
  }
  
  get level(): number {
    return this._level;
  }
  
  get experience(): number {
    return this._experience;
  }
  
  attack(target: Combatant): void {
    const damage = this.calculateDamage();
    console.log(`${this.name} attacks for ${damage} damage!`);
    target.takeDamage(damage);
  }
  
  takeDamage(amount: number): void {
    this._health = Math.max(0, this._health - amount);
    console.log(`${this.name} takes ${amount} damage! Health: ${this._health}/${this.maxHealth}`);
    
    if (!this.isAlive()) {
      console.log(`${this.name} has been defeated!`);
    }
  }
  
  heal(amount: number): void {
    this._health = Math.min(this.maxHealth, this._health + amount);
    console.log(`${this.name} heals for ${amount}! Health: ${this._health}/${this.maxHealth}`);
  }
  
  isAlive(): boolean {
    return this._health > 0;
  }
  
  gainExperience(amount: number): void {
    this._experience += amount;
    const experienceNeeded = this._level * 100;
    
    if (this._experience >= experienceNeeded) {
      this.levelUp();
    }
  }
  
  protected levelUp(): void {
    this._level++;
    this._experience = 0;
    this.maxHealth += 10;
    this._health = this.maxHealth;
    this.attackPower += 5;
    console.log(`${this.name} leveled up! Level ${this._level}`);
  }
  
  protected abstract calculateDamage(): number;
  abstract getCharacterInfo(): string;
}

class Warrior extends Character {
  constructor(name: string) {
    super(name, 120, 25);
  }
  
  protected calculateDamage(): number {
    return this.attackPower + Math.floor(Math.random() * 10);
  }
  
  // Special ability
  powerAttack(target: Combatant): void {
    const damage = this.attackPower * 1.5;
    console.log(`${this.name} uses Power Attack for ${damage} damage!`);
    target.takeDamage(damage);
  }
  
  getCharacterInfo(): string {
    return `Warrior ${this.name} - Level ${this._level} - Health: ${this.health}/${this.maxHealth}`;
  }
}

class Mage extends Character {
  private _mana: number = 100;
  
  constructor(name: string) {
    super(name, 80, 15);
  }
  
  get mana(): number {
    return this._mana;
  }
  
  protected calculateDamage(): number {
    return this.attackPower + Math.floor(Math.random() * 15);
  }
  
  // Special ability
  fireball(target: Combatant): void {
    if (this._mana >= 20) {
      this._mana -= 20;
      const damage = this.attackPower * 2;
      console.log(`${this.name} casts Fireball for ${damage} damage! Mana: ${this._mana}`);
      target.takeDamage(damage);
    } else {
      console.log(`${this.name} doesn't have enough mana for Fireball!`);
    }
  }
  
  restoreMana(amount: number): void {
    this._mana = Math.min(100, this._mana + amount);
    console.log(`${this.name} restores ${amount} mana! Mana: ${this._mana}`);
  }
  
  getCharacterInfo(): string {
    return `Mage ${this.name} - Level ${this._level} - Health: ${this.health}/${this.maxHealth} - Mana: ${this._mana}`;
  }
}

// Battle simulation
const warrior = new Warrior("Conan");
const mage = new Mage("Gandalf");

console.log(warrior.getCharacterInfo());
console.log(mage.getCharacterInfo());

// Fight!
warrior.attack(mage);
mage.fireball(warrior);
warrior.powerAttack(mage);
mage.attack(warrior);

warrior.gainExperience(150);
mage.gainExperience(120);
```

---

## 7. Advanced Types

### Union Types

```typescript
// Basic union types
type Status = "loading" | "success" | "error";
type ID = string | number;

function handleStatus(status: Status): void {
  switch (status) {
    case "loading":
      console.log("Loading...");
      break;
    case "success":
      console.log("Operation successful!");
      break;
    case "error":
      console.log("An error occurred!");
      break;
    default:
      // TypeScript ensures exhaustive checking
      const exhaustiveCheck: never = status;
      throw new Error(`Unhandled status: ${exhaustiveCheck}`);
  }
}

// Union types with objects
interface LoadingState {
  status: "loading";
}

interface SuccessState {
  status: "success";
  data: any;
}

interface ErrorState {
  status: "error";
  error: string;
}

type AsyncState = LoadingState | SuccessState | ErrorState;

function handleAsyncState(state: AsyncState): void {
  // Type narrowing with discriminated unions
  if (state.status === "loading") {
    console.log("Loading...");
  } else if (state.status === "success") {
    console.log("Data:", state.data); // TypeScript knows state.data exists
  } else {
    console.error("Error:", state.error); // TypeScript knows state.error exists
  }
}
```

### Intersection Types

```typescript
// Combining types with intersection
interface Timestamped {
  createdAt: Date;
  updatedAt: Date;
}

interface Identifiable {
  id: string;
}

interface User {
  name: string;
  email: string;
}

// Intersection type
type UserEntity = User & Timestamped & Identifiable;

const user: UserEntity = {
  id: "user-123",
  name: "John Doe",
  email: "john@example.com",
  createdAt: new Date(),
  updatedAt: new Date()
};

// Mixin pattern with intersection types
interface Flyable {
  fly(): void;
}

interface Swimmable {
  swim(): void;
}

type Duck = Flyable & Swimmable & {
  name: string;
  quack(): void;
};

const duck: Duck = {
  name: "Donald",
  fly() { console.log("Flying!"); },
  swim() { console.log("Swimming!"); },
  quack() { console.log("Quack!"); }
};
```

### Type Guards

```typescript
// typeof type guards
function processValue(value: string | number): string {
  if (typeof value === "string") {
    return value.toUpperCase(); // TypeScript knows value is string
  } else {
    return value.toFixed(2); // TypeScript knows value is number
  }
}

// instanceof type guards
class Dog {
  bark(): void { console.log("Woof!"); }
}

class Cat {
  meow(): void { console.log("Meow!"); }
}

function petSound(animal: Dog | Cat): void {
  if (animal instanceof Dog) {
    animal.bark(); // TypeScript knows animal is Dog
  } else {
    animal.meow(); // TypeScript knows animal is Cat
  }
}

// Custom type guards
interface Fish {
  swim(): void;
  layEggs(): void;
}

interface Bird {
  fly(): void;
  layEggs(): void;
}

// User-defined type guard
function isFish(pet: Fish | Bird): pet is Fish {
  return (pet as Fish).swim !== undefined;
}

function petAction(pet: Fish | Bird): void {
  if (isFish(pet)) {
    pet.swim(); // TypeScript knows pet is Fish
  } else {
    pet.fly(); // TypeScript knows pet is Bird
  }
}

// Type guard with arrays
function isStringArray(value: unknown): value is string[] {
  return Array.isArray(value) && value.every(item => typeof item === "string");
}

function processArray(data: unknown): void {
  if (isStringArray(data)) {
    data.forEach(str => console.log(str.toUpperCase())); // Safe to use string methods
  }
}
```

### Conditional Types

```typescript
// Basic conditional type
type IsArray<T> = T extends any[] ? true : false;

type StringIsArray = IsArray<string>; // false
type NumberArrayIsArray = IsArray<number[]>; // true

// More complex conditional types
type NonNullable<T> = T extends null | undefined ? never : T;

type ApiResponse<T> = T extends string 
  ? { message: T }
  : T extends number 
  ? { code: T }
  : { data: T };

type StringResponse = ApiResponse<string>; // { message: string }
type NumberResponse = ApiResponse<number>; // { code: number }
type ObjectResponse = ApiResponse<{ name: string }>; // { data: { name: string } }

// Conditional types with infer
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : never;

type FuncReturn = ReturnType<(a: number, b: string) => boolean>; // boolean

type ArrayElement<T> = T extends (infer U)[] ? U : never;

type StringArrayElement = ArrayElement<string[]>; // string
type NumberArrayElement = ArrayElement<number[]>; // number

// Distributive conditional types
type ToArray<T> = T extends any ? T[] : never;

type StringOrNumberArray = ToArray<string | number>; // string[] | number[]
```

### Mapped Types

```typescript
// Basic mapped type
type Readonly<T> = {
  readonly [P in keyof T]: T[P];
};

type Partial<T> = {
  [P in keyof T]?: T[P];
};

interface User {
  id: string;
  name: string;
  email: string;
  age: number;
}

type ReadonlyUser = Readonly<User>;
type PartialUser = Partial<User>;

// Custom mapped types
type Nullable<T> = {
  [P in keyof T]: T[P] | null;
};

type Stringify<T> = {
  [P in keyof T]: string;
};

type NullableUser = Nullable<User>;
type StringifiedUser = Stringify<User>;

// Mapped types with template literal types
type Getters<T> = {
  [P in keyof T as `get${Capitalize<string & P>}`]: () => T[P];
};

type Setters<T> = {
  [P in keyof T as `set${Capitalize<string & P>}`]: (value: T[P]) => void;
};

type UserGetters = Getters<User>;
// {
//   getId: () => string;
//   getName: () => string;
//   getEmail: () => string;
//   getAge: () => number;
// }

type UserSetters = Setters<User>;
// {
//   setId: (value: string) => void;
//   setName: (value: string) => void;
//   setEmail: (value: string) => void;
//   setAge: (value: number) => void;
// }

// Key remapping with filtering
type PickByType<T, U> = {
  [P in keyof T as T[P] extends U ? P : never]: T[P];
};

type UserStrings = PickByType<User, string>; // { id: string; name: string; email: string; }
type UserNumbers = PickByType<User, number>; // { age: number; }
```

### Template Literal Types

```typescript
// Basic template literal types
type Greeting = `hello ${string}`;
type SpecificGreeting = `hello ${"world" | "TypeScript"}`; // "hello world" | "hello TypeScript"

// Event system with template literals
type EventName = "click" | "hover" | "focus";
type ElementType = "button" | "input" | "div";

type EventHandler = `on${Capitalize<EventName>}`;
type ElementEvent = `${ElementType}:${EventName}`;

type ButtonEvents = `button:${EventName}`; // "button:click" | "button:hover" | "button:focus"

// CSS properties with template literals
type CSSLength = `${number}px` | `${number}em` | `${number}rem` | `${number}%`;
type CSSColor = `#${string}` | `rgb(${number}, ${number}, ${number})` | `hsl(${number}, ${number}%, ${number}%)`;

interface CSSProperties {
  width?: CSSLength;
  height?: CSSLength;
  color?: CSSColor;
  backgroundColor?: CSSColor;
}

const styles: CSSProperties = {
  width: "100px",
  height: "2em",
  color: "#ff0000",
  backgroundColor: "rgb(255, 255, 255)"
};

// API endpoint types
type HttpMethod = "GET" | "POST" | "PUT" | "DELETE";
type ApiVersion = "v1" | "v2";
type Resource = "users" | "posts" | "comments";

type ApiEndpoint = `/api/${ApiVersion}/${Resource}`;
type ApiRoute = `${HttpMethod} ${ApiEndpoint}`;

type UserRoutes = `${HttpMethod} /api/${ApiVersion}/users`; // All HTTP methods for users
```

### Utility Types

```typescript
// Built-in utility types examples
interface User {
  id: string;
  name: string;
  email: string;
  age: number;
  isActive: boolean;
}

// Partial - makes all properties optional
type PartialUser = Partial<User>;
const updateUser: PartialUser = { name: "John" }; // Only name is required

// Required - makes all properties required
interface OptionalUser {
  id?: string;
  name?: string;
  email?: string;
}

type RequiredUser = Required<OptionalUser>;
const user: RequiredUser = {
  id: "1",
  name: "John",
  email: "john@example.com" // All properties are now required
};

// Pick - select specific properties
type UserProfile = Pick<User, "name" | "email">;
const profile: UserProfile = {
  name: "John",
  email: "john@example.com"
};

// Omit - exclude specific properties
type PublicUser = Omit<User, "id" | "isActive">;
const publicUser: PublicUser = {
  name: "John",
  email: "john@example.com",
  age: 30
};

// Record - create object type with specific keys and values
type UserRoles = "admin" | "user" | "guest";
type Permissions = Record<UserRoles, string[]>;

const permissions: Permissions = {
  admin: ["read", "write", "delete"],
  user: ["read", "write"],
  guest: ["read"]
};

// Exclude and Extract with union types
type Status = "loading" | "success" | "error" | "idle";
type ActiveStatus = Exclude<Status, "idle">; // "loading" | "success" | "error"
type LoadingOrError = Extract<Status, "loading" | "error">; // "loading" | "error"

// ReturnType and Parameters
function createUser(name: string, age: number): User {
  return {
    id: Math.random().toString(),
    name,
    email: `${name.toLowerCase()}@example.com`,
    age,
    isActive: true
  };
}

type CreateUserReturn = ReturnType<typeof createUser>; // User
type CreateUserParams = Parameters<typeof createUser>; // [string, number]

// ConstructorParameters
class UserService {
  constructor(private apiUrl: string, private timeout: number) {}
}

type UserServiceParams = ConstructorParameters<typeof UserService>; // [string, number]
```

### Advanced Type Manipulation

```typescript
// Deep partial type
type DeepPartial<T> = {
  [P in keyof T]?: T[P] extends object ? DeepPartial<T[P]> : T[P];
};

interface NestedConfig {
  database: {
    host: string;
    port: number;
    credentials: {
      username: string;
      password: string;
    };
  };
  cache: {
    enabled: boolean;
    ttl: number;
  };
}

type PartialConfig = DeepPartial<NestedConfig>;
const config: PartialConfig = {
  database: {
    host: "localhost"
    // Other properties are optional
  }
};

// Path type for nested object properties
type Path<T> = T extends object 
  ? {
      [K in keyof T]: K extends string
        ? T[K] extends object
          ? K | `${K}.${Path<T[K]>}`
          : K
        : never;
    }[keyof T]
  : never;

type ConfigPaths = Path<NestedConfig>;
// "database" | "cache" | "database.host" | "database.port" | "database.credentials" | 
// "database.credentials.username" | "database.credentials.password" | "cache.enabled" | "cache.ttl"

// Get type by path
type GetByPath<T, P extends string> = P extends `${infer Key}.${infer Rest}`
  ? Key extends keyof T
    ? GetByPath<T[Key], Rest>
    : never
  : P extends keyof T
  ? T[P]
  : never;

type DatabaseHost = GetByPath<NestedConfig, "database.host">; // string
type CacheEnabled = GetByPath<NestedConfig, "cache.enabled">; // boolean

// Function overloading with conditional types
function getValue<T, P extends Path<T>>(obj: T, path: P): GetByPath<T, P>;
function getValue(obj: any, path: string): any {
  return path.split('.').reduce((current, key) => current?.[key], obj);
}

const configValue = getValue(config, "database.host"); // TypeScript knows this is string
```

### Practice Exercises

```typescript
// Exercise 1: Form Validation System
type ValidationRule<T> = {
  required?: boolean;
  minLength?: T extends string ? number : never;
  maxLength?: T extends string ? number : never;
  min?: T extends number ? number : never;
  max?: T extends number ? number : never;
  pattern?: T extends string ? RegExp : never;
  custom?: (value: T) => boolean;
};

type FormSchema<T> = {
  [K in keyof T]: ValidationRule<T[K]>;
};

type ValidationResult<T> = {
  [K in keyof T]: {
    value: T[K];
    isValid: boolean;
    errors: string[];
  };
};

interface UserForm {
  name: string;
  email: string;
  age: number;
  website?: string;
}

const userFormSchema: FormSchema<UserForm> = {
  name: {
    required: true,
    minLength: 2,
    maxLength: 50
  },
  email: {
    required: true,
    pattern: /^[^\s@]+@[^\s@]+\.[^\s@]+$/
  },
  age: {
    required: true,
    min: 0,
    max: 120
  },
  website: {
    pattern: /^https?:\/\/.+/
  }
};

function validateForm<T extends Record<string, any>>(
  data: T,
  schema: FormSchema<T>
): ValidationResult<T> {
  const result = {} as ValidationResult<T>;
  
  for (const key in schema) {
    const value = data[key];
    const rules = schema[key];
    const errors: string[] = [];
    
    // Required validation
    if (rules.required && (value === undefined || value === null || value === "")) {
      errors.push(`${key} is required`);
    }
    
    if (value !== undefined && value !== null && value !== "") {
      // String validations
      if (typeof value === "string") {
        if (rules.minLength && value.length < rules.minLength) {
          errors.push(`${key} must be at least ${rules.minLength} characters`);
        }
        if (rules.maxLength && value.length > rules.maxLength) {
          errors.push(`${key} must be no more than ${rules.maxLength} characters`);
        }
        if (rules.pattern && !rules.pattern.test(value)) {
          errors.push(`${key} format is invalid`);
        }
      }
      
      // Number validations
      if (typeof value === "number") {
        if (rules.min !== undefined && value < rules.min) {
          errors.push(`${key} must be at least ${rules.min}`);
        }
        if (rules.max !== undefined && value > rules.max) {
          errors.push(`${key} must be no more than ${rules.max}`);
        }
      }
      
      // Custom validation
      if (rules.custom && !rules.custom(value)) {
        errors.push(`${key} failed custom validation`);
      }
    }
    
    result[key] = {
      value,
      isValid: errors.length === 0,
      errors
    };
  }
  
  return result;
}

// Usage
const formData: UserForm = {
  name: "Jo",
  email: "invalid-email",
  age: 150,
  website: "not-a-url"
};

const validationResult = validateForm(formData, userFormSchema);
console.log(validationResult);

// Exercise 2: State Machine with Discriminated Unions
type StateNode<TState extends string, TEvent extends string, TData = {}> = {
  state: TState;
  data: TData;
  transitions: Record<TEvent, TState>;
};

// Traffic light state machine
type TrafficLightState = "red" | "yellow" | "green";
type TrafficLightEvent = "next" | "reset";

const trafficLightMachine = {
  red: {
    state: "red" as const,
    data: { duration: 30 },
    transitions: {
      next: "green" as const,
      reset: "red" as const
    }
  },
  yellow: {
    state: "yellow" as const,
    data: { duration: 5 },
    transitions: {
      next: "red" as const,
      reset: "red" as const
    }
  },
  green: {
    state: "green" as const,
    data: { duration: 25 },
    transitions: {
      next: "yellow" as const,
      reset: "red" as const
    }
  }
};

type StateMachine<T> = {
  [K in keyof T]: T[K] extends StateNode<infer S, infer E, infer D>
    ? StateNode<S, E, D>
    : never;
};

type TrafficLightMachine = StateMachine<typeof trafficLightMachine>;

function createStateMachine<T extends Record<string, StateNode<any, any, any>>>(
  definition: T,
  initialState: keyof T
) {
  let currentState = initialState;
  
  return {
    getCurrentState: () => definition[currentState],
    transition: (event: string) => {
      const current = definition[currentState];
      const nextState = current.transitions[event];
      if (nextState && definition[nextState]) {
        currentState = nextState;
        return definition[currentState];
      }
      throw new Error(`Invalid transition: ${event} from ${current.state}`);
    },
    reset: () => {
      currentState = initialState;
      return definition[currentState];
    }
  };
}

const trafficLight = createStateMachine(trafficLightMachine, "red");
console.log(trafficLight.getCurrentState()); // red
console.log(trafficLight.transition("next")); // green
console.log(trafficLight.transition("next")); // yellow
console.log(trafficLight.transition("next")); // red
```

---

## 8. Modules and Namespaces

### ES6 Modules

#### Exporting

```typescript
// math.ts - Named exports
export function add(a: number, b: number): number {
  return a + b;
}

export function subtract(a: number, b: number): number {
  return a - b;
}

export const PI = 3.14159;

export class Calculator {
  multiply(a: number, b: number): number {
    return a * b;
  }
}

// Alternative export syntax
function divide(a: number, b: number): number {
  return a / b;
}

function power(base: number, exponent: number): number {
  return Math.pow(base, exponent);
}

export { divide, power };

// Default export
export default class MathUtils {
  static factorial(n: number): number {
    return n <= 1 ? 1 : n * MathUtils.factorial(n - 1);
  }
}
```

```typescript
// user.ts - Mixed exports
export interface User {
  id: string;
  name: string;
  email: string;
}

export type UserRole = "admin" | "user" | "guest";

export class UserService {
  private users: User[] = [];
  
  addUser(user: User): void {
    this.users.push(user);
  }
  
  getUser(id: string): User | undefined {
    return this.users.find(user => user.id === id);
  }
  
  getAllUsers(): User[] {
    return [...this.users];
  }
}

// Default export
export default function createUser(name: string, email: string): User {
  return {
    id: Math.random().toString(36).substr(2, 9),
    name,
    email
  };
}
```

#### Importing

```typescript
// main.ts - Various import styles

// Named imports
import { add, subtract, PI, Calculator } from "./math";

// Default import
import MathUtils from "./math";

// Mixed imports
import createUser, { User, UserService, UserRole } from "./user";

// Import all as namespace
import * as MathOperations from "./math";

// Import with alias
import { Calculator as Calc } from "./math";
import { add as sum } from "./math";

// Usage examples
console.log(add(5, 3)); // 8
console.log(PI); // 3.14159

const calc = new Calculator();
console.log(calc.multiply(4, 7)); // 28

console.log(MathUtils.factorial(5)); // 120

// Using namespace import
console.log(MathOperations.add(10, 20)); // 30
console.log(MathOperations.PI); // 3.14159

// Using renamed imports
const calculator = new Calc();
console.log(sum(1, 2)); // 3

// User service example
const userService = new UserService();
const newUser = createUser("John Doe", "john@example.com");
userService.addUser(newUser);
```

### Dynamic Imports

```typescript
// Dynamic imports for code splitting
async function loadMathModule() {
  try {
    const mathModule = await import("./math");
    console.log(mathModule.add(5, 3));
    
    const MathUtils = mathModule.default;
    console.log(MathUtils.factorial(4));
  } catch (error) {
    console.error("Failed to load math module:", error);
  }
}

// Conditional loading
async function loadUtilityBasedOnCondition(condition: boolean) {
  if (condition) {
    const { heavyUtility } = await import("./heavy-utility");
    return heavyUtility();
  } else {
    const { lightUtility } = await import("./light-utility");
    return lightUtility();
  }
}

// Dynamic import with type assertion
async function loadConfigModule() {
  const configModule = await import("./config") as {
    default: {
      apiUrl: string;
      timeout: number;
    };
  };
  
  return configModule.default;
}
```

### Module Resolution

```typescript
// types.ts - Type-only exports
export type ApiResponse<T> = {
  success: boolean;
  data: T;
  errors?: string[];
};

export interface PaginationParams {
  page: number;
  limit: number;
  sortBy?: string;
  order?: "asc" | "desc";
}

export interface PaginatedResponse<T> extends ApiResponse<T[]> {
  pagination: {
    page: number;
    totalPages: number;
    totalItems: number;
  };
}
```

```typescript
// api.ts - Using type-only imports
import type { ApiResponse, PaginationParams, PaginatedResponse } from "./types";

export class ApiClient {
  private baseUrl: string;
  
  constructor(baseUrl: string) {
    this.baseUrl = baseUrl;
  }
  
  async get<T>(endpoint: string): Promise<ApiResponse<T>> {
    // Implementation
    return {
      success: true,
      data: {} as T
    };
  }
  
  async getPaginated<T>(
    endpoint: string, 
    params: PaginationParams
  ): Promise<PaginatedResponse<T>> {
    // Implementation
    return {
      success: true,
      data: [] as T[],
      pagination: {
        page: params.page,
        totalPages: 1,
        totalItems: 0
      }
    };
  }
}

// Re-export for convenience
export type { ApiResponse, PaginationParams, PaginatedResponse } from "./types";
```

### Namespaces (Legacy)

```typescript
// geometry.ts - Namespace example
namespace Geometry {
  export interface Point {
    x: number;
    y: number;
  }
  
  export interface Rectangle {
    topLeft: Point;
    width: number;
    height: number;
  }
  
  export class Circle {
    constructor(public center: Point, public radius: number) {}
    
    getArea(): number {
      return Math.PI * this.radius * this.radius;
    }
    
    getCircumference(): number {
      return 2 * Math.PI * this.radius;
    }
  }
  
  export namespace Utils {
    export function distance(p1: Point, p2: Point): number {
      return Math.sqrt(Math.pow(p2.x - p1.x, 2) + Math.pow(p2.y - p1.y, 2));
    }
    
    export function midpoint(p1: Point, p2: Point): Point {
      return {
        x: (p1.x + p2.x) / 2,
        y: (p1.y + p2.y) / 2
      };
    }
  }
}

// Usage
const point1: Geometry.Point = { x: 0, y: 0 };
const point2: Geometry.Point = { x: 3, y: 4 };

const circle = new Geometry.Circle(point1, 5);
console.log(circle.getArea());

const distance = Geometry.Utils.distance(point1, point2);
const mid = Geometry.Utils.midpoint(point1, point2);
```

### Module Augmentation

```typescript
// Extending existing modules
declare global {
  interface Array<T> {
    shuffle(): T[];
    sample(): T | undefined;
  }
}

Array.prototype.shuffle = function<T>(this: T[]): T[] {
  const shuffled = [...this];
  for (let i = shuffled.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [shuffled[i], shuffled[j]] = [shuffled[j], shuffled[i]];
  }
  return shuffled;
};

Array.prototype.sample = function<T>(this: T[]): T | undefined {
  return this[Math.floor(Math.random() * this.length)];
};

// Now available on all arrays
const numbers = [1, 2, 3, 4, 5];
console.log(numbers.shuffle());
console.log(numbers.sample());

// Augmenting external library types
declare module "lodash" {
  interface LoDashStatic {
    customUtility<T>(data: T[]): T[];
  }
}

// If using lodash
// import _ from "lodash";
// _.customUtility = function<T>(data: T[]): T[] {
//   return data.filter((_, index) => index % 2 === 0);
// };
```

### Barrel Exports

```typescript
// index.ts - Barrel export file
export { add, subtract, multiply, divide } from "./math/operations";
export { Calculator, ScientificCalculator } from "./math/calculators";
export { PI, E, GOLDEN_RATIO } from "./math/constants";

export { User, UserService } from "./user/user-service";
export { createUser, validateUser } from "./user/user-factory";
export type { UserRole, UserPermissions } from "./user/types";

export { ApiClient } from "./api/client";
export { AuthService } from "./api/auth";
export type { ApiResponse, PaginatedResponse } from "./api/types";

// Default export
export { default as Logger } from "./utils/logger";

// Re-export with different name
export { DatabaseConnection as DB } from "./database/connection";
```

```typescript
// consumer.ts - Clean imports using barrel exports
import {
  add,
  Calculator,
  PI,
  User,
  UserService,
  ApiClient,
  Logger
} from "./lib";

// Instead of multiple import statements:
// import { add } from "./lib/math/operations";
// import { Calculator } from "./lib/math/calculators";
// import { PI } from "./lib/math/constants";
// etc...
```

### Advanced Module Patterns

```typescript
// plugin-system.ts - Plugin architecture
export interface Plugin {
  name: string;
  version: string;
  init(): void;
  destroy(): void;
}

export class PluginManager {
  private plugins = new Map<string, Plugin>();
  
  register(plugin: Plugin): void {
    this.plugins.set(plugin.name, plugin);
    plugin.init();
  }
  
  unregister(name: string): void {
    const plugin = this.plugins.get(name);
    if (plugin) {
      plugin.destroy();
      this.plugins.delete(name);
    }
  }
  
  getPlugin(name: string): Plugin | undefined {
    return this.plugins.get(name);
  }
  
  getAllPlugins(): Plugin[] {
    return Array.from(this.plugins.values());
  }
}

// plugin-auth.ts
export class AuthPlugin implements Plugin {
  name = "auth";
  version = "1.0.0";
  
  init(): void {
    console.log("Auth plugin initialized");
  }
  
  destroy(): void {
    console.log("Auth plugin destroyed");
  }
  
  authenticate(token: string): boolean {
    // Authentication logic
    return token.length > 0;
  }
}

// plugin-logging.ts
export class LoggingPlugin implements Plugin {
  name = "logging";
  version = "1.0.0";
  
  init(): void {
    console.log("Logging plugin initialized");
  }
  
  destroy(): void {
    console.log("Logging plugin destroyed");
  }
  
  log(level: string, message: string): void {
    console.log(`[${level.toUpperCase()}] ${message}`);
  }
}

// app.ts - Using the plugin system
import { PluginManager } from "./plugin-system";
import { AuthPlugin } from "./plugin-auth";
import { LoggingPlugin } from "./plugin-logging";

const pluginManager = new PluginManager();

// Register plugins
pluginManager.register(new AuthPlugin());
pluginManager.register(new LoggingPlugin());

// Use plugins
const authPlugin = pluginManager.getPlugin("auth") as AuthPlugin;
const loggingPlugin = pluginManager.getPlugin("logging") as LoggingPlugin;

if (authPlugin && loggingPlugin) {
  const isAuthenticated = authPlugin.authenticate("some-token");
  loggingPlugin.log("info", `Authentication result: ${isAuthenticated}`);
}
```

### Practice Exercises

```typescript
// Exercise 1: Modular Calculator System
// calculator/types.ts
export interface Operation {
  name: string;
  symbol: string;
  execute(a: number, b: number): number;
}

export interface CalculatorHistory {
  expression: string;
  result: number;
  timestamp: Date;
}

export type CalculatorMode = "basic" | "scientific" | "programmer";

// calculator/operations/basic.ts
import type { Operation } from "../types";

export const addOperation: Operation = {
  name: "Addition",
  symbol: "+",
  execute: (a, b) => a + b
};

export const subtractOperation: Operation = {
  name: "Subtraction", 
  symbol: "-",
  execute: (a, b) => a - b
};

export const multiplyOperation: Operation = {
  name: "Multiplication",
  symbol: "*", 
  execute: (a, b) => a * b
};

export const divideOperation: Operation = {
  name: "Division",
  symbol: "/",
  execute: (a, b) => {
    if (b === 0) throw new Error("Division by zero");
    return a / b;
  }
};

// calculator/operations/scientific.ts
import type { Operation } from "../types";

export const powerOperation: Operation = {
  name: "Power",
  symbol: "^",
  execute: (a, b) => Math.pow(a, b)
};

export const logOperation: Operation = {
  name: "Logarithm",
  symbol: "log",
  execute: (a, b) => Math.log(a) / Math.log(b)
};

export const sinOperation: Operation = {
  name: "Sine",
  symbol: "sin",
  execute: (a) => Math.sin(a), // Note: single parameter
  // Override execute signature for single parameter operations
} as Operation & { execute(a: number): number };

// calculator/calculator.ts
import type { Operation, CalculatorHistory, CalculatorMode } from "./types";

export class Calculator {
  private operations = new Map<string, Operation>();
  private history: CalculatorHistory[] = [];
  private mode: CalculatorMode = "basic";
  
  registerOperation(operation: Operation): void {
    this.operations.set(operation.symbol, operation);
  }
  
  calculate(a: number, operatorSymbol: string, b?: number): number {
    const operation = this.operations.get(operatorSymbol);
    if (!operation) {
      throw new Error(`Unknown operation: ${operatorSymbol}`);
    }
    
    const result = b !== undefined 
      ? operation.execute(a, b)
      : (operation as any).execute(a);
    
    this.addToHistory(`${a} ${operatorSymbol} ${b ?? ""}`, result);
    return result;
  }
  
  setMode(mode: CalculatorMode): void {
    this.mode = mode;
  }
  
  getMode(): CalculatorMode {
    return this.mode;
  }
  
  getHistory(): CalculatorHistory[] {
    return [...this.history];
  }
  
  clearHistory(): void {
    this.history = [];
  }
  
  private addToHistory(expression: string, result: number): void {
    this.history.push({
      expression: expression.trim(),
      result,
      timestamp: new Date()
    });
  }
}

// calculator/index.ts - Barrel export
export { Calculator } from "./calculator";
export type { Operation, CalculatorHistory, CalculatorMode } from "./types";

// Basic operations
export {
  addOperation,
