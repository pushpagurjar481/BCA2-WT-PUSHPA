# Day 6 — Introduction to HTML: Structure, Head & Body

🔬 **Type:** Theory + Practical
🕐 **Duration:** 2 Hours
📚 **Unit:** 2 — HTML Fundamentals
🧪 **Lab Experiment:** 1 (Part 1)

---

## Learning Objectives

By the end of this session, students will be able to:
- Define HTML and explain its role in web development
- Write the basic structure of an HTML document
- Use the `<head>` and `<body>` sections correctly
- Create their first HTML webpage
- Use paragraph and heading tags

---

## 1. What is HTML?

### Definition

**HTML** (HyperText Markup Language) is the standard language for creating web pages. It describes the **structure** of a web page using a series of **elements** (tags).

> **Analogy:** If a webpage were a house, **HTML** would be the **skeleton/frame** — the walls, floors, and rooms. **CSS** would be the **paint and decoration**, and **JavaScript** would be the **electricity and plumbing** (making things work).

### Key Facts

| Fact | Detail |
|------|--------|
| **Created by** | Tim Berners-Lee (1991) |
| **Current version** | HTML5 (2014, Living Standard) |
| **File extension** | `.html` or `.htm` |
| **Interpreted by** | Web browsers (Chrome, Firefox, etc.) |
| **NOT a programming language** | It's a *markup* language — describes structure, doesn't have logic |

---

## 2. HTML Elements & Tags

### What is a Tag?

Tags are **keywords** enclosed in angle brackets that tell the browser how to display content.

```html
<tagname>Content goes here</tagname>
 └──┬──┘                   └───┬───┘
 Opening tag              Closing tag
```

### Types of Tags

| Type | Description | Example |
|------|-------------|---------|
| **Paired/Container** | Has opening and closing tags | `<p>Hello</p>` |
| **Self-closing/Empty** | No closing tag needed | `<br>`, `<hr>`, `<img>` |

### Anatomy of an HTML Element

```html
<p class="intro">Welcome to Web Technology!</p>
└┬┘ └────┬─────┘ └──────────┬──────────────┘└┬┘
Tag   Attribute           Content          Closing tag
```

---

## 3. Basic Structure of an HTML Document

Every HTML document follows this template:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My First Web Page</title>
</head>
<body>
    <!-- Your visible content goes here -->
    <h1>Hello, World!</h1>
    <p>This is my first web page.</p>
</body>
</html>
```

> **Code Explanation:**
> - `<!DOCTYPE html>` — Tells the browser this is an HTML5 document. Without it, the browser may render pages in unpredictable "quirks mode."
> - `<html lang="en">` — The root element wrapping the entire page. `lang="en"` tells browsers and screen readers the content is in English.
> - `<meta charset="UTF-8">` — Sets character encoding to UTF-8, supporting characters from all languages including Hindi (हिंदी) and symbols like ₹.
> - `<meta name="viewport" ...>` — Makes the page responsive on mobile devices by matching the device screen width.
> - `<title>` — Sets the text shown in the browser tab and in Google search results.
> - `<!-- ... -->` — An HTML comment, visible only in the source code, not rendered on the page.
> - `<h1>` and `<p>` — Visible content elements: a top-level heading and a paragraph of text.

### Line-by-Line Explanation

| Line | Tag | Purpose |
|------|-----|---------|
| 1 | `<!DOCTYPE html>` | Tells the browser this is an HTML5 document |
| 2 | `<html lang="en">` | Root element; `lang="en"` sets language to English |
| 3 | `<head>` | Contains metadata (info ABOUT the page, not visible) |
| 4 | `<meta charset="UTF-8">` | Character encoding (supports all languages) |
| 5 | `<meta name="viewport"...>` | Makes page mobile-responsive |
| 6 | `<title>` | Text shown in browser tab |
| 7 | `</head>` | End of metadata section |
| 8 | `<body>` | Contains all VISIBLE content |
| 11 | `</body>` | End of visible content |
| 12 | `</html>` | End of document |

### Head vs Body

```
┌──────────────────────────────────────┐
│ <head> — INVISIBLE (metadata)        │
│   • Page title (browser tab)         │
│   • Character encoding               │
│   • CSS links                        │
│   • Meta descriptions (for Google)   │
│   • Favicon                          │
├──────────────────────────────────────┤
│ <body> — VISIBLE (content)           │
│   • Text, images, videos             │
│   • Links, buttons, forms            │
│   • Tables, lists                    │
│   • Everything the user sees         │
└──────────────────────────────────────┘
```

### A Brief History of DOCTYPE

Before HTML5, DOCTYPE declarations were long and complicated. Here's how they have evolved:

| HTML Version | DOCTYPE Declaration |
|---|---|
| **HTML5** (Current) | `<!DOCTYPE html>` |
| **HTML 4.01 Strict** | `<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">` |
| **XHTML 1.0 Strict** | `<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">` |
| **HTML 3.2** | `<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2 Final//EN">` |

> **Good News:** In HTML5, you only need `<!DOCTYPE html>` — short, simple, and easy to remember! Earlier developers had to memorize or copy-paste those long declarations every time they created a new page.

> **Why does DOCTYPE matter?** Without a DOCTYPE, browsers enter **quirks mode** — they try to mimic old, buggy rendering behaviour from the 1990s. With `<!DOCTYPE html>`, the browser uses **standards mode**, which renders pages consistently and predictably.

### Accessibility: Why `lang="en"` Matters

The `lang` attribute on the `<html>` tag looks small but has a big impact:

| Who Benefits | How |
|---|---|
| **Screen readers** (JAWS, NVDA, VoiceOver) | Selects the correct voice and pronunciation. For example, `lang="hi"` triggers Hindi pronunciation. |
| **Search engines** (Google, Bing) | Returns your page in language-specific search results. |
| **Browsers** | Offers auto-translation when the user's preferred language differs from the page language. |
| **Spell-checkers** | Applies the correct dictionary while the user types in forms on your page. |

> **Real-World Analogy:** Think of the `lang` attribute like the language label on a book in a library. Without it, the librarian (browser) has to guess which language the book is written in, and might shelve it in the wrong section.

> **Tip for Indian Websites:** If your page is in Hindi, use `<html lang="hi">`. For a bilingual English-Hindi page, set the main language on `<html>` and override specific sections:
> ```html
> <html lang="en">
>   <body>
>     <p>This paragraph is in English.</p>
>     <p lang="hi">यह पैराग्राफ हिंदी में है।</p>
>   </body>
> </html>
> ```

### More Meta Tags in `<head>`

The `<head>` section can contain many useful meta tags beyond `charset` and `viewport`:

```html
<head>
    <!-- Basic meta tags (already covered) -->
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BCA Department - Mandsaur University</title>

    <!-- SEO meta tags — helps your page appear in Google searches -->
    <meta name="description" content="BCA Department at Mandsaur University offers a 3-year computer applications program in Mandsaur, MP.">
    <meta name="keywords" content="BCA, Mandsaur University, Computer Applications, Web Technology">
    <meta name="author" content="Mandsaur University">

    <!-- Open Graph tags — control how your link looks when shared on WhatsApp, Facebook, LinkedIn -->
    <meta property="og:title" content="BCA Department - Mandsaur University">
    <meta property="og:description" content="Learn about our BCA program and world-class facilities.">
    <meta property="og:image" content="https://www.mandsauruniversity.edu.in/campus.jpg">
    <meta property="og:url" content="https://www.mandsauruniversity.edu.in/bca">

    <!-- Favicon — the small icon shown in the browser tab -->
    <link rel="icon" href="favicon.ico" type="image/x-icon">
</head>
```

> **Code Explanation:**
> - `<meta name="description">` — A short summary (under 160 characters) shown by Google below your page title in search results. Think of it as a movie trailer for your webpage.
> - `<meta name="keywords">` — Comma-separated keywords related to your page. Less important for SEO today, but still used by some search engines.
> - `<meta name="author">` — Identifies who created the page.
> - `<meta property="og:title">` — An **Open Graph** tag. When someone shares your page link on WhatsApp or Facebook, this controls the **title** shown in the preview card.
> - `<meta property="og:image">` — The **image** shown in the social media preview card when your link is shared.
> - `<link rel="icon">` — The small icon (favicon) that appears next to the page title in the browser tab.

| Meta Tag | Purpose | Used By |
|---|---|---|
| `description` | Page summary for search results | Google, Bing |
| `keywords` | Related keywords | Some search engines |
| `author` | Page creator name | Browsers, search engines |
| `og:title` | Social media preview title | WhatsApp, Facebook, LinkedIn |
| `og:description` | Social media preview text | WhatsApp, Facebook, LinkedIn |
| `og:image` | Social media preview image | WhatsApp, Facebook, LinkedIn |

> **Real-World Analogy:** Think of meta tags like the information printed on the back cover of a textbook — the reader (browser/search engine) uses it to understand what's inside without opening the book.

### Browser Compatibility Note

Different web browsers (Chrome, Firefox, Edge, Safari) may display the same HTML slightly differently:

| Issue | What Happens |
|---|---|
| **Default styles** | Font sizes, margins, and padding may vary slightly between browsers |
| **Deprecated tags** | Tags like `<marquee>` work in some browsers but not others |
| **New HTML5 features** | Very old browsers may not support elements like `<canvas>` or `<video>` |
| **Rendering engines** | Chrome uses Blink, Firefox uses Gecko, Safari uses WebKit — each interprets code slightly differently |

> **Tips for Students:**
> - Always test your pages in at least **2 browsers** (Chrome + Firefox recommended)
> - Always use `<!DOCTYPE html>` to ensure **standards mode** — this minimizes differences between browsers
> - Use the [W3C HTML Validator](https://validator.w3.org/) to check if your HTML code is correct
> - Do not assume that because a page looks right in one browser, it will look the same everywhere

---

## 4. Heading Tags (`<h1>` to `<h6>`)

HTML provides six levels of headings, from most important (`<h1>`) to least important (`<h6>`).

```html
<h1>Main Title (Biggest)</h1>
<h2>Section Title</h2>
<h3>Sub-section Title</h3>
<h4>Sub-sub-section</h4>
<h5>Minor Heading</h5>
<h6>Smallest Heading</h6>
```

> **Code Explanation:**
> - `<h1>` — The largest and most important heading. Use it for the main title of the page (e.g., the name of your college).
> - `<h2>` to `<h6>` — Progressively smaller headings for sections and sub-sections.
> - Browsers automatically apply different font sizes: `<h1>` is the biggest, `<h6>` is the smallest.
> - Headings are **block-level elements** — each heading automatically starts on a new line with space above and below it.
> - Search engines (Google) use headings to understand the topic and structure of your page, so use them meaningfully.

> **Real-World Analogy:** Think of headings like a **newspaper**:
> - `<h1>` = Headline on the front page
> - `<h2>` = Section headers (Sports, Politics)
> - `<h3>` = Article titles within sections
> - `<h4>` to `<h6>` = Sub-points within articles

### Best Practices

- Use only **one `<h1>`** per page (main topic)
- Don't skip levels (don't go from `<h2>` to `<h4>`)
- Use headings for **structure**, not for making text big (use CSS for that)

---

## 5. Paragraph Tag (`<p>`)

```html
<p>This is a paragraph. HTML ignores extra spaces and line breaks
   within a paragraph. Everything flows      as one block of text.</p>

<p>This is another paragraph. Each &lt;p&gt; tag creates a new block
   with space above and below.</p>
```

> **Code Explanation:**
> - `<p>` — Defines a paragraph of text. The browser automatically adds vertical space (margin) before and after each paragraph.
> - HTML **collapses whitespace**: multiple spaces, tabs, and line breaks in your source code are displayed as a single space in the browser. This is why the extra spaces in "Everything flows      as one block" won't show up.
> - `&lt;p&gt;` — An HTML entity used to display the literal characters `<p>` on the page (since `<` and `>` are normally interpreted as tag delimiters).
> - Each `<p>...</p>` block is visually separated from the next — the browser adds default margins automatically.

### Line Break (`<br>`) and Horizontal Rule (`<hr>`)

```html
<p>Line one<br>Line two<br>Line three</p>

<hr> <!-- Draws a horizontal line across the page -->
```

> **Code Explanation:**
> - `<br>` — A self-closing tag that forces a line break (moves text to the next line). Unlike `<p>`, it does **not** add extra spacing — it simply starts a new line.
> - `<hr>` — A self-closing tag that draws a horizontal line across the page. Useful for visually separating sections.
> - Both `<br>` and `<hr>` are **empty/void elements** — they have no closing tag and no content between an opening and closing tag.
> - The `<!-- ... -->` after `<hr>` is a comment explaining the tag's purpose — a good coding habit.

---

## 6. Comments in HTML

Comments are notes for developers — the browser ignores them.

```html
<!-- This is a comment. Users won't see this. -->

<!-- 
    Multi-line comments
    are also possible
-->
```

> **Code Explanation:**
> - `<!-- ... -->` — Everything between `<!--` and `-->` is a comment. The browser completely ignores this content — it will not appear on the page.
> - Comments can be **single-line** (`<!-- one line -->`) or **multi-line** (spanning several lines).
> - **Use cases:** Leave notes for yourself or other developers, explain complex sections, or temporarily hide code during testing.
> - **Important:** Comments are still visible if someone views your page source (right-click → "View Page Source"), so **never** put passwords or sensitive information in comments.

---

## Practical Session

### 🧪 Lab Experiment 1 (Part 1): Create a Webpage Describing Your Department

**Objective:** Create a webpage using HTML that describes the BCA Department at Mandsaur University using paragraph and heading tags.

#### Step 1: Create the File

1. Open **VS Code**
2. Create a new file: `department.html`
3. Type `!` and press `Tab` to generate the HTML boilerplate (Emmet shortcut)

#### Step 2: Write the Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BCA Department - Mandsaur University</title>
</head>
<body>

    <h1>Department of Computer Applications (BCA)</h1>
    <h2>Mandsaur University, Mandsaur</h2>
    
    <hr>

    <h3>About the Department</h3>
    <p>
        The Department of Computer Applications at Mandsaur University offers 
        a comprehensive three-year Bachelor of Computer Applications (BCA) program. 
        The department is committed to producing skilled IT professionals who can 
        meet the growing demands of the technology industry.
    </p>

    <h3>Vision</h3>
    <p>
        To be a center of excellence in computer education, producing innovative 
        and industry-ready graduates who contribute to the advancement of 
        information technology.
    </p>

    <h3>Mission</h3>
    <p>
        To provide quality education in computer applications through a blend 
        of theoretical knowledge and practical skills. To foster creativity, 
        critical thinking, and ethical values among students.
    </p>

    <h3>Programs Offered</h3>
    <p>
        The department offers BCA (Bachelor of Computer Applications), a 
        three-year undergraduate program spread across six semesters. The 
        curriculum covers programming languages, web development, database 
        management, networking, and software engineering.
    </p>

    <h3>Infrastructure</h3>
    <p>
        The department has well-equipped computer labs with modern hardware 
        and software. High-speed internet connectivity is available throughout 
        the department. Smart classrooms enhance the learning experience 
        with multimedia teaching aids.
    </p>

    <h3>Contact Information</h3>
    <p>
        Department of Computer Applications<br>
        Mandsaur University<br>
        Mandsaur, Madhya Pradesh, India<br>
        Phone: +91-XXXX-XXXXXX<br>
        Email: bca@mandsauruniversity.edu.in
    </p>

</body>
</html>
```

> **Code Explanation:**
> - The page uses a complete HTML5 structure: `<!DOCTYPE html>`, charset, viewport meta, and a descriptive `<title>`.
> - `<h1>` is used for the department name and `<h2>` for the university — establishing a clear heading hierarchy (most important → less important).
> - `<hr>` draws a horizontal line separating the header from the content sections.
> - Multiple `<h3>` tags divide the page into sections (About, Vision, Mission, Programs, etc.) — this keeps the content well-organized and easy to scan.
> - `<br>` tags in the Contact section create line breaks within a single paragraph — ideal for formatting an address block where each line should be separate but not in its own paragraph.
> - The email is plain text here; in Day 8, you will learn to make it a clickable link using the `<a>` tag.

#### Step 3: View the Page

1. Right-click the file in VS Code → **"Open with Live Server"** (if Live Server extension is installed)
2. OR simply double-click the `.html` file to open in Chrome
3. Press `F12` in Chrome to open **Developer Tools** and inspect the elements

#### Step 4: Experiment

Try these modifications:
- Change the `<title>` and see it update in the browser tab
- Add another `<h3>` section about "Faculty Members"
- Try removing `<hr>` and see the difference
- Add comments (`<!-- -->`) to label different sections

---

## Practice Exercise

Create a new file `about-me.html` with:
1. Your name as `<h1>`
2. Your college and course as `<h2>`
3. A paragraph about yourself
4. A paragraph about your hobbies
5. A paragraph about your career goals
6. Use `<br>` for your contact details
7. Use `<hr>` to separate sections
8. Add at least 3 comments in the code

---

## Summary

| Concept | Key Takeaway |
|---------|-------------|
| HTML | Markup language for structuring web pages |
| `<!DOCTYPE html>` | Declares the document as HTML5 |
| `<head>` | Metadata — title, charset, links (invisible) |
| `<body>` | All visible page content |
| `<h1>` to `<h6>` | Headings from largest to smallest |
| `<p>` | Paragraphs |
| `<br>` | Line break |
| `<hr>` | Horizontal rule |
| `<!-- -->` | Comments (ignored by browser) |

---

*Day 6 of 55 | Unit 2 — HTML Fundamentals | Web Technology (25BCA060)*
