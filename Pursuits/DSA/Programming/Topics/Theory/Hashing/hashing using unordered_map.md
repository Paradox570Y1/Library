- In it key can be many data types like int, char, string, double but cannot have data types like pair etc.
- TC of unordered_map
	-  For fetching and storing in 
		- average and best case TC=> O(1)
		- worst case TC => O(N) , N is number of elements in map
    - Worst case will happen Once in a blue moon, if problem setup is extremely designed to fail it. 
    - Worst case very rarely happens because of internal [[collisions]].
- So most of the time use Unordered_map, if it gives TLE then switch back to map
![[Pasted image 20240705115505.png|500]]
![[Pasted image 20240705115522.png|100]]
- Order of element is random and is different for different compiler.