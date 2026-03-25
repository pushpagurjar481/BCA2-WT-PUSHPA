# Day 27 — JavaScript Functions, Loops & Arrays

🔬 **Type:** Theory + Practical
🕐 **Duration:** 2 Hours
📚 **Unit:** 5 — JavaScript
🧪 **Lab Experiment:** 18

---

## Learning Objectives

By the end of this session, students will be able to:
- Write reusable functions (declaration, expression, arrow)
- Use for, while, and for...of loops
- Work with arrays and common array methods
- Solve real-world problems using loops and functions

---

## 1. Functions

> **Analogy:** A function is like a **vending machine** — you give it input (money + selection), it processes internally, and returns output (the snack). You don't need to know how it works inside — just what goes in and what comes out.

### Function Declaration

```javascript
function greet(name) {
    return `Hello, ${name}!`;
}

console.log(greet("Rahul"));   // "Hello, Rahul!"
```

### Function Expression

```javascript
const add = function(a, b) {
    return a + b;
};

console.log(add(5, 3));   // 8
```

### Arrow Function (ES6+) ✅ Modern Syntax

```javascript
const multiply = (a, b) => a * b;

console.log(multiply(4, 5));   // 20

// Multi-line arrow function
const getGrade = (marks) => {
    if (marks >= 90) return 'A+';
    if (marks >= 75) return 'A';
    if (marks >= 60) return 'B';
    return 'C';
};
```

### Default Parameters

```javascript
function welcome(name = "Student") {
    return `Welcome, ${name}!`;
}

console.log(welcome());        // "Welcome, Student!"
console.log(welcome("Priya")); // "Welcome, Priya!"
```

---

## 2. Loops

### For Loop

```javascript
for (let i = 1; i <= 5; i++) {
    console.log(`Iteration ${i}`);
}
```

### While Loop

```javascript
let count = 1;
while (count <= 5) {
    console.log(`Count: ${count}`);
    count++;
}
```

### Do...While Loop

```javascript
let num = 1;
do {
    console.log(num);
    num++;
} while (num <= 5);
```

### For...of Loop (for arrays/strings)

```javascript
const subjects = ["HTML", "CSS", "JavaScript"];
for (const subject of subjects) {
    console.log(subject);
}
```

---

## 3. Arrays

### Creating & Accessing Arrays

```javascript
const fruits = ["Apple", "Mango", "Banana", "Orange"];

console.log(fruits[0]);       // "Apple" (index starts at 0)
console.log(fruits.length);   // 4
console.log(fruits[fruits.length - 1]);  // "Orange" (last item)
```

### Array Methods

| Method | Purpose | Example |
|--------|---------|---------|
| `push(item)` | Add to end | `fruits.push("Grape")` |
| `pop()` | Remove from end | `fruits.pop()` |
| `unshift(item)` | Add to start | `fruits.unshift("Kiwi")` |
| `shift()` | Remove from start | `fruits.shift()` |
| `indexOf(item)` | Find index | `fruits.indexOf("Mango")` → 1 |
| `includes(item)` | Check existence | `fruits.includes("Apple")` → true |
| `splice(i, n)` | Remove n items at index i | `fruits.splice(1, 1)` |
| `slice(start, end)` | Copy portion | `fruits.slice(1, 3)` |
| `join(sep)` | Array → String | `fruits.join(", ")` |
| `reverse()` | Reverse in place | `fruits.reverse()` |
| `sort()` | Sort alphabetically | `fruits.sort()` |

### Iterating Arrays

```javascript
const numbers = [10, 20, 30, 40, 50];

// forEach
numbers.forEach((num, index) => {
    console.log(`${index}: ${num}`);
});

// map — creates new array
const doubled = numbers.map(num => num * 2);
console.log(doubled);  // [20, 40, 60, 80, 100]

// filter — keeps items that pass test
const big = numbers.filter(num => num > 25);
console.log(big);  // [30, 40, 50]

// reduce — collapse to single value
const sum = numbers.reduce((total, num) => total + num, 0);
console.log(sum);  // 150
```

---

## Practical Session

### 🧪 Lab Experiment 18: Functions, Loops & Arrays

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JS Functions, Loops & Arrays</title>
    <style>
        * { box-sizing: border-box; margin: 0; padding: 0; }
        body { font-family: 'Segoe UI', sans-serif; background: #f4f4f4; padding: 30px; }
        .container { max-width: 650px; margin: 0 auto; }
        h1 { color: #1565C0; text-align: center; margin-bottom: 25px; }
        .card {
            background: white; border-radius: 10px; padding: 25px;
            margin-bottom: 20px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        }
        .card h3 { color: #333; margin-bottom: 10px; }
        input {
            width: 100%; padding: 10px; margin: 5px 0 10px;
            border: 1px solid #ddd; border-radius: 5px; font-size: 15px;
        }
        button {
            padding: 10px 25px; background: #1565C0; color: white;
            border: none; border-radius: 5px; cursor: pointer; font-size: 15px;
        }
        button:hover { background: #0D47A1; }
        .result {
            margin-top: 10px; padding: 15px; background: #E8F5E9;
            border-radius: 5px; white-space: pre-line; display: none;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>JavaScript Functions & Arrays</h1>

        <!-- 1. Multiplication Table -->
        <div class="card">
            <h3>1. Multiplication Table</h3>
            <input type="number" id="tableNum" placeholder="Enter a number (e.g., 7)">
            <button onclick="showTable()">Generate Table</button>
            <div class="result" id="tableResult"></div>
        </div>

        <!-- 2. Fibonacci Series -->
        <div class="card">
            <h3>2. Fibonacci Series</h3>
            <input type="number" id="fibCount" placeholder="How many terms? (e.g., 10)">
            <button onclick="showFibonacci()">Generate</button>
            <div class="result" id="fibResult"></div>
        </div>

        <!-- 3. Array Operations -->
        <div class="card">
            <h3>3. Student Marks Analyzer</h3>
            <input type="text" id="marksInput" placeholder="Enter marks separated by commas (e.g., 78, 92, 65, 88, 45)">
            <button onclick="analyzeMarks()">Analyze</button>
            <div class="result" id="marksResult"></div>
        </div>

        <!-- 4. Factorial -->
        <div class="card">
            <h3>4. Factorial Calculator</h3>
            <input type="number" id="factNum" placeholder="Enter a number (e.g., 6)">
            <button onclick="showFactorial()">Calculate</button>
            <div class="result" id="factResult"></div>
        </div>
    </div>

    <script>
        function showResult(id, text) {
            const el = document.getElementById(id);
            el.textContent = text;
            el.style.display = 'block';
        }

        // 1. Multiplication Table using loop
        function showTable() {
            const num = parseInt(document.getElementById('tableNum').value);
            if (isNaN(num)) { showResult('tableResult', 'Enter a valid number!'); return; }
            
            let table = '';
            for (let i = 1; i <= 10; i++) {
                table += `${num} × ${i} = ${num * i}\n`;
            }
            showResult('tableResult', table);
        }

        // 2. Fibonacci using function
        function fibonacci(n) {
            const fib = [0, 1];
            for (let i = 2; i < n; i++) {
                fib.push(fib[i - 1] + fib[i - 2]);
            }
            return fib.slice(0, n);
        }

        function showFibonacci() {
            const n = parseInt(document.getElementById('fibCount').value);
            if (isNaN(n) || n < 1 || n > 50) {
                showResult('fibResult', 'Enter a number between 1 and 50!');
                return;
            }
            const series = fibonacci(n);
            showResult('fibResult', `Fibonacci (${n} terms):\n${series.join(', ')}`);
        }

        // 3. Array Analysis
        function analyzeMarks() {
            const input = document.getElementById('marksInput').value;
            const marks = input.split(',').map(s => parseFloat(s.trim())).filter(n => !isNaN(n));
            
            if (marks.length === 0) {
                showResult('marksResult', 'Enter valid marks!');
                return;
            }

            const sum = marks.reduce((a, b) => a + b, 0);
            const avg = sum / marks.length;
            const max = Math.max(...marks);
            const min = Math.min(...marks);
            const sorted = [...marks].sort((a, b) => b - a);
            const passed = marks.filter(m => m >= 40).length;
            const failed = marks.length - passed;

            showResult('marksResult',
                `Total Students: ${marks.length}\n` +
                `Sum: ${sum}\n` +
                `Average: ${avg.toFixed(2)}\n` +
                `Highest: ${max}\n` +
                `Lowest: ${min}\n` +
                `Passed (≥40): ${passed}\n` +
                `Failed (<40): ${failed}\n` +
                `Sorted (desc): ${sorted.join(', ')}`
            );
        }

        // 4. Factorial using recursion
        function factorial(n) {
            if (n <= 1) return 1;
            return n * factorial(n - 1);
        }

        function showFactorial() {
            const n = parseInt(document.getElementById('factNum').value);
            if (isNaN(n) || n < 0 || n > 20) {
                showResult('factResult', 'Enter a number between 0 and 20!');
                return;
            }
            showResult('factResult', `${n}! = ${factorial(n)}`);
        }
    </script>

</body>
</html>
```

---

## Summary

| Concept | Key Syntax |
|---------|-----------|
| Function declaration | `function name(params) { }` |
| Arrow function | `const fn = (a, b) => a + b;` |
| For loop | `for (let i = 0; i < n; i++) { }` |
| For...of | `for (const item of array) { }` |
| Array push/pop | `arr.push()`, `arr.pop()` |
| forEach/map/filter | `arr.map(fn)`, `arr.filter(fn)` |
| reduce | `arr.reduce((sum, n) => sum + n, 0)` |

---

*Day 27 of 55 | Unit 5 — JavaScript | Web Technology (25BCA060)*
