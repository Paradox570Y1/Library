[Link](https://www.geeksforgeeks.org/problems/prefix-to-postfix-conversion/1)

```java
class Solution {
    static boolean check(char ch){
        if(ch>='a' && ch <= 'z')return true;
        if(ch>='A' && ch<='Z')return true;
        if(ch>='0' && ch<='9')return true;
        return false;
    }
    static String preToPost(String s) {
        // code here
        Stack<String> st = new Stack();
        for(int i=s.length()-1;i>=0;i--){
            char ele = s.charAt(i);
            if(check(ele))st.push(String.valueOf(ele));
            else st.push(st.pop()+st.pop()+ele);
        }
        return st.peek();
    }
}
```