# Day 10 — Tables in HTML

🔬 **Type:** Theory + Practical
🕐 **Duration:** 2 Hours
📚 **Unit:** 2 — HTML Fundamentals
🧪 **Lab Experiments:** 5, 6

---

## Learning Objectives

By the end of this session, students will be able to:
- Create tables using `<table>`, `<tr>`, `<th>`, `<td>`
- Apply table attributes (border, cellpadding, cellspacing, colspan, rowspan)
- Use tables for displaying data (timetable, layouts)
- Understand when to use and NOT use tables

---

## 1. Basic Table Structure

```html
<table border="1">
    <tr>                    <!-- Table Row -->
        <th>Name</th>       <!-- Table Header (bold, centered) -->
        <th>Age</th>
    </tr>
    <tr>
        <td>Rahul</td>     <!-- Table Data (regular cell) -->
        <td>20</td>
    </tr>
    <tr>
        <td>Priya</td>
        <td>21</td>
    </tr>
</table>
```

> **Code Explanation:**
> - `<table border="1">` — creates a table container with a 1-pixel solid border around all cells
> - `<tr>` — defines a **table row**; every row starts with `<tr>` and ends with `</tr>`
> - `<th>Name</th>` — a **table header** cell; text inside `<th>` is automatically **bold and centered**
> - `<td>Rahul</td>` — a **table data** cell; this holds regular content (left-aligned by default)
> - Each `<tr>` must contain the same number of `<th>` or `<td>` cells to keep the table aligned

**Renders as:**

| Name | Age |
|------|-----|
| Rahul | 20 |
| Priya | 21 |

> 💡 **Real-World Analogy:** Think of an HTML table like an **Excel spreadsheet** — `<table>` is the sheet itself, `<tr>` is a row, `<th>` is a header cell (like the first bold row in Excel), and `<td>` is a regular data cell.

### Key Tags

| Tag | Purpose |
|-----|---------|
| `<table>` | Creates the table container |
| `<tr>` | Table Row |
| `<th>` | Table Header (bold + centered) |
| `<td>` | Table Data (regular cell) |
| `<caption>` | Table title/caption |
| `<thead>` | Groups header rows |
| `<tbody>` | Groups body rows |
| `<tfoot>` | Groups footer rows |

### Semantic Table Structure with `<thead>`, `<tbody>`, `<tfoot>`

While a simple table works with just `<tr>`, `<th>`, and `<td>`, **semantic table tags** help the browser (and screen readers) understand which part of the table is the header, body, and footer. Think of it like a **printed report** — the header row appears on every printed page, the body has the data, and the footer shows totals.

```html
<!-- Semester marks report using semantic table structure -->
<table border="1" cellpadding="8" cellspacing="0" width="80%">
    <caption><b>BCA Semester II — Internal Marks (2025-26)</b></caption>

    <!-- Table Header: appears at top (repeated on each printed page) -->
    <thead>
        <tr bgcolor="#1565C0">
            <th><font color="white">Roll No</font></th>
            <th><font color="white">Student Name</font></th>
            <th><font color="white">Web Tech</font></th>
            <th><font color="white">Data Structures</font></th>
            <th><font color="white">Maths</font></th>
        </tr>
    </thead>

    <!-- Table Footer: totals/averages (placed before tbody in HTML, rendered at bottom) -->
    <tfoot>
        <tr bgcolor="#E3F2FD">
            <td colspan="2" align="right"><strong>Class Average:</strong></td>
            <td align="center"><strong>17.3</strong></td>
            <td align="center"><strong>16.0</strong></td>
            <td align="center"><strong>15.7</strong></td>
        </tr>
    </tfoot>

    <!-- Table Body: the actual data rows -->
    <tbody>
        <tr>
            <td align="center">001</td>
            <td>Amit Sharma</td>
            <td align="center">18</td>
            <td align="center">16</td>
            <td align="center">15</td>
        </tr>
        <tr bgcolor="#F5F5F5">
            <td align="center">002</td>
            <td>Priya Verma</td>
            <td align="center">19</td>
            <td align="center">17</td>
            <td align="center">18</td>
        </tr>
        <tr>
            <td align="center">003</td>
            <td>Ravi Patel</td>
            <td align="center">15</td>
            <td align="center">15</td>
            <td align="center">14</td>
        </tr>
    </tbody>
</table>
```

> **Code Explanation:**
> - `<thead>` wraps the **header row(s)** — browsers know this row labels the columns and may repeat it when printing
> - `<tfoot>` wraps the **footer row(s)** — used for totals, averages, or summary data. In HTML, `<tfoot>` is written **before** `<tbody>` but rendered **at the bottom**
> - `<tbody>` wraps the **data rows** — this is the main content of the table
> - `<caption>` provides a **title** for the table, displayed above it — useful for accessibility
> - `colspan="2"` in the footer merges two cells so "Class Average:" spans the Roll No and Name columns

| Semantic Tag | Purpose | Analogy |
|-------------|---------|---------|
| `<thead>` | Groups header rows | The column titles row in an Excel sheet |
| `<tbody>` | Groups data rows | The actual data in the spreadsheet |
| `<tfoot>` | Groups footer rows | The "Total" or "Average" row at the bottom |
| `<caption>` | Table title | The title you give to a report |

---

## 2. Table Attributes

```html
<table border="2" cellpadding="10" cellspacing="5" width="80%" bgcolor="#f0f0f0">
    <caption><b>Student Details</b></caption>
    <tr bgcolor="#333333">
        <th><font color="white">Name</font></th>
        <th><font color="white">Roll No</font></th>
        <th><font color="white">Course</font></th>
    </tr>
    <tr>
        <td align="center">Amit Kumar</td>
        <td align="center">001</td>
        <td align="center">BCA</td>
    </tr>
</table>
```

| Attribute | Purpose | Example |
|-----------|---------|---------|
| `border` | Border thickness (pixels) | `border="1"` |
| `cellpadding` | Space inside cells (between content and border) | `cellpadding="10"` |
| `cellspacing` | Space between cells | `cellspacing="5"` |
| `width` | Table width (px or %) | `width="80%"` |
| `height` | Table height | `height="300"` |
| `bgcolor` | Background color | `bgcolor="#f0f0f0"` |
| `align` | Table alignment | `align="center"` |

### Cell Attributes

| Attribute | Purpose | Applied To |
|-----------|---------|-----------|
| `colspan` | Span multiple columns | `<td>` or `<th>` |
| `rowspan` | Span multiple rows | `<td>` or `<th>` |
| `align` | Horizontal alignment | `<td>` or `<th>` |
| `valign` | Vertical alignment | `<td>` or `<th>` |

> **Code Explanation (Table Attributes example above):**
> - `border="2"` — sets a 2-pixel border around every cell
> - `cellpadding="10"` — adds 10px of space **inside** each cell (between the text and the cell border) — like adding padding inside a box
> - `cellspacing="5"` — adds 5px of space **between** cells — like leaving gaps between boxes on a shelf
> - `width="80%"` — makes the table occupy 80% of the parent element's width
> - `bgcolor="#f0f0f0"` — sets a light grey background colour for the entire table
> - `<caption>` — adds a title above the table (useful for accessibility and context)
> - `align="center"` on `<td>` — centres the text inside that specific cell
> - `bgcolor="#333333"` on `<tr>` — sets a dark background for the header row only

> 💡 **Cellpadding vs Cellspacing:** Imagine each cell is a **gift box**. `cellpadding` is the foam/bubble-wrap **inside** the box (between the gift and the box walls). `cellspacing` is the **gap between boxes** sitting on a shelf.

---

## 3. Colspan & Rowspan

### Colspan (Merge Columns)

```html
<table border="1" cellpadding="8">
    <tr>
        <th colspan="3">Student Information</th>
    </tr>
    <tr>
        <th>Name</th>
        <th>Roll No</th>
        <th>Grade</th>
    </tr>
    <tr>
        <td>Rahul</td>
        <td>001</td>
        <td>A</td>
    </tr>
</table>
```

> **Code Explanation (Colspan):**
> - `colspan="3"` on the first `<th>` makes it **span across 3 columns**, creating a merged title row
> - The second `<tr>` has 3 separate `<th>` cells — these become the actual column headers
> - The total number of columns in the table is determined by the row with the most individual cells (3 in this case)

### Rowspan (Merge Rows)

```html
<table border="1" cellpadding="8">
    <tr>
        <th>Day</th>         <!-- Column 1 header -->
        <th>Subject</th>     <!-- Column 2 header -->
    </tr>
    <tr>
        <td rowspan="2">Monday</td>   <!-- This cell spans 2 rows vertically -->
        <td>Web Technology</td>
    </tr>
    <tr>
        <!-- No <td> for Day column — it's covered by the rowspan above -->
        <td>Data Structures</td>
    </tr>
</table>
```

> **Code Explanation (Rowspan):**
> - `rowspan="2"` on "Monday" makes this cell **stretch down across 2 rows** — so "Monday" appears once but covers both subject rows
> - The third `<tr>` only has **one** `<td>` (Data Structures), because the Day column is already occupied by the spanning cell from the row above
> - **Common mistake:** Adding an extra `<td>` in the third row for Day — this would break the table because the rowspan already covers that space

> 💡 **Colspan vs Rowspan Visual:**
> ```
> colspan="3" (merge columns horizontally):
> ┌───────────────────────────┐
> │      Student Information   │  ← 1 cell spanning 3 columns
> ├─────────┬────────┬────────┤
> │  Name   │ Roll   │ Grade  │
> └─────────┴────────┴────────┘
>
> rowspan="2" (merge rows vertically):
> ┌─────────┬─────────────────┐
> │         │ Web Technology   │
> │ Monday  ├─────────────────┤  ← "Monday" spans 2 rows
> │         │ Data Structures  │
> └─────────┴─────────────────┘
> ```

---

## 4. Table Accessibility

When you create tables, not everyone views them visually — **screen readers** (used by visually impaired users) read tables aloud. To help screen readers understand the table structure, use the `scope` attribute on `<th>` elements.

### The `scope` Attribute

```html
<table border="1" cellpadding="8">
    <caption>BCA II Semester Exam Schedule</caption>
    <tr>
        <th scope="col">Date</th>          <!-- This header labels a column -->
        <th scope="col">Subject</th>       <!-- This header labels a column -->
        <th scope="col">Time</th>          <!-- This header labels a column -->
    </tr>
    <tr>
        <th scope="row">10 May 2026</th>   <!-- This header labels a row -->
        <td>Web Technology</td>
        <td>10:00 AM - 1:00 PM</td>
    </tr>
    <tr>
        <th scope="row">12 May 2026</th>   <!-- This header labels a row -->
        <td>Data Structures</td>
        <td>10:00 AM - 1:00 PM</td>
    </tr>
</table>
```

> **Code Explanation:**
> - `scope="col"` tells the screen reader: "This header applies to all cells **below** in this column"
> - `scope="row"` tells the screen reader: "This header applies to all cells **to the right** in this row"
> - `<caption>` gives the table a title that screen readers announce before reading the table content
> - A screen reader would announce: *"Table: BCA II Semester Exam Schedule. Row 2: Date: 10 May 2026, Subject: Web Technology, Time: 10:00 AM - 1:00 PM"*

| `scope` Value | Meaning |
|--------------|---------|
| `col` | Header applies to the entire **column** below |
| `row` | Header applies to the entire **row** to the right |
| `colgroup` | Header applies to a **group of columns** |
| `rowgroup` | Header applies to a **group of rows** |

> 💡 **Why does this matter?** In India, government websites must follow accessibility guidelines (GIGW — Guidelines for Indian Government Websites). Using `scope` and `<caption>` makes your tables accessible to all users, including those using screen readers.

---

## 5. When to Use Tables (and When NOT To)

This is an important concept many beginners get wrong. Tables are meant for **tabular data only** — data that naturally fits in rows and columns.

### ✅ When Tables ARE Appropriate

| Use Case | Example |
|----------|---------|
| Data display | Student marks, exam results |
| Schedules | Class timetable, train schedule |
| Comparisons | Feature comparison of products |
| Financial data | Price lists, invoices, budgets |
| Statistics | Census data, survey results |

### ❌ When Tables are NOT Appropriate

| Don't Use For | Use Instead |
|--------------|-------------|
| Page layout (header, sidebar, footer) | `<div>` with CSS, or HTML5 semantic tags (`<header>`, `<nav>`, `<main>`, `<footer>`) |
| Navigation menus | `<nav>` with `<ul>` list |
| Image galleries | `<div>` grid with CSS Flexbox/Grid |
| Form layout | CSS styling on `<form>` elements |
| Placing elements side by side | CSS Flexbox or CSS Grid |

> 💡 **Real-World Analogy:** Using a table for page layout is like using a **bookshelf to build a wall** — it works, but it's not the right tool. Bookshelves are for storing books (data), walls are built with bricks (CSS layouts). In the early days of the web (1990s), developers used tables for layouts because CSS didn't exist yet. Today, we use CSS for layout and tables only for data.

---

## 6. Nested Tables

You can place a table **inside another table's cell** — this is called a **nested table**. While not commonly used today, it helps understand how complex table structures work.

```html
<table border="1" cellpadding="8" width="80%">
    <tr>
        <th colspan="2">Mandsaur University — Department Overview</th>
    </tr>
    <tr>
        <td valign="top"><strong>BCA Department</strong></td>
        <td>
            <!-- Nested table inside a cell -->
            <table border="1" cellpadding="4" width="100%">
                <tr bgcolor="#E3F2FD">
                    <th>Subject</th>
                    <th>Faculty</th>
                </tr>
                <tr>
                    <td>Web Technology</td>
                    <td>Prof. Mehta</td>
                </tr>
                <tr>
                    <td>Data Structures</td>
                    <td>Prof. Joshi</td>
                </tr>
            </table>
        </td>
    </tr>
</table>
```

> **Code Explanation:**
> - The **outer table** has 2 rows — a merged title row and a data row with 2 columns
> - Inside the second column of the data row, we place an **entirely new `<table>`** — this is the nested table
> - The nested table has its own `<tr>`, `<th>`, and `<td>` — it's a complete table within a cell
> - `valign="top"` on the outer `<td>` ensures "BCA Department" aligns to the top of the cell, even if the nested table is taller

> ⚠️ **Note:** Nested tables increase complexity and can be hard to maintain. Modern web development prefers CSS-based layouts for complex structures. However, understanding nested tables is useful for reading legacy code and for exam purposes.

---

## Practical Session

### 🧪 Lab Experiment 5: Class Timetable

**Objective:** Create a table to show your class timetable.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BCA II Semester - Class Timetable</title>
</head>
<body>

    <h1 align="center">BCA II Semester — Class Timetable</h1>
    <h3 align="center">Mandsaur University | Academic Year 2025-26</h3>

    <table border="1" cellpadding="10" cellspacing="0" width="90%" align="center">
        <caption><strong>Weekly Schedule</strong></caption>
        
        <!-- Header Row -->
        <tr bgcolor="#1565C0">
            <th><font color="white">Time / Day</font></th>
            <th><font color="white">Monday</font></th>
            <th><font color="white">Tuesday</font></th>
            <th><font color="white">Wednesday</font></th>
            <th><font color="white">Thursday</font></th>
            <th><font color="white">Friday</font></th>
            <th><font color="white">Saturday</font></th>
        </tr>
        
        <!-- Period 1 -->
        <tr>
            <td bgcolor="#E3F2FD" align="center"><strong>9:00 - 10:00</strong></td>
            <td align="center">Web Technology</td>
            <td align="center">Data Structures</td>
            <td align="center">Web Technology</td>
            <td align="center">Mathematics</td>
            <td align="center">Data Structures</td>
            <td align="center">Mathematics</td>
        </tr>
        
        <!-- Period 2 -->
        <tr>
            <td bgcolor="#E3F2FD" align="center"><strong>10:00 - 11:00</strong></td>
            <td align="center">Mathematics</td>
            <td align="center">Web Technology</td>
            <td align="center">Data Structures</td>
            <td align="center">Web Technology</td>
            <td align="center">Mathematics</td>
            <td align="center">Library</td>
        </tr>
        
        <!-- Break -->
        <tr bgcolor="#FFF9C4">
            <td align="center"><strong>11:00 - 11:30</strong></td>
            <td colspan="6" align="center"><em>☕ Tea Break</em></td>
        </tr>
        
        <!-- Period 3-4 (Lab) -->
        <tr>
            <td bgcolor="#E3F2FD" align="center"><strong>11:30 - 1:30</strong></td>
            <td colspan="2" align="center" bgcolor="#E8F5E9">
                <strong>Web Technology Lab</strong><br>(Mon-Tue)
            </td>
            <td colspan="2" align="center" bgcolor="#FFF3E0">
                <strong>DS Lab</strong><br>(Wed-Thu)
            </td>
            <td colspan="2" align="center" bgcolor="#F3E5F5">
                <strong>Math Tutorial</strong><br>(Fri-Sat)
            </td>
        </tr>
        
        <!-- Lunch -->
        <tr bgcolor="#FFECB3">
            <td align="center"><strong>1:30 - 2:30</strong></td>
            <td colspan="6" align="center"><em>🍽️ Lunch Break</em></td>
        </tr>
        
        <!-- Period 5 -->
        <tr>
            <td bgcolor="#E3F2FD" align="center"><strong>2:30 - 3:30</strong></td>
            <td align="center">English</td>
            <td align="center">EVS</td>
            <td align="center">English</td>
            <td align="center">EVS</td>
            <td align="center">Sports</td>
            <td align="center">—</td>
        </tr>
    </table>

</body>
</html>
```

> **Code Explanation (Lab Experiment 5):**
> - The table uses `cellspacing="0"` to remove gaps between cells, giving a clean grid look
> - `bgcolor="#1565C0"` on the header `<tr>` creates a blue header row; `<font color="white">` makes the text readable on the dark background
> - `bgcolor="#E3F2FD"` on the time column cells gives them a light blue background so students can quickly identify time slots
> - `colspan="6"` on the Tea Break and Lunch Break rows merges all 6 day columns into one wide cell
> - `colspan="2"` on the Lab period cells merges two day columns (e.g., Mon-Tue) to show a 2-day lab session spanning those days
> - `align="center"` centres text inside cells for a neat, professional timetable appearance
> - The `<caption>` tag adds a title "Weekly Schedule" above the table

---

### 🧪 Lab Experiment 6: University Infrastructure Page (Table Layout)

**Objective:** Use tables to provide a layout for a university infrastructure page.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>University Infrastructure</title>
</head>
<body bgcolor="#FAFAFA">

    <!-- Header using table -->
    <table width="100%" bgcolor="#0D47A1" cellpadding="15">
        <tr>
            <td width="20%" align="center">
                <img src="https://via.placeholder.com/80x80?text=MU" alt="Logo">
            </td>
            <td>
                <font color="white" size="6"><b>Mandsaur University</b></font><br>
                <font color="#BBDEFB" size="3">Excellence in Education</font>
            </td>
        </tr>
    </table>

    <!-- Navigation using table -->
    <table width="100%" bgcolor="#1565C0" cellpadding="8">
        <tr>
            <td align="center"><a href="#"><font color="white">Home</font></a></td>
            <td align="center"><a href="#"><font color="white">About</font></a></td>
            <td align="center"><a href="#"><font color="white">Departments</font></a></td>
            <td align="center"><a href="#"><font color="white">Facilities</font></a></td>
            <td align="center"><a href="#"><font color="white">Contact</font></a></td>
        </tr>
    </table>

    <!-- Content area using 2-column table -->
    <table width="90%" align="center" cellpadding="15" cellspacing="10">
        <tr>
            <!-- Left column: Image -->
            <td width="50%" valign="top">
                <img src="https://via.placeholder.com/400x300?text=Computer+Lab" 
                     alt="Computer Lab" width="100%">
                <p align="center"><b>State-of-the-Art Computer Labs</b></p>
            </td>
            <!-- Right column: Description -->
            <td width="50%" valign="top">
                <h2>Computer Labs</h2>
                <p>
                    Our computer labs are equipped with the latest hardware and 
                    software. Each lab has 60 workstations with high-speed internet.
                </p>
                <p>
                    <b>Software:</b> VS Code, MySQL, Python, Java, etc.<br>
                    <b>Operating Systems:</b> Windows 11, Ubuntu Linux<br>
                    <b>Internet:</b> 100 Mbps dedicated line
                </p>
            </td>
        </tr>
        <tr>
            <td width="50%" valign="top">
                <h2>Library</h2>
                <p>
                    The central library houses over 50,000 books and subscribes 
                    to leading journals and e-resources.
                </p>
            </td>
            <td width="50%" valign="top">
                <img src="https://via.placeholder.com/400x300?text=Library" 
                     alt="Library" width="100%">
                <p align="center"><b>Central Library</b></p>
            </td>
        </tr>
    </table>

    <!-- Footer -->
    <table width="100%" bgcolor="#0D47A1" cellpadding="10">
        <tr>
            <td align="center">
                <font color="white">&copy; 2026 Mandsaur University | All Rights Reserved</font>
            </td>
        </tr>
    </table>

</body>
</html>
```

> **Code Explanation (Lab Experiment 6):**
> - This experiment demonstrates using **tables for page layout** (an older technique — modern sites use CSS, but it's important to understand)
> - **Header table:** `width="100%"` makes it span the full browser width; the logo is in a 20%-wide cell, the title text in the remaining 80%
> - **Navigation table:** Each `<td>` holds a navigation link; `<font color="white">` makes links visible on the dark blue background
> - **Content table:** `width="90%" align="center"` creates a centred content area; two `<td>` cells with `width="50%"` and `valign="top"` create a two-column layout
> - **Image cells:** `width="100%"` on the `<img>` tag makes images fill their table cell
> - **Footer table:** A simple full-width table with a dark background and centred copyright text
> - ⚠️ **Important:** This layout technique using tables is **outdated**. In Day 12, you'll learn to create the same layout using `<div>` tags, and in Unit 4 (CSS), you'll learn Flexbox and Grid — the modern way

---

## Practice Exercise

Create a table showing the **marks of 5 students** in 4 subjects with:
- Student names in the first column
- Subject names as column headers
- Use `colspan` for a merged title row
- Use `rowspan` for merging cells where appropriate
- Calculate total marks in the last column
- Use different background colors for header, even/odd rows
- Add a `<caption>`

---

## Summary

| Tag/Attribute | Purpose |
|--------------|---------|
| `<table>` | Container for the table |
| `<tr>` | Table row |
| `<th>` | Header cell (bold, centered) |
| `<td>` | Data cell |
| `<thead>` | Semantic grouping of header rows |
| `<tbody>` | Semantic grouping of data rows |
| `<tfoot>` | Semantic grouping of footer rows |
| `<caption>` | Table title (important for accessibility) |
| `scope` | Accessibility attribute on `<th>` (`col` / `row`) |
| `border` | Border width |
| `cellpadding` | Inner space in cells |
| `cellspacing` | Space between cells |
| `colspan` | Merge columns horizontally |
| `rowspan` | Merge rows vertically |
| `bgcolor` | Background color |

### Key Rules to Remember

1. ✅ Use tables for **tabular data** (marks, timetables, price lists)
2. ❌ Do NOT use tables for **page layout** — use `<div>` and CSS instead
3. Always add `<caption>` and `scope` attributes for **accessibility**
4. Use `<thead>`, `<tbody>`, `<tfoot>` for **semantic structure**
5. `colspan` merges cells **horizontally**, `rowspan` merges **vertically**

---

*Day 10 of 55 | Unit 2 — HTML Fundamentals | Web Technology (25BCA060)*
