# Step 2: Installing Required Software

> **⏱️ Time Required:** 15–30 minutes | **Difficulty:** Easy | **What You Need:** A Windows computer with internet access

---

## Software You Need

| Software | What It's For | Required? |
|----------|-------------|-----------|
| **Google Chrome** | Viewing your web pages | ✅ Yes |
| **Visual Studio Code (VS Code)** | Writing HTML/CSS/JS code | ✅ Yes |
| **GitHub Desktop** | Uploading/downloading code (no command line needed) | ✅ Yes (recommended) |
| **Git** | Version control (command line, for advanced users) | Optional |

---

## 1. Installing Google Chrome

If Chrome is already installed, skip to the next section.

1. Open any browser (Edge is fine)
2. Go to: **https://www.google.com/chrome/**
3. Click **"Download Chrome"**
4. Run the downloaded file
5. Follow the installation prompts
6. When done, set Chrome as your **default browser**:
   - Open Chrome → Click the **three dots** (⋮) at top-right
   - Go to **Settings → Default browser → Make default**

---

## 2. Installing Visual Studio Code (VS Code)

VS Code is the code editor where you will write all your HTML, CSS, and JavaScript files.

### Step-by-Step Installation

1. Open Chrome and go to: **https://code.visualstudio.com/**
2. Click the big blue **"Download for Windows"** button
3. Wait for `VSCodeUserSetup-x64-X.XX.X.exe` to download
4. **Double-click** the downloaded file to start installation
5. On the setup wizard:
   - ✅ Accept the license agreement → Click **Next**
   - ✅ Leave the default installation location → Click **Next**
   - ✅ On "Select Additional Tasks", check these boxes:
     - ☑️ **Add "Open with Code" action to Windows Explorer file context menu**
     - ☑️ **Add "Open with Code" action to Windows Explorer directory context menu**
     - ☑️ **Register Code as an editor for supported file types**
     - ☑️ **Add to PATH**
   - Click **Next** → Click **Install**
6. Wait for installation to complete → Click **Finish**

### Verify Installation

1. Press the **Windows key** on your keyboard
2. Type **"Visual Studio Code"**
3. Click to open it
4. You should see the VS Code welcome screen

### Recommended VS Code Extensions

After opening VS Code, install these helpful extensions:

1. Click the **Extensions icon** on the left sidebar (it looks like four small squares)
2. Search for and install:
   - **Live Server** — Opens HTML files in browser with auto-refresh
   - **Prettier** — Automatically formats your code neatly
   - **Auto Rename Tag** — When you change an HTML opening tag, the closing tag changes too

**How to install an extension:**
1. Click the Extensions icon (or press `Ctrl + Shift + X`)
2. Type the extension name in the search box
3. Click the blue **"Install"** button

---

## 3. Installing GitHub Desktop (Recommended for Beginners)

**GitHub Desktop** is a visual application that lets you upload and download code from GitHub **without using command line**. It is the easiest way to work with GitHub.

### Step-by-Step Installation

1. Open Chrome and go to: **https://desktop.github.com/**
2. Click **"Download for Windows (64bit)"**
3. Run the downloaded file (`GitHubDesktopSetup-x64.exe`)
4. The installer runs automatically — just wait
5. When it opens, click **"Sign in to GitHub.com"**
6. A browser window opens → Log in with your GitHub account
7. Click **"Authorize desktop"**
8. Back in GitHub Desktop, confirm your name and email
9. Click **"Finish"**

### Verify Installation

You should see the GitHub Desktop home screen with options like:
- "Clone a repository from the Internet"
- "Create a new repository on your hard drive"
- "Add an existing repository from your hard drive"

---

## 4. Installing Git (Optional — For Advanced Users / CLI)

**Git** is the command-line tool that GitHub Desktop uses internally. If you want to use Git from the terminal (command line), install it separately.

> **Note:** If you installed GitHub Desktop, you may not need this. GitHub Desktop includes Git internally.

### Step-by-Step Installation

1. Go to: **https://git-scm.com/download/win**
2. The download should start automatically
3. Run the installer (`Git-X.XX.X-64-bit.exe`)
4. On the setup wizard, **use all default settings** — just keep clicking **Next**
   - Important: On the "Choosing the default editor" screen, you can select **"Use Visual Studio Code as Git's default editor"** if you prefer
5. Click **Install** → Wait → Click **Finish**

### Verify Installation

1. Press `Win + R` → Type `cmd` → Press Enter
2. Type `git --version` and press Enter
3. You should see something like:
   ```
   git version 2.44.0.windows.1
   ```

If you see the version number, Git is installed correctly.

---

## Summary: What You've Installed

| Software | Purpose | How to Open |
|----------|---------|------------|
| **Chrome** | View web pages | Start Menu → Chrome |
| **VS Code** | Write code | Start Menu → Visual Studio Code |
| **GitHub Desktop** | Upload/download code | Start Menu → GitHub Desktop |
| **Git** (optional) | Command-line version control | Command Prompt → type `git` |

---

## You're Ready! ✅

All software is installed. Now let's download the course materials:

**👉 [Step 3: Getting the Course Materials](FOR-STUDENTS-03-Getting-Course-Materials.md)**

---

*Part of the Web Technology (25BCA060) course. Instructions and Prerequisites.*
