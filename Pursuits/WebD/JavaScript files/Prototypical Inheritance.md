[[Null Bug]]
# What is `Object.prototype`?
In JavaScript, **every object has a hidden link to another object**, called its **prototype**.
`Object.prototype` is **the default prototype** for _most_ objects in JavaScript.

It’s just a normal JavaScript object that contains shared methods like:
```js
Object.prototype.toString
Object.prototype.hasOwnProperty
Object.prototype.valueOf
```

So when you do:
```js
const obj = {};
obj.toString();
```
`toString` is **not** inside `obj` itself — it comes from `Object.prototype`.


## 2️⃣ Where is this `Object`?

`Object` is a **built-in constructor function**, provided by the JavaScript engine.

```js
typeof Object; // "function"
```

Think of it as:

- `Object` → a function
    
- `Object.prototype` → an object used as a fallback for property lookup
    

```js
Object
  └── prototype (an object)
        ├── toString()
        ├── hasOwnProperty()
        └── ...
```

---

## 3️⃣ How is `Object.prototype` attached to an object literal `{}`?

When you write:

```js
const obj = {};
```

JavaScript secretly does something like:

```js
const obj = new Object();
```

And **during object creation**, the engine sets an internal slot:

```js
obj.[[Prototype]] = Object.prototype
```

You can _see_ this relationship using:

```js
let obj = {};
Object.getPrototypeOf(obj) === Object.prototype; // true
obj = new Number(19);
Object.getPrototypeOf(obj) === Object.prototype; // false
//wrapper objects don’t inherit directly from `Object.prototype` — they have _their own_ prototype in between.
// in case of Wrapper class
→ String.prototype
→ Object.prototype
→ null
// in case of normal object
→ Object.prototype
→ null
```

or (not recommended, but illustrative):

```js
obj.__proto__ === Object.prototype; // true
```

---

## 4️⃣ How property lookup actually works

When you access a property:

```js
obj.hasOwnProperty("x");
```

JavaScript checks in this order:

1. Does `obj` have `hasOwnProperty`?
    
2. ❌ No → check `obj.[[Prototype]]`
    
3. ✅ Found on `Object.prototype`
    

If not found there, it keeps going **up the prototype chain** until it reaches `null`.

Example:

```js
obj.foo
→ obj
→ Object.prototype
→ null
```

---

## 5️⃣ Why this design exists (the “aha” moment)

This is how JavaScript gets:

- **Memory efficiency** (methods shared, not copied)
    
- **Inheritance** without classes (historically)
    
- **Dynamic behavior** (you can modify prototypes at runtime)
    

Example:

```js
Object.prototype.sayHi = function () {
  return "hi";
};

({}).sayHi(); // "hi"
```

(⚠️ Powerful but dangerous — don’t do this in real apps.)

---

## 6️⃣ One-sentence mental model

> **Every object in JavaScript points to another object for missing properties, and `Object.prototype` is the default parent of plain objects created with `{}`.**



## Creating Objects Using `Object.create()`

### What is `Object.create()`?

```js
Object.create(proto)
```

It **creates a new object** whose **prototype** is `proto`.

⚠️ **It does NOT copy properties**  
It links the new object to another object via the **prototype chain**.

---

### Basic Example

```js
const original = {
  name: "Alex",
  age: 20
};

const copy = Object.create(original);
```

### What actually happened?

- `copy` is a **new object** ✅
    
- `copy` has **NO own properties**
    
- `original` becomes the **prototype** of `copy`
    

```js
console.log(copy.name); // "Alex"
```

👉 JS looks up `name` in:

1. `copy` → not found
    
2. prototype (`original`) → found
    

---

## This Is NOT a Real Copy 🚨

Let’s test it:

```js
console.log(copy.name); // "Alex"
```

Why?

- You created a **new property on `copy`**
    
- The original object is untouched
    

BUT…

```js
original.isActive = true;  
console.log(copy.isActive); // true 😬
```

Why?

- `copy` **depends on `original`**
    
- Changes to the prototype affect all derived objects
    

---

## Memory & Reference Reality

|Aspect|Result|
|---|---|
|New object created|✅|
|Independent copy|❌|
|Shares data via prototype|✅|
|Shallow copy|❌|
|Deep copy|❌|

👉 **This is inheritance, not copying**

---

## Visual Mental Model 🧠

```txt
copy  --->  original  --->  Object.prototype
```

- `copy` has a hidden `[[Prototype]]` link to `original`
    
- Properties are **read-through**, not duplicated
    

---

## When SHOULD You Use `Object.create()`?

✅ When you want **prototype-based inheritance**

Example:

```js
const userMethods = {
  login() {
    console.log("Logged in");
  }
};

const user1 = Object.create(userMethods);
user1.name = "Alex";
```

- `login()` is shared
    
- `name` is unique
    

💡 This is memory-efficient and intentional

---

## When You Should NOT Use It

🚫 When you want a **true copy**  
🚫 When you want **independent data**  
🚫 When modifying one object should NOT affect others

---

## Comparing All Copy Methods (Updated Table)

|Method|New Object?|Real Copy?|Notes|
|---|---|---|---|
|`obj2 = obj1`|❌|❌|Same reference|
|`new Object(obj)`|❌|❌|Same reference|
|`Object.create(obj)`|✅|❌|Prototype link|
|`Object.assign({}, obj)`|✅|✅ (shallow)|Copies props|
|`{ ...obj }`|✅|✅ (shallow)|Preferred|
|`JSON.parse(JSON.stringify())`|✅|✅ (deep-ish)|Limitations|


# `Object.create()` vs `class`

Both are used for **object creation + shared behavior**, but they work at different abstraction levels.

---

## Using `Object.create()` (Prototype-first)

```js
const userMethods = {
  login() {
    return `${this.name} logged in`;
  }
};

const user1 = Object.create(userMethods);
user1.name = "Alex";
```

### What’s happening?

- `userMethods` is the **prototype**
    
- `user1` has:
    
    - own property → `name`
        
    - shared method → `login`
        

```js
user1 → userMethods → Object.prototype
```

✅ Very explicit  
✅ Pure prototype-based  
❌ Less readable for many devs

---

## Using `class` (Syntax sugar)

```js
class User {
  constructor(name) {
    this.name = name;
  }

  login() {
    return `${this.name} logged in`;
  }
}

const user1 = new User("Alex");
```

### What’s happening internally?

⚠️ **Classes still use prototypes**

```js
user1 → User.prototype → Object.prototype
```

- `login()` lives on `User.prototype`
    
- Not copied per instance
    

---

## Comparison Table

|Feature|`Object.create()`|`class`|
|---|---|---|
|Uses prototype|✅|✅|
|Syntax|Low-level|High-level|
|Readability|Medium|High|
|Popular in modern JS|❌|✅|
|Constructor support|❌|✅|
|Best for|Manual inheritance|App-level code|

### Rule of Thumb 🧠

> Use `class` for **apps**  
> Use `Object.create()` to **understand JS deeply**



# `Object.create(null)` (VERY IMPORTANT EDGE CASE)

### What does this do?

```js
const obj = Object.create(null);
```

It creates an object with **NO prototype**.

---

## Normal object

```js
const obj = {};
```

```js
obj → Object.prototype
```

Has access to:

- `toString`
    
- `hasOwnProperty`
    
- `constructor`
    

---

## `Object.create(null)`

```js
obj → null
```

### Consequences 🚨

```js
obj.toString; // undefined ❌
obj.hasOwnProperty; // undefined ❌
```

---

## Why would anyone want this?

### 1. Pure dictionary / map

```js
const dict = Object.create(null);

dict.apple = "🍎";
dict["__proto__"] = "evil"; // SAFE ✅
```

With `{}` this would be dangerous.

---

### 2. No prototype pollution

- No inherited keys
    
- No collisions
    
- Cleaner key-value storage
    

---

## Downsides

❌ No built-in methods  
❌ Must use safe checks:

```js
Object.prototype.hasOwnProperty.call(dict, "apple");
```

---

## When to use it

|Use Case|Recommended|
|---|---|
|Data maps|✅|
|JSON-like data|❌|
|Normal objects|❌|

---

# 15. Prototype Lookup (Visual + Step-by-Step)

Let’s break this **slowly and clearly**.

---

## Setup

```js
const base = {
  greet() {
    return "Hello";
  }
};

const child = Object.create(base);
child.name = "Alex";
```

---

## Property Access: `child.greet()`

JS looks in this order 👇

1️⃣ `child`  
❌ not found

2️⃣ `base` (prototype)  
✅ found

3️⃣ stop searching

---

## Property Write: `child.greet = ...`

```js
child.greet = () => "Hi";
```

- JS **does NOT modify prototype**
    
- Creates a **new property on child**
    

```js
child
 ├─ name
 └─ greet   ← new
```

Prototype remains untouched.

---

## Prototype Shadowing ⚠️

```js
console.log(child.greet()); // "Hi"
```
- Child’s property **shadows** prototype property
    

---

## Deleting Properties

```js
delete child.greet;
console.log(child.greet()); // "Hello"
```

Why?

- Shadow removed
    
- Prototype lookup resumes
    

---

## Full Mental Model 🧠

```js
child
  ↓
base
  ↓
Object.prototype
  ↓
null
```

JS walks **upwards**, never sideways, never backwards.

---

# Final Golden Rules ✨

1. **`Object.create()` ≠ copy**
    
2. **Classes are prototypes in disguise**
    
3. **Writes never affect prototypes**
    
4. **`Object.create(null)` has no safety net**
    
5. **Property lookup walks the chain**