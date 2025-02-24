# Forms in React

[Back to Index](../index.md) | [⬅️ Back to Previous Page](7-event-handling.md)

## Introduction to Forms in React

Forms are essential for collecting user input in web applications. In React, handling forms requires controlled components, proper event handling, and validation mechanisms.

---

## Controlled vs. Uncontrolled Components

### **Controlled Components**
In controlled components, form data is handled by the React component state.

**Example:**

```javascript
import { useState } from 'react';

function ControlledForm() {
  const [value, setValue] = useState("");

  const handleChange = (e) => setValue(e.target.value);
  const handleSubmit = (e) => {
    e.preventDefault();
    alert(`Submitted: ${value}`);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" value={value} onChange={handleChange} />
      <button type="submit">Submit</button>
    </form>
  );
}
```

### **Uncontrolled Components**
In uncontrolled components, form data is handled by the DOM using **refs**.

**Example:**

```javascript
import { useRef } from 'react';

function UncontrolledForm() {
  const inputRef = useRef();

  const handleSubmit = (e) => {
    e.preventDefault();
    alert(`Submitted: ${inputRef.current.value}`);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" ref={inputRef} />
      <button type="submit">Submit</button>
    </form>
  );
}
```

---

## Handling Form Inputs

### **Text Inputs:**

```javascript
<input type="text" value={value} onChange={(e) => setValue(e.target.value)} />
```

### **Checkboxes:**

```javascript
<input type="checkbox" checked={isChecked} onChange={(e) => setIsChecked(e.target.checked)} />
```

### **Select Dropdown:**

```javascript
<select value={selected} onChange={(e) => setSelected(e.target.value)}>
  <option value="apple">Apple</option>
  <option value="banana">Banana</option>
  <option value="cherry">Cherry</option>
</select>
```

### **Radio Buttons:**

```javascript
<input type="radio" value="option1" checked={selected === 'option1'} onChange={(e) => setSelected(e.target.value)} /> Option 1
<input type="radio" value="option2" checked={selected === 'option2'} onChange={(e) => setSelected(e.target.value)} /> Option 2
```

---

## Form Validation Basics

### **Client-Side Validation Example:**

```javascript
function SimpleForm() {
  const [email, setEmail] = useState("");
  const [error, setError] = useState("");

  const handleSubmit = (e) => {
    e.preventDefault();
    if (!email.includes("@")) {
      setError("Invalid email address");
    } else {
      setError("");
      alert(`Email submitted: ${email}`);
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="email"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
      />
      {error && <p style={{ color: "red" }}>{error}</p>}
      <button type="submit">Submit</button>
    </form>
  );
}
```

---

## Common Mistakes and Performance Issues

1. **Re-rendering on every keystroke** → Use debouncing for heavy operations.
2. **Storing entire form data in global state** → Keep it local unless shared globally.
3. **Not validating before submission** → Implement client-side validation.
4. **Overusing controlled components** → Use uncontrolled components for simple use cases.

---

## Tools & Libraries to Enhance Forms

### **1. React Hook Form** *(Lightweight & Performant)*

```bash
npm install react-hook-form
```

**Example:**

```javascript
import { useForm } from 'react-hook-form';

function RHFForm() {
  const { register, handleSubmit, formState: { errors } } = useForm();

  const onSubmit = (data) => alert(JSON.stringify(data));

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register("name", { required: true })} placeholder="Name" />
      {errors.name && <span>This field is required</span>}
      <button type="submit">Submit</button>
    </form>
  );
}
```

### **2. Formik + Yup** *(Popular for Complex Forms)*

```bash
npm install formik yup
```

**Example:**

```javascript
import { Formik, Form, Field, ErrorMessage } from 'formik';
import * as Yup from 'yup';

const validationSchema = Yup.object({
  email: Yup.string().email("Invalid email").required("Required"),
});

function FormikForm() {
  return (
    <Formik
      initialValues={{ email: "" }}
      validationSchema={validationSchema}
      onSubmit={(values) => alert(JSON.stringify(values))}
    >
      <Form>
        <Field name="email" type="email" />
        <ErrorMessage name="email" component="div" />
        <button type="submit">Submit</button>
      </Form>
    </Formik>
  );
}
```

---

[⬅️ Back to Index](../index.md) | [➡️ Next: Context API](9-context-api.md)