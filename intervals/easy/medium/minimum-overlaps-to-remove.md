## The Minimum Number of Overlapping Intervals
- Difficulty: medium
- [Link](https://neetcode.io/problems/non-overlapping-intervals/question)

---

### Summary
- Given `intervals`, an array of intervals, return the minimum number of intervals that needs to be removed to make `intervals` non-overlapping. Intervals are non-overlapping even if they have a common point.

---

### Ideas
- We could sort the array to simplify the problem to compare only the end of intervals.
- By locally comparing two intervals at a time and storing the interval with the earlier end time, we could remove the minimum number of intervals.
---

### Solution
```python
class Solution:
    def eraseOverlapIntervals(self, intervals: List[List[int]]) -> int:
        intervals.sort(key = lambda x : x[0])
        end = intervals[0][1]
        res = 0
        i = 1
        while i < len(intervals):
            if intervals[i][0] >= end:
                end = intervals[i][1]
            else:
                res += 1
                end = min(end, intervals[i][1])
            i += 1
        return res
```
- It sorts `intervals` by start time.
- It iterates through `intervals` and updates `end`, which stores the end time of the interval we decided to keep.
- If the current interval overlaps, it increments `res` and keeps the interval with the earlier end time.
- If not, it updates `end` to the current interval.

---

### Thoughts
- The time complexity is **`O(nlogn)`** where `n` is the number of intervals in `intervals` because the python default sorting algorithm takes `O(nlogn)`.
- The extra space complexity is **`O(1)`** if we ignore the space used by sorting, since the algorithm only uses a few variables.
- A greedy algorithm works here by **always keeping the interval with the smaller end time** when an overlap occurs.
- **Sorting** is helpful because once intervals are ordered by start time, we **only need to check each interval against the previously kept one**.
- Keeping the interval with the earlier end time **leaves more room** for future intervals, which is why the greedy choice is optimal.
