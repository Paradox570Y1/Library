**Basic Syntax**
```js
var set1 = new Set([5, 4, 3, 6]);
```

- Set are Objects where elements are in the form of array.
	![[Pasted image 20250913101512.png|200]]
- It has `Entries` property which stores elements in form of array.
- Used if we want to create an array of unique elements.
- Set returns an iterator.
- 

**Operations in JS**
```js
// Create a new empty Set
let mySet = new Set();

// Create a Set with initial values
let mySet2 = new Set([1, 2, 3, 4]);

// Add an element to Set
mySet.add(10);

// Add multiple values (chainable)
mySet.add(20).add(30);

// Delete an element from Set
mySet.delete(10);

// Check if an element exists
mySet.has(20);  // true or false

// Get the size of Set
mySet.size;  

// Clear all elements from Set
mySet.clear();

// Iterate over values using for...of
for (let val of mySet) {
  console.log(val);
}

// Iterate using forEach
mySet.forEach((val) => console.log(val)); //important

// Convert Set to Array
let arr = Array.from(mySet);

// Spread Set into Array
let arr2 = [...mySet];

// Remove duplicates from Array using Set
let uniqueArr = [...new Set([1, 2, 2, 3, 4, 4])];

// Convert Array back to Set
let setFromArr = new Set([1, 2, 3]);

// Get Set values iterator
let values = mySet.values();

// Get Set keys iterator (same as values for Set)
let keys = mySet.keys();

// Get Set entries iterator [value, value]
let entries = mySet.entries();

// Example: Using entries()
for (let [key, value] of mySet.entries()) {
  console.log(key, value); // key === value
}

```




# Map in java


```js
var map = new Map([
    ["fname", "name1"]
]);
console.log(map);
```

### 🔑 Core Features of `Map`

1. **Stores key–value pairs** → Each key maps to a value.
2. **Any type of key allowed** → Unlike objects (where keys are strings/symbols), a `Map` can use objects, functions, or primitives as keys.
3. **Insertion order preserved** → Iteration happens in the order items were inserted.
4. **Size property** → `map.size` gives the total number of entries.
5. **Efficient lookups** → Optimized for frequent additions and retrievals.


![[Pasted image 20250913103219.png|300]]


**Methods and properties of Map**

```js
let map = new Map();

// Add entries
map.set("a", 1);           // key = "a", value = 1
map.set(2, "two");         // key = number
map.set({}, "object");     // key = object

// Get value
map.get("a");              // 1

// Check existence
map.has(2);                // true

// Delete entry
map.delete("a");           // removes key "a"

// Size of map
map.size;                  // 2

// Clear all entries
map.clear();

// Iteration
for (let [key, value] of map) {
  console.log(key, value);
}

// Iterate over keys
for (let k of map.keys()) console.log(k);

// Iterate over values
for (let v of map.values()) console.log(v);

// Iterate over entries
for (let [k, v] of map.entries()) console.log(k, v);

// forEach
map.forEach((value, key) => console.log(key, value));

```