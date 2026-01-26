## Booking meeting rooms without conflicts

- Difficulty: Easy
- [Link](https://neetcode.io/problems/meeting-schedule)

---

### Summary

- Given `intervals`, an array of `interval` that consists of start and end times `[[start, end], ...] (start < end)`, return `true` if there is any overlap in their schedule.

---

### Ideas

- We **don't need to check all the values** between `start` and `end` to determine is there is a conflict.
- If the end time of a session is **bigger** than the start time of the next one, there is an overlap.
- We need to **sort the array** by the start time first.

---

### Solution

```python  
"""
Definition of Interval:
class Interval(object):
    def __init__(self, start, end):
        self.start = start
        self.end = end
"""

class Solution:
    def canAttendMeetings(self, intervals: List[Interval]) -> bool:
        intervals.sort(key = lambda i: i.start)
        for i in range(len(intervals) - 1):
            if intervals[i].end > intervals[i + 1].start:
                return False
        return True
```
- `intervals.sort(key = lambda i: i.start)` sorts the interval by the start time of the intervals using lambda.
- `lambda i: i.start` is a lambda function that returns `i.start` when `i` is given.
- `intervals.sort(key = lambda)` sets the return value of the lambda as its `key`.
- The `for` loop iterates until `i` reaches the second last element of the array since we look up `intervals[i + 1]` in each iteration.
- If the next session's start time is smaller than the current one's end time, return `False`.
---

### Thoughts

- In the first attempt, I used **set**, but its time complexity was too big.
- The time complexity is **`O(nlogn)`** because of the **Timsort** of Python, while the loop's time complexity is **`O(n)`**.
- The space complexity is **`O(1)`** because Python's built-in sort(**Timsort**) is in-place, though it may use **`O(logn)`** auxiliary stack space internally.
- **Lambda function** is useful for more concise code.