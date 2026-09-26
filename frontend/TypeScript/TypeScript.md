# TypeScript Interview Questions

> **Level:** Fresher / Junior Developer
> **Focus:** Most Asked Interview Questions
> **Goal:** Understand TypeScript concepts and explain them clearly in interviews.

---

## 1. What is TypeScript?

**Answer:**

TypeScript is a **superset of JavaScript** developed by Microsoft.

It adds features such as:

* Static typing
* Interfaces
* Types
* Generics
* Enums
* Access modifiers
* Better tooling and error checking

TypeScript code is eventually **compiled/transpiled into JavaScript**.

```ts
let username: string = "Veera";
let age: number = 21;
```

### Important Point

> TypeScript = JavaScript + Static Type Checking + Additional Features.

---

## 2. Why do we use TypeScript?

TypeScript helps developers:

* Detect errors during development
* Understand the expected data types
* Improve code readability
* Get better IDE autocomplete
* Make large applications easier to maintain
* Refactor code more safely

Example:

```ts
function add(a: number, b: number): number {
  return a + b;
}

add(10, 20);
```

This will produce an error:

```ts
add("10", 20);
```

because `"10"` is a string.

---

## 3. What is the difference between JavaScript and TypeScript?

| JavaScript                   | TypeScript                                       |
| ---------------------------- | ------------------------------------------------ |
| Dynamically typed            | Statically typed                                 |
| No compilation required      | Compiled/transpiled to JavaScript                |
| Errors may appear at runtime | Many type errors are detected during development |
| Supports objects/functions   | Adds interfaces, generics, type aliases, etc.    |
| Easier for small scripts     | Useful for large applications                    |

### Simple Example

JavaScript:

```js
let age = 21;
age = "twenty one";
```

TypeScript:

```ts
let age: number = 21;

// Error
age = "twenty one";
```

---

## 4. Is TypeScript a programming language?

Yes.

TypeScript is a programming language developed by Microsoft.

It extends JavaScript by adding a static type system and other development features.

---

## 5. How does TypeScript work?

The basic flow is:

```text
TypeScript Code
      ↓
Type Checking
      ↓
TypeScript Compiler
      ↓
JavaScript Code
      ↓
Browser / Node.js
```

Example:

```ts
const message: string = "Hello";
```

After compilation, it becomes JavaScript that can run in a JavaScript environment.

---

## 6. What is a type in TypeScript?

A type defines what kind of value a variable can contain.

```ts
let name: string = "Veera";
let age: number = 21;
let isDeveloper: boolean = true;
```

Here:

```text
name        → string
age         → number
isDeveloper → boolean
```

---

## 7. What are the basic types in TypeScript?

Common TypeScript types include:

```ts
string
number
boolean
null
undefined
any
unknown
void
never
object
array
tuple
```

Example:

```ts
let name: string = "Veera";
let age: number = 21;
let active: boolean = true;
let numbers: number[] = [10, 20, 30];
```

---

## 8. What is type inference?

Type inference means TypeScript can automatically determine the type of a variable without explicitly writing the type.

```ts
let name = "Veera";
```

TypeScript understands:

```ts
name: string
```

Another example:

```ts
let age = 21;
```

TypeScript infers:

```ts
age: number
```

### Important Point

You don't always need to explicitly write types.

---

## 9. What is type annotation?

Type annotation means explicitly specifying the type.

```ts
let username: string = "Veera";
let age: number = 21;
let isActive: boolean = true;
```

Syntax:

```ts
let variableName: type = value;
```

---

## 10. What is the `any` type?

`any` disables TypeScript's type checking for a value.

```ts
let data: any = "Hello";

data = 100;
data = true;
data = {
  name: "Veera"
};
```

Anything can be assigned to it.

### Important Point

Avoid using `any` unnecessarily because it removes many benefits of TypeScript.

---

## 11. What is the `unknown` type?

`unknown` can contain any value, but unlike `any`, TypeScript requires you to **check the type before using it**.

```ts
let data: unknown = "Hello";
```

This is not allowed directly:

```ts
// Error
data.toUpperCase();
```

You need to check:

```ts
if (typeof data === "string") {
  console.log(data.toUpperCase());
}
```

### Interview Point

> `unknown` is safer than `any`.

---

## 12. Difference between `any` and `unknown`

| `any`                          | `unknown`                        |
| ------------------------------ | -------------------------------- |
| Disables type checking         | Requires type checking           |
| Can access properties directly | Cannot access without narrowing  |
| Less safe                      | Safer                            |
| Should generally be avoided    | Useful for unknown external data |

Example:

```ts
let value1: any = "Hello";
value1.toUpperCase();
```

```ts
let value2: unknown = "Hello";

if (typeof value2 === "string") {
  value2.toUpperCase();
}
```

---

## 13. What is a union type?

A union type allows a variable to contain multiple possible types.

Use `|`.

```ts
let id: string | number;

id = 101;
id = "101";
```

Another example:

```ts
function printId(id: string | number) {
  console.log(id);
}
```

---

## 14. What is a literal type?

A literal type allows only specific values.

```ts
let status: "success" | "error" | "loading";

status = "success";
```

This is invalid:

```ts
status = "failed";
```

Literal types are useful for:

* Status values
* User roles
* Configuration options
* API states

---

## 15. What is an array in TypeScript?

An array contains multiple values of a specific type.

```ts
let numbers: number[] = [10, 20, 30];

let names: string[] = ["Veera", "Rahul", "Arun"];
```

Another syntax:

```ts
let numbers: Array<number> = [10, 20, 30];
```

---

## 16. What is a tuple?

A tuple is an array with a **fixed number of elements and specific types in specific positions**.

```ts
let user: [string, number] = ["Veera", 21];
```

Here:

```text
index 0 → string
index 1 → number
```

This is invalid:

```ts
// Error
let user: [string, number] = [21, "Veera"];
```

---

## 17. What is an object type?

You can define the structure of an object.

```ts
let user: {
  name: string;
  age: number;
} = {
  name: "Veera",
  age: 21
};
```

This ensures the object follows the expected structure.

---

## 18. What is an interface?

An interface defines the structure of an object.

```ts
interface User {
  name: string;
  age: number;
}

const user: User = {
  name: "Veera",
  age: 21
};
```

Interfaces are commonly used for:

* API response objects
* React props
* User objects
* Configuration objects

---

## 19. What is a type alias?

A type alias gives a name to a type.

```ts
type User = {
  name: string;
  age: number;
};

const user: User = {
  name: "Veera",
  age: 21
};
```

It can also represent unions:

```ts
type Status = "loading" | "success" | "error";
```

---

## 20. Difference between `interface` and `type`

Both can describe object structures.

### Interface

```ts
interface User {
  name: string;
  age: number;
}
```

### Type

```ts
type User = {
  name: string;
  age: number;
};
```

A `type` can easily represent unions:

```ts
type Status = "success" | "error";
```

Interfaces support declaration merging:

```ts
interface User {
  name: string;
}

interface User {
  age: number;
}
```

The interface becomes:

```ts
interface User {
  name: string;
  age: number;
}
```

### Interview Point

For normal object structures, both are commonly used. The choice often depends on project conventions and the specific type features required.

---

## 21. What are optional properties?

Use `?` to make a property optional.

```ts
interface User {
  name: string;
  age?: number;
}
```

Both are valid:

```ts
const user1: User = {
  name: "Veera"
};

const user2: User = {
  name: "Veera",
  age: 21
};
```

---

## 22. What is the `readonly` keyword?

`readonly` prevents a property from being reassigned after initialization.

```ts
interface User {
  readonly id: number;
  name: string;
}

const user: User = {
  id: 101,
  name: "Veera"
};
```

This is not allowed:

```ts
// Error
user.id = 102;
```

Useful for values such as:

* IDs
* Configuration values
* Immutable properties

---

## 23. How do you type a function?

You can specify parameter and return types.

```ts
function add(a: number, b: number): number {
  return a + b;
}
```

Here:

```text
a → number
b → number
return → number
```

---

## 24. What is a function return type?

The return type specifies what a function returns.

```ts
function greet(name: string): string {
  return `Hello ${name}`;
}
```

The function must return a string.

---

## 25. What is `void`?

`void` is commonly used when a function does not return a meaningful value.

```ts
function printMessage(message: string): void {
  console.log(message);
}
```

The function performs an action but does not return a value for the caller to use.

---

## 26. What are optional parameters?

Use `?` after a parameter name.

```ts
function greet(name: string, age?: number) {
  console.log(name);
}
```

Both are valid:

```ts
greet("Veera");

greet("Veera", 21);
```

---

## 27. What are default parameters?

A parameter can have a default value.

```ts
function greet(name: string = "Guest") {
  console.log(`Hello ${name}`);
}

greet();
greet("Veera");
```

---

## 28. What are generics?

Generics allow us to write reusable code that works with different types while maintaining type safety.

```ts
function identity<T>(value: T): T {
  return value;
}

const numberValue = identity<number>(100);

const stringValue = identity<string>("Hello");
```

`T` represents a type that will be determined when the function is used.

### Important Point

> Generics provide reusable and type-safe code.

---

## 29. Why are generics useful?

Without generics, you may be forced to use `any`.

```ts
function identity(value: any) {
  return value;
}
```

With generics:

```ts
function identity<T>(value: T): T {
  return value;
}
```

The type is preserved.

```ts
const result = identity<string>("Hello");
```

---

## 30. What is a type assertion?

Type assertion tells TypeScript that you know more about the type than TypeScript currently knows.

```ts
const value: unknown = "Hello";

const message = value as string;

console.log(message.toUpperCase());
```

Another syntax:

```ts
const message = <string>value;
```

The `as` syntax is commonly preferred, especially in TSX/React projects.

### Important Point

Type assertions do **not** perform runtime type conversion.

---

## 31. What is type narrowing?

Type narrowing means reducing a broader type to a more specific type using checks.

Example:

```ts
function printId(id: string | number) {
  if (typeof id === "string") {
    console.log(id.toUpperCase());
  } else {
    console.log(id.toFixed(2));
  }
}
```

Initially:

```text
string | number
```

After the check, TypeScript knows the specific type inside each block.

---

## 32. What is an enum?

An enum defines a set of named constants.

```ts
enum Role {
  ADMIN,
  USER,
  GUEST
}

const role = Role.ADMIN;
```

Enums can make certain fixed sets of values easier to represent.

However, many modern TypeScript projects also use union literal types:

```ts
type Role = "admin" | "user" | "guest";
```

---

## 33. What is the `never` type?

`never` represents a value that never occurs.

It is commonly used for functions that never successfully return.

```ts
function throwError(message: string): never {
  throw new Error(message);
}
```

Another example is an infinite loop:

```ts
function infiniteLoop(): never {
  while (true) {
    // ...
  }
}
```

### Interview Point

> `never` is different from `void`. `void` means the function does not return a useful value; `never` means it does not complete normally.

---

## 34. What is a class in TypeScript?

TypeScript supports JavaScript classes and adds features such as:

* Type annotations
* Access modifiers
* `readonly`
* Abstract classes
* Interfaces

Example:

```ts
class User {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  greet(): void {
    console.log(`Hello ${this.name}`);
  }
}

const user = new User("Veera", 21);
```

---

## 35. What are access modifiers in TypeScript?

TypeScript provides:

```text
public
private
protected
```

### Public

Accessible from anywhere.

```ts
class User {
  public name: string;

  constructor(name: string) {
    this.name = name;
  }
}
```

### Private

Accessible only inside the class.

```ts
class User {
  private password: string;

  constructor(password: string) {
    this.password = password;
  }
}
```

### Protected

Accessible inside the class and its subclasses.

```ts
class User {
  protected name: string;

  constructor(name: string) {
    this.name = name;
  }
}
```

---

# TypeScript Interview Revision Checklist

Before an interview, make sure you understand:

* [ ] TypeScript vs JavaScript
* [ ] Type inference
* [ ] Type annotations
* [ ] Primitive types
* [ ] `any`
* [ ] `unknown`
* [ ] `void`
* [ ] `never`
* [ ] Union types
* [ ] Literal types
* [ ] Arrays
* [ ] Tuples
* [ ] Objects
* [ ] Interfaces
* [ ] Type aliases
* [ ] Optional properties
* [ ] `readonly`
* [ ] Function types
* [ ] Optional parameters
* [ ] Default parameters
* [ ] Generics
* [ ] Type assertions
* [ ] Type narrowing
* [ ] Enums
* [ ] Classes
* [ ] Access modifiers

---

# Important TypeScript Interview Tip

When answering a TypeScript question, use this structure:

```text
1. Definition
2. Why it is used
3. Simple example
4. Real-world use case
5. Important difference / interview point
```

For example:

> **What is an interface?**

**Definition:** An interface defines the structure of an object.

**Why:** It provides type safety and makes object structures easier to understand.

**Example:**

```ts
interface User {
  name: string;
  age: number;
}
```

**Real-world use:**

```ts
const user: User = {
  name: "Veera",
  age: 21
};
```

**Interview Point:** Interfaces are commonly used for object shapes such as API responses, React props, and application models.

---

# Final Goal

After completing TypeScript preparation, you should be able to:

```text
Understand TypeScript
        ↓
Write typed JavaScript
        ↓
Create interfaces & types
        ↓
Use generics
        ↓
Understand narrowing
        ↓
Type functions & objects
        ↓
Use TypeScript with React
        ↓
Convert MERN projects to TypeScript
        ↓
Explain TypeScript confidently in interviews
```
