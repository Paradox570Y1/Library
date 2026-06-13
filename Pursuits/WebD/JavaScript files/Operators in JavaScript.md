# Using `...` Operator
Depending on usage it can be used as **Spread operator** or **Rest Operator**.

Usage as Spread Operator
- It always create a new array or object.
```js
//to add multiple elements while declaring array using new keyword
var arr1 = new Array(...[1, 2, 3, 4]);

//combine two arrays
var num1 = [1, 2, 3, 4];
var num2 = [4, 6, 7, 8];
var combinedArray = [...num1, ...num2];

//combine two objects
var studentObjDetail1 = {name: "name1", age:20};
var studentObjDetail2 =  {rollno: 10000025, marks: 900};
var studentObjDetails = {...studentObjDetail1, ...studentObjDetail2};
```


Usage as Rest operator
- Combines the spread elements into a single data structure.
- Basically you don't have to create an array before passing it to function, it will automatically create pack the passed elements into an array.
```js
//Used in array
sumAll(1, 2);
sumAll(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
function sumAll(...items) {
  int sum = 0;
  for (int i = 0; i < items.length; i++) {
    sum += items[i];
  }
  return sum;
}

//Used in object
values({name: "Apurav" , age: 20, University: "Chitkara"},{name: "Rohan"});

//here function puts object in array so first objection will be in 0th index of array created
function values(...object) {
    object.forEach((obj) => {
        for (let val in obj) {
            console.log(val, object[val]);
        }
    })
}
```
Other ways to use REST operator
![[Pasted image 20250828201607.png]]



# Operators
- `instanceof operator` used to check if object belongs to some class or not.
- `nullish coalescing operator`
	- It's a new operator  in javascript.
	- It's used for shorthand initialization.
	- It checks for null or undefined values.
	![[Pasted image 20250919202403.png|400]]
	![[Pasted image 20250919202450.png|400]]
	![[Pasted image 20250919202548.png|400]]
	

- `optional chaining operator` The **[[optional chaining operator]] (`?.`)** is like a _“safer dot (`.`)”_.It **extends the dot operator** by first checking if the object (or property) exists, and only then accessing the next property.
	- We should always use `?.`  instead of `.` to be on safer side.
- `conditional ternary operator`
- `ternary operator` shorthand operator for if-else