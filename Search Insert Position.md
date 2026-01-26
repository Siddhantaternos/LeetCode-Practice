# 🔍 Search Insert Position 

## 📌 Problem

You are given a **sorted array** `nums` and an integer `target`.

Return:

* the **index** if `target` exists in the array
* otherwise, the **index where it should be inserted** to keep the array sorted

⚠️ Array has **no duplicates**.

---

## 🧠 Core Idea

This is a **Binary Search** problem.

Instead of linearly checking every element, we:

* repeatedly divide the search space in half
* decide which side to continue searching

If the element is **not found**, the position where search stops (`left`) is the correct insert index.

---

## 🔁 Algorithm Logic

1. Initialize two pointers:

   * `left` → start of array
   * `right` → end of array
2. While `left <= right`:

   * Calculate `mid`
   * If `nums[mid] == target` → return `mid`
   * If `nums[mid] < target` → search right half
   * If `nums[mid] > target` → search left half
3. If loop ends:

   * `left` points to the **correct insert position**
4. Return `left`

---

## 🧩 Python Code (Exact Code Used)

```python
from typing import List

class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums) - 1

        while left <= right:
            mid = (left + right) // 2

            if nums[mid] == target:
                return mid
            elif nums[mid] < target:
                left = mid + 1
            else:
                right = mid - 1

        # left is the correct insert position
        return left
```

---

## 🔍 Why Returning `left` Works

When the loop ends:

* `right` is just **before** where `target` should go
* `left` is the **first valid position** where `target` can be inserted

Binary search naturally converges to this index.

---

## 📘 Example

```
nums = [1,3,5,6]
target = 2

Binary search ends with:
left = 1

Output: 1
```

```
nums = [1,3,5,6]
target = 7

Binary search ends with:
left = 4

Output: 4
```

---

## ⏱️ Complexity

| Metric | Value        |
| ------ | ------------ |
| Time   | **O(log n)** |
| Space  | **O(1)**     |

---

## 🧠 Pattern / Memory Hook

```
Sorted array + find position → Binary Search
Not found? → return left
```

---

## 🎯 Interview Signal

If you can explain:

* why `left` is the answer
* how binary search narrows space
* why no extra checks are needed

You’re thinking like an interviewer expects.

---

