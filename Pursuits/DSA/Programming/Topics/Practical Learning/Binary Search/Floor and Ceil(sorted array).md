[Link](https://www.naukri.com/code360/problems/ceiling-in-a-sorted-array_1825401)
While the **`ceil`** and **`lower_bound`** may seem similar for sorted data (e.g., they both locate values greater than or equal to a number), **`ceil`** works on individual numbers, whereas **`lower_bound`** operates within a sorted structure or range.

You're given a sorted array **_'a'_** of **_'n'_** integers and an integer **_'x'_**.
Find the floor and ceiling of 'x' in 'a[0..n-1]'.

**Note:**

```
Floor of 'x' is the largest element in the array which is smaller than or equal to 'x'.
Ceiling of 'x' is the smallest element in the array greater than or equal to 'x'.
```

**Example:**

```
Input: 
n=6, x=5, a=[3, 4, 7, 8, 8, 10]   

Output:
4 7

Explanation:
The floor and ceiling of 'x' = 5 are 4 and 7, respectively.
```

Detailed explanation ( Input/output format, Notes, Images )
**Sample Input 1 :**

```
6 8
3 4 4 7 8 10
```

**Sample Output 1 :**

```
8 8
```
**Explanation of sample input 1 :**

```
Since x = 8 is present in the array, it will be both floor and ceiling.
```

**Constraints :**

```
1 <= n <= 2 * 10^5      
1 <= a[i] <= 10^9
Time limit: 1 sec
```


# Brute
```java
class Solution {
    public int[] getFloorAndCeil(int x, int[] arr) {
        // code here
        int[] ans = new int[2];
        ans[0]=-1;
        ans[1]=2147483647;
        boolean flag=true;
        for(int i=0;i<arr.length;i++){
            if(arr[i]<=x){
                ans[0] = Math.max(ans[0],arr[i]);
            }
            if(arr[i]>=x){
                ans[1] = Math.min(ans[1],arr[i]);
                flag=false;
            }
        }
        if(flag)ans[1] =-1;
        return ans;
    }
}
```

# Optimal

```cpp
pair<int, int> getFloorAndCeil(vector<int> &a, int n, int x) {
	// Write your code here.
	int low = 0,high = n-1;
	pair<int,int> p={-1,-1};
	while(low<=high){
		int mid= low + (high-low)/2;
		if(a[mid]>=x){
			p.second=a[mid];
			high = mid-1;
		}
		else {
			p.first = a[mid];
			low = mid+1;
		}
	}
	if(p.second == x) p.first = p.second;

	return p;
}
```




# Individual code for both Floor and Ceil
```cpp
#include<bits/stdc++.h>
using namespace std;

int findFloor(int arr[], int n, int x) {
	int low = 0, high = n - 1;
	int ans = -1;

	while (low <= high) {
		int mid = (low + high) / 2;
		// maybe an answer
		if (arr[mid] <= x) {
			ans = arr[mid];
			//look for smaller index on the left
			low = mid + 1;
		}
		else {
			high = mid - 1; // look on the right
		}
	}
	return ans;
}

int findCeil(int arr[], int n, int x) {
	int low = 0, high = n - 1;
	int ans = -1;

	while (low <= high) {
		int mid = (low + high) / 2;
		// maybe an answer
		if (arr[mid] >= x) {
			ans = arr[mid];
			//look for smaller index on the left
			high = mid - 1;
		}
		else {
			low = mid + 1; // look on the right
		}
	}
	return ans;
}

pair<int, int> getFloorAndCeil(int arr[], int n, int x) {
	int f = findFloor(arr, n, x);
	int c = findCeil(arr, n, x);
	return make_pair(f, c);
}

int main() {
	int arr[] = {3, 4, 4, 7, 8, 10};
	int n = 6, x = 5;
	pair<int, int> ans = getFloorAndCeil(arr, n, x);
	cout << "The floor and ceil are: " << ans.first
	     << " " << ans.second << endl;
	return 0;
}
```