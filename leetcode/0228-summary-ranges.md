# 228. Summary Ranges
- Link: https://leetcode.com/problems/summary-ranges/
- Difficulty: Easy / Type: Q2 array implementation
- Solved: 2026-10-15 🔁

```py
class Solution:
    def summaryRanges(self, nums: list[int]) -> list[str]:
        if not nums:
            return []
        
        result = []
        start = nums[0]
        for i in range(len(nums)):
            if i == len(nums) - 1 or nums[i] + 1 != nums[i+1]:
                if start == nums[i]:
                    result.append(f"{nums[i]}")
                else:
                    result.append(f"{start}->{nums[i]}")
                if i + 1 < len(nums):
                    start = nums[i+1]
        return result
```

## Where I got stuck
- Got a **Runtime Error** on empty input → added `if not nums: return []`
- Tried to handle the "consecutive" case, but the key is to act only when the sequence **breaks**
- Didn't track where the current range **starts** (`start` variable)
- Forgot to update `start` after closing a range

## Approach
- Keep `start` for the current range
- Close the range when it's the last element or the next number isn't `nums[i] + 1`
- Add `"a"` if start == end, otherwise `"a->b"`