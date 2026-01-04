# 1. Two Sum

## 📌 Problem

Given an array of integers `nums` and an integer `target`, return the **indices** of the two numbers such that they add up to `target`.

### Rules

* Each input has **exactly one solution**
* You **cannot use the same element twice**
* Order of indices does **not matter**

---

## 📊 Constraints

* `2 ≤ nums.length ≤ 10⁴`
* `-10⁹ ≤ nums[i] ≤ 10⁹`
* `-10⁹ ≤ target ≤ 10⁹`

**Follow-up:**
Can you solve it in less than `O(n²)` time?

---

## 💡 Approach (Brute Force)

### Idea

Check **all possible pairs** of numbers.
If the sum of a pair equals the target, return their indices.

---

## 🔁 How Pair Checking Works

We use **two nested loops**:

* First loop picks the first number
* Second loop picks the next number after it

```python
for i in range(0, n):       # first number
    for j in range(i + 1, n):  # second number
```

This avoids using the same element twice and avoids duplicate pairs.

---

## 🔢 Number of Pairs

For an array of `n` elements:

```
Number of pairs = n × (n − 1) / 2
```

**Example**

```
nums = [2, 10, 4, 6]
Pairs = 6

(2,10), (2,4), (2,6),
(10,4), (10,6),
(4,6)
```

---

## ⏱️ Time Complexity

* **Time:** `O(n²)`
* **Space:** `O(1)`

This solution is simple but inefficient for large inputs.

---

## 🧠 Python Code (LeetCode Style)

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums)):
            for j in range(i + 1, len(nums)):
                if nums[j] == target - nums[i]:
                    return [i, j]
        return []
```

---

## 🔗 LeetCode Problem Link

[https://leetcode.com/problems/two-sum](https://leetcode.com/problems/two-sum)

---

