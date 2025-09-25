# Asynchronous JavaScript & API Handling

## 1. Synchronous vs Asynchronous JavaScript

**Synchronous (default behavior):**

- Executes line by line.
- Next statement waits for the current one to finish.
- Problem: Long-running tasks (like API calls) **block execution**.

**Asynchronous:**

- Runs tasks in the background without blocking the main thread.
- JS uses **callbacks, promises, async/await** to handle async operations.

**Example:**

```jsx
console.log("Start");

setTimeout(() => {
  console.log("Async task completed");
}, 2000);

console.log("End");
```

Output:

```
Start
End
Async task completed
```

## 2. Callbacks

**Definition:**

A callback is a function passed to another function to be executed later.

**Problem:** Callback Hell (nested callbacks, messy code).

**Example:**

```jsx
function fetchData(callback) {
  setTimeout(() => {
    callback("Data received!");
  }, 2000);
}

fetchData((data) => {
  console.log(data);
});
```

## 3. Promises

**Definition:**

- A Promise is an object representing the result of an async operation.
- States:
    - `pending` (initial)
    - `fulfilled` (resolved)
    - `rejected` (error)

**Creating & Using Promises:**

```jsx
let promise = new Promise((resolve, reject) => {
  let success = true;
  if (success) {
    resolve("Task successful");
  } else {
    reject("Task failed");
  }
});

promise
  .then(result => console.log(result))   // handles success
  .catch(error => console.error(error))  // handles error
  .finally(() => console.log("Promise finished"));
```

## 4. Fetching Data with `fetch()`

**Notes:**

- `fetch(url)` returns a **Promise**.
- Use `.then()` or `async/await` to handle response.
- Must convert response to JSON with `.json()`.

**Example with `.then()`:**

```jsx
fetch("https://jsonplaceholder.typicode.com/posts/1")
  .then(response => response.json())
  .then(data => console.log("Post:", data))
  .catch(error => console.error("Error fetching data:", error));
```

## 5. Async / Await

**Notes:**

- `async` functions always return a Promise.
- `await` pauses execution until Promise resolves/rejects.
- Makes async code look synchronous.

**Example:**

```jsx
async function getPost() {
  try {
    let response = await fetch("https://jsonplaceholder.typicode.com/posts/1");
    if (!response.ok) {
      throw new Error("Network response was not ok: " + response.status);
    }
    let data = await response.json();
    console.log("Post:", data);
  } catch (error) {
    console.error("Error fetching post:", error.message);
  } finally {
    console.log("Fetch attempt finished");
  }
}

getPost();
```

## 6. Error Handling

### 6.1 Using `try...catch`

```jsx
try {
  let result = riskyFunction();
  console.log(result);
} catch (error) {
  console.error("Caught error:", error.message);
} finally {
  console.log("Always executed");
}
```

### 6.2 Throwing Errors

```jsx
function divide(a, b) {
  if (b === 0) {
    throw new Error("Division by zero not allowed");
  }
  return a / b;
}

try {
  console.log(divide(10, 0));
} catch (error) {
  console.error("Error:", error.message);
}
```

## 7. Combining Promises, Async/Await, and Error Handling

### Example – Fetch Multiple Posts

```jsx
async function fetchPosts() {
  try {
    let response = await fetch("https://jsonplaceholder.typicode.com/posts");
    if (!response.ok) {
      throw new Error(`HTTP Error: ${response.status}`);
    }
    let posts = await response.json();
    console.log("First 3 Posts:", posts.slice(0, 3));
  } catch (error) {
    console.error("Failed to fetch posts:", error.message);
  }
}

fetchPosts();
```

### Example – Multiple Promises with `Promise.all`

```jsx
async function fetchMultiple() {
  try {
    let [post, user] = await Promise.all([
      fetch("https://jsonplaceholder.typicode.com/posts/1").then(r => r.json()),
      fetch("https://jsonplaceholder.typicode.com/users/1").then(r => r.json())
    ]);
    console.log("Post:", post);
    console.log("User:", user);
  } catch (error) {
    console.error("Error in fetching multiple:", error.message);
  }
}

fetchMultiple();
```