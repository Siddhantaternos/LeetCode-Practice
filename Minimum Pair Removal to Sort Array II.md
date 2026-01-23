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

class Solution:
    def minimumPairRemoval(self, nums: List[int]) -> int:
        stack = []
        operations = 0

        for num in nums:
            # Remove violating pairs
            while stack and stack[-1] > num:
                stack.pop()
                operations += 1

            stack.append(num)

        return operations
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

