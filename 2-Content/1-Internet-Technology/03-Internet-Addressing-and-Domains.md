# Day 3 — Internet Addressing & Domain Name System

📖 **Type:** Theory Session
🕐 **Duration:** 2 Hours
📚 **Unit:** 1 — Internet Technology

---

## Learning Objectives

By the end of this session, students will be able to:
- Explain IPv4 and IPv6 addressing schemes
- Classify IP addresses into different classes
- Understand subnet masks and their purpose
- Describe how the Domain Name System (DNS) works
- Differentiate between different types of domain names

---

## 1. IP Addresses

### What is an IP Address?

> **Real-World Analogy:** Just as every house has a unique postal address so the postman knows where to deliver mail, every device on the internet has a unique **IP address** so data packets know where to go.

An **IP Address** (Internet Protocol Address) is a unique numerical label assigned to every device connected to a network that uses the Internet Protocol for communication.

### IPv4 Addresses

**Format:** Four numbers separated by dots, each ranging from 0 to 255.

```
Example: 192.168.1.100

  192    .   168    .    1     .   100
  └─┘        └─┘        └─┘       └─┘
 8 bits    8 bits     8 bits    8 bits
           
           Total = 32 bits
```

> **Code Explanation:**
> - An IPv4 address has **4 octets** (groups), each 8 bits long, separated by dots
> - Each octet can hold values from **0 to 255** (since 2⁸ = 256 possible values)
> - In the example `192.168.1.100`: the first three octets (192.168.1) typically identify the **network**, and the last octet (100) identifies the specific **device** (host) on that network
> - 32 bits total gives us 2³² ≈ 4.3 billion possible addresses

**Total IPv4 addresses:** 2³² = **4,294,967,296** (about 4.3 billion)

### IPv4 Address Classes

| Class | Range | Default Subnet Mask | Networks | Hosts per Network | Purpose |
|-------|-------|--------------------|---------|--------------------|---------|
| **A** | 1.0.0.0 – 126.255.255.255 | 255.0.0.0 | 126 | ~16 million | Very large organizations |
| **B** | 128.0.0.0 – 191.255.255.255 | 255.255.0.0 | 16,384 | ~65,000 | Medium organizations |
| **C** | 192.0.0.0 – 223.255.255.255 | 255.255.255.0 | ~2 million | 254 | Small networks |
| **D** | 224.0.0.0 – 239.255.255.255 | — | — | — | Multicasting |
| **E** | 240.0.0.0 – 255.255.255.255 | — | — | — | Experimental/Research |

### Special IP Addresses

| Address | Purpose |
|---------|---------|
| `127.0.0.1` | Loopback (localhost) — your own computer |
| `192.168.x.x` | Private network (home/office Wi-Fi) |
| `10.x.x.x` | Private network (large organizations) |
| `172.16.x.x – 172.31.x.x` | Private network (medium organizations) |
| `0.0.0.0` | Default route / "any address" |
| `255.255.255.255` | Broadcast to all devices on network |

### IPv6 Addresses

> IPv4 only has ~4.3 billion addresses. With billions of phones, laptops, smart TVs, IoT devices — we ran out! IPv6 solves this.

**Format:** Eight groups of four hexadecimal digits, separated by colons.

```
Example: 2001:0db8:85a3:0000:0000:8a2e:0370:7334

Simplified: 2001:db8:85a3::8a2e:370:7334
(Leading zeros dropped, consecutive zero groups replaced with ::)
```

**Total IPv6 addresses:** 2¹²⁸ = approximately 340 undecillion (340 × 10³⁶)

| Feature | IPv4 | IPv6 |
|---------|------|------|
| **Bits** | 32 | 128 |
| **Format** | Decimal (192.168.1.1) | Hexadecimal (2001:db8::1) |
| **Total addresses** | ~4.3 billion | ~340 undecillion |
| **Example** | 192.168.1.1 | 2001:0db8:85a3::7334 |

### IPv6 Adoption — Why Hasn't It Fully Replaced IPv4?

Despite IPv4 running out of addresses, IPv6 adoption has been **slow**. As of 2024, only about **40-45%** of global internet traffic uses IPv6. Here's why:

| Challenge | Explanation |
|-----------|-------------|
| **NAT saved IPv4** | NAT allows millions of devices to share one public IP, delaying the urgency to switch |
| **Cost of upgrading** | Every router, firewall, and server needs to support IPv6 — expensive for ISPs and companies |
| **Compatibility** | IPv4 and IPv6 are **not directly compatible** — they can't talk to each other without translation |
| **"It works fine"** | Most users don't feel the pain of IPv4 exhaustion because NAT hides the problem |
| **Training needed** | Network engineers need to learn new addressing, subnetting, and configuration for IPv6 |

**How the Transition Works:**

| Method | How It Works |
|--------|-------------|
| **Dual-Stack** | Devices run **both** IPv4 and IPv6 simultaneously. Most modern phones and laptops already do this. Your Jio connection likely supports both! |
| **Tunneling** | IPv6 packets are wrapped inside IPv4 packets to travel through IPv4-only networks — like putting a Hindi letter inside an English envelope so the English-only post office can deliver it |
| **Translation (NAT64)** | A translator sits between IPv4 and IPv6 networks, converting addresses on the fly |

> **Indian Context:** India is actually one of the **top IPv6 adopters** in the world! Reliance Jio launched with IPv6-first infrastructure, and Jio users account for a large share of global IPv6 traffic. Airtel and BSNL are also rolling out IPv6 support.

---

## 2. Subnet Masks

### What is a Subnet Mask?

> **Analogy:** Think of a city with sectors. The city name tells you the general area (network), and the sector number tells you the exact location (host). A **subnet mask** defines where the "city" part ends and the "sector" part begins.

A subnet mask separates an IP address into two parts:
- **Network portion** — identifies which network the device belongs to
- **Host portion** — identifies the specific device on that network

```
IP Address:    192.168.1.100
Subnet Mask:   255.255.255.0
               └────────┘ └─┘
               Network    Host
               
Network ID:    192.168.1.0   (the "street")
Host ID:       100            (the "house number")
```

> **Code Explanation:**
> - The subnet mask `255.255.255.0` in binary is `11111111.11111111.11111111.00000000`
> - Where the mask has **1s** → that part of the IP is the **network address** (which network you're on)
> - Where the mask has **0s** → that part of the IP is the **host address** (which specific device you are)
> - So `192.168.1` is the network (like "Mandsaur, Sector 5"), and `100` is the specific device (like "House #100")

### Common Subnet Masks

| CIDR Notation | Subnet Mask | Hosts Available |
|--------------|-------------|-----------------|
| /8 | 255.0.0.0 | 16,777,214 |
| /16 | 255.255.0.0 | 65,534 |
| /24 | 255.255.255.0 | 254 |
| /28 | 255.255.255.240 | 14 |

### Subnet Calculation Walkthrough

Let's solve a practical example step by step:

**Question:** What are the usable IP addresses in the network `192.168.1.0/24`?

**Step 1: Understand the /24**
- `/24` means the first 24 bits are the **network portion** and the remaining 8 bits are the **host portion**
- Subnet mask: `255.255.255.0` (24 ones followed by 8 zeros in binary)

**Step 2: Calculate the number of addresses**
- Host bits = 32 − 24 = **8 bits**
- Total addresses = 2⁸ = **256**
- Usable host addresses = 256 − 2 = **254** (subtract network address and broadcast address)

**Step 3: Identify key addresses**

| Address | Type | Purpose |
|---------|------|---------|
| `192.168.1.0` | Network Address | Identifies the network itself — **cannot be assigned to a device** |
| `192.168.1.1` to `192.168.1.254` | Usable Host Addresses | **254 devices** can use these IPs |
| `192.168.1.255` | Broadcast Address | Sends data to ALL devices on this network — **cannot be assigned** |

**Another Example:** What about `10.0.0.0/28`?

| Step | Calculation |
|------|-------------|
| Host bits | 32 − 28 = **4 bits** |
| Total addresses | 2⁴ = **16** |
| Usable hosts | 16 − 2 = **14** |
| Network address | `10.0.0.0` |
| First usable | `10.0.0.1` |
| Last usable | `10.0.0.14` |
| Broadcast | `10.0.0.15` |

> **Quick Formula:** For any `/n` network:
> - Total addresses = 2^(32−n)
> - Usable hosts = 2^(32−n) − 2

### Why CIDR Replaced Classful Addressing

The old **classful** system (Class A, B, C) was extremely wasteful:

| Scenario | Classful Approach | CIDR Approach |
|----------|------------------|---------------|
| A school needs 300 IPs | Must take a Class B (65,534 IPs) → **65,234 IPs wasted!** | Use /23 (510 IPs) → Only 210 wasted |
| An office needs 20 IPs | Must take a Class C (254 IPs) → **234 IPs wasted!** | Use /27 (30 IPs) → Only 10 wasted |
| A small shop needs 5 IPs | Must take a Class C (254 IPs) → **249 IPs wasted!** | Use /29 (6 IPs) → Only 1 wasted |

> **Analogy:** Classful addressing is like buying land only in 3 sizes: 1 acre, 100 acres, or 10,000 acres. If you need 50 acres, you must buy 100 and waste 50. **CIDR** lets you buy exactly 50 acres — no waste. This is why CIDR (Classless Inter-Domain Routing) replaced classful addressing in the mid-1990s.

---

## 3. Domain Name System (DNS)

### The Problem

Humans are good at remembering names, computers are good at remembering numbers:
- Human-friendly: `www.google.com`
- Computer-friendly: `142.250.195.68`

### What is DNS?

> **Analogy:** DNS is like a **phone book** for the internet. You know a person's name (domain), and the phone book gives you their number (IP address).

**DNS** (Domain Name System) translates human-readable domain names into IP addresses that computers can understand.

### How DNS Works — Step by Step

```
You type: www.mandsauruniversity.com

Step 1: Browser checks its cache → "Do I already know this?"
            │ No
            ▼
Step 2: OS checks its cache → "Has the computer looked this up before?"
            │ No
            ▼
Step 3: Query goes to Recursive DNS Resolver (your ISP's DNS)
            │ "I don't know, let me ask..."
            ▼
Step 4: Asks Root DNS Server → "Who handles .com?"
            │ "Try the .com TLD server"
            ▼
Step 5: Asks .com TLD Server → "Who handles mandsauruniversity.com?"
            │ "Try ns1.hosting-provider.com"
            ▼
Step 6: Asks Authoritative DNS Server for mandsauruniversity.com
            │ "The IP is 103.45.67.89"
            ▼
Step 7: IP address returned to your browser
            │
            ▼
Step 8: Browser connects to 103.45.67.89 and loads the website!
```

> **Code Explanation:**
> - **Steps 1-2 (Cache checks):** Before asking anyone, the system checks if it already knows the answer — like checking your phone contacts before calling directory enquiry
> - **Step 3 (Recursive Resolver):** Your ISP's DNS server does the hard work of asking around on your behalf — like a helpful librarian who finds the book for you
> - **Steps 4-6 (Hierarchical queries):** DNS uses a tree structure — Root → TLD → Authoritative — narrowing down with each step, like asking "Which country?" → "Which city?" → "Which street?"
> - **Steps 7-8:** The IP address is returned, and your browser can finally connect to the website

### DNS Caching — Why Websites Load Faster the Second Time

DNS lookups go through **multiple cache layers** before querying the actual DNS servers. Each layer saves (caches) results to speed up future requests:

```
You type: www.flipkart.com

Layer 1: Browser Cache ──────▶ "I looked this up 2 minutes ago! IP is 163.53.78.1"
         (Chrome/Firefox)        ✅ Cache HIT → No further lookup needed!
              │ MISS
              ▼
Layer 2: OS Cache ───────────▶ "Another app looked this up recently!"
         (Windows/Mac DNS)       ✅ Cache HIT → Return immediately
              │ MISS
              ▼
Layer 3: Router Cache ───────▶ "Someone on this Wi-Fi looked this up!"
         (Home/Office Router)    ✅ Cache HIT → Return immediately
              │ MISS
              ▼
Layer 4: ISP DNS Cache ──────▶ "One of my millions of users looked this up!"
         (Jio/Airtel DNS)       ✅ Cache HIT → Return immediately
              │ MISS
              ▼
Layer 5: Full DNS Resolution ▶ Root → TLD → Authoritative Server
         (Slowest — 50-200ms)    Returns fresh result + caches it
```

> **Code Explanation:**
> - Each layer checks if it has a **cached (saved) copy** of the IP address before asking the next layer
> - **TTL (Time to Live):** Each DNS record has a TTL value (e.g., 300 seconds = 5 minutes). Once the TTL expires, the cached entry is deleted and a fresh lookup is required
> - **Why this matters:** The first visit to `www.flipkart.com` might take 100ms for DNS. The second visit (within TTL) takes **less than 1ms** because the browser cache already has the answer
> - **You can see your OS DNS cache** by running `ipconfig /displaydns` in Windows Command Prompt

### DNS Record Types

| Record Type | Purpose | Example |
|-------------|---------|---------|
| **A** | Maps domain to IPv4 address | `google.com → 142.250.195.68` |
| **AAAA** | Maps domain to IPv6 address | `google.com → 2404:6800:4009:...` |
| **CNAME** | Alias for another domain | `www.example.com → example.com` |
| **MX** | Mail server for the domain | `example.com → mail.example.com` |
| **NS** | Nameserver for the domain | `example.com → ns1.provider.com` |
| **TXT** | Text records (verification, etc.) | SPF, DKIM records for email |

### DNS Record Types — In Detail

**A Record vs CNAME Record — What's the Difference?**

| Feature | A Record | CNAME Record |
|---------|----------|-------------|
| **Maps to** | An actual IP address | Another domain name (alias) |
| **Example** | `mandsauruniversity.edu.in → 103.45.67.89` | `www.mandsauruniversity.edu.in → mandsauruniversity.edu.in` |
| **When to use** | For the "root" domain | For subdomains that point to the same place |
| **Analogy** | Your actual home address | A nickname that redirects to your home address |

> **Practical Example:** When you type `www.google.com`, the DNS first finds a CNAME record saying "`www.google.com` is an alias for `google.com`", then finds an A record saying "`google.com` has the IP `142.250.195.68`".

**How MX Records Work (Email Delivery):**

When you send an email to `student@mandsauruniversity.edu.in`, here's what happens:

```
1. Your email server asks: "Where should I deliver mail for mandsauruniversity.edu.in?"

2. DNS returns MX records:
   ┌──────────────────────────────────────────────────────┐
   │ MX Record               │ Priority │ Mail Server     │
   ├─────────────────────────┼──────────┼─────────────────┤
   │ mandsauruniversity.edu.in│    10    │ mail1.host.com  │  ← Try first
   │ mandsauruniversity.edu.in│    20    │ mail2.host.com  │  ← Backup
   └──────────────────────────┴──────────┴─────────────────┘

3. Your server connects to mail1.host.com (priority 10 = highest priority)
4. If mail1 is down, it tries mail2.host.com (priority 20 = backup)
```

> **Code Explanation:**
> - **MX records** tell email servers which mail server handles emails for a domain
> - **Priority** is a number — **lower = higher priority**. So priority 10 is tried before priority 20
> - This is like having a primary phone number and a backup number — if the first doesn't work, try the second
> - Without MX records, nobody could send you emails at your domain!

---

## 4. Domain Names

### Structure of a Domain Name

```
    https://www.mandsauruniversity.edu.in/admissions
    └─┬──┘ └┬┘ └───────┬──────────┘└┬─┘└┬┘ └────┬───┘
   Scheme  Sub  Second-Level Domain TLD ccTLD  Path
          domain                          
```

> **Code Explanation:**
> - **Scheme** (`https://`): The protocol used — HTTPS means the connection is encrypted (secure)
> - **Subdomain** (`www`): A subdivision of the main domain. Other examples: `mail.google.com`, `drive.google.com`
> - **Second-Level Domain** (`mandsauruniversity`): The actual name you register — this is your identity on the web
> - **TLD** (`.edu`): Top-Level Domain indicating the category — `.edu` means education
> - **ccTLD** (`.in`): Country Code TLD indicating the country — `.in` means India
> - **Path** (`/admissions`): The specific page or resource on the website

| Part | Example | Purpose |
|------|---------|---------|
| **Scheme/Protocol** | `https://` | How to communicate |
| **Subdomain** | `www` | Specific service of the domain |
| **Second-Level Domain** | `mandsauruniversity` | The actual name you registered |
| **TLD** (Top-Level Domain) | `.edu` | Category of the website |
| **ccTLD** (Country Code) | `.in` | Country (India) |

### Types of Top-Level Domains (TLDs)

| Type | Examples | Purpose |
|------|----------|---------|
| **gTLD** (Generic) | .com, .org, .net | General purpose |
| **ccTLD** (Country Code) | .in (India), .uk (UK), .jp (Japan) | Country-specific |
| **sTLD** (Sponsored) | .edu (education), .gov (government) | Specific communities |
| **New gTLDs** | .tech, .xyz, .ai, .io | Modern/niche purposes |

### Domain Registration

Domains are registered through **domain registrars** like:
- GoDaddy
- Namecheap
- Google Domains
- Hostinger

**ICANN** (Internet Corporation for Assigned Names and Numbers) manages the global DNS system.

---

## 5. Public vs Private IP Addresses

| Feature | Public IP | Private IP |
|---------|-----------|------------|
| **Scope** | Globally unique, accessible from anywhere | Unique within local network only |
| **Assigned by** | ISP | Router (via DHCP) |
| **Example** | 203.110.245.34 | 192.168.1.100 |
| **Analogy** | Your building's street address | Your apartment number inside the building |

### NAT (Network Address Translation)

> **Analogy:** A company has one phone number (public IP), but many extensions inside (private IPs). When someone calls, the receptionist (NAT) routes the call to the right extension.

NAT allows multiple devices on a private network to share a single public IP address.

### How NAT Actually Works — Port Mapping

NAT doesn't just translate addresses — it maintains a **translation table** to track which internal device sent which request, so return traffic goes to the right device.

```
Inside Your Home Network:                    Internet:
┌──────────────────────┐    ┌──────────┐    ┌───────────────┐
│ Ravi's Phone         │    │          │    │               │
│ 192.168.1.10:5001  ──┼──▶│          │    │               │
│                      │    │  Router  │    │  Google       │
│ Priya's Laptop       │    │  (NAT)   │──▶│  142.250.1.1  │
│ 192.168.1.11:5002  ──┼──▶│          │    │               │
│                      │    │ Public IP│    │               │
│ Dad's PC             │    │ 203.0.5.1│    │               │
│ 192.168.1.12:5003  ──┼──▶│          │    │               │
└──────────────────────┘    └──────────┘    └───────────────┘
```

**NAT Translation Table (inside the router):**

| Internal (Private) | External (Public) | Destination | Notes |
|-------------------|-------------------|-------------|-------|
| 192.168.1.10:5001 | 203.0.5.1:**40001** | 142.250.1.1:443 | Ravi's phone → Google |
| 192.168.1.11:5002 | 203.0.5.1:**40002** | 142.250.1.1:443 | Priya's laptop → Google |
| 192.168.1.12:5003 | 203.0.5.1:**40003** | 142.250.1.1:443 | Dad's PC → Google |

> **Code Explanation:**
> - All three devices (Ravi's phone, Priya's laptop, Dad's PC) have **private IPs** that are invisible to the outside world
> - The router replaces each device's private IP with its own **public IP** (203.0.5.1) but uses a **different port number** for each device (40001, 40002, 40003)
> - When Google sends a response back to `203.0.5.1:40001`, the router checks its translation table and forwards the data to **Ravi's phone** (192.168.1.10)
> - When a response comes to `203.0.5.1:40002`, it goes to **Priya's laptop** — the port number is the key to routing correctly
> - This is how your entire family can browse the internet simultaneously using just **one public IP address** from Jio/Airtel
> - **Why NAT matters:** Without NAT, every device would need its own public IPv4 address. With only 4.3 billion IPv4 addresses and billions of devices worldwide, we would have run out of addresses much sooner

---

## Summary

| Concept | Key Takeaway |
|---------|-------------|
| IPv4 | 32-bit address, ~4.3 billion addresses |
| IPv6 | 128-bit address, virtually unlimited; India is a top adopter via Jio |
| Subnet Mask | Divides IP into network and host parts; /24 = 254 usable hosts |
| CIDR | Replaced classful addressing to reduce IP wastage |
| DNS | Translates domain names to IP addresses via hierarchical lookups |
| DNS Caching | Browser → OS → Router → ISP caches speed up repeat lookups |
| DNS Records | A (IP), CNAME (alias), MX (mail), NS (nameserver), AAAA (IPv6) |
| Domain Names | Structured hierarchy: subdomain.domain.TLD |
| Public vs Private IP | Public = globally unique; Private = local network |
| NAT | Maps private IPs to one public IP using port numbers |

---

## Self-Assessment Questions

1. Convert the class of these IP addresses: 10.0.0.1, 172.16.5.3, 192.168.1.1
2. What is the purpose of a subnet mask? Explain with an example.
3. Trace the DNS resolution process when you type `www.facebook.com` in your browser.
4. What is the difference between IPv4 and IPv6?
5. Explain the difference between gTLD and ccTLD with examples.
6. Why do we need NAT?

---

## Reading for Next Session

Tomorrow we study the **World Wide Web** — the system built ON TOP of the internet that lets us browse websites, access content, and interact with web applications.

---

*Day 3 of 55 | Unit 1 — Internet Technology | Web Technology (25BCA060)*
