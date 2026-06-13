[Link](https://www.interviewbit.com/problems/nearest-smaller-element/)

```java
vector<int> Solution::prevSmaller(vector<int> &A) {
	stack<int> st;
	vector<int> ans;
	for(auto ele:A){
		if(st.empty())ans.push_back(-1);
		else{
			while(!st.empty() && st.top()>=ele)st.pop();
			if(!st.empty())ans.push_back(st.top());
			else ans.push_back(-1);
		}
		st.push(ele);
	}
	return ans;
}

```

```javascript
module.exports = { 
 //param A : array of integers
 //return a array of integers
	prevSmaller : function(A){
        let ans = [];
        let stack = [];
        for(let i=0;i<A.length;i++){
            let ele = A[i];
            if(stack.length==0)ans.push(-1);
            else{
                while(stack.length>0 && stack[stack.length-1]>=ele)stack.pop();
                if(stack.length>0)ans.push(stack[stack.length-1]);
                else ans.push(-1);
            }
            stack.push(ele);
        }
        return ans;
	}
};
```