# Jest Interview Questions and Answers

## 1. What is Jest?

Jest is a JavaScript testing framework used to test JavaScript and React applications. It provides features such as test execution, assertions, mocking, code coverage, and snapshot testing.

## 2. Why do we use Jest?

Jest helps developers:

* Identify bugs early.
* Verify application behaviour.
* Automate testing.
* Test functions, components, and APIs.
* Maintain code quality during development.

## 3. What is a test case in Jest?

A test case is a block of code that verifies whether a particular functionality works as expected.

We define test cases using `test()` or `it()`.

```javascript
test("adds two numbers", () => {
  expect(2 + 3).toBe(5);
});
```

## 4. What is the difference between `test()` and `it()`?

Both functions are used to define test cases in Jest. They work identically.

```javascript
test("checks addition", () => {
  expect(2 + 3).toBe(5);
});

it("checks subtraction", () => {
  expect(5 - 3).toBe(2);
});
```

## 5. What is `describe()` in Jest?

`describe()` groups related test cases into a logical test suite.

```javascript
describe("Math operations", () => {
  test("addition", () => {
    expect(2 + 3).toBe(5);
  });

  test("subtraction", () => {
    expect(5 - 3).toBe(2);
  });
});
```

## 6. What is `expect()` in Jest?

`expect()` is used to check whether an actual value matches an expected value.

```javascript
expect(10).toBe(10);
```

It is commonly used with Jest matchers.

## 7. What are matchers in Jest?

Matchers are methods used to verify expected results.

Common matchers include:

* `toBe()` – checks primitive values using strict equality.
* `toEqual()` – checks object and array values.
* `toBeTruthy()` – checks truthy values.
* `toBeFalsy()` – checks falsy values.
* `toContain()` – checks whether an array or string contains a value.
* `toThrow()` – checks whether a function throws an error.
* `toHaveBeenCalled()` – checks whether a mock function was called.

## 8. What is the difference between `toBe()` and `toEqual()`?

* `toBe()` checks strict equality using `Object.is()`.
* `toEqual()` checks whether objects and arrays have equivalent values.

```javascript
expect(10).toBe(10);

expect({ name: "Veera" }).toEqual({ name: "Veera" });
```

## 9. What is the difference between unit testing and integration testing?

**Unit Testing:** Tests individual functions or components independently.

**Integration Testing:** Tests whether multiple components or modules work correctly together.

## 10. What is a mock function in Jest?

A mock function is a function that tracks how it is called and can simulate a function's behaviour.

We create mock functions using `jest.fn()`.

```javascript
const mockFunction = jest.fn();

mockFunction("Hello");

expect(mockFunction).toHaveBeenCalled();
```

## 11. What is `jest.fn()`?

`jest.fn()` creates a mock function that records information such as:

* Number of calls.
* Arguments passed.
* Return values.

It is useful when testing callbacks and function interactions.

## 12. What is `jest.mock()`?

`jest.mock()` is used to mock an entire module or replace its implementation during testing.

It helps test a module without depending on the actual implementation of its external dependencies.

## 13. What is the difference between `jest.fn()` and `jest.mock()`?

* `jest.fn()` creates an individual mock function.
* `jest.mock()` mocks an entire module or its exports.

## 14. What is `mockReturnValue()`?

`mockReturnValue()` specifies the value returned whenever a mock function is called.

```javascript
const mockFunction = jest.fn();

mockFunction.mockReturnValue(100);

expect(mockFunction()).toBe(100);
```

## 15. What is `mockResolvedValue()`?

`mockResolvedValue()` makes a mock function return a Promise that resolves with a specified value.

```javascript
const mockFunction = jest.fn();

mockFunction.mockResolvedValue("Success");

await expect(mockFunction()).resolves.toBe("Success");
```

## 16. What is `mockRejectedValue()`?

`mockRejectedValue()` makes a mock function return a Promise that rejects with a specified error.

```javascript
const mockFunction = jest.fn();

mockFunction.mockRejectedValue(new Error("API failed"));

await expect(mockFunction()).rejects.toThrow("API failed");
```

## 17. How do you test asynchronous functions in Jest?

Jest supports asynchronous testing using:

* `async/await`
* Promises
* `.resolves`
* `.rejects`

```javascript
test("fetches user data", async () => {
  const result = await Promise.resolve("User");

  expect(result).toBe("User");
});
```

## 18. What is the difference between `beforeEach()` and `beforeAll()`?

* `beforeEach()` runs before every test case in its scope.
* `beforeAll()` runs once before all test cases in its scope.

They are commonly used for test setup.

## 19. What is the difference between `afterEach()` and `afterAll()`?

* `afterEach()` runs after every test case.
* `afterAll()` runs once after all test cases.

They are used for cleanup activities.

## 20. What is snapshot testing in Jest?

Snapshot testing captures the output of a component or value and compares future test results against the saved snapshot.

It helps identify unexpected changes in rendered output.

## 21. What is code coverage in Jest?

Code coverage measures how much of the application code is executed during testing.

Jest can generate coverage reports using:

```bash
npx jest --coverage
```

Common coverage metrics include:

* Statements
* Branches
* Functions
* Lines

## 22. What is the difference between `clearAllMocks()`, `resetAllMocks()`, and `restoreAllMocks()`?

* `clearAllMocks()` clears mock call history and results but keeps implementations.
* `resetAllMocks()` clears call history and resets mock implementations.
* `restoreAllMocks()` restores original implementations of spies created using `jest.spyOn()` and other restorable mocks.

## 23. What is `jest.spyOn()`?

`jest.spyOn()` creates a mock around an existing object method. It allows us to track calls and optionally replace its implementation.

```javascript
const user = {
  getName: () => "Veera",
};

const spy = jest.spyOn(user, "getName");

user.getName();

expect(spy).toHaveBeenCalled();
```

## 24. What is the difference between mocking and spying?

* **Mocking:** Replaces or simulates a function or module's behaviour.
* **Spying:** Observes calls to an existing method and can optionally replace its implementation.

## 25. How do you test error handling in Jest?

We use `toThrow()` for synchronous errors and `.rejects` for asynchronous errors.

```javascript
const divide = () => {
  throw new Error("Invalid operation");
};

test("checks error handling", () => {
  expect(divide).toThrow("Invalid operation");
});
```

## 26. How do you run Jest tests?

Common commands:

```bash
npm test
npx jest
npx jest --watch
npx jest --coverage
```

These commands run tests, watch for changes, and generate coverage reports.

## 27. What is the difference between `only()` and `skip()`?

* `test.only()` runs only the specified test.
* `test.skip()` skips the specified test.

They are useful during debugging, but `only()` should not be left in committed code unintentionally.

## 28. How do you test React components using Jest?

Jest can execute tests for React components. React Testing Library is commonly used alongside Jest to render components and verify their behaviour.

Example:

```javascript
import { render, screen } from "@testing-library/react";
import Welcome from "./Welcome";

test("displays welcome message", () => {
  render(<Welcome />);

  expect(screen.getByText("Welcome")).toBeInTheDocument();
});
```

## 29. What is the difference between Jest and React Testing Library?

**Jest:**

* JavaScript testing framework.
* Runs test cases.
* Provides assertions and mocking.
* Generates coverage reports.

**React Testing Library:**

* Helps test React components.
* Renders components.
* Queries elements.
* Simulates user interactions.

They are commonly used together.

## 30. How do you mock an API call in Jest?

We can mock an API function using `jest.fn()` or mock its module using `jest.mock()`.

Example:

```javascript
const fetchUser = jest.fn().mockResolvedValue({
  id: 1,
  name: "Veera",
});

test("checks API response", async () => {
  const user = await fetchUser();

  expect(user.name).toBe("Veera");
  expect(fetchUser).toHaveBeenCalled();
});
```

---

## Important Topics to Revise Before an Interview

* Jest fundamentals and test structure.
* `describe()`, `test()`, `it()`, and `expect()`.
* Common Jest matchers.
* Mock functions and module mocking.
* `jest.fn()`, `jest.mock()`, and `jest.spyOn()`.
* Asynchronous testing.
* Setup and cleanup methods.
* Snapshot testing.
* Code coverage.
* Jest with React Testing Library.
* API mocking and error handling.

## Complete Testing Flow

1. Write the application functionality.
2. Create a test file.
3. Group related tests using `describe()`.
4. Write test cases using `test()` or `it()`.
5. Execute functionality.
6. Verify results using `expect()` and matchers.
7. Mock external dependencies when necessary.
8. Run tests and review failures.
9. Generate coverage reports when required.

**Goal:** Understand why each testing method is used and be able to write a basic test independently.
