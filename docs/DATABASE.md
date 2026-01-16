# Database Guide - SQL & NoSQL

## Table of Contents

### 📘 SQL (Relational Databases)
1. [SQL Basics](#1️⃣-sql)
2. [Joins](#🔹-2️⃣-joins)
3. [Aggregate Functions & Grouping](#🔹-3️⃣-aggregate-functions--grouping)
4. [Subqueries & CTEs](#🔹-4️⃣-subqueries--ctes)
5. [Indexes & Performance](#🔹-5️⃣-indexes--performance)
6. [Constraints & Keys](#🔹-6️⃣-constraints--keys)
7. [Transactions & ACID](#🔹-7️⃣-transactions--acid)
8. [Isolation Levels & Locking](#🔹-8️⃣-isolation-levels--locking)
9. [Functions & Stored Procedures](#🔹-9️⃣-functions--stored-procedures)
10. [SQL Scenario-Based Questions](#🔹-🔟-sql-scenario-based-questions)
11. [Normalization & Design](#🔹-1️⃣1️⃣-normalization--design)
12. [SQL vs NoSQL](#🔹-1️⃣2️⃣-sql-vs-nosql)

### 🍃 MongoDB (NoSQL Database)
1. [MongoDB Basics](#🔹-1️⃣-mongodb-basics)
2. [CRUD Operations](#🔹-2️⃣-crud-operations)
3. [Query Operators](#🔹-3️⃣-query-operators)
4. [Update Operators](#🔹-4️⃣-update-operators)
5. [Indexing](#🔹-5️⃣-indexing)
6. [Aggregation Framework](#🔹-6️⃣-aggregation-framework)
7. [Data Modeling](#🔹-7️⃣-data-modeling)
8. [Transactions](#🔹-8️⃣-transactions)
9. [Replication & Sharding](#🔹-9️⃣-replication--sharding)
10. [MongoDB Interview Questions](#🔹-🔟-mongodb-interview-questions)
11. [Best Practices](#🔹-1️⃣1️⃣-best-practices)

---

#1️⃣ SQL

### What is SQL?
- **Structured Query Language** - used to communicate with relational databases
- Allows you to CREATE, READ, UPDATE, DELETE data (CRUD operations)
- Standard language across databases (MySQL, PostgreSQL, Oracle, SQL Server)

### DDL, DML, DCL, TCL
- **DDL (Data Definition Language)**: `CREATE`, `ALTER`, `DROP` - defines database structure
- **DML (Data Manipulation Language)**: `SELECT`, `INSERT`, `UPDATE`, `DELETE` - manipulates data
- **DCL (Data Control Language)**: `GRANT`, `REVOKE` - controls access permissions
- **TCL (Transaction Control Language)**: `COMMIT`, `ROLLBACK`, `SAVEPOINT` - manages transactions

### DELETE vs TRUNCATE vs DROP
- **DELETE**: Removes specific rows, can use WHERE clause, can be rolled back, slower (logs each row)
  ```sql
  DELETE FROM employees WHERE salary < 30000;
  ```
- **TRUNCATE**: Removes all rows, faster, cannot be rolled back easily, resets auto-increment
  ```sql
  TRUNCATE TABLE employees;
  ```
- **DROP**: Deletes entire table structure and data permanently
  ```sql
  DROP TABLE employees;
  ```

### Primary Key
- Uniquely identifies each row in a table (no duplicates, cannot be NULL)
- Only ONE primary key per table (can be composite - multiple columns)
- Automatically creates a clustered index
  ```sql
  CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100)
  );
  ```

### Foreign Key
- Creates relationship between tables by referencing another table's primary key
- Enforces referential integrity (can't insert invalid references)
- Can be NULL (unless specified NOT NULL)
  ```sql
  CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    FOREIGN KEY (customer_id) REFERENCES customers(id)
  );
  ```

### Unique Constraint
- Ensures all values in column are different (like primary key but can be NULL)
- Can have multiple unique constraints per table
- Automatically creates a non-clustered index
  ```sql
  CREATE TABLE users (
    id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE
  );
  ```

### NOT NULL
- Ensures column must always have a value (cannot be empty)
- Different from empty string '' or 0
  ```sql
  CREATE TABLE products (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
  );
  ```

### Index
- Data structure that improves query performance (like book index)
- Speeds up SELECT but slows down INSERT/UPDATE/DELETE
- Use on columns frequently used in WHERE, JOIN, ORDER BY
  ```sql
  CREATE INDEX idx_salary ON employees(salary);
  ```

### Views
- Virtual table based on a SELECT query (doesn't store data)
- Simplifies complex queries and provides security (hide sensitive columns)
- Can be used like a regular table in queries
  ```sql
  CREATE VIEW high_earners AS
  SELECT name, salary FROM employees WHERE salary > 100000;
  ```

### Schema
- Logical container/namespace for database objects (tables, views, procedures)
- Organizes database into logical groups
- In MySQL: schema = database; In PostgreSQL/SQL Server: multiple schemas per database

### CHAR vs VARCHAR
- **CHAR(n)**: Fixed length, pads with spaces, faster for fixed-size data (e.g., country codes)
- **VARCHAR(n)**: Variable length, saves space, better for variable-size data (e.g., names)
- Example: CHAR(10) stores "Hi" as "Hi        " (8 spaces), VARCHAR(10) stores "Hi" as "Hi"

### NULL
- Represents unknown or missing value (NOT zero, NOT empty string)
- NULL comparisons use `IS NULL` or `IS NOT NULL` (not `= NULL`)
- NULL in arithmetic returns NULL (e.g., 5 + NULL = NULL)
  ```sql
  SELECT * FROM employees WHERE manager_id IS NULL;
  ```

---

## 🔹 2️⃣ JOINS

### What is a JOIN?
- Combines rows from two or more tables based on related column
- Essential for relational databases to retrieve data across tables
- Performance depends on indexes and join type

### INNER JOIN
- Returns only matching rows from both tables
- Most common join type
  ```sql
  SELECT e.name, d.department_name
  FROM employees e
  INNER JOIN departments d ON e.dept_id = d.id;
  ```

### LEFT JOIN (LEFT OUTER JOIN)
- Returns all rows from left table + matching rows from right table
- NULL for non-matching rows from right table
  ```sql
  SELECT e.name, d.department_name
  FROM employees e
  LEFT JOIN departments d ON e.dept_id = d.id;
  -- Shows all employees, even those without department
  ```

### RIGHT JOIN (RIGHT OUTER JOIN)
- Returns all rows from right table + matching rows from left table
- Less common (can be rewritten as LEFT JOIN)
  ```sql
  SELECT e.name, d.department_name
  FROM employees e
  RIGHT JOIN departments d ON e.dept_id = d.id;
  -- Shows all departments, even those without employees
  ```

### FULL OUTER JOIN
- Returns all rows from both tables (matching + non-matching)
- NULL where no match exists
- Not supported in MySQL (use UNION of LEFT and RIGHT JOIN)
  ```sql
  SELECT e.name, d.department_name
  FROM employees e
  FULL OUTER JOIN departments d ON e.dept_id = d.id;
  ```

### INNER JOIN vs LEFT JOIN
- **INNER JOIN**: Only matching records (intersection)
- **LEFT JOIN**: All from left + matches from right (includes unmatched left records)
- Use LEFT JOIN when you need all records from main table regardless of matches

### JOIN vs SUBQUERY
- **JOIN**: Generally faster, can return columns from both tables
- **SUBQUERY**: More readable for simple cases, used in WHERE/SELECT/FROM
- Use JOIN when you need data from multiple tables; subquery for filtering

### Self Join
- Table joins with itself (uses aliases to differentiate)
- Common use: hierarchical data (employees and their managers)
  ```sql
  SELECT e.name AS employee, m.name AS manager
  FROM employees e
  LEFT JOIN employees m ON e.manager_id = m.id;
  ```

### Cross Join
- Cartesian product (every row from table1 × every row from table2)
- Rarely used intentionally (can create huge result sets)
  ```sql
  SELECT * FROM colors CROSS JOIN sizes;
  -- If 3 colors and 4 sizes, returns 12 rows
  ```

---

## 🔹 3️⃣ AGGREGATE FUNCTIONS & GROUPING

### Aggregate Functions
- Perform calculation on multiple rows and return single value
- Common functions: `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`
- Ignore NULL values (except COUNT(*))
  ```sql
  SELECT COUNT(*), AVG(salary), MAX(salary)
  FROM employees;
  ```

### COUNT vs COUNT(*)
- **COUNT(*)**: Counts all rows including NULLs
- **COUNT(column)**: Counts non-NULL values in that column
  ```sql
  SELECT COUNT(*), COUNT(manager_id) FROM employees;
  -- If 100 employees, 10 without manager: 100, 90
  ```

### WHERE vs HAVING
- **WHERE**: Filters rows BEFORE grouping (cannot use aggregate functions)
- **HAVING**: Filters groups AFTER grouping (can use aggregate functions)
  ```sql
  SELECT dept_id, AVG(salary)
  FROM employees
  WHERE salary > 30000  -- Filter individual rows
  GROUP BY dept_id
  HAVING AVG(salary) > 50000;  -- Filter groups
  ```

### GROUP BY
- Groups rows with same values into summary rows
- Must include all non-aggregated columns in SELECT
  ```sql
  SELECT dept_id, COUNT(*) as employee_count
  FROM employees
  GROUP BY dept_id;
  ```

### Find Second Highest Salary
- **Method 1**: Using LIMIT and OFFSET
  ```sql
  SELECT DISTINCT salary
  FROM employees
  ORDER BY salary DESC
  LIMIT 1 OFFSET 1;
  ```
- **Method 2**: Using subquery
  ```sql
  SELECT MAX(salary)
  FROM employees
  WHERE salary < (SELECT MAX(salary) FROM employees);
  ```

### Department-wise Highest Salary
- Use GROUP BY with MAX aggregate
  ```sql
  SELECT dept_id, MAX(salary) as highest_salary
  FROM employees
  GROUP BY dept_id;
  ```

### Find Duplicate Records
- Use GROUP BY with HAVING COUNT > 1
  ```sql
  SELECT email, COUNT(*) as count
  FROM users
  GROUP BY email
  HAVING COUNT(*) > 1;
  ```

### Employees with Salary Above Average
- Use subquery to calculate average
  ```sql
  SELECT name, salary
  FROM employees
  WHERE salary > (SELECT AVG(salary) FROM employees);
  ```

---

## 🔹 4️⃣ SUBQUERIES & CTEs

### What is a Subquery?
- Query nested inside another query (inner query executes first)
- Can be used in SELECT, FROM, WHERE, HAVING clauses
- Must be enclosed in parentheses
  ```sql
  SELECT name FROM employees
  WHERE salary > (SELECT AVG(salary) FROM employees);
  ```

### Scalar Subquery
- Returns single value (one row, one column)
- Can be used anywhere a single value is expected
  ```sql
  SELECT name, salary,
    (SELECT AVG(salary) FROM employees) as avg_salary
  FROM employees;
  ```

### Correlated Subquery
- References column from outer query (executes once per outer row)
- Slower than non-correlated (re-executes for each row)
  ```sql
  SELECT e1.name, e1.salary
  FROM employees e1
  WHERE salary > (
    SELECT AVG(salary) FROM employees e2
    WHERE e2.dept_id = e1.dept_id
  );
  ```

### Non-correlated Subquery
- Independent of outer query (executes once)
- Faster than correlated subquery
  ```sql
  SELECT name FROM employees
  WHERE dept_id IN (SELECT id FROM departments WHERE location = 'NY');
  ```

### Subquery vs JOIN
- **Subquery**: Better for filtering, more readable for simple cases
- **JOIN**: Better performance for large datasets, can return columns from both tables
- Use JOIN when you need data from multiple tables; subquery for existence checks

### CTE (Common Table Expression)
- Temporary named result set using WITH clause
- Makes complex queries more readable and maintainable
- Can be referenced multiple times in main query
  ```sql
  WITH high_earners AS (
    SELECT * FROM employees WHERE salary > 100000
  )
  SELECT dept_id, COUNT(*) FROM high_earners GROUP BY dept_id;
  ```

### Advantages of CTE
- **Readability**: Breaks complex queries into logical steps
- **Reusability**: Can reference same CTE multiple times
- **Recursion**: Supports recursive queries (hierarchical data)

### Recursive CTE
- CTE that references itself (useful for hierarchical data like org charts)
- Has anchor member (base case) and recursive member
  ```sql
  WITH RECURSIVE employee_hierarchy AS (
    SELECT id, name, manager_id, 1 as level
    FROM employees WHERE manager_id IS NULL
    UNION ALL
    SELECT e.id, e.name, e.manager_id, eh.level + 1
    FROM employees e
    JOIN employee_hierarchy eh ON e.manager_id = eh.id
  )
  SELECT * FROM employee_hierarchy;
  ```

---

## 🔹 5️⃣ INDEXES & PERFORMANCE

### What is an Index?
- Data structure (usually B-tree) that speeds up data retrieval
- Trade-off: faster SELECT, slower INSERT/UPDATE/DELETE
- Like a book index - helps find information without scanning entire book

### Clustered Index
- Sorts and stores actual data rows in the table (physical order)
- Only ONE per table (usually on primary key)
- Leaf nodes contain actual data
  ```sql
  CREATE TABLE employees (
    id INT PRIMARY KEY,  -- Automatically creates clustered index
    name VARCHAR(100)
  );
  ```

### Non-clustered Index
- Separate structure with pointers to actual data
- Can have multiple per table
- Leaf nodes contain pointer to data row
  ```sql
  CREATE INDEX idx_name ON employees(name);
  CREATE INDEX idx_dept_salary ON employees(dept_id, salary);
  ```

### When to Avoid Indexes?
- **Small tables**: Full table scan is faster
- **Frequently updated columns**: Index maintenance overhead
- **Low cardinality columns**: Columns with few distinct values (e.g., gender, boolean)

### How Indexes Improve Performance?
- Reduces number of rows to scan (logarithmic vs linear search)
- Speeds up WHERE, JOIN, ORDER BY, GROUP BY operations
- Example: Finding in 1M rows - without index: 1M checks, with index: ~20 checks (B-tree)

### Why Indexes Slow Down INSERT/UPDATE?
- Every INSERT/UPDATE/DELETE must update index structure
- Multiple indexes = multiple updates per operation
- Balance: index frequently queried columns, avoid over-indexing

### How to Optimize a Slow Query?
- Use `EXPLAIN` to analyze query execution plan
- Add indexes on WHERE, JOIN, ORDER BY columns
- Avoid SELECT * (retrieve only needed columns)
- Rewrite subqueries as JOINs if possible
- Use LIMIT for large result sets

### EXPLAIN PLAN
- Shows how database executes a query (execution plan)
- Reveals: table scan type, indexes used, rows examined, join order
- Key metrics: type (ALL=bad, ref/range=good), rows, Extra
  ```sql
  EXPLAIN SELECT * FROM employees WHERE dept_id = 5;
  ```

---

## 🔹 6️⃣ CONSTRAINTS & KEYS

### What are Constraints?
- Rules enforced on table columns to ensure data integrity
- Types: PRIMARY KEY, FOREIGN KEY, UNIQUE, NOT NULL, CHECK, DEFAULT
- Prevents invalid data from being inserted

### Primary Key vs Unique Key
- **Primary Key**: Uniquely identifies row, NOT NULL, only one per table, creates clustered index
- **Unique Key**: Ensures uniqueness, can be NULL, multiple per table, creates non-clustered index
  ```sql
  CREATE TABLE users (
    id INT PRIMARY KEY,        -- One primary key
    email VARCHAR(100) UNIQUE, -- Multiple unique keys allowed
    phone VARCHAR(20) UNIQUE
  );
  ```

### Foreign Key Constraints
- Enforces referential integrity between tables
- Prevents orphaned records (child without parent)
- Actions: CASCADE, SET NULL, SET DEFAULT, RESTRICT
  ```sql
  CREATE TABLE orders (
    id INT PRIMARY KEY,
    customer_id INT,
    FOREIGN KEY (customer_id) REFERENCES customers(id)
      ON DELETE CASCADE  -- Delete orders when customer deleted
      ON UPDATE CASCADE  -- Update orders when customer id changes
  );
  ```

### Referential Integrity
- Ensures relationships between tables remain consistent
- Foreign key in child table must exist in parent table (or be NULL)
- Prevents: inserting invalid foreign key, deleting referenced parent row

### Can a Table Have Multiple Primary Keys?
- **NO** - only ONE primary key per table
- Can have **composite primary key** (multiple columns together form primary key)
  ```sql
  CREATE TABLE enrollment (
    student_id INT,
    course_id INT,
    PRIMARY KEY (student_id, course_id)  -- Composite key
  );
  ```

### Can Foreign Key be NULL?
- **YES** - unless explicitly defined as NOT NULL
- NULL means "no relationship" (optional relationship)
  ```sql
  CREATE TABLE employees (
    id INT PRIMARY KEY,
    manager_id INT,  -- Can be NULL for top-level employees
    FOREIGN KEY (manager_id) REFERENCES employees(id)
  );
  ```

---

## 🔹 7️⃣ TRANSACTIONS & ACID

### What is a Transaction?
- Group of SQL operations treated as single unit (all succeed or all fail)
- Ensures data consistency (e.g., bank transfer: debit + credit together)
- Syntax: `BEGIN`, `COMMIT`, `ROLLBACK`
  ```sql
  BEGIN TRANSACTION;
  UPDATE accounts SET balance = balance - 100 WHERE id = 1;
  UPDATE accounts SET balance = balance + 100 WHERE id = 2;
  COMMIT;  -- Or ROLLBACK if error
  ```

### ACID Properties
- **Atomicity**: All or nothing (transaction fully completes or fully fails)
- **Consistency**: Database remains in valid state (constraints maintained)
- **Isolation**: Concurrent transactions don't interfere with each other
- **Durability**: Committed changes persist even after system failure

### COMMIT
- Permanently saves all changes made in current transaction
- Makes changes visible to other users
- Cannot be undone after commit
  ```sql
  BEGIN TRANSACTION;
  INSERT INTO orders VALUES (1, 100);
  COMMIT;  -- Changes are permanent
  ```

### ROLLBACK
- Undoes all changes made in current transaction
- Returns database to state before transaction began
- Used when error occurs or business logic fails
  ```sql
  BEGIN TRANSACTION;
  UPDATE accounts SET balance = balance - 100 WHERE id = 1;
  -- Error occurs
  ROLLBACK;  -- Undo the update
  ```

### SAVEPOINT
- Creates checkpoint within transaction (partial rollback)
- Can rollback to savepoint without aborting entire transaction
  ```sql
  BEGIN TRANSACTION;
  INSERT INTO orders VALUES (1, 100);
  SAVEPOINT sp1;
  INSERT INTO orders VALUES (2, 200);
  ROLLBACK TO sp1;  -- Only second insert is undone
  COMMIT;
  ```

### Auto-commit
- Each SQL statement automatically committed (no explicit COMMIT needed)
- Default mode in most databases
- Disable for multi-statement transactions: `SET AUTOCOMMIT = 0;`

### Transaction Isolation
- Controls how concurrent transactions interact
- Higher isolation = more consistency, less concurrency
- Four levels: READ UNCOMMITTED, READ COMMITTED, REPEATABLE READ, SERIALIZABLE

---

## 🔹 8️⃣ ISOLATION LEVELS & LOCKING

### Transaction Isolation Levels
- **READ UNCOMMITTED**: Lowest isolation, allows dirty reads
- **READ COMMITTED**: Prevents dirty reads (default in most DBs)
- **REPEATABLE READ**: Prevents dirty + non-repeatable reads
- **SERIALIZABLE**: Highest isolation, prevents all anomalies (slowest)
  ```sql
  SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
  ```

### Dirty Read
- Reading uncommitted changes from another transaction
- Problem: Other transaction might rollback, you read invalid data
- Prevented by: READ COMMITTED and higher

### Non-repeatable Read
- Reading same row twice in transaction returns different values
- Problem: Another transaction modified and committed between your reads
- Prevented by: REPEATABLE READ and higher
  ```sql
  -- Transaction 1
  SELECT salary FROM employees WHERE id = 1;  -- Returns 50000
  -- Transaction 2 updates salary to 60000 and commits
  SELECT salary FROM employees WHERE id = 1;  -- Returns 60000 (non-repeatable!)
  ```

### Phantom Read
- Re-executing query returns different set of rows
- Problem: Another transaction inserted/deleted rows between your queries
- Prevented by: SERIALIZABLE
  ```sql
  -- Transaction 1
  SELECT COUNT(*) FROM employees WHERE dept_id = 5;  -- Returns 10
  -- Transaction 2 inserts new employee in dept 5 and commits
  SELECT COUNT(*) FROM employees WHERE dept_id = 5;  -- Returns 11 (phantom!)
  ```

### READ COMMITTED vs REPEATABLE READ
- **READ COMMITTED**: Each query sees latest committed data (allows non-repeatable reads)
- **REPEATABLE READ**: Sees snapshot of data at transaction start (consistent reads)
- Use READ COMMITTED for most applications; REPEATABLE READ for financial transactions

### Locking
- Mechanism to control concurrent access to data
- **Shared Lock (S)**: Multiple transactions can read, none can write
- **Exclusive Lock (X)**: Only one transaction can read/write
- Prevents data inconsistencies but reduces concurrency

### Deadlock
- Two transactions wait for each other to release locks (circular wait)
- Database detects and kills one transaction (rollback)
- Prevention: Access tables in same order, keep transactions short
  ```sql
  -- Transaction 1: Locks A, waits for B
  -- Transaction 2: Locks B, waits for A
  -- DEADLOCK! Database kills one transaction
  ```

---

## 🔹 9️⃣ FUNCTIONS & STORED PROCEDURES

### Stored Procedure
- Pre-compiled SQL code stored in database (like a function)
- Accepts parameters, performs operations, can return multiple result sets
- Benefits: Reusability, security, performance (pre-compiled)
  ```sql
  CREATE PROCEDURE GetEmployeesByDept(IN dept_id INT)
  BEGIN
    SELECT * FROM employees WHERE department_id = dept_id;
  END;
  
  CALL GetEmployeesByDept(5);
  ```

### Procedure vs Function
- **Procedure**: Can have IN/OUT parameters, doesn't return value (uses OUT params), can modify data
- **Function**: Must return single value, cannot modify data (read-only), can be used in SELECT
  ```sql
  -- Function
  CREATE FUNCTION GetTotalSalary(dept_id INT) RETURNS DECIMAL
  BEGIN
    RETURN (SELECT SUM(salary) FROM employees WHERE department_id = dept_id);
  END;
  
  SELECT GetTotalSalary(5);  -- Can use in SELECT
  ```

### User-Defined Functions (UDF)
- Custom functions created by users (not built-in)
- Types: Scalar (returns single value), Table-valued (returns table)
- Use for complex calculations, data transformations
  ```sql
  CREATE FUNCTION CalculateBonus(salary DECIMAL) RETURNS DECIMAL
  BEGIN
    RETURN salary * 0.10;
  END;
  ```

### Triggers
- Automatically executed code when specific event occurs (INSERT, UPDATE, DELETE)
- Types: BEFORE trigger (executes before operation), AFTER trigger (executes after)
- Use for: Auditing, validation, maintaining derived data
  ```sql
  CREATE TRIGGER before_employee_insert
  BEFORE INSERT ON employees
  FOR EACH ROW
  BEGIN
    SET NEW.created_at = NOW();
  END;
  ```

### When to Use Triggers?
- **Audit logging**: Track who changed what and when
- **Data validation**: Enforce complex business rules
- **Maintain derived data**: Auto-update summary tables
- **Caution**: Can make debugging difficult, impacts performance

---

## 🔹 🔟 SQL SCENARIO-BASED QUESTIONS

### Find Nth Highest Salary
- **Method 1**: LIMIT with OFFSET
  ```sql
  SELECT DISTINCT salary
  FROM employees
  ORDER BY salary DESC
  LIMIT 1 OFFSET N-1;  -- For 3rd highest: OFFSET 2
  ```
- **Method 2**: Subquery with COUNT
  ```sql
  SELECT salary FROM employees e1
  WHERE N-1 = (
    SELECT COUNT(DISTINCT salary) FROM employees e2
    WHERE e2.salary > e1.salary
  );
  ```

### Delete Duplicate Rows
- Keep one copy, delete rest (using ROW_NUMBER or self-join)
  ```sql
  -- Method 1: Using CTE with ROW_NUMBER
  WITH cte AS (
    SELECT *, ROW_NUMBER() OVER (PARTITION BY email ORDER BY id) as rn
    FROM users
  )
  DELETE FROM users WHERE id IN (SELECT id FROM cte WHERE rn > 1);
  
  -- Method 2: Self-join
  DELETE u1 FROM users u1
  JOIN users u2 ON u1.email = u2.email AND u1.id > u2.id;
  ```

### Update Records Using JOIN
- Update one table based on values from another table
  ```sql
  UPDATE employees e
  JOIN departments d ON e.dept_id = d.id
  SET e.salary = e.salary * 1.10
  WHERE d.location = 'NY';
  ```

### Fetch Records in One Table but Not Another
- Use LEFT JOIN with NULL check or NOT IN/NOT EXISTS
  ```sql
  -- Method 1: LEFT JOIN
  SELECT e.* FROM employees e
  LEFT JOIN departments d ON e.dept_id = d.id
  WHERE d.id IS NULL;
  
  -- Method 2: NOT IN
  SELECT * FROM employees
  WHERE dept_id NOT IN (SELECT id FROM departments);
  
  -- Method 3: NOT EXISTS (most efficient)
  SELECT * FROM employees e
  WHERE NOT EXISTS (SELECT 1 FROM departments d WHERE d.id = e.dept_id);
  ```

### Find Records with No Matching Rows
- Use LEFT JOIN and check for NULL (orphaned records)
  ```sql
  SELECT e.* FROM employees e
  LEFT JOIN departments d ON e.dept_id = d.id
  WHERE d.id IS NULL;
  -- Employees without valid department
  ```

### Paginate Results (LIMIT/OFFSET)
- Display results in pages (e.g., 10 records per page)
  ```sql
  -- Page 1: records 1-10
  SELECT * FROM employees ORDER BY id LIMIT 10 OFFSET 0;
  
  -- Page 2: records 11-20
  SELECT * FROM employees ORDER BY id LIMIT 10 OFFSET 10;
  
  -- Page N: OFFSET = (N-1) * page_size
  ```

### Handle NULL Values
- Use COALESCE, IFNULL, or IS NULL checks
  ```sql
  -- Replace NULL with default value
  SELECT name, COALESCE(phone, 'No phone') as phone FROM users;
  
  -- Filter NULL values
  SELECT * FROM employees WHERE manager_id IS NOT NULL;
  
  -- NULL-safe comparison
  SELECT * FROM employees WHERE COALESCE(bonus, 0) > 5000;
  ```

### Find Consecutive Records
- Use window functions (LAG/LEAD) or self-join
  ```sql
  -- Find employees with consecutive IDs
  SELECT e1.id, e1.name
  FROM employees e1
  JOIN employees e2 ON e1.id = e2.id - 1;
  
  -- Using LAG window function
  SELECT id, name,
    LAG(id) OVER (ORDER BY id) as prev_id
  FROM employees
  WHERE id = prev_id + 1;
  ```

---

## 🔹 1️⃣1️⃣ NORMALIZATION & DESIGN

### What is Normalization?
- Process of organizing data to reduce redundancy and improve integrity
- Divides large tables into smaller tables and links them using relationships
- Benefits: Less storage, easier updates, prevents anomalies

### 1NF (First Normal Form)
- Each column contains atomic (indivisible) values
- No repeating groups or arrays
- Each row is unique (has primary key)
  ```sql
  -- NOT 1NF
  CREATE TABLE students (
    id INT,
    name VARCHAR(100),
    courses VARCHAR(200)  -- "Math, Physics, Chemistry" - NOT atomic
  );
  
  -- 1NF
  CREATE TABLE student_courses (
    student_id INT,
    course VARCHAR(50),
    PRIMARY KEY (student_id, course)
  );
  ```

### 2NF (Second Normal Form)
- Must be in 1NF
- All non-key columns fully depend on entire primary key (no partial dependency)
- Applies to composite keys
  ```sql
  -- NOT 2NF (instructor depends only on course, not on student)
  CREATE TABLE enrollments (
    student_id INT,
    course_id INT,
    instructor VARCHAR(100),  -- Depends only on course_id
    PRIMARY KEY (student_id, course_id)
  );
  
  -- 2NF: Split into two tables
  CREATE TABLE enrollments (
    student_id INT,
    course_id INT,
    PRIMARY KEY (student_id, course_id)
  );
  CREATE TABLE courses (
    course_id INT PRIMARY KEY,
    instructor VARCHAR(100)
  );
  ```

### 3NF (Third Normal Form)
- Must be in 2NF
- No transitive dependencies (non-key column depends on another non-key column)
  ```sql
  -- NOT 3NF (city depends on zip_code, not on employee_id)
  CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    zip_code VARCHAR(10),
    city VARCHAR(50)  -- Depends on zip_code, not id
  );
  
  -- 3NF: Split into two tables
  CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    zip_code VARCHAR(10)
  );
  CREATE TABLE zip_codes (
    zip_code VARCHAR(10) PRIMARY KEY,
    city VARCHAR(50)
  );
  ```

### Denormalization
- Intentionally adding redundancy to improve read performance
- Trade-off: Faster queries, slower updates, more storage
- Use when: Read-heavy applications, complex joins are slow, data rarely changes
  ```sql
  -- Denormalized: Store department name in employees table
  -- Avoids JOIN but duplicates department name
  CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    dept_id INT,
    dept_name VARCHAR(100)  -- Redundant but faster queries
  );
  ```

### OLTP vs OLAP
- **OLTP (Online Transaction Processing)**: Day-to-day operations (INSERT, UPDATE, DELETE)
  - Normalized, fast writes, current data, row-oriented
  - Examples: E-commerce orders, banking transactions
- **OLAP (Online Analytical Processing)**: Complex analysis and reporting
  - Denormalized, fast reads, historical data, column-oriented
  - Examples: Data warehouses, business intelligence

### Star Schema vs Snowflake Schema
- **Star Schema**: Central fact table + denormalized dimension tables (simpler, faster queries)
  - Fact table: Orders (order_id, customer_id, product_id, date_id, amount)
  - Dimension tables: Customers, Products, Dates (denormalized)
- **Snowflake Schema**: Central fact table + normalized dimension tables (less redundancy, more joins)
  - Dimension tables are further normalized (e.g., Customers → Cities → States)

---

## 🔹 1️⃣2️⃣ SQL vs NoSQL

### SQL vs NoSQL Differences
- **SQL**: Structured, fixed schema, ACID compliant, relational, vertical scaling
- **NoSQL**: Unstructured/semi-structured, flexible schema, eventual consistency, non-relational, horizontal scaling
- **SQL**: Tables with rows/columns; **NoSQL**: Documents, key-value, graph, column-family

### When to Use SQL Database?
- **Complex relationships**: Multiple tables with foreign keys
- **ACID requirements**: Financial transactions, inventory management
- **Complex queries**: JOINs, aggregations, reporting
- Examples: Banking, ERP, CRM systems

### When to Use NoSQL?
- **Flexible schema**: Rapidly changing data structure
- **Massive scale**: Horizontal scaling needed (millions of users)
- **Simple queries**: Key-value lookups, no complex JOINs
- Examples: Social media feeds, IoT data, real-time analytics, caching

### Examples of SQL Databases
- **MySQL**: Open-source, popular for web applications
- **PostgreSQL**: Advanced features, strong ACID compliance
- **Oracle**: Enterprise-grade, expensive
- **SQL Server**: Microsoft, good Windows integration
- **SQLite**: Embedded, serverless, mobile apps

### Examples of NoSQL Databases
- **MongoDB**: Document store (JSON-like)
- **Redis**: In-memory key-value store (caching)
- **Cassandra**: Column-family, highly scalable
- **Neo4j**: Graph database (relationships)
- **DynamoDB**: AWS managed key-value store

---

## 📚 Study Tips

1. **Practice queries**: Use online SQL editors (SQLFiddle, DB Fiddle)
2. **Focus on JOINs**: Most interview questions involve JOINs
3. **Master aggregations**: GROUP BY + HAVING are very common
4. **Understand indexes**: Know when to use and when to avoid
5. **Learn EXPLAIN**: Analyze query performance
6. **Practice scenarios**: Nth highest salary, duplicates, pagination
7. **Know trade-offs**: Normalization vs performance, indexes vs write speed
8. **Understand ACID**: Transactions are critical for backend roles

Good luck with your interview preparation! 🚀

---

# 🍃 MongoDB (NoSQL Database)

## 🔹 1️⃣ MongoDB Basics

### What is MongoDB?

MongoDB is a **NoSQL document database** that stores data in flexible, JSON-like documents.

> Think of it as storing data in filing cabinets with folders (collections) containing documents (JSON objects) instead of rigid spreadsheet tables.

**Key Features:**
- **Document-oriented**: Data stored as BSON (Binary JSON) documents
- **Schema-flexible**: No fixed structure, fields can vary between documents
- **Scalable**: Built for horizontal scaling (sharding)
- **High performance**: Fast reads/writes, indexing support

**Real-life analogy:**
- **SQL** = Filing cabinet with fixed forms (same fields for everyone)
- **MongoDB** = Filing cabinet with flexible notes (each note can have different information)

---

### Document Structure

Documents are JSON-like objects with field-value pairs.

```javascript
// A document in MongoDB
{
  _id: ObjectId("507f1f77bcf86cd799439011"),
  name: "John Doe",
  age: 30,
  email: "john@example.com",
  address: {
    street: "123 Main St",
    city: "New York"
  },
  hobbies: ["reading", "gaming", "coding"]
}
```

**Key points:**
- `_id` is automatically created (unique identifier)
- Fields can be strings, numbers, arrays, nested objects
- No need to define schema beforehand

---

### Database, Collection, Document

| MongoDB | SQL Equivalent | Description |
|---------|----------------|-------------|
| **Database** | Database | Container for collections |
| **Collection** | Table | Group of documents |
| **Document** | Row | Individual record (JSON object) |
| **Field** | Column | Key-value pair in document |

**Example:**
```javascript
// Database: company
// Collection: employees
// Document:
{
  _id: 1,
  name: "Alice",
  department: "Engineering",
  salary: 80000
}
```

---

### BSON vs JSON

| Feature | JSON | BSON |
|---------|------|------|
| **Format** | Text | Binary |
| **Size** | Larger | Smaller |
| **Speed** | Slower parsing | Faster parsing |
| **Data types** | Limited (string, number, boolean, null) | Extended (Date, ObjectId, Binary) |

**Why BSON?**
- Faster to parse and traverse
- Supports more data types
- Efficient for storage and network transfer

---

### ObjectId

Unique identifier automatically generated for each document.

```javascript
ObjectId("507f1f77bcf86cd799439011")
```

**Structure (12 bytes):**
- 4 bytes: Timestamp (creation time)
- 5 bytes: Random value
- 3 bytes: Incrementing counter

**Benefits:**
- Globally unique without coordination
- Contains creation timestamp
- Sortable by creation time

---

## 🔹 2️⃣ CRUD Operations

### Insert Documents

**Insert One:**
```javascript
db.users.insertOne({
  name: "John Doe",
  age: 30,
  email: "john@example.com"
});
```

**Insert Many:**
```javascript
db.users.insertMany([
  { name: "Alice", age: 25 },
  { name: "Bob", age: 35 },
  { name: "Charlie", age: 28 }
]);
```

**Real-life analogy:**
Like adding new files to a folder - each file can have different content.

---

### Find Documents (Query)

**Find All:**
```javascript
db.users.find();
```

**Find with Filter:**
```javascript
// Find users older than 25
db.users.find({ age: { $gt: 25 } });

// Find by exact match
db.users.find({ name: "John Doe" });

// Find with multiple conditions (AND)
db.users.find({ age: { $gt: 25 }, city: "New York" });
```

**Find One:**
```javascript
db.users.findOne({ email: "john@example.com" });
```

**Projection (Select specific fields):**
```javascript
// Only return name and age (exclude _id)
db.users.find({}, { name: 1, age: 1, _id: 0 });
```

---

### Update Documents

**Update One:**
```javascript
db.users.updateOne(
  { name: "John Doe" },           // Filter
  { $set: { age: 31 } }           // Update
);
```

**Update Many:**
```javascript
// Give 10% raise to all employees in Engineering
db.employees.updateMany(
  { department: "Engineering" },
  { $inc: { salary: 0.10 } }
);
```

**Replace Document:**
```javascript
db.users.replaceOne(
  { name: "John Doe" },
  { name: "John Doe", age: 31, email: "newemail@example.com" }
);
```

**Upsert (Insert if not exists):**
```javascript
db.users.updateOne(
  { email: "new@example.com" },
  { $set: { name: "New User", age: 25 } },
  { upsert: true }  // Insert if not found
);
```

---

### Delete Documents

**Delete One:**
```javascript
db.users.deleteOne({ name: "John Doe" });
```

**Delete Many:**
```javascript
// Delete all users younger than 18
db.users.deleteMany({ age: { $lt: 18 } });

// Delete all documents in collection
db.users.deleteMany({});
```

---

## 🔹 3️⃣ Query Operators

### Comparison Operators

| Operator | Meaning | Example |
|----------|---------|---------|
| `$eq` | Equal to | `{ age: { $eq: 25 } }` |
| `$ne` | Not equal | `{ age: { $ne: 25 } }` |
| `$gt` | Greater than | `{ age: { $gt: 25 } }` |
| `$gte` | Greater than or equal | `{ age: { $gte: 25 } }` |
| `$lt` | Less than | `{ age: { $lt: 25 } }` |
| `$lte` | Less than or equal | `{ age: { $lte: 25 } }` |
| `$in` | In array | `{ age: { $in: [25, 30, 35] } }` |
| `$nin` | Not in array | `{ age: { $nin: [25, 30] } }` |

**Examples:**
```javascript
// Users between 25 and 35
db.users.find({ age: { $gte: 25, $lte: 35 } });

// Users from specific cities
db.users.find({ city: { $in: ["New York", "London", "Tokyo"] } });
```

---

### Logical Operators

**$and** - All conditions must be true
```javascript
db.users.find({
  $and: [
    { age: { $gt: 25 } },
    { city: "New York" }
  ]
});

// Simplified (implicit AND)
db.users.find({ age: { $gt: 25 }, city: "New York" });
```

**$or** - At least one condition must be true
```javascript
db.users.find({
  $or: [
    { age: { $lt: 25 } },
    { age: { $gt: 60 } }
  ]
});
```

**$not** - Inverts condition
```javascript
db.users.find({ age: { $not: { $gt: 25 } } });
```

**$nor** - None of the conditions should be true
```javascript
db.users.find({
  $nor: [
    { age: { $lt: 25 } },
    { city: "New York" }
  ]
});
```

---

### Element Operators

**$exists** - Check if field exists
```javascript
// Find users with phone number
db.users.find({ phone: { $exists: true } });

// Find users without phone number
db.users.find({ phone: { $exists: false } });
```

**$type** - Check field data type
```javascript
// Find documents where age is a number
db.users.find({ age: { $type: "number" } });

// Find documents where age is a string
db.users.find({ age: { $type: "string" } });
```

---

### Array Operators

**$all** - Array contains all elements
```javascript
// Users with both "reading" and "coding" hobbies
db.users.find({ hobbies: { $all: ["reading", "coding"] } });
```

**$elemMatch** - Array element matches all conditions
```javascript
db.products.find({
  reviews: {
    $elemMatch: { rating: { $gte: 4 }, verified: true }
  }
});
```

**$size** - Array has specific length
```javascript
// Users with exactly 3 hobbies
db.users.find({ hobbies: { $size: 3 } });
```

---

## 🔹 4️⃣ Update Operators

### Field Update Operators

**$set** - Set field value
```javascript
db.users.updateOne(
  { name: "John" },
  { $set: { age: 31, city: "Boston" } }
);
```

**$unset** - Remove field
```javascript
db.users.updateOne(
  { name: "John" },
  { $unset: { phone: "" } }  // Removes phone field
);
```

**$rename** - Rename field
```javascript
db.users.updateMany(
  {},
  { $rename: { "name": "fullName" } }
);
```

**$inc** - Increment/decrement number
```javascript
// Increase age by 1
db.users.updateOne(
  { name: "John" },
  { $inc: { age: 1 } }
);

// Decrease stock by 5
db.products.updateOne(
  { _id: 1 },
  { $inc: { stock: -5 } }
);
```

**$mul** - Multiply field value
```javascript
// Double the price
db.products.updateOne(
  { _id: 1 },
  { $mul: { price: 2 } }
);
```

**$min** - Update if new value is less
```javascript
db.products.updateOne(
  { _id: 1 },
  { $min: { price: 50 } }  // Only updates if current price > 50
);
```

**$max** - Update if new value is greater
```javascript
db.products.updateOne(
  { _id: 1 },
  { $max: { price: 100 } }  // Only updates if current price < 100
);
```

---

### Array Update Operators

**$push** - Add element to array
```javascript
db.users.updateOne(
  { name: "John" },
  { $push: { hobbies: "swimming" } }
);
```

**$pull** - Remove elements matching condition
```javascript
db.users.updateOne(
  { name: "John" },
  { $pull: { hobbies: "gaming" } }
);
```

**$pop** - Remove first or last element
```javascript
// Remove last element
db.users.updateOne(
  { name: "John" },
  { $pop: { hobbies: 1 } }
);

// Remove first element
db.users.updateOne(
  { name: "John" },
  { $pop: { hobbies: -1 } }
);
```

**$addToSet** - Add element only if not exists (no duplicates)
```javascript
db.users.updateOne(
  { name: "John" },
  { $addToSet: { hobbies: "reading" } }  // Won't add if already exists
);
```

**$each** - Add multiple elements
```javascript
db.users.updateOne(
  { name: "John" },
  { $push: { hobbies: { $each: ["swimming", "hiking"] } } }
);
```

---

## 🔹 5️⃣ Indexing

### What is an Index?

Index in MongoDB is like a book index - helps find data quickly without scanning entire collection.

**Benefits:**
- ✅ Faster queries (especially with large datasets)
- ✅ Efficient sorting
- ✅ Supports unique constraints

**Trade-offs:**
- ❌ Slower writes (index must be updated)
- ❌ Uses more storage

---

### Create Index

**Single Field Index:**
```javascript
// Index on age field
db.users.createIndex({ age: 1 });  // 1 = ascending, -1 = descending
```

**Compound Index (Multiple fields):**
```javascript
// Index on age and city
db.users.createIndex({ age: 1, city: 1 });
```

**Unique Index:**
```javascript
// Ensure email is unique
db.users.createIndex({ email: 1 }, { unique: true });
```

**Text Index (Full-text search):**
```javascript
db.articles.createIndex({ title: "text", content: "text" });

// Search
db.articles.find({ $text: { $search: "mongodb tutorial" } });
```

---

### View Indexes

```javascript
// List all indexes on collection
db.users.getIndexes();
```

---

### Drop Index

```javascript
// Drop specific index
db.users.dropIndex("age_1");

// Drop all indexes except _id
db.users.dropIndexes();
```

---

### When to Use Indexes?

**✅ Use indexes on:**
- Fields frequently used in queries (`find`, `sort`)
- Fields used in joins (`$lookup`)
- Fields with high cardinality (many unique values)

**❌ Avoid indexes on:**
- Small collections (full scan is faster)
- Fields that change frequently
- Fields with low cardinality (e.g., boolean, gender)

---

### Explain Query Performance

```javascript
// Analyze query execution
db.users.find({ age: { $gt: 25 } }).explain("executionStats");
```

**Key metrics:**
- `totalDocsExamined`: Documents scanned
- `executionTimeMillis`: Query time
- `indexUsed`: Which index was used

**Real-life analogy:**
Like using a book's index vs reading every page to find a topic.

---

## 🔹 6️⃣ Aggregation Framework

### What is Aggregation?

Process data in stages (pipeline) to transform and analyze documents.

> Think of it as an assembly line - data passes through multiple stages, each stage transforms it.

**Aggregation Pipeline:**
```javascript
db.collection.aggregate([
  { stage1 },
  { stage2 },
  { stage3 }
]);
```

---

### Common Aggregation Stages

**$match** - Filter documents (like `find`)
```javascript
db.orders.aggregate([
  { $match: { status: "completed" } }
]);
```

**$group** - Group by field and calculate aggregates
```javascript
// Total sales by product
db.orders.aggregate([
  {
    $group: {
      _id: "$product",
      totalSales: { $sum: "$amount" },
      count: { $sum: 1 }
    }
  }
]);
```

**$project** - Select/reshape fields
```javascript
db.users.aggregate([
  {
    $project: {
      name: 1,
      age: 1,
      isAdult: { $gte: ["$age", 18] }
    }
  }
]);
```

**$sort** - Sort documents
```javascript
db.users.aggregate([
  { $sort: { age: -1 } }  // Sort by age descending
]);
```

**$limit** - Limit number of documents
```javascript
db.users.aggregate([
  { $sort: { age: -1 } },
  { $limit: 10 }  // Top 10 oldest users
]);
```

**$skip** - Skip documents (pagination)
```javascript
db.users.aggregate([
  { $skip: 20 },
  { $limit: 10 }  // Page 3 (skip 20, show next 10)
]);
```

**$lookup** - Join with another collection
```javascript
// Join orders with users
db.orders.aggregate([
  {
    $lookup: {
      from: "users",
      localField: "userId",
      foreignField: "_id",
      as: "userDetails"
    }
  }
]);
```

**$unwind** - Deconstruct array field
```javascript
// Expand hobbies array
db.users.aggregate([
  { $unwind: "$hobbies" }
]);

// Before: { name: "John", hobbies: ["reading", "coding"] }
// After:  { name: "John", hobbies: "reading" }
//         { name: "John", hobbies: "coding" }
```

---

### Aggregation Examples

**Example 1: Average salary by department**
```javascript
db.employees.aggregate([
  {
    $group: {
      _id: "$department",
      avgSalary: { $avg: "$salary" },
      count: { $sum: 1 }
    }
  },
  { $sort: { avgSalary: -1 } }
]);
```

**Example 2: Top 5 products by sales**
```javascript
db.orders.aggregate([
  { $match: { status: "completed" } },
  {
    $group: {
      _id: "$productId",
      totalSales: { $sum: "$amount" }
    }
  },
  { $sort: { totalSales: -1 } },
  { $limit: 5 }
]);
```

**Example 3: Users by age group**
```javascript
db.users.aggregate([
  {
    $bucket: {
      groupBy: "$age",
      boundaries: [0, 18, 30, 50, 100],
      default: "Other",
      output: {
        count: { $sum: 1 },
        users: { $push: "$name" }
      }
    }
  }
]);
```

---

## 🔹 7️⃣ Data Modeling

### Embedding vs Referencing

**Embedding (Denormalized):**
Store related data in same document.

```javascript
// User with embedded address
{
  _id: 1,
  name: "John",
  address: {
    street: "123 Main St",
    city: "New York",
    zip: "10001"
  }
}
```

**Benefits:**
- ✅ Single query to get all data
- ✅ Better performance (no joins)
- ✅ Atomic updates

**Use when:**
- One-to-one relationships
- One-to-few relationships
- Data accessed together

---

**Referencing (Normalized):**
Store reference to another document.

```javascript
// User
{
  _id: 1,
  name: "John",
  addressId: 100
}

// Address (separate collection)
{
  _id: 100,
  street: "123 Main St",
  city: "New York"
}
```

**Benefits:**
- ✅ No data duplication
- ✅ Smaller documents
- ✅ Better for many-to-many relationships

**Use when:**
- One-to-many relationships (many side is large)
- Many-to-many relationships
- Data accessed independently

---

### One-to-One Relationship

**Embed when:**
- Data always accessed together
- Small related data

```javascript
{
  _id: 1,
  name: "John",
  profile: {
    bio: "Software engineer",
    avatar: "avatar.jpg"
  }
}
```

---

### One-to-Many Relationship

**Embed when few (< 100):**
```javascript
// Blog post with comments
{
  _id: 1,
  title: "MongoDB Tutorial",
  comments: [
    { user: "Alice", text: "Great post!" },
    { user: "Bob", text: "Thanks!" }
  ]
}
```

**Reference when many:**
```javascript
// User
{ _id: 1, name: "John" }

// Orders (separate collection)
{ _id: 101, userId: 1, product: "Laptop", amount: 1000 }
{ _id: 102, userId: 1, product: "Mouse", amount: 20 }
```

---

### Many-to-Many Relationship

**Use references:**
```javascript
// Students
{ _id: 1, name: "Alice", courseIds: [101, 102] }
{ _id: 2, name: "Bob", courseIds: [101, 103] }

// Courses
{ _id: 101, name: "Math", studentIds: [1, 2] }
{ _id: 102, name: "Physics", studentIds: [1] }
```

---

### Schema Design Patterns

**Pattern 1: Attribute Pattern**
Store variable attributes as array of key-value pairs.

```javascript
// Instead of: { color: "red", size: "L", material: "cotton" }
{
  _id: 1,
  name: "T-Shirt",
  attributes: [
    { k: "color", v: "red" },
    { k: "size", v: "L" },
    { k: "material", v: "cotton" }
  ]
}
```

**Pattern 2: Bucket Pattern**
Group time-series data into buckets.

```javascript
// Instead of one document per measurement
{
  sensorId: 123,
  date: "2024-01-15",
  measurements: [
    { time: "00:00", temp: 20 },
    { time: "01:00", temp: 19 },
    { time: "02:00", temp: 18 }
  ]
}
```

---

## 🔹 8️⃣ Transactions

### What are Transactions?

Group of operations that execute together (all succeed or all fail).

**ACID in MongoDB:**
- **Atomicity**: All operations succeed or all fail
- **Consistency**: Data remains valid
- **Isolation**: Transactions don't interfere
- **Durability**: Committed changes persist

---

### Multi-Document Transactions

```javascript
const session = db.getMongo().startSession();

session.startTransaction();

try {
  // Deduct from account A
  db.accounts.updateOne(
    { _id: "A" },
    { $inc: { balance: -100 } },
    { session }
  );
  
  // Add to account B
  db.accounts.updateOne(
    { _id: "B" },
    { $inc: { balance: 100 } },
    { session }
  );
  
  session.commitTransaction();
} catch (error) {
  session.abortTransaction();
} finally {
  session.endSession();
}
```

**Real-life analogy:**
Like a bank transfer - money leaves one account and enters another, or neither happens.

---

### When to Use Transactions?

**✅ Use transactions for:**
- Financial operations (transfers, payments)
- Multi-document updates that must be atomic
- Operations across multiple collections

**❌ Avoid transactions when:**
- Single document updates (already atomic)
- Performance is critical (transactions add overhead)
- Can use embedded documents instead

---

## 🔹 9️⃣ Replication & Sharding

### Replication (High Availability)

**Replica Set:**
Group of MongoDB instances that maintain same data.

```
Primary (Read/Write)
    ↓ replicate
Secondary (Read only)
Secondary (Read only)
```

**Benefits:**
- ✅ High availability (automatic failover)
- ✅ Data redundancy
- ✅ Read scaling (read from secondaries)

**How it works:**
1. Primary receives all writes
2. Changes replicated to secondaries
3. If primary fails, secondary becomes primary

---

### Sharding (Horizontal Scaling)

**What is sharding?**
Distributing data across multiple servers.

```
App → Mongos (Router)
        ↓
    Shard 1 (users 1-1000)
    Shard 2 (users 1001-2000)
    Shard 3 (users 2001-3000)
```

**Benefits:**
- ✅ Handle massive datasets
- ✅ Distribute load across servers
- ✅ Scale horizontally

**Shard Key:**
Field used to distribute documents.

```javascript
// Shard collection by userId
sh.shardCollection("mydb.users", { userId: 1 });
```

**Choosing shard key:**
- ✅ High cardinality (many unique values)
- ✅ Evenly distributed
- ✅ Frequently used in queries

---

## 🔹 🔟 MongoDB Interview Questions

### Basic Questions

**1. What is MongoDB?**
> "MongoDB is a NoSQL document database that stores data in flexible JSON-like documents. It's designed for scalability, high performance, and flexible schemas."

**2. SQL vs MongoDB?**
> "SQL uses tables with fixed schemas and ACID transactions. MongoDB uses flexible documents, scales horizontally, and is better for unstructured data and rapid development."

**3. What is BSON?**
> "BSON is Binary JSON - MongoDB's internal format. It's faster to parse than JSON and supports additional data types like Date and ObjectId."

**4. Explain ObjectId.**
> "ObjectId is a 12-byte unique identifier automatically generated for each document. It contains timestamp, machine ID, and counter, making it globally unique."

**5. Embedding vs Referencing?**
> "Embedding stores related data in same document (faster reads, no joins). Referencing stores data separately (less duplication, better for large related data)."

---

### Intermediate Questions

**1. How does indexing work in MongoDB?**
> "Indexes create data structures (B-trees) that speed up queries. They're essential for large collections but slow down writes. Create indexes on frequently queried fields."

**2. Explain aggregation pipeline.**
> "Aggregation pipeline processes documents through stages like $match (filter), $group (aggregate), $sort (order). Each stage transforms data for the next stage."

**3. What are replica sets?**
> "Replica sets are groups of MongoDB instances maintaining same data. Primary handles writes, secondaries replicate data. Provides high availability and automatic failover."

**4. When to use transactions?**
> "Use transactions for multi-document operations that must be atomic, like financial transfers. Single document updates are already atomic and don't need transactions."

**5. How to optimize slow queries?**
> "Use indexes on query fields, use explain() to analyze performance, avoid large result sets, use projection to limit fields, consider sharding for massive datasets."

---

### Advanced Questions

**1. Explain sharding strategy.**
> "Sharding distributes data across servers using a shard key. Choose keys with high cardinality and even distribution. Avoid keys that cause hotspots (like timestamps)."

**2. How to handle schema changes?**
> "MongoDB's flexible schema allows gradual migrations. Use $set to add fields, application code handles multiple schema versions, migrate data in batches."

**3. Write concern vs Read concern?**
> "Write concern controls acknowledgment level (how many replicas must confirm write). Read concern controls data freshness (read from primary vs secondaries)."

**4. How to model many-to-many relationships?**
> "Store array of references in both collections, or create junction collection. For small datasets, embed arrays. For large datasets, use references."

**5. Explain covered queries.**
> "Covered query is satisfied entirely by index (no document lookup). All queried fields must be in index. Much faster than regular queries."

---

### Scenario-Based Questions

**1. Find duplicate emails:**
```javascript
db.users.aggregate([
  { $group: { _id: "$email", count: { $sum: 1 } } },
  { $match: { count: { $gt: 1 } } }
]);
```

**2. Find second highest salary:**
```javascript
db.employees.find().sort({ salary: -1 }).skip(1).limit(1);
```

**3. Update nested array element:**
```javascript
db.users.updateOne(
  { _id: 1, "hobbies.name": "reading" },
  { $set: { "hobbies.$.level": "advanced" } }
);
```

**4. Count documents by category:**
```javascript
db.products.aggregate([
  { $group: { _id: "$category", count: { $sum: 1 } } },
  { $sort: { count: -1 } }
]);
```

**5. Find users without orders:**
```javascript
db.users.aggregate([
  {
    $lookup: {
      from: "orders",
      localField: "_id",
      foreignField: "userId",
      as: "orders"
    }
  },
  { $match: { orders: { $size: 0 } } }
]);
```

---

## 🔹 1️⃣1️⃣ Best Practices

### Schema Design

- ✅ **Embed when data accessed together** (one-to-few)
- ✅ **Reference when data accessed independently** (one-to-many)
- ✅ **Avoid deep nesting** (max 2-3 levels)
- ✅ **Design for your queries** (optimize for read patterns)
- ❌ **Don't normalize like SQL** (embrace denormalization)

---

### Indexing

- ✅ **Index frequently queried fields**
- ✅ **Use compound indexes** for multi-field queries
- ✅ **Monitor index usage** with explain()
- ✅ **Remove unused indexes**
- ❌ **Don't over-index** (slows writes)

---

### Performance

- ✅ **Use projection** to limit returned fields
- ✅ **Use limit()** for large result sets
- ✅ **Use aggregation** instead of multiple queries
- ✅ **Enable profiler** to find slow queries
- ❌ **Avoid large documents** (> 16MB limit)

---

### Security

- ✅ **Enable authentication** (never run without auth)
- ✅ **Use role-based access control**
- ✅ **Encrypt data at rest and in transit**
- ✅ **Validate input** to prevent injection
- ❌ **Don't expose MongoDB to internet** (use firewall)

---

## 🎯 MongoDB vs SQL Quick Reference

| Feature | MongoDB | SQL |
|---------|---------|-----|
| **Data Model** | Documents (JSON) | Tables (rows/columns) |
| **Schema** | Flexible | Fixed |
| **Relationships** | Embedding/Referencing | Foreign keys |
| **Scaling** | Horizontal (sharding) | Vertical (bigger server) |
| **Transactions** | Multi-document (4.0+) | ACID by default |
| **Query Language** | MongoDB Query Language | SQL |
| **Joins** | $lookup (limited) | JOIN (powerful) |
| **Use Case** | Flexible data, high scale | Complex relationships, ACID |

---

## 📚 Study Tips for MongoDB

1. **Practice CRUD operations**: Master insert, find, update, delete
2. **Learn aggregation pipeline**: Most interview questions use aggregation
3. **Understand indexing**: Know when to use and how to optimize
4. **Master data modeling**: Embedding vs referencing decisions
5. **Practice scenarios**: Duplicates, second highest, joins, grouping
6. **Know trade-offs**: Flexibility vs consistency, performance vs storage
7. **Understand replication & sharding**: Essential for production systems
8. **Use MongoDB Atlas**: Free tier for practice

---

## 🚀 Conclusion

You now have a complete MongoDB guide covering:
- ✅ Core concepts with real-life analogies
- ✅ CRUD operations and query operators
- ✅ Indexing and performance optimization
- ✅ Aggregation framework
- ✅ Data modeling patterns
- ✅ Transactions, replication, sharding
- ✅ Interview questions and best practices

**Remember:**
> "MongoDB is about flexibility and scale. Design your schema for your queries, embrace denormalization, and use indexes wisely."

Good luck with your MongoDB interviews! 🚀
