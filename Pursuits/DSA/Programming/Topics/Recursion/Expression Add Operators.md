[282. Expression Add Operators](https://leetcode.com/problems/expression-add-operators/)

Given a string `num` that contains only digits and an integer `target`, return _**all possibilities** to insert the binary operators_ `'+'`_,_ `'-'`_, and/or_ `'*'` _between the digits of_ `num` _so that the resultant expression evaluates to the_ `target` _value_.

Note that operands in the returned expressions **should not** contain leading zeros.

**Example 1:**

**Input:** num = "123", target = 6
**Output:** ["1*2*3","1+2+3"]
**Explanation:** Both "1*2*3" and "1+2+3" evaluate to 6.

**Example 2:**

**Input:** num = "232", target = 8
**Output:** ["2*3+2","2+3*2"]
**Explanation:** Both "2*3+2" and "2+3*2" evaluate to 8.

**Example 3:**

**Input:** num = "3456237490", target = 9191
**Output:** []
**Explanation:** There are no expressions that can be created from "3456237490" to evaluate to 9191.

**Constraints:**

- `1 <= num.length <= 10`
- `num` consists of only digits.
- `-231 <= target <= 231 - 1`

# Brute

```java
class Solution {
    void generate(List<String> ans, String num, int target, String expr, int index, long prev, long curr)
        if (index == num.length()) {
            if (curr == target) {
                ans.add(expr);
            }
            return;
        }

        for (int i = index; i < num.length(); i++) {
            if (i != index && num.charAt(index) == '0') break;

            String part = num.substring(index, i + 1);
            long val = Long.parseLong(part);

            if (index == 0) {
                generate(ans, num, target, part, i + 1, val, val);
            } else {
                generate(ans, num, target, expr + "+" + part, i + 1, val, curr + val);
                generate(ans, num, target, expr + "-" + part, i + 1, -val, curr - val);
                generate(ans, num, target, expr + "*" + part, i + 1, prev * val, curr - prev + (prev * val));
            }
        }
    }

    public List<String> addOperators(String num, int target) {
        List<String> ans = new ArrayList<>();
        generate(ans, num, target, "", 0, 0, 0);
        return ans;
    }
}

```



```java
class Solution {
    public List<String> addOperators(String num, int target) {
        List<String> ans = new ArrayList<>();
        helper(num,target,ans,"",0,0,0);
        return ans;
    }
    void helper(String num,int target,List<String> ans,String s,int idx,long curVal,long prevNum){
        if(idx==num.length()){
            if(curVal==target)ans.add(s);
            return;
        }
        for(int i=idx;i<num.length();i++){
            if(i!=idx && num.charAt(idx) == '0')break;
            String strnum =  num.substring(idx,i+1);
            long curNum = Long.parseLong(strnum);
            if(idx==0){
                helper(num,target,ans,strnum,i+1,curNum,curNum);
            }
            else{
                helper(num,target,ans,s+"*"+strnum,i+1,curVal-prevNum+(curNum*prevNum),prevNum*curNum);
                helper(num,target,ans,s+"+"+strnum,i+1,curVal+curNum,curNum);
                helper(num,target,ans,s+"-"+strnum,i+1,curVal-curNum,-curNum);
            }
            
        }
        
    }
}
```

# Easy to understand

```java
class Solution {
    public List<String> addOperators(String num, int target) {
        List<String> ans = new ArrayList<>();
        helper(ans,num,target,"",0,0,0);
        return ans;
    }
    void helper(List<String> ans,String num, int target,String s,int idx,long eval,long residual){
        if(idx==num.length()){
            if(target == eval)ans.add(s);
            return;
        }
        String curStr = "";
        long val = 0;
        for(int i=idx;i<num.length();i++){
            if(i>idx && num.charAt(idx) == '0')break;
            curStr += num.charAt(i);
            val = val*10 + num.charAt(i)-'0';
            if(idx==0){
                helper(ans,num,target,s+curStr,i+1,val,val);
            }
            else{
                helper(ans,num,target,s+"+"+curStr,i+1,eval+val,val);
                helper(ans,num,target,s+"-"+curStr,i+1,eval-val,-val);
                helper(ans,num,target,s+"*"+curStr,i+1,eval-residual+residual*val,residual*val);
            }
        }
    }
}
```

```java
class Solution {
    public List<String> addOperators(String num, int target) {
        List<String> ans = new ArrayList<>();
        helper(num,target,ans,new StringBuilder(),0,0,0);
        return ans;
    }
    void helper(String num,int target,List<String> ans,StringBuilder sb,int idx,long curVal,long prevNum){
        if(idx==num.length()){
            if(curVal==target)ans.add(sb.toString());
            return;
        }
        for(int i=idx;i<num.length();i++){
            if(i!=idx && num.charAt(idx) == '0')break;
            String strnum =  num.substring(idx,i+1);
            long curNum = Long.parseLong(strnum);
            int strlen = strnum.length();
            if(idx==0){
                sb.append(strnum);
                helper(num,target,ans,sb,i+1,curNum,curNum);
                sb.setLength(sb.length() - strlen);
            }
            else{
                sb.append("*"+strnum);
                helper(num,target,ans,sb,i+1,curVal-prevNum+(curNum*prevNum),prevNum*curNum);
                sb.setLength(sb.length() - strlen -1);
                sb.append("+"+strnum);
                helper(num,target,ans,sb,i+1,curVal+curNum,curNum);
                sb.setLength(sb.length() - strlen -1);
                sb.append("-"+strnum);
                helper(num,target,ans,sb,i+1,curVal-curNum,-curNum);
                sb.setLength(sb.length() - strlen -1);
            }
            
        }
        
    }
}
```

OR

# Best runtime

```java
class Solution {
    String s;
    int target;
    List<String> ans;
    int n;
    private void generate(int i,long cal,long prev,StringBuilder sb){
        if(i==n){
            if(cal == target)ans.add(sb.toString());
            return;
        }
        long num=0;
        for(int j=i;j<n;j++){
            if(j>i && s.charAt(i)=='0')break;
            char ch = s.charAt(j);
            num = num*10 + (ch-'0');
            int n = sb.length();
            if(i==0){
                sb.append(num);
                generate(j+1,num,num,sb);
                sb.setLength(n);
            }
            else{
                sb.append("+").append(num);
                generate(j+1,cal+num,num,sb);
                sb.setLength(n);
                sb.append("*").append(num);
                generate(j+1,prev*num+cal-prev,prev*num,sb);
                sb.setLength(n);
                sb.append("-").append(num);
                generate(j+1,cal-num,-num,sb);
                sb.setLength(n);
            }
            
        }
    }
    public List<String> addOperators(String num, int target) {
        s=num;
        n = s.length();
        this.target = target;
        ans = new ArrayList<>();
        generate(0,0,0,new StringBuilder());
        return ans;
    }
}
```