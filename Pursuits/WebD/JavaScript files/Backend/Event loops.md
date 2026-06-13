# 14/08/25

<aside>
💡

### Event- Loop Queues:

Alright — let’s go through **event loop queues** step-by-step, focusing on the two main categories you mentioned: **Callback/Task queue** and **Microtask queue**.

We’ll take the example of **JavaScript** in the browser, but the concept applies (with slight differences) to Node.js and other event-loop-based runtimes too.

---

## 1. **The Event Loop at a Glance**

The **event loop** is like a traffic controller for your program:

- There’s **only one main thread** (in JS).
- Work gets divided into **tasks** (macro-tasks) and **micro-tasks**. Now all these ***tasks are asynchronous*** in nature.
- The event loop decides what to run **next** depending on which queue the work is in.

---

## 2. **Two Main Queues**

### **A. Callback Queue / Task Queue / Macrotask Queue**

- **When used:** For things like `setTimeout`, `setInterval`, DOM events, HTTP requests, etc.
- **Execution timing:** Runs **after** the current call stack finishes, and **after all microtasks** are done.
- **Examples in browser JS:**
    
    ```jsx
    setTimeout(() => console.log("Macrotask"), 0);
    setInterval(() => console.log("Interval task"), 1000);
    document.addEventListener("click", () => console.log("Click task"));
    
    ```
    
- Each entry here is called a **macrotask**.
- The event loop will take **one macrotask at a time**, run it, then empty all microtasks before picking the next macrotask.

---

### **B. Microtask Queue**

- **When used:** For **high-priority, lightweight** follow-up jobs like `Promise.then()`, `queueMicrotask()`, and `MutationObserver`.
- **Execution timing:** Runs **immediately after the current call stack** finishes, **before** the event loop picks another macrotask.
- **Examples:**
    
    ```jsx
    Promise.resolve().then(() => console.log("Microtask"));
    queueMicrotask(() => console.log("Microtask via queueMicrotask"));
    
    ```
    
- Microtasks are great for quick updates that must happen **as soon as possible**, but not in the middle of running a current function.

---

## 3. **Order of Execution**

**In each iteration (or "tick") of the event loop**:

1. **Run one macro-task** (from the task/callback queue).
2. **Run all micro-tasks** in the micro-task queue (until empty).
3. **Render** (if needed).
4. Repeat.

---

### **Example**

```jsx
console.log("Script start");

setTimeout(() => console.log("Macrotask"), 0);

Promise.resolve().then(() => console.log("Microtask 1"));
queueMicrotask(() => console.log("Microtask 2"));

console.log("Script end");

```

**Step-by-step:**

- Call stack starts → `"Script start"` printed.
- Schedules a macrotask (`setTimeout`) → goes to **Task Queue**.
- Schedules two microtasks → go to **Microtask Queue**.
- `"Script end"` printed.
- **Call stack empty → run all microtasks**:
    
    → `"Microtask 1"` → `"Microtask 2"`.
    
- **Then run macrotask**: `"Macrotask"`.

**Output:**

```
Script start
Script end
Microtask 1
Microtask 2
Macrotask

```

---

## 4. **Mental Model**

Think of it like:

- **Macro-task Queue** → Big packages (timers, events, I/O).
- **Micro-task Queue** → Small urgent letters (promises, queued microtasks).
- The postman (event loop) delivers **all urgent letters before picking up the next big package**.

---

</aside>

---

> ***Won’t this current arrangement lead to Callback Queue starvation?***
> 

> While yes, the micro tasks queue is utilised very sparsely and cleverly. The developer has to make sure that the micro tasks queue isn’t long enough and lead to page loading being blocked…
> 

---

<aside>
💡

**Sample snippet:**

```java
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
```

---

**Output:**

| Step | Action Taken | Printed | Task Queue (Macrotask) | Microtask Queue |
| --- | --- | --- | --- | --- |
| 1 | Script start | `A` | [B] | [D] |
| 2 | Run `D` | `D` | [B, E] | [] |
| 3 | Run `B` | `B` | [E] | [C] |
| 4 | Run `C` | `C` | [E] | [] |
| 5 | Run `E` | `E` | [] | [] |
</aside>

---

<aside>
💡

### Variables In Context Of JS and Event Loop:

1. All the variables are stored in Heap in case of the browser…
2. In the context of developers at a higher level, 
    1. The variables are classified as var, let, const…
        1. Const variables are immutable/unchangeable
        2. Var and let have a difference of hoisting i.e. 
        
        <aside>
        <img src="https://www.notion.so/icons/code_red.svg" alt="https://www.notion.so/icons/code_red.svg" width="40px" />
        
        - **Hoisting** applies to var, function, let, const, class, import
        - Function scope is created by a function while block scope is created by {} (e.g. if, else, for, while, do)
        - Hoisting is moving the declaration to the top of the scope, now scope can either be block scope or functional scope.
        - **var hoisting**: move var declarations to the top of innermost function, var by default has an **“undefined”** value.
        - **let hoisting**: move the let declaration to the top of the innermost block scope, a let variable cannot be used before initialisation unlike var variables which can be used without definition….for cases where there are no block exists then no hoisting happens for ***LET***, in such cases code executes line by line…
        </aside>
        
        ![Screenshot 2025-08-14 at 9.00.06 PM.png](Screenshot_2025-08-14_at_9.00.06_PM.png)
        
</aside>

---

<aside>
💡

### ⇒ **Function Declaration And Hoisting:**

```java
// Approach 1
function(foo) {
	console.log("foo is called") // function declaration are always hoisted
}
foo() // function invocation

// Approach 2
var foo = function() { 
	console.log("foo is called")  // These are called Functional expressions, here var rules for hoisting would be applied
}

// Approach 3: arrow function
var foo = () => { 
	console.log("foo is called")  // These are called Functional expressions, here var rules for hoisting would be applied
}

// Approach 4: anonymous function
() => {
  console.log("Foo anonymous is called")
}

// Approach 5: self-invoking function
// they are automatically invoked once the js file is loaded
(() => {
  console.log("Foo anonymous is called")
})();
```

---

</aside>

---

<aside>
💡

### Everything In Java Is Object:

- Example being when we put any integer data in a var variable, then it inherits its methods from INTEGER function…or var becomes an object of number.

---

> We always define params for our function declaration and we pass arguments during function call…
> 

### **⇒ Generator Function:**

1. A function which can return multiple values are termed as Generator Functions…
2. It return an iterator when the function is called. It doesn’t store the previous values, it stores the state instead.

```java
function* scoreGen(initialScore){
  let currentScore = initialScore;
  while(currentScore < 5){
    currentScore = currentScore + 1;
    yield currentScore;
  }
}
```

</aside>

---

<aside>
💡

### JSON:

1. Anything with curly braces {} is an object in javascript.

```java
var studentObj1 = {
	name: "name1";
	age: 20;
	rollno: 25;
};
```

1. Now to store this object in local storage, **localStorage.setItem(”stu1”, JSON.stringify(studentObj1)**) is used…

> If we don’t Stringify the object then localStorage won’t save the data as expected in the backend…
> 
1. We use JSON.parse(objName) is used to convert Stringify objects to normal Javascript objects.
</aside>

---

<aside>
💡

### Loops:

```java
// for loop : normal
for (let i = 0; i<numArr.length; i++){
  console.log(`The value is : ${i}`);
}

// for-OF loop : used to directly access the values
// the use of continue and break remains the same
for( let numArrItem of numArr ){
		console.log(`The value is : ${numArrItem}`);
} 

// for-IN loop : used to access the index(in arrays)/key(in objects) for the correspondong values
// the use of continue and break remains the same
// used to iterate through both array and objects
for( let numArrItem in numArr ){
		console.log(`The value is : ${numArrItem}`); // prints the index of array items
} 

// for-EACH loop(pending)

// for-EACH vs map(pending)
```

</aside>

---

<aside>
💡

### How To Create Objects:

```java
// object literal
var objLiteral = {
  name: "name",
  age: 20,
  isActive: true,
  calculate.function(){
    return this.age * 2;
  }
};

// using new keyword
var objectUsingNew = new Object({name: "name1"});

// object using assign=> params: (target, source)
// copies properties from source to target
// source is not modified, only target is updates
var objUsingAssign = Object.assign({age: 20}, objectUsingNew)

// pass by reference behaviour
var objLiteral1 = {
  name: "name",
  age: 20,
  isActive: true,
  calculate.function(){
    return this.age * 2;
  } 
};

// wrong way to create a new object from an existing object
var objectLiteral2 = objLiteral1;
// here any changes made in obj2 will be reflected in obj1 as well
// in javascript, objects are pass by reference

// This is also wrong method here, this also creates a reference only
var objectLiteral2 = new Object(objLiteral1);

// using new keyword
var objectUsingNew = new Object({name: "name1"});
```

<aside>
💡

### ⇒ Fixing The Object Creation Conundrum Of ‘NEW’ Keyword:

### ✅ Key Point:

- `new Object(obj)`
    - If `obj` is an **object**, it returns the same reference (no new object).
    - If `obj` is a **primitive**, it returns a wrapper object (`new Object(5)` → `Number(5)` object).
- `new Object({ ... })`
    - The `{ ... }` itself is a **new object literal**, so you get a new object.
    - `new Object` adds no benefit here.

---

👉 So in your two cases:

- `objectLiteral2` → **reference to `objLiteral1` (no new object)**
- `objectUsingNew` → **new object (because of the literal, not `new Object`)**
</aside>

---

***REVISE THIS BLOCK***

```java
// object using CREATE
var objCreate1 = {
  name: "name",
  age: 20,
};

// ✅ Correct way of making a different object with a separate reference from the original one
// This basically makes a new object based on the prototype of object1

var objCreate2 = Object.create(objCreate1);
// This 'PROTOTYPE' returns all properties from the OBJECT function
// Basically all properties are inherited from a base paremt function
// If a function inherits it properties from another function, 
// Then __proto__ is appended to that object to represent its parent's properties.

```

### ⇒ Javascript Inheritance:

> Javascript doesn’t have classes conventionally, in JS we have functions and those functions are inherited here…they are known as constructor functions.
> 
1. If we are writing **var x = 10**, ‘x’ inherits all properties of number function. 
2. In the same way, all objects inherit their properties from base ‘OBJECT’ class.
3. ***Prototypical Inheritance(IMPORTANT):***

<aside>
💡

---

### 1. What is prototypical inheritance?

JavaScript doesn’t use **classical inheritance** (like Java or C++). Instead, it uses something called **prototypical inheritance**, where objects can inherit properties and methods directly from other objects via the **prototype chain**.

---

### 2. Every object has a prototype

- When you create an object in JS, it has a hidden link (`[[Prototype]]`) that refers to another object (its prototype).
- You can access this link using `Object.getPrototypeOf(obj)` or the `__proto__` property (though `__proto__` is discouraged in production code).

Example:

```jsx
let animal = {
  eats: true,
  walk() {
    console.log("Animal walks");
  }
};

let dog = {
  bark() {
    console.log("Woof!");
  }
};

// Make dog inherit from animal
dog.__proto__ = animal;

console.log(dog.eats);   // true (inherited from animal)
dog.walk();              // "Animal walks" (inherited)
dog.bark();              // "Woof!" (its own method)

```

Here, `dog` doesn’t have `eats` or `walk`, so JavaScript looks up the prototype chain in `animal`.

---

### 3. The Prototype Chain

If you try to access a property on an object:

1. JavaScript checks if the property exists on the object itself.
2. If not, it looks up the prototype.
3. If not found, it goes up again, until reaching `Object.prototype`.
4. If still not found, it returns `undefined`.

---

### 4. Functions and `.prototype`

When you create a function in JavaScript, it automatically gets a `.prototype` object.

This is used when you create objects with the `new` keyword.

Example:

```jsx
function Person(name) {
  this.name = name;
}

// Add a method on Person's prototype
Person.prototype.sayHello = function() {
  console.log(`Hello, my name is ${this.name}`);
};

let john = new Person("John");

john.sayHello(); // "Hello, my name is John"

```

- `john` doesn’t have `sayHello` directly.
- But `john.__proto__` points to `Person.prototype`, which has `sayHello`.

---

### 5. ES6 `class` syntax (syntactic sugar)

JavaScript introduced `class` syntax, but under the hood, it’s still **prototypical inheritance**.

```jsx
class Animal {
  eat() {
    console.log("Eating...");
  }
}

class Dog extends Animal {
  bark() {
    console.log("Woof!");
  }
}

let d = new Dog();
d.bark(); // "Woof!"
d.eat();  // "Eating..." (inherited from Animal)

```

This is just cleaner syntax for what we saw with prototypes.

---

✅ **In short**:

- Objects in JS inherit from other objects through a **prototype chain**.
- Functions have a `.prototype` object that is used for inheritance when creating instances.
- ES6 `class` is just syntax sugar over this system.

---

![Screenshot 2025-08-16 at 12.19.42 PM.png](Screenshot_2025-08-16_at_12.19.42_PM.png)

</aside>

</aside>