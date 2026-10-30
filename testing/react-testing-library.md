# React Testing Library — Interview Questions & Answers

React Testing Library (RTL) is a testing library for React applications that helps developers test components from the **user's perspective**.

The main idea is:

> Test what the user sees and does, rather than testing React's internal implementation details.

---

## 1. What is React Testing Library?

React Testing Library is a library used to test React components and user interactions.

It is commonly used with:

* Jest
* Vitest
* `@testing-library/user-event`

Example:

```jsx
import { render, screen } from "@testing-library/react";
```

---

## 2. Why do we use React Testing Library?

RTL helps us verify that the application behaves correctly from a user's perspective.

For example, we can test:

* Text displayed on the screen
* Buttons
* Forms
* User interactions
* API loading states
* Error messages
* Navigation
* Component behaviour

---

## 3. What is the main principle of React Testing Library?

The main principle is:

```text
Test the application the way a user interacts with it.
```

Instead of checking internal component state:

```js
component.state
```

we test what the user can see:

```js
screen.getByText("Welcome");
```

This makes tests more realistic and maintainable.

---

## 4. What is `render()`?

`render()` renders a React component into the testing environment.

Example:

```jsx
import { render } from "@testing-library/react";

render(<Login />);
```

After rendering, we can search for elements and interact with them.

---

## 5. What is `screen`?

`screen` provides methods for finding elements rendered on the page.

Example:

```jsx
import { render, screen } from "@testing-library/react";

render(<h1>Hello Veera</h1>);

expect(screen.getByText("Hello Veera")).toBeInTheDocument();
```

Common `screen` queries include:

```text
getByRole
getByText
getByLabelText
getByPlaceholderText
getByTestId
```

---

## 6. What is `getByRole()`?

`getByRole()` finds an element based on its accessible role.

Example:

```jsx
<button>Login</button>
```

Test:

```jsx
screen.getByRole("button", {
  name: "Login",
});
```

This is one of the preferred RTL queries because it closely represents how users and assistive technologies identify elements.

---

## 7. What is `getByText()`?

`getByText()` finds an element based on visible text.

Example:

```jsx
<h1>Welcome Back</h1>
```

Test:

```js
screen.getByText("Welcome Back");
```

It is useful when the text itself is what we want to verify.

---

## 8. What is `getByLabelText()`?

`getByLabelText()` finds form controls using their associated label.

Example:

```jsx
<label htmlFor="email">Email</label>
<input id="email" />
```

Test:

```js
screen.getByLabelText("Email");
```

This is especially useful for testing forms.

---

## 9. What is the difference between `getBy`, `queryBy`, and `findBy`?

This is an important interview question.

| Query     | When to use                    |
| --------- | ------------------------------ |
| `getBy`   | Element should already exist   |
| `queryBy` | Element may not exist          |
| `findBy`  | Element appears asynchronously |

Example:

```js
screen.getByText("Login");
```

For checking that something does not exist:

```js
expect(screen.queryByText("Error")).not.toBeInTheDocument();
```

For asynchronous content:

```js
const message = await screen.findByText("Data loaded");
```

---

## 10. What happens when `getBy` cannot find an element?

`getBy` throws an error when the element cannot be found.

Example:

```js
screen.getByText("Not Found");
```

If the text does not exist, the test fails immediately.

Use `queryBy` when the element is expected **not to exist**.

---

## 11. What is `queryBy` used for?

`queryBy` returns the element if it exists and `null` if it does not.

Example:

```js
expect(
  screen.queryByText("Loading...")
).not.toBeInTheDocument();
```

It is commonly used for negative assertions.

---

## 12. What is `findBy`?

`findBy` is used when an element appears asynchronously.

Example:

```js
const user = await screen.findByText("John");
```

It is useful when:

* API data loads
* Components update asynchronously
* Loading states change
* Elements appear after user interaction

---

## 13. What is `userEvent`?

`userEvent` simulates realistic user interactions.

Example:

```js
import userEvent from "@testing-library/user-event";

const user = userEvent.setup();

await user.click(screen.getByRole("button", {
  name: "Login",
}));
```

It can simulate:

* Clicks
* Typing
* Keyboard interactions
* Selecting options
* Tab navigation

---

## 14. `fireEvent` vs `userEvent`

Both can trigger events, but `userEvent` provides more realistic user interactions.

### `fireEvent`

```js
fireEvent.click(button);
```

### `userEvent`

```js
await user.click(button);
```

For normal user interaction testing, **prefer `userEvent`**.

---

## 15. How do you test a button click?

Example component:

```jsx
function Counter() {
  const [count, setCount] = useState(0);

  return (
    <>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        Increment
      </button>
    </>
  );
}
```

Test:

```jsx
test("increments count", async () => {
  const user = userEvent.setup();

  render(<Counter />);

  await user.click(
    screen.getByRole("button", {
      name: "Increment",
    })
  );

  expect(screen.getByText("Count: 1"))
    .toBeInTheDocument();
});
```

---

## 16. How do you test a form?

Example:

```jsx
render(<LoginForm />);

const emailInput =
  screen.getByLabelText("Email");

const passwordInput =
  screen.getByLabelText("Password");

await user.type(emailInput, "user@example.com");
await user.type(passwordInput, "password123");

await user.click(
  screen.getByRole("button", {
    name: "Login",
  })
);
```

We can then verify the expected result.

---

## 17. How do you test an element that should not exist?

Use `queryBy`.

Example:

```js
expect(
  screen.queryByText("Invalid credentials")
).not.toBeInTheDocument();
```

Do not use `getBy` for this because `getBy` throws an error when the element is missing.

---

## 18. How do you test asynchronous API data?

Suppose the component initially displays:

```text
Loading...
```

and later displays:

```text
User loaded
```

Test:

```js
render(<UserProfile />);

expect(
  screen.getByText("Loading...")
).toBeInTheDocument();

expect(
  await screen.findByText("User loaded")
).toBeInTheDocument();
```

`findBy` waits for the asynchronous update.

---

## 19. How do you test an API call?

API requests are usually mocked during component tests.

The test should verify the component's behaviour without depending on a real backend.

Typical flow:

```text
Component
   ↓
API Request
   ↓
Mock Response
   ↓
Component Updates
   ↓
Assertion
```

Tools such as **Mock Service Worker (MSW)** are commonly used for realistic API mocking.

---

## 20. What is `jest-dom`?

`jest-dom` provides custom matchers for testing DOM elements.

Example:

```js
expect(element).toBeInTheDocument();
```

Other useful matchers include:

```js
toBeVisible()
toBeDisabled()
toHaveTextContent()
toHaveValue()
toHaveAttribute()
```

---

## 21. What is `data-testid`?

`data-testid` provides a custom identifier for finding an element.

Example:

```jsx
<div data-testid="profile">
  User Profile
</div>
```

Test:

```js
screen.getByTestId("profile");
```

However, it should generally **not be the first choice**.

Prefer:

```text
getByRole
getByLabelText
getByText
```

when possible.

---

## 22. What is `waitFor()`?

`waitFor()` waits until an assertion or condition becomes true.

Example:

```js
await waitFor(() => {
  expect(
    screen.getByText("Success")
  ).toBeInTheDocument();
});
```

It can be useful when the expected update does not map cleanly to a `findBy` query.

However, don't use `waitFor()` unnecessarily when `findBy` is sufficient.

---

## 23. What should we test in a React component?

A good component test should focus on behaviour.

For example, for a login component:

```text
Render form
   ↓
Enter email
   ↓
Enter password
   ↓
Click Login
   ↓
Show loading state
   ↓
Show success/error result
```

We should test the behaviour users actually experience.

---

## 24. What should we avoid testing with React Testing Library?

Avoid testing implementation details such as:

```text
Internal state
Internal component methods
React internals
Exact implementation structure
Private functions
```

Instead, test:

```text
What the user sees
What the user clicks
What the user types
What happens after an action
```

---

# React Testing Library Query Priority

A useful order to remember:

```text
1. getByRole
       ↓
2. getByLabelText
       ↓
3. getByPlaceholderText
       ↓
4. getByText
       ↓
5. getByTestId
```

Use the query that best represents how the user interacts with the application.

---

# Common RTL Imports

A typical test may use:

```jsx
import {
  render,
  screen,
  waitFor,
} from "@testing-library/react";

import userEvent from "@testing-library/user-event";

import "@testing-library/jest-dom";
```

---

# Typical React Testing Flow

```text
Arrange
   ↓
Render Component
   ↓
Find Elements
   ↓
Act
   ↓
User Interaction
   ↓
Assert
```

Example:

```text
Arrange
 ↓
render(<Login />)
 ↓
Find email/password/button
 ↓
Type credentials
 ↓
Click Login
 ↓
Check expected result
```

---

# Important Interview Concepts

Make sure you understand:

```text
React Testing Library
render()
screen
getByRole()
getByText()
getByLabelText()
getByTestId()
getBy vs queryBy vs findBy
userEvent
fireEvent
waitFor()
jest-dom
API mocking
MSW
Testing forms
Testing user interactions
Testing asynchronous UI
Testing behaviour vs implementation details
```

---

# React Testing Library Revision Checklist

* [ ] What is React Testing Library?
* [ ] Why is RTL used?
* [ ] What is `render()`?
* [ ] What is `screen`?
* [ ] What is `getByRole()`?
* [ ] What is `getByText()`?
* [ ] What is `getByLabelText()`?
* [ ] `getBy` vs `queryBy` vs `findBy`
* [ ] What is `userEvent`?
* [ ] `userEvent` vs `fireEvent`
* [ ] How to test button clicks
* [ ] How to test forms
* [ ] How to test asynchronous UI
* [ ] How to test API responses
* [ ] What is `jest-dom`?
* [ ] What is `data-testid`?
* [ ] What is `waitFor()`?
* [ ] What should and should not be tested?
* [ ] Behaviour vs implementation details
* [ ] RTL testing flow

---

# Final Interview Flow

When asked how you test a React component, explain:

```text
Render the component
       ↓
Find elements using accessible queries
       ↓
Perform realistic user interactions
       ↓
Wait for asynchronous updates when required
       ↓
Assert the expected UI behaviour
```

> **Interview Goal:** Understand how to test React applications from the user's perspective using `render`, `screen`, accessible queries, `userEvent`, asynchronous queries, and DOM assertions.
