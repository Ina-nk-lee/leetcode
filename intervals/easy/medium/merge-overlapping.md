## Merge Intervals
- Difficulty: medium
- [Link](https://neetcode.io/problems/merge-intervals/)

---

### Summary
- Given a list of non-overlapping `intervals` sorted by start time, insert `newInterval` into `intervals`, merging if necessary, and return the resulting list of non-overlapping `intervals` in sorted order.

---

### Ideas
- In order to maintain ascending order, we need to iterate `intervals` to the point where `newInterval` can be inserted.
- Then merge intervals if necessary.

---

### Solution
```python
class Solution:
    def insert(self, intervals: List[List[int]], newInterval: List[int]) -> List[List[int]]:
        res = []
        l = len(intervals)
        i = 0
        while i < l and intervals[i][1] < newInterval[0]:
            res.append(intervals[i])
            i += 1
        while i < l and intervals[i][0] <= newInterval[1]:
            newInterval[0] = min(intervals[i][0], newInterval[0])
            newInterval[1] = max(intervals[i][1], newInterval[1])
            i += 1
        res.append(newInterval)
        while i < l:
            res.append(intervals[i])
            i += 1
        return res
```
- The first while loop iterates `intervals` and adds intervals that are not overlapping with `newInterval` to `res`.
- The second while loop merges intervals with newInterval until there is no overlapping.
- The third while loop iterates the rest of `intervals` while adding them to `res`.
---

### Thoughts
- The time complexity is **`O(n)`** where `n` is the number of intervals in `intervals`.
- The space complexity is **`O(n)`** because `res` may store up to `O(n)` elements.
- To maintain a sorted array, iterating it and sequentially adding its elements to a return value could be efficient.
- A useful way to think about the problem is to divide intervals into three parts: intervals before `newInterval`, overlapping intervals, and intervals after `newInterval`.
