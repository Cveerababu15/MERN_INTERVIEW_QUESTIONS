# DBMS Interview Questions

> **Level:** Fresher / Junior Developer
> **Focus:** Important DBMS concepts + commonly asked interview questions
> **Purpose:** Understand how databases store, organise, protect, and manage data.

---

# 1. What is DBMS?

DBMS stands for **Database Management System**.

It is software used to:

* Store data
* Retrieve data
* Update data
* Delete data
* Manage databases
* Control access
* Maintain data consistency

Examples:

```text
MySQL
PostgreSQL
Oracle Database
SQL Server
MongoDB
```

---

# 2. What is a database?

A database is an organised collection of data.

Example:

```text
Users
Products
Orders
Payments
```

A database allows applications to store and retrieve information efficiently.

---

# 3. What is DBMS vs Database?

| Database               | DBMS                               |
| ---------------------- | ---------------------------------- |
| Collection of data     | Software that manages data         |
| Stores information     | Provides operations on information |
| Passive data structure | Management system                  |

Simple explanation:

```text
Database
→ Data

DBMS
→ Software that manages the data
```

---

# 4. What are the types of DBMS?

Common categories include:

```text
Hierarchical DBMS
Network DBMS
Relational DBMS
Object-oriented DBMS
NoSQL database systems
```

The most common relational systems include:

```text
MySQL
PostgreSQL
Oracle
SQL Server
```

---

# 5. What is RDBMS?

RDBMS stands for **Relational Database Management System**.

It stores data in tables and supports relationships between tables.

Example:

```text
users
orders
products
```

Relationships can be represented using keys.

---

# 6. DBMS vs RDBMS

| DBMS                                | RDBMS                                 |
| ----------------------------------- | ------------------------------------- |
| General database management concept | Relational database management system |
| May not use tables/relationships    | Uses tables and relationships         |
| Data model depends on system        | Based on relational model             |
| Broader term                        | Specific category                     |

---

# 7. What is a relational database?

A relational database stores information in tables.

Example:

```text
users

id | name | email
---|------|----------------
1  | Veera| veera@gmail.com
2  | Rahul| rahul@gmail.com
```

Tables can be related using keys.

---

# 8. What is a schema?

A schema describes the structure of a database.

It can define:

```text
Tables
Columns
Data types
Relationships
Constraints
Indexes
```

Example:

```text
users
├── id
├── name
├── email
└── created_at
```

---

# 9. What is data integrity?

Data integrity means maintaining the **accuracy, consistency, and validity** of data.

Example:

If an order references a user, the referenced user should satisfy the database's relationship rules.

Constraints help maintain integrity.

---

# 10. What are integrity constraints?

Common integrity constraints include:

```text
PRIMARY KEY
FOREIGN KEY
UNIQUE
NOT NULL
CHECK
DEFAULT
```

They prevent invalid data from entering the database.

---

# 11. What is entity integrity?

Entity integrity ensures that each row can be uniquely identified.

A common way to achieve this is using a primary key.

Example:

```sql
id INT PRIMARY KEY
```

---

# 12. What is referential integrity?

Referential integrity ensures that relationships between related tables remain valid.

Example:

```text
users
id = 10

orders
user_id = 10
```

The foreign key relationship ensures the referenced record follows the database's referential rules.

---

# 13. What is a primary key?

A primary key uniquely identifies a record.

Example:

```text
users

id
---
1
2
3
```

Properties:

```text
Unique
Not NULL
Identifies a row
```

---

# 14. What is a candidate key?

A candidate key is a column or set of columns that can uniquely identify a row.

Example:

```text
users

id
email
phone
```

If all three are unique, each could potentially be a candidate key.

One candidate key is selected as the primary key.

---

# 15. What is a super key?

A super key is any set of attributes that can uniquely identify a record.

A candidate key is a **minimal super key**.

Example:

```text
{id}
{id, name}
{id, email}
```

If `id` alone is unique, all of these can be super keys, while `id` is a candidate key because it is minimal.

---

# 16. What is a composite key?

A composite key uses multiple columns together to uniquely identify a record.

Example:

```text
student_id
course_id
```

Together:

```text
(student_id, course_id)
```

can uniquely identify an enrolment.

---

# 17. What is a foreign key?

A foreign key references a key in another table.

Example:

```text
users
id

orders
user_id
```

Relationship:

```text
users.id
   ↑
   |
orders.user_id
```

---

# 18. What is cardinality?

Cardinality describes the relationship between entities.

Common types:

```text
One-to-One
One-to-Many
Many-to-Many
```

---

# 19. What is a one-to-one relationship?

One record is related to one record.

Example:

```text
User
 ↓
Profile
```

One user may have one profile.

---

# 20. What is a one-to-many relationship?

One record can be related to many records.

Example:

```text
User
 ↓
Orders
 ↓
Order 1
Order 2
Order 3
```

One user can have many orders.

---

# 21. What is a many-to-many relationship?

Many records can relate to many records.

Example:

```text
Students
    ↕
Courses
```

A student can attend multiple courses.

A course can have multiple students.

A junction table is commonly used in relational databases.

```text
student_courses
----------------
student_id
course_id
```

---

# 22. What is normalization?

Normalization is the process of organising data to reduce unnecessary duplication and improve consistency.

Common normal forms:

```text
1NF
2NF
3NF
BCNF
```

---

# 23. What is 1NF?

First Normal Form requires values to be atomic and each row/column to follow a consistent structure.

Bad:

```text
user_id | phone
1       | 9999, 8888
```

Better:

```text
user_id | phone
1       | 9999
1       | 8888
```

The exact modelling decision depends on the application.

---

# 24. What is 2NF?

A relation is in 2NF when:

```text
It is in 1NF
+
No non-key attribute depends on only part of a composite candidate key
```

This primarily matters when a table has a composite key.

---

# 25. What is 3NF?

A relation is in 3NF when:

```text
It is in 2NF
+
Non-key attributes do not depend transitively on another non-key attribute
```

Basic goal:

> Non-key data should depend on the key, the whole key, and nothing but the key.

---

# 26. What is BCNF?

BCNF stands for **Boyce-Codd Normal Form**.

It is a stronger form of 3NF.

A relation is in BCNF when every determinant is a candidate key.

BCNF is used when certain dependency patterns remain after 3NF.

---

# 27. What is denormalization?

Denormalization intentionally introduces some redundancy to improve read performance or simplify queries.

Example:

Instead of joining:

```text
orders
+
users
```

an application may store selected user information directly with the order.

Trade-off:

```text
Faster / simpler reads
        ↕
More duplicated data
        ↕
More update complexity
```

---

# 28. What is an index?

An index is a database structure used to improve lookup performance for suitable queries.

Example:

```text
users.email
```

can have an index.

Conceptually:

```text
Query
 ↓
Index
 ↓
Matching records
```

Without a suitable index, the database may need to inspect many rows.

---

# 29. Advantages and disadvantages of indexes

### Advantages

```text
Faster lookups
Faster sorting/filtering for suitable queries
Can enforce uniqueness
```

### Disadvantages

```text
Extra storage
Slower writes
Extra maintenance
```

Therefore:

> Do not create indexes blindly.

---

# 30. What is a transaction?

A transaction is a sequence of operations treated as one logical unit.

Example:

```text
Transfer Money

Account A
   ↓
- ₹1000

Account B
   ↓
+ ₹1000
```

Both operations should be handled consistently.

---

# 31. What are ACID properties?

ACID means:

```text
A → Atomicity
C → Consistency
I → Isolation
D → Durability
```

### Atomicity

All operations succeed or none of them take effect.

### Consistency

Database rules remain valid before and after the transaction.

### Isolation

Concurrent transactions should not incorrectly interfere with one another.

### Durability

Committed changes remain stored even after a failure.

---

# 32. What is concurrency?

Concurrency means multiple operations or transactions can be active at overlapping times.

Example:

```text
User A → Update Account
User B → Read Account
User C → Create Order
```

A DBMS manages concurrent access to maintain correctness.

---

# 33. What is a concurrency problem?

Poorly managed concurrent transactions can cause problems such as:

```text
Dirty Read
Non-repeatable Read
Phantom Read
Lost Update
```

---

# 34. What is a dirty read?

A dirty read occurs when one transaction reads data written by another transaction before that transaction has committed.

Example:

```text
Transaction A
→ updates balance

Transaction B
→ reads updated balance

Transaction A
→ rollback
```

Transaction B read data that was never committed.

---

# 35. What is a non-repeatable read?

A transaction reads the same row twice and gets different values because another transaction changed and committed that row between the reads.

```text
Read → ₹1000
Other transaction updates
Read → ₹1500
```

---

# 36. What is a phantom read?

A transaction repeats a range query and sees additional or missing rows because another transaction inserted, deleted, or changed rows affecting that range.

Example:

```text
First query
→ 10 users

Another transaction inserts matching user

Second query
→ 11 users
```

---

# 37. What is isolation level?

An isolation level controls how one transaction can observe changes made by other concurrent transactions.

Common SQL isolation levels:

```text
Read Uncommitted
Read Committed
Repeatable Read
Serializable
```

Higher isolation can provide stronger consistency but may reduce concurrency or increase locking/coordination costs depending on the database.

---

# 38. What is a deadlock?

A deadlock occurs when transactions wait for each other indefinitely.

Example:

```text
Transaction A
locks Resource 1
waits for Resource 2

Transaction B
locks Resource 2
waits for Resource 1
```

```text
A → waits for B
B → waits for A
```

The database must detect or resolve the situation.

---

# 39. What is locking?

Locking is a mechanism used to coordinate concurrent access to data.

Common conceptual types:

```text
Shared Lock
Exclusive Lock
```

### Shared Lock

Used when data is being read under locking rules.

### Exclusive Lock

Used when data is being modified.

Exact locking behaviour depends on the database system.

---

# 40. What is a view?

A view is a virtual representation based on a query.

Example:

```sql
CREATE VIEW active_users AS
SELECT id, name
FROM users
WHERE status = 'active';
```

Views can:

* Simplify queries
* Provide controlled access
* Hide query complexity

---

# 41. What is a stored procedure?

A stored procedure is a set of SQL statements stored and executed by the database.

Conceptually:

```text
Application
    ↓
Call Procedure
    ↓
Database
    ↓
Execute SQL
```

Syntax and capabilities depend on the DBMS.

---

# 42. What is a trigger?

A trigger is database logic that automatically executes when a specified database event occurs.

Examples:

```text
INSERT
UPDATE
DELETE
```

Example use:

```text
Order inserted
    ↓
Trigger executes
    ↓
Audit record created
```

Triggers should be used carefully because they can make application behaviour less obvious.

---

# 43. What is a database transaction log?

A transaction log records changes or transaction-related information used by a DBMS for recovery and durability mechanisms.

It can help the database:

```text
Recover after failures
Maintain durability
Support rollback/recovery mechanisms
```

The exact implementation differs between database systems.

---

# 44. What is database backup?

A backup is a copy of database data that can be used for recovery.

Common strategies include:

```text
Full Backup
Incremental Backup
Differential Backup
```

A production system should have an appropriate backup and recovery strategy.

---

# 45. What is database replication?

Replication means maintaining copies of data on multiple database servers or nodes.

Example:

```text
Primary
   ↓
Replica
   ↓
Replica
```

Possible benefits:

```text
High availability
Read scaling
Disaster recovery
```

Exact replication architecture depends on the database system.

---

# 46. What is database sharding?

Sharding distributes data across multiple database servers or partitions.

Example:

```text
Users 1–1,000,000
       ↓
Shard A

Users 1,000,001–2,000,000
       ↓
Shard B
```

It can help horizontally scale very large workloads.

---

# 47. What is horizontal vs vertical scaling?

### Vertical Scaling

Increase resources of one server.

```text
More CPU
More RAM
More storage
```

### Horizontal Scaling

Add more servers.

```text
Server A
Server B
Server C
```

Databases can use different combinations depending on their architecture.

---

# 48. What is database partitioning?

Partitioning divides a large logical table or dataset into smaller physical parts.

Common forms include:

```text
Range Partitioning
List Partitioning
Hash Partitioning
```

The application can still interact with the logical table while the DBMS manages the underlying partitions.

---

# 49. What is query optimization?

Query optimization is the process of finding an efficient way to execute a database query.

A database optimizer may consider:

```text
Indexes
Join order
Filtering
Sorting
Available statistics
Execution cost
```

Example:

```text
Bad query plan
→ scans millions of rows

Better query plan
→ uses suitable index
→ examines fewer rows
```

---

# 50. What is an execution plan?

An execution plan describes how the database intends to execute a query.

It can show operations such as:

```text
Table Scan
Index Scan
Index Seek
Join
Sort
Filter
Aggregate
```

Execution plans are useful for performance troubleshooting.

---

# 51. What is a full table scan?

A full table scan means the database examines rows across the table to find matching records.

Example:

```text
Table
 ↓
Row 1
Row 2
Row 3
...
Row 1,000,000
```

For large tables, a suitable index may reduce the amount of data that needs to be examined for some queries.

---

# 52. What is data redundancy?

Data redundancy means the same information is unnecessarily stored in multiple places.

Example:

```text
Customer name
stored repeatedly in many order records
```

Potential problems:

```text
More storage
Update anomalies
Inconsistent values
```

Normalization can reduce unnecessary redundancy.

---

# 53. What are insertion, update, and deletion anomalies?

These are problems caused by poor database design.

### Insertion Anomaly

You cannot insert one piece of information without also providing unrelated information.

### Update Anomaly

The same data must be updated in multiple places.

### Deletion Anomaly

Deleting one record accidentally removes information that should have been retained.

Normalization helps reduce these problems.

---

# 54. What is data independence?

Data independence means changes at one level of database structure do not unnecessarily require changes at another level.

Two common types:

```text
Physical Data Independence
Logical Data Independence
```

---

# 55. What are the three levels of database architecture?

A common DBMS architecture describes:

```text
External Level
      ↓
Conceptual Level
      ↓
Internal Level
```

### External Level

What individual users/applications see.

### Conceptual Level

Overall logical structure of the database.

### Internal Level

How data is physically stored.

---

# 56. What is a database schema vs database instance?

### Schema

The structure/design of the database.

Example:

```text
users
├── id
├── name
└── email
```

### Instance

The actual data stored at a particular point in time.

```text
1 | Veera | veera@gmail.com
2 | Rahul | rahul@gmail.com
```

Simple:

```text
Schema → Structure
Instance → Current Data
```

---

# 57. What is SQL vs DBMS?

| SQL                                           | DBMS                                              |
| --------------------------------------------- | ------------------------------------------------- |
| Query language                                | Database management software                      |
| Used to communicate with relational databases | Stores and manages data                           |
| Example: `SELECT`                             | Example: MySQL                                    |
| Defines/manipulates data through commands     | Handles storage, transactions, security, recovery |

Simple:

```text
SQL
→ Language

DBMS
→ Software that manages the database
```

---

# 58. What is DBMS security?

DBMS security protects data from unauthorised access or modification.

Common mechanisms include:

```text
Authentication
Authorization
Roles
Permissions
Encryption
Auditing
Backups
Access controls
```

---

# 59. What is database recovery?

Database recovery restores the database to a consistent state after a failure.

Possible failures:

```text
Application crash
Server failure
Power failure
Transaction failure
Hardware failure
```

Recovery mechanisms can use:

```text
Logs
Backups
Checkpoints
Replication
```

The exact mechanisms depend on the DBMS.

---

# 60. What are the advantages of DBMS?

Important advantages:

```text
Data organisation
Data consistency
Data security
Concurrent access
Transaction management
Backup and recovery
Reduced redundancy
Data integrity
Controlled access
```

---

# DBMS Revision Checklist

## Fundamentals

* [ ] DBMS
* [ ] Database
* [ ] RDBMS
* [ ] Schema
* [ ] Instance
* [ ] Data integrity
* [ ] Data independence

## Keys

* [ ] Primary key
* [ ] Foreign key
* [ ] Candidate key
* [ ] Super key
* [ ] Composite key

## Relationships

* [ ] One-to-one
* [ ] One-to-many
* [ ] Many-to-many
* [ ] Cardinality
* [ ] Referential integrity

## Normalization

* [ ] 1NF
* [ ] 2NF
* [ ] 3NF
* [ ] BCNF
* [ ] Denormalization
* [ ] Data redundancy
* [ ] Anomalies

## Transactions

* [ ] Transaction
* [ ] ACID
* [ ] COMMIT
* [ ] ROLLBACK
* [ ] Concurrency
* [ ] Isolation levels
* [ ] Dirty read
* [ ] Non-repeatable read
* [ ] Phantom read
* [ ] Deadlock
* [ ] Locks

## Performance

* [ ] Index
* [ ] Query optimization
* [ ] Execution plan
* [ ] Full table scan
* [ ] Partitioning
* [ ] Sharding
* [ ] Replication
* [ ] Scaling

## Database Management

* [ ] Views
* [ ] Stored procedures
* [ ] Triggers
* [ ] Backup
* [ ] Recovery
* [ ] Security

---

# Final DBMS Concept Flow

```text
Application
     ↓
DBMS
     ↓
Query Processing
     ↓
Transaction Management
     ↓
Storage Management
     ↓
Database
     ↓
Data
```

For a relational application:

```text
Application
     ↓
SQL
     ↓
RDBMS
     ↓
Tables
     ↓
Relationships
     ↓
Indexes
     ↓
Transactions
     ↓
Stored Data
```

---

# SQL + DBMS Interview Connection

These two topics should be studied together.

```text
DBMS
 ↓
Understanding how databases work
 ↓
Tables + Relationships
 ↓
Keys + Constraints
 ↓
Normalization
 ↓
Transactions + ACID
 ↓
Indexes + Performance
 ↓
SQL
 ↓
SELECT / INSERT / UPDATE / DELETE
 ↓
WHERE / GROUP BY / HAVING
 ↓
JOIN
 ↓
Subqueries
 ↓
Real Database Operations
```

### Final Interview Goal

Be able to explain:

> **DBMS manages and controls database data, while SQL provides the language used to interact with relational databases.**
