# Session 12: "Ask & Answer" — FAQ Accordion + Code Organization

**BCA Semester II | Mandsaur University | Web Technology (25BCA060)**

> **Session 12 of 15** | ⏱️ Duration: 2 hours  
> **Labs Covered:** Lab 22 (Department website project)  
> **JavaScript Style:** ES6+ — `let`, `const`, template literals, arrow functions, `forEach`

---

## 🎯 What We'll Build Today

Today has **two big goals**. First, we build a "Frequently Asked Questions" section using Bootstrap's **Accordion** component. Second — and this is the important one — we **refactor ALL JavaScript** from inline `<script>` tags into a proper external `js/script.js` file. This is how professional developers organize code.

**By the end of this session, you'll have:**

- ✅ A FAQ section with 10 BCA-related questions (Bootstrap Accordion)
- ✅ ALL JavaScript moved from `index.html` to `js/script.js`
- ✅ Code wrapped in `DOMContentLoaded` and organized into `init` functions
- ✅ Callbacks converted to arrow functions, loops to `forEach`

**Project structure after today:**

```
our-class-website/
├── index.html          ← Clean HTML, NO inline <script> code
├── js/
│   └── script.js       ← ALL JavaScript lives here now ✨
└── (images, etc.)
```

---

## 📌 New Concepts at a Glance

| Concept | What It Does | Analogy |
|---------|-------------|---------|
| `.accordion` | Collapsible content panels | 📋 FAQ board at a railway station — tap a question, answer slides open |
| `.accordion-item` | One question–answer pair | One row on the FAQ board |
| `data-bs-parent` | Only one item open at a time | Like train berths — fold one down, others fold up |
| `<details>` + `<summary>` | Native HTML accordion | Browser's built-in FAQ — no CSS needed |
| `<script src="...">` | Links external JS file | Plugging in an external hard drive |
| `DOMContentLoaded` | Waits for HTML before running JS | Waiting for the building before opening the door |
| `() => {}` | Arrow function (shorter syntax) | A shortcut — same meaning, fewer words |
| `.forEach()` | Loops over each array item | Teacher calling each name from the register |

---

## 📖 Bootstrap Accordion — Deep Dive

### What Is an Accordion?

An **accordion** is a vertically stacked list of items where each can expand or collapse. You've seen them on Flipkart help pages, banking apps ("What is NEFT?"), and railway station information boards. Bootstrap gives you this component with smooth animations and accessibility built in.

### Accordion Anatomy

```
.accordion                          ← Outer wrapper
├── .accordion-item                 ← One Q&A pair
│   ├── .accordion-header           ← Contains the button
│   │   └── .accordion-button       ← Clickable question
│   └── .accordion-collapse         ← Collapsible answer panel
│       └── .accordion-body         ← Actual answer content
└── ... (more items)
```

📌 **Key Rule:** The `accordion-button` uses `data-bs-toggle="collapse"` and `data-bs-target="#faq1"` to point at the answer panel's `id`. The answer panel uses `data-bs-parent="#faqAccordion"` to link back to the wrapper.

### `data-bs-parent` — One at a Time

```html
<!-- WITH data-bs-parent → Only ONE answer open at a time -->
<div class="accordion-collapse collapse" data-bs-parent="#faqAccordion">

<!-- WITHOUT data-bs-parent → Multiple answers can stay open -->
<div class="accordion-collapse collapse">
```

Think of it like seats in a Mandsaur city bus — with `data-bs-parent`, folding one seat down automatically folds the others up.

### Accordion Variants

| Variant | Class / Change | Effect |
|---------|---------------|--------|
| Default | `.accordion` | Bordered, background on headers |
| Flush | `.accordion.accordion-flush` | Borderless, blends into the page |
| Always open | Remove `data-bs-parent` | Multiple items can stay expanded |
| Start open | Add `.show` to `.accordion-collapse` | That item is expanded on load |

---

## 📖 Native HTML: `<details>` + `<summary>`

📌 **HTML has its OWN accordion built in — no Bootstrap, no JavaScript needed!**

```html
<details>
    <summary>What is the attendance requirement?</summary>
    <p>You need at least 75% attendance to be eligible for exams.</p>
</details>
```

`<summary>` is always visible; everything else inside `<details>` is hidden until clicked. Bootstrap Accordion looks better and supports one-at-a-time, but `<details>` is great for quick prototypes with zero dependencies.

---

## 📖 External JavaScript Files — Why & How

Right now our `index.html` has ALL JavaScript in inline `<script>` tags. That's like stuffing all textbooks, notebooks, and pens into ONE bag with no compartments. 🎒

### Why External Files Are Better

| Benefit | Explanation |
|---------|-------------|
| **Caching** 🚀 | Browser downloads `script.js` once, reuses on every visit. Inline scripts reload every time. |
| **Separation of concerns** 📂 | HTML = structure, CSS = style, JS = behavior. Like keeping notes, assignments, and lab records in separate folders. |
| **Maintainability** 🔧 | Need to fix a bug? Open ONE file — don't scroll through 500 lines of HTML. |
| **Reusability** ♻️ | Same `script.js` works on multiple pages (about.html, gallery.html, etc.) |
| **Team collaboration** 👥 | Rahul works on HTML, Priya works on JS — no merge conflicts! |

### How to Link

```html
<!-- Place before </body>, AFTER Bootstrap JS -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>
<script src="js/script.js"></script>
</body>
```

📌 The `src` path is relative to `index.html`. With `js/script.js`, the browser looks for a `js` folder next to your HTML file.

---

## 📖 `DOMContentLoaded` — Wait for the Building!

If your JavaScript runs BEFORE the HTML finishes loading, `getElementById('loginBtn')` returns `null` — the button doesn't exist yet! It's like trying to open a door of a building still under construction. 🏗️

```javascript
// ❌ BAD — might run before HTML is ready
const btn = document.getElementById('loginBtn');
btn.addEventListener('click', handleLogin);  // ERROR: btn is null!

// ✅ GOOD — waits for HTML to be fully loaded
document.addEventListener('DOMContentLoaded', () => {
    const btn = document.getElementById('loginBtn');
    btn.addEventListener('click', handleLogin);  // Works!
});
```

📌 **`DOMContentLoaded`** fires when the HTML is fully parsed (all tags ready). It does NOT wait for images — just the structure. We've been safe so far because our `<script>` was at the end of `<body>`, but `DOMContentLoaded` is the professional approach that works no matter where the script tag is.

---

## 📖 Arrow Functions (ES6+)

📌 **New syntax!** A shorter, modern way to write functions.

```javascript
// Regular function → Arrow function → Shortest form
const greet = function(name) { return `Hello, ${name}!`; };
const greet = (name) => { return `Hello, ${name}!`; };
const greet = (name) => `Hello, ${name}!`;  // implicit return
```

### Rules

```javascript
const double = x => x * 2;          // One param — parens optional
const sayHi = () => 'Hello!';       // No params — parens required
const add = (a, b) => a + b;        // Multiple params — parens required
```

📌 **Pro Tip:** Arrow functions DON'T have their own `this`. For most callbacks this doesn't matter — but if you need `this` to refer to the clicked element, use a regular function.

---

## 📖 `forEach` — Cleaner Loops (ES6+)

📌 **Instead of `for` loops, use `.forEach()` on arrays and NodeLists.**

```javascript
// ❌ Old way
const students = ['Rahul', 'Priya', 'Amit', 'Neha'];
for (let i = 0; i < students.length; i++) {
    console.log(`Roll ${i + 1}: ${students[i]}`);
}

// ✅ New way — forEach with arrow function
students.forEach((student, index) => {
    console.log(`Roll ${index + 1}: ${student}`);
});

// Works on DOM NodeLists too!
document.querySelectorAll('.accordion-button').forEach((button) => {
    button.addEventListener('click', () => {
        console.log(`FAQ clicked: ${button.textContent.trim()}`);
    });
});
```

---

## 📖 Code Organization Pattern

This is the **BIG concept** of today. Here's how professional developers organize JavaScript:

```javascript
// ============================================
// BCA Batch 2025-26 — Our Class Website
// Main JavaScript File
// ============================================

document.addEventListener('DOMContentLoaded', () => {

    // --- Initialize All Sections ---
    initNavbar();
    initInfoCards();
    initFacultyCards();
    initTimetable();
    initGallery();
    initFormValidation();
    initLoginSystem();
    initCountdown();
    initDarkMode();
    initBackToTop();
    initWelcomeToast();
    initFAQ();

});

// ============================================
// Section 1: Navbar & Navigation
// ============================================
function initNavbar() {
    const navLinks = document.querySelectorAll('.navbar-nav .nav-link');
    const navbarCollapse = document.querySelector('.navbar-collapse');

    navLinks.forEach((link) => {
        link.addEventListener('click', () => {
            if (navbarCollapse.classList.contains('show')) {
                navbarCollapse.classList.remove('show');
            }
        });
    });
}

// ============================================
// Section 2: Info Cards Toggle
// ============================================
function initInfoCards() {
    // "Read More" toggle on about section cards
    // ... moved from Session 4 inline script ...
}

// ============================================
// Section 3: Faculty Cards
// ============================================
function initFacultyCards() {
    const readMoreBtns = document.querySelectorAll('.faculty-read-more');
    const counter = document.getElementById('expandedCount');
    let expandedCount = 0;
    readMoreBtns.forEach((btn) => {
        btn.addEventListener('click', () => {
            const details = btn.previousElementSibling;
            const isHidden = details.style.display === 'none';
            details.style.display = isHidden ? 'block' : 'none';
            btn.textContent = isHidden ? 'Read Less' : 'Read More';
            expandedCount += isHidden ? 1 : -1;
            if (counter) {
                counter.textContent = `Expanded: ${expandedCount} of ${readMoreBtns.length}`;
            }
        });
    });
}

// ============================================
// Section 4: Timetable Highlighting
// ============================================
function initTimetable() {
    // Highlight current day's row in timetable
    // ... moved from Session 6 inline script ...
}

// ============================================
// Section 5: Gallery Lightbox
// ============================================
function initGallery() {
    // Gallery image click → open modal
    // ... moved from Session 7 inline script ...
}

// ============================================
// Section 6: Form Validation
// ============================================
function initFormValidation() {
    const contactForm = document.getElementById('contactForm');
    if (!contactForm) return;  // Guard clause — skip if not on page
    contactForm.addEventListener('submit', (e) => {
        e.preventDefault();
        const name = document.getElementById('contactName').value.trim();
        const email = document.getElementById('contactEmail').value.trim();
        let isValid = true;
        const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        if (name.length < 2) isValid = false;
        if (!emailRegex.test(email)) isValid = false;
        if (isValid) {
            alert(`Thank you, ${name}! Your message has been received.`);
            contactForm.reset();
        }
    });
}

// ============================================
// Section 7: Login System
// ============================================
function initLoginSystem() {
    // Login modal + localStorage credential storage
    // ... moved from Session 10 inline script ...
}

// ============================================
// Section 8: Countdown Timer
// ============================================
function initCountdown() {
    // Exam countdown timer
    // ... moved from Session 11 inline script ...
}

// ============================================
// Section 9: Dark Mode
// ============================================
function initDarkMode() {
    const toggle = document.getElementById('darkModeToggle');
    if (!toggle) return;
    const savedTheme = localStorage.getItem('theme');
    if (savedTheme === 'dark') {
        document.body.classList.add('dark-mode');
        toggle.textContent = '☀️';
    }
    toggle.addEventListener('click', () => {
        document.body.classList.toggle('dark-mode');
        const isDark = document.body.classList.contains('dark-mode');
        toggle.textContent = isDark ? '☀️' : '🌙';
        localStorage.setItem('theme', isDark ? 'dark' : 'light');
    });
}

// ============================================
// Section 10: Back to Top
// ============================================
function initBackToTop() {
    const btn = document.getElementById('backToTop');
    if (!btn) return;
    window.addEventListener('scroll', () => {
        btn.style.display = window.scrollY > 300 ? 'block' : 'none';
    });
    btn.addEventListener('click', () => {
        window.scrollTo({ top: 0, behavior: 'smooth' });
    });
}

// ============================================
// Section 11: Welcome Toast
// ============================================
function initWelcomeToast() {
    // Show Bootstrap toast on page load
    // ... moved from Session 11 inline script ...
}

// ============================================
// Section 12: FAQ Section
// ============================================
function initFAQ() {
    const faqButtons = document.querySelectorAll('#faqAccordion .accordion-button');

    faqButtons.forEach((button) => {
        button.addEventListener('click', () => {
            console.log(`FAQ viewed: ${button.textContent.trim()}`);
        });
    });
}
```

### Why This Pattern Works

1. **`DOMContentLoaded`** — nothing runs too early
2. **`init` functions** — related code is grouped; easy to find, easy to debug
3. **Guard clauses** (`if (!element) return;`) — prevent errors if an element doesn't exist
4. **Comment headers** — scrolling through the file is fast
5. **Independence** — if gallery breaks, login still works

---

## 🔨 Let's Build! — Step by Step

### Step 1: Add the FAQ Section HTML

Add this **before the footer** in `index.html`:

```html
<!-- ==================== FAQ Section ==================== -->
<section id="faq" class="py-5 bg-light">
    <div class="container">
        <h2 class="text-center mb-4">❓ Frequently Asked Questions</h2>
        <p class="text-center text-muted mb-5">
            Got questions about BCA at Mandsaur University? We've got answers!
        </p>

        <div class="row justify-content-center">
            <div class="col-lg-8">
                <div class="accordion" id="faqAccordion">

                    <!-- FAQ 1 (starts open — notice .show) -->
                    <div class="accordion-item">
                        <h2 class="accordion-header">
                            <button class="accordion-button" type="button"
                                    data-bs-toggle="collapse"
                                    data-bs-target="#faq1">
                                What subjects are in BCA Semester II?
                            </button>
                        </h2>
                        <div id="faq1" class="accordion-collapse collapse show"
                             data-bs-parent="#faqAccordion">
                            <div class="accordion-body">
                                BCA Semester II includes: <strong>Web Technology</strong>
                                (this course!), <strong>Mathematics-II</strong>,
                                <strong>Data Structures</strong>,
                                <strong>English Communication</strong>, and
                                <strong>Environmental Science</strong>. Each has
                                theory lectures and practical labs.
                            </div>
                        </div>
                    </div>

                    <!-- FAQ 2 -->
                    <div class="accordion-item">
                        <h2 class="accordion-header">
                            <button class="accordion-button collapsed" type="button"
                                    data-bs-toggle="collapse"
                                    data-bs-target="#faq2">
                                What programming languages will I learn?
                            </button>
                        </h2>
                        <div id="faq2" class="accordion-collapse collapse"
                             data-bs-parent="#faqAccordion">
                            <div class="accordion-body">
                                <strong>HTML, CSS, JavaScript</strong> (this course),
                                <strong>C</strong> for fundamentals,
                                <strong>Python</strong> for scripting,
                                <strong>Java</strong> for OOP, and
                                <strong>SQL</strong> for databases. By graduation,
                                you'll know 5+ languages!
                            </div>
                        </div>
                    </div>

                    <!-- FAQ 3 -->
                    <div class="accordion-item">
                        <h2 class="accordion-header">
                            <button class="accordion-button collapsed" type="button"
                                    data-bs-toggle="collapse"
                                    data-bs-target="#faq3">
                                What is the attendance requirement?
                            </button>
                        </h2>
                        <div id="faq3" class="accordion-collapse collapse"
                             data-bs-parent="#faqAccordion">
                            <div class="accordion-body">
                                At least <strong>75% attendance</strong> in each subject
                                (theory + practicals) to be exam-eligible. Track it via
                                your attendance register or ask your CR.
                            </div>
                        </div>
                    </div>

                    <!-- FAQ 4 -->
                    <div class="accordion-item">
                        <h2 class="accordion-header">
                            <button class="accordion-button collapsed" type="button"
                                    data-bs-toggle="collapse"
                                    data-bs-target="#faq4">
                                How are lab experiments graded?
                            </button>
                        </h2>
                        <div id="faq4" class="accordion-collapse collapse"
                             data-bs-parent="#faqAccordion">
                            <div class="accordion-body">
                                Each experiment is worth <strong>15 marks</strong>
                                (5 criteria × 3 marks): Understanding, Code Quality,
                                Output Accuracy, Viva Performance, and Timely Submission.
                            </div>
                        </div>
                    </div>

                    <!-- FAQ 5 -->
                    <div class="accordion-item">
                        <h2 class="accordion-header">
                            <button class="accordion-button collapsed" type="button"
                                    data-bs-toggle="collapse"
                                    data-bs-target="#faq5">
                                Can I use my own laptop in the lab?
                            </button>
                        </h2>
                        <div id="faq5" class="accordion-collapse collapse"
                             data-bs-parent="#faqAccordion">
                            <div class="accordion-body">
                                Yes! Install <strong>VS Code</strong> and
                                <strong>Google Chrome</strong>. Add the
                                <em>Live Server</em> extension in VS Code for
                                auto-refresh as you code.
                            </div>
                        </div>
                    </div>

                    <!-- FAQ 6 -->
                    <div class="accordion-item">
                        <h2 class="accordion-header">
                            <button class="accordion-button collapsed" type="button"
                                    data-bs-toggle="collapse"
                                    data-bs-target="#faq6">
                                How do I submit assignments?
                            </button>
                        </h2>
                        <div id="faq6" class="accordion-collapse collapse"
                             data-bs-parent="#faqAccordion">
                            <div class="accordion-body">
                                Via <strong>GitHub Classroom</strong>. Click the
                                invitation link, clone the repo, write your code,
                                commit, and push. Submissions are timestamped
                                automatically — no excuses for late work! 😄
                            </div>
                        </div>
                    </div>

                    <!-- FAQ 7 -->
                    <div class="accordion-item">
                        <h2 class="accordion-header">
                            <button class="accordion-button collapsed" type="button"
                                    data-bs-toggle="collapse"
                                    data-bs-target="#faq7">
                                What is Bootstrap?
                            </button>
                        </h2>
                        <div id="faq7" class="accordion-collapse collapse"
                             data-bs-parent="#faqAccordion">
                            <div class="accordion-body">
                                A free CSS framework with pre-built components
                                (navbars, cards, modals, this accordion!) and a
                                responsive grid system. We use
                                <strong>Bootstrap 5.3.2</strong> in this course.
                            </div>
                        </div>
                    </div>

                    <!-- FAQ 8 -->
                    <div class="accordion-item">
                        <h2 class="accordion-header">
                            <button class="accordion-button collapsed" type="button"
                                    data-bs-toggle="collapse"
                                    data-bs-target="#faq8">
                                Where can I find study materials?
                            </button>
                        </h2>
                        <div id="faq8" class="accordion-collapse collapse"
                             data-bs-parent="#faqAccordion">
                            <div class="accordion-body">
                                Right here! 📚 This GitHub repository has all session
                                notes and source code. Also check
                                <a href="https://getbootstrap.com/docs/5.3/"
                                   target="_blank">Bootstrap Docs</a> and
                                <a href="https://developer.mozilla.org/"
                                   target="_blank">MDN Web Docs</a>.
                            </div>
                        </div>
                    </div>

                    <!-- FAQ 9 -->
                    <div class="accordion-item">
                        <h2 class="accordion-header">
                            <button class="accordion-button collapsed" type="button"
                                    data-bs-toggle="collapse"
                                    data-bs-target="#faq9">
                                What are the career options after BCA?
                            </button>
                        </h2>
                        <div id="faq9" class="accordion-collapse collapse"
                             data-bs-parent="#faqAccordion">
                            <div class="accordion-body">
                                Web Developer, Software Engineer, App Developer,
                                Database Administrator, System Analyst, and more.
                                You can also pursue <strong>MCA</strong> or prepare
                                for government IT exams.
                            </div>
                        </div>
                    </div>

                    <!-- FAQ 10 -->
                    <div class="accordion-item">
                        <h2 class="accordion-header">
                            <button class="accordion-button collapsed" type="button"
                                    data-bs-toggle="collapse"
                                    data-bs-target="#faq10">
                                How do I contact the department?
                            </button>
                        </h2>
                        <div id="faq10" class="accordion-collapse collapse"
                             data-bs-parent="#faqAccordion">
                            <div class="accordion-body">
                                Use the <a href="#contact">Contact Form</a> on this
                                website! Or visit the BCA department office, 2nd floor
                                IT block (10 AM – 5 PM, Mon–Sat).
                            </div>
                        </div>
                    </div>

                </div><!-- /.accordion -->
            </div><!-- /.col-lg-8 -->
        </div><!-- /.row -->
    </div><!-- /.container -->
</section>
```

📌 **Notice the pattern:** Every item has the same structure — only `id`, `data-bs-target`, and content change. Copy-paste the first item and edit — that's how real developers do it!

### Step 2: Add a Navbar Link

```html
<li class="nav-item">
    <a class="nav-link" href="#faq">FAQ</a>
</li>
```

### Step 3: Create `js/script.js`

Create a `js/` folder in your project, and a `script.js` file inside it.

### Step 4: Move ALL JavaScript to `script.js`

Open `index.html`, find every `<script>` tag with YOUR code (not the Bootstrap CDN link), **cut** all the code, and paste it into `js/script.js`. Wrap it in the `DOMContentLoaded` pattern and organize into `init` functions as shown in the Code Organization Pattern above.

### Step 5: Convert to Arrow Functions & forEach

Go through your code and replace `function()` callbacks with `() =>` and `for` loops with `.forEach()` — see the Arrow Functions and forEach sections above for the patterns.

### Step 6: Update `index.html`

Remove all inline `<script>` content and add the external file:

```html
    <!-- Bootstrap JS (keep this!) -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>
    <!-- Our JavaScript (NEW!) -->
    <script src="js/script.js"></script>
</body>
</html>
```

### Step 7: Test EVERYTHING

Open DevTools (F12 → Console) and verify:

- [ ] Navbar, carousel, faculty cards, timetable, gallery, form validation — all work
- [ ] Login system + localStorage — works
- [ ] Countdown, dark mode, back-to-top, toast — all work
- [ ] **FAQ accordion opens/closes, only one at a time**
- [ ] **No errors in Console**
- [ ] **`index.html` has zero inline `<script>` code**

---

## ✅ Checkpoint

| Check | Status |
|-------|--------|
| FAQ section visible before footer? | ⬜ |
| First FAQ starts open (`.show`), rest collapsed? | ⬜ |
| Only one FAQ answer open at a time? | ⬜ |
| `js/script.js` exists with ALL JavaScript? | ⬜ |
| `index.html` has NO inline `<script>` code? | ⬜ |
| Code wrapped in `DOMContentLoaded`? | ⬜ |
| Organized into `init` functions with comment headers? | ⬜ |
| ALL previous features still work? | ⬜ |
| No Console errors? | ⬜ |

📌 **The "everything still works" check is the MOST important.** Moving code to an external file should change NOTHING about behavior. If something broke, you likely missed a variable or function.

---

## 📋 Quick Reference

### Accordion — Minimal Template

```html
<div class="accordion" id="myAccordion">
    <div class="accordion-item">
        <h2 class="accordion-header">
            <button class="accordion-button" type="button"
                    data-bs-toggle="collapse" data-bs-target="#itemOne">
                Question Text
            </button>
        </h2>
        <div id="itemOne" class="accordion-collapse collapse show"
             data-bs-parent="#myAccordion">
            <div class="accordion-body">Answer text.</div>
        </div>
    </div>
</div>
```

### External JS + DOMContentLoaded

```javascript
// js/script.js — linked via <script src="js/script.js"></script> before </body>
document.addEventListener('DOMContentLoaded', () => { /* all code here */ });
```

### Arrow Functions & forEach

```javascript
const double = x => x * 2;                              // arrow function
['a', 'b'].forEach((item) => console.log(item));         // forEach
document.querySelectorAll('.btn').forEach((btn) => {     // DOM forEach
    btn.addEventListener('click', () => { /* ... */ });
});
```

---

## 🔑 Key Takeaways

1. **Bootstrap Accordion** — expandable FAQ with zero custom JS (Bootstrap handles it via `data-bs-*`)
2. **`data-bs-parent`** — makes it "one at a time"; remove it for "always open"
3. **`<details>` + `<summary>`** — native HTML alternative, simpler but less stylish
4. **External JS files** — better caching, maintainability, separation of concerns
5. **`DOMContentLoaded`** — ensures JS runs only after HTML is ready
6. **Arrow functions** (`=>`) — shorter syntax for callbacks and array methods
7. **`forEach`** — cleaner than `for` loops for arrays and NodeLists
8. **`init` functions + comment headers** — professional code organization pattern
9. **Guard clauses** (`if (!el) return;`) — prevent errors when elements are missing
10. **Always test after refactoring** — moving code must never change behavior

---

## 🏋️ Practice Challenges

### Challenge 1: FAQ Search/Filter (⭐⭐)

Add a search box that filters FAQ items as the user types:

```javascript
const searchInput = document.getElementById('faqSearch');
const faqItems = document.querySelectorAll('#faqAccordion .accordion-item');

searchInput.addEventListener('input', () => {
    const query = searchInput.value.toLowerCase();
    faqItems.forEach((item) => {
        const text = item.textContent.toLowerCase();
        item.style.display = text.includes(query) ? '' : 'none';
    });
});
```

### Challenge 2: "Was This Helpful?" Buttons (⭐⭐⭐)

Add thumbs up/down inside each `.accordion-body`:

```javascript
document.querySelectorAll('.helpful-btn').forEach((btn) => {
    btn.addEventListener('click', () => {
        btn.closest('p').innerHTML = '<em>Thanks for your feedback! 🙏</em>';
    });
});
```

### Challenge 3: Dark Mode Keyboard Shortcut (⭐)

Press `Ctrl + D` to toggle dark mode:

```javascript
document.addEventListener('keydown', (e) => {
    if (e.ctrlKey && e.key === 'd') {
        e.preventDefault();
        document.getElementById('darkModeToggle').click();
    }
});
```

---

## 🧪 Labs Covered

| Lab | Experiment | How It's Covered |
|-----|-----------|-----------------|
| 22 | Department website project | FAQ accordion section + full codebase refactored into external JS |

---

## ⏭️ Next Session Preview

**Session 13: "Dress to Impress" — Custom CSS + Visual Polish** — We'll create `css/custom.css` with custom colors, fonts, hover effects, and animations. Our website is about to look truly unique! 🎨

---

*Session 12 of 15 — BCA Semester II, Mandsaur University, 2025-26*
