[← Back to Main Index](../index.md)

# Foundation & Complexity - Most Important Questions and Answers

## 📖 Topic Overview

The Foundation module establishes the mathematical and analytical toolkit required for every coding interview:

- **Asymptotic Complexity (Big-O, Big-$\Omega$, Big-$\Theta$):** Characterizing time and memory growth as input size $N \to \infty$. Focus on tight upper bounds ($O$) and worst-case scenarios.
- **Bit Manipulation:** Understanding bitwise operators (`AND`, `OR`, `XOR`, `NOT`, `<<`, `>>`). Core tricks include:
  - Check if number is power of two: `(n & (n - 1)) == 0 && n > 0`
  - Clear lowest set bit: `n & (n - 1)`
  - Isolate lowest set bit: `n & (-n)`
  - XOR self-cancellation: `x ^ x = 0`, `x ^ 0 = x`
- **Essential Math:** Fast exponentiation (binary exponentiation in $O(\log n)$), Euclidean algorithm for Greatest Common Divisor ($O(\log(\min(a, b)))$), and prime factorization / Sieve of Eratosthenes ($O(n \log \log n)$).

---

## 🎯 High-Yield Problem Checklist

- [ ] **Asymptotic Analysis & Master Theorem:** Analyze recursion tree branches and recurrence relations $T(n) = aT(n/b) + f(n)$
- [ ] **Single Number (LeetCode #136):** Bit manipulation using XOR cancellation property
- [ ] **Number of 1 Bits / Hamming Weight (LeetCode #191):** Counting set bits using Brian Kernighan's algorithm (`n & (n - 1)`)
- [ ] **Counting Bits (LeetCode #338):** DP with bit manipulation offset
- [ ] **Reverse Bits (LeetCode #190):** 32-bit bitwise reversal via shifts and masks
- [ ] **Missing Number (LeetCode #268):** XOR sum vs. Gauss arithmetic sum
- [ ] **Pow(x, n) (LeetCode #50):** Fast exponentiation handling negative powers
- [ ] **Count Primes (LeetCode #204):** Sieve of Eratosthenes optimization

---

> [!TIP]
> **Want to contribute a solution or add a new question to this topic?**  
> Check our standardized format and guidelines in the [How to Contribute & Question Template Guide](../contributing.md).

---

## 💡 Example: Single Number (LeetCode #136)

### 1. Problem Statement
Given a non-empty array of integers `nums`, every element appears twice except for one. Find that single one. You must implement a solution with linear runtime complexity and use only constant extra space.

### 2. Intuition & Approach
The XOR operator has two key algebraic properties:
1. $a \oplus a = 0$ (self-inversion)
2. $a \oplus 0 = a$ (identity element)
3. Associativity & Commutativity: the order of XOR operations does not matter.

If we XOR all numbers in the array together, every duplicate pair cancels out to 0, leaving only the unique number.

### 3. Time & Space Complexity
- **Time Complexity:** $O(N)$ — single pass through the array of length $N$.
- **Space Complexity:** $O(1)$ — only one accumulator variable is needed.

### 4. Code Implementation

=== "Python"
    ```python
    from typing import List

    class Solution:
        def singleNumber(self, nums: List[int]) -> int:
            result = 0
            for num in nums:
                result ^= num
            return result
    ```

=== "C++"
    ```cpp
    #include <vector>

    class Solution {
    public:
        int singleNumber(std::vector<int>& nums) {
            int result = 0;
            for (int num : nums) {
                result ^= num;
            }
            return result;
        }
    };
    ```

=== "Java"
    ```java
    class Solution {
        public int singleNumber(int[] nums) {
            int result = 0;
            for (int num : nums) {
                result ^= num;
            }
            return result;
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function singleNumber(nums: number[]): number {
        return nums.reduce((acc, curr) => acc ^ curr, 0);
    }
    ```
