> [Documentation](https://nodejs.org/docs/latest-v18.x/api/index.html)

[[More about NodeJS]]
# Node REPL
*Full form:*
![[Pasted image 20250117150904.png|400]]

- It's not unique to node but used in many programming languages.
- It's basically an environment  (like the node runtime environment) where we can put user inputs in the form of code, what we write is read by the computer and evaluated line by line and prints back the result in the command line or console.
- We can create a server to deploy our project on it using nodeJS
> To initiate node REPL ->  Use command `node`
> then use `.help` to see some basic commands like `.exit` to exit the REPL or press `Ctrl+C` two times

- Now you can use JavaScript in the REPL just like you were using it on console in Browser.
- But now it's not in browser.

> To run a file written in JavaScript -> `node filename`


# Node Modules

**What are Native Node Modules**
- They are kind of like your starting tool set.
- You can install more modules but Native one are those which came pre bundled.
- You can learn about them from [documentation](https://nodejs.org/docs/latest-v18.x/api/index.html).


# File System
- It's the basic feature of the JavaScript.
- With Native JavaScript that is running on a browser, you can't access a user's files on your computer. But in the case of NodeJS, bcz it liberates the JavaScript out of the browser we are able to use it to access, read and write files on the server or in this case our local computer.

**What is file System?**
- It is the native node module that allows us to access Local Storage.
- To use we need to either import the code from filesystem module or we can require bits of code that we need from this module.

> NOTE 
> For now we are using common JS pattern (CJS) and later we will discuss ESM.


**What is CJS?**
- The full form of **CJS** is **CommonJS**.
- It is a module standard used in Node.js for managing dependencies and exporting/importing modules. CommonJS provides functionality to organize and reuse code effectively, especially in server-side JavaScript environments.
- For example, in CommonJS, modules are imported using `require` and exported using `module.exports`

```js
const fs = require("fs"); // to import file system module
```



# How to create a server and deploy your website

-  Create a folder called `server` within your website files.
- Now inside server folder run `npm init`
- Now create `index.js` in it.
- Now install express dependencies `npm install express`
- Now setup basic server code
![[Pasted image 20250726120059.png]]
- here using static files from public means , only the files inside public folder is accessible by express
	- Entry point is going to be `index.html` file.
	- Incase there is no `index.html` then it will give error
	![[Pasted image 20250726120809.png]]
	- Your `index.html` code will be deployed on the server on given port no.