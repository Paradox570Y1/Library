[735. Asteroid Collision](https://leetcode.com/problems/asteroid-collision/)

We are given an array `asteroids` of integers representing asteroids in a row. The indices of the asteriod in the array represent their relative position in space.

For each asteroid, the absolute value represents its size, and the sign represents its direction (positive meaning right, negative meaning left). Each asteroid moves at the same speed.

Find out the state of the asteroids after all collisions. If two asteroids meet, the smaller one will explode. If both are the same size, both will explode. Two asteroids moving in the same direction will never meet.

**Example 1:**

**Input:** asteroids = [5,10,-5]
**Output:** [5,10]
**Explanation:** The 10 and -5 collide resulting in 10. The 5 and 10 never collide.

**Example 2:**

**Input:** asteroids = [8,-8]
**Output:** []
**Explanation:** The 8 and -8 collide exploding each other.

**Example 3:**

**Input:** asteroids = [10,2,-5]
**Output:** [10]
**Explanation:** The 2 and -5 collide resulting in -5. The 10 and -5 collide resulting in 10.

**Constraints:**

- `2 <= asteroids.length <= 104`
- `-1000 <= asteroids[i] <= 1000`
- `asteroids[i] != 0`

# My Approach
TC -> O(2N)
SC -> O(N)
```java
class Solution {
    public int[] asteroidCollision(int[] asteroids) {
        int n= asteroids.length;
        Stack<Integer> st = new Stack<>();
        for(int i=0;i<n;i++){
            int right = asteroids[i];
            if(st.isEmpty()){
                st.push(right);
                continue;
            }
            if(right>0 || st.peek()<0){
                st.push(right);
                continue;
            }
            while(!st.isEmpty() && st.peek()>0 && st.peek()<Math.abs(right))st.pop();
            if(st.isEmpty() || st.peek()<0)st.push(right);
            else if(st.peek()==Math.abs(right))st.pop();
        }
        n = st.size();
        int[] ans = new int[n];
        for(int i=0;i<n;i++){
            ans[i] = st.pop();
        }
        int i=0,j=n-1;
        while(i<j){
            int temp = ans[i];
            ans[i] = ans[j];
            ans[j] = temp;
            i++;j--;
        }
        return ans;
    }
}
```

OR

```java
class Solution {
    private int collision(int left,int right){
        int mag = -right;
        if(left == mag)return 0;
        if(left < mag)return right;
        return left;
    }
    public int[] asteroidCollision(int[] asteroids) {
        Stack<Integer> st = new Stack<>();
        for(int asteroid:asteroids){
            if(st.isEmpty()){
                st.push(asteroid);
                continue;
            }
            int leftAst = st.peek();
            st.push(asteroid);
            if(asteroid<0 && leftAst>0){
                int rightAst = asteroid;
                while(!st.isEmpty() && st.peek()<0 && st.size()>1){
                    rightAst = st.pop();
                    if(st.peek()<0){
                        st.push(rightAst);
                        break;
                    }
                    leftAst = st.pop();
                    int res = collision(leftAst,rightAst);
                    if(res==0)break;
                    st.push(res);
                }
            }
        }
        int ans[] = new int[st.size()];
        for(int i=st.size()-1;i>=0;i--){
            ans[i] = st.pop();
        }
        return ans;
    }
}
```

OR

```java
class Solution {
    public int[] asteroidCollision(int[] asteroids) {
        int n = asteroids.length;
        Stack<Integer> st = new Stack<>();
        for(int asteroid:asteroids){
            if(st.isEmpty() || asteroid>0 || st.peek()<0){
                st.push(asteroid);
                continue;
            }
            while(!st.isEmpty() && st.peek()>0 && st.peek()<Math.abs(asteroid))st.pop();
            if(st.isEmpty() || st.peek()<0)st.push(asteroid);
            else if(st.peek() == Math.abs(asteroid))st.pop();
        }
        int ans[] = new int[st.size()];
        for(int i=st.size()-1;i>=0;i--){
            ans[i] = st.pop();
        }
        return ans;
    }
}
```

# Optimal

Convert stack to array
```java
class Solution {
    public int[] asteroidCollision(int[] asteroids) {
        int n = asteroids.length;
        int st[] = new int[n];
        int top=-1;
        for(int asteroid:asteroids){
            if(top==-1 || asteroid>0 || st[top]<0){
                st[++top] = asteroid;
                continue;
            }
            while(top!=-1 && st[top]>0 && st[top]<Math.abs(asteroid))st[top--] = 0;
            if(top==-1 || st[top]<0)st[++top] = asteroid;
            else if(st[top] == Math.abs(asteroid))st[top--] = 0;
        }
        int ans[] = new int[top+1];
        for(int i=0;i<=top;i++){
            ans[i]=st[i];
        }
        return ans;
    }
}
```