[← Back to Main Index](../index.md)

# Foundation & Complexity - Most Important Questions and Answers

## 📖 Topic Overview

The Foundation module establishes the mathematical, analytical, and elementary algorithmic toolkit required for every coding interview:

- **Asymptotic Complexity (Big-O, Big-$\Omega$, Big-$\Theta$):** Characterizing time and memory growth as input size $N \to \infty$. Focus on tight upper bounds ($O$) and worst-case scenarios.
- **Bit Manipulation:** Understanding bitwise operators (`AND`, `OR`, `XOR`, `NOT`, `<<`, `>>`). Core tricks include:
  - Check if number is power of two: `(n & (n - 1)) == 0 && n > 0`
  - Clear lowest set bit: `n & (n - 1)`
  - Isolate lowest set bit: `n & (-n)`
  - XOR self-cancellation: `x ^ x = 0`, `x ^ 0 = x`
- **Essential Math & Number Theory:** Fast exponentiation (binary exponentiation in $O(\log n)$), Euclidean algorithm for Greatest Common Divisor ($O(\log(\min(a, b)))$), modulo arithmetic, and prime factorization / Sieve of Eratosthenes ($O(n \log \log n)$).

---

## 🎯 High-Yield Problem Checklist

- [x] **Sum of Array Elements:** Linear scan accumulator
- [x] **Find Largest Number in an Array:** In-place running maximum scan
- [x] **Find Smallest Number in an Array:** In-place running minimum scan
- [x] **Second Largest Element in an Array:** Single-pass dual-state pointer tracking
- [x] **Palindrome Number (LeetCode #9):** Half-reversion without string conversion
- [x] **Reverse Integer (LeetCode #7):** 32-bit overflow prevention via modular arithmetic
- [x] **Count Negative Numbers in a Sorted Matrix (LeetCode #1351):** Top-right staircase traversal in $O(M + N)$
- [x] **Power of Two (LeetCode #231):** $O(1)$ bit manipulation property
- [x] **Binary Search (LeetCode #704):** Canonical divide-and-conquer on sorted arrays
- [x] **Merge Sort:** Classic divide-and-conquer sorting with $O(N \log N)$ guarantee
- [x] **Single Number (LeetCode #136):** Bit manipulation using XOR cancellation property
- [x] **Number of 1 Bits / Hamming Weight (LeetCode #191):** Brian Kernighan's algorithm (`n & (n - 1)`)
- [x] **Counting Bits (LeetCode #338):** DP with bit manipulation offset
- [x] **Reverse Bits (LeetCode #190):** 32-bit bitwise reversal via shifts and masks
- [x] **Missing Number (LeetCode #268):** XOR sum vs. Gauss arithmetic series
- [x] **Pow(x, n) (LeetCode #50):** Fast binary exponentiation handling negative powers
- [x] **Count Primes (LeetCode #204):** Sieve of Eratosthenes optimization
- [x] **Asymptotic Analysis & Master Theorem Reference:** Recurrence relations cheat sheet

---

> [!TIP]
> **Want to contribute a solution or add a new question to this topic?**  
> Check our standardized format and guidelines in the [How to Contribute & Question Template Guide](../contributing.md).

---

## 1. Sum of Array Elements

### 1. Problem Statement
Given an integer array `nums`, compute and return the total sum of all its elements.

- **Input:** `nums = [1, 2, 3, 4, 5]`
- **Output:** `15`
- **Constraints:**
  - $1 \le \text{nums.length} \le 10^5$
  - $-10^4 \le \text{nums}[i] \le 10^4$

### 2. Intuition & Approach
- Initialize an accumulator variable `total_sum = 0`.
- Iterate through each element in the array and add it to the running sum.
- When working with languages like C++ or Java, be aware of integer overflow if the sum can exceed $2^{31}-1$ (use 64-bit integers / `long` if values are large).

### 3. Time & Space Complexity
- **Time Complexity:** $O(N)$ — single linear pass through $N$ elements.
- **Space Complexity:** $O(1)$ — constant extra memory for the accumulator.

### 4. Code Implementation

=== "Python"
    ```python
    from typing import List

    class Solution:
        def sumArray(self, nums: List[int]) -> int:
            total = 0
            for num in nums:
                total += num
            return total
    ```

=== "C++"
    ```cpp
    #include <vector>
    #include <numeric>

    class Solution {
    public:
        long long sumArray(const std::vector<int>& nums) {
            long long total = 0;
            for (int num : nums) {
                total += num;
            }
            return total;
        }
    };
    ```

=== "Java"
    ```java
    class Solution {
        public long sumArray(int[] nums) {
            long total = 0;
            for (int num : nums) {
                total += num;
            }
            return total;
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function sumArray(nums: number[]): number {
        return nums.reduce((acc, curr) => acc + curr, 0);
    }
    ```

---

## 2. Find Largest Number in an Array

### 1. Problem Statement
Given an array `nums` of $N$ integers, find and return the maximum element present in the array without using built-in library functions.

- **Input:** `nums = [3, 7, 2, 9, 5]`
- **Output:** `9`
- **Constraints:**
  - $1 \le \text{nums.length} \le 10^5$
  - $-10^9 \le \text{nums}[i] \le 10^9$

### 2. Intuition & Approach
- Initialize `max_val` to the first element `nums[0]`.
- Traverse the array starting from the second element (index 1).
- For each element, if `nums[i] > max_val`, update `max_val = nums[i]`.
- After inspecting all elements, `max_val` holds the largest number.

### 3. Time & Space Complexity
- **Time Complexity:** $O(N)$ — visits each element exactly once.
- **Space Complexity:** $O(1)$ — only stores one variable.

### 4. Code Implementation

=== "Python"
    ```python
    from typing import List

    class Solution:
        def findLargest(self, nums: List[int]) -> int:
            max_val = nums[0]
            for num in nums[1:]:
                if num > max_val:
                    max_val = num
            return max_val
    ```

=== "C++"
    ```cpp
    #include <vector>

    class Solution {
    public:
        int findLargest(const std::vector<int>& nums) {
            int max_val = nums[0];
            for (size_t i = 1; i < nums.size(); ++i) {
                if (nums[i] > max_val) {
                    max_val = nums[i];
                }
            }
            return max_val;
        }
    };
    ```

=== "Java"
    ```java
    class Solution {
        public int findLargest(int[] nums) {
            int maxVal = nums[0];
            for (int i = 1; i < nums.length; i++) {
                if (nums[i] > maxVal) {
                    maxVal = nums[i];
                }
            }
            return maxVal;
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function findLargest(nums: number[]): number {
        let maxVal = nums[0];
        for (let i = 1; i < nums.length; i++) {
            if (nums[i] > maxVal) {
                maxVal = nums[i];
            }
        }
        return maxVal;
    }
    ```

---

## 3. Find Smallest Number in an Array

### 1. Problem Statement
Given an array `nums` of $N$ integers, find and return the minimum element present in the array without using built-in library functions.

- **Input:** `nums = [12, 4, 56, 1, 99]`
- **Output:** `1`
- **Constraints:**
  - $1 \le \text{nums.length} \le 10^5$
  - $-10^9 \le \text{nums}[i] \le 10^9$

### 2. Intuition & Approach
- Initialize `min_val` to `nums[0]`.
- Scan linearly across the array. Whenever an element smaller than `min_val` is encountered, update `min_val`.

### 3. Time & Space Complexity
- **Time Complexity:** $O(N)$ — single pass.
- **Space Complexity:** $O(1)$ — constant storage.

### 4. Code Implementation

=== "Python"
    ```python
    from typing import List

    class Solution:
        def findSmallest(self, nums: List[int]) -> int:
            min_val = nums[0]
            for num in nums[1:]:
                if num < min_val:
                    min_val = num
            return min_val
    ```

=== "C++"
    ```cpp
    #include <vector>

    class Solution {
    public:
        int findSmallest(const std::vector<int>& nums) {
            int min_val = nums[0];
            for (size_t i = 1; i < nums.size(); ++i) {
                if (nums[i] < min_val) {
                    min_val = nums[i];
                }
            }
            return min_val;
        }
    };
    ```

=== "Java"
    ```java
    class Solution {
        public int findSmallest(int[] nums) {
            int minVal = nums[0];
            for (int i = 1; i < nums.length; i++) {
                if (nums[i] < minVal) {
                    minVal = nums[i];
                }
            }
            return minVal;
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function findSmallest(nums: number[]): number {
        let minVal = nums[0];
        for (let i = 1; i < nums.length; i++) {
            if (nums[i] < minVal) {
                minVal = nums[i];
            }
        }
        return minVal;
    }
    ```

---

## 4. Second Largest Element in an Array

### 1. Problem Statement
Given an array of integers `nums`, return the second largest distinct element. If no second largest distinct element exists, return `-1`.

- **Input:** `nums = [12, 35, 1, 10, 34, 1]`
- **Output:** `34`
- **Constraints:**
  - $2 \le \text{nums.length} \le 10^5$
  - $-10^9 \le \text{nums}[i] \le 10^9$

### 2. Intuition & Approach
- **Naive Approach:** Sort the array in descending order in $O(N \log N)$ and search for the first distinct element smaller than `nums[0]`.
- **Optimal Single Pass:**
  - Track two variables: `first = -inf` and `second = -inf`.
  - For each number `x`:
    1. If `x > first`: the old `first` becomes `second`, and `first = x`.
    2. Else if `x > second` and `x != first`: update `second = x`.
  - If `second` remains `-inf`, return `-1`.

### 3. Time & Space Complexity
- **Time Complexity:** $O(N)$ — single linear scan.
- **Space Complexity:** $O(1)$ — two tracking variables.

### 4. Code Implementation

=== "Python"
    ```python
    from typing import List

    class Solution:
        def getSecondLargest(self, nums: List[int]) -> int:
            first = float('-inf')
            second = float('-inf')
            
            for num in nums:
                if num > first:
                    second = first
                    first = num
                elif num > second and num != first:
                    second = num
                    
            return int(second) if second != float('-inf') else -1
    ```

=== "C++"
    ```cpp
    #include <vector>
    #include <climits>

    class Solution {
    public:
        int getSecondLargest(const std::vector<int>& nums) {
            long long first = LLONG_MIN;
            long long second = LLONG_MIN;
            
            for (int num : nums) {
                if (num > first) {
                    second = first;
                    first = num;
                } else if (num > second && num != first) {
                    second = num;
                }
            }
            return (second == LLONG_MIN) ? -1 : static_cast<int>(second);
        }
    };
    ```

=== "Java"
    ```java
    class Solution {
        public int getSecondLargest(int[] nums) {
            long first = Long.MIN_VALUE;
            long second = Long.MIN_VALUE;

            for (int num : nums) {
                if (num > first) {
                    second = first;
                    first = num;
                } else if (num > second && num != first) {
                    second = num;
                }
            }
            return second == Long.MIN_VALUE ? -1 : (int) second;
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function getSecondLargest(nums: number[]): number {
        let first = -Infinity;
        let second = -Infinity;

        for (const num of nums) {
            if (num > first) {
                second = first;
                first = num;
            } else if (num > second && num !== first) {
                second = num;
            }
        }

        return second === -Infinity ? -1 : second;
    }
    ```

---

## 5. Palindrome Number (LeetCode #9)

### 1. Problem Statement
Given an integer `x`, return `true` if `x` is a palindrome, and `false` otherwise. Solve it without converting the integer to a string.

- **Input:** `x = 121` $\to$ **Output:** `true`
- **Input:** `x = -121` $\to$ **Output:** `false` (negative numbers are not palindromes due to leading `-`)
- **Constraints:** $-2^{31} \le x \le 2^{31} - 1$

### 2. Intuition & Approach
- Edge cases: Negative numbers cannot be palindromes. Also, numbers ending in 0 (except 0 itself) cannot be palindromes (e.g., 10 $\to$ 01).
- Instead of reversing the whole integer (which might cause 32-bit overflow), reverse only the **second half** of the number.
- Stop reversing when `reverted_number >= x`.
- For even length digits: check `x == reverted_number`.
- For odd length digits: the middle digit doesn't matter, check `x == reverted_number // 10`.

### 3. Time & Space Complexity
- **Time Complexity:** $O(\log_{10} N)$ — divides by 10 on each iteration.
- **Space Complexity:** $O(1)$ — constant extra space.

### 4. Code Implementation

=== "Python"
    ```python
    class Solution:
        def isPalindrome(self, x: int) -> bool:
            if x < 0 or (x % 10 == 0 and x != 0):
                return False
            
            reverted = 0
            while x > reverted:
                reverted = reverted * 10 + x % 10
                x //= 10
                
            return x == reverted or x == reverted // 10
    ```

=== "C++"
    ```cpp
    class Solution {
    public:
        bool isPalindrome(int x) {
            if (x < 0 || (x % 10 == 0 && x != 0)) return false;
            
            int reverted = 0;
            while (x > reverted) {
                reverted = reverted * 10 + x % 10;
                x /= 10;
            }
            return x == reverted || x == reverted / 10;
        }
    };
    ```

=== "Java"
    ```java
    class Solution {
        public boolean isPalindrome(int x) {
            if (x < 0 || (x % 10 == 0 && x != 0)) return false;

            int reverted = 0;
            while (x > reverted) {
                reverted = reverted * 10 + x % 10;
                x /= 10;
            }
            return x == reverted || x == reverted / 10;
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function isPalindrome(x: number): boolean {
        if (x < 0 || (x % 10 === 0 && x !== 0)) return false;

        let reverted = 0;
        while (x > reverted) {
            reverted = reverted * 10 + (x % 10);
            x = Math.floor(x / 10);
        }
        return x === reverted || x === Math.floor(reverted / 10);
    }
    ```

---

## 6. Reverse Integer (LeetCode #7)

### 1. Problem Statement
Given a signed 32-bit integer `x`, return `x` with its digits reversed. If reversing `x` causes the value to go outside the signed 32-bit integer range $[-2^{31}, 2^{31} - 1]$, return `0`.

- **Input:** `x = 123` $\to$ **Output:** `321`
- **Input:** `x = -123` $\to$ **Output:** `-321`
- **Constraints:** $-2^{31} \le x \le 2^{31} - 1$

### 2. Intuition & Approach
- Repeatedly pop the last digit: `digit = x % 10`.
- Before pushing `digit` to `rev = rev * 10 + digit`, verify that `rev` will not overflow:
  - If `rev > INT_MAX / 10` (or `rev == INT_MAX / 10 && digit > 7`), it will overflow.
  - If `rev < INT_MIN / 10` (or `rev == INT_MIN / 10 && digit < -8`), it will underflow.

### 3. Time & Space Complexity
- **Time Complexity:** $O(\log_{10} |X|)$ — roughly 10 iterations max for a 32-bit integer.
- **Space Complexity:** $O(1)$.

### 4. Code Implementation

=== "Python"
    ```python
    class Solution:
        def reverse(self, x: int) -> int:
            INT_MIN, INT_MAX = -2**31, 2**31 - 1
            rev = 0
            sign = -1 if x < 0 else 1
            x = abs(x)
            
            while x != 0:
                digit = x % 10
                x //= 10
                if rev > (INT_MAX - digit) // 10:
                    return 0
                rev = rev * 10 + digit
                
            return sign * rev
    ```

=== "C++"
    ```cpp
    #include <climits>

    class Solution {
    public:
        int reverse(int x) {
            int rev = 0;
            while (x != 0) {
                int pop = x % 10;
                x /= 10;
                if (rev > INT_MAX / 10 || (rev == INT_MAX / 10 && pop > 7)) return 0;
                if (rev < INT_MIN / 10 || (rev == INT_MIN / 10 && pop < -8)) return 0;
                rev = rev * 10 + pop;
            }
            return rev;
        }
    };
    ```

=== "Java"
    ```java
    class Solution {
        public int reverse(int x) {
            int rev = 0;
            while (x != 0) {
                int pop = x % 10;
                x /= 10;
                if (rev > Integer.MAX_VALUE / 10 || (rev == Integer.MAX_VALUE / 10 && pop > 7)) return 0;
                if (rev < Integer.MIN_VALUE / 10 || (rev == Integer.MIN_VALUE / 10 && pop < -8)) return 0;
                rev = rev * 10 + pop;
            }
            return rev;
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function reverse(x: number): number {
        const INT_MIN = -(2 ** 31);
        const INT_MAX = 2 ** 31 - 1;
        let rev = 0;
        const sign = x < 0 ? -1 : 1;
        x = Math.abs(x);

        while (x !== 0) {
            const digit = x % 10;
            x = Math.floor(x / 10);
            if (rev > Math.floor((INT_MAX - digit) / 10)) return 0;
            rev = rev * 10 + digit;
        }

        return sign * rev;
    }
    ```

---

## 7. Count Negative Numbers in a Sorted Matrix (LeetCode #1351)

### 1. Problem Statement
Given an $m \times n$ matrix `grid` which is sorted in non-increasing order both row-wise and column-wise, return the number of negative numbers in `grid`.

- **Input:** `grid = [[4,3,2,-1],[3,2,1,-1],[1,1,-1,-2],[-1,-1,-2,-3]]`
- **Output:** `8`
- **Constraints:**
  - $m == \text{grid.length}, \ n == \text{grid}[i]\text{.length}$
  - $1 \le m, n \le 100$

### 2. Intuition & Approach
- **Brute Force:** Scan every cell in $O(M \times N)$.
- **Optimal Staircase Walk:**
  - Start at the top-right corner (`row = 0`, `col = n - 1`).
  - If `grid[row][col] < 0`: because columns are sorted non-increasingly downwards, every element below `grid[row][col]` in column `col` is also negative. Hence, add `(m - row)` to our count and move left (`col--`).
  - Else (`grid[row][col] >= 0`): move downwards (`row++`).

### 3. Time & Space Complexity
- **Time Complexity:** $O(M + N)$ — starts at top-right and moves only left or down.
- **Space Complexity:** $O(1)$ — constant pointer space.

### 4. Code Implementation

=== "Python"
    ```python
    from typing import List

    class Solution:
        def countNegatives(self, grid: List[List[int]]) -> int:
            rows, cols = len(grid), len(grid[0])
            count = 0
            r = 0
            c = cols - 1
            
            while r < rows and c >= 0:
                if grid[r][c] < 0:
                    count += (rows - r)
                    c -= 1
                else:
                    r += 1
                    
            return count
    ```

=== "C++"
    ```cpp
    #include <vector>

    class Solution {
    public:
        int countNegatives(const std::vector<std::vector<int>>& grid) {
            int rows = grid.size();
            int cols = grid[0].size();
            int count = 0;
            int r = 0, c = cols - 1;
            
            while (r < rows && c >= 0) {
                if (grid[r][c] < 0) {
                    count += (rows - r);
                    c--;
                } else {
                    r++;
                }
            }
            return count;
        }
    };
    ```

=== "Java"
    ```java
    class Solution {
        public int countNegatives(int[][] grid) {
            int rows = grid.length;
            int cols = grid[0].length;
            int count = 0;
            int r = 0, c = cols - 1;

            while (r < rows && c >= 0) {
                if (grid[r][c] < 0) {
                    count += (rows - r);
                    c--;
                } else {
                    r++;
                }
            }
            return count;
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function countNegatives(grid: number[][]): number {
        const rows = grid.length;
        const cols = grid[0].length;
        let count = 0;
        let r = 0;
        let c = cols - 1;

        while (r < rows && c >= 0) {
            if (grid[r][c] < 0) {
                count += (rows - r);
                c--;
            } else {
                r++;
            }
        }

        return count;
    }
    ```

---

## 8. Power of Two (LeetCode #231)

### 1. Problem Statement
Given an integer `n`, return `true` if it is a power of two. Otherwise, return `false`. An integer `n` is a power of two if there exists an integer `x` such that $n == 2^x$.

- **Input:** `n = 16` $\to$ **Output:** `true`
- **Input:** `n = 3` $\to$ **Output:** `false`
- **Constraints:** $-2^{31} \le n \le 2^{31} - 1$

### 2. Intuition & Approach
- In binary representation, a positive power of two has exactly one bit set to `1` (e.g., $16 = 10000_2$, $4 = 100_2$).
- The expression `n & (n - 1)` clears the lowest set bit.
- If `n > 0` and `(n & (n - 1)) == 0`, then `n` had exactly one set bit and is a power of two.

### 3. Time & Space Complexity
- **Time Complexity:** $O(1)$ — single bitwise operation.
- **Space Complexity:** $O(1)$.

### 4. Code Implementation

=== "Python"
    ```python
    class Solution:
        def isPowerOfTwo(self, n: int) -> bool:
            return n > 0 and (n & (n - 1)) == 0
    ```

=== "C++"
    ```cpp
    class Solution {
    public:
        bool isPowerOfTwo(int n) {
            return n > 0 && (n & (n - 1LL)) == 0;
        }
    };
    ```

=== "Java"
    ```java
    class Solution {
        public boolean isPowerOfTwo(int n) {
            return n > 0 && (n & (n - 1)) == 0;
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function isPowerOfTwo(n: number): boolean {
        return n > 0 && (n & (n - 1)) === 0;
    }
    ```

---

## 9. Binary Search (LeetCode #704)

### 1. Problem Statement
Given an array of integers `nums` which is sorted in ascending order, and an integer `target`, write a function to search `target` in `nums`. If `target` exists, then return its index. Otherwise, return `-1`. You must write an algorithm with $O(\log n)$ runtime complexity.

- **Input:** `nums = [-1,0,3,5,9,12]`, `target = 9` $\to$ **Output:** `4`
- **Constraints:** $1 \le \text{nums.length} \le 10^4$

### 2. Intuition & Approach
- Maintain two pointers: `left = 0` and `right = len(nums) - 1`.
- While `left <= right`:
  - Calculate safe midpoint: `mid = left + (right - left) // 2` to prevent 32-bit integer overflow.
  - If `nums[mid] == target`: return `mid`.
  - If `nums[mid] < target`: target must lie in the right half $\to$ `left = mid + 1`.
  - If `nums[mid] > target`: target must lie in the left half $\to$ `right = mid - 1`.
- If the loop terminates without finding `target`, return `-1`.

### 3. Time & Space Complexity
- **Time Complexity:** $O(\log N)$ — search space halves in every iteration.
- **Space Complexity:** $O(1)$ — iterative traversal.

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
                elif nums[mid] < target:
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
        int search(const std::vector<int>& nums, int target) {
            int left = 0, right = nums.size() - 1;
            while (left <= right) {
                int mid = left + (right - left) / 2;
                if (nums[mid] == target) return mid;
                if (nums[mid] < target) left = mid + 1;
                else right = mid - 1;
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
                if (nums[mid] < target) left = mid + 1;
                else right = mid - 1;
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
            if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return -1;
    }
    ```

---

## 10. Merge Sort

### 1. Problem Statement
Implement the Merge Sort algorithm to sort an array of integers in non-decreasing order using the divide-and-conquer strategy.

- **Input:** `nums = [5, 2, 3, 1]`
- **Output:** `[1, 2, 3, 5]`
- **Constraints:** $1 \le \text{nums.length} \le 5 \cdot 10^4$

### 2. Intuition & Approach
- **Divide:** Divide the array into two halves around midpoint `mid = (left + right) // 2`.
- **Conquer:** Recursively sort the left half and right half.
- **Combine:** Merge the two sorted subarrays using two pointers into a temporary buffer, then copy back to the original array.
- Guaranteed $O(N \log N)$ worst-case time complexity, stable sorting property.

### 3. Time & Space Complexity
- **Time Complexity:** $O(N \log N)$ — recurrence $T(N) = 2T(N/2) + O(N)$.
- **Space Complexity:** $O(N)$ — auxiliary buffer for merging.

### 4. Code Implementation

=== "Python"
    ```python
    from typing import List

    class Solution:
        def sortArray(self, nums: List[int]) -> List[int]:
            def merge_sort(left: int, right: int):
                if left >= right:
                    return
                mid = left + (right - left) // 2
                merge_sort(left, mid)
                merge_sort(mid + 1, right)
                merge(left, mid, right)

            def merge(left: int, mid: int, right: int):
                temp = []
                i, j = left, mid + 1
                while i <= mid and j <= right:
                    if nums[i] <= nums[j]:
                        temp.append(nums[i])
                        i += 1
                    else:
                        temp.append(nums[j])
                        j += 1
                while i <= mid:
                    temp.append(nums[i])
                    i += 1
                while j <= right:
                    temp.append(nums[j])
                    j += 1
                nums[left:right + 1] = temp

            merge_sort(0, len(nums) - 1)
            return nums
    ```

=== "C++"
    ```cpp
    #include <vector>

    class Solution {
    public:
        std::vector<int> sortArray(std::vector<int>& nums) {
            std::vector<int> temp(nums.size());
            mergeSort(nums, temp, 0, nums.size() - 1);
            return nums;
        }

    private:
        void mergeSort(std::vector<int>& nums, std::vector<int>& temp, int left, int right) {
            if (left >= right) return;
            int mid = left + (right - left) / 2;
            mergeSort(nums, temp, left, mid);
            mergeSort(nums, temp, mid + 1, right);
            merge(nums, temp, left, mid, right);
        }

        void merge(std::vector<int>& nums, std::vector<int>& temp, int left, int mid, int right) {
            int i = left, j = mid + 1, k = left;
            while (i <= mid && j <= right) {
                if (nums[i] <= nums[j]) temp[k++] = nums[i++];
                else temp[k++] = nums[j++];
            }
            while (i <= mid) temp[k++] = nums[i++];
            while (j <= right) temp[k++] = nums[j++];
            for (int p = left; p <= right; ++p) nums[p] = temp[p];
        }
    };
    ```

=== "Java"
    ```java
    class Solution {
        public int[] sortArray(int[] nums) {
            int[] temp = new int[nums.length];
            mergeSort(nums, temp, 0, nums.length - 1);
            return nums;
        }

        private void mergeSort(int[] nums, int[] temp, int left, int right) {
            if (left >= right) return;
            int mid = left + (right - left) / 2;
            mergeSort(nums, temp, left, mid);
            mergeSort(nums, temp, mid + 1, right);
            merge(nums, temp, left, mid, right);
        }

        private void merge(int[] nums, int[] temp, int left, int mid, int right) {
            int i = left, j = mid + 1, k = left;
            while (i <= mid && j <= right) {
                if (nums[i] <= nums[j]) temp[k++] = nums[i++];
                else temp[k++] = nums[j++];
            }
            while (i <= mid) temp[k++] = nums[i++];
            while (j <= right) temp[k++] = nums[j++];
            for (int p = left; p <= right; p++) nums[p] = temp[p];
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function sortArray(nums: number[]): number[] {
        const temp = new Array(nums.length);

        function mergeSort(left: number, right: number) {
            if (left >= right) return;
            const mid = Math.floor(left + (right - left) / 2);
            mergeSort(left, mid);
            mergeSort(mid + 1, right);
            merge(left, mid, right);
        }

        function merge(left: number, mid: number, right: number) {
            let i = left, j = mid + 1, k = left;
            while (i <= mid && j <= right) {
                if (nums[i] <= nums[j]) temp[k++] = nums[i++];
                else temp[k++] = nums[j++];
            }
            while (i <= mid) temp[k++] = nums[i++];
            while (j <= right) temp[k++] = nums[j++];
            for (let p = left; p <= right; p++) nums[p] = temp[p];
        }

        mergeSort(0, nums.length - 1);
        return nums;
    }
    ```

---

## 11. Single Number (LeetCode #136)

### 1. Problem Statement
Given a non-empty array of integers `nums`, every element appears twice except for one. Find that single one. You must implement a solution with linear runtime complexity and use only constant extra space.

- **Input:** `nums = [4, 1, 2, 1, 2]` $\to$ **Output:** `4`
- **Constraints:** $1 \le \text{nums.length} \le 3 \cdot 10^4$

### 2. Intuition & Approach
- The XOR bitwise operator ($\oplus$) satisfies:
  - $a \oplus a = 0$ (self-inverse)
  - $a \oplus 0 = a$ (identity)
  - Associative and commutative: $a \oplus b \oplus a = (a \oplus a) \oplus b = 0 \oplus b = b$.
- XORing all elements together eliminates all pairs, isolating the single element in $O(N)$ time with zero extra allocations.

### 3. Time & Space Complexity
- **Time Complexity:** $O(N)$ — single pass.
- **Space Complexity:** $O(1)$ — single accumulator.

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
        int singleNumber(const std::vector<int>& nums) {
            int result = 0;
            for (int num : nums) result ^= num;
            return result;
        }
    };
    ```

=== "Java"
    ```java
    class Solution {
        public int singleNumber(int[] nums) {
            int result = 0;
            for (int num : nums) result ^= num;
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

---

## 12. Number of 1 Bits / Hamming Weight (LeetCode #191)

### 1. Problem Statement
Given a positive integer `n`, write a function that returns the number of set bits (1s) in its binary representation (also known as the Hamming weight).

- **Input:** `n = 11` ($1011_2$) $\to$ **Output:** `3`
- **Constraints:** $1 \le n \le 2^{31} - 1$

### 2. Intuition & Approach
- **Brian Kernighan's Algorithm:**
  - The operation `n & (n - 1)` always clears the lowest set bit of `n`.
  - Repeat `n = n & (n - 1)` and increment a counter until `n == 0`.
  - Runs in time proportional to the number of set bits, not the total number of bits.

### 3. Time & Space Complexity
- **Time Complexity:** $O(k)$ where $k \le 32$ is the number of set bits.
- **Space Complexity:** $O(1)$.

### 4. Code Implementation

=== "Python"
    ```python
    class Solution:
        def hammingWeight(self, n: int) -> int:
            count = 0
            while n:
                n &= (n - 1)
                count += 1
            return count
    ```

=== "C++"
    ```cpp
    class Solution {
    public:
        int hammingWeight(int n) {
            int count = 0;
            while (n) {
                n &= (n - 1);
                count++;
            }
            return count;
        }
    };
    ```

=== "Java"
    ```java
    class Solution {
        public int hammingWeight(int n) {
            int count = 0;
            while (n != 0) {
                n &= (n - 1);
                count++;
            }
            return count;
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function hammingWeight(n: number): number {
        let count = 0;
        while (n !== 0) {
            n &= (n - 1);
            count++;
        }
        return count;
    }
    ```

---

## 13. Counting Bits (LeetCode #338)

### 1. Problem Statement
Given an integer `n`, return an array `ans` of length $n + 1$ such that for each $i$ ($0 \le i \le n$), `ans[i]` is the number of `1`'s in the binary representation of $i$. Solve it in linear time $O(n)$ without calling built-in popcount functions.

- **Input:** `n = 5` $\to$ **Output:** `[0, 1, 1, 2, 1, 2]`
- **Constraints:** $0 \le n \le 10^5$

### 2. Intuition & Approach
- Notice the recurrence relation:
  - If we right-shift $i$ by 1 (`i >> 1`), we discard the least significant bit.
  - The number of 1s in $i$ equals the number of 1s in `i >> 1` plus `1` if $i$ is odd (`i & 1`), or `0` if $i$ is even:
    $$\text{ans}[i] = \text{ans}[i >> 1] + (i \ \& \ 1)$$
- Build the DP array iteratively from $1$ to $n$.

### 3. Time & Space Complexity
- **Time Complexity:** $O(N)$ — computes each entry in $O(1)$ time.
- **Space Complexity:** $O(1)$ — auxiliary space beyond the output array.

### 4. Code Implementation

=== "Python"
    ```python
    from typing import List

    class Solution:
        def countBits(self, n: int) -> List[int]:
            ans = [0] * (n + 1)
            for i in range(1, n + 1):
                ans[i] = ans[i >> 1] + (i & 1)
            return ans
    ```

=== "C++"
    ```cpp
    #include <vector>

    class Solution {
    public:
        std::vector<int> countBits(int n) {
            std::vector<int> ans(n + 1, 0);
            for (int i = 1; i <= n; ++i) {
                ans[i] = ans[i >> 1] + (i & 1);
            }
            return ans;
        }
    };
    ```

=== "Java"
    ```java
    class Solution {
        public int[] countBits(int n) {
            int[] ans = new int[n + 1];
            for (int i = 1; i <= n; i++) {
                ans[i] = ans[i >> 1] + (i & 1);
            }
            return ans;
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function countBits(n: number): number[] {
        const ans = new Array(n + 1).fill(0);
        for (let i = 1; i <= n; i++) {
            ans[i] = ans[i >> 1] + (i & 1);
        }
        return ans;
    }
    ```

---

## 14. Reverse Bits (LeetCode #190)

### 1. Problem Statement
Reverse bits of a given 32 bits unsigned integer.

- **Input:** `00000010100101000001111010011100`
- **Output:** `00111001011110000010100101000000` (decimal: `964176192`)

### 2. Intuition & Approach
- Maintain a result variable `res = 0`.
- Loop 32 times:
  - Shift `res` to the left by 1 (`res << 1`).
  - Extract the lowest bit of `n` using `n & 1`.
  - Add this bit to `res` (`res | (n & 1)`).
  - Shift `n` to the right by 1 (`n >>= 1`).

### 3. Time & Space Complexity
- **Time Complexity:** $O(1)$ — fixed 32 iterations.
- **Space Complexity:** $O(1)$.

### 4. Code Implementation

=== "Python"
    ```python
    class Solution:
        def reverseBits(self, n: int) -> int:
            res = 0
            for _ in range(32):
                res = (res << 1) | (n & 1)
                n >>= 1
            return res
    ```

=== "C++"
    ```cpp
    #include <cstdint>

    class Solution {
    public:
        uint32_t reverseBits(uint32_t n) {
            uint32_t res = 0;
            for (int i = 0; i < 32; ++i) {
                res = (res << 1) | (n & 1);
                n >>= 1;
            }
            return res;
        }
    };
    ```

=== "Java"
    ```java
    public class Solution {
        public int reverseBits(int n) {
            int res = 0;
            for (int i = 0; i < 32; i++) {
                res = (res << 1) | (n & 1);
                n >>>= 1;
            }
            return res;
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function reverseBits(n: number): number {
        let res = 0;
        for (let i = 0; i < 32; i++) {
            res = (res * 2) + (n & 1);
            n = Math.floor(n / 2);
        }
        return res;
    }
    ```

---

## 15. Missing Number (LeetCode #268)

### 1. Problem Statement
Given an array `nums` containing $n$ distinct numbers in the range $[0, n]$, return the only number in the range that is missing from the array.

- **Input:** `nums = [3, 0, 1]` $\to$ **Output:** `2`
- **Constraints:** $n == \text{nums.length}, \ 1 \le n \le 10^4$

### 2. Intuition & Approach
- **Approach 1 (XOR Cancellation):** XOR all numbers from $0$ to $n$ with all numbers in `nums`. Every number appearing in both cancels out to 0, leaving only the missing number.
- **Approach 2 (Gauss Series Sum):** Expected sum is $\frac{n(n + 1)}{2}$. The missing number is $\text{expected\_sum} - \sum \text{nums}$.

### 3. Time & Space Complexity
- **Time Complexity:** $O(N)$ — single pass.
- **Space Complexity:** $O(1)$.

### 4. Code Implementation

=== "Python"
    ```python
    from typing import List

    class Solution:
        def missingNumber(self, nums: List[int]) -> int:
            missing = len(nums)
            for i, num in enumerate(nums):
                missing ^= i ^ num
            return missing
    ```

=== "C++"
    ```cpp
    #include <vector>

    class Solution {
    public:
        int missingNumber(const std::vector<int>& nums) {
            int missing = nums.size();
            for (int i = 0; i < nums.size(); ++i) {
                missing ^= i ^ nums[i];
            }
            return missing;
        }
    };
    ```

=== "Java"
    ```java
    class Solution {
        public int missingNumber(int[] nums) {
            int missing = nums.length;
            for (int i = 0; i < nums.length; i++) {
                missing ^= i ^ nums[i];
            }
            return missing;
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function missingNumber(nums: number[]): number {
        let missing = nums.length;
        for (let i = 0; i < nums.length; i++) {
            missing ^= i ^ nums[i];
        }
        return missing;
    }
    ```

---

## 16. Pow(x, n) (LeetCode #50)

### 1. Problem Statement
Implement `pow(x, n)`, which calculates $x$ raised to the power $n$ ($x^n$).

- **Input:** `x = 2.00000`, `n = 10` $\to$ **Output:** `1024.00000`
- **Input:** `x = 2.00000`, `n = -2` $\to$ **Output:** `0.25000`
- **Constraints:** $-100.0 < x < 100.0, \ -2^{31} \le n \le 2^{31} - 1$

### 2. Intuition & Approach
- **Binary Exponentiation (Fast Power):**
  - If $n < 0$, compute $(1/x)^{-n}$. Use a 64-bit integer to prevent integer overflow when $-n = -(-2^{31}) = 2^{31}$.
  - Notice:
    - $x^{2k} = (x^2)^k$
    - $x^{2k+1} = x \cdot (x^2)^k$
  - Each step squares $x$ and halves $n$, reducing complexity from $O(N) \to O(\log N)$.

### 3. Time & Space Complexity
- **Time Complexity:** $O(\log N)$ — power $n$ is halved at every iteration.
- **Space Complexity:** $O(1)$ — iterative implementation.

### 4. Code Implementation

=== "Python"
    ```python
    class Solution:
        def myPow(self, x: float, n: int) -> float:
            if n < 0:
                x = 1 / x
                n = -n
                
            result = 1.0
            current_product = x
            
            while n > 0:
                if n % 2 == 1:
                    result *= current_product
                current_product *= current_product
                n //= 2
                
            return result
    ```

=== "C++"
    ```cpp
    class Solution {
    public:
        double myPow(double x, int n) {
            long long N = n;
            if (N < 0) {
                x = 1.0 / x;
                N = -N;
            }
            double result = 1.0;
            double current_product = x;
            while (N > 0) {
                if (N % 2 == 1) result *= current_product;
                current_product *= current_product;
                N /= 2;
            }
            return result;
        }
    };
    ```

=== "Java"
    ```java
    class Solution {
        public double myPow(double x, int n) {
            long N = n;
            if (N < 0) {
                x = 1.0 / x;
                N = -N;
            }
            double result = 1.0;
            double currentProduct = x;
            while (N > 0) {
                if (N % 2 == 1) result *= currentProduct;
                currentProduct *= currentProduct;
                N /= 2;
            }
            return result;
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function myPow(x: number, n: number): number {
        let N = n;
        if (N < 0) {
            x = 1 / x;
            N = -N;
        }
        let result = 1.0;
        let currentProduct = x;
        while (N > 0) {
            if (N % 2 === 1) result *= currentProduct;
            currentProduct *= currentProduct;
            N = Math.floor(N / 2);
        }
        return result;
    }
    ```

---

## 17. Count Primes (LeetCode #204)

### 1. Problem Statement
Given an integer $n$, return the number of prime numbers that are strictly less than $n$.

- **Input:** `n = 10` $\to$ **Output:** `4` (the 4 prime numbers less than 10 are 2, 3, 5, and 7)
- **Constraints:** $0 \le n \le 5 \cdot 10^6$

### 2. Intuition & Approach
- **Sieve of Eratosthenes:**
  - Create a boolean array `is_prime` of size $n$, initialized to `True`. Set `is_prime[0] = is_prime[1] = False`.
  - For $i = 2$ up to $\sqrt{n}$:
    - If `is_prime[i]` is `True`, all its multiples starting from $i \times i$ (i.e. $i^2, i^2 + i, i^2 + 2i, \dots$) are composite; mark them `False`.
  - The count of `True` entries in `is_prime` is the answer.

### 3. Time & Space Complexity
- **Time Complexity:** $O(N \log \log N)$ — mathematical bound of the Sieve of Eratosthenes harmonic series.
- **Space Complexity:** $O(N)$ — boolean indicator array.

### 4. Code Implementation

=== "Python"
    ```python
    class Solution:
        def countPrimes(self, n: int) -> int:
            if n <= 2:
                return 0
                
            is_prime = [True] * n
            is_prime[0] = is_prime[1] = False
            
            p = 2
            while p * p < n:
                if is_prime[p]:
                    for multiple in range(p * p, n, p):
                        is_prime[multiple] = False
                p += 1
                
            return sum(is_prime)
    ```

=== "C++"
    ```cpp
    #include <vector>

    class Solution {
    public:
        int countPrimes(int n) {
            if (n <= 2) return 0;
            std::vector<bool> is_prime(n, true);
            is_prime[0] = is_prime[1] = false;
            
            for (long long p = 2; p * p < n; ++p) {
                if (is_prime[p]) {
                    for (long long multiple = p * p; multiple < n; multiple += p) {
                        is_prime[multiple] = false;
                    }
                }
            }
            int count = 0;
            for (int i = 2; i < n; ++i) {
                if (is_prime[i]) count++;
            }
            return count;
        }
    };
    ```

=== "Java"
    ```java
    class Solution {
        public int countPrimes(int n) {
            if (n <= 2) return 0;
            boolean[] isPrime = new boolean[n];
            for (int i = 2; i < n; i++) isPrime[i] = true;

            for (long p = 2; p * p < n; p++) {
                if (isPrime[(int) p]) {
                    for (long multiple = p * p; multiple < n; multiple += p) {
                        isPrime[(int) multiple] = false;
                    }
                }
            }
            int count = 0;
            for (int i = 2; i < n; i++) {
                if (isPrime[i]) count++;
            }
            return count;
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function countPrimes(n: number): number {
        if (n <= 2) return 0;
        const isPrime = new Uint8Array(n);
        isPrime.fill(1);
        isPrime[0] = isPrime[1] = 0;

        for (let p = 2; p * p < n; p++) {
            if (isPrime[p] === 1) {
                for (let multiple = p * p; multiple < n; multiple += p) {
                    isPrime[multiple] = 0;
                }
            }
        }

        let count = 0;
        for (let i = 2; i < n; i++) {
            if (isPrime[i] === 1) count++;
        }
        return count;
    }
    ```

---

## 18. Asymptotic Analysis & Master Theorem Reference

### The Master Theorem Framework
For divide-and-conquer recurrences of the form:
$$T(n) = a T\left(\frac{n}{b}\right) + O(n^d)$$
where $a \ge 1$, $b > 1$, and $d \ge 0$:

| Condition | Complexity | Common Example |
|---|---|---|
| $d < \log_b a$ | $T(n) = \Theta(n^{\log_b a})$ | Karatsuba multiplication ($a=3, b=2, d=1 \to O(n^{1.585})$) |
| $d = \log_b a$ | $T(n) = \Theta(n^d \log n)$ | Merge Sort ($a=2, b=2, d=1 \to O(n \log n)$) |
| $d > \log_b a$ | $T(n) = \Theta(n^d)$ | Binary Search ($a=1, b=2, d=0 \to O(\log n)$) |

### Common Recurrences Cheat Sheet
- **Binary Search:** $T(n) = T(n/2) + O(1) \implies O(\log n)$
- **Binary Tree DFS Traversal:** $T(n) = 2T(n/2) + O(1) \implies O(n)$
- **Merge Sort:** $T(n) = 2T(n/2) + O(n) \implies O(n \log n)$
- **Quick Sort (Average):** $T(n) = 2T(n/2) + O(n) \implies O(n \log n)$
- **Quick Sort (Worst):** $T(n) = T(n-1) + O(n) \implies O(n^2)$
