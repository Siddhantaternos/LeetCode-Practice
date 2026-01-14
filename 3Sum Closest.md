Here are **clean, GitHub-ready notes** for **LeetCode: 3Sum Closest**.
Minimal, structured, interview-useful — just like your other problem notes.

---

# 📐 3Sum Closest — Notes

## 🚩 Problem Summary

Given an integer array `nums` and a target value `target`, find the **sum of three integers in `nums`** such that the sum is **closest** to `target`.

Return the **closest possible sum**.

---

## 🧠 Core Pattern

**Sort + Fix one element + Two pointers**

This is a variation of classical 3-sum pattern — but instead of collecting all triplets with sum zero, we want the triplet whose sum is closest to the given `target`.

---

## 🧩 Why Sorting Helps

* Makes two pointers usable
* Allows controlled pointer movement
* Ensures we evaluate all combinations efficiently

---

## 🔍 Key Strategy

1. **Sort the array**
2. Iterate through possible first elements (`i`)
3. Use **two pointers** (`left`, `right`)
4. Move pointers to approach the desired target
5. Track the **closest sum found so far**

---

## ✏️ Algorithm

```
sort nums

closest_sum = large value

for i in [0 .. n−3]:
    left  = i + 1
    right = n − 1

    while left < right:
        current = nums[i] + nums[left] + nums[right]

        if abs(current − target) < abs(closest_sum − target):
            closest_sum = current

        if current < target:
            left += 1
        else:
            right −= 1

return closest_sum
```

---

## 🧠 Trick Insight

* If the current sum is less than target, we need a bigger sum → move `left` right
* If greater than target, we need a smaller sum → move `right` left
* Always update **closest_sum** when we find a better approximation

---

## 📌 Python Code (LeetCode Format)

```python
from typing import List

class Solution:
    def threeSumClosest(self, nums: List[int], target: int) -> int:
        nums.sort()
        n = len(nums)
        closest_sum = nums[0] + nums[1] + nums[2]

        for i in range(n - 2):
            left, right = i + 1, n - 1
            while left < right:
                current = nums[i] + nums[left] + nums[right]

                if abs(current - target) < abs(closest_sum - target):
                    closest_sum = current

                if current < target:
                    left += 1
                else:
                    right -= 1

        return closest_sum
```

---

## 🧠 Complexity

| Metric | Value     |
| ------ | --------- |
| Time   | **O(n²)** |
| Space  | **O(1)**  |

---

## 🧠 Mental Model

* Sorting lets you use two pointers
* Fix one value, then try all combinations with remaining two
* Move pointers based on how current sum compares to target

---

## 📌 Interview Signals

If you can explain:

* why sorting is needed
* how pointer movement improves efficiency
* how we track and update the closest sum

you clearly understand the pattern.

---

## 💡 Related Patterns

| Problem      | Pattern                   |            |   |
| ------------ | ------------------------- | ---------- | - |
| 3Sum         | Fix one + two pointers    |            |   |
| 3Sum Closest | Same pattern but minimize | difference |   |
| 4Sum         | Fix two + two pointers    |            |   |

---

If you want:

* ASCII diagrams of pointer movement
* Comparative notes with `3Sum` / `2Sum Closest`
* A **step-by-step dry run example**
  just ask!
