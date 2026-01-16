# Node.js Complete Guide

## Table of Contents

### Node.js Fundamentals
- [Introduction to Node.js](#introduction-to-nodejs)
- [Node.js Architecture](#nodejs-architecture)
- [Modules System](#modules-system)
- [NPM & Package Management](#npm--package-management)

### Core Modules
- [File System (fs)](#file-system-fs)
- [Path Module](#path-module)
- [HTTP Module](#http-module)
- [Events Module](#events-module)
- [Stream Module](#stream-module)
- [Buffer](#buffer)

### Express.js Framework
- [Express Basics](#express-basics)
- [Routing](#routing)
- [Middleware](#middleware)
- [Error Handling](#error-handling-in-express)
- [REST API Development](#rest-api-development)

### Database Integration
- [MongoDB with Mongoose](#mongodb-with-mongoose)
- [SQL with Sequelize](#sql-with-sequelize)
- [Connection Pooling](#connection-pooling)

### Authentication & Security
- [JWT Authentication](#jwt-authentication)
- [Password Hashing](#password-hashing)
- [Security Best Practices](#security-best-practices)

### Advanced Concepts
- [Process & Child Processes](#process--child-processes)
- [Cluster Module](#cluster-module)
- [Worker Threads](#worker-threads)
- [Performance Optimization](#performance-optimization)

### Testing & Deployment
- [Testing with Jest](#testing-with-jest)
- [Environment Variables](#environment-variables)
- [Deployment Strategies](#deployment-strategies)

### Interview Preparation
- [Common Interview Questions](#common-interview-questions)
- [Coding Challenges](#coding-challenges-1)

---

# Node.js Fundamentals

## Introduction to Node.js

### 🎯 What is Node.js?

**Definition:**
> Node.js is a JavaScript runtime built on Chrome's V8 engine that allows JavaScript to run on the server side.

**Simple meaning:**
Node.js lets you use JavaScript outside the browser - for servers, APIs, and command-line tools.

**Key Features:**
- **Asynchronous & Non-blocking** - Handles many requests simultaneously
- **Event-driven** - Uses events and callbacks
- **Single-threaded** - One main thread with event loop
- **Fast** - Built on V8 engine
- **NPM** - Largest package ecosystem
- **Cross-platform** - Runs on Windows, Mac, Linux

**Real-life analogy:**
Node.js is like a restaurant with one waiter (single thread) who takes orders and delivers food without waiting for the kitchen (async I/O) - handles many customers efficiently.

---

### Node.js vs Browser JavaScript

| Feature | Browser JavaScript | Node.js |
|---------|-------------------|---------|
| **Environment** | Browser (Chrome, Firefox) | Server/Desktop |
| **Global object** | window | global |
| **DOM** | ✅ Available | ❌ Not available |
| **File system** | ❌ Limited | ✅ Full access |
| **Modules** | ES6 modules | CommonJS + ES6 |
| **APIs** | fetch, localStorage | fs, http, path |
| **Use case** | Frontend | Backend, CLI tools |

---

### When to Use Node.js

**✅ Good for:**
- REST APIs
- Real-time applications (chat, gaming)
- Microservices
- Streaming applications
- I/O-heavy applications
- Single Page Applications (SPA) backends

**❌ Not ideal for:**
- CPU-intensive tasks (video encoding, image processing)
- Heavy computations
- Blocking operations

**Interview Tip:**
> "Node.js is JavaScript runtime for server-side. Uses V8 engine, event-driven, non-blocking I/O. Single-threaded but handles concurrency via event loop. Best for I/O-heavy apps, not CPU-intensive tasks."

---

## Node.js Architecture

### 🎯 How Node.js Works

**Components:**

```
┌─────────────────────────────────┐
│      JavaScript Code            │
├─────────────────────────────────┤
│      Node.js APIs               │
├─────────────────────────────────┤
│      V8 Engine                  │
├─────────────────────────────────┤
│      libuv (Event Loop)         │
└─────────────────────────────────┘
```

**Key Components:**
1. **V8 Engine** - Executes JavaScript
2. **libuv** - Handles async I/O, event loop
3. **Node.js APIs** - Built-in modules (fs, http, etc.)
4. **Event Loop** - Manages async operations

---

### Event Loop in Node.js

**Phases:**

```
   ┌───────────────────────────┐
┌─>│        timers             │ - setTimeout, setInterval
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │    pending callbacks      │ - I/O callbacks
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │       idle, prepare       │ - Internal use
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │         poll              │ - Retrieve new I/O events
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │         check             │ - setImmediate callbacks
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │    close callbacks        │ - socket.on('close')
│  └─────────────┬─────────────┘
└──────────────────────────────┘
```

**Important:**
- `process.nextTick()` - Executes before any phase
- Microtasks (Promises) - Execute after each phase

**Interview Tip:**
> "Node.js event loop has phases: timers → I/O callbacks → poll → check → close. process.nextTick() executes before any phase. Microtasks (Promises) execute after each phase."

---

## Modules System

### 🎯 CommonJS Modules

**Definition:**
> CommonJS is Node.js's default module system using require() and module.exports.

**Exporting:**

```javascript
// math.js

// Method 1: module.exports (single export)
module.exports = {
    add: (a, b) => a + b,
    subtract: (a, b) => a - b
};

// Method 2: exports (multiple exports)
exports.PI = 3.14159;
exports.multiply = (a, b) => a * b;

// Method 3: Individual exports
module.exports.divide = (a, b) => a / b;
```

**Importing:**

```javascript
// Import entire module
const math = require('./math');
console.log(math.add(5, 3));

// Destructure imports
const { add, subtract } = require('./math');
console.log(add(5, 3));
```

---

### ES6 Modules in Node.js

**Enable ES6 modules:**
- Add `"type": "module"` in package.json
- Or use `.mjs` file extension

```javascript
// math.mjs
export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;

// Import
import { add, subtract } from './math.mjs';
```

---

### Built-in Modules

**Core modules (no installation needed):**

```javascript
const fs = require('fs');           // File system
const path = require('path');       // Path utilities
const http = require('http');       // HTTP server
const https = require('https');     // HTTPS server
const url = require('url');         // URL parsing
const querystring = require('querystring');  // Query string parsing
const crypto = require('crypto');   // Cryptography
const os = require('os');           // Operating system info
const events = require('events');   // Event emitter
const stream = require('stream');   // Stream operations
const util = require('util');       // Utility functions
```

**Interview Tip:**
> "Node.js uses CommonJS by default (require/module.exports). Can use ES6 modules with 'type: module' in package.json. Core modules are built-in, third-party modules installed via npm."

---

## NPM & Package Management

### 🎯 NPM Basics

**Definition:**
> NPM (Node Package Manager) is the default package manager for Node.js.

**Essential Commands:**

```bash
# Initialize project
npm init
npm init -y  # Skip questions

# Install packages
npm install express           # Save to dependencies
npm install -D nodemon        # Save to devDependencies
npm install -g typescript     # Install globally

# Install from package.json
npm install

# Update packages
npm update
npm update express

# Remove packages
npm uninstall express

# List installed packages
npm list
npm list --depth=0  # Top-level only

# Run scripts
npm run dev
npm start
npm test
```

---

### package.json

```json
{
  "name": "my-app",
  "version": "1.0.0",
  "description": "My Node.js app",
  "main": "index.js",
  "scripts": {
    "start": "node index.js",
    "dev": "nodemon index.js",
    "test": "jest"
  },
  "dependencies": {
    "express": "^4.18.0"
  },
  "devDependencies": {
    "nodemon": "^2.0.0"
  }
}
```

**Versioning (Semantic Versioning):**
- `^4.18.0` - Compatible with 4.x.x (minor and patch updates)
- `~4.18.0` - Compatible with 4.18.x (patch updates only)
- `4.18.0` - Exact version

---

## File System (fs)

### 🎯 Reading and Writing Files

**Synchronous (Blocking):**

```javascript
const fs = require('fs');

// Read file
const data = fs.readFileSync('file.txt', 'utf8');
console.log(data);

// Write file
fs.writeFileSync('output.txt', 'Hello World');

// Append to file
fs.appendFileSync('output.txt', '\nNew line');
```

**Asynchronous (Non-blocking - Preferred):**

```javascript
// Callback style
fs.readFile('file.txt', 'utf8', (err, data) => {
    if (err) {
        console.error('Error:', err);
        return;
    }
    console.log(data);
});

// Promise style (fs.promises)
const fs = require('fs').promises;

async function readFile() {
    try {
        const data = await fs.readFile('file.txt', 'utf8');
        console.log(data);
    } catch (error) {
        console.error('Error:', error);
    }
}
```

---

### File Operations

```javascript
const fs = require('fs').promises;

// Check if file exists
const exists = await fs.access('file.txt')
    .then(() => true)
    .catch(() => false);

// Delete file
await fs.unlink('file.txt');

// Rename/move file
await fs.rename('old.txt', 'new.txt');

// Get file stats
const stats = await fs.stat('file.txt');
console.log(stats.size);  // File size in bytes
console.log(stats.isFile());
console.log(stats.isDirectory());

// Create directory
await fs.mkdir('newDir', { recursive: true });

// Read directory
const files = await fs.readdir('.');
console.log(files);

// Remove directory
await fs.rmdir('newDir');
```

**Real-life analogy:**
Async file operations are like ordering food delivery - you place order (start read), do other things, get notified when ready (callback).

**Interview Tip:**
> "Always use async file operations (fs.promises or callbacks) to avoid blocking. Sync methods block event loop. Use fs.readFile for reading, fs.writeFile for writing, fs.promises for async/await syntax."

---

## Path Module

### 🎯 Path Utilities

```javascript
const path = require('path');

// Join paths
const filePath = path.join(__dirname, 'files', 'data.txt');
// /Users/project/files/data.txt

// Resolve absolute path
const absolute = path.resolve('files', 'data.txt');

// Get file extension
const ext = path.extname('file.txt');  // .txt

// Get filename
const filename = path.basename('/path/to/file.txt');  // file.txt

// Get directory name
const dirname = path.dirname('/path/to/file.txt');  // /path/to

// Parse path
const parsed = path.parse('/path/to/file.txt');
// {
//   root: '/',
//   dir: '/path/to',
//   base: 'file.txt',
//   ext: '.txt',
//   name: 'file'
// }

// Important globals
console.log(__dirname);   // Current directory
console.log(__filename);  // Current file path
console.log(process.cwd());  // Current working directory
```

---

## HTTP Module

### 🎯 Creating HTTP Server

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
    // Request object
    console.log(req.method);   // GET, POST, etc.
    console.log(req.url);      // /api/users
    console.log(req.headers);  // Request headers
    
    // Response
    res.statusCode = 200;
    res.setHeader('Content-Type', 'application/json');
    res.end(JSON.stringify({ message: 'Hello World' }));
});

const PORT = 3000;
server.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

---

### Handling Different Routes

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
    if (req.url === '/' && req.method === 'GET') {
        res.writeHead(200, { 'Content-Type': 'text/html' });
        res.end('<h1>Home Page</h1>');
    } 
    else if (req.url === '/api/users' && req.method === 'GET') {
        res.writeHead(200, { 'Content-Type': 'application/json' });
        res.end(JSON.stringify({ users: ['John', 'Jane'] }));
    }
    else if (req.url === '/api/users' && req.method === 'POST') {
        let body = '';
        
        req.on('data', chunk => {
            body += chunk.toString();
        });
        
        req.on('end', () => {
            const user = JSON.parse(body);
            res.writeHead(201, { 'Content-Type': 'application/json' });
            res.end(JSON.stringify({ message: 'User created', user }));
        });
    }
    else {
        res.writeHead(404, { 'Content-Type': 'text/plain' });
        res.end('Not Found');
    }
});

server.listen(3000);
```

**Interview Tip:**
> "http.createServer() creates server. Request object has method, url, headers. Response object has writeHead, write, end methods. For production, use Express instead of raw http module."

---

## Events Module

### 🎯 EventEmitter

**Definition:**
> EventEmitter is Node.js's implementation of the observer pattern for handling events.

```javascript
const EventEmitter = require('events');

class MyEmitter extends EventEmitter {}

const myEmitter = new MyEmitter();

// Register listener
myEmitter.on('event', (arg) => {
    console.log('Event occurred:', arg);
});

// Emit event
myEmitter.emit('event', 'Hello World');

// One-time listener
myEmitter.once('login', (user) => {
    console.log('User logged in:', user);
});

myEmitter.emit('login', 'John');  // Executes
myEmitter.emit('login', 'Jane');  // Ignored (once only)

// Remove listener
function handler(data) {
    console.log(data);
}
myEmitter.on('data', handler);
myEmitter.off('data', handler);  // Remove
```

---

### Custom EventEmitter

```javascript
const EventEmitter = require('events');

class Logger extends EventEmitter {
    log(message) {
        console.log(message);
        this.emit('logged', { message, timestamp: new Date() });
    }
}

const logger = new Logger();

logger.on('logged', (data) => {
    console.log('Log event:', data);
});

logger.log('User logged in');
```

**Real-life analogy:**
EventEmitter is like a notification system - subscribe to events (on), publish events (emit), get notified when events occur.

---

## Stream Module

### 🎯 Understanding Streams

**Definition:**
> Streams are objects that let you read/write data piece by piece instead of all at once.

**Simple meaning:**
Process data in chunks instead of loading everything into memory.

**Types of Streams:**
1. **Readable** - Read data (fs.createReadStream)
2. **Writable** - Write data (fs.createWriteStream)
3. **Duplex** - Both read and write (TCP socket)
4. **Transform** - Modify data while reading/writing (compression)

---

### Readable Stream

```javascript
const fs = require('fs');

// Read large file in chunks
const readStream = fs.createReadStream('large-file.txt', {
    encoding: 'utf8',
    highWaterMark: 64 * 1024  // 64KB chunks
});

readStream.on('data', (chunk) => {
    console.log('Received chunk:', chunk.length, 'bytes');
});

readStream.on('end', () => {
    console.log('Finished reading');
});

readStream.on('error', (error) => {
    console.error('Error:', error);
});
```

---

### Writable Stream

```javascript
const fs = require('fs');

const writeStream = fs.createWriteStream('output.txt');

writeStream.write('Line 1\n');
writeStream.write('Line 2\n');
writeStream.end('Final line\n');

writeStream.on('finish', () => {
    console.log('Finished writing');
});
```

---

### Piping Streams

```javascript
const fs = require('fs');

// Copy file using streams (memory efficient)
const readStream = fs.createReadStream('input.txt');
const writeStream = fs.createWriteStream('output.txt');

readStream.pipe(writeStream);

// Chain multiple streams
const zlib = require('zlib');
const gzip = zlib.createGzip();

fs.createReadStream('input.txt')
  .pipe(gzip)
  .pipe(fs.createWriteStream('input.txt.gz'));
```

**Real-life analogy:**
Streams are like a water pipe - water flows continuously in small amounts instead of filling a giant bucket first.

**Interview Tip:**
> "Streams process data in chunks, memory efficient for large files. Four types: Readable, Writable, Duplex, Transform. Use pipe() to connect streams. Example: read large file → compress → write to disk."

---

## Buffer

### 🎯 Working with Binary Data

**Definition:**
> Buffer is a temporary storage for binary data (raw bytes).

```javascript
// Create buffer
const buf1 = Buffer.from('Hello');
const buf2 = Buffer.alloc(10);  // 10 bytes, filled with 0
const buf3 = Buffer.allocUnsafe(10);  // Faster but may contain old data

// Convert to string
console.log(buf1.toString());  // 'Hello'
console.log(buf1.toString('hex'));  // Hex representation

// Write to buffer
buf2.write('Hi');

// Read from buffer
console.log(buf2.toString());  // 'Hi'

// Buffer operations
const buf4 = Buffer.concat([buf1, buf2]);
console.log(buf4.toString());  // 'HelloHi'
```

**Interview Tip:**
> "Buffer handles binary data in Node.js. Used for file I/O, network operations. Buffer.from() creates from string, Buffer.alloc() creates empty buffer. Converts to string with toString()."

---

# Express.js Framework

## Express Basics

### 🎯 What is Express?

**Definition:**
> Express is a minimal and flexible Node.js web application framework that provides robust features for web and mobile applications.

**Simple meaning:**
Express makes building web servers easier with routing, middleware, and utilities.

**Installation:**

```bash
npm install express
```

**Basic Server:**

```javascript
const express = require('express');
const app = express();

// Middleware to parse JSON
app.use(express.json());

// Simple route
app.get('/', (req, res) => {
    res.send('Hello World!');
});

// Start server
const PORT = 3000;
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

**Real-life analogy:**
Express is like a restaurant manager - handles incoming requests (customers), routes them to appropriate handlers (chefs), and sends responses (food).

---

## Routing

### 🎯 Route Methods

```javascript
const express = require('express');
const app = express();

// GET request
app.get('/api/users', (req, res) => {
    res.json({ users: ['John', 'Jane'] });
});

// POST request
app.post('/api/users', (req, res) => {
    const user = req.body;
    res.status(201).json({ message: 'User created', user });
});

// PUT request (update)
app.put('/api/users/:id', (req, res) => {
    const { id } = req.params;
    const updates = req.body;
    res.json({ message: `User ${id} updated`, updates });
});

// DELETE request
app.delete('/api/users/:id', (req, res) => {
    const { id } = req.params;
    res.json({ message: `User ${id} deleted` });
});

// Route parameters
app.get('/api/users/:id', (req, res) => {
    const { id } = req.params;
    res.json({ userId: id });
});

// Query parameters
app.get('/api/search', (req, res) => {
    const { q, limit } = req.query;  // /api/search?q=john&limit=10
    res.json({ query: q, limit });
});
```

---

### Router

```javascript
// users.routes.js
const express = require('express');
const router = express.Router();

router.get('/', (req, res) => {
    res.json({ users: [] });
});

router.post('/', (req, res) => {
    res.json({ message: 'User created' });
});

router.get('/:id', (req, res) => {
    res.json({ userId: req.params.id });
});

module.exports = router;

// app.js
const userRoutes = require('./users.routes');
app.use('/api/users', userRoutes);
```

---

## Middleware

### 🎯 What is Middleware?

**Definition:**
> Middleware functions have access to request, response, and next function in the request-response cycle.

**Simple meaning:**
Functions that execute between receiving request and sending response.

**Middleware Flow:**

```
Request → Middleware 1 → Middleware 2 → Route Handler → Response
```

---

### Types of Middleware

**1. Application-level middleware:**

```javascript
// Executed for every request
app.use((req, res, next) => {
    console.log(`${req.method} ${req.url}`);
    next();  // Pass to next middleware
});

// Executed for specific path
app.use('/api', (req, res, next) => {
    console.log('API request');
    next();
});
```

**2. Built-in middleware:**

```javascript
// Parse JSON bodies
app.use(express.json());

// Parse URL-encoded bodies
app.use(express.urlencoded({ extended: true }));

// Serve static files
app.use(express.static('public'));
```

**3. Third-party middleware:**

```javascript
const cors = require('cors');
const morgan = require('morgan');

// Enable CORS
app.use(cors());

// HTTP request logger
app.use(morgan('dev'));
```

**4. Route-level middleware:**

```javascript
// Middleware for specific route
const authMiddleware = (req, res, next) => {
    const token = req.headers.authorization;
    if (!token) {
        return res.status(401).json({ error: 'Unauthorized' });
    }
    // Verify token
    next();
};

app.get('/api/protected', authMiddleware, (req, res) => {
    res.json({ message: 'Protected data' });
});
```

**5. Error-handling middleware:**

```javascript
// Must have 4 parameters
app.use((err, req, res, next) => {
    console.error(err.stack);
    res.status(500).json({ error: 'Something went wrong!' });
});
```

**Interview Tip:**
> "Middleware functions execute in order between request and response. Have access to req, res, next. Call next() to pass control. Use for logging, authentication, parsing, error handling."

---

## Error Handling in Express

### 🎯 Error Handling Patterns

**Synchronous errors:**

```javascript
app.get('/api/users/:id', (req, res) => {
    const { id } = req.params;
    
    if (!id) {
        return res.status(400).json({ error: 'ID required' });
    }
    
    // Process request
    res.json({ userId: id });
});
```

**Asynchronous errors:**

```javascript
// Wrap async routes
const asyncHandler = (fn) => (req, res, next) => {
    Promise.resolve(fn(req, res, next)).catch(next);
};

app.get('/api/users', asyncHandler(async (req, res) => {
    const users = await User.find();  // May throw error
    res.json(users);
}));

// Or use try-catch
app.get('/api/users', async (req, res, next) => {
    try {
        const users = await User.find();
        res.json(users);
    } catch (error) {
        next(error);  // Pass to error handler
    }
});
```

**Global error handler:**

```javascript
// Must be last middleware
app.use((err, req, res, next) => {
    console.error(err.stack);
    
    res.status(err.statusCode || 500).json({
        error: err.message || 'Internal Server Error',
        ...(process.env.NODE_ENV === 'development' && { stack: err.stack })
    });
});
```

---

## REST API Development

### 🎯 Complete REST API Example

```javascript
const express = require('express');
const app = express();

app.use(express.json());

// In-memory database (for demo)
let users = [
    { id: 1, name: 'John', email: 'john@example.com' },
    { id: 2, name: 'Jane', email: 'jane@example.com' }
];

// GET all users
app.get('/api/users', (req, res) => {
    res.json(users);
});

// GET user by ID
app.get('/api/users/:id', (req, res) => {
    const user = users.find(u => u.id === parseInt(req.params.id));
    
    if (!user) {
        return res.status(404).json({ error: 'User not found' });
    }
    
    res.json(user);
});

// CREATE user
app.post('/api/users', (req, res) => {
    const { name, email } = req.body;
    
    if (!name || !email) {
        return res.status(400).json({ error: 'Name and email required' });
    }
    
    const newUser = {
        id: users.length + 1,
        name,
        email
    };
    
    users.push(newUser);
    res.status(201).json(newUser);
});

// UPDATE user
app.put('/api/users/:id', (req, res) => {
    const user = users.find(u => u.id === parseInt(req.params.id));
    
    if (!user) {
        return res.status(404).json({ error: 'User not found' });
    }
    
    user.name = req.body.name || user.name;
    user.email = req.body.email || user.email;
    
    res.json(user);
});

// DELETE user
app.delete('/api/users/:id', (req, res) => {
    const index = users.findIndex(u => u.id === parseInt(req.params.id));
    
    if (index === -1) {
        return res.status(404).json({ error: 'User not found' });
    }
    
    users.splice(index, 1);
    res.status(204).send();
});

app.listen(3000);
```

---

## MongoDB with Mongoose

### 🎯 Mongoose Basics

**Installation:**

```bash
npm install mongoose
```

**Connect to MongoDB:**

```javascript
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost:27017/myapp', {
    useNewUrlParser: true,
    useUnifiedTopology: true
})
.then(() => console.log('MongoDB connected'))
.catch(err => console.error('Connection error:', err));
```

---

### Schema and Model

```javascript
const mongoose = require('mongoose');

// Define schema
const userSchema = new mongoose.Schema({
    name: {
        type: String,
        required: true,
        trim: true
    },
    email: {
        type: String,
        required: true,
        unique: true,
        lowercase: true
    },
    age: {
        type: Number,
        min: 0,
        max: 150
    },
    createdAt: {
        type: Date,
        default: Date.now
    }
});

// Create model
const User = mongoose.model('User', userSchema);

// CRUD operations
async function examples() {
    // Create
    const user = new User({
        name: 'John Doe',
        email: 'john@example.com',
        age: 30
    });
    await user.save();
    
    // Or
    const user2 = await User.create({
        name: 'Jane',
        email: 'jane@example.com'
    });
    
    // Read
    const users = await User.find();
    const john = await User.findOne({ name: 'John Doe' });
    const userById = await User.findById('507f1f77bcf86cd799439011');
    
    // Update
    await User.updateOne({ name: 'John Doe' }, { age: 31 });
    await User.findByIdAndUpdate(id, { age: 31 }, { new: true });
    
    // Delete
    await User.deleteOne({ name: 'John Doe' });
    await User.findByIdAndDelete(id);
}
```

**Interview Tip:**
> "Mongoose is MongoDB ODM for Node.js. Define schema with types and validation, create model from schema. Provides methods: save, find, findOne, updateOne, deleteOne. Returns Promises for async operations."

---

## JWT Authentication

### 🎯 Implementing JWT Auth

**Installation:**

```bash
npm install jsonwebtoken bcryptjs
```

**Implementation:**

```javascript
const jwt = require('jsonwebtoken');
const bcrypt = require('bcryptjs');

const JWT_SECRET = 'your-secret-key';

// Register user
app.post('/api/register', async (req, res) => {
    const { email, password } = req.body;
    
    // Hash password
    const hashedPassword = await bcrypt.hash(password, 10);
    
    // Save user (pseudo-code)
    const user = await User.create({ email, password: hashedPassword });
    
    res.status(201).json({ message: 'User created' });
});

// Login
app.post('/api/login', async (req, res) => {
    const { email, password } = req.body;
    
    // Find user
    const user = await User.findOne({ email });
    if (!user) {
        return res.status(401).json({ error: 'Invalid credentials' });
    }
    
    // Verify password
    const isValid = await bcrypt.compare(password, user.password);
    if (!isValid) {
        return res.status(401).json({ error: 'Invalid credentials' });
    }
    
    // Generate JWT
    const token = jwt.sign(
        { userId: user._id, email: user.email },
        JWT_SECRET,
        { expiresIn: '24h' }
    );
    
    res.json({ token });
});

// Auth middleware
const authMiddleware = (req, res, next) => {
    const token = req.headers.authorization?.split(' ')[1];  // Bearer TOKEN
    
    if (!token) {
        return res.status(401).json({ error: 'No token provided' });
    }
    
    try {
        const decoded = jwt.verify(token, JWT_SECRET);
        req.user = decoded;  // Attach user to request
        next();
    } catch (error) {
        res.status(401).json({ error: 'Invalid token' });
    }
};

// Protected route
app.get('/api/profile', authMiddleware, (req, res) => {
    res.json({ user: req.user });
});
```

**Interview Tip:**
> "JWT authentication: hash password with bcrypt, generate JWT token on login, send token to client. Client includes token in Authorization header. Middleware verifies token and attaches user to request."

---

## Password Hashing

### 🎯 bcrypt

```javascript
const bcrypt = require('bcryptjs');

// Hash password
async function hashPassword(password) {
    const salt = await bcrypt.genSalt(10);  // Generate salt
    const hashed = await bcrypt.hash(password, salt);
    return hashed;
}

// Or simplified
const hashed = await bcrypt.hash(password, 10);

// Verify password
async function verifyPassword(password, hashedPassword) {
    const isMatch = await bcrypt.compare(password, hashedPassword);
    return isMatch;
}
```

**Why bcrypt?**
- ✅ Slow by design (prevents brute force)
- ✅ Includes salt automatically
- ✅ Adaptive (can increase rounds as computers get faster)

---

## Process & Child Processes

### 🎯 Process Object

```javascript
// Environment variables
console.log(process.env.NODE_ENV);
console.log(process.env.PORT);

// Command-line arguments
console.log(process.argv);  // Array of arguments

// Current working directory
console.log(process.cwd());

// Exit process
process.exit(0);  // Success
process.exit(1);  // Error

// Handle uncaught exceptions
process.on('uncaughtException', (error) => {
    console.error('Uncaught Exception:', error);
    process.exit(1);
});

// Handle unhandled promise rejections
process.on('unhandledRejection', (reason, promise) => {
    console.error('Unhandled Rejection:', reason);
    process.exit(1);
});
```

---

### Child Processes

```javascript
const { exec, spawn, fork } = require('child_process');

// exec - run shell command
exec('ls -la', (error, stdout, stderr) => {
    if (error) {
        console.error('Error:', error);
        return;
    }
    console.log(stdout);
});

// spawn - stream output
const ls = spawn('ls', ['-la']);

ls.stdout.on('data', (data) => {
    console.log(`Output: ${data}`);
});

ls.on('close', (code) => {
    console.log(`Process exited with code ${code}`);
});

// fork - run Node.js script
const child = fork('worker.js');

child.send({ task: 'process data' });

child.on('message', (result) => {
    console.log('Result from child:', result);
});
```

---

## Cluster Module

### 🎯 Scaling Node.js

**Definition:**
> Cluster module allows creating child processes (workers) that share the same server port.

**Simple meaning:**
Run multiple Node.js processes to utilize all CPU cores.

```javascript
const cluster = require('cluster');
const http = require('http');
const os = require('os');

if (cluster.isMaster) {
    const numCPUs = os.cpus().length;
    console.log(`Master process ${process.pid} is running`);
    console.log(`Forking ${numCPUs} workers...`);
    
    // Fork workers
    for (let i = 0; i < numCPUs; i++) {
        cluster.fork();
    }
    
    cluster.on('exit', (worker, code, signal) => {
        console.log(`Worker ${worker.process.pid} died`);
        cluster.fork();  // Restart worker
    });
} else {
    // Workers share TCP connection
    const server = http.createServer((req, res) => {
        res.writeHead(200);
        res.end(`Worker ${process.pid} handled request\n`);
    });
    
    server.listen(3000);
    console.log(`Worker ${process.pid} started`);
}
```

**Real-life analogy:**
Cluster is like a restaurant with multiple chefs (workers) sharing the same order queue (port) - utilizes all available staff.

**Interview Tip:**
> "Cluster module creates worker processes to utilize all CPU cores. Master process forks workers, workers share server port. Use for CPU-bound tasks or to handle more concurrent requests."

---

## Worker Threads

### 🎯 True Parallelism

**Definition:**
> Worker threads enable parallel execution of JavaScript code using multiple threads.

```javascript
const { Worker } = require('worker_threads');

// Main thread
function runWorker(data) {
    return new Promise((resolve, reject) => {
        const worker = new Worker('./worker.js', {
            workerData: data
        });
        
        worker.on('message', resolve);
        worker.on('error', reject);
        worker.on('exit', (code) => {
            if (code !== 0) {
                reject(new Error(`Worker stopped with code ${code}`));
            }
        });
    });
}

// Usage
runWorker({ task: 'heavy computation' })
    .then(result => console.log('Result:', result))
    .catch(err => console.error('Error:', err));

// worker.js
const { parentPort, workerData } = require('worker_threads');

// Heavy computation
const result = heavyComputation(workerData);

parentPort.postMessage(result);
```

**Cluster vs Worker Threads:**

| Feature | Cluster | Worker Threads |
|---------|---------|----------------|
| **Purpose** | Multiple processes | Multiple threads |
| **Memory** | Separate memory | Shared memory |
| **Communication** | IPC (slow) | Shared memory (fast) |
| **Use case** | Scale across CPUs | CPU-intensive tasks |

---

## Performance Optimization

### 🎯 Best Practices

**1. Use compression:**

```javascript
const compression = require('compression');
app.use(compression());  // Gzip responses
```

**2. Enable caching:**

```javascript
app.get('/api/data', (req, res) => {
    res.set('Cache-Control', 'public, max-age=300');  // 5 minutes
    res.json(data);
});
```

**3. Use connection pooling:**

```javascript
// MongoDB
mongoose.connect(uri, {
    maxPoolSize: 10  // Connection pool
});
```

**4. Implement rate limiting:**

```javascript
const rateLimit = require('express-rate-limit');

const limiter = rateLimit({
    windowMs: 15 * 60 * 1000,  // 15 minutes
    max: 100  // Limit each IP to 100 requests per windowMs
});

app.use('/api/', limiter);
```

**5. Use PM2 for production:**

```bash
npm install -g pm2
pm2 start app.js -i max  # Use all CPUs
pm2 monit  # Monitor
pm2 logs   # View logs
```

---

## Environment Variables

### 🎯 Using dotenv

**Installation:**

```bash
npm install dotenv
```

**.env file:**

```
NODE_ENV=development
PORT=3000
DB_URI=mongodb://localhost:27017/myapp
JWT_SECRET=your-secret-key
```

**Usage:**

```javascript
require('dotenv').config();

const PORT = process.env.PORT || 3000;
const DB_URI = process.env.DB_URI;
const JWT_SECRET = process.env.JWT_SECRET;

console.log('Running in:', process.env.NODE_ENV);
```

**Best practices:**
- ✅ Never commit .env to git (add to .gitignore)
- ✅ Use .env.example for documentation
- ✅ Different .env files for dev/prod
- ✅ Validate required variables on startup

---

## Testing with Jest

### 🎯 Unit Testing

**Installation:**

```bash
npm install -D jest supertest
```

**Testing functions:**

```javascript
// math.js
function add(a, b) {
    return a + b;
}
module.exports = { add };

// math.test.js
const { add } = require('./math');

describe('Math functions', () => {
    test('add should return sum of two numbers', () => {
        expect(add(2, 3)).toBe(5);
        expect(add(-1, 1)).toBe(0);
    });
});
```

**Testing Express routes:**

```javascript
const request = require('supertest');
const app = require('./app');

describe('GET /api/users', () => {
    test('should return array of users', async () => {
        const response = await request(app)
            .get('/api/users')
            .expect(200)
            .expect('Content-Type', /json/);
        
        expect(Array.isArray(response.body)).toBe(true);
    });
});

describe('POST /api/users', () => {
    test('should create new user', async () => {
        const newUser = { name: 'John', email: 'john@example.com' };
        
        const response = await request(app)
            .post('/api/users')
            .send(newUser)
            .expect(201);
        
        expect(response.body).toHaveProperty('id');
        expect(response.body.name).toBe('John');
    });
});
```

---

# Interview Preparation

## Common Interview Questions

### Node.js Basics

**1. What is Node.js?**
> "Node.js is JavaScript runtime built on V8 engine for server-side. Event-driven, non-blocking I/O, single-threaded with event loop. Best for I/O-heavy apps like APIs, real-time applications."

**2. How does Node.js handle concurrency?**
> "Node.js is single-threaded but handles concurrency via event loop and non-blocking I/O. When I/O operation starts, Node continues executing other code. Callbacks execute when I/O completes."

**3. What is event loop in Node.js?**
> "Event loop has phases: timers → I/O callbacks → poll → check → close callbacks. process.nextTick() runs before any phase. Microtasks run after each phase. Handles async operations in single thread."

**4. Difference between process.nextTick() and setImmediate()?**
> "process.nextTick() executes before event loop continues (highest priority). setImmediate() executes in check phase. nextTick can starve I/O, use setImmediate for deferring execution."

**5. What is the difference between Node.js and browser JavaScript?**
> "Node.js runs on server with access to file system, no DOM. Uses 'global' instead of 'window'. Has built-in modules (fs, http). Browser has DOM APIs, limited file access."

---

### Modules & NPM

**6. Explain require() vs import.**
> "require() is CommonJS (Node.js default), synchronous, dynamic. import is ES6 modules, asynchronous, static. Use require for CommonJS, import with 'type: module' in package.json."

**7. What is package.json?**
> "package.json contains project metadata, dependencies, scripts. dependencies for production, devDependencies for development. Scripts define custom commands (npm start, npm test)."

**8. What is the difference between dependencies and devDependencies?**
> "dependencies are required in production (express, mongoose). devDependencies only for development (nodemon, jest). Use -D flag for devDependencies: npm install -D jest."

---

### Express & APIs

**9. What is middleware in Express?**
> "Middleware functions execute between request and response. Have access to req, res, next. Used for logging, authentication, parsing, error handling. Call next() to pass control to next middleware."

**10. How to handle errors in Express?**
> "Use try-catch in async routes, pass errors to next(error). Create error-handling middleware with 4 parameters (err, req, res, next). Place at end of middleware stack."

**11. What is REST API?**
> "REST uses HTTP methods (GET, POST, PUT, DELETE) for CRUD operations. Stateless, resource-based URLs. GET /users (read), POST /users (create), PUT /users/:id (update), DELETE /users/:id (delete)."

---

### Async & Performance

**12. What are streams in Node.js?**
> "Streams process data in chunks instead of loading all into memory. Four types: Readable, Writable, Duplex, Transform. Use for large files. pipe() connects streams. Memory efficient."

**13. What is Buffer?**
> "Buffer handles binary data in Node.js. Used for file I/O, network operations. Buffer.from() creates from string, Buffer.alloc() creates empty. Converts to string with toString()."

**14. How to scale Node.js application?**
> "Use Cluster module to fork workers for all CPU cores. Use Worker Threads for CPU-intensive tasks. Use load balancer (Nginx) for multiple servers. Implement caching (Redis)."

**15. How to prevent memory leaks in Node.js?**
> "Clear timers/intervals, remove event listeners, close database connections, avoid global variables, use WeakMap for caches, monitor with --inspect flag or tools like clinic.js."

---

### Security

**16. How to secure Node.js application?**
> "Use helmet for security headers, validate input, sanitize data, use HTTPS, implement rate limiting, hash passwords (bcrypt), use JWT for auth, keep dependencies updated, use environment variables for secrets."

**17. What is CORS and how to handle it?**
> "CORS prevents requests from different origins. Use cors middleware in Express. Configure allowed origins, methods, headers. For APIs, enable CORS for specific domains or all (*)."

---

## Coding Challenges

### 1. Implement simple HTTP server

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
    if (req.url === '/') {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Home Page');
    } else if (req.url === '/api/data') {
        res.writeHead(200, { 'Content-Type': 'application/json' });
        res.end(JSON.stringify({ message: 'API Data' }));
    } else {
        res.writeHead(404);
        res.end('Not Found');
    }
});

server.listen(3000, () => console.log('Server running on port 3000'));
```

---

### 2. Read file line by line

```javascript
const fs = require('fs');
const readline = require('readline');

async function readFileLineByLine(filename) {
    const fileStream = fs.createReadStream(filename);
    
    const rl = readline.createInterface({
        input: fileStream,
        crlfDelay: Infinity
    });
    
    for await (const line of rl) {
        console.log('Line:', line);
    }
}
```

---

### 3. Implement rate limiter

```javascript
class RateLimiter {
    constructor(maxRequests, windowMs) {
        this.maxRequests = maxRequests;
        this.windowMs = windowMs;
        this.requests = new Map();
    }
    
    isAllowed(clientId) {
        const now = Date.now();
        const clientRequests = this.requests.get(clientId) || [];
        
        // Remove old requests outside window
        const validRequests = clientRequests.filter(
            time => now - time < this.windowMs
        );
        
        if (validRequests.length < this.maxRequests) {
            validRequests.push(now);
            this.requests.set(clientId, validRequests);
            return true;
        }
        
        return false;
    }
}

// Usage
const limiter = new RateLimiter(5, 60000);  // 5 requests per minute

app.use((req, res, next) => {
    const clientId = req.ip;
    
    if (limiter.isAllowed(clientId)) {
        next();
    } else {
        res.status(429).json({ error: 'Too many requests' });
    }
});
```

---

### 4. File upload handler

```javascript
const express = require('express');
const multer = require('multer');
const path = require('path');

// Configure storage
const storage = multer.diskStorage({
    destination: (req, file, cb) => {
        cb(null, 'uploads/');
    },
    filename: (req, file, cb) => {
        const uniqueName = Date.now() + '-' + file.originalname;
        cb(null, uniqueName);
    }
});

// File filter
const fileFilter = (req, file, cb) => {
    const allowedTypes = ['image/jpeg', 'image/png', 'image/gif'];
    
    if (allowedTypes.includes(file.mimetype)) {
        cb(null, true);
    } else {
        cb(new Error('Invalid file type'), false);
    }
};

const upload = multer({ 
    storage, 
    fileFilter,
    limits: { fileSize: 5 * 1024 * 1024 }  // 5MB
});

// Single file upload
app.post('/api/upload', upload.single('avatar'), (req, res) => {
    res.json({ 
        message: 'File uploaded', 
        file: req.file 
    });
});

// Multiple files
app.post('/api/upload-multiple', upload.array('photos', 5), (req, res) => {
    res.json({ 
        message: 'Files uploaded', 
        files: req.files 
    });
});
```

---

### 5. Simple caching with Redis

```javascript
const redis = require('redis');
const client = redis.createClient();

// Cache middleware
const cacheMiddleware = (duration) => async (req, res, next) => {
    const key = req.originalUrl;
    
    try {
        const cachedData = await client.get(key);
        
        if (cachedData) {
            return res.json(JSON.parse(cachedData));
        }
        
        // Store original res.json
        const originalJson = res.json.bind(res);
        
        // Override res.json to cache response
        res.json = (data) => {
            client.setEx(key, duration, JSON.stringify(data));
            originalJson(data);
        };
        
        next();
    } catch (error) {
        next();
    }
};

// Usage
app.get('/api/users', cacheMiddleware(300), async (req, res) => {
    const users = await User.find();
    res.json(users);
});
```

---

## 🎯 Quick Reference

### Node.js Cheat Sheet

| Concept | Key Points |
|---------|------------|
| **Runtime** | JavaScript on server, V8 engine, event-driven |
| **Modules** | CommonJS (require), ES6 (import with type: module) |
| **Core Modules** | fs, path, http, events, stream, buffer |
| **Express** | Web framework, routing, middleware |
| **Async** | Callbacks, Promises, async/await |
| **Streams** | Process data in chunks, memory efficient |
| **Authentication** | JWT + bcrypt for password hashing |
| **Scaling** | Cluster for multi-core, Worker Threads for CPU tasks |

---

## 🚀 Best Practices

### ✅ Do's:

- Use async file operations (never sync in production)
- Handle errors properly (try-catch, error middleware)
- Use environment variables for configuration
- Implement logging (winston, morgan)
- Use connection pooling for databases
- Implement rate limiting for APIs
- Use compression for responses
- Keep dependencies updated
- Use PM2 or similar for production
- Implement proper error handling

### ❌ Don'ts:

- Don't use sync methods in production
- Don't ignore error handling
- Don't commit secrets to git
- Don't run as root user
- Don't use outdated packages
- Don't block the event loop
- Don't use cluster for CPU-intensive tasks (use Worker Threads)
- Don't expose stack traces in production

---

## 📊 Architecture Patterns

### MVC Pattern in Node.js

```javascript
// models/User.js
const mongoose = require('mongoose');
const userSchema = new mongoose.Schema({
    name: String,
    email: String
});
module.exports = mongoose.model('User', userSchema);

// controllers/userController.js
const User = require('../models/User');

exports.getUsers = async (req, res) => {
    try {
        const users = await User.find();
        res.json(users);
    } catch (error) {
        res.status(500).json({ error: error.message });
    }
};

exports.createUser = async (req, res) => {
    try {
        const user = await User.create(req.body);
        res.status(201).json(user);
    } catch (error) {
        res.status(400).json({ error: error.message });
    }
};

// routes/userRoutes.js
const express = require('express');
const router = express.Router();
const userController = require('../controllers/userController');

router.get('/', userController.getUsers);
router.post('/', userController.createUser);

module.exports = router;

// app.js
const userRoutes = require('./routes/userRoutes');
app.use('/api/users', userRoutes);
```

---

## 🎓 Complete Project Structure

```
my-node-app/
├── src/
│   ├── config/
│   │   └── database.js
│   ├── controllers/
│   │   └── userController.js
│   ├── models/
│   │   └── User.js
│   ├── routes/
│   │   └── userRoutes.js
│   ├── middleware/
│   │   ├── auth.js
│   │   └── errorHandler.js
│   ├── utils/
│   │   └── helpers.js
│   └── app.js
├── tests/
│   └── user.test.js
├── .env
├── .gitignore
├── package.json
└── server.js
```

---

## 🎯 Key Takeaways

**Node.js Core:**
1. **Event-driven, non-blocking** - Handles concurrency efficiently
2. **Single-threaded** - One main thread with event loop
3. **Modules** - CommonJS (require) or ES6 (import)
4. **Core modules** - fs, path, http, events, stream
5. **Best for I/O** - Not for CPU-intensive tasks

**Express Framework:**
1. **Middleware** - Functions between request and response
2. **Routing** - Handle different endpoints
3. **Error handling** - Centralized error middleware
4. **REST APIs** - Standard CRUD operations
5. **Production-ready** - With proper structure and security

**Performance:**
1. **Async operations** - Never block event loop
2. **Streams** - For large files
3. **Cluster** - Utilize all CPU cores
4. **Caching** - Redis for frequently accessed data
5. **Monitoring** - PM2, logging, error tracking

**Security:**
1. **Authentication** - JWT + bcrypt
2. **Validation** - Validate all inputs
3. **Rate limiting** - Prevent abuse
4. **Environment variables** - Never hardcode secrets
5. **Security headers** - Use helmet middleware

**Remember:**
> "Node.js excels at I/O-heavy, event-driven applications. Master async patterns, understand event loop, use Express for production, implement proper error handling and security."

Good luck with your Node.js journey and interviews! 🚀
