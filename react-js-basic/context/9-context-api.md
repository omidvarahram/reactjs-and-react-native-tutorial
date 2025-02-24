# Context API

[Back to Index](../index.md) | [⬅️ Back to Previous Page](8-forms.md)

## Introduction to Context API

The **Context API** in React provides a way to pass data through the component tree **without having to pass props manually at every level**. It helps in managing global data like user authentication, themes, and app settings.

**Use Cases:**
- Global state management
- Theming
- Language preferences
- User authentication

---

## Creating and Using Context

### **1. Creating Context**

Use `createContext` to define a new context.

```javascript
import { createContext } from 'react';

const ThemeContext = createContext('light');
```

### **2. Providing Context**

Wrap components with the **Provider** to make the context available.

```javascript
import { useState } from 'react';

function App() {
  const [theme, setTheme] = useState('light');

  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      <Toolbar />
    </ThemeContext.Provider>
  );
}
```

### **3. Consuming Context**

Use the **useContext** hook or the **Consumer** component to access context values.

**With useContext:**

```javascript
import { useContext } from 'react';

function ThemedButton() {
  const { theme, setTheme } = useContext(ThemeContext);

  return (
    <button onClick={() => setTheme(theme === 'light' ? 'dark' : 'light')}>
      Current Theme: {theme}
    </button>
  );
}
```

**With Consumer (Legacy approach):**

```javascript
<ThemeContext.Consumer>
  {(value) => <button>{value.theme}</button>}
</ThemeContext.Consumer>
```

---

## Best Practices for Context API

1. **Avoid Overusing Context:**
   - For frequent state updates (like form inputs), context can lead to unnecessary re-renders.

2. **Use Multiple Contexts for Large Apps:**
   - Example: Separate contexts for user data, theme, and settings.

3. **Memoize Context Values:**
   - Prevent re-renders by wrapping context values with `useMemo`.

```javascript
const contextValue = useMemo(() => ({ theme, setTheme }), [theme]);
```

4. **Combine with useReducer for Complex State:**

```javascript
const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    default:
      return state;
  }
}

const CounterContext = createContext();

function CounterProvider({ children }) {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <CounterContext.Provider value={{ state, dispatch }}>
      {children}
    </CounterContext.Provider>
  );
}
```

---

## Context API vs. State Management Libraries

| **Feature**               | **Context API**     | **Redux/MobX/Recoil**     |
|---------------------------|---------------------|---------------------------|
| Boilerplate Code          | Low                 | Medium to High            |
| Ideal Use Case            | Small to Medium Apps| Large-scale Apps          |
| Built-in React Solution   | ✅                  | ❌                        |
| Performance Optimization  | Manual (useMemo)    | Built-in                  |

**Tip:** For simple use cases, Context API is sufficient. For complex state with multiple dependencies, consider external libraries.

---

[⬅️ Back to Index](../index.md) | [➡️ Next: Side Effects and Data Fetching](10-side-effects.md)
