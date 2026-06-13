`jQuery` is the most popular JavaScript Library.

#### History
---
In drum kit game we have to write complex code like below to make it work

![[Pasted image 20250105211925.png]]

`John Resig` looked into this issue that why need to write such complex code to do a simple task so he created a library which can make this task much simpler.

![[Pasted image 20250105212152.png|300]]

---
- jQuery is represented by symbol `$`.

```js
document.querySelector("h1");
//is same as
jQuery("h1");
//is same as
$("h1");
```

# How to incorporate jQuery in your document

> [jQuery](https://jquery.com/)

- You can download jQuery code files through their download page or you can simply use CDN (Content Delivery Network) just like bootstrap.
- Most Popular option is to use Google's CDN.

```javascript
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.7.1/jquery.min.js"></script>
```
**Advantage of using popular CDN**
>If user have been to another website which utilizes the same CDN to fetch jQuery Library, then they will likely have it already cached and saved in their browser, which means when they want to load up your website they want have to fetch a new copy of jQuery giving your website much faster load rate.

**Where to place the script tag**
- It should be placed as the first script before the end of the body bcz it will then be applied to scripts that are placed right after that.

![[Pasted image 20250105214212.png]]

- If we place it in the head tag with the other scripts then it will not work and will not give any error.
![[Pasted image 20250105214535.png|500]]

You can make it work using following function
```js
$(document).ready(function(){
	//Here you can use jQuery
	//It will process below code once jQuery is loaded
    $("h1").css("color", "red");
})
```

> **CSS & JavaScript minifier**
> [Link](https://www.minifier.org/)
> This is done to compress the space used by code which gives better execution speed.


# Selecting Elements using jQuery

```js
<h1>Hello.</h1>
<button>Click Me</button>
<button>Click Me</button>
<button>Click Me</button>
<button>Click Me</button>
<button>Click Me</button>

$("h1"); // selects only h1
$("button"); //selects all buttons
// so no difference in selecting one element and selecting many.
```

# Using css property
- If you pass one parameter then you are getting the value of the attribute.
- If you pass 2 parameters then you are setting the value of the attribute.

```js
$("h1").css("color","green"); // set the value
console.log($("h1").css("color")); //get the value
```
![[Pasted image 20250105220139.png|200]]
![[Pasted image 20250105220243.png|100]]

# Manipulating classes using jQuery

```js
$("h1").addClass("big-title"); // to add a class
$("h1").removeClass("big-title"); // to remove a class
$("h1").addClass("big-title margin-50"); // to add multiple class

$("h1").hasClass("big-title"); 
// gives boolean true or false based on if h1 element has class big-title applied to it.
```

# Manipulating Text

```js
$("h1").text("Bye"); // changes the text to Bye
//similar to .textContent
$("h1").html("<em>Bye</em>"); // changes the text to Bye with styling
//similar to .innerHTML
```

> Without understanding of traditional `Vanilla JavaScript` , jQuery seems like magic.
> 

# Find and modify attributes

```js
console.log($("a").attr("href")); // gives the reference provided
$("a").attr("href","https://google.com/"); //changes the location to redirect
console.log($("img").attr("class")); // gives all the classes applied to img as class is also an attribute of img tag if used
```

# Adding Event Listener
-  use click() to listen for clicks
```js
$("h1").click(function (){
    $("h1").css("color","purple");
});
// on clicking changes the color of element to purple.
```

```js
//To change the color of heading when any of 5 buttons get pressed
// using vanilla javascript
for(var i=0;i<5;i++){
    document.querySelectorAll("button")[i].addEventListener("click",function(){
        document.querySelector("h1").style.color = "purple";
    });
}

//using jQuery
$("button").click(function (){
    $("h1").css("color", "purple");
}); 
```

- using keypress to listen for key
```js
//here input refers to input field tag so every key we input in that field it will be logged in to the console
$("input").keypress(function(event){
	console.log(event.key);
});

// to make the key pressed show on the screen
$(document).keypress(function(event){
    $("h1").text(event.key);
});
```

- You can add any event listener using `on()` method

```js
// after moving mouse over the text its color will be set to green
$("h1").on("mouseover",function() {
    $("h1").css("color","green");
});
// 1st parameter takes the type of event to be listened
// 2nd parameter takes the callback function to be called later.
```

# Adding and Removing Elements in jQuery

```js
$("h1").before("<button>new</button>"); //before the tag
$("h1").after("<button>new</button>");  //after the tag
$("h1").prepend("<button>new</button>"); //inside tag but before content
$("h1").append("<button>new</button>"); //inside tag but after content
```
- Adds the elements to the  position as given below:-
```css
<body>
    <button>new</button>  /* before */
    <h1>
	    <button>new</button>  /* prepend */
	    Hello.
	    <button>new</button> /* append */
    </h1>
    <button>new</button>  /* after */
</body>
```

- To remove simply use remove method

```js
$("button").remove(); // to remove all the button elements
```

# Animations using jQuery

```js
//when we use hide, toggle or show then it immediately applies the effect to the element without showing transition
$("button").on("click",function(){
    $("h1").hide(); //hides the h1 element
    //or
    $("h1").show(); //show the h1 element
    //or
    $("h1").toggle(); //toggle the h1 element
});
```
- We can provide fading out , fading in animation using following code

```js
$("button").on("click",function(){
    $("h1").fadeOut(); //hides the element with transition effect
    //or
    $("h1").fadeIn(); //show the element with transition effect
    //or
    $("h1").fadeToggle(); //to toggle between effect
});
```

- Similarly we can use sliding effects

```js
$("button").on("click",function(){
	$("h1").slideUp();
    $("h1").slideDown();
    $("h1").slideToggle();
});
```

- To create custom animation we can use method like `animate`

```js
$("button").on("click",function(){
    $("h1").animate({opacity:0.5,margin:30});
});
// you can add multiple properties
// only those properties can be applied which takes numeric value to get transition
// using property like color will raise an error as it doesn't take value
$("h1").animate({opacity:0.5,margin:"30%"});
// to add value in percent or px give it inside double quotes
```

- Chaining the animation together

```js
$("h1").slideUp().slideDown().animate({opacity:0.5,margin:30});
// these animations will gets executed in order one by one
```


> **NOTE**
> jQuery methods does not operate on vanilla JavaScript
>  `this.attr("id");` // results in error as `this` is vanilla JavaScript object
> ` $(this).attr("id");` //  correct