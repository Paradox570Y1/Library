`Those who cannot remember the past are condemned to repeat it.`

# Ways to solve DP problems

- Tabulation  - Bottom Up DP
- Memoization - Top Down DP


After tabulation to get the optimal , we need to further optimize the space.
![[Pasted image 20250311144738.png]]


# Memoization
- We tend to store the value of already solved subproblem to solve it directly  in case it appears again.
- Steps to do convert any recursion into dynamic problem solution:
	- declare the size of dp array considering the size of the sub problems
	- storing the answer which is getting computed for subproblem
	- checking if subproblem has been previously solved then the value will not be -1 in case if you have assigned default of the array to be -1.


# Tabulation 
- Here you start from the base case and go to the required answer which is opposite of recursion as recursion is top down approach.
- You can use an array to store the data but it's not always needed sometimes after observing a pattern you can just use few variables to calculate the same thing as done with the help of array.