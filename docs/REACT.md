# React Complete Guide

## Table of Contents

### Core Concepts
- [What is React?](#what-is-react)
- [Virtual DOM](#virtual-dom)
- [Reconciliation Algorithm](#reconciliation-algorithm)
- [Fiber Architecture](#fiber-architecture)
- [JSX](#jsx)

### Components
- [Functional Components](#functional-components)
- [Component Lifecycle](#component-lifecycle)
- [Props](#props)
- [Children Props](#children-props)
- [Component Composition](#component-composition)

### Hooks
- [useState](#usestate)
- [useEffect](#useeffect)
- [useContext](#usecontext)
- [useReducer](#usereducer)
- [useCallback](#usecallback)
- [useMemo](#usememo)
- [useRef](#useref)
- [useLayoutEffect](#uselayouteffect)
- [useImperativeHandle](#useimperativehandle)
- [Custom Hooks](#custom-hooks)

### State Management
- [State Basics](#state-basics)
- [State Updates](#state-updates)
- [State Batching](#state-batching)
- [Context API](#context-api)
- [Redux Pattern](#redux-pattern)
- [Zustand](#zustand)

### Performance Optimization
- [React.memo](#reactmemo)
- [useMemo vs useCallback](#usememo-vs-usecallback)
- [Code Splitting](#code-splitting)
- [Lazy Loading](#lazy-loading)
- [Profiler](#profiler)

### Advanced Concepts
- [Portals](#portals)
- [Error Boundaries](#error-boundaries)
- [Refs and DOM](#refs-and-dom)
- [Higher Order Components](#higher-order-components)
- [Render Props](#render-props)
- [Controlled vs Uncontrolled](#controlled-vs-uncontrolled)

### React 18 Features
- [Concurrent Rendering](#concurrent-rendering)
- [Automatic Batching](#automatic-batching)
- [Transitions](#transitions)
- [Suspense](#suspense)
- [Server Components](#server-components)

### Interview Questions
- [Common Questions](#common-interview-questions)
- [Advanced Questions](#advanced-interview-questions)

---

## What is React?

### 🎯 React Overview

**Definition:**
> React is a declarative, component-based JavaScript library for building user interfaces, maintained by Meta (Facebook).

**Simple meaning:**
React lets you build interactive UIs by breaking them into reusable pieces (components) and automatically updates the screen when data changes.

**Why it matters:**
- ✅ Declarative approach - describe what UI should look like, React handles updates
- ✅ Component reusability - write once, use everywhere
- ✅ Virtual DOM - efficient updates without touching real DOM unnecessarily
- ✅ Unidirectional data flow - predictable state management
- ✅ Rich ecosystem - huge community and third-party libraries

**Real-life analogy:**
React is like a smart home system - you set the rules (state), and it automatically adjusts everything (UI) when conditions change, without you manually flipping each switch.

---

### 🔍 How React is Different

**React vs Vanilla JavaScript:**

| Feature | React | Vanilla JS |
|---------|-------|------------|
| **Updates** | Automatic (declarative) | Manual (imperative) |
| **DOM** | Virtual DOM | Direct DOM manipulation |
| **Code** | Component-based | Procedural |
| **State** | Built-in state management | Manual tracking |
| **Learning Curve** | Moderate | Low |

**React vs Angular:**

| Feature | React | Angular |
|---------|-------|---------|
| **Type** | Library | Framework |
| **Language** | JavaScript/JSX | TypeScript |
| **Learning** | Easier | Steeper |
| **Size** | Smaller (~45KB) | Larger (~500KB) |
| **Flexibility** | High | Opinionated |
| **DOM** | Virtual DOM | Real DOM with change detection |

**React vs Vue:**

| Feature | React | Vue |
|---------|-------|-----|
| **Syntax** | JSX | Template-based |
| **Learning** | Moderate | Easiest |
| **Flexibility** | More flexible | More structured |
| **Ecosystem** | Larger | Growing |
| **Performance** | Excellent | Excellent |

**Interview Tip:**
> "React is a library, not a framework - it focuses on the view layer and gives you flexibility to choose other tools for routing, state management, etc."

---

## Virtual DOM

### 🎯 What is Virtual DOM?

**Definition:**
> Virtual DOM is a lightweight JavaScript representation of the actual DOM, kept in memory and synced with the real DOM through a process called reconciliation.

**Simple meaning:**
Instead of updating the real DOM directly (which is slow), React updates a JavaScript copy first, calculates the minimal changes needed, then updates only those parts in the real DOM.

**Real-life analogy:**
Virtual DOM is like editing a document in draft mode - you make all your changes in the draft (virtual), then publish only the differences to the final version (real DOM), instead of rewriting the entire document.

---

### 🔧 How Virtual DOM Works Internally

**Step-by-step process:**

1. **Initial Render:**
```javascript
// React creates Virtual DOM tree
const virtualDOM = {
  type: 'div',
  props: {
    className: 'container',
    children: [
      { type: 'h1', props: { children: 'Hello' } },
      { type: 'p', props: { children: 'World' } }
    ]
  }
};

// Converts to real DOM
<div class="container">
  <h1>Hello</h1>
  <p>World</p>
</div>
```

2. **State Changes:**
```javascript
// When state updates, React creates NEW Virtual DOM
const newVirtualDOM = {
  type: 'div',
  props: {
    className: 'container',
    children: [
      { type: 'h1', props: { children: 'Hello' } },
      { type: 'p', props: { children: 'React' } } // Changed
    ]
  }
};
```

3. **Diffing Algorithm:**
```javascript
// React compares old vs new Virtual DOM
function diff(oldVTree, newVTree) {
  // Same type? Check props and children
  if (oldVTree.type === newVTree.type) {
    // Find differences in props
    const propsDiff = diffProps(oldVTree.props, newVTree.props);
    
    // Find differences in children
    const childrenDiff = diffChildren(
      oldVTree.props.children, 
      newVTree.props.children
    );
    
    return { propsDiff, childrenDiff };
  }
  // Different type? Replace entire node
  return { type: 'REPLACE', node: newVTree };
}
```

4. **Patch Real DOM:**
```javascript
// Apply only necessary changes
function patch(domNode, patches) {
  patches.forEach(patch => {
    switch(patch.type) {
      case 'UPDATE_PROPS':
        updateProps(domNode, patch.props);
        break;
      case 'UPDATE_TEXT':
        domNode.textContent = patch.text;
        break;
      case 'REPLACE':
        domNode.replaceWith(createDOM(patch.node));
        break;
    }
  });
}
```

---

**Internal Implementation (Simplified):**

```javascript
// How React creates Virtual DOM elements
function createElement(type, props, ...children) {
  return {
    type,
    props: {
      ...props,
      children: children.map(child =>
        typeof child === 'object' ? child : createTextElement(child)
      )
    }
  };
}

function createTextElement(text) {
  return {
    type: 'TEXT_ELEMENT',
    props: {
      nodeValue: text,
      children: []
    }
  };
}

// JSX transforms to this
// <div className="app">Hello</div>
// becomes:
createElement('div', { className: 'app' }, 'Hello');
```

**Benefits:**
- ✅ **Performance** - Batches DOM updates, minimizes reflows
- ✅ **Efficiency** - Updates only what changed
- ✅ **Cross-platform** - Same code for web, mobile (React Native)
- ✅ **Developer experience** - Write declarative code, React handles optimization

**Trade-offs:**

| Benefit | Cost |
|---------|------|
| **Automatic optimization** | Memory overhead for Virtual DOM tree |
| **Declarative updates** | Learning curve for beginners |
| **Batched updates** | Slight delay in updates (usually imperceptible) |

**Interview Tip:**
> "Virtual DOM is a programming concept where a virtual representation of the UI is kept in memory and synced with the real DOM through reconciliation, making updates efficient by batching changes and minimizing DOM manipulations."

---

## Reconciliation Algorithm

### 🎯 What is Reconciliation?

**Definition:**
> Reconciliation is the algorithm React uses to diff one Virtual DOM tree with another to determine which parts of the real DOM need to be updated.

**Simple meaning:**
React's smart way of figuring out what changed between renders and updating only those specific parts.

**Real-life analogy:**
Like a teacher grading papers - instead of rewriting the entire paper, they mark only the mistakes that need correction.

---

### 🔧 How Reconciliation Works

**The Diffing Algorithm:**

**1. Different Element Types:**
```javascript
// Old tree
<div>
  <Counter />
</div>

// New tree
<span>
  <Counter />
</span>

// React's action: Destroy old div and Counter, create new span and Counter
// Counter loses its state!
```

**2. Same Element Type, Different Attributes:**
```javascript
// Old
<div className="before" title="old" />

// New
<div className="after" title="new" />

// React's action: Keep same DOM node, update only className and title
// Efficient - no DOM node recreation
```

**3. Recursing on Children:**
```javascript
// Old
<ul>
  <li>First</li>
  <li>Second</li>
</ul>

// New
<ul>
  <li>First</li>
  <li>Second</li>
  <li>Third</li>
</ul>

// React's action: Keep first two <li>, add third
// Efficient - adds only new element
```

**4. Keys - The Optimization Secret:**

**❌ Bad Example (Without Keys):**
```javascript
// Old
<ul>
  <li>Duke</li>
  <li>Villanova</li>
</ul>

// New - inserted at beginning
<ul>
  <li>Connecticut</li>
  <li>Duke</li>
  <li>Villanova</li>
</ul>

// Without keys, React mutates ALL three children
// Inefficient - recreates all <li> elements
```

**✅ Good Example (With Keys):**
```javascript
// Old
<ul>
  <li key="duke">Duke</li>
  <li key="villanova">Villanova</li>
</ul>

// New
<ul>
  <li key="connecticut">Connecticut</li>
  <li key="duke">Duke</li>
  <li key="villanova">Villanova</li>
</ul>

// With keys, React knows duke and villanova moved
// Efficient - reuses existing DOM nodes, inserts only Connecticut
```

---

### 🔍 Internal Reconciliation Process

**Phase 1: Render Phase (Can be interrupted)**

```javascript
// Simplified reconciliation logic
function reconcileChildren(fiber, newChildren) {
  let oldFiber = fiber.alternate?.child;
  let prevSibling = null;
  let index = 0;

  while (index < newChildren.length || oldFiber != null) {
    const newChild = newChildren[index];
    let newFiber = null;

    // Compare oldFiber with newChild
    const sameType = oldFiber && newChild && 
                     oldFiber.type === newChild.type;

    if (sameType) {
      // UPDATE: Same type, reuse DOM node
      newFiber = {
        type: oldFiber.type,
        props: newChild.props,
        dom: oldFiber.dom,        // Reuse existing DOM
        parent: fiber,
        alternate: oldFiber,
        effectTag: 'UPDATE'        // Mark for update
      };
    }

    if (newChild && !sameType) {
      // PLACEMENT: New element
      newFiber = {
        type: newChild.type,
        props: newChild.props,
        dom: null,                 // Create new DOM
        parent: fiber,
        alternate: null,
        effectTag: 'PLACEMENT'     // Mark for insertion
      };
    }

    if (oldFiber && !sameType) {
      // DELETION: Remove old element
      oldFiber.effectTag = 'DELETION';
      deletions.push(oldFiber);
    }

    if (oldFiber) {
      oldFiber = oldFiber.sibling;
    }

    if (index === 0) {
      fiber.child = newFiber;
    } else if (newChild) {
      prevSibling.sibling = newFiber;
    }

    prevSibling = newFiber;
    index++;
  }
}
```

**Phase 2: Commit Phase (Cannot be interrupted)**

```javascript
function commitWork(fiber) {
  if (!fiber) return;

  const domParent = fiber.parent.dom;

  if (fiber.effectTag === 'PLACEMENT' && fiber.dom != null) {
    // Add new node
    domParent.appendChild(fiber.dom);
  } else if (fiber.effectTag === 'UPDATE' && fiber.dom != null) {
    // Update existing node
    updateDOM(fiber.dom, fiber.alternate.props, fiber.props);
  } else if (fiber.effectTag === 'DELETION') {
    // Remove node
    domParent.removeChild(fiber.dom);
  }

  commitWork(fiber.child);
  commitWork(fiber.sibling);
}

function updateDOM(dom, prevProps, nextProps) {
  // Remove old properties
  Object.keys(prevProps)
    .filter(isProperty)
    .filter(isGone(prevProps, nextProps))
    .forEach(name => {
      dom[name] = '';
    });

  // Set new or changed properties
  Object.keys(nextProps)
    .filter(isProperty)
    .filter(isNew(prevProps, nextProps))
    .forEach(name => {
      dom[name] = nextProps[name];
    });

  // Remove old event listeners
  Object.keys(prevProps)
    .filter(isEvent)
    .filter(key => !(key in nextProps) || isNew(prevProps, nextProps)(key))
    .forEach(name => {
      const eventType = name.toLowerCase().substring(2);
      dom.removeEventListener(eventType, prevProps[name]);
    });

  // Add new event listeners
  Object.keys(nextProps)
    .filter(isEvent)
    .filter(isNew(prevProps, nextProps))
    .forEach(name => {
      const eventType = name.toLowerCase().substring(2);
      dom.addEventListener(eventType, nextProps[name]);
    });
}
```

---

**Key Optimization Rules:**

**1. Element Type Matters:**
```javascript
// Changing element type destroys entire subtree
function MyComponent({ isSpecial }) {
  if (isSpecial) {
    return <div><ExpensiveComponent /></div>;
  }
  return <span><ExpensiveComponent /></span>; // Remounts ExpensiveComponent!
}

// Better: Keep same element type
function MyComponent({ isSpecial }) {
  return (
    <div className={isSpecial ? 'special' : 'normal'}>
      <ExpensiveComponent /> {/* Preserved! */}
    </div>
  );
}
```

**2. Keys Must Be Stable:**
```javascript
// ❌ Bad: Using index as key
{items.map((item, index) => (
  <Item key={index} {...item} /> // Breaks when list reorders
))}

// ❌ Bad: Using random keys
{items.map(item => (
  <Item key={Math.random()} {...item} /> // Recreates every render!
))}

// ✅ Good: Using stable unique ID
{items.map(item => (
  <Item key={item.id} {...item} /> // Stable across renders
))}
```

**3. Component Position Matters:**
```javascript
// Different positions = different components
function App({ showFirst }) {
  if (showFirst) {
    return (
      <>
        <Counter /> {/* Position 1 */}
        <div />
      </>
    );
  }
  return (
    <>
      <div />
      <Counter /> {/* Position 2 - Different! Remounts! */}
    </>
  );
}

// Better: Same position
function App({ showFirst }) {
  return (
    <>
      {showFirst && <Counter />} {/* Always position 1 */}
      <div />
    </>
  );
}
```

**Interview Tip:**
> "Reconciliation uses a heuristic O(n) algorithm that compares trees level by level, assuming elements of different types produce different trees, and uses keys to identify which children have moved, changed, or been added/removed."

---

## Fiber Architecture

### 🎯 What is Fiber?

**Definition:**
> Fiber is React's internal reconciliation engine redesigned in React 16+ to enable incremental rendering - the ability to split rendering work into chunks and spread it across multiple frames.

**Simple meaning:**
Fiber is React's way of breaking down rendering work into small pieces so the browser can handle user interactions (clicks, typing) without freezing, even during heavy updates.

**Real-life analogy:**
Like a chef preparing multiple dishes - instead of finishing one dish completely before starting another (blocking), they work on multiple dishes in small steps (non-blocking), checking if any customer needs immediate attention.

---

### 🔧 How Fiber Works Internally

**Fiber Data Structure:**

```javascript
// Each React element becomes a Fiber node
const fiber = {
  // Instance
  type: 'div',                    // Component type or DOM tag
  key: null,                      // Unique key
  
  // Fiber relationships (linked list)
  parent: parentFiber,            // Parent fiber
  child: firstChildFiber,         // First child
  sibling: nextSiblingFiber,      // Next sibling
  
  // State
  props: { className: 'app' },    // Current props
  state: { count: 0 },            // Current state
  hooks: [],                      // Hooks linked list
  
  // Effects
  effectTag: 'UPDATE',            // What to do: PLACEMENT, UPDATE, DELETION
  effects: [],                    // Side effects to perform
  
  // Alternate (double buffering)
  alternate: oldFiber,            // Previous fiber (for comparison)
  
  // Work
  pendingProps: {},               // Props for this update
  memoizedProps: {},              // Props from last render
  memoizedState: {},              // State from last render
  
  // Scheduling
  expirationTime: 0,              // When this work expires
  childExpirationTime: 0,         // Earliest expiration in subtree
};
```

---

**Fiber Work Loop:**

```javascript
// Simplified Fiber work loop
let nextUnitOfWork = null;
let wipRoot = null;           // Work in progress root
let currentRoot = null;       // Last committed root
let deletions = [];

function workLoop(deadline) {
  let shouldYield = false;

  // Process fibers until we run out of time
  while (nextUnitOfWork && !shouldYield) {
    nextUnitOfWork = performUnitOfWork(nextUnitOfWork);
    
    // Check if we have time left in this frame
    shouldYield = deadline.timeRemaining() < 1;
  }

  // If no more work, commit to DOM
  if (!nextUnitOfWork && wipRoot) {
    commitRoot();
  }

  // Schedule next work loop
  requestIdleCallback(workLoop);
}

// Start the work loop
requestIdleCallback(workLoop);
```

**Perform Unit of Work:**

```javascript
function performUnitOfWork(fiber) {
  // 1. PERFORM WORK: Create/update DOM node
  if (!fiber.dom) {
    fiber.dom = createDOM(fiber);
  }

  // 2. CREATE FIBERS: Create fibers for children
  const elements = fiber.props.children;
  reconcileChildren(fiber, elements);

  // 3. RETURN NEXT UNIT OF WORK
  // Try child first (depth-first)
  if (fiber.child) {
    return fiber.child;
  }

  // Then sibling
  let nextFiber = fiber;
  while (nextFiber) {
    if (nextFiber.sibling) {
      return nextFiber.sibling;
    }
    // Go up to parent
    nextFiber = nextFiber.parent;
  }

  // No more work
  return null;
}
```

---

**Fiber Tree Traversal:**

```javascript
// Example component tree
<App>
  <Header>
    <Logo />
    <Nav />
  </Header>
  <Main>
    <Content />
  </Main>
</App>

// Fiber tree structure (linked list)
App (fiber)
├─ child → Header
│          ├─ child → Logo
│          │          └─ sibling → Nav
│          └─ sibling → Main
│                       └─ child → Content
└─ parent ← (all point back to parents)

// Traversal order (depth-first):
// 1. App
// 2. Header (App's child)
// 3. Logo (Header's child)
// 4. Nav (Logo's sibling)
// 5. Main (Header's sibling)
// 6. Content (Main's child)
```

---

**Double Buffering (Alternate):**

```javascript
// React maintains TWO fiber trees
const current = {
  // Current tree (on screen)
  type: 'div',
  props: { count: 0 },
  dom: actualDOMNode,
  alternate: workInProgress  // Points to WIP tree
};

const workInProgress = {
  // Work in progress tree (being built)
  type: 'div',
  props: { count: 1 },       // New props
  dom: actualDOMNode,         // Reuses same DOM
  alternate: current          // Points back to current
};

// After commit, WIP becomes current
// Old current becomes new WIP for next update
function commitRoot() {
  // Apply all changes
  commitWork(wipRoot.child);
  
  // Swap trees
  currentRoot = wipRoot;      // WIP becomes current
  wipRoot = null;
}
```

---

**Priority and Scheduling:**

```javascript
// Different update priorities
const ImmediatePriority = 1;      // User input, clicks
const UserBlockingPriority = 2;   // User interactions
const NormalPriority = 3;         // Network responses
const LowPriority = 4;            // Analytics
const IdlePriority = 5;           // Background work

// Scheduling updates by priority
function scheduleUpdateOnFiber(fiber, expirationTime) {
  // Mark fiber as needing update
  fiber.expirationTime = expirationTime;
  
  // Bubble up to root
  let node = fiber;
  while (node.parent) {
    // Update parent's child expiration time
    if (node.parent.childExpirationTime < expirationTime) {
      node.parent.childExpirationTime = expirationTime;
    }
    node = node.parent;
  }
  
  // Schedule work on root
  scheduleWork(node, expirationTime);
}

// Process high priority work first
function getNextUnitOfWork() {
  // Find fiber with earliest expiration time
  let nextFiber = findFiberWithEarliestExpiration(wipRoot);
  return nextFiber;
}
```

---

**Interruptible Rendering:**

```javascript
// Example: Heavy rendering with interruption
function HeavyList({ items }) {
  return (
    <ul>
      {items.map(item => (
        <ExpensiveItem key={item.id} data={item} />
      ))}
    </ul>
  );
}

// Fiber breaks this into units:
// Frame 1 (16ms): Render <ul> and first 10 items
// User clicks button - HIGH PRIORITY!
// Frame 2: Handle button click (interrupts list)
// Frame 3: Resume rendering items 11-20
// Frame 4: Render items 21-30
// ...continues until done

// Without Fiber (React 15):
// Renders ALL items in one go - UI freezes
// User click waits until rendering completes
```

---

**Benefits:**
- ✅ **Non-blocking rendering** - UI stays responsive during heavy updates
- ✅ **Priority-based updates** - User interactions processed first
- ✅ **Incremental rendering** - Work split across multiple frames
- ✅ **Better error handling** - Error boundaries work better
- ✅ **Concurrent features** - Enables Suspense, Transitions, etc.

**Trade-offs:**

| Benefit | Cost |
|---------|------|
| **Smooth UI** | More complex internal architecture |
| **Interruptible** | Slightly more memory (two trees) |
| **Prioritization** | More CPU scheduling overhead |

**Interview Tip:**
> "Fiber is React's reconciliation engine that uses a linked-list tree structure to enable incremental rendering, allowing React to pause work, prioritize updates, and split rendering across multiple frames for better performance."

---

## JSX

### 🎯 What is JSX?

**Definition:**
> JSX (JavaScript XML) is a syntax extension for JavaScript that lets you write HTML-like code in JavaScript, which gets transformed into React.createElement() calls.

**Simple meaning:**
JSX lets you write HTML inside JavaScript - it looks like HTML but it's actually JavaScript that creates React elements.

**Real-life analogy:**
JSX is like a translator - you speak in a language that looks like HTML (easy to read), and it translates to JavaScript function calls (what React understands).

---

### 🔧 How JSX Works Internally

**JSX Transformation:**

```javascript
// What you write (JSX)
const element = (
  <div className="container">
    <h1>Hello, {name}!</h1>
    <p>Welcome to React</p>
  </div>
);

// What Babel transforms it to (JavaScript)
const element = React.createElement(
  'div',
  { className: 'container' },
  React.createElement('h1', null, 'Hello, ', name, '!'),
  React.createElement('p', null, 'Welcome to React')
);

// What React creates (Virtual DOM object)
const element = {
  type: 'div',
  props: {
    className: 'container',
    children: [
      {
        type: 'h1',
        props: {
          children: ['Hello, ', name, '!']
        }
      },
      {
        type: 'p',
        props: {
          children: ['Welcome to React']
        }
      }
    ]
  }
};
```

---

**React.createElement Implementation:**

```javascript
// Simplified React.createElement
function createElement(type, props, ...children) {
  return {
    type,
    props: {
      ...props,
      children: children.map(child =>
        typeof child === 'object'
          ? child
          : createTextElement(child)
      )
    }
  };
}

function createTextElement(text) {
  return {
    type: 'TEXT_ELEMENT',
    props: {
      nodeValue: text,
      children: []
    }
  };
}

// Usage
createElement('div', { id: 'app' }, 
  createElement('h1', null, 'Title'),
  'Some text'
);
```

---

**JSX Rules and Features:**

**1. JavaScript Expressions:**
```javascript
// ✅ Any JavaScript expression works in {}
const name = 'John';
const element = <h1>Hello, {name}!</h1>;

const user = { firstName: 'John', lastName: 'Doe' };
const greeting = <h1>Hello, {user.firstName + ' ' + user.lastName}!</h1>;

const numbers = [1, 2, 3];
const list = <ul>{numbers.map(n => <li key={n}>{n}</li>)}</ul>;

// ❌ Statements don't work
const bad = <div>{if (true) { 'text' }}</div>; // Error!

// ✅ Use ternary or && instead
const good = <div>{true ? 'text' : null}</div>;
const better = <div>{true && 'text'}</div>;
```

**2. Attributes:**
```javascript
// camelCase for DOM properties
<div 
  className="container"      // not 'class'
  htmlFor="input"            // not 'for'
  onClick={handleClick}      // not 'onclick'
  tabIndex={0}
  style={{ color: 'red' }}   // object, not string
/>

// How React processes attributes
function setAttributes(dom, props) {
  Object.keys(props)
    .filter(key => key !== 'children')
    .forEach(name => {
      if (name.startsWith('on')) {
        // Event listener
        const eventType = name.toLowerCase().substring(2);
        dom.addEventListener(eventType, props[name]);
      } else if (name === 'className') {
        dom.className = props[name];
      } else if (name === 'style') {
        Object.assign(dom.style, props[name]);
      } else {
        dom[name] = props[name];
      }
    });
}
```

**3. Children:**
```javascript
// Multiple ways to pass children
// 1. Nested JSX
<div>
  <h1>Title</h1>
  <p>Content</p>
</div>

// 2. Array
<div>
  {[
    <h1 key="1">Title</h1>,
    <p key="2">Content</p>
  ]}
</div>

// 3. Children prop
<div children={<h1>Title</h1>} />

// All transform to:
React.createElement('div', null,
  React.createElement('h1', null, 'Title'),
  React.createElement('p', null, 'Content')
);
```

**4. Fragments:**
```javascript
// Problem: JSX needs single root
// ❌ This doesn't work
return (
  <h1>Title</h1>
  <p>Content</p>
);

// ✅ Solution 1: Wrapper div
return (
  <div>
    <h1>Title</h1>
    <p>Content</p>
  </div>
);

// ✅ Solution 2: Fragment (no extra DOM node)
return (
  <React.Fragment>
    <h1>Title</h1>
    <p>Content</p>
  </React.Fragment>
);

// ✅ Solution 3: Short syntax
return (
  <>
    <h1>Title</h1>
    <p>Content</p>
  </>
);

// Transforms to:
React.createElement(React.Fragment, null,
  React.createElement('h1', null, 'Title'),
  React.createElement('p', null, 'Content')
);
```

---

**JSX Compilation Process:**

```javascript
// Step 1: Source code (JSX)
function App() {
  return <div className="app">Hello</div>;
}

// Step 2: Babel transforms JSX
function App() {
  return React.createElement('div', { className: 'app' }, 'Hello');
}

// Step 3: React creates element object
{
  type: 'div',
  props: {
    className: 'app',
    children: ['Hello']
  },
  key: null,
  ref: null
}

// Step 4: React creates Fiber node
{
  type: 'div',
  props: { className: 'app', children: ['Hello'] },
  dom: null,
  parent: parentFiber,
  child: null,
  sibling: null,
  alternate: null,
  effectTag: 'PLACEMENT'
}

// Step 5: React creates real DOM
const dom = document.createElement('div');
dom.className = 'app';
dom.textContent = 'Hello';
```

---

**Advanced JSX Patterns:**

**1. Conditional Rendering:**
```javascript
// && operator
{isLoggedIn && <Dashboard />}

// Ternary
{isLoggedIn ? <Dashboard /> : <Login />}

// Variable
let content;
if (isLoggedIn) {
  content = <Dashboard />;
} else {
  content = <Login />;
}
return <div>{content}</div>;

// IIFE (Immediately Invoked Function Expression)
{(() => {
  if (status === 'loading') return <Spinner />;
  if (status === 'error') return <Error />;
  return <Content />;
})()}
```

**2. Lists and Keys:**
```javascript
// Keys help React identify which items changed
const items = ['Apple', 'Banana', 'Orange'];

// ✅ Good: Unique stable keys
{items.map((item, index) => (
  <li key={item}>{item}</li>
))}

// How React uses keys internally
function reconcileChildren(fiber, newChildren) {
  // Create map of old children by key
  const existingChildren = new Map();
  let oldFiber = fiber.alternate?.child;
  while (oldFiber) {
    if (oldFiber.key !== null) {
      existingChildren.set(oldFiber.key, oldFiber);
    }
    oldFiber = oldFiber.sibling;
  }

  // Match new children with old by key
  newChildren.forEach(newChild => {
    if (existingChildren.has(newChild.key)) {
      // Reuse existing fiber
      const oldFiber = existingChildren.get(newChild.key);
      // Update props, keep DOM node
    } else {
      // Create new fiber
    }
  });
}
```

**3. Spread Attributes:**
```javascript
const props = {
  className: 'button',
  onClick: handleClick,
  disabled: false
};

// Spread props
<button {...props}>Click me</button>

// Transforms to:
React.createElement('button', props, 'Click me');

// Override specific props
<button {...props} className="special-button">
  Click me
</button>

// className becomes 'special-button' (overrides spread)
```

**Interview Tip:**
> "JSX is syntactic sugar for React.createElement() calls. Babel transforms JSX into JavaScript, creating React element objects that describe the UI structure, which React then uses to build the Virtual DOM and eventually the real DOM."

---

## Functional Components

### 🎯 What are Functional Components?

**Definition:**
> Functional components are JavaScript functions that accept props as an argument and return React elements (JSX), representing a piece of UI.

**Simple meaning:**
A functional component is just a function that takes data (props) and returns what to display (JSX).

**Real-life analogy:**
Like a vending machine - you put in money (props), and it gives you a snack (JSX). Same input always gives same output.

---

### 🔧 How Functional Components Work

**Basic Structure:**

```javascript
// Simple functional component
function Welcome(props) {
  return <h1>Hello, {props.name}!</h1>;
}

// Arrow function syntax
const Welcome = (props) => {
  return <h1>Hello, {props.name}!</h1>;
};

// Implicit return (no curly braces)
const Welcome = (props) => <h1>Hello, {props.name}!</h1>;

// Destructured props
const Welcome = ({ name }) => <h1>Hello, {name}!</h1>;
```

---

**How React Processes Functional Components:**

```javascript
// Your component
function Welcome({ name }) {
  return <h1>Hello, {name}!</h1>;
}

// Usage
<Welcome name="John" />

// React's internal process:
// 1. Create fiber for Welcome component
const fiber = {
  type: Welcome,              // Function reference
  props: { name: 'John' },
  // ...other fiber properties
};

// 2. Call the function to get elements
const elements = fiber.type(fiber.props);
// Returns: <h1>Hello, John!</h1>

// 3. Transform JSX to element object
const element = {
  type: 'h1',
  props: {
    children: ['Hello, ', 'John', '!']
  }
};

// 4. Create fiber for returned element
const h1Fiber = {
  type: 'h1',
  props: { children: ['Hello, ', 'John', '!'] },
  parent: fiber,
  // ...
};

// 5. Create DOM node
const dom = document.createElement('h1');
dom.textContent = 'Hello, John!';
```

---

**Component Lifecycle in Functional Components:**

```javascript
function MyComponent({ data }) {
  // 1. RENDER PHASE
  // Component function executes
  console.log('Rendering...');
  
  // Hooks are called in order
  const [count, setCount] = useState(0);
  const [name, setName] = useState('John');
  
  // Effects are scheduled (not executed yet)
  useEffect(() => {
    console.log('Effect will run after commit');
  });
  
  // Calculations and logic
  const doubled = count * 2;
  
  // 2. RETURN JSX
  return (
    <div>
      <p>{name}: {doubled}</p>
      <button onClick={() => setCount(count + 1)}>
        Increment
      </button>
    </div>
  );
  
  // 3. COMMIT PHASE (after return)
  // - React updates DOM
  // - useLayoutEffect runs (synchronous)
  // - Browser paints
  // - useEffect runs (asynchronous)
}
```

---

**Component Re-rendering:**

```javascript
// What triggers re-render?
function Counter() {
  const [count, setCount] = useState(0);
  
  console.log('Component renders'); // Logs on every render
  
  // 1. State change triggers re-render
  const handleClick = () => {
    setCount(count + 1); // Schedules re-render
  };
  
  return <button onClick={handleClick}>{count}</button>;
}

// Internal re-render process:
function scheduleUpdate(fiber, update) {
  // 1. Add update to fiber's update queue
  fiber.updateQueue.push(update);
  
  // 2. Mark fiber as needing work
  fiber.expirationTime = computeExpirationTime();
  
  // 3. Schedule work on root
  scheduleWorkOnRoot(fiber);
}

function processUpdateQueue(fiber) {
  // Process all queued updates
  let newState = fiber.memoizedState;
  
  fiber.updateQueue.forEach(update => {
    // If update is a function, call it with current state
    newState = typeof update === 'function' 
      ? update(newState) 
      : update;
  });
  
  fiber.memoizedState = newState;
  fiber.updateQueue = [];
}

// Re-render flow:
// 1. setState called
// 2. Update queued
// 3. Fiber marked for update
// 4. Work scheduled
// 5. Component function called again
// 6. New JSX compared with old
// 7. DOM updated if needed
```

---

**Props Flow:**

```javascript
// Parent component
function App() {
  const [user, setUser] = useState({ name: 'John', age: 30 });
  
  return <UserProfile user={user} onUpdate={setUser} />;
}

// Child component
function UserProfile({ user, onUpdate }) {
  // Props are read-only!
  // user.name = 'Jane'; // ❌ Never mutate props
  
  const handleUpdate = () => {
    // ✅ Call parent's function to update
    onUpdate({ ...user, age: user.age + 1 });
  };
  
  return (
    <div>
      <p>{user.name} is {user.age}</p>
      <button onClick={handleUpdate}>Birthday</button>
    </div>
  );
}

// How React passes props:
function renderComponent(fiber) {
  // Get component function
  const Component = fiber.type;
  
  // Get props from fiber
  const props = fiber.props;
  
  // Call component with props
  const elements = Component(props);
  
  // Component receives fresh props object every render
  // Props are immutable - new object each time
  return elements;
}
```

---

**Component Composition:**

```javascript
// Container component
function Card({ title, children }) {
  return (
    <div className="card">
      <h2>{title}</h2>
      <div className="card-body">
        {children}
      </div>
    </div>
  );
}

// Usage - composing components
function App() {
  return (
    <Card title="User Info">
      <p>Name: John</p>
      <p>Age: 30</p>
      <button>Edit</button>
    </Card>
  );
}

// How children prop works:
// JSX:
<Card title="User Info">
  <p>Name: John</p>
</Card>

// Transforms to:
React.createElement(
  Card,
  { title: 'User Info' },
  React.createElement('p', null, 'Name: John')
);

// Card receives:
{
  title: 'User Info',
  children: {
    type: 'p',
    props: { children: 'Name: John' }
  }
}
```

---

**Pure Components:**

```javascript
// Pure component - same props = same output
function PureGreeting({ name }) {
  return <h1>Hello, {name}!</h1>;
}

// Impure component - uses external data
let globalCount = 0;
function ImpureCounter() {
  return <p>{globalCount++}</p>; // ❌ Side effect in render
}

// React.memo - memoizes functional component
const MemoizedGreeting = React.memo(function Greeting({ name }) {
  console.log('Rendering Greeting');
  return <h1>Hello, {name}!</h1>;
});

// How React.memo works internally:
function memo(Component) {
  return function MemoizedComponent(props) {
    // Get previous props from fiber
    const prevProps = fiber.alternate?.memoizedProps;
    
    // Shallow compare props
    if (prevProps && shallowEqual(prevProps, props)) {
      // Props haven't changed, reuse previous result
      return fiber.alternate.child;
    }
    
    // Props changed, re-render
    return Component(props);
  };
}

function shallowEqual(obj1, obj2) {
  const keys1 = Object.keys(obj1);
  const keys2 = Object.keys(obj2);
  
  if (keys1.length !== keys2.length) return false;
  
  return keys1.every(key => obj1[key] === obj2[key]);
}
```

---

**Benefits:**
- ✅ **Simpler** - Just JavaScript functions, no class syntax
- ✅ **Less code** - No constructor, this, or binding
- ✅ **Hooks** - Access state and lifecycle without classes
- ✅ **Easier testing** - Pure functions are easy to test
- ✅ **Better performance** - Smaller bundle size, easier optimization

**Interview Tip:**
> "Functional components are JavaScript functions that take props and return JSX. With hooks, they can manage state and side effects, making them the preferred way to write React components over class components."

---

## useState

### 🎯 What is useState?

**Definition:**
> useState is a React Hook that lets you add state to functional components, returning the current state value and a function to update it.

**Simple meaning:**
useState lets your component "remember" values between renders - when you update the value, React re-renders the component with the new value.

**Real-life analogy:**
Like a sticky note on your desk - you write something (state), and it stays there (persists) until you change it (setState). When you change it, you see the new value.

---

### 🔧 How useState Works Internally

**Basic Usage:**

```javascript
function Counter() {
  // Declare state variable
  const [count, setCount] = useState(0);
  //     ↑       ↑         ↑
  //   value  updater   initial value
  
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        Increment
      </button>
    </div>
  );
}
```

---

**Internal Implementation:**

```javascript
// Simplified useState implementation
let currentFiber = null;  // Current component fiber
let hookIndex = 0;        // Current hook index

function useState(initialValue) {
  // Get current fiber's hooks array
  const fiber = currentFiber;
  const hooks = fiber.hooks || [];
  const hook = hooks[hookIndex];
  
  // First render - initialize hook
  if (!hook) {
    const newHook = {
      state: typeof initialValue === 'function' 
        ? initialValue() 
        : initialValue,
      queue: []  // Update queue
    };
    hooks[hookIndex] = newHook;
  }
  
  // Get hook for this useState call
  const currentHook = hooks[hookIndex];
  
  // Process queued updates
  currentHook.queue.forEach(update => {
    currentHook.state = typeof update === 'function'
      ? update(currentHook.state)
      : update;
  });
  currentHook.queue = [];
  
  // Create setState function
  const setState = (update) => {
    // Add update to queue
    currentHook.queue.push(update);
    
    // Schedule re-render
    scheduleUpdate(fiber);
  };
  
  // Move to next hook
  hookIndex++;
  
  // Return state and setter
  return [currentHook.state, setState];
}

// Before rendering component
function prepareToRender(fiber) {
  currentFiber = fiber;
  hookIndex = 0;
}

// Render component
function renderComponent(fiber) {
  prepareToRender(fiber);
  const Component = fiber.type;
  const elements = Component(fiber.props);
  return elements;
}
```

---

**Hook Storage in Fiber:**

```javascript
// Each component fiber has a hooks linked list
const fiber = {
  type: Counter,
  props: {},
  hooks: [
    // Hook 0: useState(0)
    {
      state: 0,
      queue: [],
      next: /* Hook 1 */
    },
    // Hook 1: useState('')
    {
      state: '',
      queue: [],
      next: /* Hook 2 */
    },
    // Hook 2: useEffect(...)
    {
      effect: () => {},
      deps: [],
      next: null
    }
  ]
};

// Hooks MUST be called in same order every render
// This is why hooks can't be in conditions/loops
```

---

**State Updates:**

**1. Direct Value:**
```javascript
const [count, setCount] = useState(0);

// Direct value update
setCount(5);  // Next render: count = 5

// Internal process:
function setState(update) {
  // Add to queue
  hook.queue.push(update);  // queue = [5]
  
  // Schedule re-render
  scheduleUpdate(fiber);
}

// On next render:
hook.state = hook.queue[0];  // state = 5
hook.queue = [];
```

**2. Functional Update:**
```javascript
const [count, setCount] = useState(0);

// Functional update - receives previous state
setCount(prevCount => prevCount + 1);

// Why functional updates matter:
function handleClick() {
  // ❌ Bad: Uses stale state
  setCount(count + 1);  // count = 0
  setCount(count + 1);  // count = 0 (still!)
  // Result: count = 1 (not 2!)
  
  // ✅ Good: Uses previous state
  setCount(prev => prev + 1);  // prev = 0, sets 1
  setCount(prev => prev + 1);  // prev = 1, sets 2
  // Result: count = 2 ✓
}

// Internal process:
function processUpdates(hook) {
  let newState = hook.state;
  
  hook.queue.forEach(update => {
    if (typeof update === 'function') {
      newState = update(newState);  // Pass current state
    } else {
      newState = update;
    }
  });
  
  hook.state = newState;
  hook.queue = [];
}
```

**3. Lazy Initialization:**
```javascript
// ❌ Expensive computation runs every render
const [data, setData] = useState(expensiveComputation());

// ✅ Computation runs only once (initial render)
const [data, setData] = useState(() => expensiveComputation());

// Internal implementation:
function useState(initialValue) {
  const hook = hooks[hookIndex];
  
  if (!hook) {
    // First render
    const newHook = {
      state: typeof initialValue === 'function'
        ? initialValue()  // Call function only once
        : initialValue,
      queue: []
    };
    hooks[hookIndex] = newHook;
  }
  
  // Subsequent renders: initialValue is ignored
  return [hooks[hookIndex].state, setState];
}
```

---

**State Batching:**

```javascript
function Counter() {
  const [count, setCount] = useState(0);
  
  const handleClick = () => {
    console.log('Before:', count);  // 0
    
    setCount(count + 1);  // Queued
    setCount(count + 1);  // Queued
    setCount(count + 1);  // Queued
    
    console.log('After:', count);   // Still 0! (not updated yet)
    
    // React batches these updates
    // Only one re-render happens
    // Final count = 1 (not 3!)
  };
  
  return <button onClick={handleClick}>{count}</button>;
}

// How batching works internally:
let isBatchingUpdates = false;
let updateQueue = [];

function batchedUpdates(fn) {
  isBatchingUpdates = true;
  try {
    fn();  // Execute event handler
  } finally {
    isBatchingUpdates = false;
    flushUpdates();  // Process all queued updates
  }
}

function scheduleUpdate(fiber) {
  if (isBatchingUpdates) {
    // Add to queue
    updateQueue.push(fiber);
  } else {
    // Update immediately
    performUpdate(fiber);
  }
}

function flushUpdates() {
  // Process all queued updates together
  updateQueue.forEach(fiber => performUpdate(fiber));
  updateQueue = [];
}

// React wraps event handlers in batchedUpdates
<button onClick={batchedUpdates(() => handleClick())} />
```

---

**Multiple State Variables:**

```javascript
function Form() {
  // Each useState call creates separate hook
  const [name, setName] = useState('');      // Hook 0
  const [email, setEmail] = useState('');    // Hook 1
  const [age, setAge] = useState(0);         // Hook 2
  
  // Stored in fiber as:
  // hooks[0] = { state: '', queue: [] }
  // hooks[1] = { state: '', queue: [] }
  // hooks[2] = { state: 0, queue: [] }
  
  return (
    <form>
      <input value={name} onChange={e => setName(e.target.value)} />
      <input value={email} onChange={e => setEmail(e.target.value)} />
      <input value={age} onChange={e => setAge(Number(e.target.value))} />
    </form>
  );
}

// Why hook order matters:
function BadExample({ condition }) {
  // ❌ WRONG: Conditional hook
  if (condition) {
    const [name, setName] = useState('');  // Sometimes Hook 0
  }
  const [age, setAge] = useState(0);       // Sometimes Hook 0, sometimes Hook 1
  
  // Render 1 (condition=true):  hooks[0]=name, hooks[1]=age
  // Render 2 (condition=false): hooks[0]=age
  // Hook mismatch! Age gets name's state!
}

function GoodExample({ condition }) {
  // ✅ CORRECT: Always same hooks
  const [name, setName] = useState('');    // Always Hook 0
  const [age, setAge] = useState(0);       // Always Hook 1
  
  if (condition) {
    // Use the state conditionally, not the hook
    return <div>{name}</div>;
  }
  return <div>{age}</div>;
}
```

---

**Object and Array State:**

```javascript
// Objects
const [user, setUser] = useState({ name: 'John', age: 30 });

// ❌ Bad: Mutating state
user.age = 31;           // Doesn't trigger re-render
setUser(user);           // Still doesn't work (same reference)

// ✅ Good: Create new object
setUser({ ...user, age: 31 });

// Arrays
const [items, setItems] = useState([1, 2, 3]);

// ❌ Bad: Mutating array
items.push(4);           // Doesn't trigger re-render
setItems(items);         // Doesn't work

// ✅ Good: Create new array
setItems([...items, 4]);
setItems(items.concat(4));

// Why immutability matters:
function checkIfStateChanged(oldState, newState) {
  // React uses Object.is() for comparison
  return !Object.is(oldState, newState);
}

const oldUser = { name: 'John' };
const newUser = oldUser;
newUser.name = 'Jane';

Object.is(oldUser, newUser);  // true - same reference!
// React thinks nothing changed, no re-render

const newerUser = { ...oldUser, name: 'Jane' };
Object.is(oldUser, newerUser);  // false - different reference
// React detects change, triggers re-render
```

---

**State Update Timing:**

```javascript
function Counter() {
  const [count, setCount] = useState(0);
  
  const handleClick = () => {
    console.log('1. Before setState:', count);  // 0
    
    setCount(count + 1);
    
    console.log('2. After setState:', count);   // Still 0!
    
    // State doesn't update immediately
    // Update is scheduled for next render
  };
  
  // After re-render, count = 1
  console.log('3. During render:', count);
  
  useEffect(() => {
    console.log('4. After commit:', count);     // 1
  });
  
  return <button onClick={handleClick}>{count}</button>;
}

// Timeline:
// 1. User clicks button
// 2. handleClick executes
//    - Logs "Before: 0"
//    - Queues update
//    - Logs "After: 0" (not updated yet)
// 3. React schedules re-render
// 4. Component function runs again
//    - Logs "During render: 1"
//    - Returns new JSX
// 5. React commits to DOM
// 6. useEffect runs
//    - Logs "After commit: 1"
```

---

**Benefits:**
- ✅ **Simple API** - Easy to understand and use
- ✅ **Automatic re-renders** - React handles updates
- ✅ **Multiple states** - Can have many useState calls
- ✅ **Functional updates** - Access previous state reliably
- ✅ **Lazy initialization** - Optimize expensive initial values

**Trade-offs:**

| Benefit | Cost |
|---------|------|
| **Automatic updates** | Must follow hooks rules (order, no conditions) |
| **Simple API** | Complex state logic can get messy |
| **Multiple states** | Many useState calls can be verbose |

**When to use useState:**
- ✅ Simple local component state
- ✅ Independent state values
- ✅ Form inputs
- ✅ Toggle states (open/closed, visible/hidden)
- ❌ Avoid for complex state logic (use useReducer)
- ❌ Avoid for global state (use Context or state management library)

**Interview Tip:**
> "useState returns a stateful value and an updater function. React stores hooks in a linked list on the component's fiber, which is why hooks must be called in the same order every render. State updates are batched and processed asynchronously, triggering re-renders only when the state reference changes."

---

## useEffect

### 🎯 What is useEffect?

**Definition:**
> useEffect is a React Hook that lets you perform side effects in functional components, running after the component renders and optionally cleaning up before the next effect or unmount.

**Simple meaning:**
useEffect lets you run code after React updates the screen - perfect for data fetching, subscriptions, or manually changing the DOM.

**Real-life analogy:**
Like setting up and cleaning up after a party - useEffect sets things up after guests arrive (render), and cleans up before they leave (unmount) or before the next party (re-render).

---

### 🔧 How useEffect Works Internally

**Basic Usage:**

```javascript
function Example() {
  const [count, setCount] = useState(0);
  
  // Runs after every render
  useEffect(() => {
    document.title = `Count: ${count}`;
  });
  
  return <button onClick={() => setCount(count + 1)}>{count}</button>;
}
```

---

**Internal Implementation:**

```javascript
// Simplified useEffect implementation
function useEffect(effect, deps) {
  const fiber = currentFiber;
  const hooks = fiber.hooks || [];
  const hook = hooks[hookIndex];
  
  // First render - create hook
  if (!hook) {
    const newHook = {
      effect,           // Effect function
      deps,            // Dependencies
      cleanup: null,   // Cleanup function
      tag: 'effect'
    };
    hooks[hookIndex] = newHook;
    
    // Schedule effect to run after commit
    fiber.effects.push(newHook);
  } else {
    // Subsequent renders - check if deps changed
    const prevDeps = hook.deps;
    const depsChanged = !deps || !prevDeps || 
      deps.some((dep, i) => !Object.is(dep, prevDeps[i]));
    
    if (depsChanged) {
      // Deps changed - schedule new effect
      hook.effect = effect;
      hook.deps = deps;
      fiber.effects.push(hook);
    }
  }
  
  hookIndex++;
}

// After commit phase
function commitEffects(fiber) {
  fiber.effects.forEach(hook => {
    // Run cleanup from previous effect
    if (hook.cleanup) {
      hook.cleanup();
    }
    
    // Run new effect
    hook.cleanup = hook.effect();
  });
  
  fiber.effects = [];
}
```

---

**Effect Lifecycle:**

```javascript
function Component() {
  const [count, setCount] = useState(0);
  
  useEffect(() => {
    console.log('1. Effect runs');
    
    // Setup code
    const timer = setInterval(() => {
      console.log('Timer tick');
    }, 1000);
    
    // Cleanup function
    return () => {
      console.log('2. Cleanup runs');
      clearInterval(timer);
    };
  }, [count]);
  
  return <button onClick={() => setCount(count + 1)}>{count}</button>;
}

// Timeline:
// Initial render:
// - Component renders
// - React commits to DOM
// - Browser paints
// - Effect runs: "1. Effect runs"
// - Timer starts

// User clicks button (count: 0 → 1):
// - Component renders with count=1
// - React commits to DOM
// - Browser paints
// - Cleanup runs: "2. Cleanup runs"
// - Old timer cleared
// - Effect runs: "1. Effect runs"
// - New timer starts

// Component unmounts:
// - Cleanup runs: "2. Cleanup runs"
// - Timer cleared
```

---

**Dependency Array:**

**1. No dependency array - runs after every render:**
```javascript
useEffect(() => {
  console.log('Runs after every render');
});

// Internal check:
function shouldRunEffect(hook) {
  return hook.deps === undefined;  // Always true
}
```

**2. Empty array - runs once (mount only):**
```javascript
useEffect(() => {
  console.log('Runs once on mount');
  
  return () => {
    console.log('Runs once on unmount');
  };
}, []);

// Internal check:
function shouldRunEffect(hook) {
  if (hook.deps.length === 0) {
    return !hook.hasRun;  // Run only if not run before
  }
}
```

**3. With dependencies - runs when deps change:**
```javascript
useEffect(() => {
  console.log('Runs when count or name changes');
}, [count, name]);

// Internal check:
function shouldRunEffect(hook) {
  const prevDeps = hook.prevDeps;
  const nextDeps = hook.deps;
  
  if (!prevDeps) return true;  // First run
  
  // Check if any dependency changed
  return nextDeps.some((dep, i) => 
    !Object.is(dep, prevDeps[i])
  );
}

// Object.is comparison:
Object.is(5, 5);              // true
Object.is('hi', 'hi');        // true
Object.is({}, {});            // false (different objects)
Object.is([1], [1]);          // false (different arrays)

const obj = { a: 1 };
Object.is(obj, obj);          // true (same reference)
```

---

**Common Patterns:**

**1. Data Fetching:**
```javascript
function UserProfile({ userId }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  
  useEffect(() => {
    let cancelled = false;  // Cleanup flag
    
    setLoading(true);
    
    fetch(`/api/users/${userId}`)
      .then(res => res.json())
      .then(data => {
        if (!cancelled) {  // Check if still mounted
          setUser(data);
          setLoading(false);
        }
      });
    
    // Cleanup: prevent state update if unmounted
    return () => {
      cancelled = true;
    };
  }, [userId]);  // Re-fetch when userId changes
  
  if (loading) return <div>Loading...</div>;
  return <div>{user.name}</div>;
}

// Why cleanup matters:
// 1. User opens profile (userId=1)
// 2. Fetch starts
// 3. User navigates away (component unmounts)
// 4. Cleanup sets cancelled=true
// 5. Fetch completes, but state update skipped
// 6. No "Can't perform state update on unmounted component" warning
```

**2. Subscriptions:**
```javascript
function ChatRoom({ roomId }) {
  const [messages, setMessages] = useState([]);
  
  useEffect(() => {
    // Subscribe
    const subscription = chatAPI.subscribe(roomId, (message) => {
      setMessages(prev => [...prev, message]);
    });
    
    // Cleanup: unsubscribe
    return () => {
      subscription.unsubscribe();
    };
  }, [roomId]);
  
  return <MessageList messages={messages} />;
}

// Timeline:
// Mount (roomId='general'):
// - Subscribe to 'general'
// - Messages flow in

// roomId changes ('general' → 'random'):
// - Cleanup: Unsubscribe from 'general'
// - Effect: Subscribe to 'random'
// - Messages from 'random' flow in

// Unmount:
// - Cleanup: Unsubscribe from 'random'
```

**3. DOM Manipulation:**
```javascript
function Modal({ isOpen }) {
  useEffect(() => {
    if (isOpen) {
      // Disable body scroll
      document.body.style.overflow = 'hidden';
      
      // Cleanup: restore scroll
      return () => {
        document.body.style.overflow = 'auto';
      };
    }
  }, [isOpen]);
  
  if (!isOpen) return null;
  return <div className="modal">...</div>;
}
```

**4. Timers:**
```javascript
function Timer() {
  const [seconds, setSeconds] = useState(0);
  
  useEffect(() => {
    const interval = setInterval(() => {
      setSeconds(prev => prev + 1);  // Functional update!
    }, 1000);
    
    // Cleanup: clear interval
    return () => clearInterval(interval);
  }, []);  // Empty deps - set up once
  
  return <div>{seconds}s</div>;
}
```

---

**Effect Execution Order:**

```javascript
function Parent() {
  useEffect(() => {
    console.log('1. Parent effect');
    return () => console.log('2. Parent cleanup');
  });
  
  return <Child />;
}

function Child() {
  useEffect(() => {
    console.log('3. Child effect');
    return () => console.log('4. Child cleanup');
  });
  
  return <div>Child</div>;
}

// Initial render:
// "3. Child effect"     (children first)
// "1. Parent effect"    (then parents)

// Re-render:
// "4. Child cleanup"    (children cleanup first)
// "2. Parent cleanup"   (then parents cleanup)
// "3. Child effect"     (children effect)
// "1. Parent effect"    (then parents effect)

// Unmount:
// "4. Child cleanup"
// "2. Parent cleanup"
```

---

**Internal Effect Queue:**

```javascript
// React maintains effect queue per fiber
const fiber = {
  type: Component,
  effects: [
    {
      effect: () => { /* effect 1 */ },
      cleanup: null,
      deps: [count],
      tag: 'PASSIVE'  // useEffect (async)
    },
    {
      effect: () => { /* effect 2 */ },
      cleanup: null,
      deps: [],
      tag: 'LAYOUT'   // useLayoutEffect (sync)
    }
  ]
};

// Commit phase:
function commitRoot(root) {
  // 1. Before mutation
  // 2. Mutation (update DOM)
  commitMutationEffects(root);
  
  // 3. Layout effects (synchronous)
  commitLayoutEffects(root);
  
  // 4. Browser paints
  
  // 5. Passive effects (asynchronous)
  schedulePassiveEffects(root);
}

function schedulePassiveEffects(root) {
  // Run effects after paint
  requestIdleCallback(() => {
    commitPassiveEffects(root);
  });
}

function commitPassiveEffects(fiber) {
  fiber.effects
    .filter(effect => effect.tag === 'PASSIVE')
    .forEach(effect => {
      // Run cleanup
      if (effect.cleanup) {
        effect.cleanup();
      }
      // Run effect
      effect.cleanup = effect.effect();
    });
}
```

---

**Common Mistakes:**

**1. Missing Dependencies:**
```javascript
// ❌ Bad: Missing count in deps
function Counter() {
  const [count, setCount] = useState(0);
  
  useEffect(() => {
    const timer = setInterval(() => {
      console.log(count);  // Always logs 0!
    }, 1000);
    
    return () => clearInterval(timer);
  }, []);  // Empty deps - effect runs once
  
  // count in effect is "stale" - captured from first render
}

// ✅ Good: Include all dependencies
useEffect(() => {
  const timer = setInterval(() => {
    console.log(count);  // Logs current count
  }, 1000);
  
  return () => clearInterval(timer);
}, [count]);  // Re-run when count changes

// ✅ Better: Use functional update (no dependency needed)
useEffect(() => {
  const timer = setInterval(() => {
    setCount(prev => {
      console.log(prev);  // Always current
      return prev;
    });
  }, 1000);
  
  return () => clearInterval(timer);
}, []);  // No count dependency needed
```

**2. Object/Array Dependencies:**
```javascript
// ❌ Bad: New object every render
function Component() {
  const options = { a: 1, b: 2 };  // New object!
  
  useEffect(() => {
    doSomething(options);
  }, [options]);  // Runs every render (different object)
}

// ✅ Good: Memoize object
function Component() {
  const options = useMemo(() => ({ a: 1, b: 2 }), []);
  
  useEffect(() => {
    doSomething(options);
  }, [options]);  // Runs once (same object)
}

// ✅ Better: Primitive dependencies
function Component() {
  const a = 1;
  const b = 2;
  
  useEffect(() => {
    doSomething({ a, b });
  }, [a, b]);  // Primitives compare correctly
}
```

**3. Infinite Loops:**
```javascript
// ❌ Bad: Sets state without deps
function Component() {
  const [count, setCount] = useState(0);
  
  useEffect(() => {
    setCount(count + 1);  // Triggers re-render
  });  // No deps - runs after every render
  // Infinite loop!
}

// ✅ Good: Add deps or condition
useEffect(() => {
  if (count < 10) {
    setCount(count + 1);
  }
}, [count]);  // Stops at 10
```

---

**Benefits:**
- ✅ **Declarative** - Describe what should happen, React handles when
- ✅ **Cleanup** - Automatic cleanup prevents memory leaks
- ✅ **Flexible** - Works for many side effects
- ✅ **Composable** - Multiple effects in one component

**Trade-offs:**

| Benefit | Cost |
|---------|------|
| **Runs after paint** | Not suitable for DOM measurements |
| **Automatic cleanup** | Must return cleanup function correctly |
| **Dependency tracking** | Easy to miss dependencies |

**When to use useEffect:**
- ✅ Data fetching
- ✅ Subscriptions
- ✅ Timers
- ✅ Logging/analytics
- ✅ External system sync
- ❌ Avoid for DOM measurements (use useLayoutEffect)
- ❌ Avoid for derived state (calculate during render)

**Interview Tip:**
> "useEffect runs asynchronously after React commits changes to the DOM and the browser paints. React compares dependencies using Object.is() to determine if the effect should re-run. Cleanup functions run before the next effect and on unmount, preventing memory leaks."

---

## useContext

### 🎯 What is useContext?

**Definition:**
> useContext is a React Hook that lets you read and subscribe to context from your component, avoiding prop drilling by providing data to the entire component tree.

**Simple meaning:**
useContext lets components access shared data without passing props through every level - like a global variable that any component can read.

**Real-life analogy:**
Like a company-wide announcement system - instead of passing a message person-to-person (prop drilling), you broadcast it once and everyone who needs it can tune in (useContext).

---

### 🔧 How useContext Works Internally

**Basic Usage:**

```javascript
// 1. Create context
const ThemeContext = React.createContext('light');

// 2. Provide context value
function App() {
  const [theme, setTheme] = useState('dark');
  
  return (
    <ThemeContext.Provider value={theme}>
      <Toolbar />
    </ThemeContext.Provider>
  );
}

// 3. Consume context
function Toolbar() {
  return <ThemedButton />;
}

function ThemedButton() {
  // No props needed!
  const theme = useContext(ThemeContext);
  return <button className={theme}>Click me</button>;
}
```

---

**Internal Implementation:**

```javascript
// createContext implementation
function createContext(defaultValue) {
  const context = {
    _currentValue: defaultValue,
    Provider: null,
    Consumer: null
  };
  
  // Provider component
  context.Provider = {
    _context: context,
    render: function(props) {
      // Update context value
      context._currentValue = props.value;
      return props.children;
    }
  };
  
  // Consumer component (legacy)
  context.Consumer = {
    _context: context,
    render: function(props) {
      return props.children(context._currentValue);
    }
  };
  
  return context;
}

// useContext implementation
function useContext(context) {
  const fiber = currentFiber;
  
  // Read current value from context
  const value = context._currentValue;
  
  // Subscribe fiber to context changes
  if (!fiber.dependencies) {
    fiber.dependencies = [];
  }
  
  fiber.dependencies.push({
    context,
    observedBits: 0
  });
  
  return value;
}
```

---

**Context Propagation:**

```javascript
// How React propagates context through tree
function propagateContextChange(fiber, context, newValue) {
  // Update context value
  context._currentValue = newValue;
  
  // Find all consumers in subtree
  const consumers = findContextConsumers(fiber, context);
  
  // Schedule re-render for each consumer
  consumers.forEach(consumerFiber => {
    scheduleUpdate(consumerFiber);
  });
}

function findContextConsumers(fiber, context) {
  const consumers = [];
  
  function traverse(node) {
    if (!node) return;
    
    // Check if this fiber uses the context
    if (node.dependencies) {
      const hasContext = node.dependencies.some(
        dep => dep.context === context
      );
      if (hasContext) {
        consumers.push(node);
      }
    }
    
    // Traverse children
    traverse(node.child);
    traverse(node.sibling);
  }
  
  traverse(fiber.child);
  return consumers;
}
```

---

**Context Stack:**

```javascript
// React maintains a context stack during render
const contextStack = [];

function pushProvider(context, newValue) {
  // Save previous value
  contextStack.push({
    context,
    previousValue: context._currentValue
  });
  
  // Set new value
  context._currentValue = newValue;
}

function popProvider() {
  // Restore previous value
  const { context, previousValue } = contextStack.pop();
  context._currentValue = previousValue;
}

// Rendering Provider
function renderProvider(fiber) {
  const context = fiber.type._context;
  const newValue = fiber.props.value;
  
  pushProvider(context, newValue);
  
  // Render children
  const children = renderChildren(fiber);
  
  popProvider();
  
  return children;
}

// Example with nested providers:
<ThemeContext.Provider value="dark">
  <UserContext.Provider value={user}>
    <Component />
  </UserContext.Provider>
</ThemeContext.Provider>

// Stack during render:
// 1. Push ThemeContext: "dark"
// 2. Push UserContext: user
// 3. Render Component (can access both)
// 4. Pop UserContext
// 5. Pop ThemeContext
```

---

**Multiple Contexts:**

```javascript
// Creating multiple contexts
const ThemeContext = createContext('light');
const UserContext = createContext(null);
const LanguageContext = createContext('en');

function App() {
  const [theme, setTheme] = useState('dark');
  const [user, setUser] = useState({ name: 'John' });
  const [language, setLanguage] = useState('en');
  
  return (
    <ThemeContext.Provider value={theme}>
      <UserContext.Provider value={user}>
        <LanguageContext.Provider value={language}>
          <Dashboard />
        </LanguageContext.Provider>
      </UserContext.Provider>
    </ThemeContext.Provider>
  );
}

function Dashboard() {
  // Use multiple contexts
  const theme = useContext(ThemeContext);
  const user = useContext(UserContext);
  const language = useContext(LanguageContext);
  
  return (
    <div className={theme}>
      {language === 'en' ? 'Hello' : 'Hola'}, {user.name}!
    </div>
  );
}

// Each useContext creates separate dependency
// Component re-renders when ANY context changes
```

---

**Context with Complex Values:**

```javascript
// ❌ Bad: New object every render
function App() {
  const [user, setUser] = useState({ name: 'John' });
  
  return (
    <UserContext.Provider value={{ user, setUser }}>
      <Dashboard />
    </UserContext.Provider>
  );
  // New object { user, setUser } every render!
  // All consumers re-render unnecessarily
}

// ✅ Good: Memoize context value
function App() {
  const [user, setUser] = useState({ name: 'John' });
  
  const value = useMemo(
    () => ({ user, setUser }),
    [user]  // Only changes when user changes
  );
  
  return (
    <UserContext.Provider value={value}>
      <Dashboard />
    </UserContext.Provider>
  );
}

// ✅ Better: Split contexts
const UserStateContext = createContext(null);
const UserDispatchContext = createContext(null);

function App() {
  const [user, setUser] = useState({ name: 'John' });
  
  return (
    <UserStateContext.Provider value={user}>
      <UserDispatchContext.Provider value={setUser}>
        <Dashboard />
      </UserDispatchContext.Provider>
    </UserStateContext.Provider>
  );
}

// Components can subscribe to only what they need
function UserDisplay() {
  const user = useContext(UserStateContext);  // Only re-renders when user changes
  return <div>{user.name}</div>;
}

function UserEditor() {
  const setUser = useContext(UserDispatchContext);  // Never re-renders
  return <button onClick={() => setUser({ name: 'Jane' })}>Edit</button>;
}
```

---

**Context Selector Pattern:**

```javascript
// Problem: Context consumers re-render on any value change
const StoreContext = createContext({
  user: { name: 'John' },
  theme: 'dark',
  language: 'en'
});

function Component() {
  const store = useContext(StoreContext);
  return <div>{store.user.name}</div>;
  // Re-renders when theme or language changes too!
}

// Solution: Use multiple contexts or state management library
// Or implement selector pattern:

function useContextSelector(context, selector) {
  const value = useContext(context);
  const selectedValue = selector(value);
  
  // Store previous selected value
  const [state, setState] = useState(selectedValue);
  
  useEffect(() => {
    const newValue = selector(value);
    // Only update if selected value changed
    if (!Object.is(state, newValue)) {
      setState(newValue);
    }
  }, [value, selector, state]);
  
  return state;
}

// Usage
function Component() {
  const userName = useContextSelector(
    StoreContext,
    store => store.user.name
  );
  // Only re-renders when user.name changes
  return <div>{userName}</div>;
}
```

---

**Context Default Values:**

```javascript
// Default value is used when no Provider exists
const ThemeContext = createContext('light');

// No Provider - uses default
function App() {
  return <ThemedButton />;
}

function ThemedButton() {
  const theme = useContext(ThemeContext);
  console.log(theme);  // "light" (default)
  return <button>{theme}</button>;
}

// With Provider - uses provided value
function App() {
  return (
    <ThemeContext.Provider value="dark">
      <ThemedButton />
    </ThemeContext.Provider>
  );
}

function ThemedButton() {
  const theme = useContext(ThemeContext);
  console.log(theme);  // "dark" (provided)
  return <button>{theme}</button>;
}

// Internal lookup:
function readContext(context) {
  // Walk up fiber tree looking for Provider
  let fiber = currentFiber.return;
  
  while (fiber) {
    if (fiber.type === context.Provider) {
      // Found Provider, return its value
      return fiber.props.value;
    }
    fiber = fiber.return;
  }
  
  // No Provider found, return default
  return context._currentValue;
}
```

---

**Context Update Optimization:**

```javascript
// React optimizes context updates
function App() {
  const [theme, setTheme] = useState('dark');
  
  return (
    <ThemeContext.Provider value={theme}>
      <Header />
      <Main />
      <Footer />
    </ThemeContext.Provider>
  );
}

function Header() {
  return <Logo />;  // Doesn't use context
}

function Logo() {
  const theme = useContext(ThemeContext);
  return <img className={theme} />;
}

function Main() {
  return <Content />;  // Doesn't use context
}

function Footer() {
  return <div>Footer</div>;  // Doesn't use context
}

// When theme changes:
// 1. React finds all context consumers (Logo)
// 2. Schedules update only for Logo and its ancestors
// 3. Header re-renders (ancestor of Logo)
// 4. Logo re-renders (consumer)
// 5. Main and Footer DON'T re-render (not ancestors of consumers)

// Internal optimization:
function propagateContextChange(providerFiber, context) {
  const consumers = [];
  
  // Find all consumers
  findContextConsumers(providerFiber.child, context, consumers);
  
  // Mark path from consumer to provider for update
  consumers.forEach(consumerFiber => {
    let fiber = consumerFiber;
    while (fiber && fiber !== providerFiber) {
      fiber.lanes = mergeLanes(fiber.lanes, updateLane);
      fiber = fiber.return;
    }
  });
}
```

---

**Benefits:**
- ✅ **Avoids prop drilling** - No need to pass props through intermediate components
- ✅ **Global state** - Share data across entire tree
- ✅ **Flexible** - Multiple contexts for different concerns
- ✅ **Type-safe** - Works well with TypeScript
- ✅ **Built-in** - No external library needed

**Trade-offs:**

| Benefit | Cost |
|---------|------|
| **No prop drilling** | All consumers re-render on context change |
| **Global access** | Can be overused, making data flow unclear |
| **Simple API** | Not suitable for high-frequency updates |

**When to use Context:**
- ✅ Theme (dark/light mode)
- ✅ User authentication
- ✅ Language/localization
- ✅ Feature flags
- ✅ Rarely changing global state
- ❌ Avoid for frequently changing values (use state management)
- ❌ Avoid for performance-critical updates
- ❌ Avoid as replacement for props (use props for direct parent-child)

**Interview Tip:**
> "useContext reads from the nearest Provider ancestor by walking up the fiber tree. When context value changes, React finds all consumers in the subtree and schedules updates only for those components and their ancestors, optimizing re-renders."

---

## useReducer

### 🎯 What is useReducer?

**Definition:**
> useReducer is a React Hook that manages complex state logic through a reducer function, similar to Redux, providing predictable state updates based on actions.

**Simple meaning:**
useReducer is like useState but for complex state - instead of setting state directly, you dispatch actions that describe what happened, and a reducer function decides how to update state.

**Real-life analogy:**
Like a restaurant order system - customers don't go to the kitchen and change things directly (setState). They send orders (dispatch actions) to the kitchen, where the chef (reducer) decides how to prepare the meal (update state).

---

### 🔧 How useReducer Works Internally

**Basic Usage:**

```javascript
// 1. Define reducer function
function counterReducer(state, action) {
  switch (action.type) {
    case 'INCREMENT':
      return { count: state.count + 1 };
    case 'DECREMENT':
      return { count: state.count - 1 };
    case 'RESET':
      return { count: 0 };
    default:
      return state;
  }
}

// 2. Use in component
function Counter() {
  const [state, dispatch] = useReducer(counterReducer, { count: 0 });
  
  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'INCREMENT' })}>+</button>
      <button onClick={() => dispatch({ type: 'DECREMENT' })}>-</button>
      <button onClick={() => dispatch({ type: 'RESET' })}>Reset</button>
    </div>
  );
}
```

---

**Internal Implementation:**

```javascript
// Simplified useReducer implementation
function useReducer(reducer, initialState, init) {
  const fiber = currentFiber;
  const hooks = fiber.hooks || [];
  const hook = hooks[hookIndex];
  
  // First render - initialize
  if (!hook) {
    const initializedState = init ? init(initialState) : initialState;
    
    const newHook = {
      state: initializedState,
      reducer,
      queue: []  // Action queue
    };
    
    hooks[hookIndex] = newHook;
  }
  
  const currentHook = hooks[hookIndex];
  
  // Process queued actions
  let newState = currentHook.state;
  currentHook.queue.forEach(action => {
    newState = reducer(newState, action);
  });
  currentHook.state = newState;
  currentHook.queue = [];
  
  // Create dispatch function
  const dispatch = (action) => {
    // Add action to queue
    currentHook.queue.push(action);
    
    // Schedule re-render
    scheduleUpdate(fiber);
  };
  
  hookIndex++;
  
  return [currentHook.state, dispatch];
}
```

---

**Reducer Pattern:**

```javascript
// Complex state management example
const initialState = {
  user: null,
  loading: false,
  error: null,
  posts: []
};

function appReducer(state, action) {
  switch (action.type) {
    case 'FETCH_START':
      return {
        ...state,
        loading: true,
        error: null
      };
    
    case 'FETCH_SUCCESS':
      return {
        ...state,
        loading: false,
        user: action.payload.user,
        posts: action.payload.posts
      };
    
    case 'FETCH_ERROR':
      return {
        ...state,
        loading: false,
        error: action.payload
      };
    
    case 'ADD_POST':
      return {
        ...state,
        posts: [...state.posts, action.payload]
      };
    
    case 'DELETE_POST':
      return {
        ...state,
        posts: state.posts.filter(post => post.id !== action.payload)
      };
    
    case 'UPDATE_POST':
      return {
        ...state,
        posts: state.posts.map(post =>
          post.id === action.payload.id
            ? { ...post, ...action.payload.updates }
            : post
        )
      };
    
    default:
      throw new Error(`Unknown action: ${action.type}`);
  }
}

function App() {
  const [state, dispatch] = useReducer(appReducer, initialState);
  
  useEffect(() => {
    dispatch({ type: 'FETCH_START' });
    
    fetch('/api/data')
      .then(res => res.json())
      .then(data => {
        dispatch({
          type: 'FETCH_SUCCESS',
          payload: data
        });
      })
      .catch(error => {
        dispatch({
          type: 'FETCH_ERROR',
          payload: error.message
        });
      });
  }, []);
  
  const handleAddPost = (post) => {
    dispatch({ type: 'ADD_POST', payload: post });
  };
  
  if (state.loading) return <div>Loading...</div>;
  if (state.error) return <div>Error: {state.error}</div>;
  
  return (
    <div>
      <h1>Welcome, {state.user?.name}</h1>
      <PostList posts={state.posts} onAdd={handleAddPost} />
    </div>
  );
}
```

---

**Lazy Initialization:**

```javascript
// Expensive initialization
function init(initialCount) {
  console.log('Expensive initialization');
  return {
    count: initialCount,
    history: []
  };
}

// ❌ Bad: Runs every render
const [state, dispatch] = useReducer(
  reducer,
  init(props.initialCount)  // Runs every render!
);

// ✅ Good: Runs only once
const [state, dispatch] = useReducer(
  reducer,
  props.initialCount,
  init  // Function reference, called only on mount
);

// Internal implementation:
function useReducer(reducer, initialArg, init) {
  const hook = hooks[hookIndex];
  
  if (!hook) {
    // First render
    const initialState = init !== undefined
      ? init(initialArg)        // Call init function
      : initialArg;             // Use initialArg directly
    
    hooks[hookIndex] = {
      state: initialState,
      reducer,
      queue: []
    };
  }
  
  // ...rest of implementation
}
```

---

**Action Batching:**

```javascript
function reducer(state, action) {
  switch (action.type) {
    case 'INCREMENT':
      console.log('Increment:', state.count);
      return { count: state.count + 1 };
    default:
      return state;
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });
  
  const handleClick = () => {
    dispatch({ type: 'INCREMENT' });  // Queued
    dispatch({ type: 'INCREMENT' });  // Queued
    dispatch({ type: 'INCREMENT' });  // Queued
    
    // React batches these
    // Reducer runs 3 times in one render
    // Only one re-render happens
  };
  
  return <button onClick={handleClick}>{state.count}</button>;
}

// Internal batching:
function batchedUpdates(fn) {
  const prevIsBatching = isBatchingUpdates;
  isBatchingUpdates = true;
  
  try {
    fn();  // All dispatches queued
  } finally {
    isBatchingUpdates = prevIsBatching;
    if (!isBatchingUpdates) {
      flushSyncCallbacks();  // Process all queued actions
    }
  }
}

// Processing queued actions:
function processUpdateQueue(hook) {
  let newState = hook.state;
  
  // Run reducer for each action
  hook.queue.forEach(action => {
    const prevState = newState;
    newState = hook.reducer(prevState, action);
  });
  
  hook.state = newState;
  hook.queue = [];
}
```

---

**useReducer vs useState:**

```javascript
// useState - simple state
function SimpleCounter() {
  const [count, setCount] = useState(0);
  
  return (
    <button onClick={() => setCount(count + 1)}>
      {count}
    </button>
  );
}

// useReducer - complex state logic
function ComplexCounter() {
  const [state, dispatch] = useReducer(
    (state, action) => {
      switch (action.type) {
        case 'INCREMENT':
          return {
            ...state,
            count: state.count + 1,
            history: [...state.history, state.count + 1]
          };
        case 'DECREMENT':
          return {
            ...state,
            count: state.count - 1,
            history: [...state.history, state.count - 1]
          };
        case 'UNDO':
          const prevValue = state.history[state.history.length - 2];
          return {
            ...state,
            count: prevValue,
            history: state.history.slice(0, -1)
          };
        default:
          return state;
      }
    },
    { count: 0, history: [0] }
  );
  
  return (
    <div>
      <button onClick={() => dispatch({ type: 'INCREMENT' })}>+</button>
      <span>{state.count}</span>
      <button onClick={() => dispatch({ type: 'DECREMENT' })}>-</button>
      <button onClick={() => dispatch({ type: 'UNDO' })}>Undo</button>
    </div>
  );
}

// When to use what:
// useState: Independent state values, simple updates
// useReducer: Related state values, complex update logic
```

---

**Dispatch Stability:**

```javascript
function Component() {
  const [state, dispatch] = useReducer(reducer, initialState);
  
  // dispatch is stable - same reference across renders
  useEffect(() => {
    // Safe to use dispatch in dependencies
    dispatch({ type: 'INIT' });
  }, [dispatch]);  // dispatch never changes
  
  // Can pass dispatch to children without causing re-renders
  return <Child onAction={dispatch} />;
}

const Child = React.memo(({ onAction }) => {
  // Won't re-render when parent re-renders
  // because dispatch reference is stable
  return <button onClick={() => onAction({ type: 'ACTION' })}>Click</button>;
});

// Internal implementation ensures dispatch stability:
function useReducer(reducer, initialState) {
  const hook = hooks[hookIndex];
  
  if (!hook) {
    // Create dispatch once
    const dispatch = (action) => {
      // Closure over hook reference
      hook.queue.push(action);
      scheduleUpdate(fiber);
    };
    
    hooks[hookIndex] = {
      state: initialState,
      reducer,
      queue: [],
      dispatch  // Store dispatch in hook
    };
  }
  
  // Return same dispatch every render
  return [hook.state, hook.dispatch];
}
```

---

**Combining with Context:**

```javascript
// Create context for state and dispatch
const StateContext = createContext(null);
const DispatchContext = createContext(null);

// Provider component
function AppProvider({ children }) {
  const [state, dispatch] = useReducer(appReducer, initialState);
  
  return (
    <StateContext.Provider value={state}>
      <DispatchContext.Provider value={dispatch}>
        {children}
      </DispatchContext.Provider>
    </StateContext.Provider>
  );
}

// Custom hooks for easy access
function useAppState() {
  const context = useContext(StateContext);
  if (!context) {
    throw new Error('useAppState must be used within AppProvider');
  }
  return context;
}

function useAppDispatch() {
  const context = useContext(DispatchContext);
  if (!context) {
    throw new Error('useAppDispatch must be used within AppProvider');
  }
  return context;
}

// Usage in components
function UserProfile() {
  const state = useAppState();
  const dispatch = useAppDispatch();
  
  return (
    <div>
      <h1>{state.user.name}</h1>
      <button onClick={() => dispatch({ type: 'LOGOUT' })}>
        Logout
      </button>
    </div>
  );
}

function App() {
  return (
    <AppProvider>
      <UserProfile />
    </AppProvider>
  );
}
```

---

**Middleware Pattern:**

```javascript
// Add middleware to useReducer
function useReducerWithMiddleware(reducer, initialState, middlewares = []) {
  const [state, dispatch] = useReducer(reducer, initialState);
  
  // Wrap dispatch with middleware
  const enhancedDispatch = useCallback(
    (action) => {
      // Run middleware chain
      let result = action;
      
      middlewares.forEach(middleware => {
        result = middleware(state, result, dispatch);
      });
      
      // Dispatch final action
      if (result) {
        dispatch(result);
      }
    },
    [state, dispatch, middlewares]
  );
  
  return [state, enhancedDispatch];
}

// Logger middleware
const loggerMiddleware = (state, action, dispatch) => {
  console.log('Previous State:', state);
  console.log('Action:', action);
  return action;  // Pass through
};

// Async middleware
const asyncMiddleware = (state, action, dispatch) => {
  if (action.type === 'FETCH_DATA') {
    fetch('/api/data')
      .then(res => res.json())
      .then(data => {
        dispatch({ type: 'FETCH_SUCCESS', payload: data });
      });
    return { type: 'FETCH_START' };  // Dispatch loading action
  }
  return action;
};

// Usage
function App() {
  const [state, dispatch] = useReducerWithMiddleware(
    reducer,
    initialState,
    [loggerMiddleware, asyncMiddleware]
  );
  
  return <div>...</div>;
}
```

---

**Benefits:**
- ✅ **Predictable** - Same action always produces same state change
- ✅ **Testable** - Reducer is pure function, easy to test
- ✅ **Debuggable** - Action history shows what happened
- ✅ **Complex logic** - Better than multiple useState for related state
- ✅ **Stable dispatch** - dispatch reference never changes

**Trade-offs:**

| Benefit | Cost |
|---------|------|
| **Centralized logic** | More boilerplate than useState |
| **Predictable updates** | Requires understanding reducer pattern |
| **Easy testing** | More code to write initially |

**When to use useReducer:**
- ✅ Complex state logic with multiple sub-values
- ✅ Next state depends on previous state
- ✅ Multiple actions that update same state
- ✅ Need to pass dispatch down (stable reference)
- ✅ Want predictable, testable state updates
- ❌ Avoid for simple independent state (use useState)
- ❌ Avoid when state updates are straightforward

**Interview Tip:**
> "useReducer manages state through a reducer function that takes current state and an action, returning new state. React batches dispatched actions and processes them sequentially through the reducer. The dispatch function has a stable reference, making it safe to pass to child components without causing re-renders."

---

## useCallback

### 🎯 What is useCallback?

**Definition:**
> useCallback is a React Hook that returns a memoized callback function, preventing unnecessary function recreations and child component re-renders.

**Simple meaning:**
useCallback "remembers" a function between renders - instead of creating a new function every time, it returns the same function unless dependencies change.

**Real-life analogy:**
Like saving a phone contact - instead of typing the number every time (new function), you save it once and reuse it (memoized function) until the number changes (dependency change).

---

### 🔧 How useCallback Works Internally

**Basic Usage:**

```javascript
function Parent() {
  const [count, setCount] = useState(0);
  const [name, setName] = useState('John');
  
  // ❌ Without useCallback - new function every render
  const handleClick = () => {
    console.log('Clicked');
  };
  
  // ✅ With useCallback - same function unless deps change
  const memoizedHandleClick = useCallback(() => {
    console.log('Clicked');
  }, []);  // Empty deps - function never changes
  
  return (
    <div>
      <button onClick={() => setCount(count + 1)}>Count: {count}</button>
      <Child onClick={memoizedHandleClick} />
    </div>
  );
}

const Child = React.memo(({ onClick }) => {
  console.log('Child rendered');
  return <button onClick={onClick}>Click me</button>;
});

// Without useCallback:
// - Parent renders
// - New handleClick created
// - Child receives new onClick prop
// - Child re-renders (even with React.memo)

// With useCallback:
// - Parent renders
// - Same memoizedHandleClick returned
// - Child receives same onClick prop
// - Child doesn't re-render (React.memo works)
```

---

**Internal Implementation:**

```javascript
// Simplified useCallback implementation
function useCallback(callback, deps) {
  const fiber = currentFiber;
  const hooks = fiber.hooks || [];
  const hook = hooks[hookIndex];
  
  // First render - store callback
  if (!hook) {
    hooks[hookIndex] = {
      callback,
      deps
    };
    hookIndex++;
    return callback;
  }
  
  // Subsequent renders - check if deps changed
  const prevDeps = hook.deps;
  const depsChanged = !deps || !prevDeps ||
    deps.some((dep, i) => !Object.is(dep, prevDeps[i]));
  
  if (depsChanged) {
    // Deps changed - store new callback
    hook.callback = callback;
    hook.deps = deps;
  }
  
  hookIndex++;
  
  // Return stored callback (old or new)
  return hook.callback;
}

// useCallback is essentially:
function useCallback(callback, deps) {
  return useMemo(() => callback, deps);
}
```

---

**Dependency Tracking:**

```javascript
function Component() {
  const [count, setCount] = useState(0);
  const [name, setName] = useState('John');
  
  // Callback depends on count
  const handleClick = useCallback(() => {
    console.log('Count:', count);
  }, [count]);  // Recreates when count changes
  
  // On first render: count = 0
  // handleClick = function() { console.log('Count:', 0); }
  
  // User clicks increment, count = 1
  // deps changed: [0] !== [1]
  // New handleClick = function() { console.log('Count:', 1); }
  
  // User changes name
  // deps unchanged: [1] === [1]
  // Same handleClick returned (still logs count: 1)
  
  return (
    <div>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <input value={name} onChange={e => setName(e.target.value)} />
      <button onClick={handleClick}>Log Count</button>
    </div>
  );
}
```

---

**Common Patterns:**

**1. Preventing Child Re-renders:**

```javascript
function ParentComponent() {
  const [count, setCount] = useState(0);
  const [items, setItems] = useState([]);
  
  // ❌ Bad: New function every render
  const handleAddItem = (item) => {
    setItems([...items, item]);
  };
  
  // ✅ Good: Memoized function
  const memoizedHandleAddItem = useCallback((item) => {
    setItems(prevItems => [...prevItems, item]);
  }, []);  // No dependencies needed with functional update
  
  return (
    <div>
      <button onClick={() => setCount(count + 1)}>
        Count: {count}
      </button>
      <ExpensiveChild onAddItem={memoizedHandleAddItem} />
    </div>
  );
}

const ExpensiveChild = React.memo(({ onAddItem }) => {
  console.log('ExpensiveChild rendered');
  // Expensive rendering logic
  return <button onClick={() => onAddItem('new')}>Add Item</button>;
});

// Without useCallback:
// - Parent count changes
// - New handleAddItem created
// - ExpensiveChild re-renders (expensive!)

// With useCallback:
// - Parent count changes
// - Same memoizedHandleAddItem returned
// - ExpensiveChild doesn't re-render (optimized!)
```

**2. useEffect Dependencies:**

```javascript
function Component({ userId }) {
  const [data, setData] = useState(null);
  
  // ❌ Bad: Causes infinite loop
  const fetchData = () => {
    fetch(`/api/users/${userId}`)
      .then(res => res.json())
      .then(setData);
  };
  
  useEffect(() => {
    fetchData();
  }, [fetchData]);  // fetchData is new every render - infinite loop!
  
  // ✅ Good: Memoized function
  const memoizedFetchData = useCallback(() => {
    fetch(`/api/users/${userId}`)
      .then(res => res.json())
      .then(setData);
  }, [userId]);  // Only changes when userId changes
  
  useEffect(() => {
    memoizedFetchData();
  }, [memoizedFetchData]);  // Safe - function is stable
  
  return <div>{data?.name}</div>;
}
```

**3. Event Handlers with Props:**

```javascript
function TodoList({ todos, onToggle, onDelete }) {
  // Memoize handlers that use props
  const handleToggle = useCallback((id) => {
    onToggle(id);
  }, [onToggle]);  // Recreate if onToggle changes
  
  const handleDelete = useCallback((id) => {
    onDelete(id);
  }, [onDelete]);
  
  return (
    <ul>
      {todos.map(todo => (
        <TodoItem
          key={todo.id}
          todo={todo}
          onToggle={handleToggle}
          onDelete={handleDelete}
        />
      ))}
    </ul>
  );
}

const TodoItem = React.memo(({ todo, onToggle, onDelete }) => {
  console.log('TodoItem rendered:', todo.id);
  
  return (
    <li>
      <input
        type="checkbox"
        checked={todo.completed}
        onChange={() => onToggle(todo.id)}
      />
      <span>{todo.text}</span>
      <button onClick={() => onDelete(todo.id)}>Delete</button>
    </li>
  );
});
```

---

**Closure Traps:**

```javascript
// ❌ Bad: Stale closure
function Counter() {
  const [count, setCount] = useState(0);
  
  const handleClick = useCallback(() => {
    console.log(count);  // Always logs 0!
  }, []);  // Empty deps - captures count from first render
  
  return (
    <div>
      <button onClick={() => setCount(count + 1)}>
        Count: {count}
      </button>
      <button onClick={handleClick}>Log Count</button>
    </div>
  );
}

// ✅ Good: Include dependency
const handleClick = useCallback(() => {
  console.log(count);  // Logs current count
}, [count]);  // Recreates when count changes

// ✅ Better: Use functional update (no dependency)
const handleIncrement = useCallback(() => {
  setCount(prev => prev + 1);  // Always has current value
}, []);  // No count dependency needed

// ✅ Best: Use ref for latest value
const countRef = useRef(count);
countRef.current = count;

const handleClick = useCallback(() => {
  console.log(countRef.current);  // Always current
}, []);  // No dependencies needed
```

---

**Performance Considerations:**

```javascript
// useCallback has overhead - only use when needed

// ❌ Unnecessary: No child components
function Component() {
  const handleClick = useCallback(() => {
    console.log('Clicked');
  }, []);
  
  return <button onClick={handleClick}>Click</button>;
  // No benefit - button doesn't care about function identity
}

// ❌ Unnecessary: Child not memoized
function Parent() {
  const handleClick = useCallback(() => {
    console.log('Clicked');
  }, []);
  
  return <Child onClick={handleClick} />;
}

function Child({ onClick }) {  // Not memoized!
  return <button onClick={onClick}>Click</button>;
  // Child re-renders anyway - useCallback wasted
}

// ✅ Necessary: Memoized child
const Child = React.memo(({ onClick }) => {
  return <button onClick={onClick}>Click</button>;
});
// Now useCallback prevents re-renders

// ✅ Necessary: useEffect dependency
useEffect(() => {
  handleClick();
}, [handleClick]);  // Needs stable reference
```

---

**Comparing Functions:**

```javascript
// Why function identity matters
function Parent() {
  const [count, setCount] = useState(0);
  
  // New function every render
  const handleClick1 = () => console.log('Click');
  const handleClick2 = () => console.log('Click');
  
  console.log(handleClick1 === handleClick2);  // false
  // Different renders create different functions
  
  // Memoized function
  const memoized = useCallback(() => console.log('Click'), []);
  
  // On re-render:
  const prevMemoized = memoized;  // Saved from previous render
  // Component re-renders...
  console.log(prevMemoized === memoized);  // true
  // Same function returned
}

// Internal comparison in React.memo:
function memo(Component) {
  return function MemoizedComponent(props) {
    const prevProps = fiber.alternate?.memoizedProps;
    
    if (prevProps) {
      // Shallow compare props
      const propsEqual = Object.keys(props).every(key =>
        Object.is(props[key], prevProps[key])
      );
      
      if (propsEqual) {
        // Props haven't changed - reuse previous render
        return fiber.alternate.child;
      }
    }
    
    // Props changed - re-render
    return Component(props);
  };
}

// Without useCallback:
<Child onClick={handleClick} />
// Every render: new handleClick
// Object.is(prevOnClick, newOnClick) = false
// Child re-renders

// With useCallback:
<Child onClick={memoizedHandleClick} />
// Same handleClick (if deps unchanged)
// Object.is(prevOnClick, newOnClick) = true
// Child doesn't re-render
```

---

**Benefits:**
- ✅ **Prevents re-renders** - Stable function reference for memoized children
- ✅ **Stable dependencies** - Safe to use in useEffect dependencies
- ✅ **Performance** - Avoids expensive child re-renders
- ✅ **Referential equality** - Same function across renders

**Trade-offs:**

| Benefit | Cost |
|---------|------|
| **Prevents re-renders** | Memory overhead (stores function) |
| **Stable reference** | CPU overhead (dependency comparison) |
| **Optimization** | Code complexity |

**When to use useCallback:**
- ✅ Passing callbacks to memoized child components
- ✅ Callbacks used in useEffect dependencies
- ✅ Callbacks passed to custom hooks
- ✅ Expensive child components
- ❌ Avoid for simple event handlers (no memoized children)
- ❌ Avoid premature optimization
- ❌ Avoid when child isn't memoized

**Interview Tip:**
> "useCallback returns a memoized function that only changes when dependencies change. React stores the function reference in the hook and compares dependencies using Object.is(). It's useful for preventing child re-renders when combined with React.memo, as it maintains referential equality across renders."

---

## useMemo

### 🎯 What is useMemo?

**Definition:**
> useMemo is a React Hook that memoizes the result of an expensive computation, recalculating only when dependencies change, optimizing performance by avoiding unnecessary calculations.

**Simple meaning:**
useMemo "remembers" the result of a calculation - instead of recalculating every render, it returns the cached result unless inputs change.

**Real-life analogy:**
Like a calculator with memory - instead of recalculating 2+2 every time (expensive), it remembers the answer is 4 and returns it instantly until the numbers change.

---

### 🔧 How useMemo Works Internally

**Basic Usage:**

```javascript
function Component({ items }) {
  // ❌ Without useMemo - recalculates every render
  const expensiveResult = items.reduce((sum, item) => sum + item.value, 0);
  
  // ✅ With useMemo - recalculates only when items change
  const memoizedResult = useMemo(() => {
    console.log('Calculating...');
    return items.reduce((sum, item) => sum + item.value, 0);
  }, [items]);
  
  return <div>Total: {memoizedResult}</div>;
}
```

---

**Internal Implementation:**

```javascript
// Simplified useMemo implementation
function useMemo(factory, deps) {
  const fiber = currentFiber;
  const hooks = fiber.hooks || [];
  const hook = hooks[hookIndex];
  
  // First render - compute and store value
  if (!hook) {
    const value = factory();  // Call factory function
    
    hooks[hookIndex] = {
      value,
      deps
    };
    
    hookIndex++;
    return value;
  }
  
  // Subsequent renders - check if deps changed
  const prevDeps = hook.deps;
  const depsChanged = !deps || !prevDeps ||
    deps.some((dep, i) => !Object.is(dep, prevDeps[i]));
  
  if (depsChanged) {
    // Deps changed - recompute
    const value = factory();
    hook.value = value;
    hook.deps = deps;
  }
  
  hookIndex++;
  
  // Return stored value (old or new)
  return hook.value;
}
```

---

**Expensive Computations:**

```javascript
function DataTable({ data, filter }) {
  // Expensive filtering and sorting
  const processedData = useMemo(() => {
    console.log('Processing data...');
    
    // Filter
    let result = data.filter(item => 
      item.name.toLowerCase().includes(filter.toLowerCase())
    );
    
    // Sort
    result = result.sort((a, b) => a.value - b.value);
    
    // Transform
    result = result.map(item => ({
      ...item,
      formatted: `${item.name}: $${item.value.toFixed(2)}`
    }));
    
    return result;
  }, [data, filter]);  // Recompute only when data or filter changes
  
  return (
    <table>
      {processedData.map(item => (
        <tr key={item.id}>
          <td>{item.formatted}</td>
        </tr>
      ))}
    </table>
  );
}

// Without useMemo:
// - Parent re-renders (e.g., unrelated state change)
// - DataTable re-renders
// - Processing runs again (expensive!)
// - Same result computed unnecessarily

// With useMemo:
// - Parent re-renders
// - DataTable re-renders
// - deps unchanged: data and filter same
// - Returns cached result (fast!)
// - No unnecessary computation
```

---

**Referential Equality:**

```javascript
function Parent() {
  const [count, setCount] = useState(0);
  
  // ❌ Bad: New object every render
  const config = {
    theme: 'dark',
    language: 'en'
  };
  
  // ✅ Good: Memoized object
  const memoizedConfig = useMemo(() => ({
    theme: 'dark',
    language: 'en'
  }), []);  // Empty deps - never changes
  
  return (
    <div>
      <button onClick={() => setCount(count + 1)}>
        Count: {count}
      </button>
      <Child config={memoizedConfig} />
    </div>
  );
}

const Child = React.memo(({ config }) => {
  console.log('Child rendered');
  return <div>{config.theme}</div>;
});

// Without useMemo:
// - Parent re-renders (count changes)
// - New config object created
// - Child receives new config prop
// - Child re-renders (even with React.memo)

// With useMemo:
// - Parent re-renders (count changes)
// - Same memoizedConfig returned
// - Child receives same config prop
// - Child doesn't re-render (optimized!)
```

---

**useMemo vs useCallback:**

```javascript
// useMemo - memoizes VALUE
const memoizedValue = useMemo(() => {
  return computeExpensiveValue(a, b);
}, [a, b]);

// useCallback - memoizes FUNCTION
const memoizedCallback = useCallback(() => {
  doSomething(a, b);
}, [a, b]);

// useCallback is shorthand for useMemo with function:
const memoizedCallback = useMemo(() => {
  return () => doSomething(a, b);
}, [a, b]);

// Example showing difference:
function Component() {
  const [count, setCount] = useState(0);
  
  // useMemo returns the NUMBER
  const doubled = useMemo(() => {
    return count * 2;
  }, [count]);
  console.log(typeof doubled);  // "number"
  
  // useCallback returns the FUNCTION
  const increment = useCallback(() => {
    setCount(count + 1);
  }, [count]);
  console.log(typeof increment);  // "function"
  
  return (
    <div>
      <p>Count: {count}</p>
      <p>Doubled: {doubled}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
}
```

---

**Common Patterns:**

**1. Expensive Calculations:**

```javascript
function PrimeNumbers({ max }) {
  const primes = useMemo(() => {
    console.log('Calculating primes...');
    const result = [];
    
    for (let num = 2; num <= max; num++) {
      let isPrime = true;
      for (let i = 2; i <= Math.sqrt(num); i++) {
        if (num % i === 0) {
          isPrime = false;
          break;
        }
      }
      if (isPrime) result.push(num);
    }
    
    return result;
  }, [max]);  // Recalculate only when max changes
  
  return <div>Found {primes.length} primes</div>;
}
```

**2. Derived State:**

```javascript
function ShoppingCart({ items }) {
  // Derive values from state
  const { total, itemCount, tax } = useMemo(() => {
    const itemCount = items.length;
    const subtotal = items.reduce((sum, item) => sum + item.price, 0);
    const tax = subtotal * 0.1;
    const total = subtotal + tax;
    
    return { total, itemCount, tax };
  }, [items]);
  
  return (
    <div>
      <p>Items: {itemCount}</p>
      <p>Tax: ${tax.toFixed(2)}</p>
      <p>Total: ${total.toFixed(2)}</p>
    </div>
  );
}
```

**3. Context Values:**

```javascript
function AppProvider({ children }) {
  const [user, setUser] = useState(null);
  const [theme, setTheme] = useState('light');
  
  // ❌ Bad: New object every render
  const value = {
    user,
    setUser,
    theme,
    setTheme
  };
  
  // ✅ Good: Memoized context value
  const memoizedValue = useMemo(() => ({
    user,
    setUser,
    theme,
    setTheme
  }), [user, theme]);  // Only changes when user or theme changes
  
  return (
    <AppContext.Provider value={memoizedValue}>
      {children}
    </AppContext.Provider>
  );
}
```

**4. Filtered/Sorted Lists:**

```javascript
function UserList({ users, searchTerm, sortBy }) {
  const filteredAndSortedUsers = useMemo(() => {
    // Filter
    let result = users.filter(user =>
      user.name.toLowerCase().includes(searchTerm.toLowerCase())
    );
    
    // Sort
    result.sort((a, b) => {
      if (sortBy === 'name') {
        return a.name.localeCompare(b.name);
      }
      if (sortBy === 'age') {
        return a.age - b.age;
      }
      return 0;
    });
    
    return result;
  }, [users, searchTerm, sortBy]);
  
  return (
    <ul>
      {filteredAndSortedUsers.map(user => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

---

**Dependency Pitfalls:**

```javascript
// ❌ Bad: Object dependency
function Component({ config }) {
  const result = useMemo(() => {
    return expensiveCalculation(config);
  }, [config]);  // config is new object every render!
  
  // Recalculates every render even if config values same
}

// ✅ Good: Primitive dependencies
function Component({ config }) {
  const result = useMemo(() => {
    return expensiveCalculation(config);
  }, [config.theme, config.language]);  // Primitives
  
  // Recalculates only when theme or language changes
}

// ❌ Bad: Missing dependencies
function Component({ items, multiplier }) {
  const total = useMemo(() => {
    return items.reduce((sum, item) => sum + item.value, 0) * multiplier;
  }, [items]);  // Missing multiplier!
  
  // Uses stale multiplier value
}

// ✅ Good: All dependencies included
const total = useMemo(() => {
  return items.reduce((sum, item) => sum + item.value, 0) * multiplier;
}, [items, multiplier]);
```

---

**Performance Considerations:**

```javascript
// useMemo has overhead - only use when needed

// ❌ Unnecessary: Simple calculation
function Component({ a, b }) {
  const sum = useMemo(() => a + b, [a, b]);
  // Overhead of useMemo > cost of addition
  // Just do: const sum = a + b;
}

// ❌ Unnecessary: Runs every render anyway
function Component({ data }) {
  const result = useMemo(() => {
    return data.map(item => item.value);
  }, [data]);
  // If data changes every render, useMemo adds overhead
}

// ✅ Necessary: Expensive calculation
function Component({ data }) {
  const result = useMemo(() => {
    // Complex algorithm that takes time
    return complexAlgorithm(data);
  }, [data]);
  // Saves time when data doesn't change
}

// ✅ Necessary: Referential equality matters
function Parent() {
  const config = useMemo(() => ({
    theme: 'dark'
  }), []);
  
  return <MemoizedChild config={config} />;
  // Prevents child re-renders
}
```

---

**Measuring Performance:**

```javascript
function Component({ data }) {
  // Measure without useMemo
  const start1 = performance.now();
  const result1 = expensiveCalculation(data);
  const end1 = performance.now();
  console.log('Without useMemo:', end1 - start1, 'ms');
  
  // Measure with useMemo
  const result2 = useMemo(() => {
    const start2 = performance.now();
    const result = expensiveCalculation(data);
    const end2 = performance.now();
    console.log('With useMemo (calculating):', end2 - start2, 'ms');
    return result;
  }, [data]);
  
  // On first render:
  // Without useMemo: 50ms
  // With useMemo (calculating): 50ms
  
  // On re-render (data unchanged):
  // Without useMemo: 50ms
  // With useMemo: 0ms (cached)
  
  return <div>{result2}</div>;
}
```

---

**Internal Memoization Process:**

```javascript
// How React decides to use cached value
function useMemo(factory, deps) {
  const hook = hooks[hookIndex];
  
  if (!hook) {
    // First render - always compute
    const value = factory();
    hooks[hookIndex] = { value, deps };
    return value;
  }
  
  // Check each dependency
  const prevDeps = hook.deps;
  let depsChanged = false;
  
  if (!deps || !prevDeps) {
    depsChanged = true;
  } else {
    for (let i = 0; i < deps.length; i++) {
      if (!Object.is(deps[i], prevDeps[i])) {
        depsChanged = true;
        break;
      }
    }
  }
  
  if (depsChanged) {
    // Recompute
    console.log('useMemo: Computing new value');
    const value = factory();
    hook.value = value;
    hook.deps = deps;
    return value;
  } else {
    // Return cached
    console.log('useMemo: Returning cached value');
    return hook.value;
  }
}

// Object.is comparison:
Object.is(5, 5);              // true
Object.is('hi', 'hi');        // true
Object.is(true, true);        // true
Object.is({}, {});            // false (different objects)
Object.is([1], [1]);          // false (different arrays)

const obj = { a: 1 };
Object.is(obj, obj);          // true (same reference)
```

---

**Benefits:**
- ✅ **Performance** - Avoids expensive recalculations
- ✅ **Referential equality** - Same object/array reference across renders
- ✅ **Optimizes children** - Prevents unnecessary child re-renders
- ✅ **Flexible** - Works with any computation

**Trade-offs:**

| Benefit | Cost |
|---------|------|
| **Avoids recalculation** | Memory overhead (stores result) |
| **Stable references** | CPU overhead (dependency comparison) |
| **Performance gain** | Code complexity |

**When to use useMemo:**
- ✅ Expensive calculations (loops, recursion, complex algorithms)
- ✅ Creating objects/arrays passed to memoized children
- ✅ Derived state from expensive operations
- ✅ Context values to prevent consumer re-renders
- ❌ Avoid for simple calculations (addition, string concat)
- ❌ Avoid premature optimization
- ❌ Avoid when dependencies change every render

**Interview Tip:**
> "useMemo memoizes the result of a computation by storing it in the hook and comparing dependencies using Object.is(). It only recalculates when dependencies change, optimizing performance for expensive operations and maintaining referential equality for objects and arrays."

---

## useRef

### 🎯 What is useRef?

**Definition:**
> useRef is a React Hook that returns a mutable ref object whose `.current` property persists across renders without causing re-renders when changed.

**Simple meaning:**
useRef creates a "box" that holds a value that persists between renders - you can read and write to it, but changing it doesn't trigger re-renders.

**Real-life analogy:**
Like a sticky note on your desk - you can write on it, read it, and change it anytime without anyone noticing (no re-render), and it stays there between meetings (renders).

---

### 🔧 How useRef Works Internally

**Basic Usage:**

```javascript
function Component() {
  // Create ref
  const countRef = useRef(0);
  const inputRef = useRef(null);
  
  console.log(countRef);
  // { current: 0 }
  
  const handleClick = () => {
    // Update ref - NO re-render
    countRef.current += 1;
    console.log('Count:', countRef.current);
  };
  
  const focusInput = () => {
    // Access DOM element
    inputRef.current.focus();
  };
  
  return (
    <div>
      <input ref={inputRef} />
      <button onClick={handleClick}>Increment (no render)</button>
      <button onClick={focusInput}>Focus Input</button>
    </div>
  );
}
```

---

**Internal Implementation:**

```javascript
// Simplified useRef implementation
function useRef(initialValue) {
  const fiber = currentFiber;
  const hooks = fiber.hooks || [];
  const hook = hooks[hookIndex];
  
  // First render - create ref object
  if (!hook) {
    const ref = {
      current: initialValue
    };
    
    hooks[hookIndex] = ref;
    hookIndex++;
    return ref;
  }
  
  // Subsequent renders - return same ref object
  hookIndex++;
  return hook;
  
  // Key point: Same object reference every render
  // Mutating .current doesn't trigger re-render
}

// Comparison with useState:
function useState(initialValue) {
  // ...
  const setState = (newValue) => {
    hook.state = newValue;
    scheduleUpdate(fiber);  // Triggers re-render
  };
  return [hook.state, setState];
}

function useRef(initialValue) {
  // ...
  // No setter function
  // No re-render mechanism
  // Just returns mutable object
  return hook;
}
```

---

**useRef vs useState:**

```javascript
function Comparison() {
  const [stateCount, setStateCount] = useState(0);
  const refCount = useRef(0);
  
  console.log('Render');
  
  return (
    <div>
      {/* useState - triggers re-render */}
      <p>State: {stateCount}</p>
      <button onClick={() => setStateCount(stateCount + 1)}>
        Increment State
      </button>
      
      {/* useRef - NO re-render */}
      <p>Ref: {refCount.current}</p>
      <button onClick={() => {
        refCount.current += 1;
        console.log('Ref:', refCount.current);
        // UI doesn't update! No re-render!
      }}>
        Increment Ref
      </button>
      
      {/* Force re-render to see ref value */}
      <button onClick={() => setStateCount(stateCount)}>
        Force Re-render
      </button>
    </div>
  );
}

// Timeline:
// 1. Initial render: stateCount=0, refCount.current=0
// 2. Click "Increment Ref" 3 times
//    - refCount.current = 1, 2, 3
//    - No re-renders
//    - UI still shows "Ref: 0"
// 3. Click "Force Re-render"
//    - Component re-renders
//    - UI updates to "Ref: 3"
```

---

**Common Use Cases:**

**1. DOM References:**

```javascript
function TextInput() {
  const inputRef = useRef(null);
  
  useEffect(() => {
    // Focus input on mount
    inputRef.current.focus();
  }, []);
  
  const handleClear = () => {
    inputRef.current.value = '';
    inputRef.current.focus();
  };
  
  return (
    <div>
      <input ref={inputRef} type="text" />
      <button onClick={handleClear}>Clear</button>
    </div>
  );
}

// How ref callback works:
function attachRef(fiber, ref) {
  if (typeof ref === 'function') {
    // Callback ref
    ref(fiber.stateNode);
  } else if (ref && ref.hasOwnProperty('current')) {
    // Ref object
    ref.current = fiber.stateNode;
  }
}

// During commit phase:
function commitWork(fiber) {
  if (fiber.ref) {
    attachRef(fiber, fiber.ref);
  }
  // ...update DOM
}
```

**2. Previous Value:**

```javascript
function Counter() {
  const [count, setCount] = useState(0);
  const prevCountRef = useRef();
  
  useEffect(() => {
    // Store current value as previous for next render
    prevCountRef.current = count;
  });
  
  return (
    <div>
      <p>Current: {count}</p>
      <p>Previous: {prevCountRef.current}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

// Render timeline:
// Render 1: count=0, prevCountRef.current=undefined
// Effect runs: prevCountRef.current=0
// 
// User clicks button
// Render 2: count=1, prevCountRef.current=0 (from previous render)
// Effect runs: prevCountRef.current=1
// 
// User clicks button
// Render 3: count=2, prevCountRef.current=1
// Effect runs: prevCountRef.current=2

// Custom hook for previous value:
function usePrevious(value) {
  const ref = useRef();
  
  useEffect(() => {
    ref.current = value;
  });
  
  return ref.current;
}

// Usage:
const prevCount = usePrevious(count);
```

**3. Storing Mutable Values:**

```javascript
function Timer() {
  const [seconds, setSeconds] = useState(0);
  const intervalRef = useRef(null);
  
  const start = () => {
    if (intervalRef.current) return;  // Already running
    
    intervalRef.current = setInterval(() => {
      setSeconds(s => s + 1);
    }, 1000);
  };
  
  const stop = () => {
    clearInterval(intervalRef.current);
    intervalRef.current = null;
  };
  
  const reset = () => {
    stop();
    setSeconds(0);
  };
  
  useEffect(() => {
    // Cleanup on unmount
    return () => {
      if (intervalRef.current) {
        clearInterval(intervalRef.current);
      }
    };
  }, []);
  
  return (
    <div>
      <p>Time: {seconds}s</p>
      <button onClick={start}>Start</button>
      <button onClick={stop}>Stop</button>
      <button onClick={reset}>Reset</button>
    </div>
  );
}

// Why ref instead of state for interval ID?
// - intervalRef.current changes don't need re-renders
// - Stable reference across renders
// - Can access latest value in cleanup
```

**4. Avoiding Stale Closures:**

```javascript
function Component() {
  const [count, setCount] = useState(0);
  
  // ❌ Bad: Stale closure
  useEffect(() => {
    const timer = setInterval(() => {
      console.log('Count:', count);  // Always logs initial count!
    }, 1000);
    
    return () => clearInterval(timer);
  }, []);  // Empty deps - captures count from first render
  
  // ✅ Good: Use ref for latest value
  const countRef = useRef(count);
  
  useEffect(() => {
    countRef.current = count;  // Update ref on every render
  });
  
  useEffect(() => {
    const timer = setInterval(() => {
      console.log('Count:', countRef.current);  // Always latest!
    }, 1000);
    
    return () => clearInterval(timer);
  }, []);  // Empty deps - but accesses latest via ref
  
  return (
    <button onClick={() => setCount(count + 1)}>
      Count: {count}
    </button>
  );
}
```

**5. Instance Variables:**

```javascript
// Like class instance variables
class ClassComponent extends React.Component {
  constructor(props) {
    super(props);
    this.renderCount = 0;  // Instance variable
  }
  
  render() {
    this.renderCount++;  // Doesn't trigger re-render
    return <div>Rendered {this.renderCount} times</div>;
  }
}

// Equivalent with useRef
function FunctionalComponent() {
  const renderCount = useRef(0);
  
  renderCount.current++;  // Doesn't trigger re-render
  
  return <div>Rendered {renderCount.current} times</div>;
}
```

---

**Ref Forwarding:**

```javascript
// Parent can access child's DOM node
const FancyInput = React.forwardRef((props, ref) => {
  return <input ref={ref} className="fancy" {...props} />;
});

function Parent() {
  const inputRef = useRef(null);
  
  const focusInput = () => {
    inputRef.current.focus();
  };
  
  return (
    <div>
      <FancyInput ref={inputRef} />
      <button onClick={focusInput}>Focus</button>
    </div>
  );
}

// How forwardRef works internally:
function forwardRef(render) {
  return {
    $$typeof: REACT_FORWARD_REF_TYPE,
    render
  };
}

function renderForwardRef(fiber) {
  const Component = fiber.type.render;
  const props = fiber.props;
  const ref = fiber.ref;
  
  // Pass ref as second argument
  const elements = Component(props, ref);
  return elements;
}
```

---

**Callback Refs:**

```javascript
// Alternative to useRef - function that receives DOM node
function Component() {
  const [height, setHeight] = useState(0);
  
  // Callback ref
  const measuredRef = useCallback(node => {
    if (node !== null) {
      setHeight(node.getBoundingClientRect().height);
    }
  }, []);
  
  return (
    <div>
      <div ref={measuredRef}>
        <p>This element's height is measured</p>
      </div>
      <p>Height: {height}px</p>
    </div>
  );
}

// When callback ref is useful:
// - Need to measure DOM node
// - Need to run code when ref attaches/detaches
// - Dynamic refs (changing elements)

// How React calls callback refs:
function commitAttachRef(fiber) {
  const ref = fiber.ref;
  const instance = fiber.stateNode;
  
  if (typeof ref === 'function') {
    // Callback ref - call with DOM node
    ref(instance);
  } else {
    // Object ref - set .current
    ref.current = instance;
  }
}

function commitDetachRef(fiber) {
  const ref = fiber.ref;
  
  if (typeof ref === 'function') {
    // Callback ref - call with null
    ref(null);
  } else {
    // Object ref - clear .current
    ref.current = null;
  }
}
```

---

**Benefits:**
- ✅ **No re-renders** - Changing .current doesn't trigger renders
- ✅ **Persists** - Value survives across renders
- ✅ **Mutable** - Can update without setState
- ✅ **DOM access** - Direct access to DOM elements
- ✅ **Stable reference** - Same object every render

**Trade-offs:**

| Benefit | Cost |
|---------|------|
| **No re-renders** | UI doesn't update when ref changes |
| **Mutable** | Can lead to bugs if overused |
| **Direct DOM access** | Breaks React's declarative model |

**When to use useRef:**
- ✅ Accessing DOM elements (focus, scroll, measure)
- ✅ Storing mutable values (timers, subscriptions)
- ✅ Keeping previous values
- ✅ Avoiding stale closures
- ✅ Instance variables (don't need re-render)
- ❌ Avoid for values that should trigger re-renders (use useState)
- ❌ Avoid for derived state (calculate during render)
- ❌ Avoid overusing for DOM manipulation (prefer declarative)

**Interview Tip:**
> "useRef returns a mutable object with a .current property that persists across renders. Unlike useState, updating .current doesn't trigger re-renders. React attaches refs to DOM nodes during the commit phase, making them useful for accessing DOM elements and storing mutable values like timers or previous state."

---

## useLayoutEffect

### 🎯 What is useLayoutEffect?

**Definition:**
> useLayoutEffect is a React Hook identical to useEffect but fires synchronously after all DOM mutations and before the browser paints, allowing you to read layout and synchronously re-render.

**Simple meaning:**
useLayoutEffect runs before the browser paints the screen, while useEffect runs after - use it when you need to measure or modify DOM before user sees it.

**Real-life analogy:**
Like a stage crew adjusting props before the curtain opens (useLayoutEffect) vs. after the show starts (useEffect) - sometimes you need to fix things before the audience sees them.

---

### 🔧 How useLayoutEffect Works Internally

**Execution Order:**

```javascript
function Component() {
  const [count, setCount] = useState(0);
  
  console.log('1. Render');
  
  useLayoutEffect(() => {
    console.log('3. useLayoutEffect');
    return () => console.log('4. useLayoutEffect cleanup');
  });
  
  useEffect(() => {
    console.log('5. useEffect');
    return () => console.log('6. useEffect cleanup');
  });
  
  return <div>{count}</div>;
}

// Timeline:
// 1. Render (component function runs)
// 2. React commits to DOM
// 3. useLayoutEffect runs (BEFORE paint)
// 4. Browser paints (user sees update)
// 5. useEffect runs (AFTER paint)

// On re-render:
// 1. Render
// 2. React commits to DOM
// 3. useLayoutEffect cleanup
// 4. useLayoutEffect
// 5. Browser paints
// 6. useEffect cleanup
// 7. useEffect
```

---

**Internal Implementation:**

```javascript
// Simplified implementation
function useLayoutEffect(effect, deps) {
  const fiber = currentFiber;
  const hooks = fiber.hooks || [];
  const hook = hooks[hookIndex];
  
  if (!hook) {
    hooks[hookIndex] = {
      effect,
      deps,
      cleanup: null,
      tag: 'LAYOUT'  // Different from useEffect's 'PASSIVE'
    };
    
    // Add to layout effects queue
    fiber.layoutEffects.push(hooks[hookIndex]);
  } else {
    const prevDeps = hook.deps;
    const depsChanged = !deps || !prevDeps ||
      deps.some((dep, i) => !Object.is(dep, prevDeps[i]));
    
    if (depsChanged) {
      hook.effect = effect;
      hook.deps = deps;
      fiber.layoutEffects.push(hook);
    }
  }
  
  hookIndex++;
}

// Commit phase execution:
function commitRoot(root) {
  // 1. Before mutation phase
  
  // 2. Mutation phase - update DOM
  commitMutationEffects(root);
  
  // 3. Layout phase - SYNCHRONOUS
  commitLayoutEffects(root);  // useLayoutEffect runs here
  
  // 4. Browser paints
  
  // 5. Passive phase - ASYNCHRONOUS
  schedulePassiveEffects(root);  // useEffect runs here
}

function commitLayoutEffects(fiber) {
  // Run synchronously - blocks paint
  fiber.layoutEffects.forEach(hook => {
    if (hook.cleanup) {
      hook.cleanup();
    }
    hook.cleanup = hook.effect();
  });
  
  // Recurse to children
  commitLayoutEffects(fiber.child);
  commitLayoutEffects(fiber.sibling);
}
```

---

**useEffect vs useLayoutEffect:**

```javascript
// useEffect - runs AFTER paint (asynchronous)
function WithUseEffect() {
  const [width, setWidth] = useState(0);
  const ref = useRef(null);
  
  useEffect(() => {
    // Runs after browser paints
    setWidth(ref.current.offsetWidth);
  }, []);
  
  return (
    <div>
      <div ref={ref}>Measure me</div>
      <p>Width: {width}px</p>
    </div>
  );
}
// Timeline:
// 1. Render with width=0
// 2. DOM updated
// 3. Browser paints (user sees "Width: 0px")
// 4. useEffect runs, measures width
// 5. setWidth triggers re-render
// 6. Browser paints again (user sees "Width: 200px")
// Result: User sees flicker (0px → 200px)

// useLayoutEffect - runs BEFORE paint (synchronous)
function WithUseLayoutEffect() {
  const [width, setWidth] = useState(0);
  const ref = useRef(null);
  
  useLayoutEffect(() => {
    // Runs before browser paints
    setWidth(ref.current.offsetWidth);
  }, []);
  
  return (
    <div>
      <div ref={ref}>Measure me</div>
      <p>Width: {width}px</p>
    </div>
  );
}
// Timeline:
// 1. Render with width=0
// 2. DOM updated
// 3. useLayoutEffect runs, measures width
// 4. setWidth triggers re-render (synchronous)
// 5. Render with width=200
// 6. DOM updated
// 7. Browser paints (user sees "Width: 200px")
// Result: No flicker, user only sees correct width
```

---

**Common Use Cases:**

**1. DOM Measurements:**

```javascript
function Tooltip({ children, text }) {
  const [position, setPosition] = useState({ top: 0, left: 0 });
  const targetRef = useRef(null);
  const tooltipRef = useRef(null);
  
  useLayoutEffect(() => {
    // Measure elements before paint
    const targetRect = targetRef.current.getBoundingClientRect();
    const tooltipRect = tooltipRef.current.getBoundingClientRect();
    
    // Calculate position
    setPosition({
      top: targetRect.bottom + 5,
      left: targetRect.left + (targetRect.width - tooltipRect.width) / 2
    });
  }, [text]);
  
  return (
    <div>
      <div ref={targetRef}>{children}</div>
      <div
        ref={tooltipRef}
        style={{
          position: 'fixed',
          top: position.top,
          left: position.left
        }}
      >
        {text}
      </div>
    </div>
  );
}
```

**2. Scroll Position:**

```javascript
function ScrollToTop() {
  const [items, setItems] = useState([]);
  
  useLayoutEffect(() => {
    // Scroll before user sees new items
    window.scrollTo(0, 0);
  }, [items]);
  
  return (
    <div>
      {items.map(item => <div key={item.id}>{item.text}</div>)}
    </div>
  );
}
```

**3. DOM Mutations:**

```javascript
function AnimatedList({ items }) {
  const listRef = useRef(null);
  
  useLayoutEffect(() => {
    // Measure before animation
    const elements = listRef.current.children;
    const positions = Array.from(elements).map(el => ({
      top: el.offsetTop,
      left: el.offsetLeft
    }));
    
    // Apply animation
    elements.forEach((el, i) => {
      const deltaY = positions[i].top - el.offsetTop;
      
      if (deltaY) {
        el.style.transform = `translateY(${deltaY}px)`;
        el.style.transition = 'transform 0s';
        
        requestAnimationFrame(() => {
          el.style.transform = '';
          el.style.transition = 'transform 0.3s';
        });
      }
    });
  }, [items]);
  
  return (
    <div ref={listRef}>
      {items.map(item => (
        <div key={item.id}>{item.text}</div>
      ))}
    </div>
  );
}
```

**4. Preventing Visual Flicker:**

```javascript
function DynamicHeight() {
  const [show, setShow] = useState(false);
  const [height, setHeight] = useState(0);
  const contentRef = useRef(null);
  
  useLayoutEffect(() => {
    if (show) {
      // Measure and set height before paint
      const contentHeight = contentRef.current.scrollHeight;
      setHeight(contentHeight);
    } else {
      setHeight(0);
    }
  }, [show]);
  
  return (
    <div>
      <button onClick={() => setShow(!show)}>Toggle</button>
      <div
        style={{
          height: height,
          overflow: 'hidden',
          transition: 'height 0.3s'
        }}
      >
        <div ref={contentRef}>
          <p>Content that expands</p>
          <p>More content...</p>
        </div>
      </div>
    </div>
  );
}
```

---

**Performance Impact:**

```javascript
// useLayoutEffect blocks painting - can cause jank

// ❌ Bad: Expensive operation in useLayoutEffect
function Component() {
  useLayoutEffect(() => {
    // Blocks browser paint
    for (let i = 0; i < 1000000000; i++) {
      // Expensive calculation
    }
  });
  
  return <div>Content</div>;
}
// User sees frozen UI while effect runs

// ✅ Good: Use useEffect for non-visual operations
function Component() {
  useEffect(() => {
    // Doesn't block paint
    for (let i = 0; i < 1000000000; i++) {
      // Expensive calculation
    }
  });
  
  return <div>Content</div>;
}
// User sees content immediately, calculation runs after
```

---

**Server-Side Rendering:**

```javascript
// useLayoutEffect doesn't run on server

function Component() {
  useLayoutEffect(() => {
    // Only runs in browser
    console.log('Browser only');
  });
  
  return <div>Content</div>;
}

// Warning: useLayoutEffect does nothing on the server

// Solution: Conditional hook
function useIsomorphicLayoutEffect(effect, deps) {
  const isServer = typeof window === 'undefined';
  
  if (isServer) {
    useEffect(effect, deps);
  } else {
    useLayoutEffect(effect, deps);
  }
}

// Or suppress warning:
const useIsomorphicLayoutEffect =
  typeof window !== 'undefined' ? useLayoutEffect : useEffect;
```

---

**Benefits:**
- ✅ **No flicker** - Updates before paint
- ✅ **Accurate measurements** - Read layout before user sees
- ✅ **Synchronous** - Guaranteed order of operations
- ✅ **DOM mutations** - Safe to modify DOM before paint

**Trade-offs:**

| Benefit | Cost |
|---------|------|
| **Before paint** | Blocks painting (can cause jank) |
| **Synchronous** | Can't be interrupted |
| **Accurate measurements** | Runs on every render (expensive) |

**When to use useLayoutEffect:**
- ✅ Measuring DOM elements
- ✅ Preventing visual flicker
- ✅ Scroll position management
- ✅ DOM mutations before paint
- ✅ Animations that need layout info
- ❌ Avoid for data fetching (use useEffect)
- ❌ Avoid for expensive operations (blocks UI)
- ❌ Avoid when useEffect works fine

**Interview Tip:**
> "useLayoutEffect runs synchronously after DOM mutations but before browser paint, while useEffect runs asynchronously after paint. Use useLayoutEffect when you need to read layout or make DOM changes that should be visible in the same frame, but prefer useEffect for most cases as useLayoutEffect blocks painting and can cause performance issues."

---

## useImperativeHandle

### 🎯 What is useImperativeHandle?

**Definition:**
> useImperativeHandle customizes the instance value exposed to parent components when using ref, allowing you to control which methods and properties are accessible.

**Simple meaning:**
useImperativeHandle lets you decide what a parent component can do with your component's ref - like creating a custom remote control with only the buttons you want to expose.

**Real-life analogy:**
Like a car dashboard - the engine has many internal functions, but the dashboard (useImperativeHandle) only exposes what the driver needs: steering, gas, brakes. Not the raw engine internals.

---

### 🔧 How useImperativeHandle Works Internally

**Basic Usage:**

```javascript
// Child component
const FancyInput = forwardRef((props, ref) => {
  const inputRef = useRef(null);
  
  // Customize ref value
  useImperativeHandle(ref, () => ({
    // Expose only these methods
    focus: () => {
      inputRef.current.focus();
    },
    clear: () => {
      inputRef.current.value = '';
    },
    getValue: () => {
      return inputRef.current.value;
    }
    // Don't expose: inputRef.current (full DOM access)
  }));
  
  return <input ref={inputRef} {...props} />;
});

// Parent component
function Parent() {
  const fancyInputRef = useRef(null);
  
  const handleClick = () => {
    fancyInputRef.current.focus();  // ✅ Works
    fancyInputRef.current.clear();  // ✅ Works
    console.log(fancyInputRef.current.getValue());  // ✅ Works
    
    // ❌ Can't access raw DOM
    // fancyInputRef.current.style.color = 'red';  // undefined
  };
  
  return (
    <div>
      <FancyInput ref={fancyInputRef} />
      <button onClick={handleClick}>Focus & Clear</button>
    </div>
  );
}
```

---

**Internal Implementation:**

```javascript
// Simplified useImperativeHandle implementation
function useImperativeHandle(ref, createHandle, deps) {
  const fiber = currentFiber;
  
  useLayoutEffect(() => {
    if (!ref) return;
    
    // Create custom handle
    const handle = createHandle();
    
    // Assign to ref
    if (typeof ref === 'function') {
      ref(handle);
    } else {
      ref.current = handle;
    }
    
    // Cleanup
    return () => {
      if (typeof ref === 'function') {
        ref(null);
      } else {
        ref.current = null;
      }
    };
  }, deps);
}

// Why useLayoutEffect?
// - Runs synchronously after DOM updates
// - Ensures ref is set before parent's useLayoutEffect
// - Consistent with ref attachment timing
```

---

**Without vs With useImperativeHandle:**

```javascript
// ❌ Without useImperativeHandle - exposes full DOM
const Input = forwardRef((props, ref) => {
  return <input ref={ref} {...props} />;
});

function Parent() {
  const inputRef = useRef(null);
  
  // Parent has full DOM access
  inputRef.current.focus();  // ✅
  inputRef.current.value = 'hack';  // ✅ Can modify directly
  inputRef.current.style.display = 'none';  // ✅ Can break UI
  // Breaks encapsulation!
}

// ✅ With useImperativeHandle - controlled API
const Input = forwardRef((props, ref) => {
  const inputRef = useRef(null);
  
  useImperativeHandle(ref, () => ({
    focus: () => inputRef.current.focus(),
    // Only expose what's needed
  }));
  
  return <input ref={inputRef} {...props} />;
});

function Parent() {
  const inputRef = useRef(null);
  
  inputRef.current.focus();  // ✅ Works
  inputRef.current.value = 'hack';  // ❌ undefined
  inputRef.current.style.display = 'none';  // ❌ undefined
  // Encapsulation maintained!
}
```

---

**Common Patterns:**

**1. Form Control:**

```javascript
const FormField = forwardRef(({ label, ...props }, ref) => {
  const inputRef = useRef(null);
  const [error, setError] = useState('');
  
  useImperativeHandle(ref, () => ({
    focus: () => {
      inputRef.current.focus();
    },
    
    validate: () => {
      const value = inputRef.current.value;
      if (!value) {
        setError('Required');
        return false;
      }
      setError('');
      return true;
    },
    
    getValue: () => {
      return inputRef.current.value;
    },
    
    setValue: (value) => {
      inputRef.current.value = value;
    },
    
    reset: () => {
      inputRef.current.value = '';
      setError('');
    }
  }));
  
  return (
    <div>
      <label>{label}</label>
      <input ref={inputRef} {...props} />
      {error && <span className="error">{error}</span>}
    </div>
  );
});

// Parent usage
function Form() {
  const nameRef = useRef(null);
  const emailRef = useRef(null);
  
  const handleSubmit = (e) => {
    e.preventDefault();
    
    // Validate all fields
    const isNameValid = nameRef.current.validate();
    const isEmailValid = emailRef.current.validate();
    
    if (isNameValid && isEmailValid) {
      const data = {
        name: nameRef.current.getValue(),
        email: emailRef.current.getValue()
      };
      console.log('Submit:', data);
    } else {
      // Focus first invalid field
      if (!isNameValid) nameRef.current.focus();
      else if (!isEmailValid) emailRef.current.focus();
    }
  };
  
  const handleReset = () => {
    nameRef.current.reset();
    emailRef.current.reset();
  };
  
  return (
    <form onSubmit={handleSubmit}>
      <FormField ref={nameRef} label="Name" />
      <FormField ref={emailRef} label="Email" type="email" />
      <button type="submit">Submit</button>
      <button type="button" onClick={handleReset}>Reset</button>
    </form>
  );
}
```

**2. Video Player:**

```javascript
const VideoPlayer = forwardRef(({ src }, ref) => {
  const videoRef = useRef(null);
  const [playing, setPlaying] = useState(false);
  
  useImperativeHandle(ref, () => ({
    play: () => {
      videoRef.current.play();
      setPlaying(true);
    },
    
    pause: () => {
      videoRef.current.pause();
      setPlaying(false);
    },
    
    stop: () => {
      videoRef.current.pause();
      videoRef.current.currentTime = 0;
      setPlaying(false);
    },
    
    seek: (time) => {
      videoRef.current.currentTime = time;
    },
    
    setVolume: (volume) => {
      videoRef.current.volume = Math.max(0, Math.min(1, volume));
    },
    
    getCurrentTime: () => {
      return videoRef.current.currentTime;
    },
    
    getDuration: () => {
      return videoRef.current.duration;
    },
    
    isPlaying: () => {
      return playing;
    }
  }));
  
  return <video ref={videoRef} src={src} />;
});

// Usage
function App() {
  const playerRef = useRef(null);
  
  return (
    <div>
      <VideoPlayer ref={playerRef} src="/video.mp4" />
      <button onClick={() => playerRef.current.play()}>Play</button>
      <button onClick={() => playerRef.current.pause()}>Pause</button>
      <button onClick={() => playerRef.current.stop()}>Stop</button>
      <button onClick={() => playerRef.current.seek(30)}>Skip to 30s</button>
    </div>
  );
}
```

**3. Modal:**

```javascript
const Modal = forwardRef(({ children }, ref) => {
  const [isOpen, setIsOpen] = useState(false);
  const modalRef = useRef(null);
  
  useImperativeHandle(ref, () => ({
    open: () => {
      setIsOpen(true);
    },
    
    close: () => {
      setIsOpen(false);
    },
    
    toggle: () => {
      setIsOpen(prev => !prev);
    },
    
    isOpen: () => {
      return isOpen;
    }
  }));
  
  useEffect(() => {
    if (isOpen) {
      // Trap focus
      modalRef.current.focus();
    }
  }, [isOpen]);
  
  if (!isOpen) return null;
  
  return (
    <div className="modal-overlay">
      <div ref={modalRef} className="modal" tabIndex={-1}>
        {children}
      </div>
    </div>
  );
});

// Usage
function App() {
  const modalRef = useRef(null);
  
  return (
    <div>
      <button onClick={() => modalRef.current.open()}>
        Open Modal
      </button>
      
      <Modal ref={modalRef}>
        <h2>Modal Content</h2>
        <button onClick={() => modalRef.current.close()}>
          Close
        </button>
      </Modal>
    </div>
  );
}
```

---

**Dependencies:**

```javascript
const Component = forwardRef((props, ref) => {
  const [count, setCount] = useState(0);
  
  // ❌ Bad: No dependencies - stale closure
  useImperativeHandle(ref, () => ({
    logCount: () => {
      console.log(count);  // Always logs initial count!
    }
  }));
  
  // ✅ Good: Include dependencies
  useImperativeHandle(ref, () => ({
    logCount: () => {
      console.log(count);  // Logs current count
    }
  }), [count]);  // Recreate when count changes
  
  // ✅ Better: Use ref for latest value
  const countRef = useRef(count);
  countRef.current = count;
  
  useImperativeHandle(ref, () => ({
    logCount: () => {
      console.log(countRef.current);  // Always latest
    }
  }), []);  // No dependencies needed
  
  return <div>{count}</div>;
});
```

---

**Benefits:**
- ✅ **Encapsulation** - Hide internal implementation
- ✅ **Controlled API** - Expose only what's needed
- ✅ **Type safety** - Clear interface for TypeScript
- ✅ **Maintainability** - Can change internals without breaking parents

**Trade-offs:**

| Benefit | Cost |
|---------|------|
| **Encapsulation** | More boilerplate code |
| **Controlled API** | Less flexible for parent |
| **Clear interface** | Extra abstraction layer |

**When to use useImperativeHandle:**
- ✅ Reusable form components
- ✅ Media players
- ✅ Modals/dialogs
- ✅ Complex widgets with imperative API
- ✅ When you need to hide implementation details
- ❌ Avoid for simple components (use regular ref)
- ❌ Avoid when declarative props work better
- ❌ Avoid overusing imperative patterns

**Interview Tip:**
> "useImperativeHandle customizes the ref value exposed to parent components, using useLayoutEffect internally to ensure the ref is set synchronously. It promotes encapsulation by exposing only specific methods instead of the full DOM node, making components more maintainable and preventing parents from depending on internal implementation details."

---

## Custom Hooks

### 🎯 What are Custom Hooks?

**Definition:**
> Custom Hooks are JavaScript functions that start with "use" and can call other Hooks, allowing you to extract and reuse stateful logic across components.

**Simple meaning:**
Custom Hooks let you package up Hook logic into reusable functions - like creating your own tools by combining React's built-in tools.

**Real-life analogy:**
Like creating a recipe (custom hook) that combines basic cooking techniques (built-in hooks) - once created, you can use the same recipe in different dishes (components).

---

### 🔧 How Custom Hooks Work

**Basic Pattern:**

```javascript
// Custom Hook
function useCounter(initialValue = 0) {
  const [count, setCount] = useState(initialValue);
  
  const increment = () => setCount(c => c + 1);
  const decrement = () => setCount(c => c - 1);
  const reset = () => setCount(initialValue);
  
  return { count, increment, decrement, reset };
}

// Usage in components
function Counter1() {
  const { count, increment, decrement, reset } = useCounter(0);
  
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>+</button>
      <button onClick={decrement}>-</button>
      <button onClick={reset}>Reset</button>
    </div>
  );
}

function Counter2() {
  const { count, increment } = useCounter(10);
  
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
}

// Each component gets its own state!
// Counter1 and Counter2 have independent counts
```

---

**How React Handles Custom Hooks:**

```javascript
// React doesn't treat custom hooks specially
// They're just functions that call other hooks

function useCustomHook() {
  // When this runs, currentFiber is set to calling component
  const [state, setState] = useState(0);  // Hook 0 in component
  useEffect(() => {}, []);                 // Hook 1 in component
  
  return state;
}

function Component() {
  // currentFiber = Component's fiber
  const value = useCustomHook();  // Calls hooks in Component's context
  const [local, setLocal] = useState('');  // Hook 2 in component
  
  // Component's hooks: [useState, useEffect, useState]
  // All stored in Component's fiber, not in useCustomHook
}

// Internal hook tracking:
let currentFiber = null;
let hookIndex = 0;

function renderComponent(fiber) {
  currentFiber = fiber;  // Set current component
  hookIndex = 0;         // Reset hook index
  
  const Component = fiber.type;
  const elements = Component(fiber.props);
  
  // All hooks called during Component() are stored in fiber.hooks
  return elements;
}
```

---

**Common Custom Hook Patterns:**

**1. Data Fetching:**

```javascript
function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);
  
  useEffect(() => {
    let cancelled = false;
    
    setLoading(true);
    
    fetch(url)
      .then(res => res.json())
      .then(data => {
        if (!cancelled) {
          setData(data);
          setLoading(false);
        }
      })
      .catch(error => {
        if (!cancelled) {
          setError(error);
          setLoading(false);
        }
      });
    
    return () => {
      cancelled = true;
    };
  }, [url]);
  
  return { data, loading, error };
}

// Usage
function UserProfile({ userId }) {
  const { data: user, loading, error } = useFetch(`/api/users/${userId}`);
  
  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error.message}</div>;
  
  return <div>{user.name}</div>;
}
```

**2. Local Storage:**

```javascript
function useLocalStorage(key, initialValue) {
  // Get initial value from localStorage
  const [storedValue, setStoredValue] = useState(() => {
    try {
      const item = window.localStorage.getItem(key);
      return item ? JSON.parse(item) : initialValue;
    } catch (error) {
      console.error(error);
      return initialValue;
    }
  });
  
  // Update localStorage when value changes
  const setValue = (value) => {
    try {
      // Allow value to be a function
      const valueToStore = value instanceof Function
        ? value(storedValue)
        : value;
      
      setStoredValue(valueToStore);
      window.localStorage.setItem(key, JSON.stringify(valueToStore));
    } catch (error) {
      console.error(error);
    }
  };
  
  return [storedValue, setValue];
}

// Usage
function Settings() {
  const [theme, setTheme] = useLocalStorage('theme', 'light');
  const [language, setLanguage] = useLocalStorage('language', 'en');
  
  return (
    <div>
      <select value={theme} onChange={e => setTheme(e.target.value)}>
        <option value="light">Light</option>
        <option value="dark">Dark</option>
      </select>
      
      <select value={language} onChange={e => setLanguage(e.target.value)}>
        <option value="en">English</option>
        <option value="es">Spanish</option>
      </select>
    </div>
  );
}
```

**3. Window Size:**

```javascript
function useWindowSize() {
  const [size, setSize] = useState({
    width: window.innerWidth,
    height: window.innerHeight
  });
  
  useEffect(() => {
    const handleResize = () => {
      setSize({
        width: window.innerWidth,
        height: window.innerHeight
      });
    };
    
    window.addEventListener('resize', handleResize);
    
    return () => {
      window.removeEventListener('resize', handleResize);
    };
  }, []);
  
  return size;
}

// Usage
function ResponsiveComponent() {
  const { width, height } = useWindowSize();
  
  return (
    <div>
      <p>Window size: {width} x {height}</p>
      {width < 768 ? <MobileView /> : <DesktopView />}
    </div>
  );
}
```

**4. Previous Value:**

```javascript
function usePrevious(value) {
  const ref = useRef();
  
  useEffect(() => {
    ref.current = value;
  });
  
  return ref.current;
}

// Usage
function Counter() {
  const [count, setCount] = useState(0);
  const prevCount = usePrevious(count);
  
  return (
    <div>
      <p>Current: {count}</p>
      <p>Previous: {prevCount}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

**5. Debounce:**

```javascript
function useDebounce(value, delay) {
  const [debouncedValue, setDebouncedValue] = useState(value);
  
  useEffect(() => {
    const timer = setTimeout(() => {
      setDebouncedValue(value);
    }, delay);
    
    return () => {
      clearTimeout(timer);
    };
  }, [value, delay]);
  
  return debouncedValue;
}

// Usage
function SearchComponent() {
  const [searchTerm, setSearchTerm] = useState('');
  const debouncedSearchTerm = useDebounce(searchTerm, 500);
  
  useEffect(() => {
    if (debouncedSearchTerm) {
      // API call only after user stops typing for 500ms
      fetch(`/api/search?q=${debouncedSearchTerm}`)
        .then(res => res.json())
        .then(data => console.log(data));
    }
  }, [debouncedSearchTerm]);
  
  return (
    <input
      value={searchTerm}
      onChange={e => setSearchTerm(e.target.value)}
      placeholder="Search..."
    />
  );
}
```

**6. Toggle:**

```javascript
function useToggle(initialValue = false) {
  const [value, setValue] = useState(initialValue);
  
  const toggle = useCallback(() => {
    setValue(v => !v);
  }, []);
  
  const setTrue = useCallback(() => {
    setValue(true);
  }, []);
  
  const setFalse = useCallback(() => {
    setValue(false);
  }, []);
  
  return [value, toggle, setTrue, setFalse];
}

// Usage
function Modal() {
  const [isOpen, toggle, open, close] = useToggle(false);
  
  return (
    <div>
      <button onClick={open}>Open Modal</button>
      {isOpen && (
        <div className="modal">
          <p>Modal Content</p>
          <button onClick={close}>Close</button>
        </div>
      )}
    </div>
  );
}
```

**7. Interval:**

```javascript
function useInterval(callback, delay) {
  const savedCallback = useRef();
  
  // Remember latest callback
  useEffect(() => {
    savedCallback.current = callback;
  }, [callback]);
  
  // Set up interval
  useEffect(() => {
    if (delay !== null) {
      const id = setInterval(() => {
        savedCallback.current();
      }, delay);
      
      return () => clearInterval(id);
    }
  }, [delay]);
}

// Usage
function Timer() {
  const [seconds, setSeconds] = useState(0);
  const [isRunning, setIsRunning] = useState(true);
  
  useInterval(() => {
    setSeconds(s => s + 1);
  }, isRunning ? 1000 : null);  // null pauses interval
  
  return (
    <div>
      <p>Seconds: {seconds}</p>
      <button onClick={() => setIsRunning(!isRunning)}>
        {isRunning ? 'Pause' : 'Resume'}
      </button>
    </div>
  );
}
```

**8. Form:**

```javascript
function useForm(initialValues) {
  const [values, setValues] = useState(initialValues);
  const [errors, setErrors] = useState({});
  const [touched, setTouched] = useState({});
  
  const handleChange = (name, value) => {
    setValues(prev => ({ ...prev, [name]: value }));
  };
  
  const handleBlur = (name) => {
    setTouched(prev => ({ ...prev, [name]: true }));
  };
  
  const validate = (validationRules) => {
    const newErrors = {};
    
    Object.keys(validationRules).forEach(field => {
      const rule = validationRules[field];
      const value = values[field];
      
      if (rule.required && !value) {
        newErrors[field] = 'Required';
      } else if (rule.minLength && value.length < rule.minLength) {
        newErrors[field] = `Min length: ${rule.minLength}`;
      } else if (rule.pattern && !rule.pattern.test(value)) {
        newErrors[field] = 'Invalid format';
      }
    });
    
    setErrors(newErrors);
    return Object.keys(newErrors).length === 0;
  };
  
  const reset = () => {
    setValues(initialValues);
    setErrors({});
    setTouched({});
  };
  
  return {
    values,
    errors,
    touched,
    handleChange,
    handleBlur,
    validate,
    reset
  };
}

// Usage
function LoginForm() {
  const form = useForm({
    email: '',
    password: ''
  });
  
  const handleSubmit = (e) => {
    e.preventDefault();
    
    const isValid = form.validate({
      email: { required: true, pattern: /\S+@\S+\.\S+/ },
      password: { required: true, minLength: 6 }
    });
    
    if (isValid) {
      console.log('Submit:', form.values);
    }
  };
  
  return (
    <form onSubmit={handleSubmit}>
      <input
        type="email"
        value={form.values.email}
        onChange={e => form.handleChange('email', e.target.value)}
        onBlur={() => form.handleBlur('email')}
      />
      {form.touched.email && form.errors.email && (
        <span>{form.errors.email}</span>
      )}
      
      <input
        type="password"
        value={form.values.password}
        onChange={e => form.handleChange('password', e.target.value)}
        onBlur={() => form.handleBlur('password')}
      />
      {form.touched.password && form.errors.password && (
        <span>{form.errors.password}</span>
      )}
      
      <button type="submit">Login</button>
      <button type="button" onClick={form.reset}>Reset</button>
    </form>
  );
}
```

---

**Rules for Custom Hooks:**

```javascript
// ✅ Good: Starts with "use"
function useCustomHook() {
  const [state, setState] = useState(0);
  return state;
}

// ❌ Bad: Doesn't start with "use"
function customHook() {
  const [state, setState] = useState(0);  // Error! Hooks can't be called here
  return state;
}

// ✅ Good: Called at top level
function Component() {
  const value = useCustomHook();
  return <div>{value}</div>;
}

// ❌ Bad: Called conditionally
function Component({ condition }) {
  if (condition) {
    const value = useCustomHook();  // Error! Breaks rules of hooks
  }
}

// ✅ Good: Returns any value
function useCustomHook() {
  return [value, setValue];  // Array
  // or
  return { value, setValue };  // Object
  // or
  return value;  // Single value
}
```

---

**Benefits:**
- ✅ **Reusability** - Share logic across components
- ✅ **Composition** - Combine hooks to create new ones
- ✅ **Testability** - Test hooks independently
- ✅ **Separation of concerns** - Extract complex logic
- ✅ **Readability** - Named, self-documenting logic

**Trade-offs:**

| Benefit | Cost |
|---------|------|
| **Reusability** | Abstraction overhead |
| **Composition** | Can become complex |
| **Separation** | More files to maintain |

**When to create custom hooks:**
- ✅ Logic used in multiple components
- ✅ Complex stateful logic
- ✅ Side effects that need cleanup
- ✅ Combining multiple built-in hooks
- ✅ API integrations
- ❌ Avoid for simple one-time logic
- ❌ Avoid premature abstraction

**Interview Tip:**
> "Custom Hooks are functions that start with 'use' and can call other Hooks. They allow extracting component logic into reusable functions. React doesn't treat them specially - when a custom hook calls useState or useEffect, those hooks are registered in the calling component's fiber, not the custom hook itself. Each component using a custom hook gets its own isolated state."

---

## State Management

### 🎯 State Management Overview

**Definition:**
> State management is the practice of handling data that changes over time in your application, determining where state lives, how it updates, and how components access it.

**Simple meaning:**
State management is deciding where to store data, how to update it, and how to share it between components.

**Real-life analogy:**
Like organizing files in an office - you decide what goes in personal desks (local state), shared filing cabinets (lifted state), or central database (global state).

---

### 🔧 State Management Patterns

**1. Local State (useState):**

```javascript
// State used only in one component
function Counter() {
  const [count, setCount] = useState(0);
  
  return (
    <div>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

// When to use:
// - UI state (open/closed, selected, hover)
// - Form inputs
// - Component-specific data
```

**2. Lifted State:**

```javascript
// State shared between siblings - lift to common parent
function Parent() {
  const [count, setCount] = useState(0);
  
  return (
    <div>
      <Display count={count} />
      <Controls onIncrement={() => setCount(count + 1)} />
    </div>
  );
}

function Display({ count }) {
  return <p>Count: {count}</p>;
}

function Controls({ onIncrement }) {
  return <button onClick={onIncrement}>Increment</button>;
}

// When to use:
// - Siblings need same data
// - Parent coordinates children
// - Simple prop drilling (1-2 levels)
```

**3. Context API:**

```javascript
// Global state without prop drilling
const ThemeContext = createContext();

function App() {
  const [theme, setTheme] = useState('light');
  
  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      <Header />
      <Main />
      <Footer />
    </ThemeContext.Provider>
  );
}

function Header() {
  const { theme, setTheme } = useContext(ThemeContext);
  
  return (
    <header className={theme}>
      <button onClick={() => setTheme(theme === 'light' ? 'dark' : 'light')}>
        Toggle Theme
      </button>
    </header>
  );
}

// When to use:
// - Theme, language, auth
// - Rarely changing global state
// - Avoid prop drilling
```

**4. Reducer Pattern:**

```javascript
// Complex state logic with useReducer
const initialState = {
  items: [],
  filter: 'all',
  loading: false
};

function reducer(state, action) {
  switch (action.type) {
    case 'ADD_ITEM':
      return {
        ...state,
        items: [...state.items, action.payload]
      };
    
    case 'REMOVE_ITEM':
      return {
        ...state,
        items: state.items.filter(item => item.id !== action.payload)
      };
    
    case 'SET_FILTER':
      return {
        ...state,
        filter: action.payload
      };
    
    case 'SET_LOADING':
      return {
        ...state,
        loading: action.payload
      };
    
    default:
      return state;
  }
}

function TodoApp() {
  const [state, dispatch] = useReducer(reducer, initialState);
  
  const addTodo = (text) => {
    dispatch({
      type: 'ADD_ITEM',
      payload: { id: Date.now(), text, completed: false }
    });
  };
  
  return (
    <div>
      <TodoList items={state.items} dispatch={dispatch} />
      <AddTodo onAdd={addTodo} />
    </div>
  );
}

// When to use:
// - Complex state logic
// - Multiple sub-values
// - Next state depends on previous
// - Want predictable updates
```

---

### 🔍 State Management Libraries

**1. Redux Pattern (without library):**

```javascript
// Store
const createStore = (reducer, initialState) => {
  let state = initialState;
  const listeners = [];
  
  const getState = () => state;
  
  const dispatch = (action) => {
    state = reducer(state, action);
    listeners.forEach(listener => listener());
  };
  
  const subscribe = (listener) => {
    listeners.push(listener);
    return () => {
      const index = listeners.indexOf(listener);
      listeners.splice(index, 1);
    };
  };
  
  return { getState, dispatch, subscribe };
};

// Reducer
const counterReducer = (state = { count: 0 }, action) => {
  switch (action.type) {
    case 'INCREMENT':
      return { count: state.count + 1 };
    case 'DECREMENT':
      return { count: state.count - 1 };
    default:
      return state;
  }
};

// Create store
const store = createStore(counterReducer, { count: 0 });

// React integration
const StoreContext = createContext();

function StoreProvider({ children }) {
  const [state, setState] = useState(store.getState());
  
  useEffect(() => {
    const unsubscribe = store.subscribe(() => {
      setState(store.getState());
    });
    return unsubscribe;
  }, []);
  
  return (
    <StoreContext.Provider value={{ state, dispatch: store.dispatch }}>
      {children}
    </StoreContext.Provider>
  );
}

function useStore() {
  return useContext(StoreContext);
}

// Usage
function Counter() {
  const { state, dispatch } = useStore();
  
  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'INCREMENT' })}>+</button>
      <button onClick={() => dispatch({ type: 'DECREMENT' })}>-</button>
    </div>
  );
}
```

**2. Zustand Pattern:**

```javascript
// Simple state management with Zustand-like pattern
const createZustandStore = (createState) => {
  let state;
  const listeners = new Set();
  
  const setState = (partial) => {
    const nextState = typeof partial === 'function'
      ? partial(state)
      : partial;
    
    state = { ...state, ...nextState };
    listeners.forEach(listener => listener(state));
  };
  
  const getState = () => state;
  
  const subscribe = (listener) => {
    listeners.add(listener);
    return () => listeners.delete(listener);
  };
  
  state = createState(setState, getState);
  
  return { getState, setState, subscribe };
};

// Create store
const useCounterStore = createZustandStore((set, get) => ({
  count: 0,
  increment: () => set(state => ({ count: state.count + 1 })),
  decrement: () => set(state => ({ count: state.count - 1 })),
  reset: () => set({ count: 0 })
}));

// React hook
function useStore(selector) {
  const [state, setState] = useState(() => 
    selector ? selector(useCounterStore.getState()) : useCounterStore.getState()
  );
  
  useEffect(() => {
    return useCounterStore.subscribe((newState) => {
      setState(selector ? selector(newState) : newState);
    });
  }, [selector]);
  
  return state;
}

// Usage
function Counter() {
  const count = useStore(state => state.count);
  const increment = useStore(state => state.increment);
  
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
}
```

---

### 📊 State Management Decision Tree

```javascript
// Decision flow for choosing state management

function chooseStateManagement(requirements) {
  // 1. Is it UI state for one component?
  if (requirements.scope === 'single-component') {
    return 'useState';
  }
  
  // 2. Is it shared between siblings?
  if (requirements.scope === 'siblings') {
    return 'Lift state to parent';
  }
  
  // 3. Is it simple global state (theme, auth)?
  if (requirements.scope === 'global' && requirements.complexity === 'simple') {
    return 'Context API';
  }
  
  // 4. Is it complex state logic?
  if (requirements.complexity === 'complex' && requirements.scope === 'local') {
    return 'useReducer';
  }
  
  // 5. Is it global with complex logic?
  if (requirements.scope === 'global' && requirements.complexity === 'complex') {
    return 'Context + useReducer or State Management Library';
  }
  
  // 6. High-frequency updates?
  if (requirements.frequency === 'high') {
    return 'State Management Library (Redux, Zustand, Jotai)';
  }
  
  // 7. Server state (API data)?
  if (requirements.type === 'server') {
    return 'React Query / SWR';
  }
  
  return 'Start with useState, refactor as needed';
}
```

---

**Interview Tip:**
> "State management in React follows a hierarchy: local state with useState for component-specific data, lifted state for sibling communication, Context API for global but infrequently changing data, useReducer for complex state logic, and external libraries like Redux or Zustand for complex global state with high-frequency updates or when you need middleware, time-travel debugging, or advanced features."

---

## React.memo

### 🎯 What is React.memo?

**Definition:**
> React.memo is a higher-order component that memoizes a component, preventing re-renders when props haven't changed by performing a shallow comparison.

**Simple meaning:**
React.memo "remembers" a component's last render - if props are the same, it skips re-rendering and reuses the previous result.

**Real-life analogy:**
Like a photocopy machine with memory - if you ask for the same document twice, it gives you the copy it already made instead of scanning again.

---

### 🔧 How React.memo Works Internally

**Basic Usage:**

```javascript
// Without React.memo
function ExpensiveComponent({ data }) {
  console.log('Rendering ExpensiveComponent');
  // Expensive rendering logic
  return <div>{data}</div>;
}

// With React.memo
const MemoizedComponent = React.memo(function ExpensiveComponent({ data }) {
  console.log('Rendering ExpensiveComponent');
  return <div>{data}</div>;
});

function Parent() {
  const [count, setCount] = useState(0);
  const [data] = useState('Hello');
  
  return (
    <div>
      <button onClick={() => setCount(count + 1)}>
        Count: {count}
      </button>
      <MemoizedComponent data={data} />
    </div>
  );
}

// Without memo:
// - Parent re-renders (count changes)
// - ExpensiveComponent re-renders (logs "Rendering...")

// With memo:
// - Parent re-renders (count changes)
// - data prop hasn't changed
// - ExpensiveComponent doesn't re-render (no log)
```

---

**Internal Implementation:**

```javascript
// Simplified React.memo implementation
function memo(Component, arePropsEqual) {
  return function MemoizedComponent(props) {
    const fiber = currentFiber;
    const prevProps = fiber.alternate?.memoizedProps;
    
    // First render - no previous props
    if (!prevProps) {
      return Component(props);
    }
    
    // Compare props
    const propsAreEqual = arePropsEqual
      ? arePropsEqual(prevProps, props)
      : shallowEqual(prevProps, props);
    
    if (propsAreEqual) {
      // Props haven't changed - reuse previous render
      return fiber.alternate.child;
    }
    
    // Props changed - re-render
    return Component(props);
  };
}

// Shallow comparison
function shallowEqual(objA, objB) {
  if (Object.is(objA, objB)) {
    return true;
  }
  
  if (typeof objA !== 'object' || objA === null ||
      typeof objB !== 'object' || objB === null) {
    return false;
  }
  
  const keysA = Object.keys(objA);
  const keysB = Object.keys(objB);
  
  if (keysA.length !== keysB.length) {
    return false;
  }
  
  // Check if all keys and values match
  for (let i = 0; i < keysA.length; i++) {
    const key = keysA[i];
    
    if (!objB.hasOwnProperty(key) ||
        !Object.is(objA[key], objB[key])) {
      return false;
    }
  }
  
  return true;
}
```

---

**Custom Comparison:**

```javascript
// Default comparison (shallow)
const MemoizedDefault = React.memo(Component);

// Custom comparison function
const MemoizedCustom = React.memo(Component, (prevProps, nextProps) => {
  // Return true if props are equal (skip re-render)
  // Return false if props are different (re-render)
  
  return prevProps.id === nextProps.id &&
         prevProps.name === nextProps.name;
  // Ignores other props
});

// Example: Only re-render when specific props change
const UserCard = React.memo(
  ({ user, onEdit, onDelete }) => {
    console.log('Rendering UserCard');
    return (
      <div>
        <h3>{user.name}</h3>
        <p>{user.email}</p>
        <button onClick={() => onEdit(user.id)}>Edit</button>
        <button onClick={() => onDelete(user.id)}>Delete</button>
      </div>
    );
  },
  (prevProps, nextProps) => {
    // Only re-render if user data changes
    // Ignore function prop changes
    return prevProps.user.id === nextProps.user.id &&
           prevProps.user.name === nextProps.user.name &&
           prevProps.user.email === nextProps.user.email;
  }
);
```

---

**Common Pitfalls:**

```javascript
// ❌ Pitfall 1: Inline objects
function Parent() {
  return (
    <MemoizedChild config={{ theme: 'dark' }} />
    // New object every render - memo doesn't help!
  );
}

// ✅ Solution: Memoize object
function Parent() {
  const config = useMemo(() => ({ theme: 'dark' }), []);
  return <MemoizedChild config={config} />;
}

// ❌ Pitfall 2: Inline functions
function Parent() {
  return (
    <MemoizedChild onClick={() => console.log('click')} />
    // New function every render - memo doesn't help!
  );
}

// ✅ Solution: useCallback
function Parent() {
  const handleClick = useCallback(() => console.log('click'), []);
  return <MemoizedChild onClick={handleClick} />;
}

// ❌ Pitfall 3: Children prop
function Parent() {
  return (
    <MemoizedChild>
      <div>Content</div>
    </MemoizedChild>
    // Children is new element every render - memo doesn't help!
  );
}

// ✅ Solution: Extract child or memoize parent
const Content = memo(() => <div>Content</div>);

function Parent() {
  return (
    <MemoizedChild>
      <Content />
    </MemoizedChild>
  );
}
```

---

**When React.memo Helps:**

```javascript
// ✅ Scenario 1: Expensive rendering
const ExpensiveList = React.memo(({ items }) => {
  // Complex calculations, large lists, etc.
  return items.map(item => <ExpensiveItem key={item.id} {...item} />);
});

// ✅ Scenario 2: Frequent parent re-renders
function Parent() {
  const [count, setCount] = useState(0);
  const [data] = useState(/* large data */);
  
  return (
    <div>
      <button onClick={() => setCount(count + 1)}>
        Increment: {count}
      </button>
      <ExpensiveList items={data} />
      {/* Parent re-renders often, but data doesn't change */}
    </div>
  );
}

// ✅ Scenario 3: Pure components
const PureDisplay = React.memo(({ value }) => {
  // Same props always produce same output
  return <div>{value}</div>;
});
```

---

**When React.memo Doesn't Help:**

```javascript
// ❌ Scenario 1: Props change every render
function Parent() {
  const [count, setCount] = useState(0);
  
  return (
    <MemoizedChild count={count} />
    // count changes every render - memo overhead wasted
  );
}

// ❌ Scenario 2: Cheap rendering
const SimpleComponent = React.memo(({ text }) => {
  return <div>{text}</div>;
  // Rendering is so cheap, memo overhead isn't worth it
});

// ❌ Scenario 3: Internal state changes
const StatefulComponent = React.memo(() => {
  const [count, setCount] = useState(0);
  
  return (
    <button onClick={() => setCount(count + 1)}>
      {count}
    </button>
  );
  // Component re-renders due to own state, not props
  // memo doesn't prevent this
});
```

---

**Performance Measurement:**

```javascript
// Measure if memo actually helps
function Parent() {
  const [count, setCount] = useState(0);
  
  return (
    <div>
      <button onClick={() => setCount(count + 1)}>
        Increment: {count}
      </button>
      
      {/* Without memo */}
      <Child name="Regular" />
      
      {/* With memo */}
      <MemoizedChild name="Memoized" />
    </div>
  );
}

const Child = ({ name }) => {
  const start = performance.now();
  
  // Simulate expensive rendering
  let i = 0;
  while (i < 100000) i++;
  
  const end = performance.now();
  console.log(`${name} render time:`, end - start, 'ms');
  
  return <div>{name}</div>;
};

const MemoizedChild = React.memo(Child);

// Results (when parent re-renders but name prop unchanged):
// Regular render time: 5ms (every render)
// Memoized render time: 0ms (skipped)
```

---

**Benefits:**
- ✅ **Performance** - Skips expensive re-renders
- ✅ **Simple API** - Easy to apply
- ✅ **Automatic** - Works without manual optimization
- ✅ **Composable** - Works with hooks

**Trade-offs:**

| Benefit | Cost |
|---------|------|
| **Skips re-renders** | Memory overhead (stores previous props) |
| **Performance gain** | CPU overhead (prop comparison) |
| **Easy to use** | Can be overused |

**When to use React.memo:**
- ✅ Component renders often with same props
- ✅ Expensive rendering (complex calculations, large lists)
- ✅ Pure components (same props = same output)
- ✅ Parent re-renders frequently
- ❌ Avoid for cheap components
- ❌ Avoid when props change every render
- ❌ Avoid premature optimization

**Interview Tip:**
> "React.memo is a higher-order component that performs shallow comparison of props. If props haven't changed, it reuses the previous render result, skipping the component function execution and reconciliation. It's useful for expensive components that receive the same props frequently, but adds overhead for prop comparison and storing previous props, so should be used judiciously."

---

## Code Splitting & Lazy Loading

### 🎯 What is Code Splitting?

**Definition:**
> Code splitting is the practice of breaking your application bundle into smaller chunks that can be loaded on demand, reducing initial load time.

**Simple meaning:**
Instead of loading your entire app at once, you load only what's needed now and load the rest later when needed.

**Real-life analogy:**
Like a restaurant menu - you don't bring all the food to the table at once. You show the menu first, then bring dishes as they're ordered.

---

### 🔧 How React.lazy Works Internally

**Basic Usage:**

```javascript
// Traditional import - bundled immediately
import HeavyComponent from './HeavyComponent';

// Dynamic import - loaded on demand
const HeavyComponent = React.lazy(() => import('./HeavyComponent'));

function App() {
  const [show, setShow] = useState(false);
  
  return (
    <div>
      <button onClick={() => setShow(true)}>Load Component</button>
      
      {show && (
        <Suspense fallback={<div>Loading...</div>}>
          <HeavyComponent />
        </Suspense>
      )}
    </div>
  );
}

// Timeline:
// 1. App loads - HeavyComponent NOT in bundle
// 2. User clicks button
// 3. import('./HeavyComponent') starts loading
// 4. Suspense shows fallback
// 5. HeavyComponent loads
// 6. Suspense renders HeavyComponent
```

---

**Internal Implementation:**

```javascript
// Simplified React.lazy implementation
function lazy(loadComponent) {
  let status = 'pending';
  let result;
  let promise;
  
  return function LazyComponent(props) {
    if (status === 'pending') {
      // Start loading
      promise = loadComponent().then(
        module => {
          status = 'resolved';
          result = module.default;
        },
        error => {
          status = 'rejected';
          result = error;
        }
      );
      
      // Throw promise to Suspense
      throw promise;
    }
    
    if (status === 'resolved') {
      // Component loaded - render it
      const Component = result;
      return <Component {...props} />;
    }
    
    if (status === 'rejected') {
      // Loading failed - throw error
      throw result;
    }
  };
}

// How Suspense catches the promise
function Suspense({ children, fallback }) {
  try {
    return children;
  } catch (promise) {
    if (promise instanceof Promise) {
      // Promise thrown - show fallback
      promise.then(() => {
        // When resolved, trigger re-render
        forceUpdate();
      });
      return fallback;
    }
    // Not a promise - rethrow
    throw promise;
  }
}
```

---

**Route-Based Code Splitting:**

```javascript
import { lazy, Suspense } from 'react';
import { BrowserRouter, Routes, Route } from 'react-router-dom';

// Lazy load route components
const Home = lazy(() => import('./routes/Home'));
const About = lazy(() => import('./routes/About'));
const Dashboard = lazy(() => import('./routes/Dashboard'));
const Profile = lazy(() => import('./routes/Profile'));

function App() {
  return (
    <BrowserRouter>
      <Suspense fallback={<LoadingSpinner />}>
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/about" element={<About />} />
          <Route path="/dashboard" element={<Dashboard />} />
          <Route path="/profile" element={<Profile />} />
        </Routes>
      </Suspense>
    </BrowserRouter>
  );
}

// Bundle structure:
// main.js - App, routing logic
// home.chunk.js - Home component
// about.chunk.js - About component
// dashboard.chunk.js - Dashboard component
// profile.chunk.js - Profile component

// User visits "/" - loads main.js + home.chunk.js only
// User navigates to "/about" - loads about.chunk.js
```

---

**Component-Based Code Splitting:**

```javascript
// Heavy modal loaded only when opened
const HeavyModal = lazy(() => import('./HeavyModal'));

function App() {
  const [isModalOpen, setIsModalOpen] = useState(false);
  
  return (
    <div>
      <button onClick={() => setIsModalOpen(true)}>
        Open Modal
      </button>
      
      {isModalOpen && (
        <Suspense fallback={<ModalSkeleton />}>
          <HeavyModal onClose={() => setIsModalOpen(false)} />
        </Suspense>
      )}
    </div>
  );
}

// Heavy chart library loaded only when needed
const ChartComponent = lazy(() => import('./ChartComponent'));

function Dashboard({ showChart }) {
  return (
    <div>
      <h1>Dashboard</h1>
      
      {showChart && (
        <Suspense fallback={<ChartSkeleton />}>
          <ChartComponent data={data} />
        </Suspense>
      )}
    </div>
  );
}
```

---

**Preloading:**

```javascript
// Preload component before user needs it
const HeavyComponent = lazy(() => import('./HeavyComponent'));

// Preload function
const preloadHeavyComponent = () => {
  import('./HeavyComponent');
};

function App() {
  return (
    <div>
      {/* Preload on hover */}
      <button
        onMouseEnter={preloadHeavyComponent}
        onClick={() => setShow(true)}
      >
        Show Component
      </button>
      
      {show && (
        <Suspense fallback={<div>Loading...</div>}>
          <HeavyComponent />
        </Suspense>
      )}
    </div>
  );
}

// Advanced: Preload after initial render
function App() {
  useEffect(() => {
    // Preload after 2 seconds of idle time
    const timer = setTimeout(() => {
      import('./HeavyComponent');
    }, 2000);
    
    return () => clearTimeout(timer);
  }, []);
  
  return <div>...</div>;
}
```

---

**Error Boundaries with Lazy:**

```javascript
class ErrorBoundary extends React.Component {
  state = { hasError: false };
  
  static getDerivedStateFromError(error) {
    return { hasError: true };
  }
  
  componentDidCatch(error, errorInfo) {
    console.error('Lazy loading failed:', error, errorInfo);
  }
  
  render() {
    if (this.state.hasError) {
      return (
        <div>
          <h2>Failed to load component</h2>
          <button onClick={() => window.location.reload()}>
            Reload
          </button>
        </div>
      );
    }
    
    return this.props.children;
  }
}

function App() {
  return (
    <ErrorBoundary>
      <Suspense fallback={<Loading />}>
        <LazyComponent />
      </Suspense>
    </ErrorBoundary>
  );
}
```

---

**Named Exports with Lazy:**

```javascript
// Component file with named export
// MyComponent.js
export function MyComponent() {
  return <div>My Component</div>;
}

// ❌ Doesn't work - lazy expects default export
const MyComponent = lazy(() => import('./MyComponent'));

// ✅ Solution 1: Re-export as default
// MyComponent.js
export function MyComponent() {
  return <div>My Component</div>;
}
export default MyComponent;

// ✅ Solution 2: Inline default export
const MyComponent = lazy(() =>
  import('./MyComponent').then(module => ({
    default: module.MyComponent
  }))
);

// ✅ Solution 3: Wrapper file
// MyComponentWrapper.js
export { MyComponent as default } from './MyComponent';

const MyComponent = lazy(() => import('./MyComponentWrapper'));
```

---

**Benefits:**
- ✅ **Faster initial load** - Smaller initial bundle
- ✅ **Better performance** - Load only what's needed
- ✅ **Improved UX** - App becomes interactive faster
- ✅ **Bandwidth savings** - Users don't download unused code

**Trade-offs:**

| Benefit | Cost |
|---------|------|
| **Smaller initial bundle** | More network requests |
| **Faster startup** | Delay when loading lazy components |
| **Less bandwidth** | Complexity in code organization |

**Interview Tip:**
> "React.lazy uses dynamic import() which returns a Promise. When a lazy component renders, it throws this Promise, which Suspense catches and shows a fallback. Once the Promise resolves with the component module, React re-renders with the actual component. This enables code splitting, reducing initial bundle size by loading components on demand."

---

## Concurrent Rendering (React 18)

### 🎯 What is Concurrent Rendering?

**Definition:**
> Concurrent rendering is React's ability to work on multiple state updates simultaneously, pause and resume work, and prioritize urgent updates over less urgent ones.

**Simple meaning:**
React can start rendering an update, pause if something more important comes up, and resume later - making apps more responsive.

**Real-life analogy:**
Like a chef who can start making a complex dish, pause to handle a quick order, then resume the complex dish - urgent tasks don't wait for long tasks to finish.

---

### 🔧 How Concurrent Rendering Works

**Before React 18 (Synchronous):**

```javascript
function App() {
  const [text, setText] = useState('');
  const [items, setItems] = useState([]);
  
  const handleChange = (e) => {
    const value = e.target.value;
    
    // Both updates processed together
    setText(value);  // Urgent - user is typing
    
    // Expensive filtering
    const filtered = hugeList.filter(item =>
      item.name.includes(value)
    );  // Blocks UI - user sees lag
    setItems(filtered);
  };
  
  return (
    <div>
      <input value={text} onChange={handleChange} />
      <List items={items} />
    </div>
  );
}

// Timeline (React 17):
// 1. User types 'a'
// 2. handleChange runs
// 3. setText('a') - queued
// 4. Expensive filter runs - BLOCKS
// 5. setItems(filtered) - queued
// 6. React renders both updates together
// 7. UI updates - user sees lag
```

**React 18 (Concurrent):**

```javascript
import { useTransition } from 'react';

function App() {
  const [text, setText] = useState('');
  const [items, setItems] = useState([]);
  const [isPending, startTransition] = useTransition();
  
  const handleChange = (e) => {
    const value = e.target.value;
    
    // Urgent update - high priority
    setText(value);
    
    // Non-urgent update - low priority
    startTransition(() => {
      const filtered = hugeList.filter(item =>
        item.name.includes(value)
      );
      setItems(filtered);
    });
  };
  
  return (
    <div>
      <input value={text} onChange={handleChange} />
      {isPending && <Spinner />}
      <List items={items} />
    </div>
  );
}

// Timeline (React 18):
// 1. User types 'a'
// 2. setText('a') - high priority
// 3. React renders input immediately
// 4. UI updates - no lag!
// 5. startTransition work begins
// 6. User types 'b' - interrupts transition
// 7. setText('b') - high priority
// 8. React renders input immediately
// 9. Previous transition abandoned
// 10. New transition begins
```

---

**Internal Priority System:**

```javascript
// React's priority levels
const ImmediatePriority = 1;      // Click, input, focus
const UserBlockingPriority = 2;   // Scroll, hover
const NormalPriority = 3;         // Network responses
const LowPriority = 4;            // Analytics, logging
const IdlePriority = 5;           // Background work

// How React schedules work
function scheduleUpdate(fiber, update, priority) {
  // Add update to fiber's queue with priority
  fiber.updateQueue.push({
    update,
    priority,
    timestamp: now()
  });
  
  // Schedule work based on priority
  if (priority === ImmediatePriority) {
    // Process immediately
    performSyncWork(fiber);
  } else {
    // Schedule for later
    scheduleCallback(priority, () => performWork(fiber));
  }
}

// Work loop with interruption
function workLoop(deadline) {
  let shouldYield = false;
  
  while (nextUnitOfWork && !shouldYield) {
    // Check for higher priority work
    if (hasHigherPriorityWork()) {
      // Pause current work
      shouldYield = true;
      break;
    }
    
    // Check if we have time left
    if (deadline.timeRemaining() < 1) {
      shouldYield = true;
      break;
    }
    
    // Process one unit of work
    nextUnitOfWork = performUnitOfWork(nextUnitOfWork);
  }
  
  // Continue later if work remains
  if (nextUnitOfWork) {
    scheduleCallback(NormalPriority, workLoop);
  } else {
    // Work complete - commit
    commitRoot();
  }
}
```

---

**useTransition:**

```javascript
function SearchResults() {
  const [query, setQuery] = useState('');
  const [results, setResults] = useState([]);
  const [isPending, startTransition] = useTransition();
  
  const handleSearch = (value) => {
    // Urgent: Update input immediately
    setQuery(value);
    
    // Non-urgent: Update results (can be interrupted)
    startTransition(() => {
      const filtered = searchData(value);
      setResults(filtered);
    });
  };
  
  return (
    <div>
      <input
        value={query}
        onChange={e => handleSearch(e.target.value)}
      />
      
      {isPending ? (
        <div>Searching...</div>
      ) : (
        <ResultsList results={results} />
      )}
    </div>
  );
}

// How useTransition works internally
function useTransition() {
  const [isPending, setIsPending] = useState(false);
  
  const startTransition = useCallback((callback) => {
    setIsPending(true);
    
    // Mark updates in callback as low priority
    runWithLowPriority(() => {
      callback();
      setIsPending(false);
    });
  }, []);
  
  return [isPending, startTransition];
}

function runWithLowPriority(callback) {
  const prevPriority = currentPriority;
  currentPriority = LowPriority;
  
  try {
    callback();
  } finally {
    currentPriority = prevPriority;
  }
}
```

---

**useDeferredValue:**

```javascript
// Alternative to useTransition
function SearchResults() {
  const [query, setQuery] = useState('');
  
  // Defer expensive computation
  const deferredQuery = useDeferredValue(query);
  
  // Expensive filtering uses deferred value
  const results = useMemo(() => {
    return searchData(deferredQuery);
  }, [deferredQuery]);
  
  // Show stale results while new results loading
  const isStale = query !== deferredQuery;
  
  return (
    <div>
      <input
        value={query}
        onChange={e => setQuery(e.target.value)}
      />
      
      <div style={{ opacity: isStale ? 0.5 : 1 }}>
        <ResultsList results={results} />
      </div>
    </div>
  );
}

// How useDeferredValue works internally
function useDeferredValue(value) {
  const [deferredValue, setDeferredValue] = useState(value);
  
  useEffect(() => {
    // Update deferred value with low priority
    startTransition(() => {
      setDeferredValue(value);
    });
  }, [value]);
  
  return deferredValue;
}
```

---

**Automatic Batching:**

```javascript
// React 17 - Only batches in event handlers
function handleClick() {
  setCount(c => c + 1);  // Batched
  setFlag(f => !f);      // Batched
  // One re-render
}

setTimeout(() => {
  setCount(c => c + 1);  // NOT batched
  setFlag(f => !f);      // NOT batched
  // Two re-renders
}, 1000);

fetch('/api').then(() => {
  setCount(c => c + 1);  // NOT batched
  setFlag(f => !f);      // NOT batched
  // Two re-renders
});

// React 18 - Batches everywhere
function handleClick() {
  setCount(c => c + 1);  // Batched
  setFlag(f => !f);      // Batched
  // One re-render
}

setTimeout(() => {
  setCount(c => c + 1);  // Batched
  setFlag(f => !f);      // Batched
  // One re-render
}, 1000);

fetch('/api').then(() => {
  setCount(c => c + 1);  // Batched
  setFlag(f => !f);      // Batched
  // One re-render
});

// Opt-out of batching if needed
import { flushSync } from 'react-dom';

function handleClick() {
  flushSync(() => {
    setCount(c => c + 1);  // Renders immediately
  });
  
  flushSync(() => {
    setFlag(f => !f);      // Renders immediately
  });
  // Two re-renders
}
```

---

**Suspense for Data Fetching:**

```javascript
// Resource that suspends
function createResource(promise) {
  let status = 'pending';
  let result;
  
  const suspender = promise.then(
    data => {
      status = 'success';
      result = data;
    },
    error => {
      status = 'error';
      result = error;
    }
  );
  
  return {
    read() {
      if (status === 'pending') {
        throw suspender;  // Suspense catches this
      }
      if (status === 'error') {
        throw result;
      }
      return result;
    }
  };
}

// Usage
const userResource = createResource(fetchUser());

function UserProfile() {
  const user = userResource.read();  // Suspends if not ready
  
  return <div>{user.name}</div>;
}

function App() {
  return (
    <Suspense fallback={<Loading />}>
      <UserProfile />
    </Suspense>
  );
}

// Timeline:
// 1. UserProfile renders
// 2. userResource.read() throws promise
// 3. Suspense catches promise
// 4. Suspense shows <Loading />
// 5. Promise resolves
// 6. React re-renders UserProfile
// 7. userResource.read() returns data
// 8. Suspense shows <UserProfile />
```

---

**Benefits:**
- ✅ **Responsive UI** - Urgent updates don't wait for slow updates
- ✅ **Interruptible** - Can pause and resume work
- ✅ **Prioritization** - Important updates processed first
- ✅ **Better UX** - Smoother interactions
- ✅ **Automatic batching** - Fewer re-renders

**Trade-offs:**

| Benefit | Cost |
|---------|------|
| **Interruptible rendering** | More complex internal logic |
| **Prioritization** | Need to understand priority levels |
| **Better performance** | Requires React 18+ |

**Interview Tip:**
> "Concurrent rendering allows React to work on multiple updates simultaneously and prioritize them. It uses a priority-based scheduler that can pause low-priority work when high-priority updates arrive. useTransition marks updates as non-urgent, allowing React to keep the UI responsive by processing urgent updates first and potentially abandoning incomplete low-priority work when new updates arrive."

---

## Common Interview Questions

### Basic Questions

**1. What is React and why use it?**
> "React is a JavaScript library for building UIs using a component-based architecture. It uses a Virtual DOM for efficient updates, provides declarative syntax with JSX, enables component reusability, and has unidirectional data flow for predictable state management."

**2. What is the Virtual DOM?**
> "Virtual DOM is a lightweight JavaScript representation of the real DOM. React creates a Virtual DOM tree, and when state changes, it creates a new tree, compares them using a diffing algorithm, calculates minimal changes needed, and updates only those parts in the real DOM, making updates efficient."

**3. What is JSX?**
> "JSX is a syntax extension that looks like HTML but is transformed into React.createElement() calls by Babel. It makes component code more readable and allows embedding JavaScript expressions using curly braces."

**4. What's the difference between state and props?**
> "Props are read-only data passed from parent to child components, while state is mutable data managed within a component. Props flow down the component tree, state is local to a component. Changing props requires parent update, changing state triggers component re-render."

**5. What is the difference between useEffect and useLayoutEffect?**
> "useEffect runs asynchronously after the browser paints, suitable for most side effects. useLayoutEffect runs synchronously after DOM mutations but before paint, used for DOM measurements or mutations that must be visible in the same frame, but can block painting if expensive."

**6. How does useState work internally?**
> "useState stores state in the component's fiber node in a hooks array. React maintains a hook index that increments with each hook call. When setState is called, React queues the update, schedules a re-render, and on next render, processes the queue to compute new state using Object.is() comparison."

**7. What are keys in React and why are they important?**
> "Keys help React identify which items in a list have changed, been added, or removed. During reconciliation, React uses keys to match elements between renders, enabling efficient reordering without recreating DOM nodes. Keys should be stable, unique, and not array indices for dynamic lists."

**8. What is prop drilling and how to avoid it?**
> "Prop drilling is passing props through multiple component layers to reach a deeply nested component. Avoid it using Context API for global state, component composition with children props, or state management libraries like Redux or Zustand."

**9. What is React.memo?**
> "React.memo is a higher-order component that memoizes a component, preventing re-renders when props haven't changed. It performs shallow comparison of props and reuses previous render if props are equal, optimizing performance for expensive components."

**10. What are custom hooks?**
> "Custom hooks are JavaScript functions starting with 'use' that can call other hooks, allowing extraction of stateful logic into reusable functions. They enable sharing logic across components while maintaining independent state for each component."

---

### Advanced Questions

**1. Explain React's reconciliation algorithm.**
> "Reconciliation is React's diffing algorithm that compares Virtual DOM trees. It uses heuristics: elements of different types produce different trees (full rebuild), same type elements update props, and keys identify moved children. It's O(n) complexity, processes level-by-level, and generates minimal DOM operations."

**2. How does Fiber architecture work?**
> "Fiber is React's reconciliation engine using a linked-list tree structure. Each element becomes a fiber node with pointers to child, sibling, and parent. Fiber enables incremental rendering by breaking work into units, pausing/resuming work, prioritizing updates, and using double buffering (current and work-in-progress trees) for concurrent features."

**3. Explain React's batching mechanism.**
> "React batches multiple setState calls into a single re-render for performance. In React 17, batching worked only in event handlers. React 18 has automatic batching everywhere - timeouts, promises, native events. React queues updates, processes them together, and commits once. Use flushSync to opt-out."

**4. How does useCallback prevent re-renders?**
> "useCallback memoizes a function, returning the same reference across renders unless dependencies change. When combined with React.memo, it prevents child re-renders because the function prop maintains referential equality. React stores the function in the hook and compares dependencies using Object.is()."

**5. What's the difference between controlled and uncontrolled components?**
> "Controlled components have form data controlled by React state - value comes from state, changes update state via onChange. Uncontrolled components store data in the DOM - access via refs, useful for simple forms or integrating with non-React code. Controlled provides validation and dynamic behavior, uncontrolled is simpler but less flexible."

**6. How does Context API work internally?**
> "Context uses a provider-consumer pattern. createContext creates an object with _currentValue. Provider updates this value and tracks consumers in the subtree. When value changes, React finds all consumers by traversing fibers, schedules updates only for consumers and their ancestors, maintaining a context stack during render for nested providers."

**7. Explain concurrent rendering in React 18.**
> "Concurrent rendering allows React to work on multiple updates simultaneously, pause work for higher priority updates, and resume later. It uses a priority-based scheduler with lanes. useTransition marks updates as non-urgent, allowing urgent updates to interrupt. This keeps UI responsive during expensive updates."

**8. How does React handle errors?**
> "Error boundaries are class components with componentDidCatch and getDerivedStateFromError lifecycle methods. They catch errors in child components during rendering, lifecycle methods, and constructors. Errors in event handlers, async code, or the error boundary itself aren't caught. Functional components can't be error boundaries yet."

**9. What are React portals and when to use them?**
> "Portals render children into a DOM node outside the parent component's hierarchy using ReactDOM.createPortal(child, container). Useful for modals, tooltips, dropdowns that need to escape overflow:hidden or z-index stacking. Events still bubble through React tree, not DOM tree."

**10. Explain the rules of hooks and why they exist.**
> "Hooks must be called at the top level (not in conditions/loops) and only in functional components or custom hooks. This is because React relies on call order to match hooks with their state stored in the fiber's hooks array. Breaking order causes hooks to get mismatched with their state, leading to bugs."

**11. How does React's Suspense work?**
> "Suspense catches promises thrown by components. When a component suspends (throws a promise), Suspense catches it, shows fallback UI, and waits for the promise to resolve. Once resolved, React re-renders the component. Used with React.lazy for code splitting and data fetching libraries."

**12. What's the difference between useMemo and useCallback?**
> "useMemo memoizes a computed value, useCallback memoizes a function. useMemo(() => computation, deps) returns the result, useCallback((args) => fn, deps) returns the function itself. useCallback(fn, deps) is equivalent to useMemo(() => fn, deps). Both prevent unnecessary recalculations/recreations."

---

## 🎓 Key Takeaways

### Core Principles:
1. **Declarative UI** - Describe what you want, React handles how
2. **Component-Based** - Build encapsulated components that manage their own state
3. **Unidirectional Data Flow** - Data flows down, events flow up
4. **Virtual DOM** - Efficient updates through reconciliation
5. **Composition over Inheritance** - Combine components rather than extend

### Performance Rules:
1. **Measure First** - Profile before optimizing
2. **Memoize Wisely** - Use React.memo, useMemo, useCallback judiciously
3. **Code Split** - Load code on demand with React.lazy
4. **Avoid Inline Objects/Functions** - In props for memoized components
5. **Keys Matter** - Use stable, unique keys for lists

### Best Practices:
1. **Keep Components Small** - Single responsibility principle
2. **Lift State Carefully** - Only as high as needed
3. **Use Custom Hooks** - Extract reusable logic
4. **Handle Errors** - Use error boundaries
5. **Test Components** - Unit and integration tests

---

