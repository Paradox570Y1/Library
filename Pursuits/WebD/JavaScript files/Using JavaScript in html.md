> Resources : [W3School](https://www.w3schools.com/js/js_htmldom.asp)
# How to add JavaScript?

**3 Ways to Add JavaScript**

- Using `onload`
	- When the body of our website gets loaded up then our JavaScript will get carried out.
	- It has several disadvantage:
		- Its's not modular.
		- Difficult to Debug.
		- Not a good practice as well.
	- `So avoid this method`
	![[Pasted image 20241212094643.png|400]]


- Using Internal JavaScript(with Script Tag)
	- While reading the file line by line when browser hits the script tag then the javascript will get carried out.
	![[Pasted image 20241212095015.png|300]]


- Using External JavaScript
	- This is the best practice to put the JavaScript right before the closing of body tag.
	- This is done so that all the elements on which functioning is provided by the JavaScript is already loaded otherwise we will get `Uncaught TypeError`
	- Also if your script is heavy and requires more loading time , then at least the user interface would have been loaded up for the user to see.
	![[Pasted image 20241212095218.png|300]]

> **Note**
> - CSS is put in head tag so that all the elements loaded in the website renders with the CSS, otherwise when we open the website it would be without CSS until the browser hits the style tag in body.
> - JavaScript is put right before the closing of body tag to ensure all the elements  on which functioning is provided by the JavaScript is already loaded otherwise we will get `Uncaught TypeError`



# DOM(Document Object Model)

- The task of converting the html file into DOM is done by the Browser when you Load up the Web Page.
- It turns each of the elements and their associated data into the tree structure with whole bunch of Objects you can select and manipulate.
![[Pasted image 20241212102040.png|200]]

Use` HTML Tree Generator Extension` to make `Dom Tree` of your website.
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <title>My Website</title>
    <link rel="stylesheet" href="styles.css">
  </head>
  <body>
    <h1>Hello</h1>
    <input type="checkbox">
    <button style=":active color:red;">Click Me</button>
    <ul>
      <li class="list">
        <a href="https://www.google.com">Google</a>
      </li>
      <li class="list">Second</li>
      <li class="list">Third</li>
    </ul>
  </body>
</html>
```

![[Pasted image 20241212102133.png|400]]

How to Navigate to the Child or Node in Console
- Use Dot notation to access the child
![[Pasted image 20241212102527.png|500]]
- Now we can manipulate the elements
![[Pasted image 20241212102950.png|300]]
![[Pasted image 20241212103211.png|300]]

##### Get Property (Getter property)

```html
car.color; // gives the color of the car
```

##### Set Property (Setter property)

```html
car.numberOfDoors = 0; // Set the no. of Doors of Car.
```

##### Call Method 

```html
car.drive(); // If we call a method drive then object car will start moving, this is Call Method
```

Example of Button
![[Pasted image 20241212103850.png|400]]

```js
document.lastElementChild.querySelector("ul").lastElementChild = "Hello";
```



# Different Ways to Select a Node

```js
document.firstElementChild; //select first node
document.lastElementChild;  //select last node

// Inside the Brackets write inside double quotes 
document.getElementByTagName("li")[2]; // selects 3rd li tag
document.getElementByTagName("li").length; //gives no. of elements

document.getElementsByClassName("btn")[0]; 
//selects the first "btn" class
document.getElementById("title"); // selects the element with ID= title

document.querySelector("h1"); // selects first h1 tag
// It can also search class, ID or combinations 
//You can use it to select very specific element by combining class, ID like
document.querySelector("li.item a");
//selects first anchor tag within item class of li tag
document.querySelector("#li a");
//even if a is the grand child of li id , still it will select first anchor tag

document.querySelectorAll("#li a");
// it will select all the anchor tag inside li ID  and create a NodeList
```

>NOTE
>`Use querySelector instead of getElement as they provide more flexibility in selecting particular element.`

> **NOTE**
> - Using `document.getElementsByClassName("btn").style.color = "red"` will give you `Uncaught TypeError` because it always return `HTML Collection` even if there is only one element so you need to access the first element using `[0]` index;
> 
> - Using `document.querySelectorAll("#li a").innerHTML="hello"` will give you `Uncaught TypeError` because it always return a NodeList even if there is only one element so you need to access the first element using `[0]` index;

Some notable details
- On selecting the li tag instead of the anchor tag only bullet color is set to red.
![[Pasted image 20241212111333.png|300]]
![[Pasted image 20241212111404.png|100]]

- On selecting anchor tag just apply color to the text of anchor tag.
![[Pasted image 20241212111602.png|300]]
![[Pasted image 20241212111635.png|100]]


> [JavaScript Styles](https://www.w3schools.com/jsref/dom_obj_style.asp)
# Properties for Manipulation
- In JavaScript properties are  Camel-Cased like font-size become `fontSize`.
- Values are represented as String.
```js
document.querySelector("h1").style.color = "red";
document.querySelector("h1").style.fontSize = "10 rem";

```



# Manipulating Style Sheet using JavaScript

##### Manipulating Classes
- Using `classList` property
	- It gives the List of classes attached to this element.
		![[Pasted image 20241212143249.png|300]]
	- Now using it we can add classes through javascript using `add()`
		![[Pasted image 20241212144639.png]]
	- To remove the class , use `remove()`
	![[Pasted image 20241212144845.png|500]]
	- To toggle the class, if it is added then gets removed and vice versa.
		![[Pasted image 20241212145036.png|400]]
		- it also says true and false which tells if class is applied or not.

###### Difference between `innerHTML` and `textContent`
![[Pasted image 20241212145605.png|400]]
- In above context there is strong tag around the text inside the h1 tag. So, `innerHTML` returns the text along with the strong tag which is not the case with `textContent`. 
- So using `innerHTML` we can manipulate the effects on text too which can't be done with  `textContent`.

##### Manipulating Attribute

- Similar to classes we can check the attributes of an element
```js
document.querySelector("a").attributes;
//Gives NamedNodeMap of attributes like href etc.
```

- Now to get a specific attribute
```js
document.querySelector("a").getAttribute("href");
```
Example given below:-
![[Pasted image 20241212150451.png|400]]

- Now to Modify a specific attribute value e
	- It takes two parameters
		- one is the attribute whose value is to be modified
		- second is the new value to replace with.
![[Pasted image 20241212151008.png|400]]

# Function
- There are only two types of function.
	- Anonymous function or arrow function.
	- Normal function with `function` keyword.
### Self calling(invoking) function
- It is heavily used in frameworks.

![[Pasted image 20250719105300.png|300]]

# Event Listener in JS

> Resources: [Link](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)
> To find more [Events](https://developer.mozilla.org/en-US/docs/Web/API/Event#introduction).

> [Events](https://developer.mozilla.org/en-US/docs/Web/Events)
```js
document.querySelector("button").addEventListener("click",handleClick);
function handleClick(){
    alert("I got clicked!");
}
// Our object button is listening to click Event and calls a function handleClick which gives an alert

// 1st parameter of EventListener tells what type of Event it listens to.
// 2nd parameter tells What to do if Event is triggered
```

>**NOTE**
>*Why we used function name without Brackets?*
>Ans. This is because if we had put the brackets then on opening the website `handleClick()` function will automatically gets called while adding the Event Listener to the object , even if we haven't clicked.
>So, to prevent that  we just pass the name of the function  as input parameter instead of calling the function.

- Using Anonymous Function
![[Pasted image 20241213002809.png|400]]
![[Pasted image 20250726094741.png|200]]

![[Pasted image 20250726094913.png|300]]
- Using name of a function
![[Pasted image 20241213002740.png|400]]


#### How to use $0 to select element in console while testing
- Select the element you want to modify.
	![[Pasted image 20241213003212.png|400]]
	On selecting  the element you will $0 at the end, Now you can access this element with $0
	![[Pasted image 20241213003333.png|400]]
	Like here I modified the Wiki data by selecting an element.


# Passing Function as Arguments

![[Pasted image 20241213003845.png|400]]

![[Pasted image 20241213004023.png]]
You can use Debugger to see the process, just use `debugger;` in console and holding shift move to next line and provide the function you want to debug. It will open a debugger.

```js
//Calculator code
function add(n1,n2){
    return n1+n2;
}
function subtract(n1,n2){
    return n1-n2;
}
function divide(n1,n2){
    return n1/n2;
}
function multiply(n1,n2){
    return n1*n2;
}
function calculator(n1,n2,operator){
    return operator(n1,n2);
}
```
Output:
![[Pasted image 20241213004732.png|200]]

# To Trigger audio file on Event

> [Resources](https://developer.mozilla.org/en-US/docs/Web/API/HTMLAudioElement)


```js
var audio = new Audio('./sounds/tom-1.mp3');
audio.play();
//This is how we can create and play an audio like in below function
var keys = document.querySelectorAll("button");
for(let i=0;i<keys.length;i++){
    keys[i].addEventListener("click",function () {
        var audio = new Audio('./sounds/tom-1.mp3');
        audio.play();
    });
}
//here on clicking button object given audio will play
```


# Using this keyword 

- This refers to current selected Object.
```js
this.style.color = "red";
//so if this is the current object then we can directly set properties and functions to it.
```

# Using Switch 

```js
var keys = document.querySelectorAll("button");
for(let i=0;i<keys.length;i++){
    keys[i].addEventListener("click",function () {
        var selectedKey = this.textContent;
        var audio;
        switch (selectedKey){
            case "w":
                audio = new Audio('./sounds/tom-1.mp3');
                break;
            case "a":
                audio = new Audio('./sounds/tom-2.mp3');
                break;
            case "s":
                audio = new Audio("./sounds/tom-3.mp3");
                break;
            case "d":
                audio = new Audio("./sounds/tom-4.mp3");
                break;
            case "j":
                audio = new Audio("./sounds/snare.mp3");
                break;
            case "k":
                audio = new Audio("./sounds/kick-bass.mp3");
                break;
            case "l":
                audio = new Audio("./sounds/crash.mp3");
                break;
            default:
                console.log(selectedKey);
        }
        audio.play();
    });
}
```


# Objects in JavaScript

![[Pasted image 20241213113611.png|350]]

- We can even add methods inside an object

![[Pasted image 20241213121459.png|400]]

- Now we can use Call Method
![[Pasted image 20241213121550.png|220]]


# Constructor Function
- In these function the name of the function should be Pascal Case which means first Letter of each word will be capital. Due to this we can distinguish them from normal function.

![[Pasted image 20241213115419.png|400]]
![[Pasted image 20241213122103.png|500]]

##### Initialize Object
- The only difference is the use of `new` keyword and the Pascal Case of the name.
![[Pasted image 20241213120143.png]]


**How Audio method might work**
![[Pasted image 20250105195135.png|400]]

# `EventListener` (`keypress`/`keydown`)

```txt
**NOTE**
TL;DR keypress is now deprecated, you should use keydown instead.

Just a quick heads up, as technology moves incredibly fast, every week or so something else will change. This is just a quick reminder that in the next lesson, when we cover detecting key presses, you should be using the keydown event listener instead of keypress.
```

- To listen to keyboard event use `keydown`
- This event listener should be applied to whole document instead of just those buttons to work
- To recognize the key which got pressed , pass event as a parameter which receive details about the event.
- Now use the event object and check its attributes, it has `key` attribute which tells what key got pressed.
![[Pasted image 20250105200919.png|300]]

# Higher Order Functions
- These are referred to Functions which can pick another functions as input.
- The function which gets passed as parameter is called Callback function and it is callback function only in that context otherwise function by itself is just a normal function.
	- Passing one function as argument to another function is called Callback function.
	- Callback function is not a type of function it's just the behavior it shows when it is passed as argument.
Ex `addEventListener` is higher order function
![[Pasted image 20250105204008.png|400]]
- When document detects the keypress then it calls the callback function.
- So callback function is a function which is not called by us , it is called by the object which experiences the event.

Creating a mock event listener function 
![[Pasted image 20250105205341.png|400]]
here you can see how the callback function is executed after the higher order function completes its execution.

# `setTime0ut` Function

- It executes in non blocking mode.
- It's not a javascript feature , it's a web API which executes after set timer runs out.
- When the timer is running then this function puts the code in a new thread and after timer runs out then that code starts its execution in the main thread.
- Other way to execute the code is after the current thread is executed by setting it to 0. [[setTimeout(func,0)]]
- We cannot have complete control like in case multiple 
- For running a function after a timer , just pass function definition and do not call it
![[Pasted image 20250105211017.png|300]]
![[Pasted image 20250719121618.png]]
![[Pasted image 20250719113535.png|400]]
Received after 5 sec
![[Pasted image 20250719113556.png]]

```js
function playAnimation(key){
  var obj = document.querySelector("."+key);
  obj.classList.add("pressed");
  setTimeout(function(){
    obj.classList.remove("pressed");
  },100);
}
```
- It calls back the callback function after delay of 0.1 second.
![[Pasted image 20250719114602.png]]


# Hoisting
- Hoisting is a feature of JavaScript which move `variable declaration` to top of innermost function  which could be a function scope or a block scope.
- So it just moves variable declaration and not it's definition. 
- The variable is accessible inside innermost function but not it's value .

As `var` supports hoisting
![[Pasted image 20250719123523.png|200]]
![[Pasted image 20250719123534.png]]


As `let` doesn't support hoisting
![[Pasted image 20250719123634.png|200]]![[Pasted image 20250719123622.png]]


Q If there are 10 identical elements in html then using javascript how can you select 8th element from it.
Ans: As they share same class name then use `document.getElementByClassname()` which will provide you the array of elements and using index we select particular element from it.