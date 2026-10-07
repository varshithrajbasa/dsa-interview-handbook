[← Back to Main Index](../index.md)

# Strings - Most Important Questions and Answers

## 📖 Topic Overview

Strings are sequences of characters often subject to immutability constraints in languages like Python and Java. High-frequency string interview questions test anagram detection, substring searches, window state caching, and palindrome symmetries.

### Core Algorithmic Patterns:
1. **Character Frequency Counting & Direct Addressing:** Using fixed-size arrays (e.g., `int[26]` for lowercase English letters) or hash tables to verify anagrams or character uniqueness in $O(N)$ time and $O(1)$ space.
2. **Sliding Window for Substrings:** Expanding a right pointer to include characters and contracting a left pointer once constraints are violated (e.g., Longest Substring Without Repeating Characters).
3. **Expand Around Center (Palindromes):** Checking odd-length ($2i$) and even-length ($2i+1$) palindrome centers to find palindromic substrings in $O(N^2)$ time and $O(1)$ space.
4. **Two Pointers from Ends:** Palindrome verification, alphanumeric sanitization, and in-place string tokenization.
5. **Rolling Hash & String Matching:** Rabin-Karp or KMP (Knuth-Morris-Pratt) algorithm for linear-time pattern matching.

---

## 🎯 High-Yield Problem Checklist

- [ ] **Valid Anagram (LeetCode #242):** Fixed-size array frequency matching
- [ ] **Valid Palindrome (LeetCode #125):** Two pointers skipping non-alphanumeric characters
- [ ] **Longest Substring Without Repeating Characters (LeetCode #3):** Dynamic sliding window with hash map
- [ ] **Longest Repeating Character Replacement (LeetCode #424):** Window size minus max frequency $\le k$
- [ ] **Minimum Window Substring (LeetCode #76):** Two-pointer sliding window with match counter
- [ ] **Group Anagrams (LeetCode #49):** Categorizing by sorted string or tuple frequency key
- [ ] **Valid Parentheses (LeetCode #20):** Matching brackets with stack verification
- [ ] **Longest Palindromic Substring (LeetCode #5):** Expand around center or Manacher's algorithm
- [ ] **Palindromic Substrings (LeetCode #647):** Count palindromic centers
- [ ] **String to Integer (atoi) (LeetCode #8):** Overflow detection and finite state simulation

---

> [!TIP]
> **Want to contribute a solution or add a new question to this topic?**  
> Check our standardized format and guidelines in the [How to Contribute & Question Template Guide](../contributing.md).

---

## 💡 Example: Valid Anagram (LeetCode #242)

### 1. Problem Statement
Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and `false` otherwise. An anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

### 2. Intuition & Approach
- If lengths differ, they cannot be anagrams.
- Since the inputs consist of lowercase English letters (`'a'` through `'z'`), an array of size 26 acts as a constant-space frequency table.
- Increment counts for each character in `s` and decrement for each in `t`. If all final counts are zero, `t` is an anagram of `s`.

### 3. Time & Space Complexity
- **Time Complexity:** $O(N)$ — single pass over both strings of length $N$.
- **Space Complexity:** $O(1)$ — constant array of size 26 regardless of string length.

### 4. Code Implementation

=== "Python"
    ```python
    class Solution:
        def isAnagram(self, s: str, t: str) -> bool:
            if len(s) != len(t):
                return False
            
            count = [0] * 26
            for char_s, char_t in zip(s, t):
                count[ord(char_s) - ord('a')] += 1
                count[ord(char_t) - ord('a')] -= 1
            
            return all(c == 0 for c in count)
    ```

=== "C++"
    ```cpp
    #include <string>
    #include <vector>

    class Solution {
    public:
        bool isAnagram(std::string s, std::string t) {
            if (s.length() != t.length()) return false;
            std::vector<int> count(26, 0);
            for (int i = 0; i < s.length(); ++i) {
                count[s[i] - 'a']++;
                count[t[i] - 'a']--;
            }
            for (int c : count) {
                if (c != 0) return false;
            }
            return true;
        }
    };
    ```

=== "Java"
    ```java
    class Solution {
        public boolean isAnagram(String s, String t) {
            if (s.length() != t.length()) return false;
            int[] count = new int[26];
            for (int i = 0; i < s.length(); i++) {
                count[s.charAt(i) - 'a']++;
                count[t.charAt(i) - 'a']--;
            }
            for (int c : count) {
                if (c != 0) return false;
            }
            return true;
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function isAnagram(s: string, t: string): bool {
        if (s.length !== t.length) return false;
        const count = new Array(26).fill(0);
        const codeA = 'a'.charCodeAt(0);
        for (let i = 0; i < s.length; i++) {
            count[s.charCodeAt(i) - codeA]++;
            count[t.charCodeAt(i) - codeA]--;
        }
        return count.every(c => c === 0);
    }
    ```
