[Link](https://www.geeksforgeeks.org/problems/postfix-to-infix-conversion/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=postfix-to-prefix-conversion)
```java
class Solution {
    static boolean check(char ch){
        if(ch<='z' && ch>='a')return true;
        if(ch<='Z' && ch>='A')return true;
        if(ch>='0' && ch<='9')return true;
        return false;
    }
    static int priority(char ch){
        if(ch=='^')return 3;
        if(ch=='/' || ch=='*')return 2;
        if(ch=='+' || ch == '-')return 1;
        return -1;
    }
    static String postToInfix(String exp) {
        // code here
        String ans = "";
        Stack<String> st = new Stack();
        for(int i=0;i<exp.length();i++){
            char ele = exp.charAt(i);
            if(check(ele))st.push(String.valueOf(ele));
            else{
                String b = st.pop();
                String a = st.pop();
                st.push('('+a+ele+b+')');
            }
        }
        return st.peek();
    }
}
```