# How to Contribute & Question Template Guide

Welcome! We are excited that you want to contribute to the **Most Important DSA Questions and Answers** handbook. This repository provides high-yield, interview-ready solutions for software engineers preparing for technical interviews at **MAANG / FAANG (Meta, Amazon, Apple, Netflix, Google)**, Big Tech, and top product companies.

For the interactive documentation version, visit [How to Contribute](docs/contributing.md) or see our live documentation.

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
   Open `http://127.0.0.1:8000` to verify formatting, math rendering, and tabs.
7. **Commit & Submit a Pull Request** with a clear title (e.g., `feat(arrays): add Two Sum II solution and complexity analysis`).

---

## 📋 The 4-Pillar Solution Standard

Every problem must follow this structure:

1. **Problem Statement:** Clear prompt, constraints ($1 \le N \le 10^5$), and input/output structure.
2. **Intuition & Approach:** Mental model, naive vs optimal transitions, and invariant logic.
3. **Time & Space Complexity:** Big-$O$ notation with mathematical proof for both runtime and auxiliary memory.
4. **Code Implementation:** Clean, idiomatic implementations across Python, C++, Java, and TypeScript.

---

## 📝 The Reusable Question Template

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
