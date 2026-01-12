# 📊 Median of Two Sorted Arrays — Notes

## Problem Summary

Given two **sorted arrays** `nums1` and `nums2`, find the **median** of the combined dataset.

* Arrays may have different sizes
* Total time complexity must be **better than O(m + n)**
* Median may be an integer or float

---

## Key Insight

We **do not merge** the arrays.

Instead, we:

* Use **binary search**
* Partition both arrays so that:

  * Left half contains smaller elements
  * Right half contains larger elements
* Median lies at the boundary

---

## Core Pattern

**Binary Search on Partition**

This is not a typical binary search on values,
but on **cut positions**.

---

## Why Binary Search Works Here

* Arrays are already sorted
* Median depends on **relative order**, not full merge
* We only need to find the **correct split point**

Always binary search on the **smaller array** to reduce complexity.

---

## Partition Logic

Let:

* `cut1` = elements taken from `nums1`
* `cut2` = elements taken from `nums2`

Total left elements:

```
cut1 + cut2 = (m + n + 1) // 2
```

This ensures:

* Left side has either equal elements (even case)
* Or one extra element (odd case)

---

## Valid Partition Condition

A partition is correct when:

```
left1 <= right2  AND  left2 <= right1
```

Where:

* `left1`  = max element on left of nums1
* `right1` = min element on right of nums1
* Same for nums2

---

## Handling Edge Cases

* If cut is at boundary:

  * Use `-∞` for left
  * Use `+∞` for right
* This avoids index errors and simplifies logic

---

## Median Calculation

### If total length is even:

```
median = (max(left1, left2) + min(right1, right2)) / 2
```

### If total length is odd:

```
median = max(left1, left2)
```

---

## Code (LeetCode Format)

```python
from typing import List

class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        if len(nums1) > len(nums2):
            nums1, nums2 = nums2, nums1

        m, n = len(nums1), len(nums2)
        low, high = 0, m

        while low <= high:
            cut1 = (low + high) // 2
            cut2 = (m + n + 1) // 2 - cut1

            left1 = float('-inf') if cut1 == 0 else nums1[cut1 - 1]
            right1 = float('inf') if cut1 == m else nums1[cut1]

            left2 = float('-inf') if cut2 == 0 else nums2[cut2 - 1]
            right2 = float('inf') if cut2 == n else nums2[cut2]

            if left1 <= right2 and left2 <= right1:
                if (m + n) % 2 == 0:
                    return (max(left1, left2) + min(right1, right2)) / 2
                else:
                    return max(left1, left2)
            elif left1 > right2:
                high = cut1 - 1
            else:
                low = cut1 + 1
```

---

## Complexity

| Metric | Value               |
| ------ | ------------------- |
| Time   | `O(log(min(m, n)))` |
| Space  | `O(1)`              |

---

## Mental Model (Important)

* Binary search decides **how many elements go left**
* Correct partition guarantees median at boundary
* No merging, no extra memory

---

## Interview Signal

If you can explain:

* why we search smaller array
* what partitions represent
* why `±∞` is used

You **own** this problem.

---

## Pattern Extension

* kth element in two sorted arrays
* percentile queries
* streaming median logic

