[← Back to Main Index](../../README.md)

# Heap / Priority Queue - Most Important Questions and Answers

## 📖 Topic Overview

A Heap is a specialized complete binary tree that satisfies the heap property: in a **Min-Heap**, parent nodes are always less than or equal to their children; in a **Max-Heap**, parent nodes are always greater than or equal to their children.

### Core Algorithmic Patterns:
1. **Array-Based Binary Heap Structure:**
   - Parent of index $i$: `(i - 1) // 2`
   - Left child of index $i$: `2 * i + 1`
   - Right child of index $i$: `2 * i + 2`
   - Building a heap from an arbitrary array (`heapify`) runs in linear $O(N)$ time.
2. **Top-K Elements Pattern:**
   - To find the $K$ largest elements, maintain a **Min-Heap** of size $K$. Any element larger than the heap's minimum evicts the root, leaving the $K$ largest items in $O(N \log K)$.
   - To find the $K$ smallest elements, maintain a **Max-Heap** of size $K$.
3. **Two Heaps (Streaming Median):**
   - Partition numbers into lower half (Max-Heap) and upper half (Min-Heap).
   - Balance sizes such that max-heap size equals or is 1 greater than min-heap size. Median is retrieved in $O(1)$.
4. **K-Way Merge:**
   - Merging $K$ sorted streams/lists by storing the current head of each list in a min-heap of size $K$ ($O(N \log K)$ overall time).

---

## 🎯 High-Yield Problem Checklist

- [ ] **Kth Largest Element in a Stream (LeetCode #703):** Fixed-size min-heap of size $K$
- [ ] **Last Stone Weight (LeetCode #1046):** Max-heap simulation
- [ ] **K Closest Points to Origin (LeetCode #973):** Max-heap of size $K$ by Euclidean distance
- [ ] **Kth Largest Element in an Array (LeetCode #215):** Min-heap or Quickselect ($O(N)$ average)
- [ ] **Top K Frequent Elements (LeetCode #347):** Frequency map + min-heap of size $K$ or bucket sort
- [ ] **Task Scheduler (LeetCode #621):** Max-heap with cooldown waiting queue
- [ ] **Design Twitter (LeetCode #355):** K-way merge of recent tweets using priority queue
- [ ] **Find Median from Data Stream (LeetCode #295):** Dual min/max balancing heaps
- [ ] **Merge K Sorted Lists (LeetCode #23):** Min-heap tracking active node pointers

---

## 📝 Reusable Question Template Skeleton

Copy and use this template whenever adding a new question to this module:

```markdown
### Problem Name (e.g., LeetCode #XX - Problem Title)

#### 1. Problem Statement
- **Description:** Provide a precise description of the problem.
- **Input:** Array, stream of elements, or list of objects with priority metrics.
- **Output:** Top-K items, streaming median, or schedule sequence.
- **Constraints:**
  - `1 <= k <= nums.length <= 10^5`

#### 2. Intuition & Approach
- **Heap Choice:** Min-heap vs. Max-heap (remember: min-heap for Top-K largest).
- **Invariant:** Heap size bounded to $K$ elements.
- **Step-by-Step Logic:**
  - Step 1: Pre-process frequencies or distances if applicable.
  - Step 2: Push elements into heap; if size exceeds $K$, pop the root.
  - Step 3: Extract or inspect root element.

#### 3. Time & Space Complexity
- **Time Complexity:** $O(N \log K)$ — $N$ elements inserted into heap of maximum size $K$.
- **Space Complexity:** $O(K)$ — heap storage.

#### 4. Code Implementation

=== "Python"
    ```python
    import heapq
    from typing import List

    class Solution:
        def solve(self, nums: List[int], k: int) -> List[int]:
            # TODO: Implement optimal solution
            pass
    ```

=== "C++"
    ```cpp
    #include <vector>
    #include <queue>

    class Solution {
    public:
        std::vector<int> solve(std::vector<int>& nums, int k) {
            // TODO: Implement optimal solution
            return {};
        }
    };
    ```

=== "Java"
    ```java
    import java.util.PriorityQueue;

    class Solution {
        public int[] solve(int[] nums, int k) {
            // TODO: Implement optimal solution
            return new int[]{};
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function solve(nums: number[], k: number): number[] {
        // TODO: Implement optimal solution
        return [];
    }
    ```
```

---

## 💡 Example: Kth Largest Element in an Array (LeetCode #215)

### 1. Problem Statement
Given an integer array `nums` and an integer `k`, return the $k^{\text{th}}$ largest element in the array. Note that it is the $k^{\text{th}}$ largest element in sorted order, not the $k^{\text{th}}$ distinct element. Can you solve it without sorting?

### 2. Intuition & Approach
- If we maintain a **Min-Heap** of size $k$:
  - For each number in `nums`, push it into the min-heap.
  - If the heap size exceeds $k$, pop the smallest element.
  - After processing all $N$ elements, the heap contains the $k$ largest elements of the entire array, and the root of the min-heap is the $k^{\text{th}}$ largest element.

### 3. Time & Space Complexity
- **Time Complexity:** $O(N \log k)$ — each push and pop on a heap of size $k$ takes $O(\log k)$.
- **Space Complexity:** $O(k)$ — storing $k$ elements in the priority queue.

### 4. Code Implementation

=== "Python"
    ```python
    import heapq
    from typing import List

    class Solution:
        def findKthLargest(self, nums: List[int], k: int) -> int:
            min_heap = []
            for num in nums:
                heapq.heappush(min_heap, num)
                if len(min_heap) > k:
                    heapq.heappop(min_heap)
            return min_heap[0]
    ```

=== "C++"
    ```cpp
    #include <vector>
    #include <queue>

    class Solution {
    public:
        int findKthLargest(std::vector<int>& nums, int k) {
            std::priority_queue<int, std::vector<int>, std::greater<int>> min_heap;
            for (int num : nums) {
                min_heap.push(num);
                if (min_heap.size() > k) {
                    min_heap.pop();
                }
            }
            return min_heap.top();
        }
    };
    ```

=== "Java"
    ```java
    import java.util.PriorityQueue;

    class Solution {
        public int findKthLargest(int[] nums, int k) {
            PriorityQueue<Integer> minHeap = new PriorityQueue<>();
            for (int num : nums) {
                minHeap.offer(num);
                if (minHeap.size() > k) {
                    minHeap.poll();
                }
            }
            return minHeap.peek();
        }
    }
    ```

=== "TypeScript"
    ```typescript
    // Using a binary min-heap implementation for O(N log K)
    function findKthLargest(nums: number[], k: number): number {
        const minHeap: number[] = [];
        
        const push = (val: number) => {
            minHeap.push(val);
            let idx = minHeap.length - 1;
            while (idx > 0) {
                const parent = Math.floor((idx - 1) / 2);
                if (minHeap[parent] <= minHeap[idx]) break;
                [minHeap[parent], minHeap[idx]] = [minHeap[idx], minHeap[parent]];
                idx = parent;
            }
        };

        const pop = (): number => {
            const top = minHeap[0];
            const bottom = minHeap.pop()!;
            if (minHeap.length > 0) {
                minHeap[0] = bottom;
                let idx = 0;
                while (true) {
                    let smallest = idx;
                    const left = 2 * idx + 1;
                    const right = 2 * idx + 2;
                    if (left < minHeap.length && minHeap[left] < minHeap[smallest]) smallest = left;
                    if (right < minHeap.length && minHeap[right] < minHeap[smallest]) smallest = right;
                    if (smallest === idx) break;
                    [minHeap[idx], minHeap[smallest]] = [minHeap[smallest], minHeap[idx]];
                    idx = smallest;
                }
            }
            return top;
        };

        for (const num of nums) {
            push(num);
            if (minHeap.length > k) {
                pop();
            }
        }
        return minHeap[0];
    }
    ```
