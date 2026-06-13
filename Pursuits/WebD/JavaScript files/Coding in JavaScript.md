### JavaScript
 - Javascript is a scripting language i.e. whenever we push a request from client to server side or vice-versa. Other examples for scripting languages are Javascript, ruby, asp.net etc.
 - JavaScript combines features from **multiple programming paradigms** which inculcates the concepts of procedural programming, Object Oriented programming, functional programming and in browsers it is event driven as well.
[[How JS works]]
 - JavaScript as a language is implemented by Browser. So whatever you write like var x = 9 , it done by Browser.
- Modern day browsers have in-built servers to run javascript code.
- JS has two versions i.e. ES5, ES6. 
	- ECMAScript just defines the rules of javascript and is not a language . It is a specification of java script language.
	- So JS can be implemented by any browser but they are standardized by ECMAScript.
- Two ways to apply JS: Internal, External,
- Three ways of variable: Var, const, let
- Difference b/w let & var
	1. ES5 has only var while ES6 has both let and var.
	2. Scope difference between var and let.
	3. Difference in window.
	4. Const values are unchangeable while var values can be modified
- JavaScript is single threaded language (at one time it can run only one process).
	- So can we do multi threading in JavaScript language ? Like can we do multiple executions in it as a language?
		- Browser helps JavaScript to achieve multi-threading. So , JavaScript can't do multi-threading by itself but Browser can provide environment to run multiple processes at single time.

---
![](https://img-c.udemycdn.com/user/50x50/67545528_5f4b_3.jpg)

### DO THESE AFTER FINISHING THE COURSE ✅


I completed this course a few months ago and wanted to share some essential steps to take after finishing it.

Firstly, thanks to Angela for her excellent teaching. This is the best online bootcamp to get started with Web Development. However, there were a few things that were not covered in depth.

  

**React Class Components**:

Learn about React Class Components alongside Functional Components. The course did not cover class components in depth.

**Additional React Hooks:**

Explore other React hooks that were not included in the bootcamp - [https://react.dev/reference/react/hooks](https://react.dev/reference/react/hooks)

**State Management**:

State management with Redux or Context API is must to know (for making big projects).

**API Handling with Axios**:

Get proficient with Axios for handling API requests in React.

**React Routing**:

Understand React routing, similar to how we used Express for routing in projects.

**Build a Static Project**:

The next step will be to make one simple static project on your own with React Class or functional Components as per need without using any databases like MongoDB to have better understanding and check what you have learnt.

**MERN Project**:

As we built a TODO application with Mongo, Express, and EJS, try creating a MERN (MongoDB, Express, React, Node.js) project. It has a different folder structure compared to a simple React application.

**Internships/Jobs**:

After completing the React portion, start applying for React or Web development internships/jobs. Gaining practical experience is invaluable.

**Open Source Contribution**:

Participate in open-source projects and programs like [GSoC](https://summerofcode.withgoogle.com/), [LFX Mentorship](https://mentorship.lfx.linuxfoundation.org/). It boosts confidence and gives a sense of accomplishment.

  

So one common mistake to prevent is to fall in the tutorial hell loop.

Don't try to fall in this loop of learning without implementing, the correct procedure which to follow should be to learn a technology, make a project, git it, deploy it, share it with your friends-family anyone you want and add to your portfolio. This will surely keep your interest in development and help you keep moving, learning further!

---
# History

> Browser of 90's => [Netscape Navigator](https://en.wikipedia.org/wiki/Netscape_Navigator)

![[Pasted image 20241209113937.png|400]]
Above are the companies that `Andreessen Horowitz` invested who was also one of the principle maker of Netscape Navigator.
![[Pasted image 20241209114331.png|300]]

##### During 1990's
 At this point in time, HTML websites were all form and no function,
 and when a website did in fact need some functionality such as retrieving a piece of data that you searched for, or just calculating something, the website had to send that request to the data server, and it was in the data server where all of this computation and business logic happened and then it would return the web page that contained the new data.                                                                                          
 Now the team at Netscape wanted something a little bit different, they envisioned a future where the web was more dynamic, with animations and real-time user interaction. And in order to enable this you needed to take away the server
 and have the code be able to run on the browser. So in order to do this they wanted to create a small scripting language.
 The requirements were that this language had to be simple and
 had to be really easy so that even non-developers and non-programmers could use it to add functionality to websites.
 So they contacted `Branden Eich` to create that programming language. And as internet history and internet lore goes, Brendan proceeded to sit down with the team, and while there were other people who tried to lose a guy in 10 days,
 Brendan was able to create JavaScript in 10 days. And now we can't even imagine what the world would look like without JavaScript.
- When it was invented it was called LiveScript.
- People at Microsoft tried to reverse Engineer that program and called it JScript
- So there was lot confusion about names of Javascript . So, European's Standardized and called it ECMAScript (European Computer Manufacturers Association Script). 

> You can even disable Javascript in your browser and load websites without javascript  . Search for content settings and disable JS.

## Any Relationship between JAVA and JavaScript?

Java and JavaScript have as much in common as car and carpet. The only reason why we call it JavaScript was bcz in 90s the word Java was about as hot as the world blockchain in today's world.

There are major differences between them like JavaScript is an interpreted programming language whereas Java is a compiled programming language.
![[Pasted image 20241209121536.png|400]]

The distinction between **interpreted** and **compiled** languages lies in how the source code is converted into machine-readable code and executed. Here's a breakdown:

### 1. **Interpreted Languages**

- **Execution Process**:  
    The source code is executed line by line by an interpreter at runtime. No intermediate machine code is generated beforehand.
- **Speed**:  
    Slower execution since the interpretation happens at runtime.
- **Platform Dependency**:  
    Typically platform-independent as the interpreter handles platform-specific details.
- **Error Handling**:  
    Errors are detected and reported line-by-line during execution, making debugging more straightforward.
- **Examples**:  
    Python, JavaScript (by itself), Ruby, PHP.

### 2. **Compiled Languages**

- **Execution Process**:  
    The source code is converted into machine code (binary format) by a compiler before execution. This machine code is then executed by the CPU.
- **Speed**:  
    Faster execution because the program is precompiled into optimized machine code.
- **Platform Dependency**:  
    Platform-dependent, as the compiled machine code often works for a specific architecture or operating system.
- **Error Handling**:  
    Errors are caught during the compilation process, which means the program must be error-free before it runs.
- **Examples**:  
    C, C++, Rust, Go.

### **Key Differences at a Glance**

| Aspect             | Interpreted Language    | Compiled Language             |
| ------------------ | ----------------------- | ----------------------------- |
| **Execution**      | Line-by-line at runtime | Precompiled into machine code |
| **Speed**          | Slower                  | Faster                        |
| **Error Handling** | At runtime              | At compile-time               |
| **Portability**    | Platform-independent    | Often platform-dependent      |
| **Examples**       | Python, JavaScript      | C, C++                        |

### Hybrid Example:

Languages like **Java** and **C#** use both approaches. Java code is compiled into bytecode (intermediate code and it's not a machine code) and then interpreted or executed by the JVM (Java Virtual Machine).
![[Pasted image 20260206124221.png|300]]
![[Pasted image 20260206124253.png|300]]

![[Pasted image 20260206124400.png|300]]


> Earlier JavaScript was only used for animation, functionality but now days due to its frameworks it can be used in both frontend and backend.

>Language Rankings  - [Redmonk](https://redmonk.com/sogrady/2024/09/12/language-rankings-6-24/)


---
# About Javascript console in Chrome

- Use Ctrl+ Shift+ J to open javascript console in chrome.
- In this console you can give single line instruction , but in case you want to give multi line instruction hold shift while pressing enter to move to next line.

To write javascript in browser , without need to hold shift open snippets
![[Pasted image 20241210100239.png|200]]
- here you can create your own js file 

>console remembers the assigned values and variables even if you clear it using `Ctrl+L`.  

> To clear the console data , right click on the reload or select 'Emty cache and Hard reload'

[[Types of Reload in browser]]

>Resources of JS : [mdn_docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript)   [javascript.info](https://javascript.info/) 
  [Principles of Writing  JavaScript](https://github.com/rwaldron/idiomatic.js) 
 [udemy_outdated_lessons](https://appbrewery.com/p/legacy-complete-web-development-course/)


### Data Types

#### Primitive Data Type
1. string
	- to get no. of characters in a string use `str.length`.
	- Text data
	- Can use single, double, or backticks
```js
let name = "JavaScript";
let msg = `Hello`;
```

2. number
	- Integers and floating-point numbers
	- Includes `Infinity`, `-Infinity`, `NaN`
```js
let a = 10;
let b = 3.14;
let c = NaN;
```

3. boolean

```js
let isReady = true;
let isDone = false;
```

4. symbol
	- Unique and immutable identifiers
	- Often used as object keys
[[Symbol in JS]]
```js
let id = Symbol("id");
```

5. undefined
	- Variable declared but **not assigned**
```js
let x;
console.log(x); // undefined
```

6. null
	- Intentional absence of value
[[Null Bug]]
```js
let y = null;
typeof null; // "object" (this is a bug in JS) 
```

7. bigint
	- for very large number beyond integer limits
```js
let big = 123456789012345678901234567890n;
```
#### Non Primitive Data Type
1. object
[[Objects in JS]]
To check data type use  `typeof()` keyword


# Useful Functions

[[Equality in JS]]
- `prompt()` - similar to alert but also takes input from user.
	- We can even store input from prompt in a variable.
	- If we are on a console after taking inputs we can remove the input code, and still use already taken input, as  console remembers the assigned values and variables. 
[[Prompt in JS]]
- `toUpperCase()/toLowerCase()`:
	![[Pasted image 20241210111434.png|200]]
	- returns new string which immutable and you must store result in case you want to use it.
	- JavaScript strings **cannot be changed in place**.
##### ❌ Non-letters are untouched

```js
"123!@#".toUpperCase(); // "123!@#" 
"Hi 123!".toLowerCase(); // "hi 123!"
```

##### ❌ Numbers, spaces, symbols stay the same

```js
"JS 101 🚀".toUpperCase(); // "JS 101 🚀"
```

- `slice`
		- ![[Pasted image 20241210110536.png|150]]
		- ![[Pasted image 20241210110559.png|80]]
		- ![[Pasted image 20241210111206.png|300]]
		- To capitalize only 1st letter of a word.
		- ![[Pasted image 20241210113411.png]]
[[Slice in JS]]
[[Splice in JS]]
- `Math.floor()` -> to round the number to smaller value.
- `Math.round()`-> to round the number to nearest number.
- `Math.random()` -> to generate a number between 0 and 0.9999999999999999 and have 16 digits decimal places.
	- we multiply it with the desired range of numbers we want , suppose i want of a random dice number i will multiply it by 6
		![[Pasted image 20241211000935.png|150]]
	 It will give number between 0 - 0.5999999999999999
	 ![[Pasted image 20241211001108.png|150]]
	 we get range between 0-5
	 ![[Pasted image 20241211001137.png|150]]
	 we get range between 1-6


# Comparators

![[Pasted image 20241211002400.png|350]]


# Does everything in JavaScript is an Object.
- JavaScript is scripting language and Object oriented language.
- Even basic variables have properties attach to it like var x = 5, now check in console what properties can be used on variable x.

# Optional Chaining Operator

- In place of `.` we can use optional chaining operator `?.` in Java Script.
- **Optional chaining (`?.`) cannot be used on the left-hand side of an assignment**. It’s designed **only for reading**, not writing.
- Use: 
	- It can be used for reading data.
	- It can be used while make method call from an object but not at the left hand side of assignment operator.
![[Pasted image 20250719111445.png]]
![[Pasted image 20260209184736.png|300]]


- It gives compile time error. As ? signifies that it could be null so browser automatically throws compile time error.
- If we don'tuse optional chaining then it will throw runtime error while assigning value to null.
*Instead you can handle it like this*
![[Pasted image 20250719113305.png]]
- Optional chaining is valid in method calls
![[Pasted image 20250719111512.png]]
![[Pasted image 20250719111529.png]]



# Blocking vs Non Blocking Mode
- In blocking mode , code is executed and then moves to next line.
- In Non blocking mode, code is executed after some time. Example: defer.

[[Blocking vs Non Blocking]]
# Using defer
[[defer in JS]]
- It's non-blocking mode
![[Pasted image 20250719105821.png|400]]
![[Pasted image 20250719105841.png|500]]
To prevent one way is to place at end of body or  another way is to download it first and execute it later by making use of `defer` .
![[Pasted image 20250719110029.png|400]]

>NOTE
>If we don't use defer then by default  script tag is blocking in nature so it will execute the script file on sight then move forward.
# Async
- It's non-blocking mode
- To increase the performance like executing when it's downloaded instead of waiting to parse whole html file.
- It is done if no DOM manipulation is involved.
- You can use intersection observer to inform when the file is executed
# Defer vs Async mode
- Downloads file in parallel thread like async but defer executes that file at the end whereas in case of async the file gets executed after it's downloading is finished which could be in middle of the body. 


# Template literal
- Use backtick to contain multi line string.


# Mapping in JS

- Mapping is heavily used in JavaScript.
Syntax: `productList.map(func)`
- Now `func` will be applied to each element of `productList` array.
- A map method just returns an array.
- Whenever browser tries to render an array it renders it as a String, so array is automatically converted to String.

# Execution in Java
- Files is just logical separation for developer point of view . There is no separation of files in javascript Runtime.
- In react components are just reusable part of UI.



# Sources tab
- In sources tab you can see execution of each line of code


# Inbuilt debugger

- Just select line to debug.
- Pause it if needed and refresh the page.

![[Pasted image 20250802123317.png]]

- After refreshing you can see the data received or sent by the function on hovering
![[Pasted image 20250802123415.png]]


- If you are not sure about what line to 

# Web Vitals
- It generates the performance report
![[Pasted image 20250802123805.png]]

![[Pasted image 20250802123846.png]]

- Try that layout shift is 0 or kept minimum
![[Pasted image 20250802123931.png]]


# Throttling
- Browser has the capability for throttle to request
- What is throttling on browser?

# Browser features
- Debugging tools
- Browser Web API (Application Programmable Interface)
	- It is a method and function which are exposed to do real world things. They are more generic and at higher level than functions.
	- Not all browser API is asynchronous
	- It is decided by browser if it needs to be executed in stack or in another space which is mostly in case of asynchronous task.
	- Example
		- Save Data API
			- Create a storage / file
			- Open the storage in write mode
			- Insert Data
			- Close file
		- Set Timeout API
			- It's a browser API which sits on top of JavaScript , but not actually a part of JavaScript.
			- Usually asynchronous functionality are not part of JavaScript.
			![[Pasted image 20250807202308.png]]
		- Application Tab
			- It is a Browser API
			- It is the application itself, doesn't matter you open multiple windows.
			- In terms of storage:
			- Cookie - User sessions.
				- Cookie is not meant to be used as storage but used for session management.
				- It is used to manage the state of user. 
				- HTTP is a stateless protocol so every request by a client is independent of each other.
				- So if same client makes multiple request so for backend to identifies a user it checks the cookie which is appended with the request to identify the user
				- Now days cookie are used less but used in third party login like after you login in gmail , it remains logged in for some time.
				- Inside cookie anything could be stored even JWT.
				- It is one way to mimics behavior of stateful protocol while still using stateless protocol.
				- Advantage of cookie is that browser by defaults append it.
				- Azure Directory ID , Clerk , Auth uses cookie
				- You can set who can use your cookie.
				![[Pasted image 20250807203231.png]]
			- Index DB - Frontend DB
				- It is a browser level database which very efficient.
				- Why frontend needs DB.
					- Sometimes we have to save data like while filling form for assurance but due to network issue you might not able to send that but it can be stored as draft offline using DB.
				- Used less frequently.
				- Can be used by any application.
			- Web Storage
				- This is the modern way to replace cookie.
				- It comprises of:
					- local storage - shared for entire browser for a particular domain(means particular website only)
						`localStorage.clear();` to clear storage
						![[Pasted image 20250807205422.png]]
						- Whatever we store in local storage is stored as string.
					- session storage - saved for particular tab of browser
				- local and session storage are nothing but key value pair.
				- `key` can only be string
			- Fetch API
			- navigator
				
	- Since Browser is client only , so `Browser API` are also called `Client API`.

# Event Loop
- It is completely managed by the browser.
- It does not work like NodeJS.
- When ever we talk about event loop it is browser event loop.
- Using it we can give delay.
- 
![[Pasted image 20250807213454.png]]
- When stack becomes stack
- Then micro tasks which are small high priority tasks are executed.
- After that tasks are executed.
- Micro task
	- It involves callback function like promises callback.
	- Then there is Queue micro task , which is used to create custom micro task and that is of high priority micro task so that is not executed in the stack. 
	- These are used like to access particular data from the database.
	- Execution moves to macro task only after micro tasks are executed or we can say micro task queue is cleaned.
	- There could be nested micro task as well.
	- Developers handle that only few micro tasks are 
- Macro task
	- DOM Events are put in callback and sent to callback queue. It takes function as parameter.

```js
console.log('A');

setTimeout(() => {
  console.log('B');
  Promise.resolve().then(() => {
    console.log('C');
  });
}, 0);

Promise.resolve().then(() => {
  console.log('D');
  setTimeout(() => {
    console.log('E');
  }, 0);
});
// A D B C E (ouput)
```

- Stack is executed before tasks queue.
```js
console.log("A");

setTimeout(() => {
  console.log("B");
}, 0);

Promise.resolve().then(() => {
  console.log("C");
});
console.log("D");
// A D C B (output)
```
- `Libuv` is a library which helps JavaScript achieve multi threading.
	- It is used to create OS level threads with NodeJS.
- If we have to do intensive threading then use Java.
- In browser all data is stored on Heap. There is not much data on browser so it doesn't require any complex data structure.

# var vs let

- let was introduces to prevent data leakage that happens during hoisting.
- Hoisting means moving the declaration to the top of the scope which can be functional scope or block scope.
- There are two types of scope at high level in terms of hoisting:
	- `Functional Scope`- created by function
	- `Block Scope` - Created by {} curly braces  (e.g., if else , for , while)
- Hoisting applies to var, function, let, const, class, import.
- `var hoisting:` Move the var declaration to the top of the innermost function.
- `let hoisting:` Move the let declaration to the top of the innermost block scope.
	- let was introduced to prevent hoisting , restrict the scope.
- Every function scope is block scope but vice versa is not true.

![[Pasted image 20250814205806.png|350]]
- here x is undefined as when it is hoisted above it was defined with `undefined` value as default means `var x;`
 

![[Pasted image 20250814205837.png|350]]

![[Pasted image 20250814210440.png]]
- let can only be used if it is declared and defined with some value.
- So they put restrictions on let so that developer has to fix the code to continue building project further otherwise in case of var developer just used to leave the code as it is where var value remains undefined instead of throwing any error like in let.
![[Pasted image 20250814210253.png]]
- JavaScript doesn't started as programming language but just as scripting language therefore var was defined such that it can be accessed anywhere. But when we needed programming behavior in it then let was introduced.

![[Pasted image 20250814213050.png|400]]


# Function expression

- General way is function declaration
	![[Pasted image 20250814213249.png|200]]
- But functional expression defines function by using let or var keyword.
	![[Pasted image 20250814213339.png|200]]
	- So this introduce function hoisting.

![[Pasted image 20250814213653.png|400]]

#### Using let inside function
![[Pasted image 20250814213848.png|400]]
- Here since function scope and block scope is same, so let became function scope instead of block scoped.
- When entering the scope, `fool` is in **Temporal Dead Zone (TDZ)** from the start of the block until the `let` statement is executed.
- At `fool();` → variable **exists** in scope but **cannot be accessed yet** (because TDZ hasn’t ended).
- This throws **ReferenceError** before it even tries to call it.

#### Using var inside function
![[Pasted image 20250814214404.png]]
- fool(); // tries to run undefined as a function
- When JavaScript parses the function, **`var fool` is hoisted** to the top of the function scope.
- However, only the **declaration** is hoisted — not the **assignment**.
- So, during the execution of `fool();` (before the assignment happens), `fool` exists but is **`undefined`**.
![[Pasted image 20250814215200.png]]


# Difference in global scope and function scope in case of let

![[Pasted image 20250814215940.png]]

### Another scenario in above context
- Now lets take the global scope scenario , it throws different error in case of different environment like in case of NodeJS it throws Cannot access before initialization but in case of Browser console it throws not defined.
![[Pasted image 20250814220153.png]]

###### Why **different errors**?

###### **In Node.js**
- Top-level code is wrapped inside a **CommonJS module scope** (not the true global scope).
- `let fooL` becomes a block-scoped variable **inside the module**.
- When you try to use it before its declaration:
    - Node sees the variable exists in scope but hasn’t been initialized yet.
    - Throws:
        `ReferenceError: Cannot access 'fooL' before initialization`
    This is the **correct TDZ error** according to the ECMAScript spec.

###### **In Browser Console**
- Each line you type in the `DevTools` console runs in a **special REPL-like environment**, not as one continuous script.
- If you paste the whole snippet:
    - In browsers, global `let` variables **don’t attach to `window`**.
    - When you call `fooL()` before the declaration, the browser **sometimes treats it as not yet declared at all** depending on how the snippet is evaluated.
    - That’s why you may see:
        `ReferenceError: fooL is not defined`
    —meaning no binding has even been created in that evaluation context yet.