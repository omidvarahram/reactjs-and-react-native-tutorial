# Side Effects and Data Fetching

[Back to Index](../index.md) | [⬅️ Back to Previous Page](9-context-api.md)

## What Are Side Effects?

In React, a **side effect** is any action that affects something outside the scope of the current function, such as:

- **Data fetching**
- **Subscriptions**
- **Timers**
- **Direct DOM manipulations**

React’s **`useEffect`** hook is designed to manage side effects in functional components.

---

## useEffect Hook Basics

`useEffect` lets you synchronize a component with external systems like APIs or browser events.

**Syntax:**

```javascript
useEffect(() => {
  // Side effect code here
  return () => {
    // Cleanup code (optional)
  };
}, [dependencies]);
```

**Example:** Logging on every render:

```javascript
useEffect(() => {
  console.log("Component rendered");
});
```

---

## Controlling Side Effects with Dependencies

The **dependency array** controls when `useEffect` runs:

- **Empty array (`[]`)** → Runs once (like `componentDidMount`).
- **Specific variables (`[count]`)** → Runs when `count` changes.
- **No array** → Runs after every render.

**Example:**

```javascript
useEffect(() => {
  console.log(`Count is ${count}`);
}, [count]);
```

---

## Cleaning Up Side Effects

If your side effect creates a subscription, timer, or event listener, clean it up to avoid memory leaks.

**Example:**

```javascript
useEffect(() => {
  const timer = setInterval(() => console.log("Tick"), 1000);
  return () => clearInterval(timer); // Cleanup
}, []);
```

---

## Data Fetching in React

### **1. Fetch API with useEffect**

```javascript
import { useState, useEffect } from 'react';

function FetchData() {
  const [data, setData] = useState([]);

  useEffect(() => {
    fetch('https://jsonplaceholder.typicode.com/posts')
      .then((response) => response.json())
      .then((json) => setData(json));
  }, []);

  return (
    <ul>
      {data.map((post) => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  );
}
```

### **2. Using Async/Await with useEffect**

```javascript
useEffect(() => {
  const fetchData = async () => {
    const response = await fetch('https://jsonplaceholder.typicode.com/posts');
    const json = await response.json();
    setData(json);
  };

  fetchData();
}, []);
```

---

## Handling Loading and Error States

**Example:**

```javascript
function FetchWithStatus() {
  const [data, setData] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    fetch('https://jsonplaceholder.typicode.com/posts')
      .then((response) => response.json())
      .then((json) => setData(json))
      .catch((err) => setError(err))
      .finally(() => setLoading(false));
  }, []);

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error.message}</p>;

  return (
    <ul>
      {data.map((post) => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  );
}
```

---

## Advanced Data Fetching Libraries

### **1. Axios** *(Promise-based HTTP client)*

```bash
npm install axios
```

**Example:**

```javascript
import axios from 'axios';

useEffect(() => {
  axios.get('https://jsonplaceholder.typicode.com/posts')
    .then((response) => setData(response.data))
    .catch((error) => console.error(error));
}, []);
```

### **2. React Query (TanStack Query)** *(For data caching and background sync)*

```bash
npm install @tanstack/react-query
```

**Example:**

```javascript
import { useQuery } from '@tanstack/react-query';

function Posts() {
  const { data, isLoading, error } = useQuery(['posts'], () =>
    fetch('https://jsonplaceholder.typicode.com/posts').then(res => res.json())
  );

  if (isLoading) return <p>Loading...</p>;
  if (error) return <p>Error loading data</p>;

  return (
    <ul>
      {data.map(post => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  );
}
```

---

## Best Practices for Side Effects

1. **Always clean up side effects** to avoid memory leaks.
2. **Use try/catch** in async functions to handle errors.
3. **Debounce expensive operations** inside `useEffect`.
4. **Use libraries like React Query** for complex data fetching needs.
5. **Avoid triggering infinite loops** by correctly managing dependencies in the dependency array.

---

[⬅️ Back to Index](../index.md) | [➡️ Next: Routing in React](11-side-effect-tools.md)
