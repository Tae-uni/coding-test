# 896. Monotonic Array
- Link: https://leetcode.com/problems/monotonic-array/
- Difficulty: Easy / Type: Q2 array implementation
- Solved: 2026-10-16 🔁

```py
class Solution:
    def isMonotonic(self, nums: list[int]) -> bool:
        inc = True
        dec = True

        for i in range(len(nums)-1):
            # The moment break inc
            if nums[i] > nums[i+1]:
                inc = False
            # The moment break dec
            if nums[i] < nums[i+1]:
                dec = False
        return inc or dec
```

## Where I Got Stuck
- Returned `True` too early; only `False` can be decided mid-loop
- Track two flags (`increasing`, `decreasing`) and turn them off when broken

## Approach
- Start with two flags: `inc = True`, `dec = True` (no empty array, since `1 <= nums.length`)
- Compare each pair `nums[i]`, `nums[i+1]`
  - If it goes down, it can't be increasing → `inc = False`
  - If it goes up, it can't be decreasing → `dec = False`
- Return `inc or dec` (equal values break neither flag)