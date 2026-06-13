### Substrings with K Distinct
On strings-> [problem](https://www.geeksforgeeks.org/problems/count-number-of-substrings4528/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=count-number-of-substrings)
On Numbers-> [Leetcode](https://leetcode.com/problems/subarrays-with-k-different-integers/)

> [Resource](https://www.geeksforgeeks.org/count-number-of-substrings-with-exactly-k-distinct-characters/)

Difficulty: **Medium**Accuracy: **20.46%**Submissions: **132K+**Points: **4**

Given a string **s** of lowercase alphabets, count all possible **substrings** (not necessarily distinct) that have **exactly k distinct** characters. 

**Examples :**

**Input:** s = "aba", k = 2
**Output:** 3
**Explanation**: The substrings are: "ab", "ba" and "aba".

**Input**: s = "abaaca", k = 1
**Output:** 7
**Explanation**: The substrings are: "a", "b", "a", "aa", "a", "c", "a".  

**Input:** s = "cdad", k = 4
**Output:** 0

**Constraints:**  
1 ≤ s.size() ≤ 106  
1 ≤ k ≤ 26

Try more examples


# Brute
TC=> O(N³)  SC = > O(N)
```java
class Solution {
    int cntEle(String s,int i,int j){
        HashSet<Character> hs = new HashSet<>();
        int cnt=0;
        while(i<=j){
            char c = s.charAt(i);
            if(!hs.contains(c)){
                cnt++;
                hs.add(c);
            }
            i++;
        }
        return cnt;
    }
    int countSubstr(String s, int k) {
        // your code here
        int ans=0;
        for(int i =0;i<s.length();i++){
            for(int j=i;j<s.length();j++){
                if(cntEle(s,i,j)==k) ans++;
            }
        }
        return ans;
    }
}
```

# Better
****Time Complexity:**** ****O(n²)****  
****Auxiliary Space: O(1),**** Only 26 size array is used, which can be considered constant space.
```java
class Solution {
    int countSubstr(String s, int k) {
        // your code here
        int ans=0;
        
        for(int i=0;i<s.length();i++){
            int cnt=0;
            int hash[] = new int[27];
            for(int j=i;j<s.length();j++){
                if(hash[s.charAt(j)-'a'] == 0)cnt++;
                hash[s.charAt(j)-'a']++;
                if(cnt==k)ans++;
                if(cnt>k)break;
            }
        }
        return ans;
    }
```

# Optimal

****Efficient Approach:**** The idea is to count all the subarrays with at most K distinct characters and then subtract all the subarrays with at most K – 1 characters. That leaves us with count of subarrays with exactly K distinct characters.

****Time Complexity: O(n)****  
****Auxiliary Space: O(n)****
```java
class Solution {
    int cntAtMostK(String s,int k){
        HashMap<Character,Integer> mp = new HashMap<>();
        int left =0;
        int ans=0;
        for(int i=0;i<s.length();i++){
            char c = s.charAt(i);
            mp.put(c,mp.getOrDefault(c,0)+1);
            while(mp.size()>k){
                char start = s.charAt(left);
                mp.put(start,mp.get(start)-1);
                if(mp.get(start) == 0)mp.remove(start);
                left++;
            }
            ans += i-left+1;
        }
        return ans;
    }
    int countSubstr(String s, int k) {
        // your code here
        return cntAtMostK(s,k) - cntAtMostK(s,k-1);
    }
}

```

****Time Complexity: O(n)****  
****Auxiliary Space: O(1)****
```java
class Solution {
    int cntAtMostK(String s,int k){
        int hash[] = new int[26];
        int cnt=0; //distinct cnt
        int left =0;
        int ans=0;
        for(int i=0;i<s.length();i++){
            char c = s.charAt(i);
            hash[c-'a']++;
            if(hash[c-'a']==1) cnt++;
            while(cnt>k){
                char start = s.charAt(left);
                hash[start-'a']--;
                left++;
                if(hash[start-'a'] == 0)cnt--;
            }
            ans += i-left+1;
        }
        return ans;
    }
    int countSubstr(String s, int k) {
        // your code here
        return cntAtMostK(s,k) - cntAtMostK(s,k-1);
    }
}
```