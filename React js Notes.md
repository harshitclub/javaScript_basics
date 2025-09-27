# React.js Notes

## 1. What is React?

- **React** is a JavaScript library developed by Facebook (first released in 2013).
- It is used for building **user interfaces**, especially for **Single Page Applications (SPAs)**.
- React focuses only on the **view layer** of an application (similar to the “V” in MVC).
- It provides a **component-based architecture**, which means the UI can be split into small, reusable pieces.

## 2. Why React? What Problems Does It Solve?

Before React, developers mostly used:

- **Vanilla JavaScript**: Writing DOM manipulation manually with `document.querySelector`, `innerHTML`, etc.
- **jQuery**: Helped with DOM manipulation and AJAX calls, but large apps became unmanageable.

**Problems without React:**

1. **Manual DOM Manipulation**
    - Developers had to update DOM elements manually whenever data changed.
    - This led to messy, error-prone code (hard to maintain).
2. **Poor Performance with Direct DOM**
    - Frequent DOM updates are slow because DOM operations are expensive.
3. **Hard to Manage State**
    - In large applications, keeping track of data (state) across multiple parts of the UI became complicated.
4. **Code Reusability Issues**
    - No clear way to reuse UI logic. Components were not a thing.
5. **Spaghetti Code**
    - Mixing data logic and UI updates made the codebase hard to maintain.

**How React solves these problems:**

- Introduces **Virtual DOM**:
    - Instead of updating the real DOM directly, React keeps a lightweight copy in memory (Virtual DOM).
    - When data changes, React compares the new Virtual DOM with the previous one (diffing) and updates only the necessary parts of the real DOM.
    - This makes updates much faster and more efficient.
- Provides **Component-based Architecture**:
    - Build UI as small, reusable components.
    - Easier to manage, test, and scale.
- **Declarative UI**:
    - Instead of manually writing "how" the UI should update, you declare "what" the UI should look like for a given state.
    - Example:
        
        ```jsx
        <h1>{isLoggedIn ? "Welcome back!" : "Please login"}</h1>
        ```
        
        React automatically updates the UI when `isLoggedIn` changes.
        
- **Unidirectional Data Flow**:
    - Data flows from parent components to child components via props.
    - Makes state changes predictable and easier to debug.
- **Ecosystem and Community**:
    - Huge ecosystem of libraries and tools (React Router, Redux, Next.js).

## 3. Setting Up a React Project with Vite

Steps:

1. Check Node.js installation:
    
    ```bash
    node -v
    npm -v
    ```
    
2. Create project using Vite:
    
    ```bash
    npm create vite@latest my-app
    ```
    
3. Choose framework:
    - Select `React` (or `React + TypeScript` if you want TypeScript).
4. Move into the project:
    
    ```bash
    cd my-app
    ```
    
5. Install dependencies:
    
    ```bash
    npm install
    ```
    
6. Start development server:
    
    ```bash
    npm run dev
    ```
    
7. Visit the server URL shown in the terminal (e.g., `http://localhost:5173`).

## 4. React Project Structure (Vite)

```
my-app/
  ├── node_modules/     # Installed packages
  ├── public/           # Static assets
  ├── src/
  │   ├── App.jsx       # Main App component
  │   ├── main.jsx      # Entry point
  │   └── components/   # Custom components
  ├── package.json      # Dependencies and scripts
  └── vite.config.js    # Vite config
```

## 5. Core Concepts of React

### 5.1 Components

- A component is a **reusable building block** of UI.
- Types:
    - **Functional Components**: Defined as functions, modern and preferred.
    - **Class Components**: Older style, less common now.

Example:

```jsx
function Welcome() {
  return <h1>Hello, React!</h1>;
}
```

### 5.2 JSX (JavaScript XML)

- JSX allows you to write HTML-like syntax in JavaScript.
- Transpiled to `React.createElement` calls under the hood.

Rules of JSX:

- Must return one parent element.
- Use `{}` to embed JavaScript expressions.
- Use `className` instead of `class`.

Example:

```jsx
const element = <h1>{2 + 2}</h1>;
```

### 5.3 Props (Properties)

- Read-only data passed from parent to child component.

Example:

```jsx
function Greeting(props) {
  return <h1>Hello {props.name}</h1>;
}

<Greeting name="Harshit" />
```

### 5.4 State

- A way to store and manage data inside a component.
- Declared using `useState` hook.

Example:

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>Increase</button>
    </div>
  );
}
```

### 5.5 Event Handling

- Events in React are camelCase.
- Pass functions as event handlers.

```jsx
<button onClick={() => alert("Clicked!")}>Click Me</button>

```

### 5.6 Conditional Rendering

```jsx
{isLoggedIn ? <p>Welcome back</p> : <p>Please login</p>}
```

### 5.7 Lists and Keys

```jsx
const items = ["Apple", "Banana", "Mango"];
<ul>
  {items.map((item, index) => (
    <li key={index}>{item}</li>
  ))}
</ul>
```

### 5.8 Forms and Controlled Components

```jsx
function Form() {
  const [name, setName] = useState("");
  return (
    <form>
      <input value={name} onChange={(e) => setName(e.target.value)} />
      <p>{name}</p>
    </form>
  );
}
```

## 6. React Hooks

### useState

- Manage local state.

### useEffect

- Handle side effects (API calls, subscriptions, timers).
- Accepts dependency array to control when effect runs.

Example:

```jsx
useEffect(() => {
  console.log("Effect runs");
}, [dependency]);
```

### useContext

- Avoids prop drilling, allows sharing state globally.

### useRef

- Access DOM elements or persist values across renders.

### useReducer

- Alternative to useState for complex state logic.

## 7. React Router

Install:

```bash
npm install react-router-dom
```

Usage:

```jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<h1>Home</h1>} />
        <Route path="/about" element={<h1>About</h1>} />
      </Routes>
    </BrowserRouter>
  );
}
```

## 8. Styling in React

Options:

- Inline styles
- CSS files
- CSS Modules
- CSS-in-JS (Styled Components, Emotion)
- Utility frameworks (Tailwind CSS)

## 9. Working with APIs

Example with fetch:

```jsx
import { useEffect, useState } from "react";

function Users() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then(res => res.json())
      .then(data => setUsers(data));
  }, []);

  return (
    <ul>
      {users.map(user => <li key={user.id}>{user.name}</li>)}
    </ul>
  );
}
```

## 10. Performance Features in React

- **Virtual DOM**: Efficient updates.
- **Keys in lists**: Help React identify items.
- **React.memo**: Prevents unnecessary re-renders.
- **useCallback and useMemo**: Optimize expensive operations.
- **Lazy loading**: `React.lazy` for code splitting.

## 11. Deployment

1. Build for production:
    
    ```bash
    npm run build
    ```
    
2. Deploy `dist/` folder:
    - Netlify
    - Vercel
    - Static server (Nginx, Apache)

## 12. Best Practices

- Keep components small and focused.
- Use meaningful names.
- Keep state minimal and at the correct level.
- Avoid prop drilling (use Context or state management libraries).
- Organize files by feature.
- Test components with Jest/React Testing Library.

## 13. React Ecosystem

- **State Management**: Redux, Zustand, Recoil.
- **Routing**: React Router.
- **Frameworks**: Next.js, Remix.
- **UI Libraries**: Material UI, Chakra UI, Ant Design.
- **Testing**: Jest, React Testing Library.

## 14. Summary

React is:

- A JavaScript library for building UIs.
- Solves performance and maintainability issues of traditional DOM manipulation.
- Uses Virtual DOM, components, and unidirectional data flow.
- Easy to learn and has a rich ecosystem.
- Suitable for everything from small apps to enterprise-scale SPAs.