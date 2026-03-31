# Day 2 — TCP/IP Architecture & Main Protocols

📖 **Type:** Theory Session
🕐 **Duration:** 2 Hours
📚 **Unit:** 1 — Internet Technology

---

## Learning Objectives

By the end of this session, students will be able to:
- Explain the TCP/IP layered architecture
- Compare TCP/IP with the OSI model
- Describe the role of key protocols (TCP, UDP, IP, ICMP, ARP)
- Understand how data encapsulation works

---

## 1. What are Protocols?

### Real-World Analogy

> When you make a phone call, both parties follow unspoken **rules**: you say "Hello," the other person responds, you take turns speaking, and you say "Bye" to end the call. These rules are a **protocol**. Without them, communication would be chaos — two people talking at once, nobody knowing when the call ends.

**Network protocols** are formal rules that define how data is formatted, transmitted, received, and acknowledged between devices on a network.

### Why Do We Need Protocols?

| Problem Without Protocols | Protocol Solution |
|--------------------------|------------------|
| Devices speak different "languages" | Standard data formats |
| Data could arrive out of order | Sequence numbering |
| Data could be lost | Acknowledgment & retransmission |
| Multiple apps share one connection | Port numbers |
| Don't know where to send data | IP addressing |

---

## 2. The TCP/IP Model

### History

TCP/IP was developed by **Vint Cerf and Bob Kahn** in the 1970s for the US Department of Defense. It became the standard protocol suite for the internet on **January 1, 1983** — often called the "birthday of the internet."

### The Four Layers

```
┌─────────────────────────────┐
│  Layer 4: APPLICATION       │  HTTP, FTP, SMTP, DNS
│  (What the user sees)       │  "Write the letter"
├─────────────────────────────┤
│  Layer 3: TRANSPORT         │  TCP, UDP
│  (Reliable delivery)        │  "Choose courier type"
├─────────────────────────────┤
│  Layer 2: INTERNET          │  IP, ICMP, ARP
│  (Addressing & routing)     │  "Write the address"
├─────────────────────────────┤
│  Layer 1: NETWORK ACCESS    │  Ethernet, Wi-Fi
│  (Physical transmission)    │  "Hand to post office"
└─────────────────────────────┘
```

> **Code Explanation:**
> - Data flows **downward** when sending (Application → Network Access) and **upward** when receiving (Network Access → Application)
> - **Layer 4 (Application):** This is where you interact — your browser (HTTP), email client (SMTP), or file manager (FTP)
> - **Layer 3 (Transport):** Decides HOW to deliver — reliably with TCP or fast with UDP
> - **Layer 2 (Internet):** Decides WHERE to deliver — IP addresses guide packets across networks
> - **Layer 1 (Network Access):** The actual physical delivery — electrical signals on cables, radio waves for Wi-Fi
> - Each layer only communicates with the layer **directly above and below** it — this modularity makes the system flexible

### Layer Details

#### Layer 1 — Network Access (Link Layer)

| Aspect | Description |
|--------|-------------|
| **Role** | Physical transmission of data over the network medium |
| **Analogy** | The actual truck/plane carrying your package |
| **Protocols** | Ethernet, Wi-Fi (802.11), PPP |
| **Data Unit** | Frame |

#### Layer 2 — Internet Layer

| Aspect | Description |
|--------|-------------|
| **Role** | Addressing and routing packets across networks |
| **Analogy** | The postal addressing system (PIN code, city, country) |
| **Key Protocol** | IP (Internet Protocol) |
| **Data Unit** | Packet |

#### Layer 3 — Transport Layer

| Aspect | Description |
|--------|-------------|
| **Role** | End-to-end data delivery, reliability, flow control |
| **Analogy** | Choosing between registered post (TCP) vs regular post (UDP) |
| **Key Protocols** | TCP, UDP |
| **Data Unit** | Segment (TCP) / Datagram (UDP) |

#### Layer 4 — Application Layer

| Aspect | Description |
|--------|-------------|
| **Role** | User-facing services and applications |
| **Analogy** | The actual letter/content you wrote |
| **Key Protocols** | HTTP, FTP, SMTP, DNS, SSH |
| **Data Unit** | Data/Message |

---

## 3. TCP/IP vs OSI Model

```
     OSI Model              TCP/IP Model
┌─────────────────┐    ┌─────────────────┐
│  7. Application │    │                 │
├─────────────────┤    │  4. Application │
│  6. Presentation│    │                 │
├─────────────────┤    │                 │
│  5. Session     │    │                 │
├─────────────────┤    ├─────────────────┤
│  4. Transport   │    │  3. Transport   │
├─────────────────┤    ├─────────────────┤
│  3. Network     │    │  2. Internet    │
├─────────────────┤    ├─────────────────┤
│  2. Data Link   │    │                 │
├─────────────────┤    │  1. Network     │
│  1. Physical    │    │     Access      │
└─────────────────┘    └─────────────────┘
    7 Layers               4 Layers
```

| Feature | OSI Model | TCP/IP Model |
|---------|-----------|-------------|
| Layers | 7 | 4 |
| Developed by | ISO (International Standards Organization) | DARPA (US Defense) |
| Approach | Theoretical/Reference | Practical/Implementation |
| Usage | Teaching & design | Actual internet communication |

---

## 4. Key Protocols Explained

### TCP (Transmission Control Protocol)

> **Analogy:** Registered post with tracking. You know exactly when the package was delivered, and if it's lost, it's sent again.

| Feature | Description |
|---------|-------------|
| **Type** | Connection-oriented |
| **Reliability** | Guaranteed delivery (acknowledgments) |
| **Ordering** | Data arrives in correct order |
| **Speed** | Slower (due to overhead) |
| **Use Cases** | Web browsing (HTTP), email (SMTP), file transfer (FTP) |

**How TCP Works (3-Way Handshake):**

```
Client                     Server
  │                          │
  │───── SYN ───────────────▶│   "Hey, want to talk?"
  │                          │
  │◀──── SYN-ACK ───────────│   "Sure, I'm ready!"
  │                          │
  │───── ACK ───────────────▶│   "Great, let's go!"
  │                          │
  │◀════ DATA TRANSFER ═════▶│
  │                          │
  │───── FIN ───────────────▶│   "I'm done."
  │◀──── ACK ───────────────│   "OK, goodbye."
```

> **Code Explanation:**
> - **SYN (Synchronize):** The client sends a SYN packet to the server saying, "I want to establish a connection." It includes a random sequence number (e.g., Seq=100).
> - **SYN-ACK (Synchronize-Acknowledge):** The server responds with its own SYN and an ACK for the client's SYN, saying "I received your request and I'm also ready." It sends its own sequence number (e.g., Seq=300) and acknowledges the client's (Ack=101).
> - **ACK (Acknowledge):** The client sends back an ACK, confirming the server's sequence number (Ack=301). Now both sides are synchronized and ready to exchange data.
> - **FIN (Finish):** When data transfer is complete, the client sends FIN to close the connection.
> - The final **ACK** confirms the connection is closed gracefully.

**What Happens When Things Go Wrong?**

| Scenario | What Happens |
|----------|-------------|
| **SYN packet is lost** | Client waits for SYN-ACK. After a timeout (usually 1 second), it **retransmits** the SYN. It retries up to ~5 times with increasing wait times (1s, 2s, 4s, 8s, 16s) — this is called **exponential backoff**. |
| **SYN-ACK is lost** | Client thinks server never responded and retransmits SYN. Server may also retransmit SYN-ACK. |
| **Data packet is lost** | Receiver sends a "duplicate ACK" for the last received packet. After 3 duplicate ACKs, the sender retransmits the missing packet (**fast retransmit**). |
| **Connection hangs** | If no response comes after all retries, the connection times out and an error is shown (e.g., "Connection timed out"). |

> **Real-World Analogy:** Imagine you call your friend Rahul. If he doesn't pick up (SYN lost), you try again after 1 minute. If you call again and he still doesn't pick up, you wait 2 minutes before trying. After 5 failed attempts, you give up (timeout). This is exactly how TCP handles lost packets.

### UDP (User Datagram Protocol)

> **Analogy:** Regular post — fast and cheap, but no tracking. If the letter gets lost, nobody knows.

| Feature | Description |
|---------|-------------|
| **Type** | Connectionless |
| **Reliability** | No guarantee of delivery |
| **Ordering** | No ordering guarantee |
| **Speed** | Faster (minimal overhead) |
| **Use Cases** | Video streaming, online gaming, DNS queries, VoIP |

### TCP vs UDP Comparison

| Feature | TCP | UDP |
|---------|-----|-----|
| Connection | Required (handshake) | Not required |
| Reliability | Guaranteed | Best-effort |
| Speed | Slower | Faster |
| Overhead | Higher | Lower |
| Example | Loading a webpage | Watching YouTube live |

### Why TCP for Email but UDP for Video Calls?

Understanding **when** to use TCP vs UDP is key. Here are real-world scenarios:

| Application | Protocol Used | Why? |
|-------------|---------------|------|
| **Email (Gmail)** | TCP | Every word in your email matters. If a packet is lost, TCP resends it. You wouldn't want your professor to receive "Your assignment is appr..." instead of "Your assignment is approved." |
| **Video Call (Google Meet)** | UDP | If one video frame is lost, showing it 2 seconds late is worse than skipping it. Your friend's face freezing for a moment is better than the video lagging further and further behind. |
| **File Download** | TCP | If even 1 byte is missing from a downloaded .zip file, the entire file is corrupted. TCP ensures every byte arrives correctly. |
| **Live Cricket Score** | UDP | The current score matters, not the score from 5 seconds ago. If a packet is lost, the next update will have the latest score anyway. |
| **Online Banking (NEFT)** | TCP | Transferring ₹5,000 requires 100% accuracy. You cannot afford a lost packet changing the amount to ₹50,000 or ₹500. |
| **Online Gaming (BGMI)** | UDP | Player positions update 60 times per second. Resending an outdated position is pointless — the player has already moved. |

> **Simple Rule of Thumb:**
> - If **accuracy** matters more than speed → use **TCP** (banking, email, file transfer)
> - If **speed** matters more than accuracy → use **UDP** (video, gaming, live streaming)

### IP (Internet Protocol)

> **Analogy:** The addressing system on an envelope. IP doesn't care about how the package is delivered — it only cares about WHERE it goes.

- **IPv4:** 32-bit addresses (e.g., `192.168.1.1`) — about 4.3 billion addresses
- **IPv6:** 128-bit addresses (e.g., `2001:0db8:85a3::8a2e:0370:7334`) — practically unlimited

### Other Important Protocols

| Protocol | Full Form | Function | Analogy |
|----------|-----------|----------|---------|
| **ICMP** | Internet Control Message Protocol | Error reporting & diagnostics | "Your package couldn't be delivered" notice |
| **ARP** | Address Resolution Protocol | Maps IP addresses to MAC addresses | Finding someone's physical address from their phone number |

### ARP (Address Resolution Protocol) — In Detail

Every network device has two addresses:
- **IP Address** — A logical address assigned by software (like your roll number in college — can change if you move to another college)
- **MAC Address** — A physical address burned into the hardware (like your Aadhaar number — permanent and unique)

**The Problem ARP Solves:** When your computer wants to send data to `192.168.1.1` (your router), it knows the IP but needs to find the **MAC address** of the router on the local network. ARP bridges this gap.

**How ARP Works — Step by Step:**

```
Your Laptop (192.168.1.100)              Router (192.168.1.1)
MAC: AA:BB:CC:DD:EE:01                  MAC: ?? (Unknown!)

Step 1: ARP Request (Broadcast to ALL devices on the network)
┌─────────────────────────────────────────────────┐
│ "Hey everyone! Who has IP 192.168.1.1?          │
│  Please tell me your MAC address!               │
│  — From: 192.168.1.100 (AA:BB:CC:DD:EE:01)"    │
└──────────────────────┬──────────────────────────┘
                       │ Broadcast → all devices hear this
                       ▼
Step 2: ARP Reply (Only the owner responds — unicast)
┌─────────────────────────────────────────────────┐
│ "That's me! My MAC is FF:GG:HH:II:JJ:02.       │
│  — From: 192.168.1.1"                           │
└──────────────────────┬──────────────────────────┘
                       │ Only sent back to requester
                       ▼
Step 3: Laptop updates its ARP Table (cache)
┌─────────────────────────────────────┐
│  ARP Table on Your Laptop:          │
│  IP Address     │ MAC Address       │
│  192.168.1.1    │ FF:GG:HH:II:JJ:02│  ← New entry!
│  192.168.1.105  │ 11:22:33:44:55:66│  ← From earlier
└─────────────────────────────────────┘
```

> **Code Explanation:**
> - **Step 1:** Your laptop broadcasts an **ARP Request** to all devices on the network (like shouting in a classroom, "Who sits at roll number 1?")
> - **Step 2:** Only the device with that IP responds with an **ARP Reply** containing its MAC address (like that student raising their hand and saying "That's me!")
> - **Step 3:** Your laptop saves this IP-to-MAC mapping in its **ARP Table** (cache), so it doesn't need to ask again for a while (typically cached for 2-20 minutes)
> - The ARP table is like a contact list — once you know Rahul's address, you don't need to ask everyone again

### DHCP (Dynamic Host Configuration Protocol) — In Detail

When you connect your phone to Wi-Fi at home, how does it automatically get an IP address? That's **DHCP** at work.

**The DORA Process:**

```
Your Phone (New device)              Wi-Fi Router (DHCP Server)
No IP address yet!                   Has a pool of IPs to assign

D — DISCOVER  ──────────────────────▶
    "I'm new here! Is there a          (Broadcast: "Any DHCP
     DHCP server that can give          server available?")
     me an IP address?"

O — OFFER     ◀──────────────────────
    "Welcome! Here's my offer:         Router: "I can offer you
     IP: 192.168.1.50                   192.168.1.50 for 24 hours"
     Subnet: 255.255.255.0
     Gateway: 192.168.1.1
     DNS: 8.8.8.8
     Lease: 24 hours"

R — REQUEST   ──────────────────────▶
    "I accept your offer!              Phone: "Yes, I'll take
     Please reserve 192.168.1.50       192.168.1.50!"
     for me."

A — ACKNOWLEDGE ◀────────────────────
    "Done! 192.168.1.50 is yours      Router: "Confirmed! It's
     for the next 24 hours."           all yours."
```

> **Code Explanation:**
> - **D (Discover):** Your phone sends a broadcast message — "Is there a DHCP server on this network?" (Since it has no IP yet, it broadcasts to everyone)
> - **O (Offer):** The router (DHCP server) responds with an available IP address, subnet mask, default gateway, and DNS server information — like a hotel receptionist offering you Room 50
> - **R (Request):** Your phone formally accepts the offer — "I'll take Room 50, please"
> - **A (Acknowledge):** The router confirms the assignment and records the **lease** — your phone "rents" this IP for a fixed period (e.g., 24 hours). After the lease expires, the phone must renew it or get a new IP.
>
> **Why leases?** If your phone disconnects and never comes back, the IP address would be wasted forever without a lease system. With leases, unused IPs are automatically returned to the pool.
| **DNS** | Domain Name System | Translates domain names to IP addresses | Phone book — looks up names to find numbers |
| **DHCP** | Dynamic Host Configuration Protocol | Automatically assigns IP addresses | Automatic seat assignment in a classroom |
| **FTP** | File Transfer Protocol | Transferring files between computers | Courier service for documents |
| **SMTP** | Simple Mail Transfer Protocol | Sending emails | Postal mail for letters |

---

## 4.1. Port Numbers — How Multiple Apps Share One Connection

### What is a Port?

> **Analogy:** Your computer's IP address is like the address of an apartment building. The **port number** is like an individual apartment number. Mail (data) is delivered to the building (IP), then to the specific apartment (port) where the right person (application) lives.

A **port** is a 16-bit number (0 to 65535) that identifies a specific application or service on a computer. Without ports, your computer wouldn't know whether incoming data is for your web browser, email client, or WhatsApp.

### Types of Port Numbers

| Range | Name | Purpose | Example |
|-------|------|---------|---------|
| **0–1023** | Well-Known Ports | Reserved for standard services | HTTP (80), HTTPS (443) |
| **1024–49151** | Registered Ports | Assigned to specific applications | MySQL (3306), MongoDB (27017) |
| **49152–65535** | Ephemeral (Dynamic) Ports | Temporarily assigned by your OS | Your browser gets a random port like 52431 |

### Important Well-Known Ports to Remember

| Port | Protocol | Service | What It Does |
|------|----------|---------|-------------|
| **20, 21** | FTP | File Transfer | Uploading/downloading files to a server |
| **22** | SSH | Secure Shell | Remote login to a server (encrypted) |
| **25** | SMTP | Email Sending | Sending emails from your client to the server |
| **53** | DNS | Domain Name System | Translating `google.com` → `142.250.195.68` |
| **80** | HTTP | Web (unencrypted) | Loading websites without HTTPS |
| **110** | POP3 | Email Receiving | Downloading emails from server to your device |
| **143** | IMAP | Email Receiving | Syncing emails across multiple devices |
| **443** | HTTPS | Web (encrypted) | Secure website loading (the 🔒 padlock in browser) |
| **3306** | MySQL | Database | Connecting to a MySQL database server |

### How Ports Work in Practice

```
Your Computer                              Google's Server
IP: 192.168.1.100                          IP: 142.250.195.68

┌────────────────┐    Request      ┌────────────────┐
│ Chrome Browser │ ──────────────▶ │ Web Server     │
│ Port: 52431    │    HTTP         │ Port: 80       │
│ (ephemeral)    │                 │ (well-known)   │
├────────────────┤                 ├────────────────┤
│ Gmail App      │ ──────────────▶ │ Mail Server    │
│ Port: 52432    │    SMTP         │ Port: 25       │
│ (ephemeral)    │                 │ (well-known)   │
├────────────────┤                 ├────────────────┤
│ WhatsApp Web   │ ──────────────▶ │ WhatsApp Server│
│ Port: 52433    │    HTTPS        │ Port: 443      │
│ (ephemeral)    │                 │ (well-known)   │
└────────────────┘                 └────────────────┘
```

> **Code Explanation:**
> - Your computer runs multiple applications simultaneously — Chrome, Gmail, WhatsApp
> - Each application gets a **random ephemeral port** (52431, 52432, 52433) assigned by the OS
> - The server uses a **fixed well-known port** (80 for HTTP, 25 for SMTP, 443 for HTTPS)
> - When data comes back from Google's server, your OS reads the **destination port** (e.g., 52431) and routes the data to Chrome, not Gmail
> - This is how you can browse the web, check email, and chat — all at the same time over one internet connection

---

### How Data Gets Wrapped as It Travels Down the Layers

```
Application Layer:  [         DATA         ]        ← "I want to see google.com"
                          ↓ Add header
Transport Layer:    [ TCP |     DATA       ]        ← Add source/destination port numbers
                          ↓ Add header
Internet Layer:     [ IP | TCP |   DATA    ]        ← Add source/destination IP addresses
                          ↓ Add header + trailer
Network Access:     [ ETH | IP | TCP | DATA | FCS ] ← Add MAC addresses + error check
```

> **Code Explanation:**
> - **Application Layer:** Your browser creates a raw HTTP request — "GET the homepage of google.com"
> - **Transport Layer:** TCP wraps this data with a header containing **port numbers** (source: 52431, destination: 80) and a **sequence number** for ordering
> - **Internet Layer:** IP wraps the TCP segment with another header containing **IP addresses** (source: your IP, destination: Google's IP) — this tells routers where to send it
> - **Network Access Layer:** Ethernet wraps everything with **MAC addresses** (source: your NIC's MAC, destination: your router's MAC) and adds an **FCS** (Frame Check Sequence) at the end for error detection
> - Think of it as putting a letter inside increasingly larger envelopes — each layer adds its own label

> **Analogy:** You write a letter (data), put it in an envelope with "To/From" (transport), put that envelope in a bigger envelope with the postal address (internet), and hand it to the postal worker who stamps it (network access).

At the **receiving end**, each layer removes its header (de-encapsulation) until the original data is extracted.

---

## Summary

| Concept | Key Takeaway |
|---------|-------------|
| Protocol | Rules for communication between devices |
| TCP/IP Model | 4 layers: Network Access → Internet → Transport → Application |
| TCP | Reliable, ordered, connection-oriented (like registered post) |
| UDP | Fast, unreliable, connectionless (like regular post) |
| IP | Handles addressing — tells packets where to go |
| ARP | Maps IP addresses to MAC addresses on local networks |
| DHCP | Automatically assigns IP addresses using the DORA process |
| Port Numbers | Identify specific applications (0-65535); well-known: 80, 443, 22, 25, 53 |
| Encapsulation | Each layer wraps data with its own header |

---

## Self-Assessment Questions

1. What is the difference between TCP and UDP? Give two use cases for each.
2. Draw the TCP/IP model and label all four layers with their functions.
3. Explain the TCP 3-way handshake with a real-world analogy.
4. What is the role of the IP protocol in internet communication?
5. How does data encapsulation work? Trace a message from application to network layer.

---

## Reading for Next Session

Tomorrow we cover **Internet Addressing & Domains** — IP addresses, subnet masks, and how the DNS system works to translate names like `google.com` into numbers.

---

*Day 2 of 55 | Unit 1 — Internet Technology | Web Technology (25BCA060)*
