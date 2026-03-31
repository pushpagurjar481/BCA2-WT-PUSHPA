# Day 9 — Images, Colors & Backgrounds

🔬 **Type:** Theory + Practical
🕐 **Duration:** 2 Hours
📚 **Unit:** 2 — HTML Fundamentals
🧪 **Lab Experiments:** 3 (continued), 4

---

## Learning Objectives

By the end of this session, students will be able to:
- Insert and configure images using the `<img>` tag
- Control image size with `width` and `height` attributes
- Apply background colors to pages and elements
- Change text and font colors using HTML attributes
- Create anchor links to the top of the page

---

## 1. Images in HTML (`<img>` Tag)

```html
<img src="path/to/image.jpg" alt="Description of image" width="300" height="200">
```

> **Code Explanation:**
> - `<img>` — A **self-closing tag** (no `</img>` needed) that embeds an image on the page.
> - `src="path/to/image.jpg"` — The **source** attribute specifies where the image file is located (a file path or a full URL).
> - `alt="Description of image"` — **Alternative text** displayed if the image cannot load, and read aloud by screen readers for visually impaired users.
> - `width="300" height="200"` — Sets the display dimensions in pixels. You can also use percentages like `width="50%"`.

| Attribute | Required | Purpose |
|-----------|----------|---------|
| `src` | ✅ | Path/URL of the image |
| `alt` | ✅ | Alternative text (shown if image fails to load; used by screen readers) |
| `width` | Optional | Width in pixels or percentage |
| `height` | Optional | Height in pixels or percentage |
| `title` | Optional | Tooltip text on hover |

### Why `alt` Text is Important

The `alt` attribute is one of the most important attributes in HTML. It serves multiple purposes:

| Purpose | How `alt` Helps |
|---|---|
| **Accessibility** | Screen readers (JAWS, NVDA) read the `alt` text aloud to visually impaired users, telling them what the image shows |
| **Broken images** | If the image fails to load (wrong path, slow internet), the `alt` text is displayed instead |
| **SEO** | Google cannot "see" images — it reads the `alt` text to understand and index your images in search results |
| **Low bandwidth** | Users on slow connections may disable images; `alt` text tells them what they're missing |

**Writing Good `alt` Text:**

```html
<!-- ❌ Bad alt text -->
<img src="campus.jpg" alt="image">          <!-- Too vague -->
<img src="campus.jpg" alt="">               <!-- Empty — screen reader skips entirely -->
<img src="campus.jpg" alt="campus.jpg">     <!-- File name is not helpful -->

<!-- ✅ Good alt text -->
<img src="campus.jpg" alt="Mandsaur University campus with the main building and garden">
<img src="logo.png" alt="Mandsaur University logo">
<img src="chart.png" alt="Bar chart showing BCA placement statistics from 2020 to 2025">
```

> **Code Explanation:**
> - Bad `alt` values like "image" or the file name don't help a blind user understand what the image shows.
> - Good `alt` text is **descriptive** — it paints a picture in words so someone who can't see the image understands its content.
> - For **decorative images** (like borders or spacers) that add no information, use `alt=""` (empty alt) so screen readers skip them entirely.
> - **Rule of thumb:** Describe what the image *shows*, not what it *is*. Say "Students working in the computer lab" instead of "Photo of lab."

### Image Sources

```html
<!-- Local image (relative path) -->
<img src="images/photo.jpg" alt="My Photo">

<!-- Local image (from parent folder) -->
<img src="../images/logo.png" alt="Logo">

<!-- External image (URL) -->
<img src="https://via.placeholder.com/300x200" alt="Placeholder">
```

> **Code Explanation:**
> - **Relative path** (`images/photo.jpg`) — The image file is inside an `images/` folder in the same directory as your HTML file. Best for your own project images.
> - **Parent folder path** (`../images/logo.png`) — `../` means "go up one folder level." Used when the image is in a sibling directory.
> - **External URL** (`https://via.placeholder.com/...`) — Loads the image from another website over the internet. Useful for testing, but your page depends on that external server being available.

### Common Image Formats

| Format | Extension | Best For |
|--------|-----------|----------|
| **JPEG** | `.jpg`, `.jpeg` | Photographs (lossy compression) |
| **PNG** | `.png` | Graphics with transparency |
| **GIF** | `.gif` | Animated images, simple graphics |
| **SVG** | `.svg` | Scalable vector graphics (logos, icons) |
| **WebP** | `.webp` | Modern format (smaller file sizes) |

### Image Size Tips

```html
<!-- Fixed size in pixels -->
<img src="photo.jpg" alt="Photo" width="400" height="300">

<!-- Percentage (responsive) -->
<img src="photo.jpg" alt="Photo" width="100%">

<!-- Only set one dimension, the other auto-adjusts proportionally -->
<img src="photo.jpg" alt="Photo" width="400">
```

> **Code Explanation:**
> - `width="400" height="300"` — Sets the image to exactly 400×300 pixels, regardless of the original image size.
> - `width="100%"` — The image stretches to fill the entire width of its parent container. On a phone, it fills the phone screen; on a desktop, it fills the content area. This makes images **responsive**.
> - Setting **only one dimension** (e.g., just `width="400"`) is the **recommended approach** — the browser calculates the other dimension automatically, preserving the original **aspect ratio** (preventing stretching or squishing).

### Responsive Images — Why Aspect Ratio Matters

When you set both `width` and `height` to arbitrary values, the image may get **distorted** (stretched or squished):

```html
<!-- ❌ Distorted: original image is 800x600, but we're forcing 400x400 -->
<img src="campus.jpg" alt="Campus" width="400" height="400">

<!-- ✅ Correct: set only width, height auto-calculates proportionally -->
<img src="campus.jpg" alt="Campus" width="400">

<!-- ✅ Responsive: image fills its container width, scales on all devices -->
<img src="campus.jpg" alt="Campus" width="100%">
```

> **Code Explanation:**
> - The first example forces a square shape (400×400) on an image that is naturally rectangular (800×600) — this **distorts** the image.
> - The second example sets only the width. The browser calculates the height automatically based on the image's natural proportions.
> - The third example makes the image **responsive** — it always fills the available space, whether viewed on a phone, tablet, or desktop.

> **Real-World Analogy:** Imagine resizing a printed photo. If you push both sides inward by different amounts, the photo looks stretched. But if you scale it evenly (like a photocopy machine at 50%), everything stays in proportion. Setting only `width` is like using the photocopy machine — the browser keeps the proportions correct.

### Image Optimization — Choosing the Right Format

When building real websites, image file size directly affects how fast your page loads. Here is a detailed guide:

| Format | Best For | Transparency? | Animation? | Typical Size | Quality |
|--------|---------|---------------|------------|-------------|---------|
| **JPEG** (.jpg) | Photographs, complex images | ❌ No | ❌ No | Small–Medium | Lossy (some quality lost) |
| **PNG** (.png) | Logos, graphics, screenshots | ✅ Yes | ❌ No | Medium–Large | Lossless (no quality lost) |
| **GIF** (.gif) | Simple animations, icons | ✅ Yes (1-bit) | ✅ Yes | Small | Limited to 256 colours |
| **SVG** (.svg) | Logos, icons, diagrams | ✅ Yes | ✅ (with CSS) | Very Small | Infinite (vector-based, scales perfectly) |
| **WebP** (.webp) | Everything (modern format) | ✅ Yes | ✅ Yes | Very Small | Both lossy and lossless options |

**When to Use Which Format:**

| Scenario | Best Format | Why |
|---|---|---|
| A photo of Mandsaur University campus | JPEG | Photos have millions of colours; JPEG compresses them well |
| The university logo on the website | SVG or PNG | Logos need crisp edges; SVG scales to any size without blurring |
| An animated banner on the homepage | GIF or WebP | GIF supports simple animation; WebP is smaller and better quality |
| A screenshot of a form for documentation | PNG | Screenshots have sharp text and solid colours; PNG preserves them perfectly |
| Any image on a modern website | WebP | Smallest file size with the best quality, supported by all modern browsers |

> **Tip for Students:** A single high-resolution photograph can be 5 MB as a PNG but only 200 KB as a JPEG. That's a **25x difference** in file size! Always choose the right format to keep your website fast.

### SVG Example (Scalable Vector Graphics)

SVG images are written in code (XML format) and can be embedded directly in HTML. They scale to any size without losing quality:

```html
<!-- SVG embedded directly in HTML — draws a simple circle -->
<svg width="200" height="200">
    <!-- A green circle with a dark green border -->
    <circle cx="100" cy="100" r="80" fill="#4CAF50" stroke="#2E7D32" stroke-width="4" />
    <!-- Text centered inside the circle -->
    <text x="100" y="108" text-anchor="middle" fill="white" font-size="20">MU</text>
</svg>

<!-- SVG as an external file (like any other image) -->
<img src="university-logo.svg" alt="Mandsaur University Logo" width="150">
```

> **Code Explanation:**
> - `<svg width="200" height="200">` — Creates a 200×200 pixel canvas for drawing vector graphics.
> - `<circle cx="100" cy="100" r="80">` — Draws a circle. `cx` and `cy` set the center point; `r` is the radius. `fill` sets the inside colour; `stroke` sets the border colour.
> - `<text x="100" y="108">MU</text>` — Draws text at position (100, 108). `text-anchor="middle"` centers the text horizontally.
> - SVGs can also be used as external files with the `<img>` tag — just like JPEG or PNG.
> - **Key advantage:** SVG images look perfectly sharp at **any zoom level** — whether printed on a visiting card or displayed on a billboard.

---

## 2. Colors in HTML

### Color Representation

| Method | Syntax | Example |
|--------|--------|---------|
| **Color Name** | `color="red"` | 147 named colors |
| **Hex Code** | `color="#FF0000"` | # + 6 hex digits (RRGGBB) |
| **RGB** | Used in CSS | `rgb(255, 0, 0)` |

### Common Color Names & Hex Codes

| Color | Name | Hex Code |
|-------|------|----------|
| 🔴 | `red` | `#FF0000` |
| 🟢 | `green` | `#008000` |
| 🔵 | `blue` | `#0000FF` |
| ⚫ | `black` | `#000000` |
| ⚪ | `white` | `#FFFFFF` |
| 🟡 | `yellow` | `#FFFF00` |
| 🟠 | `orange` | `#FFA500` |
| 🟣 | `purple` | `#800080` |

### How Hex Colors Work

```
#FF5733
 └┤└┤└┤
  R  G  B

R = FF (255) → Maximum Red
G = 57 (87)  → Some Green
B = 33 (51)  → Little Blue

Result: An orange-red color
```

### Hex Color Shorthand

When both digits of each colour pair (RR, GG, BB) are the same, you can use a **3-digit shorthand**:

| Shorthand | Full Form | Color |
|-----------|-----------|-------|
| `#FFF` | `#FFFFFF` | White |
| `#000` | `#000000` | Black |
| `#F00` | `#FF0000` | Red |
| `#0F0` | `#00FF00` | Lime Green |
| `#00F` | `#0000FF` | Blue |
| `#FF0` | `#FFFF00` | Yellow |
| `#F80` | `#FF8800` | Orange |

> **Rule:** `#RGB` expands to `#RRGGBB` — each digit is **doubled**. So `#F80` becomes `#FF8800`.
>
> You **cannot** shorten `#FF5733` to `#F53` because `FF` → `F` (ok), `57` → not the same digits (cannot shorten), `33` → `3` (ok). All three pairs must have matching digits for shorthand to work.

---

## 3. Background Colors & Text Colors

### Page Background Color

```html
<body bgcolor="#F0F0F0">
    <!-- Light gray background for the entire page -->
</body>
```

> **Code Explanation:**
> - `bgcolor="#F0F0F0"` — Sets the background colour of the entire page to a light gray.
> - `bgcolor` is an attribute of the `<body>` tag. It accepts colour names (`bgcolor="lightblue"`) or hex codes (`bgcolor="#F0F0F0"`).
> - The `<!-- ... -->` comment explains the colour choice to other developers reading the code.

### Text Colors with `<font>` Tag (Deprecated but in syllabus)

```html
<font color="red" size="5" face="Arial">Red text in Arial</font>
<font color="#0000FF" size="3">Blue text</font>
```

> **Code Explanation:**
> - `color="red"` — Sets the text colour using a colour name. `color="#0000FF"` uses a hex code for blue.
> - `size="5"` — Sets the font size on a scale of 1 (smallest) to 7 (largest). `3` is the default browser font size.
> - `face="Arial"` — Sets the font family to Arial. If Arial is not installed on the user's computer, the browser falls back to its default font.

| Attribute | Purpose | Values |
|-----------|---------|--------|
| `color` | Text color | Name or hex code |
| `size` | Font size | 1 (smallest) to 7 (largest) |
| `face` | Font family | `Arial`, `Times New Roman`, etc. |

> ⚠️ The `<font>` tag and `bgcolor` attribute are **deprecated in HTML5**. Use CSS instead (Unit 4). We learn them here to understand the concept.

### Color Accessibility — Contrast Matters

When choosing text and background colours, you must ensure there is enough **contrast** so that everyone — including people with colour blindness or low vision — can read the text:

| ❌ Bad Contrast | ✅ Good Contrast |
|---|---|
| Light gray text on white background | Dark gray text on white background |
| Yellow text on white background | Black text on yellow background |
| Red text on green background | White text on dark green background |
| Light blue text on white background | Dark blue text on white background |

**WCAG (Web Content Accessibility Guidelines) Contrast Ratios:**

| Level | Minimum Ratio | Meaning |
|---|---|---|
| **AA (Minimum)** | 4.5:1 | Normal text must have at least 4.5× contrast difference |
| **AA (Large text)** | 3:1 | Text 18px+ bold or 24px+ regular |
| **AAA (Enhanced)** | 7:1 | Maximum readability for all users |

> **Real-World Analogy:** Think of contrast like reading a signboard. A dark blue sign with white text (high contrast) is easy to read from a distance. But a light yellow sign with white text (low contrast) is almost invisible. Websites work the same way — good contrast = easy to read.

> **Free Tools to Check Contrast:**
> - [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/) — Enter foreground and background hex codes to check the contrast ratio
> - [Colour Contrast Analyser](https://www.tpgi.com/color-contrast-checker/) — Desktop tool that checks contrast
> - **Chrome DevTools** — Right-click an element → Inspect → the Styles panel shows contrast ratios

> **Tip:** In India, government websites ([india.gov.in](https://www.india.gov.in)) are required to follow WCAG guidelines. This is a good practice for all websites.

---

## Practical Session

### 🧪 Lab Experiment 4: Background Color & Back-to-Top Link

**Objective:** Change the background color of the page and create a link at the bottom that takes the user to the top of the page.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Colors and Navigation Demo</title>
</head>
<body bgcolor="#E8F5E9" id="top">

    <h1 align="center">
        <font color="#1B5E20">Mandsaur University</font>
    </h1>
    <h2 align="center">
        <font color="#388E3C">Department of Computer Applications</font>
    </h2>
    
    <hr>

    <h3><font color="#2E7D32">Section 1: About Us</font></h3>
    <p>
        Mandsaur University is a prestigious institution located in 
        <font color="blue"><b>Mandsaur, Madhya Pradesh</b></font>. 
        The university offers a wide range of programs across multiple disciplines.
    </p>
    
    <!-- Image inserted -->
    <p align="center">
        <img src="https://via.placeholder.com/500x300?text=Campus+View" 
             alt="University Campus" width="500">
    </p>

    <h3><font color="#2E7D32">Section 2: Our Programs</font></h3>
    <p>
        We offer <font color="red"><b>BCA</b></font>, 
        <font color="red"><b>BBA</b></font>, 
        <font color="red"><b>B.Tech</b></font>, and many more programs. 
        Each program is designed to provide students with practical skills 
        and theoretical knowledge.
    </p>

    <h3><font color="#2E7D32">Section 3: Facilities</font></h3>
    <p>Our state-of-the-art facilities include:</p>
    <p>
        &bull; Modern Computer Labs<br>
        &bull; High-speed Wi-Fi Campus<br>
        &bull; Digital Library<br>
        &bull; Smart Classrooms<br>
        &bull; Sports Complex<br>
        &bull; Hostel Accommodation
    </p>

    <h3><font color="#2E7D32">Section 4: Achievements</font></h3>
    <p>
        Our students have consistently performed well in national-level 
        competitions and have been placed in top IT companies. The university 
        has been recognized for its contribution to quality education.
    </p>

    <h3><font color="#2E7D32">Section 5: Contact</font></h3>
    <p>
        <font color="#333333">
        Mandsaur University<br>
        Rewas Dewda Road, Mandsaur<br>
        Madhya Pradesh - 458001<br>
        Phone: +91-XXXX-XXXXXX<br>
        Email: info@mandsauruniversity.edu.in
        </font>
    </p>

    <hr>
    
    <!-- Back to Top link -->
    <p align="center">
        <a href="#top"><b>&uarr; Back to Top</b></a>
    </p>

</body>
</html>
```

> **Code Explanation:**
> - `<body bgcolor="#E8F5E9" id="top">` — Sets a light green background colour for the entire page. `id="top"` creates an anchor point so the "Back to Top" link at the bottom can scroll here.
> - `<font color="#1B5E20">` — Uses a dark green hex colour for the university name heading.
> - `<font color="blue"><b>Mandsaur, Madhya Pradesh</b></font>` — Combines the `<font>` tag for colour with `<b>` for bold text.
> - `<img src="..." width="500">` — Inserts a campus image with only the width set (height auto-adjusts to maintain aspect ratio).
> - `<font color="red"><b>BCA</b></font>` — Programme names are displayed in bold red to make them stand out.
> - `&bull;` — HTML entity for a bullet point (•), used to create a simple list without `<ul>` or `<ol>` tags.
> - `<a href="#top">` — Links to the element with `id="top"` (the `<body>` tag at the very top), creating a "Back to Top" navigation link.
> - `&uarr;` — HTML entity for the up arrow (↑), visually indicating upward navigation.

### 🧪 Lab Experiment 3 (Continued): Image Link Practice

Create a page with 3 images, each linking to a different page:

```html
<h2>Our Departments</h2>

<a href="bca.html">
    <img src="https://via.placeholder.com/200x150?text=BCA" 
         alt="BCA Department" width="200">
</a>

<a href="bba.html">
    <img src="https://via.placeholder.com/200x150?text=BBA" 
         alt="BBA Department" width="200">
</a>

<a href="btech.html">
    <img src="https://via.placeholder.com/200x150?text=B.Tech" 
         alt="B.Tech Department" width="200">
</a>
```

> **Code Explanation:**
> - Each `<a>` tag wraps an `<img>` tag, making the entire image a clickable link.
> - `href="bca.html"`, `href="bba.html"`, `href="btech.html"` — Each image links to a different department page.
> - The placeholder images (`https://via.placeholder.com/200x150?text=BCA`) are temporary images used for development — in a real project, you would replace them with actual photos.
> - `alt="BCA Department"` — Provides meaningful alt text for each image, so screen readers can identify them.
> - `width="200"` — All three images have the same width for a consistent, uniform layout.

---

## Practice Exercise

Create `gallery.html` with:
1. Page background color set to a light shade
2. A title with a different font color
3. At least 5 images (use placeholder images)
4. Each image should have proper `alt` text
5. At least 2 images should be clickable links
6. Multiple sections with different colored headings
7. A "Back to Top" link at the bottom

---

## Summary

| Concept | Key Syntax |
|---------|-----------|
| Image | `<img src="path" alt="desc" width="N">` |
| Background color | `<body bgcolor="#color">` |
| Text color | `<font color="red">text</font>` |
| Hex colors | `#RRGGBB` (e.g., `#FF5733`) |
| Back to top | `<a href="#top">Back to Top</a>` with `id="top"` on body |
| Image formats | JPEG (photos), PNG (transparency), GIF (animation), SVG (vectors) |

---

*Day 9 of 55 | Unit 2 — HTML Fundamentals | Web Technology (25BCA060)*
