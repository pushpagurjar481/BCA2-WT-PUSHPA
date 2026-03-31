# Day 7 — Text Formatting, Paragraphs & Alignment

🔬 **Type:** Theory + Practical
🕐 **Duration:** 2 Hours
📚 **Unit:** 2 — HTML Fundamentals
🧪 **Lab Experiment:** 1 (Part 2)

---

## Learning Objectives

By the end of this session, students will be able to:
- Apply text formatting tags (bold, italic, underline, etc.)
- Use text alignment attributes
- Understand the difference between physical and logical formatting
- Insert special characters and entities in HTML

---

## 1. Text Formatting Tags

### Physical Formatting (Visual)

These tags define **how text looks**:

```html
<b>Bold text</b>
<i>Italic text</i>
<u>Underlined text</u>
<s>Strikethrough text</s>
<small>Smaller text</small>
<big>Bigger text</big>  <!-- Deprecated in HTML5 -->
<sub>Subscript</sub>    <!-- H<sub>2</sub>O renders as H₂O -->
<sup>Superscript</sup>  <!-- x<sup>2</sup> renders as x² -->
```

> **Code Explanation:**
> - `<b>` — Makes text visually **bold**. It has no semantic meaning — it just changes appearance.
> - `<i>` — Makes text visually *italic*. Again, purely visual.
> - `<u>` — Draws an underline under text. Use with caution — users often confuse underlined text with clickable links.
> - `<s>` — Draws a line through text (strikethrough), suggesting the text is no longer accurate.
> - `<small>` — Renders text in a smaller font size. Useful for fine print or disclaimers.
> - `<big>` — Renders text in a larger font size. **Deprecated in HTML5** — use CSS `font-size` instead.
> - `<sub>` — Lowers text below the baseline. Used for chemical formulas like H₂O.
> - `<sup>` — Raises text above the baseline. Used for exponents like x² or footnote references.

### Logical/Semantic Formatting (Meaningful)

These tags define **what text means** (preferred in HTML5):

```html
<strong>Important text</strong>     <!-- Looks bold, but MEANS "important" -->
<em>Emphasized text</em>            <!-- Looks italic, but MEANS "emphasis" -->
<mark>Highlighted text</mark>       <!-- Yellow background highlight -->
<del>Deleted text</del>             <!-- Strikethrough — content removed -->
<ins>Inserted text</ins>            <!-- Underlined — content added -->
<code>Code snippet</code>           <!-- Monospace font for code -->
<pre>Preformatted    text</pre>     <!-- Preserves spaces and line breaks -->
```

> **Code Explanation:**
> - `<strong>` — Marks text as **important**. Looks bold, but tells screen readers to emphasize this content vocally.
> - `<em>` — Marks text as *emphasized*. Looks italic, but screen readers change their tone of voice for this text.
> - `<mark>` — Highlights text with a yellow background, like using a highlighter pen on a textbook.
> - `<del>` — Indicates text that has been **deleted/removed**. Displayed with a strikethrough.
> - `<ins>` — Indicates text that has been **inserted/added**. Displayed with an underline.
> - `<code>` — Displays text in a monospace (fixed-width) font. Used for short code snippets within a sentence.
> - `<pre>` — Preserves **all** whitespace (spaces, tabs, line breaks) exactly as written in the source code.

> **Why Semantic Tags Matter:**
>
> Screen readers (software used by visually impaired users) interpret semantic and physical tags very differently:
>
> | Tag | What the Screen Reader Does |
> |---|---|
> | `<strong>` | Announces the text with a **stronger, louder voice** to convey importance |
> | `<b>` | Does **nothing special** — reads the text in a normal voice (no meaning attached) |
> | `<em>` | Changes **tone of voice** to indicate emphasis, like stressing a word in conversation |
> | `<i>` | Does **nothing special** — just reads normally |
> | `<del>` | May announce "deleted" before reading the text, so the listener knows it was removed |
> | `<s>` | Typically ignored — the listener has no idea the text has a line through it |
>
> **Real-World Analogy:** Using `<b>` instead of `<strong>` is like writing a word in bold ink in a letter to a blind person — they cannot see the bold, so the emphasis is lost. `<strong>` is like verbally telling them, "This part is important!" which they can understand.
>
> **Bottom Line:** Always prefer `<strong>` over `<b>` and `<em>` over `<i>` in modern HTML. Your pages will be more accessible and meaningful.

### Physical vs Semantic — Comparison

| Physical | Semantic | Looks Like | Meaning |
|----------|----------|------------|---------|
| `<b>` | `<strong>` | **Bold** | Important |
| `<i>` | `<em>` | *Italic* | Emphasized |
| `<s>` | `<del>` | ~~Strikethrough~~ | Deleted/removed |
| `<u>` | `<ins>` | <u>Underline</u> | Inserted/added |

---

## 2. More Text Tags

### Quotations

```html
<!-- Block quote (indented paragraph) -->
<blockquote>
    "Education is the most powerful weapon which you can use 
    to change the world." — Nelson Mandela
</blockquote>

<!-- Inline quotation (adds quotation marks) -->
<p>As Steve Jobs said, <q>Stay hungry, stay foolish.</q></p>

<!-- Citation -->
<p>Reference: <cite>Web Technology by N.P. Gopalan</cite></p>
```

> **Code Explanation:**
> - `<blockquote>` — Creates an indented block of text for long quotations. The browser adds left margin automatically.
> - `<q>` — Used for short, inline quotations. The browser automatically adds quotation marks ("...") around the text.
> - `<cite>` — Used to reference the title of a work (book, article, website). Displayed in *italics* by default.
> - Using these tags instead of manually typing quotation marks helps screen readers identify quoted content correctly.

### Abbreviations & Definitions

```html
<!-- Abbreviation (shows full form on hover) -->
<p><abbr title="HyperText Markup Language">HTML</abbr> is fun!</p>

<!-- Address block -->
<address>
    Mandsaur University<br>
    Mandsaur, Madhya Pradesh<br>
    India
</address>
```

> **Code Explanation:**
> - `<abbr title="...">` — Wraps an abbreviation. When the user hovers their mouse over the text, the full form appears as a tooltip. Very useful for technical terms.
> - `<address>` — A semantic tag for contact information. Browsers typically render it in *italics*. It should contain the address of the author or organization related to the page.
> - `<br>` inside `<address>` — Forces each line of the address onto a separate line, since `<address>` by itself would display everything in a single line.

### Preformatted Text

```html
<pre>
    This text preserves
    all    spaces    and
    line breaks exactly
    as written.
</pre>
```

> **Code Explanation:**
> - `<pre>` — Preserves **all whitespace** exactly as typed: multiple spaces, tabs, and line breaks are displayed as-is.
> - Without `<pre>`, the browser would collapse all those extra spaces into a single space and ignore line breaks.
> - The browser renders `<pre>` content in a **monospace font** (like Courier), where every character takes the same width.

> Useful for displaying code, poetry, or ASCII art.

### `<pre>` vs `<code>` — When to Use Each

Students often confuse `<pre>` and `<code>`. Here's the clear difference:

| Feature | `<pre>` | `<code>` |
|---|---|---|
| **Purpose** | Preserves whitespace and line breaks | Marks text as a code snippet |
| **Display** | Block-level (takes full width) | Inline (stays within the text flow) |
| **Whitespace** | Preserved exactly as written | Collapsed like normal text |
| **Font** | Monospace | Monospace |
| **Typical Use** | Multi-line code blocks, ASCII art, poetry | Short code mentions within a sentence |

```html
<!-- Use <code> for short inline code mentions -->
<p>The <code>bgcolor</code> attribute sets the background color.</p>

<!-- Use <pre> for multi-line code blocks or text where spacing matters -->
<pre>
function greet() {
    alert("Namaste!");
}
</pre>

<!-- Best practice: combine both for code blocks -->
<pre><code>
var name = "Rahul";
var city = "Mandsaur";
alert(name + " lives in " + city);
</code></pre>
```

> **Code Explanation:**
> - `<code>` alone is used inside a sentence to show a short piece of code, like mentioning a tag name.
> - `<pre>` alone preserves formatting — good for any text where spacing matters (addresses, poems, ASCII diagrams).
> - `<pre><code>...</code></pre>` — The **best practice** for displaying code blocks. `<pre>` preserves the formatting while `<code>` tells the browser (and screen readers) that the content is computer code.

> **Real-World Analogy:** Think of `<code>` like writing a word in a different handwriting style to show it's special — it stays in the same line. `<pre>` is like putting text inside a fixed-width box where every space and line break is exactly where you placed it.

### How Browsers Handle Whitespace

Understanding how browsers treat spaces and line breaks is important:

```html
<!-- What you type in your code: -->
<p>Hello      World!

How   are    you?</p>

<!-- What the browser displays: -->
<!-- "Hello World! How are you?" (all on one line, extra spaces collapsed) -->
```

> **Code Explanation:**
> - Browsers **collapse multiple spaces** into a single space.
> - Browsers **ignore line breaks** inside a `<p>` tag — everything flows as one continuous line of text.
> - To force a line break, use `<br>`. To preserve all spaces, use `<pre>`.

**Rules of Whitespace Collapsing:**

| What You Type | What Browser Shows | Why |
|---|---|---|
| `Hello      World` | `Hello World` | Multiple spaces become one space |
| A line break in source code | Treated as one space | Line breaks in HTML source are collapsed |
| `&nbsp;&nbsp;&nbsp;` | Three spaces | `&nbsp;` (non-breaking space) is never collapsed |
| Text inside `<pre>` | Exactly as typed | `<pre>` disables whitespace collapsing |

### The `<wbr>` Tag (Word Break Opportunity)

The `<wbr>` tag suggests a point where the browser **may** break a long word if needed (e.g., when the screen is too narrow):

```html
<p>Visit our website at https://www.mandsaur<wbr>university<wbr>.edu.in for more information.</p>

<p>Email: department.of.computer<wbr>.applications<wbr>@mandsaur<wbr>university.edu.in</p>
```

> **Code Explanation:**
> - `<wbr>` does **not** force a line break — it only **suggests** a break point if the line is too long for the available space.
> - Without `<wbr>`, a very long URL or email address might overflow its container and break the page layout.
> - Think of it as telling the browser: "If you need to break this long word, break it here."

---

## 3. Text Alignment

### Using the `align` Attribute (Old Way)

```html
<p align="left">Left aligned (default)</p>
<p align="center">Center aligned</p>
<p align="right">Right aligned</p>
<p align="justify">Justified text stretches to fill both margins evenly.</p>
```

> **Code Explanation:**
> - `align="left"` — Text sticks to the left margin (this is the default behaviour even without the attribute).
> - `align="center"` — Text is placed in the center of the page/container.
> - `align="right"` — Text sticks to the right margin.
> - `align="justify"` — Text stretches so both the left and right edges are perfectly aligned, like in a newspaper column.

> ⚠️ **Note:** The `align` attribute is deprecated in HTML5. Use CSS instead (which we'll learn in Unit 4). For now, it works and helps understand the concept.

### The `<center>` Tag (Deprecated)

```html
<center>
    <h1>This heading is centered</h1>
    <p>This paragraph is also centered</p>
</center>
```

> **Code Explanation:**
> - `<center>` — Centers everything inside it (headings, paragraphs, images, etc.).
> - This is a **block-level** tag — all child elements are centered within the page.
> - **Deprecated in HTML5** — the modern way is to use CSS: `text-align: center;` on the parent element, or `margin: 0 auto;` for block elements.

> ⚠️ Also deprecated in HTML5 — use CSS `text-align: center` instead.

---

## 4. HTML Entities (Special Characters)

Some characters have special meaning in HTML (like `<` and `>`). To display them, use **entities**:

| Character | Entity Name | Entity Number | Description |
|-----------|-------------|---------------|-------------|
| `<` | `&lt;` | `&#60;` | Less than |
| `>` | `&gt;` | `&#62;` | Greater than |
| `&` | `&amp;` | `&#38;` | Ampersand |
| `"` | `&quot;` | `&#34;` | Double quote |
| `'` | `&apos;` | `&#39;` | Single quote |
| ` ` | `&nbsp;` | `&#160;` | Non-breaking space |
| `©` | `&copy;` | `&#169;` | Copyright |
| `®` | `&reg;` | `&#174;` | Registered |
| `™` | `&trade;` | `&#8482;` | Trademark |
| `₹` | `&#8377;` | `&#8377;` | Indian Rupee |
| `→` | `&rarr;` | `&#8594;` | Right arrow |

### Example

```html
<p>Price: &#8377;500 &amp; above</p>
<p>The &lt;html&gt; tag is the root element.</p>
<p>&copy; 2026 Mandsaur University. All rights reserved.</p>
```

> **Code Explanation:**
> - `&#8377;` — Displays the Indian Rupee symbol ₹. Since there's no named entity for ₹, you must use the numeric code.
> - `&amp;` — Displays the ampersand character `&`. You cannot type `&` directly because the browser thinks it's the start of an entity.
> - `&lt;` and `&gt;` — Display `<` and `>` characters. Essential when you want to show HTML tags as text on the page.
> - `&copy;` — Displays the copyright symbol ©.

### More Commonly Used HTML Entities

Here are additional entities you will frequently need, especially for Indian websites:

| Character | Entity Name | Entity Number | Description |
|-----------|-------------|---------------|-------------|
| `₹` | — | `&#8377;` | Indian Rupee symbol |
| `€` | `&euro;` | `&#8364;` | Euro sign |
| `£` | `&pound;` | `&#163;` | British Pound |
| `¥` | `&yen;` | `&#165;` | Japanese Yen / Chinese Yuan |
| `°` | `&deg;` | `&#176;` | Degree symbol (e.g., 45°C) |
| `×` | `&times;` | `&#215;` | Multiplication sign |
| `÷` | `&divide;` | `&#247;` | Division sign |
| `•` | `&bull;` | `&#8226;` | Bullet point |
| `—` | `&mdash;` | `&#8212;` | Em dash (long dash) |
| `–` | `&ndash;` | `&#8211;` | En dash (medium dash, for ranges like 10–20) |
| `…` | `&hellip;` | `&#8230;` | Ellipsis (three dots) |
| `♥` | `&hearts;` | `&#9829;` | Heart symbol |
| `★` | — | `&#9733;` | Star symbol |
| `✓` | — | `&#10003;` | Checkmark |
| `✗` | — | `&#10007;` | Cross mark |

```html
<!-- Indian business examples -->
<p>Room rent: &#8377;2,500 per month</p>
<p>Temperature in Mandsaur: 42&deg;C</p>
<p>Sale: &#8377;999 &ndash; &#8377;4,999</p>
<p>Rating: &#9733;&#9733;&#9733;&#9733;&#9734; (4/5 stars)</p>
<p>Features: Fast &#10003; &bull; Reliable &#10003; &bull; Affordable &#10003;</p>
```

> **Code Explanation:**
> - `&#8377;` — The Rupee symbol ₹. Used in Indian e-commerce and business pages.
> - `&deg;` — The degree symbol °. Combine it with `C` for Celsius (e.g., `42&deg;C` shows as 42°C).
> - `&ndash;` — An en dash (–), used for number ranges like "₹999 – ₹4,999."
> - `&#9733;` and `&#9734;` — Filled star (★) and empty star (☆), often used for ratings.
> - `&#10003;` — A checkmark ✓, useful for feature lists and checklists.

---

## Practical Session

### 🧪 Lab Experiment 1 (Part 2): Enhanced Department Page

**Objective:** Enhance yesterday's department page with text formatting, alignment, and special characters.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BCA Department - Mandsaur University</title>
</head>
<body>

    <!-- Header Section -->
    <h1 align="center">Department of <em>Computer Applications</em> (BCA)</h1>
    <h2 align="center"><strong>Mandsaur University</strong>, Mandsaur</h2>
    
    <hr>

    <!-- About Section with Formatting -->
    <h3>About the Department</h3>
    <p>
        The Department of Computer Applications at <strong>Mandsaur University</strong> 
        offers a comprehensive <em>three-year</em> 
        <abbr title="Bachelor of Computer Applications">BCA</abbr> program. 
        The department is committed to producing <mark>skilled IT professionals</mark> 
        who can meet the growing demands of the technology industry.
    </p>

    <!-- Quote -->
    <blockquote>
        <em>"The only way to do great work is to love what you do."</em> 
        &mdash; Steve Jobs
    </blockquote>

    <!-- Course Details with Subscript/Superscript -->
    <h3>Course Highlights</h3>
    <p>
        Students learn technologies like <code>HTML</code>, <code>CSS</code>, 
        and <code>JavaScript</code>. The program covers 
        <strong>6 semesters</strong> with a focus on practical skills.
    </p>
    <p>
        Mathematical concepts like x<sup>2</sup> + y<sup>2</sup> = r<sup>2</sup> 
        and chemical formulas like H<sub>2</sub>O and CO<sub>2</sub> are 
        also used in various subjects.
    </p>

    <!-- Preformatted Text for Contact -->
    <h3>Contact</h3>
    <pre>
    Department of Computer Applications
    Mandsaur University
    Mandsaur, Madhya Pradesh 458001
    India
    </pre>

    <!-- Footer with Entities -->
    <hr>
    <p align="center">
        <small>&copy; 2026 Mandsaur University &bull; All Rights Reserved</small>
    </p>

</body>
</html>
```

> **Code Explanation:**
> - The page builds on Day 6's structure by adding text formatting to the department page.
> - `align="center"` on `<h1>` and `<h2>` centers the heading text (deprecated but functional for learning).
> - `<em>` wraps "Computer Applications" to give it semantic emphasis (italic).
> - `<strong>` wraps "Mandsaur University" to mark it as important (bold).
> - `<abbr title="...">` on "BCA" shows the full form ("Bachelor of Computer Applications") when hovered.
> - `<mark>` highlights "skilled IT professionals" with a yellow background to draw attention.
> - `<blockquote>` with `<em>` presents the Steve Jobs quote in an indented, italicized style.
> - `<code>` tags around "HTML", "CSS", and "JavaScript" display them in monospace font, indicating they are technical terms.
> - `<sup>` and `<sub>` are used for mathematical exponents (x²) and chemical subscripts (H₂O).
> - `<pre>` preserves the exact spacing and line breaks of the contact address.
> - `&copy;`, `&bull;` — HTML entities for the copyright symbol and bullet point in the footer.

### Practice Exercises

1. **Format a recipe page:** Create `recipe.html` with a recipe of your favorite dish. Use `<strong>` for ingredients, `<em>` for instructions, and `<mark>` for important tips.

2. **Create a resume page:** Build `resume.html` using:
   - `<h1>` for your name
   - `<h2>` for sections (Education, Skills, Hobbies)
   - `<strong>` and `<em>` for emphasis
   - `<pre>` for your address
   - `&bull;` entities for bullet points

---

## Summary

| Tag | Purpose | Example Output |
|-----|---------|-------|
| `<strong>` / `<b>` | Bold/Important | **Bold** |
| `<em>` / `<i>` | Italic/Emphasis | *Italic* |
| `<u>` / `<ins>` | Underline/Inserted | Underlined |
| `<del>` / `<s>` | Strikethrough/Deleted | ~~Deleted~~ |
| `<mark>` | Highlight | Highlighted |
| `<sub>` | Subscript | H₂O |
| `<sup>` | Superscript | x² |
| `<code>` | Inline code | `code` |
| `<pre>` | Preformatted text | Preserves spaces |
| `<blockquote>` | Block quotation | Indented quote |
| `&entity;` | Special characters | ©, ₹, → |

---

*Day 7 of 55 | Unit 2 — HTML Fundamentals | Web Technology (25BCA060)*
