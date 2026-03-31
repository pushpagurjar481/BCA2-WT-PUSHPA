# Day 4 — World Wide Web, Web Clients & Web Servers

📖 **Type:** Theory Session
🕐 **Duration:** 2 Hours
📚 **Unit:** 1 — Internet Technology

---

## Learning Objectives

By the end of this session, students will be able to:
- Differentiate between the Internet and the World Wide Web
- Explain the client-server architecture of the web
- Describe how web browsers and web servers work
- Understand URLs and how web resources are located

---

## 1. Internet ≠ World Wide Web

> **Common Misconception:** Most people use "internet" and "web" interchangeably. They are NOT the same thing.

| Feature | Internet | World Wide Web (WWW) |
|---------|----------|---------------------|
| **What** | Global network of connected computers | A service that runs ON the internet |
| **When** | 1969 (ARPANET) | 1989 (Tim Berners-Lee) |
| **Analogy** | The road system | The trucks and shops using the roads |
| **Includes** | Email, FTP, VoIP, IoT, WWW | Websites, web apps, hyperlinks |
| **Protocol** | TCP/IP | HTTP/HTTPS |

> **Analogy:** The internet is the **highway system** — the physical infrastructure of roads, bridges, and traffic signals. The WWW is just one type of **vehicle** (websites) that travels on those highways. Other vehicles include email (SMTP), file transfers (FTP), and video calls (VoIP).

---

## 2. The World Wide Web (WWW)

### What is the WWW?

The **World Wide Web** is a system of interlinked **hypertext documents** and resources, accessed via the internet using **web browsers**. It was invented by **Tim Berners-Lee** at CERN in **1989**.

### Three Pillars of the WWW

| Pillar | What It Is | Purpose |
|--------|-----------|---------|
| **HTML** | HyperText Markup Language | Structure of web pages |
| **HTTP** | HyperText Transfer Protocol | Rules for transferring web pages |
| **URL** | Uniform Resource Locator | Address of web resources |

### How the Web Works — Simplified

```
┌──────────────┐         HTTP Request          ┌──────────────┐
│              │ ──────────────────────────────▶│              │
│  Web Client  │    "GET /index.html"           │  Web Server  │
│  (Browser)   │                                │  (Apache/    │
│              │ ◀──────────────────────────────│   Nginx)     │
│              │         HTTP Response           │              │
└──────────────┘    HTML + CSS + Images          └──────────────┘
```

> **Code Explanation:**
> - The **Web Client (Browser)** on the left sends an **HTTP Request** to the **Web Server** on the right. Think of it like placing an order at a restaurant — you (client) tell the waiter (HTTP) what you want.
> - `GET /index.html` is the request — the browser is asking for a specific file called `index.html`. `GET` is the HTTP method meaning "give me this resource." The `/` before `index.html` means the file is at the root (top-level) of the website.
> - The server finds that file, wraps it in an **HTTP Response**, and sends back the HTML content along with any CSS stylesheets and images the page needs.
> - This request-response pattern is the **foundation of all web communication** — every time you open a website, this exact exchange happens (often dozens of times for all the files a page needs).

---

## 3. Web Clients (Browsers)

### What is a Web Client?

A **web client** is any software that requests and displays web content. The most common web clients are **web browsers**.

### How a Browser Works

```
User types URL
      │
      ▼
┌─────────────────┐
│  1. URL Parser   │ → Breaks down the URL
├─────────────────┤
│  2. DNS Resolver │ → Converts domain to IP
├─────────────────┤
│  3. HTTP Client  │ → Sends request to server
├─────────────────┤
│  4. HTML Parser  │ → Reads the HTML structure
├─────────────────┤
│  5. CSS Engine   │ → Applies styling
├─────────────────┤
│  6. JS Engine    │ → Runs JavaScript code
├─────────────────┤
│  7. Rendering    │ → Paints pixels on screen
│     Engine       │
└─────────────────┘
      │
      ▼
  Webpage displayed!
```

> **Code Explanation:**
> - The browser works like an **assembly line in a factory**. Raw materials (URL) come in at the top, pass through 7 stations, and a finished product (webpage) comes out at the bottom.
> - **URL Parser** breaks the address into parts (scheme, host, path) — like reading a delivery address.
> - **DNS Resolver** converts the domain name (e.g., `google.com`) into an IP address (e.g., `142.250.77.46`) — like looking up a phone number in a directory.
> - **HTTP Client** sends the actual request to the server and receives the response.
> - **HTML Parser** reads the HTML tags and builds a structured tree (called the DOM).
> - **CSS Engine** reads all the style rules and figures out how each element should look.
> - **JS Engine** runs any JavaScript code that adds interactivity.
> - **Rendering Engine** combines everything and paints the final pixels on your screen.

### 3.1 The DOM (Document Object Model)

When the browser's **HTML Parser** reads your HTML code, it doesn't just see text — it builds a **tree structure** called the **DOM (Document Object Model)**. Every HTML tag becomes a **node** in this tree.

> **Analogy:** The DOM is like an **organisational chart (org chart) of a company**. The `<html>` tag is the CEO at the top, `<head>` and `<body>` are the two Vice Presidents below, and every other element is an employee reporting to their manager. Just like you can find any employee by following the org chart, JavaScript can find any element by traversing the DOM tree.

**Example — HTML code and its DOM tree:**

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Mandsaur University</title>
  </head>
  <body>
    <h1>Welcome</h1>
    <p>BCA Department</p>
  </body>
</html>
```

```
                    Document
                       │
                     <html>
                    ┌──┴──┐
                 <head>  <body>
                   │     ┌──┴──┐
                <title> <h1>  <p>
                   │     │     │
              "Mandsaur  "Welc "BCA
              University" ome" Department"
```

> **Code Explanation:**
> - The HTML code on the left is what you **write**. The tree diagram on the right is what the **browser creates** internally.
> - `<html>` is the **root node** — everything else is inside it.
> - `<head>` and `<body>` are **child nodes** of `<html>`, and siblings of each other.
> - The actual text content ("Mandsaur University", "Welcome", "BCA Department") are **text nodes** — the leaves of the tree.
> - JavaScript uses this DOM tree to find and change elements. For example, `document.querySelector('h1')` walks down this tree to find the `<h1>` node.

### 3.2 The Browser Rendering Pipeline

Once the browser has the HTML and CSS, it goes through a multi-step **rendering pipeline** to display pixels on screen:

```
HTML Text        CSS Text
    │                │
    ▼                ▼
┌────────┐    ┌─────────┐
│  DOM   │    │  CSSOM  │
│  Tree  │    │  Tree   │
└───┬────┘    └────┬────┘
    │              │
    └──────┬───────┘
           ▼
    ┌─────────────┐
    │ Render Tree │  (DOM + CSSOM combined — only visible elements)
    └──────┬──────┘
           ▼
    ┌─────────────┐
    │   Layout    │  (Calculate position & size of each element)
    └──────┬──────┘
           ▼
    ┌─────────────┐
    │    Paint    │  (Fill in pixels — colors, text, borders, shadows)
    └──────┬──────┘
           ▼
    ┌─────────────┐
    │  Composite  │  (Layer multiple painted layers into final image)
    └─────────────┘
           │
           ▼
      Pixels on Screen!
```

**What each step does:**

| Step | What Happens | Analogy |
|------|-------------|---------|
| **DOM Tree** | Browser reads HTML and builds a tree of elements | Reading the blueprint of a house |
| **CSSOM Tree** | Browser reads CSS and builds a tree of style rules | Reading the interior design plan |
| **Render Tree** | Combines DOM + CSSOM, excludes hidden elements (`display: none`) | Merging the blueprint with the design plan — skipping rooms that are sealed off |
| **Layout** | Calculates exact position (x, y) and size (width, height) of every element | Measuring and marking where each piece of furniture goes in the house |
| **Paint** | Fills in the actual visual content — text, colors, images, borders | The painters and decorators doing their work |
| **Composite** | Combines different painted layers (like overlapping elements, animations) into the final image | Stacking transparent sheets to create the final picture |

### 3.3 CSS Engine Details

The **CSS Engine** (also called the style engine) determines how each element looks. It follows a priority system called the **cascade**:

**Cascade Priority Order (highest to lowest):**

| Priority | Type | Example |
|----------|------|---------|
| 1 (Highest) | Inline styles | `<p style="color: red;">` |
| 2 | Internal stylesheet | `<style> p { color: blue; } </style>` in `<head>` |
| 3 | External stylesheet | `<link rel="stylesheet" href="style.css">` |
| 4 (Lowest) | Browser defaults | The browser's built-in styles |

> **Analogy:** Imagine dressing for college. Your **own choice** (inline style) overrides your **hostel warden's suggestion** (internal stylesheet), which overrides the **university dress code** (external stylesheet), which overrides your **natural appearance** (browser defaults). The most specific instruction wins.

The CSS engine reads every rule, checks which DOM nodes it matches using **selectors** (like `p`, `.highlight`, `#header`), and applies the styles. When two rules conflict, **specificity** decides the winner — an ID selector (`#header`) beats a class selector (`.header`), which beats a tag selector (`h1`).

### 3.4 JavaScript Engine

The **JavaScript (JS) Engine** is the part of the browser that executes JavaScript code. The most well-known JS engine is Google's **V8** (used in Chrome and Edge).

**Key facts about the JS Engine:**

- JavaScript is **single-threaded** — it can do only one thing at a time, like a single-lane road
- By default, when the browser encounters a `<script>` tag, it **stops HTML parsing** (blocks rendering) until the script finishes executing
- This is why **script placement matters**:

**Where to place `<script>` tags:**

| Placement | Behavior | When to Use |
|-----------|----------|-------------|
| `<script>` in `<head>` | Blocks page rendering until script loads and executes | Rarely — only if the script MUST run before page appears |
| `<script>` at end of `<body>` | Page renders first, then script runs | ✅ **Best practice for beginners** — page appears fast |
| `<script async>` in `<head>` | Downloads in parallel, executes as soon as downloaded (may run out of order) | Independent scripts like analytics |
| `<script defer>` in `<head>` | Downloads in parallel, executes after HTML is fully parsed (maintains order) | ✅ **Best practice** — scripts that need the DOM |

```
Without async/defer:         With async:              With defer:
                             
HTML ████░░░░████            HTML ████████████          HTML ████████████
JS        ████               JS     ██ (when ready)    JS              ██ (after HTML done)
          ↑ blocks                  ↑ non-blocking                     ↑ non-blocking
```

> **Code Explanation:**
> - The timeline diagrams show how the browser handles script loading. The `█` blocks represent active work.
> - **Without async/defer:** The browser stops parsing HTML (the gap `░░░░`) while it downloads and runs the JS. The user sees a blank or incomplete page.
> - **With async:** HTML parsing continues while the script downloads in the background. But the script runs immediately when downloaded — so it might run before the HTML is fully parsed.
> - **With defer:** HTML parsing continues AND the script waits until all HTML is parsed before running. This is the **safest option** for most scripts.

### 3.5 Browser Caching

**Caching** means the browser saves copies of files (HTML, CSS, images) locally so it doesn't need to download them again on your next visit.

> **Analogy:** Think of it like a **photocopy of your notes**. The first time you borrow notes from a friend (server), you make a photocopy (cache). Next time you need those notes, you check your photocopy first — if the friend hasn't updated them, you use your copy and save a trip.

**Why caching matters:**
- ⚡ **Faster loading** — no need to re-download unchanged files
- 📉 **Saves bandwidth** — important in India where mobile data costs matter
- 🔋 **Reduces server load** — server handles fewer requests

**Key HTTP Headers for Caching:**

| Header | Purpose | Example |
|--------|---------|---------|
| `Cache-Control` | Tells browser how long to keep the cached copy | `Cache-Control: max-age=3600` (cache for 1 hour) |
| `ETag` | A unique fingerprint of the file — browser sends it back to check if file changed | `ETag: "abc123"` |
| `Last-Modified` | Date when the file was last changed on the server | `Last-Modified: Mon, 14 Jul 2025 10:00:00 GMT` |

**How caching works — First Visit vs Second Visit:**

```
FIRST VISIT (nothing cached):
┌─────────┐                          ┌─────────┐
│ Browser │ ── GET /style.css ──────▶│ Server  │
│         │                          │         │
│         │ ◀── 200 OK + file ───── │         │
│         │     + ETag: "abc123"     │         │
└─────────┘     + Cache-Control:     └─────────┘
   │             max-age=3600
   ▼
  💾 Saves file + headers in cache

SECOND VISIT (within 1 hour — cache is fresh):
┌─────────┐
│ Browser │ ── Checks cache → File found, not expired → Uses cached copy ✅
│         │    (No server request needed!)
└─────────┘

SECOND VISIT (after 1 hour — cache expired):
┌─────────┐                                    ┌─────────┐
│ Browser │ ── GET /style.css ────────────────▶│ Server  │
│         │    If-None-Match: "abc123"          │         │
│         │                                     │         │
│         │ ◀── 304 Not Modified ──────────────│         │
│         │     (No file sent — use your cache!)│         │
└─────────┘                                     └─────────┘
```

> **Code Explanation:**
> - **First visit:** The browser has nothing cached, so it downloads the file normally. The server includes caching headers — `ETag` (a unique ID for this version of the file) and `Cache-Control: max-age=3600` (this file is valid for 3600 seconds = 1 hour).
> - **Second visit (cache fresh):** If you revisit within 1 hour, the browser doesn't even contact the server — it just uses the saved copy. This is why pages load much faster on revisits.
> - **Second visit (cache expired):** After 1 hour, the browser asks the server "I have version `abc123` — has it changed?" The server replies with `304 Not Modified` (meaning "no changes, use your copy") — saving bandwidth because the actual file isn't sent again.

### Popular Web Browsers

| Browser | Engine | Developer | Market Share (approx.) |
|---------|--------|-----------|----------------------|
| Google Chrome | Blink/V8 | Google | ~65% |
| Safari | WebKit | Apple | ~18% |
| Firefox | Gecko | Mozilla | ~3% |
| Edge | Blink/V8 | Microsoft | ~5% |
| Opera | Blink/V8 | Opera Software | ~2% |

### Browser Developer Tools

Every modern browser includes **Developer Tools** (press `F12`) that let you:
- Inspect HTML elements
- View and edit CSS styles
- Debug JavaScript
- Monitor network requests
- Check performance

> 💡 **Pro Tip:** We'll use browser Developer Tools extensively throughout this course for debugging our web pages.

---

## 4. Web Servers

### What is a Web Server?

> **Analogy:** A web server is like a **librarian**. When you ask for a book (request a URL), the librarian (server) finds the book in the library (file system) and hands it to you (sends the response). If the book doesn't exist, the librarian tells you "Not Found" (404 error).

A **web server** is a computer that:
1. Stores web files (HTML, CSS, images, etc.)
2. Runs server software to handle HTTP requests
3. Sends responses back to clients

### How a Web Server Processes Requests

```
Client Request                        Server Processing
─────────────                        ─────────────────
GET /about.html          ┌──────────────────────────────┐
        ──────────────▶  │ 1. Receive the request        │
                         │ 2. Parse the URL path          │
                         │ 3. Find the file (/about.html) │
                         │ 4. Read the file contents       │
                         │ 5. Prepare HTTP response        │
        ◀──────────────  │ 6. Send response + file         │
HTTP 200 OK              └──────────────────────────────┘
+ about.html content
```

> **Code Explanation:**
> - The client sends `GET /about.html` — this tells the server "I want the file named `about.html`."
> - **Step 1-2:** The server receives the raw request and parses the URL path (`/about.html`) to figure out which file is being asked for.
> - **Step 3-4:** The server searches its file system (like looking through a folder on your computer) for the file `/about.html` and reads its contents into memory.
> - **Step 5-6:** The server wraps the file contents in an HTTP response with a **status code** — `HTTP 200 OK` means "I found it, here it is." If the file didn't exist, it would send `HTTP 404 Not Found` instead.
> - The entire process typically happens in **milliseconds** — faster than you can blink!

### Popular Web Servers

| Server | Developer | Used By |
|--------|-----------|---------|
| **Apache HTTP Server** | Apache Foundation | ~30% of websites |
| **Nginx** | Nginx Inc. | ~34% of websites |
| **IIS** | Microsoft | Windows-based servers |
| **LiteSpeed** | LiteSpeed Technologies | High-performance sites |
| **Node.js** | OpenJS Foundation | JavaScript-based servers |

### Static vs Dynamic Web Servers

| Feature | Static Server | Dynamic Server |
|---------|---------------|----------------|
| **Content** | Pre-built HTML files | Generated on-the-fly |
| **Speed** | Faster (just serve files) | Slower (processing needed) |
| **Example** | Personal portfolio | Amazon product page |
| **Changes** | Need to edit HTML files | Content changes with user/data |

### Static Server Example

A **static server** simply serves files stored on disk — no processing, no database, no logic. What you put on the server is exactly what the user gets.

**Example:** Rahul Sharma from Mandsaur builds a portfolio website. His server's file structure looks like:

```
📁 rahul-portfolio/
├── index.html        ← Homepage
├── about.html        ← About page
├── projects.html     ← Projects page
├── 📁 css/
│   └── style.css     ← Stylesheet
└── 📁 images/
    ├── photo.jpg      ← Rahul's photo
    └── logo.png       ← Logo
```

When someone visits `http://rahul-sharma.in/about.html`, the server simply reads `about.html` from the folder and sends it back. **Every visitor sees the exact same page** — no customisation.

### Dynamic Server Example

A **dynamic server** generates HTML **on-the-fly** based on who is visiting, what data is in the database, or what parameters are in the URL.

**Example — A university result portal:**

When **Priya Patel** (Roll No: BCA2025-042) logs in, the server generates a page showing *her* marks. When **Amit Joshi** (Roll No: BCA2025-078) logs in, the server generates a *different* page with *his* marks — even though both visit the same URL (`/results`).

**Conceptual pseudo-code (not real code — just the idea):**

```
When a student visits /results:
    1. Read the student's Roll Number from the login session
    2. Query the database: "SELECT * FROM results WHERE roll_no = ?"
    3. Get the student's name, marks, and grade
    4. Fill in a template:

    Template:
    ┌─────────────────────────────────────┐
    │ <h1>Result: {student_name}</h1>     │
    │ <p>Roll No: {roll_no}</p>           │
    │ <p>Web Technology: {marks_wt}/100</p>│
    │ <p>Grade: {grade}</p>               │
    └─────────────────────────────────────┘

    For Priya → {student_name} = "Priya Patel", {marks_wt} = 87, {grade} = "A"
    For Amit  → {student_name} = "Amit Joshi",  {marks_wt} = 72, {grade} = "B+"
    
    5. Send the filled-in HTML as the response
```

> **Code Explanation:**
> - The template uses **placeholders** like `{student_name}` — these are replaced with real data from the database before the HTML is sent to the browser.
> - This is the core idea behind **server-side rendering** — the server builds a unique HTML page for each user/request.
> - The browser receives plain HTML — it has no idea the page was dynamically generated. It looks just like a static page to the browser.

### Query String Parameters

The **query string** is the part of a URL that comes after the `?` symbol. It sends **extra data** to the server as **key-value pairs**.

**Format:** `?key1=value1&key2=value2&key3=value3`

**Example:**
```
https://shop.example.in/search?item=kurta&city=Mandsaur&price=500
└──────────┬──────────┘└──┬──┘ └──────────────┬──────────────────┘
       Base URL         Path           Query String
```

The server reads these values:

| Key | Value | Meaning |
|-----|-------|---------|
| `item` | `kurta` | The user is searching for "kurta" |
| `city` | `Mandsaur` | Filter results to Mandsaur city |
| `price` | `500` | Maximum price is ₹500 |

**URL Encoding:** Special characters in URLs must be encoded (replaced with `%` codes) because URLs can only contain certain characters.

| Character | Encoded Form | Example |
|-----------|-------------|---------|
| Space | `%20` or `+` | `Mandsaur University` → `Mandsaur%20University` |
| `&` | `%26` | Used to separate parameters, so literal `&` must be encoded |
| `=` | `%3D` | Used for key=value, so literal `=` must be encoded |
| `?` | `%3F` | Marks start of query string |
| `/` | `%2F` | Path separator |
| `#` | `%23` | Fragment identifier |
| `@` | `%40` | `priya@email.com` → `priya%40email.com` |
| `₹` | `%E2%82%B9` | Indian Rupee symbol |

**Example:** If a user searches for "silk saree red & gold", the URL becomes:
```
https://shop.example.in/search?item=silk+saree+red+%26+gold&city=Indore
```

> **Code Explanation:**
> - The space in "silk saree red" is replaced with `+` signs (or `%20`).
> - The `&` between "red" and "gold" is encoded as `%26` because a literal `&` would be mistaken as a parameter separator.
> - This encoding happens automatically when you submit a form or use a search bar — you don't have to do it manually.

---

## 5. URLs (Uniform Resource Locators)

### Anatomy of a URL

```
https://www.mandsauruniversity.edu.in:443/departments/bca?year=2026#syllabus
└─┬──┘  └─┬─────────────────────────┘└┬┘ └──────┬──────┘ └───┬───┘ └──┬───┘
Scheme          Host (Domain)        Port    Path         Query    Fragment
```

> **Code Explanation:**
> - **Scheme (`https://`):** The protocol — like choosing whether to send a letter by regular post (HTTP) or registered post (HTTPS — secure and encrypted).
> - **Host (`www.mandsauruniversity.edu.in`):** The domain name of the server — this gets converted to an IP address by DNS. The `.edu.in` tells us it's an Indian educational institution.
> - **Port (`:443`):** The specific "door" on the server to knock on. Port 443 is the default for HTTPS, so you usually don't need to type it — the browser adds it automatically.
> - **Path (`/departments/bca`):** The specific page or resource on the server — like a file path on your computer. This leads to the BCA department's page.
> - **Query String (`?year=2026`):** Extra data sent to the server — here it filters content to show the 2026 academic year.
> - **Fragment (`#syllabus`):** This does NOT go to the server — it tells the browser to scroll down to the section with `id="syllabus"` on the page.

| Component | Example | Purpose |
|-----------|---------|---------|
| **Scheme** | `https://` | Protocol to use |
| **Host** | `www.mandsauruniversity.edu.in` | Which server to contact |
| **Port** | `:443` | Which "door" on the server (443 = HTTPS default) |
| **Path** | `/departments/bca` | Which resource on the server |
| **Query String** | `?year=2026` | Additional parameters |
| **Fragment** | `#syllabus` | Jump to a section on the page |

### Common URL Schemes

| Scheme | Purpose | Default Port |
|--------|---------|-------------|
| `http://` | Regular web traffic | 80 |
| `https://` | Secure web traffic | 443 |
| `ftp://` | File transfer | 21 |
| `mailto:` | Email link | — |
| `file://` | Local file | — |

---

## 6. Client-Server Architecture

### The Request-Response Cycle

```
    CLIENT                              SERVER
  ┌────────┐                         ┌────────┐
  │        │ ─── 1. Request ────────▶│        │
  │Browser │                         │Web     │
  │        │ ◀── 2. Response ────────│Server  │
  │        │                         │        │
  └────────┘                         └────────┘
  
  Request:  "Please give me the homepage"
  Response: "Here's the HTML + CSS + images"
```

> **Code Explanation:**
> - **Step 1 (Request):** The browser (client) sends a message to the server saying "Please give me the homepage." This is an HTTP request — typically a `GET` request.
> - **Step 2 (Response):** The server processes the request, finds the requested files, and sends them back. The response contains everything the browser needs — the HTML structure, CSS for styling, and image files.
> - This is a **one-way-at-a-time** conversation — the client always speaks first (request), and the server always replies (response). The server **never** sends data to the browser without being asked first (in basic HTTP).
> - Every single thing you see on a webpage — every image, every CSS file, every JavaScript file — required a separate request-response cycle. A single webpage might trigger 50+ such cycles!

### What Happens When You Visit a Website

1. **You type** `www.google.com` and press Enter
2. **DNS lookup** — domain name → IP address
3. **TCP connection** — 3-way handshake with the server
4. **HTTP request** — browser sends `GET / HTTP/1.1`
5. **Server processing** — server finds and prepares the page
6. **HTTP response** — server sends back HTML, CSS, JS, images
7. **Browser rendering** — browser builds and displays the page
8. **Connection close** — (or kept alive for more requests)

---

## Summary

| Concept | Key Takeaway |
|---------|-------------|
| WWW | A service running on the internet (not the internet itself) |
| Web Client | Software (browser) that requests and displays web content |
| Web Server | Computer that stores and serves web files |
| URL | Complete address of a web resource |
| Client-Server | Browser sends requests, server sends responses |
| Static vs Dynamic | Static = pre-built files; Dynamic = generated per request |
| DOM | Tree structure the browser builds from HTML — JavaScript uses it to find/change elements |
| Rendering Pipeline | HTML → DOM → CSSOM → Render Tree → Layout → Paint → Composite → Pixels |
| Browser Caching | Browser saves files locally to avoid re-downloading — uses ETag and Cache-Control headers |
| Query Strings | `?key=value` pairs in URLs that send extra data to the server |

---

## Self-Assessment Questions

1. Explain the difference between the Internet and the World Wide Web.
2. What are the three pillars of the WWW?
3. Describe the role of a web browser in displaying a webpage.
4. Break down this URL into its components: `https://shop.example.com:8080/products?category=books#fiction`
5. What is the difference between a static and dynamic web server?
6. List any four popular web browsers and their rendering engines.
7. What is the DOM? Draw the DOM tree for the following HTML: `<html><body><h1>Hello</h1><p>World</p></body></html>`
8. List the six stages of the browser rendering pipeline and explain any two in your own words.
9. Explain how browser caching works. What is the purpose of the `ETag` and `Cache-Control` HTTP headers?
10. What are query string parameters? Decode this URL and identify each parameter: `https://results.example.in/search?student=Priya+Patel&semester=2&year=2026`

---

## Reading for Next Session

Tomorrow we cover **HTTP, HTTPS, Proxy Servers, and Firewalls** — the protocols and security mechanisms that protect web communication.

---

*Day 4 of 55 | Unit 1 — Internet Technology | Web Technology (25BCA060)*
