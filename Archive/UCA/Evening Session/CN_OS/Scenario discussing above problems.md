The simplest example is a **website visit counter**.

Imagine a popular website with a global counter variable, `totalVisits`, which is currently **1000**.

- **Shared Data:** `totalVisits = 1000`
    
- **Thread A:** A user from New York visits.
    
- **Thread B:** A user from London visits at the exact same time.
    

Both threads need to perform the same operation: `totalVisits = totalVisits + 1`. This operation is not one step; it's three:

1. **Read** the current value (1000).
    
2. **Calculate** the new value (1000 + 1 = 1001).
    
3. **Write** the new value (1001) back.
    

---

### 1. Race Conditions

A **race condition** is the _situation_ where the final outcome depends on the unpredictable, specific order in which the threads' steps are interleaved. The threads are "racing" to write their results.

Here is the "bad" interleaving:

1. **Thread A (Read):** Reads `totalVisits`. (Sees 1000)
    
2. **Thread B (Read):** Reads `totalVisits`. (Also sees 1000, because A hasn't written anything yet!)
    
3. **Thread A (Calculate):** Calculates its new value: 1000 + 1 = 1001.
    
4. **Thread B (Calculate):** Calculates _its_ new value: 1000 + 1 = 1001.
    
5. **Thread A (Write):** Writes **1001** to `totalVisits`.
    
6. **Thread B (Write):** Writes **1001** to `totalVisits`.
    

The final value of `totalVisits` is **1001**. It should have been **1002**. This race condition has now caused all the other problems.

---

### 2. Lost Updates

This is the _result_ of the race condition.

- Thread A's update (writing 1001) was successful.
    
- Thread B's update (also writing 1001) immediately overwrote Thread A's value.
    

Because both threads started from the same initial value (1000), one of the "plus one" operations was completely lost. **Thread A's update was lost.**

---

### 3. Inconsistent State

This is the _description_ of the data _after_ the lost update.

The program's data is now in an **inconsistent state**. The `totalVisits` variable (1001) no longer matches the reality of how many people actually visited (2). The state of the data is wrong and does not reflect the sum of all operations performed on it.

---

### 4. Corrupted Objects

This is a more severe form of inconsistent state. While a wrong number is an inconsistent state, a **corrupted object** is often one that is left _structurally_ damaged or internally contradictory.

Let's use a slightly different example: an object that manages a list of logged-in users.

```
userListObject = {
  count: 2,
  users: ["Alice", "Bob"]
}
```

- **Thread A:** Tries to add "Charlie".
    
- **Thread B:** Tries to add "David" at the same time.
    

A race condition could happen where the steps get interleaved like this:

1. **Thread A:** Reads `count`. (Sees 2)
    
2. **Thread B:** Reads `count`. (Sees 2)
    
3. **Thread A:** Updates `users` array: `users` is now `["Alice", "Bob", "Charlie"]`.
    
4. **Thread B:** Updates `users` array: `users` is now `["Alice", "Bob", "Charlie", "David"]`.
    
5. **Thread A:** Calculates new count (2 + 1 = 3) and writes `count = 3`.
    
6. **Thread B:** Calculates new count (2 + 1 = 3) and writes `count = 3`.
    

**The object is now corrupted.** Its internal state is contradictory:

- `userListObject.count` is **3**.
    
- The _actual_ number of items in `userListObject.users` is **4**.
    

Any code that now trusts `userListObject.count` to loop through the array will either miss "David" or, in some languages, crash with an "index out of bounds" error. The object itself is broken. This is far worse than just a "lost update" because the object's fundamental integrity is compromised.