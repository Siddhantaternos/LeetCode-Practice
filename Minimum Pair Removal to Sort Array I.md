# 📉 Minimum Pair Removal to Sort Array I 

## 📌 Problem Summary

Given an integer array `nums`, you may repeatedly perform the following operation:

* Select the **adjacent pair** with the **minimum sum** in `nums`.
  If multiple pairs have the same minimum sum, choose the **leftmost**.
* Replace that pair with their **sum** (i.e., merge them into a single value).

Return the **minimum number of such operations** needed to make `nums` **non-decreasing** (each element ≥ previous). ([Hello, World! System Design Newsletter][1])

---

## 💡 Core Logic

The process is **simulation-based**:

* While the array is **not non-decreasing**, repeatedly:

  * Find the adjacent pair with the **smallest sum**
  * Merge them (replace both with their sum)
  * Count one operation
* Stop once the array is non-decreasing.

This directly follows the problem rules and works because:

* Each merge reduces the array length by 1
* Eventually, the array must become non-decreasing
* Size is small (≤ 50), so simulation is efficient ([Hello, World! System Design Newsletter][1])

---

## 🧠 Example

```
nums = [5, 2, 3, 1]

- Adjacent sums: (5+2=7), (2+3=5), (3+1=4)
→ smallest: (3,1) → merge to 4
nums becomes [5,2,4]   operations = 1

Now: (5+2=7), (2+4=6)
→ smallest: (2,4) → merge to 6
nums becomes [5,6]   operations = 2

Now array is non-decreasing → STOP

Output: 2
```

---

## 🧠 Strategy (Simulation)

1. Initialize `operations = 0`
2. Loop until the array is non-decreasing

   * Find the **pair with minimum sum**
   * Replace the pair with their sum
   * Increment `operations`
3. Return `operations`

---

## 📈 Python Code (LeetCode Format)

```python
from typing import List

class Solution:
    def minimumPairRemoval(self, nums: List[int]) -> int:
        def is_non_decreasing(arr):
            # Check if array is in non-decreasing order
            return all(arr[i] <= arr[i + 1] for i in range(len(arr) - 1))

        operations = 0

        # Continue until nums is non-decreasing
        while not is_non_decreasing(nums):
            # Find leftmost adjacent pair with minimum sum
            min_sum = float('inf')
            index = 0
            for i in range(len(nums) - 1):
                current_sum = nums[i] + nums[i + 1]
                if current_sum < min_sum:
                    min_sum = current_sum
                    index = i

            # Merge the pair
            nums[index] = min_sum
            nums.pop(index + 1)
            operations += 1

        return operations
```

---

## ⏱️ Complexity

| Metric | Value     |
| ------ | --------- |
| Time   | **O(n²)** |
| Space  | **O(n)**  |

* Each while-loop iteration scans the array (O(n))
* In the worst-case, we make O(n) merges → overall O(n²) ([Hello, World! System Design Newsletter][1])

---

## 🔑 Pattern / Memory Hook

```
Repeatedly merge the smallest adjacent pair → stop when sorted
```

This is **direct simulation** — no advanced structures required.

---

## 🧠 Interview Insights

If you can explain:

* Why this simulation produces the **minimum number** of operations
* How the “leftmost smallest sum” rule is applied
* Why checking non-decreasing can be O(n)

then you **own this problem**.

---

