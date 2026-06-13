## What is a _wrapper object_?

**A wrapper object is an object version of a primitive value.**

JavaScript has primitives:

- `number`
    
- `string`
    
- `boolean`
    
- `symbol`
    
- `bigint`
    

But objects can have:

- properties
    
- methods
    

So JavaScript sometimes **wraps a primitive inside an object** so it can behave like an object.

- To access the actual value inside the wrapper use `.valueOf()` method

---

## Example (very concrete)

```js
const x = 10;
```

`x` is a **primitive number**.  
Primitives normally **cannot have methods**.

But you can do this:

```js
x.toString();
```

🤯 How?

---

## The wrapper object in action

Behind the scenes, JavaScript does this **temporarily**:

```js
new Number(10).toString();
```

That `Number(10)` is a **Number wrapper object**.

So:

- `10` → wrapped as `Number { 10 }`
    
- Method runs
    
- Wrapper is immediately discarded
    

You never see this happening — JS does it for you.

---

## Wrapper objects created by `new Object(primitive)`

When you explicitly do:

```js
const a = new Object(10);
```

You are **forcing** the wrapper object to be created.

```js
typeof a;        // "object" a instanceof Number; // true
```

This is **not** the same as the primitive `10`.

---

## Types of wrapper objects

|Primitive|Wrapper Object|
|---|---|
|`number`|`Number`|
|`string`|`String`|
|`boolean`|`Boolean`|
|`symbol`|`Symbol`|
|`bigint`|`BigInt`|

Example:

```js
new Object("hi")  // String object new Object(true)  // Boolean object
```

---

## Why wrapper objects exist (in plain terms)

> Primitives are **lightweight values**, not objects.  
> Wrapper objects let primitives **borrow object behavior**.

That’s it.

---

## Why you should almost never create wrapper objects yourself 🚫

```js
const x = new Boolean(false);

if (x) {
  console.log("This runs 😬");
}

// To access the value of x

if (x.valueOf()) {
  console.log("This doesn't run 😩");
}
```

Why?

- Objects are always **truthy**
    
- Even `new Boolean(false)` is truthy
    

This causes **subtle bugs**.

---

## Key clarification related to your code

You mentioned:

```js
const objLiteral2 = new Object(objLiteral1);
```

⚠️ Important:

- `objLiteral1` is already an object
    
- So **no wrapper is created**
    
- The **same object reference** is returned
    

Wrapper objects happen **only when the value is primitive**.

---

## One-line mental model 🧠

> Wrapper objects are **object boxes around primitive values**, created automatically or explicitly so primitives can act like objects.




# `Number()` vs `new Number()` (Same idea for `Boolean` & `String`)

---

## 1. What `Number()` does ✅ (function call)

```js
const x = Number("10");
```

### What happens?

- Converts the value to a **primitive number**
    
- Returns a **number**, not an object
    

```js
typeof x; // "number"
```

### More examples

```js
Number(true);    // 1
Number(false);   // 0
Number("10");    // 10
Number("abc");   // NaN
```

### Key idea

> `Number()` = **type conversion (safe, common, recommended)**

---

## 2. What `new Number()` does ❌ (constructor)

```js
const x = new Number("10");
```

### What happens?

- Creates a **Number wrapper object**
    
- Wraps the primitive inside an object
    

```js
typeof x; // "object" 
x.valueOf(); // 10
```

### This is where bugs start 😬

```js
if (new Number(0)) {
  console.log("Runs!");
}
```

Why?

- Objects are always **truthy**
    
- Even if the wrapped value is `0`
    

---

## 3. Side-by-side comparison 🧠

|Code|Result|Type|Truthy?|
|---|---|---|---|
|`Number(0)`|`0`|number|❌|
|`new Number(0)`|`Number {0}`|object|✅|
|`Boolean(false)`|`false`|boolean|❌|
|`new Boolean(false)`|`Boolean {false}`|object|✅|
|`String("hi")`|`"hi"`|string|✅|
|`new String("hi")`|`String {"hi"}`|object|✅|

---

## 4. Why does `new Number()` even exist?

**Historical reasons**.

Early JavaScript needed:

- Object versions of primitives
    
- To attach methods like `.toString()`
    

Today:

- JavaScript **auto-boxes primitives**
    
- Wrapper constructors are almost never needed
    

---

## 5. Auto-boxing (the magic behind the scenes)

```js
const n = 10; 
n.toString(); // "10"
```

JS does this temporarily:

```js
new Number(10).toString();
```

Then throws the object away.

👉 You get methods **without** the problems.

---

## 6. Equality comparison trap ⚠️

```js
new Number(10) === 10; // false
new Number(10) == 10;  // true (coercion)
```

Reason:

- `===` compares type + value
    
- One is object, one is primitive
    

---

## 7. The golden rule ⭐

> **Never use `new Number()`, `new Boolean()`, or `new String()`**

Use:

```js
Number() Boolean() String()
```