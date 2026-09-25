# JavaScript Interview Questions & Answers

A structured collection of commonly asked **JavaScript interview questions** covering fundamentals, ES6+, functions, objects, asynchronous JavaScript, DOM, and advanced concepts.

This section is designed for **frontend and MERN stack interview preparation**.

---

# Table of Contents

1. [What is JavaScript?](#1-what-is-javascript)
2. [What are the features of JavaScript?](#2-what-are-the-features-of-javascript)
3. [What is the difference between JavaScript and Java?](#3-what-is-the-difference-between-javascript-and-java)
4. [What are primitive and non-primitive data types?](#4-what-are-primitive-and-non-primitive-data-types)
5. [What is the difference between `var`, `let`, and `const`?](#5-what-is-the-difference-between-var-let-and-const)
6. [What is hoisting?](#6-what-is-hoisting)
7. [What is the Temporal Dead Zone?](#7-what-is-the-temporal-dead-zone)
8. [What is scope in JavaScript?](#8-what-is-scope-in-javascript)
9. [What is lexical scope?](#9-what-is-lexical-scope)
10. [What is the difference between `==` and `===`?](#10-what-is-the-difference-between--and-)
11. [What are truthy and falsy values?](#11-what-are-truthy-and-falsy-values)
12. [What is type coercion?](#12-what-is-type-coercion)
13. [What is `null` vs `undefined`?](#13-what-is-null-vs-undefined)
14. [What is `NaN`?](#14-what-is-nan)
15. [What is the difference between `typeof` and `instanceof`?](#15-what-is-the-difference-between-typeof-and-instanceof)
16. [What are function declarations and function expressions?](#16-what-are-function-declarations-and-function-expressions)
17. [What are arrow functions?](#17-what-are-arrow-functions)
18. [What are higher-order functions?](#18-what-are-higher-order-functions)
19. [What is a callback function?](#19-what-is-a-callback-function)
20. [What is a closure?](#20-what-is-a-closure)
21. [What is the `this` keyword?](#21-what-is-the-this-keyword)
22. [What are `call()`, `apply()`, and `bind()`?](#22-what-are-call-apply-and-bind)
23. [What is an IIFE?](#23-what-is-an-iife)
24. [What are rest and spread operators?](#24-what-are-rest-and-spread-operators)
25. [What is destructuring?](#25-what-is-destructuring)
26. [What are template literals?](#26-what-are-template-literals)
27. [What is optional chaining?](#27-what-is-optional-chaining)
28. [What is the nullish coalescing operator?](#28-what-is-the-nullish-coalescing-operator)
29. [What is the difference between shallow copy and deep copy?](#29-what-is-the-difference-between-shallow-copy-and-deep-copy)
30. [What is the difference between mutable and immutable data?](#30-what-is-the-difference-between-mutable-and-immutable-data)
31. [What is the difference between `map()`, `filter()`, and `reduce()`?](#31-what-is-the-difference-between-map-filter-and-reduce)
32. [What is the difference between `forEach()` and `map()`?](#32-what-is-the-difference-between-foreach-and-map)
33. [What are Promises?](#33-what-are-promises)
34. [What are the states of a Promise?](#34-what-are-the-states-of-a-promise)
35. [What is `async/await`?](#35-what-is-asyncawait)
36. [What is the difference between `Promise.all()` and `Promise.allSettled()`?](#36-what-is-the-difference-between-promiseall-and-promiseallsettled)
37. [What is the difference between `Promise.race()` and `Promise.any()`?](#37-what-is-the-difference-between-promiserace-and-promiseany)
38. [What is the Event Loop?](#38-what-is-the-event-loop)
39. [What is the difference between synchronous and asynchronous JavaScript?](#39-what-is-the-difference-between-synchronous-and-asynchronous-javascript)
40. [What are microtasks and macrotasks?](#40-what-are-microtasks-and-macrotasks)
41. [What is the prototype chain?](#41-what-is-the-prototype-chain)
42. [What are classes in JavaScript?](#42-what-are-classes-in-javascript)
43. [What is inheritance in JavaScript?](#43-what-is-inheritance-in-javascript)
44. [What is the difference between an object and a Map?](#44-what-is-the-difference-between-an-object-and-a-map)
45. [What is the difference between Map and WeakMap?](#45-what-is-the-difference-between-map-and-weakmap)
46. [What is debouncing?](#46-what-is-debouncing)
47. [What is throttling?](#47-what-is-throttling)
48. [What is event delegation?](#48-what-is-event-delegation)
49. [What is the difference between localStorage, sessionStorage, and cookies?](#49-what-is-the-difference-between-localstorage-sessionstorage-and-cookies)
50. [What is the difference between synchronous and asynchronous error handling?](#50-what-is-the-difference-between-synchronous-and-asynchronous-error-handling)

---

# 1. What is JavaScript?

### Answer

JavaScript is a **high-level, dynamically typed programming language** primarily used to build interactive and dynamic web applications.

It runs in browsers through JavaScript engines such as Google's **V8 engine** and can also run outside browsers using environments such as Node.js.

### Example

```javascript
const name = "Veera";

console.log(`Hello ${name}`);
```

### Important Point

JavaScript is not limited to frontend development. It is also used for:

* Frontend development
* Backend development with Node.js
* APIs
* Real-time applications
* Automation
* Desktop applications
* Mobile applications

---

# 2. What are the features of JavaScript?

### Answer

Important JavaScript features include:

* Dynamically typed
* Interpreted/JIT-compiled by modern engines
* First-class functions
* Object-based/prototype-based
* Supports asynchronous programming
* Event-driven
* Supports functional programming
* Supports object-oriented programming
* Runs in browsers and server environments

### Example

```javascript
const add = (a, b) => a + b;

console.log(add(10, 20));
```

Here, the function is treated like a value.

---

# 3. What is the difference between JavaScript and Java?

### Answer

JavaScript and Java are completely different programming languages.

| JavaScript                               | Java                                              |
| ---------------------------------------- | ------------------------------------------------- |
| Dynamically typed                        | Statically typed                                  |
| Primarily prototype-based                | Class-based                                       |
| Commonly used for web development        | Commonly used for enterprise/backend applications |
| Runs in JS engines                       | Runs on the JVM                                   |
| Supports functions as first-class values | Methods are associated with classes/objects       |

The similar names are historical; JavaScript is not a scripting version of Java.

---

# 4. What are primitive and non-primitive data types?

### Answer

JavaScript data types can broadly be divided into **primitive** and **non-primitive/reference** types.

### Primitive Types

```text
string
number
bigint
boolean
undefined
null
symbol
```

Example:

```javascript
let name = "Veera";
let age = 21;
let isDeveloper = true;
```

### Non-Primitive

Objects, including:

```javascript
const user = {
  name: "Veera",
  age: 21
};
```

Arrays and functions are also objects in JavaScript's type system.

### Important Point

Primitive values are immutable values, while objects are mutable data structures.

---

# 5. What is the difference between `var`, `let`, and `const`?

### Answer

All three declare variables, but they differ in scope, redeclaration, reassignment, and hoisting behaviour.

| Feature                     | `var`    | `let` | `const` |
| --------------------------- | -------- | ----- | ------- |
| Scope                       | Function | Block | Block   |
| Redeclaration in same scope | Yes      | No    | No      |
| Reassignment                | Yes      | Yes   | No      |
| Temporal Dead Zone          | No       | Yes   | Yes     |

### Example

```javascript
let age = 21;
age = 22;

const name = "Veera";
```

A `const` variable cannot be reassigned:

```javascript
const age = 21;

// Error
age = 22;
```

However, objects declared with `const` can still have their properties changed:

```javascript
const user = {
  name: "Veera"
};

user.name = "Rahul";
```

The variable binding remains the same object.

---

# 6. What is hoisting?

### Answer

Hoisting describes how JavaScript declarations are processed before the code executes.

Function declarations can be called before their declaration:

```javascript
sayHello();

function sayHello() {
  console.log("Hello");
}
```

`var` declarations are hoisted and initially have the value `undefined`.

```javascript
console.log(name);

var name = "Veera";
```

Output:

```text
undefined
```

`let` and `const` are also processed during scope creation, but accessing them before their declaration results in a `ReferenceError` because of the Temporal Dead Zone.

---

# 7. What is the Temporal Dead Zone?

### Answer

The **Temporal Dead Zone (TDZ)** is the period between entering a scope and reaching the declaration of a `let`, `const`, or `class` binding.

Example:

```javascript
console.log(age);

let age = 21;
```

This produces:

```text
ReferenceError
```

The variable exists in the lexical environment but cannot be accessed before its declaration is evaluated.

---

# 8. What is scope in JavaScript?

### Answer

Scope determines where a variable can be accessed.

Main types include:

* Global scope
* Function scope
* Block scope
* Module scope

Example:

```javascript
{
  let message = "Hello";
  console.log(message);
}

// Error
console.log(message);
```

`let` and `const` are block-scoped.

---

# 9. What is lexical scope?

### Answer

Lexical scope means that the accessibility of variables is determined by **where functions and blocks are written in the source code**.

Example:

```javascript
const name = "Veera";

function greet() {
  console.log(name);
}

greet();
```

`greet()` can access `name` because it was defined in an outer lexical scope.

This concept is fundamental to understanding closures.

---

# 10. What is the difference between `==` and `===`?

### Answer

`==` performs loose equality comparison and may perform type coercion.

`===` performs strict equality comparison without converting the operands.

```javascript
5 == "5";   // true
5 === "5";  // false
```

### Recommendation

Prefer `===` when you want predictable type-sensitive comparisons.

---

# 11. What are truthy and falsy values?

### Answer

A truthy value behaves like `true` in a Boolean context.

Falsy values include:

```text
false
0
-0
0n
""
null
undefined
NaN
```

Everything else is generally truthy, including:

```javascript
[]
{}
```

Example:

```javascript
if ("hello") {
  console.log("Truthy");
}
```

---

# 12. What is type coercion?

### Answer

Type coercion is the conversion of one data type into another during an operation.

Example:

```javascript
console.log("5" + 2);
```

Output:

```text
52
```

Because `+` with a string causes string concatenation.

Another example:

```javascript
console.log("5" - 2);
```

Output:

```text
3
```

The string is converted to a number.

### Important Point

Unexpected coercion is one reason strict equality (`===`) is generally preferred.

---

# 13. What is `null` vs `undefined`?

### `undefined`

Usually means a value has not been assigned or a property does not exist.

```javascript
let name;

console.log(name);
```

Output:

```text
undefined
```

### `null`

Usually represents an intentional absence of a value.

```javascript
let selectedUser = null;
```

### Simple Difference

```text
undefined → value is not available/assigned
null      → intentionally empty value
```

---

# 14. What is `NaN`?

### Answer

`NaN` means **Not-a-Number**.

It is a special numeric value produced when a numeric operation cannot produce a meaningful number.

```javascript
const result = Number("hello");

console.log(result); // NaN
```

To check for `NaN`, prefer:

```javascript
Number.isNaN(result);
```

---

# 15. What is the difference between `typeof` and `instanceof`?

### `typeof`

Used to determine the general type of a value.

```javascript
typeof "Hello"; // "string"
typeof 10;      // "number"
typeof true;    // "boolean"
```

### `instanceof`

Checks whether an object's prototype chain contains a constructor's `prototype`.

```javascript
const numbers = [];

console.log(numbers instanceof Array);
```

Output:

```text
true
```

---

# 16. What are function declarations and function expressions?

### Function Declaration

```javascript
function add(a, b) {
  return a + b;
}
```

Function declarations are hoisted in a way that allows them to be called before their declaration.

### Function Expression

```javascript
const add = function (a, b) {
  return a + b;
};
```

The function is assigned to a variable.

Function expressions follow the initialization rules of that variable.

---

# 17. What are arrow functions?

### Answer

Arrow functions provide shorter function syntax and have lexical `this`.

```javascript
const add = (a, b) => {
  return a + b;
};
```

Short form:

```javascript
const add = (a, b) => a + b;
```

### Important Difference

Arrow functions do not create their own `this`.

They capture `this` from their surrounding lexical scope.

---

# 18. What are higher-order functions?

### Answer

A higher-order function is a function that:

1. Accepts another function as an argument, or
2. Returns a function.

Example:

```javascript
function calculate(operation, a, b) {
  return operation(a, b);
}

const add = (a, b) => a + b;

console.log(calculate(add, 10, 20));
```

Common higher-order array methods include:

```text
map()
filter()
reduce()
forEach()
```

---

# 19. What is a callback function?

### Answer

A callback is a function passed to another function to be executed later or as part of that function's operation.

Example:

```javascript
function greet(name, callback) {
  console.log(`Hello ${name}`);
  callback();
}

greet("Veera", () => {
  console.log("Welcome!");
});
```

Callbacks are heavily used in asynchronous JavaScript and array methods.

---

# 20. What is a closure?

### Answer

A closure occurs when a function remembers and can access variables from its **lexical scope even after the outer function has finished executing**.

Example:

```javascript
function counter() {
  let count = 0;

  return function () {
    count++;
    return count;
  };
}

const increment = counter();

console.log(increment()); // 1
console.log(increment()); // 2
console.log(increment()); // 3
```

The returned function maintains access to `count`.

### Common Uses

* Data privacy
* Function factories
* Callbacks
* Event handlers
* Memoization
* Maintaining state

---

# 21. What is the `this` keyword?

### Answer

`this` refers to a value determined by **how a function is called** for ordinary functions.

Example:

```javascript
const user = {
  name: "Veera",

  greet() {
    console.log(this.name);
  }
};

user.greet();
```

Output:

```text
Veera
```

For arrow functions, `this` is lexical and is not created by the arrow function itself.

---

# 22. What are `call()`, `apply()`, and `bind()`?

### Answer

These methods allow you to control the `this` value when calling or creating a function invocation.

### `call()`

Arguments are passed individually.

```javascript
function greet(city) {
  console.log(this.name, city);
}

const user = {
  name: "Veera"
};

greet.call(user, "Bangalore");
```

### `apply()`

Arguments are passed as an array-like collection.

```javascript
greet.apply(user, ["Bangalore"]);
```

### `bind()`

Returns a new function with the specified `this`.

```javascript
const boundGreet = greet.bind(user);

boundGreet("Bangalore");
```

---

# 23. What is an IIFE?

### Answer

IIFE stands for **Immediately Invoked Function Expression**.

It is a function that is created and executed immediately.

```javascript
(function () {
  console.log("Executed immediately");
})();
```

IIFEs were historically used to create private scopes before modern module syntax became widely used.

---

# 24. What are rest and spread operators?

Both use `...`, but their purposes are different.

### Spread

Expands an iterable or object into individual elements/properties.

```javascript
const numbers = [1, 2, 3];

const copy = [...numbers];
```

### Rest

Collects multiple values into an array.

```javascript
function sum(...numbers) {
  return numbers.reduce((total, number) => total + number, 0);
}

console.log(sum(1, 2, 3, 4));
```

### Simple Difference

```text
Spread → expands
Rest   → collects
```

---

# 25. What is destructuring?

### Answer

Destructuring allows values to be extracted from arrays or objects into variables.

### Object Destructuring

```javascript
const user = {
  name: "Veera",
  age: 21
};

const { name, age } = user;
```

### Array Destructuring

```javascript
const numbers = [10, 20];

const [first, second] = numbers;
```

Destructuring is widely used in React.

```javascript
const { data, isLoading } = response;
```

---

# 26. What are template literals?

### Answer

Template literals use backticks and allow string interpolation.

```javascript
const name = "Veera";
const age = 21;

console.log(`My name is ${name} and I am ${age} years old.`);
```

They also support multiline strings.

```javascript
const message = `
Hello,
Welcome to JavaScript.
`;
```

---

# 27. What is optional chaining?

### Answer

Optional chaining `?.` allows you to safely access nested properties when an intermediate value may be `null` or `undefined`.

```javascript
const user = {};

console.log(user.address?.city);
```

Instead of throwing an error, the result is:

```text
undefined
```

It is especially useful when working with API responses.

---

# 28. What is the nullish coalescing operator?

### Answer

The `??` operator provides a fallback only when the left side is `null` or `undefined`.

```javascript
const username = null;

const name = username ?? "Guest";

console.log(name);
```

Output:

```text
Guest
```

### Difference from `||`

```javascript
0 || 100;   // 100
0 ?? 100;   // 0
```

`??` does not treat valid falsy values such as `0`, `false`, or `""` as missing.

---

# 29. What is the difference between shallow copy and deep copy?

### Shallow Copy

Copies the top-level structure but nested objects can still share references.

```javascript
const user = {
  name: "Veera",
  address: {
    city: "Bangalore"
  }
};

const copy = { ...user };
```

`copy.address` still references the same nested object.

### Deep Copy

Creates independent nested structures.

One modern approach for cloneable data is:

```javascript
const copy = structuredClone(user);
```

### Important Point

Do not assume that spread syntax creates a deep copy.

---

# 30. What is the difference between mutable and immutable data?

### Mutable

An object can be changed after creation.

```javascript
const user = {
  name: "Veera"
};

user.name = "Rahul";
```

### Immutable Approach

Create a new object instead:

```javascript
const updatedUser = {
  ...user,
  name: "Rahul"
};
```

Immutable update patterns are especially important in React and state-management libraries.

---

# 31. What is the difference between `map()`, `filter()`, and `reduce()`?

### `map()`

Transforms every element and returns a new array.

```javascript
const numbers = [1, 2, 3];

const doubled = numbers.map(number => number * 2);
```

Result:

```text
[2, 4, 6]
```

### `filter()`

Returns elements that satisfy a condition.

```javascript
const numbers = [1, 2, 3, 4];

const even = numbers.filter(number => number % 2 === 0);
```

Result:

```text
[2, 4]
```

### `reduce()`

Reduces an array to a single accumulated value.

```javascript
const numbers = [1, 2, 3, 4];

const total = numbers.reduce(
  (sum, number) => sum + number,
  0
);
```

Result:

```text
10
```

---

# 32. What is the difference between `forEach()` and `map()`?

### `forEach()`

Used to perform an operation for each element.

```javascript
numbers.forEach(number => {
  console.log(number);
});
```

It does not create a transformed array for you.

### `map()`

Creates and returns a new array.

```javascript
const doubled = numbers.map(number => number * 2);
```

### Interview Answer

Use `map()` when you need a transformed array.

Use `forEach()` when you simply want to perform an action for each element.

---

# 33. What are Promises?

### Answer

A Promise represents the eventual completion or failure of an asynchronous operation.

Example:

```javascript
const promise = fetch("/api/users");

promise
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error(error));
```

Promises help structure asynchronous operations without deeply nested callbacks.

---

# 34. What are the states of a Promise?

A Promise has three states:

```text
Pending
   ↓
 ┌───────────────┐
 ↓               ↓
Fulfilled      Rejected
```

### Pending

The operation has not completed.

### Fulfilled

The operation completed successfully.

### Rejected

The operation failed.

Once a Promise becomes fulfilled or rejected, it is **settled**.

---

# 35. What is `async/await`?

### Answer

`async/await` provides a cleaner syntax for working with Promises.

Example:

```javascript
async function getUsers() {
  try {
    const response = await fetch("/api/users");
    const data = await response.json();

    return data;
  } catch (error) {
    console.error(error);
  }
}
```

An `async` function always returns a Promise.

`await` pauses execution of that async function until the awaited Promise settles; it does not block the JavaScript thread.

---

# 36. What is the difference between `Promise.all()` and `Promise.allSettled()`?

### `Promise.all()`

Waits for all Promises to fulfill.

If one rejects, the returned Promise rejects.

```javascript
const results = await Promise.all([
  fetchUsers(),
  fetchProducts(),
  fetchOrders()
]);
```

### `Promise.allSettled()`

Waits for every Promise to settle, whether fulfilled or rejected.

```javascript
const results = await Promise.allSettled([
  fetchUsers(),
  fetchProducts(),
  fetchOrders()
]);
```

### Simple Difference

```text
Promise.all()
→ fail-fast when a Promise rejects

Promise.allSettled()
→ wait for every Promise
```

---

# 37. What is the difference between `Promise.race()` and `Promise.any()`?

### `Promise.race()`

Settles when the **first Promise settles**, whether fulfilled or rejected.

```javascript
Promise.race([
  requestOne(),
  requestTwo()
]);
```

### `Promise.any()`

Fulfills when the **first Promise fulfills**.

It rejects only if all input Promises reject.

```javascript
Promise.any([
  requestOne(),
  requestTwo()
]);
```

### Important Difference

```text
race → first settled
any  → first fulfilled
```

---

# 38. What is the Event Loop?

### Answer

The Event Loop is the mechanism that coordinates JavaScript execution with asynchronous operations.

JavaScript execution uses a call stack, while asynchronous APIs and queues allow work to be scheduled for later.

Simplified model:

```text
        JavaScript Code
              ↓
          Call Stack
              ↓
      Web / Runtime APIs
              ↓
          Task Queues
              ↓
          Event Loop
              ↓
          Call Stack
```

The Event Loop checks when the call stack is available and processes queued work according to the runtime's scheduling rules.

---

# 39. What is the difference between synchronous and asynchronous JavaScript?

### Synchronous

Operations execute sequentially.

```javascript
console.log("A");
console.log("B");
console.log("C");
```

Output:

```text
A
B
C
```

### Asynchronous

An operation can complete later while other JavaScript work continues.

```javascript
console.log("A");

setTimeout(() => {
  console.log("B");
}, 1000);

console.log("C");
```

Output:

```text
A
C
B
```

---

# 40. What are microtasks and macrotasks?

### Microtasks

Examples include:

* Promise callbacks
* `queueMicrotask()`

### Tasks / Macrotasks

Examples include:

* `setTimeout`
* `setInterval`
* Certain browser events and runtime tasks

A simplified ordering is:

```text
Synchronous Code
      ↓
Microtasks
      ↓
Next Task
```

For example:

```javascript
console.log("1");

setTimeout(() => {
  console.log("2");
}, 0);

Promise.resolve().then(() => {
  console.log("3");
});

console.log("4");
```

Output:

```text
1
4
3
2
```

The Promise callback is a microtask and is processed before the timer task in this example.

---

# 41. What is the prototype chain?

### Answer

JavaScript objects can inherit properties and methods through their prototype chain.

If a property is not found directly on an object, JavaScript looks at its prototype and continues upward.

Conceptually:

```text
object
   ↓
prototype
   ↓
prototype's prototype
   ↓
Object.prototype
   ↓
null
```

Example:

```javascript
const user = {};

console.log(user.toString);
```

`toString` is available through the object's prototype chain.

---

# 42. What are classes in JavaScript?

### Answer

Classes provide syntax for creating objects and implementing class-based patterns.

Example:

```javascript
class User {
  constructor(name) {
    this.name = name;
  }

  greet() {
    console.log(`Hello ${this.name}`);
  }
}

const user = new User("Veera");

user.greet();
```

JavaScript classes are built on top of the language's prototype-based inheritance model.

---

# 43. What is inheritance in JavaScript?

### Answer

Inheritance allows one object or class to reuse behaviour from another.

Using classes:

```javascript
class Animal {
  speak() {
    console.log("Animal speaks");
  }
}

class Dog extends Animal {
  bark() {
    console.log("Dog barks");
  }
}

const dog = new Dog();

dog.speak();
dog.bark();
```

`Dog` inherits the `speak()` method from `Animal`.

---

# 44. What is the difference between an Object and a Map?

### Object

```javascript
const user = {
  name: "Veera",
  age: 21
};
```

Objects are commonly used for structured records.

### Map

```javascript
const users = new Map();

users.set("user1", "Veera");
```

Maps are designed specifically for key-value collections.

### Important Differences

| Object                                          | Map                                |
| ----------------------------------------------- | ---------------------------------- |
| Commonly used for records                       | Designed for key-value collections |
| Keys are strings/symbols in normal object usage | Keys can be any value              |
| Has prototype-related behaviour                 | Dedicated Map API                  |
| `Object.keys()` etc.                            | `map.keys()`, `map.values()`       |

---

# 45. What is the difference between Map and WeakMap?

### Map

```javascript
const map = new Map();

map.set(user, "data");
```

Map can hold references to its keys and is iterable.

### WeakMap

```javascript
const weakMap = new WeakMap();

weakMap.set(user, "data");
```

WeakMap keys must be objects or non-registered symbols, and the collection does not prevent garbage collection of otherwise unreachable object keys.

WeakMap is useful when metadata should be associated with objects without keeping those objects alive solely because of the collection.

---

# 46. What is debouncing?

### Answer

Debouncing delays function execution until a specified period has passed without another call.

It is useful for events such as:

* Search input
* Resize events
* Form validation

Example concept:

```text
User types:
H → He → Hel → Hell → Hello

Instead of calling API 5 times:

                    Wait
                     ↓
                 API Request
```

In a search box, this can reduce unnecessary API requests while the user is typing.

---

# 47. What is throttling?

### Answer

Throttling limits how frequently a function can execute during a period of continuous events.

Useful for:

* Scroll events
* Mouse movement
* Window resize
* Continuous user interactions

Conceptually:

```text
Event Event Event Event Event
  ↓
  ↓
Function
  ↓
wait
  ↓
Function
```

### Difference

```text
Debounce → execute after activity stops
Throttle → execute at controlled intervals
```

---

# 48. What is event delegation?

### Answer

Event delegation uses a parent element to handle events from its child elements.

Instead of attaching separate listeners to many children:

```javascript
parent.addEventListener("click", (event) => {
  if (event.target.matches(".button")) {
    console.log("Button clicked");
  }
});
```

The parent handles the event using event bubbling.

### Benefits

* Fewer event listeners
* Useful for dynamically created elements
* Can simplify event handling

---

# 49. What is the difference between localStorage, sessionStorage, and cookies?

| Feature                               | localStorage             | sessionStorage              | Cookies                    |
| ------------------------------------- | ------------------------ | --------------------------- | -------------------------- |
| Persistence                           | Until explicitly removed | Until page/session ends     | Controlled by expiry       |
| Sent automatically with HTTP requests | No                       | No                          | Yes, when applicable       |
| Typical capacity                      | Larger than cookies      | Larger than cookies         | Small                      |
| Common use                            | Client preferences       | Temporary browser-tab state | Sessions/auth-related data |

Example:

```javascript
localStorage.setItem("theme", "dark");

const theme = localStorage.getItem("theme");
```

### Security Point

Do not treat browser storage as automatically secure. Sensitive authentication design should consider threats such as XSS and CSRF and use appropriate server-side and cookie-based protections where required.

---

# 50. What is the difference between synchronous and asynchronous error handling?

### Synchronous

Use `try...catch`:

```javascript
try {
  throw new Error("Something went wrong");
} catch (error) {
  console.error(error.message);
}
```

### Async with `async/await`

```javascript
async function getData() {
  try {
    const response = await fetch("/api/data");
    const data = await response.json();

    return data;
  } catch (error) {
    console.error(error);
  }
}
```

### Promise style

```javascript
fetch("/api/data")
  .then(response => response.json())
  .catch(error => {
    console.error(error);
  });
```

The important point is that asynchronous operations must have their errors handled through the mechanism used by that asynchronous API.

---

# JavaScript Interview Revision Checklist

Before an interview, make sure you can explain these topics without memorising the answers word-for-word.

```text
JavaScript Fundamentals
├── Data Types
├── var / let / const
├── Hoisting
├── Scope
├── TDZ
├── Equality
├── Type Coercion
└── Truthy / Falsy

Functions
├── Function Declaration
├── Function Expression
├── Arrow Functions
├── Callback Functions
├── Higher-Order Functions
├── Closures
└── this

ES6+
├── Destructuring
├── Spread
├── Rest
├── Template Literals
├── Optional Chaining
└── Nullish Coalescing

Arrays & Objects
├── map
├── filter
├── reduce
├── forEach
├── Shallow Copy
├── Deep Copy
├── Object
├── Map
└── WeakMap

Asynchronous JavaScript
├── Callbacks
├── Promises
├── async / await
├── Promise.all
├── Promise.allSettled
├── Promise.race
├── Promise.any
├── Event Loop
└── Microtasks / Tasks

Advanced JavaScript
├── Prototype Chain
├── Classes
├── Inheritance
├── Debouncing
├── Throttling
└── Event Delegation

Browser
├── localStorage
├── sessionStorage
└── Cookies
```

---

# Final Interview Strategy

For each question, prepare yourself to answer in this order:

```text
1. Definition
      ↓
2. Simple Explanation
      ↓
3. Code Example
      ↓
4. Real-world Use Case
      ↓
5. Important Interview Point
```

For example:

```text
Question:
What is a closure?

Definition:
A closure is a function that retains access to
variables from its lexical scope.

Example:
counter()

Use Case:
Private state / callbacks / event handlers

Interview Point:
Closures are created because functions retain
access to their lexical environment.
```

This approach helps you explain concepts naturally instead of memorising long paragraphs.

---

# Repository Learning Structure

```text
mern-interview-preparation/
│
├── frontend/
│   │
│   ├── javascript/
│   │   ├── javascript-interview-questions.md
│   │   ├── javascript-output-questions.md
│   │   └── javascript-coding-questions.md
│   │
│   ├── react/
│   │   ├── react-interview-questions.md
│   │   ├── react-scenarios.md
│   │   └── react-coding-questions.md
│   │
│   ├── html/
│   ├── css/
│   ├── tailwind/
│   └── typescript/
│
├── backend/
├── authentication/
├── api/
├── database/
├── tools/
├── testing/
├── deployment/
├── coding/
└── mock-interviews/
```

**Next step:** after adding this file as `frontend/javascript/javascript-interview-questions.md`, the React file should follow the same format and cover **40–50 React interview questions**, focusing on React fundamentals, hooks, component lifecycle, state management, rendering, performance, forms, Context API, routing, and practical React scenarios.
