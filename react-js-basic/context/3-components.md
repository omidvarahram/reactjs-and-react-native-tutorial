# Components in React

[Back to Index](../index.md) | [⬅️ Back to Previous Page](2-project-setup.md)

## What Are Components?

**Components** are the building blocks of a React application. Each component is a reusable, self-contained unit that defines part of the UI.

- **Functional Components:** Simpler, recommended for modern React development.
- **Class-Based Components:** Legacy approach, still seen in older codebases.

---

## Functional Components

Functional components are JavaScript functions that return JSX.

**Example:**

```javascript
function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}

export default Greeting;
```

**Using the Component:**

```javascript
<Greeting name="Alice" />
```

### **React Hooks in Functional Components:**

Functional components use **Hooks** to manage state and side effects.

**useState Example:**

```javascript
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

export default Counter;
```

---

## Class-Based Components

Class components use ES6 classes and the `render()` method to return JSX.

**Example:**

```javascript
import React, { Component } from 'react';

class Welcome extends Component {
  render() {
    return <h1>Hello, {this.props.name}!</h1>;
  }
}

export default Welcome;
```

### **Lifecycle Methods in Class Components:**

- `componentDidMount()` – Runs after the component mounts.
- `componentDidUpdate()` – Runs after state or props update.
- `componentWillUnmount()` – Runs before the component is removed.

---

## JSX Deep Dive

JSX (JavaScript XML) is a syntax extension that allows mixing HTML with JavaScript.

### **JSX Best Practices:**
- Always return a single parent element.
- Use `className` instead of `class`.
- Wrap dynamic values inside curly braces `{}`.

**Example with Conditions & Loops:**

```javascript
const names = ['Alice', 'Bob', 'Charlie'];

function NameList() {
  return (
    <ul>
      {names.map((name) => (
        <li key={name}>{name}</li>
      ))}
    </ul>
  );
}
```

---

## Props and PropTypes

### **Props (Properties):**
Props are used to pass data from parent to child components.

**Example:**

```javascript
function User(props) {
  return <h2>User: {props.name}</h2>;
}

<User name="John" />
```

### **PropTypes for Type-Checking:**

Use the `prop-types` package to enforce prop types.

```bash
npm install prop-types
```

**Example:**

```javascript
import PropTypes from 'prop-types';

function User(props) {
  return <h2>User: {props.name}</h2>;
}

User.propTypes = {
  name: PropTypes.string.isRequired,
};
```

---

## Mapping Arrays & Keys

When rendering lists, React requires a unique `key` for each item.

**Example:**

```javascript
const fruits = ['Apple', 'Banana', 'Cherry'];

function FruitList() {
  return (
    <ul>
      {fruits.map((fruit, index) => (
        <li key={index}>{fruit}</li>
      ))}
    </ul>
  );
}
```

### **Key Tips:**
- Use stable, unique keys (avoid array indexes if possible).
- Keys help React optimize re-renders.

---

## Component Libraries Creation & Integration

### **Creating a Component Library:**

1. **Create Reusable Components:**
   - Maintain consistent styling and API.

2. **Bundle with Tools like Rollup or Webpack.**

3. **Publish to NPM:**

```bash
npm login
npm publish
```

### **Integrating Third-Party Libraries:**

Popular UI libraries:
- **Material-UI (MUI):**

```bash
npm install @mui/material @emotion/react @emotion/styled
```

- **Ant Design:**

```bash
npm install antd
```

---

[⬅️ Back to Index](../index.md) | [➡️ Next: State Management](4-state-management.md)