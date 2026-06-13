- Important for OA.
- It is used in dynamic graphs which keep on changing.
- In constant time you can know whether two nodes are part of same component or not.
- It's used on undirected graph and you don't actually need to store edges from both directions, just one direction is enough.
- Two functionalities of Disjoint Set:
	- **Find(u)** → finds the "ultimate parent" (representative) of `u`.
		- Implemented with **path compression**.
	- **Union(u, v)** → merges two sets.
		- It means finding if u and v belongs to same component or not.
		- Uses **union by rank/size**.


# Why Disjoint Set Required?
If we want to find whether two nodes are in the same components or not then it would require traversal of whole graph in worst case using algorithms like BFS and DFS.
![[Pasted image 20250913180439.png|300]]

But if we ask the same question from disjoint set then the answer is gonna be Yes/ No in **constant time**.


# What is Dynamic Graph
About [[Dynamic Graph]]
- So, it's a graph whose structure changes over time.
- Like suppose initially all nodes are disconnected and we start building graph edge by edge then problem can state to stop at any time in between this process and tell whether two nodes are in same component or not and the answer should be done in constant time.


# How to find Union in Disjoint Set

### Using Rank Method
- We are going to use two types of arrays:
	- Rank array
	- Parent array
- Size of rank and parent array is equal to number of nodes for 0-based indexing or V+1 for 1-based indexing.
- The definition of parent is going to change as we follow this process. 
Step 1: Initialize whole parent array with parent itself as it's element. 
Step 2: Find ultimate parent of u & v, let's say pu and pv.
Step 3: Find the rank of pu and pv.
Step 4: Connect smaller rank node to larger rank node always, in case of equality you can connect any one.
>Note : Why connecting to larger rank, this is because we want the depth to be lesser so connecting smaller depth graph to larger ensures recursive depth remains less while finding parent.

Step 5: When doing this if the rank of both is same then increment the rank of the node to which other node is connected because the depth is increased now.
Step 6: Now perform **Compression of path's** by setting the ultimate parent of new connected node to parent of the node to which it got connected. This will ultimately point to root of tree. 

>Note : Without Compression of paths time complexity to find ultimate parent increases upto O(log N). Also when we compress the path we don't reduce the rank bcz if some other branch of tree has the same depth then while taking union of some element of that branch will take the wrong rank in consideration and might connect larger graph  to smaller graph based on depth.
![[Pasted image 20250913230429.png|300]]
Step 7: If now Union of (u, v) is asked then just see in parent array if there ultimate parent or root is same or not in O(1).

![[Pasted image 20250913223929.png]]

#### Time Complexity (acc. to Striver)
- To find parent is O(4α) == O(constant)
- To find union is O(4α) == O(constant)


# Complexity to find parent why not constant

### 🔹 Complexity of `Find` with Path Compression

- Without path compression, the worst-case depth of a tree can be `O(n)`.
- With **path compression**, the tree height flattens drastically over time.
- The amortized time per operation becomes **O(α(n))**, where:
    - `α(n)` is the **inverse Ackermann function**. 
    - For all practical input sizes (even `n` up to the number of atoms in the universe), `α(n) ≤ 5`.    

So yes — technically, it’s **not constant time** in the strict sense.  
But since `α(n)` grows slower than log, slower than constant factors, and is bounded by ~5, we treat it as **“almost constant”**.

### 🔹 Complexity of `Union`

- `Union(u, v)` calls two finds: `Find(u)` and `Find(v)`.
- With path compression + union by rank/size, it’s also **O(α(n)) amortized**.
### 🔹 Intuition

- Recursive path compression _looks expensive_, but the recursion depth is logarithmic in worst-case _before compression_.
- After compression, every node directly links to the root in subsequent finds.
- So over many operations, the average time per find becomes nearly constant.

---


# How to do path compression

![[Pasted image 20250913224634.png]]
- We keep visiting the parent of node until node is parent of itself.

>Using rank we are unable to get correct height (or depth) of graph  due to some distortion therefore another approach is **Union by Size**




### Implementation

```java
import java.util.*;
public class Main{
  static class DisjointSet {
    int[] parent, rank;
    DisjointSet(int n) {
      parent = new int[n+1];
      rank = new int[n+1];
      for (int i = 0; i <= n; i++) {
        parent[i] = i;
      }
    }
    
    public int findUParent(int node) {
      if (parent[node] ==  node) return node;
      return parent[node] = findUParent(parent[node]);
    }
    
    public void Union(int u, int v) {
      int up = findUParent(u);
      int vp = findUParent(v);
      
      if (rank[up] > rank[vp]) {
        parent[vp] = up;
      }
      else if (rank[up] < rank[vp]) {
        parent[up] = vp;
      } else {
        parent[vp] = up;
        rank[up]++;
      }
    }
  }
  public static void main(String[] args) {
    DisjointSet ds = new DisjointSet(7);
    ds.Union(1, 2);
    ds.Union(2, 3);
    ds.Union(4, 5);
    ds.Union(6, 7);
    ds.Union(5, 6);
    
    if (ds.findUParent(3) == ds.findUParent(7)) {
	  System.out.println("Same");
	} else {
	  System.out.println("Not Same");
	}
	ds.Union(3, 7);
	if (ds.findUParent(3) == ds.findUParent(7)) {
	  System.out.println("Same");
	} else {
	  System.out.println("Not Same");
	}
  }
}
```

# Union by Size
- Here instead of rank we use size.
- Size of graph means how big it is which means number on nodes connected in it.
- So basically size mean number of nodes in a component or subcomponent.
- If node is like the root then it's size will be the size of component and nodes connected to it will store the size of sub components.

![[Pasted image 20250913232124.png|400]]

- Compression of path is also done here
![[Pasted image 20250913232206.png|400]]

### Implementation

```java
import java.util.*;
public class Main{
  static class DisjointSet {
    int[] parent, size;
    DisjointSet(int n) {
      parent = new int[n+1];
      size = new int[n+1];
      for (int i = 0; i <= n; i++) {
        parent[i] = i;
        size[i] = 1;
      }
    }
    
    public int findUParent(int node) {
      if (parent[node] ==  node) return node;
      return parent[node] = findUParent(parent[node]);
    }
    
    public void Union(int u, int v) {
      int up = findUParent(u);
      int vp = findUParent(v);
      
      if (size[up] < size[vp]) {
        parent[up] = vp;
        size[vp] += size[up];
      } else {
        parent[vp] = up;
        size[up] += size[vp];
      }
    }
  }
  public static void main(String[] args) {
    DisjointSet ds = new DisjointSet(7);
    ds.Union(1, 2);
    ds.Union(2, 3);
    ds.Union(4, 5);
    ds.Union(6, 7);
    ds.Union(5, 6);
    
    if (ds.findUParent(3) == ds.findUParent(7)) {
	  System.out.println("Same");
	} else {
	  System.out.println("Not Same");
	}
	ds.Union(3, 7);
	if (ds.findUParent(3) == ds.findUParent(7)) {
	  System.out.println("Same");
	} else {
	  System.out.println("Not Same");
	}
  }
}
```