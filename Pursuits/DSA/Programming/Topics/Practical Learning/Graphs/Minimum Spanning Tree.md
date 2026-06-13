- Short-form MST
- It is used on undirected weighted graphs:
	- Weights can be same as well as different.
- A tree is called a spanning tree if  it has N nodes and N-1 edges and all nodes are reachable from each other.
	![[Pasted image 20250912184023.png|200]]

Below is the example on how a graph can be converted into a spanning tree in different ways.

![[Pasted image 20250912184307.png|400]]
![[Pasted image 20250912184349.png|400]]


###### Now what is a Minimum Spanning Tree?
- Among all the different ways to convert a graph into a spanning tree, the way which gives you sum of weights of edges to be the minimum then that is a MST.
	Like for below example MST is a spanning tree with sum of 16
	![[Pasted image 20250912184641.png|400]]

###### Conclusion
- A graph can have many number of spanning tree.
- But MST is those spanning tree which has the minimum weight sum, they could also be more than one.

![[Pasted image 20250912185108.png|400]]


### How to find MST using Algorithm?
- Following are the algorithms suited for the job:
	- [[Prim's Algorithm]]
	- [[Kruskal's Algorithm]]