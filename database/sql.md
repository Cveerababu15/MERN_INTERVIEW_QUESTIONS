# SQL Interview Questions

> **Level:** Fresher / Junior Developer
> **Focus:** Important SQL concepts + commonly asked interview questions
> **Purpose:** Learn SQL concepts and practise writing queries.

---

# 1. What is SQL?

SQL stands for **Structured Query Language**.

It is used to communicate with relational databases.

SQL can be used to:

* Create databases and tables
* Insert data
* Read data
* Update data
* Delete data
* Filter data
* Sort data
* Join tables
* Aggregate data

Example:

```sql
SELECT * FROM users;
```

### Interview Point

> SQL is a language used to store, retrieve, manipulate, and manage data in relational databases.

---

# 2. What is a relational database?

A relational database stores data in **tables**.

Each table contains:

```text
Rows
+
Columns
```

Example:

```text
users

id | name  | email
---|-------|----------------
1  | Veera | veera@gmail.com
2  | Rahul | rahul@gmail.com
```

Tables can also be related to each other using keys.

---

# 3. What is a table?

A table is a collection of related data organised into rows and columns.

Example:

```sql
CREATE TABLE users (
    id INT,
    name VARCHAR(100),
    email VARCHAR(100)
);
```

---

# 4. What is a row?

A row represents one complete record in a table.

Example:

```text
1 | Veera | veera@gmail.com
```

This represents one user.

---

# 5. What is a column?

A column represents a particular attribute of the data.

Example:

```text
id
name
email
```

Each column has a specific data type.

---

# 6. What are SQL commands?

SQL commands are commonly grouped into:

```text
DDL
DML
DQL
DCL
TCL
```

### DDL

Data Definition Language.

```text
CREATE
ALTER
DROP
TRUNCATE
```

### DML

Data Manipulation Language.

```text
INSERT
UPDATE
DELETE
```

### DQL

Data Query Language.

```text
SELECT
```

### DCL

Data Control Language.

```text
GRANT
REVOKE
```

### TCL

Transaction Control Language.

```text
COMMIT
ROLLBACK
SAVEPOINT
```

---

# 7. What is DDL?

DDL is used to define or modify database structures.

Examples:

```sql
CREATE TABLE users (
    id INT,
    name VARCHAR(100)
);
```

```sql
ALTER TABLE users
ADD email VARCHAR(100);
```

```sql
DROP TABLE users;
```

---

# 8. What is DML?

DML is used to modify data inside tables.

Examples:

```sql
INSERT INTO users
VALUES (1, 'Veera', 'veera@gmail.com');
```

```sql
UPDATE users
SET name = 'Rahul'
WHERE id = 1;
```

```sql
DELETE FROM users
WHERE id = 1;
```

---

# 9. What is DQL?

DQL is used to retrieve data.

Main command:

```sql
SELECT
```

Example:

```sql
SELECT * FROM users;
```

---

# 10. What is a primary key?

A primary key uniquely identifies each row in a table.

Example:

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100)
);
```

Important properties:

```text
Unique
Not NULL
Identifies one record
```

---

# 11. What is a foreign key?

A foreign key creates a relationship between tables.

Example:

```sql
CREATE TABLE orders (
    id INT PRIMARY KEY,
    user_id INT,
    FOREIGN KEY (user_id)
    REFERENCES users(id)
);
```

Here:

```text
users.id
   ↑
   |
orders.user_id
```

---

# 12. Primary key vs foreign key

| Primary Key                          | Foreign Key                        |
| ------------------------------------ | ---------------------------------- |
| Identifies a row                     | References another table           |
| Must be unique                       | Can contain duplicate values       |
| Cannot be NULL                       | Can be NULL depending on design    |
| One primary key constraint per table | Multiple foreign keys are possible |

---

# 13. What is a UNIQUE constraint?

It ensures that values in a column are unique.

Example:

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE
);
```

Two users cannot have the same email.

---

# 14. What is a NOT NULL constraint?

It prevents a column from containing NULL values.

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);
```

---

# 15. What is a DEFAULT constraint?

It provides a default value when no value is supplied.

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    role VARCHAR(20) DEFAULT 'user'
);
```

---

# 16. What is CHECK constraint?

It restricts values based on a condition.

Example:

```sql
CREATE TABLE users (
    id INT,
    age INT CHECK (age >= 18)
);
```

---

# 17. What is SELECT?

`SELECT` retrieves data.

```sql
SELECT * FROM users;
```

Select specific columns:

```sql
SELECT name, email
FROM users;
```

---

# 18. What is WHERE?

`WHERE` filters records.

```sql
SELECT *
FROM users
WHERE age > 18;
```

Only matching records are returned.

---

# 19. What are comparison operators?

Common operators:

```text
=
!=
<>
>
<
>=
<=
```

Example:

```sql
SELECT *
FROM products
WHERE price > 1000;
```

---

# 20. What are logical operators?

Common operators:

```text
AND
OR
NOT
```

Example:

```sql
SELECT *
FROM users
WHERE age > 18
AND city = 'Bangalore';
```

---

# 21. What is ORDER BY?

It sorts query results.

Ascending:

```sql
SELECT *
FROM users
ORDER BY age ASC;
```

Descending:

```sql
SELECT *
FROM users
ORDER BY age DESC;
```

---

# 22. What is DISTINCT?

`DISTINCT` removes duplicate values from the result.

```sql
SELECT DISTINCT city
FROM users;
```

---

# 23. What is LIKE?

`LIKE` performs pattern matching.

```sql
SELECT *
FROM users
WHERE name LIKE 'V%';
```

Meaning:

```text
Starts with V
```

Examples:

```text
V%   → starts with V
%a   → ends with a
%ee% → contains ee
```

---

# 24. What is IN?

`IN` checks whether a value matches one of multiple values.

```sql
SELECT *
FROM users
WHERE city IN ('Bangalore', 'Hyderabad', 'Chennai');
```

---

# 25. What is BETWEEN?

`BETWEEN` checks whether a value falls within a range.

```sql
SELECT *
FROM products
WHERE price BETWEEN 500 AND 2000;
```

---

# 26. What is NULL?

`NULL` represents a missing or unknown value.

Use:

```sql
IS NULL
```

or:

```sql
IS NOT NULL
```

Example:

```sql
SELECT *
FROM users
WHERE phone IS NULL;
```

Do not use:

```sql
phone = NULL
```

---

# 27. What is GROUP BY?

`GROUP BY` groups rows based on one or more columns.

Example:

```sql
SELECT city, COUNT(*)
FROM users
GROUP BY city;
```

Result:

```text
city        count
----------- -----
Bangalore   10
Hyderabad   7
Chennai     5
```

---

# 28. What are aggregate functions?

Aggregate functions perform calculations on multiple rows.

Common functions:

```text
COUNT()
SUM()
AVG()
MIN()
MAX()
```

Example:

```sql
SELECT AVG(salary)
FROM employees;
```

---

# 29. What is HAVING?

`HAVING` filters grouped results.

Example:

```sql
SELECT city, COUNT(*) AS total
FROM users
GROUP BY city
HAVING COUNT(*) > 5;
```

### Important Difference

```text
WHERE
→ filters rows before grouping

HAVING
→ filters groups after GROUP BY
```

---

# 30. What is JOIN?

A JOIN combines data from multiple tables.

Example:

```text
users
orders
```

```sql
SELECT users.name, orders.amount
FROM users
JOIN orders
ON users.id = orders.user_id;
```

---

# 31. What is INNER JOIN?

Returns only matching records from both tables.

```sql
SELECT *
FROM users
INNER JOIN orders
ON users.id = orders.user_id;
```

---

# 32. What is LEFT JOIN?

Returns all records from the left table and matching records from the right table.

```sql
SELECT *
FROM users
LEFT JOIN orders
ON users.id = orders.user_id;
```

Users without orders can still appear.

---

# 33. What is RIGHT JOIN?

Returns all records from the right table and matching records from the left table.

```sql
SELECT *
FROM users
RIGHT JOIN orders
ON users.id = orders.user_id;
```

---

# 34. What is FULL OUTER JOIN?

Returns matching and non-matching records from both tables.

Conceptually:

```text
All users
+
All orders
+
Matching records
```

Support varies by database system.

---

# 35. What is a SELF JOIN?

A table is joined with itself.

Example:

```text
employees
employee_id
name
manager_id
```

```sql
SELECT
    e.name AS employee,
    m.name AS manager
FROM employees e
LEFT JOIN employees m
ON e.manager_id = m.employee_id;
```

---

# 36. What is a subquery?

A subquery is a query inside another query.

Example:

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

This finds employees earning above the average salary.

---

# 37. What is a correlated subquery?

A correlated subquery depends on the outer query.

Example:

```sql
SELECT e1.name
FROM employees e1
WHERE e1.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e1.department_id
);
```

The inner query uses a value from the outer query.

---

# 38. What is an index?

An index improves the speed of data retrieval for suitable queries.

Example:

```sql
CREATE INDEX idx_users_email
ON users(email);
```

Without an appropriate index, the database may need to inspect many rows.

### Important Point

Indexes can improve reads but also add storage and write/update overhead.

---

# 39. What is a composite index?

A composite index contains multiple columns.

```sql
CREATE INDEX idx_users_city_age
ON users(city, age);
```

The order of indexed columns matters for query planning and index usability.

---

# 40. What is normalization?

Normalization organises relational data to reduce unnecessary duplication and improve consistency.

Common normal forms:

```text
1NF
2NF
3NF
BCNF
```

Basic goal:

```text
Reduce data redundancy
+
Improve data consistency
```

---

# 41. What is denormalization?

Denormalization intentionally duplicates or combines data to improve read performance or simplify access in certain workloads.

Trade-off:

```text
Fewer joins
      ↓
Potentially faster reads

But

More duplicated data
      ↓
More update complexity
```

---

# 42. What is a transaction?

A transaction is a group of database operations treated as one logical unit.

Example:

```text
Transfer ₹1000
     ↓
Deduct from Account A
     ↓
Add to Account B
```

Both operations should succeed together or be rolled back.

---

# 43. What is COMMIT?

`COMMIT` permanently saves the changes made in a transaction.

```sql
COMMIT;
```

---

# 44. What is ROLLBACK?

`ROLLBACK` undoes changes that have not been committed.

```sql
ROLLBACK;
```

---

# 45. What are ACID properties?

ACID stands for:

```text
A → Atomicity
C → Consistency
I → Isolation
D → Durability
```

### Atomicity

All operations succeed or fail as one unit.

### Consistency

The database moves from one valid state to another valid state.

### Isolation

Concurrent transactions should not incorrectly interfere with each other.

### Durability

Committed changes survive system failures.

---

# 46. DELETE vs TRUNCATE vs DROP

| DELETE                | TRUNCATE           | DROP              |
| --------------------- | ------------------ | ----------------- |
| Removes selected rows | Removes table rows | Removes table     |
| Can use WHERE         | Usually no WHERE   | Removes structure |
| Table remains         | Table remains      | Table is removed  |
| Row-level operation   | Bulk operation     | DDL operation     |

Examples:

```sql
DELETE FROM users
WHERE id = 5;
```

```sql
TRUNCATE TABLE users;
```

```sql
DROP TABLE users;
```

---

# 47. What is a view?

A view is a virtual table based on a query.

```sql
CREATE VIEW active_users AS
SELECT id, name, email
FROM users
WHERE status = 'active';
```

Then:

```sql
SELECT *
FROM active_users;
```

Views can simplify repeated queries and control which data is exposed.

---

# 48. What is a stored procedure?

A stored procedure is a set of SQL statements stored in the database and executed when called.

The exact syntax differs between database systems.

Conceptually:

```text
Application
   ↓
CALL Procedure
   ↓
Database executes SQL
```

---

# 49. What is a SQL injection attack?

SQL injection occurs when untrusted input is incorrectly incorporated into SQL statements.

Unsafe example:

```js
const query =
  "SELECT * FROM users WHERE email = '" +
  email +
  "'";
```

Use parameterized queries instead.

Example:

```sql
SELECT *
FROM users
WHERE email = ?;
```

The exact parameter syntax depends on the database driver.

### Important Rule

> Never directly concatenate untrusted user input into SQL queries.

---

# 50. What is a database constraint?

Constraints enforce rules on data.

Common constraints:

```text
PRIMARY KEY
FOREIGN KEY
UNIQUE
NOT NULL
CHECK
DEFAULT
```

They help maintain data integrity.

---

# SQL Revision Checklist

## Basics

* [ ] SQL
* [ ] Relational database
* [ ] Tables
* [ ] Rows
* [ ] Columns
* [ ] SQL command categories

## CRUD

* [ ] SELECT
* [ ] INSERT
* [ ] UPDATE
* [ ] DELETE

## Filtering

* [ ] WHERE
* [ ] AND
* [ ] OR
* [ ] NOT
* [ ] IN
* [ ] BETWEEN
* [ ] LIKE
* [ ] NULL
* [ ] DISTINCT

## Aggregation

* [ ] COUNT
* [ ] SUM
* [ ] AVG
* [ ] MIN
* [ ] MAX
* [ ] GROUP BY
* [ ] HAVING

## Relationships

* [ ] Primary key
* [ ] Foreign key
* [ ] INNER JOIN
* [ ] LEFT JOIN
* [ ] RIGHT JOIN
* [ ] FULL JOIN
* [ ] SELF JOIN
* [ ] Subqueries

## Database Design

* [ ] Constraints
* [ ] Normalization
* [ ] Denormalization
* [ ] Indexes
* [ ] Composite indexes

## Transactions

* [ ] Transaction
* [ ] COMMIT
* [ ] ROLLBACK
* [ ] ACID

## Security

* [ ] SQL Injection
* [ ] Parameterized queries
* [ ] Input validation

---

# Final SQL Flow

```text
Application
    ↓
SQL Query
    ↓
Database
    ↓
Query Processing
    ↓
Tables / Indexes
    ↓
Result
    ↓
Application
```

### One-Line Interview Answer

> **SQL is a language used to create, retrieve, update, delete, and manage data in relational databases.**
