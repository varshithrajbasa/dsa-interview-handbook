[← Back to Main Index](../index.md)

# Greedy - Most Important Questions and Answers

## 📖 Topic Overview

Greedy algorithms construct a solution by making the locally optimal choice at each stage with the expectation of arriving at a globally optimal solution. Unlike Dynamic Programming, greedy algorithms never reconsider or backtrack over previously made decisions.

### Core Algorithmic Patterns:
1. **The Greedy Choice Property & Exchange Arguments:**
   - A globally optimal solution can be arrived at by making a locally optimal choice without looking ahead.
   - Proof technique: Assume an alternative optimal solution exists, and show that exchanging its first choice with the greedy choice leaves the solution equally optimal or better.
2. **Interval Scheduling & Partitioning:**
   - Sorting intervals by end time (to maximize non-overlapping intervals) or start time (to merge overlaps or allocate rooms).
3. **Farthest Reachable Position (Jump Game):**
   - Maintaining `max_reach` dynamically as we iterate through indices.
4. **Gas Station Circuit Balance:**
   - If total gas $\ge$ total cost, a valid circuit is guaranteed; the starting point can be greedily advanced whenever running tank deficit occurs.
5. **Partition Labels:**
   - Record the last occurrence of each character; expand the partition boundary to include the maximum last occurrence of characters inside the current chunk.

---

## 🎯 High-Yield Problem Checklist

- [ ] **Maximum Subarray (LeetCode #53):** Kadane’s greedy reset on negative prefix sums
- [ ] **Jump Game (LeetCode #55):** Dynamic farthest reach updating
- [ ] **Jump Game II (LeetCode #45):** BFS-level greedy jumps between current and farthest reach
- [ ] **Gas Station (LeetCode #134):** Cumulative deficit tracking and start index advancement
- [ ] **Hand of Straights (LeetCode #846):** Ordered map greedy card group formation
- [ ] **Merge Intervals (LeetCode #56):** Sort by start time and greedily extend end time
- [ ] **Non-overlapping Intervals (LeetCode #435):** Sort by end time and count minimal deletions
- [ ] **Partition Labels (LeetCode #763):** Last seen character map and boundary expansion
- [ ] **Valid Parenthesis String (LeetCode #678):** Tracking minimum and maximum open bracket range
- [ ] **Task Scheduler (LeetCode #621):** Max frequency idle slot calculation

---

## 📝 Reusable Question Template Skeleton

Copy and use this template whenever adding a new question to this module:

```markdown
### Problem Name (e.g., LeetCode #XX - Problem Title)

#### 1. Problem Statement
- **Description:** Provide a precise description of the problem.
- **Input:** Sequences, intervals, or resource constraints.
- **Output:** Minimum operations, maximum count, or boolean feasibility.
- **Constraints:**
  - `1 <= nums.length <= 10^5`

#### 2. Intuition & Approach
- **Greedy Invariant:** What is the locally optimal choice at each step?
- **Proof / Heuristic:** Why does this local choice guarantee global optimality (exchange argument)?
- **Step-by-Step Logic:**
  - Step 1: Pre-sort or compute lookup tables (e.g., last occurrence indices).
  - Step 2: Iterate sequentially, making greedy decision.
  - Step 3: Accumulate count/length or terminate early if unreachable.

#### 3. Time & Space Complexity
- **Time Complexity:** $O(N)$ or $O(N \log N)$ (dominated by initial sort).
- **Space Complexity:** $O(1)$ auxiliary variables or $O(N)$ for sorting/frequency tables.

#### 4. Code Implementation

=== "Python"
    ```python
    from typing import List

    class Solution:
        def solve(self, nums: List[int]) -> bool:
            # TODO: Implement optimal solution
            pass
    ```

=== "C++"
    ```cpp
    #include <vector>

    class Solution {
    public:
        bool solve(std::vector<int>& nums) {
            // TODO: Implement optimal solution
            return true;
        }
    };
    ```

=== "Java"
    ```java
    class Solution {
        public boolean solve(int[] nums) {
            // TODO: Implement optimal solution
            return true;
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function solve(nums: number[]): boolean {
        // TODO: Implement optimal solution
        return true;
    }
    ```
```

---

## 💡 Example: Jump Game (LeetCode #55)

### 1. Problem Statement
You are given an integer array `nums`. You are initially positioned at the array's first index, and each element in the array represents your maximum jump length at that position. Return `true` if you can reach the last index, or `false` otherwise.

### 2. Intuition & Approach
- As we iterate through the array from left to right, we maintain `max_reach`: the furthest index reachable so far.
- If at any point the current index `i` exceeds `max_reach`, we are stuck at an unreachable index and return `false`.
- At each index `i`, greedily update `max_reach = max(max_reach, i + nums[i])`.
- If `max_reach >= len(nums) - 1`, we can reach the end immediately.

### 3. Time & Space Complexity
- **Time Complexity:** $O(N)$ — single pass through the array.
- **Space Complexity:** $O(1)$ — only one variable `max_reach` is maintained.

### 4. Code Implementation

=== "Python"
    ```python
    from typing import List

    class Solution:
        def canJump(self, nums: List[int]) -> bool:
            max_reach = 0
            
            for i, jump in enumerate(nums):
                if i > max_reach:
                    return False
                max_reach = max(max_reach, i + jump)
                if max_reach >= len(nums) - 1:
                    return True
                    
            return True
    ```

=== "C++"
    ```cpp
    #include <vector>
    #include <algorithm>

    class Solution {
    public:
        bool canJump(std::vector<int>& nums) {
            int max_reach = 0;
            int n = nums.size();
            
            for (int i = 0; i < n; ++i) {
                if (i > max_reach) return false;
                max_reach = std::max(max_reach, i + nums[i]);
                if (max_reach >= n - 1) return true;
            }
            return true;
        }
    };
    ```

=== "Java"
    ```java
    class Solution {
        public boolean canJump(int[] nums) {
            int maxReach = 0;
            for (int i = 0; i < nums.length; i++) {
                if (i > maxReach) return false;
                maxReach = Math.max(maxReach, i + nums[i]);
                if (maxReach >= nums.length - 1) return true;
            }
            return true;
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function canJump(nums: number[]): boolean {
        let maxReach = 0;
        for (let i = 0; i < nums.length; i++) {
            if (i > maxReach) return false;
            maxReach = Math.max(maxReach, i + nums[i]);
            if (maxReach >= nums.length - 1) return true;
        }
        return true;
    }
    ```
