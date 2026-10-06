## 01. Undirected Graph Cycle

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/detect-cycle-in-an-undirected-graph/1)

### Problem Description

**Task:** Given an undirected graph with V vertices and E edges, represented as a 2D vector edges[][], where each entry edges[i] = [u, v] denotes an edge between vertices u and v, determine whether the graph contains a cycle or not.

> **Note:** The graph can have multiple component.

#### Examples

##### Example 1

- **Input:**
```text
V = 4, E = 4, edges[][] = [[0, 1], [0, 2], [1, 2], [2, 3]]
```
- **Output:**
```text
true 1 - > 2 - > 0 - > 1 is a cycle.
```

##### Example 2

- **Input:**
```text
V = 4, E = 3, edges[][] = [[0, 1], [1, 2], [2, 3]]
```
- **Output:**
```text
false No cycle in the graph.
```

#### Constraints

- **1.** `1 ≤ V, E ≤ 1050 ≤ edges[i][0], edges[i][1] < V`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(V + E)
- **Expected Auxiliary Space Complexity:** O(V)

### Accepted Solutions (2)

#### Solution 1 (Java)

- **Submitted:** 2026-10-06 13:44:01
- **Status:** Correct
- **Marks:** 0

```java
class Solution {
    class Pair{
        int node;
        int parent;
        Pair(int node, int parent){
            this.node = node;
            this.parent = parent;
        }
        
    }
    public boolean isCycle(int V, int[][] edges) {
        ArrayList<ArrayList<Integer>> adj = new ArrayList<>();
        for(int i = 0; i<V; i++){
            adj.add(new ArrayList<>());
        }
        for(int[] edge : edges){
            int u = edge[0];
            int v = edge[1];
            
            adj.get(u).add(v);
            adj.get(v).add(u);
        }
        int [] vis = new int[V];
        for(int i = 0; i<V; i++){
            if(vis[i] == 0){
                Queue<Pair> q = new LinkedList<>();
                q.add(new Pair(i , -1));
                vis[i] = 1;
            
        while(!q.isEmpty()){
            Pair current = q.poll();
            int node = current.node;
            int parent = current.parent;
            
            for(int neighbour:adj.get(node)){
                if(vis[neighbour] == 0){
                    vis[neighbour] = 1;
                    q.add(new Pair(neighbour , node));
                }
                else if(neighbour != parent){
                    return true;
                }
            }
        }
        }
        }
        
        return false;
        
    }
}
```

#### Solution 2 (Java)

- **Submitted:** 2026-10-06 12:31:01
- **Status:** Correct
- **Marks:** 4

```java
class Solution {

    class Pair {
        int node;
        int parent;

        Pair(int node, int parent) {
            this.node = node;
            this.parent = parent;
        }
    }

    public boolean isCycle(int V, int[][] edges) {

        // Create adjacency list
        ArrayList<ArrayList<Integer>> adj = new ArrayList<>();

        for (int i = 0; i < V; i++) {
            adj.add(new ArrayList<>());
        }

        for (int[] edge : edges) {
            int u = edge[0];
            int v = edge[1];

            adj.get(u).add(v);
            adj.get(v).add(u);
        }

        int[] vis = new int[V];

        // Graph can be disconnected
        for (int i = 0; i < V; i++) {

            if (vis[i] == 0) {

                Queue<Pair> q = new LinkedList<>();

                q.add(new Pair(i, -1));
                vis[i] = 1;

                while (!q.isEmpty()) {

                    Pair current = q.poll();

                    int node = current.node;
                    int parent = current.parent;

                    for (int neighbour : adj.get(node)) {

                        // Not visited -> visit it
                        if (vis[neighbour] == 0) {

                            vis[neighbour] = 1;

                            q.add(new Pair(neighbour, node));
                        }

                        // Already visited and not parent -> cycle
                        else if (neighbour != parent) {

                            return true;
                        }
                    }
                }
            }
        }

        return false;
    }
}
```

*Generated on: 06/10/2026, 13:44:29*