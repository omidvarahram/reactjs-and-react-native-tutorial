# Performance Optimization

[Back to Index](../index.md) | [⬅️ Back to Previous Page](12-routing.md) | [➡️ Next: Accessibility in React](14-accessibility.md)

## Introduction to Performance Optimization

Performance optimization in React ensures that applications run smoothly, with minimal lag and efficient resource usage. While React’s virtual DOM optimizes rendering, large-scale applications require deliberate strategies for sustained performance.

---

## Identifying Performance Bottlenecks

1. **React Developer Tools:**
   - Use the **Profiler** tab to measure component render times.
2. **Chrome DevTools:**
   - Analyze memory usage, CPU performance, and network activity.
3. **Web Vitals:**
   - Monitor key metrics like **Largest Contentful Paint (LCP)**, **First Input Delay (FID)**, and **Cumulative Layout Shift (CLS)**.

---

## Optimizing Component Rendering

### **1. Memoization with `React.memo`**

Prevents unnecessary re-renders by memoizing functional components.

```javascript
import React, { memo } from 'react';

const ExpensiveComponent = memo(({ data }) => {
  console.log('Rendering ExpensiveComponent');
  return <div>{data}</div>;
});
```

### **2. Memoizing Functions with `useCallback`**

Prevents function recreation on every render.

```javascript
import { useCallback, useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  const increment = useCallback(() => setCount((c) => c + 1), []);

  return <button onClick={increment}>Count: {count}</button>;
}
```

### **3. Caching Values with `useMemo`**

Memoizes expensive computations.

```javascript
import { useMemo } from 'react';

function ExpensiveCalculation({ num }) {
  const result = useMemo(() => num * 2, [num]);
  return <p>Result: {result}</p>;
}
```

---

## Code Splitting and Lazy Loading

### **1. Dynamic Imports**

Split code into smaller chunks for faster initial load.

```javascript
import { lazy, Suspense } from 'react';

const LazyComponent = lazy(() => import('./LazyComponent'));

function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <LazyComponent />
    </Suspense>
  );
}
```

### **2. Route-Based Code Splitting**

Combine **React Router** with dynamic imports.

```javascript
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
import { lazy, Suspense } from 'react';

const Home = lazy(() => import('./Home'));
const About = lazy(() => import('./About'));

function App() {
  return (
    <Router>
      <Suspense fallback={<div>Loading...</div>}>
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/about" element={<About />} />
        </Routes>
      </Suspense>
    </Router>
  );
}
```

---

## Optimizing Lists and Tables

### **1. Virtualization with `react-window` or `react-virtualized`**

Renders only visible items in large lists.

```bash
npm install react-window
```

```javascript
import { FixedSizeList as List } from 'react-window';

function VirtualizedList({ items }) {
  return (
    <List height={400} itemCount={items.length} itemSize={35} width={300}>
      {({ index, style }) => <div style={style}>{items[index]}</div>}
    </List>
  );
}
```

### **2. Using Unique Keys in Lists**

Use stable, unique keys to help React optimize re-renders.

```javascript
{items.map(item => (
  <div key={item.id}>{item.name}</div>
))}
```

---

## Managing Re-Renders

1. **Minimize State in Components:** Keep local state as lean as possible.
2. **Lift State Up Judiciously:** Only when multiple components need to share state.
3. **Avoid Inline Functions in JSX:** Memoize callbacks with `useCallback`.
4. **Use Pure Components:** Functional components with `React.memo` or class components extending `PureComponent`.

---

## Optimizing Network Requests

1. **Debounce Rapid-Fire Requests:**

```javascript
import { useState } from 'react';

let debounceTimer;

function Search() {
  const [query, setQuery] = useState('');

  const handleChange = (e) => {
    clearTimeout(debounceTimer);
    const value = e.target.value;

    debounceTimer = setTimeout(() => setQuery(value), 300);
  };

  return <input onChange={handleChange} placeholder="Search..." />;
}
```

2. **Use Caching Libraries:** (e.g., **React Query**) for data fetching and caching.
3. **Batch Network Requests:** Reduce API calls using tools like **GraphQL** or custom batchers.

---

## Monitoring and Measuring Performance

1. **React Profiler:** Analyze component rendering times.
2. **Lighthouse Audits:** Evaluate performance, accessibility, and SEO.
3. **Web Vitals Monitoring:** Track user-centric performance metrics.
4. **Third-Party Monitoring Tools:** (e.g., **Sentry**, **Datadog**)

---

[⬅️ Back to Index](../index.md) | [➡️ Next: Accessibility in React](14-accessibility.md)

