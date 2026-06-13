[131. Palindrome Partitioning](https://leetcode.com/problems/palindrome-partitioning/)

Given a string `s`, partition `s` such that every 

substring

 of the partition is a 

**palindrome**

. Return _all possible palindrome partitioning of_ `s`.

**Example 1:**

**Input:** s = "aab"
**Output:** [["a","a","b"],["aa","b"]]

**Example 2:**

**Input:** s = "a"
**Output:** [["a"]]

**Constraints:**

- `1 <= s.length <= 16`
- `s` contains only lowercase English letters.


# Brute
TC-> O(2^n * n^2)
```java
class Solution {
    List<List<String>> ans;
    int n;
    private boolean isPal(String s){
        int i=0,j=s.length()-1;
        while(i<j){
            if(s.charAt(i) != s.charAt(j))return false;
            i++;j--;
        }
        return true;
    }
    private boolean isPalArray(List<String> li){
        if(li.size()==0)return false;
        for(String s:li){
            if(!isPal(s))return false;
        }
        return true;
    }
    private void generate(List<List<String>> ans,String s,int i,List<String> li){
        if(i==n){
            if(isPalArray(li))ans.add(new ArrayList<>(li));
            return;
        }
        li.add(s.charAt(i)+"");
        generate(ans,s,i+1,li);
        li.remove(li.size()-1);
        if(li.size()!=0){
            String last = li.get(li.size()-1);
            li.set(li.size()-1,last+s.charAt(i));
            generate(ans,s,i+1,li);
            li.set(li.size()-1,last);
        }

    }
    public List<List<String>> partition(String s) {
        ans = new ArrayList<>();
        n = s.length();
        generate(ans,s,0,new ArrayList<>());
        return ans;
    }
}
```

# Better
TC-> O(O(n⋅2^n))
SC-> O(O(n⋅2^n))
```java
class Solution {
    boolean isPal(String s){
        int i=0;
        int j=s.length()-1;
        while(i<j){
            if(s.charAt(i++)!=s.charAt(j--))return false;
        }
        return true;
    }
    void generate(String s,int i,List<String> li,List<List<String>> ans){
        if(i==s.length()){
            ans.add(new ArrayList<>(li));
            return;
        }
        String temp="";
        for(int j=i;j<s.length();j++){
            temp+=s.charAt(j);
            if(isPal(temp)){
                li.add(temp);
                generate(s,j+1,li,ans);
                li.remove(li.size()-1);
            }

        }
    }
    public List<List<String>> partition(String s) {
        List<List<String>> ans = new ArrayList<>();
        generate(s,0,new ArrayList<>(),ans);
        return ans;
    }
}
```

OR

```java
class Solution {
    List<List<String>> ans;
    String s;
    private boolean isPal(String s){
        int i=0,j=s.length()-1;
        while(i<j){
            if(s.charAt(i) != s.charAt(j))return false;
            i++;j--;
        }
        return true;
    }
    private void generate(int j,List<String> li){
        if(j==s.length()){
            ans.add(new ArrayList<>(li));
            return;
        }
        StringBuilder sb = new StringBuilder();
        for(int i=j;i<s.length();i++){
            sb.append(s.charAt(i));
            if(isPal(sb.toString())){
                li.add(sb.toString());
                generate(i+1,li);
                li.remove(li.size()-1);
            }
        }
    }
    public List<List<String>> partition(String s) {
        ans = new ArrayList<>();
        this.s = s;
        generate(0,new ArrayList<>());
        return ans;
    }
}
```


# Optimal
TC-> O(O(n⋅2^n))
```java
class Solution {
    List<List<String>> ans;
    String s;
    private boolean isPal(String s,int i,int j){
        while(i<j){
            if(s.charAt(i) != s.charAt(j))return false;
            i++;j--;
        }
        return true;
    }
    private void generate(int j,List<String> li){
        if(j==s.length()){
            ans.add(new ArrayList<>(li));
            return;
        }
        for(int i=j;i<s.length();i++){
            if(isPal(s,j,i)){
                li.add(s.substring(j,i+1));
                generate(i+1,li);
                li.remove(li.size()-1);
            }
        }
    }
    public List<List<String>> partition(String s) {
        ans = new ArrayList<>();
        this.s = s;
        generate(0,new ArrayList<>());
        return ans;
    }
}
```


OR

```java
class Solution {
    private boolean[][] isPal;
    public List<List<String>> partition(String s) {
        int n = s.length();
        isPal = new boolean[n][n];
        for (int i = 0; i < n; i++) {
            isPal[i][i] = true;
            if (i+1 < n && s.charAt(i) == s.charAt(i+1)) isPal[i][i+1] = true;
        }
        for (int grp = 3; grp <= n; grp++) {
            for (int j = grp-1; j < n; j++) {
                int i = j-grp+1;
                if (isPal[i+1][j-1] && s.charAt(i) == s.charAt(j)) isPal[i][j] = true;
            }
        }

        List<String> list = new ArrayList<>();
        List<List<String>> res = new ArrayList<>();
        helper(s, list, res, 0);
        return res;
    }
    private void helper(String s, List<String> list, List<List<String>> res, int i) {
        if (i == s.length()) {
            res.add(new ArrayList<>(list));
            return;
        }
        for (int j = i; j < s.length(); j++) {
            if (isPal[i][j]) {
                list.add(s.substring(i, j+1));
                helper(s, list, res, j+1);
                list.remove(list.size()-1);
            }
        }
    }
}
```