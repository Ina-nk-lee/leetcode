## Merge Intervals
- Difficulty: medium
- [Link](https://neetcode.io/problems/merge-intervals/)

---

### Summary
- Given `intervals`, an array of intervals, merge all the overlapping intervals and return the result. The result doesn't need to be sorted.

---

### Ideas
- Using hashmap, we can track the maximum `interval.end` for each `interval.start`.
- Iterating the hashmap, we can merge intervals gradually from the smallest `interval.start` value.

---

### Solution
```python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        mx = max(interval[0] for interval in intervals)
        mp = [-1] * (mx + 1)
        for s, e in intervals:
            mp[s] = max(mp[s], e)
        res = []
        i, l, r = 0, -1, -1
        while i < len(mp):
            if mp[i] != -1:
                if l == -1:
                    l = i
                r = max(r, mp[i])
            if i == r:
                res.append([l, r])
                l = -1
                r = -1
            i += 1
        if l != -1:
            res.append([l, r])
        return res
```
- It creates a hashmap with a size of a maximum `interval.start`, with a initial value of `-1`.
- `mp` is updated so that each key, `interval.start` to have a maximum `interval.end` as a value.
- While iterating `mp`, it merges ovelapping intervals to one interval `[l, r]`.
 - `l` is updated only if there is no merge in progress.
 - Once the iteration reaches `r`, the last value of the current interval, it closes the interval and adds it to `res`.
- `if l != -1` adds the last interval after the iteration.
---

### Thoughts
- The time complexity is **`O(n + m)`** where `n` is the number of intervals in `intervals` and `m` is the maximum value of `interval.start`.
- The space complexity is **`O(n + m)`** because `res` may store up to `O(n)` elements and `mp` may store up to `O(m)` elements..
- A greedy algorithm works by tracking the farthest reachable end for each start value.
- Although the problem allows returning intervals in any order, this approach naturally produces intervals in sorted order by start.
- This approach works without sorting, but it depends on the range of **start values**, so it is less practical when the values are large.
