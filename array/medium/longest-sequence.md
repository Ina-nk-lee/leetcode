## Longest consecutive Integer Sequence

- Difficulty: Medium
- [Link](https://neetcode.io/problems/longest-consecutive-sequence/question)

---

### Summary

- Given an array of integers `nums`, return the length of the longest consecutive integer sequence.
---

### Ideas

- It's unavoidable to check all the elements in `nums`.

---

### Solution 1 (`O(n + r)`)

```python
class Solution:  
    def longestConsecutive(self, nums: List[int]) -> int:
        if not nums:
            return 0

        s = set()
        for num in nums:
            s.add(num)
        
        mx = 0
        curr = 0
        for i in range(min(nums), max(nums) + 1):
            if i in s:
                curr += 1
                if curr > mx:
                    mx = curr
            if i not in s:
                curr = 0
        
        return mx
```
- Iterates from the smallest number in `nums` to the biggest one.
- If a new longest consecutive sequence appears, `curr` replaces `mx`.

### Solution 2 (`O(n)`)

```python  
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        if not nums:
            return 0

        s = set()
        for num in nums:
            s.add(num)
        
        mx = 0
        for num in nums:
            n = num
            count = 0
            if n - 1 not in s:
                while n in s:
                    count += 1
                    n += 1
                if count > mx:
                    mx = count

        return mx
```
- A hashset, `s`, stores unique integer values of `nums` for efficiency.
- It iterates through `nums`, and start counting from where `num - 1` doesn't exist in `s`.
- `count` updates `mx` if `count` is bigger than `mx`.


### Thoughts

- For the **solution 1**, the time complexity is **`O(n + r)`** where `n` is the length of `nums` and `r` is `max(nums) - min(nums) + 1`. The space complexity is **`O(n)`** because of the hashset, `s`.
- Because `-10^9 <= nums[i] <= 10^9`, solution 1 could possibly be too inefficient compared to solution 2.
- For the **solution 2**, the time complexity is **`O(n)`** because a while loop starts traversing from the beginning of a consecutive sequence only and each number is counted only once. The space complexity is also **`O(n)`** for the hashset.
- For both solutions, **hashset lookup** only takes **`O(1)`**.
- Need to track the start of a consecutive sequence efficiently.
