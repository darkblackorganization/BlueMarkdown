
## Introduction

**HTML** (HyperText Markup Language) is the standard language for creating web pages. Created by **Tim Berners-Lee** in **1991**, HTML defines the **structure and content** of a webpage using **elements** wrapped in **tags**. Every website you visit is built on HTML — it tells the browser what to display: headings, paragraphs, images, links, forms, tables, and more. The latest version is **HTML5**, which added powerful features like video, audio, canvas, and semantic elements. HTML works together with **CSS** (styling) and **JavaScript** (behavior) to build complete web experiences.


## Basic Structure

**Definition:** Every HTML page follows the same skeleton — these tags are required for a valid document.

### Minimal HTML Page
**Definition:** The bare minimum structure that every HTML file must have.
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Page Title</title>
  </head>
  <body>
    <h1>Hello, World!</h1>
    <p>This is a paragraph.</p>
  </body>
</html>
```

### Tag Anatomy
**Definition:** An HTML element has an opening tag, content, and a closing tag — some are self-closing.
```html
<tagname attribute="value">Content goes here</tagname>

<!-- Opening tag -->
<p>This is a paragraph</p>
<!-- Closing tag has a slash -->

<!-- Self-closing tag — no content, no closing tag needed -->
<br>
<hr>
<img src="photo.jpg" alt="A photo">
<input type="text">
```

### Nesting
**Definition:** HTML elements can be placed inside other elements — always close inner tags before outer ones.
```html
<!-- Correct nesting -->
<div>
  <p>This is <strong>bold text</strong> inside a paragraph.</p>
</div>

<!-- Wrong nesting — do NOT do this -->
<div>
  <p>Wrong <strong>nesting</div></p></strong>
```

---

## Doctype & Meta Tags

**Definition:** Doctype tells the browser which version of HTML to use — meta tags provide page information.

### DOCTYPE
**Definition:** Must be the very first line — tells the browser this is an HTML5 document.
```html
<!DOCTYPE html>
```

### Charset
**Definition:** Declares the character encoding — UTF-8 supports all languages and symbols.
```html
<meta charset="UTF-8">
```

### Viewport
**Definition:** Essential for responsive design — tells mobile browsers how to scale the page.
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

### Page Description
**Definition:** Shown in search engine results below the page title — keep under 160 characters.
```html
<meta name="description" content="A complete guide to HTML for beginners.">
```

### Author & Keywords
**Definition:** Provide additional metadata about the page — keywords are mostly ignored by modern search engines.
```html
<meta name="author" content="Dark">
<meta name="keywords" content="HTML, web, tutorial, coding">
```

### Refresh & Redirect
**Definition:** Automatically refresh the page or redirect to another URL after a delay.
```html
<meta http-equiv="refresh" content="30">                       <!-- Refresh every 30s -->
<meta http-equiv="refresh" content="5; url=https://example.com"> <!-- Redirect after 5s -->
```

---

## Headings

**Definition:** Six levels of headings — `<h1>` is the most important, `<h6>` is the least. Use one `<h1>` per page.

### All Heading Levels
**Definition:** Each level represents a different hierarchy — use them in order, don't skip levels.
```html
<h1>Heading 1 — Page Title (most important)</h1>
<h2>Heading 2 — Section Title</h2>
<h3>Heading 3 — Subsection Title</h3>
<h4>Heading 4 — Sub-subsection</h4>
<h5>Heading 5 — Minor Heading</h5>
<h6>Heading 6 — Smallest Heading</h6>
```

### Usage Rules
**Definition:** Headings define page structure for both users and search engines — use them logically.
```html
<h1>My Cooking Blog</h1>          <!-- One per page — main topic -->
  <h2>Breakfast Recipes</h2>      <!-- Section -->
    <h3>Pancakes</h3>             <!-- Subsection -->
    <h3>Omelette</h3>
  <h2>Lunch Recipes</h2>
    <h3>Pasta</h3>
```

---

## Paragraphs & Text

**Definition:** Basic text content elements — the building blocks of readable web content.

### Paragraph
**Definition:** A block of text — browsers add space above and below automatically.
```html
<p>This is a paragraph of text.</p>
<p>This is another paragraph. Browsers add vertical spacing between them.</p>
```

### Line Break
**Definition:** Force a new line inside text — use sparingly, prefer CSS margins for spacing.
```html
<p>First line<br>Second line<br>Third line</p>
```

### Horizontal Rule
**Definition:** A thematic break — draws a horizontal line to separate content sections.
```html
<p>Section one content.</p>
<hr>
<p>Section two content.</p>
```

### Preformatted Text
**Definition:** Displays text exactly as written — preserves spaces, tabs, and line breaks.
```html
<pre>
  Name:  Dark
  Age:   25
  City:  Mumbai
</pre>
```

### Blockquote
**Definition:** Marks a long quotation from an external source — browsers indent it by default.
```html
<blockquote cite="https://source.com">
  "The best way to predict the future is to invent it."
</blockquote>
```

### Inline Quote
**Definition:** A short inline quotation — browsers add quotation marks automatically.
```html
<p>He said <q>Hello, World!</q> and walked away.</p>
```

### Abbreviation
**Definition:** Shows the full form of an abbreviation on hover.
```html
<p>I love <abbr title="HyperText Markup Language">HTML</abbr>.</p>
```

### Address
**Definition:** Contact information for a person or organization — displays in italic by default.
```html
<address>
  Written by <a href="mailto:dark@example.com">Dark</a><br>
  Mumbai, India
</address>
```

---

## Text Formatting

**Definition:** Inline elements that change the appearance or meaning of text.

### Bold & Strong
**Definition:** `<b>` is visually bold — `<strong>` is bold AND semantically important (better for accessibility).
```html
<b>Visually bold text</b>
<strong>Important bold text (semantic)</strong>
```

### Italic & Emphasis
**Definition:** `<i>` is visually italic — `<em>` is italic AND adds emphasis (better for accessibility).
```html
<i>Visually italic text</i>
<em>Emphasized italic text (semantic)</em>
```

### Underline & Strikethrough
**Definition:** Underline text or show deleted/incorrect content with a line through it.
```html
<u>Underlined text</u>
<s>Strikethrough — outdated or wrong</s>
<del>Deleted content</del>
<ins>Inserted/new content</ins>
```

### Superscript & Subscript
**Definition:** Raise or lower text — used for mathematical notation, footnotes, and chemical formulas.
```html
<p>E = mc<sup>2</sup></p>         <!-- Superscript → E = mc² -->
<p>H<sub>2</sub>O</p>             <!-- Subscript → H₂O -->
<p>Reference<sup>[1]</sup></p>    <!-- Footnote style -->
```

### Code & Technical
**Definition:** Display inline code, keyboard input, sample output, or variable names.
```html
<p>Use <code>print("Hello")</code> in Python.</p>
<p>Press <kbd>Ctrl</kbd> + <kbd>C</kbd> to copy.</p>
<p>Output: <samp>Hello, World!</samp></p>
<p>The variable <var>x</var> stores the result.</p>
```

### Mark & Small
**Definition:** Highlight text like a marker pen, or show fine print in smaller text.
```html
<p>Search result: <mark>HTML</mark> cheat sheet</p>
<p>Price: $99 <small>(taxes included)</small></p>
```

---

## Links

**Definition:** Anchor tags create clickable hyperlinks — to other pages, sections, files, or email.

### Basic Link
**Definition:** The most common link — clicking it takes the user to the URL in `href`.
```html
<a href="https://google.com">Go to Google</a>
```

### Open in New Tab
**Definition:** Use `target="_blank"` to open link in a new tab — always add `rel="noopener"` for security.
```html
<a href="https://google.com" target="_blank" rel="noopener noreferrer">
  Open in new tab
</a>
```

### Link to Same Page Section
**Definition:** Jump to a specific part of the same page using an `id` as the target.
```html
<!-- The link -->
<a href="#contact">Jump to Contact</a>

<!-- The target (somewhere on the same page) -->
<h2 id="contact">Contact Us</h2>
```

### Link to Email
**Definition:** Opens the user's email client with the To field pre-filled.
```html
<a href="mailto:dark@example.com">Send Email</a>
<a href="mailto:dark@example.com?subject=Hello&body=Hi there">Email with subject</a>
```

### Link to Phone
**Definition:** On mobile devices, tapping this link starts a phone call.
```html
<a href="tel:+911234567890">Call Us</a>
```

### Link to File
**Definition:** Link directly to a file — clicking downloads or opens it depending on the file type.
```html
<a href="docs/report.pdf" download>Download Report</a>
<a href="docs/report.pdf" download="my-report.pdf">Download as my-report.pdf</a>
```

### Link States (for CSS reference)
**Definition:** Links have different visual states — style them in CSS for better user experience.
```html
<!-- Styled with CSS: -->
<!-- a:link    — unvisited link -->
<!-- a:visited — already visited -->
<!-- a:hover   — mouse over -->
<!-- a:active  — being clicked -->
```

---

## Images

**Definition:** Embed images into a webpage — `src` is the image path, `alt` describes it for accessibility.

### Basic Image
**Definition:** The `alt` attribute is required — shown if image fails to load and read by screen readers.
```html
<img src="photo.jpg" alt="A smiling person">
<img src="https://example.com/image.png" alt="Remote image">
```

### Image with Size
**Definition:** Set width and height to prevent layout shifting while the image loads.
```html
<img src="logo.png" alt="Company logo" width="200" height="100">
```

### Responsive Image
**Definition:** Let CSS control the size — use `width: 100%` to make images scale with their container.
```html
<img src="photo.jpg" alt="Photo" style="max-width: 100%; height: auto;">
```

### Image as Link
**Definition:** Wrap an image in an anchor tag to make it a clickable link.
```html
<a href="https://example.com">
  <img src="banner.jpg" alt="Visit our website">
</a>
```

### Figure & Caption
**Definition:** Wraps an image with an optional caption — semantically groups image and its description.
```html
<figure>
  <img src="chart.png" alt="Sales chart for 2025">
  <figcaption>Figure 1: Monthly sales data for 2025.</figcaption>
</figure>
```

### Multiple Sources (Picture)
**Definition:** Serve different images for different screen sizes — browser picks the best match.
```html
<picture>
  <source media="(min-width: 800px)" srcset="large.jpg">
  <source media="(min-width: 400px)" srcset="medium.jpg">
  <img src="small.jpg" alt="Responsive image fallback">
</picture>
```

---

## Lists

**Definition:** Three types of lists — unordered (bullets), ordered (numbers), and description lists.

### Unordered List
**Definition:** A bullet-point list — use when order doesn't matter.
```html
<ul>
  <li>Apple</li>
  <li>Banana</li>
  <li>Cherry</li>
</ul>
```

### Ordered List
**Definition:** A numbered list — use when order or sequence matters.
```html
<ol>
  <li>Wake up</li>
  <li>Brush teeth</li>
  <li>Have breakfast</li>
</ol>
```

### Ordered List Attributes
**Definition:** Control the starting number, counting direction, and number type.
```html
<ol start="5">              <!-- Start at 5 -->
  <li>Item five</li>
  <li>Item six</li>
</ol>

<ol reversed>               <!-- Count down: 3, 2, 1 -->
  <li>Third</li>
  <li>Second</li>
  <li>First</li>
</ol>

<ol type="A">               <!-- A, B, C... (also: a, I, i, 1) -->
  <li>Item A</li>
  <li>Item B</li>
</ol>
```

### Nested List
**Definition:** A list inside another list — creates a hierarchy of items.
```html
<ul>
  <li>Fruits
    <ul>
      <li>Apple</li>
      <li>Banana</li>
    </ul>
  </li>
  <li>Vegetables
    <ul>
      <li>Carrot</li>
      <li>Peas</li>
    </ul>
  </li>
</ul>
```

### Description List
**Definition:** Pairs of terms and their descriptions — great for glossaries or key-value content.
```html
<dl>
  <dt>HTML</dt>
  <dd>HyperText Markup Language — used to structure web pages.</dd>

  <dt>CSS</dt>
  <dd>Cascading Style Sheets — used to style web pages.</dd>

  <dt>JavaScript</dt>
  <dd>A programming language for adding interactivity to web pages.</dd>
</dl>
```

---

## Tables

**Definition:** Display data in rows and columns — use for tabular data, not for page layout.

### Basic Table
**Definition:** A table has a header row (`<thead>`), a body (`<tbody>`), and optionally a footer (`<tfoot>`).
```html
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Age</th>
      <th>City</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Dark</td>
      <td>25</td>
      <td>Mumbai</td>
    </tr>
    <tr>
      <td>Alice</td>
      <td>30</td>
      <td>Delhi</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td colspan="3">Total: 2 users</td>
    </tr>
  </tfoot>
</table>
```

### Spanning Cells
**Definition:** Make a cell span across multiple columns or rows.
```html
<table>
  <tr>
    <th colspan="2">Full Name</th>    <!-- Spans 2 columns -->
    <th>Age</th>
  </tr>
  <tr>
    <td>Dark</td>
    <td>Kumar</td>
    <td rowspan="2">25</td>           <!-- Spans 2 rows -->
  </tr>
  <tr>
    <td>John</td>
    <td>Doe</td>
  </tr>
</table>
```

### Table Caption
**Definition:** A title for the table — placed directly inside `<table>` at the top.
```html
<table>
  <caption>Monthly Sales Report — 2025</caption>
  <thead>
    <tr><th>Month</th><th>Sales</th></tr>
  </thead>
  <tbody>
    <tr><td>January</td><td>$10,000</td></tr>
    <tr><td>February</td><td>$12,500</td></tr>
  </tbody>
</table>
```

### Table Tags Reference
**Definition:** All the elements that make up a complete, semantic HTML table.

| Tag | Purpose |
|-----|---------|
| `<table>` | Container for the whole table |
| `<thead>` | Header section |
| `<tbody>` | Main body section |
| `<tfoot>` | Footer section |
| `<tr>` | Table row |
| `<th>` | Header cell (bold, centered) |
| `<td>` | Data cell |
| `<caption>` | Table title |
| `colspan="n"` | Span n columns |
| `rowspan="n"` | Span n rows |

---

## Forms

**Definition:** Forms collect user input — text, selections, checkboxes, file uploads, and more.

### Basic Form
**Definition:** The `action` sets where data is sent — `method` is usually `get` or `post`.
```html
<form action="/submit" method="post">
  <label for="name">Your Name:</label>
  <input type="text" id="name" name="name" placeholder="Enter your name">

  <label for="email">Email:</label>
  <input type="email" id="email" name="email" required>

  <button type="submit">Submit</button>
</form>
```

### Label
**Definition:** Connects a label to an input — clicking the label focuses the input (important for accessibility).
```html
<!-- Using 'for' + 'id' — recommended -->
<label for="username">Username:</label>
<input type="text" id="username" name="username">

<!-- Wrapping — also valid -->
<label>
  Password:
  <input type="password" name="password">
</label>
```

### Fieldset & Legend
**Definition:** Group related form fields together with a visible border and title.
```html
<form>
  <fieldset>
    <legend>Personal Information</legend>
    <label for="fname">First Name:</label>
    <input type="text" id="fname" name="fname">
    <label for="lname">Last Name:</label>
    <input type="text" id="lname" name="lname">
  </fieldset>

  <fieldset>
    <legend>Account Details</legend>
    <label for="email">Email:</label>
    <input type="email" id="email" name="email">
  </fieldset>
</form>
```

### Textarea
**Definition:** A multi-line text input — set size with `rows` and `cols` attributes (or CSS).
```html
<label for="message">Message:</label>
<textarea id="message" name="message" rows="5" cols="40"
          placeholder="Write your message here..."></textarea>
```

### Select Dropdown
**Definition:** A drop-down menu for selecting one or more options from a list.
```html
<!-- Single select -->
<label for="country">Country:</label>
<select id="country" name="country">
  <option value="">-- Choose --</option>
  <option value="in">India</option>
  <option value="us">United States</option>
  <option value="uk" selected>United Kingdom</option>
</select>

<!-- Multi-select -->
<select name="skills" multiple size="4">
  <option value="html">HTML</option>
  <option value="css">CSS</option>
  <option value="js">JavaScript</option>
  <option value="py">Python</option>
</select>
```

### Option Groups
**Definition:** Organize dropdown options into labeled groups.
```html
<select name="car">
  <optgroup label="German Cars">
    <option value="bmw">BMW</option>
    <option value="mercedes">Mercedes</option>
  </optgroup>
  <optgroup label="Japanese Cars">
    <option value="toyota">Toyota</option>
    <option value="honda">Honda</option>
  </optgroup>
</select>
```

---

## Input Types

**Definition:** The `type` attribute on `<input>` controls what kind of data is accepted and how it looks.

### Text Inputs
**Definition:** Different types of text-based fields — each has built-in validation.
```html
<input type="text"     name="name"     placeholder="Full name">
<input type="email"    name="email"    placeholder="you@example.com">
<input type="password" name="pass"     placeholder="Password">
<input type="url"      name="website"  placeholder="https://example.com">
<input type="tel"      name="phone"    placeholder="+91 9876543210">
<input type="search"   name="query"    placeholder="Search...">
<input type="number"   name="qty"      min="1" max="100" step="1">
```

### Date & Time Inputs
**Definition:** Date and time pickers — appearance varies by browser.
```html
<input type="date">                <!-- Date picker -->
<input type="time">                <!-- Time picker -->
<input type="datetime-local">      <!-- Date and time together -->
<input type="month">               <!-- Month and year -->
<input type="week">                <!-- Week picker -->
```

### Selection Inputs
**Definition:** Let users choose from predefined options — radio for one choice, checkbox for multiple.
```html
<!-- Radio buttons — only one can be selected -->
<input type="radio" id="male"   name="gender" value="male">
<label for="male">Male</label>

<input type="radio" id="female" name="gender" value="female">
<label for="female">Female</label>

<!-- Checkboxes — multiple can be selected -->
<input type="checkbox" id="html" name="skills" value="html">
<label for="html">HTML</label>

<input type="checkbox" id="css"  name="skills" value="css" checked>
<label for="css">CSS</label>
```

### Range & Color
**Definition:** A draggable slider for numeric ranges, and a color picker.
```html
<label>Volume: <input type="range" name="volume" min="0" max="100" value="50"></label>

<label>Pick color: <input type="color" name="color" value="#ff0000"></label>
```

### File Upload
**Definition:** Let users select a file from their device to upload.
```html
<input type="file" name="photo">
<input type="file" name="images" accept="image/*" multiple>    <!-- Images only, multiple -->
<input type="file" name="doc"    accept=".pdf,.doc,.docx">      <!-- Specific extensions -->
```

### Hidden & Other
**Definition:** Hidden inputs carry data not shown to the user — buttons submit or reset the form.
```html
<input type="hidden" name="token" value="abc123">   <!-- Not visible to user -->
<input type="submit" value="Submit Form">
<input type="reset"  value="Clear Form">
<input type="image"  src="btn.png" alt="Submit">    <!-- Image as submit button -->
```

### Datalist (Autocomplete)
**Definition:** Provides suggestions while typing — users can still type anything they want.
```html
<label for="city">City:</label>
<input type="text" id="city" name="city" list="cities">

<datalist id="cities">
  <option value="Mumbai">
  <option value="Delhi">
  <option value="Bangalore">
  <option value="Chennai">
</datalist>
```

---

## Form Attributes

**Definition:** Attributes that control validation, behavior, and appearance of form inputs.

### Validation Attributes
**Definition:** Built-in HTML validation — no JavaScript needed for basic checks.
```html
<input type="text"   required>                      <!-- Must be filled -->
<input type="text"   minlength="3" maxlength="20">  <!-- Length limits -->
<input type="number" min="1" max="100">             <!-- Number range -->
<input type="text"   pattern="[A-Za-z]{3,}">        <!-- Regex pattern -->
<input type="email"  required>                      <!-- Must be valid email -->
```

### State Attributes
**Definition:** Control whether an input is disabled, read-only, checked, or pre-filled.
```html
<input type="text"     disabled>           <!-- Cannot interact at all -->
<input type="text"     readonly value="Fixed text">  <!-- Can read, cannot edit -->
<input type="checkbox" checked>            <!-- Pre-checked -->
<input type="text"     value="Default value">        <!-- Pre-filled value -->
<input type="text"     autofocus>          <!-- Gets focus when page loads -->
<input type="text"     autocomplete="off"> <!-- Disable browser autocomplete -->
```

### Name & ID
**Definition:** `name` is sent to the server — `id` is used for JavaScript and label association.
```html
<input type="text" id="username" name="username">
<!-- id="username"   → links to <label for="username"> -->
<!-- name="username" → key in form data sent to server -->
```

---

## Buttons

**Definition:** Clickable elements for submitting forms, resetting, or triggering JavaScript actions.

### Button Types
**Definition:** Three button types — `submit` sends the form, `reset` clears it, `button` does nothing by default.
```html
<button type="submit">Submit Form</button>    <!-- Submits form data -->
<button type="reset">Clear Form</button>      <!-- Resets all fields -->
<button type="button">Click Me</button>       <!-- For JavaScript actions -->
```

### Button with Icon/HTML
**Definition:** Buttons can contain any HTML — text, images, or icons.
```html
<button type="button">
  <img src="icon.png" alt=""> Save
</button>

<button type="button">⬇ Download</button>
```

### Disabled Button
**Definition:** A button the user cannot click — visually grayed out.
```html
<button type="submit" disabled>Submit</button>
```

---

## Divs & Spans

**Definition:** Generic container elements — `<div>` is block-level, `<span>` is inline — both have no default styling.

### Div (Block Container)
**Definition:** Groups block-level content — takes full width, starts on a new line. Use for sections and layout.
```html
<div class="card">
  <div class="card-header">
    <h2>Title</h2>
  </div>
  <div class="card-body">
    <p>Card content goes here.</p>
  </div>
</div>
```

### Span (Inline Container)
**Definition:** Groups inline content — sits inside a line of text without breaking it. Use for styling parts of text.
```html
<p>
  The price is <span class="price">$99.99</span> per month.
</p>

<p>
  Status: <span style="color: green;">Active</span>
</p>
```

---

## Semantic Elements

**Definition:** HTML5 elements that describe meaning — they tell browsers and search engines what the content is, not just how it looks.

### Page Structure Elements
**Definition:** Divide a page into meaningful regions — better than using generic divs for everything.
```html
<header>    <!-- Site or section header — logo, nav -->
<nav>       <!-- Navigation links -->
<main>      <!-- Main content — use only once per page -->
<section>   <!-- Thematic grouping of content -->
<article>   <!-- Self-contained content (blog post, news) -->
<aside>     <!-- Sidebar or supplementary content -->
<footer>    <!-- Bottom of page or section -->
```

### Usage Example
**Definition:** A real-world page layout using semantic elements correctly.
```html
<body>
  <header>
    <h1>My Website</h1>
    <nav>
      <a href="/">Home</a>
      <a href="/about">About</a>
      <a href="/contact">Contact</a>
    </nav>
  </header>

  <main>
    <section>
      <h2>Latest Articles</h2>

      <article>
        <h3>Article Title</h3>
        <p>Article content...</p>
      </article>
    </section>

    <aside>
      <h3>Related Links</h3>
      <ul>
        <li><a href="#">Link 1</a></li>
      </ul>
    </aside>
  </main>

  <footer>
    <p>&copy; 2025 My Website. All rights reserved.</p>
  </footer>
</body>
```

### Other Semantic Elements
**Definition:** Additional elements with specific semantic meaning.
```html
<time datetime="2025-01-15">January 15, 2025</time>
<details>
  <summary>Click to expand</summary>
  <p>Hidden content revealed on click.</p>
</details>
<progress value="70" max="100">70%</progress>
<meter value="6" min="0" max="10">6 out of 10</meter>
<mark>Highlighted text</mark>
```

---

## Audio & Video

**Definition:** Embed media directly in the browser — HTML5 handles audio and video natively.

### Audio
**Definition:** Embed a sound file — include multiple formats for browser compatibility.
```html
<audio controls>
  <source src="music.mp3" type="audio/mpeg">
  <source src="music.ogg" type="audio/ogg">
  Your browser does not support the audio element.
</audio>

<!-- With extra attributes -->
<audio controls autoplay loop muted>
  <source src="background.mp3" type="audio/mpeg">
</audio>
```

### Video
**Definition:** Embed a video file — `controls` adds play/pause/volume — always provide `width` and `height`.
```html
<video width="640" height="360" controls>
  <source src="movie.mp4"  type="video/mp4">
  <source src="movie.webm" type="video/webm">
  Your browser does not support video.
</video>

<!-- With extra attributes -->
<video width="1280" height="720" controls autoplay muted loop poster="thumbnail.jpg">
  <source src="video.mp4" type="video/mp4">
</video>
```

### Media Attributes Reference
**Definition:** Common attributes for both `<audio>` and `<video>` elements.

| Attribute | Meaning |
|-----------|---------|
| `controls` | Show play/pause/volume controls |
| `autoplay` | Start playing automatically |
| `loop` | Replay when finished |
| `muted` | Start with sound off |
| `poster` | Image shown before video plays (video only) |
| `preload` | `auto` / `metadata` / `none` |

---

## iFrames

**Definition:** Embeds another HTML page or external content inside the current page.

### Basic iFrame
**Definition:** Load an external webpage inside a box on your page.
```html
<iframe
  src="https://example.com"
  width="800"
  height="400"
  title="Example website">
</iframe>
```

### Embed YouTube Video
**Definition:** YouTube's embed code uses an iframe — always use the `/embed/` URL format.
```html
<iframe
  width="560"
  height="315"
  src="https://www.youtube.com/embed/VIDEO_ID"
  title="YouTube video"
  allowfullscreen>
</iframe>
```

### Embed Google Map
**Definition:** Display a Google Maps location on your page using an iframe.
```html
<iframe
  src="https://maps.google.com/maps?q=Mumbai&output=embed"
  width="600"
  height="400"
  style="border:0;"
  allowfullscreen>
</iframe>
```

### Security Attribute
**Definition:** `sandbox` restricts what the iframe content can do — improves security.
```html
<iframe
  src="untrusted.html"
  sandbox="allow-scripts allow-same-origin">
</iframe>
```

---

## Attributes

**Definition:** Attributes provide additional information about elements — always written in the opening tag.

### How Attributes Work
**Definition:** Attributes are `name="value"` pairs written inside the opening tag.
```html
<element attribute="value">Content</element>

<a href="https://google.com" target="_blank" title="Go to Google">Google</a>
<!-- href     → where to go -->
<!-- target   → how to open it -->
<!-- title    → tooltip text on hover -->
```

### Common Attributes
**Definition:** Attributes used across many different HTML elements.

| Attribute | Used on | Purpose |
|-----------|---------|---------|
| `src` | `img`, `script`, `audio`, `video` | Source file path |
| `href` | `a`, `link` | Hyperlink URL |
| `alt` | `img` | Alternative text |
| `title` | Most elements | Tooltip on hover |
| `class` | Most elements | CSS/JS class names |
| `id` | Most elements | Unique identifier |
| `style` | Most elements | Inline CSS |
| `width` / `height` | `img`, `video`, `table` | Size |
| `disabled` | Form elements | Disable interaction |
| `placeholder` | `input`, `textarea` | Hint text |
| `required` | Form inputs | Must be filled |
| `type` | `input`, `button`, `link` | Element type |
| `name` | Form elements | Field name for server |
| `value` | Form elements | Default/current value |

---

## Global Attributes

**Definition:** Attributes that can be used on ANY HTML element — not specific to one tag.

### Identification
**Definition:** Give elements unique or shared identifiers for CSS and JavaScript.
```html
<div id="main-content">...</div>       <!-- Unique — only one per page -->
<p class="highlight bold">...</p>      <!-- Multiple classes, reusable -->
<span class="tag tag-html">HTML</span>
```

### Style & Display
**Definition:** Apply inline styles or hide elements entirely.
```html
<p style="color: red; font-size: 18px;">Red text</p>
<div hidden>This is invisible</div>    <!-- Hides element completely -->
```

### Interaction
**Definition:** Control whether users can interact with an element.
```html
<input tabindex="1">      <!-- Tab order — 1 gets focus first -->
<input tabindex="-1">     <!-- Removes from tab order -->
<div contenteditable="true">Users can type and edit this text.</div>
<p draggable="true">Drag me around!</p>
<div spellcheck="true">Spellcheck this content</div>
```

### Language & Direction
**Definition:** Set the language and reading direction of content — important for international sites.
```html
<html lang="en">                     <!-- English (set on html tag) -->
<p lang="hi">नमस्ते</p>              <!-- Hindi paragraph -->
<p dir="rtl">مرحبا بالعالم</p>       <!-- Right-to-left text (Arabic) -->
<p dir="ltr">Left to right text</p>  <!-- Left-to-right (default) -->
```

---

## Classes & IDs

**Definition:** Ways to target specific elements — used by CSS for styling and JavaScript for manipulation.

### ID
**Definition:** Unique identifier — only one element on a page should have a given ID.
```html
<h1 id="page-title">Welcome</h1>
<div id="hero-section">...</div>

<!-- In CSS: #page-title { color: blue; } -->
<!-- In JS:  document.getElementById("page-title") -->
<!-- In link: <a href="#page-title">Jump to title</a> -->
```

### Class
**Definition:** Reusable label — multiple elements can share a class, one element can have multiple classes.
```html
<p class="highlight">Important text</p>
<p class="highlight bold large">Multiple classes</p>
<button class="btn btn-primary">Click</button>
<button class="btn btn-danger">Delete</button>

<!-- In CSS: .highlight { background: yellow; } -->
<!-- In JS:  document.querySelectorAll(".highlight") -->
```

### When to Use What
**Definition:** Use IDs for unique page elements, classes for reusable styles.

| | `id` | `class` |
|--|------|---------|
| Uniqueness | One per page | Many elements |
| CSS selector | `#myId` | `.myClass` |
| JS selector | `getElementById()` | `querySelectorAll()` |
| Use for | Unique sections, anchors | Reusable styles |

---

## Comments

**Definition:** Notes in your HTML code — visible in source code but never displayed in the browser.

### Single and Multi-line Comments
**Definition:** Everything between `<!--` and `-->` is ignored by the browser.
```html
<!-- This is a comment — not visible on the page -->

<!--
  This is a
  multi-line comment
-->

<p>Visible content</p>
<!-- <p>This paragraph is commented out — hidden</p> -->
```

---

## Entities & Special Characters

**Definition:** HTML entities display reserved or special characters that would otherwise be misinterpreted.

### Common Entities
**Definition:** Use these when you need to display characters that HTML would treat as code.
```html
&lt;       <!-- < (less than) -->
&gt;       <!-- > (greater than) -->
&amp;      <!-- & (ampersand) -->
&quot;     <!-- " (quotation mark) -->
&apos;     <!-- ' (apostrophe) -->
&nbsp;     <!-- Non-breaking space (prevents line break) -->
&copy;     <!-- © (copyright) -->
&reg;      <!-- ® (registered trademark) -->
&trade;    <!-- ™ (trademark) -->
&euro;     <!-- € (euro sign) -->
&pound;    <!-- £ (pound sign) -->
&yen;      <!-- ¥ (yen sign) -->
&mdash;    <!-- — (em dash) -->
&ndash;    <!-- – (en dash) -->
&hellip;   <!-- … (ellipsis) -->
&hearts;   <!-- ♥ (heart symbol) -->
&star;     <!-- ★ (star symbol) -->
```

### Usage Example
**Definition:** When your content contains characters that conflict with HTML syntax.
```html
<p>Use &lt;h1&gt; for the main heading.</p>
<!-- Displays: Use <h1> for the main heading. -->

<p>Price: &euro;99 &amp; &pound;85</p>
<!-- Displays: Price: €99 & £85 -->
```

---

## Head Elements

**Definition:** Elements that go inside `<head>` — they provide metadata and link external resources.

### Title
**Definition:** The page title shown in the browser tab and in search results.
```html
<title>My Website — Home Page</title>
```

### Link External Resources
**Definition:** Connect external CSS files, icons, and fonts to the page.
```html
<!-- CSS stylesheet -->
<link rel="stylesheet" href="styles.css">

<!-- Favicon (tab icon) -->
<link rel="icon" type="image/png" href="favicon.png">
<link rel="icon" type="image/x-icon" href="favicon.ico">

<!-- Apple touch icon (iOS) -->
<link rel="apple-touch-icon" href="apple-icon.png">

<!-- Canonical URL (SEO — avoid duplicate content) -->
<link rel="canonical" href="https://example.com/page">

<!-- Google Fonts -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Roboto&display=swap" rel="stylesheet">
```

### Base URL
**Definition:** Sets the base URL for all relative links on the page.
```html
<base href="https://example.com/">
<!-- Now href="about" resolves to https://example.com/about -->
```

---

## Linking CSS & JS

**Definition:** Connect stylesheets and scripts to your HTML — placement matters for performance.

### Link CSS (in `<head>`)
**Definition:** Always put CSS in the `<head>` so styles load before content appears.
```html
<head>
  <!-- External CSS file -->
  <link rel="stylesheet" href="styles.css">

  <!-- Inline CSS — styles in the HTML file itself -->
  <style>
    body { font-family: Arial, sans-serif; }
    h1   { color: navy; }
  </style>
</head>
```

### Link JavaScript
**Definition:** Put scripts before `</body>` to avoid blocking page rendering — or use `defer`.
```html
<!-- At bottom of body — traditional approach -->
<body>
  <p>Page content...</p>
  <script src="app.js"></script>
</body>

<!-- In head with defer — modern approach (loads after HTML parsed) -->
<head>
  <script src="app.js" defer></script>
</head>

<!-- In head with async — loads in parallel, runs immediately when ready -->
<head>
  <script src="analytics.js" async></script>
</head>

<!-- Inline JavaScript -->
<script>
  console.log("Hello from JavaScript!");
</script>
```

### Script Attributes
**Definition:** Control how external JavaScript files are loaded and executed.

| Attribute | Behavior |
|-----------|---------|
| (none) | Blocks HTML parsing while loading |
| `defer` | Loads in background, runs after HTML is parsed |
| `async` | Loads in background, runs immediately when ready |
| `type="module"` | ES module support with `defer` by default |

---

## Block vs Inline Elements

**Definition:** Block elements take full width and start on new lines — inline elements sit within text flow.

### Block Elements
**Definition:** Each one starts on a new line and stretches to fill the full container width.
```html
<div>    — generic block container
<p>      — paragraph
<h1>–<h6> — headings
<ul>     — unordered list
<ol>     — ordered list
<li>     — list item
<table>  — table
<form>   — form
<header>, <footer>, <main>, <section>, <article>, <aside>, <nav>
<blockquote>
<pre>
<hr>
```

### Inline Elements
**Definition:** Sit inside a line of text — only as wide as their content, no line break before or after.
```html
<span>   — generic inline container
<a>      — link
<img>    — image
<strong> — bold
<em>     — italic
<code>   — code
<input>  — form input
<button> — button
<label>  — form label
<br>     — line break
<abbr>   — abbreviation
<mark>   — highlight
<small>  — small text
```

### Quick Comparison
**Definition:** The key difference in how they behave in the document flow.

| | Block | Inline |
|--|-------|--------|
| New line | Yes | No |
| Width | Full container | Content only |
| Can set width/height | Yes | No (by default) |
| Examples | `div`, `p`, `h1` | `span`, `a`, `img` |

---

## HTML5 Semantic Layout

**Definition:** A complete real-world page layout using semantic HTML5 elements correctly.

### Full Page Template
**Definition:** A professional HTML5 page structure with all regions properly marked up.
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Page description for SEO">
  <title>Page Title | Site Name</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>

  <!-- Site header — logo and navigation -->
  <header>
    <a href="/" class="logo">
      <img src="logo.png" alt="Site Name">
    </a>
    <nav aria-label="Main navigation">
      <ul>
        <li><a href="/">Home</a></li>
        <li><a href="/blog">Blog</a></li>
        <li><a href="/contact">Contact</a></li>
      </ul>
    </nav>
  </header>

  <!-- Hero / Banner section -->
  <section class="hero">
    <h1>Welcome to My Website</h1>
    <p>Building great things on the web.</p>
    <a href="/start" class="btn">Get Started</a>
  </section>

  <!-- Main content area -->
  <main>

    <!-- Blog posts section -->
    <section>
      <h2>Latest Articles</h2>

      <article>
        <header>
          <h3><a href="/post/1">Article Title</a></h3>
          <p>By <a href="/author/dark">Dark</a> on
             <time datetime="2025-01-15">January 15, 2025</time></p>
        </header>
        <p>Article summary goes here...</p>
        <footer>
          <a href="/post/1">Read more</a>
        </footer>
      </article>

    </section>

    <!-- Sidebar -->
    <aside>
      <h2>Categories</h2>
      <ul>
        <li><a href="/category/html">HTML</a></li>
        <li><a href="/category/css">CSS</a></li>
      </ul>
    </aside>

  </main>

  <!-- Site footer -->
  <footer>
    <nav aria-label="Footer navigation">
      <a href="/privacy">Privacy Policy</a>
      <a href="/terms">Terms</a>
    </nav>
    <p>&copy; 2025 My Website. All rights reserved.</p>
  </footer>

  <script src="app.js" defer></script>
</body>
</html>
```

---

## Data Attributes

**Definition:** Custom attributes to store extra data on HTML elements — accessible via JavaScript and CSS.

### Creating Data Attributes
**Definition:** Any attribute starting with `data-` is a valid custom data attribute.
```html
<div data-user-id="42"
     data-role="admin"
     data-active="true">
  User card
</div>

<button data-action="delete"
        data-target="user-42">
  Delete
</button>

<li data-category="fruit"
    data-price="1.99">Apple</li>
```

### Accessing in JavaScript
**Definition:** Use the `dataset` property to read or write data attributes in JavaScript.
```javascript
const div = document.querySelector("div");

div.dataset.userId     // "42"
div.dataset.role       // "admin"
div.dataset.active     // "true"

div.dataset.score = "100"    // Set new value
```

### Accessing in CSS
**Definition:** Use `attr()` or attribute selectors to style elements based on data attributes.
```css
/* Select elements with a specific data attribute value */
[data-role="admin"] { background: gold; }

/* Show data attribute value as content */
[data-price]::after { content: " — $" attr(data-price); }
```

---

## Accessibility (ARIA)

**Definition:** ARIA (Accessible Rich Internet Applications) attributes help screen readers understand your content.

### ARIA Labels
**Definition:** Provide meaningful names for elements that don't have visible text labels.
```html
<!-- Label a button with no text -->
<button aria-label="Close dialog">✕</button>

<!-- Label a search form -->
<form aria-label="Site search">
  <input type="search" aria-label="Search terms">
  <button type="submit">🔍</button>
</form>

<!-- Describe by another element -->
<input type="text" aria-describedby="name-hint">
<p id="name-hint">Enter your full name as it appears on your ID.</p>
```

### ARIA Roles
**Definition:** Tell assistive technology what role an element plays on the page.
```html
<div role="alert">Form submitted successfully!</div>
<div role="navigation">...</div>
<div role="main">...</div>
<div role="banner">...</div>
<div role="dialog" aria-modal="true">Modal content</div>
<button role="tab" aria-selected="true">Tab 1</button>
```

### ARIA States
**Definition:** Communicate the current state of interactive elements to screen readers.
```html
<button aria-expanded="false">Show Menu</button>
<button aria-pressed="true">Bold</button>
<input type="checkbox" aria-checked="true">
<div aria-hidden="true">Decorative — hidden from screen readers</div>
<li aria-current="page"><a href="/">Home</a></li>
```

### Live Regions
**Definition:** Announce dynamic content changes to screen readers without requiring focus.
```html
<!-- Screen reader reads this when content changes -->
<div aria-live="polite" id="status">
  Loading results...
</div>

<!-- Urgent — interrupts current speech -->
<div aria-live="assertive" id="error">
  Error: Connection lost!
</div>
```

### Accessibility Basics
**Definition:** Simple rules that make every page more accessible.
```html
<!-- Always write alt text for images -->
<img src="dog.jpg" alt="A golden retriever running in a park">

<!-- Decorative images — empty alt so screen readers skip them -->
<img src="divider.png" alt="">

<!-- Use semantic HTML — it's accessible by default -->
<button>Click me</button>                  <!-- Focusable, keyboard accessible -->
<div onclick="...">Click me</div>          <!-- Not accessible — avoid this -->

<!-- Label all form inputs -->
<label for="email">Email address:</label>
<input type="email" id="email" name="email">

<!-- Navigation landmarks -->
<nav aria-label="Main navigation">...</nav>
<nav aria-label="Breadcrumb">...</nav>
```

---

## Meta for SEO & Social

**Definition:** Meta tags that improve search engine ranking and control how your page appears when shared.

### Basic SEO
**Definition:** Essential tags that every page should have for search visibility.
```html
<title>How to Learn HTML — Complete Guide | MySite</title>
<meta name="description" content="A complete beginner's guide to HTML with examples. Learn HTML5 in 2025.">
<link rel="canonical" href="https://example.com/learn-html">
```

### Open Graph (Facebook, LinkedIn)
**Definition:** Controls how your page appears when shared on Facebook, LinkedIn, and most social platforms.
```html
<meta property="og:title"       content="How to Learn HTML">
<meta property="og:description" content="A complete beginner's guide to HTML.">
<meta property="og:image"       content="https://example.com/image.jpg">
<meta property="og:url"         content="https://example.com/learn-html">
<meta property="og:type"        content="article">
<meta property="og:site_name"   content="MySite">
```

### Twitter Card
**Definition:** Controls how your page appears when shared on Twitter/X.
```html
<meta name="twitter:card"        content="summary_large_image">
<meta name="twitter:title"       content="How to Learn HTML">
<meta name="twitter:description" content="A complete beginner's guide to HTML.">
<meta name="twitter:image"       content="https://example.com/image.jpg">
<meta name="twitter:site"        content="@yourusername">
```

### Robots
**Definition:** Tell search engine crawlers whether to index the page and follow its links.
```html
<meta name="robots" content="index, follow">      <!-- Default — index this page -->
<meta name="robots" content="noindex, nofollow">  <!-- Don't index, don't follow links -->
<meta name="robots" content="noindex, follow">    <!-- Don't index but follow links -->
```

---

## Best Practices

**Definition:** Guidelines for writing clean, accessible, maintainable, and well-structured HTML.

### Structure
**Definition:** Keep your HTML logical and hierarchical — use semantic elements wherever possible.
```html
<!-- Bad — div soup, no meaning -->
<div class="top">
  <div class="nav-wrap">
    <div class="nav">
      <div class="nav-item">Home</div>
    </div>
  </div>
</div>

<!-- Good — semantic, readable -->
<header>
  <nav>
    <a href="/">Home</a>
  </nav>
</header>
```

### Always Write Alt Text
**Definition:** Every `<img>` needs `alt` — screen readers and search engines depend on it.
```html
<!-- Bad — no alt -->
<img src="chart.png">

<!-- Good — descriptive alt text -->
<img src="chart.png" alt="Bar chart showing 40% increase in sales from Q1 to Q2 2025">

<!-- Decorative image — empty alt tells screen reader to skip it -->
<img src="decorative-line.png" alt="">
```

### Use Lowercase & Quote Attributes
**Definition:** HTML is case-insensitive but convention is lowercase — always quote attribute values.
```html
<!-- Bad -->
<A HREF=https://google.com CLASS=link>Go</A>

<!-- Good -->
<a href="https://google.com" class="link">Go</a>
```

### Meaningful Title & Description
**Definition:** Write unique, descriptive titles and meta descriptions for every page.
```html
<!-- Bad — too vague -->
<title>Home</title>
<meta name="description" content="Welcome to our website.">

<!-- Good — specific and keyword-rich -->
<title>Buy Running Shoes Online — Free Shipping | SportZone</title>
<meta name="description" content="Shop 500+ running shoes with free next-day shipping. Top brands including Nike, Adidas, and Asics.">
```

### Form Accessibility
**Definition:** Every form input must have a label — never rely on placeholder text alone.
```html
<!-- Bad — no label, placeholder only -->
<input type="text" placeholder="Your name">

<!-- Good — proper label -->
<label for="name">Your Name</label>
<input type="text" id="name" name="name" placeholder="e.g. John Doe">
```

### Validate Your HTML
**Definition:** Use the official W3C validator to find and fix markup errors.
```
https://validator.w3.org/
```

### Summary of Rules

* Use `<!DOCTYPE html>` on the first line — always
* Always include `charset`, `viewport`, and `title` in `<head>`
* Use **semantic elements** — `header`, `main`, `footer`, `article`, `section`
* Every `<img>` must have an `alt` attribute
* Every form `<input>` must have a `<label>`
* Use **one `<h1>` per page** — don't skip heading levels
* Put CSS in `<head>`, JavaScript before `</body>` or use `defer`
* Always **quote attribute values** and use **lowercase** tags
* Use **IDs** for unique elements, **classes** for reusable styles
* Test with the **W3C Validator** and check **accessibility**
