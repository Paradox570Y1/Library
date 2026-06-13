JavaScript is single-threaded and **non-blocking**, meaning you can’t just pause execution like in Python (`time.sleep`) or Java (`Thread.sleep`).  
If you try to block execution, the whole event loop freezes.

Instead, we simulate **sleep** using `Promise` with `setTimeout`. This lets the program wait asynchronously without blocking other code.

🔹 Example: Sleep with `Promise`
```js
function sleep(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

// Usage
sleep(2000).then(() => {
  console.log("Woke up after 2 seconds!");
});

```

Here’s what happens:

1. `sleep(2000)` returns a `Promise`.
    
2. Inside, `setTimeout` calls `resolve` after `2000 ms`.
    
3. The `.then()` runs when the promise resolves.


🔹 With `async/await` (Cleaner Way)
```js
function sleep(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function demo() {
  console.log("Start");
  await sleep(3000);  // pauses only this function
  console.log("3 seconds later...");
}

demo();
```

The `await` keyword makes the code _look synchronous_, but it still doesn’t block the entire program — only the `async` function.


### Real-World Use Cases

1. **Rate limiting** → Wait between API calls:

```js
for (let i = 0; i < 5; i++) {
  await sleep(1000);
  console.log(`API call ${i+1}`);
}

```

2. **Retry logic** → Pause before retrying a failed request.
3. **Animations** → Add delay between animation steps.
4. **Testing** → Simulate async operations.


