# JavaScript Basics — Complete Guide

**Source :** [Ashraful-Momen/Web-Development-With-React-And-Django](https://github.com/Ashraful-Momen/Web-Development-With-React-And-Django/tree/main/JavaScript)


---

## Table of Contents

| # | Topic | Source Path |
| --- | --- | --- |
| 1 | JavaScript Output & Setup | `1. Now Starting Coding` |
| 2 | Variables & Constants | `2. Variable and Constent` |
| 3 | Operators | `3. Operator` |
| 4 | Data Types | `4. Data Types` |
| 5 | Template Literals (ES6) | `5. Templete Letarals ES6` |
| 6 | Conditions | `6. Condition` |
| 7 | Loops | `7. Loop` |
| 8 | Functions | `8. Function` |
| 9 | Object Oriented Programming | `9. Object Oriented Programming` |
| 10 | DOM — Document Object Model | `10. DOM- Document Object Model` |
| 11 | Error Handling | `11. Error Handling` |
| 12 | Regular Expression | `12. Regular Expression` |
| 13 | JSON | `13. JSON` |
| 14 | AJAX | `14. Ajax` |
| 15 | Fetch API | `15. Fetch APi` |
| 16 | Project 1 — Todo App | `16. Project 1- todo App` |
| 17 | Project 2 — Book List | `17. Project 2- Book List` |
| 18 | Project 3 — GitHub API (CRUD) | `18. Project 3- GitHub API (CRUD)` |
| 19 | Leveling up to ES6 | `19. Leveling up To ES6` |
| 20 | Browser Object Model (BOM) | `JS - BOM` |

---

# 1. JavaScript Output & Setup

The very first concepts: how to output text, where to put `<script>` tags, syntax basics, comments, and how to read user input.

---

## Connecting a JS File to HTML

There are two ways to run JavaScript:

- **Inline** — between `<script>...</script>` tags inside the HTML page.
- **External** — in a separate `.js` file, loaded with `<script src="..."></script>`.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script src="/js/script.js"></script>
</body>
</html>
```

> Place the `<script>` tag just before `</body>` so the DOM is fully loaded before the script runs.

---

## Output Channels

JavaScript gives you **four** ways to display output:

| Method | Purpose | Example |
| --- | --- | --- |
| `alert("msg")` | Popup dialog box | `alert("Hello!");` |
| `document.write("msg")` | Write directly to the HTML page | `document.write("Hi");` |
| `document.getElementById("id").innerHTML = "msg"` | Inject HTML into a specific element | `document.getElementById("root").innerHTML = "I love JS";` |
| `console.log("msg")` | Print to the browser **DevTools console** | `console.log("Hello");` |

```javascript
// window.alert('Hello Shuvo!');
// alert("Hello ...!");
// document.write('Practise the JS');

// document.getElementById('root').innerHTML = "I love My Creator";
// document.getElementById('header').innerHTML = "Sent to H1";

// console.log("Hello I'm Practising the JS");
```

> In production you almost never use `document.write` — it overwrites the whole page after load. `console.log` is your friend while developing.

---

## Statement, Syntax & Comments

```javascript
// single-line comment

/*
   multi-line
   block comment
*/

let x = 5;            // a statement ends with a semicolon
let y = 10;           // JS is case-sensitive: 'X' and 'x' are different
```

JavaScript is **case-sensitive**, ignores whitespace, and treats every line ending with `;` as a complete statement.

---

## User Input

```javascript
var name;

name = prompt('Enter your name: ');

console.log(name);     // shows in DevTools
document.write(name);  // shows on the page
```

| Function | Returns |
| --- | --- |
| `prompt("msg")` | The string the user typed (or `null` if they hit Cancel). |
| `alert("msg")` | `undefined` — only displays a popup. |
| `confirm("msg")` | `true` (OK) or `false` (Cancel). |

`prompt()` **always returns a string** — convert with `parseInt()` / `parseFloat()` before doing math.

---

# 2. Variables & Constants

JavaScript has three keywords for declaring variables: `var`, `let`, and `const`.

```javascript
// var a = 20;
// let b = 30;

// var c = a;
// console.log(c);       // 20
// a = 44;
// console.log(c);       // still 20 — primitive copy, no reference shared

const pi = 3.1416;     // const MUST be initialized at declaration
```

| Keyword | Scope | Reassign | Re-declare | Hoisted |
| --- | --- | --- | --- | --- |
| `var` | Function | Yes | Yes | Yes (as `undefined`) |
| `let` | Block `{}` | Yes | No | Yes (temporal dead zone) |
| `const` | Block `{}` | **No** | No | Yes (temporal dead zone) |

> **Rules for valid names:**
> - Must start with a letter, `_`, or `$`.
> - Can contain letters, digits, `_`, `$` afterwards.
> - Cannot be a reserved keyword (`let`, `return`, `class`, …).
> - Hyphens are **not** allowed (`name-First` is illegal).

```javascript
// let a;
// let b = a;
// a = 90;

// console.log(b);     // undefined  — copying 'undefined' before assignment
```

`undefined` is what you get when you read a variable that was declared but never assigned.

---

# 3. Operators

## Arithmetic Operators

```javascript
a = 5;
b = 6;

console.log(a + b);      // 11
console.log(a - b);      // -1
console.log(a * b);      // 30
console.log(a / b);      // 0.8333333333333334
console.log(a ** b);     // 15625   (exponent)
console.log(a++);        // 5       (post-increment — returns OLD value)
console.log(++a);        // 7       (pre-increment  — returns NEW value)
```

| Operator | Name | Example | Result |
| --- | --- | --- | --- |
| `+` | Addition | `5 + 6` | `11` |
| `-` | Subtraction | `5 - 6` | `-1` |
| `*` | Multiplication | `5 * 6` | `30` |
| `/` | Division | `5 / 6` | `0.833…` |
| `**` | Exponent | `5 ** 6` | `15625` |
| `%` | Modulus | `5 % 6` | `5` |
| `++` | Increment | `a++` / `++a` | adds 1 |
| `--` | Decrement | `a--` / `--a` | subtracts 1 |

**Operator arity**

| Arity | Meaning | Example |
| --- | --- | --- |
| **Unary** | one operand | `++a`, `-x`, `typeof x` |
| **Binary** | two operands | `a + b`, `a * b` |
| **Ternary** | three operands | `cond ? a : b` |

---

## String Operator — `+`

```javascript
let firstName = "Ashraful";
let lastName  = "Momen";

console.log(firstName + " " + lastName);   // "Ashraful Momen"
```

`+` is **overloaded**: it adds numbers, but **concatenates** when either side is a string.

---

## Comparison & Logical Operators

```javascript
// Comparison: ==, ===, !=, !==, >, <, >=, <=
// Logical:    &&, ||, !

// Example:
if (age >= 80 && age <= 100) {
    console.log("A+");
} else if (age >= 70 && age < 80) {
    console.log("A");
}
```

| Operator | Meaning | Loose vs Strict |
| --- | --- | --- |
| `==` | Equal | Loose — `5 == "5"` → `true` |
| `===` | Strict equal | Strict — `5 === "5"` → `false` |
| `!=` | Not equal | Loose |
| `!==` | Strict not equal | Strict |
| `&&` | AND | Both sides true |
| `\|\|` | OR | Either side true |
| `!` | NOT | Flips the boolean |

---

# 4. Data Types

JavaScript has **8 data types** — 7 primitives and 1 reference type.

| Type | Category | Example |
| --- | --- | --- |
| `string` | Primitive | `"hello"`, `'hi'`, `` `tpl` `` |
| `number` | Primitive | `42`, `3.14`, `NaN` |
| `boolean` | Primitive | `true`, `false` |
| `null` | Primitive | `null` (intentional empty) |
| `undefined` | Primitive | `undefined` (not assigned) |
| `bigint` | Primitive | `9007199254740993n` |
| `symbol` | Primitive | `Symbol("id")` |
| `object` | Reference | `{...}`, `[...]`, `function(){...}` |

```javascript
// Different Type of Data demo:
let name     = "Ashraful";    // string
let age      = 25;            // number
let isPassed = true;          // boolean
let nothing  = null;          // null
let notSet;                   // undefined

console.log(typeof name);     // "string"
console.log(typeof age);      // "number"
console.log(typeof isPassed); // "boolean"
console.log(typeof nothing);  // "object"  ← known JS quirk
console.log(typeof notSet);   // "undefined"
```

> 🧐 `typeof null === "object"` is a famous 25-year-old bug in JavaScript, kept for compatibility.

---

## Strings & Booleans

```javascript
// Strings are immutable — methods return NEW strings.
let msg = "Hello World";

msg.length                    // 11
msg.toUpperCase()             // "HELLO WORLD"
msg.toLowerCase()             // "hello world"
msg.indexOf("World")          // 6
msg.slice(0, 5)               // "Hello"
msg.replace("World", "JS")    // "Hello JS"
msg.split(" ")                // ["Hello", "World"]

// Template literals (ES6):
let name = "Shuvo";
let greet = `Hello, ${name}!`;
```

Boolean — only two values: `true` and `false`. Anything can be **coerced** to one:

| Value | Coerced |
| --- | --- |
| `0`, `""`, `null`, `undefined`, `NaN` | `false` (falsy) |
| anything else | `true` (truthy) |

---

## Arrays

> Properties: **ordered**, **mutable / changeable**, **duplicates allowed**, **heterogeneous types allowed**.

```javascript
let fruits = ["apple", "banana", "mango", 1, 3.14, true];
console.log(fruits[0]);        // "apple"
console.log(fruits[fruits.length - 1]);  // last item
```

### Array Methods — Quick Reference

| # | Method | What it does |
| --- | --- | --- |
| 1 | `arr.push(item)` | Add to the end. |
| 2 | `arr.pop()` | Remove from the end. |
| 3 | `arr.unshift(item)` | Add to the start. |
| 4 | `arr.shift()` | Remove from the start. |
| 5 | `arr.splice(i, n, ...items)` | Remove/replace at index. |
| 6 | `arr.slice(start, end)` | Returns a new sub-array. |
| 7 | `arr.indexOf(item)` | First index of item, or `-1`. |
| 8 | `arr.includes(item)` | `true` / `false`. |
| 9 | `arr.concat(arr2)` | Merge into new array. |
| 10 | `arr.reverse()` | Reverse in place. |
| 11 | `arr.sort()` | Sort in place (as strings by default). |
| 12 | `arr.map(fn)` | New array of transformed items. |
| 13 | `arr.filter(fn)` | New array of items that pass the test. |
| 14 | `arr.reduce(fn, init)` | Accumulate to single value. |
| 15 | `arr.forEach(fn)` | Run `fn` for each item. |
| 16 | `arr.find(fn)` | First item that matches. |
| 17 | `arr.some(fn)` | `true` if any match. |
| 18 | `arr.every(fn)` | `true` if all match. |

```javascript
let nums = [1, 2, 3, 4, 5];

nums.push(6);                       // [1,2,3,4,5,6]
nums.pop();                         // [1,2,3,4,5]
nums.unshift(0);                    // [0,1,2,3,4,5]

let doubled = nums.map(n => n * 2); // [0,2,4,6,8,10]
let even    = nums.filter(n => n % 2 === 0); // [0,2,4]
let sum     = nums.reduce((a, b) => a + b, 0); // 15
```

---

## Objects

> Properties: **unordered**, **mutable**, **keys are unique**.

```javascript
let person = {
    name: "Ashraful",
    age: 25,
    isStudent: true,
    hobbies: ["coding", "reading"],
    address: { city: "Dhaka", zip: 1207 }
};

// Access
console.log(person.name);           // dot notation
console.log(person["age"]);         // bracket notation

// Add / update
person.email = "ash@example.com";
person.age = 26;

// Delete
delete person.isStudent;

// Loop through
for (let key in person) {
    console.log(key, "=>", person[key]);
}

// Keys / values / entries
Object.keys(person);
Object.values(person);
Object.entries(person);
```

---

## `undefined`, Empty Values, `null`, `NaN`

```javascript
let a;                  // undefined  (declared, never assigned)
let b = null;           // null       (intentionally empty)
let c = "";             // empty string — falsy but not undefined
let d = NaN;            // "Not a Number" — result of failed math

console.log(typeof a);  // "undefined"
console.log(typeof b);  // "object"  (JS quirk)
console.log(typeof c);  // "string"
console.log(typeof d);  // "number"  (!)
```

`NaN === NaN` is `false`. Use `Number.isNaN(x)` to test.

---

## Primitive vs Reference Types

```javascript
// Primitive — copied BY VALUE
let x = 10;
let y = x;
y = 20;
console.log(x);   // 10   (unchanged)

// Reference — copied BY REFERENCE
let arr1 = [1, 2, 3];
let arr2 = arr1;
arr2.push(4);
console.log(arr1);  // [1,2,3,4]   (BOTH changed)
```

| Type | Copied as | Comparison `===` |
| --- | --- | --- |
| Primitive (`string`, `number`, …) | **Value** | Same value → `true` |
| Reference (`object`, `array`) | **Reference** | Same memory address → `true` |

---

# 5. Template Literals (ES6)

Template literals use **backticks** `` ` `` and `${...}` for interpolation and `${ expression }` for any JS expression.

```javascript
let name = "Ashraful";
let age  = 25;

// Multi-line + interpolation
let bio = `
    Name: ${name}
    Age : ${age}
    Next year: ${age + 1}
`;

console.log(bio);
```

```javascript
function tag(strings, ...values) {
    console.log(strings);   // raw string parts
    console.log(values);    // interpolated values
}

let mood = "happy";
tag`I am ${mood} on ${new Date().toDateString()}`;
```

---

# 6. Conditions

## `if` / `else if` / `else`

The first matching branch runs; the rest are skipped.

```javascript
var age = prompt("Enter Your Marks:");

if (age >= 80 && age <= 100) {
    console.log("A+");
} else if (age >= 70 && age < 80) {
    console.log("A");
} else if (age > 0 && age < 69) {
    console.log("You did not pass.");
} else {
    console.log("Invalid input.");
}
```

---

## Nested `if` — Find the Largest of Three

```javascript
var n1 = parseInt(prompt("Enter number1:"));
var n2 = parseInt(prompt("Enter number2:"));
var n3 = parseInt(prompt("Enter number3:"));

if (n1 > n2 && n1 > n3) {
    console.log(`${n1} is Big`);
} else if (n2 > n1 && n2 > n3) {
    console.log(`${n2} is Big`);
} else {
    console.log(`${n3} is Big`);
}
```

---

## `switch` / `case`

```javascript
let day = new Date().getDay();

switch (day) {
    case 0: console.log("Sunday"); break;
    case 1: console.log("Monday"); break;
    case 2: console.log("Tuesday"); break;
    case 6: console.log("Saturday"); break;
    default: console.log("Other day");
}
```

> Without `break`, execution **falls through** to the next case.

---

## Ternary Operator

```javascript
let age = 20;
let status = (age >= 18) ? "adult" : "minor";

// Multiple ternaries (use sparingly):
let grade = score >= 80 ? "A+" :
            score >= 70 ? "A"  :
            score >= 60 ? "B"  : "F";
```

---

# 7. Loops

## `while` Loop

```javascript
let i = 1;
while (i <= 5) {
    console.log(`value of i => ${i}`);
    i++;        // ALWAYS update the counter — or infinite loop!
}
```

## `do…while` Loop

Runs the body **at least once** before checking the condition.

```javascript
let i = 1;
do {
    console.log(`value of i => ${i}`);
    i++;
} while (i <= 5);
```

## `for` Loop

```javascript
for (let i = 1; i <= 5; i++) {
    console.log("the value of i -> " + i);
}
console.log("I am out of the For-loop");
```

---

## `break` vs `continue`

| Statement | Effect |
| --- | --- |
| `break` | **Exits** the loop entirely. |
| `continue` | **Skips** to the next iteration. |

```javascript
// continue — skip 5
for (let i = 1; i < 11; i++) {
    if (i == 5) {
        console.log('****the value of 5 will be skipped');
        continue;
    }
    console.log(`The value of I => ${i}`);
}

// break — exit at 5
for (let i = 1; i < 11; i++) {
    if (i == 5) {
        console.log('****stopping at 5');
        break;
    }
    console.log(`The value of I => ${i}`);
}
```

---

## Sum & Factorial — Real Example

```javascript
let sum = 0;
let factorial = 1;
let i = 1;

while (i <= 10) {
    sum += i;
    factorial *= i;
    i++;
}

console.log("Sum:", sum);          // 55
console.log("Factorial:", factorial);  // 3628800
```

---

## `for…in` vs `for…of`

```javascript
// for…in  → keys of an object (or indices of an array)
const person = { name: "Ash", age: 25 };
for (let key in person) {
    console.log(key, "->", person[key]);
}

// for…of  → values of an iterable (array, string, map, set)
const fruits = ["apple", "banana", "mango"];
for (let fruit of fruits) {
    console.log(fruit);
}
```

| Loop | Works on | Gives you |
| --- | --- | --- |
| `for…in` | objects / arrays | property **keys** |
| `for…of` | iterables (array, string, Map, Set) | **values** |

---

## Array Iteration — `forEach` / `map` / `filter` / `reduce`

```javascript
const nums = [1, 2, 3, 4, 5];

// forEach — side effects
nums.forEach((n, i) => console.log(`${i}: ${n}`));

// map — transform
const doubled = nums.map(n => n * 2);       // [2,4,6,8,10]

// filter — keep some
const even = nums.filter(n => n % 2 === 0); // [2,4]

// reduce — accumulate
const sum = nums.reduce((acc, n) => acc + n, 0); // 15
```

---

# 8. Functions

## Three Ways to Define a Function

```javascript
// 1. Function declaration (hoisted)
function printName(name) {
    console.log("Hello", name);
}

// 2. Function expression (NOT hoisted)
var printName2 = function (name) {
    console.log("hello", name);
};

// 3. Arrow function (ES6) — short, no own `this`
var printName3 = (name) => {
    console.log("hello", name);
};

printName("Ashraful");
printName2("Momen");
printName3("Shuvo");
```

| Form | Syntax | Hoisted? | Own `this`? |
| --- | --- | --- | --- |
| Declaration | `function name(){}` | ✅ | ✅ |
| Expression | `var x = function(){}` | ❌ | ✅ |
| Arrow | `var x = () => {}` | ❌ | ❌ (lexical) |

---

## Parameters & Default Values

```javascript
function saySomething(fname = "Fazle", lname = "Rahat") {
    console.log(`Hello ${fname} ${lname}!`);
}

saySomething("Simanta", "Paul");   // Hello Simanta Paul!
saySomething();                    // Hello Fazle Rahat!

function addNum(a = 0, b = 0) {
    console.log(a + b);
}
addNum(4, 5);      // 9
addNum(3.6, 2.3);  // 5.9
```

---

## Return Values

```javascript
function add(a, b) {
    return a + b;       // send a value back
}

let result = add(3, 4); // 7
```

Without an explicit `return`, the function returns `undefined`.

---

## Math & Date Objects

```javascript
// Math
Math.min(20, 10);      // 10
Math.max(20, 10);      // 20
Math.abs(-10);         // 10
Math.sqrt(10);         // 3.162…
Math.round(3.5);       // 4
Math.floor(3.5);       // 3
Math.ceil(3.5);        // 4
Math.exp(3);           // 20.085…
Math.random();         // 0 ≤ x < 1

// Date
const now = new Date();
now.getFullYear();     // 2026
now.getMonth();        // 0-11
now.getDate();         // 1-31
now.getDay();          // 0-6 (Sun-Sat)
now.getHours();        // 0-23
now.toDateString();    // "Tue Sep 30 2026"
```

---

## Global vs Local Scope

```javascript
// Global
var globalVar = "I am global";

function test() {
    // Local — only inside this function
    var localVar = "I am local";
    console.log(globalVar);   // ✅
    console.log(localVar);    // ✅
}

test();
console.log(globalVar);       // ✅
console.log(localVar);        // ❌ ReferenceError
```

`var` is **function-scoped**; `let` and `const` are **block-scoped** (only live inside the nearest `{}`).

---

# 9. Object-Oriented Programming

## Class — Blueprint for Objects

> A **class** is a template. The variables inside are **properties**; the functions inside are **methods**.

```javascript
class Person {
    constructor(FName, LName, dob) {
        this.FirstName = FName;
        this.LastName  = LName;
        this.dob       = dob;
    }

    calculateAge() {
        let birthday = new Date(this.dob);
        let diff     = Date.now() - birthday.getTime();
        let ageDate  = new Date(diff);
        return Math.abs(ageDate.getUTCFullYear() - 1970);
    }

    fullName() {
        console.log(`Your Full Name is : ${this.FirstName} ${this.LastName}`);
    }
}

const person1 = new Person("Ashraful", "Momen", "10-28-1995");

console.log(person1.calculateAge());
person1.fullName();
```

---

## Inheritance — SubClass

```javascript
class Student extends Person {
    constructor(FName, LName, dob, studentId) {
        super(FName, LName, dob);   // call parent constructor
        this.studentId = studentId;
    }

    // override
    fullName() {
        super.fullName();
        console.log(`Student ID: ${this.studentId}`);
    }
}

const s = new Student("Ash", "Momen", "10-28-1995", "S-101");
s.fullName();
```

| Keyword | Purpose |
| --- | --- |
| `extends` | Inherit from a parent class. |
| `super()` | Call the parent constructor / method. |
| `this` | Reference the current instance. |

---

## Static Methods & Properties

Belong to the **class itself**, not to instances.

```javascript
class MathHelper {
    static PI = 3.1416;

    static add(a, b) {
        return a + b;
    }
}

console.log(MathHelper.PI);       // 3.1416
console.log(MathHelper.add(2, 3)); // 5
```

---

# 10. DOM — Document Object Model

The DOM is the browser's in-memory tree representation of your HTML page. With JavaScript you can **read** and **change** any node.

## Exploring the DOM

```html
<h1 id="header">Some Random Content</h1>
<ol>
    <li>C++</li>
    <li>Java</li>
    <li>Python</li>
    <li>PHP</li>
</ol>

<a href="https://www.google.com" class="root-1 root2">Google</a>
```

```javascript
// Read children, attributes, text
document.documentElement;        // <html>
document.head;
document.body;
document.title;
document.links;
document.forms;
document.images;
```

---

## Selectors — Single Element

| API | Selects |
| --- | --- |
| `document.getElementById("id")` | One element by `id` |
| `document.querySelector("css")` | First element matching any CSS selector |

```javascript
const header = document.getElementById("header");
const firstLink = document.querySelector(".root-1");
```

---

## Selectors — Multiple Elements

| API | Returns |
| --- | --- |
| `document.getElementsByClassName("cls")` | Live HTMLCollection |
| `document.getElementsByTagName("li")` | Live HTMLCollection |
| `document.querySelectorAll("li")` | Static NodeList |

```javascript
const items = document.querySelectorAll("li");
items.forEach(li => console.log(li.textContent));
```

---

## Traversing the DOM

```javascript
const el = document.querySelector("li");

el.parentElement;          // <ol>
el.children;               // HTMLCollection of <li> siblings
el.previousElementSibling; // the <li> above
el.nextElementSibling;     // the <li> below
el.firstElementChild;
el.lastElementChild;
```

---

## Create / Replace / Remove

```javascript
// Create
const li = document.createElement("li");
li.className = "list-item";
li.textContent = "JavaScript";
li.setAttribute("id", "js-li");

// Append
document.querySelector("ol").appendChild(li);

// Replace
const old = document.getElementById("old-li");
old.replaceWith(li);

// Remove
document.querySelector("li:last-child").remove();
```

---

## Events — Part 1

**Three ways to bind an event:**

```html
<!-- 1) Inline (avoid in real apps) -->
<button onclick="alert('Hello!');">Click Me</button>

<!-- 2) Element property -->
<button id="sample">Click</button>
<script>
document.getElementById("sample").onclick = function () {
    alert("Clicked via property!");
};
</script>

<!-- 3) addEventListener (preferred) -->
<script>
document.getElementById("sample").addEventListener("click", function () {
    alert("Clicked via listener!");
});
</script>
```

| Common events | When they fire |
| --- | --- |
| `click` | element clicked |
| `mouseover` / `mouseout` | pointer enters / leaves |
| `keydown` / `keyup` / `keypress` | keyboard |
| `submit` | form submitted |
| `change` / `input` | input value changed |
| `load` | page finished loading |
| `DOMContentLoaded` | HTML parsed (no CSS/images) |

---

## Events — Part 2 — `event` Object & Delegation

```javascript
document.getElementById("sample").addEventListener("click", function (e) {
    console.log(e.type);       // "click"
    console.log(e.target);     // the clicked element
    console.log(e.clientX);    // mouse X
    console.log(e.clientY);    // mouse Y
    e.preventDefault();        // stop default browser action
});

// Event delegation — one listener for many children
document.querySelector("ul").addEventListener("click", function (e) {
    if (e.target.matches("li")) {
        console.log("Clicked:", e.target.textContent);
    }
});
```

---

# 11. Error Handling

`try / catch / finally` keeps your program alive when something throws.

```javascript
try {
    let result = riskyOperation();
    console.log(result);
} catch (err) {
    console.error("Something went wrong:", err.message);
} finally {
    console.log("Always runs — cleanup here.");
}
```

---

## Throwing Custom Errors

```javascript
function divide(a, b) {
    if (b === 0) {
        throw new Error("Cannot divide by zero");
    }
    return a / b;
}

try {
    console.log(divide(10, 0));
} catch (e) {
    console.log(e.message);   // "Cannot divide by zero"
}
```

| Statement | Purpose |
| --- | --- |
| `try { ... }` | Run code that might fail. |
| `catch (e) { ... }` | Handle the error — `e` is the error object. |
| `finally { ... }` | Always runs (cleanup, close files, …). |
| `throw new Error("msg")` | Create your own error. |

---

# 12. Regular Expression

A **regex** is a pattern used to match character combinations in strings.

```javascript
// Two ways to build one
let re1 = /hello/;                  // literal
let re2 = new RegExp("hello");      // constructor

"hello world".match(/hello/);       // ["hello"]
/world/.test("hello world");        // true
"a1b2c3".replace(/\d/g, "*");       // "a*b*c*"
```

---

## Literal & Meta Characters

```javascript
// ^  → start of string
// $  → end of string
// .  → any single char
// |  → OR
// \  → escape

/^hello/.test("hello world");      // true
/world$/.test("hello world");      // true
/c.t/.test("cat");                 // true
```

---

## Character Sets, Quantifiers & Grouping

```javascript
// [...] → set of allowed chars
// [^..] → negated set
// {n}   → exactly n times
// {n,m} → between n and m times
// *     → 0 or more
// +     → 1 or more
// ?     → 0 or 1 (or lazy quantifier)

let phone  = /^\+?[0-9]{7,15}$/;
let postal = /^[0-9]{4,6}$/;
let email  = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;

phone.test("+8801711111111");      // true
email.test("ash@example.com");     // true
```

---

## Grouping & Captures

```javascript
let re = /(\d{4})-(\d{2})-(\d{2})/;
let m  = "2026-09-30".match(re);

console.log(m[0]);   // "2026-09-30"
console.log(m[1]);   // "2026"
console.log(m[2]);   // "09"
console.log(m[3]);   // "30"
```

| Shorthand | Means |
| --- | --- |
| `\d` | digit `[0-9]` |
| `\D` | non-digit |
| `\w` | word char `[A-Za-z0-9_]` |
| `\W` | non-word char |
| `\s` | whitespace |
| `\S` | non-whitespace |
| `\b` | word boundary |

---

# 13. JSON

> **JSON** = JavaScript Object Notation — used to **send** and **receive** data, mostly over the network.

- **Send** — convert JS object → JSON string with `JSON.stringify()`.
- **Receive** — convert JSON string → JS object with `JSON.parse()`.
- Validate JSON at <https://jsonlint.com/>.

```javascript
// JS object — keys NOT quoted
var person = {
    name: 'shuvo',
    roll: 5058,
    age : 20
};

// JSON — keys MUST be in double quotes (numbers stay raw)
var person_json = {
    "name": 'shuvo',
    "roll":  5058,
    "age" :  20
};

// JS object → JSON string
var jsonString = JSON.stringify(person);
console.log(jsonString);            // {"name":"shuvo","roll":5058,"age":20}

// JSON string → JS object
var obj = JSON.parse(jsonString);
console.log(obj.name);              // "shuvo"
```

| Operation | Function | Direction |
| --- | --- | --- |
| Object → JSON | `JSON.stringify(obj)` | Outgoing |
| JSON → Object | `JSON.parse(str)` | Incoming |

---

# 14. AJAX

**AJAX** = Asynchronous JavaScript And XML. Lets the page talk to a server **without reloading**. The old-school tool is the `XMLHttpRequest` object.

```html
<h2>Using Ajax tool to get data</h2>
<button id="get_data">Get Data</button>
<p id="passData">hello</p>

<script>
document.getElementById("get_data").addEventListener("click", function () {
    const xhr = new XMLHttpRequest();

    // xhr.open(method, url, async?)
    xhr.open("GET", "data.txt", true);

    xhr.onload = function () {
        if (this.status === 200) {
            document.getElementById("passData").innerText = this.responseText;
        }
    };

    xhr.send();
});
</script>
```

| Method | Use |
| --- | --- |
| `xhr.open(method, url, async)` | prepare the request |
| `xhr.send()` | send it |
| `xhr.onload` | runs when response arrives |
| `xhr.onerror` | runs on network error |
| `xhr.responseText` | the body of the response |

> These days most code uses `fetch()` (next section) — it returns a **Promise** and is much easier.

---

# 15. Fetch API

`fetch()` is the modern replacement for `XMLHttpRequest`. It returns a **Promise**, so you chain `.then()` / `.catch()`.

```javascript
// Fetch API Uses JavaScript Promise.

document.getElementById("get_data").addEventListener("click", getData);

function getData() {
    fetch('https://jsonplaceholder.typicode.com/posts/1')
        .then(res => res.json())        // parse the JSON body
        .then(data => { console.log(data); })
        .catch(err  => { console.log(err); });
}
```

---

## `async` / `await` — Cleaner Fetch

```javascript
// Old promise chain
fetch('http://api.icndb.com/jokes/random/5000')
    .then(response => response.json())
    .then(data => { /* use data */ });

// async/await — same thing, easier to read
async function getJokes() {
    let response = await fetch('http://api.icndb.com/jokes/random/5000');
    let data     = await response.json();
    return data;
}

getJokes().then(jokes => console.log(jokes));
```

| Keyword | What it does |
| --- | --- |
| `async` | Marks a function as returning a Promise. |
| `await` | Pauses until the Promise resolves. |
| `.then()` | Attach a success handler. |
| `.catch()` | Attach a failure handler. |

---

# 16. Project 1 — Todo App

Build a small task list that runs entirely in the browser.

**Core features:**

- Add a new task from an input field.
- Mark a task as completed (strike-through).
- Delete a task.
- Persist the list in `localStorage` so it survives page reloads.

```javascript
// Pseudocode structure:
const form    = document.querySelector("#todo-form");
const list    = document.querySelector("#todo-list");
const input   = document.querySelector("#todo-input");

let todos = JSON.parse(localStorage.getItem("todos") || "[]");

function render() {
    list.innerHTML = todos
        .map((t, i) =>
            `<li class="${t.done ? "done" : ""}" data-i="${i}">
                <span>${t.text}</span>
                <button class="toggle">✓</button>
                <button class="del">×</button>
            </li>`)
        .join("");
}

form.addEventListener("submit", e => {
    e.preventDefault();
    todos.push({ text: input.value, done: false });
    input.value = "";
    localStorage.setItem("todos", JSON.stringify(todos));
    render();
});

list.addEventListener("click", e => {
    const i = e.target.closest("li").dataset.i;
    if (e.target.matches(".toggle")) todos[i].done = !todos[i].done;
    if (e.target.matches(".del"))    todos.splice(i, 1);
    localStorage.setItem("todos", JSON.stringify(todos));
    render();
});

render();
```

**Skills practiced:** DOM selectors, events, template literals, `localStorage`, `JSON.stringify` / `JSON.parse`.

---

# 17. Project 2 — Book List

A CRUD app for managing a list of books — add, edit, delete, and persist.

**Core features:**

- Form to add a new book (title, author, ISBN).
- Table to display all books.
- Edit a book's row in place.
- Delete a row.
- Persist data with `localStorage`.

```javascript
// Pseudocode structure:
class Book {
    constructor(title, author, isbn) {
        this.title  = title;
        this.author = author;
        this.isbn   = isbn;
    }
}

class UI {
    addBookToList(book) {
        const row = document.createElement("tr");
        row.innerHTML = `
            <td>${book.title}</td>
            <td>${book.author}</td>
            <td>${book.isbn}</td>
            <td><a href="#" class="delete">×</a></td>`;
        document.querySelector("#book-list").appendChild(row);
    }

    deleteBook(target) {
        if (target.className === "delete") {
            target.parentElement.parentElement.remove();
        }
    }

    clearFields() {
        document.querySelectorAll("input").forEach(i => (i.value = ""));
    }
}

// Wire up events:
document.querySelector("#book-form").addEventListener("submit", e => {
    e.preventDefault();
    const book = new Book(title.value, author.value, isbn.value);
    new UI().addBookToList(book);
    Store.addBook(book);
    new UI().clearFields();
});

document.querySelector("#book-list").addEventListener("click", e => {
    new UI().deleteBook(e.target);
    Store.removeBook(e.target.parentElement.previousElementSibling.textContent);
});

// Persist with localStorage:
class Store {
    static getBooks()      { return JSON.parse(localStorage.getItem("books") || "[]"); }
    static addBook(book)   { const b = Store.getBooks(); b.push(book); localStorage.setItem("books", JSON.stringify(b)); }
    static removeBook(isbn){ const b = Store.getBooks().filter(x => x.isbn !== isbn); localStorage.setItem("books", JSON.stringify(b)); }
}
```

**Skills practiced:** ES6 classes, prototypes, event delegation, `localStorage`, `JSON`.

---

# 18. Project 3 — GitHub API (CRUD)

A real-world **CRUD** (Create / Read / Update / Delete) app that talks to the public GitHub REST API.

**Core features:**

- **Create** — search a GitHub user.
- **Read** — show their profile + repos.
- **Update** — change displayed data via filters.
- **Delete** — clear the result list.

```javascript
// Pseudocode structure:
document.querySelector("#searchUser").addEventListener("keyup", function (e) {
    const user = e.target.value.trim();

    if (user !== "") {
        fetch(`https://api.github.com/users/${user}`)
            .then(res => res.json())
            .then(data => {
                if (data.message === "Not Found") {
                    showAlert("User not found", "alert alert-danger");
                } else {
                    showProfile(data);
                    showRepos(data.repos_url);
                }
            });
    }
});

function showProfile(user) {
    document.querySelector("#profile").innerHTML = `
        <div class="card">
            <img src="${user.avatar_url}" class="card-img-top">
            <div class="card-body">
                <h3>${user.name}</h3>
                <p>${user.bio}</p>
                <a href="${user.html_url}" target="_blank">View profile</a>
            </div>
        </div>`;
}

function showRepos(url) {
    fetch(`${url}?per_page=5&sort=created:asc`)
        .then(res => res.json())
        .then(repos => {
            document.querySelector("#repos").innerHTML =
                repos.map(r =>
                    `<li class="list-group-item">
                        <a href="${r.html_url}">${r.name}</a>
                    </li>`).join("");
        });
}
```

**Skills practiced:** Fetch API, Promises, async/await, template literals, error handling, dynamic DOM rendering.

---

# 19. Leveling up to ES6

The features below turn JavaScript from "old-school" into the modern language used by React, Vue, Node, etc.

---

## `var` vs `let` vs `const`

```javascript
// var  → function-scoped, hoisted, can be re-declared
var a = 10;

// let  → block-scoped, can be reassigned, NOT re-declared
let b = 20;

// const → block-scoped, CANNOT be reassigned, MUST be initialised
const PI = 3.14;
```

| Keyword | Scope | Reassign | Re-declare | Hoisted |
| --- | --- | --- | --- | --- |
| `var`   | function | ✅ | ✅ | ✅ |
| `let`   | block    | ✅ | ❌ | ✅ (TDZ) |
| `const` | block    | ❌ | ❌ | ✅ (TDZ) |

---

## Arrow Functions

```javascript
// Traditional
function add(a, b) { return a + b; }

// Arrow — implicit return for single expression
const add = (a, b) => a + b;

// One parameter — no parens needed
const square = x => x * x;

// No parameters — empty parens
const greet = () => "Hello";

// Block body — explicit return
const greetUser = name => {
    const msg = `Hello, ${name}`;
    return msg;
};
```

> Arrow functions do **not** have their own `this` — they inherit it from the surrounding scope.

---

## Template Literals

```javascript
let name = "Ashraful";
let greet = `Hello, ${name}!
Welcome to ES6.`;
```

---

## Array Destructuring

```javascript
const colors = ["red", "green", "blue"];

const [first, second, third] = colors;
console.log(first);    // "red"

// Skip values
const [, , onlyBlue] = colors;

// Default values
const [a, b, c = "yellow"] = ["red", "green"];
console.log(c);        // "yellow"
```

---

## Swapping Variables

```javascript
let a = 1, b = 2;
[a, b] = [b, a];
console.log(a, b);     // 2 1
```

---

## Object Destructuring

```javascript
const user = { name: "Ash", age: 25, role: "dev" };

const { name, age, role } = user;
console.log(name, age, role);    // Ash 25 dev

// Rename + default
const { name: userName = "Guest", country = "BD" } = user;
```

---

## Spread Operator

Spreads an iterable into individual elements.

```javascript
// Array spread
const nums = [1, 2, 3];
const more = [...nums, 4, 5];        // [1,2,3,4,5]

// Object spread
const defaults = { theme: "dark" };
const settings = { ...defaults, lang: "en" };

// Combine arrays
const merged = [...nums, ...[6, 7, 8]];
```

---

## Spread with Function Parameters

```javascript
function sum(a, b, c) { return a + b + c; }

const nums = [1, 2, 3];
console.log(sum(...nums));     // 6

// Math.max takes individual args
console.log(Math.max(...[10, 5, 8]));  // 10
```

---

## Rest Operator

Collects the **rest** of the values into an array.

```javascript
function sum(...nums) {
    return nums.reduce((a, b) => a + b, 0);
}
sum(1, 2, 3, 4, 5);     // 15

// Mixed
function logAll(label, ...items) {
    console.log(label, items);
}
logAll("Fruits:", "apple", "banana", "mango");
```

| Operator | Direction | Where it goes |
| --- | --- | --- |
| Spread `...` | **out** of an array | call site / array literal |
| Rest `...`  | **into** a parameter | function signature |

---

## ES5 Class vs ES6 Class

```javascript
// ES5 — function + prototype
function PersonES5(name) { this.name = name; }
PersonES5.prototype.greet = function () {
    return "Hello, " + this.name;
};

// ES6 — class syntax (still prototype under the hood)
class PersonES6 {
    constructor(name) { this.name = name; }
    greet() { return `Hello, ${this.name}`; }
}
```

---

## `Symbol`

A **unique** primitive value — great for non-colliding object keys.

```javascript
const id = Symbol("id");
const user = { [id]: 101, name: "Ash" };

console.log(user[id]);     // 101
console.log(Object.keys(user));  // ["name"] — symbols are hidden
```

---

## Iterator & Generator

```javascript
// Iterator — object with .next() returning { value, done }
function makeRange(start, end) {
    let i = start;
    return {
        next() {
            return i <= end
                ? { value: i++, done: false }
                : { value: undefined, done: true };
        }
    };
}

for (const n of makeRange(1, 3)) console.log(n);   // 1 2 3

// Generator — function* with yield
function* range(start, end) {
    for (let i = start; i <= end; i++) yield i;
}
[...range(1, 3)];     // [1, 2, 3]
```

---

## Promise

A **Promise** represents a value that may be ready **now**, **later**, or **never**.

```javascript
const fetchData = new Promise((resolve, reject) => {
    setTimeout(() => {
        const ok = true;
        if (ok) resolve({ user: "Ash" });
        else reject(new Error("Network failed"));
    }, 1000);
});

fetchData
    .then(data => console.log("Got:", data))
    .catch(err  => console.error("Err:", err.message))
    .finally(() => console.log("Done"));
```

| State | Meaning |
| --- | --- |
| `pending` | still working |
| `fulfilled` | `resolve()` was called |
| `rejected` | `reject()` was called |

---

## `async` / `await`

```javascript
// If we mark a function async, it returns a Promise.
// await pauses until the Promise resolves — cleaner than .then() chains.

async function getUser(id) {
    try {
        let response = await fetch(`/api/users/${id}`);
        let user     = await response.json();
        return user;
    } catch (err) {
        console.error("Failed:", err);
    }
}

getUser(1).then(u => console.log(u));
```

---

## `Set`

A collection of **unique** values — duplicates are silently ignored.

```javascript
const nums = new Set([1, 2, 2, 3, 3, 3]);
console.log(nums);                  // Set {1, 2, 3}
console.log(nums.size);             // 3

nums.add(4);
nums.delete(2);
nums.has(3);                        // true

// Convert back to array
const unique = [...new Set([1, 1, 2, 3, 3])];   // [1, 2, 3]
```

---

## `Map`

A key-value collection where **keys can be any type** (objects, functions, etc.).

```javascript
const userRoles = new Map();

userRoles.set("admin",  { access: "full" });
userRoles.set("guest",  { access: "read" });

userRoles.get("admin");              // { access: "full" }
userRoles.has("guest");              // true
userRoles.size;                      // 2
userRoles.delete("guest");

// Iterate
for (const [key, value] of userRoles) {
    console.log(key, "->", value);
}
```

| Feature | `Object` | `Map` |
| --- | --- | --- |
| Key types | strings, symbols | **any** type |
| Size | manual | `.size` |
| Iteration order | mostly insertion | **guaranteed** insertion |
| Performance for many entries | slower | faster |

---

# 20. Browser Object Model (BOM)

The **BOM** is everything the browser gives JavaScript access to **outside** the document — window, location, history, navigator, screen, and the dialog methods.

> The `window` object is created automatically by the browser — it's the **global object** in browser-side JavaScript.

```javascript
// window is the global object
window.alert("Hi");
console.log(window.innerWidth);    // viewport width
console.log(window.innerHeight);   // viewport height
```

---

## Dialog Methods

| Method | Returns | Purpose |
| --- | --- | --- |
| `alert(msg)` | `undefined` | Display a popup with OK. |
| `confirm(msg)` | `true` / `false` | OK / Cancel popup. |
| `prompt(msg)` | string / `null` | Ask the user for input. |

```javascript
// alert
function msg() { alert("Hello Alert Box"); }

// confirm
function msg() {
    if (confirm("Are you sure?") === true) alert("ok");
    else                                   alert("cancel");
}

// prompt
function msg() {
    const v = prompt("Who are you?");
    alert("I am " + v);
}
```

---

## Window Control Methods

| Method | What it does |
| --- | --- |
| `open(url, name, specs)` | Opens a new window / tab. |
| `close()` | Closes the current window. |
| `setTimeout(fn, ms)` | Runs `fn` once after `ms` ms. |
| `setInterval(fn, ms)` | Runs `fn` every `ms` ms. |
| `clearTimeout(id)` | Cancels a pending `setTimeout`. |
| `clearInterval(id)` | Cancels a repeating `setInterval`. |

```javascript
// Open a new tab
function openSite() {
    open("https://www.example.com");
}

// Run something after a delay
setTimeout(() => alert("Welcome after 2s"), 2000);

// Repeating clock
const id = setInterval(() => console.log(new Date().toLocaleTimeString()), 1000);

// Stop the clock
clearInterval(id);
```

---

## Other `window` Properties

| Property | Meaning |
| --- | --- |
| `window.innerWidth` / `innerHeight` | Viewport size (pixels). |
| `window.location` | Current URL — can be read or assigned. |
| `window.history` | Back / forward navigation. |
| `window.navigator` | Browser info (user-agent, language, …). |
| `window.screen` | Physical screen dimensions. |
| `window.localStorage` | Persistent key/value store. |
| `window.sessionStorage` | Per-tab key/value store. |

```javascript
// Redirect
window.location.href = "https://www.example.com";

// Back / Forward
window.history.back();
window.history.forward();

// localStorage
localStorage.setItem("theme", "dark");
localStorage.getItem("theme");      // "dark"
```

---

## BOM Cheatsheet

| Category | API |
| --- | --- |
| Dialogs | `alert`, `confirm`, `prompt` |
| Timers | `setTimeout`, `setInterval`, `clearTimeout`, `clearInterval` |
| Window | `open`, `close`, `focus`, `blur`, `moveTo`, `resizeTo` |
| Location | `href`, `assign`, `replace`, `reload` |
| History | `back`, `forward`, `go`, `pushState` |
| Navigator | `userAgent`, `language`, `onLine`, `geolocation` |
| Screen | `width`, `height`, `availWidth`, `availHeight` |
| Storage | `localStorage`, `sessionStorage`, `cookie` |

---

# End of JavaScript Basics

You've now walked through the full curriculum:

**Fundamentals** → `Output → Variables → Operators → Data Types → Template Literals → Conditions → Loops → Functions`
**The Browser** → `OOP → DOM → Error Handling → RegExp → JSON → AJAX → Fetch`
**Real Apps** → `Todo App → Book List → GitHub API CRUD`
**Modern JS** → `ES6 features (let/const, arrows, spread/rest, destructuring, classes, symbols, iterators, promises, async/await, Set, Map) → BOM`

From here you are ready for **React**, **Node.js**, or any modern JS framework.

**Source repository:** [Ashraful-Momen/Web-Development-With-React-And-Django](https://github.com/Ashraful-Momen/Web-Development-With-React-And-Django/tree/main/JavaScript)
