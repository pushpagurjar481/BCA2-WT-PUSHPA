# Session 14: "Test Everything" — Responsive Testing + Accessibility

**BCA Semester II | Mandsaur University | Web Technology (25BCA060)**

> **Session 14 of 15** | ⏱️ Duration: 2 hours  
> **Labs Covered:** Lab 22 (Responsive testing), Lab 8 (Frames & deprecated elements)  
> **No new sections today** — we TEST, FIX, and POLISH the entire website

---

## 🎯 What We'll Do Today

Today is **Quality Assurance day**. Think of it like a car's final inspection before delivery — the car is built (our website is complete!), but we need to check every door, every mirror, every light before handing it over to the customer.

We're NOT building anything new. Instead, we're doing what professional developers spend **30–40% of their time** doing:

- 🔍 **Testing** the website across different screen sizes
- 🔧 **Fixing** responsive layout issues
- ♿ **Adding** accessibility features so everyone can use our website
- 📊 **Auditing** with Lighthouse to measure quality scores
- ✅ **Validating** our HTML to ensure standards compliance
- 🧹 **Cleaning up** our code for production-readiness

> 💡 "A website that looks great on YOUR laptop but breaks on a phone is only half-finished. Would you submit an exam paper where you only answered half the questions?" — That's what shipping untested code feels like.

**Our website so far has:** Navbar, Hero Carousel, About, Faculty Cards, Timetable, Gallery, Contact Form, Login Modal, Countdown Timer, Dark Mode Toggle, Back-to-Top Button, FAQ Accordion, Footer — split across `index.html`, `script.js`, and `custom.css`.

---

## 📋 The Ultimate Testing Checklist

Before we begin testing, here's the **master checklist** we'll work through today. Print this out (or keep it open in a tab) and tick off each item:

| #  | Category | Check | Status |
|----|----------|-------|--------|
| 1  | Responsive | Navbar hamburger appears on mobile (< 992px) | ⬜ |
| 2  | Responsive | Hamburger menu opens and closes on tap | ⬜ |
| 3  | Responsive | Carousel images scale without cropping text | ⬜ |
| 4  | Responsive | Faculty cards: 1 col on mobile, 2 on tablet, 3 on desktop | ⬜ |
| 5  | Responsive | Timetable scrolls horizontally on small screens | ⬜ |
| 6  | Responsive | Gallery images rearrange to fewer columns on mobile | ⬜ |
| 7  | Responsive | Contact form inputs are full-width on mobile | ⬜ |
| 8  | Responsive | Footer columns stack vertically on mobile | ⬜ |
| 9  | Responsive | No horizontal scrollbar at any breakpoint | ⬜ |
| 10 | Responsive | Text is readable without zooming at 320px | ⬜ |
| 11 | A11y | All `<img>` tags have meaningful `alt` text | ⬜ |
| 12 | A11y | All form inputs have associated `<label>` elements | ⬜ |
| 13 | A11y | ARIA labels on icon-only buttons (dark mode, back-to-top) | ⬜ |
| 14 | A11y | Can Tab through all interactive elements in order | ⬜ |
| 15 | A11y | Focused elements have visible outline/ring | ⬜ |
| 16 | A11y | Color contrast passes (4.5:1 ratio for text) | ⬜ |
| 17 | A11y | Heading hierarchy is correct (h1 → h2 → h3, no skips) | ⬜ |
| 18 | Validation | No HTML validation errors on W3C validator | ⬜ |
| 19 | Validation | No duplicate `id` attributes | ⬜ |
| 20 | Validation | No unclosed tags | ⬜ |
| 21 | Performance | Images have `loading="lazy"` (below the fold) | ⬜ |
| 22 | Performance | No unused CSS classes | ⬜ |
| 23 | SEO | `<meta name="description">` exists | ⬜ |
| 24 | SEO | `<html lang="en">` is set | ⬜ |
| 25 | Code Quality | Consistent indentation throughout | ⬜ |
| 26 | Code Quality | No leftover `console.log()` statements | ⬜ |
| 27 | Functionality | Dark mode toggle works and persists | ⬜ |
| 28 | Functionality | Back-to-top button appears on scroll | ⬜ |
| 29 | Functionality | Contact form validates required fields | ⬜ |
| 30 | Functionality | Countdown timer displays correct time | ⬜ |

---

## 🔧 Chrome DevTools — Your Testing Laboratory

Chrome DevTools is like a **doctor's stethoscope for websites**. It lets you see what's happening under the surface.

### Opening DevTools

| Method | Shortcut |
|--------|----------|
| Keyboard | `F12` or `Ctrl + Shift + I` |
| Right-click | Right-click any element → "Inspect" |

### The Device Toolbar (Responsive Mode)

**Toggle it:** `Ctrl + Shift + M` (while DevTools is open)

When you activate it, you'll see something like this:

```
┌──────────────────────────────────────────────────────────┐
│ [📱 Responsive ▼] [375 × 667] [100% ▼] [🔄]             │
├──────────────────────────────────────────────────────────┤
│   ┌────────────────────────┐                             │
│   │   Your website shown   │  You can drag edges to     │
│   │   at selected size     │  resize freely, or pick    │
│   │                        │  preset devices from the   │
│   │                        │  dropdown menu             │
│   └────────────────────────┘                             │
└──────────────────────────────────────────────────────────┘
```

---

## 📐 Responsive Testing — Breakpoint by Breakpoint

Bootstrap uses these breakpoints. We test at each one:

| Breakpoint | Width | Real Device | Bootstrap Class |
|------------|-------|-------------|-----------------|
| Extra Small | **320px** | iPhone SE (oldest common phone) | Default (no prefix) |
| Small | **375px** | iPhone 12/13/14 | `sm` (≥576px) |
| Medium | **768px** | iPad (portrait) | `md` (≥768px) |
| Large | **1024px** | iPad landscape / small laptop | `lg` (≥992px) |
| Extra Large | **1280px** | Laptop | `xl` (≥1200px) |
| XXL | **1920px** | Full HD desktop monitor | `xxl` (≥1400px) |

### What to Check at Each Breakpoint

| Element | 320px (Phone) | 768px (Tablet) | 1024px+ (Desktop) |
|---------|---------------|-----------------|---------------------|
| Navbar | Hamburger visible, menu opens/closes | Hamburger still shows (< 992px) | Full horizontal links visible |
| Hero Carousel | Fills width, captions readable | Images scale well | Content centered in container |
| Faculty Cards | 1 per row, no overflow | 2 per row, equal height | 3 per row, balanced layout |
| Timetable | Horizontal scroll works | May still scroll | Full table visible |
| Contact Form | Inputs full-width | Inputs properly sized | Side-by-side fields if designed |
| Gallery | 1–2 columns | 2–3 columns | 3–4 columns |
| Footer | Columns stacked vertically | 2–3 columns side by side | Full column layout |
| General | No horizontal scrollbar! | No awkward gaps | Content doesn't stretch edge-to-edge |

---

## 🔨 Common Responsive Issues and Fixes

### Issue 1: Text Overflows Its Container

**Symptom:** Long words (like email addresses) break out of their box on mobile.

```css
/* Add to custom.css */
.overflow-fix {
    overflow-wrap: break-word;
    word-wrap: break-word;
    word-break: break-word;
}
```

> 💡 **Analogy:** It's like a long train that doesn't fit in the station — you tell it to "break" into smaller coaches that fit.

### Issue 2: Images Not Scaling

**Symptom:** An image is wider than the screen on mobile.

**Fix:** Ensure ALL images have the `img-fluid` class:

```html
<!-- ❌ Wrong — image has fixed width -->
<img src="photo.jpg" width="600">

<!-- ✅ Correct — image scales with container -->
<img src="photo.jpg" class="img-fluid" alt="BCA students in computer lab">
```

### Issue 3: Table Not Scrollable on Mobile

**Symptom:** The timetable breaks the page layout on phones.

**Fix:** Ensure the table is wrapped in `table-responsive`:

```html
<!-- ✅ Correct — table scrolls horizontally on small screens -->
<div class="table-responsive">
    <table class="table table-striped table-hover">
        <!-- ... table content ... -->
    </table>
</div>
```

### Issue 4: Fixed Elements Blocking Content on Mobile

**Fix:** Adjust position/size for mobile:

```css
@media (max-width: 576px) {
    #backToTop { width: 36px; height: 36px; font-size: 14px; bottom: 15px; right: 15px; }
}
```

### Issue 5: Font Sizes Too Large on Mobile

**Fix:** Add responsive font sizing:

```css
@media (max-width: 576px) {
    h1 { font-size: 1.75rem; }
    h2 { font-size: 1.5rem; }
}
```

---

## ♿ Accessibility (A11y) — Making Our Website for EVERYONE

> "Accessibility is not a feature. It's a social responsibility." — Think of it like building ramps alongside stairs. The stairs work for most people, but the ramp makes the building usable by EVERYONE.

In India, the **Rights of Persons with Disabilities Act, 2016** requires government websites to be accessible. Even for private websites, accessibility is good practice — and Google ranks accessible websites higher!

### Who Benefits from Accessibility?

| User | Challenge | How They Browse |
|------|-----------|-----------------|
| Blind or low-vision users | Can't see the screen | Use **screen readers** (JAWS, NVDA, VoiceOver) that read text aloud |
| Motor-impaired users | Can't use a mouse | Navigate with **keyboard only** (Tab, Enter, Arrow keys) |
| Color-blind users | Can't distinguish certain colors | Need **sufficient contrast** and text labels (not just colors) |
| Deaf users | Can't hear audio | Need **captions** and **transcripts** |
| Cognitive disabilities | Difficulty processing complex info | Need **clear layout**, **simple language**, **consistent navigation** |

### Fix 1: Meaningful Alt Text on All Images

```html
<!-- ❌ Bad — meaningless alt text -->
<img src="img1.jpg" alt="image1">
<img src="photo.jpg" alt="">
<img src="campus.jpg">  <!-- missing alt entirely! -->

<!-- ✅ Good — descriptive alt text -->
<img src="img1.jpg" alt="BCA students working in the computer lab">
<img src="photo.jpg" alt="Mandsaur University main building at sunset">
<img src="campus.jpg" alt="Group photo of BCA Batch 2025-26 at the annual fest">
```

> 💡 **Rule of thumb:** Describe what you SEE in the image. If you were describing the photo to a friend on a phone call, what would you say?

**For decorative images** (like background patterns), use an empty alt: `alt=""`. This tells screen readers to skip the image.

### Fix 2: ARIA Labels on Icon-Only Buttons

Buttons with only icons (no visible text) need `aria-label` so screen readers can announce them:

```html
<!-- ❌ Screen reader says: "Button" — useless! -->
<button id="darkModeToggle">🌙</button>

<!-- ✅ Screen reader says: "Toggle dark mode" — helpful! -->
<button id="darkModeToggle" aria-label="Toggle dark mode">🌙</button>

<!-- ✅ Back-to-top button -->
<button id="backToTop" aria-label="Scroll back to top">↑</button>

<!-- ✅ Navbar toggler -->
<button class="navbar-toggler" aria-label="Toggle navigation menu">
    <span class="navbar-toggler-icon"></span>
</button>
```

### Fix 3: Form Labels Properly Linked

Every input MUST have a label. The label's `for` attribute must match the input's `id`:

```html
<!-- ✅ Correct — label is linked to input via for/id -->
<label for="contactName" class="form-label">Your Name</label>
<input type="text" class="form-control" id="contactName" name="name">

<!-- ❌ Wrong — no label, just a placeholder -->
<input type="text" class="form-control" placeholder="Enter your name">
```

> 💡 **Why does this matter?** When a blind user tabs to an input field, the screen reader reads the label aloud. Without it, the user hears "Edit text" — they have no idea what to type!

### Fix 4: Keyboard Navigation Test

Press `Tab` repeatedly from the top of the page. You must be able to reach: every navbar link, carousel controls, "Read More" buttons, form fields, submit button, login modal inputs, dark mode toggle, FAQ accordion buttons, footer links, and back-to-top button. **If you can't reach something with Tab, it's a bug!**

### Fix 5: Don't Remove Focus Outlines

```css
/* ❌ NEVER do this — kills keyboard navigation visibility */
*:focus { outline: none; }

/* ✅ REPLACE the outline, don't remove it */
*:focus-visible { outline: 2px solid #0d6efd; outline-offset: 2px; }
```

### Fix 6: Semantic HTML — Ensure Correct Structure

Your page should use `<nav>`, `<main>` (wrapping all sections), `<section>`, and `<footer>` — NOT generic `<div>`s for layout. If you haven't wrapped your sections in `<main>`, add it now! Screen readers use it to skip directly to content.

### Fix 7: Heading Hierarchy

Headings must follow a logical order. Don't skip levels:

```
✅ Correct:                    ❌ Wrong:
h1: BCA Batch 2025-26         h1: BCA Batch 2025-26
  h2: About Our Class            h3: About Our Class  ← skipped h2!
  h2: Our Faculty                h2: Our Faculty
    h3: Dr. Rajesh Sharma          h5: Details        ← skipped h3, h4!
  h2: Timetable                h1: Timetable          ← two h1s!
```

Your page should have exactly **ONE `<h1>`** (the website title) and then `<h2>` for each section.

---

## 📊 Lighthouse Audit — Your Website's Report Card

Lighthouse is Google's built-in website auditing tool. Think of it like getting your exam marks — it scores your website on four subjects.

### Running a Lighthouse Audit

1. Open your website in Chrome → Press `F12` → Click **"Lighthouse"** tab
2. Select: ✅ Performance, ✅ Accessibility, ✅ Best Practices, ✅ SEO
3. Device: **Mobile** (harder case first)
4. Click **"Analyze page load"** — wait 15–30 seconds

### Understanding the Scores

| Score | Meaning |
|-------|---------|
| 🟢 90–100 | Excellent |
| 🟠 50–89 | Needs improvement |
| 🔴 0–49 | Poor — significant issues |

Categories: **Performance** (page load speed), **Accessibility** (usability for everyone), **Best Practices** (web standards), **SEO** (search engine discoverability).

### Common Fixes to Boost Scores

**Performance** — Add `loading="lazy"` on images below the fold (not the hero!):
```html
<img src="faculty1.jpg" class="img-fluid" alt="Dr. Rajesh" loading="lazy">
```

**SEO** — Add to `<head>` if missing:
```html
<meta name="description" content="Official class website for BCA Batch 2025-26, Mandsaur University.">
```

**Best Practices** — Secure external links:
```html
<a href="https://example.com" target="_blank" rel="noopener noreferrer">External Link</a>
```

---

## ✅ HTML Validation — Grammar Check for Your Code

Just like a spell-checker on an essay, validate your HTML to catch syntax errors.

### How to Validate

1. Go to **https://validator.w3.org** → **"Validate by Direct Input"** tab
2. Paste your entire `index.html` → Click **"Check"**

### Common Validation Errors and Fixes

| Error Message | What It Means | Fix |
|--------------|---------------|-----|
| "Element `img` is missing required attribute `alt`" | An image has no `alt` text | Add `alt="description"` |
| "Duplicate attribute `id`" | Two elements have the same `id` | Make each `id` unique |
| "Unclosed element `div`" | A `<div>` was opened but never closed | Add the missing `</div>` |
| "Element `div` not allowed as child of `ul`" | Wrong nesting | Put `<li>` inside `<ul>`, not `<div>` |
| "The `frameset` element is obsolete" | Using deprecated frames | Remove and use modern layout |
| "Stray end tag" | Extra closing tag with no matching opening tag | Delete the extra tag |

> 💡 **Pro tip:** Fix errors from TOP to BOTTOM. Often, one error at line 50 causes a cascade of errors below it. Fixing the first one may resolve 5 others!

---

## 🖼️ Deprecated Elements — The Story of Frames (Lab 8)

### What Were Frames?

In the early web (1990s), developers used **frames** to divide a browser window into separate panels, each loading a different HTML file.

> 💡 **Analogy:** Imagine your classroom has four windows, each showing a different TV channel — one for navigation, one for content, one for sidebar. That's what frames did.

```html
<!-- ⚠️ DEPRECATED — DO NOT USE! Shown only for exam knowledge -->
<frameset rows="100px, *" cols="200px, *">
    <frame src="header.html" name="top">
    <frame src="nav.html" name="left">
    <frame src="content.html" name="main">
</frameset>
```

### Why Frames Were Deprecated

| Problem | Explanation |
|---------|-------------|
| **Accessibility nightmare** | Screen readers couldn't navigate between frames properly |
| **SEO disaster** | Search engines couldn't index framed pages correctly |
| **Bookmarking broken** | Users couldn't bookmark a specific "state" of the frames |
| **Printing impossible** | Printing a framed page would only print one frame |
| **Back button confusion** | Pressing Back affected only one frame, confusing users |
| **Mobile incompatible** | Frames don't work on small screens at all |

### What Replaced Frames?

| Old Way | Modern Replacement |
|---------|-------------------|
| `<frameset>` layout | CSS Grid, Flexbox, Bootstrap Grid |
| `<frame>` for navigation | `<nav>` element with CSS |
| `<frame>` for content | `<main>` element |
| `<iframe>` for page embedding | Still exists! Used for YouTube, Google Maps |

### `<iframe>` — The Survivor

`<iframe>` (inline frame) is the ONE frame-related element that's **NOT deprecated**. It's used for embedding external content:

```html
<!-- ✅ YouTube embed -->
<iframe src="https://www.youtube.com/embed/VIDEO_ID"
        title="Campus tour video" width="560" height="315"
        allowfullscreen loading="lazy"></iframe>

<!-- ✅ Google Maps embed -->
<iframe src="https://www.google.com/maps/embed?..."
        title="Mandsaur University location" width="600" height="450"
        style="border:0;" allowfullscreen loading="lazy"></iframe>
```

> ⚠️ **For exams:** `<frameset>` and `<frame>` are **deprecated**. `<iframe>` is **NOT deprecated**. Know the difference!

---

## 🧹 Code Cleanup Checklist

Before calling your website "done," walk through this:

**HTML:** All `<img>` have `alt` ☐ | All inputs have `<label>` ☐ | No duplicate `id`s ☐ | All tags closed ☐ | `lang="en"` on `<html>` ☐ | `<meta name="description">` exists ☐ | `<meta name="viewport">` exists ☐ | Semantic elements used (`<nav>`, `<main>`, `<section>`, `<footer>`) ☐

**CSS (custom.css):** Remove unused rules ☐ | Consistent formatting ☐ | Comment sections ☐ | No `!important` unless necessary ☐ | Media queries grouped at bottom ☐

**JavaScript (script.js):** Remove/comment `console.log()` ☐ | Comment each function ☐ | No unused variables ☐ | Error handling in place ☐

**General:** Consistent indentation (2 or 4 spaces) ☐ | No dead commented-out code ☐ | Lowercase filenames with hyphens ☐

---

## 🔨 Let's Do! — Step-by-Step Testing Procedure

### Step 1: Open Your Website and DevTools

1. Open `index.html` in Google Chrome
2. Press `F12` to open DevTools
3. Click the **Console** tab first — check for any red errors
4. If there are errors, note them down — we'll fix them

### Step 2: Responsive Testing at Each Breakpoint

Press `Ctrl + Shift + M` to toggle the device toolbar. Test at each width:

**At 320px (iPhone SE) and 375px (iPhone 12):**
- ☐ Navbar hamburger visible? Click it — menu opens?
- ☐ Carousel fits, captions readable?
- ☐ Cards: one per row, no overflow?
- ☐ Table: horizontal scroll works?
- ☐ Form inputs full-width?
- ☐ Gallery images stacked?
- ☐ Footer columns stacked?
- ☐ No horizontal scrollbar on the page?

**At 768px (iPad):**
- ☐ Hamburger still showing (< 992px)
- ☐ Cards: 2 per row, equal height?
- ☐ Gallery: 2–3 columns?
- ☐ Footer starting to show columns side by side?

**At 1024px (Laptop):**
- ☐ Navbar shows full horizontal links (≥ 992px)?
- ☐ All grid layouts at full column count?

**At 1920px (Full HD):**
- ☐ Content centered within container, not stretching edge-to-edge?
- ☐ No awkward gaps or oversized spacing?

### Step 3: Fix Any Responsive Issues Found

Apply the fixes from the "Common Responsive Issues and Fixes" section above. After each fix:
1. Save the file
2. Refresh the browser (`Ctrl + R`)
3. Re-check at the breakpoint where you found the issue

### Step 4: Accessibility Fixes

Apply all accessibility fixes from above: alt text, ARIA labels, form labels, keyboard navigation test, heading hierarchy check.

### Step 5: Run Lighthouse Audit (First Run)

1. DevTools → Lighthouse tab
2. Select: Mobile, all categories
3. Click "Analyze page load"
4. **Write down your scores:**
   - Performance: ___
   - Accessibility: ___
   - Best Practices: ___
   - SEO: ___

### Step 6: Fix Issues Lighthouse Identified

Lighthouse shows specific items to fix. Common ones:
- Add `loading="lazy"` to off-screen images
- Add missing `alt` text
- Add `<meta name="description">`
- Fix color contrast issues
- Add `rel="noopener"` to external links

### Step 7: Validate HTML

1. Go to https://validator.w3.org
2. Copy-paste your `index.html`
3. Click "Check"
4. Fix errors top-to-bottom
5. Re-validate until you see: **"Document checking completed. No errors or warnings to show."** 🎉

### Step 8: Run Lighthouse Again (Second Run)

After all fixes, run Lighthouse again and compare:

```
                BEFORE      AFTER
Performance:    ___    →    ___
Accessibility:  ___    →    ___
Best Practices: ___    →    ___
SEO:            ___    →    ___
```

> 🎯 **Goal:** All scores should be 80+ (ideally 90+). The improvement from your first run shows the impact of testing!

### Step 9: Final Code Cleanup

Walk through the Code Cleanup Checklist above. Clean up indentation, remove debug logs, add comments to complex functions.

---

## ✅ Checkpoint

Before moving to the next session, verify:

| # | Check | Expected Result |
|---|-------|----------------|
| 1 | Tested at 320px | No overflow, everything stacked and readable |
| 2 | Tested at 768px | Grid layouts showing 2 columns where appropriate |
| 3 | Tested at 1920px | Content centered, no stretching |
| 4 | All images have `alt` text | Every `<img>` has a descriptive `alt` attribute |
| 5 | Form inputs have labels | Every `<input>` linked to a `<label>` |
| 6 | Keyboard navigation works | Can Tab to every interactive element |
| 7 | Lighthouse Accessibility ≥ 80 | Accessibility score improved after fixes |
| 8 | HTML validates | W3C validator shows no errors |
| 9 | No console errors | Browser console (F12) shows no red errors |
| 10 | Code is clean | Consistent indentation, comments, no debug logs |

---

## 🔍 Quick Reference

### DevTools Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `F12` / `Ctrl + Shift + I` | Open DevTools |
| `Ctrl + Shift + M` | Toggle device toolbar |
| `Ctrl + Shift + C` | Inspect element mode |
| `Ctrl + Shift + J` | Open Console directly |
| `Esc` | Toggle console drawer (while in another tab) |

### Key Accessibility Attributes

| Attribute | Where to Use | Example |
|-----------|-------------|---------|
| `alt="..."` | All `<img>` tags | `alt="BCA students in lab"` |
| `aria-label="..."` | Buttons/links with no visible text | `aria-label="Close menu"` |
| `aria-expanded="true/false"` | Toggle buttons (accordion, collapse) | Already handled by Bootstrap! |
| `aria-hidden="true"` | Decorative elements screen readers should skip | `<i class="bi bi-star" aria-hidden="true">` |
| `role="..."` | When semantic HTML isn't enough | `role="alert"` for notifications |
| `for="inputId"` | `<label>` elements | `<label for="email">Email</label>` |
| `tabindex="0"` | Make non-interactive elements focusable | Rarely needed with proper HTML |

### Lighthouse Score Quick Wins

| Fix | Score Improved |
|-----|---------------|
| Add `loading="lazy"` to images | Performance |
| Add `alt` to all images | Accessibility |
| Add `<meta name="description">` | SEO |
| Add `lang="en"` to `<html>` | Accessibility |
| Fix heading hierarchy | Accessibility, SEO |
| Add `rel="noopener"` to external links | Best Practices |
| Ensure color contrast 4.5:1 | Accessibility |

---

## 📝 Key Takeaways

1. **Testing is not optional.** Professional developers spend as much time testing as building. A beautiful website that breaks on mobile is a broken website.

2. **Chrome DevTools is your best friend.** The device toolbar (`Ctrl + Shift + M`) lets you test every screen size without owning 10 different devices.

3. **Accessibility is for everyone.** Alt text, ARIA labels, and keyboard support helps screen readers, search engines, and users on slow connections — and makes YOU a better developer.

4. **Lighthouse gives you a roadmap.** Don't guess what to fix — run an audit. Always test on Mobile mode (it's stricter).

5. **Validate early, validate often.** One missing `</div>` can cascade into layout bugs. The W3C validator catches these instantly.

6. **Frames are dead, long live CSS Grid.** `<frameset>` and `<frame>` were deprecated (accessibility, SEO, mobile issues). Modern layout uses CSS Grid and Bootstrap. But `<iframe>` survives for embedding external content.

7. **Clean code is maintainable code.** Future-you will thank present-you for consistent indentation, meaningful comments, and removed debug logs.

---

## 🏋️ Practice Challenges

### Challenge 1: Achieve 90+ on All Lighthouse Scores (⭐⭐ Medium)

Run Lighthouse on mobile mode. Your goal: **90 or above on all four categories**. Work through each recommendation Lighthouse gives you until all four scores are green.

**Hints:**
- Performance: Add `loading="lazy"` to all images below the hero section
- Accessibility: Fix every item listed under the Accessibility section
- SEO: Ensure `<meta name="description">`, `lang="en"`, and proper heading hierarchy
- Best Practices: Add `rel="noopener noreferrer"` to all `target="_blank"` links

### Challenge 2: Add a Skip-to-Content Link (⭐⭐ Medium)

Screen reader users shouldn't have to Tab through 10 navbar links every time they visit a page. Add a **skip link** that appears only on focus:

```html
<!-- Add as the VERY FIRST element inside <body> -->
<a href="#main-content" class="skip-link">Skip to main content</a>

<!-- Add id to your <main> element -->
<main id="main-content">
```

```css
/* Add to custom.css */
.skip-link {
    position: absolute;
    top: -40px;
    left: 0;
    background: #0d6efd;
    color: white;
    padding: 8px 16px;
    z-index: 9999;
    transition: top 0.3s;
}

.skip-link:focus {
    top: 0;
}
```

> 💡 This link is invisible until a keyboard user presses Tab. It then appears at the top of the page, letting them jump straight to the content.

### Challenge 3: Add a Print Stylesheet (⭐⭐⭐ Hard)

When someone prints your website (`Ctrl + P`), it should look clean:

```css
/* Add to custom.css */
@media print {
    nav, .back-to-top, #darkModeToggle,
    .carousel-control-prev, .carousel-control-next,
    footer, .btn { display: none !important; }

    body { color: #000 !important; background: #fff !important; }
    a[href]::after { content: " (" attr(href) ")"; font-size: 0.8em; }
    .card { box-shadow: none !important; border: 1px solid #ccc; }
    .card, section { break-inside: avoid; }
}
```

> 💡 Test with `Ctrl + P` — buttons, navigation, and dark mode toggle should disappear in print preview!

---

## 🔗 Labs Covered in This Session

| Lab # | Experiment Description | How We Covered It |
|-------|----------------------|-------------------|
| **Lab 22** | Responsive design testing across devices | ✅ Tested at 6 breakpoints using Chrome DevTools, fixed responsive issues, ran Lighthouse audits, tested keyboard navigation and accessibility |
| **Lab 8** | HTML frames and framesets | ✅ Explained `<frameset>`, `<frame>`, `<iframe>` — why frames were deprecated, modern replacements, and why `<iframe>` still exists |

---

## ⏭️ Next Session Preview

### Session 15: "Ship It!" — Final Polish + Deployment

In our **final session**, we'll deploy the website to the real internet:

- 🚀 **GitHub Pages** — Free hosting, live on the internet
- 📦 **Git basics** — `git init`, `git add`, `git commit`, `git push`
- 🌐 **Custom domain** concepts — How `bca2025.github.io` works
- 🎨 **Final polish** — Favicon, Open Graph tags for social sharing
- 🎓 **Course recap** — Everything we've learned across 15 sessions

> 🎉 **By the end of Session 15**, your class website will be LIVE. You'll have a real URL to share with family and friends!

---

*Session 14 of 15 — Crash Course: Bootstrap + JavaScript — BCA Semester II, Mandsaur University, 2025-26*
