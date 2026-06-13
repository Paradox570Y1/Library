- When we use Stack to store elements in specific order then we call it monotonic stack.


#### **What is monotonous increase stack?**

Roughly speaking, the elements in the an monotonous increase stack keeps an increasing order.

#### **The typical paradigm for monotonous increase stack**:

```cpp
for(int i = 0; i < A.size(); i++){
  while(!in_stk.empty() && in_stk.top() > A[i]){
    in_stk.pop();
  }
  in_stk.push(A[i]);
}
```

#### **What can monotonous increase stack do?**

##### (1) find the **previous less** element of each element in a vector **with O(n) time**:

- What is the previous less element of an element?  
    For example:  
    [3, 7, 8, 4]  
    The previous less element of 7 is 3.  
    The previous less element of 8 is 7.  
    **The previous less element of 4 is 3**.  
    There is no previous less element for 3.

For simplicity of notation, we use abbreviation **PLE** to denote **P**revious **L**ess **E**lement.

- C++ code (by slitghly modifying the paradigm):  
    Instead of directly pushing the element itself, here for simplicity, we push the **index**.  
    We do some record when the index is pushed into the stack.

```cpp
// previous_less[i] = j means A[j] is the previous less element of A[i].
// previous_less[i] = -1 means there is no previous less element of A[i].
vector<int> previous_less(A.size(), -1);
for(int i = 0; i < A.size(); i++){
  while(!in_stk.empty() && A[in_stk.top()] > A[i]){
    in_stk.pop();
  }
  previous_less[i] = in_stk.empty()? -1: in_stk.top();
  in_stk.push(i);
}
```

```java
import java.util.Scanner;
import java.util.Stack;
class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int arr[] = new int[n];
        for(int i=0;i<n;i++){
            arr[i] = sc.nextInt();
        }
        Stack<Integer> st = new Stack<>();
        for(int i=0;i<n;i++){
            while(!st.isEmpty() && arr[st.peek()]>arr[i])st.pop();
            int ans = st.isEmpty()?-1:arr[st.peek()];
            st.add(i);
            System.out.print(ans+" ");
        }
        System.out.println();
    }
}
```
##### (2) find the **next less** element of each element in a vector with **O(n) time**:

- What is the next less element of an element?  
    For example:  
    [3, 7, 8, 4]  
    The next less element of 8 is 4.  
    **The next less element of 7 is 4**.  
    There is no next less element for 3 and 4.

For simplicity of notation, we use abbreviation **NLE** to denote **N**ext **L**ess **E**lement.

- C++ code (by slighly modifying the paradigm):  
    We do some record when the index is poped out from the stack.

```cpp
// next_less[i] = j means A[j] is the next less element of A[i].
// next_less[i] = -1 means there is no next less element of A[i].
vector<int> previous_less(A.size(), -1);
for(int i = 0; i < A.size(); i++){
  while(!in_stk.empty() && A[in_stk.top()] > A[i]){
    auto x = in_stk.top(); in_stk.pop();
    next_less[x] = i;
  }
  in_stk.push(i);
}
```


```java
import java.util.Scanner;
import java.util.Stack;
import java.util.List;
import java.util.ArrayList;
class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int arr[] = new int[n];
        for(int i=0;i<n;i++){
            arr[i] = sc.nextInt();
        }
        Stack<Integer> st = new Stack<>();
        List<Integer> li = new ArrayList<>();
        for(int i=n-1;i>=0;i--){
            while(!st.isEmpty() && arr[st.peek()]>arr[i])st.pop();
            int ans = st.isEmpty()?-1:arr[st.peek()];
            st.add(i);
            li.add(ans);
        }
        for(int i=n-1;i>=0;i--){
            System.out.print(li.get(i)+" ");
        }
    }
}
```

OR

```java
import java.util.Scanner;
import java.util.Stack;
class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int arr[] = new int[n];
        for(int i=0;i<n;i++){
            arr[i] = sc.nextInt();
        }
        Stack<Integer> st = new Stack<>();
        int res[] = new int[n];
        for(int i=0;i<n;i++){
            res[i] = -1;
        }
        for(int i=0;i<n;i++){
            while(!st.isEmpty() && arr[st.peek()]>arr[i]){
                int idx = st.pop();
                res[idx] = arr[i];
            }
            st.add(i);
        }
        for(int i=0;i<n;i++){
            System.out.print(res[i]+" ");
        }
    }
}
```