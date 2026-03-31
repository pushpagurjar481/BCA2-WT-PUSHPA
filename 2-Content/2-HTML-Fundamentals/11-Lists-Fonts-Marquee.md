# Day 11 — Lists, Font Styling & Marquee Tag

🔬 **Type:** Theory + Practical
🕐 **Duration:** 2 Hours
📚 **Unit:** 2 — HTML Fundamentals
🧪 **Lab Experiment:** 1 (Lists portion)

---

## Learning Objectives

By the end of this session, students will be able to:
- Create ordered, unordered, and definition lists
- Nest lists within lists
- Change list marker styles
- Use the Marquee tag for scrolling text
- Apply font color changes

---

## 1. Ordered Lists (`<ol>`)

An ordered list displays items with numbers.

```html
<h3>Steps to Create a Web Page</h3>
<ol>
    <li>Open a text editor (VS Code)</li>      <!-- Step 1 -->
    <li>Write HTML code</li>                   <!-- Step 2 -->
    <li>Save with .html extension</li>         <!-- Step 3 -->
    <li>Open in a web browser</li>             <!-- Step 4 -->
</ol>
```

> **Code Explanation:**
> - `<ol>` creates an **ordered (numbered) list** — items are automatically numbered 1, 2, 3…
> - Each `<li>` (list item) represents one item in the list
> - The browser adds numbers automatically — you don't need to type "1.", "2." etc.
> - The closing `</ol>` tells the browser where the list ends

### Changing the Number Type

```html
<ol type="1">  <!-- 1, 2, 3 (default) -->
<ol type="A">  <!-- A, B, C -->
<ol type="a">  <!-- a, b, c -->
<ol type="I">  <!-- I, II, III (Roman) -->
<ol type="i">  <!-- i, ii, iii -->
<ol start="5"> <!-- Start counting from 5 -->
```

> **Code Explanation:**
> - `type="1"` — default decimal numbers (1, 2, 3…)
> - `type="A"` — uppercase letters (A, B, C…) — useful for sub-questions in exams
> - `type="a"` — lowercase letters (a, b, c…)
> - `type="I"` — uppercase Roman numerals (I, II, III…) — commonly used for main sections
> - `type="i"` — lowercase Roman numerals (i, ii, iii…)
> - `start="5"` — the list starts counting from 5 instead of 1

---

## 2. Unordered Lists (`<ul>`)

An unordered list displays items with bullet points.

```html
<h3>Programming Languages</h3>
<ul>
    <li>Python</li>         <!-- Bullet item 1 -->
    <li>JavaScript</li>     <!-- Bullet item 2 -->
    <li>Java</li>           <!-- Bullet item 3 -->
    <li>C++</li>            <!-- Bullet item 4 -->
</ul>
```

> **Code Explanation:**
> - `<ul>` creates an **unordered (bulleted) list** — items appear with bullet markers instead of numbers
> - Use `<ul>` when the **order doesn't matter** (e.g., a list of features, languages, ingredients)
> - Use `<ol>` when the **order matters** (e.g., steps, rankings, instructions)

### Changing the Bullet Style

```html
<ul type="disc">    <!-- ● Filled circle (default) -->
<ul type="circle">  <!-- ○ Empty circle -->
<ul type="square">  <!-- ■ Filled square -->
<ul type="none">    <!-- No bullet -->
```

> **Code Explanation:**
> - `type="disc"` — default filled circle bullet (●)
> - `type="circle"` — hollow circle (○) — often used for nested list levels
> - `type="square"` — filled square (■) — gives a different visual appearance
> - `type="none"` — removes bullet markers entirely (useful for navigation menus styled with CSS)

---

## 3. Definition Lists (`<dl>`)

Used for terms and their definitions (like a glossary).

```html
<dl>
    <dt><strong>HTML</strong></dt>
    <dd>HyperText Markup Language — used for structuring web content.</dd>
    
    <dt><strong>CSS</strong></dt>
    <dd>Cascading Style Sheets — used for styling web pages.</dd>
    
    <dt><strong>JavaScript</strong></dt>
    <dd>A programming language for making web pages interactive.</dd>
</dl>
```

> **Code Explanation:**
> - `<dl>` creates a **definition list** container — used for term-definition pairs (like a dictionary or glossary)
> - `<dt>` is the **definition term** — the word or phrase being defined (displayed normally)
> - `<dd>` is the **definition description** — the meaning/explanation (automatically indented by the browser)
> - You can have **multiple `<dd>` tags** for a single `<dt>` if a term has multiple meanings

| Tag | Purpose |
|-----|---------|
| `<dl>` | Definition List container |
| `<dt>` | Definition Term (the word) |
| `<dd>` | Definition Description (the meaning, indented) |

### More Definition List Examples

Definition lists are useful in many real-world scenarios beyond glossaries:

**Example 1: FAQ Section (Frequently Asked Questions)**
```html
<!-- FAQ section for a university website -->
<h3>Frequently Asked Questions — BCA Admissions</h3>
<dl>
    <dt><strong>What is the eligibility for BCA?</strong></dt>
    <dd>10+2 pass from a recognized board with Mathematics as a subject.</dd>
    <dd>Minimum 45% aggregate marks (40% for reserved categories).</dd>
    
    <dt><strong>What is the course duration?</strong></dt>
    <dd>3 years (6 semesters), with each semester spanning approximately 6 months.</dd>
    
    <dt><strong>Is there a hostel facility?</strong></dt>
    <dd>Yes, separate hostels for boys and girls are available on campus at Mandsaur University.</dd>
</dl>
```

> **Code Explanation:**
> - This shows a FAQ where questions are `<dt>` and answers are `<dd>`
> - The first question has **two `<dd>` tags** — this is valid HTML; both descriptions are associated with the same term
> - This is a practical, real-world use of definition lists beyond just glossaries

**Example 2: Product Specification (Like Flipkart/Amazon)**
```html
<!-- Product specifications like an e-commerce site -->
<h3>Laptop Specifications — Lenovo IdeaPad</h3>
<dl>
    <dt><strong>Processor</strong></dt>
    <dd>Intel Core i5-12th Gen, 2.5 GHz base clock</dd>
    
    <dt><strong>RAM</strong></dt>
    <dd>8 GB DDR4, expandable to 16 GB</dd>
    
    <dt><strong>Storage</strong></dt>
    <dd>512 GB SSD (Solid State Drive)</dd>
    
    <dt><strong>Display</strong></dt>
    <dd>15.6 inch Full HD (1920 x 1080) IPS panel</dd>
    
    <dt><strong>Price</strong></dt>
    <dd>₹52,990 (inclusive of all taxes)</dd>
</dl>
```

> **Code Explanation:**
> - Here, `<dt>` holds the **specification name** (Processor, RAM, etc.) and `<dd>` holds the **specification value**
> - This is exactly how e-commerce sites like Flipkart and Amazon display product details
> - The ₹ symbol is used directly in HTML (it's a valid UTF-8 character)

**Example 3: Contact Information**
```html
<!-- Contact details using definition list -->
<h3>Contact Us — Mandsaur University</h3>
<dl>
    <dt><strong>📍 Address</strong></dt>
    <dd>Rewas Dewda Road, Mandsaur, Madhya Pradesh 458001</dd>
    
    <dt><strong>📞 Phone</strong></dt>
    <dd>+91 7422-252455</dd>
    <dd>+91 7422-252456 (Admission Office)</dd>
    
    <dt><strong>📧 Email</strong></dt>
    <dd>info@mandsauruniversity.edu.in</dd>
    
    <dt><strong>🌐 Website</strong></dt>
    <dd>www.mandsauruniversity.edu.in</dd>
</dl>
```

> **Code Explanation:**
> - Contact information naturally fits the term-definition pattern: label → value
> - The Phone entry has **two `<dd>` tags** for two different numbers — both are associated with the 📞 Phone term
> - Emoji characters (📍, 📞, 📧, 🌐) work directly in HTML as they are valid Unicode characters

---

## 4. Nested Lists

Lists can be placed inside other lists:

```html
<h3>BCA Curriculum</h3>
<ol>
    <li>Semester 1
        <ul>                                <!-- Nested unordered list inside an ordered list item -->
            <li>Programming in C</li>
            <li>Computer Fundamentals</li>
            <li>Mathematics</li>
        </ul>
    </li>
    <li>Semester 2
        <ul>
            <li>Web Technology</li>
            <li>Data Structures</li>
            <li>Discrete Mathematics</li>
        </ul>
    </li>
    <li>Semester 3
        <ul>
            <li>Database Management</li>
            <li>Object-Oriented Programming</li>
        </ul>
    </li>
</ol>
```

> **Code Explanation:**
> - The outer `<ol>` creates a numbered list (1. Semester 1, 2. Semester 2, etc.)
> - Inside each `<li>`, a `<ul>` creates a **nested bulleted list** for the subjects
> - The nested `<ul>` must be placed **inside** the `<li>` tag, not after `</li>` — this is a common mistake
> - You can nest any list type inside another: `<ol>` inside `<ul>`, `<ul>` inside `<ol>`, `<ul>` inside `<ul>`, etc.
> - Browsers automatically change bullet styles at each nesting level (disc → circle → square)

### List Accessibility

Screen readers (software used by visually impaired people) handle lists in a specific way that makes content easier to navigate:

| List Type | How Screen Readers Announce It |
|-----------|-------------------------------|
| `<ol>` | *"List, 4 items. 1. Open a text editor. 2. Write HTML code…"* — announces count and numbers |
| `<ul>` | *"List, 4 items. Bullet, Python. Bullet, JavaScript…"* — announces count and bullets |
| `<dl>` | *"Definition list, 3 items. Term: HTML. Definition: HyperText Markup Language…"* |
| Nested list | *"List, 3 items. 1. Semester 1. List, 3 items. Bullet, Programming in C…"* — announces nesting |

> 💡 **Why does this matter?**
> - Screen readers announce **how many items** are in the list — this helps users know what to expect
> - Users can **skip entire lists** using keyboard shortcuts, making navigation faster
> - If you use `<br>` tags and manual numbers instead of proper `<ol>`, screen readers **cannot** identify it as a list, making your page harder to use
> - **Rule:** Always use proper list tags (`<ol>`, `<ul>`, `<dl>`) instead of manually numbering items with text

---

## 5. The `<font>` Tag — Changing Font Color

```html
<font color="red" size="4" face="Georgia">This is red text in Georgia font</font>
<font color="#FF5722" size="6" face="Courier New">Orange in Courier</font>
```

> **Code Explanation:**
> - `color="red"` — sets the text colour (can use colour names like "red" or hex codes like "#FF5722")
> - `size="4"` — sets font size on a scale of 1 (smallest) to 7 (largest); default is 3
> - `face="Georgia"` — sets the font family (typeface); the browser uses this font if it's installed on the user's computer
> - The `<font>` tag wraps around the text you want to style

> ⚠️ Deprecated in HTML5 — use CSS `color`, `font-size`, `font-family` instead. Covered here as it's in the syllabus.

---

## 6. Marquee Tag

The `<marquee>` tag creates **scrolling text** or content.

```html
<!-- Basic scrolling text (left to right) -->
<marquee>Welcome to Mandsaur University!</marquee>

<!-- Different directions -->
<marquee direction="right">Right to left ←</marquee>
<marquee direction="up">Scrolling up ↑</marquee>
<marquee direction="down">Scrolling down ↓</marquee>
```

> **Code Explanation:**
> - `<marquee>` without attributes scrolls text from **right to left** by default (the most common direction)
> - `direction="right"` — text enters from the left and moves towards the right
> - `direction="up"` — text scrolls upward (useful for news tickers or notice boards)
> - `direction="down"` — text scrolls downward

### Marquee Attributes

| Attribute | Purpose | Values |
|-----------|---------|--------|
| `direction` | Scroll direction | `left`, `right`, `up`, `down` |
| `behavior` | Scroll behavior | `scroll` (continuous), `alternate` (bounce), `slide` (stop at edge) |
| `scrollamount` | Speed (pixels per frame) | Number (default: 6) |
| `scrolldelay` | Delay between frames (ms) | Number (default: 85) |
| `loop` | Number of loops | Number or `infinite` |
| `bgcolor` | Background color | Color name or hex |
| `width` | Width | Pixels or % |
| `height` | Height | Pixels |

### Marquee Examples

```html
<!-- Bouncing text -->
<marquee behavior="alternate" scrollamount="5">
    <font color="red" size="5">⚡ Flash Sale — 50% Off! ⚡</font>
</marquee>

<!-- Slow scroll with background -->
<marquee direction="up" height="100" scrollamount="2" bgcolor="#f0f0f0">
    <p>Notice 1: Exam schedule released</p>
    <p>Notice 2: Holiday on April 14</p>
    <p>Notice 3: Submit assignments by Friday</p>
</marquee>

<!-- Scrolling image -->
<marquee scrollamount="3">
    <img src="https://via.placeholder.com/100x50?text=Ad1" alt="Ad">
    &nbsp;&nbsp;&nbsp;
    <img src="https://via.placeholder.com/100x50?text=Ad2" alt="Ad">
</marquee>
```

> **Code Explanation:**
> - `behavior="alternate"` — text **bounces** back and forth between the edges (like a ball hitting walls)
> - `scrollamount="5"` — controls **speed**; higher number = faster scrolling (default is 6)
> - `direction="up" height="100"` — creates a **vertical scrolling box** of 100px height — commonly used for notice boards
> - `scrollamount="2"` — slow scrolling speed, suitable for reading notices
> - `bgcolor="#f0f0f0"` — light grey background for the scrolling area
> - The last example shows **scrolling images** — `<marquee>` can contain any HTML content, not just text
> - `&nbsp;&nbsp;&nbsp;` adds non-breaking spaces between the images for visual separation

> ⚠️ `<marquee>` is **deprecated** in HTML5 and not recommended for production websites. We cover it because it's in the syllabus. Use CSS animations instead (covered in Unit 4).

### Why `<marquee>` Was Deprecated

The `<marquee>` tag was introduced by **Microsoft Internet Explorer** in the 1990s and was never part of any official HTML standard. Here's why it was removed:

| Reason | Explanation |
|--------|-------------|
| **Not a standard** | It was a Microsoft-only tag, never approved by W3C (the organisation that makes HTML standards) |
| **Accessibility nightmare** | Screen readers cannot read moving text; users with cognitive disabilities find it distracting |
| **No user control** | Users cannot pause, stop, or slow down the animation (violates usability principles) |
| **Seizure risk** | Fast-moving content can trigger seizures in people with photosensitive epilepsy |
| **CSS can do it better** | CSS animations provide the same visual effect with much more control |

**Current Browser Support:**

| Browser | Support |
|---------|---------|
| Chrome | Still works (for backward compatibility) but may be removed anytime |
| Firefox | Still works but shows deprecation warning in developer tools |
| Safari | Still works |
| Edge | Still works (based on Chromium) |

> ⚠️ **Bottom line:** `<marquee>` works today in most browsers, but it can be removed without warning in future browser updates. For real-world projects, **always use CSS animations** instead.

### Modern Alternative: CSS Animation for Scrolling Text

Instead of `<marquee>`, you can achieve the same scrolling effect using **CSS `@keyframes` animation**. This is the modern, accessible, and standards-compliant approach:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS Marquee Alternative</title>
    <style>
        /* Container that hides content outside its boundaries */
        .scroll-container {
            width: 100%;
            overflow: hidden;          /* Hides text that goes outside the box */
            background-color: #FF5722;
            padding: 10px 0;
        }

        /* The scrolling text */
        .scroll-text {
            display: inline-block;
            white-space: nowrap;       /* Prevents text from wrapping to next line */
            color: white;
            font-size: 18px;
            animation: scroll-left 12s linear infinite;  /* Apply the animation */
        }

        /* Define the scrolling animation */
        @keyframes scroll-left {
            0% {
                transform: translateX(100%);   /* Start from right edge */
            }
            100% {
                transform: translateX(-100%);  /* End at left edge */
            }
        }

        /* Pause animation when user hovers — better accessibility! */
        .scroll-container:hover .scroll-text {
            animation-play-state: paused;
        }
    </style>
</head>
<body>
    <div class="scroll-container">
        <span class="scroll-text">
            📢 Admissions Open for 2026-27! Apply now at mandsauruniversity.edu.in
        </span>
    </div>
</body>
</html>
```

> **Code Explanation:**
> - `.scroll-container` uses `overflow: hidden` to **clip** any text that moves outside the box
> - `.scroll-text` uses `white-space: nowrap` to keep the text on a **single line** (prevents wrapping)
> - `animation: scroll-left 12s linear infinite` applies the animation named "scroll-left" that lasts 12 seconds, moves at constant speed (`linear`), and repeats forever (`infinite`)
> - `@keyframes scroll-left` defines the animation: text starts at `translateX(100%)` (fully off-screen right) and moves to `translateX(-100%)` (fully off-screen left)
> - `.scroll-container:hover .scroll-text` **pauses** the animation when the user hovers their mouse — this is a big accessibility improvement over `<marquee>` which cannot be paused
> - You'll learn CSS animations in detail in **Unit 4 (CSS)** — this is just a preview

---

## Practical Session

### 🧪 Lab Experiment 1 (Lists): Enhanced Department Page with Lists

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BCA Department</title>
</head>
<body bgcolor="#FAFAFA">

    <!-- Marquee announcement -->
    <marquee bgcolor="#FF5722" scrollamount="4">
        <font color="white" size="3">
            📢 Admissions Open for 2026-27! Apply now at mandsauruniversity.edu.in
        </font>
    </marquee>

    <h1 align="center">Department of Computer Applications</h1>
    <h2 align="center">Mandsaur University</h2>
    <hr>

    <h3>Programs Offered</h3>
    <ol type="I">
        <li><strong>BCA</strong> (Bachelor of Computer Applications)
            <ul type="circle">
                <li>Duration: 3 Years (6 Semesters)</li>
                <li>Eligibility: 10+2 with Mathematics</li>
                <li>Fee: Contact admission office</li>
            </ul>
        </li>
    </ol>

    <h3>Semester II Subjects</h3>
    <ol>
        <li>Web Technology
            <ul>
                <li>HTML, CSS, JavaScript</li>
                <li>Bootstrap Framework</li>
            </ul>
        </li>
        <li>Data Structures
            <ul>
                <li>Arrays, Linked Lists</li>
                <li>Stacks, Queues, Trees</li>
            </ul>
        </li>
        <li>Discrete Mathematics</li>
        <li>English Communication</li>
        <li>Environmental Studies</li>
    </ol>

    <h3>Key Features</h3>
    <ul type="square">
        <li>Industry-oriented curriculum</li>
        <li>Experienced faculty</li>
        <li>Modern computer labs</li>
        <li>Placement assistance</li>
        <li>Regular workshops and seminars</li>
    </ul>

    <h3>Technologies Taught</h3>
    <dl>
        <dt><font color="blue"><b>HTML</b></font></dt>
        <dd>The standard markup language for creating web pages.</dd>
        
        <dt><font color="blue"><b>CSS</b></font></dt>
        <dd>Stylesheet language for designing beautiful web pages.</dd>
        
        <dt><font color="blue"><b>JavaScript</b></font></dt>
        <dd>Programming language for adding interactivity to websites.</dd>
        
        <dt><font color="blue"><b>MySQL</b></font></dt>
        <dd>Relational database management system for data storage.</dd>
    </dl>

    <hr>
    <marquee behavior="alternate" scrollamount="3">
        <font color="green" size="4">🎓 Building Tomorrow's IT Leaders Today 🎓</font>
    </marquee>

</body>
</html>
```

> **Code Explanation (Lab Experiment 1):**
> - **Marquee announcement bar:** `bgcolor="#FF5722"` gives a bright orange background; `scrollamount="4"` controls scroll speed
> - **Ordered list with Roman numerals:** `<ol type="I">` uses Roman numerals (I, II, III) for main program listing
> - **Nested unordered list:** Inside each `<li>`, a `<ul type="circle">` creates a bulleted sub-list for program details
> - **Numbered list for subjects:** A plain `<ol>` lists semester subjects (1, 2, 3…), with nested `<ul>` for topic details
> - **Square bullets:** `<ul type="square">` uses filled squares (■) for the "Key Features" section — gives visual variety
> - **Definition list for technologies:** `<dl>` with `<dt>` for technology names and `<dd>` for descriptions — notice how `<font color="blue">` styles the term names
> - **Bouncing marquee footer:** `behavior="alternate"` makes the text bounce back and forth; `scrollamount="3"` controls speed

---

## Practice Exercise

Create `book-catalog.html`:
1. Use an ordered list to show "Top 5 Programming Books"
2. Each book should have a nested unordered list with: Author, Year, Rating
3. Add a definition list for 5 programming terms
4. Include a marquee at the top with "New Arrivals"
5. Use different list types (`type` attribute) across the page

---

## Summary

| Tag | Purpose |
|-----|---------|
| `<ol>` | Ordered list (numbered) |
| `<ul>` | Unordered list (bullets) |
| `<li>` | List item |
| `<dl>` | Definition list |
| `<dt>` | Definition term |
| `<dd>` | Definition description |
| `<marquee>` | Scrolling content (deprecated) |
| `<font>` | Font styling (deprecated) |

---

*Day 11 of 55 | Unit 2 — HTML Fundamentals | Web Technology (25BCA060)*
