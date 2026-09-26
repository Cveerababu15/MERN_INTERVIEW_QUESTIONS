# Tailwind CSS Interview Questions

> **Level:** Fresher / Junior Developer
> **Focus:** Important Tailwind CSS concepts + commonly asked interview questions
> **Prerequisite:** HTML + CSS

---

# 1. What is Tailwind CSS?

Tailwind CSS is a **utility-first CSS framework**.

Instead of writing custom CSS for every component, you use predefined utility classes directly in your HTML or JSX.

Example:

```jsx
<button className="bg-blue-500 text-white px-4 py-2 rounded">
  Login
</button>
```

---

# 2. What does utility-first CSS mean?

Utility-first CSS means using small classes that perform individual styling tasks.

Examples:

```text
p-4       → padding
mt-2      → margin-top
text-lg    → font size
font-bold  → font weight
flex       → display flex
grid       → display grid
rounded    → border radius
```

You combine these utilities to build the UI.

---

# 3. Why use Tailwind CSS?

Advantages include:

* Fast UI development
* Consistent design
* Responsive utilities
* Easy customization
* Less custom CSS
* Good developer experience
* Easy integration with React
* Utility classes can be composed directly in components

---

# 4. Tailwind CSS vs traditional CSS

### Traditional CSS

```css
.button {
  background: blue;
  color: white;
  padding: 8px 16px;
  border-radius: 6px;
}
```

```jsx
<button className="button">
  Login
</button>
```

### Tailwind

```jsx
<button className="bg-blue-500 text-white px-4 py-2 rounded">
  Login
</button>
```

---

# 5. What are utility classes?

Utility classes represent individual CSS properties.

Example:

```jsx
<div className="p-4 mt-2 text-center font-bold">
  Hello
</div>
```

Here:

```text
p-4          → padding
mt-2         → margin-top
text-center  → text alignment
font-bold    → font weight
```

---

# 6. How do you add padding in Tailwind?

Examples:

```text
p-4   → all sides
px-4  → left + right
py-4  → top + bottom
pt-4  → top
pb-4  → bottom
pl-4  → left
pr-4  → right
```

Example:

```jsx
<div className="px-6 py-4">
  Content
</div>
```

---

# 7. How do you add margin in Tailwind?

Examples:

```text
m-4
mx-4
my-4
mt-4
mb-4
ml-4
mr-4
```

Example:

```jsx
<div className="mt-6 mb-4">
  Content
</div>
```

---

# 8. How do you use Flexbox in Tailwind?

Use:

```text
flex
```

Example:

```jsx
<div className="flex">
  <div>Item 1</div>
  <div>Item 2</div>
</div>
```

Common Flexbox utilities:

```text
flex
flex-row
flex-col
justify-center
justify-between
items-center
flex-wrap
gap-4
```

---

# 9. How do you center an element using Tailwind?

For a flex container:

```jsx
<div className="flex items-center justify-center">
  <div>Centered</div>
</div>
```

Meaning:

```text
items-center
→ cross-axis alignment

justify-center
→ main-axis alignment
```

---

# 10. How do you use CSS Grid in Tailwind?

Use:

```text
grid
```

Example:

```jsx
<div className="grid grid-cols-3 gap-4">
  <div>1</div>
  <div>2</div>
  <div>3</div>
</div>
```

---

# 11. How do you create responsive designs in Tailwind?

Tailwind provides responsive prefixes.

Common breakpoints include:

```text
sm:
md:
lg:
xl:
2xl:
```

Example:

```jsx
<div className="text-sm md:text-lg lg:text-2xl">
  Responsive Text
</div>
```

The styling changes based on the viewport size.

---

# 12. Is Tailwind mobile-first?

Yes.

Tailwind's responsive system is **mobile-first**.

Unprefixed utilities apply to the base/mobile layout.

Example:

```jsx
<div className="text-sm md:text-lg">
  Hello
</div>
```

Meaning:

```text
Mobile → text-sm
md and above → text-lg
```

---

# 13. How do you add background colours?

Example:

```jsx
<div className="bg-blue-500">
  Content
</div>
```

Other examples:

```text
bg-red-500
bg-green-500
bg-yellow-500
bg-gray-100
bg-black
bg-white
```

---

# 14. How do you change text colour?

Use:

```text
text-{colour}-{shade}
```

Example:

```jsx
<p className="text-gray-700">
  Hello
</p>
```

---

# 15. How do you control font size?

Common utilities:

```text
text-xs
text-sm
text-base
text-lg
text-xl
text-2xl
text-3xl
text-4xl
```

Example:

```jsx
<h1 className="text-3xl font-bold">
  Welcome
</h1>
```

---

# 16. How do you control font weight?

Examples:

```text
font-thin
font-normal
font-medium
font-semibold
font-bold
font-extrabold
```

Example:

```jsx
<h1 className="font-bold">
  Heading
</h1>
```

---

# 17. How do you add border and border radius?

Border:

```text
border
border-2
border-gray-300
```

Radius:

```text
rounded
rounded-md
rounded-lg
rounded-xl
rounded-full
```

Example:

```jsx
<button className="border border-gray-300 rounded-lg">
  Submit
</button>
```

---

# 18. How do you add shadows?

Examples:

```text
shadow-sm
shadow
shadow-md
shadow-lg
shadow-xl
```

Example:

```jsx
<div className="shadow-lg rounded-lg">
  Card
</div>
```

---

# 19. How do you control width and height?

Examples:

```text
w-full
w-1/2
w-screen
h-full
h-screen
```

Example:

```jsx
<div className="w-full h-screen">
  Content
</div>
```

Tailwind also supports arbitrary values when required:

```jsx
<div className="w-[350px]">
  Content
</div>
```

---

# 20. What are arbitrary values?

Arbitrary values allow you to provide a custom value directly inside brackets.

Example:

```jsx
<div className="w-[350px]">
  Content
</div>
```

Another:

```jsx
<div className="bg-[#1da1f2]">
  Content
</div>
```

### Important Point

Use arbitrary values when the required value does not fit the normal design scale. Avoid using them everywhere because they can reduce consistency.

---

# 21. How do you add hover styles?

Use the `hover:` variant.

```jsx
<button className="bg-blue-500 hover:bg-blue-700">
  Submit
</button>
```

Other variants include:

```text
focus:
active:
disabled:
visited:
```

---

# 22. How do you handle dark mode?

Tailwind supports dark mode utilities.

Example:

```jsx
<div className="bg-white text-black dark:bg-gray-900 dark:text-white">
  Content
</div>
```

The exact dark-mode configuration depends on the Tailwind version and project setup.

---

# 23. How do you hide/show elements responsively?

Example:

```jsx
<div className="hidden md:block">
  Desktop Content
</div>
```

Meaning:

```text
Mobile → hidden
md and above → block
```

Another example:

```jsx
<div className="block md:hidden">
  Mobile Content
</div>
```

---

# 24. What are Tailwind variants?

Variants apply utilities under a specific condition.

Examples:

```text
hover:
focus:
active:
disabled:
dark:
sm:
md:
lg:
```

Example:

```jsx
<button className="bg-blue-500 hover:bg-blue-700 md:px-8">
  Button
</button>
```

---

# 25. How do you add transitions?

Example:

```jsx
<button className="transition duration-300 hover:scale-105">
  Hover Me
</button>
```

Common utilities:

```text
transition
duration-300
ease-in
ease-out
delay-100
```

---

# 26. How do you add animations?

Tailwind provides animation utilities such as:

```text
animate-spin
animate-ping
animate-pulse
animate-bounce
```

Example:

```jsx
<div className="animate-spin">
  Loading
</div>
```

Custom animations can also be defined through the project's Tailwind configuration/setup.

---

# 27. How do you create a responsive card using Tailwind?

Example:

```jsx
<div className="w-full md:w-1/2 lg:w-1/3 p-4">
  <div className="rounded-lg shadow-md p-6">
    <h2 className="text-xl font-bold">
      Product
    </h2>

    <p className="text-gray-600">
      Product description
    </p>
  </div>
</div>
```

This demonstrates:

* Responsive width
* Padding
* Border radius
* Shadow
* Typography

---

# 28. What is `@apply`?

`@apply` allows Tailwind utility classes to be composed inside CSS.

Example:

```css
.btn {
  @apply px-4 py-2 rounded-lg font-semibold;
}
```

Then:

```jsx
<button className="btn">
  Submit
</button>
```

### Important Point

`@apply` can be useful for repeated patterns, but excessive abstraction can reduce one of Tailwind's main advantages: composing utilities directly where needed.

---

# 29. How do you customise Tailwind?

Tailwind can be customised through the project's configuration/theme setup depending on the Tailwind version.

Common customisation areas include:

```text
Colours
Fonts
Spacing
Breakpoints
Shadows
Border radius
Animations
```

Example concept:

```js
theme: {
  extend: {
    colors: {
      primary: "#2563eb"
    }
  }
}
```

---

# 30. What is the advantage of Tailwind's design system?

Tailwind provides a consistent set of utilities for:

* Spacing
* Colours
* Typography
* Breakpoints
* Shadows
* Borders
* Layout

Instead of inventing different values throughout the application, developers can use a consistent design scale.

---

# 31. How does Tailwind help with responsive design?

Instead of writing many media queries manually:

```css
@media (...) {
  ...
}
```

you can use responsive variants directly:

```jsx
<div className="text-sm md:text-lg lg:text-2xl">
  Responsive content
</div>
```

This makes responsive behaviour visible directly in the component.

---

# 32. Tailwind CSS vs Bootstrap

| Tailwind CSS                   | Bootstrap                          |
| ------------------------------ | ---------------------------------- |
| Utility-first                  | Component-oriented framework       |
| Highly customisable            | Comes with predefined components   |
| Build UI using utility classes | Uses ready-made components/classes |
| Less opinionated visual style  | More predefined styling            |
| Excellent for custom designs   | Fast for standard UI patterns      |

Example Tailwind:

```jsx
<button className="px-4 py-2 rounded bg-blue-500 text-white">
  Login
</button>
```

---

# 33. Tailwind CSS vs CSS Modules

| Tailwind                | CSS Modules                   |
| ----------------------- | ----------------------------- |
| Utility classes         | CSS classes                   |
| Styling directly in JSX | Styling in separate CSS files |
| Fast composition        | More traditional CSS approach |
| Design system utilities | Full CSS control              |
| Minimal custom CSS      | Custom CSS is expected        |

---

# 34. Does Tailwind replace CSS?

No.

Tailwind is built on CSS.

Understanding CSS fundamentals is still important.

You should understand:

```text
Box Model
Flexbox
Grid
Positioning
Specificity
Responsive Design
Media Queries
Pseudo-classes
```

Tailwind provides utilities that make applying these concepts faster.

---

# 35. Tailwind CSS Interview Revision Checklist

* [ ] What is Tailwind CSS?
* [ ] Utility-first CSS
* [ ] Tailwind vs traditional CSS
* [ ] Utility classes
* [ ] Padding
* [ ] Margin
* [ ] Flexbox
* [ ] Grid
* [ ] Responsive design
* [ ] Mobile-first approach
* [ ] Breakpoints
* [ ] Colours
* [ ] Typography
* [ ] Font weight
* [ ] Borders
* [ ] Border radius
* [ ] Shadows
* [ ] Width/height
* [ ] Arbitrary values
* [ ] Hover/focus/active
* [ ] Dark mode
* [ ] Responsive visibility
* [ ] Variants
* [ ] Transitions
* [ ] Animations
* [ ] `@apply`
* [ ] Customisation
* [ ] Design system
* [ ] Tailwind vs Bootstrap
* [ ] Tailwind vs CSS Modules
* [ ] Tailwind vs CSS

---

# Final Tailwind CSS Revision Flow

```text
HTML
 ↓
Tailwind Utility Classes
 ↓
Layout
 ↓
Spacing
 ↓
Typography
 ↓
Colours
 ↓
Responsive Design
 ↓
Variants
 ↓
Dark Mode
 ↓
Components
 ↓
Consistent UI
```

> **Main Interview Goal:** Be able to explain utility-first CSS, responsive/mobile-first design, Flexbox/Grid utilities, variants, dark mode, arbitrary values, `@apply`, customisation, and Tailwind vs CSS/Bootstrap.
