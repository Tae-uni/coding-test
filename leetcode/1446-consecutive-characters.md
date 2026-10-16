# 1446. Consecutive Characters
- Link: https://leetcode.com/problems/consecutive-characters/
- Difficulty: Easy / Type: Q2 array implementation
- Solved: 2026-10-16 🔁

```py
class Solution:
    def maxPower(self, s: str) -> int:
        # s is only lowercase, 1<= s.length
        # Basically, count the continuos number in s...
        count = 1
        longest = 1
        # Flag needed.. 
        for i in range(len(s) - 1):
            if s[i] == s[i+1]:
                count += 1
            else:
                count = 1
            longest = max(count, longest)
        return longest
```

## Another Way: Jump by Runs (same pattern as 228)
- Outer `while`: start a new run
- Inner `while`: move `i` to the last index of the run
- Length = `i - start + 1`, then `i += 1` to jump to the next run
- Still O(n): `i` only moves forward

```py
class Solution:
    def maxPower(self, s: str) -> int:
        longest = 0
        i = 0
        while i < len(s):
            start = i
            while i + 1 < len(s) and s[i] == s[i + 1]:
                i += 1
            longest = max(longest, i - start + 1)
            i += 1
        return longest
```

## Where I Got Stuck
- Tried a dict to store counts; only one number (the max) is needed
- In `else`, updated `longest` instead of resetting `count`
- Started `longest` at 0, so a 1-character string returned 0
- In the while version, stored `s[i]` (character) instead of `i` (index) for `start`
  - 228 stores the **value** (needed for output), 1446 stores the **index** (needed for length)

## When to Use Which
- **for + reset counter**: when you only need **one number** (e.g. max length). Simpler for this problem
- **Two whiles (jump by runs)**: when you need to **build something per run** (e.g. range strings like 228, compression `"aaabb"` → `"a3b2"`). Start and end of each run are clear