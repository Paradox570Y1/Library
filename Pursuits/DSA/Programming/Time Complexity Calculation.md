The recurrence relation T(n)=2T(n/2)+n is a classic divide-and-conquer recurrence. We can solve it using the **Master Theorem** or the **substitution method** to find the asymptotic complexity.

# Using Tree Algorithm
![[Pasted image 20241210190947.png]]


### Using Master Theorem

The general form of Master Theorem is:

![[Pasted image 20241210181313.png|200]]


Where:

- a: the number of subproblems
- b: the factor by which the problem size is divided
- f(n): the cost outside the recursive calls


![[Pasted image 20241210181418.png|300]]


# Derivation

![[Pasted image 20241210183632.png|500]]
![[Pasted image 20241210183650.png|500]]
![[Pasted image 20241210183720.png|500]]



### Explanation


This means the recurrence describes an algorithm with time complexity O(nlog⁡n)
, like **merge sort**.