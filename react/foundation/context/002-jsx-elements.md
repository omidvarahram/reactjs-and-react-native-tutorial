## Chapter 2: JSX and React Elements

### 2.1 JSX Syntax and Rules

JSX is a JavaScript extension that resembles HTML, but it's compiled into `React.createElement(...)` calls. It allows embedding expressions using `{}`, enforces camelCase attributes (`className` instead of `class`), and wraps multiple elements in a single parent or fragment (`<>...</>`). JSX also escapes values by default to prevent XSS attacks.&#x20;

---

### 2.2 Elements and React.createElement

Under the hood, JSX:

```jsx
const el = <div id="app">Hi</div>;
```

becomes:

```js
const el = React.createElement('div', { id: 'app' }, 'Hi');
```

This returns a **React element**—an immutable object describing what should appear in the DOM.&#x20;

---

### 2.3 Nesting and React Children

JSX supports nested structures and arrays:

```jsx
<ul>
  {items.map(item => <li key={item.id}>{item.name}</li>)}
</ul>
```

Here, each `<li>` becomes a separate `ReactElement`, and the `key` prop ensures efficient diffing. `props.children` and `ReactNode` types encompass elements, strings, fragments, booleans, and more. ([react.dev][1])

---

### 2.4 cloneElement for Prop Injection

`React.cloneElement(element, props, ...children)` creates a new element based on an existing one, merging new props and optionally overriding children, while preserving `key` and `ref`.

#### Example:

```jsx
function Parent({ children }) {
  return React.Children.map(children,
    child => React.cloneElement(child, { className: 'highlight' })
  );
}
```

This pattern is ideal when you need to dynamically add props to child elements without rewriting JSX. ([LogRocket Blog][2])

---

### 2.5 Portals and Outside‑the‑Tree Rendering

`createPortal(children, domNode)` renders content into a DOM node outside the main React root—ideal for modals, tooltips, overlays:

```jsx
return createPortal(<ModalContent />, document.body);
```

Events and context behave as if they're within the React tree. ([react.dev][3])

---

### 2.6 Refs and DOM Interaction

Use `useRef()` or `createRef()` to access DOM nodes:

```jsx
const ref = useRef(null);
useLayoutEffect(() => {
  const rect = ref.current.getBoundingClientRect();
  console.log(rect.height);
}, []);
return <div ref={ref}>Content</div>;
```

Use `useLayoutEffect` to measure layout *before* painting to prevent flicker. ([Stack Overflow][4], [react.dev][5])

---

### 2.7 `dangerouslySetInnerHTML` (Use with Caution)

```jsx
<div dangerouslySetInnerHTML={{ __html: sanitizedHtml }} />
```

This bypasses React’s diffing and directly sets `innerHTML`. It must be sanitized (e.g. with DOMPurify) to mitigate XSS risks and is only suitable for sanitized or trusted HTML. ([LogRocket Blog][6])

---

## 📝 Summary: Core APIs for DOM & Element Control

* **JSX → `createElement`**: Core mechanism for building element trees.
* **`cloneElement`**: Adds or overrides props dynamically on existing elements.
* **Portals**: Render subtrees outside the main DOM hierarchy.
* **Refs + `useLayoutEffect`**: Direct and synchronous DOM manipulation or measurement.
* **`dangerouslySetInnerHTML`**: Raw HTML insertion—dangerous unless sanitized.

---

### 🧑‍💻 Code Challenge

Refactor this component:

```jsx
<MyContainer>
  <button>Click</button>
  <span>Info</span>
</MyContainer>
```

So `button` has `className="primary"` and `span` gains `style={{ color: 'red' }}` using `cloneElement`. Then render an informational modal using portals and measure its width using refs and `useLayoutEffect`.

---

Let me know when you're ready to move to Chapter 3!

[1]: https://react.dev/reference/react/cloneElement?utm_source=chatgpt.com "cloneElement – React"
[2]: https://blog.logrocket.com/using-react-cloneelement-function/?utm_source=chatgpt.com "Using the React.cloneElement () function to clone elements - LogRocket Blog"
[3]: https://react.dev/reference/react-dom/createPortal?utm_source=chatgpt.com "createPortal – React"
[4]: https://stackoverflow.com/questions/53539885/how-to-pass-style-using-dangerouslysetinnerhtml-in-react?utm_source=chatgpt.com "how to pass style using dangerouslySetInnerHTML in React"
[5]: https://react.dev/reference/react/useLayoutEffect?utm_source=chatgpt.com "useLayoutEffect – React"
[6]: https://blog.logrocket.com/using-dangerouslysetinnerhtml-react-application/?utm_source=chatgpt.com "Using dangerouslySetInnerHTML in a React application - LogRocket Blog"
