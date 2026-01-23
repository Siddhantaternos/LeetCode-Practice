# 🧩 Minimum Pair Removal to Sort Array II

## 📌 Problem Summary

You are given an array `nums`.

You can **remove adjacent pairs** `(nums[i], nums[i+1])` **only if**:

```
nums[i] > nums[i+1]
```

Each removal deletes **both elements**.

Your goal is to make the remaining array **non-decreasing**
(using the **minimum number of such removals**).

Return the **minimum number of operations** needed.

---

## 🧠 Key Insight (This Is NOT Greedy)

At first glance, it looks greedy:

> “Just remove every decreasing pair.”

That’s **wrong**.

Why?
Because removing one pair can **change future adjacencies** and create or eliminate new violations.

This is a **stack + simulation problem**, not brute force.

---

## 🧠 Core Idea

We want to **simulate the removals optimally**.

Think in reverse:

* Instead of removing bad pairs directly
* We **build the longest valid non-decreasing sequence**
* Any element that **breaks the order** forces removals

This becomes a **monotonic stack problem**.

---

## 🧱 Strategy (Stack-Based Thinking)

We iterate through the array and maintain a stack that is:

```
non-decreasing
```

When a violation occurs:

```
stack top > current element
```

We must **remove a pair**, which means:

* Pop from the stack
* Count one operation
* Try again (because new adjacency might still violate)

---

## 🔁 Step-by-Step Algorithm

1. Initialize:

   * empty stack
   * `operations = 0`

2. Traverse elements in `nums`

3. While stack is not empty AND `stack[-1] > current`:

   * Pop stack top
   * Increment `operations`

4. Push current element to stack

5. Return `operations`

---

## 🧠 Why This Works

Each pop corresponds to **removing a bad adjacent pair**.

The stack ensures:

* We only remove when **forced**
* Each element is pushed and popped **once**

This guarantees **minimum operations**.

---

## 🧪 Example Walkthrough

```
nums = [3, 1, 2]

stack = []
push 3 → [3]

current = 1
3 > 1 → pop 3 → operations = 1
push 1 → [1]

current = 2
1 ≤ 2 → push → [1,2]

Answer = 1
```

---

## 🧠 Python Code (LeetCode Style)

```python
from typing import List
import heapq

class Node:
    def __init__(self, value, idx):
        self.value = value
        self.idx = idx
        self.prev = None
        self.next = None
        self.removed = False

class Solution:
    def minimumPairRemoval(self, nums: List[int]) -> int:
        n = len(nums)
        
        if n <= 1:
            return 0
        
        # Create doubly linked nodes
        nodes = [Node(val, i) for i, val in enumerate(nums)]
        for i in range(n-1):
            nodes[i].next = nodes[i+1]
            nodes[i+1].prev = nodes[i]
        
        # Min-heap storing (sum, original index, left_node)
        heap = []
        for i in range(n-1):
            heapq.heappush(heap, (nums[i] + nums[i+1], i, nodes[i]))
        
        ops = 0
        
        # Track how many nodes are out of order
        def is_decreasing_pair(a, b):
            return a.value > b.value
        
        # Count initial inversions
        inv = 0
        cur = nodes[0]
        while cur.next:
            if is_decreasing_pair(cur, cur.next):
                inv += 1
            cur = cur.next
        
        # Perform merges until sorted
        while inv > 0:
            # Pop the minimum sum pair
            while True:
                s, i, left_node = heapq.heappop(heap)
                if not left_node.removed and left_node.next and not left_node.next.removed:
                    break

            right_node = left_node.next
            
            ops += 1

            # Adjust inversion count locally
            if left_node.prev and is_decreasing_pair(left_node.prev, left_node):
                inv -= 1
            if is_decreasing_pair(left_node, right_node):
                inv -= 1
            if right_node.next and is_decreasing_pair(right_node, right_node.next):
                inv -= 1

            # Merge
            left_node.value += right_node.value
            right_node.removed = True
            
            # Remove right_node from linked list
            left_node.next = right_node.next
            if right_node.next:
                right_node.next.prev = left_node

            # Re-count inversions after merge
            if left_node.prev and is_decreasing_pair(left_node.prev, left_node):
                inv += 1
            if left_node.next and is_decreasing_pair(left_node, left_node.next):
                inv += 1

            # Add new pairs around left_node
            if left_node.next:
                heapq.heappush(heap, (left_node.value + left_node.next.value, left_node.idx, left_node))
            if left_node.prev:
                heapq.heappush(heap, (left_node.prev.value + left_node.value, left_node.prev.idx, left_node.prev))
        
        return ops
```

---

## ⏱️ Complexity Analysis

| Metric    | Value  |
| --------- | ------ |
| **Time**  | `O(n)` |
| **Space** | `O(n)` |

Each element enters and exits the stack **at most once**.

---

## 🧠 Mental Model (Important)

```
Bad order?
→ Remove the left element
→ Recheck
→ Continue until valid
```

This is **controlled destruction**, not greedy deletion.

---

## 🚨 Common Mistakes

❌ Removing all decreasing pairs in one pass
❌ Restarting scans after every deletion
❌ Using nested loops (TLE risk)

---

## 🧠 Pattern Recognition

This problem belongs to:

* Monotonic Stack
* Greedy with constraints
* Array stabilization problems

Related patterns:

* Remove K digits
* Make array non-decreasing
* Stack-based sequence correction

---

## 📌 Interview Takeaway

If you can explain:

* **Why stack is needed**
* **Why popping represents a valid operation**
* **Why this minimizes removals**

You’re thinking like a systems problem-solver, not a memorizer.

---

