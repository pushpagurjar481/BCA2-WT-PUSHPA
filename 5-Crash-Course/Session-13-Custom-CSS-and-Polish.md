# Session 13: "Dress to Impress" — Custom CSS + Visual Polish

**BCA Semester II | Mandsaur University | Web Technology (25BCA060)**

> **Session 13 of 15** | ⏱️ Duration: 2 hours  
> **Labs Covered:** Lab 10 (Inline CSS styling), Lab 11 (External CSS file)  
> **JavaScript Style:** No new JavaScript today — this is a **pure CSS session!**

---

## 🎯 What We'll Build Today

Over the last 12 sessions, we've built a feature-complete website — navbar, hero carousel, about section, faculty cards, timetable, gallery, contact form, login system, countdown timer, dark mode, back-to-top button, FAQ accordion, and a clean footer. Everything works. But right now, it looks… well, it looks like **every other Bootstrap website** on the internet.

Today we fix that. Think of it this way: **you've built the house, now it's time to paint, decorate, and furnish it.** We'll give our class website a unique personality — custom colors, beautiful fonts, smooth animations, hover effects, and a polished look that screams *"BCA Batch 2025-26 made this!"*

**By the end of this session, you'll have:**

- ✅ An external stylesheet `css/custom.css` linked correctly (overriding Bootstrap)
- ✅ A custom color scheme using CSS variables (change one value, entire site updates!)
- ✅ Google Fonts for beautiful headings and body text
- ✅ Hover effects on cards, buttons, nav links, and gallery images
- ✅ Smooth transitions and scroll behavior
- ✅ Enhanced dark mode with proper variable overrides
- ✅ Responsive adjustments for smaller screens
- ✅ A website that looks uniquely *yours* — not generic Bootstrap

**Before → After:**

```
 BEFORE (Generic Bootstrap)              AFTER (Custom Themed)
┌──────────────────────────┐    ┌──────────────────────────┐
│  BCA 2025-26   [links]   │    │  BCA 2025-26   [links]   │  ← Underline animation
│                          │    │    ~~~~~~~~~~~~           │    on hover!
│  ┌────────────────────┐  │    │  ┌────────────────────┐  │
│  │   Bootstrap Blue   │  │    │  │  Custom Deep Blue   │  │  ← Your brand colors
│  │   Default Fonts    │  │    │  │  Poppins + Open Sans│  │  ← Google Fonts
│  └────────────────────┘  │    │  └────────────────────┘  │
│                          │    │                          │
│  ┌──────┐ ┌──────┐      │    │  ┌──────┐ ┌──────┐      │
│  │ Card │ │ Card │      │    │  │ Card ↑│ │ Card │      │  ← Cards lift on hover
│  │      │ │      │      │    │  │shadow!│ │      │      │
│  └──────┘ └──────┘      │    │  └──────┘ └──────┘      │
│                          │    │                          │
│  [Button]                │    │  [✨Button✨]             │  ← Glow on hover
└──────────────────────────┘    └──────────────────────────┘
```

---

## 📌 New CSS Concepts Table

No new HTML tags today! Instead, here are the **CSS concepts** you'll learn:

| Concept | What It Does | Analogy |
|---------|-------------|---------|
| `<link rel="stylesheet">` | Connects an external CSS file to the HTML page | 📌 Like attaching a *dress code sheet* to a party invitation |
| CSS Specificity | Rules for which style wins when there are conflicts | 🤼 A wrestling match — the more specific selector wins |
| `:root` selector | Targets the very top-level element (the whole document) | 🏠 The main switch board of the house — controls everything |
| `--custom-property` | CSS variable — a reusable named value | 🎨 A paint palette board — change one swatch, all paintings update |
| `var(--name)` | Uses a CSS variable's value | "Use whatever color is on the palette board" |
| `transition` | Smoothly animates changes between two states | 🚪 A door that swings open slowly instead of teleporting open |
| `transform: translateY()` | Moves an element up/down without affecting layout | 🎈 Lifting a card off the table — the table doesn't move |
| `transform: scale()` | Makes an element bigger/smaller | 🔍 A magnifying glass effect |
| `::after` pseudo-element | Creates a virtual element after an element's content | Adding an invisible underline decoration that appears on hover |
| `@media` (responsive) | Applies CSS only when screen matches certain conditions | "If classroom has < 30 students, use smaller desks" |
| `@media print` | Applies CSS only when the page is being printed | "When xeroxing notes, skip the colorful background" |
| `filter: brightness()` | Adjusts how bright/dark an element appears | Like turning the brightness knob on a TV |
| `scroll-behavior: smooth` | Makes page scroll smoothly instead of jumping | 🛗 Elevator vs. teleportation — both reach the same floor |
| `box-shadow` | Adds shadow around an element | 📦 The shadow under a book lying on a desk |

---

## 📖 External CSS — The Right Way to Style

### Three Ways to Add CSS (Lab 10 vs. Lab 11)

You've already seen CSS in three forms:

| Method | Syntax | When to Use | Analogy |
|--------|--------|-------------|---------|
| **Inline CSS** (Lab 10) | `<p style="color: red;">` | Quick testing only | Scribbling notes on your hand — works, but messy |
| **Internal CSS** | `<style>` in `<head>` | Single-page sites | Writing notes in your notebook — organized, but only in one book |
| **External CSS** (Lab 11) | `<link href="style.css">` | Real projects ✅ | A printed dress code — one sheet, every student follows it |

📌 **From now on, we ONLY use external CSS.** Inline and internal styles don't scale. Imagine 50 pages all needing the same button color — would you write `style="color: red;"` 200 times? No! One external file, one change, every page updates.

### Creating the File

In your project folder, create this structure:

```
📂 BCA-Website/
├── 📄 index.html
├── 📂 js/
│   └── 📄 script.js         ← Created in Session 12
├── 📂 css/
│   └── 📄 custom.css        ← Creating TODAY!
└── 📂 images/
    └── (your images)
```

### Linking It — Order Matters!

📌 **Critical Rule:** Your custom CSS file **MUST** be linked **AFTER** the Bootstrap CSS link.

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BCA Batch 2025-26</title>

    <!-- Bootstrap CSS (FIRST — the base coat of paint) -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css"
          rel="stylesheet">

    <!-- Google Fonts (SECOND — load the fonts) -->
    <link href="https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;600&family=Poppins:wght@600;700&display=swap"
          rel="stylesheet">

    <!-- Our Custom CSS (LAST — our paint goes ON TOP of Bootstrap) -->
    <link rel="stylesheet" href="css/custom.css">
</head>
```

**Why after?** Think of it like painting a wall:
1. 🏗️ **Bootstrap** paints the wall white (default styles)
2. 🎨 **Your custom.css** paints over it with your chosen colors

If you reverse the order, Bootstrap's white paint covers your colors. **Last loaded = last applied = wins!**

---

## 📖 CSS Specificity — How to Override Bootstrap

### The Wrestling Match Analogy

When two CSS rules conflict, the browser needs to decide which one wins. This is called **specificity** — and it works like a wrestling tournament. The heavier (more specific) selector wins.

📌 **Specificity Weight System:**

| Selector Type | Weight | Example | Analogy |
|--------------|--------|---------|---------|
| `!important` | ♾️ (infinity) | `color: red !important;` | The principal's order — overrides everyone |
| Inline style | 1000 | `style="color: red;"` | The HOD's decision |
| `#id` selector | 100 | `#hero { color: red; }` | A professor's instruction |
| `.class` selector | 10 | `.btn { color: red; }` | A class representative's suggestion |
| `element` selector | 1 | `p { color: red; }` | A student's opinion |

### How Specificity Math Works

```
p                    →  0, 0, 0, 1  (just an element)
.btn                 →  0, 0, 1, 0  (one class)
.btn-primary         →  0, 0, 1, 0  (one class)
#hero .btn           →  0, 1, 1, 0  (one id + one class = 110 > 10)
section .btn-primary →  0, 0, 1, 1  (one class + one element = 11 > 10)
```

### Overriding Bootstrap — Three Strategies

**Strategy 1: Same Specificity, Loaded Later (Best ✅)**

Bootstrap says: `.btn-primary { background-color: #0d6efd; }`
Your CSS says:  `.btn-primary { background-color: #2c3e50; }`

Both have specificity 10. But your file loads AFTER Bootstrap — **last one wins!**

**Strategy 2: Increase Specificity (When needed)**

If Strategy 1 doesn't work for some Bootstrap rule, add more context:

```css
/* Bootstrap's rule */
.navbar-brand { font-size: 1.25rem; }

/* Your override — more specific because you added "nav" context */
nav .navbar-brand { font-size: 1.5rem; }
```

**Strategy 3: `!important` (Last resort ⚠️)**

```css
.some-stubborn-class {
    color: #2c3e50 !important;
}
```

> ⚠️ **Warning:** Using `!important` is like the principal yelling over everyone. It works, but if you overuse it, nobody can override anything anymore. It becomes chaos. Use it only when Strategy 1 and 2 fail.

---

## 📖 CSS Custom Properties (Variables)

### The Color Palette Board

📌 **CSS Variables** (officially called *Custom Properties*) let you define a value once and reuse it everywhere. Think of them as a **color palette board** hanging in an art classroom:

- The board has labels: "Primary Color = Deep Blue", "Accent Color = Red"
- Every student painting a project looks at the board and uses those colors
- The teacher changes "Primary Color" on the board to Green → **every painting updates automatically**

### Defining Variables

Variables are defined in `:root` — the very top level of the document (same as `<html>`):

```css
:root {
    /* === Color Scheme === */
    --primary-color: #2c3e50;       /* Deep blue — our brand */
    --secondary-color: #e74c3c;     /* Vibrant red — for accents */
    --accent-color: #3498db;        /* Bright blue — links, highlights */
    --bg-light: #f8f9fa;            /* Light background */
    --bg-dark: #1a1a2e;             /* Dark mode background */
    --text-dark: #2c3e50;           /* Main text color */
    --text-light: #ecf0f1;          /* Text on dark backgrounds */

    /* === Typography === */
    --font-heading: 'Poppins', sans-serif;
    --font-body: 'Open Sans', sans-serif;

    /* === Effects === */
    --transition-speed: 0.3s;
    --shadow-sm: 0 2px 8px rgba(0, 0, 0, 0.1);
    --shadow-md: 0 4px 16px rgba(0, 0, 0, 0.15);
    --shadow-lg: 0 8px 32px rgba(0, 0, 0, 0.2);
    --border-radius: 8px;
}
```

### Using Variables

```css
body {
    font-family: var(--font-body);
    color: var(--text-dark);
}

h1, h2, h3, h4, h5, h6 {
    font-family: var(--font-heading);
    color: var(--primary-color);
}

.btn-primary {
    background-color: var(--primary-color);
    border-color: var(--primary-color);
}
```

📌 **Why is this powerful?** Want to change your entire website from a blue theme to a green theme? Change **one line** — `--primary-color: #27ae60;` — and every heading, button, border, and highlight that uses `var(--primary-color)` updates instantly. No "Find and Replace" across 500 lines of CSS!

---

## 📖 Google Fonts — Beautiful Typography

### Why Default Fonts Look Boring

Every computer has its own fonts. A website using `font-family: sans-serif;` will look different on a Windows PC, a MacBook, and an Android phone. **Google Fonts** gives you free, consistent fonts that look the same everywhere.

### Choosing a Font Pair

A good website uses **two fonts** — one for headings (bold, attention-grabbing) and one for body text (clean, easy to read):

| Role | Our Choice | Why |
|------|-----------|-----|
| Headings | **Poppins** (600, 700 weight) | Modern, geometric, great for titles |
| Body text | **Open Sans** (400, 600 weight) | Clean, highly readable, works at any size |

> 💡 **Tip:** Visit [fonts.google.com](https://fonts.google.com) and search for "Poppins". You can preview it with your own text — type "BCA Batch 2025-26" to see how it looks!

### Adding Google Fonts

The `<link>` tag goes in `<head>`, BEFORE your custom CSS but AFTER Bootstrap:

```html
<link href="https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;600&family=Poppins:wght@600;700&display=swap"
      rel="stylesheet">
```

Breaking it down:
- `family=Open+Sans:wght@400;600` → Load Open Sans in regular (400) and semi-bold (600)
- `family=Poppins:wght@600;700` → Load Poppins in semi-bold (600) and bold (700)
- `display=swap` → Show fallback font first, swap to Google Font when it loads (no blank text!)

### Applying Fonts in CSS

```css
body {
    font-family: var(--font-body);  /* 'Open Sans', sans-serif */
}

h1, h2, h3, h4, h5, h6 {
    font-family: var(--font-heading);  /* 'Poppins', sans-serif */
    font-weight: 700;
}
```

---

## 📖 Hover Effects & Transitions

### Why Hover Effects Matter

When a visitor hovers over a button and **nothing happens**, the website feels dead. But when a card lifts slightly, a button glows, or a nav link gets an animated underline — the website feels **alive and professional**.

Think of it like walking into a shop — a good shop has music playing, lights adjusting as you walk, products that draw your eye. Hover effects are the web equivalent.

### The `transition` Property

📌 The `transition` property tells the browser: *"When a property changes, don't change it instantly — animate it smoothly over time."*

```css
/* Syntax */
transition: property duration timing-function;

/* Examples */
transition: transform 0.3s ease;            /* Only animate transform */
transition: all 0.3s ease;                   /* Animate ALL properties */
transition: transform 0.3s ease, box-shadow 0.3s ease;  /* Multiple */
```

| Part | What It Means | Example |
|------|--------------|---------|
| `property` | Which CSS property to animate | `transform`, `opacity`, `all` |
| `duration` | How long the animation takes | `0.3s` (300 milliseconds) |
| `timing-function` | Speed curve of the animation | `ease` (slow start/end, fast middle) |

### Card Hover Effect — "Lift Off"

When you hover over a faculty card, it should gently lift up and gain a deeper shadow:

```css
.card {
    transition: transform var(--transition-speed) ease,
                box-shadow var(--transition-speed) ease;
    border: none;
    border-radius: var(--border-radius);
    box-shadow: var(--shadow-sm);
}

.card:hover {
    transform: translateY(-5px);    /* Move 5 pixels UP */
    box-shadow: var(--shadow-md);   /* Deeper shadow = "lifted" look */
}
```

📌 `translateY(-5px)` — Negative value moves UP. Think of a Y-axis graph: negative = up, positive = down. The card literally "lifts off the page" by 5 pixels.

### Button Hover Effect — "Pulse & Glow"

```css
.btn-primary {
    background-color: var(--primary-color);
    border-color: var(--primary-color);
    transition: all var(--transition-speed) ease;
}

.btn-primary:hover {
    transform: scale(1.05);                              /* 5% bigger */
    box-shadow: 0 4px 12px rgba(52, 152, 219, 0.4);     /* Blue glow */
    background-color: var(--accent-color);
}
```

### Nav Link Hover Effect — "Animated Underline"

This is the most impressive effect — an underline that grows from the center when you hover:

```css
.nav-link {
    position: relative;          /* Needed for ::after positioning */
    color: var(--text-dark);
    transition: color var(--transition-speed) ease;
}

/* 📌 ::after creates an invisible element right after the link text */
.nav-link::after {
    content: '';                 /* Empty content — we just want the line */
    position: absolute;
    width: 0;                   /* Starts invisible (zero width) */
    height: 2px;
    bottom: 0;
    left: 50%;                  /* Starts from center */
    background-color: var(--accent-color);
    transition: all var(--transition-speed) ease;
}

/* On hover, the line expands to full width from center */
.nav-link:hover::after {
    width: 100%;
    left: 0;                    /* Now starts from the left edge */
}

.nav-link:hover {
    color: var(--accent-color);
}
```

📌 **`::after` Pseudo-Element:** This creates a "virtual" element that doesn't exist in the HTML. It's like having an invisible underline decoration that only appears when the mouse is nearby. The `content: ''` is required — without it, the pseudo-element won't render.

---

## 📖 Smooth Scrolling

When someone clicks a navbar link (e.g., "Gallery"), the page currently **jumps** to that section. Let's make it **glide** smoothly:

```css
html {
    scroll-behavior: smooth;
    scroll-padding-top: 70px;   /* Offset for fixed navbar height */
}
```

That's it — two lines! Now every anchor link (`<a href="#gallery">`) scrolls smoothly.

📌 **`scroll-padding-top: 70px;`** — Without this, the section heading would hide behind the fixed navbar. This adds 70px of padding so the section starts just below the navbar. Adjust this value to match your navbar's height.

---

## 📖 Section Styling & Dividers

### Clean Section Separation

Right now our sections flow into each other without clear boundaries. Let's add subtle dividers:

```css
section {
    padding: 60px 0;
    position: relative;
}

/* Add a subtle line between consecutive sections */
section + section {
    border-top: 1px solid #eee;
}

/* Alternating background for visual rhythm */
section:nth-child(even) {
    background-color: var(--bg-light);
}
```

📌 **`section + section`** — This is the **adjacent sibling selector**. It means "a `<section>` that comes *immediately after* another `<section>`." The first section gets no top border; every subsequent one does.

---

## 📖 Gallery Image Hover Effect

Make gallery images feel interactive — zoom slightly and brighten on hover:

```css
.gallery-img {
    border-radius: var(--border-radius);
    transition: transform 0.3s ease, filter 0.3s ease;
    cursor: pointer;
    overflow: hidden;
}

.gallery-img:hover {
    transform: scale(1.05);
    filter: brightness(1.1);       /* 10% brighter */
}
```

📌 **`filter: brightness(1.1)`** — CSS filters let you apply Photoshop-like effects to elements. `1.0` is normal, `1.1` is 10% brighter, `0.8` would be 20% darker. Other filters include `blur()`, `grayscale()`, and `contrast()`.

---

## 📖 Enhanced Dark Mode Styles

In Session 11, we added dark mode with JavaScript toggling a `dark-mode` class. Let's enhance it with **proper CSS variable overrides**:

```css
body.dark-mode {
    /* Override the light-mode variables */
    --primary-color: #3498db;
    --secondary-color: #e74c3c;
    --accent-color: #5dade2;
    --bg-light: #16213e;
    --text-dark: #ecf0f1;
    --shadow-sm: 0 2px 8px rgba(0, 0, 0, 0.3);
    --shadow-md: 0 4px 16px rgba(0, 0, 0, 0.4);

    background-color: var(--bg-dark);
    color: var(--text-light);
}
```

📌 **The magic of CSS variables + dark mode:** When `body.dark-mode` is active, `--primary-color` changes from `#2c3e50` to `#3498db`. Every single element using `var(--primary-color)` — headings, buttons, borders — automatically updates. No JavaScript required for the color change!

```css
/* Dark mode specific element overrides */
body.dark-mode .card {
    background-color: #1a1a2e;
    border: 1px solid #2a2a4a;
}

body.dark-mode .navbar {
    background-color: #0f3460 !important;
}

body.dark-mode section + section {
    border-top-color: #2a2a4a;
}

body.dark-mode .form-control {
    background-color: #16213e;
    border-color: #2a2a4a;
    color: var(--text-light);
}

body.dark-mode .table {
    color: var(--text-light);
}

body.dark-mode footer {
    background-color: #0a0a1a !important;
}
```

---

## 📖 Responsive Adjustments

Bootstrap handles most responsiveness, but our custom styles need fine-tuning on smaller screens:

```css
@media (max-width: 768px) {
    .display-4 {
        font-size: 1.8rem;         /* Smaller hero heading on mobile */
    }

    .lead {
        font-size: 1rem;            /* Smaller subtitle text */
    }

    section {
        padding: 40px 0;            /* Less vertical padding on mobile */
    }

    .card:hover {
        transform: none;            /* Disable lift on mobile (no hover) */
    }
}

@media (max-width: 576px) {
    h2 {
        font-size: 1.5rem;
    }

    .btn {
        font-size: 0.9rem;
        padding: 0.4rem 0.8rem;
    }
}
```

📌 **Why disable card hover on mobile?** Mobile devices don't have a mouse cursor — there's no "hover" on a touchscreen. The `:hover` pseudo-class behaves oddly on mobile (sometimes sticking after a tap). It's cleaner to disable hover transforms on small screens.

---

## 📖 Print-Friendly Styles (Bonus)

When a student tries to print the timetable or contact info, we don't want the navbar, dark backgrounds, or animations:

```css
@media print {
    /* Hide navigation and interactive elements */
    .navbar, .back-to-top, .carousel, footer {
        display: none !important;
    }

    /* Remove shadows and backgrounds */
    .card {
        box-shadow: none !important;
        border: 1px solid #ccc !important;
    }

    /* Ensure readable text */
    body {
        color: #000 !important;
        background: #fff !important;
    }

    /* Show link URLs in print */
    a[href]::after {
        content: " (" attr(href) ")";
        font-size: 0.8em;
        color: #666;
    }
}
```

📌 **`@media print`** — These styles ONLY apply when someone hits Ctrl+P (print). On screen, they're completely ignored. The `a[href]::after` trick is clever — it prints the actual URL next to every link, since you can't click a piece of paper!

---

## 🔨 Let's Build! — Step by Step

### Step 1: Create the File

1. In your project folder, create a new folder called `css` (if it doesn't already exist)
2. Inside `css`, create a new file called `custom.css`
3. Your project structure should now be:

```
📂 BCA-Website/
├── 📄 index.html
├── 📂 js/
│   └── 📄 script.js
├── 📂 css/
│   └── 📄 custom.css    ← NEW!
└── 📂 images/
```

### Step 2: Add Links in `<head>` of `index.html`

Add these two lines AFTER the Bootstrap CSS link:

```html
<!-- Google Fonts -->
<link href="https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;600&family=Poppins:wght@600;700&display=swap"
      rel="stylesheet">

<!-- Custom CSS (MUST be last!) -->
<link rel="stylesheet" href="css/custom.css">
```

### Step 3: Write the Complete `custom.css`

Copy the following complete stylesheet into `css/custom.css`:

```css
/* ============================================================
   BCA Batch 2025-26 — Custom Stylesheet
   Session 13: "Dress to Impress"
   This file loads AFTER Bootstrap to override default styles.
   ============================================================ */

/* ============================================================
   1. CSS CUSTOM PROPERTIES (VARIABLES)
   Change these to instantly re-theme the entire website.
   ============================================================ */
:root {
    /* Color Scheme */
    --primary-color: #2c3e50;
    --secondary-color: #e74c3c;
    --accent-color: #3498db;
    --bg-light: #f8f9fa;
    --bg-dark: #1a1a2e;
    --text-dark: #2c3e50;
    --text-light: #ecf0f1;

    /* Typography */
    --font-heading: 'Poppins', sans-serif;
    --font-body: 'Open Sans', sans-serif;

    /* Effects */
    --transition-speed: 0.3s;
    --shadow-sm: 0 2px 8px rgba(0, 0, 0, 0.1);
    --shadow-md: 0 4px 16px rgba(0, 0, 0, 0.15);
    --shadow-lg: 0 8px 32px rgba(0, 0, 0, 0.2);
    --border-radius: 8px;
}

/* ============================================================
   2. BASE STYLES & TYPOGRAPHY
   ============================================================ */
html {
    scroll-behavior: smooth;
    scroll-padding-top: 70px;
}

body {
    font-family: var(--font-body);
    color: var(--text-dark);
    line-height: 1.7;
    transition: background-color var(--transition-speed) ease,
                color var(--transition-speed) ease;
}

h1, h2, h3, h4, h5, h6 {
    font-family: var(--font-heading);
    font-weight: 700;
    color: var(--primary-color);
}

a {
    color: var(--accent-color);
    transition: color var(--transition-speed) ease;
}

a:hover {
    color: var(--secondary-color);
}

/* ============================================================
   3. NAVBAR STYLES
   ============================================================ */
.navbar {
    box-shadow: var(--shadow-sm);
    transition: background-color var(--transition-speed) ease,
                box-shadow var(--transition-speed) ease;
}

.navbar-brand {
    font-family: var(--font-heading);
    font-weight: 700;
    font-size: 1.4rem;
    color: var(--primary-color) !important;
}

.nav-link {
    position: relative;
    font-weight: 600;
    padding-bottom: 8px !important;
    transition: color var(--transition-speed) ease;
}

.nav-link::after {
    content: '';
    position: absolute;
    width: 0;
    height: 2px;
    bottom: 0;
    left: 50%;
    background-color: var(--accent-color);
    transition: all var(--transition-speed) ease;
}

.nav-link:hover::after,
.nav-link.active::after {
    width: 100%;
    left: 0;
}

.nav-link:hover {
    color: var(--accent-color) !important;
}

/* ============================================================
   4. HERO / CAROUSEL STYLES
   ============================================================ */
.carousel-caption {
    background: rgba(0, 0, 0, 0.5);
    border-radius: var(--border-radius);
    padding: 20px 30px;
    backdrop-filter: blur(4px);
}

.carousel-caption h5 {
    font-family: var(--font-heading);
    font-size: 2rem;
    color: #fff;
}

.carousel-item img {
    filter: brightness(0.85);
    transition: filter var(--transition-speed) ease;
}

/* ============================================================
   5. SECTION STYLES & DIVIDERS
   ============================================================ */
section {
    padding: 60px 0;
    position: relative;
}

section + section {
    border-top: 1px solid #eee;
}

section:nth-child(even) {
    background-color: var(--bg-light);
}

section h2 {
    margin-bottom: 1rem;
    position: relative;
    display: inline-block;
}

section h2::after {
    content: '';
    display: block;
    width: 60px;
    height: 3px;
    background: var(--accent-color);
    margin-top: 8px;
    border-radius: 2px;
    transition: width var(--transition-speed) ease;
}

section h2:hover::after {
    width: 100%;
}

/* ============================================================
   6. CARD STYLES (Faculty, About, etc.)
   ============================================================ */
.card {
    border: none;
    border-radius: var(--border-radius);
    box-shadow: var(--shadow-sm);
    overflow: hidden;
    transition: transform var(--transition-speed) ease,
                box-shadow var(--transition-speed) ease;
}

.card:hover {
    transform: translateY(-5px);
    box-shadow: var(--shadow-md);
}

.card-title {
    font-family: var(--font-heading);
    color: var(--primary-color);
}

.card-body {
    padding: 1.5rem;
}

.card-img-top {
    transition: transform var(--transition-speed) ease;
}

.card:hover .card-img-top {
    transform: scale(1.03);
}

/* ============================================================
   7. BUTTON STYLES
   ============================================================ */
.btn {
    border-radius: var(--border-radius);
    font-family: var(--font-heading);
    font-weight: 600;
    padding: 0.5rem 1.5rem;
    transition: all var(--transition-speed) ease;
}

.btn-primary {
    background-color: var(--primary-color);
    border-color: var(--primary-color);
}

.btn-primary:hover {
    background-color: var(--accent-color);
    border-color: var(--accent-color);
    transform: scale(1.05);
    box-shadow: 0 4px 12px rgba(52, 152, 219, 0.4);
}

.btn-secondary {
    background-color: var(--secondary-color);
    border-color: var(--secondary-color);
}

.btn-secondary:hover {
    transform: scale(1.05);
    box-shadow: 0 4px 12px rgba(231, 76, 60, 0.4);
}

.btn-outline-primary {
    color: var(--primary-color);
    border-color: var(--primary-color);
}

.btn-outline-primary:hover {
    background-color: var(--primary-color);
    border-color: var(--primary-color);
    transform: scale(1.05);
}

/* ============================================================
   8. TABLE STYLES (Timetable)
   ============================================================ */
.table {
    border-radius: var(--border-radius);
    overflow: hidden;
}

.table thead {
    background-color: var(--primary-color);
    color: #fff;
}

.table thead th {
    font-family: var(--font-heading);
    font-weight: 600;
    border: none;
    padding: 12px 16px;
}

.table tbody tr {
    transition: background-color var(--transition-speed) ease;
}

.table tbody tr:hover {
    background-color: rgba(52, 152, 219, 0.08);
}

/* ============================================================
   9. GALLERY IMAGE STYLES
   ============================================================ */
.gallery-img {
    border-radius: var(--border-radius);
    transition: transform 0.3s ease, filter 0.3s ease;
    cursor: pointer;
}

.gallery-img:hover {
    transform: scale(1.05);
    filter: brightness(1.1);
}

/* ============================================================
   10. FORM STYLES (Contact, Login)
   ============================================================ */
.form-control,
.form-select {
    border-radius: var(--border-radius);
    border: 1px solid #ddd;
    padding: 0.6rem 1rem;
    transition: border-color var(--transition-speed) ease,
                box-shadow var(--transition-speed) ease;
}

.form-control:focus,
.form-select:focus {
    border-color: var(--accent-color);
    box-shadow: 0 0 0 0.2rem rgba(52, 152, 219, 0.25);
}

.form-label {
    font-weight: 600;
    color: var(--text-dark);
    margin-bottom: 0.4rem;
}

/* ============================================================
   11. ACCORDION STYLES (FAQ)
   ============================================================ */
.accordion-button {
    font-family: var(--font-heading);
    font-weight: 600;
    transition: background-color var(--transition-speed) ease;
}

.accordion-button:not(.collapsed) {
    background-color: rgba(52, 152, 219, 0.1);
    color: var(--primary-color);
}

.accordion-button:focus {
    box-shadow: 0 0 0 0.2rem rgba(52, 152, 219, 0.25);
}

/* ============================================================
   12. FOOTER STYLES
   ============================================================ */
footer {
    background-color: var(--primary-color) !important;
    color: var(--text-light);
    padding: 40px 0 20px;
}

footer a {
    color: var(--accent-color);
}

footer a:hover {
    color: #fff;
    text-decoration: underline;
}

/* ============================================================
   13. BACK-TO-TOP BUTTON
   ============================================================ */
.back-to-top {
    border-radius: 50%;
    width: 45px;
    height: 45px;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: var(--primary-color);
    color: #fff;
    box-shadow: var(--shadow-md);
    transition: all var(--transition-speed) ease;
}

.back-to-top:hover {
    background-color: var(--accent-color);
    transform: translateY(-3px);
    box-shadow: var(--shadow-lg);
}

/* ============================================================
   14. COUNTDOWN TIMER
   ============================================================ */
.countdown-timer {
    font-family: var(--font-heading);
    font-size: 1.5rem;
    color: var(--secondary-color);
    letter-spacing: 1px;
}

/* ============================================================
   15. DARK MODE OVERRIDES
   ============================================================ */
body.dark-mode {
    --primary-color: #3498db;
    --secondary-color: #e74c3c;
    --accent-color: #5dade2;
    --bg-light: #16213e;
    --text-dark: #ecf0f1;
    --shadow-sm: 0 2px 8px rgba(0, 0, 0, 0.3);
    --shadow-md: 0 4px 16px rgba(0, 0, 0, 0.4);

    background-color: var(--bg-dark);
    color: var(--text-light);
}

body.dark-mode .card {
    background-color: #1a1a2e;
    border: 1px solid #2a2a4a;
}

body.dark-mode .navbar {
    background-color: #0f3460 !important;
}

body.dark-mode .navbar-brand {
    color: var(--text-light) !important;
}

body.dark-mode section + section {
    border-top-color: #2a2a4a;
}

body.dark-mode section:nth-child(even) {
    background-color: #16213e;
}

body.dark-mode .form-control,
body.dark-mode .form-select {
    background-color: #16213e;
    border-color: #2a2a4a;
    color: var(--text-light);
}

body.dark-mode .table {
    color: var(--text-light);
}

body.dark-mode .table thead {
    background-color: #0f3460;
}

body.dark-mode .accordion-button {
    background-color: #1a1a2e;
    color: var(--text-light);
}

body.dark-mode .accordion-body {
    background-color: #16213e;
    color: var(--text-light);
}

body.dark-mode footer {
    background-color: #0a0a1a !important;
}

body.dark-mode .carousel-caption {
    background: rgba(0, 0, 0, 0.7);
}

body.dark-mode .modal-content {
    background-color: #1a1a2e;
    color: var(--text-light);
}

/* ============================================================
   16. RESPONSIVE ADJUSTMENTS
   ============================================================ */
@media (max-width: 768px) {
    .display-4 {
        font-size: 1.8rem;
    }

    .lead {
        font-size: 1rem;
    }

    section {
        padding: 40px 0;
    }

    .card:hover {
        transform: none;
    }

    .carousel-caption h5 {
        font-size: 1.2rem;
    }

    .carousel-caption {
        padding: 10px 15px;
    }
}

@media (max-width: 576px) {
    h2 {
        font-size: 1.5rem;
    }

    .btn {
        font-size: 0.9rem;
        padding: 0.4rem 0.8rem;
    }

    .navbar-brand {
        font-size: 1.1rem;
    }
}

/* ============================================================
   17. PRINT STYLES
   ============================================================ */
@media print {
    .navbar,
    .back-to-top,
    .carousel,
    footer,
    .btn {
        display: none !important;
    }

    .card {
        box-shadow: none !important;
        border: 1px solid #ccc !important;
        break-inside: avoid;
    }

    body {
        color: #000 !important;
        background: #fff !important;
        font-size: 12pt;
    }

    section {
        padding: 20px 0;
    }

    a[href]::after {
        content: " (" attr(href) ")";
        font-size: 0.8em;
        color: #666;
    }
}

/* ============================================================
   18. UTILITY CLASSES
   ============================================================ */
.text-accent {
    color: var(--accent-color);
}

.bg-brand {
    background-color: var(--primary-color);
    color: var(--text-light);
}

.shadow-hover {
    transition: box-shadow var(--transition-speed) ease;
}

.shadow-hover:hover {
    box-shadow: var(--shadow-md);
}
```

> 🎨 **That's 300+ lines of production-quality CSS!** Every section of our website is now custom-styled, with hover effects, transitions, dark mode support, responsive design, and even print-friendly styles.

### Step 4: Test Your Changes

1. **Save** both `index.html` and `css/custom.css`
2. **Open** `index.html` in Chrome
3. Check each of these:
   - [ ] Fonts changed? (Headings should look different — Poppins is geometric and modern)
   - [ ] Hover over a card — does it lift up with a shadow?
   - [ ] Hover over a nav link — does the underline animate from center?
   - [ ] Hover over a button — does it scale up slightly?
   - [ ] Click a navbar link — does it scroll smoothly?
   - [ ] Toggle dark mode — do colors change smoothly?
   - [ ] Resize window to mobile — do hover effects disable?
4. **Open DevTools** (F12) → go to the **Elements** tab → click on any element → check that your CSS is applying (look for `custom.css` in the Styles panel)

### Step 5: Verify CSS is Overriding Bootstrap

In DevTools, you should see your custom rules with Bootstrap rules **crossed out** beneath them:

```
.btn-primary {
    background-color: #2c3e50;     ← from custom.css (ACTIVE)
    border-color: #2c3e50;         ← from custom.css (ACTIVE)
}

.btn-primary {
    background-color: #0d6efd;     ← from bootstrap.min.css (CROSSED OUT)
    border-color: #0d6efd;         ← from bootstrap.min.css (CROSSED OUT)
}
```

If your styles are crossed out instead, check:
- Is `custom.css` linked AFTER Bootstrap in `<head>`?
- Is the file path correct? (check for typos in `href="css/custom.css"`)

---

## ✅ Checkpoint

Open `index.html` in the browser and verify everything:

| # | Check | Expected Result | ✅ / ❌ |
|---|-------|----------------|---------|
| 1 | Fonts changed | Headings use Poppins, body uses Open Sans | |
| 2 | Card hover | Cards lift up 5px with deeper shadow on hover | |
| 3 | Button hover | Buttons scale up and glow on hover | |
| 4 | Nav link hover | Animated underline grows from center on hover | |
| 5 | Smooth scrolling | Clicking nav links scrolls smoothly (not jumping) | |
| 6 | Section dividers | Subtle line between sections, alternating backgrounds | |
| 7 | Gallery hover | Images zoom slightly and brighten on hover | |
| 8 | Dark mode | All sections styled correctly (cards, forms, tables) | |
| 9 | Mobile view (resize) | Card hover disabled, text sizes adjusted | |
| 10 | DevTools check | `custom.css` rules override Bootstrap rules | |

### 🐛 Troubleshooting

| Problem | Solution |
|---------|----------|
| No style changes visible | Check `<link>` path: `css/custom.css` — case-sensitive! |
| Bootstrap styles not overridden | Make sure `custom.css` link is AFTER Bootstrap link |
| Fonts not loading | Check Google Fonts `<link>` — must be before `custom.css` |
| Hover effects jerky | Check `transition` is on the base state, not the `:hover` state |
| Dark mode colors wrong | Verify `body.dark-mode` selector matches your JS toggle class |
| Print styles not working | Use Ctrl+P to preview — they only apply when printing |

---

## 🔍 Quick Reference

### CSS Properties Used Today

| Property | What It Does | Example |
|----------|-------------|---------|
| `font-family` | Sets the typeface for text | `font-family: 'Poppins', sans-serif;` |
| `transition` | Smoothly animates property changes | `transition: all 0.3s ease;` |
| `transform` | Moves, scales, or rotates an element | `transform: translateY(-5px);` |
| `box-shadow` | Adds shadow around element | `box-shadow: 0 4px 16px rgba(0,0,0,0.15);` |
| `filter` | Applies visual effects (blur, brightness, etc.) | `filter: brightness(1.1);` |
| `scroll-behavior` | Controls scroll animation | `scroll-behavior: smooth;` |
| `scroll-padding-top` | Offset for fixed header during scroll | `scroll-padding-top: 70px;` |
| `backdrop-filter` | Blurs background behind element | `backdrop-filter: blur(4px);` |
| `border-radius` | Rounds element corners | `border-radius: 8px;` |
| `cursor` | Changes mouse cursor style | `cursor: pointer;` |

### CSS Selectors Used Today

| Selector | Meaning | Example |
|----------|---------|---------|
| `:root` | The document root (top-level scope) | `:root { --color: blue; }` |
| `.class:hover` | When mouse is over an element with that class | `.card:hover { ... }` |
| `::after` | Virtual element after content | `.nav-link::after { ... }` |
| `section + section` | A section immediately after another section | `section + section { border-top: ... }` |
| `:nth-child(even)` | Every even-numbered child element | `section:nth-child(even) { ... }` |
| `body.dark-mode .card` | A card inside body when dark mode is active | `body.dark-mode .card { ... }` |
| `@media (max-width)` | Styles for screens at or below a width | `@media (max-width: 768px) { ... }` |
| `@media print` | Styles only for printing | `@media print { ... }` |

### CSS Variable Cheat Sheet

| Variable | Light Mode Value | Dark Mode Value | Used For |
|----------|-----------------|----------------|----------|
| `--primary-color` | `#2c3e50` | `#3498db` | Headings, buttons, brand |
| `--secondary-color` | `#e74c3c` | `#e74c3c` | Alerts, highlights |
| `--accent-color` | `#3498db` | `#5dade2` | Links, hover effects |
| `--bg-light` | `#f8f9fa` | `#16213e` | Alternating section bg |
| `--text-dark` | `#2c3e50` | `#ecf0f1` | Body text color |
| `--font-heading` | `'Poppins'` | `'Poppins'` | All headings |
| `--font-body` | `'Open Sans'` | `'Open Sans'` | Body text |
| `--transition-speed` | `0.3s` | `0.3s` | All animations |

---

## 📝 Key Takeaways

1. **External CSS is the professional approach** — one file controls the entire website's look. Never use inline styles in production.

2. **Link order matters** — your `custom.css` MUST load AFTER Bootstrap CSS. Last loaded = highest priority when specificity is equal.

3. **CSS specificity is a point system** — `#id` (100) beats `.class` (10) beats `element` (1). Equal specificity? Last rule wins.

4. **CSS variables (`--custom-property`)** are game-changers — define colors once in `:root`, use them everywhere with `var()`, and change the entire theme by editing one line.

5. **Transitions go on the BASE state, not the hover state** — put `transition: all 0.3s ease;` on `.card`, not on `.card:hover`. The transition property tells the browser *how* to animate, the hover state tells it *what* to animate to.

6. **`::after` pseudo-elements** create virtual elements for decorative effects without adding extra HTML — perfect for animated underlines and dividers.

7. **Dark mode + CSS variables = automatic theming** — redefine variables inside `body.dark-mode` and every element using those variables updates instantly.

8. **Disable hover effects on mobile** — touchscreens don't have a cursor. Use `@media (max-width: 768px)` to remove `transform` on hover.

9. **Google Fonts pair wisely** — one decorative font for headings, one readable font for body text. Never use more than 2-3 fonts.

10. **`@media print` is underrated** — students printing timetables or notes will thank you. Hide navbars, remove shadows, and show link URLs.

---

## 🏋️ Practice Challenges

Try these on your own to cement today's CSS skills:

### Challenge 1: Create a Second Theme (⭐ Easy)

Change the CSS variables to create a completely different color scheme. Try an "MU Blue & Gold" theme:

```css
:root {
    --primary-color: #1a237e;       /* Dark indigo */
    --secondary-color: #ffc107;     /* Gold */
    --accent-color: #42a5f5;        /* Light blue */
}
```

**Hints:**
- Only change the `:root` variable values — nothing else!
- Verify that buttons, headings, nav underlines ALL changed automatically
- This proves the power of CSS variables

### Challenge 2: Add a Parallax Effect on the Hero Section (⭐⭐ Medium)

Make the hero/carousel background appear to move slower than the foreground when scrolling:

```css
.hero-section {
    background-attachment: fixed;
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
}
```

**Hints:**
- `background-attachment: fixed;` creates the parallax illusion
- Apply this to the hero section or a section with a background image
- Test by scrolling — the background should appear "deeper" than the content
- Note: This doesn't work on most mobile browsers (iOS ignores `fixed`)

### Challenge 3: CSS Animation on the Countdown Timer (⭐⭐⭐ Hard)

Add a pulsing animation to the countdown timer to draw attention:

```css
@keyframes pulse {
    0% { transform: scale(1); }
    50% { transform: scale(1.05); opacity: 0.8; }
    100% { transform: scale(1); }
}

.countdown-timer {
    animation: pulse 2s ease-in-out infinite;
}
```

**Hints:**
- `@keyframes` defines the animation steps (0% → 50% → 100%)
- `animation: name duration timing iterations;`
- `infinite` makes it loop forever
- Try adding `animation-play-state: paused;` on hover to let users "stop" the pulse

> 💡 **New concepts in Challenge 3:** `@keyframes` defines custom animations frame by frame. Unlike `transition` (which only animates between two states), `@keyframes` can have multiple steps and loop infinitely. We'll explore animations more in Session 14!

---

## 🔗 Labs Covered in This Session

| Lab # | Experiment Description | Status | How It's Covered |
|-------|----------------------|--------|-----------------|
| **Lab 10** | Inline CSS styling | ✅ Done | Compared inline vs. external; explained why inline is discouraged |
| **Lab 11** | External CSS file | ✅ Done | Created `css/custom.css`, linked to `index.html`, overrides Bootstrap |

*Running total: Labs 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 24, 25, 26, 27, 28, 29, 30 covered (29 of 30)*

---

## ⏭️ Next Session Preview

### Session 14: "Quality Check" — Responsive Testing + Accessibility

In the next session, we'll make sure our website works **for everyone, on every device:**

- 📖 **Responsive testing** — Chrome DevTools device emulator, testing on real phones
- 📖 **Accessibility (a11y)** — `aria-label`, `alt` text audit, keyboard navigation
- 📖 **Semantic HTML audit** — ensuring proper heading hierarchy and landmarks
- 📖 **Performance checks** — image optimization, CSS/JS load order
- 📖 **Cross-browser testing** — does it look right on Chrome, Firefox, and Edge?
- 📖 **Frames concept** (Lab 8) — why frames are deprecated and how CSS Grid replaced them

> 💡 **Building a website is 60% coding and 40% testing.** Today we made it *look* great. Next session we make sure it *works* great — on every screen, every browser, and for every user including those with disabilities.

**Labs covered next time:** Lab 22 (Department website project), Lab 8 (Frames layout) ✅

---

*Session 13 of 15 — Crash Course: Bootstrap + JavaScript — BCA Semester II, Mandsaur University, 2025-26*
