## 1. Core difference (one-liner)

|Operator|Name|What it does|
|---|---|---|
|`==`|Loose equality|**Compares after type coercion**|
|`===`|Strict equality|**Compares without type coercion**|

👉 **Rule of thumb:**  
Use `===` unless you _explicitly_ want JavaScript’s coercion rules.

---

## 2. `===` (Strict Equality)

### Definition

`a === b` is `true` **only if**:

1. **Same type**
    
2. **Same value**
    

### Behavior

- No conversions
    
- Predictable
    
- Fast mental model
    

### Examples

```js
1 === 1           // true
1 === "1"         // false
true === 1        // false
null === null     // true
undefined === undefined // true
```

### Special cases

```js
NaN === NaN       // false ❗
+0 === -0         // true
```

> `NaN` is **never equal to anything**, including itself  
> (Use `Number.isNaN()` instead)

---

## 3. `==` (Loose Equality)

### Definition

`a == b` is `true` **after JavaScript tries to convert the operands to the same type**.

### High-level coercion algorithm (simplified but accurate)

1. If types are the same → compare values
    
2. `null` and `undefined` are **only equal to each other**
    
3. If one side is `string` and the other `number` → convert string to number
    
4. If one side is `boolean` → convert boolean to number
    
5. If one side is `object` → convert object to primitive (`valueOf` / `toString`)
    
6. Compare the results
    

---

## 4. The **important** `==` cases (memorize these)

### 🔹 `null` and `undefined`

```js
null == undefined     // true
null == 0             // false
undefined == 0        // false
```
✔️ This is the **only useful, intentional case** for `==`

---

### 🔹 Boolean coercion

```js
true == 1             // true
false == 0            // true
true == "1"           // true
false == ""           // true ❗
```

Why?

```js
false → 0
"" → 0
```

---

### 🔹 String ↔ Number

```js
"5" == 5              // true
" 5 " == 5            // true
"05" == 5             // true
```
---

### 🔹 Objects

```js
[] == ""              // true
[] == 0               // true
[0] == 0              // true
```

Why?

```js
[] → "" → 0
```

But:

```js
[] == []              // false ❗ (different references)
{} == {}              // false
```

---

### 🔹 `NaN`

```js
NaN == NaN            // false
NaN === NaN           // false
```

✔️ Always use:

```js
Number.isNaN(x)
```

---

### 🔹 Zero edge case

```js
+0 == -0              // true
+0 === -0             // true
```

---

## 5. Comparison summary table

|Expression|Result|
|---|---|
|`0 == false`|true|
|`0 === false`|false|
|`"0" == false`|true|
|`"0" === false`|false|
|`null == undefined`|true|
|`null === undefined`|false|
|`[] == false`|true|
|`[] === false`|false|

---

## 6. When (if ever) should you use `==`?

**Legitimate use case:**

```js
if (value == null) {
  // catches both null and undefined
}
```

**Everywhere else:** ❌ avoid

---

## 7. Best practice (industry standard)

```js
// ✅ Preferred
if (a === b) {}

// ❌ Avoid unless intentional
if (a == b) {}
```

Many codebases enforce:

```js
"eqeqeq": "error"
```

---

## 8. Mental model (easy to remember)

- `===` → **“Are these literally the same thing?”**
    
- `==` → **“Can JavaScript bend reality until these look the same?”**
    

If you want, I can also:

- draw a **coercion flowchart**
    
- explain **`Object.is()` vs `===`**
    
- show **interview trick questions**
    
- explain **why `[] == ![]` is true** 😈