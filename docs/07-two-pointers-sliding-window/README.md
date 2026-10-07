[← Back to Main Index](../index.md)

# Two Pointers & Sliding Window - Most Important Questions and Answers

## 📖 Topic Overview

Two Pointers and Sliding Window techniques optimize quadratic $O(N^2)$ brute-force searches across sequences and subarrays into optimal $O(N)$ linear-time algorithms by discarding unviable search states in bulk.

### Core Algorithmic Patterns:
1. **Opposite-Direction Pointers (Convergence):**
   - Start with `left = 0`, `right = n - 1`.
   - Move pointers inwards based on monotonic conditions (e.g., Two Sum II on sorted array, Container With Most Water, Trapping Rain Water).
2. **Same-Direction / Fast-Slow Pointers:**
   - One pointer scans forward while the other lags behind or condenses the array in-place (e.g., Remove Duplicates, Move Zeroes).
3. **Fixed-Size Sliding Window:**
   - Window size $K$ remains constant.
   - Advance both endpoints simultaneously: subtract outgoing element `nums[i - k]` and add incoming element `nums[i]`.
4. **Dynamic-Size Sliding Window:**
   - Right pointer expands window until condition is met or violated.
   - Left pointer contracts window to restore invariant or minimize window size (e.g., Minimum Window Substring, Longest Substring Without Repeating Characters).

---

## 🎯 High-Yield Problem Checklist

- [ ] **Two Sum II - Input Array Is Sorted (LeetCode #167):** Converging two pointers on sorted array
- [ ] **3Sum (LeetCode #15):** Sorting + outer loop + converging two pointers with deduplication
- [ ] **Container With Most Water (LeetCode #11):** Moving pointer with smaller height inward
- [ ] **Trapping Rain Water (LeetCode #42):** Dual peak pointers or two-pointer max bounds
- [ ] **Best Time to Buy and Sell Stock (LeetCode #121):** Sliding buy/sell window
- [ ] **Longest Substring Without Repeating Characters (LeetCode #3):** Dynamic window with character index hash map
- [ ] **Longest Repeating Character Replacement (LeetCode #424):** Max frequency window invariant
- [ ] **Permutation in String (LeetCode #567):** Fixed size sliding window frequency match
- [ ] **Minimum Window Substring (LeetCode #76):** Dynamic contraction with match counter
- [ ] **Sliding Window Maximum (LeetCode #239):** Fixed window with monotonic deque

---

> [!TIP]
> **Want to contribute a solution or add a new question to this topic?**  
> Check our standardized format and guidelines in the [How to Contribute & Question Template Guide](../contributing.md).

---

## 💡 Example: Container With Most Water (LeetCode #11)

### 1. Problem Statement
You are given an integer array `height` of length $N$. There are $N$ vertical lines drawn such that the two endpoints of the $i^{\text{th}}$ line are $(i, 0)$ and $(i, \text{height}[i])$. Find two lines that together with the x-axis form a container, such that the container contains the most water. Return the maximum amount of water a container can store.

### 2. Intuition & Approach
- The volume of water is given by: $\text{Area} = \min(\text{height}[l], \text{height}[r]) \times (r - l)$.
- Start with the widest possible container: `left = 0` and `right = len(height) - 1`.
- To find a container with a greater area as the width $(r - l)$ decreases, we must find a taller bounding line.
- The limiting factor is always the shorter line. Therefore, moving the pointer pointing to the shorter line is the only way that might yield a larger area.

### 3. Time & Space Complexity
- **Time Complexity:** $O(N)$ — every step moves either `left` or `right` closer, inspecting each line at most once.
- **Space Complexity:** $O(1)$ — constant extra variables.

### 4. Code Implementation

=== "Python"
    ```python
    from typing import List

    class Solution:
        def maxArea(self, height: List[int]) -> int:
            left, right = 0, len(height) - 1
            max_water = 0
            
            while left < right:
                current_height = min(height[left], height[right])
                current_width = right - left
                max_water = max(max_water, current_height * current_width)
                
                if height[left] < height[right]:
                    left += 1
                else:
                    right -= 1
                    
            return max_water
    ```

=== "C++"
    ```cpp
    #include <vector>
    #include <algorithm>

    class Solution {
    public:
        int maxArea(std::vector<int>& height) {
            int left = 0, right = height.size() - 1;
            int max_water = 0;
            
            while (left < right) {
                int h = std::min(height[left], height[right]);
                max_water = std::max(max_water, h * (right - left));
                
                if (height[left] < height[right]) {
                    left++;
                } else {
                    right--;
                }
            }
            return max_water;
        }
    };
    ```

=== "Java"
    ```java
    class Solution {
        public int maxArea(int[] height) {
            int left = 0, right = height.length - 1;
            int maxWater = 0;

            while (left < right) {
                int h = Math.min(height[left], height[right]);
                maxWater = Math.max(maxWater, h * (right - left));

                if (height[left] < height[right]) {
                    left++;
                } else {
                    right--;
                }
            }
            return maxWater;
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function maxArea(height: number[]): number {
        let left = 0;
        let right = height.length - 1;
        let maxWater = 0;

        while (left < right) {
            const h = Math.min(height[left], height[right]);
            maxWater = Math.max(maxWater, h * (right - left));

            if (height[left] < height[right]) {
                left++;
            } else {
                right--;
            }
        }
        return maxWater;
    }
    ```
