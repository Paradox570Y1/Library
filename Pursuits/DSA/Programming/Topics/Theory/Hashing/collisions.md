![[Pasted image 20240705121418.png|500]]
- Division Method in hashing
- In case all elements have different remainders.
![[Pasted image 20240705121515.png|400]]

- If remainders are same we use **_Linear Chaining_** the element to the same index.
- In order to find the input element in a chain techniques like Binary Search is used.
  ![[Pasted image 20240705121751.png|600]]

  - If all elements have same remainder.
	  - Then all elements will be chained on a single index.
	  - Which means TC in worst case => O(N)
	  - In this way we got O(N) TC in worst case of Unordered_map
   ![[Pasted image 20240705122026.png|400]]
