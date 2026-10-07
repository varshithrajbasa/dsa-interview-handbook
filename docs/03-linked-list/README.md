[← Back to Main Index](../index.md)

# Linked List - Most Important Questions and Answers

## 📖 Topic Overview

Linked lists test your mastery of pointer manipulation, reference safety, memory indirection, and edge-case management (empty lists, single-node lists, and cycles).

### Core Algorithmic Patterns:
1. **Sentinel / Dummy Head Technique:** Eliminates special handling for the head node during deletions, insertions, and merges.
2. **Fast & Slow Pointers (Floyd’s Tortoise and Hare):**
   - Finding middle node in one pass ($O(N)$ time, $O(1)$ space).
   - Cycle detection and locating the cycle entrance node.
3. **In-Place Reversal:** Iteratively rewiring `next` pointers using `prev`, `curr`, and `next_temp` references without allocating new nodes.
4. **List Partitioning & Merging:** Splitting a list into halves for Merge Sort ($O(N \log N)$), interleaving, or unzipping.
5. **Complex Node Structures:** Doubly linked lists with hash maps (e.g., LRU Cache / LFU Cache design) to achieve $O(1)$ get and put operations.

---

## 🎯 High-Yield Problem Checklist

- [ ] **Reverse a Linked List (LeetCode #206):** In-place iterative and recursive pointer reversals
- [ ] **Detect Cycle in a Linked List (LeetCode #141):** Floyd’s cycle finding algorithm
- [ ] **Linked List Cycle II (LeetCode #142):** Finding the cycle entrance node mathematically
- [ ] **Merge Two Sorted Lists (LeetCode #21):** Dummy head pointer splicing
- [ ] **Merge K Sorted Lists (LeetCode #23):** Min-heap / divide-and-conquer merge
- [ ] **Remove Nth Node From End of List (LeetCode #19):** Two-pointer gap technique
- [ ] **Reorder List (LeetCode #143):** Find middle + reverse second half + interleave
- [ ] **Palindrome Linked List (LeetCode #234):** Half reversal comparison in $O(1)$ space
- [ ] **Intersection of Two Linked Lists (LeetCode #160):** Pointer realignment via circular traversal
- [ ] **Copy List with Random Pointer (LeetCode #138):** Interleaving cloned nodes or hash map clone
- [ ] **LRU Cache (LeetCode #146):** Hash map combined with doubly linked list

---

> [!TIP]
> **Want to contribute a solution or add a new question to this topic?**  
> Check our standardized format and guidelines in the [How to Contribute & Question Template Guide](../contributing.md).

---

## 💡 Example: Reverse Linked List (LeetCode #206)

### 1. Problem Statement
Given the `head` of a singly linked list, reverse the list, and return the reversed list.

### 2. Intuition & Approach
To reverse a singly linked list in-place, maintain three pointers:
1. `prev` initially pointing to `null`
2. `curr` initially pointing to `head`
3. In each iteration, save `next_temp = curr.next`, point `curr.next = prev`, shift `prev = curr`, and advance `curr = next_temp`.
When `curr` reaches `null`, `prev` points to the new head of the reversed list.

### 3. Time & Space Complexity
- **Time Complexity:** $O(N)$ — where $N$ is the number of nodes in the list.
- **Space Complexity:** $O(1)$ — constant space pointers.

### 4. Code Implementation

=== "Python"
    ```python
    from typing import Optional

    class ListNode:
        def __init__(self, val=0, next=None):
            self.val = val
            self.next = next

    class Solution:
        def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
            prev = None
            curr = head
            while curr:
                next_temp = curr.next
                curr.next = prev
                prev = curr
                curr = next_temp
            return prev
    ```

=== "C++"
    ```cpp
    struct ListNode {
        int val;
        ListNode *next;
        ListNode(int x) : val(x), next(nullptr) {}
    };

    class Solution {
    public:
        ListNode* reverseList(ListNode* head) {
            ListNode* prev = nullptr;
            ListNode* curr = head;
            while (curr != nullptr) {
                ListNode* next_temp = curr->next;
                curr->next = prev;
                prev = curr;
                curr = next_temp;
            }
            return prev;
        }
    };
    ```

=== "Java"
    ```java
    class ListNode {
        int val;
        ListNode next;
        ListNode(int x) { val = x; next = null; }
    }

    class Solution {
        public ListNode reverseList(ListNode head) {
            ListNode prev = null;
            ListNode curr = head;
            while (curr != null) {
                ListNode nextTemp = curr.next;
                curr.next = prev;
                prev = curr;
                curr = nextTemp;
            }
            return prev;
        }
    }
    ```

=== "TypeScript"
    ```typescript
    class ListNode {
        val: number;
        next: ListNode | null;
        constructor(val?: number, next?: ListNode | null) {
            this.val = (val === undefined ? 0 : val);
            this.next = (next === undefined ? null : next);
        }
    }

    function reverseList(head: ListNode | null): ListNode | null {
        let prev: ListNode | null = null;
        let curr: ListNode | null = head;
        while (curr !== null) {
            const nextTemp: ListNode | null = curr.next;
            curr.next = prev;
            prev = curr;
            curr = nextTemp;
        }
        return prev;
    }
    ```
