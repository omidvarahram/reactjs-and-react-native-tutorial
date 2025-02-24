# Introduction to React

[Back to Index](../index.md)

## What is React?

React is a **JavaScript library** for building **user interfaces** (UIs), primarily for single-page applications (SPAs). Developed and maintained by **Facebook** (now Meta), React allows developers to create large web applications that can update and render efficiently in response to data changes.

**Key Points:**
- **Declarative:** React makes it simple to design interactive UIs.
- **Component-Based:** Build encapsulated components that manage their own state.
- **Learn Once, Write Anywhere:** React can be used for web, mobile (React Native), and even desktop apps.

**Example:**

```javascript
import React from 'react';
import ReactDOM from 'react-dom/client';

function App() {
  return <h1>Hello, World!</h1>;
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);
```

---

## Key Features of React

1. **JSX (JavaScript XML):** Syntax extension that looks similar to HTML and is used to describe UI structure.
2. **Virtual DOM:** React uses a virtual representation of the DOM, which allows for efficient updates.
3. **Component-Based Architecture:** Break UIs into reusable, independent components.
4. **Unidirectional Data Flow:** Data flows in one direction, making it easier to debug.
5. **Hooks API:** Introduced in React 16.8, hooks allow functional components to manage state and side effects.

---

## Virtual DOM & Reconciliation

The **Virtual DOM** is a lightweight JavaScript representation of the actual DOM. React uses it to optimize UI updates.

**How It Works:**
1. When the state of an object changes, React updates the virtual DOM.
2. React then compares the virtual DOM with a snapshot of its previous state using a **diffing algorithm**.
3. It then updates only the elements that changed in the real DOM — improving performance.

**Example:**

```javascript
function Counter() {
  const [count, setCount] = React.useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

Every time you click the button, only the `<p>` element displaying the count is updated.

**Tip:** Always use **unique keys** when rendering lists to help React efficiently manage the virtual DOM.

---

## JSX Syntax

**JSX (JavaScript XML)** lets you write HTML-like syntax inside JavaScript code. It is transpiled by tools like **Babel** into regular JavaScript before running in the browser.

**Basic JSX Example:**

```javascript
const element = <h1>Hello, World!</h1>;

ReactDOM.render(element, document.getElementById('root'));
```

**Key JSX Rules:**
- **Return a single parent element:** Wrap multiple elements inside a parent tag or use React fragments `<>...</>`.
- **Use `className` instead of `class`:** `class` is a reserved word in JavaScript.
- **Self-close empty tags:** e.g., `<img />`, `<input />`.
- **Use curly braces `{}` for dynamic expressions:**

```javascript
const name = 'React';
const element = <h1>Welcome to {name}!</h1>;
```

**JSX Tips:**
- Comments inside JSX use `{/* like this */}`.
- Avoid using inline styles for complex styling — prefer CSS classes or styled-components.

---

## Why Choose React?

1. **Large Ecosystem:** Tons of libraries, tools, and community support.
2. **Flexibility:** Use it with various architectures (MVC, Flux, Redux, etc.).
3. **Strong Community & Corporate Backing:** Widely adopted across industries.
4. **Performance Optimizations:** Virtual DOM and diffing algorithm ensure fast updates.

---

## Quick Tips

- Use **React Developer Tools** for Chrome/Firefox to inspect components.
- Always **break UI into smaller components** for easier maintenance.
- Prefer **functional components** and hooks over class components in modern React.

---

[⬅️ Back to Index](../index.md)

