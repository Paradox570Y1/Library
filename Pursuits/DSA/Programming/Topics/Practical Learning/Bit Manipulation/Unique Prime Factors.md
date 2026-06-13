[Link](https://www.geeksforgeeks.org/problems/prime-factors5052/1)
### Prime Factors

Difficulty: **Easy**Accuracy: **30.47%**Submissions: **52K+**Points: **2**

Given a number **N**. Find its **unique prime factors** in **increasing order.**  
 

**Example 1:**

**Input:** N = 100
**Output:** 2 5
**Explanation:** 2 and 5 are the unique prime
factors of 100.

**Example 2:**

**Input:** N = 35
**Output:** 5 7
**Explanation:** 5 and 7 are the unique prime
factors of 35.

**Your Task:**  
You don't need to read or print anything. Your task is to complete the function **AllPrimeFactors()** which takes N as input parameter and returns a list of all unique prime factors of N in increasing order.

**Expected Time Complexity:** O(N)  
**Expected Space Complexity:** O(N)  
 

**Constraints:**  
1 <= N  <= 106


# Better
TC-> O(√n \* log n)
worst TC is O(n) as suppose N=37 then loop has to run from 2 to 37 in order to get a prime factor.
```java
class Solution{
	public:
	bool isPrime(int n){
	    int k=2;
	    while(k*k<=n){
	        if(n%k++==0)return false;
	    }
	    return true;
	}
	vector<int>AllPrimeFactors(int N) {
	    // Code here
	    vector<int> ans;
	    int i=2;
	    while(N!=1){
	        if(N%i==0 && isPrime(i)){
	            ans.push_back(i);
	            while(N%i==0)N/=i;
	        }
	        i++;
	    }
	    return ans;
	}
};
```

# Optimal
TC-> O(√n \* log n)
in worst case  like 37 it will run 6 times only which is √n times only.
```java
class Solution{
	public:
	vector<int>AllPrimeFactors(int N) {
	    // Code here
	    vector<int> ans;
	    int i=2;
	    while(i*i<=N){
	        if(N%i==0){
	            ans.push_back(i);
	            while(N%i==0)N/=i;
	        }
	        i++;
	    }
	    if(N!=1)ans.push_back(N);
	    return ans;
	}
};
```