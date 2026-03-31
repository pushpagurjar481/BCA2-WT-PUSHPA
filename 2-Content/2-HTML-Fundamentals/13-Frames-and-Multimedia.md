# Day 13 — Frames & Multimedia Embedding

🔬 **Type:** Theory + Practical
🕐 **Duration:** 2 Hours
📚 **Unit:** 2 — HTML Fundamentals
🧪 **Lab Experiments:** 8, 9

---

## Learning Objectives

By the end of this session, students will be able to:
- Create framesets with multiple frames
- Control frame sizes and properties
- Embed audio and video using HTML tags
- Use `<iframe>` for embedding external content

---

## 1. Frames in HTML

> **Analogy:** Frames divide a browser window into **multiple panes**, like dividing a TV screen into picture-in-picture views. Each pane loads a separate HTML file independently.

### Frameset Structure

```html
<!-- Note: DOCTYPE must be Frameset for frames to work -->
<!DOCTYPE html>
<html>
<head>
    <title>Frames Demo</title>
</head>
<!-- frameset replaces <body> — you cannot have both -->
<frameset cols="20%,60%,20%">
    <frame src="left.html" name="sidebar">     <!-- Left panel: 20% width -->
    <frame src="center.html" name="main">      <!-- Centre panel: 60% width -->
    <frame src="right.html" name="remarks">    <!-- Right panel: 20% width -->
    <noframes>
        <!-- Fallback for browsers that don't support frames -->
        <p>Your browser does not support frames.</p>
    </noframes>
</frameset>
</html>
```

> **Code Explanation:**
> - `<frameset cols="20%,60%,20%">` divides the browser window into **3 vertical columns** — 20% for left, 60% for centre, 20% for right
> - `<frame src="left.html">` loads the file `left.html` into the first (leftmost) frame — each frame loads an **independent HTML file**
> - `name="sidebar"` gives this frame a name — other pages can target links to open in this frame using `target="sidebar"`
> - `<noframes>` provides fallback content for very old browsers (or text-based browsers) that don't support frames
> - **Important:** `<frameset>` replaces `<body>` — you CANNOT have both `<frameset>` and `<body>` in the same file

### Key Tags & Attributes

| Tag/Attribute | Purpose |
|--------------|---------|
| `<frameset>` | Replaces `<body>` — defines the frame layout |
| `cols` | Divide into vertical columns |
| `rows` | Divide into horizontal rows |
| `<frame>` | Individual frame (self-closing) |
| `src` | HTML file to load in the frame |
| `name` | Name of the frame (for targeting links) |
| `<noframes>` | Fallback for browsers that don't support frames |

### Frame Attributes

| Attribute | Purpose | Example |
|-----------|---------|---------|
| `src` | Source file | `src="page.html"` |
| `name` | Frame name | `name="main"` |
| `scrolling` | Scrollbar | `yes`, `no`, `auto` |
| `noresize` | Prevent resizing | `noresize` |
| `frameborder` | Border visibility | `0` (hidden), `1` (shown) |
| `marginwidth` | Horizontal margin | `marginwidth="10"` |
| `marginheight` | Vertical margin | `marginheight="10"` |

### Targeting Links to Frames

```html
<!-- In left.html (sidebar) -->
<a href="about.html" target="main">About</a>       <!-- Opens about.html in the "main" frame -->
<a href="courses.html" target="main">Courses</a>   <!-- Opens courses.html in the "main" frame -->
```
When clicked, these links load in the frame named `"main"` (the center frame).

> **Code Explanation:**
> - `target="main"` tells the browser: "Don't load this link in the current frame; instead, load it in the frame named `main`"
> - This creates a **navigation pattern** where clicking links in the sidebar changes the content in the centre frame — similar to how a file explorer works (folder tree on left, file contents on right)
> - Other special target values: `target="_blank"` (new window), `target="_top"` (replaces all frames), `target="_parent"` (parent frameset)

> ⚠️ Frames (`<frameset>`, `<frame>`) are **deprecated in HTML5**. Use `<iframe>` or CSS layouts instead. We cover them because they're in the syllabus.

---

## 2. Inline Frames (`<iframe>`)

`<iframe>` embeds another HTML page **within** the current page (not deprecated).

```html
<!-- Embed another webpage -->
<iframe src="https://www.example.com" 
    width="600" height="400" 
    title="Example Website">       <!-- title is important for accessibility -->
</iframe>

<!-- Embed a YouTube video -->
<iframe width="560" height="315" 
    src="https://www.youtube.com/embed/dQw4w9WgXcQ" 
    title="YouTube video" 
    frameborder="0" 
    allowfullscreen>                <!-- Allows the video to go fullscreen -->
</iframe>

<!-- Embed Google Maps -->
<iframe src="https://www.google.com/maps/embed?pb=..." 
    width="600" height="450" 
    style="border:0;" 
    allowfullscreen="" 
    loading="lazy">                 <!-- lazy loading saves bandwidth -->
</iframe>
```

> **Code Explanation:**
> - `<iframe>` creates a rectangular window inside your page that displays **another webpage** — like a TV screen embedded in your page
> - `src` specifies the URL of the page to embed — can be a website, YouTube video, or Google Map
> - `width` and `height` set the iframe dimensions in pixels
> - `title="..."` describes the iframe content for **screen readers** — always include this for accessibility
> - `frameborder="0"` removes the default border around the iframe (though in modern CSS, use `style="border: none;"` instead)
> - `allowfullscreen` lets embedded videos expand to fullscreen when the user clicks the fullscreen button
> - `loading="lazy"` tells the browser to **delay loading** the iframe until the user scrolls near it — saves bandwidth and makes the page load faster

### iframe Security

When embedding external content using `<iframe>`, security is important. A malicious embedded page could potentially harm your users. HTML provides attributes to control what an iframe can do:

#### The `sandbox` Attribute

```html
<!-- Highly restricted iframe — embedded content cannot run scripts or submit forms -->
<iframe src="https://external-site.com/widget" 
    width="400" height="300"
    sandbox
    title="External Widget">
</iframe>

<!-- Selectively allow specific capabilities -->
<iframe src="https://www.youtube.com/embed/VIDEO_ID" 
    width="560" height="315"
    sandbox="allow-scripts allow-same-origin allow-presentation"
    title="YouTube Video">
</iframe>
```

> **Code Explanation:**
> - `sandbox` (without a value) applies **maximum restrictions** — the iframe cannot run JavaScript, submit forms, open popups, or access cookies
> - `sandbox="allow-scripts allow-same-origin"` selectively enables specific permissions:
>   - `allow-scripts` — lets the iframe run JavaScript (needed for YouTube player controls)
>   - `allow-same-origin` — lets the iframe access its own cookies and storage
>   - `allow-presentation` — lets the iframe use fullscreen presentation mode
>   - `allow-forms` — lets the iframe submit forms
>   - `allow-popups` — lets the iframe open new windows/popups

| `sandbox` Permission | What It Allows |
|----------------------|---------------|
| (no value — just `sandbox`) | Blocks everything — maximum security |
| `allow-scripts` | JavaScript execution |
| `allow-same-origin` | Cookie and storage access |
| `allow-forms` | Form submission |
| `allow-popups` | Opening new windows |
| `allow-presentation` | Fullscreen mode |

#### The `allow` Attribute

```html
<!-- Control browser features the iframe can access -->
<iframe src="https://video-site.com/player" 
    width="560" height="315"
    allow="autoplay; fullscreen; picture-in-picture"
    title="Video Player">
</iframe>
```

> **Code Explanation:**
> - `allow` controls which **browser features** the iframe can use (different from `sandbox` which controls security)
> - `autoplay` — allows the iframe to auto-play media
> - `fullscreen` — allows the iframe to go fullscreen
> - `picture-in-picture` — allows the video to float in a small window while user browses other tabs

> 💡 **Analogy:** Think of `sandbox` as a **locked room** — you decide which doors to unlock. Think of `allow` as **permission slips** — you decide which equipment the person in the room can use.

### Responsive iframe Technique

By default, iframes have **fixed width and height** (e.g., 560×315 pixels). On mobile phones, this iframe would overflow the screen. Here's how to make iframes responsive:

```html
<!-- Responsive YouTube embed using the aspect-ratio technique -->
<div style="position: relative; width: 100%; padding-bottom: 56.25%; height: 0; overflow: hidden;">
    <!-- 56.25% = 9/16 × 100 (for 16:9 aspect ratio) -->
    <iframe src="https://www.youtube.com/embed/VIDEO_ID"
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"
        title="Responsive YouTube Video"
        frameborder="0"
        allowfullscreen>
    </iframe>
</div>
```

> **Code Explanation:**
> - The outer `<div>` uses `padding-bottom: 56.25%` to create a responsive container — this maintains a **16:9 aspect ratio** (because 9 ÷ 16 = 0.5625 = 56.25%)
> - `height: 0` on the div means the actual height comes entirely from the padding
> - The `<iframe>` inside uses `position: absolute; width: 100%; height: 100%` to fill the entire container
> - As the browser window shrinks (e.g., on a mobile phone), the div's width shrinks, the padding adjusts proportionally, and the iframe scales perfectly
> - **Common aspect ratios:** 16:9 → `56.25%`, 4:3 → `75%`, 1:1 → `100%`

---

## 3. Audio in HTML

### HTML5 `<audio>` Tag

```html
<audio controls>
    <source src="music.mp3" type="audio/mpeg">   <!-- MP3 format (most browsers) -->
    <source src="music.ogg" type="audio/ogg">     <!-- OGG format (fallback) -->
    Your browser does not support the audio element.  <!-- Text fallback -->
</audio>
```

> **Code Explanation:**
> - `<audio controls>` creates an audio player with **play/pause button, volume slider, and progress bar** — without `controls`, the player would be invisible
> - `<source>` provides multiple audio file formats — the browser picks the **first one it supports**
> - `type="audio/mpeg"` tells the browser the file format (MIME type) — helps the browser decide quickly without downloading the file
> - The fallback text ("Your browser does not support…") displays only in very old browsers that don't support `<audio>`
> - **Why multiple `<source>` tags?** Different browsers support different formats. By providing MP3 and OGG, you ensure the audio works everywhere

### Audio Attributes

| Attribute | Purpose |
|-----------|---------|
| `controls` | Show play/pause/volume controls |
| `autoplay` | Start playing automatically |
| `loop` | Repeat continuously |
| `muted` | Start muted |
| `preload` | `auto`, `metadata`, or `none` |

### Supported Audio Formats

| Format | MIME Type | Support |
|--------|-----------|---------|
| MP3 | `audio/mpeg` | All modern browsers |
| OGG | `audio/ogg` | Firefox, Chrome, Opera |
| WAV | `audio/wav` | Most browsers |

---

## 4. Video in HTML

### HTML5 `<video>` Tag

```html
<video width="640" height="360" controls>
    <source src="video.mp4" type="video/mp4">     <!-- MP4 format (most browsers) -->
    <source src="video.webm" type="video/webm">   <!-- WebM format (fallback) -->
    Your browser does not support the video element.
</video>
```

> **Code Explanation:**
> - `<video>` creates a video player; `width="640" height="360"` sets the player size in pixels
> - `controls` adds the playback controls (play, pause, volume, fullscreen, progress bar)
> - Multiple `<source>` tags provide format fallbacks — MP4 is supported by all modern browsers; WebM is an open format preferred by Google Chrome
> - The browser tries each `<source>` in order and uses the **first one it can play**

### Video Attributes

| Attribute | Purpose |
|-----------|---------|
| `controls` | Show playback controls |
| `width` / `height` | Video dimensions |
| `autoplay` | Auto-start (requires `muted` in Chrome) |
| `loop` | Repeat video |
| `muted` | Start muted |
| `poster` | Image shown before video plays |

### The `poster` Attribute — Why It Matters

The `poster` attribute specifies a **thumbnail image** that displays before the user clicks play. Without it, the browser shows either a black rectangle or the first frame of the video.

```html
<!-- Video with a poster image -->
<video width="640" height="360" controls 
    poster="campus-thumbnail.jpg"
    muted>
    <source src="intro.mp4" type="video/mp4">
</video>
```

> **Code Explanation:**
> - `poster="campus-thumbnail.jpg"` displays this image as a **preview** before the video plays
> - `muted` starts the video with sound turned off (important for autoplay — see below)
> - **Why use a poster?**
>   - **First impressions:** A well-designed thumbnail looks professional; a black box looks broken
>   - **Bandwidth saving:** The browser doesn't need to download any video data just to show a preview
>   - **User context:** The poster tells users what the video is about before they decide to play it
>   - **Mobile data:** On slow 3G/4G connections (common in rural India), the poster loads instantly while the video may take time

### Autoplay Browser Policies

You might expect `autoplay` to automatically play videos when the page loads. However, **modern browsers block autoplay** with sound to protect users:

| Browser | Autoplay Policy |
|---------|----------------|
| **Chrome** | Blocks autoplay **with sound**. Allows autoplay only if video is `muted` |
| **Firefox** | Blocks all autoplay by default. Users can allow per-site |
| **Safari** | Blocks autoplay with sound. Allows muted autoplay |
| **Edge** | Same as Chrome (based on Chromium) |

```html
<!-- ❌ This will NOT autoplay in Chrome (has sound) -->
<video autoplay controls>
    <source src="intro.mp4" type="video/mp4">
</video>

<!-- ✅ This WILL autoplay in Chrome (muted) -->
<video autoplay muted controls>
    <source src="intro.mp4" type="video/mp4">
</video>
```

> **Code Explanation:**
> - The first example has `autoplay` but no `muted` — Chrome **blocks** this because unexpected audio is annoying (imagine opening 10 tabs and all of them start playing sound!)
> - The second example has both `autoplay` and `muted` — Chrome **allows** this because silent video is less intrusive
> - **Best practice:** Always add `muted` with `autoplay`. If you want the user to hear audio, let them click play manually or unmute themselves

> 💡 **Why do browsers block autoplay?** Imagine sitting in a quiet library or classroom, and you open a website that suddenly starts playing loud music. Embarrassing! Browsers protect users from this. Google Chrome introduced this policy in 2018 after years of user complaints about noisy websites.

### Video and Audio Codec Differences

When you provide video/audio files, the browser needs to understand the **codec** (compression format) used. Here's what you need to know:

**Video Formats:**

| Format | Codec | File Extension | Browser Support | Best For |
|--------|-------|---------------|----------------|----------|
| **MP4** | H.264 (AVC) | `.mp4` | ✅ All browsers | General use — the safest choice |
| **WebM** | VP9 | `.webm` | ✅ Chrome, Firefox, Edge; ❌ Safari | Smaller files, open source |
| **OGG** | Theora | `.ogv` | ✅ Firefox, Chrome; ❌ Safari, Edge | Older open format (rarely used now) |
| **MP4** | H.265 (HEVC) | `.mp4` | ⚠️ Safari only | Very high quality, but limited support |

**Audio Formats:**

| Format | File Extension | Browser Support | Best For |
|--------|---------------|----------------|----------|
| **MP3** | `.mp3` | ✅ All browsers | Music, podcasts — universally supported |
| **AAC** | `.aac`, `.m4a` | ✅ All browsers | Higher quality than MP3 at same file size |
| **OGG Vorbis** | `.ogg` | ✅ Chrome, Firefox; ❌ Safari | Open source alternative to MP3 |
| **WAV** | `.wav` | ✅ All browsers | Uncompressed (very large files) — avoid for web |

> 💡 **Recommendation for BCA students:**
> - For **video**: Always provide **MP4 (H.264)** as the primary format — it works everywhere. Optionally add **WebM** as a fallback for smaller file sizes.
> - For **audio**: Always provide **MP3** as the primary format. Optionally add **OGG** for open-source browser compatibility.

### The `<track>` Tag — Video Captions and Subtitles

The `<track>` tag adds **text captions or subtitles** to a video. This is essential for:
- **Deaf/hard-of-hearing users** who cannot hear the audio
- **Students watching in noisy environments** (e.g., college canteen, bus)
- **Videos in a different language** (e.g., English subtitles for a Hindi video)

```html
<video width="640" height="360" controls poster="lecture-thumbnail.jpg">
    <source src="lecture.mp4" type="video/mp4">

    <!-- English subtitles -->
    <track src="subtitles-en.vtt" 
        kind="subtitles" 
        srclang="en" 
        label="English" 
        default>

    <!-- Hindi subtitles -->
    <track src="subtitles-hi.vtt" 
        kind="subtitles" 
        srclang="hi" 
        label="हिन्दी">

    Your browser does not support the video element.
</video>
```

> **Code Explanation:**
> - `<track>` goes **inside** the `<video>` tag, alongside `<source>`
> - `src="subtitles-en.vtt"` points to a **WebVTT file** (`.vtt`) containing the subtitle text with timestamps
> - `kind="subtitles"` specifies this track contains subtitles (other options: `captions`, `descriptions`, `chapters`)
> - `srclang="en"` identifies the language of the subtitles
> - `label="English"` is the text shown in the subtitle selection menu in the video player
> - `default` makes this track the **default selection** when the video loads

**WebVTT File Format (.vtt):**

A `.vtt` file is a simple text file that contains subtitle text with timestamps:

```
WEBVTT

00:00:01.000 --> 00:00:04.000
Welcome to the Web Technology lecture.

00:00:04.500 --> 00:00:08.000
Today we will learn about HTML multimedia.

00:00:08.500 --> 00:00:12.000
Let's start with the audio and video tags.
```

> **Code Explanation:**
> - The file must start with `WEBVTT` on the first line
> - Each subtitle block has a **timestamp range** (`start --> end`) in `HH:MM:SS.mmm` format
> - Below the timestamp is the **subtitle text** that appears on screen during that time range
> - Blank lines separate each subtitle block
> - You can create `.vtt` files in any text editor (VS Code, Notepad) — just save with the `.vtt` extension

---

## 5. Embedding YouTube Videos

```html
<!-- Steps: Go to YouTube → Share → Embed → Copy code -->
<iframe width="560" height="315" 
    src="https://www.youtube.com/embed/VIDEO_ID" 
    title="Video Title" 
    frameborder="0" 
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
    allowfullscreen>
</iframe>
```

> **Code Explanation:**
> - YouTube provides an **embed code** when you click Share → Embed on any video — you just copy-paste it
> - `src="https://www.youtube.com/embed/VIDEO_ID"` — note the `/embed/` path; this is different from the regular YouTube URL
> - `allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"` — grants the iframe specific permissions needed by YouTube's player
> - `allowfullscreen` — lets the user watch the video in fullscreen mode
> - Replace `VIDEO_ID` with the actual YouTube video ID (the part after `v=` in a YouTube URL, e.g., `dQw4w9WgXcQ`)

---

## Practical Session

### 🧪 Lab Experiment 8: Three-Frame Layout

**Objective:** Create a page divided into 3 frames — left (20%) for navigation, center (60%) for content, and right (20%) for remarks.

**File: `frameset.html`**
```html
<!DOCTYPE html>
<html>
<head>
    <title>Three Frame Layout</title>
</head>
<frameset cols="20%,60%,20%">
    <frame src="nav.html" name="sidebar" scrolling="auto">
    <frame src="welcome.html" name="main" scrolling="auto">
    <frame src="remarks.html" name="remarks" scrolling="auto">
    <noframes>
        <p>Your browser does not support frames. Please use a modern browser.</p>
    </noframes>
</frameset>
</html>
```

**File: `nav.html`**
```html
<!DOCTYPE html>
<html>
<head><title>Navigation</title></head>
<body bgcolor="#E3F2FD" style="font-family: Arial;">
    <h3>Contents</h3>
    <p><a href="welcome.html" target="main">Home</a></p>
    <p><a href="about.html" target="main">About</a></p>
    <p><a href="courses.html" target="main">Courses</a></p>
    <p><a href="faculty.html" target="main">Faculty</a></p>
    <p><a href="contact.html" target="main">Contact</a></p>
</body>
</html>
```

**File: `welcome.html`**
```html
<!DOCTYPE html>
<html>
<head><title>Welcome</title></head>
<body style="font-family: Arial; padding: 20px;">
    <h1>Welcome to BCA Department</h1>
    <p>Click on the links in the left panel to navigate.</p>
    <p>This is the main content area where pages will be displayed.</p>
</body>
</html>
```

**File: `remarks.html`**
```html
<!DOCTYPE html>
<html>
<head><title>Remarks</title></head>
<body bgcolor="#FFF9C4" style="font-family: Arial;">
    <h3>Remarks</h3>
    <p><em>Updated: April 2026</em></p>
    <p>New admissions open!</p>
    <p>Lab hours: 9 AM - 5 PM</p>
</body>
</html>
```

> **Code Explanation (Lab Experiment 8 — All Files):**
> - **`frameset.html`:** The main file that defines the frame layout; `cols="20%,60%,20%"` creates 3 vertical columns; each `<frame>` loads a separate HTML file; `scrolling="auto"` shows scrollbars only when needed
> - **`nav.html`:** The left sidebar with navigation links; `target="main"` on each `<a>` tag ensures clicked links open in the centre frame (named "main") instead of the sidebar itself
> - **`welcome.html`:** The default content page loaded in the centre frame; this gets replaced when the user clicks a navigation link
> - **`remarks.html`:** The right panel with notices and updates; `bgcolor="#FFF9C4"` gives it a light yellow background to distinguish it visually
> - **How they work together:** All 4 files must be saved in the **same folder**. Opening `frameset.html` in a browser loads the other 3 files simultaneously in their respective frames

---

### 🧪 Lab Experiment 9: Embed Audio and Video

**Objective:** Create a multimedia-rich webpage with embedded audio and video.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Multimedia Gallery</title>
</head>
<body style="font-family: Arial; max-width: 800px; margin: 0 auto; padding: 20px;">

    <h1 align="center">Multimedia Gallery</h1>
    <hr>

    <!-- Audio Section -->
    <h2>🎵 Audio Player</h2>
    <p>Listen to the campus anthem:</p>
    <audio controls style="width: 100%;">
        <source src="anthem.mp3" type="audio/mpeg">
        <source src="anthem.ogg" type="audio/ogg">
        Your browser does not support the audio element.
    </audio>
    
    <br><br>

    <!-- Video Section -->
    <h2>🎬 Video Player</h2>
    <p>Watch our campus tour:</p>
    <video width="100%" controls poster="https://via.placeholder.com/800x450?text=Campus+Tour">
        <source src="campus-tour.mp4" type="video/mp4">
        <source src="campus-tour.webm" type="video/webm">
        Your browser does not support the video element.
    </video>

    <br><br>

    <!-- Embedded YouTube Video -->
    <h2>📺 Embedded YouTube Video</h2>
    <p>HTML Tutorial for Beginners:</p>
    <div align="center">
        <iframe width="560" height="315" 
            src="https://www.youtube.com/embed/qz0aGYrrlhU" 
            title="HTML Tutorial" 
            frameborder="0" 
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
            allowfullscreen>
        </iframe>
    </div>

    <hr>
    <p align="center"><em>Unit 2 Complete! Next: HTML5 &rarr;</em></p>

</body>
</html>
```

> **Code Explanation (Lab Experiment 9):**
> - `max-width: 800px; margin: 0 auto` — centres the entire page and limits its width to 800px for readability
> - **Audio player:** `controls` adds play/pause/volume; `style="width: 100%"` makes the player span the full width; two `<source>` tags provide MP3 and OGG formats for browser compatibility
> - **Video player:** `width="100%"` makes the video responsive (fills the container width); `poster="..."` shows a preview image before playing; two `<source>` tags provide MP4 and WebM formats
> - **YouTube embed:** The `<iframe>` loads YouTube's embed player; `allow="accelerometer; autoplay;..."` grants necessary permissions; `allowfullscreen` enables fullscreen viewing
> - **`<div align="center">`** centres the YouTube iframe on the page
> - All three media types (audio, video, iframe embed) are shown on a single page — a common pattern for multimedia galleries

---

## Practice Exercise

1. Create a frame-based website with:
   - Top frame (header): 15% height
   - Left frame (menu): 20% width
   - Center frame (content): remaining space
   - Use nested framesets: `rows` for top/bottom, then `cols` for left/right

2. Create a multimedia page with:
   - At least 2 audio players
   - 1 local video player with poster
   - 1 embedded YouTube video
   - Proper fallback text for unsupported browsers

---

## Summary

| Concept | Key Takeaway |
|---------|-------------|
| `<frameset>` | Divides window into frames (deprecated in HTML5) |
| `<frame>` | Individual pane loading a separate HTML file |
| `target="frameName"` | Opens link in a specific frame |
| `<iframe>` | Embeds content inline (NOT deprecated) |
| `sandbox` / `allow` | Security attributes for `<iframe>` |
| Responsive iframe | Use `padding-bottom: 56.25%` trick for 16:9 aspect ratio |
| `<audio>` | HTML5 audio player with controls |
| `<video>` | HTML5 video player with controls |
| `poster` | Preview image for video (important for UX and bandwidth) |
| `autoplay` + `muted` | Required combination for autoplay in modern browsers |
| `<source>` | Provides multiple format options for audio/video |
| `<track>` | Adds subtitles/captions to video (WebVTT format) |
| MP4 (H.264) | Safest video format — works in all browsers |
| MP3 | Safest audio format — works in all browsers |

---

**🎉 Unit 2 Complete!** Starting Day 14, we move to **Unit 3: HTML5** — semantic elements, new form types, APIs, and more.

---

*Day 13 of 55 | Unit 2 — HTML Fundamentals | Web Technology (25BCA060)*
