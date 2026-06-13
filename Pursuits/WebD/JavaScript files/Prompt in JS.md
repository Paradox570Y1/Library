## 1️⃣ What is `prompt()` in JavaScript?

`prompt()` is a **built-in browser function** that shows a modal dialog asking the user for input.

```js
const name = prompt("What is your name?");
console.log(name);
```

### What the user sees

- A popup with:
    
    - A message
        
    - An input field
        
    - **OK** and **Cancel** buttons
        

### What it returns

| User action   | Returned value |
| ------------- | -------------- |
| Clicks OK     | A **string**   |
| Clicks Cancel | `null`         |

## 2️⃣ Syntax & Parameters

```js
prompt(message, defaultValue)
```

### Parameters

- **`message`** → text shown to the user
    
- **`defaultValue` (optional)** → pre-filled input
    

```js
prompt("Enter your age", "18");
```

⚠️ Even numbers come back as **strings**


## 3️⃣ Basic Usage Patterns

### ✅ Convert input to a number

```js
const age = Number(prompt("Enter your age"));
```

### ✅ Handle cancel safely

```js
const input = prompt("Enter username");

if (input === null) {
  console.log("User cancelled");
} else {
  console.log("Hello", input);
}
```

### ❌ Common beginner mistake

```js
prompt("Enter number") + 5  // string concatenation!
```

✔ Fix:

```js
Number(prompt("Enter number")) + 5
```