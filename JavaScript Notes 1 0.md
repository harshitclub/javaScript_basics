# JavaScript Notes 1.0

## 1. Introduction & History of JavaScript

**Notes:**

- JavaScript is a lightweight, interpreted programming language used to add interactivity to web pages.
- Created in 1995 by **Brendan Eich** at Netscape in just 10 days.
- Initially called **Mocha**, then renamed **LiveScript**, and finally **JavaScript**.
- Standardized as **ECMAScript (ES)** by ECMA International in 1997.
- Today, JavaScript runs not only in browsers but also on servers (Node.js), mobile apps, and desktop apps.

**Example:**

```jsx
console.log("Hello, JavaScript!");
```

## 2. Scope in JavaScript

**Notes:**

- Scope determines where variables are accessible.
- Types of scope:
    - **Global Scope:** Accessible everywhere.
    - **Function Scope:** Variables declared inside a function are accessible only inside it.
    - **Block Scope:** Variables declared with `let` or `const` inside `{}` are accessible only inside that block.

**Example:**

```jsx
let globalVar = "I am global";

function testScope() {
  let functionVar = "I am in function scope";
  console.log(globalVar); // Accessible
  console.log(functionVar); // Accessible
}
testScope();
// console.log(functionVar); // Error: not accessible outside function

if (true) {
  let blockVar = "I am block scoped";
  console.log(blockVar); // Accessible
}
// console.log(blockVar); // Error: not accessible outside block
```

## 3. Data Types in JavaScript

**Notes:**

JavaScript has **primitive** and **non-primitive** types.

- Primitive: `string`, `number`, `boolean`, `null`, `undefined`, `symbol`, `bigint`
- Non-Primitive: `object`, `array`, `function`

**Example:**

```jsx
let name = "Harshit";    // string
let age = 22;            // number
let isDeveloper = true;  // boolean
let salary = null;       // null
let address;             // undefined
let id = Symbol("id");   // symbol
let bigNum = 12345678901234567890n; // bigint

let person = { name: "Harshit", age: 22 }; // object
let arr = [1, 2, 3]; // array
function greet() { return "Hello"; } // function
```

## 4. Variables in JavaScript

**Notes:**

- Variables store data.
- Declared using `var`, `let`, `const`.

**Example:**

```jsx
var x = 10;
let y = 20;
const z = 30;
```

## 5. var vs let vs const

**Notes:**

- `var`
    - Function-scoped.
    - Allows redeclaration and reassigning.
    - Hoisted (declared at top internally).
- `let`
    - Block-scoped.
    - Allows reassignment but not redeclaration in the same scope.
- `const`
    - Block-scoped.
    - Cannot be redeclared or reassigned.

**Example:**

```jsx
var a = 5;
var a = 10; // redeclaration allowed
console.log(a); // 10

let b = 20;
// let b = 30; // Error: redeclaration not allowed
b = 25; // reassignment allowed
console.log(b); // 25

const c = 50;
// c = 60; // Error: reassignment not allowed
console.log(c); // 50
```

## 6. Template Literals

**Notes:**

- Introduced in ES6.
- Use backticks ```, allow embedding variables and expressions.

**Example:**

```jsx
let name = "Harshit";
let age = 22;
console.log(`My name is ${name} and I am ${age} years old.`);
```

## 7. Conditionals in JavaScript

**Notes:**

- Used for decision-making.
- Types: `if`, `if-else`, `if-else-if`, `ternary operator`.

**Example:**

```jsx
let marks = 75;

if (marks > 90) {
  console.log("Grade A");
} else if (marks > 70) {
  console.log("Grade B");
} else {
  console.log("Grade C");
}

let isLoggedIn = true;
console.log(isLoggedIn ? "Welcome!" : "Please log in");
```

## 8. Loops in JavaScript

**Notes:**

- `for`, `while`, `do-while`, `for...of`, `for...in`.

**Example:**

```jsx
// for loop
for (let i = 0; i < 3; i++) {
  console.log("For loop:", i);
}

// while loop
let j = 0;
while (j < 3) {
  console.log("While loop:", j);
  j++;
}

// do-while loop
let k = 0;
do {
  console.log("Do-while loop:", k);
  k++;
} while (k < 3);

// for...of (iterates values)
let arr = [10, 20, 30];
for (let num of arr) {
  console.log("For...of:", num);
}

// for...in (iterates keys)
let person = { name: "Harshit", age: 22 };
for (let key in person) {
  console.log("For...in:", key, person[key]);
}
```

## 9. Arrays in JavaScript

**Notes:**

- Arrays store multiple values in a single variable.
- Common methods: `push`, `pop`, `shift`, `unshift`, `map`, `filter`, `reduce`, `forEach`.

**Example:**

```jsx
let numbers = [1, 2, 3];
numbers.push(4); // [1,2,3,4]
numbers.pop();   // [1,2,3]
numbers.unshift(0); // [0,1,2,3]
numbers.shift();    // [1,2,3]

let squared = numbers.map(n => n * n); // [1,4,9]
console.log(squared);
```

## 10. Objects in JavaScript

**Notes:**

- Objects store key-value pairs.
- Keys are strings or symbols; values can be any data type.

**Example:**

```jsx
let person = {
  name: "Harshit",
  age: 22,
  isDeveloper: true,
  greet: function() {
    return "Hello, " + this.name;
  }
};

console.log(person.name); // Harshit
console.log(person.greet()); // Hello, Harshit
```

## 11. Operators in JavaScript

**Notes:**

- Arithmetic: `+ - * / % **`
- Assignment: `= += -= *=`
- Comparison: `== != === !== < > <= >=`
- Logical: `&& || !`
- Ternary: `condition ? value1 : value2`

**Example:**

```jsx
let a = 10, b = 5;
console.log(a + b); // 15
console.log(a > b); // true
console.log(a === 10 && b === 5); // true
let result = (a > b) ? "A is bigger" : "B is bigger";
console.log(result);
```

## 12. Switch Case in JavaScript

**Notes:**

- Alternative to multiple `if-else` statements.
- Compares values strictly (`===`).

**Example:**

```jsx
let day = 3;

switch(day) {
  case 1:
    console.log("Monday");
    break;
  case 2:
    console.log("Tuesday");
    break;
  case 3:
    console.log("Wednesday");
    break;
  default:
    console.log("Invalid day");
}
```

# Questions

## Level 1 – Easy (Fundamentals)

1. Write a program to print **“Hello, JavaScript”** in the console.
2. Declare variables using `var`, `let`, and `const` and print their values.
3. Create variables of all primitive data types (`string`, `number`, `boolean`, `null`, `undefined`, `symbol`, `bigint`) and log them.
4. Use template literals to print:
    - Your name
    - Your age
    - A sentence like: `"My name is X and I am Y years old."`
5. Write a program that checks whether a number is **positive, negative, or zero** using `if-else`.
6. Write a program using the **ternary operator** to check if a number is even or odd.

## Level 2 – Medium (Control Flow & Loops)

1. Print numbers from **1 to 20** using a `for` loop.
2. Print the **multiplication table of 5** using a `while` loop.
3. Write a program using a `do-while` loop that prints numbers from **1 to 10**.
4. Write a program that takes a student’s marks as input and prints the grade based on conditions:
    - Marks > 90 → A
    - Marks > 75 → B
    - Marks > 50 → C
    - Else → Fail
5. Create a program using `switch-case` that prints the day of the week based on a number (1 = Monday, … 7 = Sunday).
6. Write a program that reverses an array `[1,2,3,4,5]`