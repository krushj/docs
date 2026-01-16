# JavaScript & TypeScript Complete Guide

## Table of Contents

### JavaScript Fundamentals
- [Introduction to JavaScript](#introduction-to-javascript)
- [Variables & Data Types](#variables--data-types)
- [Type Comparison & Equality](#type-comparison--equality)
- [Functions](#functions)
- [Immediately Invoked Function Expressions (IIFEs)](#immediately-invoked-function-expressions-iifes)
- [Scope & Execution Context](#scope--execution-context)
- [Execution Context](#execution-context)
- [The this Keyword](#the-this-keyword)

### Objects & Prototypes
- [Objects](#objects)
- [Arrays](#arrays)
- [Prototypes & Inheritance](#prototypes--inheritance)

### Asynchronous JavaScript
- [Asynchronous Programming Basics](#asynchronous-programming-basics)
- [Promises](#promises)
- [Async/Await](#asyncawait)
- [Event Loop](#event-loop)

### Modern JavaScript (ES6+)
- [ES6+ Features](#es6-features)
- [Modules](#modules)
- [New Data Structures](#new-data-structures)

### DOM & Browser APIs
- [DOM Manipulation](#dom-manipulation)
- [Events](#events)
- [Browser APIs](#browser-apis)

### Advanced Concepts
- [Functional Programming](#functional-programming)
- [Error Handling](#error-handling)
- [Performance & Optimization](#performance--optimization)
- [Design Patterns](#design-patterns)

### TypeScript
- [TypeScript Basics](#typescript-basics)
- [Types & Interfaces](#types--interfaces)
- [Advanced TypeScript](#advanced-typescript)
- [TypeScript Best Practices](#typescript-best-practices)

### Interview Preparation
- [Common Interview Questions](#common-interview-questions)
- [Coding Challenges](#coding-challenges)

---

# Phase 1 — JavaScript Fundamentals

## Introduction to JavaScript

### 🎯 What is JavaScript?

**Definition:**
> JavaScript is a high-level, interpreted programming language that enables interactive web pages and is an essential part of web applications.

**Simple meaning:**
A programming language that makes websites interactive and dynamic.

**Key Features:**
- **Dynamic typing** - Variables can hold any type
- **Interpreted** - Runs without compilation
- **First-class functions** - Functions are values
- **Prototype-based OOP** - Inheritance through prototypes
- **Event-driven** - Responds to user actions
- **Single-threaded** - One thing at a time (with async capabilities)

**Real-life analogy:**
JavaScript is like a puppeteer controlling a puppet show (web page) - it makes things move, respond to audience (user) actions, and creates interactive experiences.

---

### JavaScript Engines

| Engine | Used By | Company |
|--------|---------|---------|
| **V8** | Chrome, Node.js, Edge | Google |
| **SpiderMonkey** | Firefox | Mozilla |
| **JavaScriptCore** | Safari | Apple |
| **Chakra** | Old Edge | Microsoft |

**What engines do:**
1. Parse JavaScript code
2. Compile to machine code (JIT compilation)
3. Execute the code
4. Optimize hot code paths

---

### Where JavaScript Runs

**Browser (Client-side):**
- Manipulate DOM
- Handle user events
- Make API calls
- Store data locally

**Node.js (Server-side):**
- Build APIs
- File system operations
- Database operations
- Real-time applications

---

### ECMAScript Versions

| Version | Year | Key Features |
|---------|------|--------------|
| **ES5** | 2009 | Strict mode, JSON support |
| **ES6 (ES2015)** | 2015 | let/const, arrow functions, classes, promises, modules |
| **ES2016** | 2016 | Array.includes(), ** operator |
| **ES2017** | 2017 | async/await, Object.entries() |
| **ES2018** | 2018 | Rest/spread for objects, async iteration |
| **ES2019** | 2019 | Array.flat(), Object.fromEntries() |
| **ES2020** | 2020 | Optional chaining, nullish coalescing |
| **ES2021** | 2021 | String.replaceAll(), Promise.any() |
| **ES2022** | 2022 | Top-level await, private fields |

---

## Variables & Data Types

### 🎯 Variables: var, let, const

**Definition:**
> Variables are containers for storing data values.

| Feature | var | let | const |
|---------|-----|-----|-------|
| **Scope** | Function | Block | Block |
| **Hoisting** | Yes (undefined) | Yes (TDZ) | Yes (TDZ) |
| **Reassignment** | ✅ Yes | ✅ Yes | ❌ No |
| **Redeclaration** | ✅ Yes | ❌ No | ❌ No |
| **Use in modern JS** | ❌ Avoid | ✅ Yes | ✅ Yes (default) |

**Examples:**

```javascript
// var - function scoped, hoisted
var x = 10;
var x = 20;  // Redeclaration allowed
console.log(x);  // 20

// let - block scoped
let y = 10;
y = 20;  // Reassignment allowed
// let y = 30;  // Error: Cannot redeclare

// const - block scoped, immutable binding
const z = 10;
// z = 20;  // Error: Cannot reassign
const obj = { name: "John" };
obj.name = "Jane";  // OK - object properties can change
```

**Real-life analogy:**
- `var` = Old-style locker (anyone can access)
- `let` = Modern locker (only accessible in specific area)
- `const` = Safe deposit box (can't replace, but can modify contents if it's an object)

**Interview Tip:**
> "Use const by default, let when reassignment needed, avoid var. const prevents reassignment but allows object mutation. let and const are block-scoped and have Temporal Dead Zone."

---

### Data Types

**Primitive Types (7):**
```javascript
// 1. String
let name = "John";
let greeting = 'Hello';
let template = `Hi ${name}`;

// 2. Number (integer and float)
let age = 25;
let price = 99.99;
let infinity = Infinity;
let notANumber = NaN;

// 3. Boolean
let isActive = true;
let isDeleted = false;

// 4. Undefined (declared but not assigned)
let x;
console.log(x);  // undefined

// 5. Null (intentional absence of value)
let user = null;

// 6. Symbol (unique identifier)
let id = Symbol('id');

// 7. BigInt (large integers)
let bigNumber = 1234567890123456789012345678901234567890n;
```

**Reference Types:**
```javascript
// Object
let person = { name: "John", age: 30 };

// Array
let numbers = [1, 2, 3, 4, 5];

// Function
function greet() { return "Hello"; }
```

---

### null vs undefined

| Feature | null | undefined |
|---------|------|-----------|
| **Meaning** | Intentional absence | Not yet assigned |
| **Type** | object (bug in JS) | undefined |
| **Assignment** | Explicitly set | Default value |
| **Use case** | "No value" | "Not initialized" |

```javascript
let a;              // undefined (not assigned)
let b = null;       // null (explicitly no value)

console.log(typeof a);  // "undefined"
console.log(typeof b);  // "object" (historical bug)

console.log(a == b);    // true (loose equality)
console.log(a === b);   // false (strict equality)
```

**Real-life analogy:**
- `undefined` = Empty box (nothing put in yet)
- `null` = Box with "EMPTY" label (intentionally marked as empty)

---

## Type Comparison & Equality

### == vs ===

**Definition:**
> `==` performs type coercion, `===` checks type and value without coercion.

| Operator | Name | Coercion | Recommended |
|----------|------|----------|-------------|
| `==` | Loose equality | ✅ Yes | ❌ Avoid |
| `===` | Strict equality | ❌ No | ✅ Use this |

**Examples:**

```javascript
// == (loose equality) - performs type coercion
console.log(5 == "5");       // true (string converted to number)
console.log(null == undefined);  // true
console.log(0 == false);     // true
console.log("" == false);    // true

// === (strict equality) - no type coercion
console.log(5 === "5");      // false (different types)
console.log(null === undefined);  // false
console.log(0 === false);    // false
console.log("" === false);   // false
```

**Interview Tip:**
> "Always use === (strict equality) to avoid unexpected type coercion. == converts types before comparing, which can lead to bugs. Example: 0 == false is true, but 0 === false is false."

---

### Truthy and Falsy Values

**Falsy values (8 total):**
```javascript
false
0
-0
0n (BigInt zero)
"" (empty string)
null
undefined
NaN
```

**Everything else is truthy!**

```javascript
// Truthy examples
if ("hello") { }      // true
if (42) { }           // true
if ([]) { }           // true (empty array is truthy!)
if ({}) { }           // true (empty object is truthy!)

// Falsy examples
if (0) { }            // false
if ("") { }           // false
if (null) { }         // false
```

---

## Functions

### 🎯 Function Types

**Function Declaration:**
```javascript
// Hoisted - can call before declaration
function greet(name) {
    return `Hello, ${name}!`;
}

console.log(greet("John"));  // Hello, John!
```

**Function Expression:**
```javascript
// Not hoisted - must declare before use
const greet = function(name) {
    return `Hello, ${name}!`;
};

console.log(greet("Jane"));  // Hello, Jane!
```

**Arrow Function:**
```javascript
// Concise syntax, lexical 'this'
const greet = (name) => `Hello, ${name}!`;

// Multiple parameters
const add = (a, b) => a + b;

// Multiple statements
const calculate = (a, b) => {
    const sum = a + b;
    return sum * 2;
};

console.log(greet("Bob"));     // Hello, Bob!
console.log(add(5, 3));        // 8
console.log(calculate(5, 3));  // 16
```

---

### Arrow Functions vs Regular Functions

| Feature | Regular Function | Arrow Function |
|---------|------------------|----------------|
| **this binding** | Dynamic (depends on caller) | Lexical (from enclosing scope) |
| **arguments object** | ✅ Yes | ❌ No |
| **Can be constructor** | ✅ Yes (new keyword) | ❌ No |
| **Syntax** | Verbose | Concise |
| **Use case** | Methods, constructors | Callbacks, array methods |

**When NOT to use arrow functions:**
```javascript
// ❌ Bad: Object methods
const person = {
    name: "John",
    greet: () => {
        console.log(`Hello, ${this.name}`);  // 'this' is undefined!
    }
};

// ✅ Good: Regular function
const person = {
    name: "John",
    greet() {
        console.log(`Hello, ${this.name}`);  // Works!
    }
};
```

**Real-life analogy:**
Arrow functions are like a child who always remembers their home (lexical this), while regular functions are like actors who play different roles (dynamic this) depending on the scene.

---

### Callback Functions

**Definition:**
> A callback is a function passed as an argument to another function, to be executed later.

**Example:**

```javascript
// Simple callback
function processData(data, callback) {
    console.log("Processing:", data);
    callback(data);
}

processData("user123", (result) => {
    console.log("Callback executed with:", result);
});

// Real-world example: Array methods
const numbers = [1, 2, 3, 4, 5];

numbers.forEach((num) => {
    console.log(num * 2);
});

const doubled = numbers.map((num) => num * 2);
console.log(doubled);  // [2, 4, 6, 8, 10]
```

**Callback Hell:**
```javascript
// ❌ Bad: Nested callbacks (pyramid of doom)
getData(function(a) {
    getMoreData(a, function(b) {
        getMoreData(b, function(c) {
            getMoreData(c, function(d) {
                console.log(d);
            });
        });
    });
});

// ✅ Good: Use Promises or async/await
```

---

### Higher-Order Functions

**Definition:**
> Functions that take other functions as arguments or return functions.

**Examples:**

```javascript
// Function that takes function as argument
function repeat(n, action) {
    for (let i = 0; i < n; i++) {
        action(i);
    }
}

repeat(3, (i) => console.log(`Iteration ${i}`));

// Function that returns function
function multiplier(factor) {
    return (number) => number * factor;
}

const double = multiplier(2);
const triple = multiplier(3);

console.log(double(5));  // 10
console.log(triple(5));  // 15

// Common higher-order functions
const numbers = [1, 2, 3, 4, 5];

// map - transform each element
const doubled = numbers.map(n => n * 2);

// filter - keep elements that pass test
const evens = numbers.filter(n => n % 2 === 0);

// reduce - reduce to single value
const sum = numbers.reduce((acc, n) => acc + n, 0);

console.log(doubled);  // [2, 4, 6, 8, 10]
console.log(evens);    // [2, 4]
console.log(sum);      // 15
```

**Interview Tip:**
> "Higher-order functions take functions as arguments or return functions. Examples: map, filter, reduce. They enable functional programming and code reusability."

---

## Immediately Invoked Function Expressions (IIFEs)

### 🎯 What is an IIFE?

**Definition:**
> An IIFE (Immediately Invoked Function Expression) is a function that runs as soon as it is defined. It creates a private scope and executes immediately without being called explicitly.

**Syntax:**
```javascript
// Standard IIFE syntax
(function() {
    console.log("I run immediately!");
})();

// Arrow function IIFE
(() => {
    console.log("Arrow IIFE!");
})();

// IIFE with parameters
(function(name) {
    console.log(`Hello, ${name}!`);
})("John");

// Named IIFE (useful for debugging/recursion)
(function myIIFE() {
    console.log("Named IIFE executed!");
})();
```

---

### Why Use IIFEs?

**1. Avoid Global Namespace Pollution:**
```javascript
// ❌ Bad: Pollutes global scope
var counter = 0;
function increment() {
    counter++;
}

// ✅ Good: IIFE keeps variables private
const counterModule = (function() {
    let counter = 0;  // Private variable
    
    return {
        increment: function() {
            counter++;
        },
        getCount: function() {
            return counter;
        }
    };
})();

counterModule.increment();
counterModule.increment();
console.log(counterModule.getCount());  // 2
console.log(counter);  // ReferenceError: counter is not defined
```

**2. Create Private Variables (Module Pattern):**
```javascript
const bankAccount = (function() {
    let balance = 1000;  // Private
    
    return {
        deposit: function(amount) {
            balance += amount;
            return `Deposited: $${amount}. New balance: $${balance}`;
        },
        withdraw: function(amount) {
            if (amount > balance) {
                return "Insufficient funds!";
            }
            balance -= amount;
            return `Withdrew: $${amount}. New balance: $${balance}`;
        },
        getBalance: function() {
            return `Current balance: $${balance}`;
        }
    };
})();

console.log(bankAccount.deposit(500));    // Deposited: $500. New balance: $1500
console.log(bankAccount.withdraw(200));   // Withdrew: $200. New balance: $1300
console.log(bankAccount.getBalance());    // Current balance: $1300
console.log(bankAccount.balance);         // undefined (private!)
```

**3. Avoid Variable Hoisting Issues:**
```javascript
// ❌ Problem: Classic loop closure issue
for (var i = 0; i < 3; i++) {
    setTimeout(function() {
        console.log(i);  // Prints: 3, 3, 3
    }, 100);
}

// ✅ Solution: IIFE creates new scope for each iteration
for (var i = 0; i < 3; i++) {
    (function(j) {
        setTimeout(function() {
            console.log(j);  // Prints: 0, 1, 2
        }, 100);
    })(i);
}

// ✅ Modern solution: Use let (block-scoped)
for (let i = 0; i < 3; i++) {
    setTimeout(function() {
        console.log(i);  // Prints: 0, 1, 2
    }, 100);
}
```

**4. One-time Initialization:**
```javascript
const config = (function() {
    // Complex initialization logic runs once
    const apiKey = "secret-key-123";
    const baseUrl = "https://api.example.com";
    const timeout = 5000;
    
    return Object.freeze({
        apiKey,
        baseUrl,
        timeout
    });
})();

console.log(config.baseUrl);  // https://api.example.com
config.apiKey = "hacked";     // Silently fails (frozen)
console.log(config.apiKey);   // secret-key-123
```

### IIFE vs Modern Alternatives

| Feature | IIFE | ES6 Modules | Block Scope (let/const) |
|---------|------|-------------|------------------------|
| **Private variables** | ✅ Yes | ✅ Yes | ✅ Yes (within block) |
| **Immediate execution** | ✅ Yes | ❌ No | ✅ Yes |
| **Browser support** | ✅ All browsers | Requires bundler/modern browser | Modern browsers |
| **Use case** | Legacy code, quick encapsulation | Large applications | Simple scoping |

**When to use IIFEs today:**
- Working with legacy codebases
- Quick script encapsulation without module bundlers
- Creating singletons or module patterns
- Avoiding async/await at top level in older environments

**Interview Tip:**
> "An IIFE is a function that executes immediately after creation. It's used to create private scope, avoid global namespace pollution, and implement the module pattern. While ES6 modules have largely replaced IIFEs, they're still useful for quick encapsulation and legacy code."

---

## Scope & Execution Context

## Execution Context

### 🎯 What is Execution Context?

**Definition:**
> Execution Context is the environment in which JavaScript code is evaluated and executed. It contains information about the code being run, including variables, functions, scope chain, and the value of `this`.

**Simple meaning:**
Think of Execution Context as a "container" that holds all the information needed to run a piece of code.

---

### Types of Execution Context

**1. Global Execution Context (GEC):**
- Created when the script first runs
- Only ONE global context per program
- Creates the global object (`window` in browser, `global` in Node.js)
- Sets `this` to the global object

```javascript
// Global Execution Context
var globalVar = "I'm global";
let globalLet = "Also global";

console.log(this);  // Window (browser) or global (Node.js)
console.log(window.globalVar);  // "I'm global" (var attaches to global object)
console.log(window.globalLet);  // undefined (let/const don't attach)
```

**2. Function Execution Context (FEC):**
- Created each time a function is invoked
- Each function call gets its own execution context
- Multiple function contexts can exist at the same time

```javascript
function greet(name) {
    // New Function Execution Context created here
    var greeting = "Hello";
    return `${greeting}, ${name}!`;
}

greet("John");  // Creates FEC #1
greet("Jane");  // Creates FEC #2 (FEC #1 is gone by now)
```

**3. Eval Execution Context:**
- Created when code runs inside `eval()` function
- Rarely used and generally avoided for security reasons

---

### Execution Context Phases

Every Execution Context goes through **two phases**:

#### Phase 1: Creation Phase (Memory Allocation)

During this phase, JavaScript:
1. Creates the Variable Object (VO) / Lexical Environment
2. Creates the Scope Chain
3. Determines the value of `this`

```javascript
function example() {
    console.log(a);  // undefined (hoisted)
    console.log(b);  // ReferenceError (TDZ)
    console.log(c);  // ReferenceError (TDZ)
    console.log(greet);  // [Function: greet]
    
    var a = 10;
    let b = 20;
    const c = 30;
    
    function greet() {
        return "Hello";
    }
}

// During Creation Phase, memory looks like:
// {
//   a: undefined,           // var - hoisted with undefined
//   b: <uninitialized>,     // let - in TDZ
//   c: <uninitialized>,     // const - in TDZ
//   greet: function() {...} // function - fully hoisted
// }
```

#### Phase 2: Execution Phase (Code Execution)

During this phase, JavaScript:
1. Executes code line by line
2. Assigns actual values to variables
3. Executes function calls

```javascript
function example() {
    var a = 10;
    let b = 20;
    const c = 30;
    
    console.log(a);  // 10
    console.log(b);  // 20
    console.log(c);  // 30
}

// During Execution Phase, memory looks like:
// {
//   a: 10,
//   b: 20,
//   c: 30,
//   greet: function() {...}
// }
```

---

### Components of Execution Context

Each Execution Context has three main components:

```
┌─────────────────────────────────────────────┐
│           EXECUTION CONTEXT                 │
├─────────────────────────────────────────────┤
│  1. Variable Environment                    │
│     - var declarations                      │
│     - function declarations                 │
│     - arguments object                      │
├─────────────────────────────────────────────┤
│  2. Lexical Environment                     │
│     - let and const declarations            │
│     - Reference to outer environment        │
│     - Block scoped variables                │
├─────────────────────────────────────────────┤
│  3. This Binding                            │
│     - Value of 'this' keyword               │
│     - Depends on how function is called     │
└─────────────────────────────────────────────┘
```

**Example demonstrating all components:**

```javascript
var globalVar = "global";

function outer(param) {
    var outerVar = "outer";
    let outerLet = "outer let";
    
    function inner() {
        var innerVar = "inner";
        console.log(globalVar);  // "global" - from global scope
        console.log(outerVar);   // "outer" - from outer scope (closure)
        console.log(outerLet);   // "outer let" - from outer lexical env
        console.log(param);      // "argument" - from outer scope
        console.log(innerVar);   // "inner" - from current scope
        console.log(this);       // depends on how inner() is called
    }
    
    inner();
}

outer("argument");
```

---

### Call Stack (Execution Stack)

**Definition:**
> The Call Stack is a LIFO (Last In, First Out) data structure that keeps track of execution contexts.

**How it works:**

```javascript
function first() {
    console.log("First function");
    second();
    console.log("First function end");
}

function second() {
    console.log("Second function");
    third();
    console.log("Second function end");
}

function third() {
    console.log("Third function");
}

first();

// Output:
// First function
// Second function
// Third function
// Second function end
// First function end
```

**Visual representation of Call Stack:**

```
Step 1: Script starts
┌─────────────────┐
│ Global Context  │  ← Current
└─────────────────┘

Step 2: first() called
┌─────────────────┐
│ first() Context │  ← Current
├─────────────────┤
│ Global Context  │
└─────────────────┘

Step 3: second() called from first()
┌─────────────────┐
│ second() Context│  ← Current
├─────────────────┤
│ first() Context │
├─────────────────┤
│ Global Context  │
└─────────────────┘

Step 4: third() called from second()
┌─────────────────┐
│ third() Context │  ← Current
├─────────────────┤
│ second() Context│
├─────────────────┤
│ first() Context │
├─────────────────┤
│ Global Context  │
└─────────────────┘

Step 5: third() completes - popped off
┌─────────────────┐
│ second() Context│  ← Current
├─────────────────┤
│ first() Context │
├─────────────────┤
│ Global Context  │
└─────────────────┘

... and so on until stack is empty
```

---

### Stack Overflow

**What causes it:**
When the call stack exceeds its maximum size (usually due to infinite recursion).

```javascript
// ❌ Causes Stack Overflow
function infiniteLoop() {
    infiniteLoop();  // Calls itself forever
}

infiniteLoop();  // RangeError: Maximum call stack size exceeded

// ✅ Proper recursion with base case
function countdown(n) {
    if (n <= 0) {
        console.log("Done!");
        return;  // Base case - stops recursion
    }
    console.log(n);
    countdown(n - 1);
}

countdown(5);  // 5, 4, 3, 2, 1, Done!
```

---

### Execution Context in Action - Complete Example

```javascript
var name = "Global";

function outer() {
    var name = "Outer";
    
    function inner() {
        var name = "Inner";
        console.log(name);  // "Inner"
    }
    
    inner();
    console.log(name);  // "Outer"
}

outer();
console.log(name);  // "Global"

// Execution Flow:
// 1. Global EC created → name = "Global"
// 2. outer() called → Outer EC pushed → name = "Outer"
// 3. inner() called → Inner EC pushed → name = "Inner"
// 4. console.log(name) in inner → "Inner" (looks in Inner EC)
// 5. inner() completes → Inner EC popped
// 6. console.log(name) in outer → "Outer" (looks in Outer EC)
// 7. outer() completes → Outer EC popped
// 8. console.log(name) global → "Global" (looks in Global EC)
```

---

### Execution Context vs Scope

| Aspect | Execution Context | Scope |
|--------|------------------|-------|
| **What it is** | Runtime environment | Accessibility of variables |
| **When created** | When code executes | When code is written (lexical) |
| **Contains** | Variables, this, scope chain | Variable bindings |
| **Lifetime** | Until function completes | Until variables go out of scope |
| **Dynamic/Static** | Dynamic (created at runtime) | Static (determined at write time) |

**Interview Tip:**
> "Execution Context is the environment where JavaScript code runs. It has three components: Variable Environment (var, functions), Lexical Environment (let, const, outer reference), and This Binding. Each function call creates a new execution context pushed onto the Call Stack. The stack follows LIFO - last function called is first to complete."

---

### 🎯 Hoisting

**Definition:**
> Hoisting is JavaScript's behavior of moving declarations to the top of their scope before code execution.

**How it works:**

```javascript
// Variable hoisting
console.log(x);  // undefined (not ReferenceError)
var x = 5;

// Equivalent to:
var x;
console.log(x);  // undefined
x = 5;

// let and const - Temporal Dead Zone (TDZ)
console.log(y);  // ReferenceError: Cannot access before initialization
let y = 10;

// Function hoisting
greet();  // Works! "Hello"
function greet() {
    console.log("Hello");
}

// Function expression - NOT hoisted
sayHi();  // ReferenceError
const sayHi = function() {
    console.log("Hi");
};
```

**Interview Tip:**
> "Hoisting moves declarations to top. var is hoisted with undefined, let/const are hoisted but in TDZ (cannot access before declaration). Function declarations are fully hoisted, function expressions are not."

---

### Closures

**Definition:**
> A closure is a function that has access to variables in its outer (enclosing) scope, even after the outer function has returned.

**Simple meaning:**
Inner function remembers variables from outer function.

**Example:**

```javascript
function outer() {
    let count = 0;  // Private variable
    
    return function inner() {
        count++;
        console.log(count);
    };
}

const counter = outer();
counter();  // 1
counter();  // 2
counter();  // 3
// 'count' is preserved in closure!
```

**Practical uses:**

```javascript
// 1. Data privacy
function createBankAccount(initialBalance) {
    let balance = initialBalance;  // Private
    
    return {
        deposit: (amount) => {
            balance += amount;
            return balance;
        },
        withdraw: (amount) => {
            if (balance >= amount) {
                balance -= amount;
                return balance;
            }
            return "Insufficient funds";
        },
        getBalance: () => balance
    };
}

const account = createBankAccount(1000);
console.log(account.getBalance());  // 1000
account.deposit(500);
console.log(account.getBalance());  // 1500
// Cannot access 'balance' directly - it's private!

// 2. Function factory
function makeMultiplier(x) {
    return function(y) {
        return x * y;
    };
}

const double = makeMultiplier(2);
const triple = makeMultiplier(3);

console.log(double(5));  // 10
console.log(triple(5));  // 15
```

**Real-life analogy:**
Closure is like a backpack - a function carries variables from its birthplace wherever it goes, even after leaving home.

**Interview Tip:**
> "Closure is when inner function accesses outer function's variables even after outer function returns. Used for data privacy, function factories, and callbacks. Example: counter that remembers count value."

---

## The this Keyword

### 🎯 Understanding 'this'

**Definition:**
> 'this' refers to the object that is executing the current function.

**Simple meaning:**
'this' depends on HOW the function is called, not WHERE it's defined.

---

### 'this' in Different Contexts

**1. Global context:**
```javascript
console.log(this);  // Window (browser) or global (Node.js)
```

**2. Object method:**
```javascript
const person = {
    name: "John",
    greet() {
        console.log(`Hello, I'm ${this.name}`);
    }
};

person.greet();  // "Hello, I'm John" - 'this' is person
```

**3. Regular function:**
```javascript
function show() {
    console.log(this);
}

show();  // Window (non-strict) or undefined (strict mode)
```

**4. Arrow function:**
```javascript
const person = {
    name: "John",
    greet: () => {
        console.log(this.name);  // undefined - arrow function has no 'this'
    }
};

person.greet();  // undefined (lexical 'this' from outer scope)
```

**5. Constructor:**
```javascript
function Person(name) {
    this.name = name;
}

const john = new Person("John");
console.log(john.name);  // "John" - 'this' is new object
```

---

### call, apply, bind

**Definition:**
> Methods to explicitly set 'this' value for a function.

| Method | Syntax | Executes | Use Case |
|--------|--------|----------|----------|
| **call** | `func.call(thisArg, arg1, arg2)` | Immediately | Known arguments |
| **apply** | `func.apply(thisArg, [args])` | Immediately | Array of arguments |
| **bind** | `func.bind(thisArg, arg1)` | Returns new function | Event handlers |

**Examples:**

```javascript
const person = {
    name: "John",
    greet(greeting, punctuation) {
        console.log(`${greeting}, I'm ${this.name}${punctuation}`);
    }
};

const anotherPerson = { name: "Jane" };

// call - arguments separately
person.greet.call(anotherPerson, "Hi", "!");
// "Hi, I'm Jane!"

// apply - arguments as array
person.greet.apply(anotherPerson, ["Hello", "."]);
// "Hello, I'm Jane."

// bind - returns new function
const greetJane = person.greet.bind(anotherPerson, "Hey");
greetJane("!!");  // "Hey, I'm Jane!!"
```

**Real-life analogy:**
- `call` = Calling someone on phone with specific message
- `apply` = Sending email with list of points
- `bind` = Creating a pre-addressed envelope (use later)

**Interview Tip:**
> "call and apply invoke function immediately with specified 'this'. call takes arguments separately, apply takes array. bind returns new function with bound 'this', useful for event handlers."

---

# Phase 3 — Asynchronous JavaScript

## Asynchronous Programming Basics

### 🎯 Synchronous vs Asynchronous

**Synchronous:**
```javascript
console.log("1");
console.log("2");
console.log("3");
// Output: 1, 2, 3 (in order)
```

**Asynchronous:**
```javascript
console.log("1");
setTimeout(() => console.log("2"), 0);
console.log("3");
// Output: 1, 3, 2 (async operation deferred)
```

**Real-life analogy:**
- **Synchronous** = Standing in line at bank (wait for each person)
- **Asynchronous** = Restaurant buzzer (order food, do other things, buzzer notifies when ready)

---

## Event Loop

### 🎯 How JavaScript Handles Async

**Definition:**
> Event loop is the mechanism that allows JavaScript to perform non-blocking operations despite being single-threaded.

**Components:**
1. **Call Stack** - Where code executes
2. **Web APIs** - Browser-provided (setTimeout, fetch, DOM events)
3. **Task Queue (Macrotask)** - Callbacks from setTimeout, setInterval
4. **Microtask Queue** - Promises, queueMicrotask
5. **Event Loop** - Moves tasks from queues to call stack

**Execution Order:**
```
1. Execute all synchronous code (call stack)
2. Execute all microtasks (Promise callbacks)
3. Execute one macrotask (setTimeout callback)
4. Repeat
```

**Example:**

```javascript
console.log("1");  // Synchronous

setTimeout(() => console.log("2"), 0);  // Macrotask

Promise.resolve().then(() => console.log("3"));  // Microtask

console.log("4");  // Synchronous

// Output: 1, 4, 3, 2
// Explanation:
// 1, 4 - synchronous (call stack)
// 3 - microtask (Promise)
// 2 - macrotask (setTimeout)
```

**Real-life analogy:**
Event loop is like a restaurant manager - handles orders (call stack), checks for urgent requests (microtasks), then handles regular orders (macrotasks), repeating continuously.

**Interview Tip:**
> "Event loop enables async in single-threaded JavaScript. Execution order: synchronous code → microtasks (Promises) → macrotasks (setTimeout). This is why Promise.then() executes before setTimeout even with 0 delay."

---

## Promises

### 🎯 What is a Promise?

**Definition:**
> A Promise is an object representing the eventual completion or failure of an asynchronous operation.

**Simple meaning:**
A promise is like an IOU - it promises to give you a result later (success or failure).

**Promise States:**
1. **Pending** - Initial state, not fulfilled or rejected
2. **Fulfilled** - Operation completed successfully
3. **Rejected** - Operation failed

**Creating Promises:**

```javascript
const promise = new Promise((resolve, reject) => {
    // Async operation
    setTimeout(() => {
        const success = true;
        
        if (success) {
            resolve("Operation successful!");
        } else {
            reject("Operation failed!");
        }
    }, 1000);
});

// Consuming promise
promise
    .then((result) => {
        console.log(result);  // "Operation successful!"
    })
    .catch((error) => {
        console.error(error);
    })
    .finally(() => {
        console.log("Promise settled (fulfilled or rejected)");
    });
```

---

### Promise Methods

**Promise.all() - Wait for all**
```javascript
const promise1 = Promise.resolve(1);
const promise2 = Promise.resolve(2);
const promise3 = Promise.resolve(3);

Promise.all([promise1, promise2, promise3])
    .then((results) => {
        console.log(results);  // [1, 2, 3]
    });

// If any fails, entire Promise.all fails
```

**Promise.race() - First to finish**
```javascript
const slow = new Promise(resolve => setTimeout(() => resolve("slow"), 2000));
const fast = new Promise(resolve => setTimeout(() => resolve("fast"), 100));

Promise.race([slow, fast])
    .then((result) => {
        console.log(result);  // "fast"
    });
```

**Promise.allSettled() - Wait for all (success or failure)**
```javascript
const promises = [
    Promise.resolve(1),
    Promise.reject("error"),
    Promise.resolve(3)
];

Promise.allSettled(promises)
    .then((results) => {
        console.log(results);
        // [
        //   { status: 'fulfilled', value: 1 },
        //   { status: 'rejected', reason: 'error' },
        //   { status: 'fulfilled', value: 3 }
        // ]
    });
```

**Promise.any() - First to succeed**
```javascript
const promises = [
    Promise.reject("error 1"),
    Promise.resolve("success"),
    Promise.reject("error 2")
];

Promise.any(promises)
    .then((result) => {
        console.log(result);  // "success"
    });
```

---

## Async/Await

### 🎯 Modern Async Syntax

**Definition:**
> async/await is syntactic sugar over Promises, making asynchronous code look synchronous.

**Simple meaning:**
Write async code that looks like normal code.

**async Function:**
```javascript
// async function always returns a Promise
async function fetchData() {
    return "data";
}

fetchData().then(data => console.log(data));  // "data"
```

**await Keyword:**
```javascript
async function getData() {
    // await pauses execution until Promise resolves
    const result = await fetch('https://api.example.com/data');
    const data = await result.json();
    return data;
}
```

**Error Handling:**

```javascript
async function fetchUser(id) {
    try {
        const response = await fetch(`/api/users/${id}`);
        
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }
        
        const user = await response.json();
        return user;
    } catch (error) {
        console.error("Error fetching user:", error);
        throw error;  // Re-throw or handle
    }
}
```

---

### Sequential vs Parallel Execution

**Sequential (one after another):**
```javascript
async function sequential() {
    const user = await fetchUser(1);      // Wait 1s
    const posts = await fetchPosts(1);    // Wait 1s
    const comments = await fetchComments(1);  // Wait 1s
    // Total: 3 seconds
}
```

**Parallel (all at once):**
```javascript
async function parallel() {
    const [user, posts, comments] = await Promise.all([
        fetchUser(1),
        fetchPosts(1),
        fetchComments(1)
    ]);
    // Total: 1 second (all run simultaneously)
}
```

**Real-life analogy:**
- **Sequential** = Washing dishes one by one
- **Parallel** = Multiple people washing dishes simultaneously

**Interview Tip:**
> "async/await makes async code readable. async function returns Promise, await pauses execution until Promise resolves. Use try/catch for errors. For parallel operations, use Promise.all() instead of multiple awaits."

---

# Phase 4 — Modern JavaScript (ES6+)

## ES6+ Features

### Destructuring

**Array Destructuring:**
```javascript
const numbers = [1, 2, 3, 4, 5];

// Extract values
const [first, second] = numbers;
console.log(first, second);  // 1, 2

// Skip elements
const [a, , c] = numbers;
console.log(a, c);  // 1, 3

// Rest operator
const [head, ...tail] = numbers;
console.log(head);  // 1
console.log(tail);  // [2, 3, 4, 5]

// Default values
const [x, y, z = 0] = [1, 2];
console.log(z);  // 0
```

**Object Destructuring:**
```javascript
const person = {
    name: "John",
    age: 30,
    city: "New York"
};

// Extract properties
const { name, age } = person;
console.log(name, age);  // John, 30

// Rename variables
const { name: fullName, age: years } = person;
console.log(fullName, years);  // John, 30

// Default values
const { name, country = "USA" } = person;
console.log(country);  // USA

// Nested destructuring
const user = {
    id: 1,
    profile: {
        name: "Alice",
        email: "alice@example.com"
    }
};

const { profile: { name, email } } = user;
console.log(name, email);  // Alice, alice@example.com
```

---

### Spread Operator

**Definition:**
> Spread operator (...) expands an iterable into individual elements.

**Array spreading:**
```javascript
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];

// Combine arrays
const combined = [...arr1, ...arr2];
console.log(combined);  // [1, 2, 3, 4, 5, 6]

// Copy array
const copy = [...arr1];

// Add elements
const extended = [0, ...arr1, 4];
console.log(extended);  // [0, 1, 2, 3, 4]
```

**Object spreading:**
```javascript
const person = { name: "John", age: 30 };
const address = { city: "New York", country: "USA" };

// Combine objects
const user = { ...person, ...address };
console.log(user);
// { name: "John", age: 30, city: "New York", country: "USA" }

// Copy object
const copy = { ...person };

// Override properties
const updated = { ...person, age: 31 };
console.log(updated);  // { name: "John", age: 31 }
```

---

### Optional Chaining (?.)

**Definition:**
> Safely access nested properties without checking each level for null/undefined.

```javascript
const user = {
    name: "John",
    address: {
        city: "New York"
    }
};

// ❌ Without optional chaining
console.log(user.address.city);  // "New York"
console.log(user.profile.bio);   // Error: Cannot read property 'bio' of undefined

// ✅ With optional chaining
console.log(user.address?.city);      // "New York"
console.log(user.profile?.bio);       // undefined (no error!)
console.log(user.profile?.bio?.length);  // undefined

// With functions
user.greet?.();  // Only calls if greet exists

// With arrays
const firstUser = users?.[0];
```

---

### Nullish Coalescing (??)

**Definition:**
> Returns right operand when left is null or undefined (not other falsy values).

```javascript
// ?? vs ||
const value1 = 0 || 10;        // 10 (0 is falsy)
const value2 = 0 ?? 10;        // 0 (0 is not null/undefined)

const value3 = "" || "default";   // "default" (empty string is falsy)
const value4 = "" ?? "default";   // "" (empty string is not null/undefined)

const value5 = null ?? "default";      // "default"
const value6 = undefined ?? "default"; // "default"

// Practical use
function getUserName(user) {
    return user.name ?? "Guest";  // Only use "Guest" if name is null/undefined
}
```

**Interview Tip:**
> "?? returns right side only if left is null/undefined. || returns right side for any falsy value. Use ?? when 0, false, or empty string are valid values."

---

## Modules

### 🎯 ES6 Modules

**Definition:**
> Modules are reusable pieces of code that can be exported and imported.

**Named Exports:**
```javascript
// math.js
export const PI = 3.14159;

export function add(a, b) {
    return a + b;
}

export function subtract(a, b) {
    return a - b;
}

// Import
import { PI, add, subtract } from './math.js';
console.log(add(5, 3));  // 8
```

**Default Export:**
```javascript
// calculator.js
export default class Calculator {
    add(a, b) {
        return a + b;
    }
}

// Import (can use any name)
import Calculator from './calculator.js';
import Calc from './calculator.js';  // Also works
```

**Mixed Exports:**
```javascript
// utils.js
export const version = "1.0";
export function helper() { }
export default class Utils { }

// Import
import Utils, { version, helper } from './utils.js';
```

**Interview Tip:**
> "Named exports use curly braces, can have multiple per file. Default export doesn't use braces, one per file. Use named for utilities, default for main class/function."

---

# TypeScript

## TypeScript Basics

### 🎯 What is TypeScript?

**Definition:**
> TypeScript is a typed superset of JavaScript that compiles to plain JavaScript.

**Simple meaning:**
JavaScript + Type System = TypeScript

**Why TypeScript:**
- ✅ Catch errors at compile time
- ✅ Better IDE support (autocomplete, refactoring)
- ✅ Self-documenting code
- ✅ Easier refactoring
- ✅ Better for large projects

**Real-life analogy:**
TypeScript is like a spell-checker for code - catches mistakes before you publish (compile), while JavaScript only shows errors when readers (users) encounter them.

---

### Basic Types

```typescript
// Primitive types
let name: string = "John";
let age: number = 30;
let isActive: boolean = true;
let nothing: null = null;
let notDefined: undefined = undefined;

// Array types
let numbers: number[] = [1, 2, 3];
let names: Array<string> = ["Alice", "Bob"];

// Tuple (fixed-length array with specific types)
let person: [string, number] = ["John", 30];

// Any (avoid when possible)
let anything: any = "could be anything";

// Unknown (type-safe any)
let uncertain: unknown = "something";
// uncertain.toUpperCase();  // Error: must check type first
if (typeof uncertain === "string") {
    uncertain.toUpperCase();  // OK
}

// Void (function returns nothing)
function log(message: string): void {
    console.log(message);
}

// Never (function never returns)
function throwError(message: string): never {
    throw new Error(message);
}
```

---

## Types & Interfaces

### Interfaces

**Definition:**
> Interfaces define the structure of an object (shape of data).

```typescript
interface User {
    id: number;
    name: string;
    email: string;
    age?: number;  // Optional property
    readonly createdAt: Date;  // Read-only
}

const user: User = {
    id: 1,
    name: "John",
    email: "john@example.com",
    createdAt: new Date()
};

// user.createdAt = new Date();  // Error: readonly
```

**Interface vs Type:**

```typescript
// Interface (preferred for objects)
interface Person {
    name: string;
    age: number;
}

// Type alias (more flexible)
type Person = {
    name: string;
    age: number;
};

// Type can do unions
type ID = string | number;

// Type can do primitives
type Name = string;

// Interface can extend
interface Employee extends Person {
    employeeId: number;
}
```

| Feature | Interface | Type |
|---------|-----------|------|
| **Extend** | ✅ Yes (extends) | ✅ Yes (&) |
| **Union types** | ❌ No | ✅ Yes |
| **Primitives** | ❌ No | ✅ Yes |
| **Declaration merging** | ✅ Yes | ❌ No |
| **Use case** | Object shapes | Unions, primitives, complex types |

---

### Generics

**Definition:**
> Generics allow you to write reusable code that works with multiple types.

```typescript
// Generic function
function identity<T>(arg: T): T {
    return arg;
}

const num = identity<number>(42);
const str = identity<string>("hello");

// Generic interface
interface Box<T> {
    value: T;
}

const numberBox: Box<number> = { value: 42 };
const stringBox: Box<string> = { value: "hello" };

// Generic class
class DataStore<T> {
    private data: T[] = [];
    
    add(item: T): void {
        this.data.push(item);
    }
    
    get(index: number): T {
        return this.data[index];
    }
}

const numberStore = new DataStore<number>();
numberStore.add(1);
numberStore.add(2);

const stringStore = new DataStore<string>();
stringStore.add("hello");
stringStore.add("world");
```

**Real-life analogy:**
Generics are like a universal remote - same remote (function) works with different devices (types) - TV, AC, sound system.

---

### Union Types

```typescript
// Variable can be multiple types
let id: string | number;
id = "abc123";  // OK
id = 123;       // OK
// id = true;   // Error

// Function with union type
function printId(id: string | number) {
    if (typeof id === "string") {
        console.log(id.toUpperCase());
    } else {
        console.log(id.toFixed(2));
    }
}
```

---

### Type Assertions

```typescript
// Tell TypeScript "trust me, I know the type"
let someValue: unknown = "this is a string";

let strLength1 = (someValue as string).length;
let strLength2 = (<string>someValue).length;  // Alternative syntax
```

---

## Advanced TypeScript

### Utility Types

```typescript
interface User {
    id: number;
    name: string;
    email: string;
    age: number;
}

// Partial - all properties optional
type PartialUser = Partial<User>;
const user1: PartialUser = { name: "John" };  // OK

// Required - all properties required
type RequiredUser = Required<User>;

// Readonly - all properties readonly
type ReadonlyUser = Readonly<User>;

// Pick - select specific properties
type UserPreview = Pick<User, 'id' | 'name'>;
const preview: UserPreview = { id: 1, name: "John" };

// Omit - exclude specific properties
type UserWithoutEmail = Omit<User, 'email'>;

// Record - create object type with specific keys
type Roles = 'admin' | 'user' | 'guest';
type Permissions = Record<Roles, string[]>;
const perms: Permissions = {
    admin: ['read', 'write', 'delete'],
    user: ['read', 'write'],
    guest: ['read']
};
```

---

### Enums

```typescript
// Numeric enum
enum Direction {
    Up,      // 0
    Down,    // 1
    Left,    // 2
    Right    // 3
}

let dir: Direction = Direction.Up;

// String enum (preferred)
enum Status {
    Active = "ACTIVE",
    Inactive = "INACTIVE",
    Pending = "PENDING"
}

let status: Status = Status.Active;
```

---

## TypeScript Best Practices

### ✅ Do's:

- Use `interface` for object shapes
- Use `type` for unions, primitives, complex types
- Enable strict mode in tsconfig.json
- Avoid `any` (use `unknown` if needed)
- Use const assertions for literal types
- Prefer `readonly` for immutability

### ❌ Don'ts:

- Don't use `any` everywhere
- Don't ignore TypeScript errors
- Don't use `as any` to bypass type checking
- Don't over-complicate types
- Don't forget to handle null/undefined

---

# Interview Preparation

## Common Interview Questions

### JavaScript Basics

**1. What is JavaScript?**
> "JavaScript is a high-level, interpreted programming language for creating interactive web pages. It runs in browsers and Node.js, supports async operations, and is single-threaded with event loop."

**2. Difference between var, let, and const?**
> "var is function-scoped and hoisted with undefined. let and const are block-scoped with TDZ. const prevents reassignment but allows object mutation. Use const by default, let when reassignment needed."

**3. What is hoisting?**
> "Hoisting moves declarations to top of scope. var is hoisted with undefined, let/const are hoisted but in TDZ. Function declarations are fully hoisted, expressions are not."

**4. Explain closures.**
> "Closure is when inner function accesses outer function's variables even after outer returns. Used for data privacy, function factories. Example: counter function that remembers count."

**5. What is 'this' keyword?**
> "'this' refers to object executing the function. Value depends on how function is called: method (object), regular function (window/undefined), arrow function (lexical), constructor (new object)."

---

### Asynchronous JavaScript

**6. What is a Promise?**
> "Promise represents eventual completion/failure of async operation. Has three states: pending, fulfilled, rejected. Use .then() for success, .catch() for errors, .finally() for cleanup."

**7. Explain async/await.**
> "async/await is syntactic sugar over Promises. async function returns Promise, await pauses execution until Promise resolves. Use try/catch for error handling. Makes async code look synchronous."

**8. What is event loop?**
> "Event loop enables async in single-threaded JavaScript. Execution order: call stack → microtasks (Promises) → macrotasks (setTimeout). This is why Promise runs before setTimeout(0)."

**9. Difference between Promise.all() and Promise.race()?**
> "Promise.all() waits for all promises (fails if any fails). Promise.race() returns first settled promise (success or failure). Use all for parallel operations, race for timeout scenarios."

---

### ES6+ Features

**10. What is destructuring?**
> "Destructuring extracts values from arrays/objects into variables. Syntax: const {name, age} = person. Makes code cleaner, supports default values and renaming."

**11. What is spread operator?**
> "Spread (...) expands iterable into individual elements. Used to copy arrays/objects, combine arrays, pass array as function arguments. Example: [...arr1, ...arr2]."

**12. Optional chaining vs nullish coalescing?**
> "Optional chaining (?.) safely accesses nested properties (returns undefined if null). Nullish coalescing (??) provides default only for null/undefined (not other falsy values like 0 or empty string)."

---

### TypeScript

**13. What is TypeScript?**
> "TypeScript is JavaScript with static typing. Catches errors at compile time, provides better IDE support, self-documenting code. Compiles to JavaScript. Essential for large projects."

**14. Interface vs Type in TypeScript?**
> "Interface defines object shape, can extend, supports declaration merging. Type is more flexible - supports unions, primitives, intersections. Use interface for objects, type for unions and complex types."

**15. What are Generics?**
> "Generics create reusable components that work with multiple types. Example: Array<T>, Promise<T>. Provides type safety while maintaining flexibility. Like a container that can hold any type but remembers what it holds."

---

## Coding Challenges

### 1. Implement debounce

```javascript
function debounce(func, delay) {
    let timeoutId;
    
    return function(...args) {
        clearTimeout(timeoutId);
        timeoutId = setTimeout(() => {
            func.apply(this, args);
        }, delay);
    };
}

// Usage
const search = debounce((query) => {
    console.log("Searching for:", query);
}, 300);

search("a");
search("ab");
search("abc");  // Only this executes after 300ms
```

---

### 2. Implement Promise.all

```javascript
function promiseAll(promises) {
    return new Promise((resolve, reject) => {
        const results = [];
        let completed = 0;
        
        promises.forEach((promise, index) => {
            Promise.resolve(promise)
                .then((value) => {
                    results[index] = value;
                    completed++;
                    
                    if (completed === promises.length) {
                        resolve(results);
                    }
                })
                .catch(reject);
        });
    });
}
```

---

### 3. Deep clone object

```javascript
function deepClone(obj) {
    // Handle primitives and null
    if (obj === null || typeof obj !== 'object') {
        return obj;
    }
    
    // Handle Date
    if (obj instanceof Date) {
        return new Date(obj.getTime());
    }
    
    // Handle Array
    if (Array.isArray(obj)) {
        return obj.map(item => deepClone(item));
    }
    
    // Handle Object
    const cloned = {};
    for (let key in obj) {
        if (obj.hasOwnProperty(key)) {
            cloned[key] = deepClone(obj[key]);
        }
    }
    
    return cloned;
}
```

---

### 4. Flatten nested array

```javascript
function flatten(arr) {
    return arr.reduce((acc, item) => {
        if (Array.isArray(item)) {
            return acc.concat(flatten(item));
        }
        return acc.concat(item);
    }, []);
}

// Or use built-in
const nested = [1, [2, [3, [4]]]];
console.log(nested.flat(Infinity));  // [1, 2, 3, 4]
```

---

### 5. Implement curry function

```javascript
function curry(func) {
    return function curried(...args) {
        if (args.length >= func.length) {
            return func.apply(this, args);
        }
        return function(...nextArgs) {
            return curried.apply(this, args.concat(nextArgs));
        };
    };
}

// Usage
function add(a, b, c) {
    return a + b + c;
}

const curriedAdd = curry(add);
console.log(curriedAdd(1)(2)(3));  // 6
console.log(curriedAdd(1, 2)(3));  // 6
console.log(curriedAdd(1)(2, 3));  // 6
```

---

## 🎯 Quick Reference

### JavaScript Cheat Sheet

| Concept | Key Points |
|---------|------------|
| **Variables** | const (default), let (reassign), avoid var |
| **Functions** | Arrow functions for callbacks, regular for methods |
| **this** | Depends on how function is called |
| **Closures** | Inner function remembers outer variables |
| **Promises** | then/catch/finally, async/await |
| **Event Loop** | Sync → Microtasks → Macrotasks |
| **Destructuring** | Extract values from objects/arrays |
| **Spread** | Copy and combine arrays/objects |
| **Modules** | import/export for code organization |

### TypeScript Cheat Sheet

| Concept | Key Points |
|---------|------------|
| **Types** | string, number, boolean, array, tuple |
| **Interface** | Define object shape |
| **Type** | Unions, intersections, aliases |
| **Generics** | Reusable type-safe components |
| **Utility Types** | Partial, Required, Pick, Omit, Record |
| **Enums** | Named constants |
| **any vs unknown** | Avoid any, use unknown with type guards |

---

## 🚀 Best Practices

### JavaScript

**✅ Do:**
- Use const by default, let when needed
- Use === instead of ==
- Use arrow functions for callbacks
- Handle errors in async code
- Use optional chaining for nested properties
- Use destructuring for cleaner code
- Use array methods (map, filter, reduce)

**❌ Don't:**
- Use var (use let/const)
- Mutate objects directly (use spread)
- Ignore error handling
- Use == for comparison
- Create callback hell (use async/await)
- Pollute global scope

### TypeScript

**✅ Do:**
- Enable strict mode
- Use interfaces for object shapes
- Use generics for reusable code
- Use utility types (Partial, Pick, etc.)
- Define return types for functions
- Use type guards for narrowing

**❌ Don't:**
- Use any everywhere
- Ignore TypeScript errors
- Use type assertions unnecessarily
- Over-complicate types
- Forget to handle null/undefined

---

## 🎓 Learning Path

### Week 1-2: Fundamentals
- Variables, data types, operators
- Functions, scope, closures
- Objects and arrays

### Week 3-4: Asynchronous
- Callbacks, Promises
- Async/await
- Event loop

### Week 5-6: Modern JS
- ES6+ features
- Destructuring, spread
- Modules

### Week 7-8: Advanced
- Prototypes, inheritance
- Functional programming
- Design patterns

### Week 9-10: TypeScript
- Basic types
- Interfaces and types
- Generics
- Advanced features

### Week 11-12: Interview Prep
- Practice common questions
- Coding challenges
- Build projects
- Review concepts

---

## 🎯 Key Takeaways

**JavaScript:**
1. **Single-threaded** but handles async with event loop
2. **Closures** are powerful for data privacy
3. **Promises** and **async/await** for async operations
4. **ES6+** features make code cleaner
5. **this** depends on how function is called

**TypeScript:**
1. **Adds type safety** to JavaScript
2. **Catches errors** at compile time
3. **Better tooling** and IDE support
4. **Use interfaces** for object shapes
5. **Generics** for reusable type-safe code

**Remember:**
> "JavaScript is about understanding async, closures, and prototypes. TypeScript is about adding type safety. Master JavaScript first, then TypeScript becomes easy."

---

# Phase 2 — Objects & Prototypes

## Objects

### 🎯 Working with Objects

**Definition:**
> Objects are collections of key-value pairs that store related data and functionality.

**Creating Objects:**

```javascript
// Object literal (most common)
const person = {
    name: "John",
    age: 30,
    greet() {
        console.log(`Hello, I'm ${this.name}`);
    }
};

// Constructor function
function Person(name, age) {
    this.name = name;
    this.age = age;
}
const john = new Person("John", 30);

// Object.create()
const personProto = {
    greet() {
        console.log(`Hello, I'm ${this.name}`);
    }
};
const alice = Object.create(personProto);
alice.name = "Alice";

// ES6 Class
class PersonClass {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
}
```

---

### Object Methods

```javascript
const person = { name: "John", age: 30, city: "NYC" };

// Object.keys() - returns array of keys
console.log(Object.keys(person));  // ["name", "age", "city"]

// Object.values() - returns array of values
console.log(Object.values(person));  // ["John", 30, "NYC"]

// Object.entries() - returns array of [key, value] pairs
console.log(Object.entries(person));
// [["name", "John"], ["age", 30], ["city", "NYC"]]

// Object.assign() - copy properties
const copy = Object.assign({}, person);

// Object.freeze() - make immutable
Object.freeze(person);
person.age = 31;  // Ignored (or error in strict mode)

// Object.seal() - prevent adding/removing properties
Object.seal(person);
person.country = "USA";  // Ignored
person.age = 31;  // OK - can modify existing
```

---

### Object Destructuring

```javascript
const person = { name: "John", age: 30, city: "NYC" };

// Extract properties
const { name, age } = person;

// Rename
const { name: fullName } = person;

// Default values
const { country = "USA" } = person;

// Rest operator
const { name, ...rest } = person;
console.log(rest);  // { age: 30, city: "NYC" }
```

**Interview Tip:**
> "Objects store key-value pairs. Use Object.keys/values/entries for iteration. Object.assign() for shallow copy, spread operator for merging. Destructuring extracts properties cleanly."

---

## Arrays

### 🎯 Array Methods

**Definition:**
> Arrays are ordered collections of values with powerful built-in methods.

**Mutating Methods (change original array):**

```javascript
const arr = [1, 2, 3];

// push() - add to end
arr.push(4);  // [1, 2, 3, 4]

// pop() - remove from end
arr.pop();  // [1, 2, 3]

// unshift() - add to beginning
arr.unshift(0);  // [0, 1, 2, 3]

// shift() - remove from beginning
arr.shift();  // [1, 2, 3]

// splice() - add/remove at any position
arr.splice(1, 1, 10, 20);  // Remove 1 element at index 1, add 10, 20
console.log(arr);  // [1, 10, 20, 3]

// sort() - sort in place
arr.sort((a, b) => a - b);

// reverse() - reverse in place
arr.reverse();
```

**Non-mutating Methods (return new array):**

```javascript
const arr = [1, 2, 3, 4, 5];

// slice() - extract portion
const sliced = arr.slice(1, 3);  // [2, 3]

// concat() - combine arrays
const combined = arr.concat([6, 7]);  // [1, 2, 3, 4, 5, 6, 7]

// map() - transform each element
const doubled = arr.map(n => n * 2);  // [2, 4, 6, 8, 10]

// filter() - keep elements that pass test
const evens = arr.filter(n => n % 2 === 0);  // [2, 4]

// reduce() - reduce to single value
const sum = arr.reduce((acc, n) => acc + n, 0);  // 15

// find() - first element that passes test
const found = arr.find(n => n > 3);  // 4

// findIndex() - index of first match
const index = arr.findIndex(n => n > 3);  // 3

// some() - at least one passes test
const hasEven = arr.some(n => n % 2 === 0);  // true

// every() - all pass test
const allPositive = arr.every(n => n > 0);  // true

// includes() - contains value
const hasThree = arr.includes(3);  // true

// flat() - flatten nested arrays
const nested = [1, [2, [3, 4]]];
console.log(nested.flat(2));  // [1, 2, 3, 4]

// flatMap() - map then flatten
const arr2 = [1, 2, 3];
const result = arr2.flatMap(n => [n, n * 2]);  // [1, 2, 2, 4, 3, 6]
```

**Interview Tip:**
> "map transforms, filter selects, reduce accumulates. Mutating methods: push, pop, splice, sort. Non-mutating: slice, concat, map, filter. Use non-mutating for immutability."

---

## Prototypes & Inheritance

### 🎯 Understanding Prototypes

**Definition:**
> Every JavaScript object has a prototype - another object from which it inherits properties and methods.

**Simple meaning:**
Prototype is like a blueprint that objects inherit from.

**Prototype Chain:**

```javascript
const animal = {
    eats: true,
    walk() {
        console.log("Animal walks");
    }
};

const dog = Object.create(animal);
dog.barks = true;

console.log(dog.eats);   // true (inherited from animal)
console.log(dog.barks);  // true (own property)
dog.walk();  // "Animal walks" (inherited method)

// Prototype chain: dog → animal → Object.prototype → null
```

---

### __proto__ vs prototype

```javascript
function Person(name) {
    this.name = name;
}

Person.prototype.greet = function() {
    console.log(`Hello, I'm ${this.name}`);
};

const john = new Person("John");

// __proto__ - actual object used in lookup chain
console.log(john.__proto__ === Person.prototype);  // true

// prototype - property on constructor function
console.log(Person.prototype);  // { greet: [Function], constructor: Person }
```

| Term | What it is | Who has it |
|------|------------|------------|
| **prototype** | Property on constructor | Functions |
| **__proto__** | Reference to prototype | All objects |

---

### ES6 Classes (Syntactic Sugar)

```javascript
// ES6 Class syntax
class Animal {
    constructor(name) {
        this.name = name;
    }
    
    speak() {
        console.log(`${this.name} makes a sound`);
    }
}

class Dog extends Animal {
    constructor(name, breed) {
        super(name);  // Call parent constructor
        this.breed = breed;
    }
    
    speak() {
        console.log(`${this.name} barks`);
    }
}

const dog = new Dog("Buddy", "Golden Retriever");
dog.speak();  // "Buddy barks"

// Under the hood, still uses prototypes!
console.log(dog instanceof Dog);     // true
console.log(dog instanceof Animal);  // true
```

**Real-life analogy:**
Prototype is like DNA - children (objects) inherit traits (properties/methods) from parents (prototypes).

**Interview Tip:**
> "Every object has __proto__ pointing to its prototype. Constructor functions have prototype property. Prototype chain: object → prototype → Object.prototype → null. ES6 classes are syntactic sugar over prototypes."

---

# Phase 4 (Continued) — Modern JavaScript

## New Data Structures

### Map

**Definition:**
> Map is a collection of key-value pairs where keys can be any type (not just strings).

**Map vs Object:**

| Feature | Map | Object |
|---------|-----|--------|
| **Key types** | Any type | String/Symbol only |
| **Order** | Insertion order | Not guaranteed |
| **Size** | map.size | Object.keys().length |
| **Iteration** | Built-in | Need Object.keys() |
| **Performance** | Better for frequent add/delete | Better for simple lookups |

**Usage:**

```javascript
const map = new Map();

// Set values
map.set('name', 'John');
map.set(1, 'number key');
map.set(true, 'boolean key');

// Get values
console.log(map.get('name'));  // "John"

// Check existence
console.log(map.has('name'));  // true

// Delete
map.delete('name');

// Size
console.log(map.size);

// Iterate
for (let [key, value] of map) {
    console.log(key, value);
}

// Convert to array
const entries = Array.from(map);
```

---

### Set

**Definition:**
> Set is a collection of unique values (no duplicates).

**Usage:**

```javascript
const set = new Set();

// Add values
set.add(1);
set.add(2);
set.add(2);  // Duplicate - ignored

console.log(set);  // Set(2) { 1, 2 }

// Check existence
console.log(set.has(1));  // true

// Delete
set.delete(1);

// Size
console.log(set.size);

// Convert array to Set (remove duplicates)
const numbers = [1, 2, 2, 3, 3, 4];
const unique = [...new Set(numbers)];
console.log(unique);  // [1, 2, 3, 4]

// Iterate
for (let value of set) {
    console.log(value);
}
```

---

### WeakMap & WeakSet

**WeakMap:**
- Keys must be objects
- Keys are weakly referenced (garbage collected if no other references)
- No iteration methods
- Use for private data

```javascript
const weakMap = new WeakMap();
let obj = { name: "John" };

weakMap.set(obj, "some data");
console.log(weakMap.get(obj));  // "some data"

obj = null;  // Object can be garbage collected
```

**WeakSet:**
- Similar to WeakMap but stores values (not key-value pairs)
- Values must be objects

---

### Symbol

**Definition:**
> Symbol creates unique identifiers that won't collide with other property names.

```javascript
// Create symbols
const id1 = Symbol('id');
const id2 = Symbol('id');

console.log(id1 === id2);  // false (always unique)

// Use as object property
const user = {
    name: "John",
    [id1]: 123  // Symbol as key
};

console.log(user[id1]);  // 123
console.log(Object.keys(user));  // ["name"] - symbols hidden

// Global symbols
const globalSym = Symbol.for('app.id');
const same = Symbol.for('app.id');
console.log(globalSym === same);  // true
```

**Interview Tip:**
> "Map allows any key type with guaranteed order. Set stores unique values. WeakMap/WeakSet allow garbage collection. Symbol creates unique identifiers for object properties."

---

# Phase 5 — DOM & Browser APIs

## DOM Manipulation

### 🎯 Selecting Elements

```javascript
// Select single element
const element = document.getElementById('myId');
const element2 = document.querySelector('.myClass');
const element3 = document.querySelector('#myId');

// Select multiple elements
const elements = document.getElementsByClassName('myClass');
const elements2 = document.getElementsByTagName('div');
const elements3 = document.querySelectorAll('.myClass');
```

---

### Modifying Elements

```javascript
const div = document.querySelector('#myDiv');

// Change content
div.textContent = "New text";
div.innerHTML = "<strong>Bold text</strong>";

// Change attributes
div.setAttribute('data-id', '123');
div.id = 'newId';
div.className = 'newClass';

// Change styles
div.style.color = 'red';
div.style.backgroundColor = 'blue';

// Add/remove classes
div.classList.add('active');
div.classList.remove('hidden');
div.classList.toggle('visible');
div.classList.contains('active');  // true
```

---

### Creating and Removing Elements

```javascript
// Create element
const newDiv = document.createElement('div');
newDiv.textContent = "Hello";
newDiv.className = 'greeting';

// Append to DOM
document.body.appendChild(newDiv);

// Insert at specific position
const parent = document.querySelector('#parent');
parent.insertBefore(newDiv, parent.firstChild);

// Remove element
newDiv.remove();
// Or
parent.removeChild(newDiv);
```

**Interview Tip:**
> "querySelector for single element, querySelectorAll for multiple. Use textContent for text, innerHTML for HTML. classList for class manipulation. createElement and appendChild to add elements."

---

## Events

### 🎯 Event Handling

**Adding Event Listeners:**

```javascript
const button = document.querySelector('#myButton');

// Add event listener
button.addEventListener('click', function(event) {
    console.log('Button clicked!');
    console.log('Event:', event);
});

// Arrow function (be careful with 'this')
button.addEventListener('click', (e) => {
    console.log('Clicked');
});

// Remove event listener (need named function)
function handleClick(e) {
    console.log('Clicked');
}
button.addEventListener('click', handleClick);
button.removeEventListener('click', handleClick);
```

---

### Event Object

```javascript
button.addEventListener('click', (event) => {
    console.log(event.type);        // "click"
    console.log(event.target);      // Element that triggered event
    console.log(event.currentTarget);  // Element with listener
    console.log(event.clientX);     // Mouse X position
    console.log(event.clientY);     // Mouse Y position
    
    event.preventDefault();   // Prevent default action
    event.stopPropagation();  // Stop bubbling
});
```

---

### Event Bubbling and Capturing

**Definition:**
> Event propagation has three phases: capturing → target → bubbling.

```javascript
// Bubbling (default) - from target to root
div.addEventListener('click', handler);  // Bubbles up

// Capturing - from root to target
div.addEventListener('click', handler, true);  // Captures down

// Stop propagation
element.addEventListener('click', (e) => {
    e.stopPropagation();  // Stops bubbling/capturing
});
```

**Event Delegation:**

```javascript
// Instead of adding listener to each item
// Add one listener to parent
document.querySelector('#list').addEventListener('click', (e) => {
    if (e.target.tagName === 'LI') {
        console.log('List item clicked:', e.target.textContent);
    }
});
```

**Real-life analogy:**
Event bubbling is like a message traveling up a company hierarchy - starts with employee (target), goes to manager, then CEO (root).

**Interview Tip:**
> "Event bubbling: event travels from target to root. Event capturing: root to target. Use event delegation to handle multiple elements with one listener on parent. stopPropagation() stops bubbling."

---

## Browser APIs

### fetch API

**Definition:**
> fetch() is a modern way to make HTTP requests, returns a Promise.

```javascript
// GET request
fetch('https://api.example.com/users')
    .then(response => {
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }
        return response.json();
    })
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));

// With async/await
async function getUsers() {
    try {
        const response = await fetch('https://api.example.com/users');
        
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }
        
        const data = await response.json();
        return data;
    } catch (error) {
        console.error('Error:', error);
    }
}

// POST request
async function createUser(userData) {
    const response = await fetch('https://api.example.com/users', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify(userData)
    });
    
    return await response.json();
}
```

---

### localStorage vs sessionStorage

| Feature | localStorage | sessionStorage |
|---------|--------------|----------------|
| **Lifetime** | Permanent (until cleared) | Session only (tab closed) |
| **Scope** | All tabs/windows | Single tab |
| **Capacity** | ~5-10MB | ~5-10MB |
| **Use case** | User preferences | Temporary data |

**Usage:**

```javascript
// localStorage
localStorage.setItem('username', 'John');
const username = localStorage.getItem('username');
localStorage.removeItem('username');
localStorage.clear();  // Remove all

// Store objects (convert to JSON)
const user = { name: "John", age: 30 };
localStorage.setItem('user', JSON.stringify(user));
const storedUser = JSON.parse(localStorage.getItem('user'));
```

**Interview Tip:**
> "localStorage persists across sessions, sessionStorage clears when tab closes. Both store strings only - use JSON.stringify/parse for objects. Capacity ~5-10MB per domain."

---

# Phase 6 — Advanced Concepts

## Functional Programming

### 🎯 Core Concepts

**1. Pure Functions:**

```javascript
// ✅ Pure - same input, same output, no side effects
function add(a, b) {
    return a + b;
}

// ❌ Impure - depends on external state
let total = 0;
function addToTotal(value) {
    total += value;  // Side effect!
    return total;
}
```

**2. Immutability:**

```javascript
// ❌ Mutating
const arr = [1, 2, 3];
arr.push(4);  // Modifies original

// ✅ Immutable
const arr = [1, 2, 3];
const newArr = [...arr, 4];  // Creates new array
```

**3. Function Composition:**

```javascript
const add = (x) => x + 1;
const multiply = (x) => x * 2;

// Compose functions
const compose = (f, g) => (x) => f(g(x));

const addThenMultiply = compose(multiply, add);
console.log(addThenMultiply(5));  // (5 + 1) * 2 = 12
```

**4. Currying:**

```javascript
// Regular function
function add(a, b, c) {
    return a + b + c;
}

// Curried version
function curriedAdd(a) {
    return function(b) {
        return function(c) {
            return a + b + c;
        };
    };
}

console.log(curriedAdd(1)(2)(3));  // 6

// Or with arrow functions
const curriedAdd = a => b => c => a + b + c;
```

**Interview Tip:**
> "Functional programming: pure functions (no side effects), immutability (don't mutate data), function composition (combine functions), currying (transform multi-arg function to sequence of single-arg functions)."

---

## Error Handling

### 🎯 try...catch...finally

**Definition:**
> try...catch handles runtime errors gracefully without crashing the program.

```javascript
try {
    // Code that might throw error
    const data = JSON.parse(invalidJSON);
} catch (error) {
    // Handle error
    console.error('Error:', error.message);
} finally {
    // Always executes (cleanup)
    console.log('Cleanup code');
}
```

---

### Throwing Errors

```javascript
function divide(a, b) {
    if (b === 0) {
        throw new Error('Cannot divide by zero');
    }
    return a / b;
}

try {
    divide(10, 0);
} catch (error) {
    console.error(error.message);  // "Cannot divide by zero"
}
```

---

### Custom Errors

```javascript
class ValidationError extends Error {
    constructor(message) {
        super(message);
        this.name = 'ValidationError';
    }
}

function validateAge(age) {
    if (age < 0) {
        throw new ValidationError('Age cannot be negative');
    }
    if (age > 150) {
        throw new ValidationError('Age too high');
    }
    return true;
}

try {
    validateAge(-5);
} catch (error) {
    if (error instanceof ValidationError) {
        console.error('Validation failed:', error.message);
    }
}
```

---

### Error Handling in Async Code

```javascript
// Promises
fetch('/api/data')
    .then(response => response.json())
    .catch(error => console.error('Error:', error));

// Async/await
async function fetchData() {
    try {
        const response = await fetch('/api/data');
        const data = await response.json();
        return data;
    } catch (error) {
        console.error('Error:', error);
        throw error;  // Re-throw if needed
    }
}
```

**Interview Tip:**
> "try...catch handles errors without crashing. Use for JSON.parse, API calls, risky operations. finally always executes (cleanup). For async, use .catch() with Promises or try/catch with async/await."

---

## Performance & Optimization

### Debounce and Throttle

**Debounce:**
> Delays execution until after wait time has elapsed since last call.

```javascript
function debounce(func, delay) {
    let timeoutId;
    return function(...args) {
        clearTimeout(timeoutId);
        timeoutId = setTimeout(() => func.apply(this, args), delay);
    };
}

// Use case: Search input
const searchInput = document.querySelector('#search');
const search = debounce((query) => {
    console.log('Searching for:', query);
}, 300);

searchInput.addEventListener('input', (e) => search(e.target.value));
```

**Throttle:**
> Ensures function executes at most once per specified time period.

```javascript
function throttle(func, limit) {
    let inThrottle;
    return function(...args) {
        if (!inThrottle) {
            func.apply(this, args);
            inThrottle = true;
            setTimeout(() => inThrottle = false, limit);
        }
    };
}

// Use case: Scroll event
const handleScroll = throttle(() => {
    console.log('Scrolling...');
}, 1000);

window.addEventListener('scroll', handleScroll);
```

| Feature | Debounce | Throttle |
|---------|----------|----------|
| **Execution** | After wait time | At most once per interval |
| **Use case** | Search input, resize | Scroll, mouse move |
| **Analogy** | Elevator door (waits for people to stop entering) | Rate limiter (max once per second) |

---

### Deep vs Shallow Copy

**Shallow Copy:**
```javascript
const original = { name: "John", address: { city: "NYC" } };

// Shallow copies
const copy1 = { ...original };
const copy2 = Object.assign({}, original);

// Problem: nested objects still referenced
copy1.address.city = "LA";
console.log(original.address.city);  // "LA" (modified!)
```

**Deep Copy:**
```javascript
// Method 1: JSON (simple but limited)
const deepCopy1 = JSON.parse(JSON.stringify(original));
// Limitations: loses functions, undefined, Date, etc.

// Method 2: structuredClone (modern)
const deepCopy2 = structuredClone(original);

// Method 3: Recursive (custom)
function deepClone(obj) {
    if (obj === null || typeof obj !== 'object') return obj;
    if (obj instanceof Date) return new Date(obj);
    if (Array.isArray(obj)) return obj.map(deepClone);
    
    const cloned = {};
    for (let key in obj) {
        if (obj.hasOwnProperty(key)) {
            cloned[key] = deepClone(obj[key]);
        }
    }
    return cloned;
}
```

**Interview Tip:**
> "Shallow copy copies first level only (spread, Object.assign). Deep copy copies all nested levels. Use JSON.parse(JSON.stringify()) for simple objects, structuredClone() for modern browsers, or custom recursive function."

---

### Memory Management

**How JavaScript Manages Memory:**
1. **Allocation** - Memory allocated when creating variables
2. **Usage** - Reading/writing to memory
3. **Garbage Collection** - Automatic cleanup of unused memory

**Common Memory Leaks:**

```javascript
// 1. Global variables
function leak() {
    globalVar = "I'm global!";  // Forgot 'let' - creates global
}

// 2. Forgotten timers
const id = setInterval(() => {
    // Do something
}, 1000);
// clearInterval(id);  // Forgot to clear!

// 3. Closures holding references
function createClosure() {
    const largeData = new Array(1000000);
    return function() {
        console.log(largeData[0]);  // Keeps entire array in memory
    };
}

// 4. Detached DOM nodes
let element = document.querySelector('#myElement');
element.remove();
// Still referenced by 'element' variable - not garbage collected
element = null;  // Now can be collected
```

**Prevention:**
- Clear timers and intervals
- Remove event listeners when done
- Set references to null when done
- Use WeakMap/WeakSet for cache

---

## Design Patterns

### Module Pattern

**Definition:**
> Encapsulates private data and exposes public API.

```javascript
const Calculator = (function() {
    // Private variables
    let result = 0;
    
    // Private function
    function log(msg) {
        console.log(`[Calculator] ${msg}`);
    }
    
    // Public API
    return {
        add(x) {
            result += x;
            log(`Added ${x}, result: ${result}`);
            return this;
        },
        subtract(x) {
            result -= x;
            log(`Subtracted ${x}, result: ${result}`);
            return this;
        },
        getResult() {
            return result;
        },
        reset() {
            result = 0;
            return this;
        }
    };
})();

// Usage
Calculator.add(5).add(3).subtract(2);
console.log(Calculator.getResult());  // 6
```

---

### Revealing Module Pattern

```javascript
const UserModule = (function() {
    // Private
    let users = [];
    
    function validateUser(user) {
        return user.name && user.email;
    }
    
    // Public
    function addUser(user) {
        if (validateUser(user)) {
            users.push(user);
            return true;
        }
        return false;
    }
    
    function getUsers() {
        return [...users];  // Return copy
    }
    
    function getUserCount() {
        return users.length;
    }
    
    // Reveal public methods
    return {
        addUser,
        getUsers,
        getUserCount
    };
})();
```

**Interview Tip:**
> "Module pattern uses IIFE to create private scope. Returns object with public methods. Revealing module pattern explicitly lists public API at end. Used for encapsulation before ES6 modules."

---

# Additional Interview Topics

## 🎯 Advanced Interview Questions

**16. What is the difference between map() and forEach()?**
> "map() returns new array with transformed elements. forEach() executes function for each element, returns undefined. Use map for transformation, forEach for side effects."

**17. What is the prototype chain?**
> "Prototype chain is how JavaScript looks up properties. Searches object → prototype → prototype's prototype → Object.prototype → null. Used for inheritance."

**18. Explain event delegation.**
> "Event delegation adds single listener to parent instead of multiple listeners to children. Uses event bubbling. More efficient, works with dynamically added elements."

**19. What is the difference between shallow and deep copy?**
> "Shallow copy copies first level only (spread, Object.assign). Nested objects still referenced. Deep copy copies all levels recursively. Use JSON.parse(JSON.stringify()) or structuredClone()."

**20. What is debounce and when to use it?**
> "Debounce delays function execution until after wait time since last call. Use for search inputs, resize events. Prevents excessive function calls. Example: search API called only after user stops typing."

**21. What are WeakMap and WeakSet?**
> "WeakMap and WeakSet hold weak references to objects. Objects can be garbage collected even if in WeakMap/WeakSet. Use for private data, caching. Cannot iterate, keys must be objects."

**22. Difference between localStorage and sessionStorage?**
> "localStorage persists across sessions (permanent until cleared). sessionStorage clears when tab closes. Both store strings only (5-10MB limit). Use localStorage for preferences, sessionStorage for temporary data."

**23. What is CORS?**
> "CORS (Cross-Origin Resource Sharing) is security feature preventing requests to different domains. Server must send Access-Control-Allow-Origin header. Preflight requests check permissions for complex requests."

**24. Explain Symbol and its use cases.**
> "Symbol creates unique identifiers that never collide. Use for object property keys, avoiding name conflicts, creating private properties. Symbol.for() creates global symbols."

**25. What is the difference between Map and Object?**
> "Map allows any key type, maintains insertion order, has size property, better for frequent add/delete. Object keys are strings/symbols only, better for simple lookups. Use Map for dynamic key-value storage."

---

## 🎯 Coding Pattern Questions

### 1. Remove duplicates from array

```javascript
// Method 1: Set
const arr = [1, 2, 2, 3, 3, 4];
const unique = [...new Set(arr)];

// Method 2: filter
const unique2 = arr.filter((item, index) => arr.indexOf(item) === index);

// Method 3: reduce
const unique3 = arr.reduce((acc, item) => {
    return acc.includes(item) ? acc : [...acc, item];
}, []);
```

---

### 2. Group array of objects by property

```javascript
const users = [
    { name: "John", age: 30 },
    { name: "Jane", age: 25 },
    { name: "Bob", age: 30 }
];

const groupedByAge = users.reduce((acc, user) => {
    const key = user.age;
    if (!acc[key]) {
        acc[key] = [];
    }
    acc[key].push(user);
    return acc;
}, {});

console.log(groupedByAge);
// { 25: [{name: "Jane", age: 25}], 30: [{name: "John", age: 30}, {name: "Bob", age: 30}] }
```

---

### 3. Implement memoization

```javascript
function memoize(fn) {
    const cache = new Map();
    
    return function(...args) {
        const key = JSON.stringify(args);
        
        if (cache.has(key)) {
            console.log('From cache');
            return cache.get(key);
        }
        
        const result = fn.apply(this, args);
        cache.set(key, result);
        return result;
    };
}

// Usage
const fibonacci = memoize(function(n) {
    if (n <= 1) return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
});

console.log(fibonacci(10));  // Calculates
console.log(fibonacci(10));  // From cache
```

---

### 4. Implement event emitter

```javascript
class EventEmitter {
    constructor() {
        this.events = {};
    }
    
    on(event, listener) {
        if (!this.events[event]) {
            this.events[event] = [];
        }
        this.events[event].push(listener);
    }
    
    emit(event, ...args) {
        if (this.events[event]) {
            this.events[event].forEach(listener => {
                listener(...args);
            });
        }
    }
    
    off(event, listenerToRemove) {
        if (this.events[event]) {
            this.events[event] = this.events[event].filter(
                listener => listener !== listenerToRemove
            );
        }
    }
}

// Usage
const emitter = new EventEmitter();

function onMessage(msg) {
    console.log('Message:', msg);
}

emitter.on('message', onMessage);
emitter.emit('message', 'Hello!');  // Message: Hello!
emitter.off('message', onMessage);
```

---

### 5. Implement retry logic

```javascript
async function retry(fn, maxAttempts = 3, delay = 1000) {
    for (let attempt = 1; attempt <= maxAttempts; attempt++) {
        try {
            return await fn();
        } catch (error) {
            if (attempt === maxAttempts) {
                throw error;
            }
            console.log(`Attempt ${attempt} failed, retrying...`);
            await new Promise(resolve => setTimeout(resolve, delay));
        }
    }
}

// Usage
async function fetchData() {
    const response = await fetch('/api/data');
    if (!response.ok) throw new Error('Failed');
    return await response.json();
}

retry(fetchData, 3, 1000)
    .then(data => console.log(data))
    .catch(error => console.error('All attempts failed:', error));
```

---

## 📊 Complete Comparison Tables

### JavaScript vs TypeScript

| Feature | JavaScript | TypeScript |
|---------|------------|------------|
| **Typing** | Dynamic | Static |
| **Compilation** | Interpreted | Compiled to JS |
| **Error Detection** | Runtime | Compile time |
| **IDE Support** | Good | Excellent |
| **Learning Curve** | Easy | Moderate |
| **Use Case** | Small projects, scripts | Large projects, teams |

---

### Promise Methods Comparison

| Method | Waits For | Returns | Fails If |
|--------|-----------|---------|----------|
| **Promise.all()** | All promises | Array of results | Any fails |
| **Promise.race()** | First to settle | First result | First fails |
| **Promise.allSettled()** | All promises | Array of status objects | Never |
| **Promise.any()** | First to succeed | First success | All fail |

---

### Array Method Categories

| Category | Methods | Returns | Mutates |
|----------|---------|---------|---------|
| **Add/Remove** | push, pop, shift, unshift, splice | Modified array | ✅ Yes |
| **Transform** | map, filter, reduce, flatMap | New array | ❌ No |
| **Search** | find, findIndex, indexOf, includes | Element/index/boolean | ❌ No |
| **Test** | some, every | Boolean | ❌ No |
| **Sort** | sort, reverse | Modified array | ✅ Yes |
| **Extract** | slice, concat | New array | ❌ No |

---

## 🎓 Final Summary

### JavaScript Core Concepts:

1. **Variables**: Use const by default, let for reassignment
2. **Functions**: Arrow functions for callbacks, regular for methods
3. **Closures**: Inner function remembers outer scope
4. **this**: Depends on how function is called
5. **Async**: Promises and async/await for async operations
6. **Event Loop**: Sync → Microtasks → Macrotasks
7. **Prototypes**: Inheritance mechanism in JavaScript
8. **ES6+**: Destructuring, spread, optional chaining, modules

### TypeScript Essentials:

1. **Type Safety**: Catch errors at compile time
2. **Interfaces**: Define object shapes
3. **Generics**: Type-safe reusable code
4. **Utility Types**: Partial, Pick, Omit, Record
5. **Best Practice**: Strict mode, avoid any, use type guards

### Interview Success Tips:

**✅ Master these topics:**
- Closures and scope
- Promises and async/await
- Event loop and execution order
- Array methods (map, filter, reduce)
- this keyword in different contexts
- Prototypes and inheritance
- ES6+ features

**✅ Practice these patterns:**
- Debounce and throttle
- Deep clone
- Event emitter
- Memoization
- Retry logic

**✅ Be ready to explain:**
- How async works (event loop)
- Why closures matter
- When to use Map vs Object
- Difference between == and ===
- How prototypes work

**Remember:**
> "JavaScript interviews test understanding of async, closures, and prototypes. TypeScript adds type safety. Practice coding challenges, explain concepts with analogies, and always mention trade-offs."
