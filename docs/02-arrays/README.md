[← Back to Main Index](../index.md)

# Arrays - Most Important Questions and Answers

## 📖 Topic Overview

Arrays are the most ubiquitous linear data structure. Interview questions targeting arrays test your ability to navigate contiguous memory, manipulate indices, optimize nested traversals, and alter arrays in-place with $O(1)$ extra space.

### Core Algorithmic Patterns:
1. **Prefix Sums & Running Totals:** Precomputing cumulative sums to answer range sum queries in $O(1)$ time, or utilizing hash maps with prefix sums to locate subarrays with a target sum in $O(N)$.
2. **Kadane’s Algorithm:** Dynamically tracking current maximum subarray sum vs. starting fresh at the current element ($O(N)$ time, $O(1)$ space).
3. **Dutch National Flag (Three-Way Partitioning):** Sorting three distinct values (e.g. 0, 1, 2) in a single pass using three pointers (`low`, `mid`, `high`).
4. **Interval Operations:** Sorting intervals by start time, merging overlapping intervals, and inserting new intervals.
5. **In-Place Matrix Manipulation:** Transposition, horizontal/vertical reflection, and spiral order boundary tracking.

---

## 🎯 High-Yield Problem Checklist

- [ ] **Two Sum (LeetCode #1):** Hash map complement lookup in $O(N)$ time
- [ ] **Best Time to Buy and Sell Stock (LeetCode #121):** Running minimum tracking
- [ ] **Contains Duplicate (LeetCode #217):** Hash set uniqueness validation
- [ ] **Product of Array Except Self (LeetCode #238):** Prefix and suffix product passes without division
- [ ] **Maximum Subarray (LeetCode #53):** Kadane’s dynamic programming algorithm
- [ ] **Maximum Product Subarray (LeetCode #152):** Tracking both min and max running products
- [ ] **Find Minimum in Rotated Sorted Array (LeetCode #153):** Binary search pivot identification
- [ ] **Merge Intervals (LeetCode #56):** Sorting and overlapping interval merging
- [ ] **Insert Interval (LeetCode #57):** Non-overlapping binary search or linear sweep
- [ ] **Rotate Image (LeetCode #48):** Transpose and reverse matrix in-place
- [ ] **Set Matrix Zeroes (LeetCode #73):** First row/column state marker technique
- [ ] **Spiral Matrix (LeetCode #54):** Boundary shrink simulation

---

## 📝 Reusable Question Template Skeleton

Copy and use this template whenever adding a new question to this module:

```markdown
### Problem Name (e.g., LeetCode #XX - Problem Title)

#### 1. Problem Statement
- **Description:** Provide a precise description of the problem.
- **Input:** Specify types and structure of input arguments.
- **Output:** Specify return type and value expectations.
- **Constraints:**
  - `1 <= nums.length <= 10^5`
  - `-10^4 <= nums[i] <= 10^4`

#### 2. Intuition & Approach
- **Key Insight:** Explain the invariant or pattern (e.g. prefix sum, two pointers, greedy choice).
- **Brute Force:**
  - Approach: Describe the nested loops or naive solution.
  - Limitations: Time complexity $O(N^2)$ leads to Time Limit Exceeded (TLE).
- **Optimal Strategy:**
  - Step 1: Data structures and pointers initialization.
  - Step 2: Main loop logic maintaining bounds and invariants.
  - Step 3: Edge cases (empty array, single element, all negatives).

#### 3. Time & Space Complexity
- **Time Complexity:** $O(...)$ — explain work per iteration and total loops.
- **Space Complexity:** $O(...)$ — clarify auxiliary variables vs output space.

#### 4. Code Implementation

=== "Python"
    ```python
    from typing import List

    class Solution:
        def solve(self, nums: List[int]) -> int:
            # TODO: Implement optimal solution
            pass
    ```

=== "C++"
    ```cpp
    #include <vector>

    class Solution {
    public:
        int solve(std::vector<int>& nums) {
            // TODO: Implement optimal solution
            return 0;
        }
    };
    ```

=== "Java"
    ```java
    class Solution {
        public int solve(int[] nums) {
            // TODO: Implement optimal solution
            return 0;
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function solve(nums: number[]): number {
        // TODO: Implement optimal solution
        return 0;
    }
    ```
```

---

## 💡 Example: Two Sum (LeetCode #1)

### 1. Problem Statement
Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`. You may assume that each input would have exactly one solution, and you may not use the same element twice.

### 2. Intuition & Approach
- **Brute Force:** Check every pair $(i, j)$ where $i < j$. This requires $O(N^2)$ operations.
- **Optimal Strategy:** As we traverse through the array, for each element `nums[i]`, the required number to reach `target` is `complement = target - nums[i]`. By storing previously seen values and their indices in a hash map, we can check in $O(1)$ average time if the complement exists.

### 3. Time & Space Complexity
- **Time Complexity:** $O(N)$ — single pass visiting each element once with $O(1)$ average hash map operations.
- **Space Complexity:** $O(N)$ — hash map storing at most $N$ elements.

### 4. Code Implementation

=== "Python"
    ```python
    from typing import List

    class Solution:
        def twoSum(self, nums: List[int], target: int) -> List[int]:
            seen = {}
            for i, num in enumerate(nums):
                complement = target - num
                if complement in seen:
                    return [seen[complement], i]
                seen[num] = i
            return []
    ```

=== "C++"
    ```cpp
    #include <vector>
    #include <unordered_map>

    class Solution {
    public:
        std::vector<int> twoSum(std::vector<int>& nums, int target) {
            std::unordered_map<int, int> seen;
            for (int i = 0; i < nums.size(); ++i) {
                int complement = target - nums[i];
                if (seen.find(complement) != seen.end()) {
                    return {seen[complement], i};
                }
                seen[nums[i]] = i;
            }
            return {};
        }
    };
    ```

=== "Java"
    ```java
    import java.util.HashMap;
    import java.util.Map;

    class Solution {
        public int[] twoSum(int[] nums, int target) {
            Map<Integer, Integer> seen = new HashMap<>();
            for (int i = 0; i < nums.length; i++) {
                int complement = target - nums[i];
                if (seen.containsKey(complement)) {
                    return new int[]{seen.get(complement), i};
                }
                seen.put(nums[i], i);
            }
            return new int[]{};
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function twoSum(nums: number[], target: number): number[] {
        const seen = new Map<number, number>();
        for (let i = 0; i < nums.length; i++) {
            const complement = target - nums[i];
            if (seen.has(complement)) {
                return [seen.get(complement)!, i];
            }
            seen.set(nums[i], i);
        }
        return [];
    }
    ```
