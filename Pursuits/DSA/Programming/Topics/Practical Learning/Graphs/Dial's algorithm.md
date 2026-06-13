We’ll assume:

- Graph is undirected
    
- Edge weights are **non-negative integers**
    
- Maximum edge weight = `W` (small)
    

---

# 🧠 Core Idea Recap

Instead of a `PriorityQueue`, we use:

```java
List<Integer>[] buckets
```

Each bucket index represents a distance.

If shortest distance to a node is `d`, we put it in:

```java
buckets[d]
```

We then scan buckets in increasing order.

---

# ✅ Java Implementation (Dial’s Algorithm)

```java
import java.util.*;

class Solution {

    static class Edge {
        int to, weight;
        Edge(int to, int weight) {
            this.to = to;
            this.weight = weight;
        }
    }

    public int[] dial(int n, List<Edge>[] adj, int maxWeight, int src) {

        int INF = Integer.MAX_VALUE;
        int maxDistance = maxWeight * n;  // worst-case possible distance

        int[] dist = new int[n];
        Arrays.fill(dist, INF);
        dist[src] = 0;

        // Buckets: distance -> list of nodes
        List<Integer>[] buckets = new ArrayList[maxDistance + 1];
        for (int i = 0; i <= maxDistance; i++) {
            buckets[i] = new ArrayList<>();
        }

        buckets[0].add(src);

        int idx = 0;

        while (idx <= maxDistance) {

            // Find next non-empty bucket
            while (idx <= maxDistance && buckets[idx].isEmpty()) {
                idx++;
            }

            if (idx > maxDistance) break;

            int u = buckets[idx].remove(0);

            if (idx > dist[u]) continue;

            for (Edge edge : adj[u]) {
                int v = edge.to;
                int weight = edge.weight;

                int newDist = dist[u] + weight;

                if (newDist < dist[v]) {
                    dist[v] = newDist;
                    buckets[newDist].add(v);
                }
            }
        }

        return dist;
    }
}
```
# 📌 How To Use It

You must know:

```txt
maxWeight = maximum edge weight in graph
```

If weights are in range `[0, W]`, pass that as `maxWeight`.

---

# ⏱ Time Complexity

```scss
O(V + E + W*V)
```

More precisely:

```scss
O(V + E + maximum_distance)
```

If `W` is small → almost linear time.

---

# ⚠ Important Limitations

Do NOT use this if:

- Edge weights are large (like 10^9)
    
- maxWeight * n becomes huge
    

Because:

```scss
maxDistance = W * n
```

Buckets would become massive.

---

# 🔥 Special Case: 0–1 BFS

If weights are only `0` or `1`, use this instead:

```java
Deque<Integer> dq = new ArrayDeque<>();
```

Push front for weight 0  
Push back for weight 1

That gives pure:

```java
O(V + E)
```

Even cleaner.

---

# 🧠 When Dial Beats Dijkstra

If:

- `V = 10^5`
    
- `E = 2 * 10^5`
    
- `W <= 10`
    

Dial’s will destroy heap-based Dijkstra.