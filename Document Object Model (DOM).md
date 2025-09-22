# Document Object Model (DOM) – Detailed Notes

## 1. What is DOM?

- **DOM (Document Object Model)** is a programming interface for HTML and XML documents.
- It represents the page as a **tree structure** of nodes where each node is an object.
- With DOM, you can dynamically **read, update, add, or delete** elements from a web page.
- The DOM connects web pages to programming languages like JavaScript.

**Example – DOM Tree:**

HTML:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>DOM Example</title>
  </head>
  <body>
    <h1>Hello World</h1>
    <p>This is a paragraph.</p>
  </body>
</html>
```

DOM Tree representation:

```
Document
 └── html
     ├── head
     │    └── title
     └── body
          ├── h1
          └── p
```

## 2. DOM Objects

- **document** → root object of the DOM.
- **window** → global object that contains the `document` object.
- **element nodes** → HTML tags (`<h1>`, `<p>`, `<div>`, etc.).
- **text nodes** → content inside elements.
- **attributes** → properties inside HTML tags.

**Example:**

```jsx
console.log(window.document); // prints the whole HTML document
console.log(document.title);  // prints page title
```

## 3. Accessing Elements in DOM

### 3.1 By ID

```html
<p id="para">Hello DOM</p>
<script>
  let element = document.getElementById("para");
  console.log(element.innerText); // Hello DOM
</script>
```

### 3.2 By Class Name

```html
<p class="text">Para 1</p>
<p class="text">Para 2</p>
<script>
  let elements = document.getElementsByClassName("text");
  console.log(elements[0].innerText); // Para 1
</script>
```

### 3.3 By Tag Name

```html
<p>First</p>
<p>Second</p>
<script>
  let paras = document.getElementsByTagName("p");
  console.log(paras.length); // 2
</script>
```

### 3.4 By Query Selectors

```html
<p class="info">Hello</p>
<script>
  let firstPara = document.querySelector(".info"); // first match
  let allParas = document.querySelectorAll(".info"); // all matches
</script>
```

## 4. Reading and Changing Content

### 4.1 innerText

- Gets or sets text inside an element.

```jsx
document.getElementById("para").innerText = "Updated Text";
```

### 4.2 innerHTML

- Gets or sets HTML inside an element.

```jsx
document.getElementById("para").innerHTML = "<b>Bold Text</b>";
```

### 4.3 textContent

- Similar to `innerText` but shows hidden text also.

```jsx
console.log(document.getElementById("para").textContent);
```

---

## 5. Changing Attributes

```html
<img id="myImg" src="old.png" alt="image" />
<script>
  let img = document.getElementById("myImg");
  img.setAttribute("src", "new.png");
  console.log(img.getAttribute("alt")); // image
</script>
```

## 6. Changing Styles

```html
<p id="para">Style me</p>
<script>
  let p = document.getElementById("para");
  p.style.color = "red";
  p.style.fontSize = "20px";
</script>
```

## 7. Creating and Adding Elements

```html
<div id="container"></div>
<script>
  let div = document.getElementById("container");
  let newPara = document.createElement("p");
  newPara.innerText = "I am new paragraph";
  div.appendChild(newPara); // adds inside container
</script>
```

## 8. Removing Elements

```html
<p id="removeMe">Delete this</p>
<script>
  let p = document.getElementById("removeMe");
  p.remove(); // removes element
</script>
```

## 9. Event Handling in DOM

### 9.1 Inline Event

```html
<button onclick="alert('Clicked!')">Click Me</button>
```

### 9.2 Using JavaScript

```html
<button id="btn">Click Me</button>
<script>
  let btn = document.getElementById("btn");
  btn.onclick = function () {
    alert("Button clicked!");
  };
</script>
```

### 9.3 addEventListener

```html
<button id="btn2">Click Me</button>
<script>
  let btn2 = document.getElementById("btn2");
  btn2.addEventListener("click", function () {
    alert("Event Listener Clicked");
  });
</script>
```

## 10. Event Types

- `click` – mouse click
- `dblclick` – double click
- `mouseover` – hover
- `mouseout` – when cursor leaves
- `keydown`, `keyup` – keyboard events
- `submit` – form submission

**Example:**

```html
<input id="nameInput" type="text" placeholder="Type something" />
<script>
  let input = document.getElementById("nameInput");
  input.addEventListener("keyup", function (e) {
    console.log("Key pressed:", e.key);
  });
</script>
```

## 11. DOM Traversing

### 11.1 Parent Node

```jsx
let child = document.querySelector("p");
console.log(child.parentNode);
```

### 11.2 Child Nodes

```jsx
let parent = document.getElementById("container");
console.log(parent.children); // HTMLCollection
```

### 11.3 Sibling Nodes

```jsx
let element = document.querySelector("h1");
console.log(element.nextElementSibling); // next sibling
console.log(element.previousElementSibling); // previous sibling
```

## 12. Forms and Input Handling

```html
<form id="myForm">
  <input type="text" id="username" />
  <button type="submit">Submit</button>
</form>
<script>
  let form = document.getElementById("myForm");
  form.addEventListener("submit", function (e) {
    e.preventDefault(); // prevent page reload
    let name = document.getElementById("username").value;
    console.log("Name:", name);
  });
</script>
```

## 13. DOM Collections vs NodeLists

- `getElementsByClassName` → returns **HTMLCollection** (live).
- `querySelectorAll` → returns **NodeList** (static).

**Example:**

```jsx
let liveCollection = document.getElementsByClassName("item");
let staticList = document.querySelectorAll(".item");
```

## 14. Modifying CSS Classes

```html
<p id="text" class="blue">Hello</p>
<script>
  let txt = document.getElementById("text");
  txt.classList.add("bold");     // add new class
  txt.classList.remove("blue");  // remove class
  txt.classList.toggle("hidden"); // toggle on/off
</script>
```

## 15. DOM Best Practices

1. Use `querySelector` / `querySelectorAll` for flexibility.
2. Use `textContent` instead of `innerHTML` for plain text (security).
3. Cache DOM lookups in variables for performance.
4. Always remove unused event listeners.
5. Prefer `addEventListener` over inline events.

# Final Practical Example (Everything Combined)

```html
<!DOCTYPE html>
<html>
<head>
  <title>DOM Master Example</title>
  <style>
    .highlight { color: red; font-weight: bold; }
  </style>
</head>
<body>
  <h1 id="title">Welcome</h1>
  <button id="changeBtn">Change Title</button>
  <ul id="list">
    <li class="item">One</li>
    <li class="item">Two</li>
  </ul>
  <form id="form">
    <input type="text" id="input" placeholder="Enter text" />
    <button type="submit">Add Item</button>
  </form>

  <script>
    // Change Title
    document.getElementById("changeBtn").addEventListener("click", () => {
      let title = document.getElementById("title");
      title.innerText = "DOM Updated!";
      title.classList.toggle("highlight");
    });

    // Add new list item from form
    document.getElementById("form").addEventListener("submit", (e) => {
      e.preventDefault();
      let inputValue = document.getElementById("input").value;
      let li = document.createElement("li");
      li.innerText = inputValue;
      document.getElementById("list").appendChild(li);
      document.getElementById("input").value = "";
    });
  </script>
</body>
</html>

```

# Questions

1. Create a webpage with a paragraph. Use JavaScript to:
    - Get the paragraph by ID.
    - Change its text to `"Hello DOM"`.
2. Select an `<h1>` element using `querySelector` and change its color to **blue**.
3. Add three `<p>` elements inside a `<div>`. Write JavaScript to count how many `<p>` elements exist and log the number.
4. Create an image tag and use JavaScript to change its `src` attribute.
5. Select a paragraph and change its `fontSize` to `"24px"` using JavaScript.
6. Create a button that, when clicked, **adds a new paragraph** with the text `"I am new!"`.
7. Create a button that, when clicked, **removes the last list item** from a `<ul>`.
8. Write JavaScript to create a new `<li>` element with the text `"New Item"` and append it to an existing `<ul>`.