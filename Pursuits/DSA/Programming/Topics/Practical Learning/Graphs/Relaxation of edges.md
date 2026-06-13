In graph algorithms (especially shortest path algorithms like **Dijkstra’s** and **Bellman–Ford**), **relaxation of edges** is a key operation.

---

### **Definition**

Relaxation of an edge `(u, v)` with weight `w` means:

- You check whether the **currently known shortest distance** to vertex `v` can be **improved** by going through `u`.
    
- If yes, you update the distance to `v`.
    

---

### **Mathematical Formulation**

Suppose we maintain a distance array `dist[]` where `dist[x]` = shortest distance from the source to node `x` (initially ∞ for all except source = 0).

For an edge `(u, v)` with weight `w`:

![[Pasted image 20250907002005.png|340]]

This is called **relaxing the edge**.

---

### **Example**

Graph edge: `u → v` with weight 5.

- Current `dist[u] = 3`
    
- Current `dist[v] = 10`
    

Check: `dist[u] + 5 = 3 + 5 = 8 < 10` ✅

So, update: `dist[v] = 8`.  
This means we found a **shorter path** to `v` via `u`.

---

### **Where It’s Used**

- **Dijkstra’s Algorithm** → keeps relaxing edges using a priority queue until no improvement is possible.
    
- **Bellman-Ford Algorithm** → relaxes **all edges repeatedly (V-1 times)** to ensure shortest paths are found.
    
- **Floyd–Warshall Algorithm** → also based on repeated relaxations.
    

---

👉 Think of **edge relaxation** as "giving a vertex a chance to lower its distance if a better path through its neighbor exists."