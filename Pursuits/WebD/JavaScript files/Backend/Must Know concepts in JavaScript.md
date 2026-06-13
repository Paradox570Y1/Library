# Destructor in JS

- It's just a convenient way to give name to data in an array or in object.

#### Destructors in array
```js
var arr1 = [1, "Amit", "Garg", {name: "name1", age: 20}];
//de-structuring in JavaScript
var [count, fName, lName, details] = arr1;
```

#### Destructors in Object
```js
var obj1 = {
  fName : "Apurav",
  lName : "Gautam",
  marks : {Maths:98, English:90}
}
var {fName, lName} = obj1;
console.log(fName); // Apurav
console.log(lName); // Gautam
```



# Method Chaining

- When we are calling a function over another function that is method chaining.
- Method chaining is when a function returns an object
- The returned object has at least one property that is a function allowing you to call another function on that object.
![[Pasted image 20250830112319.png|300]]

Implementation of custom `concat` method

Using prototype
```js
String.prototype.infiniteConcat = function (stringToConcat) {
    return this + " " + stringToConcat;
}
```

Creating custom String

```js

function customString(InitialValue) {
    this.value = InitialValue;
    this.infiniteConcat = function(stringToConcat) {
        return {
            value: this.value + stringToConcat,
            infiniteConcat: this.infiniteConcat
        };   
    }
}
```

![[Pasted image 20250830115841.png|300]]

Cleaner way

```js

function customString(InitialValue) {
    this.value = InitialValue;
    this.infiniteConcat = function(stringToConcat) {
        let newValue = this.value + stringToConcat;
        return new customString(newValue);
    }
}
```

![[Pasted image 20250830120155.png|400]]


# Arrow Functions

- They are compact and readable form of normal function

[Resources](https://kaksha-dev.github.io/web/es6/arrow_functions)



```js
function studentArrowFunction(fName, obtainedMarks) {
  console.log(this);
  this.fNameObj = fName;
  this.obtMarksObject = obtainedMarks;

  // Normal Function
  this.checkResultsNormal = function () {
    console.log(this); // since current function is called with this object hence it returns the same this as its parent.
    function innerFunction() {
      console.log("Normal Inner function: ", this);
    }
    innerFunction(); // no object is calling inner function hence this inside inner function takes window as default object
  };

  // Arrow Function
  this.checkResultsArrow = () => {
    console.log(this); // inherited from its parent function
    innerFunction = () => {
      console.log("Arrow Inner function: ", this);//inherited from its parent function
    };
    innerFunction();
  };
}
var student = new studentArrowFunction("fname5", 100);
```
![[Pasted image 20250830122338.png]]
![[Pasted image 20250830122510.png]]

- In arrow functions the context of `this` is taken from where the function is defined rather than where it is called.
	- Arrow function doesn't create this keyword it inherits everything from parent.
	- By default it does initialize anything but inherits everything.
- Normal function - “this” inside normal function points to the object on which it is called, therefore unreliable.
	- Normal function creates this keyword based on object that called the function.
	- It doesn't inherit but initialize the object.

# Proof that Arrow functions are different than normal
- **argument** is  a predefined method for normal functions. But it doesn't exist in case of arrow function hence they are different.

![[Pasted image 20250830124104.png]]
