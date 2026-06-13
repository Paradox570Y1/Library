[152. Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/)

Given an integer array `nums`, find a  subarray
 that has the largest product, and return _the product_.

The test cases are generated so that the answer will fit in a **32-bit** integer.

**Example 1:**

**Input:** nums = [2,3,-2,4]
**Output:** 6
**Explanation:** [2,3] has the largest product 6.

**Example 2:**

**Input:** nums = [-2,0,-1]
**Output:** 0
**Explanation:** The result cannot be 2, because [-2,-1] is not a subarray.

**Constraints:**

- `1 <= nums.length <= 2 * 104`
- `-10 <= nums[i] <= 10`
- The product of any subarray of `nums` is **guaranteed** to fit in a **32-bit** integer.

# Brute
```cpp
#include<bits/stdc++.h>
using namespace std;

int maxProductSubArray(vector<int>& nums) {
    int result = INT_MIN;
    for(int i=0;i<nums.size()-1;i++) {
        for(int j=i+1;j<nums.size();j++) {
            int prod = 1;
            for(int k=i;k<=j;k++) 
                prod *= nums[k];
            result = max(result,prod);    
        }
    }
    return result;
}

int main() {
    vector<int> nums = {1,2,-3,0,-4,-5};
    cout<<"The maximum product subarray: "<<maxProductSubArray(nums);
    return 0;
}

```

# Better
```cpp
#include<bits/stdc++.h>
using namespace std;

int maxProductSubArray(vector<int>& nums) {
    int result = nums[0];
    for(int i=0;i<nums.size()-1;i++) {
        int p = nums[i];
        for(int j=i+1;j<nums.size();j++) {
           result = max(result,p);
           p *= nums[j];
        }
        result = max(result,p);//manages (n-1)th term 
    }
    return result;
}

int main() {
    vector<int> nums = {1,2,-3,0,-4,-5};
    cout<<"The maximum product subarray: "<<maxProductSubArray(nums);
    return 0;
}
```

# Optimal
#### Two approaches to solve this
- **Observation (Intuitive approach) **
- **Modified Kadane's Algo(Not that Intuitive)**
>Use intuitive approach for interview


- Observation
```java
class Solution {
    public int maxProduct(int[] nums) {
        int left=1,right=1;
        int maxi=-2147483648;
        for(int i=0;i<nums.length;i++){
            if(left==0)left=1;
            if(right==0)right=1;
            left *= nums[i];
            right *= nums[nums.length-1-i];
            maxi = Math.max(maxi,Math.max(left,right));
        }
        return maxi;
    }   
}
```

OR

```java
class Solution {
    public int maxProduct(int[] nums) {
        int prod = 1;
        int res = nums[0];
        for (int num : nums) {
            prod *= num;
            res = Math.max(res, prod);
            if (prod == 0) prod = 1;
        }
        prod = 1;
        for (int i = nums.length-1; i >= 0; i--) {
            int num = nums[i];
            prod *= num;
            res = Math.max(res, prod);
            if (prod == 0) prod = 1;
        }
        return res;
    }
}
```

OR

```java
class Solution {
    public int maxProduct(int[] nums) {
       int prod1 = nums[0],prod2 = nums[0],result = nums[0];
    for(int i=1;i<nums.length;i++) {
        int temp = Math.max(nums[i],Math.max(prod1*nums[i],prod2*nums[i]));
        prod2 = Math.min(nums[i],Math.min(prod1*nums[i],prod2*nums[i]));
        prod1 = temp;
        result = Math.max(result,prod1);
    }
    
    return result;
    }   
}
```

- Modified Kadane's Approach
```cpp
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int maxi=INT_MIN,buffer=1;
        for(int i=0;i<nums.size();i++){
            buffer *=nums[i];
            maxi = max(maxi,buffer);
            if(buffer==0) buffer=1;
        }
        buffer=1;
        for(int i=nums.size()-1;i>=0;i--){
            buffer *= nums[i];
            maxi = max(maxi,buffer);
            if(buffer==0) buffer =1;
        }
        return maxi;
    }
};
```


```js
var maxProduct = function(nums) {
    let left=1;
    let right=1;
    let maxi=nums[0];
    nums.forEach((val,idx)=>{
        left*=val;
        right*=nums[nums.length-idx-1];
        if(left>right){
            maxi = maxi>left? maxi:left;
        }
        else maxi = maxi>right? maxi:right;
        if(left==0)left++;
        if(right==0)right++;
    })
    return maxi;
};
```