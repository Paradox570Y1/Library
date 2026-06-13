[Link](https://www.geeksforgeeks.org/problems/postfix-to-prefix-conversion/1)
```java
class Solution {
    static boolean check(char ch){
        if(ch>='a' && ch <= 'z')return true;
        if(ch>='A' && ch<='Z')return true;
        if(ch>='0' && ch<='9')return true;
        return false;
    }
    static String postToPre(String s) {
        // code here
        Stack<String> st = new Stack();
        for(int i=0;i<s.length();i++){
            char ele = s.charAt(i);
            if(check(ele))st.push(String.valueOf(ele));
            else{
                String b = st.pop();
                String a = st.pop();
                st.push(String.valueOf(ele)+a+b);
            }
        }
        return st.peek();
    }
}
```