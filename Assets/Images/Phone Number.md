[17. Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)

Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent. Return the answer in **any order**.

A mapping of digits to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![](https://assets.leetcode.com/uploads/2022/03/15/1200px-telephone-keypad2svg.png)

**Example 1:**

**Input:** digits = "23"
**Output:** ["ad","ae","af","bd","be","bf","cd","ce","cf"]

**Example 2:**

**Input:** digits = ""
**Output:** []

**Example 3:**

**Input:** digits = "2"
**Output:** ["a","b","c"]

**Constraints:**

- `0 <= digits.length <= 4`
- `digits[i]` is a digit in the range `['2', '9']`.

# Brute

```java
class Solution {
    private void helper(List<String> ans,String[] hash,String s,String str,int i){
        if(i== str.length()){
            ans.add(s);
            return;
        }
        String temp = hash[str.charAt(i)-'0'];
        for(int j=0;j<temp.length();j++){
            helper(ans,hash,s+temp.charAt(j),str,i+1);
        }
    }
    public List<String> letterCombinations(String digits) {
        List<String> ans = new ArrayList<>();
        if(digits.length()==0)return ans;
        String hash[] = {"","","abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"};
        helper(ans,hash,"",digits,0);
        return ans;
    }
}
```

```java
class Solution {
    void generate(String digits,int i,String s,String[] hash,List<String> ans){
        if(i==digits.length()){
            ans.add(s);
            return;
        }
        int digit = digits.charAt(i)-'0';
        String str = hash[digit];
        for(int j=0;j<str.length();j++){
            generate(digits,i+1,s+str.charAt(j),hash,ans);
        }
    }
    public List<String> letterCombinations(String digits) {
        if(digits.length()==0)return new ArrayList<>();
        String[] hash = {"","","abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"};
        List<String> ans = new ArrayList<>();
        generate(digits,0,"",hash,ans);
        return ans;
    }
}
```

# Optimal

```java
class Solution {
    private void helper(List<String> ans,String[] hash,StringBuilder sb,String str,int i){
        if(i== str.length()){
            ans.add(sb.toString());
            return;
        }
        String temp = hash[str.charAt(i)-'0'];
        for(int j=0;j<temp.length();j++){
            sb.append(temp.charAt(j));
            helper(ans,hash,sb,str,i+1);
            sb.setLength(sb.length()-1);
        }
    }
    public List<String> letterCombinations(String digits) {
        List<String> ans = new ArrayList<>();
        if(digits.length()==0)return ans;
        String hash[] = {"","","abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"};
        helper(ans,hash,new StringBuilder(),digits,0);
        return ans;
    }
}
```

OR

```java
class Solution {
    String hash[]={"","","abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"};
    private void generate(String s,int j,List<String> ans,StringBuilder sb){
        if(j==s.length()){
            if(sb.length()!=0)ans.add(sb.toString());
            return;
        }
        int ele = s.charAt(j)-'0';
        int n = hash[ele].length();
        for(int i=0;i<n;i++){
            sb.append(hash[ele].charAt(i));
            generate(s,j+1,ans,sb);
            sb.setLength(sb.length()-1);
        }
    }
    public List<String> letterCombinations(String digits) {
        List<String> ans = new ArrayList<>();
        generate(digits,0,ans,new StringBuilder());
        return ans;
    }
}
```