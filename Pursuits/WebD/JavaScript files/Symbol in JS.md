## What a `Symbol` really is

A **`Symbol` is a primitive, unique identifier**, not text.

```js
const s1 = Symbol("id");
const s2 = Symbol("id");

s1 === s2; // false ❗
```

If symbols were immutable strings, this would be `true`.  
But **every `Symbol()` call creates a brand-new unique value**.

---

## Why it feels like a string sometimes

`Symbol("id")`

- `"id"` is just a **description**
    
- It’s **only for debugging**
    
- It does **not affect equality**
    

`String(s1); // "Symbol(id)"`

That string is just a _representation_, not the symbol itself.

---

## Key differences: Symbol vs String

|Feature|`Symbol`|`String`|
|---|---|---|
|Type|Primitive|Primitive|
|Text data|❌ No|✅ Yes|
|Immutable|✅ Yes|✅ Yes|
|Unique|✅ Always|❌ No|
|Used as object key|✅ (non-colliding)|✅|
![[Pasted image 20260206133046.png|300]]
