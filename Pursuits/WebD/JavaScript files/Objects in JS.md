👉 Everything that is **not primitive** is an **object**

```typescript
JavaScript Values
│
├── Primitive
│   ├── string
│   ├── number
│   ├── boolean
│   ├── null
│   ├── undefined
│   ├── symbol
│   └── bigint
│
└── Object (non-primitive)
    ├── Plain Object {} (object literal)
    ├── Array []
    ├── Function
    ├── Date
    ├── Map
    ├── Set
    └── etc.
```

So:
- **Object (capital O)** → a **category / type**    
- **object literal `{}`** → a **specific kind of object**

Object stores **collections of data** and **complex entities**.

## 2️⃣ Where is this `Object`?

`Object` is a **built-in constructor function**, provided by the JavaScript engine.

```js
typeof Object; // "function"
```

Includes:

- Objects (object literal)
- Arrays
	- Arrays are objects with extra rules 
	- An array is basically an object that:
		- uses **numeric keys** (`0`, `1`, `2`, …)
		- has a **magic `length` property**
		- inherits array methods (`push`, `map`, `filter`, …)
		- Even though arrays _act_ like objects, engines don’t store them like random objects internally.
- Functions
	- Function are callable objects which means they have an internal `[[call]]` method whereas Objects don't have call method unless they are function. Therefore on checking it's type , it says `function`.
- Dates
- Maps, Sets, etc.

> **Object is both:**
> 
> - a **data type category**
> - and a **specific structure (`{}`) inside that category**
>

```js
let obj = { name: "JS" };
let arr = [1, 2, 3];
let func = function () {};

typeof obj;   // "object"
typeof arr;   // "object"
typeof func;  // "function" (special case)
```

#### Why `typeof` doesn’t say `"array"`

`typeof` only answers **very coarse questions**:

- primitive vs non-primitive
- callable vs not callable

#### To check if some object is array or not
![[Pasted image 20260206160108.png|300]]
![[Pasted image 20260206160230.png|300]]


It does _not_ distinguish object subtypes.

## The mental upgrade (this matters)

# Generator Function
A generator is not “a function that returns many values”.
It is:
> **A controllable, pausable execution process**

- It returns an iterator object which has iterator and iterable protocols.
- Has built-in methods like:
	- `next()`
	- `return()`
	- `throw()`

```js
function* numberGenerator(limit) {
    let i = 0;
    while (i < limit) {
        yield i; // The function "pauses" here and returns { value: i, done: false }
        i++;
    }
    return "Finished"; // Final call returns { value: "Finished", done: true }
}

const gen = numberGenerator(3);

console.log(gen.next()); // { value: 0, done: false }
console.log(gen.next()); // { value: 1, done: false }
console.log(gen.next().value); // 2
console.log(gen.next()); // { value: "Finished", done: true }
```

![[Pasted image 20250821185032.png|400]]
[[Generator Functions]]

### Object Literal

![[Pasted image 20260208190155.png|300]]
[[JSON behavior]]
![[Pasted image 20260208201408.png|300]]
- To store object in [[localStorage]]
- JSON 
	- JSON (JavaScript Object Notation) is a lightweight, text-based data-serialization format used to represent structured data in a language-independent, machine-readable form.
	- We use JSON as in built feature to convert the object to text
	- We can use other custom ways as well with XML, CSV etc.

```js
let obj = {
  name : 'Apurav',
  age : 23,
  id : Symbol("paradox"),
  id : Symbol("paradox")
} // stored as {name: 'Apurav', age: 23, id: Symbol(paradox)}

localStorage.setItem("key_name", JSON.stringify(obj)); //returns undefined
// Without stringify data is not stored as expected
// instead it stores `[object Object]` irrespective of the data
// JSON 
localStorage.getItem("key_name"); // returns '{"name":"Apurav","age":23}'
// As we can see the returned data is inside single quotes which means the whole data is string so you can't access any attribute from it.
JSON.parse(localStorage.getItem("key_name")) // returns {name: 'Apurav', age: 23}
// parse recovers the object from the string
```

![[Pasted image 20250821185722.png | 500]]

![[Pasted image 20250821185730.png|300]]


Use of `Stringify`
- Used to send data in local storage.
- Before making HTTP call we have to use `Stringify` to send data to backend bcz the runtime reference of the object may not exist in the backend environment hence we need persistent data to send.

[[Ways to create Object]]
- `this` keyword refers to the object that calls the method
[[Wrapper Objects in JS]]

[[Prototypical Inheritance]]


![[Pasted image 20250821185950.png|400]]

![[Pasted image 20250821190006.png|400]]


![[Pasted image 20250821190029.png]]
![[Pasted image 20250821190049.png]]
![[Pasted image 20250821190058.png]]

![[Pasted image 20250821190110.png]]

![[Pasted image 20250821185247.png|400]]


# 5. ES6  class syntax (syntactic sugar)

![[Pasted image 20250821185307.png|300]]

![[Pasted image 20250821185345.png|300]]



---

Q. What is prototype?
- It is the property that is attached to the Object.

![[Pasted image 20250821201549.png]]



[Resources](https://kaksha-dev.github.io/web)
[Prototypic Inheritance](https://kaksha-dev.github.io/web/oojs/prototypical_inheritance)
- Diamond problem doesn't exist in Protype inheritance.
- Class is a blueprint to standardized


# Approach to create objects
#### Approach 1
- Niche approach of creating object in javascript
![[Pasted image 20250821202611.png]]

#Problems 
Now problems with above code is:
- No reusability.
- Not suitable to create multiple objects.

#Observation
- It will assign memory to each attribute.

#Solution
To correct this use functions or classes.

#### Approach 2: Using Function

![[Pasted image 20250821203038.png]]
![[Pasted image 20250821203125.png|200]]

#Problem
- After object of `student1` is created their is no linkage with the function `createStudent`. 
	- So, it's not really a blueprint.
	- If there is any modification to function then it will not inherit new properties.
- 

```js
// quick question, is this better to keep function outside instead of inside 
// while creating a new function in every object?

function checkResult(marks) {
    if (marks > 40) {
        return "pass"
    } else {
        return "fail"
    }
}

function Student(fname, marks) {
    return {
        fname: fname,
        marks: marks,
        result: checkResult
    }
}
```

- Keeping the function outside is better for memory as all student objects will share the same function reference but their is better way to do this
# Approach 3: Using Constructor function

- Whenever JS encounters new keyword. It binds this keyword to new object or we can say it assigns `this` keyword to lefthand side object.
- this keyword value becomes object itself (reference to object) which is being created.
- So we can say this keyword is required to get the reference of created object inside the function.
![[Pasted image 20250821204540.png|400]]
- Above code will create new object using `createStudent` function and inside this function `this` keyword will be student object itself.

![[Pasted image 20250821205622.png|400]]
Does creating new object breaks the linkage of previous object with the constructor function? 
-> No, prototype of object remains same as of function prototype and if any changes made to function will also reflect in objects prototype.


![[Pasted image 20250821205939.png]]
- Window scope : This is the scope where function is  declared.
- In case we don't use new keyword while creating object then
	- Linkage of `this` keyword with object is not created.
![[Pasted image 20250821211629.png]]


- In case we return an object then it breaks the linkage of this keyword and returns the object value instead.
	![[Pasted image 20250821210226.png|400]]
- In case we return a primitive value then linkage persists.
	![[Pasted image 20250821210536.png|400]]


Q. Does that mean there is no relation with function for earlier created function?
->No , the protype of object created is same as that of function prototype

![[Pasted image 20250821212527.png|400]]



# More about value of this

- In below image value of this is different for different object.
![[Pasted image 20250821213111.png]]
- This is because when we call function with object `student1`, JS interprets `this` as student1 object and similarly for other objects.

# Modifying the prototype

- At any instance if we modify function's prototype then it is modified for all objects  and also inherits the updated properties through prototypical inheritance.
![[Pasted image 20250821213459.png]]

#Problem 
- It's still not real blueprint.


> Getter methods are used to prevent exposing properties of the function.
\

# What if we add property to function directly instead of it's prototype

- Suppose we added a function `checkMarksOutside` in student function.
- Then it will not be added to all the objects created using that function.
![[Pasted image 20250821214358.png]]


Q. When we define the function, all the parameters and methods we set automatically get added to prototype of that function?
-> No that's not the case , When function is defined then it's properties and methods are like concrete properties and methods of function if you want to change property then you have to redefine the function.
-> But you can append new properties and methods by modifying function's protype.
![[Pasted image 20250821214913.png]]


# Homework
Based on understanding Of prototypical inheritance ,constructor functions, this keyword inside constructor functions. Using these three concepts:
- Similar to map() function of Array() , implement a new custom map() function which works exactly as map works.

Solution
```js
var arr = [1, 2, 3, 4, 5];
arr.map(function(val) {
    return val * 2;
})

Array.prototype.customMap = function(callback) {
    let newArr = [];
    for (let idx = 0; idx < this.length; idx++) {
        int callBackVal = callback(this[idx], i, this);
        newArr.push(callBackVal);
    }
    return newArr;
}
arr.map(function(val) {
	return val * 2;
});
```


![[Pasted image 20250821221200.png]]

### Issues that can come during custom prototype implementation
- Concurrency issues
	- Suppose your script is loaded in defer mode then your prototype might not be loaded.
	- If page at which  prototype  is defined is not loaded yet then there will be error.


# How to solve function duplication issue

#Issue
- This can happen if we define function inside Constructor function.

#Fix
- Either define the function outside or define the function in prototype of constructor function.

![[Pasted image 20250828203157.png|400]]

![[Pasted image 20250828203541.png|400]]