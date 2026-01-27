# 📋 Valid Sudoku 

## 📌 Problem Summary

Determine whether a given 9x9 Sudoku board is valid.

### Rules of Validity

1. Each **row** must contain digits `1–9` **without repetition**.
2. Each **column** must contain digits `1–9` **without repetition**.
3. Each **3x3 sub-box** must contain digits `1–9` **without repetition**.
4. Empty cells are filled with `'.'` and should be ignored.

> The board does **not** need to be solvable — only the current state must be checked for validity.

---

## 🧠 Core Idea

To check validity, we must ensure **no duplicates** in:

* Each row
* Each column
* Each 3×3 sub-grid

We track seen digits separately for:

* rows
* columns
* boxes

Use hashing structures (e.g., Python sets) for **fast existence checks**.

---

## 🚀 Key Observations

* When checking a cell:

  * If the number has already been seen in the same row → invalid
  * If already seen in the same column → invalid
  * If already seen in the same 3×3 box → invalid

* Use **unique keys** to identify group membership:

  * Row:   `(row, num)`
  * Col:   `(num, col)`
  * Box:   `((row // 3, col // 3), num)`

This ensures no overlap between categories.

---

## 🛠️ Python Code (LeetCode Style)

```python
from typing import List

class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        seen = set()

        for r in range(9):
            for c in range(9):
                num = board[r][c]
                if num == ".":
                    continue

                # Keys for row, column, and box
                row_key = (r, num)
                col_key = (num, c)
                box_key = (r // 3, c // 3, num)

                # If any key is already seen → invalid
                if row_key in seen or col_key in seen or box_key in seen:
                    return False

                # Mark keys as seen
                seen.add(row_key)
                seen.add(col_key)
                seen.add(box_key)

        return True
```

---

## ⏱️ Complexity

| Metric | Value                                      |
| ------ | ------------------------------------------ |
| Time   | **O(81)** → constant (board size is fixed) |
| Space  | **O(81)** → sets of seen values            |

For a general ( n \times n ) Sudoku variant:

* Time → ( O(n^2) )
* Space → ( O(n^2) )

---

## 🧠 Mental Model

* Think of this as **three simultaneous rule checks**:

  * Row rules
  * Column rules
  * Box rules

* Each number’s existence is tracked using uniquely identifiable tags.

---

## 🧩 How the Keys Work

| Type | Example                 |
| ---- | ----------------------- |
| Row  | `(r, num)`              |
| Col  | `(num, c)`              |
| Box  | `(r // 3, c // 3, num)` |

For a cell at `(r,c)` with `'5'`:

* Row key → `(2, '5')`
* Col key → `('5', 7)`
* Box key → `(0, 1, '5')` → first box row, second box col, number

---

## 🚨 Interview Insight

If you can clearly explain:

* how you detect duplicates
* why rows, columns, and boxes must be tracked separately
* why sets enable fast lookups

then you’ve *explained the heart of this problem*.

---

## 🧠 Visual Summary

```
Rows:      Box groups:        Columns:
0 1 2      0 1 2              0 3 6
3 4 5      3 4 5              1 4 7
6 7 8      6 7 8              2 5 8
```

Each 3×3 box is uniquely indexed via:

```
(box_row, box_col) = (r//3, c//3)
```

---

