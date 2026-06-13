- [[Configuration]]

# What different react does
- It introduced the concept of states at frontend side.
Example
- Earlier when user pressed a like button then it makes a request and gets updated at backend and after response the UI is updated.
	![[Pasted image 20250919203908.png|500]]
- Now React changed this process and when users clicks like button , UI is updated first and then in parallel request is made to server to update the backend. In 99% cases the backend request is a success but in 1% case if it gets failed then UI is changed again to previous state.


# DOM vs ReactDOM

- DOM operations are considered heavy and all components were re-rendered if any updates are made. Browser or react cannot optimize it. 
- Still DOM can handle basic updates like rendering data and putting it in table without react. If there are multiple such updates pushed to the DOM then it will just  try to update the changes  but it cannot control it due to which DOM also hangs as changes are so fast that before completing one two more arrives. So it will just brute force trying to do all updates as they arrive.
- They introduced virtual DOM to maintain state better.
	- Now if user change state of particular object then instead of re-rendering of whole DOM , it renders part of it where the change is happening which is called virtual DOM.
	- This also prevents the page for refreshing.
	- When there are  updates for DOM then `ReactDOM` creates a Batch of data and push that batch to DOM. Like if there are 100 updates then it creates batch of 10 updates each and push 10 batches to DOM instead of individual update.


# Basic Queries
**What is a Library?**
- Library is a piece of code which can be reused in existing code base to make things easier.
- `ReactJS` is a library.


**What is a framework?**
- `NextJS` is a framework.
- It cannot be used in existing application.
- Entire code base is managed by framework.

**Why don't we save dependencies of React**
- This is because it gets updated over time and hence can become outdated.

**How to use it locally**
- Download using packet manager

**What if you want ready to use dependencies**
- Use [CDN](https://legacy.reactjs.org/docs/cdn-links.html) links in header
- There are also minified version of react library and that means all unnecessary spaces are removed to reduce the size at cost of readability and hence they are not suitable for development but optimized version for production.


# React

- `react.development.js` is the **core React library**.
- It provides:
    
    - The **React API** (`React.createElement`, `useState`, `useEffect`, etc.).
    - The ability to define **components** and manage **state**.
    - The "engine" for building **UI logic** in a declarative way.

⚡ But note: React alone doesn’t know _where_ or _how_ to put components into the DOM.

---

# ReactDOM
- React is used so that elements are rendered on runtime which allows us to write `.jsx` which is basically dynamic HTML and that's why general HTML is called static HTML.
- `react-dom.development.js` is the **renderer for the web browser**
- It connects React to the **actual browser DOM**.
- It provides APIs like:
    - `ReactDOM.createRoot()` (React 18+ way)
    - `ReactDOM.render()` (old way, before React 18)

So React = _engine + components_, ReactDOM = _bridge to the browser’s DOM_.



# How to use
- Include the scripts in header
![[Pasted image 20250919212806.png]]

- Proved any element for DOM to render.
![[Pasted image 20250919212906.png|300]]

- You will receive an error
	![[Pasted image 20250919213258.png|400]]
	
- JSX (JavaScript expression) can not be understood by javascript and browser hence to translate it for javascript we require a transpiler like babel. 
	![[Pasted image 20250919213511.png]]
	![[Pasted image 20250919214626.png]]

- After using transpiler you will still get the same error.
- To remove error provide format type to script.
	![[Pasted image 20250919213405.png|400]]

- You can do it from javascript file by providing the type
	![[Pasted image 20250919213631.png|400]]
	![[Pasted image 20250919213723.png|500]]
	- here you can see now script.js is not `script` but is `xhr` request.
	- So script.js is transpiled and converted to `xhr` and downloaded again.

- In this way `root.render()` renders all the code passed in it as `ReactDOM`
	![[Pasted image 20250919214643.png]]


**All the dependencies or variables that you use in your application is attached to Window object**
![[Pasted image 20250920095535.png]]

# Module in JavaScript

- If we want to use import and export type `module` while importing the script.
- Now it is not a javascript file but a module.
- If any file is used in module then they are also treated as module.

#Example
- In math.js
![[Pasted image 20250920102611.png|200]]
- In index.html
![[Pasted image 20250920102556.png|300]]
- In script.js
![[Pasted image 20250920102631.png]]
![[Pasted image 20250920102705.png|200]]


- Now if want to use sum without importing in index.html then treat script.js as module and export the sum function and import in script.js. Now since script.js is a module it will treat math.js as one.


- In math.js
![[Pasted image 20250920103126.png|200]]
- In index.html
![[Pasted image 20250920103109.png]]

- In script.js
![[Pasted image 20250920103150.png]]![[Pasted image 20250920103159.png]]

- Now sum function still works without importing it in main application.


>NOTE
>React recommends using react with NEXT.js framework or you can use `Vite` or any other framework.

- Don't use  document keyword anywhere in react project to retrieve any element instead use `useRef`.


# Using function to pass React code
- This is why `jsx` exist this is possible only if you set the type of script to `text/jsx`.
![[Pasted image 20250920115601.png|300]]
- To provide additional functionality over HTML element , react created a wrapper over them which is jsx to provide additional functionality.


### **Component in React**

- It is a division of the UI/HTML code based on functionality (small, reusable pieces).
- Technically, it is a **JavaScript function** (or ES6 class) that returns JSX (HTML-like code).
- A component is treated as react component only if it's name is in pascal casing
- Components make the UI **reusable, modular, and easier to maintain**.
There are two main types:
1. **Functional Components** → Created using functions, most commonly used with Hooks.
2. **Class Components** → Created using ES6 classes, include lifecycle methods (less common now).

- `descriptionComponent()` here is not a react component as casing is different , it's just javascript function.
![[Pasted image 20250920120544.png|300]]


- Now using Pascal case in naming it's a jsx component so it has additional functionalities now
![[Pasted image 20250920120705.png]]

# Props in React

- props in jsx is considered as **properties** instead of *parameters*.
- props word  is general convention to get properties in components although you can use any word.

![[Pasted image 20250920121117.png|300]]
![[Pasted image 20250920121130.png|300]]

- Same can be done with directly getting properties as parameter
![[Pasted image 20250920121246.png|300]]


- props of components are always `ReadOnly` and never supposed to be modified hence if you try to modify then codebase will throw error
![[Pasted image 20250920122900.png|300]]
![[Pasted image 20250920122920.png|400]]
- Props is used to send parent specific data or data which varies with components.
# Use of nullish coalescing operator
Using `nullish coalescing operator` to ensure consistency
![[Pasted image 20250920121744.png|300]]
![[Pasted image 20250920121756.png|300]]

# How to return multiple elements inside ReactDOM
- Wrap elements in `React Fragment` which is used to  combine multiple elements just like div but it doesn't become the part of `jsx` itself unlike div tag which becomes part of html and unnecessary adds div as outermost layer.
- Symbol of React Fragment => `<> </>`
	![[Pasted image 20250920123127.png|350]]


# Using Custom Element
Extra Topic
[Resources](https://developer.mozilla.org/en-US/docs/Web/API/Web_components/Using_custom_elements)

>NOTE: While designing a website we often use Box Model. In a way we can say that is a component. In Box Model everything is considered as box and there is element, padding, border and margin.

# Components in React
- We can render multiple components inside components as well.
- In `.jsx` their is concept of synthetic event which is build over events and have camel case instead of pascal.
# States in React
- It is the current data that Components holds.
- If we want to update the data either we have to use props to reinitialize the function other way is using react state which only pushes that update on which react state is used.
- Props is needed if dynamic data comes from parent component.
- `React.useState()` is a method of react used to manage state of react component
- Parameter
- `React.useState()` returns an array:
	- 1st index is the value or state itself.
	- 2nd index is the function which is used to modify the state.
- Suppose we have to update state with some event handler then while using `ReactState` we can only pass function reference inside that Event Handler and that function will update the state of react component using the 2nd index function taken from react component.
- Inside `useState()`  you initialize the initial state of data.



*Correct Way*
![[Pasted image 20250925205501.png|400]]
- Here we might get previous state in console but updated value will be in DOM because we are updating the value inside of setlikes which is not updated for current state of funtion

OR

![[Pasted image 20250925212218.png|400]]
- Here we get same value in console as current likes as variable is updated outside of function of state updation.


**Wrong Way**
![[Pasted image 20250925204933.png|400]]

- We can modify multiple data passed as object inside `ReactState`
![[Pasted image 20250925210125.png]]

>NOTE : General JS can also make micro updates like ReactState but ReactState makes it easier.

- If we just create the same object with same internal state and pass that as update to the ReactState of some object then it will be updated in virtual DOM but since on comparing to the DOM state their is no visible change so this update will not be pushed to the actual DOM.
- Virtual DOM is asynchronous update so their could be stale value as it updates the actual DOM in batch later.
- So updates are pushed in next cycle instead of pushing them immediately.
- DOM update in case of browser is equivalent to component re- render.

# How to Create a button component

![[Pasted image 20250925215128.png|400]]
- If i want to use same style on dislike button then  i have to again copy the styling and then use method

![[Pasted image 20250925220249.png|400]]
- Here i can use same component Button for dislike and like , i can pass the name of button and function to call which makes it cleaner.
- If props update then component re-renders.


![[Pasted image 20250927103623.png]]

![[Pasted image 20250927103635.png|200]]

![[Pasted image 20250927103642.png|200]]

### Problems
- When components method are called outside of component
- When parent component re-renders then it removes it's child and re-renders them.


# State vs JS

![[Pasted image 20250927105903.png|300]]
![[Pasted image 20250927105818.png|300]]
- Re-renders whole div with `dynamicTextNode` ID.
![[Pasted image 20250927105932.png|400]]
- Re-renders only the variable liked. To understand how React do that understand Diffing algorithm 

> DOM uses Diffing algorithm to compare virtual DOM.

![[Pasted image 20250927124242.png|300]]

# Hooks
- In react we don't call methods in global scope although it works functionality wise but it leads to little performance issue as global function gets called again while re-rendering in DOM. So always use Hooks to call the function in React.
- React hooks are basically methods or function which are used to update the state of function or change dynamic behavior of component . It's a way that enable developer to interact with the component. `use State` is an inbuilt hook in React.
- Hooks are methods or functions provided by  react used to look into the states of components also allows to induce and inject custom behavior when react component is rendering, re-rendering, un mounting.
- It can also be flushed out of memory.
- Example : `useState()` , `useEffect()`


#### `useEffect()`
- It takes two parameters.
	- 1st parameter is a function. Decides what to do.
		![[Pasted image 20250927111818.png|200]]

	- 2nd parameter is an array. Decides when to do. It has 3 variations
		![[Pasted image 20250927111638.png]]
		- Why we need empty array use effect
			![[Pasted image 20250927112443.png]]
			It is done so that function is called only once if our use case needs that otherwise if we use function call then that will happen each time component gets updated but with empty array `useEffect()` it runs for first time only to setup initial state.


![[Pasted image 20250927121335.png|300]]
![[Pasted image 20250927120259.png|300]]

- Managing list is tricky in React. Like if you want to perform sorting on data, deletion of data then that become challenging.
- To manage list we must use key to map the records. Key can be based on database key or create some group of name and index.
- Don't use that value in index which is getting updated.
- Do not remove the element and re insert the element
- Always when you rendering a list use map for records lookups.
![[Pasted image 20250927122045.png]]

Study about hide element vs remove element in react.
Topics covered
![[Pasted image 20250927123318.png|300]]

- Using React , does client side rendering which can hang the browser. To prevent it Server side rendering is the way to go.
- For Server Side rendering , server components were added to React.
- Then React did partnership with `NextJS` which has introduced various Server Side Rendering capabilities to React. Similarly there are frameworks that you can pair up with React like `Vite`

```jsx
React.useEffect(() => {
    // fetch the backend data
    const data = fetchData();
    initialLikesCount = data
    // return () => {}; // cleanup function
  }, []);
  function fetchData() {
    // code to fetch data from backend
  }
  fetchData(); // This will lead fetchData functiion being called on every re-render
  // let likes =20; // This will lead initilization of likes to 20 on every re-render
  // ---------------------------------------------------------

  // Array with dependencies
  React.useEffect(() => {
    // send liked data backend
  }, [liked]);
```


# `useRef()`
- It is used to create global variable which are local to component.
- If store this in variable then that variable stores the reference to data passed inside `useRef()`.
- Use variable as const in `useRef` to preserve the reference during successive re-render.


# Usability issue
> In react if you are like reversing an array but since it's reference remains same so for react DOM their is no change so you need to destructor the array using spread operator which creates a new array and then reverse that.

# Performance issue and usability issue
> If we change the key in react than react removes that key and creates a new key and renders it again due to which you loose your data.

# Best use of both performance and usability issue.
>If you give key property properly then it always works as required. So key should not be index and should not change over time and uniquely identify the element in all situations.


# How to pass data from child back to parent without using React
- Method 1: return the data from child to parent. But this doesn't work every time especially in asynchronous environment.
- Method 2: use callback function to get the data as follows.

```js
function foo1() {
  let x = 20;
  let rValue;
  foo2(x, innerCallBack);
  function innerCallback (arg) {
    rValue = arg; // recieved the result from child
  }
}
function foo2(arg1, innerCallBack) {
  console.log(arg1);
  innerCallBack(arg1 + 23);
}
```


# More uses of react

- We can share data among components by sending the data to parent by callbacks and then using props we can send it to other components.
- We make use of concept of centralized state where states of all components is stored at centralized state.


# State Management
- Redux
	- latest version Redux Toolkit  which is wrapper over wrapper
	- So to pass data without props another way is to have a shared global object which is kind of what redux do.