
[Link](https://www.naukri.com/code360/problems/k-th-largest-number_920438?leftPanelTabValue=PROBLEM)

# Using reverse in-order

```java
import java.util.ArrayList;

public class Solution {
	static int cnt=0;
	private static int desc(TreeNode<Integer> root,int k){
		if(root==null)return -1;
		int right = desc(root.right,k);
		if(right!=-1)return right;
		else if(++cnt==k)return root.data;
		int left = desc(root.left,k);
		if(left!=-1)return left;
		return -1;
	}
	public static int KthLargestNumber(TreeNode<Integer> root, int k) {
		// Write your code here.
		cnt=0;
		return desc(root,k);
	}
}
```


# Using smallest to find largest

```java
import java.util.ArrayList;

public class Solution {
	static int cnt=0;
	private static int desc(TreeNode<Integer> root,int k){
		if(root==null)return -1;
		int left = desc(root.left,k);
		if(left!=-1)return left;
		else if(++cnt==k)return root.data;
		int right = desc(root.right,k);
		if(right!=-1)return right;
		return -1;
	}
	public static int KthLargestNumber(TreeNode<Integer> root, int k) {
		// Write your code here.
		cnt=0;
		
		return desc(root,len(root)-k+1);
	}
	private static int len(TreeNode<Integer> root){
		if(root==null)return 0;
		return 1+len(root.left)+len(root.right);
	}
}
```


# Using iterate reverse pre order

```java

import java.util.ArrayList;

public class Solution {
	public static int KthLargestNumber(TreeNode<Integer> root, int k) {
		// Write your code here.
		if(root == null) return -1;
		Stack<TreeNode> st = new Stack();
		TreeNode trav = root;
		int count = 0;
		while(true) {
			if(trav != null) {
				st.push(trav);
				trav = trav.right;
			} else {
				if(st.isEmpty()) return -1;
				trav = st.pop();
				count++;
				if(count == k) return (int)trav.data;
				trav = trav.left;
			}
		}
	}
}
```