It is a searching algorithm in a limited search space.
- Time Complexity Analysis
![[Pasted image 20240925081927.png|300]]

- Formula's to calculate mid element
	- Basic
		mid = (low+high)/2    
		> In case INT_MAX + INT it will overflow so another way is
	
	- Better way
		mid = low + (high - low)/2




## BS Algo
```java
class Solution {
    public int search(int[] nums, int target) {
        int start=0,end=nums.length-1;
        while(start<=end){
            int mid = start + (end-start)/2;
            if(nums[mid]>target) end = mid-1;
            else if(nums[mid]<target) start = mid+1;
            else return mid;
        }
        return -1;
    }
}
```
### Pseudocode for recursive call
![[Pasted image 20240925082431.png|300]]
