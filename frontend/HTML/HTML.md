# HTML Interview Questions & Answers

A structured collection of commonly asked **HTML interview questions** covering HTML fundamentals, semantic HTML, forms, tables, links, media, accessibility, SEO, browser behaviour, and modern HTML concepts.

This section is designed for **Frontend Developer and MERN Stack interview preparation**.

---

# Table of Contents

1. [What is HTML?](#1-what-is-html)
2. [What is the difference between HTML and HTML5?](#2-what-is-the-difference-between-html-and-html5)
3. [What is an HTML element?](#3-what-is-an-html-element)
4. [What is the difference between an element and a tag?](#4-what-is-the-difference-between-an-element-and-a-tag)
5. [What are attributes in HTML?](#5-what-are-attributes-in-html)
6. [What is the basic structure of an HTML document?](#6-what-is-the-basic-structure-of-an-html-document)
7. [What is `<!DOCTYPE html>`?](#7-what-is-doctype-html)
8. [What is the difference between `<head>` and `<body>`?](#8-what-is-the-difference-between-head-and-body)
9. [What are block-level and inline elements?](#9-what-are-block-level-and-inline-elements)
10. [What are semantic HTML elements?](#10-what-are-semantic-html-elements)
11. [Why is semantic HTML important?](#11-why-is-semantic-html-important)
12. [What is the difference between `<div>` and `<span>`?](#12-what-is-the-difference-between-div-and-span)
13. [What is the difference between `<section>` and `<div>`?](#13-what-is-the-difference-between-section-and-div)
14. [What is the difference between `<article>` and `<section>`?](#14-what-is-the-difference-between-article-and-section)
15. [What are headings in HTML?](#15-what-are-headings-in-html)
16. [What is the difference between `<strong>` and `<b>`?](#16-what-is-the-difference-between-strong-and-b)
17. [What is the difference between `<em>` and `<i>`?](#17-what-is-the-difference-between-em-and-i)
18. [What are lists in HTML?](#18-what-are-lists-in-html)
19. [What is the difference between `<a>` and `<link>`?](#19-what-is-the-difference-between-a-and-link)
20. [What is the `alt` attribute?](#20-what-is-the-alt-attribute)
21. [What are HTML forms?](#21-what-are-html-forms)
22. [What are common HTML input types?](#22-what-are-common-html-input-types)
23. [What is the difference between `id` and `class`?](#23-what-is-the-difference-between-id-and-class)
24. [What are `name`, `value`, and `placeholder` in form inputs?](#24-what-are-name-value-and-placeholder-in-form-inputs)
25. [What is the difference between GET and POST forms?](#25-what-is-the-difference-between-get-and-post-forms)
26. [What is the purpose of the `<label>` element?](#26-what-is-the-purpose-of-the-label-element)
27. [What are tables in HTML?](#27-what-are-tables-in-html)
28. [What are `<thead>`, `<tbody>`, and `<tfoot>`?](#28-what-are-thead-tbody-and-tfoot)
29. [What is the difference between `<button>` and `<input type="button">`?](#29-what-is-the-difference-between-button-and-input-typebutton)
30. [What is the difference between `disabled` and `readonly`?](#30-what-is-the-difference-between-disabled-and-readonly)
31. [What are HTML entities?](#31-what-are-html-entities)
32. [What is an iframe?](#32-what-is-an-iframe)
33. [What is accessibility in HTML?](#33-what-is-accessibility-in-html)
34. [What is ARIA and when should it be used?](#34-what-is-aria-and-when-should-it-be-used)
35. [How does HTML help SEO?](#35-how-does-html-help-seo)

---

# 1. What is HTML?

### Answer

HTML stands for **HyperText Markup Language**.

It is the standard markup language used to structure content on web pages.

HTML defines the structure of a webpage, such as:

* Headings
* Paragraphs
* Images
* Links
* Forms
* Tables
* Lists
* Sections

Example:

```html
<h1>My Portfolio</h1>

<p>I am a Full Stack Developer.</p>

<a href="/projects">View Projects</a>
```

### Important Point

HTML provides the **structure**, CSS provides the **presentation**, and JavaScript provides **behaviour and interactivity**.

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

# 2. What is the difference between HTML and HTML5?

### Answer

HTML5 is the modern version of HTML and introduced several improvements and new capabilities.

HTML5 introduced semantic elements such as:

```html
<header>
<nav>
<main>
<section>
<article>
<aside>
<footer>
```

It also introduced native elements and APIs such as:

```html
<audio>
<video>
<canvas>
```

HTML5 also improved support for modern web applications and forms.

### Interview Point

HTML5 is not a completely different language. It is a modern specification of HTML.

---

# 3. What is an HTML element?

### Answer

An HTML element generally consists of an opening tag, content, and a closing tag.

Example:

```html
<p>Hello World</p>
```

Here:

```text
<p>          → Opening tag
Hello World  → Content
</p>         → Closing tag
```

Together they form an HTML element.

Some elements are void elements and do not have closing tags.

Example:

```html
<img src="image.jpg" alt="Profile">
```

---

# 4. What is the difference between an element and a tag?

### Tag

A tag is the markup syntax itself.

```html
<p>
```

### Element

The complete structure is an element.

```html
<p>Hello World</p>
```

Simple difference:

```text
Tag     → <p>
Element → <p>Hello World</p>
```

---

# 5. What are attributes in HTML?

### Answer

Attributes provide additional information about an HTML element.

Example:

```html
<img
  src="profile.jpg"
  alt="Profile photo"
>
```

Here:

```text
src → image source
alt → alternative text
```

Another example:

```html
<a
  href="/about"
  class="nav-link"
>
  About
</a>
```

Attributes are written inside the opening tag.

---

# 6. What is the basic structure of an HTML document?

A standard HTML document looks like:

```html
<!DOCTYPE html>

<html lang="en">
<head>
  <meta charset="UTF-8">

  <meta
    name="viewport"
    content="width=device-width, initial-scale=1.0"
  >

  <title>My Website</title>
</head>

<body>

  <h1>Hello World</h1>

</body>
</html>
```

### Structure

```text
html
├── head
│   ├── meta
│   ├── title
│   └── links/scripts
│
└── body
    └── visible page content
```

---

# 7. What is `<!DOCTYPE html>`?

### Answer

`<!DOCTYPE html>` tells the browser that the document should be interpreted using the modern HTML standard.

Example:

```html
<!DOCTYPE html>
```

It should appear at the beginning of an HTML document.

### Important Point

It is a **document type declaration**, not an HTML element.

---

# 8. What is the difference between `<head>` and `<body>`?

### `<head>`

Contains metadata and resources used by the document.

Examples:

```html
<head>
  <meta charset="UTF-8">
  <title>Portfolio</title>
  <link rel="stylesheet" href="style.css">
</head>
```

### `<body>`

Contains the page content rendered to the user.

```html
<body>
  <h1>My Portfolio</h1>
  <p>Welcome.</p>
</body>
```

---

# 9. What are block-level and inline elements?

### Block-level behaviour

Block-level elements generally start on a new line and take available horizontal space.

Examples:

```html
<div></div>
<p></p>
<section></section>
<h1></h1>
```

### Inline behaviour

Inline elements generally occupy only the space required by their content.

Examples:

```html
<span></span>
<a></a>
<strong></strong>
<em></em>
```

### Important Point

Modern CSS can change how an element is displayed, so "block" and "inline" are best understood as default display behaviour rather than permanent limitations.

---

# 10. What are semantic HTML elements?

### Answer

Semantic elements clearly describe the meaning or role of their content.

Examples:

```html
<header>
<nav>
<main>
<section>
<article>
<aside>
<footer>
```

Example:

```html
<header>
  <h1>My Blog</h1>
</header>

<main>
  <article>
    <h2>Learning React</h2>
    <p>React is a JavaScript library...</p>
  </article>
</main>

<footer>
  Copyright 2026
</footer>
```

---

# 11. Why is semantic HTML important?

Semantic HTML provides meaningful structure to a document.

Benefits include:

* Better accessibility
* Better document structure
* Easier maintenance
* Better communication of content meaning
* Helps search engines understand page structure

Instead of:

```html
<div class="header">
```

Prefer:

```html
<header>
```

when the element actually represents the page header.

---

# 12. What is the difference between `<div>` and `<span>`?

### `<div>`

A generic block-level container.

```html
<div class="card">
  <h2>Product</h2>
</div>
```

### `<span>`

A generic inline container.

```html
<p>
  Price:
  <span class="price">₹299</span>
</p>
```

Neither element has inherent semantic meaning.

Use semantic elements when one accurately describes the content.

---

# 13. What is the difference between `<section>` and `<div>`?

### `<section>`

Represents a meaningful standalone section of a document.

```html
<section>
  <h2>Our Services</h2>
  <p>We provide web development services.</p>
</section>
```

### `<div>`

A generic container without semantic meaning.

```html
<div class="container">
  ...
</div>
```

### Simple Difference

```text
section → meaningful content section
div     → generic container
```

---

# 14. What is the difference between `<article>` and `<section>`?

### `<article>`

Represents a self-contained piece of content that could potentially stand on its own.

Examples:

* Blog post
* News article
* Product review
* Forum post

```html
<article>
  <h2>React Performance</h2>
  <p>...</p>
</article>
```

### `<section>`

Groups related content within a larger document.

```html
<section>
  <h2>Latest Posts</h2>

  <article>Post 1</article>
  <article>Post 2</article>
</section>
```

---

# 15. What are headings in HTML?

HTML provides six heading levels:

```html
<h1>Heading 1</h1>
<h2>Heading 2</h2>
<h3>Heading 3</h3>
<h4>Heading 4</h4>
<h5>Heading 5</h5>
<h6>Heading 6</h6>
```

They communicate document hierarchy.

Example:

```text
h1 → Page title
  h2 → Major section
    h3 → Subsection
```

### Important Point

Do not choose heading levels only because of their default font size. Use them according to document structure and hierarchy.

---

# 16. What is the difference between `<strong>` and `<b>`?

### `<strong>`

Indicates that the content has strong importance.

```html
<p>
  <strong>Important:</strong>
  Save your changes.
</p>
```

### `<b>`

Draws attention to text without adding the semantic meaning of importance.

```html
<p>
  Search for the <b>latest version</b>.
</p>
```

### Interview Point

Use `<strong>` when the content is semantically important, not simply because you want bold styling.

---

# 17. What is the difference between `<em>` and `<i>`?

### `<em>`

Represents emphasis.

```html
<p>
  You <em>must</em> complete this step.
</p>
```

### `<i>`

Represents text set apart from normal prose for a different voice or convention, such as technical terms or foreign words, depending on context.

```html
<p>
  The term <i>frontend</i> is commonly used in web development.
</p>
```

CSS should generally be used when the requirement is purely visual styling.

---

# 18. What are lists in HTML?

HTML provides three common list types.

### Unordered List

```html
<ul>
  <li>React</li>
  <li>Node.js</li>
  <li>MongoDB</li>
</ul>
```

### Ordered List

```html
<ol>
  <li>Install Node.js</li>
  <li>Install dependencies</li>
  <li>Run the application</li>
</ol>
```

### Description List

```html
<dl>
  <dt>HTML</dt>
  <dd>Markup language for web structure.</dd>
</dl>
```

---

# 19. What is the difference between `<a>` and `<link>`?

### `<a>`

Creates a hyperlink that users can interact with.

```html
<a href="/about">
  About
</a>
```

### `<link>`

Defines a relationship between the current document and an external resource.

Common example:

```html
<link
  rel="stylesheet"
  href="style.css"
>
```

### Simple Difference

```text
<a>    → user-facing hyperlink
<link> → document resource relationship
```

---

# 20. What is the `alt` attribute?

### Answer

The `alt` attribute provides alternative text for an image.

```html
<img
  src="profile.jpg"
  alt="Profile photo of a developer"
>
```

It is important for:

* Accessibility
* Situations where an image cannot be displayed
* Providing a textual alternative for meaningful images

### Decorative Images

For purely decorative images, an empty `alt` can be appropriate:

```html
<img src="decoration.png" alt="">
```

---

# 21. What are HTML forms?

### Answer

Forms collect user input.

Example:

```html
<form>
  <label for="email">Email</label>

  <input
    id="email"
    type="email"
    name="email"
  >

  <button type="submit">
    Submit
  </button>
</form>
```

Common form elements include:

```text
input
textarea
select
option
button
label
fieldset
legend
```

---

# 22. What are common HTML input types?

Common input types include:

```html
<input type="text">
<input type="email">
<input type="password">
<input type="number">
<input type="tel">
<input type="date">
<input type="time">
<input type="checkbox">
<input type="radio">
<input type="file">
<input type="url">
<input type="search">
<input type="submit">
```

The input type provides appropriate semantics and browser behaviour.

For example:

```html
<input
  type="email"
  name="email"
>
```

allows browsers to recognise the field as an email input.

---

# 23. What is the difference between `id` and `class`?

### `id`

Identifies a particular element.

```html
<div id="navbar">
```

An `id` should be unique within the document.

### `class`

Can be shared by multiple elements.

```html
<div class="card">
<div class="card">
<div class="card">
```

### Simple Difference

```text
id    → unique identity
class → reusable grouping
```

CSS:

```css
#navbar {
  ...
}

.card {
  ...
}
```

---

# 24. What are `name`, `value`, and `placeholder` in form inputs?

Consider:

```html
<input
  type="text"
  name="username"
  value="Veera"
  placeholder="Enter username"
>
```

### `name`

Identifies the field when form data is submitted.

### `value`

Represents the current/default value of the control.

### `placeholder`

Provides a temporary hint to the user.

### Important Point

A placeholder is **not a replacement for a proper `<label>`**.

---

# 25. What is the difference between GET and POST forms?

### GET

Form data is generally encoded into the URL.

```html
<form method="GET">
```

Commonly used for:

* Search
* Filtering
* Retrieving resources

Example:

```text
/search?query=react
```

### POST

Form data is sent in the request body.

```html
<form method="POST">
```

Commonly used when submitting data that causes a server-side action.

### Important Point

POST does not automatically mean "secure". HTTPS and proper server-side validation are still required.

---

# 26. What is the purpose of the `<label>` element?

### Answer

`<label>` associates descriptive text with a form control.

Example:

```html
<label for="email">
  Email
</label>

<input
  id="email"
  type="email"
  name="email"
>
```

The `for` attribute matches the input's `id`.

This improves:

* Accessibility
* Usability
* Clickable form controls

---

# 27. What are tables in HTML?

Tables represent tabular data.

Example:

```html
<table>
  <tr>
    <th>Name</th>
    <th>Role</th>
  </tr>

  <tr>
    <td>Veera</td>
    <td>Developer</td>
  </tr>
</table>
```

Important elements:

```text
<table>
<tr>   → table row
<th>   → header cell
<td>   → data cell
```

### Important Point

Do not use HTML tables for page layout. Use CSS layout systems such as Flexbox and Grid for layout.

---

# 28. What are `<thead>`, `<tbody>`, and `<tfoot>`?

They divide a table into logical sections.

```html
<table>

  <thead>
    <tr>
      <th>Product</th>
      <th>Price</th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>Mango Powder</td>
      <td>₹299</td>
    </tr>
  </tbody>

  <tfoot>
    <tr>
      <td>Total</td>
      <td>₹299</td>
    </tr>
  </tfoot>

</table>
```

They improve the semantic organisation of tabular data.

---

# 29. What is the difference between `<button>` and `<input type="button">`?

### `<button>`

More flexible because it can contain text and, depending on the use, other phrasing content.

```html
<button type="button">
  Add to Cart
</button>
```

### `<input type="button">`

A form input control whose displayed label comes from its `value`.

```html
<input
  type="button"
  value="Add to Cart"
>
```

For most interactive UI actions, `<button>` is generally the more flexible choice.

---

# 30. What is the difference between `disabled` and `readonly`?

### `disabled`

The control is disabled.

```html
<input
  type="text"
  disabled
>
```

A disabled form control generally cannot be interacted with and is not submitted as successful form data.

### `readonly`

The user cannot edit the value, but the control can still participate in form submission.

```html
<input
  type="text"
  value="Veera"
  readonly
>
```

### Simple Difference

```text
disabled → cannot interact/edit and not submitted
readonly  → cannot edit but can remain part of submitted form data
```

---

# 31. What are HTML entities?

### Answer

HTML entities provide a way to represent special characters that have meaning in HTML or are difficult to type directly.

Examples:

```html
&lt;   → <
&gt;   → >
&amp;  → &
&nbsp; → non-breaking space
```

Example:

```html
<p>
  Use &lt;div&gt; for a generic container.
</p>
```

---

# 32. What is an iframe?

### Answer

An `<iframe>` embeds another browsing context inside the current page.

Example:

```html
<iframe
  src="https://example.com"
  title="Example website"
>
</iframe>
```

Common uses include embedding:

* Maps
* Videos
* External documents
* Third-party content

### Security Point

When embedding external content, consider restrictions such as `sandbox`, appropriate permissions, and trusted origins.

---

# 33. What is accessibility in HTML?

### Answer

Accessibility means designing web content so that people with different abilities can use it effectively.

Important HTML practices include:

* Semantic elements
* Proper headings
* Labels for form controls
* Meaningful `alt` text
* Keyboard-accessible controls
* Correct button/link usage

Example:

Prefer:

```html
<button type="button">
  Delete
</button>
```

over:

```html
<div onclick="deleteItem()">
  Delete
</div>
```

A real button provides built-in semantics and keyboard behaviour.

---

# 34. What is ARIA and when should it be used?

### Answer

ARIA stands for **Accessible Rich Internet Applications**.

ARIA attributes provide additional accessibility information when native HTML semantics are insufficient.

Example:

```html
<button
  aria-label="Close menu"
>
  ×
</button>
```

### Important Rule

Prefer native HTML semantics whenever possible.

For example:

```html
<button>Submit</button>
```

is generally preferable to creating a custom clickable `<div>` and adding ARIA to imitate a button.

ARIA should enhance semantics, not replace proper HTML unnecessarily.

---

# 35. How does HTML help SEO?

HTML provides structural information that helps search engines understand a page.

Important practices include:

### Meaningful `<title>`

```html
<title>
  React Developer Portfolio
</title>
```

### Meta description

```html
<meta
  name="description"
  content="Portfolio of a React and MERN stack developer."
>
```

### Semantic HTML

```html
<header>
<nav>
<main>
<article>
<section>
<footer>
```

### Proper headings

```html
<h1>Main Page Title</h1>
<h2>Projects</h2>
<h2>Skills</h2>
```

### Meaningful links

```html
<a href="/projects">
  View Projects
</a>
```

### Important Point

HTML contributes to SEO, but SEO also depends on many factors beyond HTML, including content quality, performance, crawlability, links, and site architecture.

---

# HTML Interview Revision Checklist

Before an interview, make sure you can explain:

```text
HTML Fundamentals
├── HTML
├── HTML5
├── Elements
├── Tags
├── Attributes
├── DOCTYPE
├── Head
└── Body

Semantic HTML
├── header
├── nav
├── main
├── section
├── article
├── aside
└── footer

Text & Structure
├── Headings
├── Paragraphs
├── Strong / Bold
├── Emphasis / Italic
├── Lists
├── Links
└── Div / Span

Forms
├── form
├── input
├── textarea
├── select
├── button
├── label
├── name
├── value
├── placeholder
├── GET / POST
└── disabled / readonly

Tables
├── table
├── tr
├── th
├── td
├── thead
├── tbody
└── tfoot

Accessibility
├── Semantic HTML
├── alt
├── label
├── Keyboard Accessibility
├── ARIA
└── Native Controls

SEO
├── title
├── meta description
├── headings
├── semantic structure
└── meaningful links
```

---

# HTML Interview Answer Strategy

For every HTML question, prepare your answer using:

```text
Definition
    ↓
Purpose
    ↓
Example
    ↓
Important Difference
    ↓
Real-world Use
```

Example:

```text
Question:
What is semantic HTML?

Definition:
Semantic HTML uses elements that describe the meaning
and role of their content.

Example:
<header>
<nav>
<main>
<article>
<footer>

Why:
Accessibility
SEO
Maintainability
Clear document structure
```

---

# Final HTML Goal

You should be able to build a properly structured page using HTML **without relying on `<div>` for everything**.

The target understanding is:

```text
Document Structure
        ↓
Semantic HTML
        ↓
Forms & Tables
        ↓
Accessibility
        ↓
SEO
        ↓
Clean HTML
        ↓
CSS
        ↓
JavaScript / React
```

**Part of the MERN Interview Preparation Repository**
