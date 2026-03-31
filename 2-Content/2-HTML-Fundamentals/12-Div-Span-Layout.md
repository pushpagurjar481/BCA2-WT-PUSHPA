# Day 12 — Div, Span & Page Layout

🔬 **Type:** Theory + Practical
🕐 **Duration:** 2 Hours
📚 **Unit:** 2 — HTML Fundamentals
🧪 **Lab Experiment:** 7

---

## Learning Objectives

By the end of this session, students will be able to:
- Understand block vs inline elements
- Use `<div>` for section-level grouping
- Use `<span>` for inline text grouping
- Replace table-based layouts with div-based layouts
- Apply basic styling attributes to div elements

---

## 1. Block vs Inline Elements

### Block Elements

Block elements take up the **full width available** and start on a **new line**.

```
┌──────────────────────────────────────────┐
│ <h1>This is a heading (full width)       │
├──────────────────────────────────────────┤
│ <p>This paragraph also takes full width  │
├──────────────────────────────────────────┤
│ <div>Div is a block element             │
└──────────────────────────────────────────┘
```

Common block elements: `<div>`, `<p>`, `<h1>`–`<h6>`, `<table>`, `<ul>`, `<ol>`, `<form>`, `<hr>`

### Inline Elements

Inline elements only take up **as much width as needed** and do NOT start a new line.

```
This is a paragraph with <strong>bold</strong> and <em>italic</em> words inline.
```

Common inline elements: `<span>`, `<a>`, `<strong>`, `<em>`, `<img>`, `<b>`, `<i>`, `<code>`

### Comprehensive List: Block vs Inline Elements

Here is a complete reference of common HTML elements and their display type:

| Block Elements (Full Width, New Line) | Inline Elements (Content Width, Same Line) |
|---------------------------------------|-------------------------------------------|
| `<div>` — generic container | `<span>` — generic inline container |
| `<p>` — paragraph | `<a>` — hyperlink |
| `<h1>` to `<h6>` — headings | `<strong>` / `<b>` — bold text |
| `<ul>`, `<ol>` — lists | `<em>` / `<i>` — italic text |
| `<li>` — list item | `<img>` — image (inline by default) |
| `<table>` — table | `<input>` — form input field |
| `<form>` — form container | `<label>` — form label |
| `<hr>` — horizontal rule | `<br>` — line break |
| `<blockquote>` — quotation block | `<code>` — inline code |
| `<pre>` — preformatted text | `<sub>` / `<sup>` — subscript/superscript |
| `<address>` — contact info | `<abbr>` — abbreviation |
| `<fieldset>` — form group | `<cite>` — citation |

> 💡 **Easy Way to Remember:**
> - **Block elements** are like **paragraphs in a book** — each one starts on a new line and takes the full width
> - **Inline elements** are like **words in a sentence** — they sit next to each other on the same line
> - **Rule:** You can put inline elements inside block elements, but you should NOT put block elements inside inline elements

```html
<!-- ✅ Correct: Inline element inside block element -->
<p>Contact us at <a href="mailto:info@mu.edu.in">info@mu.edu.in</a></p>

<!-- ❌ Wrong: Block element inside inline element -->
<a href="#"><div>Click here</div></a>  <!-- Don't do this! -->
```

> **Code Explanation:**
> - The first example correctly places an `<a>` (inline) inside a `<p>` (block) — this is valid HTML
> - The second example puts a `<div>` (block) inside an `<a>` (inline) — this was invalid in HTML4 (though HTML5 relaxed this rule slightly, it's still bad practice)

---

## 2. The `<div>` Tag

> **Analogy:** `<div>` is like a **cardboard box** — it groups related items together. You can label the box, color it, size it, and move it around. By nesting boxes inside boxes, you build a page **layout**.

```html
<div style="background-color: #e0f7fa; padding: 15px; margin: 10px;">
    <h2>About Us</h2>
    <p>We are the BCA department at Mandsaur University.</p>
</div>

<div style="background-color: #fff3e0; padding: 15px; margin: 10px;">
    <h2>Our Courses</h2>
    <p>We offer BCA, a three-year undergraduate program.</p>
</div>
```

> **Code Explanation:**
> - Each `<div>` creates a **rectangular box** that groups related content together
> - `background-color: #e0f7fa` — sets a light cyan background colour for visual separation
> - `padding: 15px` — adds 15px of space **inside** the div (between content and the div's border)
> - `margin: 10px` — adds 10px of space **outside** the div (between the div and neighbouring elements)
> - The `<h2>` and `<p>` inside the div are **contained** within it — they inherit the background colour
> - Two separate `<div>` elements stack vertically (one below the other) because `<div>` is a block element

### Targeting Divs: ID vs Class

When you want to style or target specific `<div>` elements, you use the `id` or `class` attribute. Understanding the difference is essential for CSS (which you'll learn in Unit 4).

| Feature | `id` | `class` |
|---------|------|---------|
| **Uniqueness** | Must be **unique** on the page — only ONE element can have a given `id` | Can be **reused** — many elements can share the same `class` |
| **Analogy** | Like your **Aadhaar number** — unique to you alone | Like your **college name** — many students share it |
| **CSS selector** | `#header { ... }` (hash symbol) | `.card { ... }` (dot/period) |
| **Usage** | For one-of-a-kind elements (header, footer, main content) | For repeated elements (cards, buttons, menu items) |

```html
<!-- id: unique — only ONE element per page should have this id -->
<div id="main-header" style="background: #0D47A1; color: white; padding: 20px;">
    <h1>Mandsaur University</h1>
</div>

<!-- class: reusable — multiple elements can share the same class -->
<div class="info-card" style="background: #E8F5E9; padding: 15px; margin: 10px;">
    <h3>Computer Lab</h3>
    <p>60 workstations with high-speed internet</p>
</div>

<div class="info-card" style="background: #E8F5E9; padding: 15px; margin: 10px;">
    <h3>Library</h3>
    <p>50,000+ books and digital resources</p>
</div>

<div class="info-card" style="background: #E8F5E9; padding: 15px; margin: 10px;">
    <h3>Sports Complex</h3>
    <p>Indoor and outdoor sports facilities</p>
</div>
```

> **Code Explanation:**
> - `id="main-header"` — this div has a **unique ID**; no other element on this page should use "main-header"
> - `class="info-card"` — all three info boxes share the **same class**; when you learn CSS, you can style all `.info-card` elements at once with a single CSS rule
> - **When to use `id`:** Navigation links that jump to a section (`<a href="#main-header">`), unique page sections, JavaScript targeting
> - **When to use `class`:** Repeated patterns like cards, buttons, list items, notification boxes

### Common Uses of `<div>`

| Use | Description |
|-----|-------------|
| **Sections** | Group related content (header, footer, sidebar) |
| **Layout** | Create page structure (columns, rows) |
| **Styling target** | Apply CSS to a group of elements |
| **Wrapper** | Wrap the entire page content |

---

## 3. The `<span>` Tag

> **Analogy:** If `<div>` is a box, `<span>` is a **highlighter pen**. It marks a small piece of text within a line, without breaking the flow.

```html
<p>
    The exam is on <span style="color: red; font-weight: bold;">15th April</span> 
    in room <span style="background-color: yellow;">301</span>.
</p>
```

> **Code Explanation:**
> - The `<p>` tag creates a paragraph (block element) — it takes full width
> - `<span>` wraps around "15th April" and "301" **without breaking the line** — the text continues to flow normally
> - `color: red; font-weight: bold;` on the first `<span>` makes the date red and bold
> - `background-color: yellow;` on the second `<span>` highlights room number "301" with a yellow background
> - Without `<span>`, you would have to style the entire paragraph — `<span>` lets you target **specific words**

### Div vs Span

| Feature | `<div>` | `<span>` |
|---------|---------|----------|
| **Type** | Block element | Inline element |
| **Line break** | Starts on new line | Stays in the flow |
| **Default width** | Full width of parent | Only the content width |
| **Use for** | Sections, layouts, groups | Words, phrases within text |
| **Analogy** | A cardboard box | A highlighter pen |

---

## 4. Replacing Table Layouts with Div Layouts

In Day 10, we used tables for page layout. Now we replace that with `<div>` (the modern approach).

### Old Way (Table Layout) vs New Way (Div Layout)

**Old Way — Table:**
```html
<!-- Using a table for page layout — NOT recommended -->
<table width="100%">
    <tr>
        <td width="25%">Sidebar</td>     <!-- Table cell as sidebar -->
        <td width="75%">Main Content</td> <!-- Table cell as content -->
    </tr>
</table>
```

**New Way — Div (using inline styles for now, CSS later):**
```html
<!-- Using div elements for layout — the modern approach -->
<div style="width: 100%; overflow: hidden;">
    <div style="width: 25%; float: left; background: #eee; padding: 10px;">
        Sidebar
    </div>
    <div style="width: 70%; float: left; padding: 10px;">
        Main Content
    </div>
</div>
```

> **Code Explanation:**
> - The **outer div** (`overflow: hidden`) acts as a container — `overflow: hidden` is necessary to contain the floated elements inside it (without this, the container would collapse to zero height)
> - `float: left` on both inner divs makes them sit **side by side** instead of stacking vertically
> - `width: 25%` and `width: 70%` create a two-column layout (leaving 5% for spacing)
> - **Why is the new way better?** Tables are rigid and meant for data. Divs are flexible — you can easily reorder, resize, or restyle them with CSS. Screen readers also understand the difference between data tables and layout containers.

### ⚠️ Float Layout Limitations

While `float` works for simple layouts, it has several problems that led to the creation of **modern CSS layout tools** (Flexbox and Grid):

| Float Problem | Description |
|--------------|-------------|
| **Container collapse** | Parent div collapses to zero height if all children are floated — requires `overflow: hidden` hack |
| **Clearing issues** | Content after floated elements may wrap unexpectedly — requires `clear: both` |
| **Equal height columns** | Floated columns don't automatically match height — one may be shorter than the other |
| **Vertical centering** | Very difficult to vertically centre content inside floated divs |
| **Reordering** | Cannot change the visual order of elements without changing the HTML |
| **Responsive design** | Difficult to make float layouts adapt to different screen sizes |

> 💡 **Preview of Modern Alternatives (Unit 4 — CSS):**
> - **CSS Flexbox** — One-dimensional layout (rows OR columns). Perfect for navigation bars, card rows, centering.
> - **CSS Grid** — Two-dimensional layout (rows AND columns simultaneously). Perfect for full page layouts.
> - You'll learn both in Unit 4. For now, float layouts help you understand the concept of positioning elements side by side.

```
Float Layout (what we learn today):
┌──────────┬────────────────────────────┐
│ Sidebar  │ Main Content               │
│ (float)  │ (float)                    │
└──────────┴────────────────────────────┘
↑ Works, but has limitations

Flexbox Layout (Unit 4):
┌──────────┬────────────────────────────┐
│ Sidebar  │ Main Content               │  ← Automatic equal heights!
│ (flex)   │ (flex)                     │  ← Easy centering!
└──────────┴────────────────────────────┘
↑ Much better — use this in real projects
```

---

## 5. HTML5 Semantic Elements — The Modern Way

While `<div>` is versatile, it tells the browser nothing about the **meaning** of the content. HTML5 introduced **semantic elements** that describe their purpose:

| HTML5 Semantic Element | Replaces | Purpose |
|-----------------------|----------|---------|
| `<header>` | `<div id="header">` | Page or section header (logo, title, nav) |
| `<nav>` | `<div id="navigation">` | Navigation links |
| `<main>` | `<div id="content">` | Main content of the page (only one per page) |
| `<section>` | `<div class="section">` | A thematic section of content |
| `<article>` | `<div class="post">` | Self-contained content (blog post, news article) |
| `<aside>` | `<div id="sidebar">` | Sidebar or related content |
| `<footer>` | `<div id="footer">` | Page or section footer (copyright, links) |

> 💡 **Analogy:** Using `<div>` for everything is like labelling all rooms in your house as "Room 1", "Room 2", "Room 3". Using semantic elements is like labelling them "Kitchen", "Bedroom", "Bathroom" — anyone can immediately understand what each room is for.

**Comparison: Generic `<div>` vs Semantic HTML5**

```html
<!-- ❌ Old way: everything is a <div> -->
<div id="header">
    <h1>Mandsaur University</h1>
</div>
<div id="nav">
    <a href="#">Home</a> | <a href="#">About</a>
</div>
<div id="content">
    <p>Welcome to our university.</p>
</div>
<div id="footer">
    <p>&copy; 2026 Mandsaur University</p>
</div>

<!-- ✅ Modern way: semantic HTML5 elements -->
<header>
    <h1>Mandsaur University</h1>
</header>
<nav>
    <a href="#">Home</a> | <a href="#">About</a>
</nav>
<main>
    <p>Welcome to our university.</p>
</main>
<footer>
    <p>&copy; 2026 Mandsaur University</p>
</footer>
```

> **Code Explanation:**
> - Both examples produce visually **identical results** — semantic tags don't change appearance by default
> - The **difference is in meaning**: `<header>` tells browsers and screen readers "this is the page header", while `<div id="header">` is just a generic box that happens to be named "header"
> - **Screen readers** can jump directly to `<nav>`, `<main>`, or `<footer>` — this is not possible with generic `<div>` elements
> - **Search engines** (Google, Bing) use semantic tags to understand your page better, which can improve your search ranking (SEO)
> - You will learn to use these semantic elements extensively starting from **Unit 3 (HTML5)**

---

## Practical Session

### 🧪 Lab Experiment 7: Div/Span Layout for University Page

**Objective:** Recreate the university infrastructure page from Lab 6, but using `<div>` and `<span>` tags instead of tables.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>University Infrastructure - Div Layout</title>
</head>
<body style="margin: 0; font-family: Arial, sans-serif;">

    <!-- Header -->
    <div style="background-color: #0D47A1; color: white; padding: 20px; text-align: center;">
        <h1 style="margin: 0;">Mandsaur University</h1>
        <p style="margin: 5px 0 0 0;">Excellence in Education</p>
    </div>

    <!-- Navigation Bar -->
    <div style="background-color: #1565C0; padding: 10px; text-align: center;">
        <a href="#" style="color: white; text-decoration: none; margin: 0 15px;">Home</a>
        <a href="#" style="color: white; text-decoration: none; margin: 0 15px;">About</a>
        <a href="#" style="color: white; text-decoration: none; margin: 0 15px;">Departments</a>
        <a href="#" style="color: white; text-decoration: none; margin: 0 15px;">Facilities</a>
        <a href="#" style="color: white; text-decoration: none; margin: 0 15px;">Contact</a>
    </div>

    <!-- Main Content Wrapper -->
    <div style="max-width: 960px; margin: 20px auto; padding: 0 20px;">
        
        <!-- Two-column section -->
        <div style="overflow: hidden; margin-bottom: 20px;">
            <!-- Left column -->
            <div style="width: 48%; float: left;">
                <img src="https://via.placeholder.com/450x300?text=Computer+Lab" 
                     alt="Computer Lab" style="width: 100%;">
                <p style="text-align: center;"><strong>Computer Lab</strong></p>
            </div>
            <!-- Right column -->
            <div style="width: 48%; float: right;">
                <h2>Computer Labs</h2>
                <p>
                    Our computer labs feature <span style="color: #1565C0; font-weight: bold;">60 workstations</span> 
                    with high-speed internet connectivity.
                </p>
                <p>
                    Software: <span style="background-color: #E3F2FD; padding: 2px 6px;">VS Code</span>, 
                    <span style="background-color: #E3F2FD; padding: 2px 6px;">MySQL</span>, 
                    <span style="background-color: #E3F2FD; padding: 2px 6px;">Python</span>
                </p>
            </div>
        </div>
        
        <!-- Second two-column section (reversed) -->
        <div style="overflow: hidden; margin-bottom: 20px; clear: both;">
            <div style="width: 48%; float: left;">
                <h2>Library</h2>
                <p>
                    The central library has over 
                    <span style="color: red; font-weight: bold;">50,000 books</span> 
                    and digital resources.
                </p>
            </div>
            <div style="width: 48%; float: right;">
                <img src="https://via.placeholder.com/450x300?text=Library" 
                     alt="Library" style="width: 100%;">
                <p style="text-align: center;"><strong>Central Library</strong></p>
            </div>
        </div>

        <!-- Info boxes -->
        <div style="clear: both; overflow: hidden;">
            <div style="width: 30%; float: left; background: #E8F5E9; padding: 15px; margin: 1%; text-align: center;">
                <h3>Smart Classrooms</h3>
                <p>Projectors, interactive boards, and multimedia systems</p>
            </div>
            <div style="width: 30%; float: left; background: #FFF3E0; padding: 15px; margin: 1%; text-align: center;">
                <h3>Sports Complex</h3>
                <p>Indoor and outdoor sports facilities for all students</p>
            </div>
            <div style="width: 30%; float: left; background: #F3E5F5; padding: 15px; margin: 1%; text-align: center;">
                <h3>Hostels</h3>
                <p>Separate boys and girls hostels with modern amenities</p>
            </div>
        </div>
    </div>

    <!-- Footer -->
    <div style="clear: both; background-color: #0D47A1; color: white; text-align: center; padding: 15px; margin-top: 20px;">
        <p>&copy; 2026 Mandsaur University | All Rights Reserved</p>
    </div>

</body>
</html>
```

> **Code Explanation (Lab Experiment 7):**
> - **Header div:** `background-color: #0D47A1` creates a dark blue header; `text-align: center` centres all text inside it; `margin: 0` on the `<h1>` removes default heading margins
> - **Navigation div:** Links are styled inline with `color: white; text-decoration: none` (removes underline); `margin: 0 15px` adds horizontal spacing between links
> - **Content wrapper:** `max-width: 960px; margin: 20px auto` centres the content area and limits it to 960px wide — a common web design pattern
> - **Two-column layout:** `width: 48%; float: left` and `float: right` create two side-by-side columns; `overflow: hidden` on the parent prevents container collapse
> - **`<span>` for inline styling:** Used to highlight "60 workstations" in blue bold and "50,000 books" in red bold — without breaking the paragraph flow
> - **`<span>` for badges:** Software names (VS Code, MySQL, Python) are wrapped in `<span>` tags with light blue backgrounds, creating a badge-like effect
> - **Three info boxes:** Each box is `width: 30%; float: left; margin: 1%` — three boxes × 30% + margins = approximately 100% width
> - **Footer:** `clear: both` ensures the footer appears **below** all floated elements, not beside them

---

## Practice Exercise

Create `portfolio.html` — a personal portfolio page using only `<div>` and `<span>` (no tables):

1. **Header div** — Your name and tagline
2. **Navigation div** — Links to sections (About, Skills, Contact)
3. **About div** — A paragraph about yourself with `<span>` highlighting
4. **Skills div** — Three columns (Frontend, Backend, Tools) using floated divs
5. **Contact div** — Your contact details
6. **Footer div** — Copyright

---

## Summary

| Concept | Key Takeaway |
|---------|-------------|
| Block elements | Full width, new line (`<div>`, `<p>`, `<h1>`) |
| Inline elements | Flow within text (`<span>`, `<a>`, `<strong>`) |
| `<div>` | Groups block content; used for layouts and sections |
| `<span>` | Targets inline text for styling |
| `id` attribute | Unique identifier (one per page) — like an Aadhaar number |
| `class` attribute | Reusable identifier (many elements) — like a college name |
| Float layout | `float: left/right` creates multi-column layouts (has limitations) |
| HTML5 semantic tags | `<header>`, `<nav>`, `<main>`, `<footer>` — meaningful alternatives to `<div>` |
| Modern practice | Use `<div>` instead of `<table>` for page layout; use semantic tags when possible |

---

*Day 12 of 55 | Unit 2 — HTML Fundamentals | Web Technology (25BCA060)*
