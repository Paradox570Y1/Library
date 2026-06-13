### 1. The Problem Before Promises

Imagine you order food online 🍕.

- You place the order.
- The restaurant needs time to cook it.
- You don’t just sit idle staring at the phone, right? You continue watching Netflix.
- Once the food arrives, you eat.

In code, that’s called **asynchronous behavior**.

Before promises, JavaScript used **callbacks** to handle this. But callbacks can become messy (callback hell).

---

### 2. What a Promise Is

A **Promise** is like the **receipt** you get after placing your order.  
It says:

- "We’ve received your request."
- "We’ll let you know when it’s ready."

In JS terms, a promise is an **object** representing a task that may:

- ✅ _Fulfill_ (success → food delivered)
- ❌ _Reject_ (failure → order canceled)
- ⏳ _Pending_ (still cooking)


# Promise

[Resources](https://kaksha-dev.github.io/web/js/promises)
A Promise is an object created using Promise Constructor Function.
- It takes executor function as it's argument.
	- Executor function runs some logic and returns some value.
- They primarily have two properties
	- States  :
		- Pending
		- Fulfilled
		- Rejected
	- Result :
		- Any Valid Value
		- Undefined


# Simple Promise
- We pass a callback function
![[Pasted image 20250904210730.png|300]]

#### Simple Promise with resolve and reject

- Executor function is called immediately when promise is created.
- Executor function is called with 2 arguments of type function
	- resolve
	- reject

# Using resolve
![[Pasted image 20250904211028.png|250]]


# Using reject
![[Pasted image 20250904211300.png|250]]

### Example

![[Pasted image 20250904211559.png|280]]
![[Pasted image 20250904211726.png|280]]


## Functions in Promise

![[Pasted image 20250904211959.png]]
- It has two functions `.then` and `.catch`
- These functions accepts one argument which is callback function which is called either when promise is fulfilled or it is rejected.

![[Pasted image 20250904212526.png|300]]

- Promise is executed by separate browser  Web API, so to bring back the result from that browser API space to main codebase we require this complex implementation of Promise. 
- So using `.then` and `.catch` we get the exact result that was computed in different thread in the main thread.
- Promise does not directly expose the  value so using `.then` and `.catch` we can get value.
# Resolving Promise
![[Pasted image 20250904212612.png]]


# Rejected Promise
![[Pasted image 20250904212658.png|300]]
![[Pasted image 20250904212701.png]]



# Custom implementation of Promise

![[Pasted image 20250904220516.png|300]]

![[Pasted image 20250904220352.png|350]]



With resolve and reject
![[Pasted image 20250904220922.png]]

```js
function customPromiseExecutor(resolve, reject) {
  setTimeout(() => {
    resolve("Sample value");
    console.log("Inside promise executor function");
  }, 10000);
}

function PromiseCustom(executorFuncArg) {
  this.state = "pending";  
  let successCallbackCustom;
  let errorCallbackCustom;

  this.then = (arg1Callback) => {
    successCallbackCustom = arg1Callback
  };

  this.catch = (arg1Callback) => {
    errorCallbackCustom = arg1Callback
  };
  
  // Call the executor function
  executorFuncArg(
    (resolveResponseArg) => {
      this.state = "fulfilled";
      console.log(
        "Inside resolve function with return value as: ",
        responseArg
      );
      successCallbackCustom(resolveResponseArg)
    },
    (errorArg) => {
      this.state = "rejected";
      errorCallbackCustom(responseArg)
      console.log("Inside error function with error value as: ", errorArg);
    }
  );
}

var promiseCustom1 = new PromiseCustom(customPromiseExecutor);

promiseCustom1.then((someValue) => {
  responseValue = someValue;
});
```

- Things I understand from custom implementation of Promise:
	- It's nothing but a way of getting acknowledgement if the task is fulfilled or rejected.
	- Promise has method like `then` and `catch` which basically passes the function you define in these function's parameter to the scope which gets called after acknowledgement.
	- Basically `then` and `catch` is the exposed end points for developer  to pass a function which takes acknowledgement message as argument after the event has happened.