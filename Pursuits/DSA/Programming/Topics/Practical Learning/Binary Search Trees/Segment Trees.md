- In a segment trees we are generally dealing with ranges or segments which are provided to us in an array.
- Imagine the array as the base of the tree meaning each element of array is leaf node.
- Space needed to build segment tree is the total number of nodes in the tree.
- In ideal case, lets take perfect binary tree ,  leaf nodes are in order of 2^k  (ex: 2, 4, 8, 16 ...) . So in this case total nodes are 2 \* leaf nodes - 1. So we need 2\*n-1 space to store the segment tree.
- But not all trees are perfect so one way to get the space needed to build segment tree is to take nearest greater power of 2 to that number. Like if array is of size 6, means 6 leaf nodes are there then take 8 which is nearest power of 2 for 6. Now as per 8, total nodes will considered to be 2\*8 - 1 = 15.
- But why to take so much overhead so we have generalized above step for calculating the sufficient space to accommodate segment tree build from any size of array which is 4\*n where n is the number of leaf nodes.
	[[Reasoning of Segment Tree Space]]


# Problems
- [[3719. Longest Balanced Subarray I]]
- [[303. Range Sum Query - Immutable]]
- [[307. Range Sum Query - Mutable]]
- [[2080. Range Frequency Queries]]
- [[732. My Calendar III]]
- [[673. Number of Longest Increasing Subsequence]]




# Segment Tree Recursive Code

```java
package SegmentTree;
public class SegmentTree {
  private int[] segTree;
  private int[] arr;
  private int n;

  SegmentTree(int[] arr) {
    this.n = arr.length;
    this.arr = arr;
    segTree = new int[4*n];
    buildTree(1, 0, n-1);
  }

  private void buildTree(int node, int L, int R) {
    if (L == R) {
      segTree[node] = arr[L];
      return;
    }

    int mid = L + (R-L)/2;
    buildTree(node * 2, L, mid);
    buildTree(node * 2 + 1, mid+1, R);

    segTree[node] = segTree[node * 2] + segTree[node * 2 + 1];
  }
  
  public int query(int L, int R) {
    return rangeQuery(1, 0, n-1, L, R);  
  }

  private int rangeQuery(int node, int L, int R, int i, int j) {
    if (j < L || R < i) {
      return 0;
    }

    if (i <= L && R <= j) {
      return segTree[node];
    }
    
    int mid = L + (R-L)/2;
    int s1 = rangeQuery(node * 2, L, mid, i, j);
    int s2 = rangeQuery(node * 2 + 1, mid+1, R, i, j);
    return s1 + s2;
  }

  public void update(int idx, int val) {
    updateTree(1, 0, n-1, idx, val);
  }

  private void updateTree(int node, int L, int R, int idx, int val) {
    if (L == R) {
      arr[idx] = val;
      segTree[node] = val;
      return;
    }
    int mid = L + (R-L)/2;
    if (L <= idx && idx <= mid) {
      updateTree(2 * node, L, mid, idx, val);
    } else {
      updateTree(2 * node + 1, mid+1, R, idx, val);
    }
    segTree[node] = segTree[2 * node] + segTree[2 * node + 1];
  }

  public int[] getUpdatedArray() {
    return this.arr;
  }
}
```


***Time complexity:*** O(N)

- The building operation takes O(N) time
- The query operation takes O(logN) time
- Each update is performed in O(logN) time
***Auxiliary Space:*** O(n)

A segment tree with 2^x leaf nodes will have 2^(x+1)-1 total nodes due to its perfect binary tree structure. However, when dealing with a non-power-of-two number of elements, extra leaf nodes may be present. To represent all elements, the number of leaf nodes must be rounded up to the nearest power of two, resulting in a maximum of almost 2*n leaf nodes.

For instance, if n is 2^j + 1, 2^(j+1) leaf nodes will be required, leading to an O(2*n) space complexity. As the total number of nodes is about twice the number of leaf nodes, the total space complexity of the segment tree is O(4n). The space requirement can be substantial, but it is usually manageable for most practical applications.


Next stage is learning about Lazy Updation in segment trees using additional lazy array. This is better if a lot of updates are being made and data is fetched rarely.