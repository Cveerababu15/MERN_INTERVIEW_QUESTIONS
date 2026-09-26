# CSS Interview Questions & Answers

A structured collection of commonly asked **CSS interview questions** covering CSS fundamentals, selectors, box model, positioning, Flexbox, Grid, responsive design, units, specificity, pseudo-classes, pseudo-elements, animations, variables, and practical layout concepts.

This section is designed for **Frontend Developer and MERN Stack interview preparation**.

---

# Table of Contents

1. [What is CSS?](#1-what-is-css)
2. [What are the different ways to add CSS?](#2-what-are-the-different-ways-to-add-css)
3. [What is the CSS Box Model?](#3-what-is-the-css-box-model)
4. [What is the difference between margin and padding?](#4-what-is-the-difference-between-margin-and-padding)
5. [What is `box-sizing`?](#5-what-is-box-sizing)
6. [What are CSS selectors?](#6-what-are-css-selectors)
7. [What is the difference between class and ID selectors?](#7-what-is-the-difference-between-class-and-id-selectors)
8. [What is CSS specificity?](#8-what-is-css-specificity)
9. [What is the CSS cascade?](#9-what-is-the-css-cascade)
10. [What is inheritance in CSS?](#10-what-is-inheritance-in-css)
11. [What is the difference between `display: block`, `inline`, and `inline-block`?](#11-what-is-the-difference-between-display-block-inline-and-inline-block)
12. [What is `display: none` vs `visibility: hidden`?](#12-what-is-display-none-vs-visibility-hidden)
13. [What is Flexbox?](#13-what-is-flexbox)
14. [What are the main properties of Flexbox?](#14-what-are-the-main-properties-of-flexbox)
15. [What is the difference between `justify-content` and `align-items`?](#15-what-is-the-difference-between-justify-content-and-align-items)
16. [What is `flex-direction`?](#16-what-is-flex-direction)
17. [What is CSS Grid?](#17-what-is-css-grid)
18. [Flexbox vs Grid](#18-flexbox-vs-grid)
19. [What is CSS positioning?](#19-what-is-css-positioning)
20. [What is the difference between relative, absolute, fixed, and sticky positioning?](#20-what-is-the-difference-between-relative-absolute-fixed-and-sticky-positioning)
21. [What is `z-index`?](#21-what-is-z-index)
22. [What are CSS units?](#22-what-are-css-units)
23. [What is the difference between `px`, `%`, `em`, `rem`, `vw`, and `vh`?](#23-what-is-the-difference-between-px-em-rem-vw-and-vh)
24. [What are media queries?](#24-what-are-media-queries)
25. [What is responsive web design?](#25-what-is-responsive-web-design)
26. [What are pseudo-classes?](#26-what-are-pseudo-classes)
27. [What are pseudo-elements?](#27-what-are-pseudo-elements)
28. [What is the difference between `opacity: 0`, `visibility: hidden`, and `display: none`?](#28-what-is-the-difference-between-opacity-0-visibility-hidden-and-display-none)
29. [What is `overflow`?](#29-what-is-overflow)
30. [What are CSS transitions?](#30-what-are-css-transitions)
31. [What are CSS animations?](#31-what-are-css-animations)
32. [What are CSS variables?](#32-what-are-css-variables)
33. [What is the difference between `min-width`, `max-width`, `min-height`, and `max-height`?](#33-what-is-the-difference-between-min-width-max-width-min-height-and-max-height)
34. [How do you centre an element in CSS?](#34-how-do-you-centre-an-element-in-css)
35. [How do you write maintainable and scalable CSS?](#35-how-do-you-write-maintainable-and-scalable-css)

---

# 1. What is CSS?

### Answer

CSS stands for **Cascading Style Sheets**.

It is used to control the presentation and layout of HTML documents.

CSS controls:

* Colours
* Fonts
* Spacing
* Layout
* Responsive design
* Animations
* Positioning
* Visual appearance

Example:

```css
h1 {
  color: blue;
  font-size: 32px;
}
```

### Simple Relationship

```text
HTML
 ↓
Structure

CSS
 ↓
Presentation

JavaScript
 ↓
Behaviour
```

---

# 2. What are the different ways to add CSS?

There are three common ways.

## Inline CSS

```html
<p style="color: red;">
  Hello
</p>
```

## Internal CSS

```html
<style>
  p {
    color: red;
  }
</style>
```

## External CSS

```html
<link rel="stylesheet" href="style.css">
```

`style.css`:

```css
p {
  color: red;
}
```

### Best Practice

For maintainability, external stylesheets or an appropriate component styling approach are generally preferred over large amounts of inline CSS.

---

# 3. What is the CSS Box Model?

### Answer

Every element is represented as a box.

The box model consists of:

```text
┌─────────────────────────────┐
│           Margin            │
│  ┌───────────────────────┐  │
│  │        Border         │  │
│  │  ┌─────────────────┐  │  │
│  │  │     Padding     │  │  │
│  │  │  ┌───────────┐  │  │  │
│  │  │  │  Content  │  │  │  │
│  │  │  └───────────┘  │  │  │
│  │  └─────────────────┘  │  │
│  └───────────────────────┘  │
└─────────────────────────────┘
```

The four parts are:

```text
Content
Padding
Border
Margin
```

Example:

```css
.card {
  width: 300px;
  padding: 20px;
  border: 1px solid black;
  margin: 20px;
}
```

---

# 4. What is the difference between margin and padding?

### Padding

Space **inside** the element, between content and border.

```css
.card {
  padding: 20px;
}
```

### Margin

Space **outside** the element, between the element and surrounding elements.

```css
.card {
  margin: 20px;
}
```

Simple difference:

```text
Padding → inside
Margin  → outside
```

---

# 5. What is `box-sizing`?

`box-sizing` controls how an element's declared width and height are calculated.

### Default

```css
box-sizing: content-box;
```

The declared width applies to the content box.

### Border Box

```css
box-sizing: border-box;
```

The declared width includes content, padding, and border.

Common reset:

```css
* {
  box-sizing: border-box;
}
```

This makes sizing easier to reason about in many layouts.

---

# 6. What are CSS selectors?

Selectors determine which HTML elements a CSS rule applies to.

### Element selector

```css
p {
  color: red;
}
```

### Class selector

```css
.card {
  padding: 20px;
}
```

### ID selector

```css
#header {
  background: black;
}
```

### Attribute selector

```css
input[type="email"] {
  border: 1px solid gray;
}
```

### Descendant selector

```css
.card p {
  color: gray;
}
```

---

# 7. What is the difference between class and ID selectors?

### Class

```html
<div class="card"></div>
```

```css
.card {
  padding: 20px;
}
```

A class can be reused.

### ID

```html
<div id="header"></div>
```

```css
#header {
  padding: 20px;
}
```

An ID is intended to identify one unique element within the document.

### Important Point

Classes are generally preferred for reusable styling.

---

# 8. What is CSS specificity?

### Answer

Specificity determines which competing CSS declaration has higher priority when multiple rules match the same element.

A simplified ordering is:

```text
Inline styles
    ↓
ID selectors
    ↓
Class / attribute / pseudo-class selectors
    ↓
Element / pseudo-element selectors
```

Example:

```css
p {
  color: blue;
}

.text {
  color: green;
}

#message {
  color: red;
}
```

```html
<p id="message" class="text">
  Hello
</p>
```

The ID selector has higher specificity than the class and element selectors.

### Important Point

Specificity is only one part of the cascade. Origin, importance, scope, and source order also matter.

---

# 9. What is the CSS cascade?

### Answer

The **cascade** is the process the browser uses to determine which CSS declarations apply when multiple rules match an element.

The browser considers factors such as:

* Origin
* Importance
* Specificity
* Scope
* Source order

Example:

```css
p {
  color: blue;
}

p {
  color: red;
}
```

When the declarations have otherwise equal precedence, the later declaration wins.

```text
Matching Rules
     ↓
Cascade
     ↓
Applicable Declaration
     ↓
Computed Style
```

---

# 10. What is inheritance in CSS?

### Answer

Inheritance allows certain CSS properties to take their value from a parent element.

Example:

```css
body {
  color: #333;
}
```

Child text may inherit the `color` value.

Not every CSS property is inherited.

Properties commonly inherited include:

```text
color
font-family
font-size
```

Properties such as:

```text
margin
padding
border
width
```

are generally not inherited by default.

---

# 11. What is the difference between `display: block`, `inline`, and `inline-block`?

### Block

```css
display: block;
```

Generally:

* Starts on a new line
* Can have width and height
* Occupies available horizontal space by default

Examples:

```text
div
p
section
```

### Inline

```css
display: inline;
```

Generally:

* Flows within text
* Width and height do not apply in the same way as block-level boxes

Examples:

```text
span
a
strong
```

### Inline-block

```css
display: inline-block;
```

Combines inline flow with the ability to control width and height.

---

# 12. What is `display: none` vs `visibility: hidden`?

### `display: none`

The element is removed from the layout.

```css
.box {
  display: none;
}
```

### `visibility: hidden`

The element is not visible but its layout space remains.

```css
.box {
  visibility: hidden;
}
```

Simple difference:

```text
display: none
→ no layout space

visibility: hidden
→ layout space remains
```

---

# 13. What is Flexbox?

### Answer

Flexbox is a CSS layout system designed primarily for arranging elements along **one dimension**.

One dimension means:

```text
Row
OR
Column
```

Example:

```css
.container {
  display: flex;
}
```

It is commonly used for:

* Navigation bars
* Cards
* Buttons
* Aligning items
* Centering content
* Responsive layouts

---

# 14. What are the main properties of Flexbox?

Important container properties include:

```css
.container {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  gap: 20px;
}
```

Important properties:

```text
display
flex-direction
justify-content
align-items
align-content
flex-wrap
gap
```

Important item properties:

```text
flex
flex-grow
flex-shrink
flex-basis
align-self
order
```

---

# 15. What is the difference between `justify-content` and `align-items`?

The answer depends on the flex container's main axis.

For:

```css
flex-direction: row;
```

```text
justify-content → main axis → horizontal
align-items     → cross axis → vertical
```

Example:

```css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

This commonly centres items in both directions.

If the direction changes to:

```css
flex-direction: column;
```

the axes change.

### Interview Point

Do not memorise "justify = horizontal". Remember:

```text
justify-content → main axis
align-items     → cross axis
```

---

# 16. What is `flex-direction`?

`flex-direction` defines the main axis direction.

### Row

```css
.container {
  display: flex;
  flex-direction: row;
}
```

Items flow horizontally.

### Column

```css
.container {
  display: flex;
  flex-direction: column;
}
```

Items flow vertically.

Other values:

```text
row
row-reverse
column
column-reverse
```

---

# 17. What is CSS Grid?

### Answer

CSS Grid is a two-dimensional layout system.

It allows you to work with:

```text
Rows
+
Columns
```

Example:

```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}
```

This creates three equal columns.

Grid is useful for:

* Product grids
* Dashboard layouts
* Page layouts
* Complex two-dimensional designs

---

# 18. Flexbox vs Grid

### Flexbox

Best suited to one-dimensional layouts.

```text
Row
OR
Column
```

### Grid

Best suited to two-dimensional layouts.

```text
Rows
+
Columns
```

Example:

```text
Flexbox → Navbar
Grid    → Product catalog
```

This is a guideline, not a strict rule. Either system can solve many layout problems.

---

# 19. What is CSS positioning?

The `position` property controls how an element is positioned.

Common values:

```css
position: static;
position: relative;
position: absolute;
position: fixed;
position: sticky;
```

The default is:

```css
position: static;
```

---

# 20. What is the difference between relative, absolute, fixed, and sticky positioning?

### Relative

The element remains in normal flow and can be offset from its normal position.

```css
.box {
  position: relative;
  top: 10px;
}
```

It can also establish a containing block for absolutely positioned descendants.

### Absolute

The element is removed from normal flow and positioned relative to its containing block.

```css
.child {
  position: absolute;
  top: 0;
  right: 0;
}
```

### Fixed

Positioned relative to the viewport in typical cases and remains fixed while scrolling.

```css
.navbar {
  position: fixed;
  top: 0;
}
```

### Sticky

Behaves like a relatively positioned element until a scroll threshold is reached, after which it can stick within its scroll container.

```css
.header {
  position: sticky;
  top: 0;
}
```

---

# 21. What is `z-index`?

### Answer

`z-index` controls stacking order for positioned elements and other elements participating in a stacking context.

Example:

```css
.modal {
  position: fixed;
  z-index: 1000;
}
```

A higher `z-index` does not always guarantee that an element appears above everything else because **stacking contexts** can constrain how elements are painted.

---

# 22. What are CSS units?

CSS units specify dimensions.

### Absolute unit

```text
px
```

### Relative units

```text
%
em
rem
vw
vh
vmin
vmax
```

Example:

```css
.container {
  width: 80%;
  padding: 2rem;
}
```

---

# 23. What is the difference between `px`, `%`, `em`, `rem`, `vw`, and `vh`?

### `px`

A CSS pixel unit.

```css
font-size: 16px;
```

### `%`

Usually relative to another relevant dimension, depending on the property.

```css
width: 50%;
```

### `em`

Relative to the computed font size of the relevant element, with exact behaviour depending on the property.

### `rem`

Relative to the root element's font size.

```css
font-size: 1rem;
```

### `vw`

1% of the viewport width.

```css
width: 50vw;
```

### `vh`

1% of the viewport height.

```css
height: 50vh;
```

### Practical Rule

```text
rem → scalable typography/spacing
%   → relative sizing
vw  → viewport width
vh  → viewport height
px  → precise fixed-size values when appropriate
```

---

# 24. What are media queries?

### Answer

Media queries apply CSS based on conditions such as viewport width.

Example:

```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}

@media (max-width: 768px) {
  .container {
    grid-template-columns: 1fr;
  }
}
```

The layout changes when the viewport meets the specified condition.

---

# 25. What is responsive web design?

### Answer

Responsive web design means creating interfaces that adapt to different screen sizes and devices.

A responsive application considers:

```text
Mobile
Tablet
Laptop
Desktop
Large screens
```

Common techniques include:

* Flexible layouts
* Flexbox
* CSS Grid
* Relative units
* Media queries
* Responsive images
* Appropriate typography

Example:

```text
Desktop
┌──────┬──────┬──────┐
│ Card │ Card │ Card │
└──────┴──────┴──────┘

Mobile
┌──────────────┐
│     Card     │
├──────────────┤
│     Card     │
├──────────────┤
│     Card     │
└──────────────┘
```

---

# 26. What are pseudo-classes?

### Answer

Pseudo-classes select elements based on a state or condition.

Examples:

```css
button:hover {
  background: black;
}

input:focus {
  border-color: blue;
}

input:disabled {
  opacity: 0.5;
}
```

Common pseudo-classes:

```text
:hover
:focus
:active
:visited
:checked
:disabled
:first-child
:last-child
:nth-child()
:not()
```

---

# 27. What are pseudo-elements?

### Answer

Pseudo-elements allow you to style a specific part of an element or generate content associated with an element.

Common examples:

```css
.title::before {
  content: "";
}

.title::after {
  content: "";
}
```

Other examples include:

```text
::first-letter
::first-line
::placeholder
::selection
```

### Difference

```text
Pseudo-class
→ state/condition

Pseudo-element
→ part of an element
```

---

# 28. What is the difference between `opacity: 0`, `visibility: hidden`, and `display: none`?

### `display: none`

```css
display: none;
```

* Removed from layout
* Not displayed

### `visibility: hidden`

```css
visibility: hidden;
```

* Not visible
* Layout space generally remains

### `opacity: 0`

```css
opacity: 0;
```

* Element becomes visually transparent
* It generally remains in layout
* It can still receive pointer events unless those are separately disabled

Example:

```css
.hidden {
  opacity: 0;
  pointer-events: none;
}
```

### Important Point

These three properties are not interchangeable.

---

# 29. What is `overflow`?

### Answer

`overflow` controls what happens when content exceeds an element's box.

Common values:

```css
overflow: visible;
overflow: hidden;
overflow: scroll;
overflow: auto;
```

Example:

```css
.container {
  width: 300px;
  height: 200px;
  overflow: auto;
}
```

This creates scrolling when necessary.

You can also control axes separately:

```css
overflow-x: auto;
overflow-y: hidden;
```

---

# 30. What are CSS transitions?

### Answer

Transitions create smooth changes between CSS property values.

Example:

```css
.button {
  background: blue;
  transition: background 0.3s ease;
}

.button:hover {
  background: black;
}
```

Without a transition, the value changes immediately.

With a transition:

```text
Blue
 ↓
intermediate values
 ↓
Black
```

Common transition properties include:

```text
transition-property
transition-duration
transition-timing-function
transition-delay
```

---

# 31. What are CSS animations?

### Answer

CSS animations allow an element to change styles through defined keyframes.

Example:

```css
@keyframes slideIn {
  from {
    transform: translateX(-20px);
    opacity: 0;
  }

  to {
    transform: translateX(0);
    opacity: 1;
  }
}

.card {
  animation: slideIn 0.5s ease;
}
```

### Difference from Transition

```text
Transition
→ usually triggered by a property change/state

Animation
→ defined using keyframes and can run independently
```

---

# 32. What are CSS variables?

### Answer

CSS custom properties allow reusable values to be defined and referenced.

Example:

```css
:root {
  --primary-color: #2563eb;
  --spacing: 16px;
}

.button {
  background: var(--primary-color);
  padding: var(--spacing);
}
```

Benefits include:

* Reusability
* Easier theming
* Centralised design values
* Runtime modification

Example theme:

```css
:root {
  --background: white;
  --text: black;
}

.dark {
  --background: black;
  --text: white;
}
```

---

# 33. What is the difference between `min-width`, `max-width`, `min-height`, and `max-height`?

These properties define size constraints.

### `min-width`

Sets the minimum allowed width.

```css
.container {
  min-width: 300px;
}
```

### `max-width`

Sets the maximum allowed width.

```css
.container {
  max-width: 1200px;
}
```

### `min-height`

Sets the minimum height.

### `max-height`

Sets the maximum height.

A common responsive pattern is:

```css
.container {
  width: 100%;
  max-width: 1200px;
  margin-inline: auto;
}
```

---

# 34. How do you centre an element in CSS?

There are several approaches depending on the requirement.

### Flexbox

```css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

### Grid

```css
.container {
  display: grid;
  place-items: center;
}
```

### Horizontal block centering

```css
.container {
  max-width: 1200px;
  margin-inline: auto;
}
```

### Important Point

Choose the technique based on whether you need horizontal centering, vertical centering, or both.

---

# 35. How do you write maintainable and scalable CSS?

Important practices include:

### 1. Use meaningful class names

```css
.product-card {}
```

instead of:

```css
.red-box {}
```

### 2. Avoid excessive specificity

Prefer:

```css
.card {}
```

over deeply nested selectors when unnecessary.

### 3. Use reusable variables

```css
:root {
  --primary-color: #2563eb;
}
```

### 4. Use layout systems

Prefer:

```text
Flexbox
Grid
```

instead of excessive positioning hacks.

### 5. Use responsive design

Build layouts that adapt to different screen sizes.

### 6. Keep styles organised

For larger React applications, component or feature-based styling can make ownership clearer.

### 7. Avoid unnecessary `!important`

Use:

```css
!important
```

only when there is a genuine reason.

### 8. Keep accessibility in mind

Do not remove focus indicators without providing an accessible replacement.

---

# CSS Interview Revision Checklist

Before an interview, make sure you can explain:

```text
CSS Fundamentals
├── CSS
├── Ways to Add CSS
├── Box Model
├── Margin
├── Padding
├── box-sizing
├── Selectors
├── Specificity
├── Cascade
└── Inheritance

Layout
├── display
├── Block
├── Inline
├── Inline-block
├── Flexbox
├── Grid
├── Positioning
├── z-index
└── Overflow

Responsive Design
├── Media Queries
├── Responsive Design
├── %
├── rem
├── em
├── vw
├── vh
├── min-width
└── max-width

Visual Effects
├── Pseudo-classes
├── Pseudo-elements
├── Transitions
├── Animations
├── Opacity
└── CSS Variables

Practical
├── Centering
├── Flexbox alignment
├── Grid layouts
├── Responsive layouts
├── Maintainable CSS
└── Accessibility
```

---

# CSS Interview Answer Strategy

For every CSS question:

```text
Definition
    ↓
Why it is used
    ↓
Code Example
    ↓
Difference / Important Rule
    ↓
Real-world Use Case
```

Example:

```text
Question:
Flexbox vs Grid?

Flexbox:
One-dimensional layout.

Grid:
Two-dimensional layout.

Example:
Navbar → Flexbox
Product Grid → Grid

Interview Point:
Choose based on the layout requirement,
not because one is universally better.
```

---

# Final CSS Goal

You should be able to look at a UI and reason about how to build it:

```text
HTML Structure
      ↓
Box Model
      ↓
Layout
      ↓
Flexbox / Grid
      ↓
Responsive Design
      ↓
Typography & Spacing
      ↓
States & Effects
      ↓
Accessible UI
      ↓
Maintainable CSS
```

**Part of the MERN Interview Preparation Repository**
