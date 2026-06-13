## 1. What is an Object in JavaScript?

An **object** is a collection of **key–value pairs** where:

- keys are strings (property names)
    
- values can be **any JS value** (number, string, boolean, function, another object, etc.)
    

```js
const user = {
  name: "Alex",
  age: 20,
  isActive: true
};
```

---

## 2. Object Literal (Most Common & Preferred Way)

### Definition

An **object literal** is created using `{}` directly.

### Example

```js
const objLiteral = {
  name: "name",
  age: 20,
  isActive: true,
  calculate: function () {
    return this.age * 2;
  }
};
```

### Key points

- Easiest and most readable way
    
- Creates a **new object in memory**
    
- Methods can access object properties using `this`
    

---

## 3. Creating Objects Using `new Object()`

### Example

```js
const objectUsingNew = new Object({
  name: "name1"
});
```

### Important clarification ⚠️

```js
new Object(value)
```

- If `value` is already an object → **returns the same object reference**
    
- It does **NOT clone** the object
- If the value passed is a primitive (number, string, boolean) or `null`/`undefined`, `new Object()` creates a new object; if the value is already an object, it returns the same object reference.
- In case of primitives it returns Wrapper Object

So this:

```js
new Object(existingObject)
```

❌ does **not** create a copy


#### If value is empty or null  or undefined
```js
new Object();
new Object(null);
new Object(undefined);
```

👉 **What happens**

- A **new empty object** is created
    

```js
`{}`
```

### Recommendation

🚫 Avoid `new Object()`  
✅ Use object literals `{}` instead

---

## 4. Object Methods and `this`

### Method inside object

```js
const obj = {
  age: 20,
  calculate() {
    return this.age * 2;
  }
};
```

### `this` keyword

- Refers to the **object that calls the method**
    
- Not the object where it is defined (important distinction)
    

---

## 5. Objects Are Stored by Reference (Very Important Concept)

### What does “by reference” mean?

Variables don’t store objects directly — they store a **reference (address)** to the object in memory.

---

## 6. Wrong Way to “Copy” an Object

```js
const objLiteral1 = {
  name: "name",
  age: 20
};

const objLiteral2 = objLiteral1; //objLiteral1 just stores the reference
```

### What actually happens?

- `objLiteral2` points to the **same object**
    
- No new object is created
    

```js
objLiteral2.age = 30;
console.log(objLiteral1.age); // 30 😱
```

### Why?

Because **both variables reference the same object**

---

## 7. `new Object(existingObject)` Is ALSO Wrong for Copying

```js
const objLiteral2 = new Object(objLiteral1);
```

### Reality

❌ Still the same reference  
❌ Still not a copy

---

## 8. Correct Way to Copy Objects (Shallow Copy)

### Using `Object.assign()`

```js
const objUsingAssign =
  Object.assign({ age: 20 }, objectUsingNew);
```

### How it works

```js
Object.assign(target, source)
```

- Copies properties from `source` to `target`
    
- Returns `target`
    
- Source is NOT modified
    

### Example

```js
const original = { name: "Alex" };
const copy = Object.assign({}, original);
```

✅ New object created  
✅ Different memory reference

---

## 9. Modern & Preferred Way: Spread Operator

```js
const copy = { ...original };
```

Why better?

- Cleaner syntax
    
- Easier to read
    
- Widely used
    

---

## 10. Shallow Copy vs Deep Copy (Missing but Important)

### Shallow Copy

- Copies only **top-level properties**
    
- Nested objects still share references
    

```js
const obj1 = {
  info: { age: 20 }
};

const obj2 = { ...obj1 };
obj2.info.age = 30;

console.log(obj1.info.age); // 30 ❌
```

---

### Deep Copy (Simple Way)

```js
const deepCopy = JSON.parse(JSON.stringify(obj));
```

⚠️ Limitations:

- Loses functions
    
- Loses `undefined`
    
- Breaks on circular references
    

---

## 11. Summary Table 🧠

| Concept           | Creates New Object? | Notes                  |
| ----------------- | ------------------- | ---------------------- |
| `{}`              | ✅                   | Best & simplest        |
| `new Object()`    | ⚠️                  | Avoid                  |
| `obj2 = obj1`     | ❌                   | Same reference         |
| `Object.assign()` | ✅                   | Shallow copy           |
| `{ ...obj }`      | ✅                   | Preferred shallow copy |
| JSON deep copy    | ✅                   | Has limitations        |

---

## 12. Final Mental Model (Very Important)

> Objects are **not copied** by default in JavaScript.  
> Variables point to **addresses**, not values.

Think of objects like **houses**:

- Variables are **addresses**
    
- Copying the address ≠ building a new house