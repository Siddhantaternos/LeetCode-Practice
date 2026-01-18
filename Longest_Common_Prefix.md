# 14. Longest Common Prefix

## 🎯 Problem Statement

Given an array of strings, find the **longest prefix shared by all strings**.
If no common prefix exists, return an empty string `""`.

---

## 🧠 Key Insight (Why Sorting Works)

Sorting strings places the **most different strings at the extremes**.

If the **first** and **last** strings (after sorting) share a prefix,
then **every string in between must also share it**.

➡️ Result:
We only compare **two strings instead of all**.

---

## 🛠️ Approach Breakdown

```
Strings → Sort → Compare first & last → Build prefix → Stop on mismatch
```

### Step-by-step

1. Sort the array of strings
2. Take the first and last strings
3. Compare characters index by index
4. Stop when characters differ
5. Return the prefix collected so far

---

## 🧪 Example Walkthrough

| Step     | Value                          |
| -------- | ------------------------------ |
| Input    | `["flower", "flow", "flight"]` |
| Sorted   | `["flight", "flow", "flower"]` |
| Compared | `"flight"` vs `"flower"`       |
| Result   | `"fl"`                         |

---

## 🧩 Python Solution (LeetCode Compatible)

```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        if not strs:
            return ""

        strs.sort()
        first, last = strs[0], strs[-1]
        prefix = ""

        for i in range(min(len(first), len(last))):
            if first[i] != last[i]:
                break
            prefix += first[i]

        return prefix
```

---

## 🔎 Important Notes

| Line                | Purpose                               |
| ------------------- | ------------------------------------- |
| `strs.sort()`       | Brings most different strings to ends |
| `strs[0], strs[-1]` | Only these two determine the prefix   |
| `min(len(...))`     | Prevents index overflow               |
| `break` on mismatch | Prefix ends immediately               |

---

## ⏱️ Complexity Analysis

| Metric | Value                            |
| ------ | -------------------------------- |
| Time   | `O(n log n)` (sorting dominates) |
| Space  | `O(1)` extra space               |

---

## 🧠 Memory Trick

> **Sort → Compare Ends → Stop Early**

If you understand *why* sorting reduces comparisons, you understand the problem.

---
