---
title: AEM Frontend

---

Excellent! We'll now start the **Complete AEM Frontend Master Course (Beginner → Advanced)** in the same detailed style as the backend course, with explanations, code, diagrams, real-world examples, best practices, interview questions, and enterprise scenarios.

# AEM Frontend Master Course (30 Chapters)

## Module 1: Frontend Fundamentals

### Chapter 1

* ✅ HTML5 Complete

### Chapter 2

* ✅ CSS3 Complete

### Chapter 3

* ✅ Responsive Web Design

### Chapter 4

* ✅ JavaScript ES6+

### Chapter 5

* ✅ Advanced JavaScript

### Chapter 6

* ✅ TypeScript

### Chapter 7

* ✅ Node.js & npm

### Chapter 8

* ✅ Webpack & Build Tools

### Chapter 9

* ✅ SCSS (Sass)

---

## Module 2: AEM Frontend

### Chapter 10

* ✅ HTL (Sightly) Complete

### Chapter 11

* ✅ HTL Templates & Use API

### Chapter 12

* ✅ Client Libraries (ClientLibs)

### Chapter 13

* ✅ Granite UI Dialogs

### Chapter 14

* ✅ Touch UI Components

### Chapter 15

* ✅ Editable Templates

### Chapter 16

* ✅ Core Components Customization

### Chapter 17

* ✅ Style System & Policies

---

## Module 3: Modern AEM Frontend

### Chapter 18

* ✅ SPA Editor

### Chapter 19

* ✅ React + AEM

### Chapter 20

* ✅ GraphQL + React

### Chapter 21

* ✅ Frontend Build Process

### Chapter 22

* ✅ Performance Optimization

### Chapter 23

* ✅ Accessibility (WCAG)

### Chapter 24

* ✅ SEO

### Chapter 25

* ✅ Frontend Testing

---

## Module 4: Enterprise Project

### Chapter 26

* Complete Corporate Website

### Chapter 27

* Complete E-Commerce Website

### Chapter 28

* Enterprise Project Architecture

### Chapter 29

* Production Deployment

### Chapter 30

* 300+ Frontend Interview Questions

---

# Chapter 1: HTML5 Complete (Beginner → Advanced)

---

# What is HTML?

**HTML (HyperText Markup Language)** is the standard language used to create web pages.

HTML defines the **structure** of a webpage.

Think of a webpage like a house:

* HTML → Structure (walls, rooms)
* CSS → Paint and decoration
* JavaScript → Electricity and behavior

---

# How a Browser Renders HTML

```text
Browser
    │
    ▼
Reads HTML
    │
    ▼
Creates DOM
    │
    ▼
Applies CSS
    │
    ▼
Executes JavaScript
    │
    ▼
Displays Web Page
```

---

# First HTML Page

```html
<!DOCTYPE html>
<html>
<head>
    <title>My First AEM Page</title>
</head>

<body>

    <h1>Welcome to AEM</h1>

    <p>Hello World</p>

</body>
</html>
```

Output

```
Welcome to AEM

Hello World
```

---

# HTML Document Structure

```html
<!DOCTYPE html>

<html>

<head>

</head>

<body>

</body>

</html>
```

---

## 1. DOCTYPE

```html
<!DOCTYPE html>
```

Tells the browser:

> This document uses **HTML5**.

---

## 2. HTML Tag

```html
<html>

</html>
```

The root element of every HTML page.

---

## 3. Head

Contains metadata.

```html
<head>

<title>

<meta>

<link>

<script>

<style>

</head>
```

Not visible to users.

---

## 4. Body

Contains everything visible.

```html
<body>

<h1>

<p>

<img>

<button>

</body>
```

---

# Headings

```html
<h1>Main Heading</h1>

<h2>Section</h2>

<h3>Sub Section</h3>

<h4>Heading</h4>

<h5>Heading</h5>

<h6>Heading</h6>
```

Use only one `<h1>` per page for better SEO.

---

# Paragraph

```html
<p>

This is a paragraph.

</p>
```

---

# Line Break

```html
Hello

<br>

World
```

Output

```
Hello

World
```

---

# Horizontal Line

```html
<hr>
```

Creates a horizontal separator.

---

# Text Formatting

Bold

```html
<b>Adobe</b>
```

Strong

```html
<strong>Adobe</strong>
```

Italic

```html
<i>Adobe</i>
```

Emphasis

```html
<em>Adobe</em>
```

Underline

```html
<u>Adobe</u>
```

---

# Lists

### Unordered List

```html
<ul>

<li>Home</li>

<li>Products</li>

<li>Contact</li>

</ul>
```

Output

* Home
* Products
* Contact

---

### Ordered List

```html
<ol>

<li>HTML</li>

<li>CSS</li>

<li>JavaScript</li>

</ol>
```

Output

1. HTML
2. CSS
3. JavaScript

---

# Links

```html
<a href="https://www.adobe.com">

Adobe

</a>
```

Open in new tab

```html
<a href="https://www.adobe.com"

target="_blank">

Adobe

</a>
```

---

# Images

```html
<img

src="logo.png"

alt="Company Logo"

width="300">
```

The `alt` attribute is important for accessibility and SEO.

---

# Tables

```html
<table border="1">

<tr>

<th>Name</th>

<th>Role</th>

</tr>

<tr>

<td>Vijay</td>

<td>AEM Developer</td>

</tr>

</table>
```

---

# Forms

```html
<form>

<label>Name</label>

<input type="text">

<input type="email">

<input type="password">

<button>

Submit

</button>

</form>
```

---

# Semantic HTML ⭐⭐⭐⭐⭐

Instead of:

```html
<div>

Header

</div>
```

Use:

```html
<header>

</header>
```

---

Common Semantic Tags

```html
<header>

<nav>

<main>

<section>

<article>

<aside>

<footer>
```

Benefits:

* Better SEO
* Better Accessibility
* Easier Maintenance

---

# HTML5 Layout

```html
<header>

</header>

<nav>

</nav>

<main>

<section>

</section>

<article>

</article>

</main>

<footer>

</footer>
```

---

# HTML for AEM

Typical AEM component:

```html
<div class="product">

<h2>Product Name</h2>

<p>Price</p>

<button>

Buy Now

</button>

</div>
```

Later, HTL will replace static text:

```html
<h2>${properties.title}</h2>

<p>${properties.price}</p>
```

---

# HTML Best Practices

✅ Use semantic HTML.

✅ Add `alt` text to images.

✅ Use one `<h1>`.

✅ Use labels for form fields.

✅ Keep HTML clean and properly indented.

---

# Common HTML Mistakes

❌ Using tables for page layout.

❌ Missing `alt` attributes.

❌ Multiple `<h1>` tags.

❌ Excessive nesting of `<div>` elements.

❌ Inline styles instead of CSS.

---

# Interview Questions

### 1. What is HTML?

HTML is the standard markup language used to structure web pages.

---

### 2. What is HTML5?

The latest version of HTML, introducing semantic elements, multimedia support, and modern web APIs.

---

### 3. What is Semantic HTML?

Semantic HTML uses meaningful elements such as `<header>`, `<nav>`, `<main>`, `<section>`, and `<footer>` to describe the structure of a page.

---

### 4. Why is the `alt` attribute important?

It improves accessibility for screen readers and provides alternative text if an image cannot be displayed.

---

### 5. What is the difference between `<b>` and `<strong>`?

* `<b>` makes text bold for presentation.
* `<strong>` indicates strong importance and has semantic meaning.

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"Why is Semantic HTML important in AEM?"**

A strong answer is:

* It improves SEO because search engines better understand page structure.
* It improves accessibility for assistive technologies.
* It makes HTL templates cleaner and easier to maintain.
* Adobe Core Components are built using semantic HTML, so following the same approach keeps custom components consistent with Adobe best practices.

---

# Next Chapter: CSS3 Complete (Beginner → Advanced)

We'll cover:

* CSS Selectors
* Box Model
* Display
* Position
* Flexbox
* CSS Grid
* Media Queries
* Animations
* Transitions
* Variables
* SCSS Basics
* Real AEM Component Styling
* Responsive Layouts
* Enterprise Best Practices
* Interview Questions

This will give you the CSS knowledge needed to build and customize modern AEM components.
Excellent! Let's continue with the **AEM Frontend Master Course**.

# Chapter 2: CSS3 Complete (Beginner → Advanced) ⭐⭐⭐⭐⭐

CSS (Cascading Style Sheets) is used to style HTML elements. In AEM, CSS is usually delivered through **Client Libraries (ClientLibs)**.

---

# What is CSS?

CSS controls:

* Colors
* Fonts
* Layout
* Spacing
* Animations
* Responsive Design

Without CSS:

```text
HTML

↓

Plain Web Page
```

With CSS:

```text
HTML

↓

CSS

↓

Beautiful Responsive Website
```

---

# Ways to Add CSS

## 1. Inline CSS

```html
<h1 style="color:red;">Welcome to AEM</h1>
```

❌ Not recommended.

---

## 2. Internal CSS

```html
<style>
h1{
    color:blue;
}
</style>
```

Used for small examples.

---

## 3. External CSS ⭐⭐⭐⭐⭐

```html
<link rel="stylesheet" href="styles.css">
```

This is the approach used in AEM through ClientLibs.

---

# CSS Syntax

```css
selector{

    property:value;

}
```

Example

```css
h1{

    color:blue;

}
```

---

# CSS Selectors

## Element Selector

```css
h1{

color:red;

}
```

---

## Class Selector ⭐⭐⭐⭐⭐

HTML

```html
<div class="product">

Laptop

</div>
```

CSS

```css
.product{

color:blue;

}
```

---

## ID Selector

HTML

```html
<div id="header">

</div>
```

CSS

```css
#header{

background:black;

}
```

---

## Universal Selector

```css
*{

margin:0;

padding:0;

}
```

Useful for CSS reset.

---

## Attribute Selector

```css
input[type="text"]{

border:1px solid gray;

}
```

---

# CSS Colors

```css
color:red;

color:#FF0000;

color:rgb(255,0,0);

color:rgba(255,0,0,0.5);
```

---

# Background

```css
body{

background:#f5f5f5;

}
```

Background Image

```css
.hero{

background-image:url(hero.jpg);

}
```

---

# Fonts

```css
body{

font-family:Arial,sans-serif;

font-size:16px;

font-weight:bold;

}
```

---

# Text Properties

```css
text-align:center;

text-transform:uppercase;

text-decoration:none;

line-height:1.6;
```

---

# Box Model ⭐⭐⭐⭐⭐

Every HTML element is a box.

```text
+----------------------+
|      Margin          |
| +------------------+ |
| |    Border        | |
| | +--------------+ | |
| | |  Padding     | | |
| | | +----------+ | | |
| | | | Content  | | | |
| | | +----------+ | | |
| | +--------------+ | |
| +------------------+ |
+----------------------+
```

Example

```css
.card{

padding:20px;

border:1px solid gray;

margin:30px;

}
```

---

# Width & Height

```css
.card{

width:300px;

height:200px;

}
```

---

# Display Property

```css
display:block;

display:inline;

display:inline-block;

display:flex;

display:grid;
```

---

# Position

```css
position:static;

position:relative;

position:absolute;

position:fixed;

position:sticky;
```

Example

```css
.header{

position:fixed;

top:0;

}
```

---

# Flexbox ⭐⭐⭐⭐⭐

HTML

```html
<div class="container">

<div>One</div>

<div>Two</div>

<div>Three</div>

</div>
```

CSS

```css
.container{

display:flex;

justify-content:space-between;

align-items:center;

}
```

Output

```text
One      Two      Three
```

---

# CSS Grid ⭐⭐⭐⭐⭐

```css
.container{

display:grid;

grid-template-columns:

1fr 1fr 1fr;

gap:20px;

}
```

Perfect for product listings.

---

# Media Queries (Responsive Design)

```css
@media(max-width:768px){

.container{

display:block;

}

}
```

This adjusts the layout for tablets and mobile devices.

---

# Pseudo Classes

```css
button:hover{

background:blue;

}

input:focus{

border:2px solid blue;

}

li:first-child{

font-weight:bold;

}
```

---

# Transitions

```css
.button{

transition:0.3s;

}

.button:hover{

background:red;

}
```

Creates smooth hover effects.

---

# Animations

```css
@keyframes fade{

from{

opacity:0;

}

to{

opacity:1;

}

}

.box{

animation:fade 2s;

}
```

---

# CSS Variables

```css
:root{

--primary:#0055ff;

}

.button{

background:var(--primary);

}
```

Useful for consistent theming.

---

# Example: Product Card

HTML

```html
<div class="card">

<h2>Laptop</h2>

<p>₹65,000</p>

<button>Buy Now</button>

</div>
```

CSS

```css
.card{

border:1px solid #ddd;

padding:20px;

border-radius:8px;

box-shadow:0 2px 6px rgba(0,0,0,0.2);

}

.card button{

background:#0070f3;

color:white;

padding:10px;

border:none;

cursor:pointer;

}
```

---

# CSS in AEM

Project Structure

```text
ui.frontend

↓

src

↓

main

↓

scss

↓

site.scss
```

After build:

```text
ClientLib

↓

CSS

↓

AEM Page
```

---

# Best Practices

✅ Use external CSS (ClientLibs).

✅ Prefer Flexbox and Grid for layouts.

✅ Use CSS variables for colors and spacing.

✅ Keep CSS modular and organized.

✅ Follow responsive design principles.

---

# Common Mistakes

❌ Using inline CSS.

❌ Hardcoding widths everywhere.

❌ Ignoring mobile responsiveness.

❌ Deeply nested selectors.

❌ Overusing `!important`.

---

# Interview Questions

### 1. What is the CSS Box Model?

The Box Model consists of **Content → Padding → Border → Margin** and defines how element size and spacing are calculated.

---

### 2. Difference between `display:none` and `visibility:hidden`?

* `display:none` removes the element from the layout.
* `visibility:hidden` hides the element but still reserves its space.

---

### 3. Difference between Flexbox and Grid?

* **Flexbox** is best for one-dimensional layouts (row or column).
* **Grid** is best for two-dimensional layouts (rows and columns).

---

### 4. What are Media Queries?

Media Queries apply different CSS rules based on screen size or device characteristics, enabling responsive design.

---

### 5. Why are ClientLibs used in AEM?

ClientLibs manage and optimize CSS and JavaScript by grouping, minifying, caching, and controlling dependencies across AEM pages.

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"How do you make an AEM component responsive?"**

A strong answer is:

1. Build semantic HTML.
2. Use **Flexbox** or **CSS Grid** for layout.
3. Add **Media Queries** for mobile, tablet, and desktop breakpoints.
4. Deliver styles through **AEM ClientLibs**.
5. Test responsiveness across different screen sizes and browsers.

This demonstrates practical frontend knowledge aligned with modern AEM development.

---

# Next Chapter: JavaScript ES6+ (Complete)

We'll cover:

* Variables (`var`, `let`, `const`)
* Functions
* Arrow Functions
* Objects & Arrays
* DOM Manipulation
* Events
* Promises
* Async/Await
* Fetch API
* Modules
* Complete examples
* AEM JavaScript integration
* Interview questions

JavaScript is essential for building interactive AEM components such as navigation menus, carousels, forms, dialogs, and SPA integrations.
Excellent! Now we'll learn **JavaScript ES6+**, which is the **most important frontend programming language** for AEM. Every interactive AEM component (Navigation, Carousel, Search, Forms, Dialogs, etc.) uses JavaScript.

---

# Chapter 3: JavaScript ES6+ (Beginner → Advanced) ⭐⭐⭐⭐⭐

---

# What is JavaScript?

JavaScript is a programming language that makes web pages interactive.

Without JavaScript:

```text
HTML

↓

Static Page
```

With JavaScript:

```text
HTML

↓

JavaScript

↓

Interactive Website
```

Examples:

* Image Slider
* Navigation Menu
* Search
* Login Form
* Validation
* AJAX Calls
* Dynamic Content

---

# JavaScript in AEM

```text
Browser

↓

HTL Page

↓

ClientLib JavaScript

↓

User Interaction

↓

Servlet / GraphQL

↓

JSON

↓

Update UI
```

---

# Ways to Add JavaScript

### Inline

```html
<button onclick="alert('Hello')">
Click
</button>
```

❌ Not recommended.

---

### Internal

```html
<script>

console.log("Hello");

</script>
```

---

### External ⭐⭐⭐⭐⭐

```html
<script src="script.js"></script>
```

Used in AEM through **Client Libraries (ClientLibs)**.

---

# Variables

## var

```javascript
var name = "Adobe";
```

Problems:

* Function scope
* Can be redeclared

---

## let ⭐⭐⭐⭐⭐

```javascript
let age = 25;
```

* Block scope
* Can be updated
* Cannot be redeclared in the same scope

---

## const ⭐⭐⭐⭐⭐

```javascript
const company = "Adobe";
```

Cannot be reassigned.

---

# Difference

```javascript
let price = 100;
price = 200;

const tax = 18;

// tax = 20 ❌ Error
```

---

# Data Types

```javascript
let name = "Vijay";      // String
let age = 25;            // Number
let active = true;       // Boolean
let city = null;         // Null
let salary;              // Undefined
```

---

# Operators

```javascript
let total = 10 + 20;

let sub = 20 - 5;

let mul = 5 * 6;

let div = 10 / 2;
```

---

# Comparison

```javascript
10 == "10"     // true

10 === "10"    // false
```

Always prefer:

```javascript
===
```

---

# If Else

```javascript
let age = 20;

if(age >= 18){

    console.log("Adult");

}else{

    console.log("Minor");

}
```

---

# Switch

```javascript
let day = 1;

switch(day){

case 1:

console.log("Monday");

break;

default:

console.log("Unknown");

}
```

---

# Loops

### For Loop

```javascript
for(let i=1;i<=5;i++){

console.log(i);

}
```

---

### For Of

```javascript
const products = ["Laptop","Phone","TV"];

for(const product of products){

console.log(product);

}
```

---

### forEach()

```javascript
products.forEach(product=>{

console.log(product);

});
```

---

# Functions

Traditional

```javascript
function add(a,b){

return a+b;

}

console.log(add(10,20));
```

---

# Arrow Function ⭐⭐⭐⭐⭐

```javascript
const add=(a,b)=>{

return a+b;

};
```

Short Version

```javascript
const add=(a,b)=>a+b;
```

---

# Objects

```javascript
const product={

name:"Laptop",

price:65000,

brand:"Dell"

};

console.log(product.name);
```

Output

```text
Laptop
```

---

# Arrays

```javascript
const products=[

"Laptop",

"Phone",

"TV"

];
```

Access

```javascript
console.log(products[0]);
```

---

# Array Methods ⭐⭐⭐⭐⭐

### map()

```javascript
const prices=[100,200,300];

const updated=prices.map(price=>price+10);

console.log(updated);
```

Output

```text
110

210

310
```

---

### filter()

```javascript
const prices=[100,500,1000];

const result=prices.filter(price=>price>200);

console.log(result);
```

Output

```text
500

1000
```

---

### find()

```javascript
const products=[

{name:"Laptop"},

{name:"Phone"}

];

const item=products.find(

p=>p.name==="Phone"

);

console.log(item);
```

---

# DOM Manipulation ⭐⭐⭐⭐⭐

HTML

```html
<h1 id="title">

Welcome

</h1>
```

JavaScript

```javascript
document
.getElementById("title")
.innerHTML="Hello AEM";
```

Output

```text
Hello AEM
```

---

# Events

Button

```html
<button id="save">

Save

</button>
```

JavaScript

```javascript
document
.getElementById("save")
.addEventListener(

"click",

()=>{

alert("Saved");

}

);
```

---

# Promises ⭐⭐⭐⭐⭐

```javascript
const promise=new Promise(

(resolve,reject)=>{

resolve("Success");

}

);

promise.then(

data=>console.log(data)

);
```

---

# Async Await ⭐⭐⭐⭐⭐

```javascript
async function load(){

const response=

await fetch("/api/products");

const data=

await response.json();

console.log(data);

}
```

Cleaner than promise chaining.

---

# Fetch API

```javascript
fetch("/bin/products")

.then(response=>response.json())

.then(data=>{

console.log(data);

});
```

---

# Modules

Export

```javascript
export function add(){

}
```

Import

```javascript
import {add}

from "./util.js";
```

---

# JavaScript in AEM

Project

```text
ui.frontend

↓

src

↓

main

↓

js

↓

site.js
```

Build

↓

ClientLib

↓

AEM

---

# Real AEM Example

Button

```html
<button class="buy">

Buy Now

</button>
```

JavaScript

```javascript
document
.querySelector(".buy")
.addEventListener(

"click",

()=>{

alert("Product Added");

}

);
```

---

# AJAX to Servlet

```javascript
fetch("/bin/products")

.then(response=>response.json())

.then(products=>{

console.log(products);

});
```

Flow

```text
Browser

↓

JavaScript

↓

Servlet

↓

JSON

↓

Browser
```

---

# Best Practices

✅ Use `const` by default.

✅ Use `let` only when values change.

✅ Prefer arrow functions.

✅ Use `===` instead of `==`.

✅ Use `async/await` for asynchronous operations.

✅ Keep DOM manipulation efficient.

---

# Common Mistakes

❌ Using `var` everywhere.

❌ Modifying the DOM repeatedly inside loops.

❌ Ignoring error handling in `fetch()`.

❌ Using global variables unnecessarily.

---

# Interview Questions

### 1. Difference between `var`, `let`, and `const`?

* `var` → Function scope, can be redeclared.
* `let` → Block scope, can be reassigned.
* `const` → Block scope, cannot be reassigned.

---

### 2. Difference between `==` and `===`?

* `==` compares values after type coercion.
* `===` compares both value and type (recommended).

---

### 3. What is an Arrow Function?

A shorter syntax for writing functions introduced in ES6. It also has different `this` binding behavior compared to traditional functions.

---

### 4. What is a Promise?

A JavaScript object representing the eventual completion or failure of an asynchronous operation.

---

### 5. Why use `async/await`?

It makes asynchronous code easier to read and maintain compared to chaining `.then()` calls.

---

### 6. How does JavaScript communicate with an AEM Servlet?

Typically by using the **Fetch API**:

```javascript
fetch("/bin/products")
  .then(response => response.json())
  .then(data => console.log(data));
```

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"How do you load data dynamically in an AEM component?"**

A strong answer is:

1. Create an AEM Servlet (or GraphQL endpoint) that returns JSON.
2. Include JavaScript through an AEM Client Library.
3. Use the Fetch API with `async/await` to retrieve the data.
4. Update the DOM with the returned data.
5. Handle loading states and errors gracefully.

This is the standard pattern used in modern AEM applications.

---

# Next Chapter: **Advanced JavaScript (ES6+ Deep Dive)** ⭐⭐⭐⭐⭐

We'll cover:

* Closures
* Hoisting
* Scope
* Event Loop
* Call Stack
* Callback Queue
* Microtasks
* `this` keyword
* `call()`, `apply()`, `bind()`
* Prototype & Inheritance
* Classes
* Debouncing & Throttling
* Memory Leaks
* Complete interview questions

These are some of the **most frequently asked JavaScript interview topics** for AEM Frontend and Full Stack developers.
Excellent! Now we'll learn **Advanced JavaScript (ES6+ Deep Dive)**. This is one of the **most important interview topics** for AEM Frontend, React, and Full Stack Developer interviews.

---

# Chapter 4: Advanced JavaScript (ES6+ Deep Dive) ⭐⭐⭐⭐⭐

---

# Why Learn Advanced JavaScript?

Almost every frontend interview asks about:

* Closures
* Hoisting
* Scope
* Event Loop
* Promises
* Async/Await
* `this`
* Callbacks
* Prototype
* Classes
* Memory Management

These concepts are also important when writing JavaScript for AEM components.

---

# JavaScript Execution Model

When JavaScript runs:

```text
JavaScript Engine
        │
        ▼
Memory Creation Phase
        │
        ▼
Execution Phase
        │
        ▼
Output
```

JavaScript is **single-threaded**, meaning it executes one operation at a time.

---

# Execution Context ⭐⭐⭐⭐⭐

Every JavaScript program creates an **Execution Context**.

It contains:

* Variables
* Functions
* `this`

Example:

```javascript
let name = "Vijay";

function greet() {
    console.log("Hello");
}

greet();
```

Execution Flow:

```text
Global Execution Context

↓

Variable

↓

Function

↓

Function Execution Context

↓

Output
```

---

# Hoisting ⭐⭐⭐⭐⭐

## What is Hoisting?

JavaScript moves **declarations** to the top of their scope before execution.

Example:

```javascript
console.log(name);

var name = "Adobe";
```

Output:

```text
undefined
```

JavaScript interprets it like:

```javascript
var name;

console.log(name);

name = "Adobe";
```

---

## Hoisting with let

```javascript
console.log(age);

let age = 25;
```

Output:

```text
ReferenceError
```

`let` and `const` are hoisted but remain in the **Temporal Dead Zone (TDZ)** until initialized.

---

# Scope ⭐⭐⭐⭐⭐

## Global Scope

```javascript
let company = "Adobe";
```

Accessible everywhere in the script.

---

## Function Scope

```javascript
function test() {

    let name = "Vijay";

}
```

Only accessible inside the function.

---

## Block Scope

```javascript
if(true){

    let city = "Hyderabad";

}
```

`city` cannot be accessed outside the block.

---

# Closures ⭐⭐⭐⭐⭐

A closure is created when an inner function remembers variables from its outer function even after the outer function has finished executing.

Example:

```javascript
function outer(){

    let count = 0;

    return function(){

        count++;

        console.log(count);

    }

}

const counter = outer();

counter();

counter();

counter();
```

Output:

```text
1

2

3
```

### Real AEM Example

Closures are useful for:

* Maintaining component state.
* Event handlers.
* Private variables.

---

# this Keyword ⭐⭐⭐⭐⭐

Example:

```javascript
const user = {

    name: "Vijay",

    greet() {

        console.log(this.name);

    }

};

user.greet();
```

Output:

```text
Vijay
```

`this` refers to the object calling the function.

---

# Arrow Function and this

```javascript
const obj = {

    value: 10,

    show: () => {

        console.log(this.value);

    }

};
```

Arrow functions **do not create their own `this`**. They inherit it from the surrounding scope.

---

# call(), apply(), bind()

```javascript
function greet(city){

    console.log(this.name, city);

}

const user = {

    name: "Vijay"

};

greet.call(user, "Hyderabad");
```

Output:

```text
Vijay Hyderabad
```

### Differences

| Method  | Arguments          | Executes Immediately        |
| ------- | ------------------ | --------------------------- |
| call()  | Separate arguments | Yes                         |
| apply() | Array of arguments | Yes                         |
| bind()  | Separate arguments | No (returns a new function) |

---

# Callback Function

```javascript
function process(callback){

    callback();

}

process(function(){

    console.log("Done");

});
```

Callbacks are functions passed to other functions.

---

# Promise ⭐⭐⭐⭐⭐

```javascript
const promise = new Promise((resolve, reject) => {

    resolve("Success");

});

promise.then(result => {

    console.log(result);

});
```

Output:

```text
Success
```

---

# Promise States

```text
Pending

↓

Resolved

OR

Rejected
```

---

# Async/Await ⭐⭐⭐⭐⭐

```javascript
async function loadProducts(){

    try{

        const response = await fetch("/bin/products");

        const data = await response.json();

        console.log(data);

    }catch(error){

        console.error(error);

    }

}
```

This is the recommended way to work with asynchronous operations.

---

# Event Loop ⭐⭐⭐⭐⭐

JavaScript execution:

```text
Call Stack
     │
     ▼
Web APIs
     │
     ▼
Callback Queue
     │
     ▼
Event Loop
     │
     ▼
Call Stack
```

### Example

```javascript
console.log("A");

setTimeout(() => {

    console.log("B");

}, 0);

console.log("C");
```

Output:

```text
A

C

B
```

Because `setTimeout` is asynchronous.

---

# Prototype

Every JavaScript object has a prototype.

```javascript
function Person(name){

    this.name = name;

}

Person.prototype.sayHello = function(){

    console.log("Hello");

};

const p = new Person("Vijay");

p.sayHello();
```

---

# Classes (ES6)

```javascript
class Product{

    constructor(name, price){

        this.name = name;

        this.price = price;

    }

    display(){

        console.log(this.name, this.price);

    }

}

const product = new Product("Laptop", 65000);

product.display();
```

---

# Debouncing ⭐⭐⭐⭐⭐

Used for search boxes.

```javascript
function debounce(fn, delay){

    let timer;

    return function(){

        clearTimeout(timer);

        timer = setTimeout(fn, delay);

    };

}
```

### Use Case

User types:

```text
A

AE

AEM
```

Only the last request is processed after the user stops typing.

---

# Throttling

Limits how often a function can run.

Common use cases:

* Scroll events
* Resize events
* Mouse movement

---

# Memory Leaks

Avoid:

```javascript
let data = [];

setInterval(() => {

    data.push(new Array(1000));

}, 100);
```

This keeps growing memory usage.

Always:

* Remove unused event listeners.
* Clear intervals.
* Release references.

---

# JavaScript in AEM

Example:

```javascript
document.querySelector(".search")
.addEventListener("input", debounce(async () => {

    const response = await fetch("/bin/search");

    const data = await response.json();

    console.log(data);

}, 300));
```

This creates an efficient live search component.

---

# Best Practices

✅ Use `const` by default.

✅ Use `let` when reassignment is needed.

✅ Prefer `async/await`.

✅ Handle errors with `try...catch`.

✅ Use debouncing for search.

✅ Remove event listeners when no longer needed.

---

# Common Mistakes

❌ Using `var`.

❌ Ignoring Promise rejections.

❌ Creating memory leaks.

❌ Misunderstanding `this`.

❌ Making repeated API calls without debouncing.

---

# Interview Questions

### 1. What is Hoisting?

Hoisting is JavaScript's behavior of moving declarations to the top of their scope before execution.

---

### 2. What is a Closure?

A closure is a function that remembers variables from its outer lexical scope even after the outer function has finished executing.

---

### 3. What is the Event Loop?

The Event Loop coordinates the Call Stack, Web APIs, and Callback Queue to handle asynchronous JavaScript operations.

---

### 4. Difference between `call()`, `apply()`, and `bind()`?

* `call()` invokes the function immediately with individual arguments.
* `apply()` invokes the function immediately with an array of arguments.
* `bind()` returns a new function with a bound `this` value.

---

### 5. What is Debouncing?

Debouncing delays function execution until a specified period has passed since the last invocation, commonly used for search inputs.

---

### 6. What is Throttling?

Throttling limits how often a function can execute within a given time interval, useful for scroll and resize events.

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"How would you optimize a search component in AEM?"**

A strong answer is:

1. Use JavaScript **debouncing** to avoid sending a request on every keystroke.
2. Use the **Fetch API** with `async/await` to call an AEM Servlet or GraphQL endpoint.
3. Cache results where appropriate.
4. Handle errors gracefully.
5. Update the DOM efficiently without unnecessary re-renders.

This demonstrates both JavaScript expertise and practical AEM frontend knowledge.

---

# Next Chapter: **TypeScript (Complete)** ⭐⭐⭐⭐⭐

We'll cover:

* What TypeScript is.
* Type annotations.
* Interfaces.
* Classes.
* Generics.
* Enums.
* Modules.
* Type narrowing.
* Optional chaining.
* TypeScript in AEM and React.
* Enterprise examples.
* Interview questions.

TypeScript is widely used in **React-based AEM projects** and modern frontend development because it provides static type checking and improves maintainability.
Excellent! Now we'll learn **TypeScript**, which is used in **React**, **Angular**, and many **modern AEM frontend projects**. If you're working with the **AEM SPA Editor** or a React frontend, TypeScript is a valuable skill.

---

# Chapter 5: TypeScript (Beginner → Advanced) ⭐⭐⭐⭐⭐

---

# What is TypeScript?

**TypeScript** is a programming language developed by Microsoft that builds on JavaScript by adding **static typing**.

TypeScript code is transpiled into plain JavaScript before it runs in the browser.

```text
TypeScript (.ts)

        ↓

TypeScript Compiler (tsc)

        ↓

JavaScript (.js)

        ↓

Browser
```

---

# Why TypeScript?

JavaScript

```javascript
let price = "100";

price = 500;
```

No compile-time error.

TypeScript

```typescript
let price: number = 100;

// price = "Laptop"; ❌ Error
```

TypeScript catches the error before your application runs.

---

# Installing TypeScript

```bash
npm install -g typescript
```

Check the version:

```bash
tsc --version
```

---

# Your First TypeScript Program

```typescript
let message: string = "Hello AEM";

console.log(message);
```

Compile:

```bash
tsc app.ts
```

Generated JavaScript:

```javascript
var message = "Hello AEM";

console.log(message);
```

---

# Data Types

### String

```typescript
let name: string = "Vijay";
```

### Number

```typescript
let age: number = 25;
```

### Boolean

```typescript
let active: boolean = true;
```

### Array

```typescript
let products: string[] = [
    "Laptop",
    "Phone",
    "TV"
];
```

### Any

```typescript
let value: any = 100;

value = "Adobe";

value = true;
```

Use `any` sparingly because it disables type checking.

---

# Functions

```typescript
function add(a: number, b: number): number {

    return a + b;

}

console.log(add(10, 20));
```

The return type is explicitly declared as `number`.

---

# Optional Parameters

```typescript
function greet(name: string, city?: string) {

    console.log(name);

}
```

`city` is optional.

---

# Default Parameters

```typescript
function greet(name: string = "Guest") {

    console.log(name);

}
```

---

# Interfaces ⭐⭐⭐⭐⭐

Interfaces define the shape of an object.

```typescript
interface Product {

    name: string;

    price: number;

}

const product: Product = {

    name: "Laptop",

    price: 65000

};
```

---

# Optional Properties

```typescript
interface Employee {

    name: string;

    salary?: number;

}
```

---

# Readonly Properties

```typescript
interface User {

    readonly id: number;

    name: string;

}
```

`id` cannot be changed after creation.

---

# Classes

```typescript
class Product {

    name: string;

    price: number;

    constructor(name: string, price: number) {

        this.name = name;

        this.price = price;

    }

    display(): void {

        console.log(this.name, this.price);

    }

}

const laptop = new Product("Laptop", 65000);

laptop.display();
```

---

# Access Modifiers

```typescript
class Employee {

    public name: string;

    private salary: number;

    protected department: string;

    constructor() {

        this.name = "Vijay";

        this.salary = 50000;

        this.department = "IT";

    }

}
```

### public

Accessible everywhere.

### private

Accessible only within the class.

### protected

Accessible within the class and subclasses.

---

# Inheritance

```typescript
class Animal {

    speak() {

        console.log("Animal Sound");

    }

}

class Dog extends Animal {

    bark() {

        console.log("Woof");

    }

}

const dog = new Dog();

dog.speak();

dog.bark();
```

---

# Generics ⭐⭐⭐⭐⭐

Generics allow reusable code while preserving type safety.

```typescript
function identity<T>(value: T): T {

    return value;

}

console.log(identity<string>("Adobe"));

console.log(identity<number>(100));
```

---

# Enums

```typescript
enum Role {

    Admin,

    Author,

    Editor

}

let role = Role.Author;
```

---

# Type Aliases

```typescript
type ProductId = number;

let id: ProductId = 101;
```

---

# Union Types

```typescript
let value: string | number;

value = "Laptop";

value = 500;
```

---

# Type Narrowing

```typescript
function print(value: string | number) {

    if (typeof value === "string") {

        console.log(value.toUpperCase());

    } else {

        console.log(value.toFixed(2));

    }

}
```

---

# Optional Chaining

```typescript
const user = {

    profile: {

        name: "Vijay"

    }

};

console.log(user.profile?.name);
```

This avoids runtime errors when properties may be missing.

---

# Nullish Coalescing

```typescript
let city = null;

console.log(city ?? "Hyderabad");
```

Output:

```text
Hyderabad
```

---

# Modules

Export

```typescript
export class Product {

}
```

Import

```typescript
import { Product } from "./Product";
```

---

# TypeScript in React

```typescript
interface Props {

    title: string;

}

function Header(props: Props) {

    return <h1>{props.title}</h1>;

}
```

---

# TypeScript in AEM

Typical project structure:

```text
ui.frontend

    src

        main

            ts

                app.ts
```

Build process:

```text
TypeScript

↓

Webpack

↓

ClientLib

↓

AEM
```

---

# Real AEM Example

```typescript
interface Product {

    id: number;

    name: string;

    price: number;

}

async function loadProducts(): Promise<Product[]> {

    const response = await fetch("/bin/products");

    return response.json();

}
```

This provides auto-completion and compile-time type checking.

---

# Best Practices

✅ Prefer `interface` for object contracts.

✅ Avoid `any` unless absolutely necessary.

✅ Enable strict mode.

✅ Use generics for reusable code.

✅ Keep types small and focused.

---

# Common Mistakes

❌ Using `any` everywhere.

❌ Ignoring compiler errors.

❌ Duplicating interfaces.

❌ Using `enum` when a union type is sufficient.

---

# Interview Questions

### 1. What is TypeScript?

A typed superset of JavaScript that compiles to JavaScript and provides static type checking.

---

### 2. Difference between `interface` and `type`?

* `interface` is commonly used to define object shapes and supports declaration merging.
* `type` is more flexible and can represent unions, intersections, primitives, tuples, and more.

---

### 3. What are Generics?

Generics allow functions, classes, and interfaces to work with multiple types while preserving type safety.

---

### 4. What is Optional Chaining?

The `?.` operator safely accesses nested properties without throwing an error if a value is `null` or `undefined`.

---

### 5. Why use TypeScript in AEM?

* Better code quality.
* Compile-time error detection.
* Improved IDE support.
* Easier maintenance for large React or SPA-based AEM projects.

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"Why would you choose TypeScript over JavaScript?"**

A strong answer is:

* TypeScript catches many errors during development instead of at runtime.
* It improves code readability and maintainability through explicit types.
* It provides excellent IDE support such as auto-completion and refactoring.
* It scales well for large enterprise applications like React-based AEM frontends.

---

# Next Chapter: **Node.js & npm (Complete)** ⭐⭐⭐⭐⭐

We'll cover:

* What Node.js is.
* npm and `package.json`.
* Installing packages.
* Scripts.
* Common frontend build tools.
* How `ui.frontend` works in AEM.
* Webpack integration.
* ClientLib generation.
* Real enterprise project setup.
* Interview questions.

This chapter is essential because **every modern AEM frontend project** relies on Node.js, npm, and build tools to generate optimized Client Libraries.
Excellent! Now let's learn **Node.js & npm**, which are the foundation of the **AEM Frontend Build System**. Every modern AEM frontend project (especially with `ui.frontend`) uses Node.js, npm, Webpack, and ClientLib generation.

---

# Chapter 6: Node.js & npm (Beginner → Advanced) ⭐⭐⭐⭐⭐

---

# What is Node.js?

**Node.js** is a JavaScript runtime that allows you to run JavaScript **outside the browser**.

Before Node.js:

```text
JavaScript

↓

Browser Only
```

After Node.js:

```text
JavaScript

↓

Browser

OR

Server
```

---

# Why Does AEM Need Node.js?

Node.js is used for:

* Frontend builds
* SCSS compilation
* JavaScript bundling
* Webpack
* Babel
* ClientLib generation
* React development
* TypeScript compilation

It is **not** used to run AEM itself.

---

# What is npm?

**npm (Node Package Manager)** is the default package manager for Node.js.

It helps you:

* Install libraries
* Manage dependencies
* Run build scripts
* Update packages

---

# Install Node.js

Download from:

**[https://nodejs.org](https://nodejs.org)**

Check installation:

```bash
node -v
```

Example:

```text
v22.x.x
```

Check npm:

```bash
npm -v
```

---

# Creating a Project

```bash
mkdir myproject

cd myproject

npm init
```

This creates:

```text
package.json
```

---

# package.json

Example:

```json
{
  "name": "aem-project",
  "version": "1.0.0",
  "scripts": {
    "build": "webpack",
    "start": "webpack serve"
  }
}
```

---

# Understanding package.json

```json
{
"name":"Project Name",
"version":"Project Version",
"dependencies":{},
"devDependencies":{},
"scripts":{}
}
```

---

# Installing Packages

Example

```bash
npm install lodash
```

Updates:

```text
package.json

↓

node_modules
```

---

# Installing Development Packages

```bash
npm install webpack --save-dev
```

or

```bash
npm install -D webpack
```

These packages are used only during development.

---

# Dependencies vs devDependencies

| dependencies        | devDependencies               |
| ------------------- | ----------------------------- |
| Required at runtime | Required only for development |
| Example: React      | Example: Webpack              |
| Example: Axios      | Example: Babel                |

---

# node_modules

After installing:

```text
project

    node_modules

    package.json

    package-lock.json
```

`node_modules` contains all installed packages.

---

# package-lock.json

Stores:

* Exact package versions
* Dependency tree

This ensures every developer installs the same versions.

---

# npm Scripts ⭐⭐⭐⭐⭐

Example

```json
"scripts":{

"start":"webpack serve",

"build":"webpack",

"test":"jest"

}
```

Run:

```bash
npm run build
```

---

# Installing Multiple Packages

```bash
npm install react react-dom
```

---

# Removing Packages

```bash
npm uninstall react
```

---

# Updating Packages

```bash
npm update
```

---

# npx

Instead of installing globally:

```bash
npx webpack
```

Runs the local package version.

---

# AEM ui.frontend Structure

```text
ui.frontend

    src

        main

            js

            scss

    package.json

    webpack.config.js
```

---

# Build Flow

```text
JavaScript

↓

TypeScript

↓

SCSS

↓

Webpack

↓

ClientLib Generator

↓

ui.apps

↓

AEM
```

---

# Real Enterprise Build Flow

Developer writes:

```text
SCSS

JavaScript

TypeScript
```

↓

```text
npm run build
```

↓

```text
Webpack
```

↓

```text
Minified CSS

Minified JS
```

↓

```text
ClientLib
```

↓

```text
AEM
```

---

# Common npm Commands

Install all packages:

```bash
npm install
```

Run build:

```bash
npm run build
```

Run development server:

```bash
npm start
```

Check outdated packages:

```bash
npm outdated
```

List installed packages:

```bash
npm list
```

---

# Example package.json for AEM

```json
{
  "name": "ui.frontend",
  "private": true,
  "scripts": {
    "build": "webpack --mode production",
    "dev": "webpack serve --mode development"
  },
  "devDependencies": {
    "webpack": "^5",
    "webpack-cli": "^5",
    "sass": "^1",
    "typescript": "^5"
  }
}
```

---

# AEM Frontend Build Lifecycle

```text
Developer

↓

npm install

↓

node_modules

↓

npm run build

↓

Webpack

↓

CSS + JS

↓

ClientLibs

↓

AEM
```

---

# Best Practices

✅ Commit `package.json` and `package-lock.json`.

✅ Do **not** commit `node_modules` to Git.

✅ Use `npm ci` in CI/CD pipelines for reproducible builds.

✅ Keep dependencies updated, but test before upgrading major versions.

---

# Common Mistakes

❌ Editing files directly inside `node_modules`.

❌ Committing `node_modules` to version control.

❌ Installing every package globally.

❌ Ignoring security warnings from `npm audit`.

---

# Interview Questions

### 1. What is Node.js?

Node.js is a JavaScript runtime that executes JavaScript outside the browser.

---

### 2. What is npm?

npm is the Node Package Manager used to install, update, and manage JavaScript packages.

---

### 3. What is `package.json`?

It is the project's configuration file that defines metadata, dependencies, and scripts.

---

### 4. Difference between `dependencies` and `devDependencies`?

* **dependencies**: Needed when the application runs.
* **devDependencies**: Needed only for development and build tasks.

---

### 5. Why is Node.js required in an AEM frontend project?

Because it powers the frontend toolchain, including:

* Webpack
* TypeScript
* SCSS compilation
* ClientLib generation
* Modern JavaScript builds

---

### 6. Why shouldn't `node_modules` be committed?

Because it is large, can be recreated with `npm install`, and is generated from `package.json` and `package-lock.json`.

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"What is the role of Node.js in AEM?"**

A strong answer is:

> "Node.js is not used to run AEM itself. Instead, it provides the frontend build environment. It installs project dependencies through npm, compiles SCSS and TypeScript, bundles JavaScript with Webpack, and generates optimized Client Libraries that are deployed to AEM."

This clearly distinguishes **AEM's Java backend** from the **frontend build pipeline**, which is a common interview topic.

---

# Next Chapter: Webpack (Complete) ⭐⭐⭐⭐⭐

We'll cover:

* What Webpack is.
* Entry and Output.
* Loaders.
* Plugins.
* SCSS compilation.
* Babel.
* TypeScript integration.
* Asset optimization.
* ClientLib generation.
* Enterprise AEM frontend build pipeline.
* Interview questions.

Webpack is the **heart of the modern AEM frontend build process**, and understanding it is essential for working on enterprise AEM projects.
Excellent! Now let's learn **Webpack**, which is the **core build tool** used in modern AEM frontend projects. Every enterprise AEM project with a `ui.frontend` module uses Webpack to bundle JavaScript, compile SCSS, optimize assets, and generate Client Libraries.

---

# Chapter 7: Webpack Complete (Beginner → Advanced) ⭐⭐⭐⭐⭐

---

# What is Webpack?

**Webpack** is a **module bundler**.

It takes multiple frontend files:

* JavaScript
* TypeScript
* SCSS
* CSS
* Images
* Fonts

and bundles them into optimized files for the browser.

Without Webpack:

```text
script1.js
script2.js
style1.css
style2.css

↓

Many HTTP Requests
```

With Webpack:

```text
script1.js
script2.js
style1.css
style2.css

↓

Webpack

↓

bundle.js
bundle.css
```

---

# Why Webpack in AEM?

AEM uses Webpack to:

* Bundle JavaScript
* Compile TypeScript
* Compile SCSS
* Optimize images
* Minify CSS
* Minify JavaScript
* Generate ClientLibs

---

# Webpack Build Flow

```text
Developer

↓

JavaScript

SCSS

Images

↓

Webpack

↓

Optimized Assets

↓

ClientLib

↓

AEM
```

---

# Install Webpack

```bash
npm install webpack webpack-cli --save-dev
```

---

# Project Structure

```text
ui.frontend

│
├── src
│   ├── main
│   │   ├── js
│   │   │    app.js
│   │   ├── scss
│   │   │    site.scss
│
├── dist
│
├── package.json
│
└── webpack.config.js
```

---

# Basic Webpack Configuration

```javascript
const path = require("path");

module.exports = {

    entry: "./src/main/js/app.js",

    output: {

        filename: "bundle.js",

        path: path.resolve(__dirname, "dist")

    }

};
```

---

# Understanding the Configuration

### Entry

```javascript
entry:"./src/main/js/app.js"
```

This is the starting point of your application.

---

### Output

```javascript
output:{

filename:"bundle.js"

}
```

Webpack creates:

```text
dist

↓

bundle.js
```

---

# Running Webpack

```bash
npx webpack
```

Output

```text
dist

bundle.js
```

---

# Loaders ⭐⭐⭐⭐⭐

Webpack cannot understand SCSS or TypeScript directly.

Loaders convert them into JavaScript or CSS.

```text
SCSS

↓

sass-loader

↓

CSS

↓

Browser
```

---

# CSS Loader

Install

```bash
npm install css-loader style-loader --save-dev
```

Configuration

```javascript
module.exports={

module:{

rules:[

{

test:/\.css$/,

use:["style-loader","css-loader"]

}

]

}

}
```

---

# SCSS Loader

Install

```bash
npm install sass sass-loader --save-dev
```

Configuration

```javascript
{

test:/\.scss$/,

use:[

"style-loader",

"css-loader",

"sass-loader"

]

}
```

Now Webpack compiles:

```text
site.scss

↓

site.css
```

---

# Babel Loader

Babel converts modern JavaScript into browser-compatible JavaScript.

Install

```bash
npm install babel-loader @babel/core @babel/preset-env --save-dev
```

Configuration

```javascript
{

test:/\.js$/,

exclude:/node_modules/,

use:{

loader:"babel-loader",

options:{

presets:["@babel/preset-env"]

}

}

}
```

---

# TypeScript Loader

Install

```bash
npm install ts-loader typescript --save-dev
```

Configuration

```javascript
{

test:/\.ts$/,

loader:"ts-loader"

}
```

---

# Asset Loader

Images

```javascript
{

test:/\.(png|jpg|svg)$/,

type:"asset/resource"

}
```

Webpack copies the image into the output folder.

---

# Plugins ⭐⭐⭐⭐⭐

Plugins perform additional tasks.

Examples:

* Minification
* HTML generation
* Cleaning folders
* Environment variables

---

# HtmlWebpackPlugin

Install

```bash
npm install html-webpack-plugin --save-dev
```

Configuration

```javascript
const HtmlWebpackPlugin=require(
"html-webpack-plugin"
);

plugins:[

new HtmlWebpackPlugin()

]
```

---

# CleanWebpackPlugin

Deletes the old build before creating a new one.

```javascript
new CleanWebpackPlugin()
```

---

# Development Mode

```bash
npm run dev
```

or

```bash
webpack --mode development
```

Features

* Fast build
* Source Maps
* Easier debugging

---

# Production Mode

```bash
webpack --mode production
```

Automatically:

* Minifies JavaScript
* Minifies CSS
* Optimizes assets
* Removes unused code

---

# Source Maps

Enable debugging.

```javascript
devtool:"source-map"
```

---

# Webpack Dev Server

Install

```bash
npm install webpack-dev-server --save-dev
```

Run

```bash
npm start
```

Automatically reloads the browser after file changes.

---

# Real AEM Build Flow ⭐⭐⭐⭐⭐

```text
Developer

↓

SCSS

↓

TypeScript

↓

JavaScript

↓

Webpack

↓

bundle.js

site.css

↓

ClientLib Generator

↓

ui.apps

↓

AEM
```

---

# package.json

```json
{

"scripts":{

"dev":"webpack serve",

"build":"webpack --mode production"

}

}
```

Run

```bash
npm run build
```

---

# Webpack + ClientLib

After build

```text
dist

↓

bundle.js

site.css

↓

clientlib-site

↓

AEM
```

---

# Enterprise Architecture

```text
VS Code

↓

TypeScript

↓

SCSS

↓

Webpack

↓

ClientLib Generator

↓

ui.apps

↓

Maven Build

↓

Cloud Manager

↓

AEM Cloud
```

---

# Best Practices

✅ Keep entry points small.

✅ Enable production mode for deployments.

✅ Use Source Maps during development.

✅ Split large bundles when needed.

✅ Optimize images.

---

# Common Mistakes

❌ Putting all code into one huge JavaScript file.

❌ Forgetting production mode.

❌ Not minifying assets.

❌ Ignoring bundle size.

---

# Interview Questions

### 1. What is Webpack?

Webpack is a module bundler that combines JavaScript, CSS, SCSS, TypeScript, images, and other assets into optimized bundles for deployment.

---

### 2. What is an Entry Point?

The first file Webpack starts processing to build the dependency graph.

---

### 3. What are Loaders?

Loaders transform non-JavaScript files (such as SCSS or TypeScript) into formats Webpack can process.

---

### 4. What are Plugins?

Plugins extend Webpack by performing tasks such as cleaning output directories, generating HTML, and optimizing bundles.

---

### 5. Why is Webpack used in AEM?

Webpack compiles frontend assets, bundles JavaScript and CSS, optimizes them, and prepares Client Libraries for deployment into AEM.

---

### 6. Difference between Development and Production Mode?

| Development      | Production               |
| ---------------- | ------------------------ |
| Faster builds    | Optimized builds         |
| Source maps      | Minified assets          |
| Easier debugging | Smaller bundle size      |
| Not optimized    | Optimized for deployment |

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"Explain the AEM frontend build process."**

A strong answer is:

```text
Developer

↓

TypeScript / JavaScript / SCSS

↓

Webpack

↓

Optimized CSS & JS

↓

ClientLib Generator

↓

ui.apps

↓

Maven Build

↓

Cloud Manager

↓

AEM
```

Then explain:

* **Webpack** bundles and optimizes assets.
* **SCSS** is compiled into CSS.
* **TypeScript** is compiled into JavaScript.
* The generated files are packaged into **AEM Client Libraries**.
* Maven packages the project.
* Cloud Manager deploys it to AEM as a Cloud Service.

This demonstrates a complete understanding of the modern AEM frontend pipeline.

---

# Next Chapter: SCSS (Sass) Complete ⭐⭐⭐⭐⭐

We'll cover:

* Variables
* Nesting
* Mixins
* Functions
* Partials
* Imports
* Inheritance
* Responsive Mixins
* Enterprise folder structure
* SCSS in AEM ClientLibs
* Best practices
* Interview questions

SCSS is the preferred way to write maintainable CSS in enterprise AEM projects because it improves reusability, organization, and scalability.
Excellent! Now let's learn **SCSS (Sass)**, which is the standard way to write CSS in **enterprise AEM projects**. Almost every modern AEM project uses SCSS because it's easier to maintain than plain CSS.

---

# Chapter 8: SCSS (Sass) Complete ⭐⭐⭐⭐⭐

---

# What is SCSS?

**SCSS (Sassy CSS)** is a superset of CSS that adds programming features such as:

* Variables
* Nesting
* Mixins
* Functions
* Inheritance
* Imports

SCSS is compiled into standard CSS before being served to the browser.

```text
SCSS

↓

Sass Compiler

↓

CSS

↓

Browser
```

---

# Why Use SCSS?

Without SCSS

```css
.button{
    background:#0055ff;
}

.card{
    border:1px solid #0055ff;
}

.header{
    color:#0055ff;
}
```

The same color is repeated.

---

With SCSS

```scss
$primary:#0055ff;

.button{
    background:$primary;
}

.card{
    border:1px solid $primary;
}

.header{
    color:$primary;
}
```

Change the variable once, and every component updates.

---

# SCSS File Structure in AEM

```text
ui.frontend

└── src

    └── main

        └── scss

            ├── site.scss
            ├── _variables.scss
            ├── _mixins.scss
            ├── _buttons.scss
            ├── _header.scss
            ├── _footer.scss
            └── _card.scss
```

---

# Variables ⭐⭐⭐⭐⭐

```scss
$primary-color:#0055ff;
$secondary-color:#333;
$font-size:16px;
```

Use:

```scss
body{

    color:$secondary-color;

    font-size:$font-size;

}

.button{

    background:$primary-color;

}
```

---

# Nesting ⭐⭐⭐⭐⭐

Without SCSS

```css
.card h2{

color:red;

}

.card p{

color:gray;

}
```

SCSS

```scss
.card{

    h2{

        color:red;

    }

    p{

        color:gray;

    }

}
```

Compiled CSS

```css
.card h2{
    color:red;
}

.card p{
    color:gray;
}
```

---

# Parent Selector (&)

```scss
.button{

    background:blue;

    &:hover{

        background:red;

    }

}
```

Output

```css
.button:hover{

background:red;

}
```

---

# Mixins ⭐⭐⭐⭐⭐

A mixin is reusable CSS.

```scss
@mixin center{

    display:flex;

    justify-content:center;

    align-items:center;

}
```

Use

```scss
.hero{

    @include center;

}
```

Output

```css
.hero{

display:flex;

justify-content:center;

align-items:center;

}
```

---

# Mixins with Parameters

```scss
@mixin button($bg,$color){

    background:$bg;

    color:$color;

}
```

Use

```scss
.save{

@include button(green,white);

}

.cancel{

@include button(red,white);

}
```

---

# Inheritance (@extend)

```scss
.box{

    padding:20px;

    border-radius:5px;

}

.card{

    @extend .box;

    background:white;

}
```

The `.card` inherits the styles from `.box`.

---

# Functions

```scss
@function rem($px){

    @return $px/16*1rem;

}
```

Use

```scss
.title{

font-size:rem(32);

}
```

---

# Partials

Files starting with `_` are partials.

```text
_variables.scss

_mixins.scss

_buttons.scss
```

They are imported into the main stylesheet.

---

# Imports

```scss
@use "variables";
@use "mixins";
@use "buttons";
```

`@use` is the modern replacement for the older `@import`.

---

# Responsive Mixins

```scss
@mixin mobile{

    @media(max-width:768px){

        @content;

    }

}
```

Use

```scss
.header{

    display:flex;

    @include mobile{

        display:block;

    }

}
```

---

# Example: Product Card

```scss
$primary:#0070f3;

.card{

    border:1px solid #ddd;

    padding:20px;

    border-radius:8px;

    h2{

        color:$primary;

    }

    button{

        background:$primary;

        color:white;

        border:none;

        padding:10px;

        cursor:pointer;

        &:hover{

            background:#0050c0;

        }

    }

}
```

---

# SCSS Build Process in AEM

```text
SCSS Files

↓

Webpack

↓

CSS

↓

ClientLib

↓

AEM

↓

Browser
```

---

# Best Practices

✅ Keep variables in a separate file.

✅ Create reusable mixins.

✅ Use nesting carefully (avoid deep nesting).

✅ Use meaningful file names.

✅ Organize styles by component.

---

# Common Mistakes

❌ Hardcoding colors repeatedly.

❌ Nesting selectors too deeply.

❌ Creating one huge SCSS file.

❌ Duplicating styles instead of using mixins.

---

# Interview Questions

### 1. What is SCSS?

SCSS is a CSS preprocessor that adds features like variables, mixins, nesting, and functions. It is compiled into standard CSS.

---

### 2. What are Variables?

Variables store reusable values, such as colors, font sizes, and spacing.

Example:

```scss
$primary:#0055ff;
```

---

### 3. What is a Mixin?

A reusable block of CSS that can be included in multiple selectors using `@include`.

---

### 4. What is the difference between `@extend` and `@mixin`?

| @extend                   | @mixin                        |
| ------------------------- | ----------------------------- |
| Shares existing selectors | Reuses blocks of CSS          |
| Generates less CSS        | More flexible with parameters |
| Good for inheritance      | Good for reusable utilities   |

---

### 5. How is SCSS used in AEM?

SCSS files are stored in the `ui.frontend` module, compiled by Webpack into CSS, packaged into Client Libraries, and then delivered by AEM.

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"Why do enterprise AEM projects use SCSS instead of plain CSS?"**

A strong answer is:

* SCSS improves maintainability through variables and mixins.
* It reduces duplicated code.
* It allows component-based styling.
* It integrates well with Webpack and the AEM `ui.frontend` build pipeline.
* It scales much better for large enterprise applications with hundreds of components.

---

# 🎯 Next Chapter: HTL (Sightly) Complete ⭐⭐⭐⭐⭐

This is **the most important AEM Frontend topic**.

We'll cover in detail:

* HTL Syntax
* Expressions (`${}`)
* `data-sly-use`
* `data-sly-test`
* `data-sly-list`
* `data-sly-repeat`
* `data-sly-resource`
* `data-sly-include`
* `data-sly-template`
* `data-sly-call`
* Context-aware escaping
* Sling Models integration
* Core Components integration
* Real enterprise examples
* Best practices
* 50+ interview questions

**HTL is the heart of AEM frontend development**, and mastering it is essential for becoming an AEM Full Stack Developer.
Excellent! Now we'll start the **most important AEM Frontend topic**.

# Chapter 9: HTL (Sightly) Complete (Beginner → Advanced) ⭐⭐⭐⭐⭐

> **HTL (HTML Template Language)**, formerly called **Sightly**, is Adobe's recommended templating language for AEM. Almost every AEM component is built using HTL.

---

# What is HTL?

HTL is a server-side template language used to create AEM components.

Instead of writing Java code inside JSP pages, HTL keeps HTML clean and uses expressions to display data.

**Flow:**

```text
Browser
      │
      ▼
HTL (.html)
      │
      ▼
Sling Model
      │
      ▼
OSGi Service (Optional)
      │
      ▼
JCR Repository
      │
      ▼
Generated HTML
      │
      ▼
Browser
```

---

# Why HTL?

Before HTL (JSP):

```jsp
<%
String title=(String)resource.getValueMap().get("jcr:title");
out.println(title);
%>
```

Problems:

* Java mixed with HTML
* Hard to maintain
* Security risks

With HTL:

```html
<h1>${properties.jcr:title}</h1>
```

Advantages:

* Clean HTML
* Secure by default
* Easy to read
* Adobe recommended

---

# HTL File Structure

```
/apps/mysite/components/title

├── title.html
├── _cq_dialog/.content.xml
├── TitleModel.java
└── clientlibs
```

---

# HTL Expressions ⭐⭐⭐⭐⭐

Display a property:

```html
<h1>${properties.jcr:title}</h1>
```

If `jcr:title = Home Page`

Output:

```html
<h1>Home Page</h1>
```

---

# Display Component Properties

Dialog stores:

```
./title
```

HTL:

```html
<h2>${properties.title}</h2>
```

Repository:

```
title = Adobe AEM
```

Output:

```html
<h2>Adobe AEM</h2>
```

---

# Display Sling Model Data

Sling Model:

```java
@Model(adaptables = Resource.class)
public class ProductModel {

    @ValueMapValue
    private String name;

    public String getName() {
        return name;
    }
}
```

HTL:

```html
<sly data-sly-use.model=
"com.mysite.core.models.ProductModel"/>

<h2>${model.name}</h2>
```

Output:

```html
<h2>Laptop</h2>
```

---

# data-sly-use ⭐⭐⭐⭐⭐

Loads a Sling Model or Java helper.

```html
<sly data-sly-use.model=
"com.mysite.core.models.ProductModel"/>
```

Now the model is available:

```html
${model.name}

${model.price}
```

---

# data-sly-test ⭐⭐⭐⭐⭐

Conditional rendering.

Example:

```html
<sly data-sly-test="${properties.showButton}">

<button>Buy Now</button>

</sly>
```

If:

```
showButton=true
```

Output:

```html
<button>Buy Now</button>
```

If false:

No HTML is generated.

---

# if...else in HTL

```html
<sly data-sly-test.isAdmin="${properties.admin}">

<p>Admin User</p>

</sly>

<sly data-sly-test="${!isAdmin}">

<p>Normal User</p>

</sly>
```

---

# data-sly-list ⭐⭐⭐⭐⭐

Used for iteration.

Model:

```java
public List<String> getProducts() {

    return Arrays.asList(
        "Laptop",
        "Phone",
        "TV"
    );

}
```

HTL:

```html
<ul data-sly-list.product="${model.products}">

<li>${product}</li>

</ul>
```

Output:

```html
<ul>

<li>Laptop</li>

<li>Phone</li>

<li>TV</li>

</ul>
```

---

# List Metadata

```html
<ul data-sly-list.item="${model.products}">

<li>

${item}

${itemList.count}

${itemList.first}

${itemList.last}

</li>

</ul>
```

Useful properties:

* `itemList.index`
* `itemList.count`
* `itemList.first`
* `itemList.last`
* `itemList.odd`
* `itemList.even`

---

# data-sly-repeat

```html
<div data-sly-repeat.product="${model.products}">

<h2>${product.name}</h2>

</div>
```

Unlike `data-sly-list`, it repeats the host element itself.

---

# data-sly-resource ⭐⭐⭐⭐⭐

Includes another AEM resource/component.

```html
<sly data-sly-resource="${'header'}"/>
```

Flow:

```
Home Page

↓

Header Component

↓

Rendered HTML
```

---

# data-sly-include

Includes another HTL file.

```html
<sly data-sly-include="footer.html"/>
```

---

# data-sly-template

Create reusable templates.

```html
<template data-sly-template.card="${@ title}">

<div class="card">

<h2>${title}</h2>

</div>

</template>
```

---

# data-sly-call

Call a template.

```html
<sly data-sly-call="${card @ title='Laptop'}"/>
```

Output:

```html
<div class="card">

<h2>Laptop</h2>

</div>
```

---

# data-sly-unwrap

Remove unnecessary wrapper elements.

```html
<div data-sly-unwrap>

<h1>Title</h1>

</div>
```

Output:

```html
<h1>Title</h1>
```

---

# Comments

HTL comment:

```html
<!--/*

Hidden from output

*/-->
```

These comments are not rendered in the final HTML.

---

# Context-Aware Escaping ⭐⭐⭐⭐⭐

HTL automatically escapes output to prevent XSS attacks.

Example:

```html
${properties.title}
```

If title contains:

```text
<script>alert('XSS')</script>
```

HTL escapes it instead of executing it.

For URLs:

```html
<a href="${properties.url}">

Link

</a>
```

HTL applies the correct escaping for URL contexts.

---

# Working with Core Components

Proxy component:

```
/apps/mysite/components/title
```

`title.html`

```html
<div class="custom-title">

<sly
data-sly-resource="${resource
@ resourceType='core/wcm/components/title/v3/title'}"/>

</div>
```

This wraps the Adobe Core Title component with custom markup.

---

# Complete Example

Sling Model

```java
@Model(adaptables = Resource.class)
public class WelcomeModel {

    @ValueMapValue
    private String title;

    public String getTitle() {

        return title;

    }

}
```

HTL

```html
<sly
data-sly-use.model=
"com.mysite.core.models.WelcomeModel"/>

<section class="hero">

<h1>${model.title}</h1>

<sly data-sly-test="${properties.showButton}">

<button>Explore</button>

</sly>

</section>
```

Output:

```html
<section class="hero">

<h1>Welcome to AEM</h1>

<button>Explore</button>

</section>
```

---

# HTL Best Practices

✅ Keep business logic in Sling Models.

✅ Use `data-sly-use` for models.

✅ Use `data-sly-test` for conditions.

✅ Use `data-sly-list` for collections.

✅ Reuse templates with `data-sly-template`.

✅ Let HTL handle escaping automatically.

---

# Common Mistakes

❌ Writing business logic in HTL.

❌ Calling JCR APIs directly from templates.

❌ Copying Core Component HTL instead of extending.

❌ Disabling escaping unnecessarily.

---

# HTL vs JSP

| HTL                   | JSP                        |
| --------------------- | -------------------------- |
| Secure by default     | Requires manual care       |
| Easy to read          | Java mixed with HTML       |
| Adobe recommended     | Legacy approach            |
| Supports Sling Models | Often relies on scriptlets |

---

# Interview Questions

### 1. What is HTL?

HTL (HTML Template Language) is Adobe's server-side templating language for rendering AEM components.

---

### 2. What does `data-sly-use` do?

It loads a Sling Model or Java helper into the HTL template.

---

### 3. What is the difference between `data-sly-list` and `data-sly-repeat`?

* **`data-sly-list`** iterates over a collection and provides loop metadata like `itemList.index` and `itemList.first`.
* **`data-sly-repeat`** repeats the host HTML element itself for each item.

---

### 4. What is `data-sly-resource` used for?

It includes and renders another AEM resource or component.

---

### 5. Why is HTL considered secure?

Because it performs **context-aware output escaping** automatically, helping prevent Cross-Site Scripting (XSS) attacks.

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"How do HTL, Sling Models, and OSGi Services work together?"**

A strong answer is:

```text
JCR Content
      │
      ▼
OSGi Service (Business Logic)
      │
      ▼
Sling Model (Prepare Data)
      │
      ▼
HTL (Render HTML)
      │
      ▼
Browser
```

Explain:

* **OSGi Services** perform business logic and integrations.
* **Sling Models** adapt resources and prepare data for the view.
* **HTL** displays the data without containing business logic.

This separation of responsibilities is a core principle of clean AEM development.

---

## Next Chapter: Client Libraries (ClientLibs) ⭐⭐⭐⭐⭐

We'll cover in depth:

* What ClientLibs are
* Folder structure
* `css.txt` and `js.txt`
* Categories
* Dependencies
* Embedding ClientLibs
* Loading CSS and JavaScript in HTL
* ClientLib generation from `ui.frontend`
* Cache busting
* Performance optimization
* Real enterprise examples
* Complete interview questions

**ClientLibs are the backbone of frontend asset management in AEM**, and every AEM frontend developer should understand them thoroughly.
Excellent! Now we'll learn **Client Libraries (ClientLibs)**, one of the **most important AEM Frontend topics**. Every AEM project uses ClientLibs to manage CSS and JavaScript.

---

# Chapter 10: Client Libraries (ClientLibs) Complete ⭐⭐⭐⭐⭐

---

# What are Client Libraries?

**Client Libraries (ClientLibs)** are AEM's built-in mechanism for managing and delivering frontend assets such as:

* CSS
* JavaScript
* Images
* Fonts

Instead of linking CSS/JS files manually, AEM serves them through ClientLibs.

---

# Why ClientLibs?

Without ClientLibs:

```text
index.html

↓

styles.css

↓

main.js

↓

header.js

↓

footer.js
```

Many files are loaded individually.

With ClientLibs:

```text
CSS Files
JS Files

↓

ClientLib

↓

Optimized Bundle

↓

Browser
```

Benefits:

* Minification
* Caching
* Dependency management
* Versioning
* Performance optimization

---

# ClientLib Architecture

```text
Browser

↓

HTL

↓

ClientLib

↓

CSS

↓

JavaScript

↓

Browser
```

---

# Folder Structure

```text
/apps/mysite

└── clientlibs

      ├── clientlib-site

      ├── clientlib-base

      └── clientlib-author
```

---

# Inside a ClientLib

```text
clientlib-site

│── css

│     styles.css

│

│── js

│     script.js

│

│── resources

│

│── css.txt

│── js.txt

└── .content.xml
```

---

# `.content.xml`

```xml
<jcr:root
    jcr:primaryType="cq:ClientLibraryFolder"
    categories="[mysite.site]"
    allowProxy="{Boolean}true"/>
```

---

# Understanding the Properties

## `cq:ClientLibraryFolder`

Marks the folder as a Client Library.

---

## `categories`

Example

```text
mysite.site
```

This category name is used to include the ClientLib.

---

## `allowProxy`

```text
true
```

Allows ClientLibs under `/apps` to be served through `/etc.clientlibs`, which is the recommended approach.

---

# css.txt

Lists CSS files.

```text
#base=css

styles.css

header.css

footer.css
```

Load order follows the file order.

---

# js.txt

Lists JavaScript files.

```text
#base=js

main.js

search.js

carousel.js
```

---

# CSS Example

```css
body{

font-family:Arial;

}

.button{

background:blue;

}
```

---

# JavaScript Example

```javascript
document

.querySelector(".button")

.addEventListener(

"click",

()=>{

alert("Clicked");

}

);
```

---

# Including ClientLibs in HTL ⭐⭐⭐⭐⭐

Load the Granite template:

```html
<sly
data-sly-use.clientlib=
"/libs/granite/sightly/templates/clientlib.html"/>
```

Load CSS

```html
<sly
data-sly-call="${clientlib.css
@ categories='mysite.site'}"/>
```

Load JavaScript

```html
<sly
data-sly-call="${clientlib.js
@ categories='mysite.site'}"/>
```

---

# Generated HTML

```html
<link rel="stylesheet"

href="/etc.clientlibs/mysite/clientlib-site.css">

<script

src="/etc.clientlibs/mysite/clientlib-site.js">

</script>
```

---

# Categories ⭐⭐⭐⭐⭐

Examples

```text
mysite.site

mysite.author

mysite.base

mysite.theme
```

Different pages can load different categories.

---

# Dependencies

Suppose

```text
clientlib-site

↓

Depends on

↓

clientlib-base
```

Configuration

```text
dependencies

↓

mysite.base
```

Flow

```text
clientlib-base

↓

clientlib-site

↓

Browser
```

Dependencies ensure correct loading order.

---

# Embedding ClientLibs

Instead of multiple requests:

```text
Base CSS

↓

Theme CSS

↓

Component CSS
```

Embed:

```text
Single CSS Bundle
```

Property

```text
embed

↓

mysite.base
```

---

# AEM Frontend Build

```text
SCSS

↓

Webpack

↓

CSS

↓

ClientLib Generator

↓

clientlib-site

↓

AEM
```

---

# ui.frontend Integration

```text
ui.frontend

↓

dist

↓

clientlib-site

↓

ui.apps

↓

AEM
```

---

# ClientLib Types

| ClientLib        | Purpose                |
| ---------------- | ---------------------- |
| clientlib-site   | Website CSS & JS       |
| clientlib-base   | Shared resources       |
| clientlib-author | Authoring enhancements |
| clientlib-theme  | Theme-specific styles  |

---

# Real Project Example

Corporate Website

```text
clientlib-base

↓

Bootstrap

↓

clientlib-site

↓

Project CSS

↓

Browser
```

---

# Cache

Browser

↓

Downloads

↓

ClientLib

↓

Stores in Cache

↓

Next Request

↓

Uses Cached Version

This improves performance.

---

# allowProxy

Instead of

```text
/apps/mysite/clientlibs
```

Browser accesses:

```text
/etc.clientlibs/mysite/clientlib-site.css
```

This is more secure and recommended.

---

# Best Practices

✅ Use meaningful category names.

✅ Enable `allowProxy`.

✅ Separate author and publish ClientLibs.

✅ Minify CSS and JavaScript.

✅ Bundle related assets.

---

# Common Mistakes

❌ Loading many ClientLibs unnecessarily.

❌ Forgetting `allowProxy`.

❌ Incorrect dependency configuration.

❌ Placing JavaScript inline instead of in ClientLibs.

---

# Interview Questions

### 1. What are ClientLibs?

AEM's mechanism for managing and serving CSS, JavaScript, fonts, and other frontend assets.

---

### 2. What is the purpose of `categories`?

They identify a Client Library so it can be included from HTL.

---

### 3. What does `allowProxy=true` do?

It allows ClientLibs stored under `/apps` to be served via `/etc.clientlibs`, which is the recommended and secure approach.

---

### 4. What are `css.txt` and `js.txt`?

They define which CSS and JavaScript files belong to the Client Library and the order in which they are loaded.

---

### 5. What is the difference between `dependencies` and `embed`?

| Dependencies                       | Embed                                         |
| ---------------------------------- | --------------------------------------------- |
| Loads another ClientLib separately | Merges another ClientLib into the current one |
| Separate HTTP requests             | Fewer HTTP requests                           |
| Good for reusable libraries        | Good for performance optimization             |

---

### 6. How are ClientLibs included in HTL?

```html
<sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html"/>

<sly data-sly-call="${clientlib.css @ categories='mysite.site'}"/>

<sly data-sly-call="${clientlib.js @ categories='mysite.site'}"/>
```

---

# Real Enterprise Example

```text
Developer

↓

SCSS + JavaScript

↓

Webpack

↓

ClientLib Generator

↓

clientlib-site

↓

HTL Includes ClientLib

↓

Browser

↓

Cached Assets
```

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"How do you include CSS and JavaScript in an AEM component?"**

A strong answer is:

1. Create a `cq:ClientLibraryFolder`.
2. Configure `categories` and set `allowProxy=true`.
3. Add your CSS files in `css.txt` and JavaScript files in `js.txt`.
4. Include the ClientLib in HTL using the Granite `clientlib.html` template.
5. For modern projects, generate the ClientLib automatically from the `ui.frontend` module using Webpack.

This is the **Adobe-recommended approach** used in enterprise AEM projects.

---

# 🎯 Next Chapter: Granite UI Dialogs (Complete) ⭐⭐⭐⭐⭐

In the next lesson, we'll cover:

* Granite UI
* Touch UI Dialogs
* TextField
* PathField
* Select
* Checkbox
* Multifield
* FileUpload
* Tabs
* Composite Multifield
* Validation
* Show/Hide fields
* Coral UI components
* Complete dialog XML
* Real enterprise examples
* Interview questions

**Granite UI Dialogs are one of the most frequently asked AEM frontend interview topics**, because every custom component requires an authoring dialog.
Excellent! Now let's learn **Granite UI Dialogs**, one of the **most important AEM Frontend topics**. Every AEM component needs a dialog so that authors can configure it. If you know Granite UI well, you can build almost any AEM component.

---

# Chapter 11: Granite UI Dialogs (Beginner → Advanced) ⭐⭐⭐⭐⭐

---

# What is a Granite UI Dialog?

A **Granite UI Dialog** is the authoring interface shown when an author edits a component.

Example:

```text
Author

↓

Clicks "Edit"

↓

Granite UI Dialog Opens

↓

Enters Data

↓

Data Saved in JCR

↓

HTL Displays Data
```

---

# Component Structure

```text
/apps/mysite/components/hero

│── hero.html
│── HeroModel.java
│── _cq_dialog
│      └── .content.xml
│── clientlibs
```

The `_cq_dialog` folder contains the dialog definition.

---

# Dialog Architecture

```text
Author

↓

Dialog

↓

JCR Properties

↓

Sling Model

↓

HTL

↓

Browser
```

---

# Basic Dialog

```xml
<jcr:root
    xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
    xmlns:cq="http://www.day.com/jcr/cq/1.0"
    xmlns:jcr="http://www.jcp.org/jcr/1.0"
    jcr:primaryType="nt:unstructured"
    sling:resourceType="cq/gui/components/authoring/dialog">
</jcr:root>
```

---

# TextField ⭐⭐⭐⭐⭐

Most commonly used field.

```xml
<textfield
    sling:resourceType="granite/ui/components/coral/foundation/form/textfield"
    fieldLabel="Title"
    name="./title"/>
```

Author enters:

```text
Adobe AEM
```

JCR:

```text
title = Adobe AEM
```

HTL:

```html
<h2>${properties.title}</h2>
```

Output:

```html
<h2>Adobe AEM</h2>
```

---

# TextArea

```xml
<textarea
    sling:resourceType="granite/ui/components/coral/foundation/form/textarea"
    fieldLabel="Description"
    name="./description"/>
```

Used for longer text.

---

# Checkbox

```xml
<checkbox
    sling:resourceType="granite/ui/components/coral/foundation/form/checkbox"
    fieldLabel="Show Button"
    name="./showButton"
    value="{Boolean}true"/>
```

HTL:

```html
<sly data-sly-test="${properties.showButton}">
    <button>Buy Now</button>
</sly>
```

---

# Select (Dropdown)

```xml
<select
    sling:resourceType="granite/ui/components/coral/foundation/form/select"
    fieldLabel="Theme"
    name="./theme">

    <items jcr:primaryType="nt:unstructured">

        <light
            text="Light"
            value="light"/>

        <dark
            text="Dark"
            value="dark"/>

    </items>

</select>
```

JCR:

```text
theme = dark
```

---

# NumberField

```xml
<numberfield
    sling:resourceType="granite/ui/components/coral/foundation/form/numberfield"
    fieldLabel="Price"
    name="./price"/>
```

---

# PathField ⭐⭐⭐⭐⭐

Used to select a page, asset, or folder.

```xml
<pathfield
    sling:resourceType="granite/ui/components/coral/foundation/form/pathfield"
    fieldLabel="Page Path"
    name="./pagePath"
    rootPath="/content"/>
```

Author selects:

```text
/content/mysite/en/home
```

---

# FileUpload

```xml
<fileupload
    sling:resourceType="cq/gui/components/authoring/dialog/fileupload"
    fieldLabel="Image"
    name="./fileReference"/>
```

Stores a reference to an uploaded asset.

---

# Date Picker

```xml
<datepicker
    sling:resourceType="granite/ui/components/coral/foundation/form/datepicker"
    fieldLabel="Publish Date"
    name="./publishDate"/>
```

---

# Radio Group

```xml
<radiogroup
    sling:resourceType="granite/ui/components/coral/foundation/form/radiogroup"
    name="./alignment">

    <items>

        <left text="Left" value="left"/>

        <right text="Right" value="right"/>

    </items>

</radiogroup>
```

---

# Multifield ⭐⭐⭐⭐⭐

Allows multiple values.

Example:

```text
Author Adds

Phone

Laptop

TV
```

Dialog:

```xml
<multifield
    sling:resourceType="granite/ui/components/coral/foundation/form/multifield"
    fieldLabel="Products">
```

JCR:

```text
products

    0 = Phone

    1 = Laptop

    2 = TV
```

---

# Composite Multifield ⭐⭐⭐⭐⭐

Used for complex data.

Example:

```text
Employee

↓

Name

Email

Phone
```

Each entry contains multiple fields.

This is heavily used in enterprise projects.

---

# Tabs

```text
General

SEO

Advanced
```

Dialog structure:

```xml
<tabs
    sling:resourceType="granite/ui/components/coral/foundation/tabs">
```

Improves organization for large dialogs.

---

# Validation

Required field:

```xml
required="{Boolean}true"
```

Pattern:

```xml
validation="foundation.jcr.name"
```

---

# Show/Hide Fields

Example:

Checkbox:

```text
Enable Banner
```

If checked:

```text
Banner Title

Banner Image
```

If unchecked:

Hidden

This is commonly implemented with Coral UI and JavaScript.

---

# Real Hero Component Dialog

Fields:

```text
Title

Description

Image

Button Text

Button Link

Theme

Show Button
```

---

# Repository After Authoring

```text
hero

    title = Welcome

    description = Learn AEM

    buttonText = Explore

    buttonLink = /content/mysite/en

    showButton = true
```

---

# Sling Model

```java
@Model(adaptables = Resource.class)
public class HeroModel {

    @ValueMapValue
    private String title;

    @ValueMapValue
    private String buttonText;

    @ValueMapValue
    private Boolean showButton;

    public String getTitle() {
        return title;
    }

    public String getButtonText() {
        return buttonText;
    }

    public Boolean getShowButton() {
        return showButton;
    }
}
```

---

# HTL

```html
<sly data-sly-use.model=
"com.mysite.core.models.HeroModel"/>

<h1>${model.title}</h1>

<sly data-sly-test="${model.showButton}">
    <button>${model.buttonText}</button>
</sly>
```

---

# Complete Flow

```text
Author

↓

Granite Dialog

↓

JCR

↓

Sling Model

↓

HTL

↓

HTML

↓

Browser
```

---

# Best Practices

✅ Use meaningful field names.

✅ Group fields using Tabs.

✅ Use Multifield for repeatable content.

✅ Validate required fields.

✅ Use PathField instead of free-text paths.

✅ Keep dialogs simple and author-friendly.

---

# Common Mistakes

❌ Hardcoding values.

❌ Creating very large dialogs without tabs.

❌ Using TextField instead of PathField for repository paths.

❌ Storing unnecessary data.

---

# Interview Questions

### 1. What is a Granite UI Dialog?

A Granite UI Dialog is the authoring interface used to configure AEM components.

---

### 2. Where is the dialog stored?

```text
/apps/<project>/components/<component>/_cq_dialog/.content.xml
```

---

### 3. What is the purpose of `name="./title"`?

It stores the entered value as a property named `title` under the component's JCR node.

---

### 4. What is a Multifield?

A field that allows authors to add multiple values or entries dynamically.

---

### 5. What is a Composite Multifield?

A Multifield where each item contains multiple child fields, such as Name, Email, and Phone.

---

### 6. Why use PathField?

It allows authors to browse and select valid repository paths instead of typing them manually, reducing errors.

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"How do component data and dialogs work together in AEM?"**

A strong answer is:

```text
Granite UI Dialog
        │
        ▼
Author Enters Data
        │
        ▼
JCR Properties
        │
        ▼
Sling Model
        │
        ▼
HTL
        │
        ▼
Rendered HTML
```

Explain that:

* The **dialog** collects input.
* AEM stores the values in the **JCR repository**.
* The **Sling Model** reads those properties.
* **HTL** renders the values on the page.

This is the complete lifecycle of an AEM component and is one of the most frequently asked interview topics.

---

## 🎯 Next Chapter: Core Components Customization ⭐⭐⭐⭐⭐

We'll cover:

* Proxy Components
* `sling:resourceSuperType`
* Extending Core Components
* Custom Sling Models
* Custom HTL
* Style System
* Policies
* Real enterprise customization examples
* Best practices
* Interview questions

This is the standard approach for customizing Adobe Core Components in enterprise AEM projects.
Excellent! Now we'll learn **Core Components Customization**, which is one of the **most important topics for experienced AEM developers (3–10 years)**.

> **Interview Question:** *"Do you create components from scratch or extend Core Components?"*

The expected answer in most enterprise projects is:

> **"We extend Adobe Core Components using Proxy Components and `sling:resourceSuperType` instead of copying them."**

---

# Chapter 12: Core Components Customization (Beginner → Advanced) ⭐⭐⭐⭐⭐

---

# What are Core Components?

Core Components are Adobe-provided reusable AEM components that follow best practices.

Examples:

```text
Title
Text
Image
Button
Teaser
List
Accordion
Carousel
Tabs
Navigation
Breadcrumb
Search
Language Navigation
Experience Fragment
PDF Viewer
```

---

# Why Use Core Components?

Without Core Components:

```text
Developer

↓

Creates Everything

↓

More Bugs

↓

More Maintenance
```

With Core Components:

```text
Adobe Core Component

↓

Customize

↓

Deploy
```

Benefits:

* Adobe-supported
* Accessible (WCAG)
* Responsive
* SEO-friendly
* Cloud-ready
* Easier upgrades

---

# Core Component Location

```text
/libs/core/wcm/components
```

Never modify anything under `/libs`.

---

# Correct Approach

```text
/apps/mysite/components

↓

Proxy Component

↓

sling:resourceSuperType

↓

Core Component
```

---

# Proxy Component

A Proxy Component references a Core Component instead of copying it.

Example:

```text
/apps/mysite/components/title
```

`.content.xml`

```xml
<jcr:root
    jcr:primaryType="cq:Component"
    sling:resourceSuperType="core/wcm/components/title/v3/title"/>
```

---

# Architecture

```text
Browser

↓

Proxy Component

↓

Core Component

↓

Rendered HTML
```

---

# What is `sling:resourceSuperType`?

It tells Sling:

> "If my component doesn't have something, inherit it from another component."

Example:

```xml
sling:resourceSuperType="core/wcm/components/title/v3/title"
```

This means:

```text
My Title Component

↓

Core Title Component
```

---

# Folder Structure

```text
/apps

└── mysite

    └── components

        └── title

            ├── .content.xml
            ├── title.html
            └── _cq_dialog
```

---

# Reusing Core HTL

If you don't override `title.html`, AEM automatically uses the Core Component's HTL.

---

# Overriding HTL

You can customize only the markup.

Example:

```html
<sly
data-sly-resource="${resource
@ resourceType='core/wcm/components/title/v3/title'}"/>

<div class="custom-border"></div>
```

This wraps the Core Title component with extra HTML.

---

# Extending the Dialog

You can add extra authoring fields.

Example:

```xml
<textfield
    sling:resourceType="granite/ui/components/coral/foundation/form/textfield"
    fieldLabel="Subtitle"
    name="./subtitle"/>
```

Now the dialog contains:

```text
Title

Subtitle
```

---

# Custom Sling Model

```java
@Model(
    adaptables = Resource.class,
    adapters = Title.class
)
public class CustomTitleModel {

    @ValueMapValue
    private String subtitle;

    public String getSubtitle() {
        return subtitle;
    }
}
```

---

# HTL

```html
<h1>${properties.jcr:title}</h1>

<h3>${properties.subtitle}</h3>
```

Output:

```html
<h1>Adobe AEM</h1>

<h3>Learning Platform</h3>
```

---

# Style System ⭐⭐⭐⭐⭐

Instead of creating multiple components:

```text
Blue Title

Red Title

Large Title

Small Title
```

Create one Title component.

Author chooses:

```text
Blue

Red

Large

Small
```

using the **Style System**.

---

# Component Policies

Policies define:

* Allowed Styles
* Allowed Components
* Default CSS Classes

Location:

```text
Template

↓

Policy

↓

Component
```

---

# Resource Inheritance

```text
Proxy Component

↓

Looks for HTL

↓

If Missing

↓

Core Component HTL
```

Same for:

* Dialogs
* Models
* Scripts

---

# Example: Image Component

Instead of creating a new image component:

```text
Core Image

↓

Proxy

↓

Rounded Corners

↓

Shadow

↓

Lazy Loading
```

---

# Example: Teaser Component

Core Component:

```text
Image

Title

Description

Button
```

Custom Version:

```text
Image

Title

Description

Button

Rating ⭐⭐⭐⭐⭐

Price ₹
```

Only extend what you need.

---

# Custom CSS

ClientLib

```css
.custom-title{

color:blue;

border-left:5px solid red;

padding-left:10px;

}
```

HTL

```html
<div class="custom-title">

<sly
data-sly-resource="${resource
@ resourceType='core/wcm/components/title/v3/title'}"/>

</div>
```

---

# Request Flow

```text
Browser

↓

HTL

↓

Proxy Component

↓

Core Component

↓

Sling Model

↓

JCR

↓

HTML
```

---

# Real Enterprise Example

Corporate Website

```text
Core Teaser

↓

Proxy Component

↓

Additional CTA

↓

Analytics Tracking

↓

Custom CSS

↓

Deployment
```

This avoids duplicating Adobe's implementation.

---

# Best Practices

✅ Always create **Proxy Components**.

✅ Never copy components from `/libs`.

✅ Use `sling:resourceSuperType`.

✅ Customize only what's required.

✅ Reuse Core Component dialogs whenever possible.

---

# Common Mistakes

❌ Copying Core Components into `/apps`.

❌ Editing `/libs`.

❌ Rewriting Adobe functionality unnecessarily.

❌ Creating duplicate components for styling differences.

---

# Core Components vs Custom Components

| Core Components  | Custom Components         |
| ---------------- | ------------------------- |
| Adobe-supported  | Fully custom              |
| Upgrade-friendly | More maintenance          |
| Accessible       | Depends on implementation |
| Recommended      | Use only when needed      |

---

# Interview Questions

### 1. What are Core Components?

Adobe-provided reusable AEM components built with best practices.

---

### 2. What is a Proxy Component?

A custom component that references a Core Component using `sling:resourceSuperType`.

---

### 3. Why shouldn't you modify `/libs`?

Because `/libs` is managed by Adobe and can be overwritten during upgrades.

---

### 4. What is `sling:resourceSuperType`?

It enables inheritance from another component, allowing customization without copying the original.

---

### 5. Why use the Style System?

To offer multiple visual styles for the same component without creating duplicate components.

---

### 6. How do you customize a Core Component?

Typical approach:

1. Create a Proxy Component.
2. Set `sling:resourceSuperType`.
3. Extend the dialog if needed.
4. Add a Sling Model if additional data is required.
5. Override or wrap the HTL only when necessary.
6. Add custom CSS/JavaScript through ClientLibs.

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"How do you customize the Core Teaser component?"**

A strong answer is:

```text
Core Teaser

↓

Create Proxy Component

↓

Set sling:resourceSuperType

↓

Extend Dialog

↓

Add Custom Sling Model

↓

Customize HTL

↓

Add ClientLib CSS/JS
```

Then explain:

* You **do not copy** the Core Component.
* You inherit from it using `sling:resourceSuperType`.
* You only add the extra functionality (for example, a subtitle, badge, rating, or analytics attributes).
* This approach keeps the component compatible with future Adobe upgrades.

This is exactly how enterprise AEM projects are expected to customize Core Components.

---

# 🎯 Next Chapter: Editable Templates & Template Policies ⭐⭐⭐⭐⭐

In the next chapter, we'll cover:

* Editable Templates
* Template Types
* Initial Content
* Structure
* Policies
* Layout Container
* Responsive Grid
* Allowed Components
* Style System
* Template Editor
* Real enterprise examples
* Complete interview questions

**Editable Templates are one of the most frequently asked AEM interview topics** because nearly all modern AEM projects use them instead of Static Templates.
Excellent! Now we'll learn one of the **most important AEM topics**.

# Chapter 13: Editable Templates & Template Policies (Beginner → Advanced) ⭐⭐⭐⭐⭐

> **Interview Question:** *"What is the difference between Static Templates and Editable Templates?"*

Almost every AEM interview asks this.

---

# What are Editable Templates?

An **Editable Template** allows authors (not developers) to create and modify page templates using the AEM Template Editor.

Instead of developers creating new templates in code every time, authors can configure templates themselves.

---

# Evolution of Templates

## Static Templates (Old)

```text
Developer

↓

Create Template

↓

Deploy Code

↓

Author Uses Template
```

Every template change required a deployment.

---

## Editable Templates (Modern)

```text
Developer

↓

Creates Template Type

↓

Author Creates Editable Template

↓

No Deployment Required
```

Much more flexible.

---

# Editable Template Architecture

```text
Author

↓

Template Editor

↓

Editable Template

↓

Policy

↓

Page

↓

Website
```

---

# Repository Structure

```text
/conf

└── mysite

    ├── settings

    │    └── wcm

    │         ├── templates

    │         └── policies

    │
    └── settings
```

Unlike Static Templates (stored in `/apps`), Editable Templates are stored under `/conf`.

---

# Editable Template Structure

```text
/conf/mysite

↓

templates

↓

homepage-template

│

├── initial

├── structure

├── policies
```

---

# Three Important Parts

## 1. Structure ⭐⭐⭐⭐⭐

Contains locked components.

Example:

```text
Header

Navigation

Footer
```

Authors **cannot delete** these components.

---

## 2. Initial Content

Contains editable default content.

Example:

```text
Welcome Banner

Sample Image

Sample Text
```

Authors can modify or remove this content.

---

## 3. Policies ⭐⭐⭐⭐⭐

Policies define:

* Allowed Components
* Default Styles
* Style System
* Design Configuration

---

# Structure vs Initial Content

| Structure     | Initial Content |
| ------------- | --------------- |
| Locked        | Editable        |
| Cannot delete | Can modify      |
| Header/Footer | Banner/Text     |

---

# Template Editor

Go to:

```text
Tools

↓

General

↓

Templates
```

Here authors can:

* Create templates
* Edit templates
* Assign policies
* Configure layouts

---

# Template Type

A **Template Type** acts as a blueprint.

Example:

```text
Basic Page

↓

Homepage Template

↓

Landing Page Template

↓

Product Template
```

---

# Creating a Template

Flow:

```text
Template Type

↓

Create Editable Template

↓

Add Structure

↓

Assign Policies

↓

Enable Template

↓

Create Pages
```

---

# Layout Container

The Layout Container is the main editable area.

```text
Header

↓

Layout Container

↓

Footer
```

Authors drag and drop components into the Layout Container.

---

# Allowed Components

Example:

```text
Allowed Components

↓

Title

Image

Text

Carousel

Button

Teaser
```

If a component is not allowed by the policy, authors cannot add it.

---

# Style System ⭐⭐⭐⭐⭐

Instead of multiple components:

```text
Blue Button

Red Button

Green Button
```

Use one Button component.

Policy provides styles:

```text
Primary

Secondary

Outline
```

Authors choose the style in the page editor.

---

# Responsive Grid

Editable Templates support responsive layouts.

Desktop

```text
+--------+--------+
| Card 1 | Card 2 |
+--------+--------+
```

Mobile

```text
+--------+
| Card 1 |
+--------+
| Card 2 |
+--------+
```

No separate template is required.

---

# Page Creation Flow

```text
Author

↓

Create Page

↓

Choose Template

↓

Page Created

↓

Edit Content

↓

Publish
```

---

# Example: Homepage Template

Structure

```text
Header

Navigation

Footer
```

Initial Content

```text
Hero Banner

Welcome Text
```

Allowed Components

```text
Title

Image

Button

Carousel

Teaser
```

---

# Template Policies

Policies control:

* Allowed Components
* CSS Classes
* Responsive Settings
* Style System Options
* Default Values

Example:

```text
Policy

↓

Title Component

↓

Styles

Large

Medium

Small
```

Authors select the style without changing code.

---

# Real Enterprise Example

Corporate Website

```text
Homepage Template

↓

Header (Locked)

↓

Navigation (Locked)

↓

Layout Container (Editable)

↓

Footer (Locked)
```

Marketing authors can edit the page without affecting the site structure.

---

# Static vs Editable Templates

| Static Template     | Editable Template |
| ------------------- | ----------------- |
| Stored in `/apps`   | Stored in `/conf` |
| Developer changes   | Author changes    |
| Deployment required | No deployment     |
| Less flexible       | Highly flexible   |
| Legacy approach     | Adobe recommended |

---

# Best Practices

✅ Use Editable Templates for all new projects.

✅ Keep global elements in **Structure**.

✅ Put sample content in **Initial Content**.

✅ Configure Policies instead of creating duplicate components.

✅ Use the Style System for visual variations.

---

# Common Mistakes

❌ Creating many similar templates instead of using policies.

❌ Putting editable content into the Structure section.

❌ Allowing too many components on every template.

❌ Creating duplicate components for styling differences.

---

# Interview Questions

### 1. What are Editable Templates?

Editable Templates allow authors to create and configure page templates without requiring code deployments.

---

### 2. Where are Editable Templates stored?

```text
/conf/<project>/settings/wcm/templates
```

---

### 3. What is the difference between Structure and Initial Content?

* **Structure** contains locked components.
* **Initial Content** contains editable default content.

---

### 4. What are Policies?

Policies define:

* Allowed Components
* Style System options
* Default configurations
* Responsive behavior

---

### 5. What is a Layout Container?

A component that allows authors to drag and drop other components into the page.

---

### 6. Why are Editable Templates preferred?

* No deployment for template changes.
* More flexibility for authors.
* Easier maintenance.
* Better support for reusable policies and styles.

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"Explain the lifecycle of an Editable Template."**

A strong answer is:

```text
Developer

↓

Creates Template Type

↓

Author Creates Editable Template

↓

Configures Structure

↓

Assigns Policies

↓

Enables Template

↓

Creates Pages

↓

Authors Edit Content

↓

Publish
```

Then explain:

* The developer creates the reusable template type.
* The author creates an editable template from that type.
* Locked content goes into **Structure**.
* Default editable content goes into **Initial Content**.
* Policies define what authors can do.
* Pages created from the template inherit this configuration.

This demonstrates a solid understanding of modern AEM authoring and is a very common enterprise interview topic.

---

# 🎯 Next Chapter: SPA Editor & React Integration ⭐⭐⭐⭐⭐

We'll cover:

* What SPA Editor is.
* Why React is used with AEM.
* SPA Architecture.
* Editable React Components.
* React Mapping.
* Model Manager.
* JSON Model Exporter.
* GraphQL integration.
* Routing.
* Real enterprise examples.
* Complete interview questions.

This chapter is especially valuable if you're targeting **AEM Full Stack Developer** roles that use **React with AEM**.
