## ✅ What is Prettier?

Prettier is an **automatic code formatter**.

> It **re-formats your code to follow a consistent style** — spacing, quotes, line breaks, indentation, etc. — **without changing how your code works**.

Think of Prettier as:

> **A robotic stylist for your code’s appearance.**

It _does not_ check logic or bugs — only **how the code looks**.

---

## 🎯 Where Is Prettier Used?

Prettier is used **during development** in almost every modern project:

### ✅ 1. Frontend Projects

- React
    
- Next.js
    
- Vue.js
    
- Angular
    

---

### ✅ 2. Backend Projects

- Node.js APIs
    
- Express servers
    
- Microservices
    

---

### ✅ 3. Code Editors (Live Formatting)

Most commonly with:

- Visual Studio Code
    

It auto-formats:

- On save
    
- On paste
    
- On command (`Format Document`)
    

---

### ✅ 4. Team & Company Codebases

Used in:

- Startups
    
- Product companies
    
- Open-source projects
    
- MNCs
    

So that **everyone’s code looks identical**.

---

## 🧠 What Exactly Does Prettier Fix?

### ❌ Messy Code

```js
function add(a,b){return a+b}
```

### ✅ After Prettier

```js
function add(a, b) {
  return a + b;
}
```

---

### ❌ Inconsistent Quotes

```js
const name = "Aman"
const city = 'Delhi'
```

### ✅ After Prettier

```js
const name = "Aman";
const city = "Delhi";
```

---

### ❌ Ugly JSX

```jsx
<div><h1>Hello</h1><p>World</p></div>
```

### ✅ After Prettier

```jsx
<div>
  <h1>Hello</h1>
  <p>World</p>
</div>
```

---

## ⚙️ How Prettier Is Used in a Project

### ✅ Install

```bash
npm install --save-dev prettier
```

---

### ✅ Format a File Manually

```bash
npx prettier app.js --write
```

---

### ✅ Format Everything

```bash
npx prettier . --write
```

---

### ✅ Prettier Config File

Create:

`.prettierrc`

Example:

```json
{
  "semi": true,
  "singleQuote": false,
  "tabWidth": 2
}
```

---

## 🧩 Prettier vs ESLint (Important Difference)

|Feature|Prettier|ESLint|
|---|---|---|
|Purpose|Format code|Find bugs + enforce rules|
|Handles logic errors|❌ No|✅ Yes|
|Handles spacing/style|✅ Yes|✅ Some|
|Auto-fixes layout|✅ Always|✅ Sometimes|
|Breaks build on error|❌ No|✅ Yes (CI)|

👉 **Best industry setup:**

> ✅ Prettier + ✅ ESLint together

- ESLint → “Is this code _correct_?”
    
- Prettier → “Is this code _beautiful & consistent_?”
    

---

## ✅ What Languages Prettier Supports

Prettier formats:

- JavaScript
    
- TypeScript
    
- JSON
    
- HTML
    
- CSS
    
- SCSS
    
- JSX
    
- Markdown
    
- YAML
    

All with **one consistent style engine**.

---

## 🚫 What Prettier is NOT

- ❌ Not a linter
    
- ❌ Not a test tool
    
- ❌ Not a compiler
    
- ❌ Not a bundler
    

It only **formats code**.

---

## 🎯 Real-Life Example Workflow (How Devs Actually Use It)

1. You write messy code
    
2. You press **Ctrl + S**
    
3. Prettier auto-formats
    
4. ESLint checks for bugs
    
5. Git commit stays clean ✅
    

This is **standard professional workflow**.

---

## ✅ One-Line Interview Definition

> **Prettier is an opinionated code formatter used to automatically format code for consistent style across a project.**

---

## 🧠 Memory Trick

- **Compiler** → runs code
    
- **Jest** → tests code
    
- **ESLint** → judges code
    
- **Prettier** → beautifies code ✨