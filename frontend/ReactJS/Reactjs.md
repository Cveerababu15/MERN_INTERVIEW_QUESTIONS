# React.js Interview Questions & Answers

A structured collection of commonly asked **React.js interview questions** covering React fundamentals, components, JSX, props, state, hooks, rendering, forms, Context API, performance, state management, and practical concepts.

This section is designed for **Frontend Developer and MERN Stack interviews**.

---

# Table of Contents

1. [What is React.js?](#1-what-is-reactjs)
2. [Why is React used?](#2-why-is-react-used)
3. [What are the main features of React?](#3-what-are-the-main-features-of-react)
4. [What is a React component?](#4-what-is-a-react-component)
5. [What is the difference between functional and class components?](#5-what-is-the-difference-between-functional-and-class-components)
6. [What is JSX?](#6-what-is-jsx)
7. [Why can't browsers directly understand JSX?](#7-why-cant-browsers-directly-understand-jsx)
8. [What are props in React?](#8-what-are-props-in-react)
9. [What is state in React?](#9-what-is-state-in-react)
10. [Props vs state](#10-props-vs-state)
11. [What is one-way data flow?](#11-what-is-one-way-data-flow)
12. [What is the Virtual DOM?](#12-what-is-the-virtual-dom)
13. [What is reconciliation?](#13-what-is-reconciliation)
14. [What is rendering in React?](#14-what-is-rendering-in-react)
15. [What causes a React component to re-render?](#15-what-causes-a-react-component-to-re-render)
16. [What is the `key` prop?](#16-what-is-the-key-prop)
17. [Why should we not use array indexes as keys?](#17-why-should-we-not-use-array-indexes-as-keys)
18. [What is conditional rendering?](#18-what-is-conditional-rendering)
19. [What are React Fragments?](#19-what-are-react-fragments)
20. [What is `useState`?](#20-what-is-usestate)
21. [Why should state updates be treated as immutable?](#21-why-should-state-updates-be-treated-as-immutable)
22. [What is `useEffect`?](#22-what-is-useeffect)
23. [What is the dependency array in `useEffect`?](#23-what-is-the-dependency-array-in-useeffect)
24. [What is cleanup in `useEffect`?](#24-what-is-cleanup-in-useeffect)
25. [What is `useRef`?](#25-what-is-useref)
26. [What is the difference between `useRef` and `useState`?](#26-what-is-the-difference-between-useref-and-usestate)
27. [What is `useMemo`?](#27-what-is-usememo)
28. [What is `useCallback`?](#28-what-is-usecallback)
29. [What is `React.memo`?](#29-what-is-reactmemo)
30. [What is the difference between `useMemo`, `useCallback`, and `React.memo`?](#30-what-is-the-difference-between-usememo-usecallback-and-reactmemo)
31. [What are the Rules of Hooks?](#31-what-are-the-rules-of-hooks)
32. [Why can't Hooks be called conditionally?](#32-why-cant-hooks-be-called-conditionally)
33. [What are custom Hooks?](#33-what-are-custom-hooks)
34. [What is prop drilling?](#34-what-is-prop-drilling)
35. [What is the Context API?](#35-what-is-the-context-api)
36. [Context API vs Zustand/Redux](#36-context-api-vs-zustandredux)
37. [What are controlled components?](#37-what-are-controlled-components)
38. [What are uncontrolled components?](#38-what-are-uncontrolled-components)
39. [How do you handle forms in React?](#39-how-do-you-handle-forms-in-react)
40. [How do you fetch API data in React?](#40-how-do-you-fetch-api-data-in-react)
41. [How do you handle loading and error states?](#41-how-do-you-handle-loading-and-error-states)
42. [What is lifting state up?](#42-what-is-lifting-state-up)
43. [What is component composition?](#43-what-is-component-composition)
44. [What are portals?](#44-what-are-portals)
45. [What are error boundaries?](#45-what-are-error-boundaries)
46. [What is lazy loading in React?](#46-what-is-lazy-loading-in-react)
47. [What is `Suspense`?](#47-what-is-suspense)
48. [How can you optimise React performance?](#48-how-can-you-optimise-react-performance)
49. [What is Strict Mode?](#49-what-is-strict-mode)
50. [How would you structure a scalable React application?](#50-how-would-you-structure-a-scalable-react-application)

---

# 1. What is React.js?

### Answer

React.js is a **JavaScript library for building user interfaces**, especially component-based web applications.

React allows applications to be divided into reusable components.

Example:

```jsx
function Welcome() {
  return <h1>Hello, React!</h1>;
}
```

A larger application can be composed from many such components.

```text
Application
    │
    ├── Navbar
    ├── Sidebar
    ├── ProductList
    ├── ProductCard
    └── Footer
```

### Interview Point

React is primarily a UI library. Routing, server-state management, and other application concerns are commonly handled using additional libraries or frameworks.

---

# 2. Why is React used?

React is commonly used because it provides:

* Component-based architecture
* Reusable UI components
* Declarative UI development
* Efficient update mechanisms
* A large ecosystem
* Strong developer tooling
* Support for modern frontend architectures

Example:

```text
ProductCard
     ↓
Reusable
     ↓
Product 1
Product 2
Product 3
Product 4
```

Instead of writing separate markup for every product, one component can be reused with different data.

---

# 3. What are the main features of React?

Important React features include:

* Components
* JSX
* Props
* State
* Hooks
* Declarative UI
* One-way data flow
* Component composition
* Reconciliation
* Context API
* Client-side rendering capabilities

React also has an ecosystem for routing, data fetching, state management, testing, and other application requirements.

---

# 4. What is a React component?

### Answer

A component is a reusable unit of UI and logic.

Example:

```jsx
function ProductCard({ name, price }) {
  return (
    <div>
      <h2>{name}</h2>
      <p>₹{price}</p>
    </div>
  );
}
```

It can be reused:

```jsx
<ProductCard name="Mango Powder" price={299} />

<ProductCard name="Banana Powder" price={249} />
```

### Important Point

Good components generally have a clear responsibility and should be reusable where appropriate.

---

# 5. What is the difference between functional and class components?

### Functional Component

Uses a JavaScript function.

```jsx
function Welcome() {
  return <h1>Hello</h1>;
}
```

Modern React development primarily uses functional components and Hooks.

### Class Component

Uses a JavaScript class:

```jsx
class Welcome extends React.Component {
  render() {
    return <h1>Hello</h1>;
  }
}
```

Class components are still supported, but new React code generally favours function components.

---

# 6. What is JSX?

### Answer

JSX is a syntax extension that allows you to write markup-like syntax inside JavaScript.

Example:

```jsx
const element = <h1>Hello React</h1>;
```

JSX makes component UI easier to describe.

You can also embed JavaScript expressions:

```jsx
const name = "Veera";

const element = <h1>Hello {name}</h1>;
```

JSX is transformed into JavaScript during the build process.

---

# 7. Why can't browsers directly understand JSX?

### Answer

JSX is not standard browser JavaScript syntax.

A build tool/compiler transforms JSX into JavaScript that the browser can execute.

Conceptually:

```text
JSX
 ↓
Transformation
 ↓
JavaScript
 ↓
Browser JavaScript Engine
```

Modern React projects commonly use build tools such as Vite to handle this transformation as part of the development/build pipeline.

---

# 8. What are props in React?

### Answer

Props are values passed from a parent component to a child component.

Example:

```jsx
function Product({ name, price }) {
  return (
    <div>
      <h2>{name}</h2>
      <p>₹{price}</p>
    </div>
  );
}
```

Parent:

```jsx
<Product name="Mango Powder" price={299} />
```

### Important Point

Props are read-only from the receiving component's perspective. A child should not directly modify the props it receives.

---

# 9. What is state in React?

### Answer

State is data managed by a component that can change over time.

Example:

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      {count}
    </button>
  );
}
```

When the state changes, React schedules the component to render again.

---

# 10. Props vs State

| Props                        | State                                  |
| ---------------------------- | -------------------------------------- |
| Passed from parent           | Managed by component                   |
| Read-only to child           | Updated through state setters/dispatch |
| Used to configure components | Represents changing data               |
| Parent controls the value    | Component manages its state            |

Example:

```text
Parent
  │
  │ props
  ↓
Child
  │
  │ local state
  ↓
Child UI
```

---

# 11. What is one-way data flow?

### Answer

React follows a model where data generally flows from parent components to child components through props.

```text
Parent
  ↓
Props
  ↓
Child
  ↓
Grandchild
```

If a child needs to cause a parent-owned state to change, the parent can pass a callback.

```jsx
function Parent() {
  const [count, setCount] = useState(0);

  return <Child onIncrement={() => setCount(count + 1)} />;
}
```

The child calls the provided function rather than directly modifying the parent's state.

---

# 12. What is the Virtual DOM?

### Answer

The Virtual DOM is an in-memory representation of UI used by React's rendering system.

When state or props change, React creates a new representation and determines what needs to change in the actual UI.

Conceptually:

```text
State / Props Change
        ↓
React Render
        ↓
New UI Representation
        ↓
Reconciliation
        ↓
Required DOM Updates
```

### Important Point

React's performance does not simply come from "using a Virtual DOM". Its rendering and reconciliation architecture determines how updates are processed.

---

# 13. What is reconciliation?

### Answer

Reconciliation is React's process of determining how the UI should change when a component renders again.

React compares the previous rendered tree with the next rendered result and determines the necessary updates.

Keys are particularly important when rendering lists because they help React identify list items.

```jsx
items.map(item => (
  <Product key={item.id} {...item} />
));
```

---

# 14. What is rendering in React?

### Answer

Rendering means React calls components to determine what the UI should look like for the current state and props.

Example:

```jsx
function App() {
  return <h1>Hello</h1>;
}
```

When relevant state or props change, React may render the component again.

### Important Point

A render does not necessarily mean the browser DOM is completely rebuilt. React determines the required UI updates.

---

# 15. What causes a React component to re-render?

Common reasons include:

1. Its state changes.
2. Its parent renders and passes changed props.
3. A consumed context value changes.
4. An external store subscription reports a relevant change.

Example:

```jsx
const [count, setCount] = useState(0);

setCount(count + 1);
```

This schedules a render because the component's state changed.

---

# 16. What is the `key` prop?

### Answer

The `key` prop gives React a stable identity for elements in a list.

Example:

```jsx
products.map(product => (
  <Product
    key={product.id}
    product={product}
  />
));
```

Keys help React determine which items were added, removed, or reordered.

### Best Practice

Use a stable unique identifier from the data whenever possible.

---

# 17. Why should we not use array indexes as keys?

Consider:

```jsx
items.map((item, index) => (
  <Item key={index} item={item} />
));
```

If items are inserted, removed, or reordered, the same index can refer to a different item.

This can cause incorrect component identity and unexpected state behaviour.

Prefer:

```jsx
<Item key={item.id} item={item} />
```

when a stable ID is available.

---

# 18. What is conditional rendering?

### Answer

Conditional rendering means displaying different UI based on a condition.

Using a ternary:

```jsx
{isLoggedIn ? (
  <Dashboard />
) : (
  <Login />
)}
```

Using `&&`:

```jsx
{isAdmin && <AdminPanel />}
```

Using an `if` statement:

```jsx
if (isLoading) {
  return <Loading />;
}
```

---

# 19. What are React Fragments?

### Answer

Fragments allow multiple elements to be returned without adding an unnecessary DOM element.

```jsx
<>
  <h1>Hello</h1>
  <p>Welcome</p>
</>
```

Instead of:

```jsx
<div>
  <h1>Hello</h1>
  <p>Welcome</p>
</div>
```

Fragments are useful when an extra wrapper would affect markup structure or styling.

---

# 20. What is `useState`?

### Answer

`useState` is a React Hook that lets a function component hold state.

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      {count}
    </button>
  );
}
```

The return value contains:

```text
[count, setCount]
```

The setter schedules a state update.

---

# 21. Why should state updates be treated as immutable?

### Answer

React state should be updated by creating a new value rather than directly mutating the existing state.

Incorrect:

```jsx
user.name = "Rahul";
setUser(user);
```

Better:

```jsx
setUser({
  ...user,
  name: "Rahul"
});
```

For arrays:

```jsx
setItems([
  ...items,
  newItem
]);
```

Immutable update patterns make state changes predictable and work well with React's rendering model.

---

# 22. What is `useEffect`?

### Answer

`useEffect` is a Hook used to synchronise a component with external systems.

Common examples include:

* Fetching data
* Subscribing to events
* Timers
* Browser APIs
* External connections

Example:

```jsx
useEffect(() => {
  document.title = "Dashboard";
}, []);
```

### Important Point

`useEffect` should not be used simply because code needs to run after every render. It is intended for synchronising with external systems.

---

# 23. What is the dependency array in `useEffect`?

The dependency array controls when an Effect is re-run based on its reactive dependencies.

### No dependency array

```jsx
useEffect(() => {
  console.log("Effect");
});
```

It runs after every relevant render.

### Empty array

```jsx
useEffect(() => {
  console.log("Effect");
}, []);
```

It runs after the initial mount in normal production behaviour.

### With dependencies

```jsx
useEffect(() => {
  console.log(userId);
}, [userId]);
```

It re-runs when `userId` changes.

---

# 24. What is cleanup in `useEffect`?

### Answer

An Effect can return a cleanup function.

Example:

```jsx
useEffect(() => {
  const timer = setInterval(() => {
    console.log("Running");
  }, 1000);

  return () => {
    clearInterval(timer);
  };
}, []);
```

Cleanup is used to remove subscriptions, timers, listeners, or other resources established by the Effect.

---

# 25. What is `useRef`?

### Answer

`useRef` returns a mutable ref object whose `.current` value persists across renders without itself causing a re-render when changed.

### DOM Example

```jsx
const inputRef = useRef(null);

function focusInput() {
  inputRef.current?.focus();
}

return (
  <>
    <input ref={inputRef} />
    <button onClick={focusInput}>
      Focus
    </button>
  </>
);
```

It can also store mutable values that need to survive between renders.

---

# 26. What is the difference between `useRef` and `useState`?

| `useState`                      | `useRef`                                              |
| ------------------------------- | ----------------------------------------------------- |
| Stores state used for rendering | Stores a mutable reference                            |
| Updating it schedules a render  | Changing `.current` does not itself trigger a render  |
| Used for UI state               | Used for DOM references and persistent mutable values |

Example:

```jsx
const [count, setCount] = useState(0);

const renderCount = useRef(0);
```

---

# 27. What is `useMemo`?

### Answer

`useMemo` caches the result of a calculation between renders until its dependencies change.

```jsx
const filteredProducts = useMemo(() => {
  return products.filter(product =>
    product.name.includes(search)
  );
}, [products, search]);
```

It can be useful when a calculation is expensive and avoiding repeated calculation has measurable value.

### Important Point

Do not use `useMemo` everywhere. Memoization has its own cost and should solve an actual performance problem.

---

# 28. What is `useCallback`?

### Answer

`useCallback` caches a function reference between renders until its dependencies change.

```jsx
const handleDelete = useCallback((id) => {
  deleteProduct(id);
}, [deleteProduct]);
```

It is commonly useful when passing callbacks to memoized child components or when a stable function reference is otherwise required.

---

# 29. What is `React.memo`?

### Answer

`React.memo` can skip re-rendering a function component when its props have not changed according to its comparison.

Example:

```jsx
const ProductCard = React.memo(function ProductCard({ product }) {
  return <h2>{product.name}</h2>;
});
```

It is a performance optimisation, not something every component requires.

---

# 30. What is the difference between `useMemo`, `useCallback`, and `React.memo`?

| Tool          | Memoizes                                     |
| ------------- | -------------------------------------------- |
| `useMemo`     | A calculated value                           |
| `useCallback` | A function reference                         |
| `React.memo`  | A component's rendered result based on props |

Example:

```text
useMemo
  ↓
value

useCallback
  ↓
function

React.memo
  ↓
component
```

They should be used when they provide a measurable or meaningful optimisation.

---

# 31. What are the Rules of Hooks?

React Hooks follow two main rules:

### Rule 1

Call Hooks only at the top level.

Do not call them inside:

* Loops
* Conditions
* Nested functions

Incorrect:

```jsx
if (isLoggedIn) {
  useState(0);
}
```

### Rule 2

Call Hooks only from:

* React function components
* Custom Hooks

These rules allow React to maintain consistent Hook ordering between renders.

---

# 32. Why can't Hooks be called conditionally?

React relies on the order in which Hooks are called to associate Hook state with the correct Hook call.

Incorrect:

```jsx
if (condition) {
  useState(0);
}

useEffect(() => {});
```

If `condition` changes between renders, the Hook ordering changes.

Correct:

```jsx
const [count, setCount] = useState(0);

useEffect(() => {
  if (condition) {
    // logic
  }
}, [condition]);
```

---

# 33. What are custom Hooks?

### Answer

A custom Hook is a reusable function whose name starts with `use` and which can use other Hooks.

Example:

```jsx
function useCounter() {
  const [count, setCount] = useState(0);

  const increment = () => {
    setCount(value => value + 1);
  };

  return {
    count,
    increment
  };
}
```

Usage:

```jsx
const { count, increment } = useCounter();
```

Custom Hooks help reuse stateful logic without duplicating it across components.

---

# 34. What is prop drilling?

### Answer

Prop drilling occurs when data is passed through several intermediate components that do not actually need the data themselves.

```text
App
 ↓
Parent
 ↓
Child
 ↓
GrandChild
 ↓
Component needing data
```

For large component trees, this can make code harder to maintain.

Possible solutions include:

* Component composition
* Context
* State-management libraries
* Better component boundaries

---

# 35. What is the Context API?

### Answer

Context allows data to be made available to components deeper in the component tree without manually passing props through every intermediate component.

Example:

```jsx
const ThemeContext = createContext(null);
```

Provider:

```jsx
<ThemeContext.Provider value={theme}>
  <App />
</ThemeContext.Provider>
```

Consumer:

```jsx
const theme = useContext(ThemeContext);
```

Common uses include:

* Theme
* Locale
* Authentication information
* Shared configuration

---

# 36. Context API vs Zustand/Redux

### Context

Useful for making values available through a component tree.

### Zustand / Redux

Designed specifically for application state management and can provide more structured state subscriptions and update patterns.

A simple distinction:

```text
Context
→ dependency/value distribution

Zustand / Redux
→ application state management
```

The right choice depends on application requirements rather than one tool always being superior.

---

# 37. What are controlled components?

### Answer

A controlled form element gets its current value from React state.

```jsx
function Login() {
  const [email, setEmail] = useState("");

  return (
    <input
      value={email}
      onChange={event => setEmail(event.target.value)}
    />
  );
}
```

React state is the source of truth for the input value.

---

# 38. What are uncontrolled components?

### Answer

An uncontrolled component allows the DOM to maintain the form value, while React can access it using a ref.

```jsx
function Form() {
  const inputRef = useRef(null);

  function handleSubmit(event) {
    event.preventDefault();

    console.log(inputRef.current.value);
  }

  return (
    <form onSubmit={handleSubmit}>
      <input ref={inputRef} />
      <button>Submit</button>
    </form>
  );
}
```

### Simple Difference

```text
Controlled
React state → input value

Uncontrolled
DOM → input value
```

---

# 39. How do you handle forms in React?

A common approach is controlled inputs.

```jsx
function LoginForm() {
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");

  function handleSubmit(event) {
    event.preventDefault();

    console.log({
      email,
      password
    });
  }

  return (
    <form onSubmit={handleSubmit}>
      <input
        value={email}
        onChange={event => setEmail(event.target.value)}
      />

      <input
        type="password"
        value={password}
        onChange={event => setPassword(event.target.value)}
      />

      <button type="submit">
        Login
      </button>
    </form>
  );
}
```

For larger forms, libraries such as React Hook Form can reduce repetitive form-management code.

---

# 40. How do you fetch API data in React?

For a simple component, an Effect can be used to synchronise with an API request.

```jsx
useEffect(() => {
  async function fetchProducts() {
    const response = await fetch("/api/products");
    const data = await response.json();

    setProducts(data);
  }

  fetchProducts();
}, []);
```

In production applications, server-state libraries such as TanStack Query can provide caching, request deduplication, invalidation, retries, and other features.

---

# 41. How do you handle loading and error states?

A common pattern is to maintain separate states.

```jsx
const [products, setProducts] = useState([]);
const [loading, setLoading] = useState(false);
const [error, setError] = useState(null);
```

Then:

```jsx
if (loading) {
  return <p>Loading...</p>;
}

if (error) {
  return <p>{error}</p>;
}

return <ProductList products={products} />;
```

### State Flow

```text
Request
   ↓
Loading
   ↓
 ┌───────────────┐
 ↓               ↓
Success         Error
 ↓               ↓
Data            Error UI
```

---

# 42. What is lifting state up?

### Answer

Lifting state up means moving shared state to the closest common parent of the components that need it.

Example:

```text
        Parent
       /      \
      ↓        ↓
  Input      Preview
```

If both components need the same value, the parent can own the state and pass the value and update function to each child.

```jsx
function Parent() {
  const [value, setValue] = useState("");

  return (
    <>
      <Input value={value} onChange={setValue} />
      <Preview value={value} />
    </>
  );
}
```

---

# 43. What is component composition?

### Answer

Composition means building larger components by combining smaller components.

Example:

```jsx
function Card({ children }) {
  return (
    <div className="card">
      {children}
    </div>
  );
}
```

Usage:

```jsx
<Card>
  <h2>Product</h2>
  <p>₹299</p>
</Card>
```

Composition is often preferred over creating deeply specialised components with many configuration props.

---

# 44. What are portals?

### Answer

A portal allows React to render a component's DOM output into a different DOM node while keeping it in the same React tree.

A common use case is a modal.

```text
React Tree
   │
   └── Modal
          │
          ↓
     document.body
```

Conceptually:

```jsx
createPortal(
  <Modal />,
  document.body
);
```

Portals are useful for UI that needs to escape normal DOM stacking or overflow constraints.

---

# 45. What are error boundaries?

### Answer

Error boundaries are React components that catch certain rendering errors in their child component tree and display fallback UI instead of allowing the entire affected UI section to fail.

Traditionally, error boundaries are implemented using class components.

They are useful for:

* Application-level fallback UI
* Isolating failures
* Reporting rendering errors

They do not replace normal `try/catch` for arbitrary asynchronous JavaScript errors.

---

# 46. What is lazy loading in React?

### Answer

Lazy loading allows a component's code to be loaded only when it is needed.

Example:

```jsx
const Dashboard = lazy(() => import("./Dashboard"));
```

This can reduce the initial JavaScript that must be loaded for an application.

Typical use case:

```text
Application
    ↓
Initial Bundle
    ↓
User navigates to Dashboard
    ↓
Dashboard chunk loads
```

---

# 47. What is `Suspense`?

### Answer

`Suspense` allows React to display fallback UI while a supported part of the component tree is not ready.

With lazy loading:

```jsx
<Suspense fallback={<p>Loading...</p>}>
  <Dashboard />
</Suspense>
```

The fallback is displayed while the lazy-loaded component is being loaded.

---

# 48. How can you optimise React performance?

Common techniques include:

### 1. Avoid unnecessary state

Keep state close to where it is needed.

### 2. Use stable keys

```jsx
key={product.id}
```

### 3. Memoise selectively

Use:

```text
React.memo
useMemo
useCallback
```

when there is a real performance reason.

### 4. Lazy-load large features

```jsx
lazy(() => import("./Dashboard"));
```

### 5. Avoid unnecessary effects

Do not use Effects for derived values that can be calculated during rendering.

### 6. Optimise large lists

For very large datasets, consider list virtualisation.

### 7. Optimise network requests

Use caching and appropriate server-state management.

### Important Point

Performance optimisation should be based on measurement and actual bottlenecks rather than blindly adding memoization.

---

# 49. What is Strict Mode?

### Answer

`StrictMode` is a development-only React feature that helps identify potential problems in an application.

Example:

```jsx
<StrictMode>
  <App />
</StrictMode>
```

It can intentionally invoke certain development behaviours more than once to help reveal unsafe assumptions.

### Important Point

Development behaviour under Strict Mode can differ from production behaviour. It does not mean your production application will necessarily execute the same code twice.

---

# 50. How would you structure a scalable React application?

A simple feature-oriented structure could look like:

```text
src/
│
├── components/
│   ├── common/
│   └── layout/
│
├── features/
│   ├── auth/
│   ├── products/
│   ├── cart/
│   └── orders/
│
├── hooks/
│
├── services/
│
├── store/
│
├── routes/
│
├── utils/
│
├── assets/
│
├── App.jsx
└── main.jsx
```

### Example Responsibility

```text
features/
    ↓
Business/domain functionality

components/
    ↓
Reusable UI

hooks/
    ↓
Reusable React logic

services/
    ↓
API communication

store/
    ↓
Global client state

routes/
    ↓
Application navigation
```

The exact structure should depend on application size and team requirements.

---

# React Interview Revision Checklist

Before an interview, make sure you can explain:

```text
React Fundamentals
├── React
├── Components
├── JSX
├── Props
├── State
├── One-way Data Flow
├── Rendering
├── Reconciliation
└── Keys

Hooks
├── useState
├── useEffect
├── useRef
├── useMemo
├── useCallback
├── useContext
└── Custom Hooks

Component Architecture
├── Composition
├── Lifting State
├── Prop Drilling
└── Reusable Components

Forms
├── Controlled Components
├── Uncontrolled Components
└── Form Handling

Data
├── API Requests
├── Loading State
├── Error State
└── Server State

Performance
├── React.memo
├── useMemo
├── useCallback
├── Lazy Loading
├── Suspense
└── Large List Optimisation

Advanced
├── Context API
├── Portals
├── Error Boundaries
├── Strict Mode
└── Scalable Architecture
```

---

# React Interview Answer Strategy

For every React question, use this structure during an interview:

```text
1. Definition
       ↓
2. Why it is used
       ↓
3. Simple explanation
       ↓
4. Code example
       ↓
5. Real-world use case
       ↓
6. Important interview point
```

For example:

```text
Question:
What is useEffect?

Definition:
useEffect is a Hook used to synchronise a component
with an external system.

Why:
It is useful for subscriptions, timers, browser APIs,
and network synchronisation.

Example:
useEffect(() => {
  document.title = "Dashboard";
}, []);

Important Point:
Do not use Effects unnecessarily for values that can
be derived directly during rendering.
```

---

# React Learning Progress

```text
React Fundamentals
       ↓
Components & JSX
       ↓
Props & State
       ↓
Rendering & Reconciliation
       ↓
Hooks
       ↓
Forms
       ↓
Context API
       ↓
API Integration
       ↓
Performance
       ↓
Advanced React
       ↓
Real-World Architecture
```

---

# Final Goal

The purpose of this section is not to memorise 50 answers.

The goal is to be able to:

```text
Understand
    ↓
Explain
    ↓
Write Code
    ↓
Debug
    ↓
Apply in Projects
    ↓
Explain the Design Decision in an Interview
```

This prepares the React foundation required for **Frontend Developer and MERN Stack interviews**.

---

**Part of the MERN Interview Preparation Repository**
