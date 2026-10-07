[← Back to Main Index](../index.md)

# Stacks and Queues - Most Important Questions and Answers

## 📖 Topic Overview

Stacks (Last-In-First-Out, LIFO) and Queues (First-In-First-Out, FIFO) are foundational linear structures with distinct access paradigms. They are pivotal for parsing nested expressions, managing recursive lifecycles iteratively, and maintaining sliding window extrema.

### Core Algorithmic Patterns:
1. **Parentheses Matching & Grammar Parsing:** Using a stack to pair opening and closing tokens, or evaluating arithmetic expressions in Reverse Polish Notation (RPN).
2. **Monotonic Stack (Decreasing / Increasing):**
   - Essential for finding the *Next Greater Element* or *Previous Smaller Element* in $O(N)$ linear time instead of $O(N^2)$.
   - Each element is pushed and popped at most once.
3. **Largest Rectangle / Histogram Problems:** Utilizing monotonic stacks to find left and right span boundaries for each bar.
4. **Monotonic Deque (Double-Ended Queue):** Maintaining elements in monotonic order while evicting expired indices from the front (e.g., Sliding Window Maximum in $O(N)$).
5. **Two-Stack Queue / Two-Queue Stack Simulation:** Amortized $O(1)$ push/pop implementations.

---

## 🎯 High-Yield Problem Checklist

- [ ] **Valid Parentheses (LeetCode #20):** LIFO bracket matching with stack
- [ ] **Min Stack (LeetCode #155):** Dual stack or pair encoding for $O(1)$ minimum retrieval
- [ ] **Evaluate Reverse Polish Notation (LeetCode #150):** Operand stack evaluation
- [ ] **Daily Temperatures (LeetCode #739):** Monotonic decreasing stack tracking indices
- [ ] **Next Greater Element I (LeetCode #496):** Monotonic stack precomputation mapped via hash table
- [ ] **Largest Rectangle in Histogram (LeetCode #84):** Boundary expansion with monotonic increasing stack
- [ ] **Implement Queue using Stacks (LeetCode #232):** In-stack and out-stack amortized $O(1)$ operations
- [ ] **Implement Stack using Queues (LeetCode #225):** Single or dual queue rotations
- [ ] **Sliding Window Maximum (LeetCode #239):** Monotonic decreasing deque
- [ ] **Basic Calculator II (LeetCode #227):** Operator precedence evaluation via stack

---

> [!TIP]
> **Want to contribute a solution or add a new question to this topic?**  
> Check our standardized format and guidelines in the [How to Contribute & Question Template Guide](../contributing.md).

---

## 💡 Example: Valid Parentheses (LeetCode #20)

### 1. Problem Statement
Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.
An input string is valid if:
1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

### 2. Intuition & Approach
- Whenever an opening bracket is seen, push it onto the stack (or push its corresponding expected closing bracket).
- When a closing bracket appears, check if the stack is non-empty and whether the top matches.
- If a mismatch occurs or the stack is empty upon encountering a closing bracket, return `false`.
- At the end, the stack must be empty for the string to be valid.

### 3. Time & Space Complexity
- **Time Complexity:** $O(N)$ — single pass over the string of length $N$.
- **Space Complexity:** $O(N)$ — worst-case all opening brackets stored on the stack.

### 4. Code Implementation

=== "Python"
    ```python
    class Solution:
        def isValid(self, s: str) -> bool:
            bracket_map = {')': '(', '}': '{', ']': '['}
            stack = []
            
            for char in s:
                if char in bracket_map:
                    top = stack.pop() if stack else '#'
                    if bracket_map[char] != top:
                        return False
                else:
                    stack.append(char)
                    
            return len(stack) == 0
    ```

=== "C++"
    ```cpp
    #include <string>
    #include <stack>
    #include <unordered_map>

    class Solution {
    public:
        bool isValid(std::string s) {
            std::stack<char> st;
            std::unordered_map<char, char> map = {
                {')', '('},
                {'}', '{'},
                {']', '['}
            };
            
            for (char c : s) {
                if (map.count(c)) {
                    if (st.empty() || st.top() != map[c]) {
                        return false;
                    }
                    st.pop();
                } else {
                    st.push(c);
                }
            }
            return st.empty();
        }
    };
    ```

=== "Java"
    ```java
    import java.util.Stack;
    import java.util.Map;
    import java.util.HashMap;

    class Solution {
        public boolean isValid(String s) {
            Stack<Character> stack = new Stack<>();
            Map<Character, Character> map = new HashMap<>();
            map.put(')', '(');
            map.put('}', '{');
            map.put(']', '[');

            for (char c : s.toCharArray()) {
                if (map.containsKey(c)) {
                    if (stack.isEmpty() || stack.pop() != map.get(c)) {
                        return false;
                    }
                } else {
                    stack.push(c);
                }
            }
            return stack.isEmpty();
        }
    }
    ```

=== "TypeScript"
    ```typescript
    function isValid(s: string): boolean {
        const stack: string[] = [];
        const map: Record<string, string> = {
            ')': '(',
            '}': '{',
            ']': '['
        };

        for (const char of s) {
            if (char in map) {
                if (stack.length === 0 || stack.pop() !== map[char]) {
                    return false;
                }
            } else {
                stack.push(char);
            }
        }

        return stack.length === 0;
    }
    ```
