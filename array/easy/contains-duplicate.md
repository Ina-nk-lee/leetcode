## Contains Duplicate

- Difficulty: Easy
- [Link](https://neetcode.io/problems/duplicate-integer?list=neetcode150)

---

### Summary

- Given an integer array `nums`, return `True` if any value appears more than once.
- Otherwise, return `False`.

---

### Ideas

- We need to **keep track of values** to check whether they've appeared before.
- This requires **iterating through the array**, which takes O(n) time.
- We also need a **data structure** to efficiently remember which values we've seen.
- Since **element order doesn't matter**, a **hash set** is a suitable choice.
- The **uniqueness constraint** of sets prevents duplicates by design.
- Additionally, **lookup in a set takes O(1)** time on average.
- The hash set requires **O(n) space** in the worst case.

---

### Solution

```python
class Solution:
    def hasDuplicate(self, nums: List[int]) -> bool:
        saved = set()
        for num in nums:
            if num in saved:
                return True
            saved.add(num)
        return False
```

- `saved` stores the values we've seen so far.
- For each number in `nums`, the loop checks if it already exists in `saved`.

---

### Thoughts

- This was a fairly easy and familiar problem, but it was still helpful to revisit Python’s **hash-based set syntax**.
- The constant-time lookup and **duplicate prevention** in sets are useful features.
- This pattern might be helpful in more complex cases where **duplicate detection** is needed.
