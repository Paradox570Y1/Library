[Link](https://www.geeksforgeeks.org/problems/count-total-set-bits-1587115620/1)
### Count total set bits

Difficulty: **Medium**Accuracy: **35.77%**Submissions: **208K+**Points: **4**

You are given a number **n**. Find the total count of set bits for all numbers from 1 to n (both inclusive).  
  
**Examples :  
**

**Input**: n = 4
**Output**: 5
**Explanation**: For numbers from 1 to 4. For 1: 0 0 1 = 1 set bits For 2: 0 1 0 = 1 set bits For 3: 0 1 1 = 2 set bits For 4: 1 0 0 = 1 set bits Therefore, the total set bits is 5.

**Input**: n = 17
**Output**: 35
**Explanation**: From numbers 1 to 17(both inclusive), the total number of set bits is 35.

**Expected Time Complexity:** O(logn)  
**Expected Auxiliary Space:** O(1)  
  
**Constraints:**  
1 ≤ n ≤ 108

# Brute
TC-> O(N log N)
```java
class Solution{
    static int cntBit(int n){
        int cnt=0;
        while(n!=0){   // takes log n
            cnt+=(n&1);
            n>>=1;
        }
        return cnt;
    }
    public static int countSetBits(int n){
    
        // Your code here
        int cnt =0;
        for(int i=1;i<=n;i++){
            cnt+= cntBit(i);
        }
        return cnt;
    }
}
```

# Little Better
TC-> O(N) * O(31) 

```java
class Solution{
    //Function to return sum of count of set bits in the integers from 1 to n.
    static int cntBit(int n){
        int cnt=0;
        while(n!=0){
            n &= n-1; // turns off rightmost set bit
            cnt++;
        }
        return cnt;
    }
    public static int countSetBits(int n){
    
        // Your code here
        int cnt =0;
        for(int i=1;i<=n;i++){
            cnt+= cntBit(i);
        }
        return cnt;
    }
}
```


# Optimal

```java
class Solution{
    
    static int leftMostSetBit(int n){
        int x=0;
        while(n!=0){
            n>>=1;
            x++;
        }
        return x-1;
    }
    public static int countSetBits(int n){
    
        // Your code here
        if(n==0)return 0;
        int x = leftMostSetBit(n);
        int cntTill2Pow = (1<<x-1)*x; // 2^(x-1) * x
        int restCnt = n-(1<<x)+1 + countSetBits(n-(1<<x)); //n- 2^x + 1
        return cntTill2Pow + restCnt;
    }
}
```