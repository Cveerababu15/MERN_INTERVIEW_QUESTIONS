# Zustand Interview Questions

> **Level:** Fresher / Junior Developer
> **Focus:** Important Zustand concepts + commonly asked interview questions
> **Prerequisite:** React + JavaScript

---

# 1. What is Zustand?

Zustand is a **small state management library for React**.

It provides a simple way to create and manage global state without requiring a large amount of boilerplate.

Example:

```js
import { create } from "zustand";

const useCounterStore = create((set) => ({
  count: 0,

  increment: () =>
    set((state) => ({
      count: state.count + 1
    }))
}));
```

---

# 2. Why is Zustand used?

Zustand is useful for managing shared state such as:

* Authentication
* Shopping cart
* User preferences
* Theme
* Notifications
* Global UI state

It is popular because the API is small and straightforward.

---

# 3. How do you create a Zustand store?

Use the `create()` function.

```js
import { create } from "zustand";

const useStore = create((set) => ({
  count: 0,

  increment: () => {
    set((state) => ({
      count: state.count + 1
    }));
  }
}));
```

The returned value is a React hook.

---

# 4. How do you access Zustand state?

Call the store hook inside a React component.

```jsx
function Counter() {
  const count = useStore((state) => state.count);

  return <h1>{count}</h1>;
}
```

---

# 5. How do you update Zustand state?

Use the `set` function.

```js
const useStore = create((set) => ({
  count: 0,

  increment: () =>
    set((state) => ({
      count: state.count + 1
    }))
}));
```

Then:

```jsx
const increment = useStore(
  (state) => state.increment
);

increment();
```

---

# 6. What is the `set` function?

`set` updates the Zustand store.

Example:

```js
set({
  count: 10
});
```

Or based on the previous state:

```js
set((state) => ({
  count: state.count + 1
}));
```

The second approach is useful when the new state depends on the previous state.

---

# 7. What is the `get` function?

`get` allows you to access the current Zustand state inside the store.

Example:

```js
const useStore = create((set, get) => ({
  count: 0,

  doubleCount: () => {
    const count = get().count;

    set({
      count: count * 2
    });
  }
}));
```

---

# 8. Does Zustand require a Provider?

No.

Unlike Redux, Zustand does not normally require wrapping the React application with a Provider.

Redux commonly uses:

```jsx
<Provider store={store}>
  <App />
</Provider>
```

Zustand can simply be used through its store hook:

```jsx
const count = useStore((state) => state.count);
```

---

# 9. What is a Zustand selector?

A selector chooses a specific part of the store.

```js
const count = useStore(
  (state) => state.count
);
```

Instead of reading the entire store:

```js
const store = useStore();
```

you select only what the component needs.

### Important Point

Selectors can help reduce unnecessary component re-renders.

---

# 10. Why should we use selectors?

Suppose the store contains:

```js
{
  user,
  cart,
  theme,
  notifications
}
```

A component that only needs `cart` can select:

```js
const cart = useStore(
  (state) => state.cart
);
```

This keeps the component focused on the state it actually needs.

---

# 11. Zustand vs React useState

| `useState`            | Zustand                |
| --------------------- | ---------------------- |
| Local component state | Shared/global state    |
| Built into React      | External library       |
| Simple UI state       | Cross-component state  |
| No external setup     | Requires Zustand       |
| Good for local values | Good for shared values |

Example:

```js
const [isOpen, setIsOpen] = useState(false);
```

A modal's local open/close state usually does not need Zustand.

---

# 12. Zustand vs Redux Toolkit

| Zustand                               | Redux Toolkit               |
| ------------------------------------- | --------------------------- |
| Very small API                        | Larger structured ecosystem |
| Minimal boilerplate                   | More structured             |
| No Provider required for normal usage | Provider commonly used      |
| Simple store setup                    | `configureStore` + slices   |
| Easy to start                         | More formal architecture    |
| Selectors built into usage            | `useSelector`               |
| Middleware available                  | Middleware ecosystem        |

### Interview Point

Neither should automatically be considered "better." The choice depends on application requirements and team architecture.

---

# 13. How do you create multiple state values?

```js
const useStore = create((set) => ({
  name: "Veera",
  age: 21,
  isLoggedIn: false,

  login: () =>
    set({
      isLoggedIn: true
    })
}));
```

---

# 14. How do you update an object in Zustand?

Example:

```js
const useStore = create((set) => ({
  user: {
    name: "Veera",
    age: 21
  },

  updateName: (name) =>
    set((state) => ({
      user: {
        ...state.user,
        name
      }
    }))
}));
```

The spread operator preserves the other properties.

---

# 15. How do you update an array in Zustand?

Example:

```js
const useStore = create((set) => ({
  todos: [],

  addTodo: (todo) =>
    set((state) => ({
      todos: [...state.todos, todo]
    }))
}));
```

Remove an item:

```js
removeTodo: (id) =>
  set((state) => ({
    todos: state.todos.filter(
      (todo) => todo.id !== id
    )
  }))
```

---

# 16. Can Zustand handle asynchronous operations?

Yes.

Example:

```js
const useStore = create((set) => ({
  users: [],
  loading: false,

  fetchUsers: async () => {
    set({ loading: true });

    const response = await fetch("/api/users");
    const users = await response.json();

    set({
      users,
      loading: false
    });
  }
}));
```

---

# 17. How do you handle loading and errors?

A common pattern is:

```js
const useStore = create((set) => ({
  data: [],
  loading: false,
  error: null,

  fetchData: async () => {
    try {
      set({
        loading: true,
        error: null
      });

      const response = await fetch("/api/data");

      if (!response.ok) {
        throw new Error("Request failed");
      }

      const data = await response.json();

      set({
        data,
        loading: false
      });
    } catch (error) {
      set({
        error: error.message,
        loading: false
      });
    }
  }
}));
```

---

# 18. What is Zustand middleware?

Zustand supports middleware that can extend store functionality.

Common middleware includes:

```text
persist
devtools
immer
```

---

# 19. What is `persist` middleware?

`persist` allows Zustand state to be persisted, commonly in browser storage.

Example:

```js
import { persist } from "zustand/middleware";

const useStore = create(
  persist(
    (set) => ({
      theme: "dark",

      setTheme: (theme) =>
        set({ theme })
    }),
    {
      name: "app-storage"
    }
  )
);
```

The state can survive page refreshes.

---

# 20. What is Zustand DevTools middleware?

DevTools middleware can integrate the store with Redux DevTools for debugging.

Example:

```js
import { devtools } from "zustand/middleware";

const useStore = create(
  devtools((set) => ({
    count: 0,

    increment: () =>
      set((state) => ({
        count: state.count + 1
      }))
  }))
);
```

---

# 21. What is Immer middleware in Zustand?

Immer can simplify immutable updates for complex nested state.

Conceptually:

```js
set((state) => {
  state.user.name = "Veera";
});
```

Immer handles the immutable update process.

It is particularly useful when state has deeply nested structures.

---

# 22. Can Zustand store functions?

Yes.

State and actions can be stored together.

```js
const useStore = create((set) => ({
  count: 0,

  increment: () =>
    set((state) => ({
      count: state.count + 1
    }))
}));
```

This is a common Zustand pattern.

---

# 23. Can Zustand have multiple stores?

Yes.

For example:

```text
stores/
│
├── authStore.js
├── cartStore.js
├── themeStore.js
└── productStore.js
```

You can create separate stores based on application requirements.

---

# 24. What is a good Zustand folder structure?

Example:

```text
src/
│
├── stores/
│   ├── authStore.js
│   ├── cartStore.js
│   └── productStore.js
│
├── components/
├── pages/
├── services/
└── App.jsx
```

For larger applications, stores can also be organized by feature.

---

# 25. How does Zustand trigger React re-renders?

A component subscribes to selected state through the store hook.

Example:

```js
const count = useStore(
  (state) => state.count
);
```

When the selected state changes, the component can re-render.

Using selectors helps components subscribe to only the state they need.

---

# 26. Is Zustand immutable?

Zustand supports immutable state updates.

You normally create new objects/arrays when updating state:

```js
set((state) => ({
  user: {
    ...state.user,
    name: "Veera"
  }
}));
```

Immer middleware can simplify immutable updates for complex state.

---

# 27. Does Zustand work outside React?

Zustand stores are not limited to React component rendering.

A store can expose access to its state and actions outside components as well.

Example:

```js
const currentState = useStore.getState();
```

This can be useful in certain application services or event handlers.

---

# 28. When should you use Zustand?

Good use cases:

* Authentication state
* Shopping cart
* Global UI state
* Theme
* User preferences
* Shared application state
* Small-to-medium React applications

Avoid using global state for every value.

---

# 29. What should not necessarily be stored in Zustand?

Examples:

```text
Input value used by one component
Modal state used by one component
Temporary hover state
Simple local UI state
```

These can often remain with:

```js
useState()
```

---

# 30. Zustand Interview Revision Checklist

* [ ] What is Zustand?
* [ ] Why use Zustand?
* [ ] `create()`
* [ ] `set()`
* [ ] `get()`
* [ ] Store
* [ ] Actions
* [ ] Selectors
* [ ] Provider requirement
* [ ] Zustand vs useState
* [ ] Zustand vs Redux Toolkit
* [ ] Async operations
* [ ] Loading/error handling
* [ ] Middleware
* [ ] `persist`
* [ ] `devtools`
* [ ] Immer
* [ ] Multiple stores
* [ ] Re-render behaviour
* [ ] Immutable updates
* [ ] Zustand outside React
* [ ] Folder structure
* [ ] When to use Zustand

---

# Final Zustand Flow

```text
React Component
      ↓
useStore(selector)
      ↓
Zustand Store
      ↓
Action
      ↓
set()
      ↓
State Updated
      ↓
Subscribed Components Re-render
```

> **Main Interview Goal:** Be able to explain Zustand's `create`, `set`, `get`, selectors, async actions, middleware, persistence, and Zustand vs Redux Toolkit.
