# 🚀 **What is `npx`?**

`npx` is a tool that **runs packages without installing them globally**.

Think of it as:

> “Run a package directly, even if it is _not installed_.”

---

# 🔥 **So what’s the actual difference?**

## ✅ **`npm install`**

- Installs packages (locally by default)
    
- Creates `node_modules/`
    
- Adds entry in `package.json` (npm v5+)
    
- Packages stay installed
    

Example:

`npm install create-react-app -g`

Now `create-react-app` is installed globally and stays until you uninstall it.

---

## 🚀 **`npx`**

- **Runs** a package **temporarily**
    
- Doesn’t keep it installed
    
- No pollution of global modules
    
- Always runs the latest version (unless installed locally)
    

Example:

`npx create-react-app myapp`

What happens?

- It downloads CRA temporarily
    
- Runs it
    
- Deletes it afterward  
    👉 No global install needed.
    

---

# Examples to Compare

### With `npm`

`npm install -g typescript tsc --version`

You must install it first.

### With `npx`

`npx tsc --version`

No install needed — runs it directly.

---

# ⭐ Why was `npx` created?

Because earlier people had to:

- install global packages (messy)
    
- update outdated global versions
    
- remove unused global packages manually
    

`npx` fixes all of this.

---

# 🧠 When to use npm vs npx?

|Task|Use|
|---|---|
|Install dependency for app|**npm install**|
|Install a global CLI for everyday use|**npm install -g**|
|Run a package once (e.g., create-react-app, parcel, typescript, jest)|**npx**|
|Run a local package without typing long path|**npx**|

---

# 📝 Summary in One Line

**npm installs packages.  
npx runs packages without installing them globally.**