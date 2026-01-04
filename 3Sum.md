Here’s a **polished, minimal, GitHub-ready version** of your **3Sum notes**.
Same content, tighter language, cleaner structure, zero fluff. Paste directly into `3Sum.md`.

---

# 3Sum — Clean Notes (Interview Ready)

## 📌 Goal

Find **all unique triplets** in the array whose sum is **0**.
Duplicate triplets are **not allowed**.

---

## 🧠 Core Pattern

**Sort → Fix one element → Two pointers**

This is a **pattern problem**, not a math trick.

---

## 🔑 Why Sorting Is Required

* Enables **two-pointer technique**
* Makes **duplicates adjacent**
* Allows controlled pointer movement to adjust sum

---

## 🔁 Step-by-Step Strategy

### 1. Sort the array

Creates order and predictability.

---

### 2. Fix one element (`i`)

Treat `nums[i]` as the first number of the triplet.

---

### 3. Skip duplicates for `i`

If `nums[i] == nums[i - 1]`, skip to avoid repeated triplets.

---

### 4. Apply two pointers

* `left = i + 1`
* `right = last index`

---

### 5. Adjust pointers based on sum

| Condition | Action                          |
| --------- | ------------------------------- |
| `sum < 0` | Move `left` right               |
| `sum > 0` | Move `right` left               |
| `sum = 0` | Store triplet + skip duplicates |

---

### 6. Skip duplicates after a valid triplet

Move pointers until values change.

---

## 🧠 Python Code (LeetCode Style)

```python
from typing import List

class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        ans = []
        n = len(nums)

        for i in range(n - 2):
            if i > 0 and nums[i] == nums[i - 1]:
                continue

            left, right = i + 1, n - 1

            while left < right:
                total = nums[i] + nums[left] + nums[right]

                if total == 0:
                    ans.append([nums[i], nums[left], nums[right]])
                    left += 1
                    right -= 1

                    while left < right and nums[left] == nums[left - 1]:
                        left += 1
                    while left < right and nums[right] == nums[right + 1]:
                        right -= 1

                elif total < 0:
                    left += 1
                else:
                    right -= 1

        return ans
```

---

## ⏱️ Complexity

* **Time:** `O(n²)`
* **Space:** `O(1)` (excluding output)

---

## 🧠 Mental Model

* Sorting gives **direction**
* `left` → increases sum
* `right` → decreases sum
* Duplicates are skipped at **every level**

---

## 🎯 Interview Signal

* If you know **why pointers move**, you understand 3Sum
* If you memorize code, you don’t

---

## 🔗 Pattern Expansion

```
2Sum → Hash / Two pointers
3Sum → Fix one + Two pointers
4Sum → Fix two + Two pointers
```

Same logic. More control.

---

If you want next:

* **4Sum notes**
* **Common mistakes in 3Sum**
* **Dry run walkthrough**
* **How interviewers grill this problem**

Say the direction and we continue cleanly.
