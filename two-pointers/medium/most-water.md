## Biggest Water Container

- Difficulty: Medium
- [Link](https://neetcode.io/problems/max-water-container/question)

---

### Summary

- Given an array of integers `heights` with possible bar heights, find two bars to form the biggest water container and return the amount of water it can store.
---

### Ideas

- It's unavoidable to check all the heights in `heights`.
- Need to consider width, the distance between two bars, as well.
- The water height depends on the height of the shorter bar.
- Starting from the both ends to reach the centre can maximize the width of the container.

---

### Solution (`O(n)`)

```python
class Solution:
    def maxArea(self, heights: List[int]) -> int:
        l = 0
        r = len(heights) - 1
        cur_left = heights[l]
        cur_right = heights[r]
        cur_vol = (r - l) * min(heights[l], heights[r])
        while l < r:
            if heights[l] <= heights[r]:
                new_vol = (r - l) * min(heights[l], heights[r])
                if new_vol > cur_vol:
                    cur_vol = new_vol
                    cur_left = heights[l]
                l += 1
            else:
                new_vol = (r - l) * min(heights[l], heights[r])
                if new_vol > cur_vol:
                    cur_vol = new_vol
                    cur_right = heights[r]
                r -= 1
        return cur_vol
```
- `l` and `r` point to the leftmost and rightmost indices.
- In the while loop, it increments `l` if `heights[l]` is shorter than or equal to `heights[r]`.
- If not, it decrements `r`.
- At each step, compute the area `(r - l) * min(heights[l], heights[r])` and update `cur_vol` if it's larger.
- The process is repeated until `l` meets `r`, and it returns `cur_vol`.

### Thoughts
- The time complexity of the solution is **`O(n)`** where `n` is the length of `heights`.
- The space complexity is **`O(1)`** to store the integer variables.
- In a loop, keep it simple: **read** current values, **decide** a next behaviour(`e.g. if-else`), and **update** the state(`e.g. pointer manipulation, push, pop`).
- Avoid moving pointers multiple times inside one iteration.
