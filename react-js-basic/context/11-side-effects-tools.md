# Side Effect Tools

[Back to Index](../index.md) | [⬅️ Back to Previous Page](10-side-effects.md)

## Introduction to Side Effect Tools

Managing side effects in React can become complex as applications grow. While `useEffect` handles simple cases, advanced tools like **Redux-Saga**, **Redux-Thunk**, and **React Query** provide more control and structure for handling side effects.

---

## Redux Thunk

**Redux Thunk** is a middleware that allows you to write action creators that return a function instead of an action.

### **1. Installation**

```bash
npm install redux-thunk
```

### **2. Basic Setup**

```javascript
import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';

const store = createStore(reducer, applyMiddleware(thunk));
```

### **3. Example Thunk**

```javascript
const fetchData = () => {
  return (dispatch) => {
    dispatch({ type: 'FETCH_START' });
    fetch('https://jsonplaceholder.typicode.com/posts')
      .then((response) => response.json())
      .then((data) => dispatch({ type: 'FETCH_SUCCESS', payload: data }))
      .catch((error) => dispatch({ type: 'FETCH_ERROR', error }));
  };
};
```

---

## Redux Saga

**Redux Saga** uses **generator functions** to handle side effects.

### **1. Installation**

```bash
npm install redux-saga
```

### **2. Basic Setup**

```javascript
import createSagaMiddleware from 'redux-saga';
import { createStore, applyMiddleware } from 'redux';

const sagaMiddleware = createSagaMiddleware();
const store = createStore(reducer, applyMiddleware(sagaMiddleware));

sagaMiddleware.run(rootSaga);
```

### **3. Example Saga**

```javascript
import { call, put, takeEvery } from 'redux-saga/effects';

function* fetchData() {
  try {
    const response = yield call(fetch, 'https://jsonplaceholder.typicode.com/posts');
    const data = yield response.json();
    yield put({ type: 'FETCH_SUCCESS', payload: data });
  } catch (error) {
    yield put({ type: 'FETCH_ERROR', error });
  }
}

function* watchFetchData() {
  yield takeEvery('FETCH_REQUEST', fetchData);
}

export default function* rootSaga() {
  yield watchFetchData();
}
```

---

## React Query (TanStack Query)

**React Query** simplifies data fetching, caching, and synchronization.

### **1. Installation**

```bash
npm install @tanstack/react-query
```

### **2. Basic Example**

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

## Comparison of Side Effect Tools

| **Feature**             | **Redux Thunk**       | **Redux Saga**       | **React Query**         |
|-------------------------|-----------------------|----------------------|-------------------------|
| **Complexity**          | Low                   | Medium               | Low                     |
| **Ideal Use Case**      | Simple async actions  | Complex workflows    | Data fetching & caching |
| **Learning Curve**      | Easy                  | Moderate             | Easy                    |
| **Built-in Caching**    | ❌                    | ❌                   | ✅                      |

---

## Best Practices

1. **Use Thunk for simple async actions.**
2. **Use Saga for complex side effects (e.g., workflows, retries).**
3. **Use React Query for efficient data fetching and caching.**
4. **Combine tools when necessary** (e.g., Redux + React Query).

---

[⬅️ Back to Index](../index.md) | [➡️ Next: Performance Optimization](12-routing.md)
