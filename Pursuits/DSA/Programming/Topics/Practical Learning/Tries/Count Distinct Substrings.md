
[Link](https://www.naukri.com/code360/problems/count-distinct-substrings_985292)
## Problem statement

Given a string 'S', you are supposed to return the number of distinct substrings(including empty substring) of the given string. You should implement the program using a trie.

**Note :**

```
A string ‘B’ is a substring of a string ‘A’ if ‘B’ that can be obtained by deletion of, several characters(possibly none) from the start of ‘A’ and several characters(possibly none) from the end of ‘A’. 

Two strings ‘X’ and ‘Y’ are considered different if there is at least one index ‘i’  such that the character of ‘X’ at index ‘i’ is different from the character of ‘Y’ at index ‘i’(X[i]!=Y[i]).
```

Detailed explanation ( Input/output format, Notes, Images )

**Constraints :**

```
1 <= T <= 5
1 <= |S| <= 10^3

‘S’ contains only lowercase English letters.

Time Limit: 1 sec
```

##### Sample Input 1 :

```
2
sds
abc
```

##### Sample Output 1 :

```
6
7
```

##### Explanation of Sample Input 1 :

```
In the first test case, the 6 distinct substrings are { ‘s’,’ d’, ”sd”, ”ds”, ”sds”, “” }

In the second test case, the 7 distinct substrings are {‘a’, ‘b’, ‘c’, “ab”, “bc”, “abc”, “” }.
```

##### Sample Input 2 :

```
2
aa
abab
```

##### Sample Output 2 :

```
3
8
```

##### Explanation of Sample Input 2 :

```
In the first test case, the two distinct substrings are {‘a’, “aa”, “” }.

In the second test case, the seven distinct substrings are {‘a’, ‘b’, “ab”, “ba”, “aba”, “bab”, “abab”, “” }
```

  

##### Hints:

```
1. Can you think about a data structure that can be used to store the distinct substrings?
2. Can you think about using the fact that every substring of ‘S’ is a prefix of some suffix string of ‘S’?
3. Try to insert every suffix of the string in Trie.
```



# Brute

Run two loops and create all substrings, add them to a set and return the size of the set.
- it's TC => O(N x N x 1)
- It's SC => O (N x (N + 1)/2  x N/2)  where N/2 is like the avg length of substrings


So, you can improve the space complexity here by using Tries.
It will become  O(N x (N + 1)/2)



# Using Trie

```java

import java.util.*;

public class Solution 
{
	static class Trie{
		private Trie[] links;
		private boolean flag;
		
		Trie() {
			links = new Trie[26];
			flag = false;
		}

		public boolean contains(char ch) {
			return links[ch-'a'] != null;
		}

		public void put(char ch) {
			links[ch-'a'] = new Trie();
		}

		public Trie get(char ch) {
			return links[ch-'a'];
		}

		public void setEnd() {
			flag = true;
		}
	}
	public static int countDistinctSubstrings(String s) 
	{
		//	  Write your code here.
		int distinctCount = 1;
		Trie root = new Trie();
		for (int i = 0; i < s.length(); i++) {
			Trie trav = root;
			for (int j = i; j < s.length(); j++) {
				char ch = s.charAt(j);
				if (!trav.contains(ch)) {
					trav.put(ch);
					distinctCount++;
				}
				trav = trav.get(ch);
			}
		}
		return distinctCount;
	}
}
```
