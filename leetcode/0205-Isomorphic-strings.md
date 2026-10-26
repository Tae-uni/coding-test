# 205. Isomorphic Strings
- Link: https://leetcode.com/problems/isomorphic-strings/
- Difficulty: Easy / Type: Q2 array implementation
- Solved: 2026-10-20 🔁 -> 2026-10-26 🔁

## Re-solve Log
### 2026-10-26
- Remembered the structure (`shape()` + compare), but not what to store
- Tried "seen → 1, new → 0" → fails on `"aba"` vs `"abb"` (both `[0, 0, 1]`)
- Store the **first-seen number**: `word[x] = len(word)` (not just `len(word)`)
- `append` goes **outside** the `if`, every time


```py
class Solution:
    def isIsomorphic(self, s: str, t: str) -> bool:
        # dict, count the pattern..
        def shape(phrase):
            word = {}
            result = []
            for x in phrase:
                if x not in word:
                    word[x] = len(word)
                result.append(word[x])
            return result
            
        return shape(s) == shape(t)
```

## Where I Got Stuck
- Thought counting repeats was enough, but **positions** matter (`"aab"` vs `"abb"` -> False)
- Mapping s → t with one dict misses `"ab"` vs `"aa"`; needs a second dict (t → s)
- Easier idea: convert each string to a **first-seen order pattern** and compare
  - `"egg"` → `[0, 1, 1]`, `"add"` → `[0, 1, 1]`
- Didn't know I could define a helper function inside the method makes it easier

## Approach
- Turn each string into a first-seen order pattern and compare
- `"egg"` -> `[0, 1, 1]`, `"add"` -> `[0, 1, 1]` -> `True`