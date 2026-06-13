**JavaScript `Array.prototype.splice()`** 
## `splice()` syntax

```js
array.splice(start, deleteCount, item1, item2, ...)
```

### 1️⃣ `start` (required)

- Index where changes begin
    
- Can be **negative** (counts from the end)
    
```js
arr.splice(2)     // start at index 2
arr.splice(-1)    // start from last element
```

### 2️⃣ `deleteCount` (optional)

- Number of elements to remove
    
- If omitted → removes everything from `start` to end
    
- If `0` → removes nothing
    

```js
arr.splice(1, 2)  // remove 2 elements starting at index 1
```

### 3️⃣ `item1, item2, ...` (optional)

- Elements to **insert** at `start`
    
- Inserted in the order provided
    

```js
arr.splice(1, 0, "a", "b") // insert without deleting
```

---

## What `splice()` returns

👉 An **array of removed elements**

```js
const arr = [1, 2, 3, 4];
const removed = arr.splice(1, 2);

console.log(removed); // [2, 3]
console.log(arr);     // [1, 4]
```

---

## Common patterns (super useful)

### Replace elements

```js
arr.splice(1, 1, "x");
```

### Insert elements

```js
arr.splice(2, 0, "new");
```

### Remove elements

```js
arr.splice(0, 1);
```

### Clear an array

```js
arr.splice(0);
```

---

## `splice()` vs `slice()` (classic gotcha 😅)

|Method|Mutates array?|Purpose|
|---|---|---|
|`splice()`|✅ Yes|Add / remove / replace|
|`slice()`|❌ No|Copy part of array|

---

### TL;DR

- **`start`** → where to begin
    
- **`deleteCount`** → how many to remove
    
- **items** → what to insert
    
- **Mutates** the original array