# JavaScript Notes 2.0

## 1. How JavaScript Runs in Browsers

**Notes:**

- Browsers have a built-in **JavaScript Engine** (e.g., Chrome → V8, Firefox → SpiderMonkey).
- Process:
    1. HTML and CSS are parsed by the browser.
    2. When a `<script>` tag is found, the JavaScript engine executes the code.
    3. The engine converts JS code into **machine code**.
    4. Code executes inside the **Execution Context** (Global, Function).
- **Event Loop, Call Stack, Web APIs** handle async tasks (like setTimeout, fetch).

**Example:**

```html
<script>
  console.log("Script starts");
  setTimeout(() => console.log("Async code"), 0);
  console.log("Script ends");
</script>
```

Output order:

```
Script starts
Script ends
Async code
```

## 2. Type Conversion & Coercion

**Notes:**

- **Conversion**: Explicitly changing type (`Number()`, `String()`, `Boolean()`).
- **Coercion**: JavaScript automatically converts types when needed.

**Example:**

```jsx
// Conversion
console.log(Number("123"));   // 123
console.log(String(123));     // "123"
console.log(Boolean(0));      // false

// Coercion
console.log("5" + 2);   // "52"  (string concatenation)
console.log("5" - 2);   // 3    (string converted to number)
console.log("5" * "2"); // 10   (both strings converted to numbers)
```

## 3. Arrays – Methods and Properties

**Properties:**

- `length` → number of items.

**Important Methods:**

- **Modification**: `push`, `pop`, `shift`, `unshift`, `splice`, `slice`
- **Iteration**: `forEach`, `map`, `filter`, `reduce`
- **Others**: `indexOf`, `includes`, `join`, `concat`

**Example:**

```jsx
let arr = [10, 20, 30];
arr.push(40);       // [10,20,30,40]
arr.pop();          // [10,20,30]
arr.unshift(5);     // [5,10,20,30]
arr.shift();        // [10,20,30]

console.log(arr.includes(20)); // true
console.log(arr.indexOf(30));  // 2
console.log(arr.slice(1, 3));  // [20,30]
```

## 4. for...of Loop

**Notes:**

- Used to iterate over iterable objects (arrays, strings, sets, maps).
- Returns **values**, not indexes.

**Example:**

```jsx
let numbers = [1, 2, 3];
for (let num of numbers) {
  console.log(num);
}
```

## 5. forEach vs map

**Notes:**

- `forEach`: Executes a function for each element, doesn’t return a new array.
- `map`: Returns a new array with transformed values.

**Example:**

```jsx
let nums = [1, 2, 3];

// forEach
nums.forEach(n => console.log(n * 2)); // just prints values

// map
let doubled = nums.map(n => n * 2);
console.log(doubled); // [2,4,6]
```

## 6. Function Parameters & Arguments

**Notes:**

- **Parameter** → variable in function definition.
- **Argument** → actual value passed when calling.

**Example:**

```jsx
function greet(name) { // name is parameter
  console.log("Hello " + name);
}

greet("Harshit"); // "Harshit" is argument
```

## 7. Default Parameters

**Notes:**

- Introduced in ES6.
- Assigns a default value if no argument is passed.

**Example:**

```jsx
function multiply(a, b = 2) {
  return a * b;
}

console.log(multiply(5));   // 10
console.log(multiply(5, 3)); // 15
```

## 8. IIFE (Immediately Invoked Function Expression)

**Notes:**

- A function that runs immediately after being defined.
- Used to avoid polluting global scope.

**Example:**

```jsx
(function() {
  console.log("IIFE executed");
})();
```

## 9. Callbacks

**Notes:**

- A function passed as an argument to another function, executed later.
- Used in async tasks.

**Example:**

```jsx
function fetchData(callback) {
  console.log("Fetching data...");
  setTimeout(() => {
    callback("Data received");
  }, 1000);
}

fetchData(function(message) {
  console.log(message);
});
```

## 10. break & continue Statements

**Notes:**

- `break`: exits the loop immediately.
- `continue`: skips current iteration, goes to next.

**Example:**

```jsx
for (let i = 1; i <= 5; i++) {
  if (i === 3) continue; // skip 3
  if (i === 5) break;    // stop at 5
  console.log(i);
}
// Output: 1, 2, 4
```

## 11. Date Object Basics

**Notes:**

- Represents dates and times.

**Common Methods:**

- `new Date()` → current date/time
- `getFullYear()`, `getMonth()`, `getDate()`, `getDay()`
- `getHours()`, `getMinutes()`, `getSeconds()`

**Example:**

```jsx
let now = new Date();
console.log(now.toString());
console.log(now.getFullYear());
console.log(now.getMonth()); // 0-11
console.log(now.getDate());
console.log(now.getDay());   // 0=Sunday
```

## 12. String Methods Basics

**Notes:**

- Common methods:
    - `length`, `toUpperCase()`, `toLowerCase()`
    - `includes()`, `indexOf()`, `slice()`, `substring()`
    - `replace()`, `trim()`, `split()`

**Example:**

```jsx
let str = "  JavaScript Basics  ";
console.log(str.length);          // 20
console.log(str.trim());          // "JavaScript Basics"
console.log(str.toUpperCase());   // "JAVASCRIPT BASICS"
console.log(str.includes("Script")); // true
console.log(str.slice(2, 6));     // "vaSc"
console.log(str.split(" "));      // ["","JavaScript","Basics",""]
```

## 13. Math Object Basics

**Notes:**

- Provides mathematical operations.

**Common Methods:**

- `Math.round()`, `Math.floor()`, `Math.ceil()`
- `Math.random()` → random number (0–1)
- `Math.max()`, `Math.min()`
- `Math.pow()`, `Math.sqrt()`

**Example:**

```jsx
console.log(Math.round(4.6)); // 5
console.log(Math.floor(4.9)); // 4
console.log(Math.ceil(4.1));  // 5
console.log(Math.max(1, 10, 5)); // 10
console.log(Math.min(1, 10, 5)); // 1
console.log(Math.sqrt(16));  // 4
console.log(Math.pow(2, 3)); // 8
console.log(Math.random());  // random between 0 and 1
```