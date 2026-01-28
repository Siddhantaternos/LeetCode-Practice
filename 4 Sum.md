# 📦 4 Sum 

## Problem Summary

Given an integer array `nums` and an integer `target`, return **all unique quadruplets** `[a, b, c, d]` such that:

```
a + b + c + d == target
```

You must avoid duplicate quadruplets and return the result in any order.

---

## Core Idea

**Sort + Fix two elements + Two pointers**

This is a natural extension of:

* 2Sum → hashing / two pointers
* 3Sum → fix one + two pointers
* 4Sum → fix two + two pointers

Sorting enables consistency and duplicate handling.

---

## Algorithm (Step-by-Step)

1. **Sort** the array.
2. Loop `i` from `0` to `n − 4`.

   * Skip duplicates for `nums[i]`.
3. Loop `j` from `i + 1` to `n − 3`.

   * Skip duplicates for `nums[j]`.
4. Use **two pointers** (`left`, `right`) between `j + 1` and end.
5. Compute sum:

   * If sum == target:

     * Add quadruplet to result
     * Skip duplicates
     * Move both pointers
   * If sum < target → move `left` right
   * If sum > target → move `right` left
6. Return all unique quadruplets.

---

## Python Code (LeetCode Format)

```python
from typing import List

class Solution:
    def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        nums.sort()
        n = len(nums)
        result = []

        for i in range(n - 3):
            if i > 0 and nums[i] == nums[i - 1]:
                continue

            for j in range(i + 1, n - 2):
                if j > i + 1 and nums[j] == nums[j - 1]:
                    continue

                left = j + 1
                right = n - 1

                while left < right:
                    total = nums[i] + nums[j] + nums[left] + nums[right]

                    if total == target:
                        result.append([nums[i], nums[j], nums[left], nums[right]])
                        left += 1
                        right -= 1

                        while left < right and nums[left] == nums[left - 1]:
                            left += 1
                        while left < right and nums[right] == nums[right + 1]:
                            right -= 1

                    elif total < target:
                        left += 1
                    else:
                        right -= 1

        return result
```

---

## Complexity

| Metric | Value                       |
| ------ | --------------------------- |
| Time   | **O(n³)**                   |
| Space  | **O(1)** (excluding output) |

---

## Mental Model

* Sorting simplifies duplicate handling.
* The outer two loops **fix two values**.
* Two pointers scan the remainder for the complementary pair.
* This avoids brute force `O(n⁴)`.

Essentially:

```
Fix i
  Fix j
    Two pointers → find pairs
```

---

## Why This Works

Sorting + structured pointers ensures:

* We explore combinations in a **systematic order**
* We skip duplicates cleanly
* We prune unnecessary comparisons by moving pointers based on sum

---

## Interview Signals

If you can explain:

* Why sorting is needed
* Why duplicates are skipped at each level
* Why two pointers work after fixing two values

Then you truly understand the pattern.

---

## Related Problem Family

| Problem  | Pattern                    |
| -------- | -------------------------- |
| 2Sum     | Hash / two pointers        |
| 3Sum     | Fix one + two pointers     |
| **4Sum** | Fix two + two pointers     |
| kSum     | Recursion / generalization |

Extension:

* kSum recursion
* Target variation problems

---
