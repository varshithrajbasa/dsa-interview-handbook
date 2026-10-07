# How to Contribute & Question Template Guide

Welcome! We are excited that you want to contribute to the **Most Important DSA Questions and Answers** handbook. This repository is dedicated to providing high-yield, interview-ready solutions for software engineers preparing for technical interviews at **MAANG / FAANG (Meta, Amazon, Apple, Netflix, Google)**, Big Tech, and top product companies.

---

## 🚀 Quick Contribution Workflow

1. **Fork & Clone** the repository:
   ```bash
   git clone https://github.com/varshithrajbasa/dsa-interview-handbook.git
   cd dsa-interview-handbook
   ```
2. **Create a new branch** for your question or topic:
   ```bash
   git checkout -b feat/add-two-sum-ii
   ```
3. **Navigate to the target topic** under `docs/` (e.g., `docs/02-arrays/README.md` or `docs/07-two-pointers-sliding-window/README.md`).
4. **Copy the Question Template** below and fill in the 4 standardized sections.
5. **Mark the problem as completed** in the topic's `- [x]` checklist if applicable.
6. **Preview locally** using MkDocs:
   ```bash
   pip install mkdocs-material
   mkdocs serve
   ```
   Open `http://127.0.0.1:8000` to ensure formatting, math rendering, and code tabs look clean.
7. **Commit & Submit a Pull Request** with a descriptive title (e.g., `feat(arrays): add Two Sum II solution and complexity analysis`).

---

## 📋 The 4-Pillar Solution Standard

To maintain consistent quality across all topics, every problem must follow this structure:

### 1. Problem Statement
- **Description:** Clear, concise problem prompt.
- **Constraints:** Mathematical bounds ($1 \le N \le 10^5$, etc.) which dictate expected complexity.
- **Input / Output:** Exact signatures and expected return values.

### 2. Intuition & Approach
- **Core Mental Model:** Pattern recognition (e.g., *monotonic deque*, *dynamic window*, *post-order DFS*).
- **Brute Force vs Optimal:** Naive baseline and why it falls short (e.g., $O(N^2)$ TLE), followed by the optimal invariant.
- **Step-by-Step Logic:** Clear breakdown of the algorithm's lifecycle and edge-case precautions.

### 3. Time & Space Complexity
- **Time Complexity:** Explicit Big-$O$ notation with mathematical justification for loops, recursion, and heap operations.
- **Space Complexity:** Distinction between auxiliary memory, recursion call stack depth, and output storage.

### 4. Code Implementation
- Idiomatic, clean code with meaningful variable names.
- Provide solutions using MkDocs Material content tabs (`=== "Language"`), including Python, C++, Java, and TypeScript where possible.

---

## 📝 The Reusable Question Template

Copy the markdown snippet below whenever adding a new question to any module:

```markdown
### Problem Name (e.g., LeetCode #XX - Problem Title)

#### 1. Problem Statement
- **Description:** Provide a precise description of the problem.
- **Input:** Specify types and structure of input arguments.
- **Output:** Specify return type and value expectations.
- **Constraints:**
  - `1 <= nums.length <= 10^5`
  - Values bounded between `[-10^9, 10^9]`

#### 2. Intuition & Approach
- **Key Insight:** Explain the invariant, pattern, or mathematical breakthrough.
- **Brute Force:**
  - Approach: Describe the naive approach.
  - Limitations: Time complexity $O(N^2)$ leads to Time Limit Exceeded (TLE).
- **Optimal Strategy:**
  - Step 1: Initialize data structures and pointers.
  - Step 2: Traverse while maintaining the core invariant.
  - Step 3: Handle edge cases (empty inputs, single elements, duplicates, negative numbers).

#### 3. Time & Space Complexity
- **Time Complexity:** $O(N)$ — explain why (e.g., single pass with amortized $O(1)$ operations).
- **Space Complexity:** $O(1)$ — explain auxiliary memory usage.

#### 4. Code Implementation

=== "Python"
    ```python
    from typing import List

    class Solution:
        def solve(self, nums: List[int]) -> int:
            # TODO: Add optimal solution
            pass
    ```

=== "C++"
    ```cpp
    #include <vector>

    class Solution {
    public:
        int solve(std::vector<int>& nums) {
            // TODO: Add optimal solution
            return 0;
        }
    };
    ```

=== "Java"
    ```java
    class Solution {
        public int solve(int[] nums) {
            // TODO: Add optimal solution
            return 0;
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function solve(nums: number[]): number {
        // TODO: Add optimal solution
        return 0;
    }
    ```
```

---

## 🗂️ Topic Directory Reference

| Topic | Directory Path |
|---|---|
| 01. Foundation & Complexity | `docs/01-foundation/README.md` |
| 02. Arrays | `docs/02-arrays/README.md` |
| 03. Linked Lists | `docs/03-linked-list/README.md` |
| 04. Strings | `docs/04-strings/README.md` |
| 05. Stacks & Queues | `docs/05-stacks-and-queues/README.md` |
| 06. Binary Search | `docs/06-binary-search/README.md` |
| 07. Two Pointers & Sliding Window | `docs/07-two-pointers-sliding-window/README.md` |
| 08. Binary Trees | `docs/08-binary-tree/README.md` |
| 09. Binary Search Trees | `docs/09-binary-search-tree/README.md` |
| 10. Heap / Priority Queue | `docs/10-heap/README.md` |
| 11. Backtracking | `docs/11-backtracking/README.md` |
| 12. Greedy Algorithms | `docs/12-greedy/README.md` |
| 13. Dynamic Programming | `docs/13-dynamic-programming/README.md` |
| 14. Graphs | `docs/14-graphs/README.md` |
