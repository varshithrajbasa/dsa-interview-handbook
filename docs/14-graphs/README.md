[← Back to Main Index](../index.md)

# Graphs - Most Important Questions and Answers

## 📖 Topic Overview

A Graph $G = (V, E)$ consists of vertices (nodes) and edges (connections). Graphs can be directed or undirected, cyclic or acyclic, and weighted or unweighted.

### Core Algorithmic Patterns:
1. **Graph Representations:**
   - Adjacency List: Space-efficient $O(V + E)$, fast neighbor iteration.
   - Adjacency Matrix: $O(V^2)$ space, $O(1)$ edge existence check.
2. **Breadth-First Search (BFS):**
   - Unweighted shortest paths and multi-source simultaneous diffusion (e.g., Rotting Oranges, Word Ladder).
3. **Depth-First Search (DFS) & Connected Components:**
   - Flood-fill (Number of Islands), cycle detection (3-color state: unvisited, visiting, visited).
4. **Topological Sort (DAGs):**
   - **Kahn’s Algorithm (BFS):** Track in-degrees of all nodes. Initialize queue with nodes having in-degree 0; decrement neighbor in-degrees upon dequeue. Detects cycles if processed nodes $< V$.
   - **DFS Post-Order:** Reverse post-order traversal with cycle detection.
5. **Dijkstra’s Algorithm:**
   - Shortest path on weighted graphs with non-negative edge weights using a Min-Heap / Priority Queue in $O((V + E) \log V)$ time.
6. **Union-Find / Disjoint Set Union (DSU):**
   - Near $O(1)$ operations with *Path Compression* and *Union by Rank*: $\alpha(V)$ (inverse Ackermann function). Ideal for dynamic connectivity and Kruskal's Minimum Spanning Tree.

---

## 🎯 High-Yield Problem Checklist

- [ ] **Number of Islands (LeetCode #200):** Grid DFS/BFS connected components
- [ ] **Clone Graph (LeetCode #133):** Hash map DFS/BFS deep copy
- [ ] **Max Area of Island (LeetCode #695):** Recursive component size accumulation
- [ ] **Pacific Atlantic Water Flow (LeetCode #417):** Reverse ocean reachability DFS
- [ ] **Surrounded Regions (LeetCode #130):** Border escape flood-fill
- [ ] **Rotting Oranges (LeetCode #994):** Multi-source queue-based BFS
- [ ] **Course Schedule (LeetCode #207):** Topological sort / cycle detection in directed graph
- [ ] **Course Schedule II (LeetCode #210):** Kahn's algorithm producing topological order
- [ ] **Graph Valid Tree (LeetCode #261):** Cycle detection and connectivity count (DSU / BFS)
- [ ] **Number of Connected Components in an Undirected Graph (LeetCode #323):** DSU or BFS/DFS
- [ ] **Redundant Connection (LeetCode #684):** Cycle detection via Union-Find
- [ ] **Word Ladder (LeetCode #127):** BFS shortest transformation sequence
- [ ] **Network Delay Time (LeetCode #743):** Dijkstra's priority queue shortest paths
- [ ] **Reconstruct Itinerary (LeetCode #332):** Hierholzer's algorithm for Eulerian path
- [ ] **Min Cost to Connect All Points (LeetCode #1584):** Prim's or Kruskal's MST

---

> [!TIP]
> **Want to contribute a solution or add a new question to this topic?**  
> Check our standardized format and guidelines in the [How to Contribute & Question Template Guide](../contributing.md).

---

## 💡 Example: Number of Islands (LeetCode #200)

### 1. Problem Statement
Given an $m \times n$ 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

### 2. Intuition & Approach
- Traverse each cell of the grid.
- When an unvisited land cell `'1'` is found, increment the island counter and launch a DFS/BFS traversal to sink all connected land cells by flipping them to `'0'` (or marking them in a visited set).
- Once the traversal finishes, all cells in that island have been processed.

### 3. Time & Space Complexity
- **Time Complexity:** $O(M \times N)$ — each cell is visited a constant number of times.
- **Space Complexity:** $O(M \times N)$ — worst-case recursion call stack when the entire grid is land.

### 4. Code Implementation

=== "Python"
    ```python
    from typing import List

    class Solution:
        def numIslands(self, grid: List[List[str]]) -> int:
            if not grid:
                return 0
                
            rows, cols = len(grid), len(grid[0])
            island_count = 0
            
            def dfs(r: int, c: int):
                if r < 0 or r >= rows or c < 0 or c >= cols or grid[r][c] != '1':
                    return
                grid[r][c] = '0'  # Sink the cell
                dfs(r + 1, c)
                dfs(r - 1, c)
                dfs(r, c + 1)
                dfs(r, c - 1)
                
            for r in range(rows):
                for c in range(cols):
                    if grid[r][c] == '1':
                        island_count += 1
                        dfs(r, c)
                        
            return island_count
    ```

=== "C++"
    ```cpp
    #include <vector>

    class Solution {
    public:
        int numIslands(std::vector<std::vector<char>>& grid) {
            if (grid.empty()) return 0;
            int rows = grid.size();
            int cols = grid[0].size();
            int count = 0;
            
            for (int r = 0; r < rows; ++r) {
                for (int c = 0; c < cols; ++c) {
                    if (grid[r][c] == '1') {
                        count++;
                        dfs(grid, r, c, rows, cols);
                    }
                }
            }
            return count;
        }

    private:
        void dfs(std::vector<std::vector<char>>& grid, int r, int c, int rows, int cols) {
            if (r < 0 || r >= rows || c < 0 || c >= cols || grid[r][c] != '1') {
                return;
            }
            grid[r][c] = '0';
            dfs(grid, r + 1, c, rows, cols);
            dfs(grid, r - 1, c, rows, cols);
            dfs(grid, r, c + 1, rows, cols);
            dfs(grid, r, c - 1, rows, cols);
        }
    };
    ```

=== "Java"
    ```java
    class Solution {
        public int numIslands(char[][] grid) {
            if (grid == null || grid.length == 0) return 0;
            int rows = grid.length;
            int cols = grid[0].length;
            int count = 0;

            for (int r = 0; r < rows; r++) {
                for (int c = 0; c < cols; c++) {
                    if (grid[r][c] == '1') {
                        count++;
                        dfs(grid, r, c, rows, cols);
                    }
                }
            }
            return count;
        }

        private void dfs(char[][] grid, int r, int c, int rows, int cols) {
            if (r < 0 || r >= rows || c < 0 || c >= cols || grid[r][c] != '1') {
                return;
            }
            grid[r][c] = '0';
            dfs(grid, r + 1, c, rows, cols);
            dfs(grid, r - 1, c, rows, cols);
            dfs(grid, r, c + 1, rows, cols);
            dfs(grid, r, c - 1, rows, cols);
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function numIslands(grid: string[][]): number {
        if (!grid || grid.length === 0) return 0;
        const rows = grid.length;
        const cols = grid[0].length;
        let count = 0;

        function dfs(r: number, c: number): void {
            if (r < 0 || r >= rows || c < 0 || c >= cols || grid[r][c] !== '1') {
                return;
            }
            grid[r][c] = '0';
            dfs(r + 1, c);
            dfs(r - 1, c);
            dfs(r, c + 1);
            dfs(r, c - 1);
        }

        for (let r = 0; r < rows; r++) {
            for (let c = 0; c < cols; c++) {
                if (grid[r][c] === '1') {
                    count++;
                    dfs(r, c);
                }
            }
        }

        return count;
    }
    ```
