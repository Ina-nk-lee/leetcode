## Two Sum

- Difficulty: Easy
- [Link](https://neetcode.io/problems/two-integer-sum?list=neetcode150)

---

### Summary

- Given the target integer, find two indices such that the values at those indices add up to the target.
- Assume that there is exactly one pair of indices that satisfy the condition.
- The smaller index should come first in the pair.

---

### Ideas

- We need to **keep track of values** to check whether the complement (`target - current value`) has already been seen.
- This requires **iterating through the given array**, which takes O(n) time.
- We also need a **data structure** to efficiently store values and their indices.
- Since there is **exactly one pair of indices** in the array, a **hash map that maps values to their indices** is suitable.
- Additionally, **lookup in a hash map takes O(1)** time on average.
- The hash map requires **O(n) space** in the worst case.

---

### Solution

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        seen = {}
        for i in range(len(nums)):
            diff = target - nums[i]
            if diff in seen:
                return [seen[diff], i]
            else:
                seen[nums[i]] = i
```

- While iterating, `seen` stores the value-index pairs from `nums`.
- For each number in `nums`, the loop checks if its complement (target minus the number) exists in `seen`.
- If it does, it returns the stored index from `seen` and the current index.
- If the complement doesn’t exist, it adds the current number and its index to `seen`.
- This is natural because a valid pair must consist of a number and its complement. By saving each number, we can check for its complement later.

---

### Thoughts

- The general idea came quickly, but the ending was a bit messy.
- I initially made a mistake by storing the wrong key in the hash map (saved the difference instead of the number itself).
- Fixing that helped reinforce the importance of understanding what to save (the number) and what to compare (the complement).
- Constant-time lookup in hash maps is very useful in scenarios that involve quick searching.