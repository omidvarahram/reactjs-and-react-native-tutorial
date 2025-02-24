# Lifecycle Methods

[Back to Index](../index.md) | [⬅️ Back to Previous Page](4-state-management.md)

## Introduction to Component Lifecycle

In React, each component goes through a **lifecycle** from creation to removal. Understanding this lifecycle helps in managing side effects, optimizing performance, and ensuring clean unmounting.

Lifecycle stages:
1. **Mounting** – Component is created and inserted into the DOM.
2. **Updating** – Component is re-rendered due to state/props changes.
3. **Unmounting** – Component is removed from the DOM.

---

## Class Component Lifecycle Methods

### **Mounting Phase**

- **`constructor()`**: Initializes state and binds methods.

  ```javascript
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }
  ```

- **`componentDidMount()`**: Invoked after the component is mounted. Ideal for API calls or setting up subscriptions.

  ```javascript
  componentDidMount() {
    console.log("Component mounted");
  }
  ```

### **Updating Phase**

- **`shouldComponentUpdate()`**: Determines if the component should re-render. Useful for performance optimization.

  ```javascript
  shouldComponentUpdate(nextProps, nextState) {
    return nextState.count !== this.state.count;
  }
  ```

- **`componentDidUpdate()`**: Called after the component updates. Ideal for DOM manipulations or new API calls based on prop/state changes.

  ```javascript
  componentDidUpdate(prevProps, prevState) {
    if (prevState.count !== this.state.count) {
      console.log("Count updated");
    }
  }
  ```

### **Unmounting Phase**

- **`componentWillUnmount()`**: Cleanup method used to clear timers, cancel API calls, or remove event listeners.

  ```javascript
  componentWillUnmount() {
    console.log("Component will unmount");
  }
  ```

---

## Lifecycle in Functional Components (with Hooks)

Functional components use **Hooks** to manage lifecycle behaviors.

### **useEffect Hook**

The `useEffect` hook replaces multiple lifecycle methods.

- **`componentDidMount` equivalent:**

  ```javascript
  import { useEffect } from 'react';

  useEffect(() => {
    console.log("Component mounted");
  }, []);
  ```

- **`componentDidUpdate` equivalent:**

  ```javascript
  useEffect(() => {
    console.log("Component updated");
  });
  ```

- **`componentWillUnmount` equivalent:**

  ```javascript
  useEffect(() => {
    return () => {
      console.log("Component will unmount");
    };
  }, []);
  ```

### **Controlling Re-Renders with Dependencies**

The second parameter in `useEffect` (the dependency array) controls when the effect runs.

- **Run on specific state/prop change:**

  ```javascript
  useEffect(() => {
    console.log("Count changed");
  }, [count]);
  ```

- **Run once (on mount):** Pass an empty array `[]`.

- **Run on every render:** Omit the dependency array.

---

## Common Lifecycle Use Cases

1. **API calls** → `componentDidMount` or `useEffect`
2. **Event listeners** → Add in `componentDidMount`/`useEffect`, remove in `componentWillUnmount`/cleanup function
3. **Timers/Intervals** → Start in `componentDidMount`/`useEffect`, clear in cleanup
4. **DOM manipulations** → `componentDidUpdate` or `useEffect`

---

## Best Practices

- Avoid heavy computations inside lifecycle methods/hooks.
- Always clean up side effects in `useEffect` cleanup or `componentWillUnmount`.
- Use **`useMemo`** and **`useCallback`** to prevent unnecessary re-renders.
- Minimize dependencies in `useEffect` to avoid unintended side effects.

---

[⬅️ Back to Index](../index.md) | [➡️ Next: React Hooks](6-hooks.md)
