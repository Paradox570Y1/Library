JSON only knows how to write down **simple stuff**:

- text
    
- numbers
    
- true / false
    
- lists
    
- plain objects
    

If something doesn’t fit those rules, JSON just **ignores it or gives up**.

---

## 1️⃣ “JSON drops functions”

### Why?

A function is **instructions**, not data.

```js
const obj = {
  name: "Alex",
  sayHi() {
    console.log("hi");
  }
};
```

When you stringify:

```js
JSON.stringify(obj);
```

JSON thinks:

> “I don’t know how to write _behavior_ on paper.”

So it does this:

`{"name":"Alex"}`

👉 The function is **silently removed**.

**Simple reason:**  
You can’t store “do something later” as plain text data.

---

## 2️⃣ “JSON drops `undefined`”

### Why?

`undefined` basically means:

> “There is nothing here.”

```js
const obj = {
  a: 1,
  b: undefined
};
```

JSON’s reaction:

> “Why would I write down _nothing_?”

Result:

```js
{"a":1}
```

👉 `undefined` disappears.

(If it’s inside an array, it becomes `null` instead — still a placeholder.)

---

## 3️⃣ “JSON cannot represent circular references”

### What does that mean?

A circular reference is when something points back to itself:

```js
const obj = {};
obj.self = obj;
```

This is like writing:

> “This page refers to this page refers to this page refers to…”

JSON tries to write it down and goes:

> “I’ll never finish 😵”

So it **throws an error**.

```js
JSON.stringify(obj); // ❌ Error
```

![[Pasted image 20260208193632.png|400]]


**Simple reason:**  
You can’t fully describe an endless loop using plain text.

---

## One super-simple summary 🧠

JSON is like a form that only allows:

- simple values
    
- no actions
    
- no “nothing”
    
- no loops
    

Anything that doesn’t fit:

- gets **removed**
    
- or **breaks the process**