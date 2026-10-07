[← Back to Main Index](../index.md)

# Dynamic Programming - Most Important Questions and Answers

## 📖 Topic Overview

Dynamic Programming (DP) solves complex optimization problems by breaking them down into simpler subproblems, solving each subproblem once, and storing their solutions (memoization or tabulation) to prevent redundant recomputation.

### Core Prerequisites:
1. **Optimal Substructure:** An optimal solution to the overall problem incorporates optimal solutions to its subproblems.
2. **Overlapping Subproblems:** The recursive solution spaces repeatedly revisit identical smaller subproblems.

### Core Patterns:
1. **1D Linear State DP:**
   - State: `dp[i]` depends on `dp[i - 1]`, `dp[i - 2]` (e.g., Climbing Stairs, House Robber, Decode Ways).
   - Space optimization: If only the last $K$ values are required, reduce $O(N)$ space to $O(1)$ variables.
2. **0/1 Knapsack & Unbounded Knapsack:**
   - 0/1: Iterate backwards through weights to ensure each item is picked at most once (e.g., Partition Equal Subset Sum).
   - Unbounded: Iterate forward allowing repeated picking (e.g., Coin Change).
3. **Longest Common Subsequence (LCS) & Edit Distance:**
   - 2D grid matching characters: `dp[i][j] = dp[i-1][j-1] + 1` if match, else `max(dp[i-1][j], dp[i][j-1])`.
4. **Longest Increasing Subsequence (LIS):**
   - $O(N^2)$ standard DP or $O(N \log N)$ patience sort with binary search (`bisect_left`).
5. **2D Grid Paths:**
   - `dp[r][c] = dp[r-1][c] + dp[r][c-1]` for Unique Paths with space compression to a single 1D row.

---

## 🎯 High-Yield Problem Checklist

- [ ] **Climbing Stairs (LeetCode #70):** Fibonacci state progression in $O(1)$ space
- [ ] **Min Cost Climbing Stairs (LeetCode #746):** Running minimum step costs
- [ ] **House Robber (LeetCode #198):** Rob vs skip non-adjacent transition
- [ ] **House Robber II (LeetCode #213):** Circular array split into two linear passes
- [ ] **Coin Change (LeetCode #322):** Unbounded knapsack minimum coins
- [ ] **Maximum Product Subarray (LeetCode #152):** Tracking both min and max running products
- [ ] **Decode Ways (LeetCode #91):** Single-digit and dual-digit valid transitions
- [ ] **Word Break (LeetCode #139):** Substring dictionary matching DP
- [ ] **Longest Increasing Subsequence (LeetCode #300):** $O(N \log N)$ binary search patience sorting
- [ ] **Partition Equal Subset Sum (LeetCode #416):** 0/1 Knapsack boolean subset sum
- [ ] **Unique Paths (LeetCode #62):** Grid path combinations with 1D row optimization
- [ ] **Longest Common Subsequence (LeetCode #1143):** 2D character matching table
- [ ] **Best Time to Buy and Sell Stock with Cooldown (LeetCode #309):** State machine DP (Hold, Sold, Rest)
- [ ] **Edit Distance (LeetCode #72):** Insert, delete, replace minimum transformations

---

## 📝 Reusable Question Template Skeleton

Copy and use this template whenever adding a new question to this module:

```markdown
### Problem Name (e.g., LeetCode #XX - Problem Title)

#### 1. Problem Statement
- **Description:** Provide a precise description of the problem.
- **Input:** Sequences, values, capacity, or cost matrices.
- **Output:** Maximum profit, minimum cost, total ways, or boolean feasibility.
- **Constraints:**
  - $N \le 10^3$ to $10^5$

#### 2. Intuition & Approach
- **State Definition:** What does `dp[i]` (or `dp[i][j]`) represent precisely?
- **Base Cases:** Smallest subproblems (e.g. `dp[0] = 0`, `dp[1] = ...`).
- **Recurrence Relation:** Formula to transition from subproblems to `dp[i]`.
- **Computation Direction:** Top-Down (memoized recursion) vs Bottom-Up (iterative tabulation).
- **Space Optimization:** Can the table be compressed from $O(N^2) \to O(N)$ or $O(N) \to O(1)$?

#### 3. Time & Space Complexity
- **Time Complexity:** $O(\text{Number of States} \times \text{Work per State})$.
- **Space Complexity:** $O(\text{Number of States})$ or $O(1)$ if space-optimized.

#### 4. Code Implementation

=== "Python"
    ```python
    from typing import List

    class Solution:
        def solve(self, n: int) -> int:
            # TODO: Implement optimal solution
            pass
    ```

=== "C++"
    ```cpp
    #include <vector>

    class Solution {
    public:
        int solve(int n) {
            // TODO: Implement optimal solution
            return 0;
        }
    };
    ```

=== "Java"
    ```java
    class Solution {
        public int solve(int n) {
            // TODO: Implement optimal solution
            return 0;
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function solve(n: number): number {
        // TODO: Implement optimal solution
        return 0;
    }
    ```
```

---

## 💡 Example: Coin Change (LeetCode #322)

### 1. Problem Statement
You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money. Return the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return `-1`. You may assume that you have an infinite number of each kind of coin.

### 2. Intuition & Approach
- **State Definition:** Let `dp[i]` be the minimum number of coins needed to make up amount `i`.
- **Base Case:** `dp[0] = 0` (zero coins needed to make amount 0). All other amounts initialized to $\infty$.
- **Recurrence Relation:**
  $$\text{dp}[i] = \min_{c \in \text{coins}, c \le i} (\text{dp}[i - c] + 1)$$
- We build the solution iteratively from amount $1$ up to `amount`.

### 3. Time & Space Complexity
- **Time Complexity:** $O(\text{amount} \times |\text{coins}|)$ — for each sub-amount, iterate through all coin types.
- **Space Complexity:** $O(\text{amount})$ — 1D table of size `amount + 1`.

### 4. Code Implementation

=== "Python"
    ```python
    from typing import List

    class Solution:
        def coinChange(self, coins: List[int], amount: int) -> int:
            dp = [float('inf')] * (amount + 1)
            dp[0] = 0
            
            for i in range(1, amount + 1):
                for coin in coins:
                    if i - coin >= 0:
                        dp[i] = min(dp[i], dp[i - coin] + 1)
                        
            return dp[amount] if dp[amount] != float('inf') else -1
    ```

=== "C++"
    ```cpp
    #include <vector>
    #include <algorithm>

    class Solution {
    public:
        int coinChange(std::vector<int>& coins, int amount) {
            std::vector<int> dp(amount + 1, amount + 1);
            dp[0] = 0;
            
            for (int i = 1; i <= amount; ++i) {
                for (int coin : coins) {
                    if (i - coin >= 0) {
                        dp[i] = std::min(dp[i], dp[i - coin] + 1);
                    }
                }
            }
            return dp[amount] > amount ? -1 : dp[amount];
        }
    };
    ```

=== "Java"
    ```java
    import java.util.Arrays;

    class Solution {
        public int coinChange(int[] coins, int amount) {
            int[] dp = new int[amount + 1];
            Arrays.fill(dp, amount + 1);
            dp[0] = 0;

            for (int i = 1; i <= amount; i++) {
                for (int coin : coins) {
                    if (i - coin >= 0) {
                        dp[i] = Math.min(dp[i], dp[i - coin] + 1);
                    }
                }
            }
            return dp[amount] > amount ? -1 : dp[amount];
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function coinChange(coins: number[], amount: number): number {
        const dp = new Array(amount + 1).fill(amount + 1);
        dp[0] = 0;

        for (let i = 1; i <= amount; i++) {
            for (const coin of coins) {
                if (i - coin >= 0) {
                    dp[i] = Math.min(dp[i], dp[i - coin] + 1);
                }
            }
        }

        return dp[amount] > amount ? -1 : dp[amount];
    }
    ```
