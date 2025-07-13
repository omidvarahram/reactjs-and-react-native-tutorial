# Chapter 1: Introduction to React

---

## 1.1 What is React?

React is a component-based, open-source JavaScript **library** maintained by Meta, designed for building fast and interactive user interfaces. It emphasizes:

* **Declarative UI**: Define *what* the UI should look like; React handles DOM updates.
* **Virtual DOM**: An in-memory representation that diffs and efficiently updates the real DOM.
* **Unidirectional Data Flow**: Predictable state changes simplify debugging.
* **Functional Components with Hooks**: Modern React favors functions and hooks, while still supporting class components.

---

## Virtual DOM in React: What It Is and How It Works

---

### What Is the Virtual DOM?

The **Virtual DOM (VDOM)** is a lightweight, in-memory representation of the **real DOM** (Document Object Model). It is a **JavaScript object tree** that mirrors the structure of the UI as it should appear in the browser.

* It’s **not** visible to users.
* It’s **not** the same as the shadow DOM or browser DOM APIs.
* It’s a **performance optimization layer** between your React components and the real browser DOM.

---

### How Is It Different from the Real DOM?

| Aspect          | Virtual DOM              | Real DOM                                                      |
| --------------- | ------------------------ | ------------------------------------------------------------- |
| Format          | Plain JavaScript objects | Browser-managed live HTML/CSS/JS nodes                        |
| Mutation Cost   | Cheap – done in memory   | Expensive – triggers reflows/repaints                         |
| Accessibility   | Internal to React        | Accessible via browser APIs (e.g., `document.getElementById`) |
| Update Strategy | Batched diff and patch   | Direct mutation                                               |
| Performance     | Fast and optimized       | Slower when updating frequently                               |

---

### Why the Virtual DOM Exists

Direct manipulation of the real DOM is expensive:

* Updating DOM elements triggers **layout recalculations**, **reflows**, and **repaints**.
* Even a small change can have **wide ripple effects** in the browser rendering pipeline.

By introducing the VDOM:

* React can **batch multiple changes** and only apply the **minimal set of operations** to the real DOM.
* This makes UI updates **predictable, fast, and efficient**, especially in complex UIs.

---

### How React Uses the Virtual DOM (Step-by-Step)

Let’s walk through the lifecycle of how React renders and updates the DOM using the VDOM.

---

#### 📦 1. Initial Render

1. Your React code (`<App />`) is transformed into a **Virtual DOM tree** using `React.createElement(...)`.
2. React builds an **internal tree representation** of your UI (also called the **Fiber tree**).
3. React **calculates** what the real DOM should look like.
4. React **creates real DOM elements** based on the VDOM and **inserts them** into the page via `ReactDOM.createRoot(...).render(...)`.

---

#### 🔁 2. Update Phase (When State or Props Change)

Let’s say your component calls `setState(...)`. What happens?

##### Step 1: Trigger an Update

* React marks the component as **dirty**.
* It re-renders that component (i.e., calls the render function again).
* This produces a **new Virtual DOM tree** for that component and its children.

##### Step 2: Diffing (Reconciliation)

* React **compares the new Virtual DOM** to the **previous one** (old VDOM).
* This is called the **diffing algorithm**:

  * It walks both trees node-by-node.
  * It checks for differences in type, props, children.
  * It builds a **"patch plan"**: a list of minimal changes needed to update the real DOM.

##### Step 3: Commit Phase

* React applies this plan to the **real DOM**:

  * Add/remove elements
  * Update attributes/props
  * Add/remove event listeners
* This is the only point where React interacts with the real DOM.

---

### Example

Before `setCount(1)`:

```jsx
<div>
  <p>Count: 0</p>
  <button>Increment</button>
</div>
```

After `setCount(1)`:

```jsx
<div>
  <p>Count: 1</p>
  <button>Increment</button>
</div>
```

React’s diffing detects:

* Only the **text node inside `<p>` has changed**.
* It doesn’t touch the `<div>` or `<button>`.

So instead of replacing the entire component or subtree, it just updates:

```js
textNode.data = "Count: 1"
```

---

### Optimizations in React 18 and 19

* **React 18** introduced **concurrent rendering**: allows React to prepare VDOM updates in the background and interrupt long renders.
* **React 19** adds **compiler-driven auto-memoization**, reducing how often VDOM diffing is even necessary for stable subtrees.

---

### Summary

* The Virtual DOM is a **high-performance in-memory UI snapshot**.
* React uses it to **calculate what needs to change**, not how to change it.
* This avoids costly real DOM operations and provides a **predictable update model**.


## 1.2 History and Evolution

A timeline of React's major milestones:

* **2011** – Internal prototype at Facebook
* **2013** – Public open-source release
* **2015** – React Native introduced (mobile UI)
* **2018** – React 16.8 brings Hooks
* **2022** – React 18 adds automatic batching, transitions, and concurrent rendering
* **2024 (Dec 5)** – React 19 becomes stable, introducing hydration improvements, new compiler optimizations, and new hooks: `useActionState`, `useFormStatus`, `useOptimistic`, `use()` ([Code Your Path Coding School][1], [Saeloun Blog][2], [Peerlist][3], [Developer Way][4], [Curiosum][5], [React][6])

---

## 1.3 React vs. Other Frameworks

| Aspect        | React (v18/19)                    | Angular                      | Vue                        |
| ------------- | --------------------------------- | ---------------------------- | -------------------------- |
| Type          | Library                           | Full framework               | Progressive framework      |
| DOM Handling  | Virtual DOM                       | Change detection on real DOM | Virtual DOM                |
| Paradigm      | Functional + Hooks                | Class + Dependency Injection | Template + Composition API |
| Data Binding  | Unidirectional                    | Two-way binding              | Unidirectional             |
| Configuration | Very flexible (choose your stack) | Highly opinionated           | Moderately flexible        |
| Performance   | Excellent (compiler, memoization) | Good                         | Excellent                  |

React 19 introduces **automatic memoization via the React compiler**, reducing the need for `useMemo` and `useCallback` in most cases ([Curiosum][5], [RedDemonFox][7], [DEV Community][8]).

---

## 1.4 React Architecture & Ecosystem

### Core Architecture

* **react**: Core library for components and hooks.
* **react-dom** / **react-dom/client**: Rendering and hydration via `createRoot` and `hydrateRoot`.
* **React Fiber**: Enables interruptible and concurrent rendering.

### Rendering Lifecycle

1. JSX → compiled to `React.createElement`.
2. `ReactDOM.createRoot(container).render(<App />)` mounts the app.
3. State or prop changes trigger Virtual DOM diffing and optimized real DOM updates.

### Concurrency & Batching (React 18+)

* **Automatic batching** across events, timers, and promises.
* **Concurrent rendering and transitions** improve UX during async updates ([React][9], [WireFuture][10]).

### Hydration (React 19)

* `hydrateRoot` replaces old `hydrate` for improved streaming SSR support.
* Supports **selective**, **progressive**, and **out-of-order hydration**, optimizing interaction-ready elements first ([Telerik.com][11]).

### Compiler & Automatic Optimizations

* React 19 introduces a **React compiler** that auto-memoizes component values and functions, minimizing manual performance overhead ([DEV Community][8]).

### Forms, Actions & New Hooks

React 19 enhances forms and async logic with built-in primitives and hooks:

* New `<form action={…}>`: Native support for server/client actions.
* **`useActionState`**: Manage form submission state, result, and pending status ([React][6]).
* **`useFormStatus`**: Access parent form status (e.g. pending) via context ([WireFuture][10]).
* **`useOptimistic`**: Enables optimistic UI updates during async operations ([React][6]).
* **`use()`**: Inline suspension of Promises or Context reads, compatible with `Suspense` and `ErrorBoundary` ([WireFuture][10]).
* Other updates: Server Components stable by default, removal of `forwardRef`, built-in document metadata and asset preloading ([Peerlist][3]).

---

## 1.5 Setting Up the Environment

### Prerequisites

* Install **Node.js** (LTS).
* Optionally install **Yarn** (`npm install -g yarn`).

### Option 1: Create React App (CRA)

```bash
npx create-react-app my-app --template typescript
cd my-app
npm start
```

* ✅ Quick start with TS, Jest, RTL, webpack
* ❌ Limited build customizability

### Option 2: Vite (recommended)

```bash
npm create vite@latest my-app -- --template react-ts
cd my-app
npm install
npm run dev
```

* ⚡ Super fast HMR and build times
* ⚠️ Testing and SSR require manual setup

### Option 3: Custom Webpack

```bash
npm init -y
npm install react react-dom typescript @types/react @types/react-dom \
  webpack webpack-cli webpack-dev-server ts-loader babel-loader \
  @babel/core @babel/preset-env @babel/preset-react @babel/preset-typescript \
  html-webpack-plugin
```

* 🛠 Full control over build pipeline
* ⚠️ Requires manual config

---

### TypeScript Configuration

CRA and Vite auto-generate `tsconfig.json`. Manual setup requires:

```json
{
  "compilerOptions": {
    "jsx": "react-jsx",
    "target": "ES6",
    "module": "ESNext",
    "strict": true,
    "esModuleInterop": true,
    "moduleResolution": "node",
    "sourceMap": true
  },
  "include": ["src"]
}
```

Enable `"jsx": "react-jsx"` to support React 19’s new JSX transform ([OliCoding Blog][12], [Code Your Path Coding School][1], [React][6]).

---

### Testing: Jest + React Testing Library

#### CRA: built-in testing setup.

#### Vite/Webpack manual install:

```bash
npm install -D jest ts-jest @testing-library/react \
  @testing-library/jest-dom @testing-library/user-event jest-environment-jsdom @types/jest
```

Add `jest.config.js`:

```js
module.exports = {
  preset: 'ts-jest',
  testEnvironment: 'jsdom',
  setupFilesAfterEnv: ['@testing-library/jest-dom'],
  transform: { '^.+\\.(ts|tsx)$': 'ts-jest' }
};
```

Add to `package.json`:

```json
"scripts": {
  "test": "jest"
}
```

---

## Code Challenge

**Goal**: Bootstrap a React 19 + TS project using Vite, install Jest + RTL, create a `Counter` component, and test it:

1. Run `npm create vite@latest counter-app -- --template react-ts`
2. `cd counter-app && npm install` plus test libs above
3. Create `src/Counter.tsx`:

```tsx
import React, { useState } from 'react';

export function Counter() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(c => c + 1)}>Increment</button>
    </div>
  );
}
```

4. Create `src/Counter.test.tsx`:

```tsx
import { render, screen, fireEvent } from '@testing-library/react';
import { Counter } from './Counter';

test('counter increments', () => {
  render(<Counter />);
  fireEvent.click(screen.getByText('Increment'));
  expect(screen.getByText('Count: 1')).toBeInTheDocument();
});
```

5. Run `npm test` — the test should pass.

---

[⬅️ Back to React Foundation Index](../index.md)

[1]: https://www.codeyourpath.com/2024/05/28/react-19-compiler/?utm_source=chatgpt.com "React 19 Compiler - Best Auto Memoization Tool For Developers?"
[2]: https://blog.saeloun.com/2024/06/05/new-hooks-in-react-19/?utm_source=chatgpt.com "Explore new hooks coming up in React 19 - Saeloun Blog"
[3]: https://peerlist.io/blog/engineering/everything-you-need-to-know-about-react19?utm_source=chatgpt.com "Everything You Need to Know About React 19 - peerlist.io"
[4]: https://www.developerway.com/posts/react-compiler-soon?utm_source=chatgpt.com "React Compiler & React 19 - forget about memoization soon?"
[5]: https://curiosum.com/blog/react-19-features?utm_source=chatgpt.com "React 19: New Hooks and Features for Forms and Server-Side Components ..."
[6]: https://react.dev/blog/2024/12/05/react-19?utm_source=chatgpt.com "React v19 – React"
[7]: https://www.reddemonfox.com/blog/react-19-new-features?utm_source=chatgpt.com "What's New in React 19? - RedDemonFox"
[8]: https://dev.to/joodi/react-19-memoization-is-usememo-usecallback-no-longer-necessary-3ifn?utm_source=chatgpt.com "React 19 Memoization: Is useMemo & useCallback No Longer Necessary?"
[9]: https://react.dev/reference/react/useOptimistic?utm_source=chatgpt.com "useOptimistic – React"
[10]: https://wirefuture.com/post/react-19-features-and-migration-guide?utm_source=chatgpt.com "React 19 Features and Migration Guide - WireFuture"
[11]: https://www.telerik.com/blogs/guide-new-hooks-react-19?utm_source=chatgpt.com "The Guide to New Hooks in React 19 - Telerik"
[12]: https://blog.olicoding.dev/react-19-nextjs-14?utm_source=chatgpt.com "React 19 Insights"
