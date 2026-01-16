# Phase 1 — Fundamentals

## Outline
- [1. Introduction](#1-introduction)
  - [What is Angular?](#what-is-angular)
  - [Why Angular?](#why-angular)
  - [Angular vs React vs Vue](#angular-vs-react-vs-vue-short-clear-key-points)
  - [SPA vs MPA](#spa-vs-mpa)
  - [Angular Architecture Overview](#angular-architecture--compilation-process)
- [2. Angular Basics](#2-angular-basics)
  - [Angular CLI](#angular-cli--commands-with-flags-simple-guide)
  - [Project structure](#angular-project-structure-simple-explanation)
  - [main.ts](#maints-explained-simply)
  - [Bootstrap process](#angular-bootstrap-process-simple-explanation)
  - [Standalone vs NgModules](#standalone-components-vs-ngmodules)
- [3. Components](#3-components)
  - [What is a Component?](#what-is-a-component)
  - [Component metadata](#component-metadata)
  - [Templates](#1%EF%B8%8F%E2%83%A3-templates-html)
  - [Styles](#2%EF%B8%8F%E2%83%A3-styles-cssscss)
  - [Component lifecycle](#component-lifecycle)
  - [constructor vs ngOnInit](#4%EF%B8%8F%E2%83%A3-constructor-vs-ngoninit)
  - [Change detection basics](#5%EF%B8%8F%E2%83%A3-change-detection-basics)
- [4. Templates & Data Binding](#4-templates--data-binding)
  - [Interpolation](#interpolation)
  - [Property binding](#property-binding)
  - [Event binding](#event-binding)
  - [Two-way binding](#two-way-binding)
  - [Template expressions](#template-expressions)
  - [Safe navigation operator](#safe-navigation-operator)
- [5. Directives](#5-directives)
  - [Attribute directives](#attribute-directives)
  - [Structural directives](#structural-directives)
  - [`*ngIf`, `*ngFor`, `*ngSwitch`](#built-in-structural-directives)
  - [Custom attribute directives](#custom-attribute-directive)
  - [Custom structural directives](#custom-structural-directive)
- [6. Pipes](#6-pipes)
  - [Built-in pipes](#built-in-pipes)
  - [Custom pipes](#custom-pipes)
  - [Pure vs impure pipes](#pure-vs-impure-pipes)

## 1. Introduction

### What is Angular?

* Angular is a **frontend framework** for building **single-page applications (SPAs)**
* Used mainly for **large and enterprise-level applications**
* Written in **TypeScript**
* Developed and maintained by **Google**
* Uses a **component-based architecture**
* Automatically updates the UI when data changes

---

### Why Angular? (What makes Angular different)

#### 1️⃣ Complete Framework

* Angular provides **everything out of the box**
  * Routing
  * Forms
  * HTTP
  * Dependency Injection
* No need to choose many external libraries

#### 2️⃣ Strong Structure & Opinionated

* Enforces a **clear architecture**
* Easier for large teams to work together
* Less architectural confusion

#### 3️⃣ TypeScript First

* Strong typing
* Fewer runtime bugs
* Better tooling & refactoring

#### 4️⃣ Built-in Dependency Injection

* Makes code reusable
* Easier testing
* Better separation of concerns

#### 5️⃣ Enterprise Focus

* Designed for **scalability and maintainability**
* Preferred for long-term, complex projects

---

### Why Angular? (Quick reasons)

Angular is chosen mainly for **large, complex, and long-term applications**.

#### 🔹 1️⃣ Strong Structure

* Angular enforces a **clear architecture**
* Easy to maintain large codebases
* Best for **team-based development**

#### 🔹 2️⃣ All-in-One Framework

* Comes with **routing, forms, HTTP, DI, testing**
* No need to assemble many third-party libraries
* Saves setup and decision time

#### 🔹 3️⃣ TypeScript by Default

* Strong typing
* Better error detection at compile time
* Easier refactoring and safer code

#### 🔹 4️⃣ Built for Enterprise

* Scales well as the app grows
* Predictable patterns
* Used heavily in banking, healthcare, corporate tools

#### 🔹 5️⃣ Powerful Tooling

* Angular CLI for scaffolding, build, test, lint
* Consistent development experience
* Faster onboarding for new developers

#### 🔹 6️⃣ Performance Features

* Lazy loading
* Ahead-of-Time (AOT) compilation
* OnPush change detection
* Signals (modern Angular)

---

### What Makes Angular a Good Choice?

* You want **long-term maintainability**
* You have **large teams**
* You prefer **clear rules over flexibility**
* You need a **complete solution**, not just a UI library

### Angular vs React vs Vue (Short, Clear, Key Points)

---

### 🔹 Angular

* **Type**: Full **framework**
* **Language**: TypeScript
* **Architecture**: Opinionated, structured
* **Built-in features**: Routing, Forms, HTTP, DI
* **Best for**: Large & enterprise applications

**Strengths**

* Everything included
* Strong structure
* Easy to scale for big teams

**Weakness**

* Steeper learning curve
* More boilerplate

---

### 🔹 React

* **Type**: **Library** (UI only)
* **Language**: JavaScript / TypeScript
* **Architecture**: Flexible, unopinionated
* **Built-in features**: ❌ (needs external libs)
* **Best for**: UI-heavy, flexible apps

**Strengths**

* Simple to start
* Huge ecosystem
* Very popular

**Weakness**

* You must choose many libraries
* Architecture can become inconsistent

---

### 🔹 Vue

* **Type**: Progressive framework
* **Language**: JavaScript / TypeScript
* **Architecture**: Semi-opinionated
* **Built-in features**: Some (router, state via libs)
* **Best for**: Small to medium apps

**Strengths**

* Easy to learn
* Clean syntax
* Flexible adoption

**Weakness**

* Smaller ecosystem than React
* Less enterprise adoption than Angular

---

## 📊 Quick Comparison Table

| Feature        | Angular   | React    | Vue       |
| -------------- | --------- | -------- | --------- |
| Type           | Framework | Library  | Framework |
| Learning Curve | High      | Medium   | Low       |
| Structure      | Strong    | Flexible | Moderate  |
| Enterprise Use | ⭐⭐⭐⭐      | ⭐⭐       | ⭐         |
| Built-in Tools | Yes       | No       | Partial   |

---

## 🎯 When to Choose What?

* ✅ **Angular** → Enterprise apps, large teams, long-term projects
* ✅ **React** → UI-focused apps, flexibility, startups
* ✅ **Vue** → Quick development, small/medium apps

---

### SPA vs MPA

---

#### SPA (Single Page Application)

##### What it is

* The app loads **one HTML page**
* Content updates **without full page reload**
* Navigation happens using **JavaScript**

##### How it works

* Browser loads app once
* Angular/React/Vue fetch data via APIs
* UI updates dynamically

##### Examples

* Gmail
* Facebook
* Angular dashboards

##### Pros

* Faster navigation
* Better user experience
* Less server load after first load

##### Cons

* Initial load can be heavy
* SEO needs extra handling (SSR)

---

#### MPA (Multi Page Application)

##### What it is

* Each page is a **separate HTML page**
* Every navigation causes a **full page reload**

##### How it works

* Browser requests a new page from server
* Server renders HTML each time

##### Examples

* Traditional websites
* News portals
* Server-rendered apps

### Pros

* Better SEO by default
* Simple architecture
* Good for content-heavy sites

### Cons

* Slower navigation
* More server requests
* Less interactive feel

---

## 📊 Quick Comparison

| Feature     | SPA             | MPA               |
| ----------- | --------------- | ----------------- |
| Page reload | ❌ No            | ✅ Yes             |
| Speed       | Fast after load | Slower            |
| UX          | App-like        | Website-like      |
| SEO         | Needs SSR       | Good by default   |
| Examples    | Angular apps    | Traditional sites |

---

## 🎯 When to Use What?

* ✅ **SPA** → Dashboards, admin panels, web apps
* ✅ **MPA** → Blogs, marketing sites, SEO-heavy pages

---

### Angular Architecture & Compilation Process

---

## 🔷 PART 1: Angular Architecture (How Angular Is Structured)

### 🔹 Big Idea

Angular architecture is designed to **separate concerns**, so that:

* UI logic
* Business logic
* Data access
* Navigation are **cleanly isolated**.

This makes applications **scalable, testable, and maintainable**.

---

## 🧱 Core Architectural Layers

### 1️⃣ Components (Presentation Layer)

* Control **what the user sees**
* Handle user interactions
* Bind data to the UI

👉 Components are **not supposed to contain heavy logic**.

---

### 2️⃣ Templates (View Layer)

* HTML that displays data
* Uses Angular binding syntax
* Automatically updates when data changes

👉 Angular manages DOM updates for you.

---

### 3️⃣ Services (Business Logic Layer)

* Handle:

  * API calls
  * Data processing
  * Shared logic
* Independent of UI

👉 Services allow **reuse and clean separation**.

---

### 4️⃣ Dependency Injection (Glue Layer)

* Automatically provides services to components
* Manages object creation and lifecycle

👉 You don’t manually create dependencies — Angular does it.

---

### 5️⃣ Router (Navigation Layer)

* Maps URLs to components
* Enables SPA behavior
* Supports lazy loading

👉 Navigation without page reload.

---

### 6️⃣ Modules / Standalone Components (Organization Layer)

* **Older Angular** → NgModules
* **Modern Angular** → Standalone components

Purpose:

* Group related functionality
* Control what is loaded and when

👉 Angular is moving toward **standalone-first architecture**.

---

## 🔄 Architectural Flow (Simple)

1. User opens the app
2. Angular loads the root component
3. Router decides which component to show
4. Component requests data from a service
5. Service fetches data (API)
6. Angular updates the UI automatically

---

## 🔷 PART 2: Angular Compilation Process (How Angular Runs)

### **1️⃣ User opens the app**

* The browser requests:

  * `index.html`
  * JavaScript bundles (compiled Angular code)
  * CSS assets

* `index.html` contains **one root tag** (example: `<app-root>`)

👉 At this point:

* The browser **does not know Angular**
* It just sees an empty custom HTML tag

Angular has **not started yet**.

---

### **2️⃣ Angular loads the root component**

* The browser executes the main JavaScript bundle
* Angular runtime starts
* Angular:

  1. Creates the **root injector** (Dependency Injection system)
  2. Initializes platform-level services
  3. Finds the root component selector (`app-root`)
  4. Creates an **instance of the root component**
  5. Links the component to the DOM

👉 This process is called **bootstrapping**

At the end of this step:

* Angular is now “alive”
* The root component exists in memory
* Change detection is initialized

---

### **3️⃣ Router decides which component to show**

* Angular Router:

  * Reads the current browser URL
  * Matches it against route configuration
* Router checks:

  * Guards (authentication, permissions)
  * Lazy-loading conditions

If allowed:

* Router creates the target component instance
* Inserts it into `<router-outlet>`

👉 No page reload happens
👉 Only component instances are created/destroyed

Internally:

* Old component (if any) is destroyed
* New component lifecycle starts

---

### **4️⃣ Component requests data from a service**

* Angular creates the component instance
* During creation:

  * Angular looks at the constructor
  * Sees required services
* Dependency Injection system:

  * Finds or creates service instances
  * Injects them into the component

👉 Services are usually:

* Singleton (one instance)
* Cached in the injector tree

The component **does not create services** — Angular does.

---

### **5️⃣ Service fetches data (API)**

* The service:

  * Uses Angular’s HTTP client
* HTTP client:

  * Creates an HTTP request
  * Passes it through **interceptors**
  * Sends request to browser networking layer

While waiting:

* JavaScript thread is **non-blocking**
* UI stays responsive

When response arrives:

* HTTP client emits the data
* Service passes data back to component

👉 Angular does not block rendering
👉 Everything is async and event-driven

---

### **6️⃣ Angular updates the UI automatically**

#### This is the MOST IMPORTANT part - What triggers UI update?

Angular uses **change detection**.

Internally:

* Angular knows **something changed** because:

  * An async task completed (HTTP, event, timer)
  * Zone.js (or signals) notifies Angular

Angular then:

1. Starts a **change detection cycle**
2. Checks component state
3. Compares old values vs new values
4. Updates only the affected DOM nodes

👉 No full DOM re-render
👉 Only necessary parts are updated

---

#### 🔄 Internal Loop (Simplified)

Angular continuously runs this loop:

```
Event happens →
Angular notified →
Change detection runs →
UI updates →
Wait for next event
```

This is why:

* UI stays in sync
* You don’t manually update the DOM


# 🔹 Ivy vs View Engine (Angular Compilers)

## 🧠 What are they?

Both **Ivy** and **View Engine** are **Angular’s internal rendering & compilation engines**.
They decide **how Angular components are compiled and rendered in the browser**.

---

## ✅ View Engine (Old – before Angular 9)


## ⭐ Key Differences (Simple)

| Feature            | View Engine | Ivy        |
| ------------------ | ----------- | ---------- |
| Angular Version    | ≤ Angular 8 | Angular 9+ |
| Bundle Size        | Larger      | Smaller    |
| Build Speed        | Slower      | Faster     |
| Debugging          | Hard        | Easy       |
| Tree Shaking       | Poor        | Excellent  |
| Standalone Support | ❌ No        | ✅ Yes      |
| Future Features    | ❌           | ✅ Yes      |


# 🔹 AOT vs JIT (Compilation Modes)


## ⭐ AOT vs JIT Comparison Table

| Feature          | JIT         | AOT               |
| ---------------- | ----------- | ----------------- |
| Compilation Time | In browser  | Before deployment |
| Startup Speed    | Slower      | Faster            |
| Bundle Size      | Larger      | Smaller           |
| Error Detection  | Runtime     | Build time        |
| Performance      | Lower       | Higher            |
| Use Case         | Development | Production        |

---

## 🌳 What is Tree Shaking?

**Tree shaking is a build-time optimization technique that removes unused code from your application.**

In simple words:
👉 *If you don’t use something, it won’t be included in the final bundle.*

---

## 🤔 Why Is It Called “Tree Shaking”?

Imagine your application as a **tree**:

* Branches = code
* Leaves = functions, classes, components

Tree shaking **shakes the tree** and removes **dead branches** (unused code).

---

## 🎯 Why Tree Shaking Is Important

Without tree shaking:

* Your app ships **extra unused code**
* Bigger bundle size
* Slower load time

With tree shaking:

* Smaller bundles
* Faster startup
* Better performance

This is **critical for large Angular apps**.

---

## ⚙️ How Tree Shaking Works (Internally, Simple)

Tree shaking works in **3 main steps**:

---

### 1️⃣ Static Analysis (at build time)

* The compiler analyzes your imports
* It checks what is **actually used**
* Unused exports are marked as “dead code”

👉 This only works with **ES modules** (`import / export`)

---

### 2️⃣ Compiler + Bundler Cooperation

* Angular (Ivy) + bundler (Webpack / esbuild)
* Removes unused:

  * Components
  * Services
  * Functions
  * Libraries

👉 Code that is never referenced is dropped.

---

### 3️⃣ Final Bundle Creation

* Only **used code** is bundled
* Dead code is completely removed
* Browser never downloads it

---

## 🧠 Why Ivy Is Better at Tree Shaking

Ivy:

* Compiles components independently
* Does not rely heavily on NgModules
* Makes dependencies more explicit

👉 This allows **much finer-grained tree shaking**.

That’s why Angular bundles got **much smaller after Angular 9**.

---

## 🚫 When Tree Shaking Does NOT Work Well

Tree shaking struggles when:

* Code has side effects
* Dynamic imports are unclear
* Everything is imported in one place
* Large “barrel files” are misused

---

#### Quick questions — Introduction

1. What is Angular and how is it different from plain JavaScript?
2. Why is Angular considered a full framework rather than a library?
3. In what scenarios would you choose Angular over React or Vue?
4. What is the difference between SPA and MPA, and how does Angular support SPA?
5. Can you explain Angular architecture at a high level?

---

## 2. Angular Basics

### Angular CLI – Commands with Flags (Simple Guide)

#### What is Angular CLI?

Angular CLI is a **tool** that helps you **create, run, build, test, and manage Angular apps** using simple commands.

#### `ng new` – Create a New App

**Use:** Creates a new Angular project with all setup done.

##### Common Flags

* `--routing` → Adds routing support
* `--style=scss` → Use SCSS instead of CSS
* `--standalone` → Uses modern standalone setup
* `--skip-tests` → Does not create test files
* `--strict` → Enables strict TypeScript rules

👉 Used once at project start.

---

#### `ng serve` – Run the App

**Use:** Runs the app locally for development.

##### Common Flags

* `--open` → Opens browser automatically
* `--port=4201` → Runs app on a specific port
* `--configuration=production` → Run prod build locally
* `--host=0.0.0.0` → Allow access from other devices

👉 Used daily during development.

---

#### `ng build` – Build the App

**Use:** Creates files ready for deployment.

##### Common Flags

* `--configuration=production` → Production build
* `--output-path` → Where build files are saved
* `--source-map` → Enables debugging
* `--stats-json` → Generates build stats

👉 Used before deployment.

---

#### `ng generate` / `ng g` – Create Files

**Use:** Generates Angular building blocks.

##### Common Flags

* `--standalone` → Create standalone component
* `--skip-tests` → Skip test files
* `--flat` → Do not create extra folder
* `--inline-style` → Put styles in TS file
* `--inline-template` → Put HTML in TS file

👉 Keeps structure clean and consistent.

---

#### Common `ng generate` Aliases

| Purpose   | Command   |
| --------- | --------- |
| Component | `ng g c`  |
| Service   | `ng g s`  |
| Guard     | `ng g g`  |
| Pipe      | `ng g p`  |
| Directive | `ng g d`  |
| Module    | `ng g m`  |
| Interface | `ng g i`  |
| Class     | `ng g cl` |
| Enum      | `ng g e`  |

---

#### `ng test` – Run Unit Tests

**Use:** Runs unit tests.

##### Common Flags

* `--watch` → Re-run tests on file changes
* `--code-coverage` → Generate coverage report
* `--browsers` → Choose browser

👉 Used in development and CI.

---

#### `ng lint` – Check Code Quality

**Use:** Finds code style and quality issues.

##### Common Flags

* `--fix` → Automatically fix issues

👉 Helps keep code clean.

---

#### `ng update` – Update Angular

**Use:** Safely updates Angular packages.

##### Common Flags

* `--force` → Force update (not recommended)
* `--next` → Update to next version
* `--allow-dirty` → Update with uncommitted changes

👉 Always preferred over manual updates.

---

#### `ng add` – Add Libraries

**Use:** Adds Angular libraries with configuration.

##### Common Flags

* Library-specific flags
* `--skip-confirmation` → Skip prompts

👉 Used for Angular Material, NgRx, SSR, etc.

---

#### `ng e2e` – End-to-End Tests

**Use:** Runs full app tests simulating real users.

##### Common Flags

* `--configuration` → Choose test config
* `--watch` → Watch mode

👉 Used before major releases.


Below is a **simple, clear, real-world explanation of Angular Project Structure**, written so **beginners understand it** and **interviewers like it**.
No deep theory, no unnecessary details.

---

### Angular Project Structure (Simple Explanation)

Angular project structure is designed to **keep code organized, scalable, and easy to maintain**, especially for **large applications**.

Think of it as **separating responsibilities**.

---

#### High-Level Structure

At the top level, an Angular project looks like this:

```
project-name/
 ├── src/
 ├── angular.json
 ├── package.json
 ├── tsconfig.json
 └── README.md
```

Each part has a **clear purpose**.

---

#### Root Files (Configuration Level)

##### 📄 `package.json`

* Lists project dependencies
* Contains scripts (start, build, test)
* Controls Angular & library versions

👉 Tells **what the project uses**.

---

##### 📄 `angular.json`

* Build configuration
* Environment handling
* Assets & styles setup

👉 Tells Angular **how to build the app**.

---

##### 📄 `tsconfig.json`

* TypeScript configuration
* Controls strictness and compilation

👉 Ensures **type safety**.

---

##### 📄 `README.md`

* Project documentation
* Setup instructions

👉 Helps new developers understand the project.

---

#### 📂 `src/` Folder (Actual Application)

This is where **your application lives**.

```
src/
 ├── index.html
 ├── main.ts
 ├── styles.css
 ├── environments/
 └── app/
```

---

##### 📄 `index.html`

* Single HTML file
* Contains the root Angular tag

👉 Angular renders everything inside this file.

---

##### 📄 `main.ts`

* Entry point of the app
* Starts Angular

👉 This is **where Angular begins**.

---

##### 📄 `styles.css / styles.scss`

* Global styles
* App-wide themes

👉 Component styles are separate.

---

##### 📂 `environments/`

* Environment-specific configuration
* Example: dev, prod URLs

👉 Helps manage **Dev / Stage / Prod** settings.

---

#### 📂 `app/` Folder (MOST IMPORTANT)

This folder contains **application logic**.

A **recommended real-world structure**:

```
app/
 ├── core/
 ├── shared/
 ├── features/
 ├── state/
 ├── app.component.ts
 └── app.routes.ts
```

---

##### `app.component`

* Root component
* Contains layout (header, footer, router outlet)

👉 Should have **minimal logic**.

---

##### `app.routes`

* Central routing configuration
* Defines navigation paths

👉 Controls **which page shows for which URL**.

---

##### `core/` (App-Wide Logic)

Contains things used **once** across the app.

Examples:

* Authentication
* Route guards
* HTTP interceptors
* Global services

👉 Loaded **only once** during app lifetime.

---

##### `shared/` (Reusable Things)

Contains reusable items used in **many places**.

Examples:

* Buttons
* Modals
* Pipes
* Directives
* Models

👉 No business logic here.

---

##### `features/` (Business Features)

Each feature represents a **real business area**.

Examples:

* Login
* Dashboard
* Users
* Orders

👉 Each feature:

* Has its own components
* Can be lazy loaded
* Is easy to scale

---

##### `state/` (State Management)

Contains:

* NgRx state
* Signal stores
* Global state logic

👉 Keeps **state separate from UI**.

---

#### Why This Structure Is Important

* Easy to understand
* Easy to scale
* Team-friendly
* Interview-approved
* Enterprise-ready

---

Below is a **simple, clear, conceptual explanation of `main.ts`**, exactly what it is, **why it exists**, and **what happens inside it** — **no code**, just understanding.

---



### `main.ts` (Explained Simply)

#### What is `main.ts`?

`main.ts` is the **starting point of an Angular application**.

👉 It is the **first file Angular runs** when the app starts.

If Angular were a machine,
**`main.ts` is the power switch**.

---

#### Why `main.ts` is Important

Nothing in Angular works until:

* `main.ts` runs
* Angular is bootstrapped
* The root component is loaded

👉 Without `main.ts`, Angular **cannot start**.

---

#### What Happens in `main.ts` (Conceptually)

When the browser loads your app:

1️⃣ Browser loads compiled JavaScript files
2️⃣ `main.ts` executes first
3️⃣ Angular runtime starts
4️⃣ Angular creates the application environment
5️⃣ Angular loads the **root component**
6️⃣ App becomes interactive

---

#### What `main.ts` Is Responsible For

`main.ts` tells Angular:

* **Which component** is the root component
* **How to start** the application
* **Which global features** are enabled

Examples of what gets configured here (conceptually):

* Routing
* HTTP client
* Global providers
* Change detection mode
* SSR / hydration support

👉 All **app-wide setup** happens here.

---

#### How `main.ts` Fits in the Architecture

```
Browser
  ↓
main.ts
  ↓
Angular Runtime
  ↓
Root Component
  ↓
Router
  ↓
Feature Components
```

#### Old vs Modern Angular (Important Concept)

* **Old Angular**: `main.ts` bootstrapped a module
* **Modern Angular (16/17+)**: `main.ts` bootstraps a **standalone root component**

👉 This makes apps:

* Simpler
* Faster
* Less boilerplate

---

### Angular Bootstrap Process (Simple Explanation)

#### What is the Bootstrap Process?

The **bootstrap process** is how **Angular starts the application** and makes it ready for the user.

👉 In simple words:
**Bootstrap = Angular coming to life**

---

#### High-Level Idea

When a user opens an Angular app:

> Angular loads → initializes itself → creates the first component → shows the UI

That entire startup journey is called **bootstrapping**.

---

#### Bootstrap Process – Step by Step

##### 1️⃣ Browser Loads the App

* Browser loads `index.html`
* Downloads compiled JavaScript files
* Sees a custom HTML tag (like the app’s root tag)

👉 Browser still doesn’t understand Angular yet.

---

##### 2️⃣ `main.ts` Executes

* This is the **first Angular file that runs**
* It tells Angular:
  👉 “Start the application”

---

##### 3️⃣ Angular Runtime Initializes

Angular now:

* Starts its internal engine
* Prepares the dependency injection system
* Sets up change detection
* Prepares the router (if present)

👉 Angular environment is now ready.

---

##### 4️⃣ Root Injector Is Created

* Angular creates the **root dependency injector**
* App-wide services are registered
* Singleton services are prepared

👉 This is how Angular manages services automatically.

---

##### 5️⃣ Root Component Is Created

* Angular creates an instance of the **root component**
* Links it to the custom tag in `index.html`
* Initializes component lifecycle

👉 The first UI appears on screen.

---

##### 6️⃣ Router Takes Control (If Used)

* Router checks the current URL
* Decides which component should be shown
* Loads that component inside the app layout

👉 Still no page reload.

---

##### 7️⃣ Change Detection Starts

* Angular starts watching for:

  * User actions
  * API responses
  * Async events
* UI updates automatically when data changes

👉 App becomes fully interactive.

---

#### Bootstrap Flow (Very Easy View)

```
Browser loads page
   ↓
main.ts runs
   ↓
Angular initializes
   ↓
Root injector created
   ↓
Root component loaded
   ↓
Router loads page
   ↓
UI becomes interactive
```

---

#### Why Bootstrap Process Is Important

Because it:

* Defines how Angular starts
* Controls app initialization order
* Sets up performance, DI, routing
* Ensures consistency in large apps

This is why Angular apps are **predictable and scalable**.

---

### Standalone Components vs NgModules

---

#### What is an NgModule? (Old Angular Way)

##### NgModule is:

A **container** used to group:

* Components
* Directives
* Pipes
* Services

Angular **required NgModules** earlier to tell:

* What belongs together
* What can be used where

👉 Every Angular app **had to start with an AppModule**.

##### Problems with NgModules

* Extra boilerplate
* Hard to understand for beginners
* Complex dependency management
* Indirect imports (hard to trace)

---

#### What are Standalone Components? (Modern Angular Way)

##### Standalone Components are:

Components that **do not need an NgModule**.

Each component:

* Declares its own dependencies
* Is self-contained
* Can be lazy loaded directly

👉 Introduced to **simplify Angular architecture**.

---

#### Key Conceptual Difference

| Aspect             | NgModules    | Standalone      |
| ------------------ | ------------ | --------------- |
| Structure          | Module-based | Component-based |
| Boilerplate        | More         | Less            |
| Learning curve     | Steep        | Easier          |
| Dependency clarity | Indirect     | Explicit        |
| Lazy loading       | Via modules  | Direct          |
| Modern Angular     | ❌ Legacy     | ✅ Preferred     |

---

#### Why Angular Introduced Standalone

Angular introduced standalone components to:

* Reduce complexity
* Remove unnecessary abstractions
* Improve tree shaking
* Simplify lazy loading
* Make Angular easier to learn



#### Quick questions — Angular Basics

1. What is Angular CLI and why is it important in Angular development?
2. Explain the typical Angular project folder structure.
3. What is the role of `main.ts` in an Angular application?
4. What happens during the Angular bootstrap process?
5. What is the difference between Standalone Components and NgModules?

---

## 3. Components

### What is a Component?

A **component** is a **small, reusable part of the user interface** in an Angular application.

👉 In simple words:
**A component controls what you see on the screen and how it behaves.**

---

#### What Does a Component Do?

A component is responsible for:

* Displaying data
* Handling user actions (clicks, input)
* Connecting the UI with application logic

Each screen or section of a screen is usually a **component**.

---

#### What Makes Up a Component (Conceptually)

A component has **three main parts**:

1️⃣ **View (HTML)**

* What the user sees

2️⃣ **Logic (TypeScript)**

* How the component behaves
* Holds data and handles actions

3️⃣ **Styles (CSS/SCSS)**

* How the component looks

👉 Angular ties these three together into **one unit** called a component.

---

#### Why Components Are Important

Components help by:

* Breaking large UIs into small pieces
* Making code reusable
* Making apps easier to understand
* Allowing teams to work independently

Without components, large apps would be **hard to manage**.
---

### Component Metadata

In Angular, **component metadata** is provided using the `@Component` decorator.

This decorator tells Angular **everything it needs to know about a component**.

---

#### Basic Component Metadata Example

```ts
@Component({
  selector: 'app-user',
  templateUrl: './user.component.html',
  styleUrls: ['./user.component.scss']
})
export class UserComponent {
  name = 'John';
}
```

Now let’s break this **slowly and clearly** 👇

---

#### `@Component({...})`

* This is a **decorator**
* It tells Angular:
  👉 “This class is a component”

Without `@Component`, Angular would treat `UserComponent` as a **normal TypeScript class**.

---

#### `selector`

```ts
selector: 'app-user'
```

##### What it means

* Defines **how the component is used in HTML**
* This becomes a **custom HTML tag**

##### Usage in HTML

```html
<app-user></app-user>
```

##### Important rules

* Should be **unique**
* Usually starts with `app-` or company prefix
* Prevents name conflicts

---

#### `templateUrl`

```ts
templateUrl: './user.component.html'
```

##### What it means

* Points to the **HTML file** for this component
* This is what the user sees on screen

##### Why separate file?

* Cleaner code
* Easier to maintain
* Better for large templates

---

#### `styleUrls`

```ts
styleUrls: ['./user.component.scss']
```

##### What it means

* Styles applied **only to this component**
* Angular scopes styles automatically

##### Benefit

* No CSS conflicts
* Styles don’t leak to other components

---

#### Component Class

```ts
export class UserComponent {
  name = 'John';
}
```

##### What it does

* Holds data
* Handles logic
* Responds to user actions

##### Connection to template

```html
<p>{{ name }}</p>
```

Angular binds:

* `name` → UI automatically

---

#### Inline Metadata (Alternative)

Sometimes, template and styles are written **inside the component file**.

```ts
@Component({
  selector: 'app-user',
  template: `<p>{{ name }}</p>`,
  styles: [`p { color: blue; }`]
})
```

##### When to use

* Small components
* Quick demos

##### When NOT to use

* Large templates
* Real enterprise apps

---

#### Other Important Metadata Properties (Conceptual + Example)

##### `standalone`

```ts
standalone: true
```

* Marks component as **standalone**
* No NgModule needed
* Modern Angular approach

---

##### `imports`

```ts
imports: [CommonModule, FormsModule]
```

* Defines what this component depends on
* Makes dependencies **explicit**

---

##### `changeDetection`

```ts
changeDetection: ChangeDetectionStrategy.OnPush
```

* Improves performance
* Angular checks component only when data changes

---

##### `providers`

```ts
providers: [UserService]
```

* Creates a **component-level service**
* Each component gets its own instance

Even if a service is provided in root, adding it to a component’s providers array creates a new instance scoped to that component, overriding the root instance due to Angular’s hierarchical dependency injection.

---

#### How Angular Uses Metadata Internally

When Angular starts:

1. Reads metadata
2. Registers component
3. Links selector to DOM
4. Compiles template
5. Sets up change detection
6. Injects dependencies

👉 Metadata is processed **before the component runs**.

Below is a **clear, step-by-step explanation** of each topic with **small, focused code examples** and **plain-English explanations**. I’ll keep it practical and interview-ready.

---


#### Quick questions — Components

1. What is a component in Angular and why is it important?
2. What is component metadata and why does Angular need it?
3. What is the difference between templates and styles in a component?
4. Explain the Angular component lifecycle in simple terms.
5. What is the difference between `constructor` and `ngOnInit`?

---

## 4. Templates & Data Binding

### Data Binding at a Glance

- **Interpolation**: `{{ value }}` to read data into the view.
- **Property binding**: `[prop]="value"` to set DOM/input properties.
- **Event binding**: `(event)="handler($event)"` to react to user actions.
- **Two-way binding**: `[(ngModel)]="value"` combines property + event binding.
- **Template expressions**: lightweight logic inside bindings (no assignments or side effects).
- **Safe navigation**: `user?.name` to guard against `null`/`undefined`.

### Templates (HTML)

#### What is a Template?

A **template** is the HTML that defines **what the component renders** and **how data/events are bound**.

##### Key ideas

* Displays component data
* Handles user events
* Uses Angular bindings

##### Example

```html
<!-- user.component.html -->
<h2>Hello {{ name }}</h2>
<button (click)="changeName()">Change</button>
```

```ts
export class UserComponent {
  name = 'John';
  changeName() {
    this.name = 'Jane';
  }
}
```

**What’s happening**

* `{{ name }}` → interpolation (read data)
* `(click)` → event binding
* When `name` changes, Angular updates the UI automatically

---

### Styles (CSS/SCSS)

#### What are Component Styles?

Styles defined for a component are **scoped to that component only** (no leaking).

##### Key ideas

* Encapsulation by default
* Safe, conflict-free styling

##### Example

```scss
/* user.component.scss */
h2 {
  color: blue;
}
```

**What’s happening**

* Angular scopes these styles to `UserComponent`
* Other components’ `<h2>` are unaffected

---

### Component Lifecycle

#### What is the Lifecycle?

The **lifecycle** is the sequence of stages a component goes through:
**create → render → update → destroy**.

Below is a **complete explanation of ALL Angular lifecycle hooks**, with **simple meaning**, **when they run**, and **small code examples**.
I’ll keep it **clear, practical, and interview-ready**.

---

Angular lifecycle hooks are **methods Angular calls automatically** at specific moments in a component’s life.

Think of them as **checkpoints** from creation → update → destruction.

---

#### Lifecycle Order (Important)

```
constructor
ngOnChanges
ngOnInit
ngDoCheck
ngAfterContentInit
ngAfterContentChecked
ngAfterViewInit
ngAfterViewChecked
ngOnDestroy
```

---

#### 1️⃣ `constructor` (NOT a lifecycle hook, but important)

##### Purpose

* Create the component instance
* Inject dependencies

```ts
constructor(private userService: UserService) {}
```

##### Key points

* Runs first
* No access to inputs
* ❌ Don’t call APIs here

📌 Use only for **dependency injection**

---

#### 2️⃣ `ngOnChanges`

##### When it runs

* When an **@Input() value changes**
* Runs **before ngOnInit**
* Can run multiple times

```ts
ngOnChanges(changes: SimpleChanges) {
  console.log(changes);
}
```

##### Use case

* React to input changes from parent
* Compare previous vs current values

---

#### 3️⃣ `ngOnInit`

##### When it runs

* Once after component initialization
* After first `ngOnChanges`

```ts
ngOnInit() {
  this.loadUsers();
}
```

##### Use case

* API calls
* Initial data setup
* Subscriptions

📌 **Most commonly used hook**

---

#### 4️⃣ `ngDoCheck`

##### When it runs

* On **every change detection cycle**

```ts
ngDoCheck() {
  console.log('Change detected');
}
```

##### Use case

* Custom change detection logic
* Rarely used

⚠️ Can hurt performance if misused

---

#### 5️⃣ `ngAfterContentInit`

##### When it runs

* Once after **content projection** (`ng-content`) is initialized

```ts
ngAfterContentInit() {
  console.log('Content initialized');
}
```

##### Use case

* Work with projected content

---

#### 6️⃣ `ngAfterContentChecked`

##### When it runs

* After projected content is checked
* Runs multiple times

```ts
ngAfterContentChecked() {}
```

##### Use case

* Rare
* Avoid heavy logic

---

#### 7️⃣ `ngAfterViewInit`

##### When it runs

* Once after component **view & child views** are initialized

```ts
ngAfterViewInit() {
  this.inputElement.focus();
}
```

##### Use case

* DOM access
* ViewChild initialization
* Third-party UI libraries

📌 Best place for **direct DOM interaction**

---

#### 8️⃣ `ngAfterViewChecked`

##### When it runs

* After every check of component view

```ts
ngAfterViewChecked() {}
```

##### Use case

* Very rare
* Debugging view updates

⚠️ Avoid logic here (performance risk)

---

#### 9️⃣ `ngOnDestroy`

##### When it runs

* Just before component is destroyed

```ts
ngOnDestroy() {
  this.subscription.unsubscribe();
}
```

##### Use case

* Cleanup
* Unsubscribe observables
* Clear timers
* Prevent memory leaks


#### `constructor` vs `ngOnInit`

##### `constructor`

**Purpose:** Create the class instance & inject dependencies.

```ts
constructor(private userService: UserService) {
  // ❌ Avoid heavy logic here
}
```

* Runs **first**
* Used for **dependency injection**
* Should be lightweight

---

##### `ngOnInit`

**Purpose:** Initialize component logic.

```ts
ngOnInit() {
  this.loadUsers();
}
```

* Runs **after Angular sets inputs**
* Best place for:

  * API calls
  * Initialization logic
  * Subscriptions

##### Simple rule (remember this)

> **constructor = setup**
> **ngOnInit = work**

---

#### Change Detection (Basics)

##### What is Change Detection?

Change detection is how Angular **keeps the UI in sync with data**.

Whenever something changes:

* User clicks
* API returns data
* Timer fires

Angular:

1. Checks component values
2. Updates the DOM **only where needed**

---

##### Example

```ts
count = 0;

increment() {
  this.count++;
}
```

```html
<p>{{ count }}</p>
<button (click)="increment()">+</button>
```

**What’s happening**

* Button click changes `count`
* Angular detects the change
* Updates only the `<p>`

---

### Default vs Optimized (conceptual)

* **Default**: Angular checks frequently (safe, simple)
* **OnPush**: Angular checks only when inputs change (faster)

Below is a **clear, practical explanation** of **directives** with **code where required**, explained **step by step**, and **real-world focused**.
I’ll start from basics and build up logically.

---


#### Quick questions — Templates & Data Binding

1. What is interpolation in Angular and when do you use it?
2. What is the difference between property binding and event binding?
3. How does two-way data binding work in Angular?
4. What are template expressions and what rules do they follow?
5. What is the safe navigation operator and why is it used?

---

## 5. Directives

### Directives in Angular

#### What is a Directive?

A **directive** is a class that **changes the behavior or appearance of the DOM**.

👉 In simple words:
**Directives tell Angular how to manipulate HTML elements.**

Angular has **two main types**:

1. **Attribute directives**
2. **Structural directives**

---

### Attribute Directives

#### What are Attribute Directives?

Attribute directives **modify the appearance or behavior of an existing element**.

✔ They **do NOT add or remove elements**
✔ They **change how an element looks or behaves**

---

#### Built-in Attribute Directives

##### `ngClass`

Dynamically adds/removes CSS classes.

```html
<p [ngClass]="{ active: isActive }">User status</p>
```

📌 Used for:

* Active/inactive states
* Error highlighting

---

##### `ngStyle`

Applies styles dynamically.

```html
<p [ngStyle]="{ color: isError ? 'red' : 'green' }">
  Status
</p>
```

📌 Used for:

* Dynamic colors
* Conditional styling

---

### Structural Directives

#### What are Structural Directives?

Structural directives **change the structure of the DOM**.

✔ They **add or remove elements**
✔ They start with `*`

👉 They control **what exists in the DOM**

---

#### Why `*` (Asterisk)?

The `*` is **syntactic sugar**.
It tells Angular:

> “This directive will change the DOM structure”

Internally, Angular rewrites it using `<ng-template>`.

---

### Built-in Structural Directives

---

#### `*ngIf`

##### Purpose

Conditionally **add or remove elements**.

```html
<p *ngIf="isLoggedIn">Welcome back!</p>
```

##### What happens internally

* If `true` → element is created
* If `false` → element is destroyed

📌 Best for:

* Auth-based UI
* Conditional sections

---

#### `*ngFor`

##### Purpose

Render a list dynamically.

```html
<li *ngFor="let user of users; let i = index">
  {{ i + 1 }} - {{ user.name }}
</li>
```

### Common variables

* `index`
* `first`
* `last`
* `even`
* `odd`

📌 Best for:

* Lists
* Tables
* Menus

---

## ✅ `*ngSwitch`

### Purpose

Display elements based on multiple conditions.

```html
<div [ngSwitch]="role">
  <p *ngSwitchCase="'admin'">Admin Panel</p>
  <p *ngSwitchCase="'user'">User Dashboard</p>
  <p *ngSwitchDefault>Guest</p>
</div>
```

📌 Cleaner than multiple `*ngIf`

---

# 4️⃣ Custom Attribute Directive

## 🔹 When do we need it?

When you want to **change behavior or style** of elements **reusably**.

### Example: Highlight element on hover

### Directive

```ts
@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective {
  constructor(private el: ElementRef) {}

  @HostListener('mouseenter')
  onEnter() {
    this.el.nativeElement.style.backgroundColor = 'yellow';
  }

  @HostListener('mouseleave')
  onLeave() {
    this.el.nativeElement.style.backgroundColor = '';
  }
}
```

##### Usage

```html
<p appHighlight>Hover me</p>
```

📌 Real-life uses:

* Highlight invalid fields
* Role-based styling
* Hover effects

---

# 5️⃣ Custom Structural Directive

## 🔹 When do we need it?

When you want to **add/remove elements based on custom logic**.

### Example: `*appIfAdmin`

### Directive

```ts
@Directive({
  selector: '[appIfAdmin]'
})
export class IfAdminDirective {
  constructor(
    private templateRef: TemplateRef<any>,
    private viewContainer: ViewContainerRef
  ) {}

  @Input() set appIfAdmin(isAdmin: boolean) {
    this.viewContainer.clear();
    if (isAdmin) {
      this.viewContainer.createEmbeddedView(this.templateRef);
    }
  }
}
```

### Usage

```html
<button *appIfAdmin="isAdmin">Delete User</button>
```

📌 Real-life uses:

* Role-based UI
* Feature flags
* Permission control

---

# 🔁 Attribute vs Structural (Easy Comparison)

| Feature                     | Attribute Directive | Structural Directive |
| --------------------------- | ------------------- | -------------------- |
| Changes DOM structure       | ❌                   | ✅                    |
| Changes appearance/behavior | ✅                   | ❌                    |
| Uses `*`                    | ❌                   | ✅                    |
| Example                     | `ngClass`           | `ngIf`               |

---

## 🎯 Interview-Ready Summary

* **Attribute directives** change how elements look or behave
* **Structural directives** add or remove elements from the DOM
* `*ngIf`, `*ngFor`, `*ngSwitch` are built-in structural directives
* Custom directives help build reusable UI logic

---


#### Quick questions — Directives

1. What is a directive and why are directives important in Angular?
2. What is the difference between attribute and structural directives?
3. How does `*ngIf` work internally compared to hiding elements with CSS?
4. What is the purpose of `*ngFor` and why is `trackBy` important?
5. When would you create a custom directive, and what problem does it solve?

---

Below is a **clear, practical explanation of Pipes in Angular**, with **code examples**, **simple language**, and **interview-ready points**.

---
## 6. Pipes

### Pipes in Angular

#### What is a Pipe?

A **pipe** is used to **transform data before displaying it in the template**.

👉 Pipes **do not change the actual data**, only how it appears in the UI.

Think of pipes as **formatters for display**.

---

#### Why Pipes Are Useful

* Keep templates clean
* Avoid formatting logic in components
* Reuse display logic
* Improve readability

---

### Built-in Pipes

Angular provides many **ready-to-use pipes**.

---

#### Common Built-in Pipes

##### `date`

Formats dates.

```html
<p>{{ today | date:'shortDate' }}</p>
```

📌 Used for showing readable dates.

---

##### `uppercase` / `lowercase`

Changes text case.

```html
<p>{{ name | uppercase }}</p>
```

---

##### `currency`

Formats numbers as currency.

```html
<p>{{ price | currency:'USD' }}</p>
```

---

##### `percent`

Formats numbers as percentages.

```html
<p>{{ progress | percent }}</p>
```

---

##### `slice`

Extracts part of a string or array.

```html
<p>{{ title | slice:0:5 }}</p>
```

---

##### `async`

Handles observables or promises automatically.

```html
<p>{{ users$ | async }}</p>
```

📌 Automatically subscribes and unsubscribes
📌 Very important for memory safety

---

### Custom Pipes

#### When Do We Need Custom Pipes?

When:

* Built-in pipes are not enough
* You want reusable formatting logic
* Logic is **only for display**, not business rules

---

#### Example: Custom Pipe (Title Case)

##### Pipe

```ts
@Pipe({
  name: 'titleCase'
})
export class TitleCasePipe implements PipeTransform {
  transform(value: string): string {
    return value
      .split(' ')
      .map(word => word[0].toUpperCase() + word.slice(1))
      .join(' ');
  }
}
```

### Usage

```html
<p>{{ 'angular pipes are useful' | titleCase }}</p>
```

📌 Output:
**Angular Pipes Are Useful**

---

#### Important Rule

> **Use pipes only for UI formatting**
> ❌ Do NOT put heavy business logic in pipes

---

### Pure vs Impure Pipes (VERY IMPORTANT)

---

#### Pure Pipes (Default)

##### What they are

* Run **only when input value changes**
* Faster and more efficient

```ts
@Pipe({
  name: 'pureExample',
  pure: true // default
})
```

##### When Angular runs them

* Primitive value changes
* Object reference changes

📌 Best for:

* Formatting
* Filtering
* Sorting display data

---

#### Impure Pipes

##### What they are

* Run **on every change detection**
* Slower

```ts
@Pipe({
  name: 'impureExample',
  pure: false
})
```

##### When Angular runs them

* Every UI update
* Even when input hasn’t changed

📌 Use carefully!

---

#### Why Impure Pipes Are Dangerous

* Run very frequently
* Can cause performance issues
* Should be lightweight

📌 Use impure pipes only when:

* Data mutates without reference change
* You fully understand performance impact

---

### Pure vs Impure (Easy Table)

| Feature     | Pure Pipe     | Impure Pipe            |
| ----------- | ------------- | ---------------------- |
| Default     | ✅ Yes         | ❌ No                   |
| Runs when   | Input changes | Every change detection |
| Performance | Fast          | Slow                   |
| Use case    | Formatting    | Special edge cases     |

---

#### Quick questions — Pipes

1. What is a pipe in Angular and why is it used?
2. Name some commonly used built-in pipes and their purpose.
3. When would you create a custom pipe?
4. What is the difference between pure and impure pipes?
5. Why can impure pipes negatively affect application performance?

---

## 🎯 Bonus: Common Follow-Up Questions

* Where should heavy logic go: component, pipe, or service?
* How does Angular keep the UI in sync with data?
* What mistakes do beginners commonly make in Angular fundamentals?
* How does Angular ensure scalability for large applications?
* What Angular fundamentals matter most in real projects?


# Phase 2 — Advanced Angular

## Outline
- [1. Dependency Injection (DI)](#1-dependency-injection-di)
  - [What is Dependency Injection?](#1-what-is-dependency-injection-di)
  - [Injectable Services](#2-injectable-services)
  - [Provider Scopes](#3-provider-scopes-very-important)
  - [`providedIn` options](#4-providedin-root--platform--any)
  - [DI Hierarchy](#5-di-hierarchy-critical-concept)
  - [DI Under the Hood](#6-di-under-the-hood-how-angular-actually-does-it)
  - [Real-World Example](#7-real-world-example)
  - [Interview-Ready One-Liners](#8-interview-ready-one-liners)
- [2. Routing & Navigation](#2-routing--navigation)
  - [What Routing Is](#what-routing-is-quick)
  - [Router Setup](#1-router-setup-foundation)
  - [RouterOutlet](#2-routeroutlet-where-pages-render)
  - [Navigation from HTML](#3-navigation-from-html-declarative)
  - [Navigation from TypeScript](#4-navigation-from-typescript-programmatic)
  - [Reading Route Data](#5-reading-route-data)
  - [Route Guards](#6-route-guards-security--rules)
  - [Lazy Loading](#7-lazy-loading-performance)
  - [Preloading Strategies](#8-preloading-strategies-faster-subsequent-loads)
  - [Typical Navigation Flow](#9-typical-navigation-flow-end-to-end)
  - [HTML vs TS Navigation](#html-vs-ts-navigation-quick-compare)
- [3. Angular Forms](#3-angular-forms)
  - [Template-Driven Forms](#1-template-driven-forms)
  - [Reactive Forms](#2-reactive-forms-recommended)
  - [FormControl](#3-formcontrol)
  - [FormGroup](#4-formgroup)
  - [FormArray](#5-formarray)
  - [Validators](#6-validators-built-in)
  - [Custom Validators](#7-custom-validators)
  - [Async Validators](#8-async-validators)
  - [Conditional Forms](#9-conditional-forms)
  - [Dynamic Forms](#10-dynamic-forms)
  - [Form Best Practices](#11-form-best-practices-very-important)
  - [Template vs Reactive Comparison](#template-vs-reactive-quick-comparison)
  - [Interview-Ready One-Liners](#interview-ready-one-liners-1)

---

## 1. Dependency Injection (DI)

### 1. What is Dependency Injection (DI)?

### Simple meaning

**Dependency Injection is a design pattern where Angular creates and provides objects (services) instead of you creating them manually.**

👉 You *ask* for what you need, Angular *gives* it to you.

---

### Why DI exists

Without DI:

* Components create their own dependencies
* Tight coupling
* Hard to test
* Hard to reuse

With DI:

* Loose coupling
* Easy testing
* Reusable services
* Cleaner architecture

---

### Simple example (conceptual)

> Component needs UserService
> Component does NOT create UserService
> Angular creates UserService and injects it

---

### 2. Injectable Services

### What is an Injectable Service?

A **service** is a class that contains:

* Business logic
* API calls
* Shared data

`@Injectable()` tells Angular:

> “This class can be injected using DI”

---

### Example

```ts
@Injectable({
  providedIn: 'root'
})
export class UserService {
  getUsers() {
    return ['Alice', 'Bob'];
  }
}
```

📌 `@Injectable` makes the class available to Angular’s DI system.

---

### Using the service in a component

```ts
constructor(private userService: UserService) {}
```

👉 You did not create `UserService`
👉 Angular injected it

---

### 3. Provider Scopes (VERY IMPORTANT)

Provider scope defines:

> **Where and how many instances of a service are created**

Angular has **multiple scopes**.

---

### 🔹 Component-level Provider

```ts
@Component({
  providers: [UserService]
})
```

**Behavior**

* New instance per component
* Destroyed when component is destroyed
* NOT shared

📌 Use when data must be **isolated**

---

### 🔹 Root-level Provider

```ts
@Injectable({
  providedIn: 'root'
})
```

**Behavior**

* Single instance for entire app
* Shared everywhere
* Created during app bootstrap

📌 Most common & recommended

---

### 4. `providedIn: root / platform / any`

This controls **where Angular registers the service**.

---

### 🔹 `providedIn: 'root'` ✅ (Most used)

```ts
@Injectable({ providedIn: 'root' })
```

* One instance for whole app
* Tree-shakable
* Best for:

  * AuthService
  * API services
  * Global state

---

### 🔹 `providedIn: 'platform'`

```ts
@Injectable({ providedIn: 'platform' })
```

* One instance shared across **multiple Angular apps**
* Rarely used
* Used in:

  * Micro-frontend platforms
  * Shared runtime services

---

### 🔹 `providedIn: 'any'`

```ts
@Injectable({ providedIn: 'any' })
```

* New instance per **lazy-loaded module**
* Shared within that module only

📌 Useful when:

* Each lazy module needs its own instance

⚠️ Less common today with standalone APIs

---

### 🔁 Quick Comparison

| Scope    | Instance | Shared?         | Use case          |
| -------- | -------- | --------------- | ----------------- |
| root     | One      | Entire app      | Global services   |
| platform | One      | Across apps     | Platform services |
| any      | Multiple | Per lazy module | Module isolation  |

---

### 5. DI Hierarchy (CRITICAL CONCEPT)

Angular resolves dependencies using a **hierarchical injector tree**.

### Injector order:

```
Component Injector
   ↓
Route / Module Injector
   ↓
Root Injector
   ↓
Platform Injector
```

---

### What this means

* Angular looks **locally first**
* If not found → goes up the tree
* Closest provider wins

---

### Example

If:

* Service is provided in component
* Also provided in root

👉 Angular uses the **component instance**, not root

---

### 6. DI Under the Hood (How Angular Actually Does It)

### Internally Angular:

1. Reads `@Injectable` metadata
2. Registers provider in injector
3. Creates service instance **only when needed**
4. Caches instance based on scope
5. Injects instance via constructor

---

### Important internals

* DI uses **tokens** (class = token)
* Uses metadata generated by Ivy
* Services are **lazy-instantiated**
* Destroyed when their injector is destroyed

---

### Why this is powerful

* No manual object creation
* Automatic lifecycle handling
* Easy mocking for tests
* High performance

---

### 7. Real-World Example

### AuthService

* Provided in `root`
* Shared across app
* Holds logged-in user state

### CartService (per feature)

* Provided in component or route
* Each feature has its own cart
* Destroyed when feature exits

---

### 8. Interview-Ready One-Liners

* **What is DI?**

  > Dependency Injection is a pattern where Angular provides required dependencies instead of components creating them manually.

* **Why DI?**

  > DI improves reusability, testability, and separation of concerns.

* **Hierarchy?**

  > Angular resolves dependencies using a hierarchical injector tree where the closest provider wins.

* **providedIn root vs any?**

  > `root` creates a singleton app-wide service, while `any` creates separate instances per lazy-loaded module.

---

## 2. Routing & Navigation

### What Routing Is (Quick)

Angular Routing maps **URLs → components** so users can navigate the app **without page reloads** (SPA behavior).

---

### 1. Router Setup (Foundation)

### Routes configuration

```ts
// app.routes.ts
import { Routes } from '@angular/router';
import { HomeComponent } from './home.component';
import { UsersComponent } from './users.component';
import { UserDetailComponent } from './user-detail.component';

export const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'users', component: UsersComponent },
  { path: 'users/:id', component: UserDetailComponent },
  { path: 'admin', loadComponent: () => import('./admin.component').then(m => m.AdminComponent) }
];
```

### Provide the router at bootstrap

```ts
// main.ts
import { bootstrapApplication } from '@angular/platform-browser';
import { provideRouter, withPreloading, PreloadAllModules } from '@angular/router';
import { AppComponent } from './app.component';
import { routes } from './app.routes';

bootstrapApplication(AppComponent, {
  providers: [provideRouter(routes, withPreloading(PreloadAllModules))]
});
```

**Why this matters**

* Centralizes navigation rules
* Enables lazy loading and preloading
* Keeps SPA navigation fast

---

### 2. RouterOutlet (Where pages render)

```html
<!-- app.component.html -->
<header>
  <a routerLink="/">Home</a>
  <a routerLink="/users" routerLinkActive="active">Users</a>
  <a routerLink="/admin" routerLinkActive="active">Admin</a>
</header>

<router-outlet></router-outlet>
```

**Key idea**
`<router-outlet>` is a **placeholder**. Angular creates/destroys routed components here.

---

### 3. Navigation from HTML (Declarative)

### Basic links

```html
<a routerLink="/">Home</a>
<a routerLink="/users">Users</a>
```

### With route params

```html
<a [routerLink]="['/users', user.id]">View User</a>
```

### With query params

```html
<a [routerLink]="['/users']"
   [queryParams]="{ page: 2, sort: 'name' }">
  Users (Page 2)
</a>
```

### Active route styling

```html
<a routerLink="/users" routerLinkActive="active">Users</a>
```

**When to use HTML navigation**

* Menus, links, simple buttons
* No conditional logic needed

---

### 4. Navigation from TypeScript (Programmatic)

### Inject the Router

```ts
import { Router } from '@angular/router';

constructor(private router: Router) {}
```

### Simple navigation

```ts
goToUsers() {
  this.router.navigate(['/users']);
}
```

```html
<button (click)="goToUsers()">Go to Users</button>
```

### With route params

```ts
viewUser(id: number) {
  this.router.navigate(['/users', id]);
}
```

### With query params

```ts
goToUsersPage() {
  this.router.navigate(['/users'], {
    queryParams: { page: 1, sort: 'date' }
  });
}
```

### Conditional navigation (very common)

```ts
loginSuccess() {
  this.router.navigate(['/dashboard']);
}
```

**When to use TS navigation**

* After form submit
* After API success
* Auth redirects
* Conditional flows

By default, Angular **replaces** existing query parameters when navigating.

```ts
this.router.navigate(['/users'], {
  queryParams: { page: 1 }
});
```

👉 Old query params are **lost**.

---

### 🔹 What does **`merge`** do?

```ts
this.router.navigate(['/users'], {
  queryParams: { page: 1 },
  queryParamsHandling: 'merge'
});
```

👉 **Keeps existing query params** and **adds/updates new ones**.

---

### Example

Current URL:

```
/users?filter=active
```

After navigation:

```
/users?filter=active&page=1
```

---

### 🔁 Options (Easy to Remember)

| Option     | Meaning        |
| ---------- | -------------- |
| default    | Replace params |
| `merge`    | Keep + update  |
| `preserve` | Keep only      |


---

### 5. Reading Route Data

### Route params

```ts
import { ActivatedRoute } from '@angular/router';

constructor(private route: ActivatedRoute) {
  const id = this.route.snapshot.paramMap.get('id');
}
```

### Query params (reactive)

```ts
this.route.queryParams.subscribe(params => {
  console.log(params['page'], params['sort']);
});
```

**Rule of thumb**

* **Route params** → required identifiers
* **Query params** → optional filters/sorting/pagination

---

### 6. Route Guards (Security & Rules)

### CanActivate guard

```ts
import { CanActivateFn } from '@angular/router';

export const authGuard: CanActivateFn = () => {
  const isLoggedIn = true; // replace with real auth check
  return isLoggedIn;
};
```

### Apply the guard

```ts
{ path: 'admin', component: AdminComponent, canActivate: [authGuard] }
```

**Use guards to**

* Protect routes
* Enforce permissions
* Prevent navigation

---

### 7. Lazy Loading (Performance)

### Lazy-load a standalone component

```ts
{
  path: 'admin',
  loadComponent: () =>
    import('./admin.component').then(m => m.AdminComponent)
}
```

### Lazy-load route groups

```ts
{
  path: 'shop',
  loadChildren: () =>
    import('./shop.routes').then(m => m.shopRoutes)
}
```

**Why**

* Smaller initial bundle
* Faster startup

---

### 8. Preloading Strategies (Faster Subsequent Loads)

```ts
import { PreloadAllModules } from '@angular/router';

provideRouter(routes, withPreloading(PreloadAllModules));
```

**Options**

* `NoPreloading` (default)
* `PreloadAllModules` (recommended for many apps)
* Custom strategies (advanced)

---

### 9. Typical Navigation Flow (End-to-End)

1. User clicks a link (`routerLink`) **or** code calls `router.navigate`
2. Router checks **guards**
3. Loads component (lazy if needed)
4. Renders it in `<router-outlet>`
5. Updates URL (no reload)

---

### HTML vs TS Navigation (Quick Compare)

| Aspect      | HTML (`routerLink`) | TS (`router.navigate`) |
| ----------- | ------------------- | ---------------------- |
| Simplicity  | ✅                   | ❌                      |
| Logic-based | ❌                   | ✅                      |
| Best for    | Menus & links       | Auth, forms, redirects |

---


## 3. Angular Forms

### Overview

Angular provides **two form approaches**:

1. **Template-driven forms** (simple, HTML-focused)
2. **Reactive forms** (powerful, scalable, TypeScript-focused)

---

### 1. Template-Driven Forms

### What they are

Forms driven mostly by **HTML templates** with minimal TypeScript.

### When to use

* Simple forms
* Few fields
* Less dynamic behavior

---

### Example: Simple Login Form (Template-driven)

#### HTML

```html
<form #loginForm="ngForm" (ngSubmit)="onSubmit(loginForm)">
  <input
    name="email"
    ngModel
    required
    email
    placeholder="Email" />

  <input
    name="password"
    ngModel
    required
    minlength="6"
    type="password"
    placeholder="Password" />

  <button type="submit" [disabled]="loginForm.invalid">
    Login
  </button>
</form>
```

#### Component

```ts
onSubmit(form: any) {
  console.log(form.value);
}
```

### Key points

* Uses `ngModel`
* Validation defined in HTML
* Less control for complex cases

---

### 2. Reactive Forms (Recommended)

### What they are

Forms fully controlled in **TypeScript** using form objects.

### When to use

* Large forms
* Dynamic fields
* Complex validation
* Enterprise apps

---

### 3. FormControl

### What it is

Represents **a single form field**.

```ts
import { FormControl } from '@angular/forms';

name = new FormControl('');
```

### With validation

```ts
name = new FormControl('', Validators.required);
```

---

### 4. FormGroup

### What it is

A **group of FormControls** (entire form).

---

### Example: Registration Form

```ts
import { FormGroup, FormControl, Validators } from '@angular/forms';

form = new FormGroup({
  username: new FormControl('', Validators.required),
  email: new FormControl('', [Validators.required, Validators.email]),
  password: new FormControl('', Validators.minLength(6))
});
```

#### HTML

```html
<form [formGroup]="form" (ngSubmit)="submit()">
  <input formControlName="username" />
  <input formControlName="email" />
  <input type="password" formControlName="password" />

  <button [disabled]="form.invalid">Submit</button>
</form>
```

---

### 5. FormArray

### What it is

Used for **dynamic lists of controls** (add/remove fields).

---

### Example: Skills Form

```ts
import { FormArray, FormBuilder } from '@angular/forms';

constructor(private fb: FormBuilder) {}

form = this.fb.group({
  name: [''],
  skills: this.fb.array([])
});

get skills() {
  return this.form.get('skills') as FormArray;
}

addSkill() {
  this.skills.push(this.fb.control(''));
}
```

#### HTML

```html
<div formArrayName="skills">
  <div *ngFor="let skill of skills.controls; let i = index">
    <input [formControlName]="i" />
  </div>
</div>

<button (click)="addSkill()">Add Skill</button>
```

---

### 6. Validators (Built-in)

### Common Validators

```ts
Validators.required
Validators.email
Validators.minLength(6)
Validators.maxLength(20)
Validators.pattern(/^[A-Z]+$/)
```

### Usage

```ts
email: ['', [Validators.required, Validators.email]]
```

---

### 7. Custom Validators

### When to use

* Business-specific rules
* Cross-field validation

---

### Example: Password Match Validator

```ts
import { AbstractControl } from '@angular/forms';

export function passwordMatchValidator(control: AbstractControl) {
  const password = control.get('password')?.value;
  const confirm = control.get('confirmPassword')?.value;

  return password === confirm ? null : { passwordMismatch: true };
}
```

#### Apply to FormGroup

```ts
this.form = this.fb.group(
  {
    password: [''],
    confirmPassword: ['']
  },
  { validators: passwordMatchValidator }
);
```

---

### 8. Async Validators

### What they are

Validators that run **asynchronously** (API calls).

---

### Example: Username Availability

```ts
import { AbstractControl } from '@angular/forms';
import { map } from 'rxjs/operators';

usernameValidator(control: AbstractControl) {
  return this.userService.checkUsername(control.value).pipe(
    map(isTaken => (isTaken ? { usernameTaken: true } : null))
  );
}
```

```ts
username: ['', null, this.usernameValidator.bind(this)]
```

---

### 9. Conditional Forms

### Example: Company Field Only for Business Users

```ts
this.form = this.fb.group({
  type: ['personal'],
  company: ['']
});

this.form.get('type')?.valueChanges.subscribe(type => {
  const company = this.form.get('company');
  if (type === 'business') {
    company?.setValidators(Validators.required);
  } else {
    company?.clearValidators();
  }
  company?.updateValueAndValidity();
});
```

---

### 10. Dynamic Forms

### What they are

Forms created **from configuration or API data**.

---

### Example: Build from Config

```ts
fields = [
  { name: 'email', validators: [Validators.required, Validators.email] },
  { name: 'password', validators: [Validators.required] }
];

form = this.fb.group(
  this.fields.reduce((acc: any, field) => {
    acc[field.name] = ['', field.validators];
    return acc;
  }, {})
);
```

📌 Used in:

* Survey builders
* Admin panels
* CMS systems

---

### 11. Form Best Practices (VERY IMPORTANT)

### ✅ Do

* Prefer **Reactive Forms**
* Keep logic in TS, not templates
* Use custom validators for business rules
* Unsubscribe from `valueChanges` if needed
* Use `FormBuilder` for cleaner code

---

### ❌ Avoid

* Heavy logic in templates
* Using `any` for forms
* Overusing template-driven forms
* Mixing template-driven & reactive in same form

---

### Template vs Reactive (Quick Comparison)

| Feature        | Template-driven | Reactive   |
| -------------- | --------------- | ---------- |
| Control        | Low             | High       |
| Scalability    | ❌               | ✅          |
| Dynamic forms  | ❌               | ✅          |
| Validation     | HTML            | TypeScript |
| Enterprise use | ❌               | ✅          |

---


### ✅ Common `FormControl` Methods — Quick Reference Table

| Method                     | Example Code                                 | What it Does                                              |
| -------------------------- | -------------------------------------------- | --------------------------------------------------------- |
| `setValue()`               | `control.setValue('test@mail.com')`          | Sets the value exactly; errors if structure doesn’t match |
| `patchValue()`             | `control.patchValue('test@mail.com')`        | Safely updates the value (partial update allowed)         |
| `reset()`                  | `control.reset()`                            | Resets value, validation state, and flags                 |
| `disable()`                | `control.disable()`                          | Disables the control; excluded from `form.value`          |
| `enable()`                 | `control.enable()`                           | Enables a disabled control                                |
| `setValidators()`          | `control.setValidators(Validators.required)` | Replaces existing validators                              |
| `addValidators()`          | `control.addValidators(Validators.email)`    | Adds validators without removing existing ones            |
| `clearValidators()`        | `control.clearValidators()`                  | Removes all validators                                    |
| `updateValueAndValidity()` | `control.updateValueAndValidity()`           | Re-runs validation and updates status                     |
| `markAsTouched()`          | `control.markAsTouched()`                    | Marks control as touched (for showing errors)             |
| `markAsDirty()`            | `control.markAsDirty()`                      | Marks control as modified                                 |
| `markAsPristine()`         | `control.markAsPristine()`                   | Marks control as not modified                             |
| `markAsUntouched()`        | `control.markAsUntouched()`                  | Marks control as untouched                                |
| `hasError()`               | `control.hasError('required')`               | Checks if a specific validation error exists              |
| `getRawValue()`            | `form.getRawValue()`                         | Gets values including disabled controls                   |
| `valueChanges`             | `control.valueChanges.subscribe()`           | Emits value changes (Observable)                          |
| `statusChanges`            | `control.statusChanges.subscribe()`          | Emits status changes (VALID / INVALID / PENDING)          |

Perfect 👍
Below are **ALL remaining tables** you asked for — **clear, compact, interview-ready**, and **real-world focused**.

---

### ✅ `FormGroup` Methods — Quick Reference Table

| Method                     | Example Code                                 | What it Does                                            |
| -------------------------- | -------------------------------------------- | ------------------------------------------------------- |
| `setValue()`               | `form.setValue({name:'A', email:'a@b.com'})` | Sets values for **all controls** (exact match required) |
| `patchValue()`             | `form.patchValue({email:'a@b.com'})`         | Updates **partial values safely**                       |
| `reset()`                  | `form.reset()`                               | Resets all controls and states                          |
| `get()`                    | `form.get('email')`                          | Gets a specific control                                 |
| `disable()`                | `form.disable()`                             | Disables entire form                                    |
| `enable()`                 | `form.enable()`                              | Enables entire form                                     |
| `setValidators()`          | `form.setValidators(customValidator)`        | Sets group-level validators                             |
| `clearValidators()`        | `form.clearValidators()`                     | Removes group validators                                |
| `updateValueAndValidity()` | `form.updateValueAndValidity()`              | Re-runs validation                                      |
| `hasError()`               | `form.hasError('passwordMismatch')`          | Checks group-level error                                |
| `markAllAsTouched()`       | `form.markAllAsTouched()`                    | Marks all fields touched                                |
| `valueChanges`             | `form.valueChanges.subscribe()`              | Emits form value changes                                |
| `statusChanges`            | `form.statusChanges.subscribe()`             | Emits form status changes                               |

---

### ✅ `FormArray` Methods — Quick Reference Table

| Method         | Example Code                          | What it Does             |
| -------------- | ------------------------------------- | ------------------------ |
| `push()`       | `skills.push(new FormControl('JS'))`  | Adds a new control       |
| `insert()`     | `skills.insert(1, new FormControl())` | Inserts control at index |
| `removeAt()`   | `skills.removeAt(0)`                  | Removes control at index |
| `clear()`      | `skills.clear()`                      | Removes all controls     |
| `at()`         | `skills.at(0)`                        | Gets control at index    |
| `length`       | `skills.length`                       | Number of controls       |
| `setValue()`   | `skills.setValue(['JS','TS'])`        | Sets values exactly      |
| `patchValue()` | `skills.patchValue(['JS'])`           | Partial update           |
| `reset()`      | `skills.reset()`                      | Resets array             |
| `disable()`    | `skills.disable()`                    | Disables all controls    |
| `enable()`     | `skills.enable()`                     | Enables all controls     |

---

### ✅ Form Control States — What They Mean

| State       | Meaning                      |
| ----------- | ---------------------------- |
| `valid`     | Control passes validation    |
| `invalid`   | Validation failed            |
| `pending`   | Async validation running     |
| `touched`   | User focused & blurred field |
| `untouched` | User never touched field     |
| `dirty`     | Value changed                |
| `pristine`  | Value unchanged              |
| `disabled`  | Control disabled             |

---

### ✅ Checking States (Code Examples)

| Check      | Code                           |
| ---------- | ------------------------------ |
| Is valid   | `control.valid`                |
| Is invalid | `control.invalid`              |
| Is touched | `control.touched`              |
| Is dirty   | `control.dirty`                |
| Has error  | `control.hasError('required')` |

---

# ✅ When to Use What (Real-World Guide)

| Scenario               | Use               |
| ---------------------- | ----------------- |
| Simple form            | `FormControl`     |
| Full form              | `FormGroup`       |
| Dynamic list           | `FormArray`       |
| Conditional validation | `setValidators()` |
| Show errors            | `markAsTouched()` |
| API-driven UI          | `valueChanges`    |

---

# Angular Advanced Topics - Complete Guide (Phase 3-7)

---

## Phase 3 — Asynchronous & Reactivity

### 10. RxJS

#### **What is RxJS?**
**The River Analogy:** Think of RxJS as a river system where water (data) flows continuously. You can observe the river (subscribe), filter debris (operators), merge streams (combine), and react when water arrives (callbacks).

RxJS (Reactive Extensions for JavaScript) is a library for composing asynchronous and event-based programs using observable sequences.

```typescript
// Observable: A stream of data over time
import { Observable } from 'rxjs';

const dataStream$ = new Observable(observer => {
  observer.next('First data');
  observer.next('Second data');
  observer.complete();
});
```

#### **Observables vs Promises**

| Feature | Promise | Observable |
|---------|---------|------------|
| **Emits** | Single value | Multiple values over time |
| **Lazy** | Eager (executes immediately) | Lazy (executes on subscribe) |
| **Cancellable** | No | Yes (unsubscribe) |
| **Operators** | then, catch | map, filter, switchMap, etc. |

```typescript
// Promise - Single value, eager
const promise = fetch('/api/user');
promise.then(data => console.log(data));

// Observable - Multiple values, lazy
import { fromEvent } from 'rxjs';
const clicks$ = fromEvent(button, 'click');
clicks$.subscribe(event => console.log(event)); // Only executes on subscribe
```

#### **Subscriptions**
**The Newspaper Analogy:** Subscribing is like subscribing to a newspaper. You receive updates until you unsubscribe.

```typescript
import { interval } from 'rxjs';

// Create a stream that emits every second
const timer$ = interval(1000);

// Subscribe to receive values
const subscription = timer$.subscribe(value => {
  console.log(`Received: ${value}`);
});

// Unsubscribe to stop receiving values
setTimeout(() => {
  subscription.unsubscribe();
  console.log('Stopped subscription');
}, 5000);
```

#### **Common RxJS Operators**

**1. map - Transform each value**
```typescript
import { of, map } from 'rxjs';

// Transform data like Array.map()
of(1, 2, 3).pipe(
  map(x => x * 10)
).subscribe(val => console.log(val)); // 10, 20, 30
```

**2. filter - Filter values**
```typescript
import { of, filter } from 'rxjs';

of(1, 2, 3, 4, 5).pipe(
  filter(x => x % 2 === 0)
).subscribe(val => console.log(val)); // 2, 4
```

**3. switchMap - Switch to new observable, cancel previous**
```typescript
import { fromEvent, switchMap } from 'rxjs';
import { ajax } from 'rxjs/ajax';

// Cancel previous request when new search happens
fromEvent(searchInput, 'input').pipe(
  map(event => event.target.value),
  switchMap(searchTerm => ajax.getJSON(`/api/search?q=${searchTerm}`))
).subscribe(results => console.log(results));
```

**4. mergeMap - Merge all observables, don't cancel**
```typescript
import { of, mergeMap, delay } from 'rxjs';

// Process all requests in parallel
of(1, 2, 3).pipe(
  mergeMap(id => ajax.getJSON(`/api/user/${id}`))
).subscribe(user => console.log(user));
```

**5. concatMap - Process one at a time in order**
```typescript
import { of, concatMap } from 'rxjs';

// Wait for each request to complete before starting next
of(1, 2, 3).pipe(
  concatMap(id => ajax.getJSON(`/api/user/${id}`))
).subscribe(user => console.log(user));
```

**6. forkJoin - Wait for all to complete (like Promise.all)**
```typescript
import { forkJoin } from 'rxjs';

forkJoin({
  users: ajax.getJSON('/api/users'),
  posts: ajax.getJSON('/api/posts'),
  comments: ajax.getJSON('/api/comments')
}).subscribe(({ users, posts, comments }) => {
  console.log('All loaded:', users, posts, comments);
});
```

**7. combineLatest - Combine latest values from multiple streams**
```typescript
import { combineLatest } from 'rxjs';

combineLatest([
  userSettings$,
  appConfig$,
  featureFlags$
]).subscribe(([settings, config, flags]) => {
  console.log('Combined state:', settings, config, flags);
});
```

#### **Error Handling**
```typescript
import { catchError, retry } from 'rxjs';
import { of } from 'rxjs';

ajax.getJSON('/api/data').pipe(
  retry(3), // Retry 3 times on error
  catchError(error => {
    console.error('Error occurred:', error);
    return of({ error: true, message: 'Failed to load' }); // Return fallback
  })
).subscribe(data => console.log(data));
```

#### **Unsubscribing & Memory Leaks**

**The Problem:** Forgetting to unsubscribe causes memory leaks.

```typescript
export class BadComponent implements OnInit {
  ngOnInit() {
    // BAD: No unsubscribe = memory leak
    this.dataService.getData().subscribe(data => {
      this.data = data;
    });
  }
}

// Solution 1: Manual unsubscribe
export class GoodComponent implements OnInit, OnDestroy {
  private subscription: Subscription;
  
  ngOnInit() {
    this.subscription = this.dataService.getData().subscribe(data => {
      this.data = data;
    });
  }
  
  ngOnDestroy() {
    this.subscription.unsubscribe();
  }
}

// Solution 2: takeUntil pattern
export class BetterComponent implements OnInit, OnDestroy {
  private destroy$ = new Subject<void>();
  
  ngOnInit() {
    this.dataService.getData().pipe(
      takeUntil(this.destroy$)
    ).subscribe(data => this.data = data);
  }
  
  ngOnDestroy() {
    this.destroy$.next();
    this.destroy$.complete();
  }
}

// Solution 3: async pipe (Angular handles unsubscribe)
@Component({
  template: `<div>{{ data$ | async }}</div>`
})
export class BestComponent {
  data$ = this.dataService.getData(); // No manual subscribe needed
  
  constructor(private dataService: DataService) {}
}
```

---

### 11. Signals (Angular 16+)

#### **What are Signals?**
**The Reactive Variable Analogy:** Signals are like smart variables that automatically notify everyone when they change. Think of them as cells in Excel that auto-update formulas when their values change.

```typescript
import { signal, computed, effect } from '@angular/core';

export class CounterComponent {
  // Create a signal
  count = signal(0);
  
  // Computed signal (derived state)
  doubleCount = computed(() => this.count() * 2);
  
  // Effect (side effect when signal changes)
  constructor() {
    effect(() => {
      console.log(`Count changed to: ${this.count()}`);
    });
  }
  
  increment() {
    this.count.set(this.count() + 1); // Set new value
    // or
    this.count.update(value => value + 1); // Update based on current
  }
}
```

#### **signal(), computed(), effect()**

**1. signal() - Writable reactive state**
```typescript
// Create signal with initial value
const name = signal('John');

// Read value
console.log(name()); // 'John'

// Set new value
name.set('Jane');

// Update based on current value
name.update(current => current.toUpperCase());
```

**2. computed() - Derived state**
```typescript
const firstName = signal('John');
const lastName = signal('Doe');

// Automatically updates when dependencies change
const fullName = computed(() => `${firstName()} ${lastName()}`);

console.log(fullName()); // 'John Doe'
firstName.set('Jane');
console.log(fullName()); // 'Jane Doe'
```

**3. effect() - Side effects**
```typescript
const count = signal(0);

// Runs whenever count changes
effect(() => {
  console.log(`Count is now: ${count()}`);
  localStorage.setItem('count', count().toString());
});

count.set(5); // Console logs "Count is now: 5" and saves to localStorage
```

#### **Signals vs Observables**

| Feature | Signals | Observables |
|---------|---------|-------------|
| **Synchronous** | Yes | No |
| **Always has value** | Yes | No (until first emission) |
| **Lazy** | No (always has value) | Yes |
| **Multiple values** | Always current | Stream over time |
| **Best for** | Component state | Async operations, events |

```typescript
// Signals - Synchronous state
const count = signal(0);
console.log(count()); // Immediate value

// Observables - Asynchronous streams
const count$ = new BehaviorSubject(0);
count$.subscribe(val => console.log(val)); // Need to subscribe
```

#### **Zoneless Change Detection**
**The Manual vs Automatic Analogy:** Zone.js is like having a spy watch everything. Signals are like asking to be notified only when specific things change.

```typescript
// Traditional (Zone.js) - Angular checks everything
export class OldComponent {
  count = 0;
  
  increment() {
    this.count++; // Zone.js triggers change detection for entire app
  }
}

// Signal-based (Zoneless) - Angular checks only what changed
export class NewComponent {
  count = signal(0);
  
  increment() {
    this.count.update(v => v + 1); // Only this component re-renders
  }
}
```

#### **When to Use Signals**
- ✅ **Component state** (form values, UI state, counters)
- ✅ **Derived calculations** (computed values from other signals)
- ✅ **Simple reactive state** without async complexity
- ❌ **Async operations** (HTTP requests, WebSockets) → Use Observables
- ❌ **Event streams** (clicks over time) → Use Observables

```typescript
export class UserProfileComponent {
  // Signals for component state
  user = signal<User | null>(null);
  isLoading = signal(false);
  
  // Computed derived state
  displayName = computed(() => {
    const u = this.user();
    return u ? `${u.firstName} ${u.lastName}` : 'Guest';
  });
  
  // Observable for HTTP request
  loadUser(id: number) {
    this.isLoading.set(true);
    this.http.get<User>(`/api/users/${id}`).subscribe(user => {
      this.user.set(user);
      this.isLoading.set(false);
    });
  }
}
```

---

### 12. State Management

#### **Service + RxJS Pattern**
**The Shared Memory Analogy:** A service acts like a shared notebook that all components can read from and write to.

```typescript
@Injectable({ providedIn: 'root' })
export class TodoService {
  private todosSubject = new BehaviorSubject<Todo[]>([]);
  todos$ = this.todosSubject.asObservable();
  
  addTodo(todo: Todo) {
    const current = this.todosSubject.value;
    this.todosSubject.next([...current, todo]);
  }
  
  removeTodo(id: string) {
    const current = this.todosSubject.value;
    this.todosSubject.next(current.filter(t => t.id !== id));
  }
}

// Component usage
export class TodoListComponent {
  todos$ = this.todoService.todos$;
  
  constructor(private todoService: TodoService) {}
  
  addTodo(text: string) {
    this.todoService.addTodo({ id: uuid(), text, completed: false });
  }
}
```

#### **Signal Store (Modern Pattern)**
```typescript
import { signalStore, withState, withMethods } from '@ngrx/signals';

interface TodosState {
  todos: Todo[];
  filter: 'all' | 'active' | 'completed';
}

export const TodosStore = signalStore(
  { providedIn: 'root' },
  withState<TodosState>({
    todos: [],
    filter: 'all'
  }),
  withMethods((store) => ({
    addTodo(todo: Todo) {
      patchState(store, { todos: [...store.todos(), todo] });
    },
    setFilter(filter: 'all' | 'active' | 'completed') {
      patchState(store, { filter });
    }
  }))
);

// Component usage
export class TodoComponent {
  store = inject(TodosStore);
  
  todos = this.store.todos;
  filter = this.store.filter;
  
  addTodo(text: string) {
    this.store.addTodo({ id: uuid(), text, completed: false });
  }
}
```

#### **NgRx (Redux Pattern)**
**The Event-Driven Store Analogy:** NgRx is like a government system: Actions are citizen requests, Reducers are laws that process requests, and the Store is the official records.

**1. Actions - What happened**
```typescript
import { createAction, props } from '@ngrx/store';

export const loadTodos = createAction('[Todo Page] Load Todos');
export const loadTodosSuccess = createAction(
  '[Todo API] Load Todos Success',
  props<{ todos: Todo[] }>()
);
export const addTodo = createAction(
  '[Todo Page] Add Todo',
  props<{ text: string }>()
);
```

**2. Reducers - How state changes**
```typescript
import { createReducer, on } from '@ngrx/store';

export interface TodoState {
  todos: Todo[];
  loading: boolean;
  error: string | null;
}

const initialState: TodoState = {
  todos: [],
  loading: false,
  error: null
};

export const todoReducer = createReducer(
  initialState,
  on(loadTodos, (state) => ({ ...state, loading: true })),
  on(loadTodosSuccess, (state, { todos }) => ({
    ...state,
    todos,
    loading: false
  })),
  on(addTodo, (state, { text }) => ({
    ...state,
    todos: [...state.todos, { id: uuid(), text, completed: false }]
  }))
);
```

**3. Effects - Side effects (API calls)**
```typescript
import { Injectable } from '@angular/core';
import { Actions, createEffect, ofType } from '@ngrx/effects';
import { map, mergeMap, catchError } from 'rxjs/operators';
import { of } from 'rxjs';

@Injectable()
export class TodoEffects {
  loadTodos$ = createEffect(() =>
    this.actions$.pipe(
      ofType(loadTodos),
      mergeMap(() =>
        this.todoApi.getTodos().pipe(
          map(todos => loadTodosSuccess({ todos })),
          catchError(error => of(loadTodosFailure({ error: error.message })))
        )
      )
    )
  );
  
  constructor(
    private actions$: Actions,
    private todoApi: TodoApiService
  ) {}
}
```

**4. Selectors - Query state**
```typescript
import { createFeatureSelector, createSelector } from '@ngrx/store';

export const selectTodoState = createFeatureSelector<TodoState>('todos');

export const selectAllTodos = createSelector(
  selectTodoState,
  (state) => state.todos
);

export const selectActiveTodos = createSelector(
  selectAllTodos,
  (todos) => todos.filter(t => !t.completed)
);

export const selectTodoCount = createSelector(
  selectAllTodos,
  (todos) => todos.length
);
```

**5. Component usage**
```typescript
export class TodoComponent {
  todos$ = this.store.select(selectAllTodos);
  activeTodos$ = this.store.select(selectActiveTodos);
  
  constructor(private store: Store) {}
  
  ngOnInit() {
    this.store.dispatch(loadTodos());
  }
  
  addTodo(text: string) {
    this.store.dispatch(addTodo({ text }));
  }
}
```

#### **When to Use Which**

| Pattern | Best For | Complexity |
|---------|----------|------------|
| **Service + RxJS** | Small-medium apps, simple state | Low |
| **Signal Store** | Medium apps, modern Angular | Medium |
| **NgRx** | Large apps, complex state, time-travel debugging | High |

```typescript
// Simple app: Service + RxJS
// 1-5 components sharing state
@Injectable({ providedIn: 'root' })
export class SimpleStateService {
  private state = signal({ count: 0 });
  
  increment() {
    this.state.update(s => ({ count: s.count + 1 }));
  }
}

// Medium app: Signal Store
// 5-20 components, multiple features
export const AppStore = signalStore(
  withState(initialState),
  withMethods(...)
);

// Large app: NgRx
// 20+ components, complex business logic, audit trail
// Full Redux architecture with actions, reducers, effects, selectors
```

---

## Phase 4 — Advanced Angular

### 13. Change Detection

#### **How Change Detection Works**
**The Inspection System Analogy:** Angular is like a quality inspector checking if products (component data) have changed and need to be updated on the display shelf (DOM).

```typescript
// When does Angular check for changes?
// 1. Browser events (click, input, etc.)
button.addEventListener('click', () => {
  this.count++; // Zone.js detects this and triggers change detection
});

// 2. Timers (setTimeout, setInterval)
setTimeout(() => {
  this.message = 'Updated'; // Zone.js detects this
}, 1000);

// 3. HTTP requests
this.http.get('/api/data').subscribe(data => {
  this.data = data; // Zone.js detects this
});
```

#### **Default Strategy**
**The Full Inspection Analogy:** Angular checks EVERY component from top to bottom, every time something changes.

```typescript
@Component({
  selector: 'app-parent',
  template: `
    <h1>{{ title }}</h1>
    <app-child></app-child>
  `,
  changeDetection: ChangeDetectionStrategy.Default // Default setting
})
export class ParentComponent {
  title = 'Parent';
  
  updateTitle() {
    this.title = 'Updated'; // Angular checks ENTIRE tree
  }
}
```

#### **OnPush Strategy**
**The Smart Inspection Analogy:** Only check a component if its inputs changed or it emitted an event.

```typescript
@Component({
  selector: 'app-child',
  template: `<p>{{ user.name }}</p>`,
  changeDetection: ChangeDetectionStrategy.OnPush // Only check when input changes
})
export class ChildComponent {
  @Input() user: User;
  
  // Angular only checks this component when:
  // 1. @Input() reference changes
  // 2. Event handler is triggered
  // 3. Observable used with async pipe emits
  // 4. Manually triggered with ChangeDetectorRef
}

// Parent component
export class ParentComponent {
  user = { name: 'John', age: 30 };
  
  updateUser() {
    // ❌ BAD: Mutating object (OnPush won't detect)
    this.user.name = 'Jane';
    
    // ✅ GOOD: Creating new reference
    this.user = { ...this.user, name: 'Jane' };
  }
}
```

#### **Zones & Zone.js**
**The Monkey Patch Analogy:** Zone.js wraps all async operations to detect when they complete.

```typescript
// Zone.js patches these APIs:
// - setTimeout/setInterval
// - Promise.then
// - XMLHttpRequest
// - EventListener
// - requestAnimationFrame

// Behind the scenes:
const originalSetTimeout = window.setTimeout;
window.setTimeout = function(fn, delay) {
  return originalSetTimeout(() => {
    fn();
    // Zone.js: Hey Angular, something async finished!
    ApplicationRef.tick(); // Trigger change detection
  }, delay);
};
```

#### **Zoneless Angular**
**The Manual Notification Analogy:** Instead of Zone.js auto-detecting everything, you explicitly tell Angular when to update.

```typescript
// Enable zoneless mode (angular.json)
{
  "projects": {
    "app": {
      "architect": {
        "build": {
          "options": {
            "polyfills": [] // Remove zone.js
          }
        }
      }
    }
  }
}

// Use signals for automatic updates
export class ZonelessComponent {
  count = signal(0);
  
  increment() {
    this.count.update(v => v + 1); // Auto triggers update
  }
}

// Or manually trigger
export class ManualComponent {
  count = 0;
  
  constructor(private cdr: ChangeDetectorRef) {}
  
  increment() {
    this.count++;
    this.cdr.markForCheck(); // Manually tell Angular to update
  }
}
```

#### **Performance Implications**

```typescript
// ❌ BAD: Default strategy + function calls in template
@Component({
  template: `
    <div *ngFor="let item of getItems()">{{ item }}</div>
  `
})
export class SlowComponent {
  getItems() {
    console.log('Called on every change detection!');
    return this.items.filter(i => i.active);
  }
}

// ✅ GOOD: OnPush + pure pipe
@Component({
  template: `
    <div *ngFor="let item of items | activeItems">{{ item }}</div>
  `,
  changeDetection: ChangeDetectionStrategy.OnPush
})
export class FastComponent {
  @Input() items: Item[];
}

@Pipe({ name: 'activeItems', pure: true })
export class ActiveItemsPipe {
  transform(items: Item[]) {
    console.log('Only called when items reference changes');
    return items.filter(i => i.active);
  }
}
```

---

### 14. Performance Optimization

#### **Lazy Loading**
**The On-Demand Delivery Analogy:** Don't load all modules upfront; load them only when the user navigates to them.

```typescript
// app.routes.ts
export const routes: Routes = [
  {
    path: 'admin',
    loadChildren: () => import('./admin/admin.routes').then(m => m.ADMIN_ROUTES)
    // Only loads admin module when user visits /admin
  },
  {
    path: 'dashboard',
    loadComponent: () => import('./dashboard/dashboard.component').then(m => m.DashboardComponent)
    // Lazy load standalone component
  }
];

// Before lazy loading: Initial bundle = 1.5MB
// After lazy loading: Initial bundle = 500KB, Admin module = 300KB (loaded on demand)
```

#### **trackBy Function**
**The Identity Check Analogy:** Help Angular identify which items changed instead of re-creating everything.

```typescript
// ❌ BAD: Angular re-creates all DOM elements on every change
@Component({
  template: `
    <div *ngFor="let user of users">
      {{ user.name }}
    </div>
  `
})
export class SlowListComponent {
  users = [{ id: 1, name: 'John' }, { id: 2, name: 'Jane' }];
  
  addUser() {
    this.users = [...this.users, { id: 3, name: 'Bob' }];
    // Angular destroys and recreates ALL <div> elements
  }
}

// ✅ GOOD: Angular only adds the new element
@Component({
  template: `
    <div *ngFor="let user of users; trackBy: trackById">
      {{ user.name }}
    </div>
  `
})
export class FastListComponent {
  users = [{ id: 1, name: 'John' }, { id: 2, name: 'Jane' }];
  
  trackById(index: number, item: User) {
    return item.id; // Angular uses ID to track identity
  }
  
  addUser() {
    this.users = [...this.users, { id: 3, name: 'Bob' }];
    // Angular only creates ONE new <div> for Bob
  }
}
```

#### **OnPush Change Detection**
(Covered in detail in section 13)

```typescript
@Component({
  changeDetection: ChangeDetectionStrategy.OnPush
})
export class OptimizedComponent {
  @Input() data: Data; // Only check when this reference changes
}
```

#### **Signals for Reactivity**
```typescript
// Traditional: Zone.js checks entire app
export class OldComponent {
  count = 0;
  doubleCount = 0;
  
  increment() {
    this.count++;
    this.doubleCount = this.count * 2; // Manual update
  }
}

// Signals: Granular reactivity
export class NewComponent {
  count = signal(0);
  doubleCount = computed(() => this.count() * 2); // Auto updates
  
  increment() {
    this.count.update(v => v + 1);
    // Only this component updates, not entire app
  }
}
```

#### **Pure Pipes**
```typescript
// Pure pipe: Only re-executes when input reference changes
@Pipe({ name: 'expensiveCalc', pure: true })
export class ExpensiveCalcPipe {
  transform(data: number[]) {
    console.log('Pipe executed'); // Only when data array reference changes
    return data.reduce((sum, n) => sum + n, 0);
  }
}

// Impure pipe: Re-executes on EVERY change detection
@Pipe({ name: 'expensiveCalc', pure: false })
export class ImpureExpensiveCalcPipe {
  transform(data: number[]) {
    console.log('Pipe executed'); // On EVERY button click, even unrelated
    return data.reduce((sum, n) => sum + n, 0);
  }
}
```

#### **Bundle Optimization**

```typescript
// 1. Code splitting
// app.routes.ts
const routes: Routes = [
  { path: 'admin', loadChildren: () => import('./admin/admin.module') }
];

// 2. Tree shaking - Import only what you need
// ❌ BAD
import * as _ from 'lodash'; // Imports entire library
_.debounce(...);

// ✅ GOOD
import debounce from 'lodash-es/debounce'; // Imports only debounce

// 3. Production build optimizations
// ng build --configuration production
// - Minification
// - Dead code elimination
// - Ahead-of-time compilation
// - Bundle optimization

// 4. Differential loading (modern vs legacy browsers)
// Automatically generates ES2015 and ES5 bundles
// Modern browsers get smaller, faster bundles

// 5. Preloading strategies
const routes: Routes = [
  {
    path: 'feature',
    loadChildren: () => import('./feature/feature.module'),
    data: { preload: true }
  }
];

// Preload after initial load completes
export class CustomPreloadStrategy implements PreloadingStrategy {
  preload(route: Route, load: () => Observable<any>): Observable<any> {
    return route.data?.['preload'] ? load() : of(null);
  }
}
```

---

### 15. Dynamic UI

#### **Dynamic Components**
**The Runtime Assembly Analogy:** Like building furniture: instead of having pre-built pieces, you assemble components at runtime based on user needs.

```typescript
import { Component, ViewChild, ViewContainerRef, ComponentRef } from '@angular/core';

@Component({
  selector: 'app-dynamic-host',
  template: `
    <button (click)="loadComponent('alert')">Load Alert</button>
    <button (click)="loadComponent('card')">Load Card</button>
    <ng-container #dynamicHost></ng-container>
  `
})
export class DynamicHostComponent {
  @ViewChild('dynamicHost', { read: ViewContainerRef }) container!: ViewContainerRef;
  
  private componentRef?: ComponentRef<any>;
  
  async loadComponent(type: string) {
    // Clear previous component
    this.container.clear();
    
    // Dynamically import and create component
    if (type === 'alert') {
      const { AlertComponent } = await import('./alert.component');
      this.componentRef = this.container.createComponent(AlertComponent);
      this.componentRef.instance.message = 'Dynamic Alert!';
    } else if (type === 'card') {
      const { CardComponent } = await import('./card.component');
      this.componentRef = this.container.createComponent(CardComponent);
      this.componentRef.instance.title = 'Dynamic Card!';
    }
  }
  
  ngOnDestroy() {
    this.componentRef?.destroy();
  }
}
```

#### **ViewContainerRef**
**The Container Analogy:** ViewContainerRef is like a container shelf where you can dynamically add/remove components.

```typescript
export class ModalService {
  constructor(
    private viewContainerRef: ViewContainerRef,
    private injector: Injector
  ) {}
  
  open(component: Type<any>, data?: any) {
    const componentRef = this.viewContainerRef.createComponent(component, {
      injector: this.injector
    });
    
    // Pass data to component
    if (data) {
      Object.assign(componentRef.instance, data);
    }
    
    return componentRef;
  }
}

// Usage
export class AppComponent {
  constructor(private modalService: ModalService) {}
  
  openUserModal() {
    const modal = this.modalService.open(UserModalComponent, {
      userId: 123,
      onClose: () => modal.destroy()
    });
  }
}
```

#### **ContentChild vs ViewChild**

**ViewChild: Your own template**
```typescript
@Component({
  selector: 'app-parent',
  template: `
    <h1 #heading>Title</h1>
    <app-child #child></app-child>
  `
})
export class ParentComponent {
  // Access elements in OWN template
  @ViewChild('heading') heading!: ElementRef;
  @ViewChild('child') child!: ChildComponent;
  
  ngAfterViewInit() {
    console.log(this.heading.nativeElement.textContent); // 'Title'
  }
}
```

**ContentChild: Projected content**
```typescript
@Component({
  selector: 'app-card',
  template: `
    <div class="card">
      <ng-content></ng-content>
    </div>
  `
})
export class CardComponent {
  // Access content projected INTO this component
  @ContentChild('cardTitle') title!: ElementRef;
  
  ngAfterContentInit() {
    console.log(this.title.nativeElement.textContent);
  }
}

// Usage
@Component({
  template: `
    <app-card>
      <h2 #cardTitle>Projected Title</h2>
    </app-card>
  `
})
export class AppComponent {}
```

#### **Angular Elements (Web Components)**
**The Universal Component Analogy:** Turn Angular components into standard web components that work anywhere (React, Vue, vanilla JS).

```typescript
import { createCustomElement } from '@angular/elements';
import { Injector } from '@angular/core';

@Component({
  selector: 'app-hello',
  template: `<h1>Hello {{ name }}!</h1>`
})
export class HelloComponent {
  @Input() name = 'World';
}

// Convert to Web Component
export class AppModule {
  constructor(private injector: Injector) {
    const helloElement = createCustomElement(HelloComponent, { injector });
    customElements.define('hello-widget', helloElement);
  }
  
  ngDoBootstrap() {} // Don't bootstrap, we're creating a custom element
}

// Now use in ANY framework or plain HTML
// <hello-widget name="Angular"></hello-widget>
```

#### **Deferrable Views (@defer)**
**The Lazy Content Analogy:** Load parts of your UI only when needed, like loading images as you scroll.

```typescript
@Component({
  template: `
    <h1>Main Content</h1>
    
    <!-- Defer loading until visible -->
    @defer (on viewport) {
      <heavy-component />
    } @placeholder {
      <div>Loading...</div>
    } @loading (minimum 1s) {
      <spinner />
    } @error {
      <div>Failed to load</div>
    }
    
    <!-- Defer until user interacts -->
    @defer (on interaction) {
      <comment-section />
    } @placeholder {
      <button>Load Comments</button>
    }
    
    <!-- Defer until idle -->
    @defer (on idle) {
      <analytics-widget />
    }
    
    <!-- Defer with timer -->
    @defer (on timer(5s)) {
      <advertisement />
    }
  `
})
export class OptimizedPageComponent {}

// Multiple triggers
@Component({
  template: `
    @defer (on viewport; on timer(10s); prefetch on idle) {
      <expensive-chart />
    }
  `
})
```

---

## Phase 5 — Architecture & Enterprise

### 16. Authentication & Security

#### **JWT Authentication**
**The Passport Analogy:** JWT is like a passport that proves who you are. You show it at each checkpoint (API request).

```typescript
// auth.service.ts
@Injectable({ providedIn: 'root' })
export class AuthService {
  private tokenKey = 'auth_token';
  private refreshTokenKey = 'refresh_token';
  
  login(credentials: { email: string; password: string }) {
    return this.http.post<AuthResponse>('/api/auth/login', credentials).pipe(
      tap(response => {
        this.storeTokens(response.accessToken, response.refreshToken);
      })
    );
  }
  
  private storeTokens(accessToken: string, refreshToken: string) {
    localStorage.setItem(this.tokenKey, accessToken);
    localStorage.setItem(this.refreshTokenKey, refreshToken);
  }
  
  getAccessToken(): string | null {
    return localStorage.getItem(this.tokenKey);
  }
  
  getRefreshToken(): string | null {
    return localStorage.getItem(this.refreshTokenKey);
  }
  
  isAuthenticated(): boolean {
    const token = this.getAccessToken();
    if (!token) return false;
    
    // Check if token is expired
    const payload = JSON.parse(atob(token.split('.')[1]));
    return payload.exp * 1000 > Date.now();
  }
  
  logout() {
    localStorage.removeItem(this.tokenKey);
    localStorage.removeItem(this.refreshTokenKey);
  }
}
```

#### **Access Tokens & Refresh Tokens**
**The Ticket System Analogy:** Access token is a day pass (expires quickly), refresh token is a season pass (lasts longer, used to get new day passes).

```typescript
// Access Token: Short-lived (15 minutes), used for API requests
// Refresh Token: Long-lived (7 days), used to get new access tokens

@Injectable()
export class TokenInterceptor implements HttpInterceptor {
  constructor(private authService: AuthService) {}
  
  intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    // Add access token to every request
    const token = this.authService.getAccessToken();
    
    if (token) {
      req = req.clone({
        setHeaders: {
          Authorization: `Bearer ${token}`
        }
      });
    }
    
    return next.handle(req).pipe(
      catchError(error => {
        if (error.status === 401) {
          // Access token expired, try to refresh
          return this.handleTokenRefresh(req, next);
        }
        return throwError(() => error);
      })
    );
  }
  
  private handleTokenRefresh(req: HttpRequest<any>, next: HttpHandler) {
    const refreshToken = this.authService.getRefreshToken();
    
    return this.authService.refreshAccessToken(refreshToken).pipe(
      switchMap(newTokens => {
        this.authService.storeTokens(newTokens.accessToken, newTokens.refreshToken);
        
        // Retry original request with new token
        const clonedReq = req.clone({
          setHeaders: {
            Authorization: `Bearer ${newTokens.accessToken}`
          }
        });
        return next.handle(clonedReq);
      }),
      catchError(error => {
        // Refresh failed, logout user
        this.authService.logout();
        return throwError(() => error);
      })
    );
  }
}
```

#### **HTTP Interceptors**
**The Security Gate Analogy:** Interceptors are like security gates that process all requests/responses going in and out.

```typescript
// auth.interceptor.ts
@Injectable()
export class AuthInterceptor implements HttpInterceptor {
  intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    const token = this.authService.getToken();
    
    if (token) {
      req = req.clone({
        setHeaders: { Authorization: `Bearer ${token}` }
      });
    }
    
    return next.handle(req);
  }
}

// error.interceptor.ts
@Injectable()
export class ErrorInterceptor implements HttpInterceptor {
  intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    return next.handle(req).pipe(
      catchError((error: HttpErrorResponse) => {
        let errorMessage = '';
        
        if (error.error instanceof ErrorEvent) {
          // Client-side error
          errorMessage = `Error: ${error.error.message}`;
        } else {
          // Server-side error
          errorMessage = `Error Code: ${error.status}\nMessage: ${error.message}`;
        }
        
        this.toastService.error(errorMessage);
        return throwError(() => error);
      })
    );
  }
}

// logging.interceptor.ts
@Injectable()
export class LoggingInterceptor implements HttpInterceptor {
  intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    const started = Date.now();
    
    return next.handle(req).pipe(
      tap(event => {
        if (event instanceof HttpResponse) {
          const elapsed = Date.now() - started;
          console.log(`${req.method} ${req.urlWithParams} took ${elapsed}ms`);
        }
      })
    );
  }
}

// app.config.ts - Register interceptors
export const appConfig: ApplicationConfig = {
  providers: [
    provideHttpClient(
      withInterceptors([
        authInterceptor,
        errorInterceptor,
        loggingInterceptor
      ])
    )
  ]
};
```

#### **Route Guards**
**The Bouncer Analogy:** Guards are like club bouncers checking if you're allowed to enter.

```typescript
// auth.guard.ts - Can user access route?
export const authGuard: CanActivateFn = () => {
  const authService = inject(AuthService);
  const router = inject(Router);
  
  if (authService.isAuthenticated()) {
    return true;
  }
  
  return router.createUrlTree(['/login']);
};

// role.guard.ts - Does user have required role?
export const roleGuard: CanActivateFn = (route) => {
  const authService = inject(AuthService);
  const router = inject(Router);
  
  const requiredRole = route.data['role'];
  const userRole = authService.getUserRole();
  
  if (userRole === requiredRole) {
    return true;
  }
  
  return router.createUrlTree(['/unauthorized']);
};

// unsaved-changes.guard.ts - Prevent leaving with unsaved data
export const unsavedChangesGuard: CanDeactivateFn<FormComponent> = (component) => {
  if (component.hasUnsavedChanges()) {
    return confirm('You have unsaved changes. Do you really want to leave?');
  }
  return true;
};

// Routes configuration
const routes: Routes = [
  {
    path: 'dashboard',
    component: DashboardComponent,
    canActivate: [authGuard]
  },
  {
    path: 'admin',
    component: AdminComponent,
    canActivate: [authGuard, roleGuard],
    data: { role: 'admin' }
  },
  {
    path: 'edit/:id',
    component: EditComponent,
    canDeactivate: [unsavedChangesGuard]
  }
];
```

#### **Role-Based Access Control (RBAC)**
```typescript
// User roles
enum Role {
  Admin = 'admin',
  Editor = 'editor',
  Viewer = 'viewer'
}

// auth.service.ts
@Injectable({ providedIn: 'root' })
export class AuthService {
  private currentUserSubject = new BehaviorSubject<User | null>(null);
  currentUser$ = this.currentUserSubject.asObservable();
  
  hasRole(role: Role): boolean {
    const user = this.currentUserSubject.value;
    return user?.roles.includes(role) ?? false;
  }
  
  hasAnyRole(roles: Role[]): boolean {
    return roles.some(role => this.hasRole(role));
  }
}

// Directive for conditional rendering
@Directive({
  selector: '[appHasRole]',
  standalone: true
})
export class HasRoleDirective {
  constructor(
    private templateRef: TemplateRef<any>,
    private viewContainer: ViewContainerRef,
    private authService: AuthService
  ) {}
  
  @Input() set appHasRole(roles: Role | Role[]) {
    const roleArray = Array.isArray(roles) ? roles : [roles];
    
    if (this.authService.hasAnyRole(roleArray)) {
      this.viewContainer.createEmbeddedView(this.templateRef);
    } else {
      this.viewContainer.clear();
    }
  }
}

// Usage in template
@Component({
  template: `
    <button *appHasRole="'admin'">Delete User</button>
    <button *appHasRole="['admin', 'editor']">Edit Content</button>
  `
})
```

#### **Secure Storage**
```typescript
// ❌ BAD: Storing sensitive data in localStorage (vulnerable to XSS)
localStorage.setItem('token', token);

// ✅ BETTER: HTTP-only cookies (can't be accessed by JavaScript)
// Set on server:
// Set-Cookie: token=xxx; HttpOnly; Secure; SameSite=Strict

// ✅ GOOD: Encrypted storage (for non-sensitive data in localStorage)
@Injectable({ providedIn: 'root' })
export class SecureStorageService {
  private encryptionKey = environment.storageKey;
  
  setItem(key: string, value: any) {
    const encrypted = CryptoJS.AES.encrypt(
      JSON.stringify(value),
      this.encryptionKey
    ).toString();
    localStorage.setItem(key, encrypted);
  }
  
  getItem<T>(key: string): T | null {
    const encrypted = localStorage.getItem(key);
    if (!encrypted) return null;
    
    const decrypted = CryptoJS.AES.decrypt(encrypted, this.encryptionKey);
    return JSON.parse(decrypted.toString(CryptoJS.enc.Utf8));
  }
}

// Security best practices:
// 1. Never store passwords
// 2. Use HTTPS only
// 3. Implement CSRF protection
// 4. Sanitize user input
// 5. Set Content Security Policy headers
// 6. Use HTTP-only cookies for tokens when possible
```

---

### 17. Server-Side Rendering (SSR)

#### **Angular Universal**
**The Pre-Rendered Menu Analogy:** Instead of cooking every dish when customers arrive (CSR), prepare dishes in advance (SSR) so they're ready instantly.

```typescript
// Add SSR to existing app
ng add @angular/ssr

// server.ts (generated file)
import { APP_BASE_HREF } from '@angular/common';
import { CommonEngine } from '@angular/ssr';
import express from 'express';
import { fileURLToPath } from 'node:url';
import { dirname, join, resolve } from 'node:path';
import bootstrap from './src/main.server';

const serverDistFolder = dirname(fileURLToPath(import.meta.url));
const browserDistFolder = resolve(serverDistFolder, '../browser');
const indexHtml = join(serverDistFolder, 'index.server.html');

const app = express();

app.get('*', (req, res, next) => {
  const { protocol, originalUrl, baseUrl, headers } = req;

  commonEngine
    .render({
      bootstrap,
      documentFilePath: indexHtml,
      url: `${protocol}://${headers.host}${originalUrl}`,
      publicPath: browserDistFolder,
      providers: [{ provide: APP_BASE_HREF, useValue: baseUrl }],
    })
    .then((html) => res.send(html))
    .catch((err) => next(err));
});
```

#### **SSR vs CSR (Client-Side Rendering)**

| Feature | CSR | SSR |
|---------|-----|-----|
| **Initial Load** | Slower (downloads JS first) | Faster (HTML ready) |
| **SEO** | Poor (search engines see empty page) | Excellent (full HTML) |
| **Time to Interactive** | Slower | Faster for first view |
| **Server Load** | Low | Higher |
| **Best For** | Apps, dashboards | Marketing sites, blogs |

```typescript
// CSR Flow:
// 1. Browser requests page
// 2. Server sends empty HTML + JS bundle
// 3. JS downloads and executes
// 4. Angular bootstraps
// 5. App renders
// Total: 3-5 seconds

// SSR Flow:
// 1. Browser requests page
// 2. Server renders Angular app to HTML
// 3. Browser receives full HTML (can see content immediately)
// 4. JS downloads and hydrates
// Total to first view: <1 second
```

#### **Hydration**
**The Awakening Analogy:** SSR sends a "frozen" HTML page. Hydration "awakens" it by attaching event listeners and making it interactive.

```typescript
// main.ts - Enable hydration
import { bootstrapApplication } from '@angular/platform-browser';
import { provideClientHydration } from '@angular/platform-browser';
import { AppComponent } from './app/app.component';

bootstrapApplication(AppComponent, {
  providers: [
    provideClientHydration() // Enables hydration
  ]
});

// What hydration does:
// 1. Browser receives pre-rendered HTML from server
// 2. User sees content immediately (non-interactive)
// 3. JS loads and Angular "hydrates" the DOM
// 4. Attaches event listeners
// 5. Page becomes interactive

// Without hydration: Angular destroys and re-creates DOM (flicker)
// With hydration: Angular reuses existing DOM (smooth)
```

#### **SEO Handling**
```typescript
// meta.service.ts - Dynamic meta tags
import { Injectable } from '@angular/core';
import { Meta, Title } from '@angular/platform-browser';

@Injectable({ providedIn: 'root' })
export class SeoService {
  constructor(
    private meta: Meta,
    private title: Title
  ) {}
  
  updateMetaTags(data: {
    title: string;
    description: string;
    image?: string;
    url?: string;
  }) {
    // Update title
    this.title.setTitle(data.title);
    
    // Update meta tags
    this.meta.updateTag({ name: 'description', content: data.description });
    this.meta.updateTag({ property: 'og:title', content: data.title });
    this.meta.updateTag({ property: 'og:description', content: data.description });
    
    if (data.image) {
      this.meta.updateTag({ property: 'og:image', content: data.image });
    }
    
    if (data.url) {
      this.meta.updateTag({ property: 'og:url', content: data.url });
    }
  }
}

// product.component.ts
export class ProductComponent implements OnInit {
  constructor(private seoService: SeoService) {}
  
  ngOnInit() {
    this.seoService.updateMetaTags({
      title: 'Amazing Product - Buy Now',
      description: 'The best product you will ever buy',
      image: 'https://example.com/product.jpg',
      url: 'https://example.com/products/123'
    });
  }
}
```

#### **Browser vs Server Code**
**The Platform Check Analogy:** Some code only works in browsers (localStorage, window), some only on servers (file system, Node.js APIs).

```typescript
import { isPlatformBrowser, isPlatformServer } from '@angular/common';
import { PLATFORM_ID, inject } from '@angular/core';

export class MyComponent {
  private platformId = inject(PLATFORM_ID);
  
  ngOnInit() {
    if (isPlatformBrowser(this.platformId)) {
      // Browser-only code
      localStorage.setItem('key', 'value');
      console.log(window.innerWidth);
    }
    
    if (isPlatformServer(this.platformId)) {
      // Server-only code
      const fs = require('fs');
      fs.readFile('data.json');
    }
  }
}

// Transfer state - Share data between server and browser
import { makeStateKey, TransferState } from '@angular/core';

const DATA_KEY = makeStateKey<any>('productData');

export class ProductComponent {
  constructor(private transferState: TransferState) {}
  
  ngOnInit() {
    if (isPlatformServer(this.platformId)) {
      // On server: Fetch data and store
      this.http.get('/api/product').subscribe(data => {
        this.transferState.set(DATA_KEY, data);
      });
    }
    
    if (isPlatformBrowser(this.platformId)) {
      // On browser: Get data from transfer state (no second request)
      const data = this.transferState.get(DATA_KEY, null);
      if (data) {
        this.product = data;
      }
    }
  }
}
```

---

### 18. Testing

#### **Unit Testing Basics**
**The Lab Test Analogy:** Unit tests are like testing individual ingredients before making a dish.

```typescript
// calculator.service.ts
@Injectable({ providedIn: 'root' })
export class CalculatorService {
  add(a: number, b: number): number {
    return a + b;
  }
  
  divide(a: number, b: number): number {
    if (b === 0) throw new Error('Division by zero');
    return a / b;
  }
}

// calculator.service.spec.ts
describe('CalculatorService', () => {
  let service: CalculatorService;
  
  beforeEach(() => {
    TestBed.configureTestingModule({});
    service = TestBed.inject(CalculatorService);
  });
  
  it('should add two numbers', () => {
    expect(service.add(2, 3)).toBe(5);
  });
  
  it('should divide two numbers', () => {
    expect(service.divide(10, 2)).toBe(5);
  });
  
  it('should throw error when dividing by zero', () => {
    expect(() => service.divide(10, 0)).toThrowError('Division by zero');
  });
});
```

#### **Component Tests**
```typescript
// counter.component.ts
@Component({
  selector: 'app-counter',
  template: `
    <div>Count: {{ count }}</div>
    <button (click)="increment()">+</button>
  `
})
export class CounterComponent {
  count = 0;
  
  increment() {
    this.count++;
  }
}

// counter.component.spec.ts
describe('CounterComponent', () => {
  let component: CounterComponent;
  let fixture: ComponentFixture<CounterComponent>;
  
  beforeEach(async () => {
    await TestBed.configureTestingModule({
      imports: [CounterComponent]
    }).compileComponents();
    
    fixture = TestBed.createComponent(CounterComponent);
    component = fixture.componentInstance;
    fixture.detectChanges();
  });
  
  it('should display initial count', () => {
    const div = fixture.nativeElement.querySelector('div');
    expect(div.textContent).toContain('Count: 0');
  });
  
  it('should increment count when button clicked', () => {
    const button = fixture.nativeElement.querySelector('button');
    button.click();
    fixture.detectChanges();
    
    expect(component.count).toBe(1);
    const div = fixture.nativeElement.querySelector('div');
    expect(div.textContent).toContain('Count: 1');
  });
});
```

#### **Service Tests with Dependencies**
```typescript
// user.service.ts
@Injectable({ providedIn: 'root' })
export class UserService {
  constructor(private http: HttpClient) {}
  
  getUser(id: number) {
    return this.http.get<User>(`/api/users/${id}`);
  }
  
  createUser(user: User) {
    return this.http.post<User>('/api/users', user);
  }
}

// user.service.spec.ts
describe('UserService', () => {
  let service: UserService;
  let httpMock: HttpTestingController;
  
  beforeEach(() => {
    TestBed.configureTestingModule({
      imports: [HttpClientTestingModule],
      providers: [UserService]
    });
    
    service = TestBed.inject(UserService);
    httpMock = TestBed.inject(HttpTestingController);
  });
  
  afterEach(() => {
    httpMock.verify(); // Ensure no outstanding requests
  });
  
  it('should fetch user by id', () => {
    const mockUser = { id: 1, name: 'John' };
    
    service.getUser(1).subscribe(user => {
      expect(user).toEqual(mockUser);
    });
    
    const req = httpMock.expectOne('/api/users/1');
    expect(req.request.method).toBe('GET');
    req.flush(mockUser); // Respond with mock data
  });
  
  it('should create user', () => {
    const newUser = { name: 'Jane' };
    const createdUser = { id: 2, name: 'Jane' };
    
    service.createUser(newUser).subscribe(user => {
      expect(user).toEqual(createdUser);
    });
    
    const req = httpMock.expectOne('/api/users');
    expect(req.request.method).toBe('POST');
    expect(req.request.body).toEqual(newUser);
    req.flush(createdUser);
  });
});
```

#### **Directive Tests**
```typescript
// highlight.directive.ts
@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective {
  @Input() highlightColor = 'yellow';
  
  constructor(private el: ElementRef) {}
  
  @HostListener('mouseenter') onMouseEnter() {
    this.highlight(this.highlightColor);
  }
  
  @HostListener('mouseleave') onMouseLeave() {
    this.highlight('');
  }
  
  private highlight(color: string) {
    this.el.nativeElement.style.backgroundColor = color;
  }
}

// highlight.directive.spec.ts
@Component({
  template: `<p appHighlight highlightColor="red">Test</p>`
})
class TestComponent {}

describe('HighlightDirective', () => {
  let fixture: ComponentFixture<TestComponent>;
  let p: HTMLElement;
  
  beforeEach(() => {
    TestBed.configureTestingModule({
      declarations: [HighlightDirective, TestComponent]
    });
    
    fixture = TestBed.createComponent(TestComponent);
    p = fixture.nativeElement.querySelector('p');
  });
  
  it('should highlight on mouseenter', () => {
    p.dispatchEvent(new Event('mouseenter'));
    expect(p.style.backgroundColor).toBe('red');
  });
  
  it('should remove highlight on mouseleave', () => {
    p.dispatchEvent(new Event('mouseenter'));
    p.dispatchEvent(new Event('mouseleave'));
    expect(p.style.backgroundColor).toBe('');
  });
});
```

#### **Pipe Tests**
```typescript
// truncate.pipe.ts
@Pipe({ name: 'truncate' })
export class TruncatePipe implements PipeTransform {
  transform(value: string, limit: number = 50): string {
    return value.length > limit ? value.substring(0, limit) + '...' : value;
  }
}

// truncate.pipe.spec.ts
describe('TruncatePipe', () => {
  let pipe: TruncatePipe;
  
  beforeEach(() => {
    pipe = new TruncatePipe();
  });
  
  it('should truncate long text', () => {
    const text = 'This is a very long text that should be truncated';
    expect(pipe.transform(text, 20)).toBe('This is a very long ...');
  });
  
  it('should not truncate short text', () => {
    const text = 'Short';
    expect(pipe.transform(text, 20)).toBe('Short');
  });
});
```

#### **Guard Tests**
```typescript
// auth.guard.ts
export const authGuard: CanActivateFn = () => {
  const authService = inject(AuthService);
  const router = inject(Router);
  
  return authService.isAuthenticated() || router.createUrlTree(['/login']);
};

// auth.guard.spec.ts
describe('authGuard', () => {
  let authService: jasmine.SpyObj<AuthService>;
  let router: jasmine.SpyObj<Router>;
  
  beforeEach(() => {
    const authSpy = jasmine.createSpyObj('AuthService', ['isAuthenticated']);
    const routerSpy = jasmine.createSpyObj('Router', ['createUrlTree']);
    
    TestBed.configureTestingModule({
      providers: [
        { provide: AuthService, useValue: authSpy },
        { provide: Router, useValue: routerSpy }
      ]
    });
    
    authService = TestBed.inject(AuthService) as jasmine.SpyObj<AuthService>;
    router = TestBed.inject(Router) as jasmine.SpyObj<Router>;
  });
  
  it('should allow access when authenticated', () => {
    authService.isAuthenticated.and.returnValue(true);
    
    const result = TestBed.runInInjectionContext(() => 
      authGuard({} as any, {} as any)
    );
    
    expect(result).toBe(true);
  });
  
  it('should redirect to login when not authenticated', () => {
    authService.isAuthenticated.and.returnValue(false);
    const urlTree = {} as UrlTree;
    router.createUrlTree.and.returnValue(urlTree);
    
    const result = TestBed.runInInjectionContext(() => 
      authGuard({} as any, {} as any)
    );
    
    expect(result).toBe(urlTree);
    expect(router.createUrlTree).toHaveBeenCalledWith(['/login']);
  });
});
```

#### **Interceptor Tests**
```typescript
// auth.interceptor.ts
export const authInterceptor: HttpInterceptorFn = (req, next) => {
  const authService = inject(AuthService);
  const token = authService.getToken();
  
  if (token) {
    req = req.clone({
      setHeaders: { Authorization: `Bearer ${token}` }
    });
  }
  
  return next(req);
};

// auth.interceptor.spec.ts
describe('authInterceptor', () => {
  let httpMock: HttpTestingController;
  let authService: jasmine.SpyObj<AuthService>;
  
  beforeEach(() => {
    const authSpy = jasmine.createSpyObj('AuthService', ['getToken']);
    
    TestBed.configureTestingModule({
      imports: [HttpClientTestingModule],
      providers: [
        { provide: AuthService, useValue: authSpy },
        provideHttpClient(withInterceptors([authInterceptor]))
      ]
    });
    
    httpMock = TestBed.inject(HttpTestingController);
    authService = TestBed.inject(AuthService) as jasmine.SpyObj<AuthService>;
  });
  
  it('should add Authorization header when token exists', () => {
    authService.getToken.and.returnValue('test-token');
    const http = TestBed.inject(HttpClient);
    
    http.get('/api/data').subscribe();
    
    const req = httpMock.expectOne('/api/data');
    expect(req.request.headers.get('Authorization')).toBe('Bearer test-token');
    req.flush({});
  });
  
  it('should not add header when no token', () => {
    authService.getToken.and.returnValue(null);
    const http = TestBed.inject(HttpClient);
    
    http.get('/api/data').subscribe();
    
    const req = httpMock.expectOne('/api/data');
    expect(req.request.headers.has('Authorization')).toBe(false);
    req.flush({});
  });
});
```

#### **Mocking & Best Practices**
```typescript
// Mock service
class MockUserService {
  getUser(id: number) {
    return of({ id, name: 'Mock User' });
  }
}

// Test with mock
beforeEach(() => {
  TestBed.configureTestingModule({
    providers: [
      { provide: UserService, useClass: MockUserService }
    ]
  });
});

// Spy on methods
it('should call service method', () => {
  const spy = spyOn(service, 'getUser').and.returnValue(of(mockUser));
  component.loadUser(1);
  expect(spy).toHaveBeenCalledWith(1);
});

// Testing best practices:
// 1. One assertion per test (when possible)
// 2. Use descriptive test names
// 3. Arrange-Act-Assert pattern
// 4. Clean up after tests
// 5. Don't test implementation details
// 6. Mock external dependencies
```

---

### 19. CI/CD & Environments

#### **Environment Configuration**
**The Multi-Stage Deployment Analogy:** Like having different versions of your restaurant - test kitchen (dev), soft launch (stage), grand opening (prod).

```typescript
// src/environments/environment.development.ts
export const environment = {
  production: false,
  apiUrl: 'http://localhost:3000/api',
  enableDebug: true,
  featureFlags: {
    newFeature: true
  }
};

// src/environments/environment.ts (production)
export const environment = {
  production: true,
  apiUrl: 'https://api.myapp.com',
  enableDebug: false,
  featureFlags: {
    newFeature: false
  }
};

// Usage in code
import { environment } from '../environments/environment';

@Injectable()
export class ApiService {
  private apiUrl = environment.apiUrl;
  
  getData() {
    return this.http.get(`${this.apiUrl}/data`);
  }
}
```

#### **Dev / Stage / Prod Builds**
```typescript
// angular.json configurations
{
  "projects": {
    "my-app": {
      "architect": {
        "build": {
          "configurations": {
            "development": {
              "fileReplacements": [{
                "replace": "src/environments/environment.ts",
                "with": "src/environments/environment.development.ts"
              }],
              "optimization": false,
              "sourceMap": true
            },
            "staging": {
              "fileReplacements": [{
                "replace": "src/environments/environment.ts",
                "with": "src/environments/environment.staging.ts"
              }],
              "optimization": true,
              "sourceMap": false
            },
            "production": {
              "fileReplacements": [{
                "replace": "src/environments/environment.ts",
                "with": "src/environments/environment.ts"
              }],
              "optimization": true,
              "budgets": [{
                "type": "initial",
                "maximumWarning": "500kb",
                "maximumError": "1mb"
              }]
            }
          }
        }
      }
    }
  }
}

// Build commands
// ng build --configuration development
// ng build --configuration staging
// ng build --configuration production
```

#### **CI Pipelines (GitHub Actions Example)**
```yaml
# .github/workflows/ci.yml
name: CI Pipeline

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      
      - name: Install dependencies
        run: npm ci
      
      - name: Run linter
        run: npm run lint
      
      - name: Run tests
        run: npm run test:ci
      
      - name: Build
        run: npm run build --configuration production
  
  deploy-staging:
    needs: test
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/develop'
    
    steps:
      - uses: actions/checkout@v3
      - name: Deploy to Staging
        run: |
          npm ci
          npm run build --configuration staging
          # Deploy to staging server
  
  deploy-production:
    needs: test
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    
    steps:
      - uses: actions/checkout@v3
      - name: Deploy to Production
        run: |
          npm ci
          npm run build --configuration production
          # Deploy to production server
```

#### **Deployment Strategies**

**1. Blue-Green Deployment**
```typescript
// Two identical production environments
// Blue (current) → Green (new version)
// Switch traffic instantly, rollback if issues

// Steps:
// 1. Deploy new version to Green environment
// 2. Run smoke tests on Green
// 3. Switch load balancer to Green
// 4. Keep Blue for rollback
// 5. If issues: switch back to Blue instantly
```

**2. Canary Deployment**
```typescript
// Gradual rollout to users
// 5% → 25% → 50% → 100%

// Example with feature flags
@Injectable()
export class FeatureFlagService {
  isCanaryUser(): boolean {
    const userId = this.authService.getUserId();
    const canaryPercentage = 25; // 25% of users
    
    return (userId % 100) < canaryPercentage;
  }
}

// Component
export class NewFeatureComponent {
  showNewFeature = this.featureFlags.isCanaryUser();
}
```

**3. Rolling Deployment**
```typescript
// Update servers one by one
// Server1 → Server2 → Server3 → Server4

// No downtime
// Gradual rollout
// Easy rollback (stop at any server)
```

#### **Runtime Configuration**
**The Dynamic Settings Analogy:** Load configuration from server at runtime instead of building it into the app.

```typescript
// assets/config.json (fetched at runtime)
{
  "apiUrl": "https://api.example.com",
  "features": {
    "enableChat": true,
    "enableAnalytics": false
  }
}

// app.config.ts
export function initializeApp(): () => Promise<any> {
  return (): Promise<any> => {
    return fetch('/assets/config.json')
      .then(response => response.json())
      .then(config => {
        // Store config globally
        (window as any).appConfig = config;
      });
  };
}

export const appConfig: ApplicationConfig = {
  providers: [
    {
      provide: APP_INITIALIZER,
      useFactory: initializeApp,
      multi: true
    }
  ]
};

// config.service.ts
@Injectable({ providedIn: 'root' })
export class ConfigService {
  get config() {
    return (window as any).appConfig;
  }
  
  get apiUrl() {
    return this.config.apiUrl;
  }
  
  isFeatureEnabled(feature: string): boolean {
    return this.config.features[feature] ?? false;
  }
}

// Benefits:
// - Same build for all environments
// - Change config without rebuilding
// - Faster deployments
```

---

### 20. Micro-Frontends

#### **Monolithic vs Micro-Frontends**

**Monolithic:** One large Angular app containing everything
```
┌────────────────────────────┐
│   Single Angular App       │
│  ┌──────┬──────┬──────┐   │
│  │ Shop │ Blog │Admin │   │
│  └──────┴──────┴──────┘   │
└────────────────────────────┘
```

**Micro-Frontends:** Multiple independent apps composed together
```
┌─────────┐  ┌─────────┐  ┌─────────┐
│  Shop   │  │  Blog   │  │  Admin  │
│ Angular │  │  React  │  │   Vue   │
└─────────┘  └─────────┘  └─────────┘
      ↓           ↓            ↓
┌────────────────────────────────────┐
│       Shell/Container App          │
└────────────────────────────────────┘
```

#### **Module Federation (Webpack)**
**The Plugin System Analogy:** Load remote modules at runtime like installing plugins.

```typescript
// webpack.config.js (Host/Shell App)
const ModuleFederationPlugin = require('webpack/lib/container/ModuleFederationPlugin');

module.exports = {
  plugins: [
    new ModuleFederationPlugin({
      name: 'host',
      remotes: {
        shop: 'shop@http://localhost:4201/remoteEntry.js',
        blog: 'blog@http://localhost:4202/remoteEntry.js'
      },
      shared: {
        '@angular/core': { singleton: true, strictVersion: true },
        '@angular/common': { singleton: true, strictVersion: true }
      }
    })
  ]
};

// webpack.config.js (Remote App - Shop)
module.exports = {
  plugins: [
    new ModuleFederationPlugin({
      name: 'shop',
      filename: 'remoteEntry.js',
      exposes: {
        './ProductList': './src/app/product-list/product-list.component.ts'
      },
      shared: {
        '@angular/core': { singleton: true, strictVersion: true }
      }
    })
  ]
};

// Host app routes
const routes: Routes = [
  {
    path: 'shop',
    loadChildren: () => 
      import('shop/ProductList').then(m => m.ProductListModule)
  },
  {
    path: 'blog',
    loadChildren: () =>
      import('blog/BlogModule').then(m => m.BlogModule)
  }
];
```

#### **Nx Monorepos**
**The Organized Workspace Analogy:** All apps and libraries in one repo, sharing code efficiently.

```bash
# Create Nx workspace
npx create-nx-workspace@latest my-org

# Generate apps
nx g @nx/angular:app shop
nx g @nx/angular:app admin
nx g @nx/angular:app blog

# Generate shared libraries
nx g @nx/angular:lib shared-ui
nx g @nx/angular:lib shared-data-access

# Project structure
my-org/
├── apps/
│   ├── shop/
│   ├── admin/
│   └── blog/
├── libs/
│   ├── shared-ui/
│   │   ├── button/
│   │   └── modal/
│   └── shared-data-access/
│       ├── auth/
│       └── api/
└── nx.json
```

#### **Shared Libraries**
```typescript
// libs/shared-ui/button/button.component.ts
@Component({
  selector: 'myorg-button',
  template: `<button class="custom-btn"><ng-content></ng-content></button>`
})
export class ButtonComponent {}

// libs/shared-data-access/auth/auth.service.ts
@Injectable()
export class AuthService {
  login() { /* shared auth logic */ }
}

// apps/shop/src/app/app.component.ts
import { ButtonComponent } from '@myorg/shared-ui';
import { AuthService } from '@myorg/shared-data-access/auth';

@Component({
  imports: [ButtonComponent],
  template: `<myorg-button>Shop Now</myorg-button>`
})
export class ShopComponent {
  constructor(private auth: AuthService) {}
}

// Benefits:
// - Code reuse across apps
// - Single source of truth
// - Easier refactoring
// - Better dependency management
```

#### **Cross-App Communication**
```typescript
// 1. Custom Events (Browser API)
// App 1: Emit event
window.dispatchEvent(new CustomEvent('user-logged-in', {
  detail: { userId: 123 }
}));

// App 2: Listen for event
window.addEventListener('user-logged-in', (event: any) => {
  console.log('User logged in:', event.detail.userId);
});

// 2. Shared State Service (Module Federation)
// shared-state.service.ts (exposed via Module Federation)
@Injectable({ providedIn: 'root' })
export class SharedStateService {
  private userSubject = new BehaviorSubject<User | null>(null);
  user$ = this.userSubject.asObservable();
  
  setUser(user: User) {
    this.userSubject.next(user);
  }
}

// 3. Query Parameters
// App 1: Navigate with data
this.router.navigate(['/app2/page'], {
  queryParams: { userId: 123 }
});

// App 2: Read data
this.route.queryParams.subscribe(params => {
  const userId = params['userId'];
});

// 4. localStorage/sessionStorage
// App 1: Store data
localStorage.setItem('sharedData', JSON.stringify(data));

// App 2: Read data
const data = JSON.parse(localStorage.getItem('sharedData') || '{}');
```

---

## Phase 6 — TypeScript & JavaScript

### 21. TypeScript Essentials

#### **Types**
```typescript
// Primitive types
let name: string = 'John';
let age: number = 30;
let isActive: boolean = true;
let data: null = null;
let notDefined: undefined = undefined;

// Array types
let numbers: number[] = [1, 2, 3];
let names: Array<string> = ['John', 'Jane'];

// Tuple (fixed-length array with specific types)
let user: [string, number] = ['John', 30];

// Any (avoid when possible)
let anything: any = 'hello';
anything = 123; // OK, but loses type safety

// Unknown (safer than any)
let value: unknown = 'hello';
if (typeof value === 'string') {
  console.log(value.toUpperCase()); // OK after type check
}

// Void (no return value)
function logMessage(message: string): void {
  console.log(message);
}

// Never (function never returns)
function throwError(message: string): never {
  throw new Error(message);
}

// Union types (multiple possible types)
let id: string | number;
id = '123'; // OK
id = 123;   // OK

// Type aliases
type ID = string | number;
let userId: ID = '123';

// Literal types
let direction: 'up' | 'down' | 'left' | 'right';
direction = 'up'; // OK
// direction = 'diagonal'; // Error
```

#### **Interfaces**
```typescript
// Define object shape
interface User {
  id: number;
  name: string;
  email: string;
  age?: number; // Optional property
  readonly createdAt: Date; // Readonly property
}

const user: User = {
  id: 1,
  name: 'John',
  email: 'john@example.com',
  createdAt: new Date()
};

// user.createdAt = new Date(); // Error: readonly

// Extending interfaces
interface Admin extends User {
  role: 'admin';
  permissions: string[];
}

const admin: Admin = {
  id: 1,
  name: 'Admin',
  email: 'admin@example.com',
  createdAt: new Date(),
  role: 'admin',
  permissions: ['read', 'write', 'delete']
};

// Function interfaces
interface MathOperation {
  (a: number, b: number): number;
}

const add: MathOperation = (a, b) => a + b;
const multiply: MathOperation = (a, b) => a * b;

// Index signatures (dynamic keys)
interface Dictionary {
  [key: string]: string;
}

const translations: Dictionary = {
  hello: 'Hola',
  goodbye: 'Adiós'
};
```

#### **Enums**
```typescript
// Numeric enum
enum Status {
  Pending,    // 0
  Active,     // 1
  Inactive    // 2
}

let userStatus: Status = Status.Active;

// String enum
enum HttpMethod {
  GET = 'GET',
  POST = 'POST',
  PUT = 'PUT',
  DELETE = 'DELETE'
}

function makeRequest(method: HttpMethod) {
  console.log(`Making ${method} request`);
}

makeRequest(HttpMethod.POST);

// Const enum (compiled away for performance)
const enum Direction {
  Up,
  Down,
  Left,
  Right
}

let move = Direction.Up; // Compiled to: let move = 0;
```

#### **Generics**
**The Template Analogy:** Generics are like cookie cutters - same shape, different materials.

```typescript
// Generic function
function identity<T>(value: T): T {
  return value;
}

const num = identity<number>(42);      // T = number
const str = identity<string>('hello'); // T = string
const auto = identity(true);           // T inferred as boolean

// Generic array function
function firstElement<T>(arr: T[]): T | undefined {
  return arr[0];
}

const firstNum = firstElement([1, 2, 3]);      // number | undefined
const firstStr = firstElement(['a', 'b', 'c']); // string | undefined

// Generic interface
interface Response<T> {
  data: T;
  status: number;
  message: string;
}

const userResponse: Response<User> = {
  data: { id: 1, name: 'John', email: 'john@example.com', createdAt: new Date() },
  status: 200,
  message: 'Success'
};

// Generic class
class DataStore<T> {
  private data: T[] = [];
  
  add(item: T): void {
    this.data.push(item);
  }
  
  get(index: number): T | undefined {
    return this.data[index];
  }
  
  getAll(): T[] {
    return this.data;
  }
}

const userStore = new DataStore<User>();
userStore.add({ id: 1, name: 'John', email: 'john@example.com', createdAt: new Date() });

// Generic constraints
interface HasId {
  id: number;
}

function findById<T extends HasId>(items: T[], id: number): T | undefined {
  return items.find(item => item.id === id);
}

// Multiple type parameters
function merge<T, U>(obj1: T, obj2: U): T & U {
  return { ...obj1, ...obj2 };
}

const merged = merge({ name: 'John' }, { age: 30 });
// merged: { name: string } & { age: number }
```

#### **Strict Mode**
```typescript
// tsconfig.json
{
  "compilerOptions": {
    "strict": true,  // Enables all strict checks
    
    // Or enable individually:
    "noImplicitAny": true,           // Error on implicit 'any'
    "strictNullChecks": true,        // null/undefined must be explicit
    "strictFunctionTypes": true,     // Strict function type checking
    "strictPropertyInitialization": true, // Class properties must be initialized
    "strictBindCallApply": true,     // Strict bind/call/apply
    "noImplicitThis": true          // Error on implicit 'this'
  }
}

// Examples
// strictNullChecks
let name: string = 'John';
// name = null; // Error: Type 'null' is not assignable to type 'string'

let nullableName: string | null = 'John';
nullableName = null; // OK

// noImplicitAny
// function bad(x) { return x; } // Error: Parameter 'x' implicitly has an 'any' type
function good(x: number) { return x; } // OK

// strictPropertyInitialization
class User {
  // name: string; // Error: Property 'name' has no initializer
  name: string = '';  // OK
  age!: number;       // OK with definite assignment assertion
}
```

#### **TypeScript with Angular**
```typescript
// Component with typed inputs/outputs
@Component({
  selector: 'app-user-card'
})
export class UserCardComponent {
  @Input() user!: User;  // Typed input
  @Output() delete = new EventEmitter<number>(); // Typed output
  
  onDelete() {
    this.delete.emit(this.user.id); // Type-safe
  }
}

// Service with typed HTTP
@Injectable()
export class UserService {
  constructor(private http: HttpClient) {}
  
  getUsers(): Observable<User[]> {
    return this.http.get<User[]>('/api/users');
  }
  
  getUser(id: number): Observable<User> {
    return this.http.get<User>(`/api/users/${id}`);
  }
  
  createUser(user: Omit<User, 'id' | 'createdAt'>): Observable<User> {
    return this.http.post<User>('/api/users', user);
  }
}

// Type guards
function isAdmin(user: User | Admin): user is Admin {
  return 'role' in user && user.role === 'admin';
}

if (isAdmin(user)) {
  console.log(user.permissions); // TypeScript knows it's Admin
}
```

---

### 22. ES6+ JavaScript Essentials

#### **let / const**
```javascript
// var: Function-scoped, hoisted
function varExample() {
  console.log(x); // undefined (hoisted)
  var x = 5;
  
  if (true) {
    var x = 10;
  }
  console.log(x); // 10 (same variable)
}

// let: Block-scoped
function letExample() {
  // console.log(x); // Error: Cannot access before initialization
  let x = 5;
  
  if (true) {
    let x = 10; // Different variable
    console.log(x); // 10
  }
  console.log(x); // 5
}

// const: Block-scoped, cannot reassign
const PI = 3.14159;
// PI = 3.14; // Error: Assignment to constant

const user = { name: 'John' };
user.name = 'Jane'; // OK: Modifying object property
// user = {}; // Error: Reassigning constant
```

#### **Arrow Functions**
```javascript
// Traditional function
function add(a, b) {
  return a + b;
}

// Arrow function
const add = (a, b) => a + b;

// With single parameter (parentheses optional)
const double = x => x * 2;

// With block body
const greet = name => {
  const message = `Hello, ${name}!`;
  return message;
};

// 'this' binding difference
class Counter {
  count = 0;
  
  // Traditional function: 'this' depends on how it's called
  increment() {
    setTimeout(function() {
      // this.count++; // Error: 'this' is undefined
    }, 1000);
  }
  
  // Arrow function: 'this' is lexically bound
  incrementArrow() {
    setTimeout(() => {
      this.count++; // OK: 'this' refers to Counter instance
    }, 1000);
  }
}
```

#### **Destructuring**
```javascript
// Object destructuring
const user = {
  id: 1,
  name: 'John',
  email: 'john@example.com',
  address: {
    city: 'New York',
    country: 'USA'
  }
};

const { name, email } = user;
console.log(name, email); // 'John', 'john@example.com'

// Renaming
const { name: userName, email: userEmail } = user;

// Default values
const { age = 30 } = user;

// Nested destructuring
const { address: { city } } = user;

// Array destructuring
const numbers = [1, 2, 3, 4, 5];
const [first, second, ...rest] = numbers;
console.log(first);  // 1
console.log(second); // 2
console.log(rest);   // [3, 4, 5]

// Skipping elements
const [, , third] = numbers;
console.log(third); // 3

// Function parameters
function printUser({ name, email }) {
  console.log(`${name}: ${email}`);
}

printUser(user);
```

#### **Spread Operator**
```javascript
// Array spread
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
const combined = [...arr1, ...arr2]; // [1, 2, 3, 4, 5, 6]

// Copying arrays
const copy = [...arr1]; // Creates new array

// Object spread
const user = { name: 'John', age: 30 };
const updatedUser = { ...user, age: 31 }; // { name: 'John', age: 31 }

// Merging objects
const obj1 = { a: 1, b: 2 };
const obj2 = { b: 3, c: 4 };
const merged = { ...obj1, ...obj2 }; // { a: 1, b: 3, c: 4 }

// Function arguments
function sum(...numbers) {
  return numbers.reduce((total, n) => total + n, 0);
}

sum(1, 2, 3, 4, 5); // 15
```

#### **Optional Chaining**
```javascript
const user = {
  name: 'John',
  address: {
    city: 'New York'
  }
};

// Without optional chaining
const city = user && user.address && user.address.city;

// With optional chaining
const city = user?.address?.city; // 'New York'
const zip = user?.address?.zip;   // undefined (no error)

// With arrays
const firstUser = users?.[0];

// With function calls
const result = obj.method?.();
```

#### **Nullish Coalescing**
```javascript
// || returns right side if left is falsy (false, 0, '', null, undefined, NaN)
const value1 = 0 || 'default';        // 'default'
const value2 = '' || 'default';       // 'default'
const value3 = false || 'default';    // 'default'

// ?? returns right side only if left is null or undefined
const value4 = 0 ?? 'default';        // 0
const value5 = '' ?? 'default';       // ''
const value6 = false ?? 'default';    // false
const value7 = null ?? 'default';     // 'default'
const value8 = undefined ?? 'default'; // 'default'

// Useful for default values
function greet(name) {
  const displayName = name ?? 'Guest';
  console.log(`Hello, ${displayName}!`);
}

greet('John');    // 'Hello, John!'
greet('');        // 'Hello, !' (empty string is valid)
greet(null);      // 'Hello, Guest!'
greet(undefined); // 'Hello, Guest!'
```

#### **Async / Await**
```javascript
// Promises
function fetchUser(id) {
  return fetch(`/api/users/${id}`)
    .then(response => response.json())
    .then(data => data)
    .catch(error => console.error(error));
}

// Async/Await (cleaner)
async function fetchUser(id) {
  try {
    const response = await fetch(`/api/users/${id}`);
    const data = await response.json();
    return data;
  } catch (error) {
    console.error(error);
  }
}

// Sequential async operations
async function loadUserData(userId) {
  const user = await fetchUser(userId);
  const posts = await fetchPosts(userId);
  const comments = await fetchComments(userId);
  return { user, posts, comments };
}

// Parallel async operations
async function loadUserDataParallel(userId) {
  const [user, posts, comments] = await Promise.all([
    fetchUser(userId),
    fetchPosts(userId),
    fetchComments(userId)
  ]);
  return { user, posts, comments };
}

// Top-level await (in modules)
const config = await fetch('/config.json').then(r => r.json());
```

---

## Phase 7 — Real-World & Interviews

### 23. Real Project Scenarios

#### **Migrating Angular Versions**
```typescript
// Major version upgrade (e.g., 15 → 17)

// 1. Update Angular CLI
npm install -g @angular/cli@17

// 2. Update project
ng update @angular/core@17 @angular/cli@17

// 3. Update other dependencies
ng update @angular/material@17
ng update @ngrx/store@17

// 4. Address breaking changes
// Standalone components migration
ng generate @angular/core:standalone

// 5. Test thoroughly
npm run test
npm run e2e

// Common migration issues:
// - Deprecated APIs removed
// - New strict mode requirements
// - Ivy renderer changes
// - RxJS version updates
```

#### **NgModules → Standalone Components**
```typescript
// Before: NgModule approach
@NgModule({
  declarations: [UserComponent, UserListComponent],
  imports: [CommonModule, FormsModule],
  exports: [UserComponent]
})
export class UserModule {}

// After: Standalone approach
@Component({
  selector: 'app-user',
  standalone: true,
  imports: [CommonModule, FormsModule, UserListComponent],
  template: `...`
})
export class UserComponent {}

// Migration command
ng generate @angular/core:standalone

// Benefits:
// - Simpler mental model
// - Better tree-shaking
// - Easier lazy loading
// - No need for module files
```

#### **Performance Tuning**
```typescript
// 1. Enable production mode
if (environment.production) {
  enableProdMode();
}

// 2. Lazy load routes
const routes: Routes = [
  {
    path: 'admin',
    loadChildren: () => import('./admin/admin.routes')
  }
];

// 3. Use OnPush change detection
@Component({
  changeDetection: ChangeDetectionStrategy.OnPush
})

// 4. Virtual scrolling for long lists
import { ScrollingModule } from '@angular/cdk/scrolling';

@Component({
  template: `
    <cdk-virtual-scroll-viewport itemSize="50" style="height: 400px">
      <div *cdkVirtualFor="let item of items">{{ item }}</div>
    </cdk-virtual-scroll-viewport>
  `
})

// 5. Analyze bundle size
ng build --stats-json
npx webpack-bundle-analyzer dist/stats.json

// 6. Preload strategies
@NgModule({
  imports: [
    RouterModule.forRoot(routes, {
      preloadingStrategy: PreloadAllModules
    })
  ]
})
```

#### **Large Form Handling**
```typescript
// Dynamic form with FormArray
@Component({
  selector: 'app-survey-form'
})
export class SurveyFormComponent {
  surveyForm = new FormGroup({
    title: new FormControl('', Validators.required),
    questions: new FormArray([])
  });
  
  get questions() {
    return this.surveyForm.get('questions') as FormArray;
  }
  
  addQuestion() {
    const questionForm = new FormGroup({
      text: new FormControl('', Validators.required),
      type: new FormControl('text'),
      options: new FormArray([])
    });
    
    this.questions.push(questionForm);
  }
  
  removeQuestion(index: number) {
    this.questions.removeAt(index);
  }
  
  // Optimize with trackBy
  trackByIndex(index: number) {
    return index;
  }
  
  // Debounce form changes
  ngOnInit() {
    this.surveyForm.valueChanges.pipe(
      debounceTime(300),
      distinctUntilChanged()
    ).subscribe(value => {
      this.autosave(value);
    });
  }
}
```

#### **State Management Decisions**
```typescript
// Decision tree:

// Small app (< 5 components sharing state)
// → Service + BehaviorSubject
@Injectable({ providedIn: 'root' })
export class SimpleStateService {
  private state = new BehaviorSubject({ count: 0 });
  state$ = this.state.asObservable();
  
  update(value: any) {
    this.state.next(value);
  }
}

// Medium app (5-15 components, multiple features)
// → Signal Store
export const TodoStore = signalStore(
  withState({ todos: [], filter: 'all' }),
  withMethods(...)
);

// Large app (15+ components, complex workflows)
// → NgRx
// Full Redux pattern with actions, reducers, effects

// Criteria:
// - Team size and experience
// - App complexity
// - Testing requirements
// - Time-travel debugging needs
// - Performance requirements
```

---

### 24. Interview Preparation

#### **Common Angular Questions**

**Q1: What is the difference between constructor and ngOnInit?**
```typescript
export class MyComponent {
  data: any;
  
  // Constructor: Dependency injection only
  constructor(private service: DataService) {
    // ❌ DON'T: Call async operations
    // this.service.getData().subscribe(...);
    
    // ✅ DO: Initialize simple properties
    this.data = [];
  }
  
  // ngOnInit: Component initialization logic
  ngOnInit() {
    // ✅ DO: Fetch data, subscribe to observables
    this.service.getData().subscribe(data => {
      this.data = data;
    });
  }
}

// Answer: Constructor is for dependency injection, ngOnInit is for initialization logic
```

**Q2: Explain Angular lifecycle hooks**
```typescript
export class LifecycleComponent implements OnInit, OnChanges, DoCheck, 
  AfterContentInit, AfterContentChecked, AfterViewInit, AfterViewChecked, OnDestroy {
  
  @Input() data: any;
  
  constructor() {
    console.log('1. Constructor');
  }
  
  ngOnChanges(changes: SimpleChanges) {
    console.log('2. OnChanges - when @Input() changes');
  }
  
  ngOnInit() {
    console.log('3. OnInit - after first ngOnChanges');
  }
  
  ngDoCheck() {
    console.log('4. DoCheck - custom change detection');
  }
  
  ngAfterContentInit() {
    console.log('5. AfterContentInit - after <ng-content> initialized');
  }
  
  ngAfterContentChecked() {
    console.log('6. AfterContentChecked - after content checked');
  }
  
  ngAfterViewInit() {
    console.log('7. AfterViewInit - after view initialized');
  }
  
  ngAfterViewChecked() {
    console.log('8. AfterViewChecked - after view checked');
  }
  
  ngOnDestroy() {
    console.log('9. OnDestroy - cleanup before component destruction');
  }
}

// Order: Constructor → OnChanges → OnInit → DoCheck → AfterContent* → AfterView* → OnDestroy
```

**Q3: What is change detection?**
```typescript
// Answer: Process where Angular checks if component data changed and updates DOM

// Default strategy: Checks entire component tree
@Component({
  changeDetection: ChangeDetectionStrategy.Default
})

// OnPush strategy: Only checks when:
// 1. @Input() reference changes
// 2. Event handler triggered
// 3. Observable with async pipe emits
// 4. Manually triggered (markForCheck)
@Component({
  changeDetection: ChangeDetectionStrategy.OnPush
})
export class OptimizedComponent {
  @Input() user: User;
  
  constructor(private cdr: ChangeDetectorRef) {}
  
  updateManually() {
    this.cdr.markForCheck(); // Manually trigger change detection
  }
}
```

**Q4: ViewChild vs ContentChild**
```typescript
// ViewChild: Query own template
@Component({
  template: `<input #myInput>`
})
export class ParentComponent {
  @ViewChild('myInput') input!: ElementRef;
  
  ngAfterViewInit() {
    this.input.nativeElement.focus();
  }
}

// ContentChild: Query projected content
@Component({
  selector: 'app-wrapper',
  template: `<ng-content></ng-content>`
})
export class WrapperComponent {
  @ContentChild('projected') content!: ElementRef;
  
  ngAfterContentInit() {
    console.log(this.content);
  }
}

// Usage:
// <app-wrapper>
//   <div #projected>Projected content</div>
// </app-wrapper>
```

**Q5: Observables vs Promises**
```typescript
// Promise: Single value, eager
const promise = new Promise(resolve => {
  console.log('Promise started'); // Runs immediately
  resolve('value');
});

// Observable: Multiple values, lazy
const observable = new Observable(observer => {
  console.log('Observable started'); // Runs only when subscribed
  observer.next('value 1');
  observer.next('value 2');
});

observable.subscribe(); // Now it starts

// Key differences:
// 1. Promises emit 1 value, Observables emit 0-N values
// 2. Promises are eager, Observables are lazy
// 3. Promises not cancellable, Observables are (unsubscribe)
// 4. Observables have operators (map, filter, etc.)
```

---

#### **Senior-Level Questions**

**Q1: How would you optimize a slow Angular application?**
```typescript
// Answer checklist:
// 1. Use OnPush change detection
@Component({ changeDetection: ChangeDetectionStrategy.OnPush })

// 2. Lazy load modules/components
{ path: 'admin', loadChildren: () => import('./admin/admin.routes') }

// 3. Use trackBy in *ngFor
<div *ngFor="let item of items; trackBy: trackById">

// 4. Avoid function calls in templates
// ❌ BAD
<div>{{ calculateValue() }}</div>

// ✅ GOOD
<div>{{ calculatedValue }}</div>

// 5. Use pure pipes
@Pipe({ name: 'myPipe', pure: true })

// 6. Virtual scrolling for large lists
<cdk-virtual-scroll-viewport>

// 7. Detach change detection for heavy components
constructor(private cdr: ChangeDetectorRef) {
  this.cdr.detach();
}

// 8. Use Web Workers for heavy computations
// 9. Implement pagination/infinite scroll
// 10. Bundle size optimization (tree shaking, code splitting)
```

**Q2: Explain Dependency Injection hierarchy**
```typescript
// Answer: DI has 3 levels

// 1. Root level (app-wide singleton)
@Injectable({ providedIn: 'root' })
export class GlobalService {} // One instance for entire app

// 2. Module level
@NgModule({
  providers: [ModuleService] // One instance per module
})

// 3. Component level
@Component({
  providers: [ComponentService] // New instance per component and children
})

// Example hierarchy:
// AppComponent (has ServiceA)
//   ├─ ChildComponent (inherits ServiceA)
//   └─ OtherComponent (has its own ServiceA if provided)

// Interview tip: Explain that child components inherit parent providers
// unless they override them
```

**Q3: How do you handle memory leaks?**
```typescript
// Answer: Memory leaks happen when subscriptions aren't cleaned up

// ❌ BAD: Memory leak
export class BadComponent implements OnInit {
  ngOnInit() {
    this.service.getData().subscribe(data => {
      this.data = data; // Subscription never cleaned
    });
  }
}

// ✅ GOOD: Solutions

// 1. takeUntil pattern
export class GoodComponent implements OnInit, OnDestroy {
  private destroy$ = new Subject<void>();
  
  ngOnInit() {
    this.service.getData().pipe(
      takeUntil(this.destroy$)
    ).subscribe(data => this.data = data);
  }
  
  ngOnDestroy() {
    this.destroy$.next();
    this.destroy$.complete();
  }
}

// 2. async pipe (automatic cleanup)
export class BestComponent {
  data$ = this.service.getData();
  // Template: {{ data$ | async }}
}

// 3. Subscription array
export class AlternativeComponent {
  private subscriptions: Subscription[] = [];
  
  ngOnInit() {
    this.subscriptions.push(
      this.service.getData().subscribe(...)
    );
  }
  
  ngOnDestroy() {
    this.subscriptions.forEach(sub => sub.unsubscribe());
  }
}
```

**Q4: Explain NgRx flow**
```typescript
// Answer: Unidirectional data flow

// Component dispatches action
this.store.dispatch(loadUsers());

// Effect listens for action, makes API call
loadUsers$ = createEffect(() =>
  this.actions$.pipe(
    ofType(loadUsers),
    mergeMap(() => this.api.getUsers().pipe(
      map(users => loadUsersSuccess({ users }))
    ))
  )
);

// Reducer updates state based on action
on(loadUsersSuccess, (state, { users }) => ({
  ...state,
  users,
  loading: false
}))

// Component selects state
users$ = this.store.select(selectAllUsers);

// Flow: Component → Action → Effect → API → Action → Reducer → State → Component
```

**Q5: How would you implement authentication?**
```typescript
// Answer: Complete auth flow

// 1. Auth service
@Injectable({ providedIn: 'root' })
export class AuthService {
  login(credentials) {
    return this.http.post('/api/login', credentials).pipe(
      tap(response => {
        localStorage.setItem('token', response.token);
        this.currentUserSubject.next(response.user);
      })
    );
  }
  
  logout() {
    localStorage.removeItem('token');
    this.currentUserSubject.next(null);
    this.router.navigate(['/login']);
  }
  
  isAuthenticated(): boolean {
    const token = localStorage.getItem('token');
    return token && !this.isTokenExpired(token);
  }
}

// 2. HTTP Interceptor (add token to requests)
export const authInterceptor: HttpInterceptorFn = (req, next) => {
  const token = inject(AuthService).getToken();
  
  if (token) {
    req = req.clone({
      setHeaders: { Authorization: `Bearer ${token}` }
    });
  }
  
  return next(req);
};

// 3. Route guard
export const authGuard: CanActivateFn = () => {
  const authService = inject(AuthService);
  return authService.isAuthenticated() || inject(Router).createUrlTree(['/login']);
};

// 4. Token refresh logic
// 5. Error handling for 401/403
```

---

#### **Architecture Questions**

**Q1: Monolithic vs Micro-frontends?**
```typescript
// Answer:

// Monolithic (single app):
// Pros: Simpler, easier to develop, better performance
// Cons: Tight coupling, hard to scale teams, longer build times

// Micro-frontends (multiple apps):
// Pros: Team autonomy, independent deployments, tech diversity
// Cons: Complexity, duplication, runtime overhead

// Use micro-frontends when:
// - Large teams (50+ developers)
// - Different teams own different features
// - Need independent deployments
// - Long-term scalability requirements

// Implementation:
// - Module Federation (runtime composition)
// - Nx monorepo (shared code, separate apps)
// - iframe (simple but limited)
```

**Q2: How do you structure a large Angular application?**
```typescript
// Answer: Feature-based architecture

src/
├── app/
│   ├── core/                 // Singleton services, guards, interceptors
│   │   ├── auth/
│   │   ├── guards/
│   │   └── interceptors/
│   ├── shared/               // Reusable components, pipes, directives
│   │   ├── components/
│   │   ├── pipes/
│   │   └── directives/
│   ├── features/             // Feature modules
│   │   ├── user/
│   │   │   ├── components/
│   │   │   ├── services/
│   │   │   ├── models/
│   │   │   └── user.routes.ts
│   │   └── product/
│   └── app.routes.ts

// Principles:
// 1. Core: Import once in app
// 2. Shared: Import in features
// 3. Features: Lazy loaded
// 4. Smart/Dumb component pattern
// 5. State management at feature level
```

**Q3: Signals vs RxJS - when to use which?**
```typescript
// Answer:

// Use Signals for:
// - Component state (counters, toggles, form values)
// - Derived calculations (computed values)
// - Synchronous reactive state
const count = signal(0);
const doubleCount = computed(() => count() * 2);

// Use RxJS for:
// - Async operations (HTTP, WebSockets)
// - Event streams
// - Complex data flows with operators
this.http.get('/api/data').pipe(
  retry(3),
  switchMap(data => this.process(data))
);

// Often use both:
export class Component {
  // Signal for local state
  isLoading = signal(false);
  
  // Observable for async data
  users$ = this.http.get<User[]>('/api/users').pipe(
    tap(() => this.isLoading.set(false))
  );
}
```

---

#### **Live Coding Patterns**

**Pattern 1: Debounced Search**
```typescript
@Component({
  template: `
    <input [formControl]="searchControl" placeholder="Search...">
    <div *ngFor="let result of results$ | async">{{ result }}</div>
  `
})
export class SearchComponent {
  searchControl = new FormControl('');
  
  results$ = this.searchControl.valueChanges.pipe(
    debounceTime(300),
    distinctUntilChanged(),
    switchMap(term => term ? this.search(term) : of([]))
  );
  
  constructor(private searchService: SearchService) {}
  
  search(term: string) {
    return this.searchService.search(term);
  }
}
```

**Pattern 2: Loading State**
```typescript
@Component({
  template: `
    <button (click)="loadData()" [disabled]="isLoading()">
      {{ isLoading() ? 'Loading...' : 'Load Data' }}
    </button>
    <div *ngIf="error()">{{ error() }}</div>
    <div *ngIf="data()">{{ data() | json }}</div>
  `
})
export class LoadingComponent {
  isLoading = signal(false);
  data = signal<any>(null);
  error = signal<string | null>(null);
  
  loadData() {
    this.isLoading.set(true);
    this.error.set(null);
    
    this.http.get('/api/data').subscribe({
      next: (data) => {
        this.data.set(data);
        this.isLoading.set(false);
      },
      error: (err) => {
        this.error.set(err.message);
        this.isLoading.set(false);
      }
    });
  }
}
```

**Pattern 3: Form with Validation**
```typescript
@Component({
  template: `
    <form [formGroup]="form" (ngSubmit)="onSubmit()">
      <input formControlName="email">
      <div *ngIf="email.invalid && email.touched">
        <span *ngIf="email.errors?.['required']">Email is required</span>
        <span *ngIf="email.errors?.['email']">Invalid email</span>
      </div>
      
      <button [disabled]="form.invalid">Submit</button>
    </form>
  `
})
export class FormComponent {
  form = new FormGroup({
    email: new FormControl('', [Validators.required, Validators.email]),
    password: new FormControl('', [
      Validators.required,
      Validators.minLength(8)
    ])
  });
  
  get email() {
    return this.form.get('email')!;
  }
  
  onSubmit() {
    if (this.form.valid) {
      console.log(this.form.value);
    }
  }
}
```

---

#### **Debugging Scenarios**

**Scenario 1: ExpressionChangedAfterItHasBeenCheckedError**
```typescript
// ❌ Problem: Changing data during change detection
export class ParentComponent {
  @ViewChild(ChildComponent) child!: ChildComponent;
  
  ngAfterViewInit() {
    this.child.message = 'Updated'; // Error!
  }
}

// ✅ Solution: Use setTimeout or ChangeDetectorRef
export class ParentComponent {
  @ViewChild(ChildComponent) child!: ChildComponent;
  
  constructor(private cdr: ChangeDetectorRef) {}
  
  ngAfterViewInit() {
    setTimeout(() => {
      this.child.message = 'Updated';
    });
    // Or
    this.child.message = 'Updated';
    this.cdr.detectChanges();
  }
}
```

**Scenario 2: Infinite Loop in Observable**
```typescript
// ❌ Problem: Subscribing inside subscription
export class BadComponent {
  ngOnInit() {
    this.service.getData().subscribe(data => {
      this.service.getMore().subscribe(more => {
        // This creates new subscription every time
      });
    });
  }
}

// ✅ Solution: Use operators
export class GoodComponent {
  ngOnInit() {
    this.service.getData().pipe(
      switchMap(data => this.service.getMore())
    ).subscribe(more => {
      // Clean, no nested subscriptions
    });
  }
}
```

**Scenario 3: Memory Leak**
```typescript
// ❌ Problem: Interval not cleaned up
export class BadComponent {
  ngOnInit() {
    setInterval(() => {
      console.log('Running...'); // Runs forever, even after component destroyed
    }, 1000);
  }
}

// ✅ Solution: Clean up in ngOnDestroy
export class GoodComponent implements OnDestroy {
  private intervalId: any;
  
  ngOnInit() {
    this.intervalId = setInterval(() => {
      console.log('Running...');
    }, 1000);
  }
  
  ngOnDestroy() {
    clearInterval(this.intervalId);
  }
}
``