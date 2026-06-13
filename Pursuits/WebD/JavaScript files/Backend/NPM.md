# 🚀 **Why Do We Use NPM?** (Uses)

NPM helps with:
- Installing libraries
- Managing dependencies
- Running scripts
- Version control
- Publishing packages
- Handling local/global tools

### ✔ 1. **Install External Libraries**

For example, React, Express, Lodash, Axios, etc.

`npm install react`

### ✔ 2. **Manage Project Dependencies**

Tracks all libraries your project is using.

Stored in:  
`package.json` → main file for project dependencies  
`package-lock.json` → exact dependency versions

### ✔ 3. **Run Scripts**

You can run commands defined inside `package.json`.

Example:

```java
"scripts": {
  "start": "node app.js",
  "dev": "next dev"
}
```

Run using:
```bash
npm run dev
```

### ✔ 4. **Version Control**

Allows you to install specific library versions.

`npm install react@18.2.0`

### ✔ 5. **Publish Your Own Packages**

If you build a library, you can publish it on NPM.

`npm publish`



# Package.json
- It's the heart of your project.

It contains:

- Project name, version
- Dependencies (libraries you install)
- Dev dependencies
- Scripts
- Metadata (author, license)

Example snippet:
```json
{
  "name": "my-app",
  "version": "1.0.0",
  "dependencies": {
    "axios": "^1.2.0"
  },
  "devDependencies": {
    "nodemon": "^3.0.0"
  }
}
```


## 2️⃣ **package-lock.json**

Stores the **exact versions** of every library (including sub-dependencies).  
Ensures everyone on your team has the **same environment**.

You should **NEVER manually edit it**.

## 3️⃣ **Dependencies vs Dev Dependencies**

- **dependencies (`--save`)**
	Required **in production**  
	Examples: React, Express, Mongoose
	
	Install:
	
	`npm install express`
	
	Stored under `"dependencies"`.

- **devDependencies (`--save-dev`)**
	Required **only during development**  
	Examples: nodemon, eslint, jest
	
	Install:
	
	`npm install nodemon --save-dev`
	
	Stored under `"devDependencies"`.

|Command|Behavior Today|
|---|---|
|`npm install package`|Installs + saves to dependencies|
|`npm install package --save`|Same as above (redundant)|
|`npm install package --save-dev`|Saves to devDependencies|

## **node_modules folder**

Contains all installed libraries.

You **never upload this** to GitHub—  
instead you upload only `package.json` and `package-lock.json`.

- The Core Difference: Production vs. Development
	- The most important distinction is what happens in a **production** environment.
	
	- When you (or a hosting service) deploy your application, you typically run `npm install --production`. This command **ONLY** installs the packages listed in `dependencies` and **completely skips** everything in `devDependencies`.
	
	- Why? Because your live application doesn't need your test library (`jest`) or your code-formatting tool (`eslint`) to run. Omitting them makes your final application smaller, more secure, and faster to install.

To reinstall everything:
```bash
npm install --production //To install just dependencies needed for production

npm install //To install dependencies, dev dependencies, optionalDependencies etc.
```

## 5️⃣ **Semantic Versioning (SemVer)** → VERY IMPORTANT

Packages use a version pattern like:

`1.4.2 MAJOR.MINOR.PATCH`

Meaning:

- **MAJOR** → breaking changes
    
- **MINOR** → new features
    
- **PATCH** → bug fixes

Symbols you must know:

| Symbol   | Meaning                     |
| -------- | --------------------------- |
| `^1.4.2` | Allow MINOR & PATCH updates |
| `~1.4.2` | Allow only PATCH updates    |
| `1.4.2`  | Exact version               |

## 6️⃣ **Global vs Local Packages**

### **Local package**

Installed inside project → used only in that project.

`npm install next`

### **Global package**

Installed system-wide → used as CLI tools.

`npm install -g nodemon`


## 7️⃣ **NPM Scripts**

You can automate tasks.

Example:

```json
"scripts": {
  "start": "node server.js",
  "build": "next build",
  "test": "jest"
}
```
Run:

```bash
npm run build
```

Some default scripts have shortcuts:

```bash
npm start  // runs "start"
npm test   // runs "test"
```

## 8️⃣ **npx (Important)**

**npx = Node Package Executer**

Used for running commands **without installing them globally**.

Examples:

```bash
npx create-react-app myapp npx tailwindcss init
```

It makes sure you're always using the **latest version** of a tool.

[[npx vs npm]]
## 9️⃣ **Updating Packages**

```bash
npm update
npm update <package-name>
```

## 🔟 **Uninstalling Packages**

```bash
npm uninstall <package-name>
```

Removes it from `package.json` too.


# Bonus: How NPM Works Internally

When you run:

`npm install axios`

NPM:

1. Downloads from npm registry
2. Adds entry in `package.json`
3. Updates `package-lock.json`
4. Places library in `node_modules`