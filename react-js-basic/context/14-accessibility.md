# Accessibility in React

[Back to Index](../index.md) | [⬅️ Back to Previous Page](13-performance.md) | [➡️ Next: Best Practices](15-best-practices.md)

## Introduction to Accessibility

**Accessibility (a11y)** ensures that web applications are usable by everyone, including people with disabilities. Building accessible React applications involves following best practices, adhering to WCAG (Web Content Accessibility Guidelines), and leveraging semantic HTML.

---

## ARIA Roles and Accessibility Standards

**ARIA (Accessible Rich Internet Applications)** roles help communicate the purpose of UI elements to assistive technologies.

### **1. Common ARIA Roles:**

- `role="button"` — Declares an element as a button.
- `role="dialog"` — Identifies modal dialogs.
- `role="alert"` — Announces dynamic alerts.

**Example:**

```javascript
<button aria-label="Close" onClick={handleClose}>X</button>
```

### **2. Accessibility Standards (WCAG):**

- **Perceivable:** Content must be available to all senses.
- **Operable:** Users can interact using a keyboard or assistive devices.
- **Understandable:** Clear navigation and readable text.
- **Robust:** Compatible with assistive technologies.

---

## Keyboard Navigation Support

Ensure users can navigate your app without a mouse.

### **1. Focus Management:**

- Use `tabIndex` to control focusable elements.
- Ensure interactive elements are keyboard accessible.

**Example:**

```javascript
<button tabIndex="0">Focusable Button</button>
```

### **2. Handling Keyboard Events:**

Implement keyboard shortcuts and key navigation.

```javascript
function handleKeyDown(event) {
  if (event.key === 'Enter') {
    console.log('Enter key pressed');
  }
}

<input type="text" onKeyDown={handleKeyDown} />
```

### **3. Skip Links:**

Allow users to skip repetitive content (e.g., navbars).

```javascript
<a href="#main-content" className="skip-link">Skip to Content</a>

<main id="main-content">
  <h1>Page Title</h1>
</main>
```

---

## Screen Reader Testing

Test your app with screen readers like **NVDA** (Windows) or **VoiceOver** (Mac).

### **1. Use Semantic HTML:**

Elements like `<header>`, `<nav>`, `<main>`, and `<footer>` enhance screen reader navigation.

### **2. ARIA Live Regions:**

Announce updates to users in real-time.

```javascript
<div aria-live="polite">You have 3 new notifications</div>
```

### **3. Announce Dynamic Content:**

For content that changes without a page reload, use ARIA attributes.

```javascript
<div role="status" aria-live="assertive">Form submitted successfully!</div>
```

---

## Testing Accessibility

### **1. Browser Extensions:**

- **axe DevTools** — Chrome extension for WCAG audits.
- **Wave** — Accessibility evaluation tool.

### **2. Automated Testing:**

Use **jest-axe** or **@testing-library/jest-dom** for accessibility testing.

```bash
npm install jest-axe @testing-library/jest-dom
```

**Example Test:**

```javascript
import { render } from '@testing-library/react';
import { axe } from 'jest-axe';

it('should have no accessibility violations', async () => {
  const { container } = render(<button>Click Me</button>);
  const results = await axe(container);
  expect(results).toHaveNoViolations();
});
```

---

## Best Practices for Accessibility

1. Use **semantic HTML** whenever possible.
2. Provide **alt text** for all images.
3. Ensure sufficient **color contrast** for readability.
4. Make interactive elements **keyboard-accessible**.
5. Test using **screen readers** and **keyboard-only navigation**.

---

[⬅️ Back to Index](../index.md) | [➡️ Next: Best Practices](15-best-practices.md)
