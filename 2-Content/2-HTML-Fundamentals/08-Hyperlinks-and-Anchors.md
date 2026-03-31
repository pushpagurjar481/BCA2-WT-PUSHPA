# Day 8 — Hyperlinks, Anchors & Navigation

🔬 **Type:** Theory + Practical
🕐 **Duration:** 2 Hours
📚 **Unit:** 2 — HTML Fundamentals
🧪 **Lab Experiments:** 2, 3

---

## Learning Objectives

By the end of this session, students will be able to:
- Create hyperlinks using the `<a>` tag
- Link to external websites, internal pages, and page sections
- Use image links
- Understand absolute vs relative URLs
- Use the `target` attribute

---

## 1. What is a Hyperlink?

> **Analogy:** Think of hyperlinks as **doors** in a building. Each door leads you to a different room (page). Some doors lead to rooms in the same building (internal links), while others take you to a completely different building (external links).

A **hyperlink** is a clickable element that takes the user to another page, file, or location.

### The `<a>` Tag

```html
<a href="URL">Link Text</a>
```

> **Code Explanation:**
> - `<a>` — The **anchor** tag, used to create a hyperlink. The text between `<a>` and `</a>` becomes clickable.
> - `href` — The **Hypertext REFerence** attribute — the most important attribute. It specifies the URL or destination where the link leads.
> - `Link Text` — The visible, clickable text the user sees on the page (usually displayed in blue and underlined by default).

| Attribute | Purpose |
|-----------|---------|
| `href` | The URL/destination (Hypertext REFerence) |
| `target` | Where to open the link |
| `title` | Tooltip text on hover |

---

## 2. Types of Links

### External Links (To Other Websites)

```html
<a href="https://www.google.com">Visit Google</a>
<a href="https://www.mandsauruniversity.edu.in">Mandsaur University</a>
```

> **Code Explanation:**
> - Both links use **absolute URLs** (complete web addresses starting with `https://`).
> - When clicked, the browser navigates away from the current page to the specified website.
> - By default, the link opens in the **same tab** (replacing the current page).

### Internal Links (To Other Pages on Your Site)

```html
<!-- Same folder -->
<a href="about.html">About Page</a>

<!-- Subfolder -->
<a href="pages/contact.html">Contact Page</a>

<!-- Parent folder -->
<a href="../index.html">Back to Home</a>
```

> **Code Explanation:**
> - `href="about.html"` — Links to a file in the **same folder** as the current page. No folder path needed.
> - `href="pages/contact.html"` — Links to a file inside a **subfolder** called `pages/`.
> - `href="../index.html"` — The `../` means "go **up one folder level**" first, then find `index.html`. Think of `..` as "parent folder."

### Section Links (Jump to a Part of the Same Page)

```html
<!-- Create an anchor point (target) -->
<h2 id="courses">Our Courses</h2>

<!-- Link that jumps to it -->
<a href="#courses">Jump to Courses Section</a>

<!-- Link to top of page -->
<a href="#top">Back to Top</a>  <!-- #top works automatically -->
```

> **Code Explanation:**
> - `id="courses"` — Creates a **named anchor point** (bookmark) on the `<h2>` element. The `id` value must be unique on the page.
> - `href="#courses"` — The `#` symbol tells the browser to **jump to the element with that id** on the same page. This is called a **fragment identifier**.
> - `href="#top"` — A special shortcut. Browsers automatically scroll to the very top of the page when `#top` is used, even without an element having `id="top"`.
> - Fragment identifiers also appear in the browser's address bar (e.g., `mypage.html#courses`), so users can bookmark or share a link to a specific section.

### How Fragment Identifiers (`#`) Work

When you click a link like `<a href="#courses">`, the browser:

1. Searches the current page for an element with `id="courses"`
2. Scrolls the page so that element is at the top of the viewport
3. Updates the URL in the address bar to `yourpage.html#courses`

```html
<!-- Step 1: Create target sections with unique id attributes -->
<h2 id="about">About Mandsaur University</h2>
<p>Mandsaur University was established in...</p>

<h2 id="admission">Admission Process</h2>
<p>Admissions are open for BCA, BBA, B.Tech...</p>

<h2 id="fees">Fee Structure</h2>
<p>The annual fee for BCA is...</p>

<!-- Step 2: Create a navigation menu at the top that jumps to each section -->
<p>
    <a href="#about">About</a> |
    <a href="#admission">Admission</a> |
    <a href="#fees">Fees</a>
</p>
```

> **Code Explanation:**
> - Each `<h2>` has a unique `id` attribute — these serve as **anchor targets** (bookmarks) on the page.
> - The navigation links at the top use `href="#id"` to jump directly to the corresponding section.
> - This is how **Table of Contents** navigation works on long web pages — the user clicks a link and is instantly scrolled to the relevant section.
> - You can also link to a specific section on **another page**: `<a href="about.html#fees">See Fee Structure</a>` opens `about.html` and scrolls to the `#fees` section.

### Email & Phone Links

```html
<a href="mailto:info@mandsauruniversity.edu.in">Send Email</a>
<a href="tel:+911234567890">Call Us</a>
```

> **Code Explanation:**
> - `mailto:` — A special URL scheme that opens the user's default email application (Gmail, Outlook, etc.) with the email address pre-filled.
> - `tel:` — Opens the phone dialer on mobile devices with the number pre-filled. On desktops, it may open Skype or another calling app.
> - `+91` is the country code for India. Always include it for phone links to ensure international compatibility.

---

## 3. The `target` Attribute

| Value | Behavior |
|-------|----------|
| `_self` | Opens in the same tab (default) |
| `_blank` | Opens in a new tab |
| `_parent` | Opens in parent frame |
| `_top` | Opens in full window (breaks out of frames) |

```html
<!-- Opens in same tab -->
<a href="https://www.google.com">Google (same tab)</a>

<!-- Opens in new tab -->
<a href="https://www.google.com" target="_blank">Google (new tab)</a>
```

> **Code Explanation:**
> - The first link (without `target`) opens Google in the **same tab**, replacing the current page.
> - The second link with `target="_blank"` opens Google in a **new browser tab**, keeping the original page open.
> - `_blank` is the most commonly used value. `_self` is the default behavior.
> - `_parent` and `_top` are only relevant when using frames (an older HTML feature).

> ⚠️ **Security Tip:** When using `target="_blank"`, add `rel="noopener noreferrer"` to prevent the new page from accessing your page's `window` object.

```html
<a href="https://example.com" target="_blank" rel="noopener noreferrer">Safe External Link</a>
```

> **Code Explanation:**
> - `rel="noopener"` — Prevents the new page from accessing the original page's `window.opener` property, which could be a security risk.
> - `rel="noreferrer"` — Prevents the browser from sending the referring page's URL to the new page, protecting user privacy.
> - **Best Practice:** Always add `rel="noopener noreferrer"` when using `target="_blank"` for links to external (third-party) websites.

---

## 4. Absolute vs Relative URLs

| Type | Example | Use When |
|------|---------|----------|
| **Absolute** | `https://www.google.com/images` | Linking to other websites |
| **Relative** | `images/photo.jpg` | Linking within your own site |
| **Root-relative** | `/about/team.html` | From any page on your site |

### File Structure Example

```
my-website/
├── index.html
├── about.html
├── pages/
│   ├── contact.html
│   └── team.html
└── images/
    └── logo.png
```

```html
<!-- From index.html -->
<a href="about.html">About</a>                    <!-- Same folder -->
<a href="pages/contact.html">Contact</a>           <!-- Into subfolder -->

<!-- From pages/contact.html -->
<a href="../index.html">Home</a>                   <!-- Go up one folder -->
<a href="../images/logo.png">Logo</a>              <!-- Up, then into images -->
<a href="team.html">Team</a>                       <!-- Same folder -->
```

> **Code Explanation:**
> - **From `index.html`:** `href="about.html"` works because both files are in the same folder. `href="pages/contact.html"` goes into the `pages/` subfolder.
> - **From `pages/contact.html`:** `href="../index.html"` uses `../` to go **up one level** to the parent folder where `index.html` lives. `href="../images/logo.png"` goes up one level, then into the `images/` folder.
> - **Same folder:** `href="team.html"` links to a file in the same folder — no path prefix needed.
> - **Key rule:** Always think of the path **relative to the current file's location**, not the root of the website.

---

## 5. Image as a Link

You can wrap an `<img>` tag inside an `<a>` tag to make an image clickable:

```html
<a href="https://www.mandsauruniversity.edu.in">
    <img src="university-logo.png" alt="Mandsaur University Logo" width="200">
</a>
```

> **Code Explanation:**
> - An `<img>` tag is placed **inside** an `<a>` tag — this makes the entire image clickable.
> - `href` on the `<a>` tag determines where the user goes when they click the image.
> - `alt` on the `<img>` tag is essential — if the image fails to load, the alt text appears instead. Screen readers also read this text aloud.
> - `width="200"` sets the display width of the image to 200 pixels.

---

## 6. URL Encoding (Special Characters in URLs)

URLs can only contain a specific set of characters (letters, numbers, and a few symbols). If your URL contains spaces, Hindi characters, or special symbols, they must be **encoded** (converted to a safe format):

| Character | Encoded Form | Example |
|-----------|-------------|---------|
| Space | `%20` | `my page.html` → `my%20page.html` |
| `&` | `%26` | Used to separate parameters in URLs |
| `#` | `%23` | Since `#` is used for fragment identifiers |
| `?` | `%3F` | Since `?` starts the query string |
| `=` | `%3D` | Since `=` separates key-value pairs in queries |
| `@` | `%40` | Used in email addresses |
| `+` | `%2B` | Sometimes used as a space in queries |
| `₹` | `%E2%82%B9` | Indian Rupee symbol |

```html
<!-- URL with spaces (encoded) -->
<a href="notes/web%20technology.pdf">Download Notes</a>

<!-- URL with query parameters -->
<a href="https://www.google.com/search?q=Mandsaur+University">Search on Google</a>

<!-- URL with multiple parameters separated by & -->
<a href="results.html?semester=2&subject=web%20technology">View Results</a>
```

> **Code Explanation:**
> - `web%20technology.pdf` — The space between "web" and "technology" is encoded as `%20` because URLs cannot contain literal spaces.
> - `?q=Mandsaur+University` — The `?` starts a **query string** (data sent to the server). `+` is another way to represent a space in query strings.
> - `semester=2&subject=web%20technology` — Multiple parameters are separated by `&`. Each parameter has a `key=value` format.

> **Real-World Analogy:** URL encoding is like writing an address on a postcard — you can't use certain characters (like line breaks), so you have to write the full address on one line using standard formatting. Similarly, URLs must encode special characters so browsers can understand them.

> **Tip:** You usually don't need to encode URLs manually — the browser does it automatically when you type in the address bar. But it helps to understand encoding when you see `%20` in a URL and wonder what it means.

---

## 7. Link Accessibility — Writing Good Link Text

Screen readers often navigate a page by listing all links. Imagine hearing just the link text without any surrounding context:

| ❌ Bad Link Text | ✅ Good Link Text |
|---|---|
| `<a href="...">Click here</a>` | `<a href="...">Download the BCA syllabus (PDF)</a>` |
| `<a href="...">Read more</a>` | `<a href="...">Read more about admission requirements</a>` |
| `<a href="...">Link</a>` | `<a href="...">Visit the Mandsaur University website</a>` |
| `<a href="...">Here</a>` | `<a href="...">View the fee structure for 2026</a>` |

```html
<!-- ❌ Bad: Screen reader user hears "Click here, Click here, Click here" — no idea where each link goes -->
<p>To see our courses, <a href="courses.html">click here</a>.</p>
<p>For admission details, <a href="admission.html">click here</a>.</p>

<!-- ✅ Good: Screen reader user hears clear, descriptive destinations -->
<p><a href="courses.html">View BCA and BBA course details</a></p>
<p><a href="admission.html">Read the 2026 admission requirements</a></p>
```

> **Code Explanation:**
> - In the bad example, all links say "click here" — a visually impaired user using a screen reader has no way to tell them apart.
> - In the good example, each link text clearly describes the destination — the user can choose which link to follow without reading the entire paragraph.
> - **Rule of thumb:** Link text should make sense even when read **out of context** (separate from the surrounding paragraph).

---

## 8. Visited & Unvisited Link States

By default, browsers display links in different colors based on whether you've visited them before:

| Link State | Default Color | Description |
|---|---|---|
| **Unvisited** (`link`) | 🔵 Blue (`#0000EE`) | A link you haven't clicked yet |
| **Visited** (`visited`) | 🟣 Purple (`#551A8B`) | A link you've already clicked |
| **Hover** (`hover`) | Depends on browser | When your mouse pointer is over the link |
| **Active** (`active`) | 🔴 Red | The moment you click (mouse button is down) |

> **How it works:** Your browser keeps a history of all URLs you've visited. When a page loads, the browser checks each link's `href` against your browsing history. If the URL matches, the link is displayed in the "visited" color.

> **Real-World Analogy:** Think of it like a to-do list. Unvisited links are tasks you haven't completed (marked in blue). Visited links are tasks you've already done (marked in purple). This helps users remember which pages they've already read.

> **Note:** You'll learn how to customize these colors using CSS in Unit 4 with the `:link`, `:visited`, `:hover`, and `:active` pseudo-classes.

---

## 9. The `title` Attribute on Links

The `title` attribute adds a **tooltip** — a small text box that appears when the user hovers their mouse over the link:

```html
<!-- Tooltip provides additional context about the destination -->
<a href="syllabus.pdf" title="Download the BCA Semester 2 Syllabus (PDF, 245 KB)">
    BCA Syllabus
</a>

<!-- Tooltip on an external link -->
<a href="https://www.ugc.gov.in" target="_blank" title="Opens the official UGC website in a new tab">
    University Grants Commission
</a>
```

> **Code Explanation:**
> - `title="..."` — The text inside appears as a small floating tooltip when the user hovers their mouse over the link for a second.
> - Useful for providing **extra information** such as file size, file format, or a note that the link opens in a new tab.
> - **Important:** `title` is NOT a substitute for good link text. Screen readers may or may not read the `title` attribute. The link text itself should always be descriptive.

> **When to use `title`:**
> - To indicate the file type and size (e.g., "PDF, 2.5 MB")
> - To warn that a link opens in a new tab
> - To provide a brief description of an external website

---

## Practical Session

### 🧪 Lab Experiment 2: Link Words to Wikipedia

**Objective:** Create links on specific words to link them to their Wikipedia pages.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Networking Terminology</title>
</head>
<body>

    <h1>Networking Basics</h1>
    
    <p>
        Modern computer networks use various technologies to connect devices. 
        <a href="https://en.wikipedia.org/wiki/Wi-Fi" target="_blank" rel="noopener noreferrer">Wi-Fi</a> 
        is a wireless networking technology that allows devices to connect to the 
        internet without physical cables. It uses radio waves and is commonly found 
        in homes, offices, and public places.
    </p>
    
    <p>
        On the other hand, a 
        <a href="https://en.wikipedia.org/wiki/Local_area_network" target="_blank" rel="noopener noreferrer">LAN</a> 
        (Local Area Network) connects computers within a limited area such as a 
        school, office, or building. LANs typically use 
        <a href="https://en.wikipedia.org/wiki/Ethernet" target="_blank" rel="noopener noreferrer">Ethernet</a> 
        cables for wired connections.
    </p>
    
    <p>
        The 
        <a href="https://en.wikipedia.org/wiki/Internet" target="_blank" rel="noopener noreferrer">Internet</a> 
        is a vast 
        <a href="https://en.wikipedia.org/wiki/Wide_area_network" target="_blank" rel="noopener noreferrer">WAN</a> 
        (Wide Area Network) that connects millions of LANs worldwide using the 
        <a href="https://en.wikipedia.org/wiki/Internet_protocol_suite" target="_blank" rel="noopener noreferrer">TCP/IP</a> 
        protocol suite.
    </p>

</body>
</html>
```

> **Code Explanation:**
> - The page contains three paragraphs, each describing a networking concept.
> - Key technical terms (Wi-Fi, LAN, Ethernet, Internet, WAN, TCP/IP) are wrapped in `<a>` tags linking to their Wikipedia articles.
> - `target="_blank"` opens each Wikipedia link in a new tab so the student doesn't lose the current page.
> - `rel="noopener noreferrer"` is added for security on every external link.
> - This demonstrates how hyperlinks can turn ordinary text into an **interactive learning resource** — students can click any term to learn more.

---

### 🧪 Lab Experiment 3: Image Link

**Objective:** Insert an image and make it a clickable link to another page.

**File 1: `index.html`**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Image Link Demo</title>
</head>
<body>

    <h1>Welcome to Mandsaur University</h1>
    
    <p>Click the image below to learn more about our campus:</p>
    
    <!-- Image as a link -->
    <a href="campus.html" title="Click to see campus details">
        <img src="https://via.placeholder.com/400x250?text=University+Campus" 
             alt="Mandsaur University Campus" 
             width="400" height="250">
    </a>
    
    <p>
        <a href="campus.html">View Campus Details &rarr;</a>
    </p>

</body>
</html>
```

> **Code Explanation:**
> - `title="Click to see campus details"` on the `<a>` tag shows a tooltip when the user hovers over the image.
> - The `<img>` inside `<a>` makes the entire image a clickable link to `campus.html`.
> - `alt="Mandsaur University Campus"` provides alternative text for screen readers and for cases where the image fails to load.
> - `width="400" height="250"` sets the display dimensions of the image.
> - `&rarr;` is an HTML entity for the right arrow (→), used to visually indicate that the text link leads to another page.

**File 2: `campus.html`**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Campus Details</title>
</head>
<body>

    <h1>Campus Details</h1>
    <p>Mandsaur University has a sprawling campus with modern facilities...</p>
    <p><a href="index.html">&larr; Back to Home</a></p>

</body>
</html>
```

> **Code Explanation:**
> - This is the **destination page** that opens when the user clicks the campus image on `index.html`.
> - `<a href="index.html">` links back to the home page, allowing **two-way navigation** between pages.
> - `&larr;` is the HTML entity for a left arrow (←), visually suggesting "go back."
> - **Two-page linking** is a fundamental web pattern: Page A links to Page B, and Page B links back to Page A.

---

## Practice Exercise

Create a 3-page mini-website:
1. **`index.html`** — Home page with links to other two pages
2. **`courses.html`** — List of BCA courses with links back to home
3. **`faculty.html`** — Faculty information with links back to home

Each page should:
- Have navigation links to all three pages at the top
- Include at least one external link (to a relevant website)
- Use section links (`#section-id`) within the page
- Include a "Back to Top" link at the bottom

---

## Summary

| Concept | Syntax | Example |
|---------|--------|---------|
| External link | `<a href="https://...">` | Link to Google |
| Internal link | `<a href="page.html">` | Link to another page |
| Section link | `<a href="#id">` | Jump within page |
| New tab | `target="_blank"` | Opens in new tab |
| Image link | `<a href="..."><img ...></a>` | Clickable image |
| Email link | `<a href="mailto:...">` | Opens email client |

---

*Day 8 of 55 | Unit 2 — HTML Fundamentals | Web Technology (25BCA060)*
