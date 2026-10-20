# 205. Isomorphic Strings
- Link: https://leetcode.com/problems/isomorphic-strings/
- Difficulty: Easy / Type: Q2 array implementation
- Solved: 2026-10-20 🔁

```py
class Solution:
    def isIsomorphic(self, s: str, t: str) -> bool:
        # s와 t의 글자와 상관없이, 특정 인덱스의 값이 몇번씩 반복되는지.. 알아내면 된다
        def pattern(word):
            seen = {}
            result = []
            for ch in word:
                if ch not in seen:
                    seen[ch] = len(seen)
                result.append(seen[ch])
            return result
    
        return pattern(s) == pattern(t)
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