[Link](https://www.geeksforgeeks.org/problems/prefix-to-infix-conversion/1)

```java
class Solution {
    static boolean check(char ele){
        if(ele<='Z' && ele >='A')return true;
        if(ele>='a' && ele <='z')return true;
        if(ele<='9' && ele >='0')return true;
        return false;
    }
    static String reverse(String s){
        StringBuilder sb = new StringBuilder();
        for(int i=s.length()-1;i>=0;i--){
            sb.append(s.charAt(i));
        }
        return sb.toString();
    }
    static String preToInfix(String s) {
        // code here
        s = reverse(s);
        String ans = "";
        Stack<String> st = new Stack();
        for(int i=0;i<s.length();i++){
            char ele = s.charAt(i);
            if(check(ele)){
                st.push(String.valueOf(ele));
            }
            else{
                String a = st.pop();
                String b = st.pop();
                String temp = ")"+b+ele+a+"(";
                st.push(temp);
            }
        }
        return reverse(st.peek());
    }
}
```

//Not Working
```java
class Solution {
    static boolean check(char ele){
        if(ele<='Z' && ele >='A')return true;
        return false;
    }
    static String preToInfix(String pre_exp) {
        // code here
        String ans="";
        int char_cnt=0;
        int close=0;
        int op_cnt=0;
        Stack<Character> st = new Stack();
        for(int i=0;i<pre_exp.length();i++){
            char ele = pre_exp.charAt(i);
            if(check(ele)){
                ans += ele;
                char_cnt++;
                if(!st.isEmpty() && char_cnt%2==1){
                    ans += st.pop();
                    op_cnt++;
                }
                else{
                    while(op_cnt!=0){
                        ans+=')';
                        op_cnt--;
                    }
                    if(!st.isEmpty()){
                        ans+=st.pop();
                        close++;
                    }
                }
            }
            else{
                st.push(ele);
                ans+='(';
                char_cnt=0;
            }
        }
        while(close!=0){
            ans+=')';
            close--;
        }
        return ans;
    }
}
```