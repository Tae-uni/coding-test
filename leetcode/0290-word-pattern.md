# 290. Word Pattern
- Link: https://leetcode.com/problems/word-pattern
- Difficulty: Easy / Type: Q2 array implementation
- Solved: 2026-10-22 🔁

```python
class Solution:
    def wordPattern(self, pattern: str, s: str) -> bool:
        def shape(seq):
            seen = {}
            result = []
            for item in seq:
                if item not in seen:
                    seen[item] = len(seen)
                result.append(seen[item])
            return result
            
        words = s.split()
        return shape(words) == shape(pattern)
```

## Where I Got Stuck
- Started from an empty loop instead of reusing 205
- Used `join()` instead of `split()`
- Forgot `return result` → returned `None`, so every case was `True`
- Confused `seen` (number for each item) with `result` (numbers in order)

## When to Use
- "Same structure?" / "One-to-one mapping?" → first-seen order pattern
- `len(seen)` works as an auto counter for new keys