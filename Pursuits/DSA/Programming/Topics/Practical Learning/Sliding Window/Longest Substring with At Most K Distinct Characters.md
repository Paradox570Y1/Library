## Problem statement

Send feedback

You are given a string 'str' and an integer ‘K’. Your task is to find the length of the largest substring with at most ‘K’ distinct characters.

**For example:**

```
You are given ‘str’ = ‘abbbbbbc’ and ‘K’ = 2, then the substrings that can be formed are [‘abbbbbb’, ‘bbbbbbc’]. Hence the answer is 7.
```

Detailed explanation ( Input/output format, Notes, Images )

**Constraints:**

```
1 <= T <= 10
1 <= K <= 26
1 <= |str| <= 10^6

The string str will contain only lowercase alphabets.    

Time Limit: 1 sec
```


# Better
TC-> O(2N)
```java
public class Solution {

	public static int kDistinctChars(int k, String str) {
		// Write your code here
		HashMap<Character,Integer> mp = new HashMap<>();
		int n= str.length();
		int ans=0;
		int j=0;
		for(int i=0;i<n;i++){
			char ch = str.charAt(i);
			mp.put(ch,mp.getOrDefault(ch,0)+1);
			while(mp.size()>k){
				char ele = str.charAt(j);
				mp.put(ele,mp.get(ele)-1);
				if(mp.get(ele)==0)mp.remove(ele);
				j++;
			}
			ans= Math.max(ans,i-j+1);
		}
		return ans;
	}

}
```

# Optimal

Using Map
```java
public class Solution {

	public static int kDistinctChars(int k, String str) {
		// Write your code here
		HashMap<Character,Integer> mp = new HashMap<>();
		int n= str.length();
		int ans=0;
		int j=0;
		for(int i=0;i<n;i++){
			char ch = str.charAt(i);
			mp.put(ch,mp.getOrDefault(ch,0)+1);
			if(mp.size()>k){
				char ele = str.charAt(j);
				mp.put(ele,mp.get(ele)-1);
				if(mp.get(ele)==0)mp.remove(ele);
				j++;
			}
			else ans= Math.max(ans,i-j+1);
		}
		return ans;
	}

}
```


Without using map

```java
public class Solution {

	public static int kDistinctChars(int k, String str) {
		// Write your code here
		int hash[] = new int[26];
		int n= str.length();
		int ans=0;
		int j=0;
		int cnt=0;
		for(int i=0;i<n;i++){
			int ch = str.charAt(i)-'a';
			if(hash[ch]==0)cnt++;
			hash[ch]++;
			if(cnt>k){
				int ele = str.charAt(j)-'a';
				hash[ele]--;
				if(hash[ele]==0)cnt--;
				j++;
			}
			else ans= Math.max(ans,i-j+1);
		}
		return ans;
	}

}
```