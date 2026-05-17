# 🐘 PostgreSQL — From Basics to Advanced

> A comprehensive, beginner-friendly guide to mastering PostgreSQL — the world's most advanced open-source relational database.

---

## 📖 Introduction

**PostgreSQL** (also called **Postgres**) is a powerful, open-source object-relational database management system (ORDBMS) that has been actively developed for over 35 years. It is known for its reliability, feature robustness, and performance.

PostgreSQL goes beyond standard SQL — it supports advanced data types (JSON, arrays, ranges), full-text search, custom functions, stored procedures, and much more.

### 🚀 Why Learn PostgreSQL?

- 🏆 **Industry Standard** — Used by companies like Apple, Instagram, Spotify, Reddit, and Twitch.
- 🔒 **ACID Compliant** — Guarantees data integrity through Atomicity, Consistency, Isolation, Durability.
- 🧠 **Feature-Rich** — JSON support, full-text search, geospatial data (PostGIS), custom types.
- 🌍 **Open Source & Free** — No licensing cost; massive community support.
- ⚡ **High Performance** — Handles millions of rows with proper indexing and query optimization.
- 🔗 **ORM Friendly** — Works seamlessly with Prisma, SQLAlchemy, TypeORM, Django ORM, and more.

---

## 📚 Table of Contents

1. [Setup & Installation](#1-setup--installation)
2. [psql CLI Basics](#2-psql-cli-basics)
3. [Databases](#3-databases)
4. [Data Types](#4-data-types)
5. [Tables — CREATE, ALTER, DROP](#5-tables--create-alter-drop)
6. [INSERT — Adding Data](#6-insert--adding-data)
7. [SELECT — Querying Data](#7-select--querying-data)
8. [WHERE Clause & Filtering](#8-where-clause--filtering)
9. [UPDATE — Modifying Data](#9-update--modifying-data)
10. [DELETE — Removing Data](#10-delete--removing-data)
11. [Exercise 1](#11-exercise-1)
12. [Constraints](#12-constraints)
13. [Primary Key & Foreign Key](#13-primary-key--foreign-key)
14. [Relationships](#14-relationships)
15. [JOINs](#15-joins)
16. [Aggregate Functions](#16-aggregate-functions)
17. [GROUP BY & HAVING](#17-group-by--having)
18. [ORDER BY & LIMIT](#18-order-by--limit)
19. [Exercise 2](#19-exercise-2)
20. [Subqueries](#20-subqueries)
21. [Views](#21-views)
22. [Indexes](#22-indexes)
23. [Transactions](#23-transactions)
24. [Stored Procedures & Functions](#24-stored-procedures--functions)
25. [Triggers](#25-triggers)
26. [CTEs (Common Table Expressions)](#26-ctes-common-table-expressions)
27. [Window Functions](#27-window-functions)
28. [JSON & JSONB](#28-json--jsonb)
29. [Full-Text Search](#29-full-text-search)
30. [Roles & Permissions](#30-roles--permissions)
31. [Performance & EXPLAIN](#31-performance--explain)
32. [Backup & Restore](#32-backup--restore)
33. [Conclusion & Resources](#33-conclusion--resources)

---

## 1. 🛠️ Setup & Installation

### 📌 Definition
Installing PostgreSQL and connecting to it for the first time.

### 💻 Installation

#### On Ubuntu / Debian
```bash
sudo apt update
sudo apt install postgresql postgresql-contrib

# Start the service
sudo systemctl start postgresql
sudo systemctl enable postgresql  # Auto-start on boot

# Check status
sudo systemctl status postgresql
```

#### On macOS (using Homebrew)
```bash
brew install postgresql@16
brew services start postgresql@16

# Add to PATH
echo 'export PATH="/opt/homebrew/opt/postgresql@16/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

#### On Windows
Download the installer from [https://www.postgresql.org/download/windows/](https://www.postgresql.org/download/windows/) and follow the setup wizard. It installs PostgreSQL + pgAdmin (GUI tool).

### 🔐 First Login
```bash
# Switch to postgres system user
sudo -i -u postgres

# Enter PostgreSQL shell
psql

# OR in one command
sudo -u postgres psql
```

### ⚠️ Important Points
- Default superuser is `postgres`.
- Default port is `5432`.
- PostgreSQL stores data in a "data directory" (usually `/var/lib/postgresql/`).

> 💡 **Tip:** Install **pgAdmin 4** (GUI) or **DBeaver** (GUI) alongside psql for a visual interface — great for beginners.

---

## 2. 💻 psql CLI Basics

### 📌 Definition
`psql` is PostgreSQL's interactive terminal — your primary tool for running SQL commands and managing databases.

### 🔤 Essential psql Meta-Commands

```sql
-- Connect to a database
psql -U username -d database_name -h localhost -p 5432

-- Inside psql:
\l          -- List all databases
\c dbname   -- Connect/switch to a database
\dt         -- List all tables in current database
\d tablename -- Describe table structure
\du         -- List all users/roles
\df         -- List all functions
\dv         -- List all views
\di         -- List all indexes

\timing     -- Toggle query execution time display
\e          -- Open query in external editor
\i file.sql -- Execute SQL from a file
\o file.txt -- Save output to a file

\x          -- Toggle expanded display (vertical output)
\q          -- Quit psql
\?          -- Help for psql commands
\h SELECT   -- Help for SQL command syntax
```

### 💡 Connection String Format
```bash
# Full connection string
psql "postgresql://username:password@localhost:5432/mydb"

# Or with flags
psql -U myuser -d mydb -h localhost -p 5432 -W
# -W forces password prompt
```

> 💡 **Tip:** Use `\x auto` for automatic expanded display — makes wide result sets readable.

---

## 3. 🗄️ Databases

### 📌 Definition
A database is an organized container that holds all your tables, views, functions, and other objects.

### 🔤 Syntax & Examples

```sql
-- Create a database
CREATE DATABASE shop_db;

-- Create with specific owner and encoding
CREATE DATABASE company_db
  OWNER = admin_user
  ENCODING = 'UTF8'
  LC_COLLATE = 'en_US.UTF-8'
  LC_CTYPE = 'en_US.UTF-8';

-- Connect to a database
\c shop_db

-- Rename a database
ALTER DATABASE shop_db RENAME TO ecommerce_db;

-- Change owner
ALTER DATABASE ecommerce_db OWNER TO new_owner;

-- Drop a database (CAREFUL! Irreversible)
DROP DATABASE shop_db;

-- Drop only if it exists (safer)
DROP DATABASE IF EXISTS shop_db;

-- List all databases
SELECT datname, pg_size_pretty(pg_database_size(datname)) AS size
FROM pg_database
ORDER BY pg_database_size(datname) DESC;
```

### ⚠️ Important Points
- You cannot drop a database you are currently connected to.
- Always use `UTF8` encoding for international character support.
- Use `IF EXISTS` to avoid errors in scripts.

---

## 4. 🔢 Data Types

### 📌 Definition
Data types define what kind of data a column can store, ensuring data integrity and storage efficiency.

### 📊 PostgreSQL Data Types Reference

#### Numeric Types
```sql
SMALLINT          -- 2 bytes, -32768 to 32767
INTEGER (INT)     -- 4 bytes, ~-2.1B to 2.1B
BIGINT            -- 8 bytes, very large integers
DECIMAL(p, s)     -- Exact precision (financial data)
NUMERIC(p, s)     -- Same as DECIMAL
REAL              -- 4 bytes, floating-point
DOUBLE PRECISION  -- 8 bytes, floating-point
SERIAL            -- Auto-incrementing INTEGER (4 bytes)
BIGSERIAL         -- Auto-incrementing BIGINT (8 bytes)
```

#### Character Types
```sql
CHAR(n)           -- Fixed length, padded with spaces
VARCHAR(n)        -- Variable length, max n characters
TEXT              -- Unlimited length string
```

#### Date & Time Types
```sql
DATE              -- 'YYYY-MM-DD'
TIME              -- 'HH:MM:SS'
TIMESTAMP         -- Date + time (no timezone)
TIMESTAMPTZ       -- Date + time WITH timezone
INTERVAL          -- Time duration ('1 year 2 months')
```

#### Boolean
```sql
BOOLEAN           -- TRUE / FALSE / NULL
```

#### Special Types
```sql
UUID              -- Universally Unique Identifier
JSON              -- Stored as text (validated JSON)
JSONB             -- Binary JSON (indexed, faster queries)
ARRAY             -- Array of any type (e.g., INTEGER[])
BYTEA             -- Binary data
INET              -- IPv4 or IPv6 address
CIDR              -- IP network address
POINT             -- Geometric point (x, y)
```

### 💡 Example — Creating a Table with Various Types
```sql
CREATE TABLE employees (
  id            BIGSERIAL PRIMARY KEY,
  employee_code UUID DEFAULT gen_random_uuid(),
  first_name    VARCHAR(50) NOT NULL,
  last_name     VARCHAR(50) NOT NULL,
  email         VARCHAR(100) UNIQUE NOT NULL,
  salary        NUMERIC(10, 2),         -- 10 digits, 2 decimal places
  is_active     BOOLEAN DEFAULT TRUE,
  hire_date     DATE DEFAULT CURRENT_DATE,
  last_login    TIMESTAMPTZ,
  bio           TEXT,
  tags          TEXT[],                 -- Array of strings
  metadata      JSONB                   -- JSON data
);
```

### 📊 Type Comparison Table

| Category | Type | Storage | Best For |
|----------|------|---------|----------|
| Integer | `INTEGER` | 4 bytes | IDs, counts |
| Integer | `BIGINT` | 8 bytes | Large IDs |
| Decimal | `NUMERIC(p,s)` | Variable | Money, prices |
| Float | `DOUBLE PRECISION` | 8 bytes | Scientific data |
| String | `VARCHAR(n)` | Variable | Names, emails |
| String | `TEXT` | Variable | Long text, bios |
| Date | `DATE` | 4 bytes | Birthdays |
| DateTime | `TIMESTAMPTZ` | 8 bytes | Events, logs |
| Auto ID | `BIGSERIAL` | 8 bytes | Primary keys |
| Unique ID | `UUID` | 16 bytes | Distributed IDs |

> 💡 **Best Practice:** Use `NUMERIC` for money (never `FLOAT` — floating-point imprecision can cause rounding errors in financial calculations). Use `TIMESTAMPTZ` over `TIMESTAMP` to avoid timezone bugs.

---

## 5. 📋 Tables — CREATE, ALTER, DROP

### 📌 Definition
Tables are the core structure in PostgreSQL — organized grids of rows and columns that store your data.

### 🔤 Syntax & Examples

#### CREATE TABLE
```sql
-- Basic table creation
CREATE TABLE products (
  id          BIGSERIAL PRIMARY KEY,
  name        VARCHAR(200) NOT NULL,
  description TEXT,
  price       NUMERIC(10, 2) NOT NULL CHECK (price >= 0),
  stock       INTEGER DEFAULT 0 CHECK (stock >= 0),
  category    VARCHAR(100),
  created_at  TIMESTAMPTZ DEFAULT NOW()
);

-- Create table only if it doesn't exist (safe for scripts)
CREATE TABLE IF NOT EXISTS products (
  id   BIGSERIAL PRIMARY KEY,
  name VARCHAR(200) NOT NULL
);

-- Create table from another table's structure
CREATE TABLE products_archive AS
  SELECT * FROM products WHERE 1=0; -- Empty copy (no data)

-- Create table with data from SELECT
CREATE TABLE expensive_products AS
  SELECT * FROM products WHERE price > 10000;
```

#### ALTER TABLE
```sql
-- Add a new column
ALTER TABLE products ADD COLUMN sku VARCHAR(50);

-- Add column with default value
ALTER TABLE products ADD COLUMN is_featured BOOLEAN DEFAULT FALSE;

-- Drop a column
ALTER TABLE products DROP COLUMN sku;

-- Rename a column
ALTER TABLE products RENAME COLUMN name TO product_name;

-- Change column data type
ALTER TABLE products ALTER COLUMN price TYPE DECIMAL(12, 2);

-- Set / Drop NOT NULL constraint
ALTER TABLE products ALTER COLUMN category SET NOT NULL;
ALTER TABLE products ALTER COLUMN category DROP NOT NULL;

-- Set default value
ALTER TABLE products ALTER COLUMN stock SET DEFAULT 100;

-- Rename the table
ALTER TABLE products RENAME TO inventory;
```

#### DROP TABLE
```sql
-- Drop a table (WARNING: All data lost)
DROP TABLE products;

-- Drop only if exists
DROP TABLE IF EXISTS products;

-- Drop multiple tables
DROP TABLE IF EXISTS products, categories, orders;

-- Drop table and all dependent objects (views, foreign keys)
DROP TABLE products CASCADE;
```

### ⚠️ Important Points
- `CASCADE` drops all dependent objects — use carefully.
- `RESTRICT` (default) prevents dropping if dependencies exist.
- Always use `IF EXISTS` in migration scripts to prevent errors.

> 🧠 **Interview Tip:** Know the difference between `TRUNCATE` (removes all rows, resets sequences, fast) and `DROP` (removes the table itself).

---

## 6. ➕ INSERT — Adding Data

### 📌 Definition
`INSERT` adds new rows of data into a table.

### 🔤 Syntax & Examples

```sql
-- Insert a single row
INSERT INTO products (name, price, stock, category)
VALUES ('iPhone 15', 79999.00, 50, 'Electronics');

-- Insert multiple rows at once (much faster than separate INSERTs)
INSERT INTO products (name, price, stock, category)
VALUES
  ('Samsung Galaxy S24', 74999.00, 30, 'Electronics'),
  ('MacBook Pro 14"',   199999.00, 15, 'Computers'),
  ('Sony Headphones',    24999.00, 100, 'Audio'),
  ('Nike Air Max',       12999.00, 200, 'Footwear');

-- Insert and return the generated values (RETURNING)
INSERT INTO products (name, price, stock)
VALUES ('iPad Pro', 89999.00, 25)
RETURNING id, name, created_at;

-- Insert from SELECT (copy data between tables)
INSERT INTO products_archive
SELECT * FROM products WHERE created_at < NOW() - INTERVAL '1 year';

-- Insert or do nothing on conflict (UPSERT)
INSERT INTO products (name, price, stock)
VALUES ('iPhone 15', 79999.00, 50)
ON CONFLICT (name) DO NOTHING;

-- Insert or update on conflict (true UPSERT)
INSERT INTO products (name, price, stock)
VALUES ('iPhone 15', 84999.00, 60)
ON CONFLICT (name)
DO UPDATE SET
  price = EXCLUDED.price,
  stock = EXCLUDED.stock,
  updated_at = NOW();
-- EXCLUDED refers to the row that was rejected due to conflict
```

### ⚠️ Important Points
- Omitted columns use their `DEFAULT` value or `NULL`.
- `RETURNING` is very useful — avoids a separate `SELECT` to get the inserted ID.
- `ON CONFLICT` enables "upsert" — insert if not exists, update if it does.
- Batch inserts (multiple rows in one statement) are significantly faster than individual inserts.

> 💡 **Best Practice:** Always specify column names explicitly in `INSERT` statements — never rely on column order. It protects against future schema changes.

---

## 7. 🔍 SELECT — Querying Data

### 📌 Definition
`SELECT` retrieves data from one or more tables. It's the most used SQL statement.

### 🔤 Syntax & Examples

```sql
-- Select all columns
SELECT * FROM products;

-- Select specific columns
SELECT name, price, stock FROM products;

-- Column aliases (rename output)
SELECT
  name        AS product_name,
  price       AS "Price (₹)",
  stock       AS available_qty
FROM products;

-- Computed columns
SELECT
  name,
  price,
  stock,
  price * stock AS total_value,
  price * 0.18  AS gst_amount
FROM products;

-- Distinct values (remove duplicates)
SELECT DISTINCT category FROM products;

-- Select with string functions
SELECT
  UPPER(name)           AS name_upper,
  LENGTH(name)          AS name_length,
  TRIM(category)        AS category_clean,
  CONCAT(name, ' - ₹', price) AS display_label
FROM products;

-- Select with date functions
SELECT
  name,
  created_at,
  DATE_PART('year', created_at)  AS year,
  DATE_PART('month', created_at) AS month,
  AGE(NOW(), created_at)          AS age
FROM products;

-- Conditional column (CASE WHEN)
SELECT
  name,
  price,
  CASE
    WHEN price < 10000  THEN 'Budget'
    WHEN price < 50000  THEN 'Mid-Range'
    WHEN price < 100000 THEN 'Premium'
    ELSE 'Luxury'
  END AS price_tier
FROM products;

-- COALESCE — return first non-null value
SELECT
  name,
  COALESCE(description, 'No description available') AS description
FROM products;

-- NULLIF — return NULL if values are equal
SELECT NULLIF(stock, 0) AS stock_or_null FROM products;
```

### ⚠️ Important Points
- `SELECT *` is fine for exploration but avoid it in production code — always name columns.
- Aliases with spaces or special characters require double quotes `"Price (₹)"`.
- `COALESCE` is essential for handling NULL values gracefully.

---

## 8. 🔎 WHERE Clause & Filtering

### 📌 Definition
The `WHERE` clause filters rows based on conditions — only rows matching the condition are returned.

### 🔤 Syntax & Examples

```sql
-- Basic comparison
SELECT * FROM products WHERE price > 50000;
SELECT * FROM products WHERE category = 'Electronics';
SELECT * FROM products WHERE stock = 0;

-- Multiple conditions
SELECT * FROM products
WHERE category = 'Electronics' AND price < 100000;

SELECT * FROM products
WHERE category = 'Audio' OR category = 'Electronics';

-- NOT operator
SELECT * FROM products WHERE NOT category = 'Footwear';

-- BETWEEN (inclusive on both ends)
SELECT * FROM products WHERE price BETWEEN 10000 AND 50000;

-- IN — match any value in a list
SELECT * FROM products
WHERE category IN ('Electronics', 'Computers', 'Audio');

-- NOT IN
SELECT * FROM products
WHERE category NOT IN ('Footwear', 'Clothing');

-- LIKE — pattern matching
SELECT * FROM products WHERE name LIKE 'iPhone%';   -- Starts with iPhone
SELECT * FROM products WHERE name LIKE '%Pro%';     -- Contains Pro
SELECT * FROM products WHERE name LIKE '_ike%';     -- Second char is 'i'

-- ILIKE — case-insensitive LIKE (PostgreSQL-specific)
SELECT * FROM products WHERE name ILIKE '%apple%';  -- Any case

-- IS NULL / IS NOT NULL
SELECT * FROM products WHERE description IS NULL;
SELECT * FROM products WHERE description IS NOT NULL;

-- Date filtering
SELECT * FROM products
WHERE created_at >= '2024-01-01'
  AND created_at < '2025-01-01';

-- Date with interval
SELECT * FROM products
WHERE created_at > NOW() - INTERVAL '30 days';

-- ANY / ALL with arrays
SELECT * FROM products
WHERE category = ANY(ARRAY['Electronics', 'Audio']);
```

### 📊 Comparison Operators

| Operator | Meaning | Example |
|----------|---------|---------|
| `=` | Equal | `price = 999` |
| `!=` or `<>` | Not equal | `status != 'inactive'` |
| `>` | Greater than | `price > 1000` |
| `<` | Less than | `stock < 10` |
| `>=` | Greater or equal | `age >= 18` |
| `<=` | Less or equal | `discount <= 50` |
| `BETWEEN` | Within range | `price BETWEEN 100 AND 500` |
| `IN` | In list | `role IN ('admin', 'user')` |
| `LIKE` | Pattern match | `name LIKE 'A%'` |
| `ILIKE` | Case-insensitive | `name ILIKE '%apple%'` |
| `IS NULL` | Is null | `deleted_at IS NULL` |

---

## 9. ✏️ UPDATE — Modifying Data

### 📌 Definition
`UPDATE` modifies existing data in a table.

### 🔤 Syntax & Examples

```sql
-- Update a single column
UPDATE products
SET price = 84999.00
WHERE name = 'iPhone 15';

-- Update multiple columns
UPDATE products
SET
  price      = 89999.00,
  stock      = 45,
  updated_at = NOW()
WHERE id = 1;

-- Update using expressions
UPDATE products
SET price = price * 0.90  -- Apply 10% discount
WHERE category = 'Electronics';

-- Update with RETURNING (see what changed)
UPDATE products
SET stock = stock - 1
WHERE id = 5
RETURNING id, name, stock;

-- Update based on another table's data (UPDATE with JOIN)
UPDATE products p
SET price = p.price * (1 - d.discount_pct / 100)
FROM discounts d
WHERE p.category = d.category;

-- Conditional update with CASE
UPDATE employees
SET salary = CASE
  WHEN department = 'Engineering' THEN salary * 1.15
  WHEN department = 'Sales'       THEN salary * 1.10
  ELSE salary * 1.05
END;
```

### ⚠️ Important Points
- **ALWAYS use a WHERE clause** — without it, you update EVERY row in the table.
- Test your `WHERE` condition with a `SELECT` before running `UPDATE`.
- `RETURNING` confirms what was actually changed.

> 🧠 **Common Mistake:** `UPDATE products SET price = 0;` — No WHERE clause means ALL prices become 0. Always double-check!

---

## 10. 🗑️ DELETE — Removing Data

### 📌 Definition
`DELETE` removes rows from a table based on a condition.

### 🔤 Syntax & Examples

```sql
-- Delete specific rows
DELETE FROM products WHERE id = 5;

-- Delete with multiple conditions
DELETE FROM products
WHERE stock = 0 AND category = 'Electronics';

-- Delete old records
DELETE FROM logs
WHERE created_at < NOW() - INTERVAL '90 days';

-- Delete and return deleted rows
DELETE FROM products
WHERE price < 100
RETURNING *;

-- Delete all rows (keeps table structure)
DELETE FROM products;

-- TRUNCATE — faster alternative to delete all rows
TRUNCATE TABLE products;                    -- Simple truncate
TRUNCATE TABLE products RESTART IDENTITY;   -- Also resets SERIAL counter
TRUNCATE TABLE products, orders CASCADE;    -- Truncate multiple + dependents
```

### 📊 DELETE vs TRUNCATE vs DROP

| Operation | Removes | WHERE clause | Rollback | Speed | Resets Serial |
|-----------|---------|-------------|---------|-------|--------------|
| `DELETE` | Rows | ✅ Yes | ✅ Yes | Slower | ❌ No |
| `TRUNCATE` | All rows | ❌ No | ✅ Yes | ⚡ Fast | Optional |
| `DROP` | Entire table | ❌ No | ✅ Yes | Fast | N/A |

### ⚠️ Important Points
- Like UPDATE, always use a WHERE clause unless you intend to delete everything.
- `TRUNCATE` is faster for clearing all rows but cannot be used with a WHERE clause.
- Both `DELETE` and `TRUNCATE` can be rolled back inside a transaction.

---

## 11. 🏋️ Exercise 1

Practice the fundamentals!

```sql
-- Setup: Run this first to create sample data
CREATE TABLE students (
  id         BIGSERIAL PRIMARY KEY,
  name       VARCHAR(100) NOT NULL,
  age        INTEGER CHECK (age > 0),
  grade      CHAR(2),
  marks      NUMERIC(5, 2) CHECK (marks BETWEEN 0 AND 100),
  city       VARCHAR(100),
  enrolled   BOOLEAN DEFAULT TRUE,
  joined_on  DATE DEFAULT CURRENT_DATE
);

INSERT INTO students (name, age, grade, marks, city) VALUES
  ('Alice',   20, 'A',  92.5, 'Mumbai'),
  ('Bob',     22, 'B',  75.0, 'Delhi'),
  ('Charlie', 19, 'A+', 98.0, 'Bangalore'),
  ('Diana',   21, 'C',  55.5, 'Mumbai'),
  ('Edward',  23, 'B',  80.0, 'Chennai'),
  ('Fatima',  20, 'A',  88.0, 'Hyderabad'),
  ('George',  24, 'D',  45.0, 'Delhi'),
  ('Hannah',  19, 'A+', 95.0, 'Bangalore');

-- EXERCISES:

-- Q1. List all students from Mumbai.
-- Q2. Find students with marks above 80.
-- Q3. Find students from Delhi OR Bangalore.
-- Q4. List students aged between 19 and 21.
-- Q5. Find students whose name starts with a vowel (A, E, I, O, U).
-- Q6. Update George's marks to 50.0.
-- Q7. Delete all students with grade 'D'.
-- Q8. Display each student's name and a 'Pass'/'Fail' label (pass = marks >= 50).

-- ANSWERS:

-- Q1.
SELECT * FROM students WHERE city = 'Mumbai';

-- Q2.
SELECT name, marks FROM students WHERE marks > 80;

-- Q3.
SELECT * FROM students WHERE city IN ('Delhi', 'Bangalore');

-- Q4.
SELECT * FROM students WHERE age BETWEEN 19 AND 21;

-- Q5.
SELECT * FROM students WHERE name ILIKE 'A%'
  OR name ILIKE 'E%' OR name ILIKE 'I%'
  OR name ILIKE 'O%' OR name ILIKE 'U%';
-- Cleaner: WHERE SUBSTRING(name, 1, 1) ILIKE ANY(ARRAY['A','E','I','O','U'])

-- Q6.
UPDATE students SET marks = 50.0 WHERE name = 'George';

-- Q7.
DELETE FROM students WHERE grade = 'D';

-- Q8.
SELECT name, marks,
  CASE WHEN marks >= 50 THEN 'Pass ✅' ELSE 'Fail ❌' END AS result
FROM students;
```

---

## 12. 🔐 Constraints

### 📌 Definition
Constraints are rules enforced on columns to ensure data validity and integrity.

### 🔤 Syntax & Examples

```sql
CREATE TABLE orders (
  id           BIGSERIAL,
  order_number VARCHAR(20),
  customer_id  BIGINT,
  amount       NUMERIC(10, 2),
  status       VARCHAR(20),
  email        VARCHAR(100),
  created_at   TIMESTAMPTZ DEFAULT NOW(),

  -- PRIMARY KEY constraint
  CONSTRAINT orders_pkey PRIMARY KEY (id),

  -- UNIQUE constraint
  CONSTRAINT orders_number_unique UNIQUE (order_number),

  -- NOT NULL is applied inline
  -- CHECK constraint
  CONSTRAINT orders_amount_positive CHECK (amount > 0),

  -- CHECK with allowed values
  CONSTRAINT orders_status_valid
    CHECK (status IN ('pending', 'confirmed', 'shipped', 'delivered', 'cancelled'))
);

-- Add constraints to existing table
ALTER TABLE orders
  ADD CONSTRAINT orders_email_valid
  CHECK (email ~* '^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$');

-- Drop a constraint
ALTER TABLE orders DROP CONSTRAINT orders_status_valid;

-- Make a column NOT NULL
ALTER TABLE orders ALTER COLUMN email SET NOT NULL;

-- UNIQUE on multiple columns (composite unique)
ALTER TABLE orders
  ADD CONSTRAINT orders_customer_number_unique
  UNIQUE (customer_id, order_number);
```

### 📊 Constraints Reference

| Constraint | Purpose | Example |
|------------|---------|---------|
| `PRIMARY KEY` | Unique identifier per row | `id BIGSERIAL PRIMARY KEY` |
| `NOT NULL` | Column cannot be empty | `name VARCHAR(100) NOT NULL` |
| `UNIQUE` | No duplicate values | `email VARCHAR UNIQUE` |
| `CHECK` | Custom validation rule | `CHECK (age >= 18)` |
| `FOREIGN KEY` | Link to another table | `REFERENCES users(id)` |
| `DEFAULT` | Value if none provided | `DEFAULT NOW()` |

---

## 13. 🔑 Primary Key & Foreign Key

### 📌 Definition
- **Primary Key (PK):** Uniquely identifies each row in a table. Cannot be NULL.
- **Foreign Key (FK):** Links a column in one table to the Primary Key of another, enforcing referential integrity.

### 🔤 Syntax & Examples

```sql
-- Parent table
CREATE TABLE categories (
  id   BIGSERIAL PRIMARY KEY,
  name VARCHAR(100) NOT NULL UNIQUE
);

-- Child table with Foreign Key
CREATE TABLE products (
  id          BIGSERIAL PRIMARY KEY,
  name        VARCHAR(200) NOT NULL,
  price       NUMERIC(10, 2),
  category_id BIGINT NOT NULL,

  -- Foreign key constraint
  CONSTRAINT products_category_fk
    FOREIGN KEY (category_id)
    REFERENCES categories(id)
    ON DELETE RESTRICT    -- Prevent deleting category with products
    ON UPDATE CASCADE     -- If category id changes, update here too
);

-- Adding FK to existing table
ALTER TABLE products
  ADD CONSTRAINT products_category_fk
  FOREIGN KEY (category_id) REFERENCES categories(id);

-- Composite Primary Key
CREATE TABLE order_items (
  order_id   BIGINT,
  product_id BIGINT,
  quantity   INTEGER NOT NULL,
  price      NUMERIC(10, 2) NOT NULL,

  PRIMARY KEY (order_id, product_id),  -- Composite PK

  FOREIGN KEY (order_id)   REFERENCES orders(id)   ON DELETE CASCADE,
  FOREIGN KEY (product_id) REFERENCES products(id) ON DELETE RESTRICT
);
```

### 📊 ON DELETE / ON UPDATE Options

| Option | Behavior |
|--------|----------|
| `RESTRICT` | Prevent deletion if child rows exist |
| `CASCADE` | Delete/update child rows automatically |
| `SET NULL` | Set FK column to NULL on parent delete |
| `SET DEFAULT` | Set FK column to default on parent delete |
| `NO ACTION` | Like RESTRICT but checked at end of transaction |

> 💡 **Best Practice:** Use `ON DELETE CASCADE` for dependent data (order_items depends on orders). Use `ON DELETE RESTRICT` to protect critical referenced data (don't delete a category that has products).

---

## 14. 🔗 Relationships

### 📌 Definition
Relationships define how tables relate to each other — the foundation of relational database design.

### 📝 Types of Relationships

#### One-to-One (1:1)
```sql
-- Each user has one profile
CREATE TABLE users (
  id    BIGSERIAL PRIMARY KEY,
  email VARCHAR(100) UNIQUE NOT NULL
);

CREATE TABLE user_profiles (
  id         BIGSERIAL PRIMARY KEY,
  user_id    BIGINT UNIQUE NOT NULL REFERENCES users(id), -- UNIQUE enforces 1:1
  bio        TEXT,
  avatar_url VARCHAR(500),
  website    VARCHAR(200)
);
```

#### One-to-Many (1:N) — Most Common
```sql
-- One customer can have many orders
CREATE TABLE customers (
  id   BIGSERIAL PRIMARY KEY,
  name VARCHAR(100) NOT NULL
);

CREATE TABLE orders (
  id          BIGSERIAL PRIMARY KEY,
  customer_id BIGINT NOT NULL REFERENCES customers(id), -- Many orders → one customer
  total       NUMERIC(10, 2),
  order_date  DATE DEFAULT CURRENT_DATE
);
```

#### Many-to-Many (M:N) — Uses Junction Table
```sql
-- A student can enroll in many courses; a course has many students
CREATE TABLE students (
  id   BIGSERIAL PRIMARY KEY,
  name VARCHAR(100) NOT NULL
);

CREATE TABLE courses (
  id    BIGSERIAL PRIMARY KEY,
  title VARCHAR(200) NOT NULL
);

-- Junction (bridge) table
CREATE TABLE enrollments (
  student_id  BIGINT NOT NULL REFERENCES students(id) ON DELETE CASCADE,
  course_id   BIGINT NOT NULL REFERENCES courses(id)  ON DELETE CASCADE,
  enrolled_on DATE DEFAULT CURRENT_DATE,
  grade       CHAR(2),

  PRIMARY KEY (student_id, course_id) -- Prevents duplicate enrollments
);
```

---

## 15. 🔀 JOINs

### 📌 Definition
JOINs combine rows from two or more tables based on a related column between them.

### 🔤 Syntax & Examples

```sql
-- Sample data for examples
-- categories: id, name
-- products: id, name, price, category_id

-- INNER JOIN — only matching rows from BOTH tables
SELECT
  p.name        AS product,
  p.price,
  c.name        AS category
FROM products p
INNER JOIN categories c ON p.category_id = c.id;

-- LEFT JOIN — all rows from LEFT table, matching from RIGHT (NULL if no match)
SELECT
  c.name        AS category,
  p.name        AS product,
  p.price
FROM categories c
LEFT JOIN products p ON c.id = p.category_id
ORDER BY c.name;
-- Shows ALL categories, even those with no products (NULL product columns)

-- RIGHT JOIN — all rows from RIGHT table (less common, often rewritten as LEFT JOIN)
SELECT
  p.name, c.name AS category
FROM products p
RIGHT JOIN categories c ON p.category_id = c.id;

-- FULL OUTER JOIN — all rows from BOTH tables
SELECT
  c.name AS category,
  p.name AS product
FROM categories c
FULL OUTER JOIN products p ON c.id = p.category_id;

-- CROSS JOIN — every combination (Cartesian product)
SELECT c.name, s.name
FROM colors c
CROSS JOIN sizes s;
-- If colors has 3 rows and sizes has 4, result has 12 rows

-- Multiple JOINs
SELECT
  o.id           AS order_id,
  c.name         AS customer_name,
  p.name         AS product_name,
  oi.quantity,
  oi.price
FROM orders o
JOIN customers  c  ON o.customer_id  = c.id
JOIN order_items oi ON o.id           = oi.order_id
JOIN products   p  ON oi.product_id  = p.id
WHERE o.order_date >= '2024-01-01'
ORDER BY o.id;

-- SELF JOIN — join a table to itself
-- Example: find employees and their managers
SELECT
  e.name  AS employee,
  m.name  AS manager
FROM employees e
LEFT JOIN employees m ON e.manager_id = m.id;
```

### 📊 JOIN Types Visual Reference

| JOIN Type | Returns |
|-----------|---------|
| `INNER JOIN` | Only rows with matches in BOTH tables |
| `LEFT JOIN` | All rows from left + matching from right (NULL if no match) |
| `RIGHT JOIN` | All rows from right + matching from left (NULL if no match) |
| `FULL OUTER JOIN` | All rows from both tables (NULL where no match) |
| `CROSS JOIN` | Every combination of rows (Cartesian product) |
| `SELF JOIN` | A table joined with itself |

> 🧠 **Interview Tip:** Understand `LEFT JOIN` with a `WHERE right.id IS NULL` — this finds rows in the left table that have NO matching row in the right table.
> ```sql
> -- Products with no category assigned
> SELECT p.* FROM products p
> LEFT JOIN categories c ON p.category_id = c.id
> WHERE c.id IS NULL;
> ```

---

## 16. 📊 Aggregate Functions

### 📌 Definition
Aggregate functions perform calculations on a set of rows and return a single summary value.

### 🔤 Syntax & Examples

```sql
-- COUNT — number of rows
SELECT COUNT(*)          AS total_products  FROM products;
SELECT COUNT(description) AS with_description FROM products; -- Excludes NULLs
SELECT COUNT(DISTINCT category) AS categories FROM products;

-- SUM — total of numeric column
SELECT SUM(price)         AS total_value FROM products;
SELECT SUM(price * stock) AS inventory_value FROM products;

-- AVG — average value
SELECT AVG(price)                        AS avg_price FROM products;
SELECT ROUND(AVG(price), 2)              AS avg_price_rounded FROM products;

-- MIN / MAX
SELECT MIN(price) AS cheapest, MAX(price) AS most_expensive FROM products;
SELECT MIN(created_at) AS oldest, MAX(created_at) AS newest FROM products;

-- Multiple aggregates in one query
SELECT
  COUNT(*)          AS total_products,
  SUM(stock)        AS total_stock,
  ROUND(AVG(price), 2) AS avg_price,
  MIN(price)        AS min_price,
  MAX(price)        AS max_price,
  SUM(price * stock) AS total_inventory_value
FROM products;

-- STRING_AGG — concatenate strings
SELECT
  category,
  STRING_AGG(name, ', ' ORDER BY name) AS products_list
FROM products
GROUP BY category;

-- ARRAY_AGG — collect values into an array
SELECT
  category,
  ARRAY_AGG(name ORDER BY price DESC) AS products_by_price
FROM products
GROUP BY category;
```

---

## 17. 📦 GROUP BY & HAVING

### 📌 Definition
- `GROUP BY` groups rows with the same values in specified columns, so aggregate functions apply per group.
- `HAVING` filters groups (like WHERE, but for aggregated data).

### 🔤 Syntax & Examples

```sql
-- Group by category — count products per category
SELECT
  category,
  COUNT(*) AS product_count
FROM products
GROUP BY category
ORDER BY product_count DESC;

-- Multiple aggregates per group
SELECT
  category,
  COUNT(*)             AS count,
  ROUND(AVG(price), 2) AS avg_price,
  SUM(stock)           AS total_stock,
  MIN(price)           AS cheapest,
  MAX(price)           AS most_expensive
FROM products
GROUP BY category;

-- HAVING — filter after grouping
-- Show only categories with more than 5 products
SELECT
  category,
  COUNT(*) AS product_count
FROM products
GROUP BY category
HAVING COUNT(*) > 5
ORDER BY product_count DESC;

-- Combine WHERE (pre-group filter) + HAVING (post-group filter)
SELECT
  category,
  ROUND(AVG(price), 2) AS avg_price
FROM products
WHERE is_active = TRUE          -- Filter rows BEFORE grouping
GROUP BY category
HAVING AVG(price) > 10000       -- Filter groups AFTER grouping
ORDER BY avg_price DESC;

-- Group by multiple columns
SELECT
  category,
  DATE_TRUNC('month', created_at) AS month,
  COUNT(*) AS new_products
FROM products
GROUP BY category, DATE_TRUNC('month', created_at)
ORDER BY month, category;
```

### 📊 WHERE vs HAVING

| Feature | WHERE | HAVING |
|---------|-------|--------|
| Filters | Individual rows | Groups |
| When | Before GROUP BY | After GROUP BY |
| Aggregates | ❌ Cannot use | ✅ Can use |
| Performance | ⚡ Faster (less data to group) | Slower |

> 💡 **Rule:** Use `WHERE` to filter rows before grouping (faster). Use `HAVING` to filter aggregated results.

---

## 18. 📑 ORDER BY & LIMIT

### 📌 Definition
- `ORDER BY` sorts results.
- `LIMIT` restricts the number of rows returned.
- `OFFSET` skips a number of rows (used for pagination).

### 🔤 Syntax & Examples

```sql
-- Sort ascending (default)
SELECT name, price FROM products ORDER BY price;
SELECT name, price FROM products ORDER BY price ASC;

-- Sort descending
SELECT name, price FROM products ORDER BY price DESC;

-- Sort by multiple columns
SELECT name, category, price
FROM products
ORDER BY category ASC, price DESC;

-- Sort by expression
SELECT name, price, stock, price * stock AS inventory_value
FROM products
ORDER BY price * stock DESC;

-- NULLS FIRST / NULLS LAST
SELECT name, description FROM products
ORDER BY description NULLS LAST; -- NULLs appear at end

-- LIMIT — top N results
SELECT name, price FROM products
ORDER BY price DESC
LIMIT 10; -- Top 10 most expensive

-- OFFSET — skip rows (PAGINATION)
-- Page 1: rows 1-10
SELECT name, price FROM products ORDER BY id LIMIT 10 OFFSET 0;
-- Page 2: rows 11-20
SELECT name, price FROM products ORDER BY id LIMIT 10 OFFSET 10;
-- Page N: OFFSET = (page_number - 1) * page_size

-- Pagination helper
-- Page 3, 20 items per page:
SELECT * FROM products
ORDER BY created_at DESC
LIMIT 20
OFFSET (3 - 1) * 20; -- OFFSET 40
```

> 💡 **Performance Note:** For large datasets, `OFFSET` becomes slow as page numbers increase because PostgreSQL scans all skipped rows. Use **keyset/cursor pagination** for high-performance pagination:
> ```sql
> -- Instead of OFFSET, use WHERE with last seen id
> SELECT * FROM products
> WHERE id > :last_seen_id
> ORDER BY id
> LIMIT 20;
> ```

---

## 19. 🏋️ Exercise 2

Practice JOINs and Aggregates!

```sql
-- Setup
CREATE TABLE departments (
  id   BIGSERIAL PRIMARY KEY,
  name VARCHAR(100) NOT NULL
);

CREATE TABLE employees (
  id            BIGSERIAL PRIMARY KEY,
  name          VARCHAR(100) NOT NULL,
  salary        NUMERIC(10, 2),
  department_id BIGINT REFERENCES departments(id),
  hire_date     DATE DEFAULT CURRENT_DATE
);

INSERT INTO departments (name) VALUES
  ('Engineering'), ('Sales'), ('Marketing'), ('HR'), ('Finance');

INSERT INTO employees (name, salary, department_id, hire_date) VALUES
  ('Alice',   95000, 1, '2020-01-15'),
  ('Bob',     72000, 2, '2019-06-01'),
  ('Charlie', 88000, 1, '2021-03-10'),
  ('Diana',   65000, 3, '2022-07-20'),
  ('Edward',  78000, 2, '2018-11-05'),
  ('Fatima',  91000, 1, '2020-09-01'),
  ('George',  55000, 4, '2023-01-10'),
  ('Hannah',  82000, 5, '2021-05-15'),
  (  'Ivan',  69000, 3, '2022-03-25'),
  ('Julia',   110000, 1, '2017-08-12');

-- EXERCISES:
-- Q1. List all employees with their department name.
-- Q2. Find the average salary per department.
-- Q3. Find departments where average salary exceeds ₹80,000.
-- Q4. List the top 3 highest-paid employees.
-- Q5. Count employees per department, sorted by count descending.
-- Q6. Find departments that have more than 2 employees.
-- Q7. List employees hired before 2021 with their department.
-- Q8. Find the highest salary in each department.

-- ANSWERS:

-- Q1.
SELECT e.name, d.name AS department, e.salary
FROM employees e
JOIN departments d ON e.department_id = d.id;

-- Q2.
SELECT d.name, ROUND(AVG(e.salary), 2) AS avg_salary
FROM employees e
JOIN departments d ON e.department_id = d.id
GROUP BY d.name
ORDER BY avg_salary DESC;

-- Q3.
SELECT d.name, ROUND(AVG(e.salary), 2) AS avg_salary
FROM employees e
JOIN departments d ON e.department_id = d.id
GROUP BY d.name
HAVING AVG(e.salary) > 80000;

-- Q4.
SELECT name, salary FROM employees ORDER BY salary DESC LIMIT 3;

-- Q5.
SELECT d.name, COUNT(e.id) AS emp_count
FROM departments d
LEFT JOIN employees e ON d.id = e.department_id
GROUP BY d.name
ORDER BY emp_count DESC;

-- Q6.
SELECT d.name, COUNT(e.id) AS emp_count
FROM departments d
JOIN employees e ON d.id = e.department_id
GROUP BY d.name
HAVING COUNT(e.id) > 2;

-- Q7.
SELECT e.name, d.name AS department, e.hire_date
FROM employees e
JOIN departments d ON e.department_id = d.id
WHERE e.hire_date < '2021-01-01';

-- Q8.
SELECT d.name, MAX(e.salary) AS highest_salary
FROM employees e
JOIN departments d ON e.department_id = d.id
GROUP BY d.name;
```

---

## 20. 🔁 Subqueries

### 📌 Definition
A subquery is a query nested inside another query. It can appear in `SELECT`, `FROM`, `WHERE`, or `HAVING` clauses.

### 🔤 Syntax & Examples

```sql
-- Subquery in WHERE — find products more expensive than average
SELECT name, price
FROM products
WHERE price > (SELECT AVG(price) FROM products)
ORDER BY price DESC;

-- Subquery with IN — find customers who have placed orders
SELECT name FROM customers
WHERE id IN (SELECT DISTINCT customer_id FROM orders);

-- NOT IN — customers with NO orders
SELECT name FROM customers
WHERE id NOT IN (SELECT customer_id FROM orders WHERE customer_id IS NOT NULL);

-- Subquery in FROM clause (derived table / inline view)
SELECT category, avg_price
FROM (
  SELECT category, ROUND(AVG(price), 2) AS avg_price
  FROM products
  GROUP BY category
) AS category_stats
WHERE avg_price > 20000;

-- Correlated subquery — references outer query row by row
-- Find employees who earn more than their department's average
SELECT e.name, e.salary, e.department_id
FROM employees e
WHERE e.salary > (
  SELECT AVG(e2.salary)
  FROM employees e2
  WHERE e2.department_id = e.department_id -- References outer query
);

-- EXISTS — check if subquery returns any rows (faster than IN for large sets)
SELECT name FROM customers c
WHERE EXISTS (
  SELECT 1 FROM orders o WHERE o.customer_id = c.id
);

-- NOT EXISTS — customers with no orders
SELECT name FROM customers c
WHERE NOT EXISTS (
  SELECT 1 FROM orders o WHERE o.customer_id = c.id
);

-- Scalar subquery in SELECT
SELECT
  name,
  price,
  (SELECT COUNT(*) FROM orders WHERE product_id = p.id) AS times_ordered
FROM products p;
```

### 📊 Subquery vs JOIN

| Aspect | Subquery | JOIN |
|--------|----------|------|
| Readability | Easier for simple cases | Better for complex |
| Performance | Can be slower (especially correlated) | Usually faster |
| Use with | `IN`, `EXISTS`, scalar values | Combining columns from multiple tables |

> 💡 **Tip:** Use `EXISTS` instead of `IN` when checking against large subquery results — it short-circuits as soon as one match is found.

---

## 21. 👁️ Views

### 📌 Definition
A view is a saved SQL query that acts like a virtual table. It doesn't store data — it retrieves data dynamically from underlying tables.

### 📝 Theory
Views simplify complex queries, improve security (expose only needed columns), and provide a stable API even when the underlying schema changes.

### 🔤 Syntax & Examples

```sql
-- Create a view
CREATE VIEW product_summary AS
SELECT
  p.id,
  p.name,
  p.price,
  c.name     AS category,
  p.stock,
  p.is_active
FROM products p
JOIN categories c ON p.category_id = c.id;

-- Query the view just like a table
SELECT * FROM product_summary WHERE category = 'Electronics';
SELECT * FROM product_summary WHERE price > 50000 ORDER BY price;

-- Create or replace (update the view definition)
CREATE OR REPLACE VIEW product_summary AS
SELECT
  p.id,
  p.name,
  p.price,
  c.name   AS category,
  p.stock,
  p.created_at  -- New column added
FROM products p
JOIN categories c ON p.category_id = c.id;

-- Materialized View — stores the result physically (must refresh manually)
CREATE MATERIALIZED VIEW monthly_sales AS
SELECT
  DATE_TRUNC('month', order_date) AS month,
  SUM(total_amount)               AS revenue,
  COUNT(*)                        AS order_count
FROM orders
GROUP BY DATE_TRUNC('month', order_date)
ORDER BY month;

-- Refresh materialized view (update the stored data)
REFRESH MATERIALIZED VIEW monthly_sales;

-- Refresh without locking (allows reads during refresh)
REFRESH MATERIALIZED VIEW CONCURRENTLY monthly_sales;

-- Drop a view
DROP VIEW IF EXISTS product_summary;
DROP MATERIALIZED VIEW IF EXISTS monthly_sales;
```

### 📊 View vs Materialized View

| Feature | View | Materialized View |
|---------|------|-------------------|
| Data storage | ❌ None (always fresh) | ✅ Stored snapshot |
| Query speed | Depends on underlying tables | ⚡ Fast (pre-computed) |
| Data freshness | Always current | Stale until refreshed |
| Use case | Simplify queries, security | Expensive aggregation, reporting |
| Refresh needed | ❌ No | ✅ Yes (`REFRESH`) |

---

## 22. ⚡ Indexes

### 📌 Definition
An index is a data structure that speeds up data retrieval by providing fast lookup of rows based on column values — like an index in a book.

### 📝 Theory
Without an index, PostgreSQL does a full table scan (reads every row). With an index on the searched column, it jumps directly to matching rows. The trade-off: indexes speed up reads but slow down writes and use disk space.

### 🔤 Syntax & Examples

```sql
-- Default B-Tree index (best for =, <, >, BETWEEN, ORDER BY)
CREATE INDEX idx_products_category ON products(category);
CREATE INDEX idx_products_price    ON products(price);

-- Unique index (also enforces uniqueness)
CREATE UNIQUE INDEX idx_products_sku ON products(sku);

-- Composite index (multiple columns — order matters!)
CREATE INDEX idx_orders_customer_date ON orders(customer_id, order_date);
-- This index helps: WHERE customer_id = X AND order_date = Y
-- Also helps:       WHERE customer_id = X (leading column)
-- Does NOT help:    WHERE order_date = Y alone (not leading)

-- Partial index (only indexes rows matching condition — smaller, faster)
CREATE INDEX idx_active_products ON products(name)
WHERE is_active = TRUE;

-- Expression index (index on computed value)
CREATE INDEX idx_products_name_lower ON products(LOWER(name));
-- Now this query uses the index:
SELECT * FROM products WHERE LOWER(name) = 'iphone 15';

-- GIN index (for JSONB, arrays, full-text search)
CREATE INDEX idx_products_metadata ON products USING GIN(metadata);
CREATE INDEX idx_products_tags     ON products USING GIN(tags);

-- View existing indexes
SELECT indexname, tablename, indexdef
FROM pg_indexes
WHERE tablename = 'products';

-- Drop an index
DROP INDEX IF EXISTS idx_products_category;

-- Rebuild an index (useful after heavy writes)
REINDEX INDEX idx_products_category;
REINDEX TABLE products;
```

### 📊 Index Types

| Index Type | Best For | Example |
|------------|----------|---------|
| `BTREE` (default) | `=`, `<`, `>`, `BETWEEN`, `ORDER BY` | Most columns |
| `HASH` | `=` only (faster than BTREE for equality) | UUID lookups |
| `GIN` | Arrays, JSONB, full-text search | `tags @> ARRAY['sale']` |
| `GIST` | Geometric data, ranges | PostGIS, date ranges |
| `BRIN` | Very large tables with sequential data | `created_at` on logs |

### ⚠️ Important Points
- Don't over-index — each index slows down INSERT/UPDATE/DELETE.
- Index columns that appear in `WHERE`, `JOIN ON`, `ORDER BY` frequently.
- Composite indexes: put the most selective column first.
- PostgreSQL automatically creates indexes for `PRIMARY KEY` and `UNIQUE` constraints.

---

## 23. 💱 Transactions

### 📌 Definition
A transaction is a group of SQL operations that execute as a single unit — either all succeed or all fail (rolled back).

### 📝 Theory
Transactions implement ACID properties: Atomicity (all or nothing), Consistency (data stays valid), Isolation (transactions don't interfere), Durability (committed data is permanent).

### 🔤 Syntax & Examples

```sql
-- Basic transaction
BEGIN;  -- Start transaction

  UPDATE accounts SET balance = balance - 5000 WHERE id = 1;  -- Debit
  UPDATE accounts SET balance = balance + 5000 WHERE id = 2;  -- Credit

COMMIT; -- Save all changes permanently

-- Rollback on error
BEGIN;

  UPDATE accounts SET balance = balance - 5000 WHERE id = 1;

  -- Oops! Something went wrong...
ROLLBACK; -- Undo everything since BEGIN

-- SAVEPOINT — partial rollback
BEGIN;

  INSERT INTO orders (customer_id, total) VALUES (1, 5000);
  SAVEPOINT after_order; -- Create a checkpoint

  INSERT INTO order_items VALUES (currval('orders_id_seq'), 1, 2, 2500);
  -- If this fails, roll back to savepoint (not entire transaction)
  ROLLBACK TO SAVEPOINT after_order;

  -- Continue with different approach...
  INSERT INTO order_items VALUES (currval('orders_id_seq'), 2, 1, 5000);

COMMIT;

-- Transaction with error handling (PL/pgSQL)
DO $$
BEGIN
  BEGIN  -- Inner block for exception handling
    UPDATE accounts SET balance = balance - 10000 WHERE id = 1;

    IF (SELECT balance FROM accounts WHERE id = 1) < 0 THEN
      RAISE EXCEPTION 'Insufficient funds!';
    END IF;

    UPDATE accounts SET balance = balance + 10000 WHERE id = 2;

  EXCEPTION
    WHEN OTHERS THEN
      RAISE NOTICE 'Transaction failed: %', SQLERRM;
      -- Inner block automatically rolls back
  END;
END;
$$;
```

### ⚠️ Important Points
- Every statement in PostgreSQL runs in an implicit transaction if not inside an explicit `BEGIN`.
- If any statement fails inside a transaction, PostgreSQL marks it as aborted — no more queries will execute until `ROLLBACK`.
- `COMMIT` makes changes permanent; `ROLLBACK` undoes all changes since `BEGIN`.

---

## 24. ⚙️ Stored Procedures & Functions

### 📌 Definition
- **Function:** Returns a value; can be used in SELECT statements.
- **Stored Procedure:** Executes logic; cannot return a value directly (Postgres 11+); called with `CALL`.

### 🔤 Syntax & Examples

#### Functions
```sql
-- Simple function: calculate discount price
CREATE OR REPLACE FUNCTION apply_discount(price NUMERIC, discount_pct NUMERIC)
RETURNS NUMERIC AS $$
BEGIN
  RETURN price - (price * discount_pct / 100);
END;
$$ LANGUAGE plpgsql;

-- Use in SELECT
SELECT name, price, apply_discount(price, 10) AS discounted_price
FROM products;

-- Function returning a table
CREATE OR REPLACE FUNCTION get_products_by_category(cat_name VARCHAR)
RETURNS TABLE(id BIGINT, name VARCHAR, price NUMERIC) AS $$
BEGIN
  RETURN QUERY
    SELECT p.id, p.name, p.price
    FROM products p
    JOIN categories c ON p.category_id = c.id
    WHERE c.name = cat_name;
END;
$$ LANGUAGE plpgsql;

-- Use like a table
SELECT * FROM get_products_by_category('Electronics');

-- Function with security check
CREATE OR REPLACE FUNCTION transfer_funds(
  from_id BIGINT,
  to_id   BIGINT,
  amount  NUMERIC
) RETURNS TEXT AS $$
DECLARE
  from_balance NUMERIC;
BEGIN
  SELECT balance INTO from_balance FROM accounts WHERE id = from_id;

  IF from_balance < amount THEN
    RETURN 'Error: Insufficient funds';
  END IF;

  UPDATE accounts SET balance = balance - amount WHERE id = from_id;
  UPDATE accounts SET balance = balance + amount WHERE id = to_id;

  RETURN 'Transfer successful';
END;
$$ LANGUAGE plpgsql;

SELECT transfer_funds(1, 2, 5000);
```

#### Stored Procedures (PostgreSQL 11+)
```sql
-- Stored procedure
CREATE OR REPLACE PROCEDURE process_monthly_payroll(month_date DATE)
LANGUAGE plpgsql AS $$
DECLARE
  emp RECORD;
BEGIN
  FOR emp IN SELECT * FROM employees WHERE is_active = TRUE LOOP
    INSERT INTO payroll_records (employee_id, month, amount, processed_at)
    VALUES (emp.id, month_date, emp.salary, NOW());
  END LOOP;

  RAISE NOTICE 'Payroll processed for %', month_date;
END;
$$;

-- Call a procedure
CALL process_monthly_payroll('2024-01-01');
```

### 📊 Function vs Stored Procedure

| Feature | Function | Stored Procedure |
|---------|----------|-----------------|
| Returns value | ✅ Yes | ❌ Not directly |
| Use in SELECT | ✅ Yes | ❌ No |
| Transaction control | ❌ Limited | ✅ Full (COMMIT/ROLLBACK inside) |
| Called with | `SELECT func()` | `CALL proc()` |

---

## 25. ⚡ Triggers

### 📌 Definition
A trigger is a function that automatically executes when a specified event (INSERT, UPDATE, DELETE) occurs on a table.

### 🔤 Syntax & Examples

```sql
-- Step 1: Create the trigger function
CREATE OR REPLACE FUNCTION update_timestamp()
RETURNS TRIGGER AS $$
BEGIN
  NEW.updated_at = NOW(); -- Modify the new row before saving
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;

-- Step 2: Attach the trigger to a table
CREATE TRIGGER products_update_timestamp
  BEFORE UPDATE ON products    -- Fires BEFORE each UPDATE row
  FOR EACH ROW
  EXECUTE FUNCTION update_timestamp();

-- Audit log trigger
CREATE TABLE audit_log (
  id          BIGSERIAL PRIMARY KEY,
  table_name  VARCHAR(100),
  operation   VARCHAR(10),
  old_data    JSONB,
  new_data    JSONB,
  changed_at  TIMESTAMPTZ DEFAULT NOW(),
  changed_by  VARCHAR(100) DEFAULT CURRENT_USER
);

CREATE OR REPLACE FUNCTION log_changes()
RETURNS TRIGGER AS $$
BEGIN
  IF TG_OP = 'DELETE' THEN
    INSERT INTO audit_log (table_name, operation, old_data)
    VALUES (TG_TABLE_NAME, 'DELETE', row_to_json(OLD)::jsonb);
    RETURN OLD;
  ELSIF TG_OP = 'UPDATE' THEN
    INSERT INTO audit_log (table_name, operation, old_data, new_data)
    VALUES (TG_TABLE_NAME, 'UPDATE', row_to_json(OLD)::jsonb, row_to_json(NEW)::jsonb);
    RETURN NEW;
  ELSIF TG_OP = 'INSERT' THEN
    INSERT INTO audit_log (table_name, operation, new_data)
    VALUES (TG_TABLE_NAME, 'INSERT', row_to_json(NEW)::jsonb);
    RETURN NEW;
  END IF;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER products_audit
  AFTER INSERT OR UPDATE OR DELETE ON products
  FOR EACH ROW
  EXECUTE FUNCTION log_changes();

-- Drop a trigger
DROP TRIGGER IF EXISTS products_audit ON products;

-- List all triggers
SELECT trigger_name, event_manipulation, event_object_table
FROM information_schema.triggers
ORDER BY event_object_table;
```

### 📊 Trigger Timing Options

| Timing | Fires | Use Case |
|--------|-------|----------|
| `BEFORE` | Before the operation | Validate/modify data before saving |
| `AFTER` | After the operation | Audit logs, notifications |
| `INSTEAD OF` | Instead of the operation | On views |
| `FOR EACH ROW` | Once per affected row | Most common |
| `FOR EACH STATEMENT` | Once per SQL statement | Summary logging |

---

## 26. 📝 CTEs (Common Table Expressions)

### 📌 Definition
A CTE (Common Table Expression) is a temporary named result set defined with the `WITH` clause, used to simplify complex queries by breaking them into readable steps.

### 🔤 Syntax & Examples

```sql
-- Basic CTE
WITH high_value_products AS (
  SELECT * FROM products WHERE price > 50000
)
SELECT name, price FROM high_value_products ORDER BY price DESC;

-- Multiple CTEs chained
WITH
  dept_salaries AS (
    SELECT department_id, AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
  ),
  dept_info AS (
    SELECT d.name, ds.avg_salary
    FROM departments d
    JOIN dept_salaries ds ON d.id = ds.department_id
  )
SELECT * FROM dept_info WHERE avg_salary > 80000;

-- CTE for readability — monthly revenue report
WITH
  orders_2024 AS (
    SELECT * FROM orders
    WHERE order_date BETWEEN '2024-01-01' AND '2024-12-31'
  ),
  monthly_revenue AS (
    SELECT
      DATE_TRUNC('month', order_date) AS month,
      SUM(total_amount)               AS revenue,
      COUNT(*)                        AS order_count
    FROM orders_2024
    GROUP BY DATE_TRUNC('month', order_date)
  )
SELECT
  TO_CHAR(month, 'Mon YYYY') AS month,
  revenue,
  order_count,
  ROUND(revenue / order_count, 2) AS avg_order_value
FROM monthly_revenue
ORDER BY month;

-- Recursive CTE — hierarchical data (e.g., org chart, categories tree)
WITH RECURSIVE org_chart AS (
  -- Base case: top-level employees (no manager)
  SELECT id, name, manager_id, 0 AS level, name::TEXT AS path
  FROM employees
  WHERE manager_id IS NULL

  UNION ALL

  -- Recursive case: employees with managers
  SELECT e.id, e.name, e.manager_id, oc.level + 1,
         oc.path || ' > ' || e.name
  FROM employees e
  JOIN org_chart oc ON e.manager_id = oc.id
)
SELECT
  REPEAT('  ', level) || name AS employee,
  level,
  path
FROM org_chart
ORDER BY path;
```

### ⚠️ Important Points
- CTEs improve readability — complex queries become step-by-step.
- In PostgreSQL, CTEs are by default "optimization fences" — each CTE executes independently. Add `NOT MATERIALIZED` to let PostgreSQL optimize them.
- Recursive CTEs require a base case + recursive case with `UNION ALL`.

---

## 27. 🪟 Window Functions

### 📌 Definition
Window functions perform calculations across a set of table rows related to the current row — without collapsing them into a single result like GROUP BY does.

### 📝 Theory
Window functions operate "over a window" of rows defined by `OVER()`. They're used for rankings, running totals, moving averages, and comparisons with neighboring rows.

### 🔤 Syntax & Examples

```sql
-- Basic syntax
function_name() OVER (
  PARTITION BY column  -- Group rows (like GROUP BY, but keeps all rows)
  ORDER BY column      -- Sort within partition
  ROWS BETWEEN ...     -- Define row range (optional)
)

-- ROW_NUMBER — unique sequential number
SELECT
  name, department_id, salary,
  ROW_NUMBER() OVER (PARTITION BY department_id ORDER BY salary DESC) AS rank_in_dept
FROM employees;

-- RANK — same rank for ties, gaps in sequence
-- DENSE_RANK — same rank for ties, no gaps
SELECT
  name, salary,
  RANK()       OVER (ORDER BY salary DESC) AS rank,
  DENSE_RANK() OVER (ORDER BY salary DESC) AS dense_rank,
  ROW_NUMBER() OVER (ORDER BY salary DESC) AS row_num
FROM employees;

-- NTILE — divide into N equal buckets
SELECT name, salary,
  NTILE(4) OVER (ORDER BY salary) AS salary_quartile -- 1=lowest, 4=highest
FROM employees;

-- LAG / LEAD — access previous / next row
SELECT
  name,
  salary,
  LAG(salary)  OVER (ORDER BY hire_date) AS previous_hire_salary,
  LEAD(salary) OVER (ORDER BY hire_date) AS next_hire_salary,
  salary - LAG(salary) OVER (ORDER BY hire_date) AS salary_diff
FROM employees;

-- Running total (cumulative sum)
SELECT
  name,
  hire_date,
  salary,
  SUM(salary) OVER (ORDER BY hire_date) AS running_total_payroll
FROM employees;

-- Moving average (3-row window)
SELECT
  name,
  salary,
  ROUND(
    AVG(salary) OVER (ORDER BY id ROWS BETWEEN 2 PRECEDING AND CURRENT ROW),
    2
  ) AS moving_avg_3
FROM employees;

-- Percentage of total
SELECT
  name,
  department_id,
  salary,
  ROUND(100.0 * salary / SUM(salary) OVER (PARTITION BY department_id), 2) AS pct_of_dept
FROM employees;

-- TOP N per group (top 2 earners per department)
SELECT * FROM (
  SELECT
    name, department_id, salary,
    ROW_NUMBER() OVER (PARTITION BY department_id ORDER BY salary DESC) AS rn
  FROM employees
) ranked
WHERE rn <= 2;
```

### 📊 Common Window Functions

| Function | Purpose |
|----------|---------|
| `ROW_NUMBER()` | Unique rank (no ties) |
| `RANK()` | Rank with gaps for ties |
| `DENSE_RANK()` | Rank without gaps |
| `NTILE(n)` | Divide into n buckets |
| `LAG(col, n)` | Value from n rows before |
| `LEAD(col, n)` | Value from n rows ahead |
| `SUM() OVER()` | Running/cumulative total |
| `AVG() OVER()` | Moving average |
| `FIRST_VALUE()` | First value in window |
| `LAST_VALUE()` | Last value in window |

---

## 28. 📄 JSON & JSONB

### 📌 Definition
PostgreSQL natively supports JSON data. `JSONB` stores JSON in binary format — faster for querying and supports indexing.

### 📝 Theory
Use `JSONB` (not `JSON`) in almost all cases — it's faster for reads, supports indexing, and deduplicates keys.

### 🔤 Syntax & Examples

```sql
-- Table with JSONB column
CREATE TABLE products (
  id       BIGSERIAL PRIMARY KEY,
  name     VARCHAR(200),
  metadata JSONB
);

-- Insert JSON data
INSERT INTO products (name, metadata) VALUES
  ('iPhone 15', '{"color": "black", "storage": "256GB", "features": ["5G", "Face ID"]}'),
  ('MacBook Pro', '{"color": "silver", "ram": "16GB", "specs": {"cpu": "M3", "screen": "14 inch"}}');

-- Accessing JSON fields
SELECT
  name,
  metadata -> 'color'             AS color_json,    -- Returns JSON (with quotes)
  metadata ->> 'color'            AS color_text,    -- Returns TEXT (no quotes)
  metadata -> 'specs' ->> 'cpu'   AS cpu            -- Nested access
FROM products;

-- Query by JSON field value
SELECT * FROM products WHERE metadata ->> 'color' = 'black';
SELECT * FROM products WHERE (metadata -> 'specs' ->> 'cpu') = 'M3';

-- Check if key exists
SELECT * FROM products WHERE metadata ? 'storage';          -- Has key 'storage'
SELECT * FROM products WHERE metadata ?| ARRAY['5G', 'wifi']; -- Has any key

-- Check if JSON contains value
SELECT * FROM products
WHERE metadata @> '{"color": "black"}';  -- Contains this JSON

-- Array operations
SELECT * FROM products
WHERE metadata -> 'features' @> '["5G"]'; -- features array contains '5G'

-- Update JSONB
UPDATE products
SET metadata = metadata || '{"discount": 10}'  -- Merge/add key
WHERE name = 'iPhone 15';

UPDATE products
SET metadata = metadata - 'discount'            -- Remove a key
WHERE name = 'iPhone 15';

-- GIN index for JSONB (fast @> queries)
CREATE INDEX idx_products_metadata_gin ON products USING GIN(metadata);

-- Extract all keys
SELECT jsonb_object_keys(metadata) FROM products WHERE id = 1;

-- Convert table to JSON
SELECT json_agg(row_to_json(p)) AS products_json
FROM products p;
```

### 📊 JSON vs JSONB

| Feature | JSON | JSONB |
|---------|------|-------|
| Storage | Text (exact) | Binary (parsed) |
| Write speed | ⚡ Faster | Slightly slower |
| Read speed | Slower | ⚡ Faster |
| Indexing | ❌ No GIN | ✅ GIN supported |
| Key order | Preserved | Not preserved |
| Duplicate keys | Allowed | Last value wins |
| **Use in production** | ❌ Rarely | ✅ Almost always |

---

## 29. 🔍 Full-Text Search

### 📌 Definition
Full-text search enables searching through large text content intelligently — finding relevant documents based on meaning, not just exact matches.

### 🔤 Syntax & Examples

```sql
-- tsvector: a processed document ready for search
-- tsquery: a search query

-- Basic full-text search
SELECT name, description
FROM products
WHERE to_tsvector('english', name || ' ' || COALESCE(description, ''))
      @@ to_tsquery('english', 'wireless & headphones');

-- Create a dedicated search column (better performance)
ALTER TABLE products ADD COLUMN search_vector TSVECTOR;

-- Populate it
UPDATE products
SET search_vector = to_tsvector('english',
  COALESCE(name, '') || ' ' ||
  COALESCE(description, '') || ' ' ||
  COALESCE(category, '')
);

-- GIN index for full-text search
CREATE INDEX idx_products_fts ON products USING GIN(search_vector);

-- Search queries
SELECT name FROM products WHERE search_vector @@ to_tsquery('english', 'wireless');
SELECT name FROM products WHERE search_vector @@ to_tsquery('english', 'wireless & headphones');
SELECT name FROM products WHERE search_vector @@ to_tsquery('english', 'apple | samsung');
SELECT name FROM products WHERE search_vector @@ to_tsquery('english', 'head:*'); -- Prefix search

-- Ranking results by relevance
SELECT
  name,
  ts_rank(search_vector, query) AS rank
FROM products, to_tsquery('english', 'wireless headphones') query
WHERE search_vector @@ query
ORDER BY rank DESC;

-- Highlight matching terms
SELECT
  name,
  ts_headline('english', description,
    to_tsquery('english', 'wireless'),
    'StartSel=<mark>, StopSel=</mark>'
  ) AS highlighted
FROM products
WHERE search_vector @@ to_tsquery('english', 'wireless');

-- Auto-update search vector with trigger
CREATE OR REPLACE FUNCTION update_search_vector()
RETURNS TRIGGER AS $$
BEGIN
  NEW.search_vector = to_tsvector('english',
    COALESCE(NEW.name, '') || ' ' || COALESCE(NEW.description, '')
  );
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER products_search_update
  BEFORE INSERT OR UPDATE ON products
  FOR EACH ROW EXECUTE FUNCTION update_search_vector();
```

---

## 30. 👤 Roles & Permissions

### 📌 Definition
PostgreSQL uses roles (users and groups) to control who can access and modify database objects.

### 🔤 Syntax & Examples

```sql
-- Create a role (user)
CREATE ROLE app_user WITH LOGIN PASSWORD 'SecurePassword123!';

-- Create a role without login (group)
CREATE ROLE readonly_group;

-- Grant group role to user
GRANT readonly_group TO app_user;

-- Common privileges
GRANT CONNECT ON DATABASE mydb TO app_user;
GRANT USAGE   ON SCHEMA public TO app_user;

-- Table-level permissions
GRANT SELECT ON ALL TABLES IN SCHEMA public TO readonly_group;
GRANT SELECT, INSERT, UPDATE, DELETE ON products TO app_user;

-- Grant specific columns only (column-level security)
GRANT SELECT (name, price, category) ON products TO readonly_group;
-- readonly_group can only read those 3 columns

-- Revoke permissions
REVOKE DELETE ON products FROM app_user;

-- Grant future table permissions automatically
ALTER DEFAULT PRIVILEGES IN SCHEMA public
  GRANT SELECT ON TABLES TO readonly_group;

-- Row Level Security (RLS) — users see only their own data
ALTER TABLE orders ENABLE ROW LEVEL SECURITY;

CREATE POLICY user_own_orders ON orders
  FOR ALL
  USING (customer_id = current_setting('app.current_user_id')::BIGINT);

-- Superuser actions
ALTER ROLE app_user CREATEDB;          -- Allow creating databases
ALTER ROLE app_user WITH SUPERUSER;    -- Make superuser (use carefully!)
ALTER ROLE app_user WITH NOSUPERUSER;  -- Remove superuser

-- List all roles
\du  -- In psql

-- Or via SQL:
SELECT rolname, rolsuper, rolcreatedb, rolcanlogin
FROM pg_roles ORDER BY rolname;
```

### 📊 Permission Types

| Privilege | Applies To | Meaning |
|-----------|-----------|---------|
| `SELECT` | Table/View | Read rows |
| `INSERT` | Table | Add rows |
| `UPDATE` | Table | Modify rows |
| `DELETE` | Table | Remove rows |
| `TRUNCATE` | Table | Empty table |
| `REFERENCES` | Table | Create foreign keys |
| `TRIGGER` | Table | Create triggers |
| `CONNECT` | Database | Connect to DB |
| `USAGE` | Schema | Access schema |
| `EXECUTE` | Function | Call function |

---

## 31. 🚀 Performance & EXPLAIN

### 📌 Definition
Query analysis and optimization techniques to identify and fix slow queries in PostgreSQL.

### 🔤 Syntax & Examples

```sql
-- EXPLAIN — show query plan (estimated)
EXPLAIN SELECT * FROM products WHERE price > 50000;

-- EXPLAIN ANALYZE — actually run and show real stats
EXPLAIN ANALYZE SELECT * FROM products WHERE price > 50000;

-- EXPLAIN with more detail
EXPLAIN (ANALYZE, BUFFERS, FORMAT TEXT)
SELECT p.name, c.name
FROM products p
JOIN categories c ON p.category_id = c.id
WHERE p.price > 50000;

-- Understanding EXPLAIN output:
-- Seq Scan      → Full table scan (no index used — potentially slow)
-- Index Scan    → Used an index (fast)
-- Bitmap Scan   → Used an index for multiple rows
-- Hash Join     → Join method (good for large datasets)
-- Nested Loop   → Join method (good for small datasets)
-- cost=X..Y     → X=startup cost, Y=total cost (higher = slower)
-- rows=N        → Estimated rows returned
-- actual rows=N → Real rows (from ANALYZE)

-- Performance best practices:

-- 1. Check for missing indexes
SELECT schemaname, tablename, attname, n_distinct, correlation
FROM pg_stats
WHERE tablename = 'products';

-- 2. Find slow queries (requires pg_stat_statements extension)
CREATE EXTENSION IF NOT EXISTS pg_stat_statements;

SELECT query, mean_exec_time, calls, total_exec_time
FROM pg_stat_statements
ORDER BY mean_exec_time DESC
LIMIT 10;

-- 3. Check index usage
SELECT indexrelname, idx_scan, idx_tup_read
FROM pg_stat_user_indexes
WHERE relname = 'products'
ORDER BY idx_scan DESC;

-- 4. Find unused indexes (candidates for removal)
SELECT indexrelname, idx_scan
FROM pg_stat_user_indexes
WHERE idx_scan = 0
  AND schemaname = 'public';

-- 5. Table bloat — run VACUUM to reclaim space
VACUUM products;
VACUUM ANALYZE products; -- Also updates statistics
VACUUM FULL products;    -- Full rewrite (locks table — use off-peak)

-- 6. Analyze table (update planner statistics)
ANALYZE products;
```

### 📊 Performance Checklist

| Issue | Symptom | Fix |
|-------|---------|-----|
| Missing index | `Seq Scan` on large table | Add index on filtered/joined column |
| Stale statistics | Wrong row estimates | Run `ANALYZE` |
| Table bloat | Slow scans after many UPDATEs | Run `VACUUM` |
| N+1 queries | Many small queries | Use JOINs or subqueries |
| No connection pool | Too many connections | Use PgBouncer |

---

## 32. 💾 Backup & Restore

### 📌 Definition
Backing up PostgreSQL databases and restoring them when needed.

### 🔤 Syntax & Examples

```bash
# ============================================
# pg_dump — backup a single database
# ============================================

# Plain SQL backup (human-readable)
pg_dump -U postgres -d mydb > mydb_backup.sql

# Compressed backup (recommended for large DBs)
pg_dump -U postgres -d mydb -F c -f mydb_backup.dump
# -F c = custom format (compressed, allows selective restore)

# Include only specific tables
pg_dump -U postgres -d mydb -t products -t categories -F c -f partial.dump

# Backup schema only (no data)
pg_dump -U postgres -d mydb --schema-only -f schema_only.sql

# Backup data only (no schema)
pg_dump -U postgres -d mydb --data-only -f data_only.sql

# ============================================
# pg_dumpall — backup ALL databases + roles
# ============================================
pg_dumpall -U postgres > full_backup.sql

# ============================================
# Restore
# ============================================

# Restore plain SQL backup
psql -U postgres -d mydb < mydb_backup.sql

# Restore custom format backup
pg_restore -U postgres -d mydb mydb_backup.dump

# Restore to a new database
createdb -U postgres newdb
pg_restore -U postgres -d newdb mydb_backup.dump

# Restore only specific table
pg_restore -U postgres -d mydb -t products mydb_backup.dump

# Verbose restore (see progress)
pg_restore -U postgres -d mydb -v mydb_backup.dump

# ============================================
# Automated backup script (bash)
# ============================================
# Save as: /etc/cron.daily/pg_backup.sh
#!/bin/bash
DATE=$(date +%Y%m%d_%H%M%S)
BACKUP_DIR="/var/backups/postgres"
mkdir -p $BACKUP_DIR

pg_dump -U postgres -d mydb -F c \
  -f "${BACKUP_DIR}/mydb_${DATE}.dump"

# Keep only last 7 days
find $BACKUP_DIR -name "*.dump" -mtime +7 -delete

echo "Backup complete: mydb_${DATE}.dump"
```

### 📊 Backup Methods Comparison

| Method | Command | Format | Selective Restore | Size |
|--------|---------|--------|-------------------|------|
| Plain SQL | `pg_dump` | `.sql` | ❌ No | Large |
| Custom | `pg_dump -F c` | `.dump` | ✅ Yes | Compressed |
| Directory | `pg_dump -F d` | Dir | ✅ Yes | Compressed |
| All DBs | `pg_dumpall` | `.sql` | ❌ No | Large |

> 💡 **Best Practice:** Always use custom format (`-F c`) for production backups — it's compressed, faster to restore, and supports selective table restore. Test your restores regularly!

---

## 33. 🏁 Conclusion & Resources

### 🎉 Congratulations!

You've completed the PostgreSQL journey from basics to advanced! Here's a summary of what you've mastered:

✅ Installation & psql CLI
✅ Databases, Data Types, Tables
✅ CRUD — INSERT, SELECT, UPDATE, DELETE
✅ Constraints — PK, FK, CHECK, UNIQUE
✅ Relationships — 1:1, 1:N, M:N
✅ JOINs — INNER, LEFT, RIGHT, FULL, SELF
✅ Aggregates — COUNT, SUM, AVG, MIN, MAX
✅ GROUP BY, HAVING, ORDER BY, LIMIT
✅ Subqueries & CTEs
✅ Views & Materialized Views
✅ Indexes & Performance
✅ Transactions (ACID)
✅ Stored Procedures & Functions
✅ Triggers
✅ Window Functions
✅ JSON / JSONB
✅ Full-Text Search
✅ Roles & Permissions
✅ Backup & Restore

---

### 🗺️ What's Next?

1. **PostGIS** — Geospatial queries and mapping
2. **pg_partitioning** — Partition large tables for performance
3. **Logical Replication** — Real-time database replication
4. **Connection Pooling** — PgBouncer for scaling
5. **PostgreSQL with ORMs** — Prisma, SQLAlchemy, TypeORM, Django ORM
6. **PostgreSQL + Node.js** — Using `pg`, `postgres`, or `Drizzle ORM`
7. **TimescaleDB** — Time-series data on PostgreSQL

---

### 📚 Recommended Resources

#### Official Documentation
- 🌐 [PostgreSQL Official Docs](https://www.postgresql.org/docs/) — The definitive reference
- 🌐 [PostgreSQL Tutorial](https://www.postgresqltutorial.com/) — Beginner to advanced with examples
- 🌐 [PostgreSQL Wiki](https://wiki.postgresql.org/) — Community knowledge base

#### Interactive Learning
- 🌐 [pgexercises.com](https://pgexercises.com/) — 80+ SQL exercises with instant feedback
- 🌐 [SQLZoo](https://sqlzoo.net/) — Interactive SQL tutorials
- 🌐 [Mode Analytics SQL Tutorial](https://mode.com/sql-tutorial/) — Real-world SQL practice

#### Tools
- 🛠️ [pgAdmin 4](https://www.pgadmin.org/) — Official GUI for PostgreSQL
- 🛠️ [DBeaver](https://dbeaver.io/) — Free universal DB tool
- 🛠️ [TablePlus](https://tableplus.com/) — Modern, lightweight DB GUI
- 🛠️ [Postico 2](https://eggerapps.at/postico2/) — macOS PostgreSQL client

#### Books
- 📖 *PostgreSQL: Up and Running* — Regina O. Obe & Leo S. Hsu
- 📖 *The Art of PostgreSQL* — Dimitri Fontaine
- 📖 *Learning PostgreSQL* — Salahaldin Juba

#### Video Courses
- 🎥 [FreeCodeCamp PostgreSQL Course (YouTube)](https://www.youtube.com/watch?v=qw--VYLpxG4) — Free 4-hour course
- 🎥 [Amigoscode PostgreSQL (YouTube)](https://www.youtube.com/c/amigoscode) — Great beginner content

#### Community
- 💬 [PostgreSQL Mailing Lists](https://www.postgresql.org/list/) — Official community
- 💬 [r/PostgreSQL](https://www.reddit.com/r/PostgreSQL/) — Active community
- 💬 [DBA Stack Exchange](https://dba.stackexchange.com/) — Expert Q&A

---

### 💡 Final Tips for Your PostgreSQL Journey

1. **Practice on real data** — Import a public dataset (e.g., Northwind, DVD Rental) and query it.
2. **Always use EXPLAIN** — Before deploying a query, check its plan.
3. **Index thoughtfully** — Index columns in WHERE and JOIN, not everything.
4. **Use transactions** — Any multi-step write operation should be in a transaction.
5. **Back up regularly** — And test your restores — a backup you've never restored is an untested backup.
6. **Never use `SELECT *` in production** — Name your columns explicitly.
7. **Use `TIMESTAMPTZ`** — Always store timestamps with timezone info.

---

*Happy Querying! 🐘 PostgreSQL is not just a database — it's a platform.*

---

> 📝 **Maintained by:** Community Contributors
> 📅 **Last Updated:** 2024
> 🐘 **PostgreSQL Version:** 16.x
> 📄 **License:** MIT
