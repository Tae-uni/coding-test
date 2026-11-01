# 2022. Convert 1D Array Into 2D Array
- Link: https://leetcode.com/problems/convert-1d-array-into-2d-array
- Difficulty: Easy / Type: Q3 matrix
- Solved: 2026-11-01 🔁

## Approach
- If `len(original) != m * n` -> `[]` leftover are now allowed either.
- Cell `(r, c)` takes `original[r * n + c]`
  - Each row has `n` items, so skipping `r` rows = `r * n`

```py
class Solution:
    def construct2DArray(self, original: list[int], m: int, n: int) -> list[list[int]]:
        # check if... n * m is possible
        if len(original) != n * m:
            return []
            
        result = []
        for r in range(m):
            row = []
            for c in range(n):
                row.append(original[r * n + c])
            result.append(row)
        return result
```

## Where I Got Stuck
- Used `<` instead of `!=` (extra items also make it impossible)
- `original[c]` → every row repeated the first `n` items
- `original[r + c]` → skipped only 1 item per row, not `n`