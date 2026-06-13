
Think of a **JavaScript object** like a **living thing in your app’s memory**.

```js
const user = { name: "Alex", age: 25 };
```

This object:

- Only exists **while the app is running**
    
- Lives in the browser’s **working memory**
    
- Can contain things like:
    
    - Functions
        
    - References to other objects
        
    - Complex links the browser understands, but a file on disk does not
        

Now compare that to **storage** (`localStorage`).

---

### Storage is like writing on paper 📝

`localStorage` is like a **notebook** the browser keeps on disk.

Paper can only hold:

- Letters
    
- Numbers written as text
    

You **cannot put a “living object” on paper**.

So the browser says:

> “If you want to store something here, write it down as text.”

---

### Why objects don’t fit directly

An object isn’t just text. It’s more like:

- A bunch of boxes
    
- With arrows pointing to other boxes
    
- Some boxes contain instructions (functions)
    

When the browser shuts down:

- All those boxes and arrows disappear
    
- The notebook (storage) stays
    

The notebook has **no idea** how to rebuild those arrows unless you **explain them in text first**.

---

### That’s what `JSON.stringify` does

`JSON.stringify` is just:

> “Explain this object using plain text.”

```js
{ name: "Alex", age: 25 } 
↓ 
"{\"name\":\"Alex\",\"age\":25}"
```

Now it’s:

- Just letters
    
- Safe to store
    
- Easy to read back later
    

When you come back:

`JSON.parse(...)`

means:

> “Turn this written description back into an object.”

---

### Why the browser doesn’t do this automatically

Because it can’t guess:

- What parts of the object matter
- What to do with functions
- How to handle weird or complex objects

So **you decide**, not the browser.