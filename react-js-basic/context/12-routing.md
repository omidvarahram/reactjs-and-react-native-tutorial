# Routing in React

[Back to Index](../index.md) | [⬅️ Back to Previous Page](11-side-effects-tools.md) | [➡️ Next: Performance Optimization](13-performance.md)

## Introduction to Routing

Routing in React allows you to create **single-page applications (SPAs)** where navigation between pages does not trigger a full page reload. The most popular library for routing in React is **React Router**.

---

## React Router Setup

### **1. Install React Router**

```bash
npm install react-router-dom
```

### **2. Basic Setup**

```javascript
import { BrowserRouter as Router, Routes, Route, Link } from 'react-router-dom';

function App() {
  return (
    <Router>
      <nav>
        <Link to="/">Home</Link>
        <Link to="/about">About</Link>
      </nav>

      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </Router>
  );
}

function Home() {
  return <h2>Home Page</h2>;
}

function About() {
  return <h2>About Page</h2>;
}
```

---

## Dynamic Routes and Nested Routing

Dynamic routing enables routes that can adapt based on URL parameters.

### **1. Dynamic Routes**

```javascript
import { useParams } from 'react-router-dom';

function UserProfile() {
  const { id } = useParams();
  return <h2>User ID: {id}</h2>;
}

<Routes>
  <Route path="/user/:id" element={<UserProfile />} />
</Routes>
```

### **2. Nested Routes**

Nested routes allow hierarchical routing structures.

```javascript
<Routes>
  <Route path="/dashboard" element={<Dashboard />}>
    <Route path="stats" element={<Stats />} />
    <Route path="settings" element={<Settings />} />
  </Route>
</Routes>

function Dashboard() {
  return (
    <div>
      <h2>Dashboard</h2>
      <Outlet />
    </div>
  );
}
```

---

## Route Guards and Lazy Loading

### **1. Route Guards (Protected Routes)**

Use route guards to restrict access based on conditions like authentication.

```javascript
import { Navigate } from 'react-router-dom';

function PrivateRoute({ children, isAuthenticated }) {
  return isAuthenticated ? children : <Navigate to="/login" />;
}

<Routes>
  <Route
    path="/profile"
    element={<PrivateRoute isAuthenticated={true}><Profile /></PrivateRoute>}
  />
</Routes>
```

### **2. Lazy Loading Routes**

Lazy load components for better performance.

```javascript
import { lazy, Suspense } from 'react';

const LazyAbout = lazy(() => import('./About'));

function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <Routes>
        <Route path="/about" element={<LazyAbout />} />
      </Routes>
    </Suspense>
  );
}
```

---

## Best Practices

1. **Use meaningful URLs** for better SEO and user experience.
2. **Implement lazy loading** for heavy components.
3. **Secure private routes** using authentication guards.
4. **Use error boundaries** to catch errors in route components.

---

[⬅️ Back to Index](../index.md) | [➡️ Next: Performance Optimization](13-performance.md)

