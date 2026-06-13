[Link](https://www.geeksforgeeks.org/problems/infix-to-postfix-1587115620/1)
![[Pasted image 20250123100808.png|200]]

```cpp
class Solution {
  public:
    // Function to convert an infix expression to a postfix expression.
    int priority(char ch){
        if(ch=='+' || ch=='-')return 1;
        if(ch=='/' || ch=='*')return 2;
        if(ch=='^')return 3;
        return -1;
    }
    string infixToPostfix(string& s) {
        // Your code here
        stack<char> st;
        string ans= "";
        for(int i=0;i<s.size();i++){
            char c = s[i];
            if(c<='z' && c>='a' || c<='Z' && c>='A' || c<='9' && c>='0')ans+=c;
            else if(st.empty() || c == '(')st.push(c);
            else if(c == ')'){
                while(!st.empty() && st.top()!='('){
                    ans+=st.top();
                    st.pop();
                }
                st.pop();
            }
            else if(priority(st.top())<priority(c))st.push(c);
            else{
                while(!st.empty() && priority(st.top())>=priority(c)){
                    ans+=st.top();
                    st.pop();
                }
                st.push(c);
            }
        }
        while(!st.empty()){
            ans+=st.top();
            st.pop();
        }
        return ans;
    }
};
```

```cpp
class Solution {
  public:
    // Function to convert an infix expression to a postfix expression.
    string infixToPostfix(string& s) {
        // Your code here
        stack<char> st;
        string ans= "";
        unordered_map<char,int> priority;
        priority['+']=1;
        priority['-']=1;
        priority['*']=2;
        priority['/']=2;
        priority['^']=3;
        priority['(']=0;
        for(int i=0;i<s.size();i++){
            char c = s[i];
            //Character.isLetterOrDigit(c)
            if(c<='z' && c>='a' || c<='Z' && c>='A' || c<='9' && c>='0')ans+=c;
            else if(st.empty() || c == '(')st.push(c);
            else{
                if(c == ')'){
                    while(!st.empty() && st.top()!='('){
                        ans+=st.top();
                        st.pop();
                    }
                    st.pop();
                }
                else if(priority[st.top()]<priority[c])st.push(c);
                else{
                    while(!st.empty() && priority[st.top()]>=priority[c]){
                        ans+=st.top();
                        st.pop();
                    }
                    st.push(c);
                }
            }
        }
        while(!st.empty()){
            ans+=st.top();
            st.pop();
        }
        return ans;
    }
};
```