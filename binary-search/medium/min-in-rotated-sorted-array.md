## Find Minimum in Rotated Sorted Array

- Difficulty: Medium
- [Link](https://neetcode.io/problems/find-minimum-in-rotated-sorted-array/question?list=blind75)

---

### Summary

- Given an array `nums` that is sorted in an ascending order with unique numbers and rotated `1` to `n` times, find the minimum number from the array.
- The time complexity must be `O(logn)`.

---

### Ideas

- First, in order to follow the time complexity limit, **`O(logn)`**, binary search is necessary.
- Need to find where the sudden gap from the highest to the lowest is.

---

### Solution

```python
class Solution:
    def findMin(self, nums: List[int]) -> int:
        l = 0
        r = len(nums) - 1
        while l <= r:
            mid = (l + r) // 2
            if nums[mid] > nums[r]:
                l = mid + 1
            elif nums[l] > nums[mid]:
                r = mid
            else:
                return nums[l]
        return -1
```
- Initialize `l = 0`, `r = len(nums) - 1`.
- While `l <= r`, it finds the sudden gap if the left or the right part contains it.
- If the left half has it, the minimum is in the left, so it updates `r` with `mid`.
- If the right half has it, the minimum is in the right, so it updates `l` with `mid`.
- If there's no gap in both parts, return `nums[l]`.
- Once there are only two numbers in the window, return the smaller value.`
---

### Thoughts

- The time complexity is **`O(logn)`** where `n = len(nums)` because the search window is halved each step.
- The space complexity is **`O(1)`**.
- Binary search works here because the array is sorted except for one rotation pivot, so one side of the window is always "properly sorted".