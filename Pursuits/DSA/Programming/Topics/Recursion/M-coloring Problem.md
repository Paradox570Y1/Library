[Link](https://www.geeksforgeeks.org/problems/m-coloring-problem-1587115620/1)
### M-Coloring Problem

Difficulty: **Medium**Accuracy: **34.42%**Submissions: **142K+**Points: **4**

You are given an undirected graph consisting of **`v`** vertices and a list of **edges**, along with an integer **`m`**. Your task is to determine whether it is possible to color the graph using at most `m` different colors such that no two adjacent vertices share the same color. Return `true` if the graph can be colored with at most `m` colors, otherwise return `false`.  

**Note:** The graph is indexed with 0-based indexing.

**Examples:**

**Input:** v = 4, edges[] = [(0,1),(1,2),(2,3),(3,0),(0,2)], m = 3
**Output:** true
**Explanation:** It is possible to color the given graph using 3 colors, for example, one of the possible ways vertices can be colored as follows:
Vertex 0: Color 3
Vertex 1: Color 2
Vertex 2: Color 1
Vertex 3: Color 2

**Input:** v = 3, edges[] = [(0,1),(1,2),(0,2)], m = 2
**Output:** false  
**Explanation:** It is not possible to color the given graph using only 2 colors because vertices 0, 1, and 2 form a triangle.

**Expected Time Complexity:** O(mV)  
**Expected Auxiliary** **Space:** O(v2)

**Constraints:**  
1 ≤ v ≤ 20  
1 ≤ edges.size() ≤ (v*(v-1))/2  
0 ≤ edges[i][j] ≤ n-1  
1 ≤ m ≤ v


# Brute
**Time Complexity: O( N^M) (n raised to m)**
**Space Complexity: O(N)**

```java
class Solution {
    boolean possible(int vertex,int col,List<int[]> edges,int[] colour){
        for(int i=0;i<edges.size();i++){
            if(edges.get(i)[0] == vertex){
                int connected_vertex = edges.get(i)[1];
                if(colour[connected_vertex]== col)return false;
            }
            if(edges.get(i)[1] == vertex){
                int connected_vertex = edges.get(i)[0];
                if(colour[connected_vertex]== col)return false;
            }
        }
        return true;
    }
    boolean color(int n,int i,List<int[]> edges,int m,int[] colour){
        if(i==n)return true;
        for(int c=1;c<=m;c++){
            if(possible(i,c,edges,colour)){
                colour[i] = c;
                if(color(n,i+1,edges,m,colour))return true;
                colour[i] = 0;
            }
        }
        return false;
    }
    boolean graphColoring(int v, List<int[]> edges, int m) {
        // code here
        return color(v,0,edges,m,new int[v]);
    }
}
```


```java
class Solution {
    boolean graphColoring(int v, List<int[]> edges, int m) {
        // code here
        return helper(v,edges,m,0,new int[v]);
    }
    boolean helper(int v, List<int[]> edges, int m,int i,int[] hash){
        if(i==v)return true;
        for(int c=1;c<=m;c++){
            if(isSafe(i,edges,c,hash)){
                hash[i] = c;
                if(helper(v,edges,m,i+1,hash))return true;
                hash[i] = 0;
            }
        }
        return false;
    }
    boolean isSafe(int v,List<int[]> edges,int color,int[] hash){
        for(int i=0;i<edges.size();i++){
            if(edges.get(i)[0] == v){
                if(hash[edges.get(i)[1]] == color)return false;
            }
            if(edges.get(i)[1] == v){
                if(hash[edges.get(i)[0]] == color)return false;
            }
        }
        return true;
    }
    
}
```