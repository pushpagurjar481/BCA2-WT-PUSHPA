# Day 33 — Bootstrap Components: Cards, Tables & Images

🔬 **Type:** Theory + Practical
🕐 **Duration:** 2 Hours
📚 **Unit:** 6 — Bootstrap
🧪 **Lab Experiment:** 16

---

## Learning Objectives

By the end of this session, students will be able to:
- Create Bootstrap cards with headers, images, and footers
- Style tables using Bootstrap's table classes
- Use Bootstrap's responsive image and figure classes
- Combine cards in a responsive grid layout

---

## 1. Bootstrap Cards

```html
<!-- Basic Card -->
<div class="card" style="width: 18rem;">
    <img src="https://via.placeholder.com/300x180?text=Course+Image" 
         class="card-img-top" alt="Course">
    <div class="card-body">
        <h5 class="card-title">Web Technology</h5>
        <p class="card-text">Learn HTML, CSS, JavaScript, and Bootstrap.</p>
        <a href="#" class="btn btn-primary">Learn More</a>
    </div>
</div>

<!-- Card with Header/Footer -->
<div class="card">
    <div class="card-header bg-primary text-white">Featured Course</div>
    <div class="card-body">
        <h5 class="card-title">Data Structures</h5>
        <p class="card-text">Arrays, Linked Lists, Trees, and Graphs.</p>
    </div>
    <div class="card-footer text-muted">Last updated: April 2026</div>
</div>

<!-- Card with List Group -->
<div class="card">
    <div class="card-header">Semesters</div>
    <ul class="list-group list-group-flush">
        <li class="list-group-item">Semester I</li>
        <li class="list-group-item active">Semester II (Current)</li>
        <li class="list-group-item">Semester III</li>
    </ul>
</div>
```

---

## 2. Bootstrap Tables

```html
<!-- Basic Styled Table -->
<table class="table">
    <thead><tr><th>#</th><th>Name</th><th>Marks</th></tr></thead>
    <tbody>
        <tr><td>1</td><td>Rahul</td><td>85</td></tr>
        <tr><td>2</td><td>Priya</td><td>92</td></tr>
    </tbody>
</table>

<!-- Striped + Hoverable + Bordered -->
<table class="table table-striped table-hover table-bordered">
    ...
</table>

<!-- Dark Table -->
<table class="table table-dark table-striped">
    ...
</table>

<!-- Responsive Table (horizontal scroll on small screens) -->
<div class="table-responsive">
    <table class="table">...</table>
</div>
```

### Table Classes

| Class | Effect |
|-------|--------|
| `table` | Basic styling |
| `table-striped` | Zebra striping |
| `table-hover` | Highlight on hover |
| `table-bordered` | Borders on all sides |
| `table-borderless` | No borders |
| `table-dark` | Dark background |
| `table-sm` | Compact (less padding) |
| `table-responsive` | Horizontal scroll |

### Row Colors

```html
<tr class="table-success">Green row</tr>
<tr class="table-danger">Red row</tr>
<tr class="table-warning">Yellow row</tr>
<tr class="table-info">Light blue row</tr>
<tr class="table-primary">Blue row</tr>
```

---

## 3. Bootstrap Images

```html
<!-- Responsive image (max-width: 100%) -->
<img src="photo.jpg" class="img-fluid" alt="Responsive image">

<!-- Rounded corners -->
<img src="photo.jpg" class="img-fluid rounded" alt="Rounded">

<!-- Circle (works best with square images) -->
<img src="photo.jpg" class="rounded-circle" alt="Circle" width="150">

<!-- Thumbnail (border + padding) -->
<img src="photo.jpg" class="img-thumbnail" alt="Thumbnail" width="200">

<!-- Figure with caption -->
<figure class="figure">
    <img src="photo.jpg" class="figure-img img-fluid rounded" alt="Photo">
    <figcaption class="figure-caption text-center">BCA Department Building</figcaption>
</figure>
```

---

## Practical Session

### 🧪 Lab Experiment 16: Cards, Tables & Components

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bootstrap Components</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body class="bg-light">

    <!-- Header -->
    <div class="bg-primary text-white text-center py-4 mb-4">
        <h1 class="mb-0">Bootstrap Components</h1>
        <p class="lead mb-0">Cards, Tables & Images</p>
    </div>

    <div class="container">

        <!-- Card Grid -->
        <h2 class="text-primary mb-3">Course Cards</h2>
        <div class="row g-4 mb-5">
            <div class="col-md-6 col-lg-4">
                <div class="card h-100 shadow-sm">
                    <div class="bg-primary text-white text-center py-4">
                        <span style="font-size: 3em;">🌐</span>
                    </div>
                    <div class="card-body">
                        <h5 class="card-title">Web Technology</h5>
                        <p class="card-text">Build modern websites using HTML5, CSS3, JavaScript, and Bootstrap.</p>
                    </div>
                    <div class="card-footer d-flex justify-content-between align-items-center">
                        <small class="text-muted">Semester II</small>
                        <a href="#" class="btn btn-sm btn-primary">View</a>
                    </div>
                </div>
            </div>
            <div class="col-md-6 col-lg-4">
                <div class="card h-100 shadow-sm">
                    <div class="bg-success text-white text-center py-4">
                        <span style="font-size: 3em;">📊</span>
                    </div>
                    <div class="card-body">
                        <h5 class="card-title">Data Structures</h5>
                        <p class="card-text">Master arrays, linked lists, trees, graphs, and algorithms.</p>
                    </div>
                    <div class="card-footer d-flex justify-content-between align-items-center">
                        <small class="text-muted">Semester II</small>
                        <a href="#" class="btn btn-sm btn-success">View</a>
                    </div>
                </div>
            </div>
            <div class="col-md-6 col-lg-4">
                <div class="card h-100 shadow-sm">
                    <div class="bg-warning text-center py-4">
                        <span style="font-size: 3em;">🧮</span>
                    </div>
                    <div class="card-body">
                        <h5 class="card-title">Mathematics</h5>
                        <p class="card-text">Discrete math, probability theory, and linear algebra.</p>
                    </div>
                    <div class="card-footer d-flex justify-content-between align-items-center">
                        <small class="text-muted">Semester II</small>
                        <a href="#" class="btn btn-sm btn-warning">View</a>
                    </div>
                </div>
            </div>
        </div>

        <!-- Student Table -->
        <h2 class="text-primary mb-3">Student Records</h2>
        <div class="table-responsive mb-5">
            <table class="table table-striped table-hover table-bordered align-middle">
                <thead class="table-dark">
                    <tr>
                        <th>#</th>
                        <th>Name</th>
                        <th>Roll No</th>
                        <th>Web Tech</th>
                        <th>Data Structures</th>
                        <th>Mathematics</th>
                        <th>Total</th>
                        <th>Grade</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>1</td><td>Rahul Kumar</td><td>25BCA001</td>
                        <td>85</td><td>78</td><td>92</td>
                        <td class="fw-bold">255</td>
                        <td><span class="badge bg-success">A</span></td>
                    </tr>
                    <tr>
                        <td>2</td><td>Priya Sharma</td><td>25BCA002</td>
                        <td>92</td><td>88</td><td>95</td>
                        <td class="fw-bold">275</td>
                        <td><span class="badge bg-primary">A+</span></td>
                    </tr>
                    <tr>
                        <td>3</td><td>Amit Patel</td><td>25BCA003</td>
                        <td>65</td><td>72</td><td>58</td>
                        <td class="fw-bold">195</td>
                        <td><span class="badge bg-warning text-dark">B</span></td>
                    </tr>
                    <tr class="table-danger">
                        <td>4</td><td>Neha Singh</td><td>25BCA004</td>
                        <td>35</td><td>42</td><td>38</td>
                        <td class="fw-bold">115</td>
                        <td><span class="badge bg-danger">F</span></td>
                    </tr>
                    <tr>
                        <td>5</td><td>Vikram Joshi</td><td>25BCA005</td>
                        <td>78</td><td>82</td><td>75</td>
                        <td class="fw-bold">235</td>
                        <td><span class="badge bg-success">A</span></td>
                    </tr>
                </tbody>
            </table>
        </div>

        <!-- List Group -->
        <h2 class="text-primary mb-3">Quick Links</h2>
        <div class="row mb-5">
            <div class="col-md-6">
                <div class="list-group">
                    <a href="#" class="list-group-item list-group-item-action active">Current Semester</a>
                    <a href="#" class="list-group-item list-group-item-action">Syllabus Download</a>
                    <a href="#" class="list-group-item list-group-item-action">Time Table</a>
                    <a href="#" class="list-group-item list-group-item-action">Exam Schedule</a>
                    <a href="#" class="list-group-item list-group-item-action disabled">Results (Coming Soon)</a>
                </div>
            </div>
        </div>

    </div>

    <!-- Footer -->
    <div class="bg-dark text-white text-center py-3 mt-4">
        <p class="mb-0">&copy; 2026 Mandsaur University</p>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```

---

## Summary

| Component | Key Classes |
|-----------|------------|
| Card | `card`, `card-body`, `card-title`, `card-img-top` |
| Table | `table`, `table-striped`, `table-hover`, `table-bordered` |
| Images | `img-fluid`, `rounded-circle`, `img-thumbnail` |
| List Group | `list-group`, `list-group-item` |
| Badges | `badge bg-primary` |

---

*Day 33 of 55 | Unit 6 — Bootstrap | Web Technology (25BCA060)*
