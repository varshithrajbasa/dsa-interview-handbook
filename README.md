# Most Important DSA Questions and Answers

[![GitHub Pages Deployment](https://github.com/varshithrajbasa/dsa-interview-handbook/actions/workflows/deploy.yml/badge.svg)](https://github.com/varshithrajbasa/dsa-interview-handbook/actions/workflows/deploy.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Built with MkDocs Material](https://img.shields.io/badge/Material_for_MkDocs-526CFE?logo=materialformkdocs&logoColor=white)](https://squidfunk.github.io/mkdocs-material/)

A curated, production-ready handbook containing the most frequently asked, high-yield Data Structures and Algorithms (DSA) interview questions, patterns, intuitions, and optimized solutions. Designed specifically for software engineers preparing for technical interviews at MAANG / FAANG (Meta, Amazon, Apple, Netflix, Google), Big Tech, and top product companies.

---

## 🌐 Live Documentation Website

Access the interactive, searchable web handbook hosted on GitHub Pages:

🔗 **[https://varshithrajbasa.github.io/dsa-interview-handbook/](https://varshithrajbasa.github.io/dsa-interview-handbook/)**

*(Once GitHub Actions completes its initial run on `main`, the live documentation will be accessible at this URL.)*

---

## 📚 Table of Contents

Explore each module below. Every topic includes conceptual deep dives, algorithmic patterns, high-frequency interview checklists, and standardized solution templates.

| # | Topic | Description & Core Focus | Documentation Link |
|---|-------|--------------------------|--------------------|
| 01 | **Foundation & Complexity** | Asymptotic analysis (Big-O), Bit Manipulation, Math basics | [docs/01-foundation/README.md](docs/01-foundation/README.md) |
| 02 | **Arrays** | Sliding subarrays, prefix sums, cycle sort, matrix traversal | [docs/02-arrays/README.md](docs/02-arrays/README.md) |
| 03 | **Linked Lists** | Two pointers (fast/slow), in-place reversal, list merges | [docs/03-linked-list/README.md](docs/03-linked-list/README.md) |
| 04 | **Strings** | Anagrams, sliding window substrings, palindromes | [docs/04-strings/README.md](docs/04-strings/README.md) |
| 05 | **Stacks and Queues** | Monotonic stacks, min/max stack, monotonic deque | [docs/05-stacks-and-queues/README.md](docs/05-stacks-and-queues/README.md) |
| 06 | **Binary Search** | Search on sorted arrays, rotated arrays, binary search on answers | [docs/06-binary-search/README.md](docs/06-binary-search/README.md) |
| 07 | **Two Pointers & Sliding Window** | Opposite ends, fast/slow, fixed & dynamic windows | [docs/07-two-pointers-sliding-window/README.md](docs/07-two-pointers-sliding-window/README.md) |
| 08 | **Binary Trees** | DFS/BFS, tree traversals, diameters, LCA, path sums | [docs/08-binary-tree/README.md](docs/08-binary-tree/README.md) |
| 09 | **Binary Search Trees (BST)** | BST properties, validation, in-order traversal, rebalancing | [docs/09-binary-search-tree/README.md](docs/09-binary-search-tree/README.md) |
| 10 | **Heap / Priority Queue** | Top-K elements, streaming medians, K-way merges | [docs/10-heap/README.md](docs/10-heap/README.md) |
| 11 | **Backtracking** | Combinations, permutations, subsets, board constraint solving | [docs/11-backtracking/README.md](docs/11-backtracking/README.md) |
| 12 | **Greedy Algorithms** | Interval scheduling, local-to-global optimum decisions | [docs/12-greedy/README.md](docs/12-greedy/README.md) |
| 13 | **Dynamic Programming** | 1D/2D DP, knapsack variations, LCS, LIS, grid paths, memoization | [docs/13-dynamic-programming/README.md](docs/13-dynamic-programming/README.md) |
| 14 | **Graphs** | BFS/DFS, cycle detection, Topological Sort, Dijkstra, Union-Find | [docs/14-graphs/README.md](docs/14-graphs/README.md) |

---

## 🎯 Solution Architecture & Standardization Guide

To maintain uniform clarity, every problem in this repository adheres to a strict 4-part structure:

### 1. Problem Statement
- **Description:** Concise specification of the input, expected output, and underlying rules.
- **Constraints:** Bounds on input size ($n \le 10^5$, etc.) and values which dictate acceptable time complexity.
- **Examples:** Clear input/output samples including typical edge cases (empty inputs, negative values, duplicates).

### 2. Intuition & Approach
- **Mental Model:** The underlying pattern (e.g., *monotonic stack*, *dynamic window*, *post-order DFS*).
- **Step-by-Step Logic:**
  1. *Brute Force:* Initial naive line of thought and why it falls short (e.g., $O(n^2)$ time).
  2. *Optimized Transformation:* What invariant or observation enables the jump to $O(n)$ or $O(n \log n)$.
  3. *Edge Cases:* Handling `null`, single-element collections, cycles, and boundary conditions.

### 3. Time & Space Complexity
- **Time Complexity:** Expressed in Big-$O$ notation with detailed justification of each component (e.g., traversing vertices + edges in BFS $\to O(V + E)$).
- **Space Complexity:** Explicitly distinguishes auxiliary working space, recursion call stack depth, and output storage.

### 4. Code Implementation
- Robust, idiomatic, clean code written with meaningful variable names and zero unnecessary overhead.
- Multi-language support (Python, C++, Java, JavaScript/TypeScript).

---

## 🛠️ Local Development & Preview

This documentation is built with [MkDocs Material](https://squidfunk.github.io/mkdocs-material/). You can serve the documentation locally to preview additions before pushing:

```bash
# 1. Create and activate a virtual environment (optional but recommended)
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate

# 2. Install dependencies
pip install mkdocs-material

# 3. Start local development server
mkdocs serve
```

Visit `http://127.0.0.1:8000/` in your browser to view the interactive documentation with hot reload.

---

## 🚀 Automated Deployment

Every push to the `main` branch automatically triggers the `.github/workflows/deploy.yml` workflow, compiling the Markdown files into static HTML and publishing them to GitHub Pages.

---

## 📄 License

This repository is licensed under the [MIT License](LICENSE).
