This is one of **JavaScript’s most famous “historical bugs”**

## Short answer
- **`null` _is_ a primitive data type**
- **`typeof null === "object"` is a bug**
- It happened due to an **early design mistake** in JavaScript
- The bug was **never fixed** because it would break the web 🌍


```js
null  // primitive value meaning “no value”
```

It represents:

- Intentional absence of a value
- Empty reference
- “Nothing here (on purpose)”

## 1️⃣ What _is_ `null` in JavaScript?

`null` is a **primitive value** that means:

> “no object” / “intentional absence of any object value”

It is **not an object**, even though:

`typeof null === "object"; // 🤦 legacy bug`

That result exists for historical reasons and cannot be fixed.

---

## 2️⃣ Does `null` have a prototype?

**No. Absolutely none.**

```js
Object.getPrototypeOf(null);
// ❌ TypeError: Cannot convert undefined or null to object
```

Why? Because **only objects have prototypes**, and `null` is not an object.

---

## 3️⃣ Why does `null` matter for prototypes?

Because **`null` is the end of every prototype chain**.

Example:

```js
obj
→ Object.prototype
→ null   ← STOP HERE
```

When JavaScript looks up a property and reaches `null`, it stops and returns `undefined`.

That’s why this doesn’t crash:

```js
({}).foo; // undefined bcz lookup at least started
```

But this _does_ crash:

```js
null.foo; // ❌ TypeError
```

Because lookup can’t even start.

---

## 4️⃣ `Object.prototype`’s prototype is… `null`

This is crucial:

```js
Object.getPrototypeOf(Object.prototype) === null; // true
```

So the full picture:

```js
{}
→ Object.prototype
→ null
```

That’s the **entire universe** for plain objects.

---

## 5️⃣ Objects created with `Object.create(null)`

Here’s where `null` becomes _intentional_ and useful:

```js
const obj = Object.create(null);
```

Prototype chain:

```js
obj
→ null
```

So:

```js
obj.toString;        // undefined
obj.hasOwnProperty; // undefined
```

No inherited properties. Clean slate.

### Why would anyone want this?

- Dictionary / map objects
    
- Avoiding prototype pollution
    
- No name collisions (`__proto__`, `constructor`, etc.)
    

Example:

```js
const dict = Object.create(null);
dict.apple = 1;

"toString" in dict; // false ✅
```

---

## 6️⃣ Compare everything side by side 🧠

|Value|Has prototype?|Prototype|
|---|---|---|
|`{}`|✅|`Object.prototype`|
|`[]`|✅|`Array.prototype`|
|`new String()`|✅|`String.prototype`|
|`"hi"`|❌ (primitive)|none|
|`null`|❌|none|
|`Object.prototype`|✅|`null`|