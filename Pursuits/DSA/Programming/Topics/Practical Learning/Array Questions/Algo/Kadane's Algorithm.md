Kadane's algorithm is an efficient method for finding the maximum sum of a contiguous subarray within a one-dimensional array of numbers, which can contain both positive and negative numbers. It runs in O(n) time complexity, where n is the number of elements in the array. Here's a step-by-step explanation:

### Steps of Kadane's Algorithm:

1. **Initialization**:
    
    - Start by initializing two variables: `max_current` and `max_global`. Set both to the first element of the array.
    
    cpp
    
    Copy code
    
```java
int max_current = array[0]; 
int max_global = array[0];
```
    
2. **Iterate through the array**:
    
    - Iterate through the array starting from the second element.
    - For each element, update `max_current` to be the maximum of the current element itself and the sum of `max_current` and the current element. This decision determines whether to start a new subarray at the current element or to continue the existing subarray.
```cpp
for (int i = 1; i < n; i++) {     
	max_current = max(array[i], max_current + array[i]);     
	if (max_current > max_global) {         
		max_global = max_current;     
} }
```
    
3. **Update the global maximum**:
    
    - After updating `max_current`, check if it's greater than `max_global`. If it is, update `max_global` to `max_current`.
    
    This ensures that `max_global` always contains the maximum sum of any subarray found so far.
    

### Example:

Consider the array `[-2, 1, -3, 4, -1, 2, 1, -5, 4]`.

1. Initialize:
    
    - `max_current = -2`
    - `max_global = -2`
2. Iterate through the array:
    
    - At `i = 1`: `max_current = max(1, -2 + 1) = 1`; `max_global = max(-2, 1) = 1`
    - At `i = 2`: `max_current = max(-3, 1 - 3) = -2`; `max_global = max(1, -2) = 1`
    - At `i = 3`: `max_current = max(4, -2 + 4) = 4`; `max_global = max(1, 4) = 4`
    - At `i = 4`: `max_current = max(-1, 4 - 1) = 3`; `max_global = max(4, 3) = 4`
    - At `i = 5`: `max_current = max(2, 3 + 2) = 5`; `max_global = max(4, 5) = 5`
    - At `i = 6`: `max_current = max(1, 5 + 1) = 6`; `max_global = max(5, 6) = 6`
    - At `i = 7`: `max_current = max(-5, 6 - 5) = 1`; `max_global = max(6, 1) = 6`
    - At `i = 8`: `max_current = max(4, 1 + 4) = 5`; `max_global = max(6, 5) = 6`
3. The maximum sum of a contiguous subarray is `6`.
    

### Summary

Kadane's algorithm efficiently finds the maximum sum subarray by iterating through the array once and keeping track of the current and global maximum sums. This makes it suitable for large arrays due to its linear time complexity.