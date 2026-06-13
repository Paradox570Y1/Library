![[Pasted image 20250919202053.png]]

### Normal `.` operator

In JavaScript, the **dot (`.`) operator** lets us access or extend properties of an object:

```js
let user = { name: "Alex", address: { city: "Delhi" } };
console.log(user.address.city); // "Delhi"
```
But if the property in between is **`undefined` or `null`**, it crashes:

```js
let user = { name: "Alex" };
console.log(user.address.city); // ❌ TypeError

```

---

### Improvised Definition of `?.`

The **optional chaining operator (`?.`)** is like a _“safer dot (`.`)”_.  
It **extends the dot operator** by first checking if the object (or property) exists, and only then accessing the next property.

👉 If the reference is **`null` or `undefined`**, instead of throwing an error, it returns **`undefined`**.

---

### Example

```js
let user = { name: "Alex" };

// normal dot → throws error
// console.log(user.address.city); ❌

// optional chaining → safe access
console.log(user.address?.city); // ✅ undefined
```