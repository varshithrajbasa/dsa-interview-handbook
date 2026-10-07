[← Back to Main Index](../index.md)

# Binary Search Tree - Most Important Questions and Answers

## 📖 Topic Overview

A Binary Search Tree (BST) is a binary tree where every node satisfies the invariant: all keys in the left subtree are strictly less than the node's key, and all keys in the right subtree are strictly greater than the node's key:
$$\forall u \in \text{left}(v), \text{val}(u) < \text{val}(v) \quad \text{and} \quad \forall w \in \text{right}(v), \text{val}(w) > \text{val}(v)$$

### Core Algorithmic Patterns:
1. **In-Order Traversal is Monotonically Sorted:** Performing an in-order traversal (`left`, `root`, `right`) yields values in strictly increasing order. This enables $O(K)$ retrieval of the $K^{\text{th}}$ smallest element.
2. **BST Validation via Range Propagation:** Passing `(min_val, max_val)` bounds down the tree during DFS; checking only immediate children is insufficient.
3. **Logarithmic Search & Insertion:** Navigating left or right in $O(H)$ time depending on whether target is smaller or greater than `root.val`.
4. **Node Deletion Cases:**
   - Leaf node: remove directly.
   - One child: replace node with its child.
   - Two children: replace with in-order successor (smallest node in right subtree) and delete that successor.
5. **Lowest Common Ancestor (LCA) in BST:** Utilizing the BST order property to find LCA in $O(H)$ time without searching both subtrees unconditionally.

---

## 🎯 High-Yield Problem Checklist

- [ ] **Search in a Binary Search Tree (LeetCode #700):** Basic recursive/iterative BST walk
- [ ] **Insert into a Binary Search Tree (LeetCode #701):** Leaf pointer attachment
- [ ] **Delete Node in a BST (LeetCode #450):** 3-case deletion with in-order successor swap
- [ ] **Validate Binary Search Tree (LeetCode #98):** Range propagation `(low, high)` DFS
- [ ] **Kth Smallest Element in a BST (LeetCode #230):** In-order traversal counter
- [ ] **Lowest Common Ancestor of a BST (LeetCode #235):** Directional split branching
- [ ] **Construct BST from Preorder Traversal (LeetCode #1008):** Upper bound DFS construction
- [ ] **Convert Sorted Array to Binary Search Tree (LeetCode #108):** Balanced midpoint divide & conquer

---

## 📝 Reusable Question Template Skeleton

Copy and use this template whenever adding a new question to this module:

```markdown
### Problem Name (e.g., LeetCode #XX - Problem Title)

#### 1. Problem Statement
- **Description:** Provide a precise description of the problem.
- **Node Definition:**
  - Standard `TreeNode` with `val`, `left`, `right`.
- **Constraints:**
  - `1 <= Number of Nodes <= 10^4`
  - Unique BST keys within `[-10^9, 10^9]`

#### 2. Intuition & Approach
- **Key Insight:** Exploit the BST invariant: when to branch left vs right.
- **Traversal Strategy:**
  - In-order traversal for sorted sequence tasks.
  - Directional pruning: if `target < root.val` go left; if `target > root.val` go right.
- **Range Maintenance:** When validating, pass `(min_limit, max_limit)`.

#### 3. Time & Space Complexity
- **Time Complexity:** $O(H)$ — where $H$ is the tree height ($O(\log N)$ average for balanced BST, $O(N)$ worst case for degenerate line).
- **Space Complexity:** $O(H)$ — call stack depth.

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
        def solve(self, root: Optional[TreeNode]) -> bool:
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
        bool solve(TreeNode* root) {
            // TODO: Implement optimal solution
            return true;
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
        public boolean solve(TreeNode root) {
            // TODO: Implement optimal solution
            return true;
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

    function solve(root: TreeNode | null): boolean {
        // TODO: Implement optimal solution
        return true;
    }
    ```
```

---

## 💡 Example: Validate Binary Search Tree (LeetCode #98)

### 1. Problem Statement
Given the `root` of a binary tree, determine if it is a valid binary search tree (BST).
A valid BST is defined as follows:
- The left subtree of a node contains only nodes with keys strictly less than the node's key.
- The right subtree of a node contains only nodes with keys strictly greater than the node's key.
- Both the left and right subtrees must also be binary search trees.

### 2. Intuition & Approach
- It is insufficient to simply check if `root.left.val < root.val < root.right.val`. All nodes in the left subtree must be less than the root, and all in the right must be greater.
- Propagate a valid interval `(low, high)` through recursion:
  - The root can take any value: `(-inf, +inf)`.
  - When going left: `high` becomes `root.val`.
  - When going right: `low` becomes `root.val`.

### 3. Time & Space Complexity
- **Time Complexity:** $O(N)$ — visits each node once.
- **Space Complexity:** $O(H)$ — where $H$ is the tree height.

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
        def isValidBST(self, root: Optional[TreeNode]) -> bool:
            def validate(node, low=float('-inf'), high=float('inf')) -> bool:
                if not node:
                    return True
                if not (low < node.val < high):
                    return False
                return validate(node.left, low, node.val) and validate(node.right, node.val, high)
                
            return validate(root)
    ```

=== "C++"
    ```cpp
    #include <climits>

    struct TreeNode {
        int val;
        TreeNode *left;
        TreeNode *right;
        TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
    };

    class Solution {
    public:
        bool isValidBST(TreeNode* root) {
            return validate(root, LONG_MIN, LONG_MAX);
        }

    private:
        bool validate(TreeNode* node, long low, long high) {
            if (!node) return true;
            if (node->val <= low || node->val >= high) return false;
            return validate(node->left, low, node->val) && validate(node->right, node->val, high);
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
        public boolean isValidBST(TreeNode root) {
            return validate(root, null, null);
        }

        private boolean validate(TreeNode node, Integer low, Integer high) {
            if (node == null) return true;
            if ((low != null && node.val <= low) || (high != null && node.val >= high)) {
                return false;
            }
            return validate(node.left, low, node.val) && validate(node.right, node.val, high);
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

    function isValidBST(root: TreeNode | null): boolean {
        function validate(node: TreeNode | null, low: number, high: number): boolean {
            if (!node) return true;
            if (node.val <= low || node.val >= high) return false;
            return validate(node.left, low, node.val) && validate(node.right, node.val, high);
        }
        return validate(root, -Infinity, Infinity);
    }
    ```
