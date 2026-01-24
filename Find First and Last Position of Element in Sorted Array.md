# 📍 Find First and Last Position of Element in Sorted Array

## 📌 Problem Summary

Given a **sorted array** `nums` and a value `target`, find the **starting** and **ending** positions (indices) of `target` in the array.

* If `target` **doesn’t exist**, return `[-1, -1]`
* You must solve this in **O(log n)** time

### Examples

```
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]

Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]
```

---

## 🧠 Core Pattern

This is a **Binary Search** problem with a small twist:

You must find:

* the **first occurrence** of `target`
* the **last occurrence** of `target`

Instead of linear scanning, use **two modified binary searches**:

1. One to find the **leftmost index**
2. One to find the **rightmost index**

---

## 🔑 Why Two Searches?

Standard binary search stops when it finds `target`.
Here we need:

* the **earliest position**
* the **latest position**

Because the array is sorted, we can find them independently in `O(log n)` each.

---

## 🧠 Modified Binary Search (Leftmost / Rightmost)

### Leftmost (First Occurrence)

At each step:

* If `nums[mid] < target`: move `low = mid + 1`
* Else (equal or greater): move `high = mid − 1`
  Stop when you find first position that equals `target`.

### Rightmost (Last Occurrence)

At each step:

* If `nums[mid] <= target`: move `low = mid + 1`
* Else: move `high = mid − 1`
  Stop when you find last position that equals `target`.

---

## 🧠 Python Code (LeetCode Style)

```python
from typing import List

class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:
        def findLeft(nums, target):
            low, high = 0, len(nums) - 1
            idx = -1
            while low <= high:
                mid = (low + high) // 2
                if nums[mid] < target:
                    low = mid + 1
                else:
                    high = mid - 1
                if nums[mid] == target:
                    idx = mid
            return idx

        def findRight(nums, target):
            low, high = 0, len(nums) - 1
            idx = -1
            while low <= high:
                mid = (low + high) // 2
                if nums[mid] <= target:
                    low = mid + 1
                else:
                    high = mid - 1
                if nums[mid] == target:
                    idx = mid
            return idx

        return [findLeft(nums, target), findRight(nums, target)]
```

---

## ⏱️ Complexity

| Metric | Value      |
| ------ | ---------- |
| Time   | `O(log n)` |
| Space  | `O(1)`     |

---

## 🧠 Pattern / Memory Hook

```
2 × Modified Binary Search → Leftmost & Rightmost
```

---

## 🔍 Example Walkthrough

```
nums = [5, 7, 7, 8, 8, 10]
target = 8

Left search → first 8 at index 3
Right search → last 8 at index 4

Answer → [3, 4]
```

---

## 📌 Interview Signals

You *own* this question if you can explain:

1. Why one binary search is not enough
2. How the search direction changes for leftmost vs rightmost
3. Why the array being sorted is essential

This problem is a classic **Binary Search variant**, and mastering it unlocks many follow-ups like:

* First bad version
* Count occurrences
* Frequency queries

---

## 🧠 Variations

Related problems:

* Find First and Last Position of Element (this)
* Search Insert Position
* Find Peak Element
* Count Occurrences of Target
* K-Closest Elements (binary search + two pointers)

---
