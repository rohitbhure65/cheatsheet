# 🗄️ SQL — Complete Handbook: Basics to Advanced

> A beginner-friendly, comprehensive guide to learning SQL from scratch to production-ready skills.

---

## 📌 What is SQL?

**SQL (Structured Query Language)** is the standard language used to communicate with relational databases. It allows you to **create**, **read**, **update**, and **delete** data stored in tables.

### 🌍 Why is SQL Important?
- Powers almost every application that stores user data
- Used by developers, data analysts, data scientists, and DBAs worldwide
- One of the most in-demand skills in the tech industry
- Consistent syntax across different database systems

### 🏢 Where is SQL Used?
| Industry | Use Case |
|----------|----------|
| E-commerce | Orders, products, inventory management |
| Banking | Transactions, account management |
| Healthcare | Patient records, prescriptions |
| Social Media | Users, posts, relationships, feeds |
| Analytics | Reports, dashboards, business intelligence |

### 🛢️ Popular SQL Databases
| Database | Best For |
|----------|----------|
| **MySQL** | Web apps, open-source projects |
| **PostgreSQL** | Complex queries, enterprise apps |
| **SQLite** | Mobile apps, embedded databases |
| **SQL Server** | Microsoft ecosystem |
| **Oracle** | Large enterprise systems |

---

## 📋 Table of Contents

1. [SQL Basics](#1-sql-basics)
   - [Introduction to SQL](#11-introduction-to-sql)
   - [What is a Database?](#12-what-is-a-database)
   - [DBMS vs RDBMS](#13-dbms-vs-rdbms)
   - [SQL Syntax](#14-sql-syntax)
   - [SQL Data Types](#15-sql-data-types)
2. [Database Operations](#2-database-operations)
3. [CRUD Operations](#3-crud-operations)
4. [Filtering & Sorting](#4-filtering--sorting)
5. [SQL Operators](#5-sql-operators)
6. [Constraints](#6-constraints)
7. [Joins](#7-joins)
8. [Aggregate Functions](#8-aggregate-functions)
9. [Grouping](#9-grouping)
10. [Subqueries](#10-subqueries)
11. [Advanced SQL](#11-advanced-sql)
12. [Relationships](#12-relationships)
13. [Normalization](#13-normalization)
14. [SQL with Real Projects](#14-sql-with-real-projects)
15. [PostgreSQL Concepts](#15-postgresql-concepts)
16. [Performance Optimization](#16-performance-optimization)
17. [Security](#17-security)
18. [Backup & Migration](#18-backup--migration)
19. [Comparison Tables](#19-comparison-tables)
20. [Exercises](#20-exercises)
21. [Resources & Roadmap](#21-resources--roadmap)

---

## 1. SQL Basics

### 1.1 Introduction to SQL

**Definition:** SQL is a domain-specific language used to manage and manipulate relational databases.

SQL commands are grouped into categories:
- **DDL** — Data Definition Language (`CREATE`, `ALTER`, `DROP`)
- **DML** — Data Manipulation Language (`INSERT`, `UPDATE`, `DELETE`)
- **DQL** — Data Query Language (`SELECT`)
- **DCL** — Data Control Language (`GRANT`, `REVOKE`)
- **TCL** — Transaction Control Language (`COMMIT`, `ROLLBACK`)

> 💡 **Interview Tip:** Always be ready to name and explain the 5 SQL command categories with examples.

---

### 1.2 What is a Database?

**Definition:** A database is an organized collection of structured data stored electronically.

Think of a database as a filing cabinet:
- The **cabinet** = the database
- Each **drawer** = a table
- Each **folder** = a row (record)
- Each **label on the folder** = a column (field)

**Real-world example:** Instagram stores user profiles, posts, likes, and comments in a database.

---

### 1.3 DBMS vs RDBMS

| Feature | DBMS | RDBMS |
|---------|------|-------|
| Data Storage | Files | Tables |
| Relationships | Not supported | Supported via foreign keys |
| Normalization | No | Yes |
| SQL Support | No | Yes |
| Examples | File System, XML | MySQL, PostgreSQL, Oracle |

> 📝 **Note:** All modern production databases you'll work with are RDBMS.

---

### 1.4 SQL Syntax

**Basic rules:**
- SQL is **not case-sensitive** (`SELECT` = `select`), but writing keywords in UPPERCASE is convention
- Statements end with a **semicolon** `;`
- Strings use **single quotes** `'value'`
- Comments: `--` for single line, `/* */` for multi-line

```sql
-- This is a single-line comment

/*
  This is a
  multi-line comment
*/

-- Basic SELECT statement
SELECT column1, column2
FROM table_name
WHERE condition
ORDER BY column1;
```

---

### 1.5 SQL Data Types

#### Numeric Types
| Type | Description | Example |
|------|-------------|---------|
| `INT` | Whole numbers | `42` |
| `BIGINT` | Very large integers | `9999999999` |
| `DECIMAL(p,s)` | Exact decimal | `99.99` |
| `FLOAT` | Approximate decimal | `3.14` |

#### String Types
| Type | Description | Example |
|------|-------------|---------|
| `CHAR(n)` | Fixed-length string | `'M'` |
| `VARCHAR(n)` | Variable-length string | `'John'` |
| `TEXT` | Unlimited text | Long descriptions |

#### Date/Time Types
| Type | Description | Example |
|------|-------------|---------|
| `DATE` | Date only | `'2024-01-15'` |
| `TIME` | Time only | `'14:30:00'` |
| `DATETIME` | Date + Time | `'2024-01-15 14:30:00'` |
| `TIMESTAMP` | Date + Time + TZ | Auto-updated timestamps |

#### Other Types
| Type | Description |
|------|-------------|
| `BOOLEAN` | `TRUE` or `FALSE` |
| `BLOB` | Binary data (images, files) |
| `NULL` | Represents missing/unknown value |

> ⚠️ **Common Mistake:** Confusing `CHAR` and `VARCHAR`. Use `CHAR` only for fixed-length data (like country codes `'US'`). Use `VARCHAR` for everything else — it saves storage space.

---

## 2. Database Operations

### CREATE DATABASE

**Definition:** Creates a new database.

```sql
-- Create a new database
CREATE DATABASE shop_db;

-- Create only if it doesn't exist (safer)
CREATE DATABASE IF NOT EXISTS shop_db;

-- PostgreSQL: with encoding
CREATE DATABASE shop_db
  ENCODING 'UTF8'
  LC_COLLATE 'en_US.UTF-8';
```

**Best practice:** Always use `IF NOT EXISTS` to avoid errors in scripts.

---

### DROP DATABASE

**Definition:** Permanently deletes a database and all its data.

```sql
-- Delete a database (IRREVERSIBLE!)
DROP DATABASE shop_db;

-- Safer version
DROP DATABASE IF EXISTS shop_db;
```

> ⚠️ **Warning:** `DROP DATABASE` cannot be undone. Always back up before dropping.

---

### CREATE TABLE

**Definition:** Creates a new table with defined columns and data types.

```sql
-- Create a users table
CREATE TABLE users (
    id          INT PRIMARY KEY AUTO_INCREMENT,  -- unique identifier
    name        VARCHAR(100) NOT NULL,           -- required field
    email       VARCHAR(150) UNIQUE NOT NULL,    -- must be unique
    age         INT CHECK (age >= 18),           -- must be 18+
    created_at  DATETIME DEFAULT CURRENT_TIMESTAMP  -- auto-set on insert
);
```

**Best practice:** Always define a primary key, set NOT NULL on required fields, and use appropriate data type sizes.

---

### ALTER TABLE

**Definition:** Modifies an existing table's structure.

```sql
-- Add a new column
ALTER TABLE users ADD COLUMN phone VARCHAR(15);

-- Modify a column's data type
ALTER TABLE users MODIFY COLUMN phone VARCHAR(20);

-- Rename a column (MySQL 8+)
ALTER TABLE users RENAME COLUMN phone TO mobile;

-- Drop a column
ALTER TABLE users DROP COLUMN mobile;

-- Add a constraint
ALTER TABLE users ADD CONSTRAINT chk_age CHECK (age >= 0);
```

---

### DROP TABLE

**Definition:** Permanently deletes a table and all its data.

```sql
-- Drop a table
DROP TABLE users;

-- Safer version
DROP TABLE IF EXISTS users;
```

---

### TRUNCATE TABLE

**Definition:** Removes all rows from a table but keeps the table structure.

```sql
-- Remove all data, keep structure
TRUNCATE TABLE users;
```

| Operation | Removes Data | Removes Table | Can Rollback |
|-----------|-------------|---------------|--------------|
| `DELETE` | Yes (rows) | No | Yes |
| `TRUNCATE` | Yes (all rows) | No | No (usually) |
| `DROP` | Yes (all) | Yes | No |

---

## 3. CRUD Operations

CRUD = **C**reate, **R**ead, **U**pdate, **D**elete — the four fundamental database operations.

### INSERT

**Definition:** Adds new rows to a table.

```sql
-- Insert a single row
INSERT INTO users (name, email, age)
VALUES ('Rohit Sharma', 'rohit@example.com', 25);

-- Insert multiple rows at once (more efficient)
INSERT INTO users (name, email, age)
VALUES
    ('Priya Patel', 'priya@example.com', 28),
    ('Arjun Singh', 'arjun@example.com', 30),
    ('Meera Nair', 'meera@example.com', 22);

-- Insert from another table
INSERT INTO archived_users (name, email)
SELECT name, email FROM users WHERE age > 60;
```

> ⚠️ **Common Mistake:** Not specifying column names. Always list the columns — it makes code readable and prevents bugs when table structure changes.

---

### SELECT

**Definition:** Retrieves data from one or more tables.

```sql
-- Select all columns
SELECT * FROM users;

-- Select specific columns
SELECT name, email FROM users;

-- Select with alias (rename output column)
SELECT name AS full_name, email AS contact FROM users;

-- Select with calculation
SELECT name, age, age + 5 AS age_in_5_years FROM users;

-- Select distinct values (no duplicates)
SELECT DISTINCT city FROM users;
```

> 💡 **Best Practice:** Avoid `SELECT *` in production — always name the columns you need. It's faster and more maintainable.

---

### UPDATE

**Definition:** Modifies existing rows in a table.

```sql
-- Update a single user
UPDATE users
SET email = 'new_email@example.com'
WHERE id = 1;

-- Update multiple columns
UPDATE users
SET email = 'rohit_new@example.com',
    age = 26
WHERE name = 'Rohit Sharma';

-- Update all rows (use with caution!)
UPDATE users
SET is_active = TRUE;
```

> ⚠️ **Critical:** ALWAYS use `WHERE` with `UPDATE`. Without it, every row in the table gets updated.

```sql
-- DANGEROUS — updates every row!
UPDATE users SET age = 0;

-- SAFE — only updates one row
UPDATE users SET age = 0 WHERE id = 5;
```

---

### DELETE

**Definition:** Removes rows from a table.

```sql
-- Delete a specific user
DELETE FROM users WHERE id = 3;

-- Delete based on condition
DELETE FROM users WHERE age < 18;

-- Delete all rows (same as TRUNCATE but slower)
DELETE FROM users;
```

> ⚠️ **Critical:** Always use `WHERE` with `DELETE`. Test your `WHERE` condition with a `SELECT` first before deleting.

```sql
-- Step 1: Preview what will be deleted
SELECT * FROM users WHERE age < 18;

-- Step 2: If correct, then delete
DELETE FROM users WHERE age < 18;
```

---

## 4. Filtering & Sorting

### WHERE Clause

**Definition:** Filters rows based on a condition.

```sql
-- Basic comparison
SELECT * FROM users WHERE age = 25;
SELECT * FROM users WHERE age > 20;
SELECT * FROM users WHERE age != 30;

-- Combine conditions with AND / OR
SELECT * FROM users WHERE age > 20 AND city = 'Mumbai';
SELECT * FROM users WHERE city = 'Delhi' OR city = 'Mumbai';

-- Negate with NOT
SELECT * FROM users WHERE NOT city = 'Delhi';
```

---

### ORDER BY

**Definition:** Sorts the result set by one or more columns.

```sql
-- Sort ascending (default)
SELECT * FROM users ORDER BY name ASC;

-- Sort descending
SELECT * FROM users ORDER BY age DESC;

-- Sort by multiple columns
SELECT * FROM products ORDER BY category ASC, price DESC;
```

---

### LIMIT

**Definition:** Restricts the number of rows returned.

```sql
-- Return only 10 rows
SELECT * FROM users LIMIT 10;

-- Pagination: skip 20 rows, return next 10 (page 3)
SELECT * FROM users LIMIT 10 OFFSET 20;

-- SQL Server equivalent
SELECT TOP 10 * FROM users;
```

**Real-world use case:** Pagination in web apps — showing 20 products per page.

---

### DISTINCT

**Definition:** Returns only unique values, eliminating duplicates.

```sql
-- Get all unique cities
SELECT DISTINCT city FROM users;

-- Distinct combination of columns
SELECT DISTINCT city, country FROM users;
```

---

### BETWEEN

**Definition:** Filters rows within a range (inclusive).

```sql
-- Users aged 20 to 30
SELECT * FROM users WHERE age BETWEEN 20 AND 30;

-- Products within a price range
SELECT * FROM products WHERE price BETWEEN 100.00 AND 500.00;

-- Date range
SELECT * FROM orders WHERE order_date BETWEEN '2024-01-01' AND '2024-12-31';
```

---

### IN

**Definition:** Filters rows matching any value in a list.

```sql
-- Users from specific cities
SELECT * FROM users WHERE city IN ('Mumbai', 'Delhi', 'Bangalore');

-- Equivalent to:
SELECT * FROM users WHERE city = 'Mumbai' OR city = 'Delhi' OR city = 'Bangalore';

-- NOT IN — exclude values
SELECT * FROM users WHERE city NOT IN ('Mumbai', 'Delhi');
```

---

### LIKE

**Definition:** Pattern matching for strings (used with `WHERE`).

```sql
-- Names starting with 'R'
SELECT * FROM users WHERE name LIKE 'R%';

-- Names ending with 'a'
SELECT * FROM users WHERE name LIKE '%a';

-- Names containing 'oh'
SELECT * FROM users WHERE name LIKE '%oh%';

-- Exactly 4 characters
SELECT * FROM users WHERE code LIKE '____';
```

### Wildcards

| Symbol | Meaning | Example |
|--------|---------|---------|
| `%` | Zero or more characters | `'R%'` → Rohit, Ram, R |
| `_` | Exactly one character | `'R_m'` → Ram, Rim |

> 💡 **Performance Note:** `LIKE '%text%'` (leading wildcard) cannot use indexes and is slow on large tables. Use full-text search for better performance.

---

## 5. SQL Operators

### Arithmetic Operators

```sql
SELECT price, price * 1.18 AS price_with_gst FROM products;
SELECT 100 / 4;      -- Result: 25
SELECT 10 % 3;       -- Result: 1 (remainder)
```

| Operator | Description |
|----------|-------------|
| `+` | Addition |
| `-` | Subtraction |
| `*` | Multiplication |
| `/` | Division |
| `%` | Modulo (remainder) |

---

### Comparison Operators

| Operator | Meaning | Example |
|----------|---------|---------|
| `=` | Equal | `age = 25` |
| `!=` or `<>` | Not equal | `age != 25` |
| `>` | Greater than | `age > 18` |
| `<` | Less than | `price < 1000` |
| `>=` | Greater than or equal | `rating >= 4` |
| `<=` | Less than or equal | `stock <= 5` |

---

### Logical Operators

```sql
-- AND: both conditions must be true
SELECT * FROM users WHERE age > 18 AND city = 'Mumbai';

-- OR: at least one condition must be true
SELECT * FROM users WHERE city = 'Delhi' OR city = 'Chennai';

-- NOT: negates the condition
SELECT * FROM products WHERE NOT category = 'Electronics';
```

---

### NULL Operators

```sql
-- Find rows where phone is not set
SELECT * FROM users WHERE phone IS NULL;

-- Find rows where phone IS set
SELECT * FROM users WHERE phone IS NOT NULL;

-- Replace NULL with a default value
SELECT name, COALESCE(phone, 'N/A') AS phone FROM users;
```

> ⚠️ **Common Mistake:** Using `= NULL` instead of `IS NULL`. In SQL, `NULL = NULL` is always `FALSE` because NULL represents "unknown." Always use `IS NULL` or `IS NOT NULL`.

```sql
-- WRONG
SELECT * FROM users WHERE phone = NULL;

-- CORRECT
SELECT * FROM users WHERE phone IS NULL;
```

---

## 6. Constraints

Constraints enforce rules on the data in a table, ensuring accuracy and reliability.

### PRIMARY KEY

**Definition:** Uniquely identifies each row. Cannot be NULL or duplicate.

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,          -- simple primary key
    name VARCHAR(100)
);

-- Composite primary key (two columns together are unique)
CREATE TABLE order_items (
    order_id INT,
    product_id INT,
    quantity INT,
    PRIMARY KEY (order_id, product_id)
);
```

---

### FOREIGN KEY

**Definition:** Links a column to the primary key of another table, enforcing referential integrity.

```sql
CREATE TABLE orders (
    id         INT PRIMARY KEY AUTO_INCREMENT,
    user_id    INT NOT NULL,
    total      DECIMAL(10,2),
    -- user_id must exist in users.id
    FOREIGN KEY (user_id) REFERENCES users(id)
        ON DELETE CASCADE    -- delete orders when user is deleted
        ON UPDATE CASCADE    -- update if user's id changes
);
```

**ON DELETE options:**
| Option | Behavior |
|--------|----------|
| `CASCADE` | Delete child rows automatically |
| `SET NULL` | Set foreign key to NULL |
| `RESTRICT` | Prevent deletion of parent |
| `NO ACTION` | Same as RESTRICT |

---

### UNIQUE

**Definition:** Ensures all values in a column are different.

```sql
CREATE TABLE users (
    id    INT PRIMARY KEY,
    email VARCHAR(150) UNIQUE  -- no two users can have same email
);

-- Multiple unique columns
ALTER TABLE users ADD CONSTRAINT uq_username UNIQUE (username);
```

> **PRIMARY KEY vs UNIQUE:** A table can have only ONE primary key but MULTIPLE unique constraints. Primary key cannot be NULL; unique can be NULL (one null per column in most databases).

---

### NOT NULL

**Definition:** Ensures a column cannot have a NULL value.

```sql
CREATE TABLE products (
    id    INT PRIMARY KEY,
    name  VARCHAR(100) NOT NULL,  -- name is required
    price DECIMAL(10,2) NOT NULL  -- price is required
);
```

---

### CHECK

**Definition:** Validates that values in a column satisfy a condition.

```sql
CREATE TABLE employees (
    id     INT PRIMARY KEY,
    name   VARCHAR(100),
    salary DECIMAL(10,2) CHECK (salary > 0),
    age    INT CHECK (age BETWEEN 18 AND 65)
);
```

---

### DEFAULT

**Definition:** Sets a default value when no value is provided on insert.

```sql
CREATE TABLE posts (
    id         INT PRIMARY KEY,
    title      VARCHAR(200),
    is_published BOOLEAN DEFAULT FALSE,
    views      INT DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

### AUTO_INCREMENT / SERIAL

**Definition:** Automatically generates a unique number for each new row.

```sql
-- MySQL
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100)
);

-- PostgreSQL
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100)
);

-- PostgreSQL (modern syntax)
CREATE TABLE users (
    id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    name VARCHAR(100)
);
```

---

## 7. Joins

Joins combine rows from two or more tables based on a related column.

**Sample Tables for all examples:**

```sql
-- users table
| id | name    | city    |
|----|---------|---------|
|  1 | Rohit   | Mumbai  |
|  2 | Priya   | Delhi   |
|  3 | Arjun   | Chennai |

-- orders table
| id | user_id | product  |
|----|---------|----------|
|  1 |       1 | Laptop   |
|  2 |       1 | Phone    |
|  3 |       4 | Tablet   |  <-- user_id 4 doesn't exist in users
```

---

### INNER JOIN

**Definition:** Returns rows that have matching values in BOTH tables.

```sql
SELECT u.name, o.product
FROM users u
INNER JOIN orders o ON u.id = o.user_id;

-- Result:
-- Rohit | Laptop
-- Rohit | Phone
-- (Priya and Arjun excluded — no orders)
-- (Tablet excluded — user_id 4 doesn't exist)
```

**Real-world use case:** Show all orders with customer names — only orders that have a valid customer.

---

### LEFT JOIN

**Definition:** Returns ALL rows from the left table and matching rows from the right table. Unmatched right rows show NULL.

```sql
SELECT u.name, o.product
FROM users u
LEFT JOIN orders o ON u.id = o.user_id;

-- Result:
-- Rohit  | Laptop
-- Rohit  | Phone
-- Priya  | NULL   <-- Priya has no orders
-- Arjun  | NULL   <-- Arjun has no orders
```

**Real-world use case:** Show all users, even those who haven't placed any orders yet.

---

### RIGHT JOIN

**Definition:** Returns ALL rows from the right table and matching rows from the left table.

```sql
SELECT u.name, o.product
FROM users u
RIGHT JOIN orders o ON u.id = o.user_id;

-- Result:
-- Rohit | Laptop
-- Rohit | Phone
-- NULL  | Tablet  <-- order with no matching user
```

> 💡 **Tip:** A RIGHT JOIN is rarely used. Most developers rewrite it as a LEFT JOIN by swapping the table order — it's easier to read.

---

### FULL JOIN (FULL OUTER JOIN)

**Definition:** Returns ALL rows from both tables, with NULLs where there is no match.

```sql
-- PostgreSQL / SQL Server
SELECT u.name, o.product
FROM users u
FULL OUTER JOIN orders o ON u.id = o.user_id;

-- MySQL workaround (MySQL doesn't support FULL JOIN directly)
SELECT u.name, o.product FROM users u LEFT JOIN orders o ON u.id = o.user_id
UNION
SELECT u.name, o.product FROM users u RIGHT JOIN orders o ON u.id = o.user_id;
```

---

### CROSS JOIN

**Definition:** Returns the Cartesian product — every row from the first table combined with every row from the second table.

```sql
-- 3 sizes × 3 colors = 9 combinations
SELECT s.size, c.color
FROM sizes s
CROSS JOIN colors c;
```

**Real-world use case:** Generating all possible product variants (size + color combinations).

---

### SELF JOIN

**Definition:** Joins a table with itself. Used for hierarchical or comparative data.

```sql
-- Find employees and their managers (both in same table)
SELECT
    e.name AS employee,
    m.name AS manager
FROM employees e
LEFT JOIN employees m ON e.manager_id = m.id;
```

**Real-world use case:** Org charts, finding pairs (users who live in the same city).

---

### Join Visual Summary

```
Table A:  [1][2][3]
Table B:  [2][3][4]

INNER JOIN:  [2][3]           -- only matches
LEFT JOIN:   [1][2][3]        -- all of A + matches from B
RIGHT JOIN:  [2][3][4]        -- matches from A + all of B
FULL JOIN:   [1][2][3][4]     -- everything
```

---

## 8. Aggregate Functions

Aggregate functions perform calculations on a set of rows and return a single value.

### COUNT()

```sql
-- Count all rows
SELECT COUNT(*) FROM users;

-- Count non-NULL values only
SELECT COUNT(phone) FROM users;

-- Count with condition
SELECT COUNT(*) FROM orders WHERE status = 'completed';
```

### SUM()

```sql
-- Total revenue
SELECT SUM(amount) AS total_revenue FROM orders;

-- Total by category
SELECT category, SUM(price) AS total FROM products GROUP BY category;
```

### AVG()

```sql
-- Average order value
SELECT AVG(amount) AS avg_order FROM orders;

-- Round to 2 decimal places
SELECT ROUND(AVG(rating), 2) AS avg_rating FROM reviews;
```

### MIN() and MAX()

```sql
-- Cheapest and most expensive product
SELECT MIN(price) AS cheapest, MAX(price) AS most_expensive FROM products;

-- Earliest and latest order
SELECT MIN(created_at) AS first_order, MAX(created_at) AS last_order FROM orders;
```

> 📝 **Note:** `COUNT(*)` counts all rows including NULLs. `COUNT(column)` counts only non-NULL values. This distinction matters for optional fields.

---

## 9. Grouping

### GROUP BY

**Definition:** Groups rows that have the same values in specified columns, usually used with aggregate functions.

```sql
-- Number of users per city
SELECT city, COUNT(*) AS user_count
FROM users
GROUP BY city;

-- Total sales per product
SELECT product_id, SUM(quantity) AS total_sold
FROM order_items
GROUP BY product_id;

-- Multiple columns
SELECT city, gender, COUNT(*) AS count
FROM users
GROUP BY city, gender;
```

> ⚠️ **Rule:** Every column in `SELECT` must either be in `GROUP BY` or inside an aggregate function. This is the most common GROUP BY error.

```sql
-- WRONG: 'name' is not in GROUP BY or an aggregate
SELECT name, city, COUNT(*) FROM users GROUP BY city;

-- CORRECT
SELECT city, COUNT(*) FROM users GROUP BY city;
```

---

### HAVING

**Definition:** Filters groups after `GROUP BY` (like `WHERE` but for groups).

```sql
-- Cities with more than 100 users
SELECT city, COUNT(*) AS user_count
FROM users
GROUP BY city
HAVING COUNT(*) > 100;

-- Products with average rating above 4
SELECT product_id, AVG(rating) AS avg_rating
FROM reviews
GROUP BY product_id
HAVING AVG(rating) >= 4.0
ORDER BY avg_rating DESC;
```

### WHERE vs HAVING

| Clause | Filters | Runs Before/After GROUP BY |
|--------|---------|---------------------------|
| `WHERE` | Individual rows | Before |
| `HAVING` | Groups | After |

```sql
-- Combined example
SELECT city, COUNT(*) AS user_count
FROM users
WHERE age >= 18           -- filter rows first
GROUP BY city
HAVING COUNT(*) > 50      -- then filter groups
ORDER BY user_count DESC;
```

---

## 10. Subqueries

### Nested Queries

**Definition:** A query inside another query.

```sql
-- Find users who have placed orders
SELECT name FROM users
WHERE id IN (SELECT DISTINCT user_id FROM orders);

-- Find products more expensive than average
SELECT name, price FROM products
WHERE price > (SELECT AVG(price) FROM products);

-- Subquery in FROM clause (derived table)
SELECT city, avg_age
FROM (
    SELECT city, AVG(age) AS avg_age
    FROM users
    GROUP BY city
) AS city_stats
WHERE avg_age > 25;
```

---

### Correlated Subqueries

**Definition:** A subquery that references columns from the outer query — runs once per row.

```sql
-- For each user, find their order count
SELECT
    name,
    (SELECT COUNT(*) FROM orders o WHERE o.user_id = u.id) AS order_count
FROM users u;

-- Find users whose total spend is above average
SELECT name FROM users u
WHERE (
    SELECT SUM(amount) FROM orders o WHERE o.user_id = u.id
) > (SELECT AVG(total_spent) FROM user_stats);
```

> 💡 **Performance:** Correlated subqueries run for EVERY row in the outer query. For large tables, rewrite them as JOINs for better performance.

---

## 11. Advanced SQL

### Views

**Definition:** A virtual table based on a saved SELECT query. The view always shows current data.

```sql
-- Create a view
CREATE VIEW active_users AS
SELECT id, name, email
FROM users
WHERE is_active = TRUE;

-- Use the view like a table
SELECT * FROM active_users;

-- Update a view
CREATE OR REPLACE VIEW active_users AS
SELECT id, name, email, city
FROM users
WHERE is_active = TRUE;

-- Drop a view
DROP VIEW IF EXISTS active_users;
```

**Benefits:** Simplifies complex queries, provides a security layer (hide sensitive columns), reusable logic.

---

### Indexes

**Definition:** A data structure that speeds up data retrieval at the cost of extra storage and slightly slower writes.

```sql
-- Create index on email (for fast lookups)
CREATE INDEX idx_users_email ON users(email);

-- Unique index (also enforces uniqueness)
CREATE UNIQUE INDEX idx_users_username ON users(username);

-- Composite index (for queries filtering on both columns)
CREATE INDEX idx_orders_user_status ON orders(user_id, status);

-- Drop an index
DROP INDEX idx_users_email ON users;       -- MySQL
DROP INDEX idx_users_email;                -- PostgreSQL
```

**When to add indexes:**
- Columns used frequently in `WHERE`, `JOIN`, `ORDER BY`
- Foreign key columns
- Columns with high cardinality (many unique values)

**When NOT to add indexes:**
- Small tables
- Columns rarely queried
- Tables with heavy write operations (indexes slow down INSERT/UPDATE/DELETE)

---

### Stored Procedures

**Definition:** A saved block of SQL code that can be executed by name with parameters.

```sql
-- MySQL stored procedure
DELIMITER //

CREATE PROCEDURE get_user_orders(IN user_id INT)
BEGIN
    SELECT o.id, o.total, o.created_at
    FROM orders o
    WHERE o.user_id = user_id
    ORDER BY o.created_at DESC;
END //

DELIMITER ;

-- Call the procedure
CALL get_user_orders(5);
```

---

### Functions

**Definition:** Similar to procedures but always returns a value and can be used in SELECT.

```sql
-- MySQL function
DELIMITER //

CREATE FUNCTION calculate_tax(price DECIMAL(10,2))
RETURNS DECIMAL(10,2)
DETERMINISTIC
BEGIN
    RETURN price * 0.18;
END //

DELIMITER ;

-- Use in a query
SELECT name, price, calculate_tax(price) AS tax FROM products;
```

---

### Triggers

**Definition:** Automatically runs SQL code before or after an INSERT, UPDATE, or DELETE.

```sql
-- Log every user deletion to an audit table
CREATE TRIGGER before_user_delete
BEFORE DELETE ON users
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (action, user_id, deleted_at)
    VALUES ('DELETE', OLD.id, NOW());
END;
```

**Trigger timing options:**
| When | Action |
|------|--------|
| `BEFORE INSERT` | Before a row is inserted |
| `AFTER INSERT` | After a row is inserted |
| `BEFORE UPDATE` | Before a row is updated |
| `AFTER DELETE` | After a row is deleted |

---

### Transactions

**Definition:** A group of SQL operations that execute as a single unit — all succeed or all fail.

```sql
-- Example: Transfer money between accounts
START TRANSACTION;

UPDATE accounts SET balance = balance - 5000 WHERE id = 1;  -- debit
UPDATE accounts SET balance = balance + 5000 WHERE id = 2;  -- credit

-- Check if everything is OK
COMMIT;    -- save changes permanently

-- If something went wrong:
-- ROLLBACK;   -- undo all changes
```

```sql
-- With error handling (MySQL)
START TRANSACTION;

UPDATE accounts SET balance = balance - 5000 WHERE id = 1;

-- If balance goes negative, rollback
IF (SELECT balance FROM accounts WHERE id = 1) < 0 THEN
    ROLLBACK;
ELSE
    COMMIT;
END IF;
```

---

### ACID Properties

| Property | Meaning | Example |
|----------|---------|---------|
| **Atomicity** | All operations succeed or all fail | Payment deducted but not credited → rolled back |
| **Consistency** | Database stays in valid state | Balance can't go below 0 |
| **Isolation** | Concurrent transactions don't interfere | Two users booking the last seat |
| **Durability** | Committed changes survive crashes | Committed data survives power failure |

> 💡 **Interview Tip:** ACID is one of the most common database interview topics. Memorize the acronym and give a real-world banking example for each property.

---

## 12. Relationships

### One-to-One

Each row in Table A relates to exactly one row in Table B.

```sql
-- Each user has one profile
CREATE TABLE users (id INT PRIMARY KEY, name VARCHAR(100));
CREATE TABLE user_profiles (
    id      INT PRIMARY KEY,
    user_id INT UNIQUE,           -- UNIQUE enforces one-to-one
    bio     TEXT,
    avatar  VARCHAR(200),
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

**Example:** User ↔ Passport, Employee ↔ Desk

---

### One-to-Many

One row in Table A can relate to many rows in Table B.

```sql
-- One user can have many orders
CREATE TABLE users (id INT PRIMARY KEY, name VARCHAR(100));
CREATE TABLE orders (
    id      INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,                  -- no UNIQUE — allows multiple orders per user
    total   DECIMAL(10,2),
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

**Example:** User → Orders, Author → Books, Department → Employees

---

### Many-to-Many

Many rows in Table A can relate to many rows in Table B — requires a **junction table**.

```sql
-- Students enroll in many courses; courses have many students
CREATE TABLE students (id INT PRIMARY KEY, name VARCHAR(100));
CREATE TABLE courses  (id INT PRIMARY KEY, title VARCHAR(200));

-- Junction table
CREATE TABLE enrollments (
    student_id INT,
    course_id  INT,
    enrolled_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY (student_id, course_id),
    FOREIGN KEY (student_id) REFERENCES students(id),
    FOREIGN KEY (course_id)  REFERENCES courses(id)
);
```

**Example:** Students ↔ Courses, Products ↔ Tags, Users ↔ Roles

---

## 13. Normalization

Normalization organizes a database to reduce redundancy and improve data integrity.

### 1NF — First Normal Form

**Rule:** Each column must contain atomic (indivisible) values. No repeating groups.

```sql
-- VIOLATES 1NF: multiple phones in one column
| id | name  | phones              |
|----|-------|---------------------|
|  1 | Rohit | 9876543210,8765432109|

-- CORRECT 1NF
CREATE TABLE user_phones (
    user_id INT,
    phone   VARCHAR(15),
    PRIMARY KEY (user_id, phone)
);
```

---

### 2NF — Second Normal Form

**Rule:** Must be in 1NF + every non-key column must depend on the ENTIRE primary key (no partial dependency). Applies only to composite primary keys.

```sql
-- VIOLATES 2NF: 'product_name' depends only on product_id, not on (order_id, product_id)
| order_id | product_id | product_name | quantity |

-- CORRECT 2NF: move product_name to its own table
CREATE TABLE products (product_id INT PRIMARY KEY, product_name VARCHAR(100));
CREATE TABLE order_items (order_id INT, product_id INT, quantity INT,
    PRIMARY KEY (order_id, product_id));
```

---

### 3NF — Third Normal Form

**Rule:** Must be in 2NF + no transitive dependencies (non-key column should not depend on another non-key column).

```sql
-- VIOLATES 3NF: zip_code → city (city depends on zip_code, not on user_id)
| user_id | name  | zip_code | city    |

-- CORRECT 3NF: move city to a zip_codes table
CREATE TABLE zip_codes (zip_code VARCHAR(10) PRIMARY KEY, city VARCHAR(100));
CREATE TABLE users (user_id INT PRIMARY KEY, name VARCHAR(100), zip_code VARCHAR(10),
    FOREIGN KEY (zip_code) REFERENCES zip_codes(zip_code));
```

---

### BCNF — Boyce-Codd Normal Form

**Rule:** A stricter version of 3NF. For every functional dependency X → Y, X must be a superkey (can uniquely identify a row).

> 📝 **Note:** BCNF is mostly theoretical. In practice, 3NF is sufficient for most production databases.

---

## 14. SQL with Real Projects

### User Authentication Tables

```sql
CREATE TABLE users (
    id            INT PRIMARY KEY AUTO_INCREMENT,
    username      VARCHAR(50) UNIQUE NOT NULL,
    email         VARCHAR(150) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,       -- NEVER store plain text passwords
    is_verified   BOOLEAN DEFAULT FALSE,
    created_at    TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at    TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

CREATE TABLE sessions (
    id         VARCHAR(128) PRIMARY KEY,        -- session token
    user_id    INT NOT NULL,
    expires_at TIMESTAMP NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);

CREATE TABLE password_resets (
    id         INT PRIMARY KEY AUTO_INCREMENT,
    user_id    INT NOT NULL,
    token      VARCHAR(128) UNIQUE NOT NULL,
    expires_at TIMESTAMP NOT NULL,
    used       BOOLEAN DEFAULT FALSE,
    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
```

---

### E-commerce Database

```sql
CREATE TABLE categories (
    id        INT PRIMARY KEY AUTO_INCREMENT,
    name      VARCHAR(100) NOT NULL,
    parent_id INT,                              -- for subcategories
    FOREIGN KEY (parent_id) REFERENCES categories(id)
);

CREATE TABLE products (
    id          INT PRIMARY KEY AUTO_INCREMENT,
    category_id INT,
    name        VARCHAR(200) NOT NULL,
    description TEXT,
    price       DECIMAL(10,2) NOT NULL CHECK (price >= 0),
    stock       INT DEFAULT 0 CHECK (stock >= 0),
    is_active   BOOLEAN DEFAULT TRUE,
    created_at  TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (category_id) REFERENCES categories(id)
);

CREATE TABLE orders (
    id         INT PRIMARY KEY AUTO_INCREMENT,
    user_id    INT NOT NULL,
    status     ENUM('pending','confirmed','shipped','delivered','cancelled') DEFAULT 'pending',
    total      DECIMAL(10,2) NOT NULL,
    address    TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id)
);

CREATE TABLE order_items (
    id         INT PRIMARY KEY AUTO_INCREMENT,
    order_id   INT NOT NULL,
    product_id INT NOT NULL,
    quantity   INT NOT NULL CHECK (quantity > 0),
    unit_price DECIMAL(10,2) NOT NULL,          -- snapshot price at time of purchase
    FOREIGN KEY (order_id)   REFERENCES orders(id) ON DELETE CASCADE,
    FOREIGN KEY (product_id) REFERENCES products(id)
);
```

---

### Blogging Platform Database

```sql
CREATE TABLE authors (
    id       INT PRIMARY KEY AUTO_INCREMENT,
    name     VARCHAR(100) NOT NULL,
    email    VARCHAR(150) UNIQUE NOT NULL,
    bio      TEXT
);

CREATE TABLE posts (
    id           INT PRIMARY KEY AUTO_INCREMENT,
    author_id    INT NOT NULL,
    title        VARCHAR(300) NOT NULL,
    slug         VARCHAR(300) UNIQUE NOT NULL,   -- URL-friendly title
    content      LONGTEXT,
    status       ENUM('draft','published','archived') DEFAULT 'draft',
    published_at TIMESTAMP,
    created_at   TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (author_id) REFERENCES authors(id)
);

CREATE TABLE tags (id INT PRIMARY KEY AUTO_INCREMENT, name VARCHAR(50) UNIQUE NOT NULL);

CREATE TABLE post_tags (
    post_id INT, tag_id INT,
    PRIMARY KEY (post_id, tag_id),
    FOREIGN KEY (post_id) REFERENCES posts(id) ON DELETE CASCADE,
    FOREIGN KEY (tag_id)  REFERENCES tags(id)  ON DELETE CASCADE
);

CREATE TABLE comments (
    id         INT PRIMARY KEY AUTO_INCREMENT,
    post_id    INT NOT NULL,
    user_id    INT NOT NULL,
    parent_id  INT,                             -- for nested replies
    content    TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (post_id)   REFERENCES posts(id) ON DELETE CASCADE,
    FOREIGN KEY (parent_id) REFERENCES comments(id) ON DELETE CASCADE
);
```

---

### School Management Database

```sql
CREATE TABLE departments (id INT PRIMARY KEY AUTO_INCREMENT, name VARCHAR(100) NOT NULL);

CREATE TABLE teachers (
    id            INT PRIMARY KEY AUTO_INCREMENT,
    department_id INT,
    name          VARCHAR(100) NOT NULL,
    email         VARCHAR(150) UNIQUE,
    FOREIGN KEY (department_id) REFERENCES departments(id)
);

CREATE TABLE students (
    id           INT PRIMARY KEY AUTO_INCREMENT,
    roll_number  VARCHAR(20) UNIQUE NOT NULL,
    name         VARCHAR(100) NOT NULL,
    date_of_birth DATE,
    email        VARCHAR(150) UNIQUE
);

CREATE TABLE courses (
    id         INT PRIMARY KEY AUTO_INCREMENT,
    teacher_id INT,
    name       VARCHAR(200) NOT NULL,
    credits    INT DEFAULT 3,
    FOREIGN KEY (teacher_id) REFERENCES teachers(id)
);

CREATE TABLE enrollments (
    student_id INT,
    course_id  INT,
    grade      DECIMAL(4,2),
    PRIMARY KEY (student_id, course_id),
    FOREIGN KEY (student_id) REFERENCES students(id),
    FOREIGN KEY (course_id)  REFERENCES courses(id)
);
```

---

## 15. PostgreSQL Concepts

### SERIAL / IDENTITY

```sql
-- Legacy approach
CREATE TABLE users (id SERIAL PRIMARY KEY, name VARCHAR(100));

-- Modern PostgreSQL (recommended)
CREATE TABLE users (
    id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    name VARCHAR(100)
);
```

---

### UUID

```sql
-- Enable extension
CREATE EXTENSION IF NOT EXISTS "pgcrypto";

CREATE TABLE users (
    id   UUID DEFAULT gen_random_uuid() PRIMARY KEY,
    name VARCHAR(100)
);
```

**UUID vs INT:** Use UUID when you need distributed systems, public-facing IDs, or merging data from multiple databases.

---

### JSON & JSONB

```sql
CREATE TABLE products (
    id         SERIAL PRIMARY KEY,
    name       VARCHAR(200),
    attributes JSONB           -- JSONB is binary, indexed, faster than JSON
);

-- Insert JSON data
INSERT INTO products (name, attributes)
VALUES ('Laptop', '{"brand": "Dell", "ram": 16, "tags": ["gaming", "work"]}');

-- Query JSON fields
SELECT name, attributes->>'brand' AS brand FROM products;

-- Query nested JSON
SELECT name, attributes->'specs'->>'cpu' AS cpu FROM products;

-- Filter by JSON value
SELECT * FROM products WHERE attributes->>'brand' = 'Dell';

-- Index on JSONB field
CREATE INDEX idx_products_brand ON products ((attributes->>'brand'));
```

---

### ARRAY Data Type

```sql
CREATE TABLE posts (
    id   SERIAL PRIMARY KEY,
    tags TEXT[]
);

INSERT INTO posts (tags) VALUES (ARRAY['sql', 'postgresql', 'database']);

-- Query: find posts with 'sql' tag
SELECT * FROM posts WHERE 'sql' = ANY(tags);
```

---

### ENUM Types

```sql
-- Create custom ENUM type
CREATE TYPE order_status AS ENUM ('pending', 'confirmed', 'shipped', 'delivered', 'cancelled');

CREATE TABLE orders (
    id     SERIAL PRIMARY KEY,
    status order_status DEFAULT 'pending'
);

-- Add a new value to ENUM
ALTER TYPE order_status ADD VALUE 'refunded';
```

---

## 16. Performance Optimization

### Query Optimization

```sql
-- Use EXPLAIN to understand query execution
EXPLAIN SELECT * FROM users WHERE email = 'rohit@example.com';

-- EXPLAIN ANALYZE — actually runs the query and shows real timings
EXPLAIN ANALYZE SELECT * FROM orders WHERE user_id = 5;
```

**Reading EXPLAIN output — watch for:**
- `Seq Scan` = full table scan (slow on large tables) → needs an index
- `Index Scan` = using index (fast)
- High `cost=` values → potential optimization target

---

### Indexing Tips

```sql
-- Add index on frequently queried foreign keys
CREATE INDEX idx_orders_user_id ON orders(user_id);

-- Composite index for frequent multi-column queries
-- Good for: WHERE status = 'shipped' AND user_id = 5
CREATE INDEX idx_orders_status_user ON orders(status, user_id);

-- Partial index — index only a subset of rows
-- Great for: WHERE is_active = TRUE (if most rows are inactive)
CREATE INDEX idx_active_users ON users(email) WHERE is_active = TRUE;
```

---

### Avoiding Slow Queries

```sql
-- SLOW: function on indexed column disables the index
SELECT * FROM users WHERE YEAR(created_at) = 2024;

-- FAST: use range instead
SELECT * FROM users WHERE created_at BETWEEN '2024-01-01' AND '2024-12-31';

-- SLOW: leading wildcard prevents index use
SELECT * FROM users WHERE name LIKE '%Rohit%';

-- FAST: trailing wildcard CAN use index
SELECT * FROM users WHERE name LIKE 'Rohit%';

-- SLOW: SELECT * fetches unnecessary columns
SELECT * FROM orders WHERE user_id = 5;

-- FAST: select only what you need
SELECT id, total, status FROM orders WHERE user_id = 5;

-- SLOW: N+1 queries (one query per user in a loop)
-- Instead, use JOINs to fetch everything in one query
SELECT u.name, o.total
FROM users u
LEFT JOIN orders o ON u.id = o.user_id;
```

---

## 17. Security

### SQL Injection

**Definition:** An attack where malicious SQL is inserted into input fields to manipulate the database.

```sql
-- VULNERABLE — never do this
username = "' OR '1'='1"
query = "SELECT * FROM users WHERE username = '" + username + "'"
-- Becomes: SELECT * FROM users WHERE username = '' OR '1'='1'
-- This logs in as the first user in the database!
```

---

### Prepared Statements

**Definition:** SQL with placeholders, where values are passed separately — prevents injection.

```sql
-- MySQL with prepared statements
PREPARE stmt FROM 'SELECT * FROM users WHERE email = ? AND password_hash = ?';
SET @email = 'user@example.com';
SET @hash = 'hashed_password';
EXECUTE stmt USING @email, @hash;
DEALLOCATE PREPARE stmt;
```

In application code (Python example):
```python
# SAFE — parameterized query
cursor.execute("SELECT * FROM users WHERE email = %s", (email,))

# UNSAFE — string concatenation
cursor.execute("SELECT * FROM users WHERE email = '" + email + "'")
```

---

### Database Security Best Practices

```sql
-- Create a limited-privilege user for your app
CREATE USER 'app_user'@'localhost' IDENTIFIED BY 'strong_password';
GRANT SELECT, INSERT, UPDATE, DELETE ON shop_db.* TO 'app_user'@'localhost';
-- DO NOT grant DROP, CREATE, or admin privileges to app users

-- Revoke unnecessary privileges
REVOKE DELETE ON shop_db.* FROM 'app_user'@'localhost';

-- View user privileges
SHOW GRANTS FOR 'app_user'@'localhost';
```

**Security checklist:**
- ✅ Use prepared statements / parameterized queries
- ✅ Apply principle of least privilege — app users get minimum required access
- ✅ Hash passwords with bcrypt or Argon2 (never MD5 or plain text)
- ✅ Encrypt sensitive columns (credit cards, SSNs)
- ✅ Enable SSL/TLS for database connections
- ✅ Regularly audit and rotate credentials
- ✅ Keep database behind a firewall (never expose directly to internet)

---

## 18. Backup & Migration

### Database Backup

```bash
# MySQL — backup entire database
mysqldump -u root -p shop_db > shop_db_backup.sql

# MySQL — backup specific tables
mysqldump -u root -p shop_db users orders > partial_backup.sql

# PostgreSQL — backup
pg_dump -U postgres shop_db > shop_db_backup.sql

# PostgreSQL — compressed backup
pg_dump -U postgres -Fc shop_db > shop_db_backup.dump
```

---

### Restore Database

```bash
# MySQL restore
mysql -u root -p shop_db < shop_db_backup.sql

# PostgreSQL restore
psql -U postgres shop_db < shop_db_backup.sql

# PostgreSQL restore from compressed dump
pg_restore -U postgres -d shop_db shop_db_backup.dump
```

---

### Export & Import Data

```sql
-- MySQL: export to CSV
SELECT * FROM users
INTO OUTFILE '/tmp/users.csv'
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n';

-- MySQL: import from CSV
LOAD DATA INFILE '/tmp/users.csv'
INTO TABLE users
FIELDS TERMINATED BY ','
ENCLOSED BY '"';

-- PostgreSQL: export to CSV
COPY users TO '/tmp/users.csv' WITH CSV HEADER;

-- PostgreSQL: import from CSV
COPY users FROM '/tmp/users.csv' WITH CSV HEADER;
```

---

## 19. Comparison Tables

### SQL vs NoSQL

| Feature | SQL (Relational) | NoSQL |
|---------|-----------------|-------|
| Structure | Tables with fixed schema | Flexible (JSON, key-value, graph) |
| Relationships | Built-in (JOINs, foreign keys) | Manual handling |
| ACID | Full support | Varies by database |
| Scalability | Vertical (scale up) | Horizontal (scale out) |
| Best for | Complex queries, transactions | High-volume, unstructured data |
| Examples | MySQL, PostgreSQL | MongoDB, Redis, Cassandra |

---

### DELETE vs TRUNCATE vs DROP

| Feature | `DELETE` | `TRUNCATE` | `DROP` |
|---------|----------|------------|--------|
| Removes rows | Yes (with WHERE) | Yes (all) | Yes (all) |
| Removes table | No | No | Yes |
| Can rollback | Yes | No (usually) | No |
| Fires triggers | Yes | No | No |
| Resets AUTO_INCREMENT | No | Yes | Yes |
| Speed | Slower | Faster | Fastest |

---

### WHERE vs HAVING

| Feature | `WHERE` | `HAVING` |
|---------|---------|----------|
| Filters | Individual rows | Groups |
| Used with | SELECT, UPDATE, DELETE | GROUP BY |
| Aggregate functions | ❌ Cannot use | ✅ Can use |
| Runs | Before grouping | After grouping |

---

### INNER JOIN vs LEFT JOIN

| Feature | `INNER JOIN` | `LEFT JOIN` |
|---------|-------------|------------|
| Returns | Only matching rows | All left rows + matches |
| Unmatched rows | Excluded | Shown with NULLs |
| Use when | Need only matches | Need all records from left table |

---

### CHAR vs VARCHAR

| Feature | `CHAR(n)` | `VARCHAR(n)` |
|---------|-----------|--------------|
| Length | Fixed (always n characters) | Variable (up to n characters) |
| Storage | Always uses n bytes | Uses actual length + 1-2 bytes |
| Speed | Slightly faster for fixed-length | Slightly slower |
| Use for | Short fixed-length codes (`'US'`, `'M'`) | Names, emails, descriptions |

---

### PRIMARY KEY vs UNIQUE KEY

| Feature | `PRIMARY KEY` | `UNIQUE KEY` |
|---------|--------------|--------------|
| Per table | Only ONE | Multiple allowed |
| NULL values | Not allowed | One NULL allowed (in most DBs) |
| Auto index | Yes (clustered) | Yes (non-clustered) |
| Purpose | Uniquely identify each row | Prevent duplicate values |

---

## 20. Exercises

### Beginner Exercises

```sql
-- 1. Create a 'books' table with id, title, author, price, published_year
-- 2. Insert 5 books into the table
-- 3. Select all books published after 2000
-- 4. Update the price of a specific book
-- 5. Delete a book by its id
```

### Filtering Practice

```sql
-- 6. Find all users whose email ends with '@gmail.com'
-- 7. Find products priced between 500 and 2000
-- 8. List users from 'Mumbai', 'Delhi', or 'Bangalore'
-- 9. Find all orders placed in the last 30 days
-- 10. List employees with salary > 50000 AND department = 'Engineering'
```

### JOIN Challenges

```sql
-- 11. List all customers with their order count (include customers with no orders)
-- 12. Find products that have never been ordered
-- 13. Show each employee with their manager's name
-- 14. List all students and their enrolled courses (include students with no enrollments)
```

### Aggregate Challenges

```sql
-- 15. Find the average salary per department
-- 16. Find the top 3 most expensive products per category
-- 17. Count the number of orders per month in 2024
-- 18. Find departments where average salary > 60000
-- 19. Show total revenue per product, sorted highest first
```

### Real-World Mini Tasks

```sql
-- 20. Design a database for a library (books, members, loans)
-- 21. Write a query to find users who haven't logged in for 30+ days
-- 22. Find products with stock below 10 that have had orders in the last week
-- 23. Calculate each user's lifetime value (total amount spent)
-- 24. Write a query to detect duplicate emails in the users table
```

---

## 21. Resources & Roadmap

### 📚 SQL Learning Roadmap

```
Beginner
  ├── SQL Syntax & Data Types
  ├── CRUD Operations
  ├── WHERE, ORDER BY, LIMIT
  └── Basic JOINs

Intermediate
  ├── All JOIN types
  ├── Aggregate Functions + GROUP BY
  ├── Subqueries
  ├── Constraints & Relationships
  └── Normalization

Advanced
  ├── Indexes & Query Optimization
  ├── Views, Stored Procedures, Triggers
  ├── Transactions & ACID
  ├── Security & SQL Injection Prevention
  └── PostgreSQL-specific features

Expert
  ├── Query performance tuning (EXPLAIN ANALYZE)
  ├── Database design for production
  ├── Replication & High Availability
  └── Sharding & Partitioning
```

---

### 🔗 Official Documentation

| Resource | Link |
|----------|------|
| PostgreSQL Docs | https://www.postgresql.org/docs/ |
| MySQL Docs | https://dev.mysql.com/doc/ |
| SQLite Docs | https://www.sqlite.org/docs.html |
| SQL Server Docs | https://learn.microsoft.com/en-us/sql/ |

---

### 🏋️ Practice Platforms

| Platform | Description |
|----------|-------------|
| **SQLZoo** | https://sqlzoo.net — Interactive tutorials |
| **LeetCode** | https://leetcode.com/problemset/database — SQL interview problems |
| **HackerRank** | https://hackerrank.com/domains/sql — Beginner to advanced challenges |
| **Mode Analytics** | https://mode.com/sql-tutorial — Data analyst focused |
| **W3Schools SQL** | https://w3schools.com/sql — Quick reference |
| **pgexercises** | https://pgexercises.com — PostgreSQL practice |

---

### 🎓 Recommended Learning Path

1. **Start here:** W3Schools SQL basics → practice with SQLZoo
2. **Build something:** Create a simple blog or e-commerce schema
3. **Go deeper:** PostgreSQL docs + pgexercises
4. **Interview prep:** LeetCode database problems (Easy → Medium → Hard)
5. **Production skills:** Learn query optimization, indexing strategies, backup procedures

---

## ✅ Conclusion

SQL is one of the most valuable skills you can learn in tech. Key takeaways:

- Always use **WHERE** with `UPDATE` and `DELETE`
- Use **prepared statements** to prevent SQL injection
- **Index** the columns you query most — but don't over-index
- Normalize your schema — but don't over-normalize (denormalization is sometimes the right choice for read-heavy workloads)
- Understand **ACID** and use transactions for critical operations
- Practice regularly on real datasets — the best way to get good at SQL is to write SQL

> 🚀 **Start small, build real projects, and you'll master SQL faster than you think.**

---

*Last updated: 2025 | Maintained for learners at all levels*
