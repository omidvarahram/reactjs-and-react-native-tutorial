# React Hooks

[Back to Index](../index.md) | [⬅️ Back to Previous Page](5-lifecycle-methods.md)

## What Are Hooks?

**React Hooks** are functions that let you use **state** and other **React features** in functional components. Introduced in **React 16.8**, they allow functional components to have side effects, manage state, and handle lifecycle events without using class components.

**Key Benefits:**
- Write cleaner and more concise code.
- Share logic across components using **custom hooks**.
- Replace lifecycle methods in functional components.

---

## useState

`useState` allows you to add state to functional components.

**Example:**

```javascript
import { useState } from 'react';

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
- Returns an array with **current state** and a **setter function**.
- Triggers a re-render when the state is updated.

---

## useEffect

`useEffect` handles **side effects** like API calls, subscriptions, and manual DOM manipulations.

**Example:**

```javascript
import { useEffect, useState } from 'react';

function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => setSeconds(s => s + 1), 1000);
    return () => clearInterval(interval); // Cleanup
  }, []);

  return <p>Timer: {seconds} seconds</p>;
}
```

**Dependency Array:**
- `[]` → Runs once on mount (like `componentDidMount`).
- `[variable]` → Runs on variable change.
- Omit → Runs on every render.

---

## useContext

`useContext` allows functional components to access the **Context API**.

**Example:**

```javascript
import { createContext, useContext } from 'react';

const ThemeContext = createContext('light');

function ThemedComponent() {
  const theme = useContext(ThemeContext);
  return <p>Current Theme: {theme}</p>;
}
```

**Tip:** Combine with `useReducer` or global state libraries for complex state management.

---

## useRef

`useRef` provides a **mutable reference** that persists across renders, often used to directly access DOM elements or store values without causing re-renders.

**Example:**

```javascript
import { useRef } from 'react';

function FocusInput() {
  const inputRef = useRef();

  const focusInput = () => {
    inputRef.current.focus();
  };

  return (
    <div>
      <input ref={inputRef} />
      <button onClick={focusInput}>Focus Input</button>
    </div>
  );
}
```

**Other Use Cases:**
- Storing previous state.
- Managing timers.

---

## useMemo & useCallback

### **useMemo:** Memoizes expensive computations.

**Example:**

```javascript
import { useMemo, useState } from 'react';

function ExpensiveCalculation({ num }) {
  const result = useMemo(() => {
    return num * 2;
  }, [num]);

  return <p>Result: {result}</p>;
}
```

### **useCallback:** Memoizes callback functions to prevent unnecessary re-renders.

**Example:**

```javascript
import { useCallback, useState } from 'react';

function Button() {
  const [count, setCount] = useState(0);

  const handleClick = useCallback(() => setCount(c => c + 1), []);

  return <button onClick={handleClick}>Count: {count}</button>;
}
```

---

## Custom Hooks

Create reusable hooks for shared logic.

**Example:**

```javascript
import { useState, useEffect } from 'react';

function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch(url)
      .then((response) => response.json())
      .then((data) => {
        setData(data);
        setLoading(false);
      });
  }, [url]);

  return { data, loading };
}
```

**Using the Custom Hook:**

```javascript
const { data, loading } = useFetch('https://api.example.com/data');
if (loading) return <p>Loading...</p>;
return <div>{JSON.stringify(data)}</div>;
```

---

## Best Practices

- Use hooks **only inside functional components or custom hooks**.
- **Do not call hooks inside loops, conditions, or nested functions.**
- Always follow **React’s Hook Rules**.

---

[⬅️ Back to Index](../index.md) | [➡️ Next: Event Handling](7-event-handling.md)
