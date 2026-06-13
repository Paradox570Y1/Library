- [[Introduction to Graphs]]
- [[BFS]]
- [[DFS]]
- [[Dial's algorithm]]

# Problems on BFS/DFS

- [[547. Number of Provinces]] // Count components with BFS or DFS
- [[994. Rotting Oranges]] // Count the time with BFS from rotten oranges, standard BFS question
- [[Flood Fill]] // From given  coordinate get original color and then start from there and transform all the neighbors with original color to provided color. This looks BFS but can easily be simulated with more optimum runtime with DFS.
- [[Undirected Graph Cycle]] // check if any visited node is not the parent , that's the culprit
- [[542. 01 Matrix]] // The question is asked in a way where we have to find the shortest distance of destination from source but we can rephrase it in opposite way to mark all the shortest distances from the destination itself and that's the key to solve it better in graph approach.
  //Other way is to use DP approach to solve this as we know distance can be calculated from 4 directions, so if we are building from top left then that means left and top direction is being computed during the process which we can use to get minimum distance from these two paths but we can't know the distance from future path here which is bottom and right so for that we will later restart from the bottom right of matrix and compute those path and minimize our result answer which was computed earlier based on left and top path.
- [[130. Surrounded Regions]] // We can do some precomputation from edges where we mark the regions which can cannot be captured either by using a boolean matrix or by changing it to some other character. Then do the DFS from internal nodes which can be region and capture them.
- [[1020. Number of Enclaves]] // Do precomputation by marking the land from the edges as sea and then calculating the count of land left.
- [[Word ladder - 1]] // In this question we want shortest path to transform initial word to final word through feasible transformations given in list. Therefore it's best to use BFS for shortest path.
  // Basic approach is to start from the initial word and explore it's all possible transformations which exist in given list level by level and enqueue those words and mark them visited to prevent re processing from same word which was visited earlier. If by this logic you are able to deque a word which is equal to final word then return the count of levels you traversed to achieve that else return 0 at the end.
  // Another approach is to again start with initial word and explore all transformations  within the given list at each time and if it is unvisited then enqueue that transformation and mark it visited. Repeat this process level by level. If by this logic you are able to deque a word which is equal to final word then return the count of levels you traversed to achieve that else return 0 at the end.
  // The optimal way to do this is by bi-directional queue. This approach involves three hash sets. In this we explore possibilities from both ends (i.e. both initial and final word). Initially you put the begin word in set1 and end word in set2 and all the words in list are put in set3. After that the loop runs until either you get the result or one of the set out of set1 and set2 becomes empty. Inside loop you will pick the smaller set out of set1 & set2  then for each word explore all possibilities, if any possibility exist in the bigger set then return the count otherwise check if the possibility exist in set3 then remove it from their and take a buffer to keep it. After this step is done for all words in smaller set now this buffer is assigned to that smaller set which signifies that now smaller set contains the possibilities at next level and increment the count as well which is the count of steps taken to reach that level. So if transformed word is found in bigger set then that's the result else at the end return 0.
- [[126. Word Ladder II]] // In this question the approach is to do the BFS from begin word till the level which contains the end word. During this process either you can create adjacency map or store level of visited nodes. After this you can use this adjacency map to traverse back from end word using DFS. If we are able to reach back begin node than add the list made to the result. 
- [[Find the number of islands]] // standard DFS
- [[785. Is Graph Bipartite]] // standard DFS with alternate assignment
- [[Directed Graph Cycle]] // In directed graph the flow is more restricted to particular direction so unlike undirected graph where we can mark the nodes visited globally, here we have to mark nodes in current path only and while backtracking un mark them.

# Topo Sort and Algos

- [[Topological Sorting]]
- [[207. Course Schedule]] // Kahn's algorithm is modified BFS where nodes with 0 dependencies are put in a queue and then neighbors dependency (i.e. in degree) is reduced based on visit and if there is 0 dependency then only the neighbor is put in the queue, if in case it fails to put any node in the queue then that implies it's not feasible to get rid of all the dependencies on that node and hence can't be done.
  // Another approach is to check if it is a DAG for which we can use DFS to check for cycles in directed graph.
	// During the process of Kahn's algo the so called no dependency nodes are enqueued well these nodes are also those nodes which are not involved in any cycle.
- [[210. Course Schedule II]] // Either use DFS with cycle detection and store the result or use BFS based Kahn's algorithm which has extra overhead due to storing inorder degree but often used in production and competitive programming environment because it is iterative and can handle a large data while DFS uses stack
- [[802. Find Eventual Safe States]] // one way to solve this is by implementing Kahn's algorithm after creating a reverse graph of given graph. Safe nodes are one which either points to another safe node or points to a terminal node. So we don't want nodes which has no dependency instead we want safe nodes which leads to other safe nodes. So we do backward traversal from ultimate safe nodes which are terminal nodes to other safe nodes.
  // From another perspective what's an unsafe nodes. These are those nodes which lead to cycle. So if we use DFS to check cycle in forward direction and in case we don't find any cycle in current path and reached terminal node then while backtracking we add those as safe nodes. To prevent sorting after result just take a boolean array and mark the safe vertex to true and then traverse in increasing order and add safe vertex to result directly.
	// or we can mark unsafe nodes which are in cycle
- [[Alien dictionary]] // compare consecutive strings lexically if encountered different character then add that relation to the graph and proceed to next consecutive pair. After building graph you can implement topological sorting using DFS or Kahn's algorithm.


# Shortest Path Algorithms and Problems
- [[Shortest Path Intuition]]
- [[Shortest Path in Undirected Graph]] // For unit weights just use BFS
	// For variable weights use Queue bases bellman-ford relaxation (O(V\*E)) only in case of +ve weights or use Topological Order + Relaxation of edges (O(V + E)).
- [[Shortest path in Directed Acyclic Graph]] // For unit weights just use BFS
	// For variable weights we can use Queue bases bellman-ford relaxation even in case of -ve weights but no -ve cycle 
	// Standard best approach is to use Topological Order + Relaxation of edges  which works fine for -ve weights but no -ve cycle 
- [[Dijkstra Algorithm]] //Time complexity is E log V
- [[Shortest Path in Weighted undirected graph]] // Use dijkstra algo to find shortest dist and use parent array to traverse the path from n to 1.
- [[1091. Shortest Path in Binary Matrix]] // Can be done with normal BFS as they are unit weights 
- [[1631. Path With Minimum Effort]]  // Can be done with both Dijkstra and Bellman ford algorithm even Prim works.
  // Other ways include  Kruskal algorithm as well but they are not very optimal and prims is dijkstra only.
	- Try this with Binary Search as well
- [[787. Cheapest Flights Within K Stops]] // Here you can't use dijkstra on prices as it prevents higher price to override lower price in case the path with the lower price can't even reach the destination. Instead of that think about route with less stops to reach the destination to keep the stops less than k and since it's weight is going to increase by 1 every time so normal BFS  can be implemented relaxation on prices as now we have fixed that the stops during updates are same so lower price always wins.
  //Optimal way is to link this problem to Bellman ford algorithm as K is going to limit the distance from source that we can reach therefore with bellman ford in worst case (each iteration changes only one edge) the maximum iterations that we need to make is k+1 (k stops in between mean path can reach k+1). We also want to avoid reusing the updated value within the same iteration which can be done by updating on a copy and taking prices from the original array.
	- Try with DFS as well
	- Try with **Bellman-Ford (relaxation)** (since K is small, just do k+1 relaxations).
	- DFS with Pruning (although non standard way)
- [[743. Network Delay Time]]
- [[1976. Number of Ways to Arrive at Destination]]
- [[Minimum Multiplications to reach End]]
- [[Bellman Ford Algorithm]] // you can explore distance from the explored nodes only and to do that you still have to check relation with all nodes except itself. Imp - in each iteration we do not move just 1 step from the explored node but it can be multiple steps as well in case it is using the updated value that was calculated within the same iteration. So to make it level order you just need to make updates on a copy of the original array and use previous computed value of original array.
- [[Floyd Warshall Algorithm]]
- [[1334. Find the City With the Smallest Number of Neighbors at a Threshold Distance]] // In this there is no single source so we need to think that threshold can be around each city and to count the neighbors within the threshold we need to know the distance of each city from others. So we need to make a matrix where for each ith city i will compute minimum distance to all reachable cities and then for each city i , we can check how many of cities distance is less than the threshold. If lower count of neighbor city is encountered the answer will point to that city.
# Shortest Path Algorithms and Problems

- [[Minimum Spanning Tree]] // Tree with N nodes and N-1 edges which connect all nodes with the minimum weights possible from the entire graph.
- [[Prim's Algorithm]] // implementation is 95 % Dijkstra algo with slight change of using visited array and marking nodes visited while enqueuing and adding enqueued node weight to sum if not visited earlier.
- [[Disjoint Set]] // We add lower rank or size node to upper rank or size node because it endures that recursive depth remains less while finding the ultimate parent. This reduces the depth of the graph in short.
- [[Disjoint Set Union]] // To print the components size we can check if parent of node is the node itself or not
- [[Kruskal's Algorithm]] // This algo makes use of Disjoint Sets and add minimum weight to sum while performing union. But it requires sorted edges which can take additional E log E time complexity but with dynamic graph this is the way.
- [[1319. Number of Operations to Make Network Connected]] // To check how many extra edge connections are there we can use an external counter of DSU and count number of subnets formed which is connected components using parent array. If extra edges are more than subnets-1 then return subnets-1 otherwise return -1.
- [[947. Most Stones Removed with Same Row or Column]] // one way to solve this is to treat each stone as node and based on the relation of same row which is x coordinate or same column which is y coordinate create adjacency list or matrix then find the number of components  and subtract that from total number of stones as from each component only 1 stone cannot be picked.
- [[721. Accounts Merge]] // Treat each account as nodes and figure the way to take union of accounts based on relation. Brute force way is to check if any mail in current account exist in another then take union of those two. Another way is to check if same mail repeats in another account number then take union of those (optimal way) by keeping mails in a map. After making the parent array now in case of brute force you need to add one account mails to other based on who is the parent account using `TreeSet` to maintain order and remove duplicates. In case of optimal you can iterate through all the mails in the map which are unique by itself and add them to their parent account number. After that create resultant array using account name and merged account.
- [[Number of Islands]]// can be done without simulating matrix with Kruskal  algo only.
- [[827. Making A Large Island]] // build the DSU from already built matrix instead of relation and after that at each point where we have water will fetch the size of land in 4 directions + 1 for current mock land and maximize it.
- [[778. Swim in Rising Water]] // Can be done easily with dijkstra algorithm
	// Other way to do is Kruskal Algorithm but to think that is tricky and time complexity is also inferior to Dijkstra.

# More Algorithms
- [[Tarjan Algorithm]] // Great algo used to find edge which can disconnect the graph into two components also called bridge and also can be used to find all group of SCC (strongly connected component) in case of directed graph but in case of undirected graph every component is SCC. Can also be used to find articulation point.
- [[Articulation Point]] // To find it use Tarjan algo, most of it remains same as for finding bridge, slight change comes when back edge is discovered reaching the current node (u) , here in case it reaches current node still current node can be articulation point bcz removal of it results in degeneration of graph.
- [[Kosaraju Algorithm]] // Finding number of SCC , we can also use Tarjan algo which is even better
  // Kosaraju Algo is nothing but using DFS to find components two times where first time leads to getting an order of elements based on the finishing time and in 2nd time we run the outer loop of finding components based on the order (we got in first iteration) over the reverse graph.
# Others

- [[1765. Map of Highest Peak]]
- [[407. Trapping Rain Water II]]
- [[417. Pacific Atlantic Water Flow]]
- [[3607. Power Grid Maintenance]]
- [[684. Redundant Connection]]
- [[Number Of Islands 2]]