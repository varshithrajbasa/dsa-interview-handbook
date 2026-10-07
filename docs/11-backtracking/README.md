[← Back to Main Index](../index.md)

# Backtracking - Most Important Questions and Answers

## 📖 Topic Overview

Backtracking is an algorithmic paradigm for solving constraint satisfaction problems by incrementally building candidate solutions and abandoning ("backtracking" from) candidates as soon as it is determined that they cannot lead to a valid final solution.

### Core Algorithmic Patterns:
1. **The Universal Backtracking Blueprint:**
   ```
   function backtrack(state):
       if is_solution(state):
           output(state)
           return
       for choice in candidate_choices:
           if is_valid(choice, state):
               make_choice(choice, state)
               backtrack(state)
               undo_choice(choice, state)  # <-- The Backtrack Step
   ```
2. **Subsets & Combinations:** Elements can either be included or excluded (`2^N`), or picked with a forward-moving index `start_index` to prevent permutations/duplicates.
3. **Handling Duplicates (Subsets II, Permutations II):** Sort input first; skip identical adjacent elements when `i > start and nums[i] == nums[i - 1]`.
4. **Permutations:** Ordering matters ($N!$). Maintain a `visited` boolean array or swap elements in-place.
5. **Constraint Satisfaction Grids:** N-Queens, Sudoku Solver, Word Search on 2D matrices using visited bitmasks or board character mutations.

---

## 🎯 High-Yield Problem Checklist

- [ ] **Subsets (LeetCode #78):** Power set generation via inclusion/exclusion or index looping
- [ ] **Subsets II (LeetCode #90):** Sorted input with adjacent duplicate pruning
- [ ] **Combination Sum (LeetCode #39):** Unbounded element reuse with decreasing target
- [ ] **Combination Sum II (LeetCode #40):** Bounded reuse with duplicate branch skipping
- [ ] **Permutations (LeetCode #46):** Visited array state permutation generation
- [ ] **Permutations II (LeetCode #47):** Visited array + duplicate condition pruning
- [ ] **Word Search (LeetCode #79):** 2D grid DFS with temporary cell marking
- [ ] **Palindrome Partitioning (LeetCode #131):** Substring palindrome check and partition
- [ ] **Letter Combinations of a Phone Number (LeetCode #17):** Digit map branching
- [ ] **N-Queens (LeetCode #51):** Diagonal and column attack tracking sets
- [ ] **Sudoku Solver (LeetCode #37):** Row, column, and $3 \times 3$ box constraint backtracking

---

## 📝 Reusable Question Template Skeleton

Copy and use this template whenever adding a new question to this module:

```markdown
### Problem Name (e.g., LeetCode #XX - Problem Title)

#### 1. Problem Statement
- **Description:** Provide a precise description of the problem.
- **Input:** Choices, candidate collections, constraints, target sum/size.
- **Output:** List of valid combinations, permutations, or boolean feasibility.
- **Constraints:**
  - $N \le 20$ (indicative of $O(2^N)$ or $O(N!)$ combinatorial search).

#### 2. Intuition & Approach
- **Decision Tree:** What constitutes a step/level in the recursion?
- **Base Case:** When is a candidate added to the results?
- **Pruning Conditions:** How to eliminate branches early?
- **State Mutation & Restoration:** What state is modified before recursion and reverted after?

#### 3. Time & Space Complexity
- **Time Complexity:** $O(2^N)$ or $O(N!)$ — bounded by number of leaves in the decision tree.
- **Space Complexity:** $O(N)$ — recursion depth and current path storage.

#### 4. Code Implementation

=== "Python"
    ```python
    from typing import List

    class Solution:
        def solve(self, nums: List[int]) -> List[List[int]]:
            # TODO: Implement optimal solution
            pass
    ```

=== "C++"
    ```cpp
    #include <vector>

    class Solution {
    public:
        std::vector<std::vector<int>> solve(std::vector<int>& nums) {
            // TODO: Implement optimal solution
            return {};
        }
    };
    ```

=== "Java"
    ```java
    import java.util.List;
    import java.util.ArrayList;

    class Solution {
        public List<List<Integer>> solve(int[] nums) {
            // TODO: Implement optimal solution
            return new ArrayList<>();
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function solve(nums: number[]): number[][] {
        // TODO: Implement optimal solution
        return [];
    }
    ```
```

---

## 💡 Example: Subsets (LeetCode #78)

### 1. Problem Statement
Given an integer array `nums` of unique elements, return all possible subsets (the power set). The solution set must not contain duplicate subsets. Return the solution in any order.

### 2. Intuition & Approach
- Every subset represents a path in a decision tree.
- For every index from `start` to `len(nums) - 1`, we append `nums[i]` to `current_path`, recursively build further subsets starting from `i + 1`, and then pop `nums[i]` to backtrack.
- At every invocation of the helper function, a snapshot of `current_path` is a valid subset.

### 3. Time & Space Complexity
- **Time Complexity:** $O(N \cdot 2^N)$ — there are $2^N$ total subsets, and copying each subset takes $O(N)$ time.
- **Space Complexity:** $O(N)$ — recursion call stack and current path buffer.

### 4. Code Implementation

=== "Python"
    ```python
    from typing import List

    class Solution:
        def subsets(self, nums: List[int]) -> List[List[int]]:
            results = []
            
            def backtrack(start: int, current: List[int]):
                results.append(list(current))
                for i in range(start, len(nums)):
                    current.append(nums[i])
                    backtrack(i + 1, current)
                    current.pop()
                    
            backtrack(0, [])
            return results
    ```

=== "C++"
    ```cpp
    #include <vector>

    class Solution {
    public:
        std::vector<std::vector<int>> subsets(std::vector<int>& nums) {
            std::vector<std::vector<int>> results;
            std::vector<int> current;
            backtrack(0, nums, current, results);
            return results;
        }

    private:
        void backtrack(int start, const std::vector<int>& nums, std::vector<int>& current, std::vector<std::vector<int>>& results) {
            results.push_back(current);
            for (int i = start; i < nums.size(); ++i) {
                current.push_back(nums[i]);
                backtrack(i + 1, nums, current, results);
                current.pop_back();
            }
        }
    };
    ```

=== "Java"
    ```java
    import java.util.List;
    import java.util.ArrayList;

    class Solution {
        public List<List<Integer>> subsets(int[] nums) {
            List<List<Integer>> results = new ArrayList<>();
            backtrack(0, nums, new ArrayList<>(), results);
            return results;
        }

        private void backtrack(int start, int[] nums, List<Integer> current, List<List<Integer>> results) {
            results.add(new ArrayList<>(current));
            for (int i = start; i < nums.length; i++) {
                current.add(nums[i]);
                backtrack(i + 1, nums, current, results);
                current.remove(current.size() - 1);
            }
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function subsets(nums: number[]): number[][] {
        const results: number[][] = [];

        function backtrack(start: number, current: number[]): void {
            results.push([...current]);
            for (let i = start; i < nums.length; i++) {
                current.push(nums[i]);
                backtrack(i + 1, current);
                current.pop();
            }
        }

        backtrack(0, []);
        return results;
    }
    ```
