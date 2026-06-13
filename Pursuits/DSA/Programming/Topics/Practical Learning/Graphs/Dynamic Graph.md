A **dynamic graph** is a graph whose structure changes over time. Unlike a static graph (where the set of vertices and edges remains fixed), a dynamic graph allows updates such as:

- **Adding or removing vertices**
- **Adding or removing edges**
- **Changing edge weights or directions**

This makes dynamic graphs useful in real-world applications where relationships evolve over time.

### Examples in real life:

- **Social networks** → Friendships (edges) are added/removed as people connect or disconnect.
- **Computer networks** → Routers and connections may join/leave the network.
- **Road traffic networks** → Roads (edges) may be closed/opened, and travel times (weights) may change dynamically.
- **Streaming data analysis** → Graphs updated in real time with new information.

### Types of dynamic graphs:

1. **Incremental** → Only additions are allowed (new vertices/edges).
2. **Decremental** → Only deletions are allowed.
3. **Fully dynamic** → Both additions and deletions are allowed.