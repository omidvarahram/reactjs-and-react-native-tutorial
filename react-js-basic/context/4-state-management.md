# State Management

[Back to Index](../index.md) | [⬅️ Back to Previous Page](3-components.md)

## Introduction to State

In React, **state** is a built-in object that stores property values that belong to a component. When the state object changes, the component re-renders to reflect those changes.

- **Local State:** Managed within individual components.
- **Global State:** Managed across multiple components.

---

## useState Hook

The `useState` hook allows functional components to manage state.

**Example:**

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
```

**Key Points:**
- The state is initialized using `useState(initialValue)`.
- `setCount` updates the state and triggers a re-render.

---

## State in Class Components

Class components use `this.state` and `this.setState()` for state management.

**Example:**

```javascript
import React, { Component } from 'react';

class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  increment = () => {
    this.setState({ count: this.state.count + 1 });
  };

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={this.increment}>Increment</button>
      </div>
    );
  }
}
```

---

## Lifting State Up

When multiple components need to share state, **lift the state up** to their closest common ancestor.

**Example:**

```javascript
function Parent() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <Child count={count} />
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

function Child({ count }) {
  return <h2>Count: {count}</h2>;
}
```

**Tip:** Minimize lifting state when possible by using context or state management libraries.

---

## Prop Drilling

**Prop Drilling** occurs when you pass data through multiple layers of components, even if intermediate components don’t need it.

**Example:**

```javascript
function Grandparent() {
  const [data, setData] = useState("Hello");
  return <Parent data={data} />;
}

function Parent({ data }) {
  return <Child data={data} />;
}

function Child({ data }) {
  return <h3>{data}</h3>;
}
```

### **Solutions to Prop Drilling:**
- **React Context API**
- **State Management Libraries** (Redux, Zustand)

---

## Best Practices for State Management

1. **Keep state as local as possible.**
2. **Use global state only when necessary.**
3. **Avoid deeply nested state objects.**
4. **Use memoization (`useMemo`, `useCallback`) to avoid unnecessary re-renders.**
5. **Normalize complex data structures.**

---

## When to Use External State Management Libraries

- When **multiple components** need shared state.
- When dealing with **complex data flows**.
- When the app scales beyond basic prop drilling and context API.

**Popular Libraries:**
- **Redux (with Redux Toolkit)**
- **Zustand**
- **MobX**

---

[⬅️ Back to Index](../index.md) | [➡️ Next: Lifecycle Methods](5-lifecycle-methods.md)
