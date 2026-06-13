[901. Online Stock Span](https://leetcode.com/problems/online-stock-span/)

Design an algorithm that collects daily price quotes for some stock and returns **the span** of that stock's price for the current day.

The **span** of the stock's price in one day is the maximum number of consecutive days (starting from that day and going backward) for which the stock price was less than or equal to the price of that day.

- For example, if the prices of the stock in the last four days is `[7,2,1,2]` and the price of the stock today is `2`, then the span of today is `4` because starting from today, the price of the stock was less than or equal `2` for `4` consecutive days.
- Also, if the prices of the stock in the last four days is `[7,34,1,2]` and the price of the stock today is `8`, then the span of today is `3` because starting from today, the price of the stock was less than or equal `8` for `3` consecutive days.

Implement the `StockSpanner` class:

- `StockSpanner()` Initializes the object of the class.
- `int next(int price)` Returns the **span** of the stock's price given that today's price is `price`.

**Example 1:**

**Input**
["StockSpanner", "next", "next", "next", "next", "next", "next", "next"]
[[], [100], [80], [60], [70], [60], [75], [85]]
**Output**
[null, 1, 1, 1, 2, 1, 4, 6]

**Explanation**
StockSpanner stockSpanner = new StockSpanner();
stockSpanner.next(100); // return 1
stockSpanner.next(80);  // return 1
stockSpanner.next(60);  // return 1
stockSpanner.next(70);  // return 2
stockSpanner.next(60);  // return 1
stockSpanner.next(75);  // return 4, because the last 4 prices (including today's price of 75) were less than or equal to today's price.
stockSpanner.next(85);  // return 6

**Constraints:**

- `1 <= price <= 105`
- At most `104` calls will be made to `next`.

# Brute

```java
class StockSpanner {
    List<Integer> li;
    public StockSpanner() {
        li = new ArrayList<>();
    }
    
    public int next(int price) {
        li.add(price);
        int n = li.size();
        int cnt=1;
        for(int i=n-2;i>=0;i--){
            if(li.get(i)>price)break;
            cnt++;
        }
        return cnt;
    }
}

/**
 * Your StockSpanner object will be instantiated and called as such:
 * StockSpanner obj = new StockSpanner();
 * int param_1 = obj.next(price);
 */
```

OR

```java
class StockSpanner {
    ArrayList<Integer> li;
    int size;

    public StockSpanner() {
        li = new ArrayList<>();
        size=0;
    }
    
    public int next(int price) {
        if(size==0){
            li.add(price);
            size=1;
            return 1;
        }
        int span=1;
        int p = size-1;
        while(p>=0 && li.get(p)<=price){
            span++;
            p--;
        }
        li.add(price);
        size++;
        return span;
    }
}
```

# Using Stack
TC -> O(2N)
SC -> O(N)
```java
class StockSpanner {
    Stack<int[]> st;
    public StockSpanner() {
        st = new Stack<>();
    }
    
    public int next(int price) {
        int temp=0;
        if(!st.isEmpty())temp = st.peek()[1]+1;
        while(!st.isEmpty() && st.peek()[0]<=price)st.pop();
        int maxIdx = (st.isEmpty())?-1:st.peek()[1];
        st.add(new int[]{price,temp});
        return temp - maxIdx;
    }
}

```

OR

```java
class StockSpanner {
    Stack<int[]> st;
    int cnt;
    public StockSpanner() {
        st = new Stack<>();
        cnt=0;
    }
    
    public int next(int price) {
        int pos = ++cnt;
        while(!st.isEmpty() && st.peek()[0]<=price){
            pos = st.pop()[1];
        }
        int ans = cnt-pos+1;
        st.push(new int[]{price,pos});
        return ans;
    }
}
```

OR
Gives bad time complexity
```java
class StockSpanner {
    int[][] st;
    int p;
    int cnt;
    public StockSpanner() {
        st = new int[10001][2];
        p=-1;
        cnt=0;
    }
    
    public int next(int price) {
        int pos = ++cnt;
        while(p!=-1 && st[p][0]<=price){
            pos = st[p--][1];
        }
        int ans = cnt-pos+1;
        st[++p] = new int[]{price,pos};
        return ans;
    }
}

/**
 * Your StockSpanner object will be instantiated and called as such:
 * StockSpanner obj = new StockSpanner();
 * int param_1 = obj.next(price);
 */
```
# Using list to implement stack
TC -> O(2N)
SC -> O(N)
```java
class StockSpanner {
    List<int[]> li;
    public StockSpanner() {
        li = new ArrayList<>();
    }
    
    public int next(int price) {
        int temp=0;
        if(li.size()!=0)temp = li.get(li.size()-1)[1]+1;
        while(li.size()!=0 && li.get(li.size()-1)[0]<=price)li.remove(li.size()-1);
        int maxIdx = (li.size()==0)?-1:li.get(li.size()-1)[1];
        li.add(new int[]{price,temp});
        return temp - maxIdx;
    }
}
```