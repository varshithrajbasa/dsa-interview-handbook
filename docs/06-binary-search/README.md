[← Back to Main Index](../../README.md)

# Binary Search - Most Important Questions and Answers

## 📖 Topic Overview

Binary Search is a divide-and-conquer paradigm that reduces the search space by half in each iteration, achieving $O(\log N)$ logarithmic runtime. While simple in concept, handling loop termination bounds (`left <= right` vs `left < right`), midpoint calculations, and predicate monotonicity is a frequent source of off-by-one errors.

### Core Algorithmic Patterns:
1. **Classic Binary Search:** Searching on sorted arrays with boundary conditions and overflow-safe midpoint calculation: `mid = left + (right - left) // 2`.
2. **Rotated Sorted Arrays:** Determining which half is strictly sorted (`nums[left] <= nums[mid]` vs `nums[mid] <= nums[right]`) and checking if the target lies within the sorted half.
3. **Boundary / Insertion Point Detection:** Lower bound (first index where `nums[i] >= target`) and upper bound (first index where `nums[i] > target`).
4. **Binary Search on the Answer (Monotonic Predicate):**
   - When the problem asks for the minimum or maximum feasible value $k$ satisfying a condition $P(k)$.
   - If $P(k)$ is monotonic (`FFFFTTTT` or `TTTTFFFF`), binary search the answer range in $O(\text{range} \times \text{validation\_time})$.
   - Examples: Koko Eating Bananas, Capacity to Ship Packages, Split Array Largest Sum.
5. **2D Matrix Binary Search:** Treating a matrix of size $M \times N$ as a virtual 1D array where index $k$ maps to `row = k // N`, `col = k % N`.

---

## 🎯 High-Yield Problem Checklist

- [ ] **Binary Search (LeetCode #704):** Classic bounds and midpoint template
- [ ] **Search a 2D Matrix (LeetCode #74):** Virtual 1D array index mapping
- [ ] **Find Minimum in Rotated Sorted Array (LeetCode #153):** Inflection point binary search
- [ ] **Search in Rotated Sorted Array (LeetCode #33):** Sorted-half branch pruning
- [ ] **First and Last Position of Element in Sorted Array (LeetCode #34):** Left and right boundary bisect
- [ ] **Search Insert Position (LeetCode #35):** Lower bound index location
- [ ] **Koko Eating Bananas (LeetCode #875):** Binary search on speed answer range
- [ ] **Capacity To Ship Packages Within D Days (LeetCode #1011):** Feasibility predicate binary search
- [ ] **Find Peak Element (LeetCode #162):** Gradient ascent on unsorted array
- [ ] **Median of Two Sorted Arrays (LeetCode #4):** Dual array partition binary search ($O(\log(\min(M, N)))$)

---

## 📝 Reusable Question Template Skeleton

Copy and use this template whenever adding a new question to this module:

```markdown
### Problem Name (e.g., LeetCode #XX - Problem Title)

#### 1. Problem Statement
- **Description:** Provide a precise description of the problem.
- **Input:** Sorted array or search space boundaries with target / constraints.
- **Output:** Index, boolean flag, or optimal integer value.
- **Constraints:**
  - `1 <= nums.length <= 10^5`
  - `-10^9 <= nums[i], target <= 10^9`

#### 2. Intuition & Approach
- **Key Insight:** Identify the monotonic property: where does the condition transition from false to true?
- **Search Space:**
  - `left = minimum_possible_value`
  - `right = maximum_possible_value`
- **Predicate Function:** `is_valid(mid)` returning boolean in $O(N)$ or $O(1)$.
- **Boundary Decision:**
  - If `is_valid(mid)`: search one half (`right = mid` or `left = mid + 1`).
  - Else: search the complementary half.

#### 3. Time & Space Complexity
- **Time Complexity:** $O(\log(\text{SearchSpace}) \times \text{Cost(Predicate)})$.
- **Space Complexity:** $O(1)$ — iterative implementation using constant pointers.

#### 4. Code Implementation

=== "Python"
    ```python
    from typing import List

    class Solution:
        def search(self, nums: List[int], target: int) -> int:
            # TODO: Implement optimal solution
            pass
    ```

=== "C++"
    ```cpp
    #include <vector>

    class Solution {
    public:
        int search(std::vector<int>& nums, int target) {
            // TODO: Implement optimal solution
            return -1;
        }
    };
    ```

=== "Java"
    ```java
    class Solution {
        public int search(int[] nums, int target) {
            // TODO: Implement optimal solution
            return -1;
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function search(nums: number[], target: number): number {
        // TODO: Implement optimal solution
        return -1;
    }
    ```
```

---

## 💡 Example: Search in Rotated Sorted Array (LeetCode #33)

### 1. Problem Statement
Given an integer array `nums` sorted in ascending order (with distinct values) that has been rotated at an unknown pivot, and an integer `target`, return the index of `target` if it is in `nums`, or `-1` if it is not in `nums`. You must write an algorithm with $O(\log N)$ runtime complexity.

### 2. Intuition & Approach
- In any rotated sorted array, splitting the array at midpoint `mid` will always produce at least one half that is completely sorted.
- If `nums[left] <= nums[mid]`, the left half is sorted:
  - If `nums[left] <= target < nums[mid]`, the target must be in the left half $\to$ `right = mid - 1`.
  - Otherwise, search the right half $\to$ `left = mid + 1`.
- Otherwise, the right half is sorted:
  - If `nums[mid] < target <= nums[right]`, the target must be in the right half $\to$ `left = mid + 1`.
  - Otherwise, search the left half $\to$ `right = mid - 1`.

### 3. Time & Space Complexity
- **Time Complexity:** $O(\log N)$ — search space halves in every iteration.
- **Space Complexity:** $O(1)$ — iterative pointer traversal.

### 4. Code Implementation

=== "Python"
    ```python
    from typing import List

    class Solution:
        def search(self, nums: List[int], target: int) -> int:
            left, right = 0, len(nums) - 1
            
            while left <= right:
                mid = left + (right - left) // 2
                
                if nums[mid] == target:
                    return mid
                
                # Check if left half is sorted
                if nums[left] <= nums[mid]:
                    if nums[left] <= target < nums[mid]:
                        right = mid - 1
                    else:
                        left = mid + 1
                # Otherwise, right half must be sorted
                else:
                    if nums[mid] < target <= nums[right]:
                        left = mid + 1
                    else:
                        right = mid - 1
                        
            return -1
    ```

=== "C++"
    ```cpp
    #include <vector>

    class Solution {
    public:
        int search(std::vector<int>& nums, int target) {
            int left = 0, right = nums.size() - 1;
            
            while (left <= right) {
                int mid = left + (right - left) / 2;
                if (nums[mid] == target) return mid;
                
                if (nums[left] <= nums[mid]) {
                    if (nums[left] <= target && target < nums[mid]) {
                        right = mid - 1;
                    } else {
                        left = mid + 1;
                    }
                } else {
                    if (nums[mid] < target && target <= nums[right]) {
                        left = mid + 1;
                    } else {
                        right = mid - 1;
                    }
                }
            }
            return -1;
        }
    };
    ```

=== "Java"
    ```java
    class Solution {
        public int search(int[] nums, int target) {
            int left = 0, right = nums.length - 1;
            
            while (left <= right) {
                int mid = left + (right - left) / 2;
                if (nums[mid] == target) return mid;
                
                if (nums[left] <= nums[mid]) {
                    if (nums[left] <= target && target < nums[mid]) {
                        right = mid - 1;
                    } else {
                        left = mid + 1;
                    }
                } else {
                    if (nums[mid] < target && target <= nums[right]) {
                        left = mid + 1;
                    } else {
                        right = mid - 1;
                    }
                }
            }
            return -1;
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function search(nums: number[], target: number): number {
        let left = 0;
        let right = nums.length - 1;

        while (left <= right) {
            const mid = Math.floor(left + (right - left) / 2);
            if (nums[mid] === target) return mid;

            if (nums[left] <= nums[mid]) {
                if (nums[left] <= target && target < nums[mid]) {
                    right = mid - 1;
                } else {
                    left = mid + 1;
                }
            } else {
                if (nums[mid] < target && target <= nums[right]) {
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
            }
        }
        return -1;
    }
    ```
