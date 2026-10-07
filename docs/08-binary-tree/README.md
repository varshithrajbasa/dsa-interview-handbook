[← Back to Main Index](../index.md)

# Binary Tree - Most Important Questions and Answers

## 📖 Topic Overview

Binary Trees are non-linear hierarchical data structures where each node has at most two children (`left` and `right`). Questions test your recursion modeling, tree traversal patterns, subtree state propagation, and queue-based level order traversals.

### Core Algorithmic Patterns:
1. **Depth-First Search (DFS) Traversals:**
   - *Pre-Order (Node, Left, Right):* Serialization, tree cloning, prefix structures.
   - *In-Order (Left, Node, Right):* Sorted extraction in BSTs.
   - *Post-Order (Left, Right, Node):* Bottom-up information propagation (e.g., maximum depth, subtree validation, tree diameter, LCA).
2. **Breadth-First Search (BFS) / Level-Order:**
   - Level-by-level processing using a queue. Snapshot the queue length `size = len(q)` at each level.
3. **Lowest Common Ancestor (LCA):**
   - Searching both subtrees recursively; if both return non-null, the current root is the LCA.
4. **Tree Construction:**
   - Rebuilding unique binary trees from combinations like Preorder + Inorder traversals using divide-and-conquer index boundaries.
5. **Path Sums & Diameters:**
   - Passing running sums down vs returning max contributions up.

---

## 🎯 High-Yield Problem Checklist

- [ ] **Maximum Depth of Binary Tree (LeetCode #104):** Post-order bottom-up height aggregation
- [ ] **Invert / Flip Binary Tree (LeetCode #226):** Recursive child swap
- [ ] **Same Tree (LeetCode #100):** Simultaneous dual-tree DFS traversal
- [ ] **Subtree of Another Tree (LeetCode #572):** Tree matching with hashing or identical checks
- [ ] **Lowest Common Ancestor of a Binary Tree (LeetCode #236):** Recursive bottom-up target bubble
- [ ] **Binary Tree Level Order Traversal (LeetCode #102):** Queue-based BFS level snapshot
- [ ] **Binary Tree Right Side View (LeetCode #199):** BFS level-end or DFS right-first preorder
- [ ] **Count Good Nodes in Binary Tree (LeetCode #1448):** Preorder path max tracking
- [ ] **Diameter of Binary Tree (LeetCode #543):** Global maximum updated via post-order heights
- [ ] **Balanced Binary Tree (LeetCode #110):** Height difference $-1$ early termination
- [ ] **Binary Tree Maximum Path Sum (LeetCode #124):** Non-negative branch contribution
- [ ] **Serialize and Deserialize Binary Tree (LeetCode #297):** BFS/DFS string delimiter encoding
- [ ] **Construct Binary Tree from Preorder and Inorder Traversal (LeetCode #105):** Divide-and-conquer hash map split

---

## 📝 Reusable Question Template Skeleton

Copy and use this template whenever adding a new question to this module:

```markdown
### Problem Name (e.g., LeetCode #XX - Problem Title)

#### 1. Problem Statement
- **Description:** Provide a precise description of the problem.
- **Node Definition:**
  - `val`: node value
  - `left`: left child pointer
  - `right`: right child pointer
- **Constraints:**
  - Number of nodes in range `[0, 10^4]`
  - `-10^4 <= Node.val <= 10^4`

#### 2. Intuition & Approach
- **Key Insight:** DFS (Pre/In/Post-order) vs. BFS Level-Order.
- **Base Cases:** `if not root: return ...`
- **Subproblem Division:**
  - Left subtree result: `dfs(root.left)`
  - Right subtree result: `dfs(root.right)`
  - Node processing: combine left and right results with `root.val`.
- **Global State vs Return Value:** Clarify if an answer is tracked via global variable (like diameter) or returned directly.

#### 3. Time & Space Complexity
- **Time Complexity:** $O(N)$ — every node is visited a constant number of times.
- **Space Complexity:** $O(H)$ — where $H$ is tree height ($O(\log N)$ for balanced, $O(N)$ for skewed tree call stack).

#### 4. Code Implementation

=== "Python"
    ```python
    from typing import Optional

    class TreeNode:
        def __init__(self, val=0, left=None, right=None):
            self.val = val
            self.left = left
            self.right = right

    class Solution:
        def solve(self, root: Optional[TreeNode]) -> int:
            # TODO: Implement optimal solution
            pass
    ```

=== "C++"
    ```cpp
    struct TreeNode {
        int val;
        TreeNode *left;
        TreeNode *right;
        TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
    };

    class Solution {
    public:
        int solve(TreeNode* root) {
            // TODO: Implement optimal solution
            return 0;
        }
    };
    ```

=== "Java"
    ```java
    class TreeNode {
        int val;
        TreeNode left;
        TreeNode right;
        TreeNode(int x) { val = x; }
    }

    class Solution {
        public int solve(TreeNode root) {
            // TODO: Implement optimal solution
            return 0;
        }
    }
    ```

=== "TypeScript"
    ```typescript
    class TreeNode {
        val: number;
        left: TreeNode | null;
        right: TreeNode | null;
        constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
            this.val = (val === undefined ? 0 : val);
            this.left = (left === undefined ? null : left);
            this.right = (right === undefined ? null : right);
        }
    }

    function solve(root: TreeNode | null): number {
        // TODO: Implement optimal solution
        return 0;
    }
    ```
```

---

## 💡 Example: Maximum Depth of Binary Tree (LeetCode #104)

### 1. Problem Statement
Given the `root` of a binary tree, return its maximum depth. A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

### 2. Intuition & Approach
- A tree's maximum depth can be expressed recursively:
  - If the node is `null`, its depth is 0.
  - Otherwise, its depth is $1 + \max(\text{depth}(\text{left}), \text{depth}(\text{right}))$.
- This post-order traversal computes child depths before determining the parent node's depth.

### 3. Time & Space Complexity
- **Time Complexity:** $O(N)$ — each of the $N$ nodes is visited once.
- **Space Complexity:** $O(H)$ — recursion call stack bounded by tree height $H$ ($O(\log N)$ best, $O(N)$ worst).

### 4. Code Implementation

=== "Python"
    ```python
    from typing import Optional

    class TreeNode:
        def __init__(self, val=0, left=None, right=None):
            self.val = val
            self.left = left
            self.right = right

    class Solution:
        def maxDepth(self, root: Optional[TreeNode]) -> int:
            if not root:
                return 0
            left_depth = self.maxDepth(root.left)
            right_depth = self.maxDepth(root.right)
            return 1 + max(left_depth, right_depth)
    ```

=== "C++"
    ```cpp
    #include <algorithm>

    struct TreeNode {
        int val;
        TreeNode *left;
        TreeNode *right;
        TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
    };

    class Solution {
    public:
        int maxDepth(TreeNode* root) {
            if (!root) return 0;
            return 1 + std::max(maxDepth(root->left), maxDepth(root->right));
        }
    };
    ```

=== "Java"
    ```java
    class TreeNode {
        int val;
        TreeNode left;
        TreeNode right;
        TreeNode(int x) { val = x; }
    }

    class Solution {
        public int maxDepth(TreeNode root) {
            if (root == null) return 0;
            return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
        }
    }
    ```

=== "TypeScript"
    ```typescript
    class TreeNode {
        val: number;
        left: TreeNode | null;
        right: TreeNode | null;
        constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
            this.val = (val === undefined ? 0 : val);
            this.left = (left === undefined ? null : left);
            this.right = (right === undefined ? null : right);
        }
    }

    function maxDepth(root: TreeNode | null): number {
        if (!root) return 0;
        return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
    }
    ```
