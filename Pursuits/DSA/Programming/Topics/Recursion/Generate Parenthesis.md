[22. Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)

Given `n` pairs of parentheses, write a function to _generate all combinations of well-formed parentheses_.

**Example 1:**

**Input:** n = 3
**Output:** ["((()))","(()())","(())()","()(())","()()()"]

**Example 2:**

**Input:** n = 1
**Output:** ["()"]

**Constraints:**

- `1 <= n <= 8`

# Using recursion

```java
class Solution {
public:
    void generate(int limit,int open,int close,string s,vector<string>& v){
        if(limit == open && limit==close){
            v.push_back(s);
            return;
        }
        if(open<limit){
            generate(limit,open+1,close,s+'(',v);
        }
        if(close<open){
            generate(limit,open,close+1,s+')',v);
        }
    }
    vector<string> generateParenthesis(int n) {
        vector<string> ans;
        if(n>0)generate(n,0,0,"",ans);
        return ans;
    }
};
```


```java
class Solution {
    List<String> generate(int limit,int open,int close,String s,List<String> li){
        if(open == limit && close == limit){
            li.add(s);
            return li;
        }
        if(open<limit){
            generate(limit,open+1,close,s+'(',li);
        }
        if(close<open){
            generate(limit,open,close+1,s+')',li);
        }
        return li;
    }
    public List<String> generateParenthesis(int n) {
        List<String> li = new ArrayList<>();
        if(n>0){
            li  = generate(n,0,0,"",li);
        }
        return li;
    }
}
```

OR

```java
class Solution {
    private void generate(List<String> ans,StringBuilder sb,int i,int j){
        if(i==0 && j==0){
            ans.add(sb.toString());
            return;
        }
        if(i>0 && i<=j){
            sb.append('(');
            generate(ans,sb,i-1,j);
            sb.setLength(sb.length()-1);
        }
        if(j>i){
            sb.append(')');
            generate(ans,sb,i,j-1);
            sb.setLength(sb.length()-1);
        }
    }
    public List<String> generateParenthesis(int n) {
        List<String> ans = new ArrayList<>();
        generate(ans,new StringBuilder(),n,n);
        return ans;
    }
}
```


In case we want only number of ways to generate parenthesis
![[Pasted image 20260123202600.png|500]]
![[Pasted image 20260123202629.png|500]]
![[Pasted image 20260123203031.png|300]]

![[Pasted image 20260123204250.png]]

![[Pasted image 20260123204718.png]]