[Link](http://naukri.com/code360/problems/maximum-xor_973113)
## Problem statement

You are given two arrays of non-negative integers say ‘arr1’ and ‘arr2’. Your task is to find the maximum value of ( ‘A’ xor ‘B’ ) where ‘A’ and ‘B’ are any elements from ‘arr1’ and ‘arr2’ respectively and ‘xor’ represents the bitwise xor operation.

Detailed explanation ( Input/output format, Notes, Images )

**Constraints:**

```
1 <=  T  <= 5
1 <=  N, M <= 1000
0 <=  arr1[i], arr2[i]  <= 10 ^ 9

Where 'T' denotes the number of test cases, 'N', ‘M’ denotes the number of elements in the first array and second array, ‘arr1[i]', and ‘arr2[i]’ denotes the 'i-th' element of the first array and second array.

Time limit: 1 sec
```

#### Sample Input 1:

```
1
7 7
6 6 0 6 8 5 6
1 7 1 7 8 0 2
```

#### Sample Output 1:

```
15
```

#### Explanation of sample input 1:

```
First testcase:
Possible pairs are (6, 7), (6, 8), (6, 2), (8, 7), (8, 8), (6, 2). And 8 xor 7 will give the maximum result i.e. 15
```

#### Sample Input 2:

```
1
3 3
25 10 2
8 5 3
```

#### Sample Output 2:

```
28
```

#### Explanation of sample input 2:

```
First test case:
28 is the maximum possible xor given by pair = (25, 5). It is the maximum possible xor among all possible pairs.
```

![[Pasted image 20260205205322.png|400]]


![[Pasted image 20260205210145.png]]


![[Pasted image 20260205210427.png|400]]


![[Pasted image 20260205210708.png|400]]

![[Pasted image 20260205210931.png|300]]




```java

import java.util.ArrayList;

public class Solution 
{
	static class Node {
		Node[] links;
		Node() {
			links = new Node[2];
		}
		public boolean contains(int bit) {
			return links[bit] != null;
		}
		public Node get(int bit) {
			return links[bit];
		}

		public void put(int bit) {
			links[bit] = new Node();
		}
	}
	static class Trie{
		private Node root;
		Trie() {
			root = new Node();
		}

		public void insert(int num) {
			Node trav = root;
			for (int i = 31; i >= 0; i--) {
				int bit = (num >> i) & 1;
				if (!trav.contains(bit)) trav.put(bit);
				trav = trav.get(bit);
			}
		}

		public int getMax(int num) {
			int res = 0;
			Node trav = root;
			for (int i = 31; i >= 0; i--) {
				int bit = (num >> i) & 1;
				if (trav.contains(1-bit)) {
					res = res | (1<<i);
					trav = trav.get(1-bit);
				} else trav = trav.get(bit);
			}
			return res;
		}
	}
	public static int maxXOR(int n, int m, ArrayList<Integer> arr1, ArrayList<Integer> arr2) 
	{
	    // Write your code here.  
		Trie trie = new Trie();
		for (int ele : arr1) {
			trie.insert(ele);
		}
		int res = 0;
		for (int ele : arr2) {
			res = Math.max(res, trie.getMax(ele));
		}
		return res;
	}
}

```



