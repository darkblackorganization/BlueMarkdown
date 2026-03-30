# CSS Cheat Sheet

## Introduction

**CSS** (Cascading Style Sheets) is a stylesheet language used to describe the **visual presentation** of HTML documents. Created by **Håkon Wium Lie** and released in **1996**, CSS separates content (HTML) from design (CSS). It controls layout, colors, fonts, spacing, animations, and responsiveness. The "cascading" in CSS means that multiple style rules can apply to one element — specificity and order determine which one wins. The current standard is **CSS3**, which introduced features like Flexbox, Grid, animations, variables, and media queries.

---

## Table of Contents

1. [Basic Syntax](#basic-syntax)
2. [Selectors](#selectors)
3. [Combinators](#combinators)
4. [Pseudo-classes](#pseudo-classes)
5. [Pseudo-elements](#pseudo-elements)
6. [Specificity & Cascade](#specificity--cascade)
7. [CSS Variables (Custom Properties)](#css-variables-custom-properties)
8. [Colors](#colors)
9. [Units & Values](#units--values)
10. [Box Model](#box-model)
11. [Display](#display)
12. [Positioning](#positioning)
13. [Flexbox](#flexbox)
14. [CSS Grid](#css-grid)
15. [Typography](#typography)
16. [Backgrounds](#backgrounds)
17. [Borders](#borders)
18. [Shadows](#shadows)
19. [Overflow](#overflow)
20. [Opacity & Visibility](#opacity--visibility)
21. [Transforms](#transforms)
22. [Transitions](#transitions)
23. [Animations](#animations)
24. [Responsive Design & Media Queries](#responsive-design--media-queries)
25. [Filters](#filters)
26. [Gradients](#gradients)
27. [Object Fit & Object Position](#object-fit--object-position)
28. [Scroll Behavior](#scroll-behavior)
29. [Clipping & Masking](#clipping--masking)
30. [CSS Functions](#css-functions)
31. [At-Rules](#at-rules)
32. [Logical Properties](#logical-properties)
33. [Container Queries](#container-queries)
34. [Useful Snippets](#useful-snippets)
35. [Best Practices](#best-practices)

---

## Basic Syntax

**Definition:** A CSS rule consists of a selector and a declaration block containing property-value pairs.

### Rule Structure
**Definition:** Every CSS rule follows the same format — selector, then declarations inside curly braces.
```css
selector {
    property: value;
    property: value;
}

/* Example */
h1 {
    color: navy;
    font-size: 32px;
    margin-bottom: 16px;
}
```

### Where to Write CSS
**Definition:** Three ways to add CSS to a page — external file is the recommended approach.
```html
<!-- 1. External stylesheet — recommended -->
<link rel="stylesheet" href="styles.css">

<!-- 2. Internal style block — in <head> -->
<style>
  h1 { color: red; }
</style>

<!-- 3. Inline style — on the element -->
<h1 style="color: red; font-size: 24px;">Hello</h1>
```

### Comments
**Definition:** CSS comments are ignored by the browser — use them to explain your code.
```css
/* This is a single-line comment */

/*
 * This is a
 * multi-line comment
 */

.button {
    color: white;        /* Text color */
    background: blue;    /* Button background */
}
```

### Shorthand Properties
**Definition:** Many properties have shorthand versions that set multiple related values at once.
```css
/* Longhand */
margin-top:    10px;
margin-right:  20px;
margin-bottom: 10px;
margin-left:   20px;

/* Shorthand — top right bottom left (clockwise) */
margin: 10px 20px 10px 20px;

/* Two values — vertical horizontal */
margin: 10px 20px;

/* One value — all sides */
margin: 10px;

/* Border shorthand */
border: 2px solid #333;         /* width style color */

/* Background shorthand */
background: url(img.jpg) no-repeat center / cover;

/* Font shorthand */
font: italic bold 16px/1.5 Arial, sans-serif;
/* style weight size/line-height family */

/* Transition shorthand */
transition: all 0.3s ease-in-out;
/* property duration timing-function */
```

---

## Selectors

**Definition:** Selectors target which HTML elements the styles apply to.

### Type & Universal
**Definition:** Select elements by tag name or select all elements.
```css
p    { color: gray; }        /* All <p> elements */
h1   { font-size: 2rem; }   /* All <h1> elements */
div  { display: block; }     /* All <div> elements */
*    { box-sizing: border-box; }  /* ALL elements */
```

### Class & ID
**Definition:** Class targets multiple elements, ID targets exactly one unique element.
```css
.card      { border: 1px solid #ddd; }   /* class="card" */
.btn       { padding: 8px 16px; }         /* class="btn" */
#header    { background: navy; }          /* id="header" */
#main-nav  { position: sticky; }         /* id="main-nav" */

/* Multiple classes on one element */
.btn.btn-primary { background: blue; }   /* class="btn btn-primary" */
```

### Attribute Selectors
**Definition:** Target elements based on their HTML attributes and attribute values.
```css
[href]              { color: blue; }      /* Has href attribute */
[type="text"]       { border: 1px solid; }/* type exactly "text" */
[class~="card"]     { padding: 1rem; }    /* class contains word "card" */
[lang|="en"]        { font: serif; }      /* lang is "en" or starts "en-" */
[href^="https"]     { color: green; }     /* href starts with "https" */
[href$=".pdf"]      { color: red; }       /* href ends with ".pdf" */
[href*="example"]   { font-style: italic; } /* href contains "example" */
[disabled]          { opacity: 0.5; }     /* Has disabled attribute */

/* Case-insensitive flag */
[type="text" i]     { border: 1px solid; }  /* Matches TEXT, text, Text */
```

### Group Selector
**Definition:** Apply the same styles to multiple selectors separated by commas.
```css
h1, h2, h3, h4 {
    font-family: Georgia, serif;
    color: #333;
}

.btn-primary,
.btn-secondary,
.btn-danger {
    padding: 8px 16px;
    border-radius: 4px;
    cursor: pointer;
}
```

---

## Combinators

**Definition:** Combine selectors to target elements based on their relationship in the HTML structure.

### Descendant Combinator (space)
**Definition:** Target any descendant element — regardless of how deeply nested.
```css
/* Any <a> inside a <nav>, at any depth */
nav a { color: white; }

/* Any <p> inside .card */
.card p { margin-bottom: 1rem; }
```

### Child Combinator (>)
**Definition:** Target only direct children — not grandchildren or deeper.
```css
/* Only direct <li> children of <ul> */
ul > li { list-style: disc; }

/* Only direct children of .menu */
.menu > .menu-item { display: flex; }
```

### Adjacent Sibling (+)
**Definition:** Target the immediately following sibling element.
```css
/* <p> that immediately follows an <h2> */
h2 + p { font-size: 1.1rem; font-style: italic; }

/* Input directly after a label */
label + input { margin-left: 8px; }
```

### General Sibling (~)
**Definition:** Target all following siblings (not just the immediate one).
```css
/* All <p> elements after an <h2> in the same parent */
h2 ~ p { color: #555; }

/* All siblings after a checked checkbox */
input:checked ~ .panel { display: block; }
```

---

## Pseudo-classes

**Definition:** Select elements based on their state or position — added with `:` prefix.

### Link & Interaction States
**Definition:** Style elements based on user interaction — hover, focus, active, visited.
```css
a:link    { color: blue; }        /* Unvisited link */
a:visited { color: purple; }      /* Already visited */
a:hover   { color: red; }         /* Mouse over */
a:active  { color: orange; }      /* Being clicked */
/* Order matters: LVHA — link, visited, hover, active */

button:hover  { background: darkblue; }
input:focus   { outline: 2px solid blue; }
button:active { transform: scale(0.98); }
:focus-visible { outline: 2px solid blue; }    /* Only keyboard focus */
:focus-within  { background: #f5f5f5; }        /* Container has focused child */
```

### Form States
**Definition:** Style form elements based on their current state.
```css
input:disabled        { opacity: 0.5; cursor: not-allowed; }
input:enabled         { border-color: #333; }
input:required        { border-left: 3px solid red; }
input:optional        { border-left: 3px solid gray; }
input:checked         { accent-color: blue; }
input:valid           { border-color: green; }
input:invalid         { border-color: red; }
input:read-only       { background: #f9f9f9; }
input:read-write      { background: white; }
input:placeholder-shown { border-style: dashed; }
input:blank           { background: #fff3cd; }
```

### Structural Pseudo-classes
**Definition:** Target elements based on their position in the document tree.
```css
:first-child        { font-weight: bold; }     /* First child of its parent */
:last-child         { margin-bottom: 0; }       /* Last child of its parent */
:only-child         { border: 2px solid red; }  /* Only child of its parent */

:first-of-type      { color: blue; }            /* First of its element type */
:last-of-type       { color: red; }             /* Last of its element type */
:only-of-type       { font-style: italic; }     /* Only of its element type */

/* nth-child — powerful positional selector */
:nth-child(1)       { }   /* First child */
:nth-child(2)       { }   /* Second child */
:nth-child(odd)     { background: #f9f9f9; }   /* 1st, 3rd, 5th... */
:nth-child(even)    { background: white; }      /* 2nd, 4th, 6th... */
:nth-child(3n)      { }   /* Every 3rd: 3, 6, 9... */
:nth-child(3n+1)    { }   /* 1, 4, 7, 10... */
:nth-child(-n+3)    { }   /* First 3: 1, 2, 3 */
:nth-child(n+4)     { }   /* From 4th onwards */

:nth-last-child(1)  { }   /* Last child */
:nth-last-child(2)  { }   /* Second to last */

:nth-of-type(2)     { }   /* Second of its type */
:nth-last-of-type(1){ }   /* Last of its type */
```

### Other Useful Pseudo-classes
**Definition:** Additional pseudo-classes for content, emptiness, and negation.
```css
:empty     { display: none; }         /* Element with no children */
:not(.btn) { color: gray; }           /* Anything NOT matching */
:not(:first-child) { border-top: 1px solid #eee; }
:is(h1, h2, h3)   { font-family: serif; }   /* Matches any in list */
:where(.btn, .link){ cursor: pointer; }      /* Like :is() but 0 specificity */
:has(img)          { padding: 0; }           /* Parent containing img */
:has(+ .error)     { border-color: red; }    /* Before an error element */
:root  { --color-primary: #0066cc; }         /* Root element (<html>) */
```

---

## Pseudo-elements

**Definition:** Create virtual elements or target specific parts of an element — added with `::` prefix.

### Content Pseudo-elements
**Definition:** Insert content before or after an element's actual content.
```css
/* Add content before element */
.quote::before {
    content: '"';
    font-size: 2em;
    color: gray;
}

/* Add content after element */
.external-link::after {
    content: ' ↗';
    font-size: 0.8em;
}

/* content values */
::before { content: "text"; }
::before { content: url(icon.svg); }
::before { content: attr(data-label); }   /* Value of HTML attribute */
::before { content: counter(section); }
::before { content: ""; }               /* Empty — for shapes/decorations */
::before { content: none; }             /* Remove content */
```

### Text Pseudo-elements
**Definition:** Target specific parts of text within an element.
```css
/* First letter of a block */
p::first-letter {
    font-size: 3em;
    font-weight: bold;
    float: left;
    margin-right: 8px;
}

/* First line of a block */
p::first-line {
    font-variant: small-caps;
    color: #333;
}

/* User's text selection */
::selection {
    background: #ffeb3b;
    color: #000;
}

/* Placeholder text in inputs */
input::placeholder {
    color: #999;
    font-style: italic;
}

/* Marker of list items */
li::marker {
    color: blue;
    font-size: 1.2em;
}
```

---

## Specificity & Cascade

**Definition:** When multiple rules target the same element, CSS uses specificity and order to determine which wins.

### Specificity Scoring
**Definition:** Each selector type has a weight — higher score wins over lower score.
```
Specificity is calculated as: (A, B, C)
A = Inline styles (style="") — highest
B = IDs (#id)
C = Classes (.class), attributes ([attr]), pseudo-classes (:hover)
D = Elements (div, p) and pseudo-elements (::before) — lowest

Examples:
  *                   → (0, 0, 0, 0)  — zero specificity
  p                   → (0, 0, 0, 1)
  .class              → (0, 0, 1, 0)
  #id                 → (0, 1, 0, 0)
  style=""            → (1, 0, 0, 0)
  p.highlight         → (0, 0, 1, 1)
  #nav .active        → (0, 1, 1, 0)
  #nav .active:hover  → (0, 1, 2, 0)
```

### !important
**Definition:** Overrides ALL specificity — use as a last resort only.
```css
/* Wins over everything including inline styles */
.hidden { display: none !important; }

/* !important specificity order:
   1. Inline !important styles
   2. !important in stylesheets (higher specificity first)
   3. Regular inline styles
   4. Regular stylesheet rules (by specificity) */
```

### Cascade Order
**Definition:** When specificity is equal, the rule that appears LAST in the CSS wins.
```css
/* This applies — comes last */
p { color: red; }
p { color: blue; }     /* Blue wins — declared later */

/* Source order matters across stylesheets too */
/* Stylesheet loaded last wins when specificity is equal */
```

### The `all` Property
**Definition:** Reset all properties of an element to their initial or inherited values.
```css
.reset-all  { all: unset; }      /* Unsets all properties */
.reset-all  { all: initial; }    /* Reset to browser defaults */
.reset-all  { all: inherit; }    /* Inherit all from parent */
.reset-all  { all: revert; }     /* Revert to browser stylesheet */
```

---

## CSS Variables (Custom Properties)

**Definition:** Store values in named variables — reuse them throughout the stylesheet and update globally.

### Define & Use Variables
**Definition:** Declare with `--` prefix in a selector, use with `var()` function.
```css
/* Define on :root for global access */
:root {
    --color-primary:    #0066cc;
    --color-secondary:  #6c757d;
    --color-success:    #28a745;
    --color-danger:     #dc3545;
    --color-background: #f8f9fa;
    --color-text:       #212529;

    --font-size-base:   16px;
    --font-size-sm:     14px;
    --font-size-lg:     18px;
    --font-family:      'Inter', sans-serif;

    --spacing-xs:  4px;
    --spacing-sm:  8px;
    --spacing-md:  16px;
    --spacing-lg:  24px;
    --spacing-xl:  48px;

    --border-radius:    8px;
    --border-color:     #dee2e6;
    --shadow:           0 2px 4px rgba(0,0,0,0.1);
}

/* Use variables */
.button {
    background: var(--color-primary);
    color: white;
    padding: var(--spacing-sm) var(--spacing-md);
    border-radius: var(--border-radius);
    font-size: var(--font-size-base);
}

/* With fallback value */
.card {
    background: var(--card-background, white);   /* Falls back to white */
    border: 1px solid var(--border-color, #ccc);
}
```

### Scoped Variables
**Definition:** Override variables locally — the new value only applies within that scope.
```css
/* Global */
:root { --color-primary: #0066cc; }

/* Override in a component */
.dark-theme {
    --color-primary:    #4da6ff;
    --color-background: #1a1a2e;
    --color-text:       #e0e0e0;
}

/* JavaScript can update variables */
/* document.documentElement.style.setProperty('--color-primary', '#ff0000'); */
```

### Calculated Variables
**Definition:** Use `calc()` with variables for flexible computed values.
```css
:root {
    --base-size:    16px;
    --spacing-unit: 8px;
}

.container {
    padding:  calc(var(--spacing-unit) * 2);    /* 16px */
    font-size: calc(var(--base-size) * 1.5);    /* 24px */
    max-width: calc(100% - var(--spacing-unit) * 4);
}
```

---

## Colors

**Definition:** CSS supports many color formats — choose based on what you need (named, opacity, dynamism).

### Color Formats
**Definition:** Different ways to specify colors — each with different capabilities.
```css
/* Named colors */
color: red;
color: tomato;
color: steelblue;
color: transparent;

/* Hex — #RRGGBB */
color: #ff0000;      /* Red */
color: #000;         /* Black (shorthand #RGB) */
color: #fff;         /* White */
color: #0066cc;      /* Blue */

/* Hex with alpha — #RRGGBBAA */
color: #ff0000ff;    /* Fully opaque red */
color: #ff000080;    /* 50% transparent red */

/* RGB */
color: rgb(255, 0, 0);         /* Red */
color: rgb(0 128 255);         /* Modern syntax (no commas) */

/* RGBA — with alpha (0=transparent, 1=opaque) */
color: rgba(0, 0, 0, 0.5);    /* 50% transparent black */
color: rgba(0 0 0 / 50%);     /* Modern syntax */

/* HSL — hue saturation lightness */
color: hsl(210, 100%, 50%);    /* Blue */
color: hsl(0, 100%, 50%);      /* Red */
color: hsl(120, 60%, 40%);     /* Green */

/* HSLA — with alpha */
color: hsla(210, 100%, 50%, 0.8);
color: hsl(210 100% 50% / 80%);   /* Modern syntax */

/* oklch — perceptual color (modern) */
color: oklch(60% 0.2 240);     /* Lightness chroma hue */

/* currentColor — inherits current text color */
border: 2px solid currentColor;
fill: currentColor;
```

---

## Units & Values

**Definition:** CSS values use different units depending on what you're measuring — absolute or relative.

### Absolute Units
**Definition:** Fixed sizes that don't change based on context.
```css
/* Pixels — most common absolute unit */
font-size: 16px;
margin: 24px;

/* Print units (rarely used on screen) */
width:  10cm;    /* Centimeters */
height: 5in;     /* Inches */
margin: 10mm;    /* Millimeters */
font-size: 12pt; /* Points (1pt = 1/72 inch) */
```

### Relative Units
**Definition:** Size relative to something else — viewport, parent, or root element.
```css
/* Font-relative */
font-size: 1.5em;      /* Relative to parent font-size */
font-size: 1.5rem;     /* Relative to root (html) font-size */
line-height: 1.6;      /* Unitless — relative to element's font-size */

/* Viewport units */
width:  100vw;   /* 100% of viewport width */
height: 100vh;   /* 100% of viewport height */
width:  50vw;    /* 50% of viewport width */
font-size: 5vw;  /* 5% of viewport width */

/* Modern viewport units (avoid scroll bar issues) */
height: 100dvh;  /* Dynamic viewport height */
height: 100svh;  /* Small viewport height */
height: 100lvh;  /* Large viewport height */

/* Percentage */
width:  50%;     /* 50% of parent width */
height: 100%;    /* 100% of parent height */
margin: 5%;      /* 5% of containing block */

/* Character units */
width:  20ch;    /* Width of 20 "0" characters */
width:  60ex;    /* Height of lowercase "x" */

/* Container-based (modern) */
width:  50cqw;   /* 50% of container query width */
```

### Calc & Math Functions
**Definition:** Perform math operations with mixed units — extremely powerful for responsive layouts.
```css
/* calc() — mix any units */
width:  calc(100% - 48px);
height: calc(100vh - 64px);
font-size: calc(16px + 0.5vw);
padding: calc(var(--spacing) * 2);

/* min() — use the smaller value */
width: min(500px, 90%);         /* Never wider than 500px or 90% */
font-size: min(3vw, 24px);      /* Never larger than 24px */

/* max() — use the larger value */
width: max(200px, 30%);         /* Never narrower than 200px */

/* clamp(min, preferred, max) — fluid sizing */
font-size: clamp(14px, 2vw, 20px);     /* Between 14px and 20px */
width:     clamp(300px, 50%, 800px);   /* Between 300px and 800px */
```

---

## Box Model

**Definition:** Every element is a box with content, padding, border, and margin — understanding this is fundamental.

### Box Model Properties
**Definition:** The four layers of the CSS box model from inside to outside.
```css
.box {
    /* Content area */
    width:  200px;
    height: 100px;

    /* Padding — space INSIDE the border */
    padding:        20px;            /* All sides */
    padding-top:    10px;
    padding-right:  20px;
    padding-bottom: 10px;
    padding-left:   20px;
    padding:        10px 20px;       /* Vertical horizontal */
    padding:        10px 15px 20px;  /* Top h-sides bottom */

    /* Border — the element's outline */
    border:        2px solid #333;
    border-top:    3px dashed red;
    border-right:  0;
    border-width:  2px;
    border-style:  solid;
    border-color:  #333;

    /* Margin — space OUTSIDE the border */
    margin:        20px;
    margin-top:    10px;
    margin:        0 auto;   /* Center horizontally */
    margin-left:   auto;
    margin-right:  auto;
}
```

### Box Sizing
**Definition:** `border-box` makes width/height include padding and border — strongly recommended to use always.
```css
/* Default — content-box: width = content only */
/* padding + border ADDED to the width */
.content-box {
    box-sizing: content-box;
    width: 200px;
    padding: 20px;
    /* Total width = 200 + 40 = 240px */
}

/* border-box — width = content + padding + border */
/* padding + border INCLUDED in the width */
.border-box {
    box-sizing: border-box;
    width: 200px;
    padding: 20px;
    /* Total width = 200px (content shrinks to 160px) */
}

/* Apply border-box to everything — universal reset */
*, *::before, *::after {
    box-sizing: border-box;
}
```

### Margin Collapse
**Definition:** Vertical margins between adjacent elements collapse to the larger of the two values.
```css
/* These two paragraphs share a collapsed margin */
p { margin: 20px 0; }

/* Between two 20px margins, you get 20px (not 40px) */
/* Ways to prevent collapse: */
.prevent-collapse {
    overflow: hidden;    /* Or auto */
    display: flex;
    padding-top: 1px;
    border-top: 1px solid transparent;
}
```

---

## Display

**Definition:** The `display` property controls how an element generates its box and how it interacts with siblings.

### Display Values
**Definition:** Each value changes how the element participates in layout.
```css
display: block;           /* Full width, starts on new line (div, p, h1) */
display: inline;          /* Flows with text, no width/height (span, a, em) */
display: inline-block;    /* Flows inline but accepts width/height */
display: none;            /* Hidden completely — takes no space */
display: flex;            /* Flexbox container */
display: inline-flex;     /* Inline flexbox container */
display: grid;            /* Grid container */
display: inline-grid;     /* Inline grid container */
display: table;           /* Behaves like <table> */
display: table-cell;      /* Behaves like <td> */
display: list-item;       /* Behaves like <li> */
display: contents;        /* Element itself invisible, children remain */
```

### Visibility vs Display
**Definition:** `display: none` removes from layout — `visibility: hidden` hides but keeps space.
```css
.removed  { display: none; }       /* Gone — no space, no interaction */
.hidden   { visibility: hidden; }  /* Invisible — space reserved */
.zero-size { opacity: 0; }         /* Invisible — space reserved, events work */
```

---

## Positioning

**Definition:** Control where elements are placed on the page — relative to their normal position, parent, or viewport.

### Position Values
**Definition:** Five position modes — each changes what the offset properties (`top`, `left`, etc.) are relative to.
```css
/* static — default, no offset properties */
position: static;

/* relative — offset from its normal position, still in flow */
position: relative;
top:  10px;
left: 20px;

/* absolute — removed from flow, positioned relative to nearest positioned ancestor */
position: absolute;
top:    0;
right:  0;
bottom: 0;
left:   0;

/* fixed — removed from flow, positioned relative to VIEWPORT */
position: fixed;
top:   0;
left:  0;
width: 100%;

/* sticky — relative until scroll threshold, then fixed */
position: sticky;
top: 0;      /* Sticks to top when page scrolls past this point */
```

### Z-index
**Definition:** Control stacking order — higher value appears in front.
```css
.modal    { z-index: 1000; }    /* In front */
.overlay  { z-index: 999; }     /* Behind modal */
.header   { z-index: 100; }     /* Behind overlay */
.content  { z-index: 1; }       /* Normal content */

/* z-index only works on positioned elements (not static) */
/* z-index: auto — uses parent's stacking context */
```

### Common Centering with Position
**Definition:** Center an absolute element within its positioned parent.
```css
/* Center absolutely positioned element */
.parent { position: relative; }

.child {
    position: absolute;
    top:  50%;
    left: 50%;
    transform: translate(-50%, -50%);
}

/* Modern: inset shorthand */
.fill-parent {
    position: absolute;
    inset: 0;     /* top: 0; right: 0; bottom: 0; left: 0; */
}
```

---

## Flexbox

**Definition:** A one-dimensional layout system for arranging items in a row or column with flexible sizing.

### Flex Container Properties
**Definition:** Properties applied to the parent element to control how children are laid out.
```css
.container {
    display: flex;            /* Enable flexbox */

    /* Direction */
    flex-direction: row;           /* Default — left to right */
    flex-direction: row-reverse;   /* Right to left */
    flex-direction: column;        /* Top to bottom */
    flex-direction: column-reverse;/* Bottom to top */

    /* Wrap */
    flex-wrap: nowrap;      /* Default — single line */
    flex-wrap: wrap;        /* Wrap to multiple lines */
    flex-wrap: wrap-reverse;/* Wrap in reverse */

    /* Shorthand */
    flex-flow: row wrap;    /* flex-direction + flex-wrap */

    /* Main axis alignment (horizontal for row) */
    justify-content: flex-start;    /* Default — items at start */
    justify-content: flex-end;      /* Items at end */
    justify-content: center;        /* Items centered */
    justify-content: space-between; /* First, last at edges, space between */
    justify-content: space-around;  /* Equal space around each item */
    justify-content: space-evenly;  /* Equal space between all */

    /* Cross axis alignment (vertical for row) */
    align-items: stretch;       /* Default — fill container height */
    align-items: flex-start;    /* Items at top */
    align-items: flex-end;      /* Items at bottom */
    align-items: center;        /* Items vertically centered */
    align-items: baseline;      /* Items aligned by text baseline */

    /* Multiple lines alignment (when wrapping) */
    align-content: flex-start;
    align-content: flex-end;
    align-content: center;
    align-content: space-between;
    align-content: space-around;
    align-content: stretch;

    /* Gap between items */
    gap:        16px;         /* Row and column gap */
    row-gap:    16px;
    column-gap: 24px;
}
```

### Flex Item Properties
**Definition:** Properties applied to children to control their individual sizing and alignment.
```css
.item {
    /* Growth — how much item grows to fill extra space */
    flex-grow:   0;     /* Default — don't grow */
    flex-grow:   1;     /* Grow to fill available space */
    flex-grow:   2;     /* Grow twice as much as flex-grow: 1 */

    /* Shrink — how much item shrinks when container is too small */
    flex-shrink: 1;     /* Default — can shrink */
    flex-shrink: 0;     /* Don't shrink */

    /* Basis — initial size before growing/shrinking */
    flex-basis: auto;   /* Default — use width/height */
    flex-basis: 200px;  /* Start at 200px */
    flex-basis: 0;      /* Ignore natural size */

    /* Shorthand: grow shrink basis */
    flex: 0 1 auto;    /* Default */
    flex: 1;           /* grow:1 shrink:1 basis:0 */
    flex: 1 1 auto;    /* Grow and shrink freely */
    flex: none;        /* 0 0 auto — rigid size */
    flex: auto;        /* 1 1 auto — fully flexible */

    /* Override cross-axis alignment for this item only */
    align-self: auto;         /* Use container's align-items */
    align-self: flex-start;
    align-self: flex-end;
    align-self: center;
    align-self: stretch;

    /* Change display order (doesn't change source order) */
    order: 0;      /* Default */
    order: -1;     /* Move to front */
    order: 1;      /* Move toward back */
}
```

### Flexbox Patterns
**Definition:** Common layout solutions using flexbox.
```css
/* Perfect center */
.center {
    display: flex;
    justify-content: center;
    align-items: center;
}

/* Sticky footer — main grows to push footer down */
body {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
}
main { flex: 1; }

/* Navigation with logo left, links right */
nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

/* Card grid that wraps */
.cards {
    display: flex;
    flex-wrap: wrap;
    gap: 16px;
}
.card { flex: 1 1 300px; }   /* Minimum 300px, then grows */
```

---

## CSS Grid

**Definition:** A two-dimensional layout system — control both rows and columns simultaneously.

### Grid Container Properties
**Definition:** Properties applied to the parent to define the grid structure.
```css
.container {
    display: grid;

    /* Define columns */
    grid-template-columns: 200px 1fr 1fr;      /* Fixed + flexible */
    grid-template-columns: repeat(3, 1fr);      /* 3 equal columns */
    grid-template-columns: repeat(4, minmax(200px, 1fr));  /* Min 200px */
    grid-template-columns: 1fr 2fr 1fr;         /* Proportional */
    grid-template-columns: auto 1fr auto;        /* Fit-content sides */

    /* Define rows */
    grid-template-rows: 100px auto 100px;       /* Header + content + footer */
    grid-template-rows: repeat(3, 1fr);

    /* Auto-fill/auto-fit — responsive without media queries */
    grid-template-columns: repeat(auto-fill,  minmax(200px, 1fr));
    grid-template-columns: repeat(auto-fit,   minmax(200px, 1fr));
    /* auto-fill: keeps empty columns | auto-fit: collapses empty columns */

    /* Named template areas */
    grid-template-areas:
        "header header header"
        "sidebar main    main"
        "footer  footer footer";

    /* Gap between cells */
    gap:        16px;
    row-gap:    16px;
    column-gap: 24px;

    /* Implicit grid for overflow items */
    grid-auto-rows:    minmax(100px, auto);
    grid-auto-columns: 200px;
    grid-auto-flow:    row;       /* Fill row by row */
    grid-auto-flow:    column;    /* Fill column by column */
    grid-auto-flow:    dense;     /* Fill gaps with smaller items */
}
```

### Grid Item Properties
**Definition:** Control where and how individual items are placed in the grid.
```css
.item {
    /* Place by line numbers (1-indexed) */
    grid-column: 1 / 3;          /* Start at line 1, end at line 3 */
    grid-column: 1 / span 2;     /* Start at 1, span 2 columns */
    grid-column: 1 / -1;         /* Span entire row */

    grid-row: 1 / 3;             /* Rows 1 and 2 */
    grid-row: span 2;            /* Span 2 rows */

    /* Shorthand: row-start / col-start / row-end / col-end */
    grid-area: 1 / 1 / 3 / 3;

    /* Named area */
    grid-area: header;            /* Must match grid-template-areas name */

    /* Self alignment within cell */
    justify-self: start;     /* Horizontal: start, end, center, stretch */
    align-self:   center;    /* Vertical: start, end, center, stretch */
    place-self:   center;    /* Shorthand: align-self justify-self */
}
```

### Grid Alignment (Container)
**Definition:** Align the entire grid within its container.
```css
.container {
    /* Align all items horizontally within their cells */
    justify-items: start | end | center | stretch;

    /* Align all items vertically within their cells */
    align-items: start | end | center | stretch;

    /* Shorthand */
    place-items: center;          /* align-items justify-items */

    /* Align the grid tracks within the container */
    justify-content: start | end | center | space-between | space-around;
    align-content:   start | end | center | space-between | space-around;
    place-content: center;
}
```

### Grid Patterns
**Definition:** Common layout solutions with CSS Grid.
```css
/* Holy Grail Layout */
body {
    display: grid;
    grid-template-areas:
        "header"
        "main"
        "sidebar"
        "footer";
    grid-template-rows: auto 1fr auto auto;
    min-height: 100vh;
}

@media (min-width: 768px) {
    body {
        grid-template-areas:
            "header  header"
            "sidebar main"
            "footer  footer";
        grid-template-columns: 250px 1fr;
        grid-template-rows: auto 1fr auto;
    }
}

header  { grid-area: header; }
main    { grid-area: main; }
.sidebar { grid-area: sidebar; }
footer  { grid-area: footer; }
```

---

## Typography

**Definition:** Control how text looks — font family, size, weight, line height, spacing, and alignment.

### Font Family
**Definition:** Set the typeface — always provide fallbacks in case the first font isn't available.
```css
/* System font stack — fast, no download */
font-family: system-ui, -apple-system, sans-serif;

/* Specific fonts with fallbacks */
font-family: 'Roboto', Arial, sans-serif;
font-family: Georgia, 'Times New Roman', serif;
font-family: 'Courier New', Courier, monospace;

/* Load Google Fonts */
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&display=swap');
font-family: 'Inter', sans-serif;

/* System emoji font */
font-family: 'Apple Color Emoji', 'Segoe UI Emoji', 'Noto Color Emoji';
```

### Font Properties
**Definition:** Control the weight, style, size, and variant of text.
```css
font-size:   16px;         /* Absolute size */
font-size:   1.5rem;       /* Relative to root */
font-size:   larger;       /* Relative keyword */

font-weight: normal;       /* 400 */
font-weight: bold;         /* 700 */
font-weight: 100;          /* Thin */
font-weight: 300;          /* Light */
font-weight: 400;          /* Normal */
font-weight: 500;          /* Medium */
font-weight: 600;          /* Semi-bold */
font-weight: 700;          /* Bold */
font-weight: 900;          /* Black */

font-style:  normal;
font-style:  italic;
font-style:  oblique;

font-variant: normal;
font-variant: small-caps;
```

### Text Layout
**Definition:** Control spacing, alignment, and decoration of text.
```css
line-height: 1.6;          /* Unitless — relative to font-size */
line-height: 24px;
line-height: 150%;

letter-spacing: 0.05em;    /* Space between characters */
letter-spacing: -0.02em;   /* Tighter — for headings */
word-spacing:   4px;       /* Space between words */

text-align: left;
text-align: right;
text-align: center;
text-align: justify;
text-align: start;         /* Logical — respects RTL */
text-align: end;

text-decoration: none;
text-decoration: underline;
text-decoration: line-through;
text-decoration: overline;
text-decoration: underline dotted red;  /* style + color */

text-transform: none;
text-transform: uppercase;
text-transform: lowercase;
text-transform: capitalize;   /* First letter of each word */

text-indent: 2em;          /* First line indent */
text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
text-overflow: ellipsis;   /* Clip with ... */
white-space: nowrap;       /* Prevent wrapping */
```

### Text Overflow
**Definition:** Control what happens when text is too long for its container.
```css
/* Single-line ellipsis */
.truncate {
    white-space:   nowrap;
    overflow:      hidden;
    text-overflow: ellipsis;
}

/* Multi-line ellipsis (modern) */
.clamp {
    display:            -webkit-box;
    -webkit-line-clamp: 3;           /* Show 3 lines max */
    -webkit-box-orient: vertical;
    overflow:           hidden;
}
```

### Web Fonts with @font-face
**Definition:** Load custom fonts hosted on your own server.
```css
@font-face {
    font-family: 'MyFont';
    src: url('myfont.woff2') format('woff2'),
         url('myfont.woff')  format('woff');
    font-weight: 400;
    font-style:  normal;
    font-display: swap;    /* Show fallback while loading */
}

body {
    font-family: 'MyFont', sans-serif;
}
```

---

## Backgrounds

**Definition:** Control the background color, image, size, position, and repeat of elements.

### Background Color
**Definition:** Set a solid background color.
```css
background-color: white;
background-color: #f0f0f0;
background-color: rgba(0, 0, 0, 0.5);
background-color: transparent;
```

### Background Image
**Definition:** Set an image as the background — with control over position, size, and repetition.
```css
background-image:    url('image.jpg');
background-repeat:   no-repeat;   /* repeat, repeat-x, repeat-y, no-repeat */
background-position: center;      /* top, bottom, left, right, center */
background-position: 50% 50%;     /* x% y% */
background-position: 20px 40px;   /* From top-left */
background-size:     cover;       /* Cover container (may crop) */
background-size:     contain;     /* Fit inside without cropping */
background-size:     100% auto;   /* Full width, auto height */
background-size:     200px 150px; /* Explicit size */
background-attachment: scroll;    /* Moves with page */
background-attachment: fixed;     /* Fixed to viewport (parallax) */
background-attachment: local;     /* Moves with element content */
background-origin:   padding-box; /* border-box, padding-box, content-box */
background-clip:     padding-box; /* border-box, padding-box, content-box, text */
```

### Background Shorthand
**Definition:** Set all background properties in one declaration.
```css
/* color image position/size repeat attachment */
background: #fff url('bg.jpg') center/cover no-repeat;
background: linear-gradient(to right, #000, #fff);
```

### Multiple Backgrounds
**Definition:** Layer multiple backgrounds on one element — first listed is on top.
```css
.element {
    background:
        url('overlay.png') no-repeat center,
        url('bg.jpg') no-repeat center/cover,
        #f0f0f0;
}
```

---

## Borders

**Definition:** Add borders to elements — control width, style, color, and radius.

### Border Properties
**Definition:** Set border properties individually or with shorthand.
```css
border:        2px solid #333;    /* Shorthand: width style color */
border-top:    3px dashed red;
border-right:  0;
border-bottom: 1px solid #eee;
border-left:   4px solid blue;

border-width:  2px;
border-style:  solid | dashed | dotted | double | groove | ridge | inset | outset | none;
border-color:  #333;
```

### Border Radius
**Definition:** Round the corners of an element.
```css
border-radius: 8px;             /* All corners */
border-radius: 50%;             /* Circle (with equal width/height) */
border-radius: 8px 0;           /* Top corners 8px, bottom corners 0 */
border-radius: 8px 4px 16px 2px;/* TL TR BR BL */

/* Per-corner control */
border-top-left-radius:     8px;
border-top-right-radius:    4px;
border-bottom-right-radius: 8px;
border-bottom-left-radius:  4px;

/* Elliptical corners */
border-radius: 50% / 30%;      /* Horizontal / vertical radii */
```

### Outline
**Definition:** Like border but outside the element — doesn't affect layout.
```css
outline:        2px solid blue;
outline-width:  2px;
outline-style:  solid | dashed | dotted;
outline-color:  blue;
outline-offset: 4px;            /* Gap between border and outline */
outline: none;                  /* Remove outline (be careful — accessibility!) */
```

---

## Shadows

**Definition:** Add depth and elevation effects using box shadows and text shadows.

### Box Shadow
**Definition:** Add shadow to an element's box — can stack multiple shadows.
```css
/* offset-x | offset-y | blur | color */
box-shadow: 2px 2px 4px rgba(0,0,0,0.2);

/* offset-x | offset-y | blur | spread | color */
box-shadow: 0 4px 8px 0 rgba(0,0,0,0.3);

/* Inset shadow — inside the element */
box-shadow: inset 0 2px 4px rgba(0,0,0,0.2);

/* Multiple shadows */
box-shadow:
    0 1px  3px rgba(0,0,0,0.12),
    0 1px  2px rgba(0,0,0,0.24);

/* No shadow */
box-shadow: none;
```

### Text Shadow
**Definition:** Add shadow effect to text characters.
```css
/* offset-x | offset-y | blur | color */
text-shadow: 1px 1px 2px rgba(0,0,0,0.5);

/* Multiple text shadows */
text-shadow:
    0 0 10px white,
    0 0 20px blue,
    0 0 40px blue;

/* No text shadow */
text-shadow: none;
```

---

## Overflow

**Definition:** Control what happens when content is too large for its container.

### Overflow Values
**Definition:** Different strategies for handling overflowing content.
```css
overflow:   visible;  /* Default — content spills out */
overflow:   hidden;   /* Clip overflowing content */
overflow:   scroll;   /* Always show scrollbar */
overflow:   auto;     /* Scrollbar only when needed */
overflow:   clip;     /* Clip without scrollbar (no scroll allowed) */

overflow-x: hidden;   /* Control horizontal only */
overflow-y: auto;     /* Control vertical only */

/* Scroll snapping for carousels */
overflow-x:       scroll;
scroll-snap-type: x mandatory;
.item { scroll-snap-align: start; }
```

---

## Opacity & Visibility

**Definition:** Control the transparency and visibility of elements.

### Opacity
**Definition:** Make an element and all its children semi-transparent.
```css
opacity: 1;     /* Fully visible (default) */
opacity: 0.5;   /* 50% transparent */
opacity: 0;     /* Invisible but still takes space and receives events */
```

### Visibility
**Definition:** Hide or show an element — invisible elements still take up space.
```css
visibility: visible;    /* Default */
visibility: hidden;     /* Invisible, space preserved, no mouse events */
visibility: collapse;   /* For table rows/columns — removes them from layout */
```

### Pointer Events
**Definition:** Control whether an element can receive mouse/touch events.
```css
pointer-events: auto;   /* Default — element receives events */
pointer-events: none;   /* Element ignores all pointer events */
```

---

## Transforms

**Definition:** Visually move, scale, rotate, or skew elements without affecting document flow.

### 2D Transforms
**Definition:** Transform elements in the horizontal and vertical plane.
```css
/* Translate — move element */
transform: translateX(50px);
transform: translateY(-20px);
transform: translate(50px, -20px);
transform: translate(50%, -50%);    /* Percentage of element's own size */

/* Scale — resize element */
transform: scaleX(1.5);
transform: scaleY(0.8);
transform: scale(1.5);             /* Uniform scale */
transform: scale(1.5, 0.8);        /* X and Y independently */

/* Rotate — spin element */
transform: rotate(45deg);
transform: rotate(-90deg);
transform: rotateX(45deg);         /* 3D rotate around X axis */
transform: rotateY(45deg);         /* 3D rotate around Y axis */

/* Skew — distort element */
transform: skewX(10deg);
transform: skewY(5deg);
transform: skew(10deg, 5deg);

/* Chain multiple transforms */
transform: translate(50%, -50%) rotate(45deg) scale(1.2);
```

### Transform Origin
**Definition:** Set the pivot point for transforms — default is center.
```css
transform-origin: center;       /* Default */
transform-origin: top left;     /* Rotate from top-left corner */
transform-origin: 0 0;          /* Same as top left */
transform-origin: 50% 50%;      /* Center (default) */
transform-origin: 100% 100%;    /* Bottom-right corner */
```

### 3D Transforms
**Definition:** Create depth effects with 3D transformations.
```css
/* Add perspective to container */
.container {
    perspective: 800px;
    perspective-origin: center;
}

.card {
    transform-style: preserve-3d;   /* Children maintain 3D position */
    transform: rotateY(180deg);
    backface-visibility: hidden;     /* Hide back face */
}
```

---

## Transitions

**Definition:** Smoothly animate property changes over time — triggered by state changes like `:hover`.

### Basic Transition
**Definition:** Define which property to animate, how long, and how it eases.
```css
/* Shorthand: property duration timing-function delay */
transition: color 0.3s ease;
transition: all  0.3s ease;
transition: background-color 0.2s ease-in-out;
transition: transform 0.4s cubic-bezier(0.25, 0.46, 0.45, 0.94);

/* Multiple transitions */
transition:
    color     0.2s ease,
    transform 0.3s ease,
    opacity   0.2s ease;
```

### Transition Properties
**Definition:** Control each aspect of the transition individually.
```css
transition-property:        color, background;  /* Which properties */
transition-duration:        0.3s;               /* How long */
transition-timing-function: ease;               /* Easing curve */
transition-delay:           0.1s;               /* Wait before starting */
```

### Timing Functions
**Definition:** Control the speed curve of the animation.
```css
transition-timing-function: linear;            /* Constant speed */
transition-timing-function: ease;              /* Slow → fast → slow (default) */
transition-timing-function: ease-in;           /* Slow start */
transition-timing-function: ease-out;          /* Slow end */
transition-timing-function: ease-in-out;       /* Slow start and end */
transition-timing-function: cubic-bezier(0.25, 0.1, 0.25, 1);  /* Custom */
transition-timing-function: steps(4, end);     /* Stepped animation */
```

---

## Animations

**Definition:** Define multi-step animations using `@keyframes` — more powerful than transitions.

### Define Keyframes
**Definition:** Use `@keyframes` to specify the animation at different points in time.
```css
/* from/to — simple two-step animation */
@keyframes fadeIn {
    from { opacity: 0; }
    to   { opacity: 1; }
}

/* Percentage steps — precise control */
@keyframes bounce {
    0%   { transform: translateY(0); }
    30%  { transform: translateY(-30px); }
    50%  { transform: translateY(0); }
    70%  { transform: translateY(-15px); }
    100% { transform: translateY(0); }
}

@keyframes slideIn {
    from { transform: translateX(-100%); opacity: 0; }
    to   { transform: translateX(0);     opacity: 1; }
}

@keyframes spin {
    from { transform: rotate(0deg); }
    to   { transform: rotate(360deg); }
}

@keyframes pulse {
    0%, 100% { transform: scale(1); }
    50%       { transform: scale(1.05); }
}
```

### Apply Animation
**Definition:** Attach keyframes to an element with animation properties.
```css
.element {
    animation-name:            fadeIn;
    animation-duration:        0.5s;
    animation-timing-function: ease-in-out;
    animation-delay:           0.2s;
    animation-iteration-count: 1;          /* Or: infinite */
    animation-direction:       normal;     /* reverse, alternate, alternate-reverse */
    animation-fill-mode:       forwards;   /* Keep end state: none, forwards, backwards, both */
    animation-play-state:      running;    /* paused to pause */

    /* Shorthand: name duration timing delay count direction fill play-state */
    animation: fadeIn 0.5s ease-in-out 0.2s 1 normal forwards;
}

/* Multiple animations */
.spinner {
    animation:
        spin 1s linear infinite,
        pulse 2s ease-in-out infinite;
}
```

### Respecting User Preferences
**Definition:** Always respect the user's motion preference.
```css
@media (prefers-reduced-motion: reduce) {
    *, *::before, *::after {
        animation-duration:        0.01ms !important;
        animation-iteration-count: 1      !important;
        transition-duration:       0.01ms !important;
    }
}
```

---

## Responsive Design & Media Queries

**Definition:** Apply different styles based on screen size, device type, or user preferences.

### Basic Media Query
**Definition:** Wrap CSS rules in `@media` to apply them only when conditions are met.
```css
/* Mobile first — start with small, add styles for larger */

/* Base styles — mobile */
.container { width: 100%; padding: 16px; }

/* Tablet — 768px and up */
@media (min-width: 768px) {
    .container { max-width: 720px; margin: 0 auto; }
}

/* Desktop — 1024px and up */
@media (min-width: 1024px) {
    .container { max-width: 960px; }
}

/* Wide — 1280px and up */
@media (min-width: 1280px) {
    .container { max-width: 1200px; }
}
```

### Common Breakpoints
**Definition:** Standard screen width breakpoints used across modern frameworks.
```css
/* Mobile first breakpoints */
/* xs:  < 576px   — small phones */
/* sm:  ≥ 576px   — large phones */
/* md:  ≥ 768px   — tablets */
/* lg:  ≥ 1024px  — laptops */
/* xl:  ≥ 1280px  — desktops */
/* 2xl: ≥ 1536px  — large screens */

/* Tailwind/Bootstrap inspired */
@media (min-width: 640px)  { /* sm */ }
@media (min-width: 768px)  { /* md */ }
@media (min-width: 1024px) { /* lg */ }
@media (min-width: 1280px) { /* xl */ }
@media (min-width: 1536px) { /* 2xl */ }
```

### Media Feature Types
**Definition:** Media queries can check many different conditions beyond just screen width.
```css
/* Width and height */
@media (min-width: 768px)    { }
@media (max-width: 767px)    { }
@media (width: 768px)        { }

/* Orientation */
@media (orientation: portrait)  { }
@media (orientation: landscape) { }

/* Resolution / retina */
@media (min-resolution: 2dppx)  { }  /* Retina displays */
@media (-webkit-min-device-pixel-ratio: 2) { }  /* Webkit */

/* Color scheme */
@media (prefers-color-scheme: dark)  { }
@media (prefers-color-scheme: light) { }

/* Motion preference */
@media (prefers-reduced-motion: reduce) { }
@media (prefers-reduced-motion: no-preference) { }

/* Hover capability */
@media (hover: hover)    { }   /* Device supports hover */
@media (hover: none)     { }   /* Touch device — no hover */

/* Pointer precision */
@media (pointer: fine)   { }   /* Mouse */
@media (pointer: coarse) { }   /* Touch */

/* Print */
@media print { }

/* Multiple conditions */
@media (min-width: 768px) and (orientation: landscape) { }
@media (max-width: 600px), (orientation: portrait)     { }   /* OR */
```

### Fluid Typography
**Definition:** Font size scales smoothly between breakpoints using clamp.
```css
:root {
    font-size: clamp(14px, 2.5vw, 18px);
}

h1 { font-size: clamp(24px, 5vw, 48px); }
h2 { font-size: clamp(20px, 4vw, 36px); }
p  { font-size: clamp(14px, 2vw, 18px); }
```

---

## Filters

**Definition:** Apply graphical effects to elements — blur, brightness, contrast, and more.

### Filter Functions
**Definition:** Chain multiple filter effects in one declaration.
```css
filter: blur(4px);                  /* Gaussian blur */
filter: brightness(0.8);            /* Darken (0=black, 1=normal, 2=brighten) */
filter: contrast(1.5);              /* Increase contrast */
filter: grayscale(1);               /* Full grayscale (0=none, 1=full) */
filter: grayscale(50%);             /* Partial grayscale */
filter: sepia(0.8);                 /* Sepia tone */
filter: saturate(2);                /* Double saturation */
filter: hue-rotate(90deg);          /* Rotate hue wheel */
filter: invert(1);                  /* Invert colors */
filter: opacity(0.7);               /* Transparency (like opacity property) */
filter: drop-shadow(4px 4px 8px rgba(0,0,0,0.5)); /* Shadow (respects transparency) */

/* Chain multiple filters */
filter: brightness(0.9) contrast(1.1) saturate(1.2);

/* Backdrop filter — blur behind element */
backdrop-filter: blur(10px);
backdrop-filter: blur(10px) brightness(0.8);
```

---

## Gradients

**Definition:** Create smooth color transitions as background images — no separate image file needed.

### Linear Gradient
**Definition:** Colors transition in a straight line.
```css
/* Direction then colors */
background: linear-gradient(to right, red, blue);
background: linear-gradient(to bottom right, red, yellow, blue);
background: linear-gradient(45deg, #000, #fff);

/* Color stops with positions */
background: linear-gradient(to right, red 0%, orange 25%, yellow 50%, green 100%);

/* Hard color stop — no blend */
background: linear-gradient(to right, red 50%, blue 50%);

/* Transparent gradient */
background: linear-gradient(to bottom, rgba(0,0,0,0.8), transparent);
```

### Radial Gradient
**Definition:** Colors radiate outward from a center point.
```css
/* Circle */
background: radial-gradient(circle, red, blue);
background: radial-gradient(circle at center, #fff, #000);
background: radial-gradient(circle at top left, yellow, green);

/* Ellipse (default) */
background: radial-gradient(ellipse, #fff 30%, #000 80%);

/* Sized */
background: radial-gradient(circle closest-side, red, blue);
background: radial-gradient(circle 200px at center, red, blue);
```

### Conic Gradient
**Definition:** Colors transition around a center point — like a color wheel or pie chart.
```css
/* Pie chart effect */
background: conic-gradient(red 0deg 120deg, green 120deg 240deg, blue 240deg 360deg);

/* Color wheel */
background: conic-gradient(red, orange, yellow, green, blue, violet, red);

/* Pie chart with percentages */
background: conic-gradient(
    #ff6b6b 0%    30%,   /* Red: 30% */
    #ffd93d 30%   70%,   /* Yellow: 40% */
    #6bcb77 70%   100%   /* Green: 30% */
);
```

### Repeating Gradients
**Definition:** Repeat a gradient pattern to fill the element.
```css
/* Striped background */
background: repeating-linear-gradient(
    45deg,
    #f0f0f0,
    #f0f0f0 10px,
    white 10px,
    white 20px
);

/* Bullseye */
background: repeating-radial-gradient(circle, white, white 10px, #ddd 10px, #ddd 20px);
```

---

## Object Fit & Object Position

**Definition:** Control how replaced content (images, videos) fills its container box.

### Object Fit
**Definition:** Similar to `background-size` but for `<img>` and `<video>` elements.
```css
img {
    width:  300px;
    height: 200px;
    object-fit: fill;       /* Default — stretch to fill (may distort) */
    object-fit: contain;    /* Fit inside without cropping (letterbox) */
    object-fit: cover;      /* Fill without distorting (may crop) */
    object-fit: none;       /* Natural size, no scaling */
    object-fit: scale-down; /* Smaller of contain or none */
}
```

### Object Position
**Definition:** Set the alignment of the content within its box — like `background-position`.
```css
img {
    object-fit:      cover;
    object-position: center;     /* Center (default) */
    object-position: top;        /* Show top of image */
    object-position: bottom;     /* Show bottom */
    object-position: left;
    object-position: 20% 80%;    /* X% Y% */
    object-position: 10px 20px;  /* From top-left */
}
```

---

## Scroll Behavior

**Definition:** Control scrolling behavior and snap points for smooth navigation.

### Smooth Scrolling
**Definition:** Enable smooth animated scrolling instead of instant jumps.
```css
/* Apply to root for page-wide smooth scroll */
html {
    scroll-behavior: smooth;
}

/* Respect user motion preference */
@media (prefers-reduced-motion: no-preference) {
    html { scroll-behavior: smooth; }
}
```

### Scroll Margin & Padding
**Definition:** Offset where the page scrolls to when targeting an anchor — accounts for fixed headers.
```css
/* Add offset when scrolling to an element */
.section {
    scroll-margin-top: 80px;   /* Offset from top (e.g. sticky header height) */
}

/* Add padding before scrolled-to content */
html {
    scroll-padding-top: 80px;
}
```

### Scroll Snap
**Definition:** Create snap points for carousel-style scrolling.
```css
/* Container */
.slider {
    display:          flex;
    overflow-x:       scroll;
    scroll-snap-type: x mandatory;   /* or: x proximity */
    gap:              16px;
}

/* Each item snaps into place */
.slide {
    flex:             0 0 100%;
    scroll-snap-align: start;    /* start, end, or center */
}
```

---

## Clipping & Masking

**Definition:** Show only part of an element by clipping it to a shape or masking with an image.

### clip-path
**Definition:** Clip an element to a geometric shape — content outside is hidden.
```css
/* Basic shapes */
clip-path: circle(50%);                             /* Circle */
clip-path: circle(100px at center);                 /* Circle with size and position */
clip-path: ellipse(50% 30% at center);
clip-path: inset(10px 20px 10px 20px);              /* Rectangle inset */
clip-path: inset(10px round 8px);                   /* Rounded rectangle */

/* Polygon — list of x y points */
clip-path: polygon(0 0, 100% 0, 100% 80%, 0 100%); /* Parallelogram */
clip-path: polygon(50% 0%, 0% 100%, 100% 100%);     /* Triangle */
clip-path: polygon(50% 0%, 100% 100%, 0% 100%);     /* Inverted triangle */

/* Animate clip-path */
.element {
    clip-path: circle(0% at 50% 50%);
    transition: clip-path 0.5s ease;
}
.element:hover {
    clip-path: circle(100% at 50% 50%);
}
```

---

## CSS Functions

**Definition:** Built-in functions used as property values — from math to color manipulation.

### Math Functions
**Definition:** Perform calculations in CSS property values.
```css
width:     calc(100% - 48px);
font-size: calc(1rem + 0.5vw);

width:     min(500px, 90%);          /* Use smaller value */
width:     max(200px, 30%);          /* Use larger value */
font-size: clamp(14px, 2vw, 20px);  /* Constrain between min and max */

/* Other math functions */
width: round(nearest, 100px, 10px);  /* Round to nearest 10px */
width: mod(15px, 4px);               /* Modulo */
width: abs(-20px);                   /* Absolute value */
```

### Color Functions
**Definition:** Manipulate and create colors dynamically.
```css
color: rgb(255, 128, 0);
color: rgba(255, 128, 0, 0.5);
color: hsl(30, 100%, 50%);
color: hsla(30, 100%, 50%, 0.5);
color: oklch(60% 0.2 30);
color: color-mix(in srgb, blue 50%, red 50%);    /* Mix two colors */
color: color-mix(in oklch, var(--primary) 30%, white);
```

### Other Functions
**Definition:** Additional CSS functions for images, counters, and more.
```css
background: url('image.jpg');
background: image-set(url('img.png') 1x, url('img@2x.png') 2x);

/* Counters */
counter-reset:     section;
counter-increment: section;
content:           counter(section);
content:           counters(section, ".");

/* Environment variables */
padding-top: env(safe-area-inset-top);          /* iPhone notch */
padding-bottom: env(safe-area-inset-bottom);    /* iPhone home bar */

/* Grid functions */
grid-template-columns: repeat(3, minmax(200px, 1fr));
grid-template-columns: fit-content(200px) 1fr;
```

---

## At-Rules

**Definition:** Special CSS instructions that start with `@` — control imports, media, fonts, and more.

### @import
**Definition:** Import another CSS file — always put at the top of your stylesheet.
```css
@import url('reset.css');
@import url('variables.css');
@import url('https://fonts.googleapis.com/css2?family=Inter&display=swap');

/* With media query */
@import url('print.css') print;
@import url('mobile.css') screen and (max-width: 768px);
```

### @media
**Definition:** Apply styles conditionally based on device/viewport properties.
```css
@media screen and (min-width: 768px) { }
@media print { }
@media (prefers-color-scheme: dark) { }
```

### @keyframes
**Definition:** Define animation frames for use with the `animation` property.
```css
@keyframes myAnimation {
    0%   { opacity: 0; }
    100% { opacity: 1; }
}
```

### @font-face
**Definition:** Load a custom font file for use in the document.
```css
@font-face {
    font-family: 'MyFont';
    src: url('font.woff2') format('woff2');
    font-weight: 400;
    font-display: swap;
}
```

### @layer
**Definition:** Organize CSS into named layers to control cascade order (CSS Cascade Layers).
```css
/* Declare layer order — earlier = lower priority */
@layer reset, base, components, utilities;

@layer reset {
    * { margin: 0; padding: 0; }
}

@layer base {
    body { font-family: sans-serif; }
}

@layer utilities {
    .hidden { display: none; }
}
```

### @supports
**Definition:** Conditionally apply styles only if a CSS feature is supported.
```css
/* Only if browser supports grid */
@supports (display: grid) {
    .container { display: grid; }
}

/* Only if browser does NOT support a feature */
@supports not (display: grid) {
    .container { display: flex; }
}

/* Test a specific value */
@supports (backdrop-filter: blur(10px)) {
    .panel { backdrop-filter: blur(10px); }
}
```

---

## Logical Properties

**Definition:** Writing-mode-aware properties that work correctly for RTL languages — replace physical left/right/top/bottom.

### Logical vs Physical
**Definition:** Logical properties adapt automatically to text direction and writing mode.
```css
/* Physical (left-to-right specific) */
margin-left:  16px;
margin-right: 24px;
padding-top:  8px;
border-left:  2px solid;

/* Logical (works in RTL and vertical writing modes) */
margin-inline-start:  16px;   /* margin-left in LTR, margin-right in RTL */
margin-inline-end:    24px;   /* margin-right in LTR, margin-left in RTL */
padding-block-start:  8px;    /* padding-top in horizontal writing */
border-inline-start:  2px solid;

/* Shorthand logical properties */
margin-inline:  16px 24px;   /* Start end (LTR: left right) */
margin-block:   8px 16px;    /* Start end (LTR: top bottom) */
padding-inline: 16px;
padding-block:  8px;

/* Logical sizing */
width:  → inline-size
height: → block-size

/* Logical positions */
top:    → inset-block-start
bottom: → inset-block-end
left:   → inset-inline-start
right:  → inset-inline-end
inset:  1rem;   /* Shorthand for all four sides */
```

---

## Container Queries

**Definition:** Apply styles based on the size of a container element — not the viewport. Modern and powerful.

### Define Container
**Definition:** Mark an element as a container so children can query its size.
```css
/* Define a container */
.card-wrapper {
    container-type: inline-size;   /* Enable width queries */
    container-name: card;          /* Optional name */
}

/* Shorthand */
.card-wrapper {
    container: card / inline-size;
}
```

### Query the Container
**Definition:** Apply styles to children based on the container's dimensions.
```css
/* When the container is at least 500px wide */
@container (min-width: 500px) {
    .card {
        display: flex;
        gap: 16px;
    }
}

/* Named container query */
@container card (min-width: 400px) {
    .card-title { font-size: 1.5rem; }
}

/* Container query units */
.card {
    font-size: 4cqi;    /* 4% of container inline size */
    width: 50cqw;       /* 50% of container width */
    height: 50cqh;      /* 50% of container height */
}
```

---

## Useful Snippets

**Definition:** Ready-to-use CSS patterns that solve common layout and style problems.

### CSS Reset
**Definition:** Remove inconsistent browser default styles — use as the foundation of any project.
```css
*, *::before, *::after {
    box-sizing: border-box;
    margin:     0;
    padding:    0;
}

html {
    font-size:               16px;
    -webkit-text-size-adjust: 100%;
    scroll-behavior:         smooth;
}

body {
    font-family:    system-ui, -apple-system, sans-serif;
    line-height:    1.5;
    -webkit-font-smoothing:   antialiased;
    -moz-osx-font-smoothing:  grayscale;
}

img, video, canvas, svg {
    display:   block;
    max-width: 100%;
}

input, button, textarea, select {
    font: inherit;
}

p, h1, h2, h3, h4, h5, h6 {
    overflow-wrap: break-word;
}
```

### Center Anything
**Definition:** Multiple ways to center content — choose based on context.
```css
/* Flexbox center (best for most cases) */
.center {
    display:         flex;
    justify-content: center;
    align-items:     center;
}

/* Grid center */
.center {
    display:     grid;
    place-items: center;
}

/* Absolute center (positioned element) */
.center {
    position:  absolute;
    top:       50%;
    left:      50%;
    transform: translate(-50%, -50%);
}

/* Auto margin (block elements, known width) */
.center {
    width:        500px;
    margin-left:  auto;
    margin-right: auto;
}
```

### Visually Hidden (Accessible)
**Definition:** Hide content visually but keep it accessible to screen readers.
```css
.sr-only {
    position:   absolute;
    width:      1px;
    height:     1px;
    padding:    0;
    margin:     -1px;
    overflow:   hidden;
    clip:       rect(0, 0, 0, 0);
    white-space: nowrap;
    border:     0;
}
```

### Aspect Ratio
**Definition:** Maintain a fixed aspect ratio — images, videos, and embed containers.
```css
/* Modern — use aspect-ratio property */
.video-wrapper {
    aspect-ratio: 16 / 9;
    width: 100%;
}

.square    { aspect-ratio: 1; }
.photo     { aspect-ratio: 4 / 3; }
.cinema    { aspect-ratio: 21 / 9; }
```

### Dark Mode
**Definition:** Apply a dark color theme based on system preference.
```css
:root {
    --bg:     #ffffff;
    --text:   #212529;
    --border: #dee2e6;
}

@media (prefers-color-scheme: dark) {
    :root {
        --bg:     #1a1a2e;
        --text:   #e0e0e0;
        --border: #444;
    }
}

body {
    background: var(--bg);
    color:      var(--text);
}
```

### Sticky Header
**Definition:** Header that sticks to the top of the viewport when scrolling.
```css
header {
    position:   sticky;
    top:        0;
    z-index:    100;
    background: white;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

/* Prevent content from hiding under sticky header */
:target { scroll-margin-top: 70px; }
```

### Custom Scrollbar
**Definition:** Style the browser scrollbar — works in WebKit and Chromium browsers.
```css
/* For WebKit (Chrome, Safari, Edge) */
::-webkit-scrollbar       { width: 8px; }
::-webkit-scrollbar-track { background: #f1f1f1; }
::-webkit-scrollbar-thumb { background: #888; border-radius: 4px; }
::-webkit-scrollbar-thumb:hover { background: #555; }

/* Firefox */
* {
    scrollbar-width: thin;
    scrollbar-color: #888 #f1f1f1;
}
```

---

## Best Practices

**Definition:** Guidelines for writing maintainable, performant, and accessible CSS.

### Organization
**Definition:** Structure CSS files for readability and maintainability.
```css
/*
 * Recommended file structure:
 * 1. @import statements
 * 2. CSS custom properties (:root variables)
 * 3. CSS reset / base styles
 * 4. Layout (body, containers, grid)
 * 5. Typography
 * 6. Components (buttons, cards, forms)
 * 7. Utilities and helpers
 * 8. Media queries (or co-locate with components)
 */

/*
 * BEM Naming Convention — Block Element Modifier
 */
.card          { }          /* Block */
.card__title   { }          /* Element (child of block) */
.card__image   { }          /* Element */
.card--featured { }         /* Modifier (variation of block) */
.card--dark    { }          /* Modifier */
.card__title--large { }     /* Element modifier */
```

### Performance
**Definition:** Write CSS that renders fast and doesn't cause unnecessary repaints.
```css
/* Use transform/opacity for animations — GPU accelerated */
.animate {
    transform: translateX(100px);   /* GPU: yes */
    opacity:   0.5;                  /* GPU: yes */
    /* Avoid animating: width, height, top, left, background */
}

/* Avoid universal selectors deep in chains */
/* Bad  */ .nav * .item { }
/* Good */ .nav .item { }

/* Use will-change for elements you know will animate */
.animated-card {
    will-change: transform;   /* Hint to browser — use sparingly */
}

/* Prefer shorthand */
margin: 8px 16px;    /* Instead of 4 separate declarations */
```

### Accessibility
**Definition:** Write CSS that doesn't break accessibility features.
```css
/* Never remove focus indicators without replacement */
/* Bad */
*:focus { outline: none; }

/* Good — style it instead */
:focus-visible {
    outline:        2px solid #0066cc;
    outline-offset: 2px;
}

/* Sufficient color contrast — WCAG requires: */
/* Normal text: 4.5:1 contrast ratio */
/* Large text:  3:1 contrast ratio */

/* Don't hide text needed for screen readers */
/* Use .sr-only instead of display:none */

/* Respect user preferences */
@media (prefers-reduced-motion: reduce) {
    * { animation-duration: 0.01ms !important; }
}

@media (prefers-contrast: high) {
    .button { border: 2px solid currentColor; }
}
```

### Summary of Rules

* Use **`box-sizing: border-box`** on everything — apply with `*, *::before, *::after`
* Use **CSS variables** (`--custom-property`) for all repeated values
* Write **mobile-first** — start small, add styles for larger screens with `min-width`
* Use **Flexbox** for one-dimensional layout, **Grid** for two-dimensional
* Use **`rem`** for font sizes, **`px`** for borders/shadows, **`%`** or **`vw`** for containers
* Prefer **`transform` and `opacity`** for animations — they don't trigger layout
* Never remove **`:focus` styles** without providing an alternative
* Use **semantic class names** (`card`, `nav`, `btn`) not visual ones (`red-box`, `float-left`)
* Always use **fallback fonts** in `font-family` stacks
* Validate with **DevTools** — use Chrome/Firefox's computed styles panel
