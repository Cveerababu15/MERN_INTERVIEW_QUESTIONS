# MongoDB Interview Questions

> **Level:** Fresher / Junior Backend Developer
> **Focus:** Important MongoDB + Mongoose concepts and commonly asked interview questions
> **Prerequisite:** Node.js + Express.js

---

# 1. What is MongoDB?

MongoDB is a **NoSQL, document-oriented database**.

Instead of storing data primarily in rows and columns like a relational database, MongoDB stores data as documents.

```text
Database
   ↓
Collection
   ↓
Documents
   ↓
Fields
```

Example document:

```json
{
  "name": "Veera",
  "age": 21,
  "role": "Developer"
}
```

---

# 2. What is a NoSQL database?

NoSQL databases are databases designed for data models that are not limited to traditional relational tables.

MongoDB uses a **document model**.

Other NoSQL database types include:

```text
Document
Key-Value
Wide-Column
Graph
```

MongoDB is a **document database**.

---

# 3. MongoDB vs SQL

| MongoDB                     | SQL                                   |
| --------------------------- | ------------------------------------- |
| NoSQL document database     | Relational database                   |
| Collection                  | Table                                 |
| Document                    | Row                                   |
| Field                       | Column                                |
| Embedded documents possible | Usually uses related tables           |
| Flexible document structure | Schema defined through tables/columns |

Conceptually:

```text
MongoDB:

users
 ├── document
 ├── document
 └── document
```

SQL:

```text
users table
 ├── row
 ├── row
 └── row
```

---

# 4. What is a database in MongoDB?

A database is a logical container for collections.

Example:

```text
ecommerce
├── users
├── products
├── orders
└── reviews
```

---

# 5. What is a collection?

A collection is a group of MongoDB documents.

It is roughly comparable to a table in SQL.

Example:

```text
users
products
orders
```

A `users` collection could contain:

```json
{
  "name": "Veera",
  "email": "veera@example.com"
}
```

---

# 6. What is a document?

A document is an individual record stored in a MongoDB collection.

Example:

```json
{
  "_id": "123",
  "name": "Veera",
  "email": "veera@example.com",
  "age": 21
}
```

MongoDB documents are stored in **BSON**, a binary representation of JSON-like data.

---

# 7. What is BSON?

BSON stands for **Binary JSON**.

MongoDB uses BSON to store documents.

It supports data types such as:

* String
* Number
* Boolean
* Array
* Object
* Date
* ObjectId
* Null
* Binary data

---

# 8. What is `_id` in MongoDB?

Every MongoDB document normally has a unique `_id` field.

Example:

```json
{
  "_id": "ObjectId(...)",
  "name": "Veera"
}
```

If you don't provide `_id`, MongoDB normally generates an `ObjectId`.

---

# 9. What is ObjectId?

`ObjectId` is a BSON type commonly used as MongoDB's default `_id` value.

Example:

```js
new mongoose.Types.ObjectId()
```

It provides a unique identifier suitable for MongoDB documents.

---

# 10. What is CRUD?

CRUD stands for:

```text
Create
Read
Update
Delete
```

MongoDB operations:

```text
insertOne()
find()
findOne()
updateOne()
updateMany()
deleteOne()
deleteMany()
```

---

# 11. How do you insert a document?

Using MongoDB:

```js
db.users.insertOne({
  name: "Veera",
  age: 21
});
```

Using Mongoose:

```js
const user = await User.create({
  name: "Veera",
  age: 21
});
```

---

# 12. How do you find documents?

Find all:

```js
const users = await User.find();
```

Find one:

```js
const user = await User.findOne({
  email: "veera@example.com"
});
```

Find by ID:

```js
const user = await User.findById(id);
```

---

# 13. How do you update a document?

Using Mongoose:

```js
const user = await User.findByIdAndUpdate(
  id,
  { name: "Veerababu" },
  { new: true }
);
```

`new: true` returns the updated document.

---

# 14. How do you delete a document?

```js
await User.findByIdAndDelete(id);
```

Or:

```js
await User.deleteOne({
  _id: id
});
```

---

# 15. What are MongoDB query operators?

Query operators allow you to filter and manipulate documents.

Common comparison operators:

```text
$eq
$ne
$gt
$gte
$lt
$lte
$in
$nin
```

Example:

```js
const users = await User.find({
  age: {
    $gte: 18
  }
});
```

---

# 16. What are logical operators?

Common logical operators:

```text
$and
$or
$not
$nor
```

Example:

```js
const users = await User.find({
  $or: [
    { role: "admin" },
    { role: "manager" }
  ]
});
```

---

# 17. What is `$in`?

`$in` matches values contained in an array.

```js
const users = await User.find({
  role: {
    $in: ["admin", "manager"]
  }
});
```

---

# 18. What is `$regex`?

`$regex` performs pattern matching.

Example:

```js
const users = await User.find({
  name: {
    $regex: "veera",
    $options: "i"
  }
});
```

`i` makes the search case-insensitive.

---

# 19. What is projection?

Projection controls which fields are returned.

Example:

```js
const users = await User.find()
  .select("name email");
```

You can exclude fields too:

```js
const users = await User.find()
  .select("-password");
```

This is particularly important when returning user data.

---

# 20. What is sorting?

Sorting controls the order of query results.

```js
const users = await User.find()
  .sort({ createdAt: -1 });
```

```text
1  → Ascending
-1 → Descending
```

---

# 21. What is pagination?

Pagination returns data in smaller sets instead of returning thousands of documents at once.

Common approach:

```js
const page = 1;
const limit = 10;

const users = await User.find()
  .skip((page - 1) * limit)
  .limit(limit);
```

For large datasets, cursor-based pagination can also be considered.

---

# 22. What is an index?

An index improves query performance by allowing MongoDB to find matching documents more efficiently.

Example:

```js
userSchema.index({
  email: 1
});
```

Common index types include:

```text
Single-field
Compound
Multikey
Text
Geospatial
Unique
```

---

# 23. What is a unique index?

A unique index prevents duplicate values for a field.

Example:

```js
userSchema.index(
  { email: 1 },
  { unique: true }
);
```

This is useful for fields such as:

```text
email
username
SKU
```

### Important Point

A Mongoose `unique` option is primarily an instruction for index creation; it is not a normal validator that guarantees uniqueness by itself.

---

# 24. What is a compound index?

A compound index contains multiple fields.

```js
userSchema.index({
  role: 1,
  createdAt: -1
});
```

It can help queries that filter/sort using the indexed field combination.

Index design should be based on actual query patterns.

---

# 25. What is Mongoose?

Mongoose is an **ODM (Object Data Modeling) library for MongoDB and Node.js**.

It provides:

* Schemas
* Models
* Validation
* Middleware/hooks
* Query APIs
* Relationships through references/population

---

# 26. MongoDB vs Mongoose

| MongoDB                      | Mongoose                                                          |
| ---------------------------- | ----------------------------------------------------------------- |
| Database                     | ODM library                                                       |
| Stores documents             | Helps application interact with MongoDB                           |
| Database technology          | Node.js library                                                   |
| Provides database operations | Provides schemas/models and additional application-level features |

Example:

```text
Node.js
   ↓
Mongoose
   ↓
MongoDB
```

---

# 27. What is a Mongoose Schema?

A schema defines the expected structure and rules for documents handled by a Mongoose model.

Example:

```js
const userSchema = new mongoose.Schema({
  name: {
    type: String,
    required: true
  },

  email: {
    type: String,
    required: true,
    unique: true
  },

  age: {
    type: Number
  }
});
```

---

# 28. What is a Mongoose Model?

A model is created from a schema and is used to interact with a MongoDB collection.

```js
const User = mongoose.model(
  "User",
  userSchema
);
```

Then:

```js
const users = await User.find();
```

---

# 29. Schema vs Model

### Schema

Defines structure and rules:

```js
const userSchema = new mongoose.Schema({
  name: String
});
```

### Model

Provides an interface for database operations:

```js
const User = mongoose.model(
  "User",
  userSchema
);
```

Simple:

```text
Schema → Structure
Model  → Database operations
```

---

# 30. What is Mongoose validation?

Mongoose allows validation rules in schemas.

Example:

```js
const userSchema = new mongoose.Schema({
  name: {
    type: String,
    required: true
  },

  age: {
    type: Number,
    min: 18
  }
});
```

Other commonly used rules include:

```text
required
min
max
minLength
maxLength
enum
match
```

---

# 31. What is `timestamps` in Mongoose?

Mongoose can automatically maintain:

```text
createdAt
updatedAt
```

Example:

```js
const userSchema = new mongoose.Schema(
  {
    name: String
  },
  {
    timestamps: true
  }
);
```

---

# 32. What is `populate()`?

`populate()` replaces referenced IDs with related documents.

Example:

```js
const orderSchema = new mongoose.Schema({
  user: {
    type: mongoose.Schema.Types.ObjectId,
    ref: "User"
  }
});
```

Query:

```js
const orders = await Order.find()
  .populate("user");
```

Conceptually:

```text
Order
  ↓
user: ObjectId
  ↓
populate()
  ↓
User document
```

---

# 33. Embedding vs Referencing

MongoDB supports both approaches.

### Embedded document

```json
{
  "name": "Veera",
  "address": {
    "city": "Bangalore",
    "country": "India"
  }
}
```

### Referenced document

```json
{
  "name": "Veera",
  "addressId": "ObjectId(...)"
}
```

### General idea

Embedding can be useful when related data is usually read together and has a suitable size/lifecycle.

Referencing can be useful when related data is large, shared, or managed independently.

---

# 34. What is an aggregation pipeline?

Aggregation processes documents through a sequence of stages.

Example:

```js
const result = await Order.aggregate([
  {
    $match: {
      status: "completed"
    }
  },
  {
    $group: {
      _id: "$userId",
      total: {
        $sum: "$amount"
      }
    }
  }
]);
```

Common stages:

```text
$match
$group
$project
$sort
$limit
$skip
$lookup
$unwind
```

---

# 35. What is `$match`?

`$match` filters documents in an aggregation pipeline.

```js
{
  $match: {
    status: "completed"
  }
}
```

It is conceptually similar to filtering documents in a normal query.

---

# 36. What is `$group`?

`$group` groups documents and can calculate values such as:

```text
$sum
$avg
$min
$max
$count
```

Example:

```js
{
  $group: {
    _id: "$category",
    totalProducts: {
      $sum: 1
    }
  }
}
```

---

# 37. What is `$lookup`?

`$lookup` performs a join-like operation between collections.

Example concept:

```text
Orders
   ↓
$lookup
   ↓
Users
```

Example:

```js
{
  $lookup: {
    from: "users",
    localField: "userId",
    foreignField: "_id",
    as: "user"
  }
}
```

---

# 38. What is a transaction?

A transaction allows multiple database operations to be treated as one logical unit.

Conceptually:

```text
Start Transaction
       ↓
Operation 1
       ↓
Operation 2
       ↓
Operation 3
       ↓
Commit
```

If an error occurs, the transaction can be aborted.

Transactions are useful when multiple related changes need atomic behaviour.

---

# 39. What is MongoDB Atlas?

MongoDB Atlas is MongoDB's managed cloud database service.

It provides features such as:

* Cloud-hosted MongoDB databases
* Monitoring
* Backups
* Security configuration
* Scaling options

A Node.js application can connect to an Atlas deployment using a MongoDB connection string.

---

# 40. How do you connect Node.js to MongoDB using Mongoose?

Install:

```bash
npm install mongoose
```

Then:

```js
const mongoose = require("mongoose");

mongoose
  .connect(process.env.MONGO_URI)
  .then(() => {
    console.log("MongoDB connected");
  })
  .catch((error) => {
    console.error("MongoDB connection failed", error);
  });
```

Use environment variables for the connection string rather than hard-coding credentials.

---

# 41. How do you structure MongoDB models in a MERN backend?

Example:

```text
src/
├── models/
│   ├── User.js
│   ├── Product.js
│   ├── Order.js
│   └── Review.js
```

Each model can define its own Mongoose schema.

---

# 42. What is `lean()` in Mongoose?

`lean()` tells Mongoose to return plain JavaScript objects instead of full Mongoose documents.

```js
const users = await User.find()
  .lean();
```

This can reduce Mongoose document overhead for read-only operations.

### Important Point

Lean documents do not provide normal Mongoose document methods.

---

# 43. What is `findOne()` vs `find()`?

### `find()`

Returns multiple matching documents:

```js
const users = await User.find({
  role: "user"
});
```

### `findOne()`

Returns one matching document:

```js
const user = await User.findOne({
  email: "veera@example.com"
});
```

---

# 44. What is `findById()`?

`findById()` retrieves a document by its `_id`.

```js
const user = await User.findById(userId);
```

It is essentially a convenient form for an `_id` query.

---

# 45. How do you protect sensitive fields?

Avoid returning sensitive fields such as passwords.

Example:

```js
const user = await User.findById(id)
  .select("-password");
```

You can also configure schema behaviour for sensitive fields.

Example:

```js
password: {
  type: String,
  required: true,
  select: false
}
```

Then explicitly request it when needed:

```js
const user = await User.findOne({
  email
}).select("+password");
```

---

# 46. How do you search products in MongoDB?

Simple search:

```js
const products = await Product.find({
  name: {
    $regex: search,
    $options: "i"
  }
});
```

For larger search requirements, MongoDB text indexes or MongoDB Atlas Search may be more appropriate depending on the application.

---

# 47. How do you filter products?

Example:

```js
const products = await Product.find({
  category: "fruits",
  price: {
    $lte: 500
  }
});
```

Multiple filters can be combined:

```js
const products = await Product.find({
  category: "fruits",
  stock: {
    $gt: 0
  },
  price: {
    $lte: 500
  }
});
```

---

# 48. How do you improve MongoDB query performance?

Important techniques:

```text
Use appropriate indexes
Return only required fields
Use pagination
Avoid unnecessary queries
Use efficient query patterns
Use lean() for suitable read-only queries
Analyse query plans
Avoid unbounded large result sets
```

MongoDB's `explain()` can help analyse query execution.

---

# 49. What is database normalization vs MongoDB denormalization?

Traditional relational databases often use normalization to reduce duplicate data.

MongoDB can use denormalized or embedded structures when they better fit application read patterns.

Example:

```text
User
 └── Address embedded
```

instead of always storing address separately.

The correct design depends on:

* Read patterns
* Write patterns
* Data size
* Update frequency
* Relationship structure

---

# 50. How does MongoDB fit into a MERN application?

MERN stands for:

```text
M → MongoDB
E → Express.js
R → React
N → Node.js
```

Typical flow:

```text
React
  ↓
HTTP Request
  ↓
Express
  ↓
Controller
  ↓
Service
  ↓
Mongoose
  ↓
MongoDB
  ↓
Mongoose
  ↓
Express
  ↓
JSON Response
  ↓
React
```

---

# MongoDB + Mongoose Interview Revision Checklist

## MongoDB Fundamentals

* [ ] MongoDB
* [ ] NoSQL
* [ ] Database
* [ ] Collection
* [ ] Document
* [ ] BSON
* [ ] `_id`
* [ ] ObjectId
* [ ] MongoDB vs SQL

## CRUD & Queries

* [ ] CRUD
* [ ] `insertOne()`
* [ ] `find()`
* [ ] `findOne()`
* [ ] `findById()`
* [ ] `updateOne()`
* [ ] `deleteOne()`
* [ ] Query operators
* [ ] `$in`
* [ ] `$or`
* [ ] `$regex`
* [ ] Projection
* [ ] Sorting
* [ ] Pagination

## Indexing

* [ ] Index
* [ ] Unique index
* [ ] Compound index
* [ ] Query performance
* [ ] `explain()`

## Mongoose

* [ ] Mongoose
* [ ] Schema
* [ ] Model
* [ ] Validation
* [ ] `timestamps`
* [ ] `populate()`
* [ ] `lean()`
* [ ] Sensitive fields
* [ ] MongoDB connection

## Advanced Important Topics

* [ ] Embedding
* [ ] Referencing
* [ ] Aggregation
* [ ] `$match`
* [ ] `$group`
* [ ] `$lookup`
* [ ] Transactions
* [ ] MongoDB Atlas
* [ ] Search
* [ ] Performance optimisation

---

# Final MongoDB Interview Flow

You should be able to explain a typical MERN database operation:

```text
React
  ↓
POST /api/products
  ↓
Express Route
  ↓
Controller
  ↓
Service
  ↓
Mongoose Model
  ↓
MongoDB
  ↓
Document Created
  ↓
Response
  ↓
React
```

### One-Line Interview Answer

> **MongoDB is a NoSQL document database that stores flexible BSON documents in collections, while Mongoose provides schemas, models, validation, queries, and other application-level features for using MongoDB from Node.js.**
