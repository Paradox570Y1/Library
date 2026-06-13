[Link](https://www.hackerearth.com/practice/data-structures/disjoint-data-strutures/basics-of-disjoint-data-structures/practice-problems/algorithm/disjoint-set-union/)

Problem

You are given number of nodes, _N_, and number of edges, _M_, of a undirected connected graph. After adding each edge, print the size of all the connected components (in increasing order).

**Input:**  
First line contains two integers, _N_ and _M_, number of nodes and number of edges.  
Next _M_ lines contains two integers each, _X_ and _Y_, denoting that there is an edge between _X_ and _Y_.

**Output:**  
For each edge, print the **size of all the connected components (in increasing order)** after adding that edge.

**Constraints:**  
  
  

Sample Input

[](https://he-s3-ap-south-1.s3.amazonaws.com/media/hackathon/question-for-new-practice-section/problems/951f589a-0-sample-input-951eb74.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA6I2ISGOYMPJGUFGY%2F20250913%2Fap-south-1%2Fs3%2Faws4_request&X-Amz-Date=20250913T175548Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=aabd4cdbf9b0d4cb9bc6782a11f055658ffd2dde631225b57a3de31b3ffb0a1d "Download")

5 4
1 2
3 4
4 5
1 3

Sample Output

[](https://he-s3-ap-south-1.s3.amazonaws.com/media/hackathon/question-for-new-practice-section/problems/9fb9c272-0-sample-output-9fb9261.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA6I2ISGOYMPJGUFGY%2F20250913%2Fap-south-1%2Fs3%2Faws4_request&X-Amz-Date=20250913T175549Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=fd6a4099314697aec1b8c313181cdb5f099698598f2321b3293f1c1cc0eccb1e "Download")

1 1 1 2
1 2 2
2 3
5

Time Limit: 1

Memory Limit: 256

Source Limit:

Explanation

After adding first edge the connected components are [1, 2], 3, 4, 5 and their sizes are 1, 1, 1, 2.  
After adding second edge the connected components are [1, 2], [3, 4], 5 and their sizes are 1, 2, 2.  
After adding third edge the connected components are [1, 2]. [3, 4, 5] and their sizes are 2, 3.  
After adding the fourth edge the connected component is [1, 2, 3, 4, 5] and its size is 5 .




```java
import java.io.*;
import java.util.*;
class TestClass {
    static class DisjointSet {
        int[] parent, size;
        DisjointSet(int N) {
            size = new int[N+1];
            parent = new int[N+1];
            for (int i = 0; i <= N; i++) {
                parent[i] = i;
                size[i] = 1;
            }
            size[0] = 0;
        }

        public int findUParent(int node) {
            if (node == parent[node]) return node;
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

        public void printSizeOfComponents() {
            List<Integer> res = new ArrayList<>();
            for (int i = 1; i < parent.length; i++) {
                if (parent[i] == i) {
                    res.add(size[i]);
                }
            }
            Collections.sort(res);
            for (int ele : res) {
                System.out.print(ele + " ");
            }
            System.out.println();
        }
    }
    public static void main(String args[] ) throws Exception {
        //BufferedReader
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(st.nextToken());
        int M = Integer.parseInt(st.nextToken());
        
        DisjointSet ds = new DisjointSet(N);
        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int u = Integer.parseInt(st.nextToken());
            int v = Integer.parseInt(st.nextToken());
            ds.Union(u, v);
            ds.printSizeOfComponents();
        }
    }
}

```

OR

```java
import java.io.BufferedReader;
import java.util.StringTokenizer;
import java.io.InputStreamReader;
import java.lang.Integer;
class TestClass {
    static class Dsu {
        private int[] parent, size;
        Dsu(int V) {
            parent = new int[V+1];
            size = new int[V+1];
            for (int i = 0; i < V+1; i++) {
                parent[i] = i;
                size[i] = 1;
            }
        }

        private int find(int node) {
            if (parent[node] == node) return node;
            return parent[node] = find(parent[node]);
        }

        public void union(int u, int v) {
            int pu = find(u);
            int pv = find(v);
            if (size[pu] > size[pv]) {
                parent[pv] = pu;
                size[pu] += size[pv];
            } else {
                parent[pu] = pv;
                size[pv] += size[pu];
            }
        }

        public void printConnectedComponents() {
            int hash[] = new int[size.length];
            for (int v = 1; v < size.length; v++) {
                if (parent[v] == v) {
                    hash[size[v]]++;
                }
            }
            for (int i = 1; i < hash.length; i++) {
                while (hash[i] != 0) {
                    System.out.print(i + " ");
                    hash[i]--;
                }
            }
            System.out.println();
        }
    }
    public static void main(String args[] ) throws Exception {
        BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer token = new StringTokenizer(reader.readLine());
        int N = Integer.parseInt(token.nextToken());
        int M = Integer.parseInt(token.nextToken());

        Dsu dsu = new Dsu(N);
        for (int e = 0; e < M; e++) {
            token = new StringTokenizer(reader.readLine());
            int u = Integer.parseInt(token.nextToken());
            int v = Integer.parseInt(token.nextToken());
            if (dsu.find(u) != dsu.find(v)) {
                dsu.union(u, v);
                dsu.printConnectedComponents();
            }
        }
    }
}

```