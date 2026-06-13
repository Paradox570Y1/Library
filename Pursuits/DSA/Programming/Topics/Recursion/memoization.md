### **What is Memoization?**

**Memoization** is an optimization technique used to improve the performance of recursive algorithms by storing the results of expensive function calls and reusing them when the same inputs occur again.

In simple terms:

- Instead of recalculating the result of a function for the same input multiple times, store the result the first time it is computed.
- When the function is called again with the same input, return the stored result instead of recalculating.

This technique is particularly useful for problems with **overlapping subproblems**, such as:

- Fibonacci sequence
- Word segmentation (like your problem)
- Dynamic programming problems

---

### **Key Concepts**

1. **Subproblem Overlap**:
    
    - Many recursive problems solve the same subproblem multiple times. Memoization ensures each subproblem is solved only once.
2. **Storage**:
    
    - Results are stored in a **data structure** such as a hash map (`Map` in Java) or an array.
3. **Time Complexity**:
    
    - Without memoization: O(2n)O(2^n)O(2n) for many problems.
    - With memoization: O(n)O(n)O(n) to O(n2)O(n^2)O(n2), depending on the problem.
4. **Space Complexity**:
    
    - Additional space is required to store results, but the trade-off is worth it for significant time savings.