# Day 5 — HTTP, HTTPS, Proxy Servers & Firewalls

📖 **Type:** Theory Session
🕐 **Duration:** 2 Hours
📚 **Unit:** 1 — Internet Technology

---

## Learning Objectives

By the end of this session, students will be able to:
- Explain the HTTP protocol and its features
- Describe the HTTP request-response model with methods and status codes
- Differentiate between HTTP and HTTPS
- Explain what proxy servers and firewalls do

---

## 1. HTTP — HyperText Transfer Protocol

### What is HTTP?

> **Analogy:** HTTP is like the **language** spoken between a customer (browser) and a waiter (server) in a restaurant. The customer says "I'd like the menu" (GET request), and the waiter brings it. The customer says "I'd like to order butter chicken" (POST request), and the waiter takes the order to the kitchen.

**HTTP** is an application-layer protocol that defines how messages are formatted and transmitted between web clients and servers.

### Features of HTTP

| Feature | Description |
|---------|-------------|
| **Stateless** | Each request is independent — server doesn't remember previous requests |
| **Text-based** | Messages are readable text (not binary) |
| **Request-Response** | Client always initiates; server always responds |
| **Connectionless** | Connection is closed after each request-response (HTTP/1.0) |
| **Media independent** | Can transfer any type of data (HTML, images, video, JSON) |
| **Port** | Uses port 80 by default |

### Understanding Statelessness

> **Analogy:** Imagine a shopkeeper with **amnesia**. Every time you walk into the shop, the shopkeeper greets you as if meeting you for the first time. Even if you visited 5 minutes ago and were halfway through buying groceries, the shopkeeper has no memory of it. **That's HTTP** — every request starts completely fresh.

**Why was HTTP designed stateless?**

- **Simplicity**: The server doesn't need to store information about every connected client
- **Scalability**: Any server in a group can handle any request — no need to remember which server previously talked to which client
- **Reliability**: If a server crashes, no client session data is lost — clients simply reconnect

**The Problem:** If HTTP is stateless, how does a website like Flipkart know you're logged in when you navigate from the homepage to your cart?

The answer: developers use **workarounds** to maintain state on top of the stateless HTTP protocol.

#### State Management Techniques

**1. Cookies**
A cookie is a small piece of data that the **server sends to the browser**, and the browser **sends it back with every subsequent request**. Think of it like a wristband at a Mandsaur mela — once you get it, you show it at every stall.

**2. Sessions**
The server creates a **session** (a temporary record on the server) and gives the client a **session ID** (stored in a cookie). The actual data stays on the server — the client only carries the ID. Think of it like a **cloakroom token** at a wedding hall — you carry a small token, but your belongings are stored safely inside.

**3. Tokens (JWT — JSON Web Token)**
A JWT is a **self-contained** token that carries the user's information inside it (encoded, not encrypted by default). The server doesn't need to store anything — the token itself proves who you are. Think of it like an **Aadhaar card** — it carries your identity details and can be verified without calling a central database every time.

#### Cookies vs Sessions vs Tokens — Comparison

| Feature | Cookies | Sessions | Tokens (JWT) |
|---------|---------|----------|--------------|
| **Stored where?** | Browser | Server (ID in browser cookie) | Browser (localStorage or cookie) |
| **Server memory needed?** | No | Yes (session store) | No |
| **Sent with every request?** | Yes (automatically) | Yes (session ID in cookie) | Yes (manually in `Authorization` header) |
| **Security** | Vulnerable to XSS, CSRF | More secure (data on server) | Vulnerable if not stored securely |
| **Expiry** | Set by server (`Set-Cookie`) | Server-controlled | Encoded inside the token |
| **Scalability** | Good | Poor (server must share session data) | Excellent (no server storage) |
| **Best for** | Preferences, tracking | Traditional web apps (like university portals) | APIs, mobile apps, single-page apps |

---

## 2. HTTP Request-Response Model

### HTTP Request Structure

```
GET /index.html HTTP/1.1          ← Request Line
Host: www.example.com             ← Headers
User-Agent: Chrome/120.0
Accept: text/html
Accept-Language: en-IN
                                  ← Empty line
                                  ← Body (empty for GET)
```

> **Code Explanation:**
> - **`GET /index.html HTTP/1.1`** — This is the **request line**. `GET` is the HTTP method (we want to retrieve data). `/index.html` is the path of the resource on the server. `HTTP/1.1` is the protocol version.
> - **`Host: www.example.com`** — Tells the server *which website* we want. A single server can host multiple websites, so this header is essential.
> - **`User-Agent: Chrome/120.0`** — Identifies the browser/client making the request. Servers use this to send different content to different browsers.
> - **`Accept: text/html`** — Tells the server what type of content the browser can understand. Here, it wants HTML.
> - **`Accept-Language: en-IN`** — Tells the server the preferred language (English, India). Multilingual websites use this to serve regional content.
> - **Empty line** — Separates headers from the body. This is mandatory in HTTP.
> - **Body** — For GET requests, the body is empty. POST/PUT requests include data in the body.

### HTTP Response Structure

```
HTTP/1.1 200 OK                   ← Status Line
Content-Type: text/html           ← Headers
Content-Length: 1234
Date: Sat, 28 Mar 2026 10:00:00 GMT
                                  ← Empty line
<html>                            ← Body (the actual content)
  <body>Hello World!</body>
</html>
```

> **Code Explanation:**
> - **`HTTP/1.1 200 OK`** — This is the **status line**. `HTTP/1.1` is the protocol version. `200` is the status code (success). `OK` is the human-readable reason phrase.
> - **`Content-Type: text/html`** — Tells the browser that the body contains HTML content. Without this, the browser wouldn't know how to display the data.
> - **`Content-Length: 1234`** — The size of the body in bytes. Helps the browser know when it has received the complete response.
> - **`Date: Sat, 28 Mar 2026 10:00:00 GMT`** — The date and time the response was generated on the server.
> - **Empty line** — The mandatory separator between headers and body. Everything after this line is the actual content.
> - **`<html>...</html>`** — The **body** of the response — the actual HTML page the browser will render and display to the user.

### HTTP Methods (Verbs)

> **Restaurant Analogy Continued:**

| Method | Purpose | Restaurant Analogy |
|--------|---------|-------------------|
| **GET** | Retrieve data | "Show me the menu" |
| **POST** | Submit data | "I'd like to place an order" |
| **PUT** | Update/Replace data | "Change my order to paneer" |
| **PATCH** | Partially update data | "Add extra spice to my order" |
| **DELETE** | Remove data | "Cancel my order" |
| **HEAD** | Get headers only (no body) | "Do you serve Chinese food?" (yes/no) |
| **OPTIONS** | Check what methods are allowed | "What services do you offer?" |

### Common HTTP Headers

HTTP headers carry **metadata** about the request or response — think of them as labels on a courier package (sender address, contents description, handling instructions).

| Header | What It Does | Example Value | Sent By |
|--------|-------------|---------------|---------|
| **`Host`** | Specifies which website the request is for | `www.mandsauruniversity.edu.in` | Client |
| **`User-Agent`** | Identifies the browser/client | `Mozilla/5.0 Chrome/120.0` | Client |
| **`Accept`** | What content types the client can handle | `text/html, application/json` | Client |
| **`Content-Type`** | Format of the data in the body | `application/json` | Both |
| **`Content-Length`** | Size of the body in bytes | `348` | Both |
| **`Cache-Control`** | Caching instructions | `max-age=3600, no-cache` | Both |
| **`Authorization`** | Credentials for authentication | `Bearer eyJhbGciOiJIUz...` | Client |
| **`Set-Cookie`** | Server sends a cookie to the browser | `session_id=abc123; Path=/` | Server |
| **`Cookie`** | Browser sends stored cookies back | `session_id=abc123` | Client |
| **`Referer`** | The page that linked to this request | `https://www.google.com/` | Client |
| **`Location`** | URL to redirect the client to | `https://www.example.com/new-page` | Server |

### POST Request Body — Examples

When you submit a form or send data to a server, the data goes in the **request body**. The `Content-Type` header tells the server what format the data is in.

#### Form-Encoded POST (Traditional HTML Forms)

```
POST /register HTTP/1.1
Host: www.mandsauruniversity.edu.in
Content-Type: application/x-www-form-urlencoded
Content-Length: 62

name=Priya+Sharma&email=priya%40example.com&course=BCA&semester=2
```

> **Code Explanation:**
> - **`POST /register HTTP/1.1`** — A POST request to the `/register` path. POST means we are **sending data** to the server.
> - **`Host: www.mandsauruniversity.edu.in`** — The request is going to Mandsaur University's website.
> - **`Content-Type: application/x-www-form-urlencoded`** — The body uses **form encoding**: keys and values are joined with `=`, pairs are separated with `&`, and special characters are percent-encoded (e.g., `@` becomes `%40`, spaces become `+`).
> - **`Content-Length: 62`** — The body is 62 bytes long.
> - **Body** — `name=Priya+Sharma&email=priya%40example.com&course=BCA&semester=2` — The actual form data. This is exactly what a browser sends when you submit an HTML `<form>`.

#### JSON POST (Modern APIs)

```
POST /api/students HTTP/1.1
Host: www.mandsauruniversity.edu.in
Content-Type: application/json
Content-Length: 96

{
  "name": "Priya Sharma",
  "email": "priya@example.com",
  "course": "BCA",
  "semester": 2
}
```

> **Code Explanation:**
> - **`POST /api/students HTTP/1.1`** — A POST request to an API endpoint. APIs commonly use `/api/` prefixed paths.
> - **`Content-Type: application/json`** — The body is in **JSON format** (JavaScript Object Notation) — structured, human-readable, and the standard for modern web APIs.
> - **Body** — A JSON object with key-value pairs. Note: strings use double quotes, numbers don't. JSON is easier to read and parse than form-encoded data.

#### Form-Encoded vs JSON — Comparison

| Feature | Form-Encoded | JSON |
|---------|-------------|------|
| **Content-Type** | `application/x-www-form-urlencoded` | `application/json` |
| **Format** | `key=value&key=value` | `{ "key": "value" }` |
| **Readability** | Hard to read with many fields | Clean and structured |
| **Nested data** | Not supported natively | Supports objects and arrays |
| **Used by** | HTML `<form>` elements | JavaScript `fetch()`, mobile apps, APIs |
| **Special characters** | Must be percent-encoded (`%40`, `+`) | Written naturally (`@`, spaces in quotes) |

### HTTP Status Codes

Status codes tell the client what happened with their request.

| Code Range | Category | Meaning |
|-----------|----------|---------|
| **1xx** | Informational | "Hold on, I'm working on it" |
| **2xx** | Success | "Here you go!" |
| **3xx** | Redirection | "Look somewhere else" |
| **4xx** | Client Error | "You made a mistake" |
| **5xx** | Server Error | "I (server) messed up" |

#### Common Status Codes

| Code | Message | Meaning | When You See It |
|------|---------|---------|-----------------|
| **200** | OK | Request successful | Page loads normally |
| **201** | Created | New resource created | After form submission |
| **301** | Moved Permanently | Page has a new URL forever | Old URL redirects |
| **302** | Found (Temporary Redirect) | Page temporarily at another URL | Login redirects |
| **304** | Not Modified | Use cached version | Browser cache used |
| **400** | Bad Request | Request was malformed | Invalid form data |
| **401** | Unauthorized | Authentication required | Need to log in |
| **403** | Forbidden | You don't have permission | Restricted page |
| **404** | Not Found | Page doesn't exist | Typo in URL |
| **500** | Internal Server Error | Server crashed/bug | Server-side problem |
| **502** | Bad Gateway | Gateway/proxy got bad response | Server overloaded |
| **503** | Service Unavailable | Server temporarily down | Maintenance mode |

---

## 3. HTTP Versions

| Version | Year | Key Features |
|---------|------|-------------|
| **HTTP/0.9** | 1991 | Only GET method, no headers |
| **HTTP/1.0** | 1996 | Headers, status codes, content types |
| **HTTP/1.1** | 1997 | Persistent connections, chunked transfer, host header |
| **HTTP/2** | 2015 | Multiplexing, header compression, server push |
| **HTTP/3** | 2022 | Based on QUIC (UDP), faster connections |

### HTTP/1.1 vs HTTP/2 — Visual Comparison

```
HTTP/1.1 (One at a time):
Browser: ──request1──▶ ◀──response1── ──request2──▶ ◀──response2──

HTTP/2 (Multiplexing):
Browser: ──request1──▶ 
         ──request2──▶  ◀──response1──
         ──request3──▶  ◀──response2──
                        ◀──response3──
```

> **Code Explanation:**
> - **HTTP/1.1** sends requests **one at a time** (sequentially). The browser must wait for `response1` before sending `request2`. This is like a single-lane road — one vehicle must pass before the next can go.
> - **HTTP/2** sends **multiple requests simultaneously** on the same connection (multiplexing). The browser fires off `request1`, `request2`, and `request3` without waiting. Responses arrive as they're ready, possibly out of order. This is like a **multi-lane highway** — all vehicles move in parallel.

### HTTP/2 — Binary Framing & Multiplexing

HTTP/2 introduced several major improvements over HTTP/1.1:

**1. Binary Framing**
HTTP/1.1 sends data as **plain text** (human-readable). HTTP/2 converts everything into **binary frames** (0s and 1s) before sending. Binary is faster for computers to parse, like how a computer processes machine code faster than English.

**2. Multiplexing**
Multiple requests and responses are **interleaved** on a single TCP connection. In HTTP/1.1, if one large file blocks the connection (head-of-line blocking), everything waits. In HTTP/2, different streams share the same connection independently.

```
HTTP/2 Binary Frames on a Single Connection:
┌──────────────────────────────────────────────────┐
│  TCP Connection                                  │
│                                                  │
│  [Frame: Stream 1 HEADERS] [Frame: Stream 2 HEADERS]  │
│  [Frame: Stream 1 DATA]   [Frame: Stream 3 HEADERS]   │
│  [Frame: Stream 2 DATA]   [Frame: Stream 1 DATA]      │
│  [Frame: Stream 3 DATA]   [Frame: Stream 2 DATA]      │
│                                                  │
│  Streams 1, 2, 3 are interleaved on ONE connection│
└──────────────────────────────────────────────────┘
```

**3. Header Compression (HPACK)**
HTTP headers (like `User-Agent`, `Accept`, `Cookie`) are repeated in every request. HTTP/2 uses **HPACK compression** — headers that were sent before are stored in a table and referenced by index instead of being sent again. This saves significant bandwidth.

**4. Server Push**
The server can **proactively send resources** the client hasn't asked for yet. For example, when you request `index.html`, the server knows you'll also need `style.css` and `script.js`, so it pushes them without waiting for separate requests.

### HTTP/3 — The Future of Web Communication

> **Analogy:** TCP is like a **formal phone call** — you dial, wait for the ring, the person answers, you talk. If the call drops, you start all over. **QUIC (used by HTTP/3)** is like sending a **WhatsApp voice note** — instant, works even if you switch from WiFi to mobile data, and you can send multiple notes at the same time.

HTTP/3 replaces the underlying **TCP** protocol with **QUIC** (Quick UDP Internet Connections), which runs over **UDP**.

**Why not TCP?**

TCP requires a **3-way handshake** (SYN → SYN-ACK → ACK) before any data transfer. With TLS, this adds even more round trips. QUIC combines transport and encryption handshakes into **fewer round trips**.

**Key Features of HTTP/3:**

| Feature | Description |
|---------|-------------|
| **QUIC over UDP** | Uses UDP instead of TCP for faster connection setup |
| **0-RTT Connections** | On reconnection, data can be sent immediately without a handshake — like resuming a paused conversation |
| **No Head-of-Line Blocking** | In TCP, if one packet is lost, all streams wait. In QUIC, only the affected stream pauses |
| **Connection Migration** | If you switch from WiFi to mobile data, the connection survives — TCP connections break on network change |
| **Built-in Encryption** | TLS 1.3 is mandatory and integrated — always secure by default |

#### HTTP/1.1 vs HTTP/2 vs HTTP/3 — Comparison

| Feature | HTTP/1.1 | HTTP/2 | HTTP/3 |
|---------|----------|--------|--------|
| **Year** | 1997 | 2015 | 2022 |
| **Transport** | TCP | TCP | QUIC (UDP) |
| **Format** | Text-based | Binary frames | Binary frames |
| **Multiplexing** | ❌ No | ✅ Yes | ✅ Yes |
| **Header Compression** | ❌ No | ✅ HPACK | ✅ QPACK |
| **Server Push** | ❌ No | ✅ Yes | ✅ Yes |
| **Encryption** | Optional | Optional (but usually HTTPS) | ✅ Always (TLS 1.3 built-in) |
| **Head-of-Line Blocking** | Yes (per connection) | Yes (at TCP level) | ❌ No (per stream) |
| **Connection Setup** | 1-3 RTT | 1-3 RTT | 0-1 RTT |
| **Used by** | Legacy websites | Most modern websites | Google, YouTube, Cloudflare |

---

## 4. HTTPS — HyperText Transfer Protocol Secure

### What is HTTPS?

> **Analogy:** HTTP is like sending a **postcard** — anyone handling it can read the message. HTTPS is like sending a **sealed, locked envelope** — only the recipient has the key to open it.

**HTTPS** = HTTP + **TLS/SSL** encryption

| Feature | HTTP | HTTPS |
|---------|------|-------|
| **Full Form** | HyperText Transfer Protocol | HyperText Transfer Protocol Secure |
| **Port** | 80 | 443 |
| **Encryption** | None (plaintext) | TLS/SSL encrypted |
| **URL** | `http://` | `https://` |
| **Security** | Data can be intercepted | Data is encrypted end-to-end |
| **Certificate** | Not required | Requires SSL/TLS certificate |
| **Speed** | Slightly faster | Slightly slower (encryption overhead) |
| **SEO** | Not preferred | Preferred by Google |
| **Browser** | "Not Secure" warning | Lock icon (🔒) shown |

### How HTTPS Works (TLS Handshake)

```
Browser                                  Server
   │                                       │
   │────── ClientHello ───────────────────▶│  "I support these encryption methods"
   │                                       │
   │◀───── ServerHello + Certificate ──────│  "Let's use this one. Here's my ID."
   │                                       │
   │  (Browser verifies certificate        │
   │   with Certificate Authority)         │
   │                                       │
   │────── Key Exchange ──────────────────▶│  "Here's a shared secret (encrypted)"
   │                                       │
   │◀───── Finished ──────────────────────│  "Got it. Encryption active!"
   │                                       │
   │◀═══ ENCRYPTED DATA TRANSFER ═════════▶│
```

> **Code Explanation:**
> - **ClientHello** — The browser initiates the handshake by telling the server: "Here are the encryption methods I support (e.g., AES-256, ChaCha20)." It also sends a random number used later for key generation.
> - **ServerHello + Certificate** — The server picks an encryption method and sends its **digital certificate** (containing the server's public key and identity, issued by a Certificate Authority).
> - **Browser Verifies Certificate** — The browser checks: Is this certificate valid? Is it issued by a trusted CA? Does it match the domain name? If verification fails, you see the "Your connection is not private" warning.
> - **Key Exchange** — The browser generates a **pre-master secret**, encrypts it with the server's public key, and sends it. Both sides now derive the same **session key** for symmetric encryption.
> - **Finished** — Both sides confirm encryption is active. From this point, all data is encrypted with the shared session key — fast symmetric encryption (not slow public-key encryption).

### SSL/TLS Certificates

- Issued by **Certificate Authorities (CAs)** like Let's Encrypt, DigiCert, Comodo
- Verify that a website is who it claims to be
- **Let's Encrypt** provides free certificates
- Certificates must be renewed periodically

### TLS Versions

Not all encryption protocols are equally secure. Older versions have known vulnerabilities and should not be used.

| Version | Year | Status | Notes |
|---------|------|--------|-------|
| **SSL 2.0** | 1995 | ❌ Deprecated | Severely broken — never use |
| **SSL 3.0** | 1996 | ❌ Deprecated | Vulnerable to POODLE attack |
| **TLS 1.0** | 1999 | ❌ Deprecated | Known vulnerabilities, removed by most browsers |
| **TLS 1.1** | 2006 | ❌ Deprecated | Also removed by most browsers since 2020 |
| **TLS 1.2** | 2008 | ✅ Widely used | Currently the most common version on the web |
| **TLS 1.3** | 2018 | ✅ Latest & fastest | Fewer round trips, stronger security, no legacy algorithms |

#### TLS 1.2 vs TLS 1.3 — Comparison

| Feature | TLS 1.2 | TLS 1.3 |
|---------|---------|---------|
| **Handshake round trips** | 2 RTT (two back-and-forth exchanges) | 1 RTT (one exchange) |
| **0-RTT resumption** | ❌ Not supported | ✅ Supported (instant reconnection) |
| **Weak algorithms removed** | Still allows some (e.g., RC4, SHA-1) | ❌ Removed all weak algorithms |
| **Forward secrecy** | Optional | ✅ Mandatory (past sessions can't be decrypted even if key is leaked) |
| **Speed** | Slower handshake | Faster handshake |
| **Adoption** | Universal | Growing rapidly (supported by all modern browsers) |

> **Note for students:** When you visit any `https://` website today, your browser is most likely using TLS 1.2 or TLS 1.3. You can check this in Chrome DevTools → Security tab.

---

## 5. Proxy Servers

### What is a Proxy Server?

> **Analogy:** A proxy server is like a **personal assistant** who makes calls on your behalf. When you want to call someone, your assistant dials the number, talks to the person, and gives you the message. The person on the other end only knows your assistant's number, not yours.

A **proxy server** acts as an intermediary between a client and a server.

```
Without Proxy:
Client ──────────────────────────▶ Server

With Proxy:
Client ──────▶ Proxy Server ──────▶ Server
Client ◀────── Proxy Server ◀────── Server
```

### Types of Proxy Servers

| Type | Direction | Purpose |
|------|-----------|---------|
| **Forward Proxy** | Client → Proxy → Server | Hides client identity, content filtering |
| **Reverse Proxy** | Client → Proxy → Server(s) | Load balancing, caching, security |
| **Transparent Proxy** | Client → Proxy → Server | Monitoring without client's knowledge |

### Benefits of Proxy Servers

| Benefit | Description |
|---------|-------------|
| **Privacy/Anonymity** | Hides client's real IP address |
| **Content Filtering** | Block certain websites (e.g., in schools/offices) |
| **Caching** | Store copies of frequently accessed pages for faster loading |
| **Load Balancing** | Distribute requests across multiple servers |
| **Logging/Monitoring** | Track internet usage |

### Real-World Example

> In your college computer lab, the network likely uses a **proxy server** that:
> - Blocks social media sites during class hours
> - Caches frequently accessed educational sites for faster access
> - Logs which sites are visited

---

## 6. Firewalls

### What is a Firewall?

> **Analogy:** A firewall is like a **security guard at a building entrance**. The guard has a list of who is allowed in and who is not. Every person (data packet) trying to enter must pass the guard's checks. Suspicious persons are turned away.

A **firewall** is a network security system that monitors and controls incoming and outgoing network traffic based on predefined security rules.

```
 Internet                Firewall               Internal Network
┌────────┐          ┌──────────────┐          ┌────────────────┐
│Allowed │──────────│              │──────────│                │
│Traffic │    ✅    │   Security   │    ✅    │  Your Devices  │
│        │──────────│    Rules     │──────────│                │
└────────┘          │              │          └────────────────┘
┌────────┐          │              │
│Blocked │───── ✖ ──│              │
│Traffic │          └──────────────┘
│(Hackers│
│ Malware│
│ etc.)  │
└────────┘
```

### Types of Firewalls

| Type | How It Works | Analogy |
|------|-------------|---------|
| **Packet-Filtering** | Checks each packet's header (source, destination, port) | Guard checks ID cards |
| **Stateful Inspection** | Tracks active connections, allows related packets | Guard remembers who came in and expects their return |
| **Application-Level** | Inspects packet content (not just headers) | Guard opens bags and checks contents |
| **Next-Gen (NGFW)** | Deep packet inspection + intrusion prevention | Guard with X-ray scanner + threat database |

### Firewall Rules — Examples

| Rule | Action | Description |
|------|--------|-------------|
| Allow port 80 inbound | ✅ ALLOW | Let web traffic in |
| Allow port 443 inbound | ✅ ALLOW | Let HTTPS traffic in |
| Block port 23 inbound | ❌ BLOCK | No Telnet (insecure) |
| Allow port 22 from admin IP | ✅ ALLOW | SSH only from trusted IP |
| Block all other inbound | ❌ BLOCK | Default deny |

### Software vs Hardware Firewalls

| Feature | Software Firewall | Hardware Firewall |
|---------|-------------------|-------------------|
| **Location** | Installed on individual device | Standalone device on network |
| **Example** | Windows Defender Firewall | Cisco ASA, pfSense |
| **Protection** | Single device | Entire network |
| **Cost** | Usually free (built into OS) | Can be expensive |

### Stateful vs Stateless Firewalls

> **Analogy:** A **stateless guard** checks every person's ID card every single time — even if they just stepped out for a minute. A **stateful guard** remembers faces and knows: "This person entered 5 minutes ago, they're on their way back — let them through."

| Feature | Stateless Firewall | Stateful Firewall |
|---------|-------------------|-------------------|
| **How it works** | Checks each packet individually based on rules | Tracks active connections, knows if a packet is part of an established session |
| **Memory** | No memory of previous packets | Maintains a connection state table |
| **Speed** | Faster (less processing per packet) | Slightly slower (must look up connection table) |
| **Security** | Basic — can be tricked by crafted packets | Strong — understands context of traffic |
| **Example** | Simple router ACLs (Access Control Lists) | Windows Defender Firewall, Cisco ASA |
| **Best for** | High-speed environments with simple needs | Most networks that need real security |

### How a Stateful Firewall Tracks Connections

When you visit a website, the firewall creates a **temporary entry** in its connection table to allow the response back in.

```
Connection Table (Stateful Firewall)
┌─────────────┬───────────────┬─────────────┬───────────────┬──────────┐
│ Source IP    │ Dest IP       │ Source Port │ Dest Port     │ State    │
├─────────────┼───────────────┼─────────────┼───────────────┼──────────┤
│ 192.168.1.5 │ 93.184.216.34 │ 52431       │ 443 (HTTPS)   │ ESTABLISHED │
│ 192.168.1.8 │ 142.250.77.4  │ 49872       │ 80 (HTTP)     │ ESTABLISHED │
│ 10.0.0.3    │ 104.26.10.33  │ 55100       │ 443 (HTTPS)   │ TIME_WAIT   │
└─────────────┴───────────────┴─────────────┴───────────────┴──────────┘

When you request https://www.google.com:
1. Browser sends packet: 192.168.1.5:52431 → 142.250.77.4:443
2. Firewall creates entry in connection table (state: NEW → ESTABLISHED)
3. Google's response: 142.250.77.4:443 → 192.168.1.5:52431
4. Firewall checks table: "This matches an active connection — ALLOW"
5. Connection closes → entry removed from table
```

> **Code Explanation:**
> - The connection table stores **5 key fields** for each active connection: source IP, destination IP, source port, destination port, and connection state.
> - **ESTABLISHED** means the connection is active and packets are flowing in both directions.
> - **TIME_WAIT** means the connection is closing — the firewall keeps the entry briefly in case any remaining packets arrive.
> - If an incoming packet does **not** match any entry in the connection table and no rule allows it, the firewall **blocks** it. This is how stateful firewalls prevent unsolicited incoming traffic.

### NAT vs Firewall — They Are NOT the Same

> **Analogy:** **NAT** is like a **receptionist** at an office who redirects calls — callers only know the office's main number, not individual extensions. But the receptionist doesn't check if the caller is dangerous. A **firewall** is the **security guard** who actually inspects visitors before letting them in.

**NAT (Network Address Translation)** translates **private IP addresses** (like `192.168.1.x`) to a **public IP address** when accessing the internet. This was invented because the world ran out of IPv4 addresses — NAT lets hundreds of devices share one public IP.

**Common misconception:** "NAT provides security because it hides internal IPs."

NAT **hides** your internal network structure, but it does **not inspect or block** malicious traffic. It simply translates addresses. A firewall actively examines packets and enforces security rules.

| Feature | NAT | Firewall |
|---------|-----|----------|
| **Primary purpose** | Address translation (private ↔ public IP) | Security (inspect and block traffic) |
| **Inspects packet content?** | ❌ No | ✅ Yes |
| **Blocks malicious traffic?** | ❌ No (just translates) | ✅ Yes (based on rules) |
| **Hides internal IPs?** | ✅ Yes (side effect) | Not its job (but can) |
| **Example** | Your home WiFi router translates `192.168.1.5` → your ISP-assigned public IP | Windows Defender Firewall blocks suspicious incoming connections |
| **Analogy** | Receptionist redirecting calls | Security guard checking visitors |

---

## Summary

| Concept | Key Takeaway |
|---------|-------------|
| HTTP | Text-based, stateless protocol for web communication (port 80) |
| Cookies/Sessions/Tokens | Workarounds to maintain state over stateless HTTP — cookies (browser), sessions (server), JWT (self-contained) |
| HTTP Headers | Metadata labels on requests/responses — `Host`, `Content-Type`, `Authorization`, `Cookie`, etc. |
| HTTP Methods | GET (read), POST (create), PUT (update), DELETE (remove) |
| Status Codes | 2xx = success, 4xx = client error, 5xx = server error |
| HTTP/2 | Binary framing, multiplexing, header compression, server push |
| HTTP/3 & QUIC | Uses UDP instead of TCP — 0-RTT connections, no head-of-line blocking, connection migration |
| HTTPS | HTTP + encryption (TLS/SSL) — secure communication (port 443) |
| TLS Versions | TLS 1.2 (widely used) and TLS 1.3 (latest, fastest) — older versions are deprecated |
| Proxy Server | Intermediary between client and server — privacy, caching, filtering |
| Firewall | Security guard for network traffic — allows or blocks based on rules |
| Stateful Firewall | Tracks active connections — smarter than stateless firewalls that check packets individually |
| NAT | Translates private IPs to public IPs — NOT a security tool (unlike a firewall) |

---

## Self-Assessment Questions

1. What does "stateless" mean in the context of HTTP?
2. What HTTP method would you use to submit a login form? Why?
3. What status code would a server return if the requested page doesn't exist?
4. Explain the difference between HTTP and HTTPS with a real-world analogy.
5. What is the role of a proxy server in a college network?
6. How does a firewall protect a network from unauthorized access?
7. You see a "502 Bad Gateway" error — what might have gone wrong?
8. Compare cookies, sessions, and tokens (JWT) for maintaining user login state. Which would you choose for a mobile app and why?
9. What does the `Content-Type` header tell the server? Give two different values it can have and when each is used.
10. How does HTTP/3 solve the head-of-line blocking problem that exists in HTTP/2?
11. What is the key difference between TLS 1.2 and TLS 1.3 in terms of handshake speed?
12. Explain the difference between a stateful and stateless firewall with a real-world analogy.
13. Your friend says "My home router uses NAT, so I don't need a firewall." Is this correct? Explain why or why not.

---

## What's Next?

Unit 1 is complete! Starting **Day 6 (30 March)**, we begin **Unit 2: HTML Fundamentals** — where you'll write your very first web page. Make sure you have a text editor (VS Code recommended) and a web browser (Chrome) installed.

### Software to Install Before Day 6

| Software | Download Link | Purpose |
|----------|---------------|---------|
| **VS Code** | https://code.visualstudio.com | Code editor |
| **Google Chrome** | https://www.google.com/chrome | Web browser |
| **Git** | https://git-scm.com | Version control |

---

*Day 5 of 55 | Unit 1 — Internet Technology | Web Technology (25BCA060)*
