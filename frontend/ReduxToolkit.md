# Redux Toolkit Interview Questions

> **Level:** Fresher / Junior Developer
> **Focus:** Important Redux Toolkit concepts + commonly asked interview questions
> **Prerequisite:** Basic React + JavaScript

---

# 1. What is Redux?

Redux is a **state management library** used to manage application state in a predictable way.

It is useful when multiple components need access to the same state.

### Example

```text
React Components
       ↓
     Redux
       ↓
   Global State
```

Common use cases:

* Authentication state
* Shopping cart
* User profile
* Theme
* Notifications
* Application-wide data

---

# 2. What is Redux Toolkit?

Redux Toolkit (RTK) is the **official recommended way to write Redux logic**.

It simplifies Redux development by providing utilities such as:

* `configureStore`
* `createSlice`
* `createAsyncThunk`
* `createEntityAdapter`
* Immer integration

Example:

```js
import { createSlice } from "@reduxjs/toolkit";
```

### Important Interview Point

> Redux Toolkit reduces the amount of boilerplate required when working with Redux.

---

# 3. Why was Redux Toolkit introduced?

Traditional Redux often required:

* Action types
* Action creators
* Reducers
* Switch statements
* Multiple files
* Immutable update logic

Redux Toolkit simplifies this.

### Traditional Redux

```text
Action Type
    ↓
Action Creator
    ↓
Dispatch
    ↓
Reducer
    ↓
Store
```

### Redux Toolkit

```text
createSlice()
    ↓
Actions + Reducer
```

---

# 4. What are the main Redux Toolkit APIs?

Important APIs include:

```text
configureStore()
createSlice()
createAsyncThunk()
createSelector()
createEntityAdapter()
```

For fresher interviews, focus mainly on:

* `configureStore`
* `createSlice`
* `createAsyncThunk`
* `useSelector`
* `useDispatch`

---

# 5. What is the Redux Store?

The Redux store contains the application's global state.

Example:

```js
const store = configureStore({
  reducer: {
    user: userReducer,
    cart: cartReducer
  }
});
```

The store becomes the central location for Redux-managed state.

---

# 6. What is `configureStore()`?

`configureStore()` creates the Redux store with sensible defaults.

Example:

```js
import { configureStore } from "@reduxjs/toolkit";

const store = configureStore({
  reducer: {
    counter: counterReducer
  }
});
```

It also automatically configures commonly useful Redux middleware and development checks.

---

# 7. What is a slice?

A slice represents a specific section of the Redux state.

For example:

```text
Redux Store
│
├── user
├── cart
├── products
└── auth
```

Each section can have its own slice.

---

# 8. What is `createSlice()`?

`createSlice()` is used to create:

* Slice state
* Reducers
* Action creators
* Action types

Example:

```js
import { createSlice } from "@reduxjs/toolkit";

const counterSlice = createSlice({
  name: "counter",

  initialState: {
    value: 0
  },

  reducers: {
    increment: (state) => {
      state.value += 1;
    },

    decrement: (state) => {
      state.value -= 1;
    }
  }
});

export const { increment, decrement } = counterSlice.actions;

export default counterSlice.reducer;
```

---

# 9. What is an action in Redux Toolkit?

An action describes **what happened**.

Example:

```js
dispatch(increment());
```

Redux Toolkit automatically creates the action for us when using `createSlice()`.

---

# 10. What is a reducer?

A reducer determines how the state changes when an action is dispatched.

Example:

```js
reducers: {
  increment: (state) => {
    state.value += 1;
  }
}
```

The reducer receives:

```text
state
+
action
↓
new state
```

---

# 11. What is `dispatch()`?

`dispatch()` sends an action to Redux.

Example:

```js
const dispatch = useDispatch();

dispatch(increment());
```

Flow:

```text
User Action
    ↓
dispatch()
    ↓
Reducer
    ↓
State Updated
    ↓
Components Re-render
```

---

# 12. What is `useSelector()`?

`useSelector()` reads data from the Redux store.

Example:

```js
const count = useSelector(
  (state) => state.counter.value
);
```

It subscribes the component to the selected Redux state.

---

# 13. What is `useDispatch()`?

`useDispatch()` gives access to the Redux `dispatch` function.

Example:

```js
const dispatch = useDispatch();

dispatch(increment());
```

### Simple Difference

```text
useSelector()
→ Read state

useDispatch()
→ Update state / send actions
```

---

# 14. How do you connect Redux Toolkit with React?

First create the store.

Then wrap the application with `Provider`.

```jsx
import { Provider } from "react-redux";
import { store } from "./store";

<Provider store={store}>
  <App />
</Provider>
```

Now React components can access the Redux store.

---

# 15. What is Redux Provider?

`Provider` makes the Redux store available to React components.

Example:

```jsx
<Provider store={store}>
  <App />
</Provider>
```

Without `Provider`, components cannot use Redux hooks such as:

```js
useSelector();
useDispatch();
```

---

# 16. Why can Redux Toolkit appear to mutate state?

Normally Redux state should not be mutated directly.

Redux Toolkit uses **Immer internally**.

Therefore this:

```js
state.value += 1;
```

is allowed inside a Redux Toolkit reducer.

Immer internally produces the immutable state update.

### Important Point

> Redux Toolkit does not actually mutate the Redux state directly; Immer handles the immutable update process.

---

# 17. What is `createAsyncThunk()`?

`createAsyncThunk()` is used to handle asynchronous operations such as API requests.

Example:

```js
import { createAsyncThunk } from "@reduxjs/toolkit";

export const fetchUsers = createAsyncThunk(
  "users/fetchUsers",
  async () => {
    const response = await fetch("/api/users");
    return response.json();
  }
);
```

It automatically provides lifecycle states:

```text
pending
fulfilled
rejected
```

---

# 18. How do you handle API states with `createAsyncThunk()`?

Example:

```js
const usersSlice = createSlice({
  name: "users",

  initialState: {
    data: [],
    loading: false,
    error: null
  },

  reducers: {},

  extraReducers: (builder) => {
    builder
      .addCase(fetchUsers.pending, (state) => {
        state.loading = true;
      })

      .addCase(fetchUsers.fulfilled, (state, action) => {
        state.loading = false;
        state.data = action.payload;
      })

      .addCase(fetchUsers.rejected, (state) => {
        state.loading = false;
        state.error = "Failed to fetch users";
      });
  }
});
```

---

# 19. What is `extraReducers`?

`extraReducers` allows a slice to respond to actions generated outside its own `reducers` field.

It is commonly used with:

```js
createAsyncThunk()
```

Example:

```js
extraReducers: (builder) => {
  builder.addCase(fetchUsers.fulfilled, (state, action) => {
    state.data = action.payload;
  });
}
```

---

# 20. What are the three states of an async thunk?

A thunk normally has:

```text
pending
   ↓
fulfilled
```

or:

```text
pending
   ↓
rejected
```

Example:

```js
.addCase(fetchUsers.pending, ...)
.addCase(fetchUsers.fulfilled, ...)
.addCase(fetchUsers.rejected, ...)
```

These are useful for:

* Loading indicators
* API success
* Error messages

---

# 21. What is middleware in Redux?

Middleware runs between:

```text
dispatch()
   ↓
middleware
   ↓
reducer
```

Middleware can be used for:

* Async operations
* Logging
* Side effects
* API-related workflows

Redux Toolkit's store setup includes useful middleware by default.

---

# 22. What is Redux DevTools?

Redux DevTools helps developers inspect Redux state and actions.

You can inspect:

* Current state
* Dispatched actions
* State changes
* Action payloads
* State history

It is very useful for debugging Redux applications.

---

# 23. What is a payload?

A payload contains additional data associated with an action.

Example:

```js
dispatch(addTodo({
  title: "Learn Redux Toolkit"
}));
```

The reducer can access it through:

```js
action.payload
```

Example:

```js
addTodo: (state, action) => {
  state.todos.push(action.payload);
}
```

---

# 24. What is the Redux data flow?

Redux follows a predictable one-way data flow:

```text
Component
    ↓
dispatch(action)
    ↓
Reducer
    ↓
Store Updated
    ↓
useSelector()
    ↓
Component Re-renders
```

This is one of the most important Redux interview concepts.

---

# 25. Redux vs Context API

| Redux Toolkit                       | Context API                      |
| ----------------------------------- | -------------------------------- |
| Dedicated state-management solution | React built-in feature           |
| Better for complex global state     | Useful for simpler shared values |
| Powerful debugging tools            | Simpler setup                    |
| Middleware support                  | No Redux middleware system       |
| Structured architecture             | Less opinionated                 |

Examples:

### Context

```text
Theme
Language
Simple authentication context
```

### Redux

```text
Large application state
Cart
Complex user state
Multiple state interactions
```

---

# 26. Redux Toolkit vs traditional Redux

| Traditional Redux        | Redux Toolkit             |
| ------------------------ | ------------------------- |
| More boilerplate         | Less boilerplate          |
| Manual action types      | Generated action types    |
| Manual action creators   | Generated action creators |
| Manual immutable updates | Immer                     |
| More configuration       | `configureStore()`        |
| More files/code          | More concise              |

### Interview Answer

> Redux Toolkit is the modern recommended approach for writing Redux logic because it reduces boilerplate and provides useful defaults.

---

# 27. When should you use Redux Toolkit?

Redux Toolkit is useful when:

* Many components share state
* State logic is complex
* Application has multiple global state domains
* You need predictable state updates
* You need powerful debugging
* Multiple developers work on a large application

Avoid putting every piece of local state into Redux.

For example:

```js
const [isOpen, setIsOpen] = useState(false);
```

does not necessarily need Redux.

---

# 28. What should be stored in Redux?

Good candidates:

* Authentication state
* Current user
* Cart
* Global application settings
* Shared filters
* Complex application state

Usually keep local UI state local:

```text
Modal open/close
Input value
Hover state
Temporary form state
```

unless multiple parts of the application need it.

---

# 29. Redux Toolkit folder structure

A simple React project can use:

```text
src/
│
├── app/
│   └── store.js
│
├── features/
│   ├── auth/
│   │   └── authSlice.js
│   │
│   ├── cart/
│   │   └── cartSlice.js
│   │
│   └── products/
│       └── productSlice.js
│
├── components/
│
└── App.jsx
```

This feature-based structure scales well.

---

# 30. Redux Toolkit Interview Revision Checklist

* [ ] What is Redux?
* [ ] What is Redux Toolkit?
* [ ] Why use Redux Toolkit?
* [ ] `configureStore`
* [ ] `createSlice`
* [ ] Store
* [ ] State
* [ ] Actions
* [ ] Reducers
* [ ] `dispatch`
* [ ] `useSelector`
* [ ] `useDispatch`
* [ ] Provider
* [ ] Immer
* [ ] `createAsyncThunk`
* [ ] `extraReducers`
* [ ] `pending / fulfilled / rejected`
* [ ] Middleware
* [ ] Payload
* [ ] Redux DevTools
* [ ] Redux data flow
* [ ] Redux vs Context
* [ ] Redux vs traditional Redux
* [ ] When to use Redux
* [ ] What belongs in Redux

---

# Final Redux Toolkit Flow

```text
User Interaction
       ↓
dispatch(action)
       ↓
Redux Middleware
       ↓
Reducer
       ↓
Redux Store
       ↓
State Updated
       ↓
useSelector()
       ↓
React Component Re-renders
```

> **Main Interview Goal:** Be able to explain `configureStore`, `createSlice`, `useSelector`, `useDispatch`, `createAsyncThunk`, Redux data flow, and Redux vs Context clearly.
