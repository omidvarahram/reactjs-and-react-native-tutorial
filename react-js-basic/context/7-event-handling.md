# Event Handling

[Back to Index](../index.md) | [⬅️ Back to Previous Page](6-hooks.md)

## Introduction to Event Handling in React

React uses a **synthetic event system** that wraps around the native browser events to ensure cross-browser compatibility. Events in React are named using **camelCase** (`onClick` instead of `onclick`) and are passed as functions.

**Example:**

```javascript
function Button() {
  const handleClick = () => alert("Button Clicked!");

  return <button onClick={handleClick}>Click Me</button>;
}
```

---

## Common Events in React

### **1. Mouse Events**
- `onClick` — Click event.
- `onDoubleClick` — Double-click event.
- `onMouseEnter` / `onMouseLeave` — Mouse hover events.
- `onContextMenu` — Right-click event.

### **2. Keyboard Events**
- `onKeyDown` — When a key is pressed.
- `onKeyUp` — When a key is released.
- `onKeyPress` — When a key is pressed (deprecated, use `onKeyDown`).

### **3. Form Events**
- `onChange` — Value change in form inputs.
- `onSubmit` — Form submission.
- `onFocus` / `onBlur` — Focus events.

### **4. Touch Events**
- `onTouchStart` / `onTouchEnd` — Touch interactions.
- `onTouchMove` — Detects finger movement on the screen.

---

## Passing Arguments to Event Handlers

To pass arguments to event handlers, use arrow functions.

**Example:**

```javascript
function ListItem({ id }) {
  const handleClick = (id) => {
    alert(`Item ${id} clicked`);
  };

  return <li onClick={() => handleClick(id)}>Item {id}</li>;
}
```

---

## Synthetic Events

React wraps native events into a **SyntheticEvent** to provide a consistent interface.

**Example:**

```javascript
function Form() {
  const handleSubmit = (e) => {
    e.preventDefault(); // Prevent page reload
    alert("Form submitted!");
  };

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" />
      <button type="submit">Submit</button>
    </form>
  );
}
```

**Tip:** Synthetic events are pooled for performance, so their properties may be nullified after the event callback runs. To access the event asynchronously, use `e.persist()`.

---

## Event Propagation

React supports **event bubbling** and **event capturing**.

- **Bubbling (default):** Event propagates from the target element up.
- **Capturing:** Event propagates from the root down to the target.

**Stopping Propagation:**

```javascript
function Parent() {
  const handleParentClick = () => alert("Parent clicked");
  const handleChildClick = (e) => {
    e.stopPropagation();
    alert("Child clicked");
  };

  return (
    <div onClick={handleParentClick}>
      <button onClick={handleChildClick}>Click Me</button>
    </div>
  );
}
```

---

## Debouncing & Throttling Events

- **Debouncing:** Ensures that a function is only called after a certain delay since the last event.
- **Throttling:** Ensures that a function is called at most once every specified time interval.

**Debouncing Example:**

```javascript
import { useState } from 'react';

function Search() {
  const [query, setQuery] = useState("");
  let debounceTimer;

  const handleChange = (e) => {
    clearTimeout(debounceTimer);
    const value = e.target.value;

    debounceTimer = setTimeout(() => setQuery(value), 300);
  };

  return <input onChange={handleChange} placeholder="Search..." />;
}
```

---

## Dynamic Event Binding

Dynamic event handling allows components to attach or remove event listeners conditionally.

**Example:**

```javascript
import { useEffect, useState } from 'react';

function WindowResize() {
  const [width, setWidth] = useState(window.innerWidth);

  useEffect(() => {
    const handleResize = () => setWidth(window.innerWidth);
    window.addEventListener("resize", handleResize);

    return () => window.removeEventListener("resize", handleResize);
  }, []);

  return <p>Window width: {width}px</p>;
}
```

---

## Best Practices

- Use **arrow functions** inside JSX sparingly to avoid unnecessary re-renders.
- Always **clean up** event listeners in `useEffect` cleanup functions.
- **Debounce or throttle** heavy events (e.g., scroll, resize).
- **Stop event propagation** when necessary using `e.stopPropagation()`.

---

[⬅️ Back to Index](../index.md) | [➡️ Next: Forms in React](8-forms.md)

