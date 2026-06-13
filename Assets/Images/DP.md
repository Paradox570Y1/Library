- [[DP Theory]]
- [[Fibonacci Number DP]] // to talk about space we need to store previous 2 value and we need one slot to store the current hence dp size will be 3 although can be done in 2 as well since we just need latest 2 value so directly override the earliest value
- [[Climbing Stairs]] // it's Fibonacci number as well
- [[Frog Jump]] 
- [[Frog Jump with k distances]] // create a dp of size n as we need to find n-1 distance.
// in case k is much smaller than n, then you can save some space by creating a dp of k size (k to store latest k elements). This dp will act as circular buffer.
>If we want to directly update in dp instead of taking a temp during calculation then we need dp of size k+1 as storing current calculated element in place of one of the k blocks  during the process of calculation will result in value of one of the previous k state getting altered which will fail our calculation.
- [[198. House Robber]]  //base case can be reduced in dp in some cases 
- [[213. House Robber II]] // base case can be designed in a way to accommodate any starting point at least for the dp where extra calculation is not needed we just have to pick an amount
#### 2D/3D DP

- [[ Ninja’s Training]] 
- [[62. Unique Paths]]
- [[63. Unique Paths II]] // in case of obstacle cut the way by setting it zero
//make sure if your restricting range for better dp implementation then it should not violate the logic, for example starting the inner dp loop from 1 to get j-1 always should not break the logic.
- [[64. Minimum Path Sum]] // at any point you can either reach from top or from left use that in dp
- [[Minimum path sum in Triangular Grid (120. Triangle)]] // in the optimal solution the cur dp overrides the prev but the overridden value is also needed for 1 next iteration so in such cases we can have an external dp array to save the value before changing in cur dp.
  // Although tabulation approach can be applied from top to bottom or bottom to top here but bottom to top is much better as we can compute all smaller pool of possibilities from larger pool of possibilities while vice versa may require extra overhead.
- [[931. Minimum Falling Path Sum]] // again take care to take minimum of the amount getting stored instead of just the next value
  // either use checks before calling helper function or create a base case for those checks both works fine.
- [[Ninja And His Friends(3D DP)]] // In 3D DP, instead of tracking one position per row, we store a 2D sheet per row that represents all combinations of the two active states moving together.

#### DP on subsequences
- [[Subsequence Theory]]
- [[Subset Sum Equal To K]] // To reach k we need k to reach it which is measured from 0, now what if we have k-2 then we just need 2 more to reach so till k we need to see if cur number can reach the k due to some other potential starting points in between.
  // So from each previous milestone we need to make the cur total(take) in case previous milestone is not there then cur should be kept as it was(not take).
- [[416. Partition Equal Subset Sum]]
- [[Array partition with minimum difference]] // use dp array to know which sum can be formed and then from 1 sum you can get the other and calculate min difference and minimize it.
- [[Count Subsets with Sum K]] // In this case 0 is also included then instead of setting dp\[0]  to be 1 again and again just process it like others
- [[Partitions With Given Difference]] // can be converted to count subset with sum k
- [[Assign cookies]] // just sort and assign no dp needed
- [[322. Coin Change]] // this can be done both way either selecting coins from outer loop or  selecting amount from outer loop
  // the new thing here is we don't just need count but need to minimize it so for that we need to start with maximum value and take dp\[0] = 0.
- [[494. Target Sum]] // it is twisted version of the count subsets with sum k so you can use that technique to solve it (most efficient for this question)
  //Another way is new DP approach build over subsets with sum k approach where we have to always take cur count and need to add this to at max two positions which is cur-num & cur + num and need to handle negatives with shifting of index. Be careful in start we **can not** take dp\[0] = 1.
- [[518. Coin Change II]] // nothing but count subsets with sum k

# Unbounded Knapsack pattern
- [[Unbounded Knapsack]] // although it can be done with heap but it's actually a dp question
  // it can be converted to subset sum k dp approach by taking the **limiting factor** weight as the sum which we will make while storing the profit and performing maximization over it.
- [[Rod cutting problem]] // it's also based on subset sum k approach and length of the rod is the limiting factor itself and we again need to reach the length while maximizing the profit

# DP on Strings
- [[DP Strings]]
- [[1143. Longest Common Subsequence]] // it's like a dp in a maze but instead of using previous 2 possibilities it uses 3 and that too with 2 conditions if characters are equal or not
- [[Print Longest Common Subsequence]] // Recursion code is almost same approach while building the word
  //But DP approach is extended here after building the LCS table we iterate from last to build the word and reverse it before returning
- [[Longest Common Substring]] // use only dp approach in this question as it gives TLE in recursion approach bcz memoization is tricky and requires even 3D dp.
- [[516. Longest Palindromic Subsequence]] //it's lcs  and take a second string as reverse of first.
- [[1312. Minimum Insertion Steps to Make a String Palindrome]] // same as LPS
- [[583. Delete Operation for Two Strings]] // same as LPS
- [[1092. Shortest Common Supersequence ]] // Interesting twist on lcs
- [[115. Distinct Subsequences]]  // new sequence here , take the string whose distinct subsequences are made in outer loop and dp size will be decided by the target string then in case letters are same then from prev dp take dp\[j] + dp\[j-1] otherwise it remains same as dp\[j].
  // You can even do it with single array if inner loop is reversed.
- [[72. Edit Distance(Levenshtein distance)]] // in this DP approach is tricky for the first time the base initialization of dp is incrementing instead of fixed and 0th index for inner loop is also incrementing after that if letters are same then result of i-1 and j-1 is used otherwise minimum of all three incoming directions is taken and 1 is added to that.
- [[44. Wildcard Matching]] // take the pattern to be matched in outer loop
  // the dp\[0] setup is lil complicated it's initially true but changes after inner loop if the current letter of pattern is \* then it remains what it was before the inner loop otherwise it changes to false.
  // if pattern letter is \* then it checks if either dp\[i]\[j-1] or dp\[i-1]\[j]  are true else becomes false
  // if pattern letter is ? or matches the string letter then it copies the value of dp\[i-1]\[j-1] else if not matched not ? and not \* then cur dp value is set to false.
  // How to this without DP or Greedy? Just take two pointers and in case of \* save the checkpoint of both pointers and if further matches are not found but a previous checkpoint exist then move back to that checkpoint with 1 more increment to the pointer of the string which means 1 more character is consumed by the \*.This continues until the string is exhausted or unable to make a match. After the string is exhausted then check if remaining characters in pattern is just \* (asterisk) which can be nullified to match the string.
- [[121. Best Time to Buy and Sell Stock]] // here keep track of min buying cost before current day and maximize profit by selling it at highest possible price after that by evaluating if profit made by selling at current price is higher than previous profit or not.
- [[122. Best Time to Buy and Sell Stock II]] // In this you can buy stocks multiple times and sell them multiple times but you cannot hold more than 1 stock which means if you want to buy a stock then you have to sell the previous one and vice versa.
	- There are two ways to make it's state either by taking length of the array for both state where first one will be for buy and second for sell , other way is to take two states again but one will be the stock space and second will be a flag which tells if you can buy stock or sell it.
	- There is also greedy approach which says buy stock and next day sell it and now buy that next day stock  continue the process and in case profit is more than 0 then add it to the result.
- [[123. Best Time to Buy and Sell Stock III]]
	- You can solve it with brute force in N² by getting max profit till i and then checking for next max profit after i.
	- You can make state like i, canBuy, k transactions.
	- You can use greedy and start from the beginning and calculate buy1 then sell1 and after that buy2 over sell1(add previous sold price of Trans. 1) and then sell2, either you can take buying as -ve value which you can maximize or you can take it +ve as well but then you need to minimize it.
	- You can use greedy in 2 pass fashion as well where you calculate max profit from both ends of array at any index the sum of profit from both sides is the profit attainable by two transactions at most.
- [[188. Best Time to Buy and Sell Stock IV]] //nothing special just expand above logic for k transactions
- [[309. Best Time to Buy and Sell Stock with Cooldown]]
	- In this the cooldown time will impact when we are selling stock as we cannot add profit from immediate previous buy instead add from previous to previous buy
- [[714. Best Time to Buy and Sell Stock with Transaction Fee]]
	- Same logic as Buy and Sell Stock 2 but with a transaction fee which will be deducted when buying or can say starting a new transaction.
- [[Make Target string from dictionary]]

# DP on LIS
- [[300. Longest Increasing Subsequence]] // In this problem dp will store the length of some sequence upto ith index. So ,Iterate in the array from left to right where at each index check for smaller number to the left of it and add 1 to the dp of that number and maximize the value at the ith index. This way you procure the longest sequence upto that ith number which will later support in finding sequences upto later numbers. Also, you need to add 1 to the answer because this doesn't account for the ith index itself. So either initialize the dp with 1 in the start or just add 1 while returning answer.
- [[368. Largest Divisible Subset]] // It's solution is done using dp only as recursion results in TLE and can't be memoized.
- [[1048. Longest String Chain]] // same as LIS just for words
- [[Longest Bitonic Subsequence]] // same as LIS from both sides in opposite condition
- [[673. Number of Longest Increasing Subsequence]] // It can become little tricky if not know how to form the count while doing LIS 
  // In this take another dp to store the count and if we are updating the value during LIS then copy count at j onto i , in case previous number is smaller but the length that it is forming with its index is already formed then increment the count at ith by that jth count.

# DP on MCM
- [[Matrix Chain Multiplication]] //In DP we Try to expand from smaller boundary to bigger while storing the smaller boundary result at two index it is bounded by. There are 2 dp approaches for this in one approach you calculate for all adjacent pairs of size 2 then all adjacent pairs of size 3 and so on. While in another approach for ith matrix you start the another pointer from closer to ith index and moves farther till bounds.
  // In MCM it's all about defining the partition boundary and using expanding strategy in a way we are able to reuse smaller bounds result in the bigger bounds partition.
- [[1547. Minimum Cost to Cut a Stick]] //in Recursion you have better control over the domain
- [[312. Burst Balloons]] // think about the last balloon to be popped within current boundaries which gives the max coins.
// do some precomputation to create a new array with boundaries of 1 included in both sides. Now take 0th and last index as bounds and between these select last balloon and reduce the boundary based on the selected balloon and do until i > j;
// So in recursive approach we select a balloon from whole domain and now  reverse the pop operation on it, now this balloon exist so for left and right sub domain to that balloon we can select next balloon taking current balloon as boundary balloon.
- [[1106. Parsing A Boolean Expression]] //it can be done using stack either from end or from start where you have to process operators and operands separately which can be simplified if we store the values to be processed in an ArrayList and pass ArrayList with operator in another function for evaluation.
// Optimal way to do it is using recursion where you have global iterator and not a general recursion. The idx movement is controlled manually at each step.
- [[Boolean Parenthesization]] // same as MCM just need to understand how to utilize the input data to get the output
- [[132. Palindrome Partitioning II]] // in this partition DP approach is used to do some precomputation which stores if subarray (i, j) is palindrome or not. Then 1D dp is used to count number of palindrome till ith index. To find the cuts required just subtract 1 from total number of minimum palindrome found.
- [[1043. Partition Array for Maximum Sum]] // In this question partition 1D dp is used. In this from index i we compute by taking maximum of all elements in variable length windows times window length till it is less then given max partition size + computed max value of rest of the array.
- [[85. Maximal Rectangle]] // It's mostly monotonic stack problem just calculating array for each row is the dp part of it.
- [[1277. Count Square Submatrices with All Ones]] // in this question we use 2 dimension to calculate the final answer first dimension is calculating all sizes of squares possible if (i, j) is bottom left coordinate of square and adding this res into the final result.
# Hard
- [[2035. Partition Array Into Two Arrays to Minimize Sum Difference]]
# Others

- [[264. Ugly Number II]]
- [[838. Push Dominoes]]
- [[3459. Length of Longest V-Shaped Diagonal Segment]]
- [[2327. Number of People Aware of a Secret]]
- [[3494. Find the Minimum Amount of Time to Brew Potions]]
- [[3186. Maximum Total Damage With Spell Casting]]
- [[3539. Find Sum of Array Product of Magical Sequences]] // Unsolved
- [[3003. Maximize the Number of Partitions After Operations]] // Unsolved
- [[1526. Minimum Number of Increments on Subarrays to Form a Target Array]]
- [[1578. Minimum Time to Make Rope Colorful]]
- [[474. Ones and Zeroes]]
- [[Print Longest Increasing Subsequence]]
- [[1653. Minimum Deletions to Make String Balanced]]
- [[3844. Longest Almost-Palindromic Substring]]