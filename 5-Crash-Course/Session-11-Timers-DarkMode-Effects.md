# Session 11: "Make It Alive" — Timers, Countdown, Dark Mode & Dynamic Effects

**BCA Semester II | Mandsaur University | Web Technology (25BCA060)**

> **Session 11 of 15** | ⏱️ Duration: 2 hours  
> **Labs Covered:** Lab 18 (JS alert on page load), Lab 19 (JS background color timer), Lab 4 (Background color + anchor to top), Lab 20 (JS dynamic styling)  
> **JavaScript Style:** ES6+ — `let`, `const`, `` `template ${literals}` ``, `addEventListener`

---

## 🎯 What We'll Build Today

Our class website already has a navbar, hero carousel, about section, faculty cards, timetable, gallery, contact form, login system, and admin messages. Today we **bring it to life** — adding things that move, change, and react on their own. Think of it like giving a heartbeat to your website. Until now everything waited for a user click — today the page starts doing things **by itself**.

**By the end of this session, you'll have:**

- ✅ A live **countdown timer** to semester exams (updates every second!)
- ✅ A **dark mode toggle** — sun/moon button that switches the entire page theme
- ✅ A **back-to-top floating button** that appears when you scroll down
- ✅ A **welcome toast notification** on first visit (like a phone notification)
- ✅ An **auto-changing background color** demo (changes every 5 seconds)
- ✅ A proper **footer** with university info, quick links, and social media icons
- ✅ **Bootstrap Icons** integrated across the page

**What the new features look like:**

```
┌─────────────────────────────────────────────────────────┐
│  [Navbar]                          [🌙 Dark Mode] [Login]│
├─────────────────────────────────────────────────────────┤
│                                                         │
│           ⏱️ Days Until Semester Exam                    │
│        45 days  12 hrs  34 min  56 sec                  │
│                                                         │
│  ... (hero, about, faculty, timetable, gallery, etc.)   │
│                                                         │
│  🎨 [Start Color Change Demo]                           │
│                                                         │
├─────────────────────────────────────────────────────────┤
│  FOOTER                                                 │
│  About MU  |  Quick Links  |  Connect With Us           │
│  📍 Address |  Home         |  📘 Facebook               │
│  📞 Phone   |  Faculty      |  📸 Instagram              │
│  ✉️ Email   |  Timetable    |  🐦 Twitter                │
│─────────────────────────────────────────────────────────│
│  © 2025-26 BCA Department, Mandsaur University          │
└─────────────────────────────────────────────────────────┘

          [🔝 Back to Top]  ← floating, appears on scroll

┌──── Toast (bottom-right) ────┐
│ 👋 Welcome!           ✕ │
│ Welcome to BCA 2025-26       │
│ class website!               │
└──────────────────────────────┘
```

---

## 📌 New HTML Tags & Concepts

Every session we learn new HTML elements. Here are today's **first-time tags:**

| Tag | What It Does | Analogy |
|-----|-------------|---------|
| 📌 `<footer>` | Semantic footer section at page bottom | Like the last page of a textbook — copyright, publisher, contact info |
| 📌 `<small>` | Renders text in a smaller size | Like the fine print at the bottom of a contract |
| 📌 `<time datetime="...">` | Semantic time/date element (machines can read the `datetime`) | Like a stamp on a letter — humans see "25 May 2026", computers read `2026-05-25` |
| 📌 `<hr>` | Horizontal rule — a visible divider line | Like the line between sections on an exam paper |
| 📌 `<i class="bi bi-sun">` | Bootstrap Icon element (NOT italic!) | Like an emoji, but from a font library — scalable and customizable |

> ⚠️ **The `<i>` tag confusion:** Originally `<i>` meant *italic text*. But in modern web development, `<i>` is reused for **icons** (Bootstrap Icons, Font Awesome). When you see `<i class="bi bi-sun"></i>`, that's an **icon**, not italic text. For actual italic text, use `<em>` (emphasis) instead.

---

## 📖 Bootstrap Icons — Your Icon Library

### What Are Bootstrap Icons?

Bootstrap Icons is a **free icon library** made by the Bootstrap team. It gives you 2,000+ icons that you can use anywhere on your page — buttons, navigation, footers, anywhere you need a small picture.

🎒 **Analogy:** Think of it like a sticker book. Instead of drawing every small icon by hand, you pick a sticker from the book and paste it. The sticker automatically matches the size and color of the text around it.

### Setup — Add the CDN Link

Add this line in your `<head>`, right after the Bootstrap CSS link:

```html
<!-- Bootstrap Icons CDN -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.min.css">
```

📌 **How it works:** This loads a special font file where each "letter" is actually an icon. When you write `<i class="bi bi-sun"></i>`, the browser looks up the "sun" character from this font and displays it as a ☀️ icon.

### Using Icons

```html
<!-- Basic usage -->
<i class="bi bi-sun-fill"></i>          <!-- Filled sun -->
<i class="bi bi-moon-fill"></i>         <!-- Filled moon -->
<i class="bi bi-arrow-up"></i>          <!-- Up arrow -->

<!-- Inside a button -->
<button class="btn btn-dark">
    <i class="bi bi-moon-fill"></i> Dark Mode
</button>

<!-- With custom size (just change font-size) -->
<i class="bi bi-facebook" style="font-size: 1.5rem;"></i>
```

### Icons We'll Use Today

| Icon Class | Looks Like | Where We'll Use It |
|-----------|-----------|-------------------|
| `bi bi-sun-fill` | ☀️ | Dark mode button (light theme) |
| `bi bi-moon-fill` | 🌙 | Dark mode button (dark theme) |
| `bi bi-arrow-up` | ⬆️ | Back-to-top button |
| `bi bi-facebook` | 📘 | Footer social links |
| `bi bi-instagram` | 📸 | Footer social links |
| `bi bi-twitter-x` | 🐦 | Footer social links |
| `bi bi-envelope-fill` | ✉️ | Footer contact info |
| `bi bi-telephone-fill` | 📞 | Footer contact info |
| `bi bi-geo-alt-fill` | 📍 | Footer address |
| `bi bi-clock` | 🕐 | Countdown section |
| `bi bi-palette` | 🎨 | Color change demo button |

---

## 📖 Bootstrap Toast — Phone-Style Notifications

### What Is a Toast?

📱 **Analogy:** You know those notifications that slide in on your phone — "New message from Rahul" — and disappear after a few seconds? That's exactly what a Bootstrap Toast is. It **pops up** briefly to show a message, then **fades away** on its own.

### Toast Structure

```html
<!-- Toast container (positioned fixed at bottom-right) -->
<div class="position-fixed bottom-0 end-0 p-3" style="z-index: 1080;">
    <div id="welcomeToast" class="toast" role="alert">
        <div class="toast-header bg-success text-white">
            <strong class="me-auto">👋 Welcome!</strong>
            <button type="button" class="btn-close btn-close-white" data-bs-dismiss="toast"></button>
        </div>
        <div class="toast-body">
            Welcome to BCA Batch 2025-26 class website! 🎓
        </div>
    </div>
</div>
```

📌 **`position-fixed bottom-0 end-0 p-3`** — This pins the toast to the **bottom-right corner** of the screen. `position-fixed` means it stays there even when you scroll. `z-index: 1080` ensures it appears above everything else.

📌 **`role="alert"`** — Tells screen readers "Hey, this is an important notification!" — accessibility matters!

📌 **`data-bs-dismiss="toast"`** — The close button. When clicked, Bootstrap automatically hides the toast. No JavaScript needed for the close action.

### Showing a Toast with JavaScript

Unlike most Bootstrap components, toasts **don't show automatically**. You must trigger them:

```javascript
const toastElement = document.getElementById('welcomeToast');
const toast = new bootstrap.Toast(toastElement);
toast.show();
```

---

## 📖 Bootstrap Tooltip — Hover Hints

### What Is a Tooltip?

💬 **Analogy:** When you hover over an icon on your phone and a small text bubble appears explaining what it does — that's a tooltip. It's a tiny **hint** that appears on hover.

### Setup

Add `data-bs-toggle="tooltip"` and `title="..."` to any element:

```html
<button class="btn btn-dark" data-bs-toggle="tooltip" title="Switch between light and dark theme">
    <i class="bi bi-moon-fill"></i>
</button>
```

### Initialize All Tooltips (JavaScript)

Tooltips need one line of initialization to work. Add this to your JavaScript:

```javascript
// Initialize all tooltips on the page
const tooltipTriggerList = document.querySelectorAll('[data-bs-toggle="tooltip"]');
tooltipTriggerList.forEach(el => new bootstrap.Tooltip(el));
```

📌 **Why manual initialization?** Bootstrap doesn't auto-initialize tooltips because they're expensive — each one creates a hidden `<div>`. By requiring manual init, Bootstrap lets you control when and where they appear.

---

## 📖 JavaScript `setTimeout` — "Do This After X Seconds"

### The Concept

⏰ **Analogy:** Imagine you tell your friend: *"5 minute baad mujhe yaad dila dena"* (Remind me after 5 minutes). Your friend waits, and after exactly 5 minutes, reminds you. That's `setTimeout` — it runs a piece of code **once** after a specified delay.

### Syntax

```javascript
setTimeout(function() {
    // This code runs ONCE after the delay
    console.log('5 seconds have passed!');
}, 5000);  // 5000 milliseconds = 5 seconds
```

📌 **Milliseconds, not seconds!** JavaScript timers use **milliseconds**:
- 1000 ms = 1 second
- 2000 ms = 2 seconds
- 5000 ms = 5 seconds

### Real-World Use Cases

| Use Case | Delay | Code |
|----------|-------|------|
| Show welcome toast after page loads | 2 seconds | `setTimeout(() => toast.show(), 2000)` |
| Auto-hide a success message | 3 seconds | `setTimeout(() => msg.style.display = 'none', 3000)` |
| Redirect after form submission | 2 seconds | `setTimeout(() => window.location = 'home.html', 2000)` |

### Cancelling a Timeout

```javascript
const timerId = setTimeout(function() {
    alert('This will NOT run if cancelled!');
}, 5000);

// Changed your mind? Cancel it:
clearTimeout(timerId);
```

📌 **`clearTimeout(timerId)`** — Stops the timer before it fires. Think of it like cancelling the reminder you set on your phone.

---

## 📖 JavaScript `setInterval` — "Do This Every X Seconds"

### The Concept

🔁 **Analogy:** If `setTimeout` is *"remind me once after 5 minutes"*, then `setInterval` is *"remind me every 5 minutes, again and again, until I tell you to stop"*. It's like a repeating alarm — the code runs **over and over** at regular intervals.

### Syntax

```javascript
const intervalId = setInterval(function() {
    // This code runs REPEATEDLY every 1000ms
    console.log('One second passed!');
}, 1000);
```

### Stopping the Interval

```javascript
// Stop the repeating timer
clearInterval(intervalId);
```

⚠️ **Always save the return value!** If you don't save `intervalId`, you can never stop the interval. It will keep running forever (until the page is closed).

### setTimeout vs setInterval — Comparison

| Feature | `setTimeout` | `setInterval` |
|---------|-------------|--------------|
| How many times? | **Once** | **Repeats forever** (until cleared) |
| Analogy | "Wake me up at 7 AM tomorrow" | "Wake me up at 7 AM every day" |
| Stop with | `clearTimeout(id)` | `clearInterval(id)` |
| Returns | Timer ID (number) | Timer ID (number) |
| Use case | Show toast once, redirect | Countdown, clock, slideshow |

### Common Pattern: Run Immediately + Repeat

```javascript
function doSomething() {
    console.log('Tick!');
}

// Problem: setInterval waits before the FIRST run
setInterval(doSomething, 1000);  // First "Tick!" after 1 second

// Solution: Call it once manually, THEN start the interval
doSomething();                    // First "Tick!" immediately
setInterval(doSomething, 1000);   // Then every 1 second after
```

---

## 📖 Countdown Timer Logic — Date Math

### How Does a Countdown Work?

🧮 **Analogy:** You know when you check "How many days until Diwali?" on Google? The logic is simple: **Future Date − Today = Time Remaining**. Then we break that remaining time into days, hours, minutes, and seconds.

### JavaScript Date Object

```javascript
// Create a future date (exam date)
const examDate = new Date('2026-05-25T09:00:00');

// Get current date/time
const now = new Date();

// Difference in milliseconds
const diff = examDate - now;  // e.g., 31536000000 ms
```

📌 **`new Date('2026-05-25T09:00:00')`** — Creates a date object for May 25, 2026 at 9:00 AM. The `T` separates date from time. This is the ISO 8601 format — works in every browser.

### Breaking Milliseconds into Days/Hours/Minutes/Seconds

```javascript
// 1 second  = 1000 ms
// 1 minute  = 60 × 1000 = 60,000 ms
// 1 hour    = 60 × 60 × 1000 = 3,600,000 ms
// 1 day     = 24 × 60 × 60 × 1000 = 86,400,000 ms

const days    = Math.floor(diff / (1000 * 60 * 60 * 24));
const hours   = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
const seconds = Math.floor((diff % (1000 * 60)) / 1000);
```

📌 **`Math.floor()`** — Rounds DOWN to the nearest whole number. `Math.floor(3.7)` = `3`. We don't want "3.7 days" — we want "3 days".

📌 **`%` (modulo/remainder)** — Returns the leftover after division. `10 % 3 = 1` (because 10 ÷ 3 = 3 remainder 1). We use it to get the "remaining hours after counting full days," then "remaining minutes after counting full hours," etc.

---

## 📖 Dark Mode — Toggle Themes

### How Dark Mode Works

🌗 **Analogy:** Think of dark mode like a light switch in a room. One click → lights off (dark). Another click → lights on (light). The room (page) is the same — only the **appearance** changes.

**The technique:**
1. Write CSS rules for dark mode inside a `.dark-mode` class
2. Toggle that class on `<body>` with JavaScript
3. When `<body>` has `class="dark-mode"`, the dark CSS rules activate
4. When the class is removed, the page reverts to normal Bootstrap styles

### `classList.toggle()` — The Light Switch

```javascript
document.body.classList.toggle('dark-mode');
// If body HAS 'dark-mode'    → REMOVES it (light mode)
// If body DOESN'T have it    → ADDS it (dark mode)
```

📌 **`classList.toggle()`** is the most elegant way to flip a class on/off. No `if/else` needed — it handles both directions in one call.

### Saving User Preference

Nobody wants to toggle dark mode on every page refresh! We save the choice in `localStorage`:

```javascript
// Save: 'on' or 'off'
localStorage.setItem('darkMode', isDark ? 'on' : 'off');

// Load on page start
if (localStorage.getItem('darkMode') === 'on') {
    document.body.classList.add('dark-mode');
}
```

---

## 📖 `sessionStorage` vs `localStorage`

We already know `localStorage` from Session 10. Now meet its sibling:

| Feature | `localStorage` | `sessionStorage` |
|---------|---------------|-----------------|
| Data lifespan | **Forever** (until you clear it) | **Until the tab is closed** |
| Analogy | Writing in a **notebook** — stays until you tear the page | Writing on a **whiteboard** — erased when you leave the room |
| Shared between tabs? | ✅ Yes | ❌ No (each tab has its own) |
| Use case | Dark mode preference, login data | "Show welcome toast only once per visit" |
| Syntax | `localStorage.setItem(key, value)` | `sessionStorage.setItem(key, value)` |

### Why sessionStorage for the Welcome Toast?

We want the toast to show **once per visit**. If the user refreshes the page, we don't show it again. But if they close the tab and come back later, we show it again (it's a "new visit"). That's exactly what `sessionStorage` does!

```javascript
if (!sessionStorage.getItem('welcomed')) {
    // First visit this session — show toast
    setTimeout(() => toast.show(), 2000);
    sessionStorage.setItem('welcomed', 'true');
}
```

---

## 🔨 Let's Build! — Step by Step

### Where Does Everything Go?

```
<head>
    ... existing CSS links ...
    + Bootstrap Icons CDN link          ← Step 1
    + <style> block for dark mode CSS   ← Step 3
</head>
<body>
    [Navbar]                            (add dark mode toggle button — Step 2)
    [Hero Carousel]
    [Countdown Timer Section]           ← Step 4 (NEW)
    [About Section]
    [Faculty Cards]
    [Timetable]
    [Gallery]
    [Contact Form]
    [Login Modal]
    [Admin Messages]
    [Color Change Demo]                 ← Step 7 (NEW)
    [Footer]                            ← Step 5 (NEW)
    [Welcome Toast HTML]                ← Step 6 (NEW)
    [Back-to-Top Button]                ← Step 8 (NEW)

    <script>
        ... existing JavaScript ...
        + All new JavaScript             ← Step 9
    </script>
</body>
```

---

### Step 1: Add Bootstrap Icons CDN

Add this line in your `<head>` section, right after the Bootstrap CSS link:

```html
<head>
    <!-- ... existing meta tags and title ... -->

    <!-- Bootstrap CSS (already there) -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">

    <!-- Bootstrap Icons CDN (NEW) -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.min.css">
</head>
```

📌 **Order matters:** Icons CSS should come **after** Bootstrap CSS so it can use Bootstrap's base styles.

---

### Step 2: Add Dark Mode Toggle to Navbar

Inside your existing `<nav>`, add a dark mode button next to the login button:

```html
<!-- Inside the navbar, before or after the Login button -->
<div class="d-flex align-items-center gap-2">
    <button class="btn btn-outline-light btn-sm" id="darkModeBtn"
            data-bs-toggle="tooltip" title="Toggle Dark Mode"
            onclick="toggleDarkMode()">
        <i id="darkModeIcon" class="bi bi-moon-fill"></i>
    </button>
    <!-- Your existing Login button stays here -->
</div>
```

📌 **`btn-outline-light`** — A bordered button that works well against a dark navbar background.

📌 **`gap-2`** — Bootstrap utility for adding spacing between flex items. Think of it like automatic margin between siblings.

📌 **`id="darkModeIcon"`** — We give the icon an id so JavaScript can swap it between sun ☀️ and moon 🌙 when toggling.

---

### Step 3: Add Dark Mode CSS

Add this `<style>` block inside your `<head>`, after the Bootstrap Icons CDN link:

```html
<style>
    /* ============================================
       DARK MODE STYLES (Session 11)
       These rules ONLY activate when <body> has
       the class "dark-mode"
       ============================================ */

    /* Base dark mode — background and text */
    .dark-mode {
        background-color: #1a1a2e;
        color: #e0e0e0;
        transition: background-color 0.3s ease, color 0.3s ease;
    }

    /* Navbar */
    .dark-mode .navbar {
        background-color: #16213e !important;
    }

    /* Cards */
    .dark-mode .card {
        background-color: #0f3460;
        color: #e0e0e0;
        border-color: #1a3a6b;
    }

    /* Sections with bg-light */
    .dark-mode .bg-light {
        background-color: #16213e !important;
        color: #e0e0e0;
    }

    /* Tables */
    .dark-mode .table {
        color: #e0e0e0;
    }
    .dark-mode .table-bordered {
        border-color: #1a3a6b;
    }

    /* Form inputs */
    .dark-mode .form-control,
    .dark-mode .form-select {
        background-color: #0f3460;
        color: #e0e0e0;
        border-color: #1a3a6b;
    }

    /* Modal */
    .dark-mode .modal-content {
        background-color: #16213e;
        color: #e0e0e0;
    }

    /* Footer stays dark always, but adjust border */
    .dark-mode footer {
        border-top: 1px solid #1a3a6b;
    }

    /* Carousel caption readability */
    .dark-mode .carousel-caption {
        background-color: rgba(0, 0, 0, 0.7);
    }

    /* Back-to-top button */
    #backToTop {
        display: none;
        position: fixed;
        bottom: 30px;
        right: 30px;
        z-index: 1070;
        width: 45px;
        height: 45px;
        border-radius: 50%;
        font-size: 1.2rem;
        box-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
    }

    /* Countdown number highlight */
    .countdown-number {
        font-size: 2.5rem;
        font-weight: 700;
        color: #0d6efd;
    }
    .dark-mode .countdown-number {
        color: #6ea8fe;
    }
    .countdown-label {
        font-size: 0.9rem;
        text-transform: uppercase;
        letter-spacing: 1px;
    }
</style>
```

📌 **`transition: background-color 0.3s ease`** — This makes the dark mode switch **smooth** instead of instant. The colors fade over 0.3 seconds. Try it without the transition and you'll see the harsh jump!

📌 **`!important`** — We use this sparingly because Bootstrap's own styles are very specific. Without `!important`, our dark overrides might lose the CSS specificity battle. Rule of thumb: avoid `!important` unless overriding a framework.

---

### Step 4: Add Countdown Timer Section

Place this after the Hero Carousel and before the About section:

```html
<!-- ============================================
     COUNTDOWN TIMER SECTION (Session 11)
     Labs: 18, 19
     ============================================ -->
<section id="countdown-section" class="py-4 bg-light">
    <div class="container text-center">
        <h3 class="mb-3">
            <i class="bi bi-clock"></i> Days Until Semester Exam
        </h3>
        <p class="text-muted mb-2">
            Exam Date: <time datetime="2026-05-25">25 May 2026</time>
        </p>
        <div id="countdown" class="d-flex justify-content-center gap-3 gap-md-4 flex-wrap">
            <div>
                <span class="countdown-number" id="countDays">--</span>
                <div class="countdown-label">Days</div>
            </div>
            <div>
                <span class="countdown-number" id="countHours">--</span>
                <div class="countdown-label">Hours</div>
            </div>
            <div>
                <span class="countdown-number" id="countMinutes">--</span>
                <div class="countdown-label">Minutes</div>
            </div>
            <div>
                <span class="countdown-number" id="countSeconds">--</span>
                <div class="countdown-label">Seconds</div>
            </div>
        </div>
    </div>
</section>
```

📌 **`<time datetime="2026-05-25">`** — The `<time>` tag tells search engines and screen readers that this text is a date. The `datetime` attribute gives the machine-readable format. Humans see "25 May 2026"; Google sees `2026-05-25`.

📌 **`d-flex justify-content-center gap-3 flex-wrap`** — A flexbox row that centers the countdown boxes, adds spacing between them, and wraps on small screens. This makes the countdown responsive without a grid.

📌 **`id="countDays"`, `id="countHours"`, etc.** — Each number has its own id so JavaScript can update them individually every second.

---

### Step 5: Add the Footer

Place this after the Admin Messages section (and the Color Change Demo), just before the closing `</body>` tag area:

```html
<!-- ============================================
     FOOTER SECTION (Session 11)
     Lab: 4 (background + anchor)
     ============================================ -->
<footer class="bg-dark text-light pt-5 pb-3 mt-5">
    <div class="container">
        <div class="row g-4">
            <!-- Column 1: About -->
            <div class="col-md-4">
                <h5><i class="bi bi-mortarboard-fill"></i> BCA Department</h5>
                <p class="text-secondary">
                    <small>Department of Computer Applications, Mandsaur University, 
                    preparing future tech leaders since establishment.</small>
                </p>
                <ul class="list-unstyled">
                    <li class="mb-1">
                        <i class="bi bi-geo-alt-fill text-info"></i>
                        <small> Mandsaur University, Mandsaur, M.P. 458001</small>
                    </li>
                    <li class="mb-1">
                        <i class="bi bi-telephone-fill text-info"></i>
                        <small> +91 07422-274141</small>
                    </li>
                    <li class="mb-1">
                        <i class="bi bi-envelope-fill text-info"></i>
                        <small> bca@mfrsu.ac.in</small>
                    </li>
                </ul>
            </div>

            <!-- Column 2: Quick Links -->
            <div class="col-md-4">
                <h5><i class="bi bi-link-45deg"></i> Quick Links</h5>
                <ul class="list-unstyled">
                    <li class="mb-1"><a href="#home" class="text-secondary text-decoration-none">
                        <i class="bi bi-chevron-right"></i> Home</a></li>
                    <li class="mb-1"><a href="#about" class="text-secondary text-decoration-none">
                        <i class="bi bi-chevron-right"></i> About</a></li>
                    <li class="mb-1"><a href="#faculty" class="text-secondary text-decoration-none">
                        <i class="bi bi-chevron-right"></i> Faculty</a></li>
                    <li class="mb-1"><a href="#timetable" class="text-secondary text-decoration-none">
                        <i class="bi bi-chevron-right"></i> Timetable</a></li>
                    <li class="mb-1"><a href="#gallery" class="text-secondary text-decoration-none">
                        <i class="bi bi-chevron-right"></i> Gallery</a></li>
                    <li class="mb-1"><a href="#contact" class="text-secondary text-decoration-none">
                        <i class="bi bi-chevron-right"></i> Contact</a></li>
                </ul>
            </div>

            <!-- Column 3: Connect -->
            <div class="col-md-4">
                <h5><i class="bi bi-people-fill"></i> Connect With Us</h5>
                <p class="text-secondary"><small>Follow us on social media for updates:</small></p>
                <div class="d-flex gap-3 fs-4">
                    <a href="#" class="text-info"><i class="bi bi-facebook"></i></a>
                    <a href="#" class="text-info"><i class="bi bi-instagram"></i></a>
                    <a href="#" class="text-info"><i class="bi bi-twitter-x"></i></a>
                    <a href="#" class="text-info"><i class="bi bi-youtube"></i></a>
                    <a href="#" class="text-info"><i class="bi bi-linkedin"></i></a>
                </div>
                <p class="text-secondary mt-3">
                    <small>Batch: 2025-26 | Semester: II</small>
                </p>
            </div>
        </div>

        <hr class="border-secondary my-3">

        <div class="text-center">
            <small class="text-secondary">
                &copy; 2025-26 BCA Department, Mandsaur University. Built with 
                <i class="bi bi-heart-fill text-danger"></i> by BCA Students.
            </small>
        </div>
    </div>
</footer>
```

📌 **`<footer>`** — A **semantic HTML5** element. It tells the browser: "This is the footer of the page." Using `<footer>` instead of `<div class="footer">` is better for accessibility and SEO. Screen readers announce it as a footer landmark.

📌 **`<small>`** — Renders text in a smaller font size. Perfect for copyright notices, disclaimers, and fine print. It's semantic — it tells the browser this text is secondary/supplementary.

📌 **`<hr class="border-secondary">`** — A horizontal rule (divider line). We style it with `border-secondary` to make it subtle on the dark background.

📌 **`list-unstyled`** — Bootstrap class that removes bullet points and left padding from `<ul>`. Perfect for navigation lists that don't need traditional bullets.

📌 **`&copy;`** — HTML entity for the © copyright symbol. Some common entities: `&amp;` = &, `&lt;` = <, `&gt;` = >, `&nbsp;` = non-breaking space.

---

### Step 6: Add Welcome Toast HTML

Place this just before the footer (or just before the `</body>` close):

```html
<!-- ============================================
     WELCOME TOAST (Session 11)
     Lab: 18 (JS alert on page load)
     ============================================ -->
<div class="position-fixed bottom-0 end-0 p-3" style="z-index: 1080;">
    <div id="welcomeToast" class="toast" role="alert" aria-live="assertive" aria-atomic="true">
        <div class="toast-header bg-primary text-white">
            <i class="bi bi-mortarboard-fill me-2"></i>
            <strong class="me-auto">👋 Welcome!</strong>
            <small class="text-light">just now</small>
            <button type="button" class="btn-close btn-close-white ms-2" data-bs-dismiss="toast"></button>
        </div>
        <div class="toast-body">
            Welcome to <strong>BCA Batch 2025-26</strong> class website! 🎓
            Explore our timetable, gallery, and more.
        </div>
    </div>
</div>
```

📌 **`aria-live="assertive"`** — Accessibility attribute. Tells screen readers to immediately announce this toast when it appears. `"assertive"` means interrupt whatever is being read; `"polite"` would wait.

---

### Step 7: Add Color Change Demo Button

Place this in a small section before the footer (after admin messages):

```html
<!-- ============================================
     BACKGROUND COLOR CHANGE DEMO (Session 11)
     Lab: 19 (JS background color timer)
     ============================================ -->
<section id="color-demo" class="py-4 text-center">
    <div class="container">
        <h4><i class="bi bi-palette"></i> Background Color Auto-Change Demo</h4>
        <p class="text-muted">Click the button to start — background changes every 5 seconds!</p>
        <button class="btn btn-warning btn-lg" id="colorChangeBtn" onclick="startColorChange()">
            <i class="bi bi-play-fill"></i> Start Color Change
        </button>
        <button class="btn btn-outline-secondary btn-lg ms-2" id="colorStopBtn" 
                onclick="stopColorChange()" style="display: none;">
            <i class="bi bi-stop-fill"></i> Stop
        </button>
        <p class="mt-2"><small class="text-muted" id="colorStatus"></small></p>
    </div>
</section>
```

---

### Step 8: Add Back-to-Top Button

Place this just before the closing `</body>` tag (it's a floating element):

```html
<!-- ============================================
     BACK TO TOP BUTTON (Session 11)
     Lab: 4 (anchor to top of page)
     ============================================ -->
<button id="backToTop" class="btn btn-primary" 
        data-bs-toggle="tooltip" title="Back to Top">
    <i class="bi bi-arrow-up"></i>
</button>
```

📌 **No wrapper needed!** The CSS we wrote in Step 3 already handles `position: fixed`, `bottom: 30px`, `right: 30px`, and `display: none`. The JavaScript will toggle its visibility based on scroll position.

---

### Step 9: Add All JavaScript

Add this entire block inside your `<script>` tag, after any existing JavaScript from previous sessions:

```javascript
// ============================================
// SESSION 11: TIMERS, DARK MODE & EFFECTS
// Labs: 18, 19, 4, 20
// ============================================


// -----------------------------------------
// 1. INITIALIZE TOOLTIPS
// Purpose: Activate all Bootstrap tooltips on the page
// -----------------------------------------
const tooltipTriggerList = document.querySelectorAll('[data-bs-toggle="tooltip"]');
tooltipTriggerList.forEach(el => new bootstrap.Tooltip(el));


// -----------------------------------------
// 2. COUNTDOWN TIMER
// Purpose: Show time remaining until semester exam
// Concept: setInterval runs every 1000ms (1 second)
// -----------------------------------------
const examDate = new Date('2026-05-25T09:00:00');

function updateCountdown() {
    const now = new Date();
    const diff = examDate - now;  // difference in milliseconds

    // If exam date has passed, show a message and stop
    if (diff <= 0) {
        document.getElementById('countDays').textContent = '0';
        document.getElementById('countHours').textContent = '0';
        document.getElementById('countMinutes').textContent = '0';
        document.getElementById('countSeconds').textContent = '0';
        clearInterval(countdownTimer);
        return;
    }

    // Break milliseconds into days, hours, minutes, seconds
    const days = Math.floor(diff / (1000 * 60 * 60 * 24));
    const hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
    const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
    const seconds = Math.floor((diff % (1000 * 60)) / 1000);

    // Update each element
    document.getElementById('countDays').textContent = days;
    document.getElementById('countHours').textContent = hours;
    document.getElementById('countMinutes').textContent = minutes;
    document.getElementById('countSeconds').textContent = seconds;
}

// Run immediately, then every second
updateCountdown();
const countdownTimer = setInterval(updateCountdown, 1000);


// -----------------------------------------
// 3. DARK MODE TOGGLE
// Purpose: Switch between light and dark themes
// Concept: classList.toggle + localStorage
// -----------------------------------------
function toggleDarkMode() {
    // Toggle the dark-mode class on <body>
    document.body.classList.toggle('dark-mode');

    // Update the icon (sun ↔ moon)
    const icon = document.getElementById('darkModeIcon');
    const isDark = document.body.classList.contains('dark-mode');
    icon.className = isDark ? 'bi bi-sun-fill' : 'bi bi-moon-fill';

    // Save preference to localStorage
    localStorage.setItem('darkMode', isDark ? 'on' : 'off');
}

// Check saved preference on page load
if (localStorage.getItem('darkMode') === 'on') {
    document.body.classList.add('dark-mode');
    // Also update the icon to sun (since we're in dark mode)
    const icon = document.getElementById('darkModeIcon');
    if (icon) {
        icon.className = 'bi bi-sun-fill';
    }
}


// -----------------------------------------
// 4. BACK TO TOP BUTTON
// Purpose: Show/hide a floating button based on scroll
// Concept: window scroll event + smooth scrolling
// -----------------------------------------
window.addEventListener('scroll', function () {
    const btn = document.getElementById('backToTop');
    if (window.scrollY > 300) {
        btn.style.display = 'block';
    } else {
        btn.style.display = 'none';
    }
});

document.getElementById('backToTop').addEventListener('click', function () {
    window.scrollTo({ top: 0, behavior: 'smooth' });
});


// -----------------------------------------
// 5. WELCOME TOAST (shows once per visit)
// Purpose: Greet user on first page load
// Concept: sessionStorage + setTimeout
// -----------------------------------------
const toastElement = document.getElementById('welcomeToast');
const welcomeToast = new bootstrap.Toast(toastElement, { delay: 5000 });

if (!sessionStorage.getItem('welcomed')) {
    // First visit in this session — show toast after 2 seconds
    setTimeout(function () {
        welcomeToast.show();
    }, 2000);
    sessionStorage.setItem('welcomed', 'true');
}


// -----------------------------------------
// 6. BACKGROUND COLOR AUTO-CHANGE (Lab 19)
// Purpose: Cycle through colors every 5 seconds
// Concept: setInterval + clearInterval + arrays
// -----------------------------------------
const colors = ['#f8d7da', '#d1ecf1', '#d4edda', '#fff3cd', '#e2e3e5'];
const colorNames = ['Rose', 'Sky Blue', 'Mint', 'Sunshine', 'Silver'];
let colorIndex = 0;
let colorIntervalId = null;
let originalBg = '';  // to restore later

function startColorChange() {
    // Save the original background color
    originalBg = document.body.style.backgroundColor;

    // Disable dark mode during demo (would conflict)
    if (document.body.classList.contains('dark-mode')) {
        toggleDarkMode();
    }

    // Apply first color immediately
    document.body.style.backgroundColor = colors[colorIndex];
    document.getElementById('colorStatus').textContent =
        `Current: ${colorNames[colorIndex]}`;

    // Start interval — change every 5 seconds
    colorIntervalId = setInterval(function () {
        colorIndex = (colorIndex + 1) % colors.length;
        document.body.style.backgroundColor = colors[colorIndex];
        document.getElementById('colorStatus').textContent =
            `Current: ${colorNames[colorIndex]}`;
    }, 5000);

    // Show stop button, hide start button
    document.getElementById('colorChangeBtn').style.display = 'none';
    document.getElementById('colorStopBtn').style.display = 'inline-block';
}

function stopColorChange() {
    // Stop the interval
    clearInterval(colorIntervalId);
    colorIntervalId = null;

    // Restore original background
    document.body.style.backgroundColor = originalBg;
    document.getElementById('colorStatus').textContent = 'Stopped — background restored.';

    // Show start button, hide stop button
    document.getElementById('colorChangeBtn').style.display = 'inline-block';
    document.getElementById('colorStopBtn').style.display = 'none';
}
```

📌 **`const countdownTimer = setInterval(updateCountdown, 1000)`** — We store the interval ID in a `const` because we need it later to call `clearInterval(countdownTimer)` when the exam date arrives.

📌 **`(colorIndex + 1) % colors.length`** — This is the **circular array pattern**. When `colorIndex` reaches 4 (last item), adding 1 gives 5, and `5 % 5 = 0` — wrapping back to the first color. It creates an endless loop through the array.

📌 **`window.addEventListener('scroll', ...)`** — We use `addEventListener` (ES6+ style) instead of `window.onscroll = ...` because `addEventListener` allows **multiple** listeners on the same event. `onscroll` would overwrite any previous listener.

📌 **`window.scrollTo({ top: 0, behavior: 'smooth' })`** — The `behavior: 'smooth'` option makes the page scroll **smoothly** instead of jumping instantly to the top. Much better user experience!

---

## ✅ Checkpoint

Before moving on, verify that everything works:

| # | Check | Expected Result |
|---|-------|----------------|
| 1 | Page loads without errors | Open browser console (F12 → Console tab) — no red errors |
| 2 | Bootstrap Icons visible | You see moon icon in navbar, icons in footer |
| 3 | Countdown timer updates | Numbers change every second (watch the seconds digit) |
| 4 | Countdown shows correct time | Compare with a manual calculation — days should match roughly |
| 5 | Dark mode toggle works | Click moon button → page turns dark; click sun → back to light |
| 6 | Dark mode persists | Toggle dark mode ON, refresh the page — should still be dark |
| 7 | Cards look good in dark mode | Faculty cards should have dark background, light text |
| 8 | Back-to-top button hidden initially | On page load (at top), the button should NOT be visible |
| 9 | Scroll down → button appears | Scroll past ~300px, floating blue circle appears at bottom-right |
| 10 | Click back-to-top → smooth scroll | Click the button → page smoothly scrolls to the top |
| 11 | Welcome toast appears once | On first load, toast pops up after 2 seconds at bottom-right |
| 12 | Toast doesn't repeat | Refresh the page — toast should NOT appear again (same tab) |
| 13 | Close tab, reopen → toast shows again | Close the tab completely, open the page again — toast appears |
| 14 | Color change demo works | Click "Start Color Change" → background changes every 5 seconds |
| 15 | Color change stops | Click "Stop" → background returns to original |
| 16 | Footer is visible | Scroll to bottom — 3-column footer with icons and copyright line |
| 17 | Footer links work | Click "Faculty" in Quick Links → page scrolls to faculty section |
| 18 | Tooltips appear | Hover over the dark mode button — tooltip text appears |

---

## 🔍 Quick Reference

### Bootstrap Classes Used Today

| Class | Category | What It Does |
|-------|----------|-------------|
| `position-fixed` | Position | Fixes element to viewport (stays on scroll) |
| `bottom-0` | Position | Pins to bottom edge |
| `end-0` | Position | Pins to right edge |
| `toast` | Component | Toast notification container |
| `toast-header` | Component | Toast title bar |
| `toast-body` | Component | Toast content area |
| `list-unstyled` | Typography | Removes bullets and padding from `<ul>` |
| `text-secondary` | Color | Muted grey text |
| `text-info` | Color | Teal/cyan text (used for icons) |
| `gap-2`, `gap-3` | Spacing | Gap between flex items |
| `fs-4` | Typography | Font size level 4 (1.5rem) |
| `border-secondary` | Border | Grey border color |
| `btn-outline-light` | Button | Bordered button for dark backgrounds |
| `btn-close-white` | Button | White close icon (for dark headers) |
| `d-flex` | Layout | Enables flexbox |
| `flex-wrap` | Layout | Allows flex items to wrap to next line |
| `justify-content-center` | Layout | Centers flex items horizontally |
| `mt-5`, `pt-5`, `pb-3` | Spacing | Margin-top, padding-top/bottom |
| `g-4` | Grid | Gap between grid columns |

### JavaScript Concepts Used Today

| Concept | Syntax | Purpose |
|---------|--------|---------|
| Set timeout | `setTimeout(fn, ms)` | Run code once after delay |
| Clear timeout | `clearTimeout(id)` | Cancel a pending timeout |
| Set interval | `setInterval(fn, ms)` | Run code repeatedly at intervals |
| Clear interval | `clearInterval(id)` | Stop a repeating interval |
| Date object | `new Date('2026-05-25T09:00:00')` | Create a specific date/time |
| Date difference | `futureDate - new Date()` | Get time difference in ms |
| Math.floor | `Math.floor(3.7)` → `3` | Round down to whole number |
| Modulo | `10 % 3` → `1` | Get remainder after division |
| Toggle class | `element.classList.toggle('name')` | Add class if missing, remove if present |
| Check class | `element.classList.contains('name')` | Returns `true`/`false` |
| Scroll event | `window.addEventListener('scroll', fn)` | Detect page scrolling |
| Scroll position | `window.scrollY` | Current vertical scroll in pixels |
| Smooth scroll | `window.scrollTo({ top: 0, behavior: 'smooth' })` | Animated scroll to position |
| sessionStorage set | `sessionStorage.setItem('key', 'value')` | Store data for this tab session |
| sessionStorage get | `sessionStorage.getItem('key')` | Retrieve session-scoped data |
| Bootstrap Toast | `new bootstrap.Toast(el).show()` | Show a toast notification |
| Bootstrap Tooltip | `new bootstrap.Tooltip(el)` | Initialize a tooltip |
| Template literal | `` `Hello ${name}` `` | String with embedded expressions |

---

## 📝 Key Takeaways

1. **`setTimeout` = once, `setInterval` = repeat.** Both accept a function and a delay in milliseconds. Always save the timer ID so you can cancel it later with `clearTimeout` / `clearInterval`.

2. **Countdown timers are just date math.** Subtract today's date from the target date to get milliseconds, then divide by the right numbers to get days, hours, minutes, seconds. The modulo operator (`%`) gives you the remainder for each unit.

3. **Dark mode is just a CSS class toggle.** Write a `.dark-mode` class with overrides for background, text, and component colors. Use `classList.toggle()` to switch it on/off, and `localStorage` to remember the user's choice.

4. **`sessionStorage` is for temporary data; `localStorage` is for permanent data.** Use `sessionStorage` when you want data to disappear when the tab closes (like "already showed welcome toast"). Use `localStorage` when data should persist (like "dark mode is on").

5. **The `<footer>` tag is semantic HTML.** Just like `<nav>` and `<section>`, using `<footer>` tells browsers and screen readers the purpose of the content. Always prefer semantic tags over generic `<div>` elements.

6. **Bootstrap Icons work like a special font.** Add one CDN link, then use `<i class="bi bi-icon-name">` anywhere. Icons automatically match text size and color — no image files needed!

7. **The scroll listener pattern** — `window.addEventListener('scroll', ...)` with `window.scrollY` — is how every "sticky header," "back-to-top button," and "lazy loading" feature works on the modern web. Master this pattern.

8. **`behavior: 'smooth'` makes everything feel professional.** One word in `window.scrollTo()` transforms a jarring page jump into a smooth animation. Small details like this separate amateur sites from polished ones.

---

## 🏋️ Practice Challenges

Try these on your own to reinforce what you learned:

### Challenge 1: Build a Stopwatch (⭐⭐ Medium)

Add a **stopwatch** to the page with Start, Stop, and Reset buttons:
- Display format: `00:00:00` (minutes : seconds : centiseconds)
- "Start" begins counting up every 10ms
- "Stop" pauses the count
- "Reset" sets it back to `00:00:00`

**Hints:**
- Use `setInterval` with a 10ms delay
- Track total centiseconds in a variable, then convert to mm:ss:cc
- To pad numbers with leading zeros: `` String(num).padStart(2, '0') ``
- The Stop button should call `clearInterval()` but NOT reset the counter variable

### Challenge 2: Typing Effect for Welcome Message (⭐⭐ Medium)

Instead of showing the welcome toast, make a **typing effect** — text that appears one letter at a time, like someone is typing it:

**Message:** "Welcome to BCA Batch 2025-26 Class Website! 🎓"

**Hints:**
- Create a `<p id="typingText"></p>` element somewhere visible
- Use a variable to track the current character index
- Use `setInterval` with ~80ms delay
- Each interval: add one more character from the message string using `message.charAt(index)`
- Stop with `clearInterval` when you reach the end of the string

```javascript
const message = 'Welcome to BCA Batch 2025-26 Class Website! 🎓';
let charIndex = 0;

const typingInterval = setInterval(function () {
    document.getElementById('typingText').textContent += message.charAt(charIndex);
    charIndex++;
    if (charIndex >= message.length) {
        clearInterval(typingInterval);
    }
}, 80);
```

### Challenge 3: Animated Dark Mode Transition (⭐⭐⭐ Hard)

Make the dark mode toggle feel **premium** — instead of just switching colors, add a circular reveal animation:

1. When toggling, create a full-screen overlay `<div>` with the target background color
2. Animate its `clip-path` from `circle(0% at 95% 5%)` (navbar button position) to `circle(150% at 95% 5%)`
3. After the animation completes, apply the actual dark mode class and remove the overlay

**Hints:**
- Use `element.animate()` (Web Animations API) for the clip-path animation
- Create the overlay dynamically with `document.createElement('div')`
- Set `position: fixed; top: 0; left: 0; width: 100%; height: 100%; z-index: 9999`
- Animation duration: ~500ms
- Remove the overlay element after animation finishes using `.addEventListener('finish', ...)`

> 💡 **New concepts in this challenge:** `element.animate()` (Web Animations API), `clip-path` CSS property, `document.createElement()`, dynamic element creation/removal. These are advanced — don't worry if you can't get it working on the first try!

---

## 🔗 Labs Covered in This Session

| Lab # | Experiment Description | How We Covered It |
|-------|----------------------|-------------------|
| **Lab 18** | JS alert on page load | ✅ Welcome toast notification appears automatically 2 seconds after page loads (modern replacement for `alert()`) |
| **Lab 19** | JS background color timer | ✅ Auto-changing background color demo using `setInterval` — cycles through 5 colors every 5 seconds |
| **Lab 4** | Background color + anchor to top | ✅ Back-to-top floating button with smooth scroll; background color change via both dark mode toggle and color demo |
| **Lab 20** | JS dynamic bold/italic/underline styling | ✅ Dynamic class toggling (`classList.toggle`) for dark mode; `style.display` and `style.backgroundColor` manipulation throughout |

---

## ⏭️ Next Session Preview

### Session 12: FAQ Accordion + Code Organization

In the next session, we'll build a **Frequently Asked Questions** section and learn how to **organize our growing JavaScript** into clean, maintainable code. You'll learn:

- 📖 **Bootstrap Accordion** — collapsible panels for FAQ (click question → answer expands)
- 📖 **External JavaScript files** — moving `<script>` code into a separate `.js` file
- 📖 **Code organization** — grouping related functions, naming conventions
- 📖 **`DOMContentLoaded` event** — the right way to run JS after the page is ready

> 💡 **Fun preview:** Our `<script>` tag is getting HUGE. It's like having all your textbooks, notebooks, and assignments in one giant bag. Session 12 teaches you how to organize that bag — separate files for separate concerns. Your future self will thank you!

**Labs covered next time:** Lab 22 ✅

---

*Session 11 of 15 — Crash Course: Bootstrap + JavaScript — BCA Semester II, Mandsaur University, 2025-26*
