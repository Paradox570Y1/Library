**Jest** is a **JavaScript testing framework**, and we install it as a **dev dependency**, it means:

---

# ✅ **What is Jest?**

**Jest** is a testing library created by **Facebook (Meta)** that is used to test JavaScript and React code.

It helps you:
- Write unit tests
- Test functions and components
- Mock APIs
- Check expected outputs
- Ensure your code works correctly
- Integration tests
- Mocking functions
- Testing APIs
- Testing React components


---

# 🧪 **Why is Jest installed as a _dev dependency_?**

Because **tests are only needed during development**, not in production.

Production (deployed build) does **not** need testing tools.  
So we install Jest like:

`npm install jest --save-dev`

This stores Jest under `"devDependencies"` in `package.json`.

### ✔ Dev dependency means:

Tools needed **only for developers**, not for the app to run.

Examples of dev dependencies:

- Jest (testing)
- ESLint (linting)
- Prettier (formatting)
- Babel (transpiling)
- Webpack (bundling)
- Nodemon (auto-restart server)
Your production code **does not depend on** these tools.

---

# 🛠 Example of how Jest is used

Test file: `sum.test.js`

```js
const sum = (a, b) => a + b;  
test("adds numbers correctly", () => {   
  expect(sum(2, 3)).toBe(5); 
});
```

Run Jest:

```bash
npm test
```

Jest will:

- Run the test
    
- Check the output
    
- Show pass/fail results
    

---

# 🎯 Summary

**Jest dev dependency** means:

- Jest is installed **only for development**
    
- It is used to **test JavaScript or React code**
    
- It is not required in production
    
- It helps maintain reliability and catch bugs