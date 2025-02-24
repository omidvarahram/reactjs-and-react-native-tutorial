# Project Setup

[Back to Index](../index.md) | [⬅️ Back to Previous Page](1-introduction.md)

## Setting up with Create React App (CRA)

**Create React App (CRA)** is the most popular tool to bootstrap a new React project. It sets up everything you need for development with a sensible default configuration.

**Steps to Create a New Project:**

1. **Install CRA:**

```bash
npx create-react-app my-app
cd my-app
npm start
```

2. **Folder Structure Overview:**

```text
my-app/
├── node_modules/
├── public/
│   └── index.html
├── src/
│   ├── App.css
│   ├── App.js
│   ├── index.js
│   └── ...
├── package.json
└── README.md
```

3. **Run the App:**

```bash
npm start
```

Your app will be available at `http://localhost:3000/`.

---

## Vite + React for Faster Setup

**Vite** is a next-generation frontend tooling that offers faster builds and development experience compared to CRA.

**Steps to Create a Vite + React Project:**

1. **Initialize Project:**

```bash
npm create vite@latest my-vite-app -- --template react
cd my-vite-app
npm install
npm run dev
```

2. **Why Use Vite Over CRA?**
- Faster build times.
- Native ES module support.
- Hot module replacement (HMR).

---

## Project Structure Overview

While CRA and Vite provide a default structure, you can customize it for scalability:

```text
my-app/
├── public/
│   └── index.html
├── src/
│   ├── assets/
│   ├── components/
│   ├── pages/
│   ├── hooks/
│   ├── utils/
│   ├── App.js
│   └── index.js
├── .env
├── package.json
└── README.md
```

**Best Practices:**
- Group related components and utilities.
- Use `.env` files for environment variables.
- Use absolute imports with `jsconfig.json`:

```json
{
  "compilerOptions": {
    "baseUrl": "src"
  },
  "include": ["src"]
}
```

---

## Additional Setup

1. **Linting & Formatting:**
   - **ESLint:**

   ```bash
   npm install eslint --save-dev
   ```

   - **Prettier:**

   ```bash
   npm install prettier eslint-config-prettier --save-dev
   ```

2. **TypeScript Integration:**

   - In CRA:

   ```bash
   npx create-react-app my-app --template typescript
   ```

   - In Vite:

   ```bash
   npm create vite@latest my-vite-app -- --template react-ts
   ```

3. **Testing Libraries:**
   - **Jest** and **React Testing Library** are commonly used:

   ```bash
   npm install --save-dev jest @testing-library/react
   ```

---

[⬅️ Back to Index](../index.md) | [➡️ Next: Components in React](3-components.md)
