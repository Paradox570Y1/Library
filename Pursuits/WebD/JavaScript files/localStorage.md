Objects are memory based
[[objects are not storage-friendly by default]]
## 1. `localStorage` is fundamentally a **string → string map**

Conceptually, `localStorage` is defined as:

```js
Map<string, string>
```

That’s it. No objects, no numbers, no booleans — **everything is text**.

```js
localStorage.setItem("count", 5); 
localStorage.getItem("count"); // "5" (string)
```

This is **intentional**, not a limitation of JavaScript itself.


## 2. Why strings specifically?

### ✅ **Interoperability**

The Web platform had to work across:

- Browsers
    
- Operating systems
    
- Programming languages
    
- Time (old data must still work years later)
    

Strings are the **lowest common denominator**:

- Easy to serialize
    
- Easy to persist
    
- Stable across environments
    
- Human-readable
    

Objects, on the other hand:

- Have references
    
- Can contain functions
    
- Can have circular structures
    
- Are runtime-specific
    

There is **no universal way** to store a live JS object safely.

---

## 3. Objects are runtime structures, not storage formats

A JavaScript object:

```js
{ a: 1, b: () => {} }
```

is:

- Memory-based
    
- Engine-specific
    
- Tied to execution context
    

Storage (like `localStorage`) is:

- Persistent
    
- Disk-backed
    
- Context-independent
    

So the browser _cannot_ just “store the object” — it must be **converted into data**.

That conversion step is called **serialization**.

---

## 4. Why JSON.stringify?

`JSON.stringify` is simply the **standard serialization format** chosen by developers:

```js
localStorage.setItem("user", JSON.stringify(user));
```

Why JSON?

- Text-based (fits `localStorage`)
    
- Language-agnostic
    
- Predictable
    
- Reversible (`JSON.parse`)
    

>**NOTE**
> JSON drops functions
   JSON drops `undefined`
   JSON cannot represent circular references
   [[JSON behavior]] 


Which again reinforces: [[objects are not storage-friendly by default]].

---

## 5. Why doesn’t `localStorage` stringify automatically?

Because that would be **dangerous and ambiguous**.

Imagine:

```js
localStorage.setItem("x", { a: 1 });
```

Questions the browser would have to answer:

- Should functions be kept?
    
- What about Dates?
    
- What about Maps, Sets?
    
- What about circular references?
    
- Which serialization format?
    

There is **no single correct answer**, so the browser:

> makes you choose explicitly

This is a design rule of the Web:  
👉 **Serialization must be explicit, not implicit**

---

## 6. Historical + performance reasons

A few more practical reasons:

- `localStorage` is **synchronous**
    
- Simple string storage is fast and predictable
    
- Designed _before_ modern JS data structures existed
    
- Meant for **small amounts of data** (config, flags, tokens)
    

For richer storage:

- `IndexedDB` (structured data, async)
    
- Cache API
    
- Cookies (also string-based!)