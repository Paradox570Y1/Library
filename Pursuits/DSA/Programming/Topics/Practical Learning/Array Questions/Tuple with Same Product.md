[1726. Tuple with Same Product](https://leetcode.com/problems/tuple-with-same-product/)


Given an array `nums` of **distinct** positive integers, return _the number of tuples_ `(a, b, c, d)` _such that_ `a * b = c * d` _where_ `a`_,_ `b`_,_ `c`_, and_ `d` _are elements of_ `nums`_, and_ `a != b != c != d`_._

**Example 1:**

**Input:** nums = [2,3,4,6]
**Output:** 8
**Explanation:** There are 8 valid tuples:
(2,6,3,4) , (2,6,4,3) , (6,2,3,4) , (6,2,4,3)
(3,4,2,6) , (4,3,2,6) , (3,4,6,2) , (4,3,6,2)

**Example 2:**

**Input:** nums = [1,2,4,5,10]
**Output:** 16
**Explanation:** There are 16 valid tuples:
(1,10,2,5) , (1,10,5,2) , (10,1,2,5) , (10,1,5,2)
(2,5,1,10) , (2,5,10,1) , (5,2,1,10) , (5,2,10,1)
(2,10,4,5) , (2,10,5,4) , (10,2,4,5) , (10,2,5,4)
(4,5,2,10) , (4,5,10,2) , (5,4,2,10) , (5,4,10,2)

**Constraints:**

- `1 <= nums.length <= 1000`
- `1 <= nums[i] <= 104`
- All elements in `nums` are **distinct**.


```java
class Solution {
    public int tupleSameProduct(int[] nums) {
        HashMap<Integer,Integer> hm = new HashMap<>();
        for(int i=0;i<nums.length;i++){
            for(int j=i+1;j<nums.length;j++){
                int ele = nums[i]*nums[j];
                hm.put(ele,hm.getOrDefault(ele,0)+1);
            }
        }
        int ans=0;
        for(Map.Entry<Integer,Integer> e:hm.entrySet()){
            int ele =e.getValue();
            ele*=2;
            ans+=(ele*(ele-1) - ele);
        }
        return ans;
    }
}
```

```java
class Solution {
    public int tupleSameProduct(int[] nums) {
        HashMap<Integer,Integer> hm = new HashMap<>();
        for(int i=0;i<nums.length;i++){
            for(int j=i+1;j<nums.length;j++){
                int ele = nums[i]*nums[j];
                hm.put(ele,hm.getOrDefault(ele,0)+1);
            }
        }
        int ans=0;
        for(Map.Entry<Integer,Integer> e:hm.entrySet()){
            int ele =e.getValue();
            ans+=4*ele*(ele-1);
        }
        return ans;
    }
}
```